---
title: Windows 10 の構成項目を作成する
titleSuffix: Configuration Manager
description: Windows 10 構成アイテムを使用して、構成マネージャー クライアントで管理されている Windows 10 コンピューターの設定を管理します。
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9a1bda440ab3ccd02432f0b023a134b9f54cdafb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692540"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Windows 10 デバイスの構成項目を作成する

Configuration Manager の **Windows 10** 構成アイテムを使用して、構成マネージャー クライアントで管理されている Windows 10 コンピューターの設定を管理します。  
  
> [!IMPORTANT]  
>  このリリースでは、(構成マネージャー クライアントで管理されているデバイスのために) **Windows 10** タイプの構成項目の一部として**パスワード**設定を作成した場合、次の問題に注意してください。 この設定がまだ存在しない場合、または Windows 10 デバイスで構成されていない場合でも、準拠として誤って評価されます。  
>   
>  この問題を回避するには、これらのデバイスの設定を作成するときに、構成項目の作成ウィザードの設定ページで、必ず **[対応していない設定を修復する]** を選択します。 さらに、パスワードの設定を含む Windows 10 構成アイテムが含まれる構成基準を展開するときに、 **[サポートされている場合は対応していない規則を修復する]** を選択します。 [構成基準の展開] ダイアログ ボックスで、この選択を行います。 この回避策を使用すると、設定が監視され、非対応であることが検出された場合は修復されます。 修復後、設定は **[対応]** として適切にレポートされます (問題が発生していない場合。問題が発生した場合は、 **[エラー]** としてレポートされます)。  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Windows 10 構成項目を作成するには  
  
1. Configuration Manager コンソールで、 **[資産とコンプライアンス]** を選択します。  
  
2. **[資産とコンプライアンス]** ワークスペースで **[コンプライアンス設定]** を展開してから、 **[構成アイテム]** を選択します。  
  
3. **[ホーム]** タブの **[作成]** グループで、 **[構成アイテムの作成]** を選択します。  
  
4. **[構成アイテムの作成]** ウィザードの **[全般]** ページで、構成アイテムの名前と、必要に応じて説明を入力します。  
  
5. **[作成する構成項目の種類の指定]** で、 **[Windows 10]** を選択します。  
  
6. Configuration Manager コンソールで構成アイテムを検索およびフィルター処理するためにカテゴリを作成して割り当てる場合、 **[カテゴリ]** を選択します。  
  
7. ウィザードの **[サポートされているプラットフォーム]** ページで、構成項目を評価する特定の Windows 10 プラットフォームを選択します。  
  
