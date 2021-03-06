---
title: OS の展開のセキュリティとプライバシー
titleSuffix: Configuration Manager
description: Configuration Manager の OS の展開でのセキュリティとプライバシーのベスト プラクティスについて説明します。
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709330"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Configuration Manager の OS の展開でのセキュリティとプライバシー

*適用対象:Configuration Manager (Current Branch)*

この記事には、Configuration Manager での OS 展開機能のセキュリティとプライバシーに関する情報が含まれています。  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a> OS 展開のセキュリティのベスト プラクティス  

Configuration Manager でオペレーティング システムを展開する際、次のセキュリティのベストプラクティスを参考にします。  


### <a name="implement-access-controls-to-protect-bootable-media"></a>アクセス制御を実装して起動可能なメディアを保護する

起動可能なメディアを作成するときは、メディアを保護するためにパスワードを常に割り当てます。 パスワードが割り当てられても、機密情報を含むファイルのみが暗号化され、すべてのファイルを上書きできます。  

メディアに対する物理的アクセスを制御して、攻撃者が暗号化攻撃を使用してクライアント認証証明書を取得することを防ぐことができます。  

改ざんされたコンテンツまたはクライアント ポリシーがクライアントにインストールされないように、コンテンツはハッシュ化されます。また、コンテンツは元のポリシーと共に使用する必要があります。 コンテンツをハッシュ化できなかった場合、あるいはコンテンツとポリシーの一致を確認できなかった場合、クライアントではその起動可能なメディアが使用されません。 コンテンツのみがハッシュ化されます。 ポリシーはハッシュ化されませんが、パスワードを指定すれば、暗号化され、セキュリティで保護されます。 この動作により、攻撃者がポリシーの変更に成功することが一層難しくなります。  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>OS イメージのメディアを作成するとき、セキュリティで保護された場所を使用する

承認されていないユーザーが場所にアクセスできるとき、作成したファイルが改ざんされる可能性があります。 ディスクの空き容量がすべて利用され、メディアの作成に失敗することもあります。  


### <a name="protect-certificate-files"></a>証明書ファイルを保護する 

強力なパスワードで証明書ファイル (.pfx) を保護します。 ファイルをネットワーク上に保存する場合、そのファイルを Configuration Manager にインポートするときにネットワーク チャネルをセキュリティで保護する

起動可能なメディアで使用するクライアント認証証明書のインポートにパスワードが必要であれば、攻撃者から証明書を保護するのにこの構成が役立ちます。  

ネットワークの場所とサイト サーバーの間で SMB 署名または IPsec を使用して、攻撃者が証明書ファイルを改ざんするのを防ぎます。  


### <a name="block-or-revoke-any-compromised-certificates"></a>危害を受けた証明書をブロックするか、取り消す 

クライアント証明書が危害を受けた場合、Configuration Manager からの証明書をブロックします。 PKI 証明書の場合は取り消します。  

起動可能なメディアと PXE ブートを使用して OS を展開するには、プライベート キーの付いたクライアント認証証明書が必要です。 証明書が侵害された場合は、 **[管理]** ワークスペースの **[証明書]** ノードおよび **[セキュリティ]** ノード内の証明書をブロックします。  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>サイト サーバーと SMS プロバイダーの間の通信チャネルをセキュリティで保護する

SMS プロバイダーがサイト サーバーから離れた場所にある場合は、通信チャネルをセキュリティで保護し、ブート イメージを保護します。

ブート イメージを変更するとき、サイト サーバーではないサーバーで SMS プロバイダーが実行されている場合、ブート イメージが攻撃を受けやすくなります。 SMB 署名または IPsec を使用して、これらのコンピューター間のネットワーク チャネルを保護します。  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>セキュリティで保護されたネットワーク セグメントでのみ配布ポイントの PXE クライアント通信を有効にする

クライアントが PXE ブートの要求を送信するとき、その要求に対して有効な PXE 対応の配布ポイントからサービスが提供されることを確認する方法はありません。 このシナリオには次のセキュリティ リスクがあります。  

- PXE 要求に応答する偽の配布ポイントが、クライアントに改ざんされたイメージを送信する。  

- PXE によって使用される TFTP プロトコルに対して攻撃者が中間者攻撃をしかけることがあります。 そのような攻撃者は OS ファイルを利用し、悪意のあるコードを送信する可能性があります。 その攻撃者はまた、偽のクライアントを作成し、配布ポイントに直接、TFTP 要求を行う可能性があります。  

