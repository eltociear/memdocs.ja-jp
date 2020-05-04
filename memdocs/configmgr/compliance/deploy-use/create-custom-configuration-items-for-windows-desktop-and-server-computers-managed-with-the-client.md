---
title: カスタム構成項目の作成
titleSuffix: Configuration Manager
description: Windows デスクトップおよびサーバーのカスタム構成アイテムを使って、Windows コンピューターおよびサーバーの設定を管理します
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63f11066918854d72af0f1160d7d7569a93d7ebe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692520"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>構成マネージャー クライアントを使って管理されている Windows デスクトップおよびサーバー コンピューター向けのカスタム構成アイテムを作成します

*適用対象:Configuration Manager (Current Branch)*


Configuration Manager **カスタム Windows デスクトップおよびサーバー**の構成アイテムを使って、Configuration Manager クライアントで管理されている Windows コンピューターおよびサーバーの設定を管理します。  



## <a name="start-the-wizard"></a>ウィザードの開始

1. Configuration Manager コンソールで **[資産とコンプライアンス]** ワークスペースに移動し、 **[コンプライアンス設定]** を展開して、 **[構成アイテム]** ノードを選択します。  

2. リボンの **[ホーム]** タブの **[作成]** グループで、 **[構成項目の作成]** を選択します。  

3. **構成項目の作成ウィザード** の **[全般]** ページで、構成項目の名前と、必要に応じて説明を入力します。  

4. **[作成する構成項目の種類の指定]** で、 **[Windows デスクトップおよびサーバー (カスタム)]** を選択します。  

    > [!TIP]  
    > アプリケーションの有無を確認する検出方法の設定を指定するには、 **[この構成ファイルにアプリケーションの設定が含まれる]** を選択します。  

5. Configuration Manager コンソールで構成アイテムを検索およびフィルター処理する場合、 **[カテゴリ]** を選択してカテゴリの作成と割り当てを行うと役立ちます。  



## <a name="detection-methods"></a>検出方法  

構成項目の検出方法に関する情報を指定するには、次の手順に従います。  

> [!NOTE]  
> この情報が適用されるのは、ウィザードの **[全般]** ページで **[この構成項目にアプリケーション設定を含める]** を選択した場合のみです。  

Configuration Manager における検出方法には、アプリケーションがコンピューターにインストールされているかどうかを検出するために使用される規則が含まれます。 この検出は、クライアントが構成項目のコンプライアンスを評価する前に発生します。 アプリケーションがインストールされているかどうかを検出するため、そのアプリケーションの Windows インストーラー ファイルの存在を検出します。または、 **[常にアプリケーションがインストールされていると仮定する]** を選択して、アプリケーションがインストールされているかどうかに関係なく、コンプライアンスに関する構成項目の評価が行われるようにします。  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Windows インストーラー ファイルを使用してアプリケーションのインストールを検出するには  

1. **[構成項目の作成ウィザード]** の **[検出方法]** ページで、 **[Windows インストーラーの検出を使用する]** オプションを選択します。  

2. **[開く]** を選択して、検出する Windows インストーラー (.msi) ファイルを参照してから、 **[開く]** を選択します。  

3. **[バージョン]** フィールドには、Windows インストーラー ファイルのバージョン番号が自動的に入力されます。 表示された値が正しくない場合は、ここで新しいバージョン番号を入力します。  

4. コンピューター上のユーザー プロファイルごとに検出を実行する場合は、 **[このアプリケーションは 1 人以上のユーザー用にインストールする]** を選択します。  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>特定のアプリケーションおよび展開の種類を検出するには  

1. **[構成項目の作成ウィザード]** の **[検出方法]** ページで、 **[特定のアプリケーションと展開の種類を検出する]** を選択します。 **[選択]** を選択します。   

2. **[アプリケーションの指定]** ダイアログ ボックスで、検出するアプリケーションおよび関連付けられている展開の種類を選択します。  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>カスタム スクリプトを使用してアプリケーションのインストールを検出するには  

1. **[構成項目の作成ウィザード]** の **[検出方法]** ページで、 **[カスタム スクリプトを使用してこのアプリケーションを検出する]** オプションを選択します。  

