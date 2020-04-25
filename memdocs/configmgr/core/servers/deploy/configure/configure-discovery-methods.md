---
title: 探索の構成
titleSuffix: Configuration Manager
description: 探索方法を構成して、ネットワーク、Active Directory、および Azure Active Directory から管理するリソースを検索します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3bd03cb15ae1633d8ddfc8c2f26a741d2679b083
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704750"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Configuration Manager の探索方法を構成する

*適用対象:Configuration Manager (Current Branch)*

探索方法を構成して、ネットワーク、Active Directory、および Azure Active Directory (Azure AD) から管理するリソースを検索します。 最初に環境の検索に使用する各方法を有効にしてから構成します。 探索方法は、有効にするのと同じ手順で無効にすることもできます。 このプロセスの唯一の例外は、定期探索とサーバー検出です。  

- 既定では、**定期探索**は、Configuration Manager プライマリ サイトをインストールするときに既に有効になっています。 これは基本スケジュールで実行するために構成されています。 定期探索は有効にしたままにしてください。 定期探索によってデバイスの探索データ レコード (DDR) が確実に最新の状態になります。 定期探索の詳細については、「[定期探索について](about-discovery-methods.md#bkmk_aboutHeartbeat)」を参照してください。  

- **サーバー検出**は自動検出方法です。 サイト システムとして使用しているコンピューターを検索します。 構成も無効化も実行できません。  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Active Directory フォレストの探索  

Active Directory フォレストの探索の構成を完了するには、Configuration Manager コンソール次の 2 つの場所で設定を構成します。  

- **[探索方法]** ノードで、次の操作を行います。

  - 探索方法を有効にします。  

  - ポーリングのスケジュールを設定します。  

  - 探索対象の Active Directory サイトとサブネットの境界を自動的に作成するかどうかを選択します。  

- **[Active Directory フォレスト]** ノードで、次の操作を行います。

  - 探索するフォレストを追加します。  

  - そのフォレストでの Active Directory サイトとサブネットの探索を有効にします。  

  - Configuration Manager サイトがサイト情報をフォレストに発行できるようにする設定を構成します。  

  - 各フォレストで Active Directory フォレスト アカウントとして使用するアカウントを割り当てます。  

Active Directory フォレストの探索を有効にし、Active Directory フォレストの探索で使用する個々のフォレストを構成するには、次の手順に従います。  

### <a name="configure-active-directory-forest-discovery"></a>Active Directory フォレストの探索の構成  

1. Configuration Manager コンソールで **[管理]** ワークスペースに移動し、 **[階層の構成]** を展開して、 **[探索方法]** ノードを選択します。  

2. 探索を構成するサイトの Active Directory フォレストの探索方法を選択します。  

3. リボンの **[ホーム]** タブで、 **[プロパティ]** を選択します。  

4. プロパティの **[全般]** タブで、次の設定を構成します。  

    - 探索方法を有効にします。

    - 探索する場所に対してサイト境界を作成するオプションを指定します。  

    - 探索を実行するスケジュールを指定します。  

5. **[OK]** を選択して構成を保存します。  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Active Directory フォレストの探索のフォレストを構成する  

1. **[管理]** ワークスペースで、 **[階層の構成]** を展開し、 **[Active Directory フォレスト]** ノードを選択します。 Active Directory フォレストの検索を前に実行している場合は、検出されたフォレストが結果ウィンドウに表示されます。 この探索方法を実行すると、ローカル フォレストと信頼されているフォレストが検出されます。 信頼されていないフォレストを手動で追加します。  

    - 既に検出済みのフォレストを構成するには、結果ウィンドウでそのフォレストを選択します。 リボンで、 **[プロパティ]** を選択して、フォレストのプロパティを開きます。

    - 一覧に示されていない新しいフォレストを構成するには、リボンの **[ホーム]** タブの **[作成]** グループで、 **[フォレストの追加]** を選択します。 この操作で、 **[フォレストの追加]** ダイアログ ボックスが開かれます。

2. **[全般]** タブで、探索するフォレストの構成を完了し、 **[Active Directory フォレスト アカウント]** を指定します。 このアカウントの詳細については、[アカウント](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account)に関するページを参照してください。  

    > [!NOTE]  
    > Active Directory フォレストの探索で、信頼されていないフォレストを検出して、そのフォレストに発行するにはグローバル アカウントが必要です。 サイト サーバーのコンピューター アカウントを使用しない場合は、グローバル アカウントのみ選択できます。  

3. サイト データをこのフォレストに発行できるようにする場合は、 **[発行]** タブで、必要な構成を行います。  

    > [!NOTE]  
    > サイトをフォレストに発行できるようにする場合は、Configuration Manager 用にそのフォレストの Active Directory スキーマを拡張します。 Active Directory フォレスト アカウントには、そのフォレストの System コンテナーに対するフル コントロールのアクセス許可が必要です。  

4. **[OK]** を選択して構成を保存します。  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> コンピューター、ユーザー、またはグループの Active Directory 探索  

コンピューター、ユーザー、またはグループの探索を構成するには、次に示す一般的な手順から開始します。

1. Configuration Manager コンソールで **[管理]** ワークスペースに移動し、 **[階層の構成]** を展開して、 **[探索方法]** ノードを選択します。  

2. 探索を構成するサイトの探索方法を選択します。  

3. リボンの **[ホーム]** タブで、 **[プロパティ]** を選択します。  

4. プロパティの **[全般]** タブで、探索を有効にするチェック ボックスをオンにします。 先に探索を構成し、後で探索を有効にすることもできます。  

特定の探索方法を構成するには、以下のセクションの情報を参照してください。  

- [Active Directory グループの探索](#bkmk_config-adgd)  

- [Active Directory システムの探索](#bkmk_config-adgd)  

- [Active Directory ユーザー検出](#bkmk_config-adud)  

> [!NOTE]  
> このセクションの情報は、Active Directory フォレストの探索には当てはまりません。  

これらの各探索方法は相互に独立していますが、同様のオプションを使用します。 これらの構成オプションに関する詳細については、「[Shared options for Group, System, and User discovery](about-discovery-methods.md#bkmk_shared)」(グループ、システム、ユーザー探索の共有オプション) を参照してください。  

> [!WARNING]  
> これらの各探索方法での Active Directory ポーリングで、大量のネットワーク トラフィックが発生する可能性があります。 このネットワーク トラフィックが業務上のネットワークの使用に悪影響を及ぼさない時間帯に各探索が実行されるように、探索のスケジュールを設定する必要があります。  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a> Active Directory グループの探索の構成  

1. Active Directory グループ探索の [プロパティ] ウィンドウの **[全般]** タブで、 **[追加]** を選択して探索のスコープを構成します。 **[グループ]** または **[場所]** のいずれかを選択します。 次に、 **[グループの追加]** または **[Active Directory の場所の追加]** ダイアログ ボックスで次の構成を完了します。  

    1. この探索スコープの **[名前]** を指定します。  

    2. **[Active Directory ドメイン]** または **[場所]** を指定して検索します。  

        - **[グループ]** を選択した場合、探索する 1 つまたは複数の Active Directory グループを指定します。  

        - **[場所]** を選択した場合、探索する場所として Active Directory コンテナーを指定します。 この場所に対して Active Directory の子コンテナーの再帰検索を有効にすることもできます。  

    3. この探索スコープを検索するためにサイトで使用する **[Active Directory グループ探索アカウント]** を指定します。 詳細については、[アカウント](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account)に関するページを参照してください。  

    4. **[OK]** を選択して探索スコープの構成を保存します。  

2. 定義する追加の探索スコープごとに、上記の手順を繰り返します。  

3. **[ポーリングのスケジュール]** タブで、完全な探索ポーリングのスケジュールと差分探索の両方を構成します。

4. **[オプション]** タブで、探索から古いコンピューターのレコードをフィルタリングして取り除く、つまり除外するように設定を構成します。 また、配布グループのメンバーシップの探索も構成します。  

    > [!NOTE]  
    > 既定では、Active Directory グループの探索では、セキュリティ グループのメンバーシップのみ探索されます。  

5. **[OK]** を選択して構成を保存します。  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a> Active Directory システムの探索を構成する  

1. Active Directory システム探索の [プロパティ] ウィンドウの **[全般]** タブで、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択して、新しい Active Directory コンテナーを指定します。 **[Active Directory コンテナー]** ダイアログ ボックスで、次の構成を完了します。  

    1. **パス**への場所を入力するか、または参照します。 この値は、コンテナーまたは組織単位 (OU) に対する有効な LDAP パスです。 サイトでは、リソースのためにこのパスを照会します。 たとえば、 `LDAP://CN=Computers,DC=contoso,DC=com` と記述します。  

    2. 検索動作を変更するオプションを指定します。  

        - **[Active Directory グループ内でオブジェクトを探索する]** :サイトでは、このパスにあるグループのメンバーシップも確認します。  

        - **[Active Directory の子コンテナーを反復検索する]** :このオプションを有効にした場合、サイトは上記のパス内で追加のコンテナーや OU を検索します。 このオプションを無効にした場合、サイトは特定のパスにあるリソースのみを検索します。  

          バージョン 1806 以降では、この反復検索から除外するサブコンテナーを選択します。 このオプションは、検出されるオブジェクトの数を絞り込むのに役立ちます。 **[追加]** を選択して、上記のパスにあるコンテナーを選択します。 [新しいコンテナーの選択] ダイアログ ボックスで、除外する子コンテナーを選択します。 **[OK]** を選択し、[新しいコンテナーの選択] ダイアログ ボックスを閉じます。<!--1358143-->

          > [!Tip]  
          > Active Directory システム探索の [プロパティ] ウィンドウにある Active Directory コンテナーの一覧には、 **[Has Exclusions]** \(除外する\) 列が含まれています。 除外するコンテナーを選択した場合、この値は **[はい]** になります。  

    3. 場所ごとに、 **[Active Directory 探索アカウント]** として使用するアカウントを指定します。 詳細については、[アカウント](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account)に関するページを参照してください。  

        > [!TIP]  
        > 指定した場所ごとに、探索オプションのセットおよび一意の Active Directory 探索アカウントを構成できます。  

    4. **[OK]** を選択して Active Directory コンテナーの構成を保存します。  

2. **[ポーリングのスケジュール]** タブで、完全な探索ポーリングのスケジュールと差分探索の両方を構成します。  

3. **[Active Directory の属性]** タブで、探索するコンピューターの追加の Active Directory 属性を構成します。 このタブには、既定のオブジェクト属性が表示されます。  

    > [!Tip]  
    > たとえば、組織が Active Directory のコンピューター アカウントの **Description** 属性を使用します。 **[カスタム]** を選択し、カスタム属性として `Description` を追加します。 この探索方法の実行後、この属性は、Configuration Manager コンソールでデバイスの [プロパティ] タブに表示されます。<!--513948-->  

4. **[オプション]** タブで、探索から古いコンピューターのレコードをフィルタリングして取り除く、つまり除外するように設定を構成します。  

5. **[OK]** を選択して構成を保存します。  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a> Active Directory ユーザーの探索を構成する  

1. Active Directory ユーザー探索の [プロパティ] ウィンドウの **[全般]** タブで、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択して、新しい Active Directory コンテナーを指定します。 **[Active Directory コンテナー]** ダイアログ ボックスで、次の構成を完了します。  

    1. 検索する 1 つまたは複数の場所を指定します。  

    2. 場所ごとに、検索動作を変更するオプションを指定します。  

    3. 場所ごとに、 **[Active Directory 探索アカウント]** として使用するアカウントを指定します。 詳細については、[アカウント](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account)に関するページを参照してください。  

        > [!NOTE]  
        > 指定した場所ごとに、探索オプションの一意のセットおよび一意の Active Directory 探索アカウントを構成できます。  

    4. **[OK]** を選択して Active Directory コンテナーの構成を保存します。  

2. **[ポーリングのスケジュール]** タブで、完全な探索ポーリングのスケジュールと差分探索の両方を構成します。  

3. **[Active Directory の属性]** タブで、探索するコンピューターの追加の Active Directory 属性を構成します。 このタブには、既定のオブジェクト属性が表示されます。  

4. **[OK]** を選択して構成を保存します。  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a>Azure AD ユーザー探索

Azure AD ユーザー探索は、他の探索方法と同じように、有効にしたり構成することはできません。 Configuration Manager サイトを Azure AD にオンボードする際に構成します。

詳細については、「[Azure AD ユーザー探索](about-discovery-methods.md#azureaddisc)」を参照してください。

### <a name="prerequisites"></a>[前提条件]

この探索方法を有効にして構成するには、**クラウド管理**用に [Azure サービスを構成](azure-services-wizard.md)します。

Configuration Manager を使用して Azure アプリを*作成*する場合、Configuration Manager は、必要なアクセス許可を使用してアプリを構成します。

最初に Azure でアプリを作成し、それを Configuration Manager に*インポート*する場合は、手動でアプリを構成する必要があります。 この構成には、サーバー アプリがディレクトリ データを読み取るためのアクセス許可の付与が含まれます。

1. *グローバル管理者*のアクセス許可を持つユーザーとして [Azure portal](https://portal.azure.com) を開きます。 **[Azure Active Directory]** に移動して、 **[アプリの登録]** を選択します。 必要に応じて、 **[すべてのアプリケーション]** に切り替えます。

1. ターゲット アプリケーションを選択します。

1. **[管理]** メニューで、 **[API のアクセス許可]** を選択します。  

    1. **[API のアクセス許可]** パネルで、 **[アクセス許可の追加]** を選択します。  

    2. **[API アクセス許可の要求]** パネルで、 **[所属する組織で使用している API]** に切り替えます。  

    3. **Microsoft Graph** API を検索して選択します。  

        > [!Tip]
        > バージョン 1810 以前では、**Azure Active Directory Graph** API を使用します。

    4. **[アプリケーションのアクセス許可]** グループを選択します。 **[ディレクトリ]** を展開して、 **[Directory.Read.All]** を選択します。  

    5. **[アクセス許可の追加]** を選択します。  

1. **[API のアクセス許可]** パネルの **[同意の付与]** セクションで、 **[管理者の同意の付与]** を選択します。 **[はい]** を選択します。  

### <a name="configure-azure-ad-user-discovery"></a>Azure AD ユーザー探索を構成する

**クラウド管理** Azure サービスを構成する場合は、次の手順を実行します。

- ウィザードの **[検出]** ページで、 **[Azure Active Directory ユーザーの探索を有効にする]** オプションをクリックします。
- **[設定]** を選択します。
- [Azure AD ユーザー探索設定] ダイアログ ボックスで、検出を実行するスケジュールを設定します。 Azure AD の新規または変更されたアカウントのみをチェックする差分探索を有効にすることもできます。

> [!Note]  
> ユーザーがフェデレーション ID または同期 ID である場合、Azure AD ユーザー探索だけでなく、Configuration Manager の [Active Directory ユーザー探索](about-discovery-methods.md#bkmk_aboutUser)を使用する必要があります。 ハイブリッド ID の詳細については、「[ハイブリッド ID 導入戦略の定義](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)」を参照してください。<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a> Azure AD ユーザー グループの探索

<!--3611956-->
> [!Tip]  
> この機能はバージョン 1906 で[プレリリース機能](../../manage/pre-release-features.md)として初めて導入されました。 バージョン 2002 以降、プレリリース機能ではなくなりました。  

Azure AD からユーザー グループとそのグループのメンバーを検出できます。 Azure AD グループ内で以前検出されなかったユーザーがサイトで検出されると、Configuration Manager でそれらのユーザーが新しいユーザー リソースとして追加されます。 グループがセキュリティ グループのとき、ユーザー グループ リソース レコードが作成されます。

### <a name="prerequisites"></a>[前提条件]

- クラウド管理 [Azure サービス](azure-services-wizard.md)
- Azure AD グループを読み取り、検索するアクセス許可

### <a name="limitations"></a>制限事項

Azure AD ユーザー グループの探索の差分探索は現在、無効になっています。

### <a name="log-files"></a>ログ ファイル

トラブルシューティングには、SMS_AZUREAD_DISCOVERY_AGENT.log を使用します。 このログは、Azure AD ユーザー探索とも共有されます。 詳細については、[ログ ファイル](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs)に関するページを参照してください。

### <a name="enable-azure-ad-user-group-discovery"></a>Azure AD ユーザー グループ探索を有効にする

既存の**クラウド管理** Azure サービスで探索を有効にするには、次の操作を行います。

1. **[管理]** ワークスペースに移動し、 **[クラウド サービス]** を展開して、 **[Azure サービス]** ノードを選択します。
1. いずれかの Azure サービスを選択し、リボンで **[プロパティ]** を選択します。
1. **[探索]** タブで、 **[Azure Active Directory グループの探索を有効にする]** のチェックボックスをオンにし、 **[設定]** を選択します。
1. **[探索スコープ]** タブにある **[追加]** を選択します。
    - 他のタブで **[ポーリングのスケジュール]** を変更できます。
1. 1 つまたは複数のユーザー グループを選択します。 名前で**検索**したり、**セキュリティ グループのみ**を表示するかどうか選択したりできます。
    - **[検索]** を初めて選択すると、Azure にサインインするように求められます。
1. グループの選択が完了したら、 **[OK]** を選択します。
1. 探索が終わったら、 **[ユーザー]** ノードで Azure AD ユーザー グループを参照できます。

新しい **クラウド管理** Azure サービスを有効にするには、次の操作を行います。

- ウィザードの **[検出]** ページで、 **[Azure Active Directory グループの探索を有効にする]** オプションを選択します。
- **[設定]** を選択します。
- [Azure AD ユーザー探索設定] ダイアログ ボックスで、探索スコープと探索を実行するスケジュールを設定します。


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> 定期探索

プライマリ サイトをインストールすると、Configuration Manager は定期探索を有効にします。 7 日おきの既定のスケジュールを使用する場合は、他の構成作業は必要ありません。 既定のスケジュールを使用しない場合は、クライアントが管理ポイントに定期探索データ レコードを送信する頻度のスケジュールを構成する作業だけが必要になります。  

> [!NOTE]  
> 同じサイトで、クライアント プッシュ インストールおよび **[インストール フラグのクリア]** のサイト メンテナンス タスクの両方が有効な場合、定期探索のスケジュールを、 **[インストール フラグのクリア]** サイト メンテナンス タスクの **[クライアント再探索期間]** より小さく設定します。 サイトのメンテナンス タスクの詳細については、[メンテナンス タスク](../../manage/maintenance-tasks.md)に関するページを参照してください。  

### <a name="configure-the-heartbeat-discovery-schedule"></a>定期探索スケジュールを構成する  

1. Configuration Manager コンソールで **[管理]** ワークスペースに移動し、 **[階層の構成]** を展開して、 **[探索方法]** ノードを選択します。  

2. 定期探索を構成するサイトの **[定期探索]** を選択します。  

3. リボンの **[ホーム]** タブで、 **[プロパティ]** を選択します。  

4. クライアントが定期探索データ レコードを送信する頻度を構成します。 次に、 **[OK]** を選択して構成を保存します。  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> ネットワーク探索  

ネットワーク探索を構成する前に、次のトピックについて把握しておきます。  

- 利用可能なレベルのネットワーク探索  

- 利用できるネットワーク探索オプション  

- ネットワークにおけるネットワーク探索の制限  

詳細については、「[ネットワーク探索について](about-discovery-methods.md#bkmk_aboutNetwork)」を参照してください。  

以下のセクションでは、ネットワーク探索の一般的な構成について説明します。 同じ探索を実行するときに使用するように、これらの構成の 1 つまたは複数を構成できます。 複数の構成を使用する場合、探索結果に影響する可能性がある処理を計画します。  

たとえば、特定の SNMP コミュニティ名を使用するすべての簡易ネットワーク管理プロトコル (SNMP) デバイスを探索します。 同じ探索を実行する際に、特定のサブネットでの探索を無効にします。 探索の実行時に、ネットワーク探索では、無効になっているサブネットで指定のコミュニティ名を持つ SNMP デバイスは探索されません。  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> ネットワーク トポロジの確認  

トポロジのみの探索を使用してネットワークをマップできます。 この種の探索では、存在する可能性があるクライアントは探索されません。 トポロジのみのネットワーク探索では、SNMP が使用されます。  

ネットワーク トポロジをマップする場合、 **[ネットワーク探索のプロパティ]** ダイアログ ボックスの **[SNMP]** タブで、 **[最大ホップ数]** を構成します。 わずか数ホップで、探索の実行時に使用されるネットワーク帯域幅を制御できます。 探索するネットワークが増えるにつれて、ホップ数を増やすと、ネットワーク トポロジへの理解が深まります。  

ネットワーク トポロジを理解した後は、ネットワーク探索の追加のプロパティを構成します。 これらのプロパティは、潜在的なクライアントとオペレーティング システムを検出するのに役立ちます。 また、検索できるネットワーク セグメントを制限するように、ネットワーク探索を構成します。  

詳細については、「[ネットワーク トポロジの決定方法](#bkmk_proc-top)」を参照してください。

### <a name="network-discovery-search-options"></a>ネットワーク探索の検索オプション

Configuration Manager では、ネットワークを検索する次の方法をサポートします。

- [ サブネットを使用した検索の制限](#BKMK_LimitBySubnet)
- [ 特定のドメインの検索](#BKMK_SearchByDomain)
- [ SNMP コミュニティ名を使用した検索の制限](#BKMK_LimitBySNMPname)
- [ 特定の DHCP サーバーの検索](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> サブネットを使用した検索の制限  

探索の実行中に特定のサブネットを検索するように、ネットワーク探索を構成できます。 既定では、ネットワーク探索では、探索を実行しているサーバーのサブネットが検索されます。 構成して有効にした追加のサブネットは、SNMP 検索オプションおよび DHCP 検索オプションにのみ適用されます。 ネットワーク探索でドメインを検索する場合、サブネットの構成によって検索が制限されることはありません。  

**[ネットワーク探索のプロパティ]** ダイアログ ボックスの **[サブネット]** タブで、1 つまたは複数のサブネットを指定する場合、 **[有効]** とマークされているサブネットのみが検索されます。  

サブネットを無効にすると、サイトはそのサブネットを探索から除外し、次の条件が適用されます。  

- SNMP ベースのクエリは、そのサブネットで実行されません。  

- DHCP サーバーは、そのサブネットに配置されたリソースの一覧では応答しません。  

- ドメイン ベースのクエリで、そのサブネットに配置されたリソースを探索できます。  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> 特定のドメインの検索  

探索の実行中に特定ドメインまたはドメインのセットを検索するように、ネットワーク探索を構成できます。 既定では、ネットワーク探索では、探索を実行しているサーバーのローカル ドメインが検索されます。  

**[ネットワーク探索のプロパティ]** ダイアログ ボックスの **[ドメイン]** タブで、1 つまたは複数のドメインを指定する場合、 **[有効]** とマークされているドメインのみが検索されます。  

ドメインを無効にすると、サイトはそのドメインを探索から除外し、次の条件が適用されます。  

- ネットワーク探索で、そのドメイン内のドメイン コントローラーは照会されません。  

- SNMP ベースのクエリは、そのドメイン内のサブネットで引き続き実行できます。  

- DHCP サーバーは、そのドメイン内に配置されたリソースの一覧で引き続き応答できます。  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> SNMP コミュニティ名を使用した検索の制限  

探索の実行中に特定の SNMP コミュニティまたはコミュニティのセットを検索するように、ネットワーク探索を構成できます。 既定では、メソッドは **public** というコミュニティ名を構成します。  

ネットワーク探索は、コミュニティ名を使用して、SNMP デバイスになっているルーターへのアクセスを取得します。 ルーターは、最初のルーターにリンクされている他のルーターやサブネットに関する情報をネットワーク探索に提供できます。  

> [!NOTE]  
> SNMP コミュニティ名は、パスワードのようなものです。 ネットワーク探索では、コミュニティ名を指定された SNMP デバイスからのみ情報を取得できます。 各 SNMP デバイスは独自のコミュニティ名を持つことができますが、多くの場合は複数のデバイスで同じコミュニティ名が共有されます。 また、ほとんどの SNMP デバイスは、既定の **public** というコミュニティ名を使用します。 ただし、セキュリティ上の理由から、デバイスから **public** というコミュニティ名を削除している組織もあります。  

**[ネットワーク探索のプロパティ]** ダイアログ ボックスの **[SNMP]** タブに複数の SNMP コミュニティが含まれる場合、表示されている順序で検索を行います。 最もよく使用される名前が、常に一覧の最上位に配置されています。 この構成によって、別の名前を使用してデバイスへの接続を試行した場合に、サイトが生成するネットワーク トラフィックを最小限に抑えることができます。

> [!NOTE]  
> SNMP コミュニティ名を使用できるだけでなく、特定の SNMP デバイスの IP アドレスまたは解決可能な名前も指定できます。 このアクションは、 **[ネットワーク探索のプロパティ]** ダイアログ ボックスの **[SNMP デバイス]** タブで行います。  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> 特定の DHCP サーバーの検索  

特定の DHCP サーバーまたは複数のサーバーを使用して探索の実行中に DHCP クライアントを探索するように、ネットワーク探索を構成できます。  

ネットワーク探索は、 **[ネットワーク探索のプロパティ]** ダイアログ ボックスの **[DHCP]** タブで指定する各 DHCP サーバーを検索します。 探索を実行しているサーバーが DHCP サーバーから IP アドレスをリースしている場合は、その DHCP サーバーを検索するように探索を構成できます。 **[Include the DHCP server that the site server is configured to use]** \(サイトのサーバーで使用するように構成された DHCP サーバーを含める\) オプションを使用して、この動作を有効にします。  

> [!NOTE]  
> ネットワーク探索時に使用する DHCP サーバーを構成するには、環境で IPv4 をサポートしている必要があります。 ネイティブの IPv6 環境で、ネットワーク探索時に使用する DHCP サーバーを構成することはできません。  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> ネットワーク探索の構成方法  

次の手順に従って、まずネットワーク トポロジのみ探索します。次に、1 つまたは複数の使用可能なネットワーク探索オプションを使用して、存在する可能性があるクライアントを探索するようにネットワーク探索を構成します。  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a> ネットワーク トポロジの決定方法  

1. Configuration Manager コンソールで **[管理]** ワークスペースに移動し、 **[階層の構成]** を展開して、 **[探索方法]** ノードを選択します。  

2. ネットワーク リソースを探索するサイトの **[ネットワーク探索]** 方法を選択します。  

3. リボンの **[ホーム]** タブで、 **[プロパティ]** を選択します。  

    - **[全般]** タブで、 **[ネットワーク探索を有効にする]** オプションを選択します。 次に、 **[探索の種類]** オプションから **[トポロジ]** を選択します。  

    - **[サブネット]** タブで、 **[ローカル サブネットを探索]** オプションを選択します。  

      > [!TIP]  
      > ネットワークを構成している特定のサブネットがわかっている場合は、 **[ローカル サブネットを検索する]** チェック ボックスをオフにします。 次に、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択して、検索する特定のサブネットを追加します。 大規模なネットワークの場合、サブネットを一度に 1 つまたは 2 つだけ検索して、ネットワーク帯域幅の使用を最小限に抑えます。  

    - **[ドメイン]** タブで、 **[ローカル ドメインを検索]** オプションを選択します。  

    - **[SNMP]** タブで、 **[最大ホップ数]** ドロップダウン リストから 1 つのオプションを選択します。 このオプションでは、トポロジのマッピングでネットワーク探索が利用できるルーター ホップ数を指定します。  

      > [!TIP]  
      > ネットワーク トポロジの初回マップ時には、ネットワーク帯域幅の使用を最小限に抑えるため、ごくわずかな数のルーター ホップを構成します。  

4. **[スケジュール]** タブで、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択して、探索の実行スケジュールを設定します。  

    > [!NOTE]  
    > 複数の探索構成を、ネットワーク探索のスケジュールを分けるように割り当てることはできません。 ネットワーク探索の実行時は毎回、現在の探索構成が使用されます。  

5. **[OK]** を選択して、構成を受け入れます。 ネットワーク探索が、スケジュールされた時刻に実行されます。  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a> ネットワーク探索の構成方法  

1. Configuration Manager コンソールで **[管理]** ワークスペースに移動し、 **[階層の構成]** を展開して、 **[探索方法]** ノードを選択します。  

2. ネットワーク リソースを探索するサイトの **[ネットワーク探索]** 方法を選択します。  

3. リボンの **[ホーム]** タブで、 **[プロパティ]** を選択します。  

4. **[全般]** タブで、 **[ネットワーク探索を有効にする]** オプションを選択します。  

    - **[探索の種類]** オプションから、実行する探索の種類を選択します。  

    - Configuration Manager が低帯域幅のネットワークに対して自動調整を行うように、 **[低速のネットワーク]** オプションを有効にします。  

5. サブネットを検索するように探索を構成するには、 **[サブネット]** タブに切り替えます。次に、以下のオプションのうち、1 つまたは複数を構成します。  

    - 探索を実行するコンピューターのローカルのサブネットで探索を実行するには、 **[ローカル サブネットを検索する]** オプションを有効にします。  

    - 特定のサブネットを検索するには、サブネットが **[検索するサブネット]** に表示され、 **[検索]** の値が **[有効]** になっていることを確認します。  

      1. サブネットが一覧に表示されていない場合、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択します。 **[新しいサブネットの割り当て]** ダイアログ ボックスに、 **[サブネット]** と **[マスク]** の情報を入力して、 **[OK]** を選択します。 既定では、新しいサブネットの検索が有効になります。  

      2. 一覧に示されたサブネットの **[検索]** の値を変更するには、一覧から該当の値を選択します。 次に、 **[切り替え]** アイコンを選択して、 **[無効]** と **[有効]** のいずれかに値を切り替えます。  

6. ドメインを検索するように探索を構成するには、 **[ドメイン]** タブに切り替えます。次に、以下のオプションのうち、1 つまたは複数を構成します。  

    - 探索を実行するコンピューターのドメイン上で探索を実行するには、 **[ローカル ドメインを検索する]** オプションを有効にします。  

    - 特定のドメインを検索するには、ドメインが **[ドメイン]** に表示され、 **[検索]** の値が **[有効]** になっていることを確認します。  

      1. ドメインが一覧に表示されていない場合、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択します。 **[ドメインのプロパティ]** ダイアログ ボックスで、**ドメイン**の情報を入力し、 **[OK]** を選択します。 既定では、新しいドメインの検索が有効になります。  

      2. 一覧に示されたドメインの **[検索]** の値を変更するには、一覧から該当の値を選択します。 次に、 **[切り替え]** アイコンを選択して、 **[無効]** と **[有効]** のいずれかに値を切り替えます。  

7. SNMP デバイスの特定の SNMP コミュニティ名を検索するように探索を構成するには、 **[SNMP]** タブに切り替えます。次に、以下のオプションのうち、1 つまたは複数を構成します。  

    - **[SNMP コミュニティ名]** の一覧に SNMP コミュニティ名を追加するには、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択します。 検索するコミュニティの名前を **[新しい SNMP コミュニティ名]** ダイアログ ボックスで、SNMP コミュニティの**名前**を指定し、 **[OK]** を選択します。  

    - SNMP コミュニティ名を削除するには、コミュニティ名を選択して、 **[削除]** アイコン ![[削除] アイコン](media/Disc_delete_Icon.gif) をクリックします。  

    - SNMP コミュニティ名の検索順序を調整するには、一覧からコミュニティ名を選択します。 次に、 **[Move Item Up]** \(項目を上へ移動\) アイコン ![項目を上へ移動アイコン](media/Disc_moveUp_Icon.gif) または **[Move Item Down]** \(項目を下へ移動\) アイコン ![項目を下へ移動アイコン](media/Disc_moveDown_Icon.gif) を選択します。 探索の実行時に、上から下の順番でコミュニティ名が検索されます。 

    - SNMP 検索で使用するルーター ホップの最大数を構成するには、 **[最大ホップ数]** ドロップダウン リストからホップの数を選択します。  

8. SNMP デバイスを構成するには、 **[SNMP デバイス]** タブに切り替えます。デバイスが一覧に表示されていない場合、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択します。 **[新しい SNMP デバイス]** ダイアログ ボックスで、SNMP デバイスの IP アドレスまたはデバイス名を指定し、 **[OK]** を選択します。  

    > [!NOTE]  
    > デバイス名を指定する場合、Configuration Manager が NetBIOS 名を IP アドレスに解決できる必要があります。  

9. 特定の DHCP サーバーを照会するように探索を構成するには、 **[DHCP]** タブに切り替えます。次に、以下のオプションのうち、1 つまたは複数を構成します。  

    - 探索を実行しているコンピューターで DHCP サーバーを照会するには、 **[サイト サーバーの DHCP サーバーを常に使用する]** オプションを有効にします。  

      > [!NOTE]  
      > このオプションを使用するには、サーバーが DHCP サーバーから IP アドレスをリースしている必要があります。また、静的 IP アドレスは使用できません。  

    - 特定の DHCP サーバーを照会するには、 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択します。 **[新しい DHCP サーバー]** ダイアログ ボックスで DHCP サーバーの IP アドレスまたはサーバー名を指定し、 **[OK]** を選択します。  

      > [!NOTE]  
      > サーバー名を指定する場合、Configuration Manager が NetBIOS 名を IP アドレスに解決できる必要があります。  

10. 探索の実行タイミングを構成するには、 **[スケジュール]** タブに切り替えます。 **[新規]** アイコン ![新規アイコン](media/Disc_new_Icon.gif) を選択して、ネットワーク探索の実行スケジュールを設定します。 複数の定期スケジュールや、繰り返しパターンのない複数のスケジュールなど、さまざまなスケジュールを構成できます。  

    > [!NOTE]  
    > **[スケジュール]** タブに複数のスケジュールが同時に表示される場合、スケジュールに示されている時刻に構成されているとおりに、すべてのスケジュールでネットワーク探索が実行されます。 この動作は定期スケジュールにも当てはまります。  

11. **[OK]** を選択して構成を保存します。  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> ネットワーク探索の終了を確認する方法  

ネットワーク検索が完了するのに必要な時間は、次の 1 つ以上の要因によって異なります。  

- ネットワークの規模  

- ネットワークのトポロジー  

- ネットワーク上のルーターを検出するように構成されているホップの最大数  

- 実行される探索の種類  

ネットワーク探索では、終了時に、終了を通知するメッセージは作成されません。 次の手順を使用して、探索がいつ終了したかを確認します。  

1. Configuration Manager コンソールで、 **[監視]** ワークスペースに移動します。 **[システム ステータス]** を展開して、 **[ステータス メッセージ クエリ]** ノードを選択します。  

2. **[すべてのステータス メッセージ]** クエリを選択します。  

3. リボンの **[ホーム]** タブの **[ステータス メッセージ クエリ]** グループで、 **[メッセージを表示する]** を選択します。  

4. [すべてのステータス メッセージ] ウィンドウで、 **[日時の選択]** ドロップダウン リストから、探索が開始された時点を含む値を選択します。 次に、 **[OK]** を選択して、 **[Configuration Manager ステータス メッセージ ビューアー]** を開きます。  

    > [!TIP]  
    > **[日時の選択]** オプションを使用して、探索を実行した日時を指定することもできます。 このオプションは、指定した日にネットワーク探索を実行し、その日のメッセージのみを取得したい場合に便利です。  

5. ネットワーク探索が終了したことを確認するには、次の情報が含まれたステータス メッセージを検索します。  

    - メッセージ ID: **502**  

    - コンポーネント: **SMS_NETWORK_DISCOVERY**  

    - 説明 :**このコンポーネントは停止しました。**  

    このステータス メッセージが表示されない場合は、ネットワーク探索は終了していません。  

6. ネットワーク探索が開始したことを確認するには、次の情報が含まれたステータス メッセージを検索します。  

    - メッセージ ID: **500**  

    - コンポーネント: **SMS_NETWORK_DISCOVERY**  

    - 説明 :**このコンポーネントが開始しました。**  

    この情報は、ネットワーク探索が開始したことを確認するものです。 この情報が表示されない場合は、ネットワーク探索のスケジュールを変更します。  