- 攻撃者は悪意のあるクライアントを使用して、配布ポイントにサービス拒否攻撃を仕掛けることもできます。  

徹底的に防御し、PXE が有効な配布ポイントにクライアントがアクセスするネットワーク セグメントを保護します。  

> [!WARNING]  
>  こうしたセキュリティ リスクがあるため、境界ネットワークのような信頼されていないネットワークでは配布ポイントの PXE 通信を有効にしないでください。  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>指定されたネットワーク インターフェイスの PXE 要求のみに応答するように PXE 対応の配布ポイントを構成する  

配布ポイントがすべてのネットワーク インターフェースの PXE 要求に応答するように構成すると、PXE サービスが信頼されないネットワークにさらされる可能性があります。  


### <a name="require-a-password-to-pxe-boot"></a>PXE ブートでパスワードを要求する

PXE ブートでパスワードを要求すると、PXE ブート プロセスのセキュリティが一段高まります。 この構成は、Configuration Manager 階層に入り込んだ偽のクライアントに対する防御策として役立ちます。  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>PXE ブートまたはマルチキャストに使用される OS イメージのコンテンツを制限する

基幹業務アプリケーションや機密データの含まれたソフトウェアを、PXE ブートまたはマルチキャストで使用するイメージに含めないでください。  

PXE ブートやマルチキャストには特有のセキュリティ リスクがあるため、偽のコンピューターが OS システム イメージをダウンロードしたときのリスクを軽減します。  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>タスク シーケンス変数によりインストールされるコンテンツを制限する

基幹業務アプリケーションや機密データの含まれたソフトウェアを、タスク シーケンス変数を使用してインストールするアプリケーション パッケージに含めないでください。  

タスク シーケンス変数を使用してソフトウェアを展開すると、そのソフトウェアの受信が承認されていないコンピューターやユーザーにインストールされる可能性があります。  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>ユーザーの状態を移行するとき、ネットワーク チャネルをセキュリティで保護する

ユーザー状態を移行するとき、SMB 署名または IPsec を使用し、クライアントと状態移行ポイントの間のネットワーク チャネルをセキュリティで保護します。  

最初に HTTP で接続された後、ユーザー状態管理データが SMB を使用して送信されます。 ネットワーク チャネルをセキュリティで保護しないと、攻撃者がこのデータを読み込み、変更する可能性があります。  


### <a name="use-the-latest-version-of-usmt"></a>最新版の USMT を使用する

Configuration Manager がサポートする最新バージョンのユーザー状態移行ツール (USMT) を使用してください。  

USMT の最新バージョンは、セキュリティ上の改善とユーザー状態データを移行する際のよりすぐれた制御を提供します。  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>状態移行ポイントの使用を止めるとき、フォルダーを手動で削除する  

Configuration Manager コンソールで状態移行ポイントのプロパティにある状態移行ポイント フォルダーを削除しても、物理フォルダーは削除されません。 情報の漏洩からユーザー状態移行データを守るため、手動でネットワーク共有とフォルダーを削除してください。  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>ユーザー状態をすぐに削除するように削除ポリシーを構成しない  

状態移行ポイントの削除ポリシーで、削除マークの付いたデータをすぐに削除するように構成した場合、ユーザー状態データを有効なコンピューターが取得する前に攻撃者が取得してしまうと、サイトによってユーザー状態データがすぐに削除されます。 **[次の時期以降に削除する]** 間隔を、ユーザー状態のデータの修復が成功したことを確認するのに十分な長さに設定します。  


### <a name="manually-delete-computer-associations"></a>コンピューターの関連付けを手動で削除する 

ユーザー状態移行データの復元が完了し、確認されたときにコンピューターの関連付けを手動で削除してください。

Configuration Manager によってコンピューターの関連付けが自動的に削除されることはありません。 必要なくなったコンピューターの関連付けを手動で削除することで、ユーザー状態データが特定されるのを防ぎます。  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>状態移行ポイントのユーザー状態移行データを手動でバックアップする  

Configuration Manager バックアップでは、サイト バックアップにユーザー状態移行データが含まれません。  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>アクセス制御を実装して事前設定されたメディアを保護する  

メディアに対する物理的アクセスを制御して、攻撃者が暗号化攻撃を使用してクライアント認証証明書と機密データを取得することを防ぐことができます。  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>アクセス制御を実装して参照コンピューターのイメージ プロセスを保護する  