2. 一覧で、スクリプトの言語を選択します。 次の形式から選択します。  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > バージョン 1810 以降では、Windows PowerShell スクリプトを検出方法として実行すると、構成マネージャー クライアントにより `-NoProfile` パラメーターを使用して PowerShell が呼び出されます。 このオプションでは、プロファイルなしで PowerShell が起動されます。 PowerShell プロファイルは、PowerShell の開始時に実行されるスクリプトです。 <!--3607762-->  

3. **[開く]** を選択して、使用するスクリプトを参照してから、 **[開く]** を選択します。  



## <a name="specify-supported-platforms"></a>サポートされているプラットフォームの指定  

**[構成項目の作成ウィザード]** の **[サポートされているプラットフォーム]** ページで、構成アイテムのコンプライアンスを評価したい Windows バージョンを選択するか、 **[すべて選択]** を選択します。

**[Windows のバージョンを手動で指定する]** こともできます。 **[追加]** を選択し、Windows ビルド番号の各部分を指定します。

> [!NOTE]
> Windows Server 2016 を指定する場合、`All Windows Server 2016 and higher 64-bit)` の選択には Windows Server 2019 も含まれます。 Windows Server 2016 のみを指定するには、**Windows のバージョンを手動で指定する**ためのオプションを使用します。 <!--5866480-->



##  <a name="configure-settings"></a>設定の構成  

構成項目の設定を構成するには、次の手順に従います。  

設定は、クライアント デバイスでコンプライアンス対応の評価に使用されるビジネス条件または技術条件を表わします。 新しい設定を構成することも、参照コンピューターの既存の設定を参照することもできます。  

1. **[構成項目の作成ウィザード]** の **[設定]** ページで、 **[新規]** を選択します。  

