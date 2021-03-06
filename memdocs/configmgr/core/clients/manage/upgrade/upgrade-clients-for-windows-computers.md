---
title: Windows でクライアントをアップグレードする
titleSuffix: Configuration Manager
description: Configuration Manager 内で Windows コンピューター上のクライアントをアップグレードします。
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 6143fd47-48ec-4bca-b53b-5b9b9f067bc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8b0a69b07a3be633434203f93b0724cec4ea88a3
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347145"
---
# <a name="how-to-upgrade-clients-for-windows-computers-in-configuration-manager"></a>Configuration Manager 内で Windows コンピューターのクライアントをアップグレードする方法

*適用対象:Configuration Manager (Current Branch)*

クライアント インストール方法または自動クライアント アップグレード機能を使用して、Windows コンピューター上の Configuration Manager クライアントをアップグレードします。 次のクライアント インストール方法は、Windows コンピューター上のクライアント ソフトウェアをアップグレードする有効な方法です。  

- グループ ポリシーによるインストール  

- ログオン スクリプトによるインストール  

- 手動インストール  

- アップグレード インストール  

詳しくは、「[Windows コンピューターにクライアントを展開する方法](../../deploy/deploy-clients-to-windows-computers.md)」をご覧ください。

除外コレクションを指定することにより、クライアントをアップグレードから除外します。 詳しくは、[クライアントをアップグレードから除外する方法](exclude-clients-windows.md)に関する記事をご覧ください。 除外されたクライアントでも CCMSETUP をダウンロードして実行することはできますが、アップグレードされません。

> [!TIP]  
> サーバー インフラストラクチャを以前のバージョンの Configuration Manager からアップグレードする場合は、Configuration Manager クライアントをアップグレードする前に、サーバーのアップグレードを完了してください。 このプロセスには、Current Branch のすべての更新プログラムのインストールが含まれます。 Current Branch の最新の更新プログラムには、最新バージョンのクライアントが含まれています。 Configuration Manager のすべての更新プログラムをインストールした後に、クライアントをアップグレードします。