OS イメージのキャプチャに使用する参照コンピューターが安全な環境にあることを確認してください。 予想外のソフトウェアや悪意のあるソフトウェアがインストールされ、キャプチャしたイメージに不手際で含まれることがないように、適切なアクセス制御を使用してください。 イメージをキャプチャするとき、保存先のネットワークの場所が安全であることを確認します。 このプロセスは、キャプチャ後のイメージ改ざん防止になります。  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>参照コンピューターに最新のセキュリティの更新を常にインストールする  

参照コンピューターのセキュリティが最新に更新されていれば、新しいコンピューターが初めて起動したときに攻撃されるリスクを軽減することができます。  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>不明なコンピューターに OS を展開するとき、アクセス制御を実装する

OS を不明なコンピューターに展開する必要がある場合は、アクセス制御を実装し、承認されていないコンピューターがネットワークに接続できないようにします。  

不明なコンピューターのプロビジョニングは、新しいコンピューターを要望に応じて展開する方法として便利です。 しかしながら、ご利用のネットワーク上で攻撃者が信頼されるクライアントになることを簡単に許す可能性があります。 ネットワークへの物理アクセスを制限し、クライアントを監視して不正なコンピューターを検出します。 

PXE で始動した OS 展開に応答するコンピューターで、このプロセスの間、すべてのデータが破棄されてしまう可能性があります。 この動作の結果、間違って再フォーマットされたシステムが利用できなくなることがあります。  


### <a name="enable-encryption-for-multicast-packages"></a>マルチキャスト パッケージの暗号化を有効にする  

Configuration Manager がマルチキャストを使用してパッケージを送信する場合、各 OS の展開パッケージに対して暗号化を有効にすることができます。 偽のコンピューターがマルチキャスト セッションに入り込むことを阻止するのにこの構成が役立ちます。 攻撃者が転送を改ざんすることも防ぎます。  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>不正なマルチキャスト対応配布ポイントを監視する  

ネットワークへのアクセス権を取得すると、攻撃者は偽のマルチキャスト サーバーを構成して OS の展開を偽装できます。  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>ネットワークの場所にタスク シーケンスをエクスポートする際、その場所とネットワーク チャネルをセキュリティで保護する

ネットワーク フォルダーにアクセスできるユーザーを制限します。  

ネットワークの場所とサイト サーバーの間でSMB 署名または IPsec を使用して、攻撃者がエクスポートしたタスク シーケンスを改ざんするのを防ぎます。  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>タスク シーケンスの実行アカウントを使用する場合、セキュリティ対策を増やす

[タスクシーケンスの実行アカウント](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account)を使用する場合は、次の事前措置を講じます。  

- できるだけアクセス許可が制限されたアカウントを使用します。  

- このアカウントにはネットワーク アクセス アカウントを使用しないでください。  

- このアカウントをドメイン管理者にしない  

- このアカウントにローミング プロファイルを構成しない タスク シーケンスを実行するときにアカウントのローミング プロファイルをダウンロードするので、ローカル コンピューターのプロファイルにアクセスされる危険性があります。  

- アカウントのスコープを制限する たとえば、タスク シーケンスごとに異なるタスク シーケンス実行アカウントを作成します。 1 つのアカウントが侵害された場合、侵害されるのはそのアカウントがアクセスできるクライアント コンピューターだけです。 コマンド ラインにコンピューターの管理アクセスが必要な場合は、タスク シーケンスの実行アカウント専用のローカル管理者アカウントを作成することを検討してください。 タスク シーケンスを実行するすべてのコンピューターでこのローカル アカウントを作成し、不要になったらすぐにアカウントを削除します。  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>OS 展開マネージャーのセキュリティの役割を付与された管理ユーザーを制限し、監視する

**OS 展開マネージャー**のセキュリティの役割を付与された管理ユーザーは、自己署名証明書を作成できます。 作成した自己署名証明書は、クライアントになりすましたり、Configuration Manager からクライアント ポリシーを取得したりする目的で利用されることがあります。  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>拡張 HTTP を使用し、ネットワーク アクセス アカウントの必要性の減らす

バージョン 1806 以降では、[拡張 HTTP](../../core/plan-design/hierarchy/enhanced-http.md) を有効にすると、一部の OS 展開シナリオでは、配布ポイントからコンテンツをダウンロードするためにネットワーク アクセス アカウントを必要としません。 詳細については、「[タスク シーケンスとネットワーク アクセス アカウント](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount)」をご覧ください。<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>OS 展開におけるセキュリティの問題  