2. **[設定の作成]** ダイアログ ボックスの **[全般]** タブで、次の情報を指定します。  

    - **名前**:設定の一意の名前を入力します。 最大 256 文字を使用できます。  

    - **説明**:設定の説明を入力します。 最大 256 文字を使用できます。  

    - **[設定の種類]** :一覧で、この設定を使用する次の設定の種類のいずれかを選択して、構成します。  
        - [Active Directory クエリ](#bkmk_adquery)
        - [アセンブリ](#bkmk_assembly)
        - [ファイル システム](#bkmk_file)
        - [IIS メタベース](#bkmk_iis)
        - [レジストリ キー](#bkmk_regkey)
        - [レジストリ値](#bkmk_regval)
        - [スクリプト](#bkmk_script)
        - [SQL クエリ](#bkmk_sql)
        - [WQL クエリ](#bkmk_wql)
        - [XPath クエリ](#bkmk_xpath)

    - **[データ型]** :設定の評価に使用する前に、条件の戻り値となるデータの形式を選択します。 **[データの種類]** の一覧は、設定の種類によっては表示されません。  

        > [!Tip]  
        > **[浮動小数点]** データの種類は、小数点第 3 位までをサポートしています。  

3. **[設定の種類]** 一覧の下でこの設定についての追加情報を構成します。 構成できる項目は、選択した設定の種類によって異なります。  

4. **[OK]** を選択して設定を保存し、 **[設定の作成]** ダイアログ ボックスを閉じます。  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a> Active Directory クエリ

- **LDAP プレフィックス**:クライアント コンピューター上でコンプライアンスを評価するための Active Directory Domain Services クエリの有効なプレフィックスを指定します。 グローバル カタログ検索を実行するには、`LDAP://` または `GC://` を使用します。  

- **識別名 (DN)** :クライアント コンピューター上でコンプライアンスを評価する Active Directory Domain Services オブジェクトの識別名を指定します。  

- **検索フィルター**:クライアント コンピューターで対応を評価するための Active Directory Domain Services クエリの結果を絞り込む、オプションの LDAP フィルターを指定します。 クエリからすべての結果を返すには、「`(objectclass=*)`」と入力します。  

- **検索範囲**:Active Directory Domain Services の検索範囲を指定します  

    - **ベース**:指定したオブジェクトのみを対象としてクエリを実行します  

    - **1 つのレベル**:このバージョンの Configuration Manager では使用されないオプションです  

    - **サブツリー**:指定したオブジェクトと、ディレクトリ内のその完全なサブツリーに対してクエリを実行します  

- **プロパティ**: クライアント コンピューター上でコンプライアンスを評価するために使用する Active Directory Domain Services オブジェクトのプロパティを指定します。  

    たとえば、ユーザーが誤ったパスワードを入力した回数を格納する Active Directory プロパティに対してクエリを実行するには、このフィールドに「`badPwdCount`」と入力します。  

- **クエリ**: **[LDAP プレフィックス]** 、 **[識別名 (DN)]** 、 **[検索フィルター]** (指定した場合)、 **[プロパティ]** のエントリから構成された LDAP クエリを表示します。  


### <a name="assembly"></a><a name="bkmk_assembly"></a> アセンブリ

アセンブリは、アプリケーション間で共有可能なコードの断片です。 アセンブリのファイル拡張子は .dll または .exe です。 グローバル アセンブリ キャッシュは、クライアント コンピューター上のフォルダー `%SystemRoot%\Assembly` です。 このキャッシュは、Windows によってすべての共有アセンブリが格納される場所です。  

- **アセンブリ名:** 検索対象のアセンブリ オブジェクトの名前を指定します。 名前は、同じ種類の他のアセンブリ オブジェクトと同じにすることはできません。 最初にそれを、グローバル アセンブリ キャッシュに登録します。 アセンブリ名は 256 文字以内で指定します。  


### <a name="file-system"></a><a name="bkmk_file"></a> ファイル システム

- **種類**:一覧で、 **[ファイル ]** と **[フォルダー]** のどちらを検索するかを選択します。  

- **パス**:指定したファイルまたはフォルダーのクライアント コンピューター上のパスを指定します。 パスには、システム環境変数と `%USERPROFILE%` 環境変数を指定できます。  

    > [!NOTE]  
    > **[パス]** ボックスまたは **[ファイル名またはフォルダー名]** ボックスで `%USERPROFILE%` 環境変数を使用する場合、Configuration Manager クライアントによって、クライアント コンピューター上のすべてのユーザー プロファイルが検索されます。 この動作によって、複数インスタンスのファイルやフォルダーが見つかる結果になる可能性があります。  
    >   
    > 指定されたパスに対するアクセス権がコンプライアンス設定に含まれていない場合、検出エラーが発生します。 また、検索対象のファイルが使用中である場合も、検出エラーが発生します。  

    > [!Tip]  
    > 参照コンピューターの値から設定を構成するには、 **[参照]** を選択します。   

- **ファイル名またはフォルダー名**:検索対象のファイルまたはフォルダー オブジェクトの名前を指定します。 ファイル名またはフォルダー名には、システム環境変数と `%USERPROFILE%` 環境変数を指定できます。 ファイル名には、ワイルドカードとして `*` と `?` を使用できます。  

    > [!NOTE]  
    > ファイル名またはフォルダー名を指定してワイルドカードを使用すると、この組み合わせにより多数の結果が返されることがあります。 また、これによりクライアント コンピューターのリソース使用率が高くなり、Configuration Manager に結果をレポートするときにネットワーク トラフィックが増える場合もあります。  

- **サブフォルダーも含める**:指定したパスの下にあるすべてのサブフォルダーも検索します。  

- **このファイルまたはフォルダーは 64 ビット アプリケーションに関連付けられている**:有効になっている場合、64 ビット コンピューター上の `%ProgramFiles%` など、64 ビット ファイルがある場所のみを検索します。 このオプションが有効になっていない場合は、64 ビットの場所と 32 ビットの場所 (`%ProgramFiles(x86)%` など) の両方を検索します。  

    > [!NOTE]  
    > 同じ 64 ビット コンピューターで 32 ビット システム ファイルの場所と 64 ビット システム ファイルの場所に同じファイルまたはフォルダーが存在する場合、グローバル条件では複数のファイルが検出されます。  

    **[ファイル システム]** の設定の種類では、 **[パス]** ボックスにネットワーク共有への UNC パスを指定することはできません。  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a> IIS メタベース

- **メタベース パス**:インターネット インフォメーション サービス (IIS) メタベースへの有効なパスを指定します。 たとえば、`/LM/W3SVC/` となります。  

- **プロパティ ID**:IIS メタベース設定の数値プロパティを指定します。  


### <a name="registry-key"></a><a name="bkmk_regkey"></a> レジストリ キー

- **ハイブ**:検索対象のレジストリ ハイブを選択します

    > [!Tip]  
    > 参照コンピューターの値から設定を構成するには、 **[参照]** を選択します。 リモート コンピューターのレジストリ キーを参照するには、リモート コンピューターで**リモート レジストリ** サービスを有効にします。  

- **キー**:検索対象のレジストリ キーの名前を指定します。 「`key\subkey`」の形式を使用します。  

- **このレジストリ キーを 64 ビット アプリケーションに関連付ける**:64 ビット バージョンの Windows を稼働しているクライアント上で、32 ビット レジストリ キーだけでなく 64 ビット レジストリ キーも検索します。  

    > [!NOTE]  
    > 64 ビット コンピューターの 64 ビット および 32 ビット システム ファイルの場所に同じレジストリ キーが存在する場合は、グローバル条件によって両方のレジストリ キーが検知されます。  


### <a name="registry-value"></a><a name="bkmk_regval"></a> レジストリ値

- **ハイブ**:検索するレジストリ ハイブを選択します。  

    > [!Tip]  
    > 参照コンピューターの値から設定を構成するには、 **[参照]** を選択します。 リモート コンピューターのレジストリ値を参照するには、リモート コンピューターで**リモート レジストリ** サービスを有効にします。 リモート コンピューターにアクセスするには、管理者のアクセス許可も必要です。  

- **キー**:検索するレジストリ キーの名前を指定します。 「`key\subkey`」の形式を使用します。  

- **値**:指定されたレジストリ キーに含まれている必要がある値を指定します。  

- **このレジストリ キーを 64 ビット アプリケーションに関連付ける**:64 ビット バージョンの Windows を稼働しているクライアント上で、32 ビット レジストリ キーだけでなく 64 ビット レジストリ キーも検索します。  

    > [!NOTE]  
    > 64 ビット コンピューターの 64 ビット および 32 ビット システム ファイルの場所に同じレジストリ キーが存在する場合は、グローバル条件によって両方のレジストリ キーが検知されます。  


### <a name="script"></a><a name="bkmk_script"></a> スクリプト

スクリプトによって返された値は、グローバル条件のコンプライアンスを評価するのに使用されます。 たとえば、VBScript を使用している場合、コマンド **[WScript.Echo Result]** を使用して、 *Result* 変数値をグローバル条件に返すことができます。  

- **探索スクリプト**: **[スクリプトの追加]** を選択し、スクリプトを入力または参照します。 このスクリプトは、値を見つけるために使用されます。 Windows PowerShell、VBScript、または Microsoft JScript のスクリプトが使用できます。  

- **修復スクリプト (オプション)** : **[スクリプトの追加]** を選択し、スクリプトを入力または参照します。 このスクリプトは、準拠していない設定値を修復するために使用されます。 Windows PowerShell、VBScript、または Microsoft JScript のスクリプトが使用できます。  

- **ログオンしたユーザーの資格情報を使用してスクリプトを実行する**:このオプションを有効にすると、サインインしているユーザーの資格情報を使って、クライアント コンピューター上でスクリプトが実行されます。  

> [!Note]  
> バージョン 1810 以降では、Windows PowerShell スクリプトを検出用または修復用のスクリプトとして実行すると、`-NoProfile` パラメーターを使用して、Configuration Manager クライアントによって PowerShell が呼び出されます。 このオプションでは、プロファイルなしで PowerShell が起動されます。 PowerShell プロファイルは、PowerShell の開始時に実行されるスクリプトです。 <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a> SQL クエリ

- **SQL Server インスタンス**:既定のインスタンス、すべてのインスタンス、または特定のデータベースのインスタンス名のどれで SQL クエリを実行するかを選択します。  

    > [!NOTE]  
    > インスタンス名は、SQL Server のローカル インスタンスを参照する必要があります。 クラスター化された SQL Server インスタンスを参照するには、スクリプト設定を使用する必要があります。  

- **データベース**: SQL クエリを実行する対象となる Microsoft SQL Server データベースの名前を指定します。  

- **列**: グローバル条件のコンプライアンス評価に使用される Transact-SQL ステートメントによって返される列名を指定します。  

- **Transact-SQL ステートメント**:グローバル条件で使用する完全な SQL クエリを指定します。 既存の SQL クエリを使用するには **[開く]** を選択します。  

    > [!IMPORTANT]  
    > SQL クエリ設定では、データベースを変更する SQL コマンドをサポートしていません。 データベースから情報を読み込む SQL コマンドのみ使用できます。  


### <a name="wql-query"></a><a name="bkmk_wql"></a> WQL クエリ

- **名前空間**:クライアント コンピューターでのコンプライアンスについて評価される WMI 名前空間を指定します。 既定値は `root\cimv2` です。  

- **Class**:上記の名前空間におけるターゲット WMI クラスを指定します。  

- **プロパティ**: 上記のクラスにおけるターゲット WMI プロパティを指定します。  

- **WQL クエリの WHERE 句**:結果数を減らすには、修飾する句を指定します。 たとえば、Win32_Service クラスの DHCP サービスのみをクエリの対象とするには、WHERE 句を `Name = 'DHCP' and StartMode = 'Auto'` のようにします。   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a> XPath クエリ

- **パス**:コンプライアンスを評価するために使用するクライアント コンピューター上の .xml ファイルへのパスを指定します。 Configuration Manager では、パス名ですべての Windows システム環境変数と `%USERPROFILE%` ユーザー変数を使用できます。  

- **XML ファイル名**:上記のパスの XML クエリが含まれているファイル名を指定します。  

- **サブフォルダーも含める**:指定したパスの下にあるサブフォルダーを検索する場合は、このオプションをオンにします。  

- **このファイルは 64 ビット アプリケーションに関連付けられている**:64 ビットバージョンの Windows を実行している Configuration Manager クライアント上の 32 ビット システム ファイルがある場所 `%Windir%\Syswow64` に加えて、64 ビット システム ファイルの場所 `%Windir%\System32` を検索します。  

- **XPath クエリ**:有効な XML Path Language (XPath) クエリを完全な形式で指定します。  

- **名前空間**:XPath クエリの実行時に使用される名前空間とプレフィックスを指定します。  

暗号化された .xml ファイルを検出しようとすると、コンプライアンス設定ではファイルが見つかりますが、XPath クエリでは結果が生成されません。 Configuration Manager クライアントでは、エラーは生成されません。  

XPath クエリが有効でない場合は、設定はクライアント コンピューター上でコンプライアンス非対応として評価されます。  



##  <a name="configure-compliance-rules"></a>コンプライアンス規則の構成  

コンプライアンス規則は、構成項目のコンプライアンスを定義する条件を指定します。 設定に対してコンプライアンス評価が行われる前に、少なくとも 1 つのコンプライアンス規則を設ける必要があります。 WMI、レジストリ、およびスクリプトの設定により、コンプライアンス非対応となった値の修復ができます。 新しい規則を作成、または構成項目の既存の設定を参照して規則を選択することができます。  


### <a name="to-create-a-compliance-rule"></a>コンプライアンス規則を作成するには  

1. **[構成項目の作成ウィザード]** の **[コンプライアンスの規則]** ページで、 **[次へ]** を選択します。  

2. **[規則の作成]** ダイアログ ボックスで、次の情報を入力します。  

    - **名前**:コンプライアンス規則の名前を入力します。  

    - **説明**:コンプライアンス規則の説明を入力します。  

    - **[選択した設定]:** **[参照]** を選択し、 **[設定の選択]** ダイアログ ボックスを開きます。 規則を定義する設定を選択するか、または **[新しい設定]** を選択します。 完了したら、 **[選択]** を選択します。  

        > [!Tip]  
        > 現在選択されている設定についての情報を表示するには、 **[プロパティ]** を選択します。  

    - **ルールの種類**: 使用するコンプライアンス規則の種類を選択します。  

        - **値**:指定する値と構成項目によって返される値を比較するルールを作成します。 追加設定の詳細については、「[値の規則](#bkmk_value)」を参照してください。  

        - **存在**:設定を、それがクライアント デバイス上に存在するかどうか、またはそれが見つかった回数に応じて評価する規則を作成します。 追加設定の詳細については、「[存在の規則](#bkmk_exist)」を参照してください。  

3. **[OK]** を選択して **[規則の作成]** ダイアログ ボックスを閉じます。  




### <a name="value-rules"></a><a name="bkmk_value"></a> 値の規則  

- **プロパティ**: 調べるオブジェクトのプロパティは、選択される設定によって異なります。 指定できるプロパティは、設定の種類によってさまざまです。 

- **The setting must comply with the following... (設定は、次の ... に従う必要があります)** :指定できる規則またはアクセス許可は、設定の種類によって異なります。

- **サポートされている場合は準拠していない規則を修復する**:このオプションを選択すると、Configuration Manager によりコンプライアンス非対応の規則が自動的に修復されます。 Configuration Manager では、以下の規則の種類を使用して、このアクションをサポートしています。  

    - **レジストリ値**:準拠していない場合、クライアントによってこのレジストリ値が設定されます。 存在しなければ、クライアントによって値が作成されます。  

    - **スクリプト**:クライアントは、ユーザーが設定で指定した修復スクリプトを使用します。  

    - **WQL クエリ**  

    > [!IMPORTANT]  
    > コンプライアンス非対応の規則は、演算子が **[等しい]** に設定されている場合にのみ修復されます。  

- **この設定インスタンスが見つからない場合はコンプライアンス非対応としてレポートする**:クライアント コンピューターでこの設定が見つからない場合は、構成項目からコンプライアンス非対応を報告するためにこのオプションを有効にします。  

- **レポートするコンプライアンス非対応の重要度**:このコンプライアンス規則に従っていないときに、Configuration Manager レポートでレポートする重要度のレベルを指定します。 以下の重要度レベルを使用できます。  
    - **なし**  
    - **[情報]**  
    - **警告**  
    - **[重大]**  
    - **重大 (イベント)** : このコンプライアンス規則を満たしていないコンピューターは、**重大**というレベルで非対応を報告します。 重要度のレベルは、アプリケーションのイベント ログでも Windows のイベントとしてログが登録されます。  


### <a name="existential-rules"></a><a name="bkmk_exist"></a> 存在の規則 

> [!NOTE]  
> 表示されるオプションは、規則を構成する設定の種類によって異なる場合があります。  

- **この設定はクライアント デバイスに存在しなければならない**  

- **この設定はクライアント デバイスに存在してはならない**  

- **この設定は次の回数出現する:**  

- **レポートするコンプライアンス非対応の重要度**:このコンプライアンス規則に従っていないときに、Configuration Manager レポートでレポートする重要度のレベルを指定します。 以下の重要度レベルを使用できます。  
    - **なし**  
    - **[情報]**  
    - **警告**  
    - **[重大]**  
    - **重大 (イベント)** : このコンプライアンス規則を満たしていないコンピューターは、**重大**というレベルで非対応を報告します。 重要度のレベルは、アプリケーションのイベント ログでも Windows のイベントとしてログが登録されます。  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a> 構成項目の修復の追跡
<!--4261411-->
*(バージョン 2002 で導入)*

Configuration Manager バージョン 2002 以降では、構成項目のコンプライアンス規則に関して、**サポートされている場合は修復履歴を追跡**できます。 このオプションが有効になっているときには、クライアントで構成項目に対して発生した修復があると、状態メッセージが生成されます。 履歴は、Configuration Manager データベースに格納されます。

修復履歴を表示するには、パブリック ビューの **v_CIRemediationHistory** を使用してカスタム レポートを作成します。 `RemediationDate` 列は、クライアントが修復を実行した時刻 (UTC) です。 `ResourceID` によってデバイスが識別されます。 **v_CIRemediationHistory** ビューを使用してカスタム レポートを作成すると、以下のことに役立ちます。

- 修復スクリプトで発生する可能性のある問題を特定する
- 各評価サイクルで常に準拠していないクライアントなど、修復における傾向を見つける。

### <a name="enable-the-track-remediation-history-when-supported-option"></a>[Track remediation history when supported] (サポートされている場合は修復履歴を追跡する) オプションの有効化

- 新しい構成アイテムの場合は、ウィザードの **[設定]** ページで新しい設定を作成するときに、 **[コンプライアンス規則]** タブの **[Track remediation history when supported]\(サポートされている場合は修復履歴を追跡する\)** オプションを追加します。
- 既存の構成項目には、その構成項目の **[プロパティ]** の **[コンプライアンス規則]** タブで、 **[Track remediation history when supported] (サポートされている場合は修復履歴を追跡する)** オプションを追加します。
[ ![バージョン 2002 での [Track remediation history when supported] (サポートされている場合は修復履歴を追跡する)](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>次のステップ

[構成基準を作成する](create-configuration-baselines.md)