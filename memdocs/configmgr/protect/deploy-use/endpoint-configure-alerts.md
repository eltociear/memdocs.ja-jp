---
title: Endpoint Protection 用のアラートの構成
titleSuffix: Configuration Manager
description: Configuration Manager で Endpoint Protection のアラートを構成する方法について説明します。
ms.date: 03/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: f504de3e-4caf-455c-80d7-a63f13f4c5d9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5b44147006a9ae4d38d2275a4515d71d61eec55c
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074862"
---
#  <a name="configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager での Endpoint Protection 用のアラートの構成

*適用対象:Configuration Manager (Current Branch)*

 Microsoft Configuration Manager で Endpoint Protection アラートを構成して、階層内でのマルウェア感染などの特定のイベントが発生したときに管理ユーザーに通知することができます。 通知は、Configuration Manager コンソールの Endpoint Protection ダッシュボードで、 **[監視]** ワークスペースの **[アラート]** ノードに表示されます。また、指定されたユーザーに電子メールで通知を送信することもできます。

 Configuration Manager で Endpoint Protection 用のアラートを構成するには、このトピックの次の手順と補足手順に従います。

> [!IMPORTANT]
>  Endpoint Protection のアラートを構成するコレクションの **[セキュリティ ポリシーの実施]** アクセス許可が必要です。

## <a name="steps-to-configure-alerts-for-endpoint-protection-in-configuration-manager"></a>Configuration Manager で Endpoint Protection 用のアラートを構成する手順

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** をクリックします。

2.  **[資産とコンプライアンス]** ワークスペースで **[デバイス コレクション]** をクリックします。

3.  **[デバイス コレクション]** 一覧で、アラートを構成するコレクションを選んでから、 **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]** をクリックします。

    > [!NOTE]
    >  ユーザーのコレクションに対してアラートを構成することはできません。

4.  Configuration Manager コンソールの **[監視]** ワークスペースで、このコレクションのマルウェア対策操作について詳細を表示する場合は、 _[<コレクション名\>_ **のプロパティ]** ダイアログ ボックスの **[アラート]** タブで、 **[このコレクションを Endpoint Protection ダッシュボードに表示する]** を選択します。

    > [!NOTE]
    >  このオプションは、 **[すべてのシステム]** コレクションには選択できません。

5.  _[<コレクション名\>_ **のプロパティ]** ダイアログ ボックスの **[アラート]** タブで、 **[追加]** をクリックします。

6.  **[コレクションの新しいアラートの追加]** ダイアログ ボックスの **[Generate an alert when these conditions apply]** (これらの条件を満たす場合にアラートを生成する) セクションで、特定の Endpoint Protection イベントが発生したときに Configuration Manager が生成するアラートを選択してから、 **[OK]** をクリックします。

7.  **[アラート]** タブの **[条件]** 一覧で、Endpoint Protection の各アラートを選択してから、次の情報を指定します。

    -   **アラート名** - 既定の名前を受け入れるか、新しいアラート名を入力します。

    -   **アラートの重要度** - この一覧で、Configuration Manager コンソールに表示されるアラート レベルを選択します。