8. ウィザードの **[デバイスの設定]** ページで、構成する設定グループを選択します。 (詳細については、この記事の「[Windows 10 の構成項目設定のリファレンス](#BKMK_Ref)」をご覧ださい。)その後、 **[次へ]** を選択します。  
  
   > [!TIP]  
   >  必要な設定が表示されていない場合は、 **[既定の設定グループに含まれない追加の設定を構成する]** を選択します。  
  
9. 各設定ページで、必要な設定と、その設定がデバイスに対応していないときにその設定を修正するかどうかを構成します (これがサポートされている場合)。  
  
10. 設定グループごとに、構成アイテムが非対応であることが検出されたときに報告される重要度を構成することもできます。  
  
    -   **なし**: このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に非対応重要度を何も報告しません。  
  
    -   **情報**: このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に**情報**というレベルで非準拠重要度を報告します。  
  
    -   **警告**: このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に**警告**というレベルで非準拠重要度を報告します。  
  
    -   **重大**: このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に**重大**というレベルで非準拠重要度を報告します。  
  
    -   **重大 (イベント)** : このコンプライアンス規則を満たしていないデバイスは、Configuration Manager レポート用に**重大**というレベルで非準拠重要度を報告します。 重要度のレベルは、アプリケーションのイベント ログでも Windows のイベントとしてログが登録されます。  
  
11. ウィザードの **[プラットフォームの適用性]** ページで、前に選択したサポート対象プラットフォームと互換性がないすべての設定を確認します。 前に戻ってこれらの設定を削除するか、操作を続行できます。  
  
    > [!TIP]  
    >  サポートされていない設定のコンプライアンスは評価されません。  
  
12. ウィザードを完了します。  
  
    新しい構成項目は、 **[資産とコンプライアンス]** ワークスペースの **[構成項目]** ノードに表示されます。  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>パスワード  
  
|設定|詳細|  
|-------------|-------------|  
|**デバイスのパスワードの設定が必要**|サポート対象デバイスのパスワードが必要です。|  
|**パスワードの最小文字数**|パスワードの最小文字数。|  
|**パスワードの有効期限 (日数)**|パスワードの変更が必要になるまでの日数。|  
|**記憶するパスワードの数**|以前のパスワードを再利用できないようにします。|  
|**デバイスをワイプするまでのログオン失敗回数**|サインインがこの回数だけ失敗した場合は、デバイスがワイプされます。|  
|**デバイスをロックするまでのアイドル時間**|デバイスが自動的にロックされるまでに非アクティブにしておく必要がある時間 (分) を指定します。|  
|**パスワードの複雑さ**|'1234' などの PIN を指定できるのか、または強力なパスワードを指定する必要があるのかを選択します。|
|**パスワードに必要な複雑な文字セットの数**|**強力な**パスワードを選択した場合、この設定を使用して、複雑な文字セットの必要な数を構成します。 強力なパスワードの場合は、この設定を少なくとも **3** (つまり、文字と数字の両方が必要) に設定する必要があります。 さらに **(%$** などの特殊文字を必要とするパスワードを要求する場合は、**4** を選択します。<br>(Windows 10 のみ)  |
  
###  <a name="device"></a>デバイス  
  
|設定の名前|詳細|  
|------------------|-------------|  
|**Bluetooth**|デバイスの Bluetooth 機能を使用できるようにします。|  
  
### <a name="cloud"></a>クラウド  
  
|設定の名前|詳細|  
|------------------|-------------|  
|**設定の同期**|デバイス間で設定を同期できるようにします。|  
|**資格情報の同期**|デバイス間で資格情報を同期できるようにします。|  
|**従量制課金接続での設定の同期**|インターネット接続が従量制課金の場合に、設定を同期できるようにします。|  
  
### <a name="roaming"></a>ローミング  
  
|設定の名前|詳細|  
|------------------|-------------|  
|**データ ローミング**|データへのアクセス中にネットワーク間のローミングを許可します。|  
  
### <a name="encryption"></a>暗号化  
  
|設定の名前|詳細|  
|------------------|-------------|  
|**デバイスのファイルの暗号化**|デバイス上のファイルを必ず暗号化するようにします。|  
  
### <a name="system-security"></a>システム セキュリティ  
  
|設定の名前|詳細|  
|------------------|-------------|  
|**ユーザー アカウント コントロール**|デバイスの Windows ユーザー アカウント制御を構成します。<br />たとえば、ユーザー アカウント制御を無効にしたり、その通知レベルを設定したりできます。|  
|**ネットワーク ファイアウォール**|Windows ファイアウォールを有効または無効にします。|  
|**スマート スクリーン**|Windows スマート スクリーンを有効または無効にします。|  
|**ウイルス対策**|ウイルス対策ソフトウェアをインストールして、構成する必要があります。|  
|**ウイルス対策署名は最新です**|デバイス上のウイルス対策ソフトウェアの署名ファイルは、最新の状態にしておく必要があります。|  
  
### <a name="windows-information-protection"></a>Windows Information Protection

企業内で従業員が所有するデバイスが増加すると、メール、ソーシャル メディア、パブリック クラウドなどのアプリやサービスを介して誤ってデータが漏えいするリスクも増大します。 これらは組織の制御の範囲外です。 たとえば、従業員が以下を行う場合です。

- 個人用の電子メール アカウントから最新のエンジニアリング画像を送信する。
- 製品情報をコピーしてツイートに貼り付ける。
- 作成中の営業レポートをパブリック クラウド ストレージに保存する。

Windows Information Protection (WIP、旧称エンタープライズ データ保護) を使うと、この潜在的なデータ漏えいを防止することができ、それ以外の場合に従業員のエクスペリエンスが妨げられることはありません。 また、WIP によって、企業が所有するデバイスや従業員が職場に持ち込む個人用デバイス上での誤ったデータ漏えいから、企業のアプリとデータを保護することもできます。 WIP では、環境や他のアプリを変更する必要はありません。

Configuration Manager の Windows 情報保護構成項目では、以下が管理されます。

- WIP によって保護されるアプリの一覧
- エンタープライズ ネットワークの場所
- 保護レベル
- 暗号化の設定
  
Configuration Manager で WIP を構成する方法については、以下をご覧ください。

- [Windows 情報保護 (WIP) を使用したエンタープライズ データの保護](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Configuration Manager を使用した Windows 情報保護 (WIP) ポリシーの作成と展開](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Windows 情報保護 (WIP) 使用時の制限](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>関連項目  
[Configuration Manager クライアントを使用して管理されているデバイスの構成項目](../../compliance/deploy-use/create-configuration-items.md)