> [!NOTE]
> アップグレード中にクライアントのサイトを再割り当てする予定の場合は、`SMSSITECODE` client.msi プロパティを使用して新しいサイトを指定します。 `SMSSITECODE` に `AUTO` の 値を使用する場合は、`SITEREASSIGN=TRUE` も指定します。 このプロパティを使用すると、アップグレード中にサイトの自動再割り当てを行うことができます。 詳しくは、[クライアント インストールのプロパティ - SMSSITECODE](../../deploy/about-client-installation-properties.md#smssitecode) に関するページをご覧ください。

## <a name="about-automatic-client-upgrade"></a><a name="bkmk_autoupdate"></a> 自動クライアント アップグレードについて

クライアントを最新の Configuration Manager バージョンに自動的にアップグレードするようにサイトを構成します。 割り当てられたクライアントのバージョンが階層のバージョンよりも前であることが Configuration Manager によって識別された場合、クライアントは自動的にアップグレードされます。 このシナリオには、クライアントを Configuration Manager サイトに割り当てるときの最新バージョンへのアップグレードも含まれます。  

クライアントは、次の場合に自動的にアップグレードできます。  

- クライアント バージョンが、階層内で使用されているバージョンよりも前のバージョンである。  

- 中央管理サイト (CAS) 上のクライアントに言語パックがインストールされており、既存のクライアントにはインストールされていない。  

- 階層内のクライアントの前提条件のバージョンが、クライアントにインストールされている前提条件とは異なっている  

- クライアント インストール ファイルのバージョンが異なっている  

> [!NOTE]  
> 階層内の異なるバージョンの Configuration Manager クライアントを識別するには、レポート フォルダー **Site - Client Information** 内の **[Configuration Manager クライアント バージョン別の数]** レポートを使用します。  

既定では、Configuration Manager によってアップグレード パッケージが作成されます。 これにより、パッケージが階層内のすべての配布ポイントに自動的に送信されます。 CAS 上のクライアント パッケージに変更を加えると、Configuration Manager によってパッケージが自動的に更新され、再配布されます。 変更の例としては、クライアント言語パックを追加する場合があります。 自動クライアント アップグレードを有効にすると、すべてのクライアントに新しいクライアント言語パッケージが自動的にインストールされます。

階層全体の自動クライアント アップグレードを有効にしてください。 この構成では、より少ない作業量でクライアントを最新の状態に保つことができます。  

Configuration Manager サイト システムもクライアントとして管理する場合は、それらを自動アップグレード プロセスの一部として含めるかどうかを決定します。 すべてのサーバーを除外することも、クライアントのアップグレードから特定のコレクションを除外することもできます。 一部の Configuration Manager サイトの役割は、クライアント フレームワークを共有します。 たとえば、管理ポイントやプル配布ポイントです。 これらの役割はサイトの更新時にアップグレードされるので、これらのサーバー上のクライアント バージョンが同時に更新されます。

## <a name="configure-automatic-client-upgrade"></a><a name="bkmk_configure"></a> 自動クライアント アップグレードを構成する

次の手順を使用して、CAS で自動クライアント アップグレードを構成します。 この構成は、階層内のすべてのクライアントに適用されます。  

1. Configuration Manager コンソールで、 **[管理]** ワークスペースに移動し、 **[サイトの構成]** を展開してから **[サイト]** ノードを選択します。  

1. リボンの **[ホーム]** タブの **[サイト]** グループで、 **[階層設定]** を選択します。  

1. **[クライアント アップグレード]** タブに切り替えます。実稼働クライアントのバージョンと日付を確認します。 これが、クライアントのアップグレードに使用するバージョンであることを確認します。 目的のクライアント バージョンでない場合は、実稼働前環境クライアントを実稼働環境に昇格させることが必要になることがあります。 詳細については、「[System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストする方法](test-client-upgrades.md)」を参照してください。  

1. **[実稼働クライアントを使用して階層内のすべてのクライアントをアップグレードする]** を選択します。 **[OK]** をクリックして確定します。  

1. クライアントのアップグレードをサーバーに適用しない場合は、 **[サーバーをアップグレードしない]** を選択します。  

1. 何日以内にデバイスでクライアントをアップグレードする必要があるかを指定します。 デバイスによってポリシーが受け取られると、この日数内のランダムな間隔でクライアントがアップグレードされます。 この動作により、多数のクライアントが同時にアップグレードされるのを防ぐことができます。

    > [!NOTE]
    > クライアントをアップグレードするコンピューターが実行されている必要があります。 アップグレードを受信するようにスケジュールされている時刻にコンピューターが実行されていない場合、アップグレードは発生しません。 コンピューターの電源をオンにしてポリシーを受け取ると、許可されている日数内の任意の時点にアップグレードがスケジュールされます。 アップグレードが可能な日数の期限が切れた後にこの状況が発生する場合は、コンピューターの電源オンの後 24 時間以内の任意の時点にアップグレードが行われるようにスケジュールされます。
    >
    > この動作のために、定期的にシャットダウンされるコンピューターは、ランダムにスケジュールされたアップグレード時間が通常の業務時間内ではない場合、アップグレードされるまでに予想以上に時間がかかることがあります。

1. クライアントをアップグレードから除外するには、 **[指定したクライアントをアップグレードから除外する]** を選択し、除外するコレクションを指定します。 詳しくは、[アップグレードからのクライアントの除外](exclude-clients-windows.md)に関する記事をご覧ください。

1. サイトで、**事前設定されたコンテンツ**が有効になっている配布ポイントにクライアント インストール パッケージをコピーする場合は、[[事前設定されたコンテンツ用に有効になっている配布ポイントにクライアント インストール パッケージを自動配布する]](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent) のオプションを選択します。  

1. **[OK]** を選択して設定を保存し、[階層設定のプロパティ] を閉じます。

次回クライアントでポリシーをダウンロードしたときに、これらの設定が受信されます。

> [!NOTE]
> Configuration Manager のメンテナンス期間を構成している場合、クライアントのアップグレードではそれが優先されます。 execmgr スレッドは、メンテナンス期間中にのみクライアント セットアップ ブートストラップ プログラム (ccmsetup.exe) を実行します。 デバイスが書き込みフィルターがある Windows エディションを実行する場合、ccmsetup はダウンロードとインストールを同時に試行します。 それ以外の場合は、ccmsetup はコンテンツのダウンロードをランダムな時間に実行します。 コンテンツをダウンロードし、ローカル ポリシーをコンパイルしたら、execmgr は、次回のメンテナンス期間中にクライアントのアップグレードをスケジュールします。<!-- SCCMDocs#896 -->

## <a name="next-steps"></a>次のステップ

クライアントをアップグレードする別の方法については、[Windows コンピューターにクライアントを展開する方法](../../deploy/deploy-clients-to-windows-computers.md)に関する記事をご覧ください。

特定のクライアントを自動アップグレードから除外します。 詳しくは、[クライアントをアップグレードから除外する方法](exclude-clients-windows.md)に関する記事をご覧ください。