8.  選択したアラートに応じて、次の追加情報を指定します。

    -   **[マルウェア検出]** - このアラートは、監視するコレクション内のコンピューターでマルウェアが検出されると、生成されます。 **[マルウェア検出のしきい値]** で、このアラートが生成されるマルウェア検出のレベルを指定します。

        -   **[高 - すべて検出]** - Endpoint Protection クライアントが実行する操作に関係なく、指定されたコレクションの 1 台以上のコンピューターでマルウェアが検出されると、アラートが生成されます。

        -   **[中 - 検出、操作を保留中]** - 指定されたコレクションの 1 台以上のコンピューターでマルウェアが検出されると、アラートが生成されます。マルウェアは、手動で削除する必要があります。

        -   **[低 - 検出、操作中]** - 指定されたコレクションの 1 台以上のコンピューターでマルウェアが検出されると、アラートが生成されますが、マルウェアはアクティブなままです。

    -   **[マルウェア大量感染]** - このアラートは、監視するコレクション内の、指定した割合のコンピューターで特定のマルウェアが検出されると、生成されます。

        -   **[マルウェアが検出されたコンピューターの割合]** - コレクション内で、マルウェアが検出されたコンピューターの割合が指定したパーセンテージを超えると、アラートが生成されます。 割合を指定する **1** を通じて **99** です。

            > [!NOTE]
            >  パーセンテージの値は、コレクション内のコンピューターの数に基づきますが、構成マネージャー クライアントがインストールされていないコンピューターは除外されます。 これには Endpoint Protection クライアントがまだインストールされていないコンピューターが含まれます。

    -   **[マルウェア連続検出]** - このアラートは、監視するコレクション内のコンピューターで、指定した時間数にわたって指定した回数を超えて特定のマルウェアが検出されると、生成されます。 次の情報を指定して、このアラートを構成します。

        -   **マルウェアが検出された回数を超える:** -指定した回数よりも詳細のコレクション内のコンピューターで同じマルウェアが検出されたときに、アラートが生成されます。 値を指定して **2** を通じて **32** です。

        -   **[検出期間 (時間)]** 指定したマルウェア検出回数での検出期間を時間で指定します。 **[1]** から **[168]** までの数で指定します。

    -   **[複数のマルウェア検出]** - このアラートは、監視するコレクション内のコンピューターで、指定した時間数にわたって指定した種類の数を超えたマルウェアが検出されると、生成されます。 次の情報を指定して、このアラートを構成します。

        -   **[検出されたマルウェアの種類の数]** コレクション内のコンピューターで、種類の異なるマルウェアが指定した数で検出されると、アラートが生成されます。 値を指定して **2** を通じて **32** です。

        -   **[検出期間 (時間)]** 指定したマルウェア検出回数での検出期間を時間で指定します。 **[1]** から **[168]** までの数で指定します。

9. **[OK]** をクリックして _[<コレクション名\>_ **のプロパティ]** ダイアログ ボックスを閉じます。  

## <a name="alert-for-outdated-malware-client"></a>期限切れのマルウェア クライアントのアラート

Configuration Manager のバージョン 1702 から、Endpoint Protection クライアントが古くならないようにするためのアラートを構成することができます。 任意のデバイス コレクションから、属性**マルウェア対策クライアント バージョン**および**Endpoint Protection の展開状態**の一覧に列を追加できるようになりました。 たとえば、コンソールで **[資産とコンプライアンス]**  >  **[概要]**  >  **[デバイス コレクション]**  >  **[すべてのデスクトップ クライアントおよびサーバー クライアント]** に移動します。 列見出しを右クリックし、追加する列を選択します。 アラートを確認するには、 **[監視]** ワークスペースの **[アラート]** を表示します。 20% を超える管理対象クライアントが期限切れバージョンのマルウェア対策ソフトウェアを実行している場合、"マルウェア対策クライアント バージョンが期限切れです" のアラートが表示されます。 このアラートは、 **[監視]**  >  **[概要]** タブには表示されません。期限切れのマルウェア対策クライアントを更新するには、マルウェア対策クライアントのソフトウェア更新プログラムを有効にします。

アラートを生成するパーセント値を構成するには、 **[監視]**  >  **[アラート]**  >  **[すべてのアラート]** を展開し、 **[期限切れのマルウェア対策クライアント]** をダブルクリックし、 **[管理されたクライアントのうち、期限切れのバージョンのマルウェア対策クライアントを使用しているものが次の割合を超えたら、アラートを生成する]** オプションを変更します。

> [!div class="button"]
> [次のステップ >](endpoint-definition-updates.md)
> 
> [!div class="button"]
> [戻る >](endpoint-protection-site-role.md)