OS 展開はネットワーク上のコンピューターにとって最も安全なオペレーティング システムと構成を展開する方法かもしれませんが、次のようなセキュリティ上のリスクがあります。  


### <a name="information-disclosure-and-denial-of-service"></a>情報開示およびサービスの拒否  

Configuration Manager インフラストラクチャの制御が管理者に渡ると、あるゆるタスク シーケンスを実行される可能性があります。 その過程ですべてのクライアント コンピューターのハード ドライブがフォーマットされることもあります。 タスク シーケンスは、ドメインおよびボリュームのライセンス キーに参加する許可が与えられたアカウントなど、機密情報を取得するように構成することができます。  


### <a name="impersonation-and-elevation-of-privileges"></a>偽装および権限の昇格  

タスク シーケンスは、コンピューターをドメインに参加することができます。つまり偽のコンピューターに認証されたネットワーク アクセスを渡してしまう可能性があります。 

起動可能なタスク シーケンス メディアと PXE ブート展開に使用されるクライアント認証証明書を保護してください。 クライアント認証証明書をキャプチャするとき、攻撃者が証明書のプライベート キーを取得する機会がその過程で与えられます。 証明書が手に入ると、ネットワーク上で有効なクライアントになりすますことができます。 このシナリオでは、偽のコンピューターは、機密データを含む可能性があるポリシーをダウンロードできます。  

状態移行ポイントに保存されているデータにアクセスする目的でクライアントによってネットワーク アクセス アカウントが使用される場合、そのようなクライアントでは同じ ID が効果的に共有されます。 ネットワーク アクセス アカウントが使用される別のクライアントから状態移行データにアクセスされることがあります。 元のクライアントのみが読み取ることができるようにデータは暗号化されますが、データが改ざんされたり削除されたりする可能性があります。  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>管理ポイントによって発行される Configuration Manager トークンを使用して、状態移行ポイントに対するクライアント認証を実行できます。  

Configuration Manager によって、状態移行ポイントに格納されているデータの量が制限されたり、管理されたりすることはありません。 攻撃者がディスクの空き容量を占有し、サービス拒否を引き起こすことがあります。  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>コレクション変数を使用すると、ローカルの管理者が潜在的な機密情報を読み取れる  

コレクション変数を使用すると、柔軟にオペレーティング システムを展開できますが、情報が開示される可能性があります。  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a> OS 展開のプライバシー情報  

OS のないコンピューターに OS を展開する以外にも、Configuration Manager を使用してユーザーのファイルと設定をあるコンピューターから別のコンピューターへ移行できます。 管理者は、個人データ ファイル、構成設定、およびブラウザーのクッキーなど、どの情報を転送するか構成します。  

Configuration Manager によって状態移行ポイントに情報が格納され、転送時や保存時に暗号化されます。 状態情報に関連付けられている新しいコンピューターのみが格納されている情報を取得できます。 新規コンピューターが情報を取得するためのキーをなくした場合、コンピューター関連インスタンス オブジェクトの**回復情報の表示**権限を持つ Configuration Manager 管理者は、情報にアクセスして新規コンピューターに関連付けることができます。 新規コンピューターが状態情報を復元すると、コンピューターは既定で 1 日後にデータを削除します。 状態移行ポイントで、削除の印が付いたデータをいつ削除するか構成できます。 Configuration Manager によってサイト データベースに状態移行情報が格納されることはなく、Microsoft に送信されることはありません。  

ブート メディアを使用して OS イメージを展開する場合、ブート メディアをパスワード保護する既定のオプションを必ず使用します。 パスワードは、タスク シーケンス内に格納された変数すべてを暗号化します。しかし、変数内に格納されていない情報は開示される恐れがあります。  

OS 展開では、タスク シーケンスを使用して展開プロセス時にさまざまな異なるタスクを実行できます。タスクには、アプリケーションやソフトウェア更新プログラムのインストールなどが含まれます。 タスク シーケンスを構成する場合、ソフトウェアのインストールに関するプライバシーについても留意する必要があります。  

Configuration Manager では、既定で OS 展開が実装されません。 ユーザー状態情報の収集や、タスク シーケンスまたはブート イメージの作成を実行する前に、いくつかの構成手順を実施する必要があります。  

OS 展開を構成する前に、プライバシー要件について検討してください。  



## <a name="see-also"></a>関連項目

[診断結果と使用状況データ](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Configuration Manager のセキュリティとプライバシー](../../core/plan-design/security/security-and-privacy.md)
