---
title: アプリケーションの作成
titleSuffix: Configuration Manager
description: 展開の種類、検出方法、およびソフトウェアのインストール要件を指定してアプリケーションを作成します。
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 33a95ae78fdc80c6c08b59cfe5ec5b2e88485a8f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074658"
---
# <a name="create-applications-in-configuration-manager"></a>Configuration Manager でアプリケーションを作成する

*適用対象:Configuration Manager (Current Branch)*

Configuration Manager アプリケーションではアプリケーションに関するメタデータが定義されます。 アプリケーションには 1 つ以上の展開の種類があります。 このような展開の種類には、デバイスにソフトウェアをインストールするために必要なインストール ファイルと情報が含まれます。 展開の種類には、検出方法や要件などの規則もあります。 これらの規則では、クライアントでソフトウェアをインストールするタイミングと方法が指定されます。  

次の方法を使用してアプリケーションを作成します。  

- アプリケーション インストール ファイルを読み取って、アプリケーションおよび展開の種類を自動的に作成する:  
  - [アプリケーションを作成](#bkmk_create)し、アプリケーションの情報を[自動的に検出する](#bkmk_auto-app)
  - [展開の種類を作成](#bkmk_create-dt)し、展開の種類の情報を[自動的に識別する](#bkmk_auto-dt)

- アプリケーションを手動で作成してから、後で展開の種類を追加する:  
  - [アプリケーションを作成](#bkmk_create)し、アプリケーションの情報を[手動で指定する](#bkmk_manual-app)
  - [展開の種類を作成](#bkmk_create-dt)し、展開の種類の情報を[手動で指定する](#bkmk_manual-dt)

- ファイルから[アプリケーションをインポートする](#bkmk_import)  

この記事には、展開の種類を構成するための以下の情報も含まれます。  

- [コンテンツ](#bkmk_dt-content)
- [タスク シーケンス](#bkmk_dt-ts)
- [検出方法](#bkmk_dt-detect)
- [ユーザー エクスペリエンス](#bkmk_dt-ux)
- [Requirements](#bkmk_dt-require)
- [リターン コード](#bkmk_dt-return)
- [の依存関係](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a> アプリケーションを作成する  

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** ノードを選択します。  

2. リボンの **[ホーム]** タブにある **[作成]** グループで、 **[アプリケーションの作成]** を選択します。  

次に、アプリケーションの情報を自動的に検出するか、手動で指定します。  

- 単一の展開の種類で基本的なアプリケーションを作成するには、アプリケーションの情報を[自動的に検出](#bkmk_auto-app)します。 たとえば、依存関係または要件を持たない Windows インストーラー ファイルなどです。 この手順を使用してアプリケーションを作成した後、必要に応じて編集します。 展開の種類を追加したり、変更したりすることができます。また、検出方法、依存関係、要件を追加することができます。  

- より複雑なアプリケーションを作成するには、アプリケーションの情報を[手動で指定](#bkmk_manual-app)します。 複数の展開の種類、依存関係、検出方法、または要件を定義します。  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a> アプリケーションの情報を自動的に検出する  

1. アプリケーションの作成ウィザードの **[全般]** ページで、 **[このアプリケーションの情報をインストール ファイルから自動的に検出する]** を選択します。  

2. **[種類]** ドロップダウン リストから、アプリケーション情報の検出に使用するアプリケーション インストール ファイルの種類を選択します。 利用可能なインストールの種類の詳細については、[Configuration Manager でサポートされる展開の種類](create-applications.md#bkmk_deploy-types)に関するページを参照してください。  

3. **[場所]** ボックスで、アプリケーション情報の検出に使用するアプリケーション インストール ファイルを指定します。 この場所は、ネットワーク パス (`\\server\share\filename`) またはストア リンクです。 ネットワーク パス、およびアプリケーションのコンテンツが含まれているサブフォルダーのアクセス権を持っている必要があります。  

    > [!IMPORTANT]  
    > **[Windows インストーラー (\*.msi ファイル)]** をアプリケーションの種類として選ぶと、指定したフォルダーにあるすべてのファイルがサイトでインポートされます。 その後、これらのファイルは配布ポイントに送信されます。 指定したフォルダーに、アプリケーションのインストールに必要なファイルのみが含まれていることを確認してください。 Microsoft では、アプリケーション パッケージで最大 20,000 個のファイルをサポートするように Configuration Manager がテストされています。 アプリケーションにそれ以上のファイルがある場合は、複数のアプリケーションを作成してファイルを分けることを検討してください。  

4. アプリケーションの作成ウィザードの **[情報のインポート]** ページで、情報を確認し、 **[次へ]** を選択します。 必要に応じて、 **[前へ]** を選択して戻り、エラーを修正します。  

5. アプリケーションの作成ウィザードの **[一般情報]** ページで、次の情報を指定します。  

    > [!NOTE]  
    > Configuration Manager がアプリケーション インストール ファイルからこの情報を自動的に検出した場合は、ここに既に設定されています。 また、作成するアプリケーションの種類によって、表示されるオプションが異なります。  

    - アプリケーションの**名前**、**管理者のコメント**、**発行元**、**ソフトウェア バージョン**など、アプリケーションに関する全般情報。 Configuration Manager コンソールでアプリケーションを見つけやすいように、**オプションの参照**を指定するか、**管理カテゴリ**を選択します。  

    - **インストール プログラム**:アプリケーションの展開の種類をインストールするのに必要なインストール プログラムとプロパティを指定します。  

        > [!TIP]  
        > インストール プログラムが表示されない場合は、 **[参照]** を選んでインストール プログラムの場所を参照します。  

    - **インストールの処理**:Configuration Manager でのこの展開の種類のインストール方法について、3 つのオプションのいずれかを選択します。 これらのオプションの詳細については、[ユーザー エクスペリエンス](#bkmk_dt-ux)に関する記述を参照してください。  

    - **自動 VPN 接続を使用する (構成されている場合)** :ユーザーがアプリを起動するデバイス上に VPN プロファイルを展開した場合は、アプリの開始時に VPN を接続します。 このオプションは Windows 8.1 および Windows Phone 8.1 専用です。 Windows Phone 8.1 デバイスでは、複数の VPN プロファイルをデバイスに展開する場合、自動 VPN 接続はサポートされません。 詳細については、[VPN プロファイル](../../protect/deploy-use/vpn-profiles.md)に関するページをご覧ください。  

    - **このアプリケーションをデバイス上のすべてのユーザーにプロビジョニングする**<!--1358310-->:デバイス上のすべてのユーザーに対して、Windows アプリ パッケージを含むアプリケーションをプロビジョニングします。 詳しくは、「[Windows アプリケーションを作成する](../get-started/creating-windows-applications.md#bkmk_provision)」をご覧ください。  

       > [!Tip]  
       > 既存のアプリケーションを変更する場合、この設定は Windows アプリ パッケージの展開の種類プロパティの **[ユーザー エクスペリエンス]** タブにあります。  

6. **[次へ]** を選択し、 **[概要]** ページでアプリケーションの情報を確認してから、アプリケーションの作成ウィザードを終了します。  

これで、Configuration Manager コンソールの **[アプリケーション]** ノードに、新しいアプリケーションが表示されます。 アプリケーションの作成は完了しました。

展開の種類をさらに追加する場合や、その他の設定を構成する場合は、「[アプリケーションの展開の種類を作成する](#bkmk_create-dt)」を参照してください。  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a> アプリケーションの情報を手動で指定する  

1. アプリケーションの作成ウィザードの **[全般]** ページで、 **[アプリケーションの情報を手動で指定する]** を選択し、 **[次へ]** を選択します。  

2. アプリケーションに関する**全般情報**を指定します。  

    - アプリケーションの**名前**は必須であり、256 文字未満にする必要があります。  

    - **管理者のコメント**、**発行元**、**ソフトウェア バージョン**は、アプリケーションについてさらに詳しく記述するための追加のメタデータです。  

    - Configuration Manager コンソールでアプリケーションを見つけやすいように、**オプションの参照**を指定するか、**管理カテゴリ**を選択します。  

    - **発行日**  

    - **所有者**および**サポートの連絡先**として、このアプリケーションを担当するユーザーまたはグループを選択します。 既定では、これらの値はユーザー名に設定されます。  

3. アプリケーションの作成ウィザードの **[ソフトウェア センター]** ページで、次の情報を指定します。  

    > [!Note]  
    > バージョン 1902 以前では、このページに「**アプリケーション カタログ**」という名前が付けられていました。

    - **選択した言語**:ドロップダウン リストから、セットアップするアプリケーションの言語バージョンを選びます。 **[追加/削除]** を選択し、このアプリケーションにその他の言語をセットアップします。  

    - **ローカライズされたアプリケーション名**:選択した言語でアプリケーション名を指定します。  

        > [!IMPORTANT]  
        > 設定する言語バージョンごとにローカライズされたアプリケーション名が必要です。  

    - **ユーザー カテゴリ**: **[編集]** を選び、選択した言語でアプリケーションのカテゴリを指定します。 ソフトウェア センターのユーザーはこれらのカテゴリを使用して、アプリケーションのフィルター処理と並べ替えを行うことができます。  

        > [!Note]  
        > バージョン 1902 以前では、ユーザー コレクションに対して利用可能な展開にのみユーザー カテゴリが適用されます。 コンピューター コレクションにアプリケーションを展開する場合は、ユーザー カテゴリは無視されます。
        >
        > バージョン 1906 より、デバイスを対象としたアプリケーションの展開のユーザー カテゴリが、ソフトウェア センターでフィルターとして表示されます。 これらの展開は、利用可能または必須のいずれかです。
        >
        > <!-- 4726793 -->カテゴリの名前変更や削除は、このカテゴリのアプリに自動的には適用されません。 これらの変更は、アプリの次のリビジョンに適用されます。 名前の変更または削除に関するこの問題を回避するには、次の操作を行います。
        >
        > - 最初に、そのカテゴリを参照するアプリのカテゴリのチェックボックスをオフにします。 その後、その変更を適用して、アプリを改訂します。
        >     - 次に、名前の変更アクションではなく、新しい名前で新しいカテゴリを作成し、関連するアプリにその新しいカテゴリを追加します。
        >     - カテゴリは、アプリの改訂後に削除できます。

    - **ユーザー ドキュメント**:ソフトウェア センターのユーザーがこのアプリケーションに関する詳細情報を取得できるファイルの場所を指定します。 この場所は、Web サイト アドレス、またはネットワーク パスとファイル名です。 ユーザーがこの場所にアクセスできることを確認してください。  

    - **リンク テキスト**:ユーザー ドキュメントが指定されている場合に、"追加情報" の代わりに表示されるテキストを指定します。  

    - **[プライバシー URL]** : アプリケーションのプライバシーに関する声明の Web サイト アドレスを指定します。  

    - **ローカライズされた説明**:選択した言語でこのアプリケーションの説明を入力します。  

    - **キーワード**:選択した言語でキーワードの一覧を入力します。 これらのキーワードは、ソフトウェア センターのユーザーがアプリケーションを検索するときに役立ちます。  

    - **アイコン**: **[参照]** を選択して、このアプリケーション用のアイコンを選択します。 アイコンを指定しない場合、Configuration Manager では既定のアイコンが使用されます。 アイコンでは、最大 512 x 512 のピクセル寸法を使用できます。  

4. アプリケーションの作成ウィザードの **[展開の種類]** ページで **[追加]** を選択し、新しい展開の種類を作成します。 詳細については、「[アプリケーションの展開の種類を作成する](#bkmk_create-dt)」を参照してください。  

5. **[次へ]** を選択し、 **[概要]** ページでアプリケーションの情報を確認してから、アプリケーションの作成ウィザードを終了します。  

これで、Configuration Manager コンソールの **[アプリケーション]** ノードに、新しいアプリケーションが表示されます。  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a> アプリケーションの展開の種類を作成する  

[アプリケーションの情報を自動検出する](#bkmk_auto-app)場合、このセクションの手順の一部は行わなくてもよい可能性があります。  

> [!Note]  
> 既存の展開の種類のプロパティを表示するときに、展開の種類のプロパティ ウィンドウのタブに対応するセクションには次のようなものがあります。  
>
> - [コンテンツ](#bkmk_dt-content)
> - [タスク シーケンス](#bkmk_dt-ts)
> - [検出方法](#bkmk_dt-detect)
> - [ユーザー エクスペリエンス](#bkmk_dt-ux)
> - [Requirements](#bkmk_dt-require)
> - [リターン コード](#bkmk_dt-return)
> - [の依存関係](#bkmk_dt-depend)
>  
> 展開の種類のプロパティの **[インストールの処理]** タブについては、「[実行中の実行可能ファイルを確認する](deploy-applications.md#bkmk_exe-check)」を参照してください。  

### <a name="start-the-create-deployment-type-wizard"></a>展開の種類の作成ウィザードを開始する  

展開の種類の作成ウィザードを開始する方法は 3 つあります。

- **[アプリケーション] ノードで**:Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** ノードを選択します。 アプリケーションを選択し、リボンの **[展開の種類の作成]** を選択します。  

- **アプリケーションを作成するとき**:アプリケーションの作成ウィザードで[アプリケーションの情報を手動で指定する](#bkmk_manual-app)場合は、[展開の種類] ページで **[追加]** を選択します。  

- **アプリケーションのプロパティから**: **[アプリケーション]** ノードで既存のアプリケーションを選択し、 **[プロパティ]** を選択します。 **[展開の種類]** タブに切り替え、 **[追加]** を選択します。

次に、以下のいずれかの手順を使用して、展開の種類の情報を[自動的に識別する](#bkmk_auto-dt)か、[手動で指定](#bkmk_manual-dt)します。  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a> 展開の種類の情報を自動的に識別する  

1. 展開の種類の作成ウィザードの **[全般]** ページで:  

    1. アプリケーション インストール ファイルの**種類**を選択し、展開の種類の情報を検出します。  

    2. **[この展開の種類に関する情報をインストール ファイルから自動的に識別する]** を選択します。  

    3. **[場所]** ボックスで、展開の種類の情報を検出するために使用するアプリケーション インストール ファイルを指定します。 この場所は、ネットワーク パス (`\\server\share\filename`) またはストア リンクです。 ネットワーク パス、およびアプリケーションのコンテンツが含まれているサブフォルダーのアクセス権を持っている必要があります。  

2. 展開の種類の作成ウィザードの **[情報のインポート]** ページで、情報を確認し、 **[次へ]** を選択します。 必要に応じて、 **[前へ]** を選択して戻り、エラーを修正します。  

3. 展開の種類の作成ウィザードの **[一般情報]** ページで、次の情報を指定します。  

    > [!NOTE]  
    > 展開の種類の情報によっては、既にアプリケーション インストール ファイルから読み込まれて入力されている場合があります。 また、作成する展開の種類によって、表示されるオプションが異なる場合があります。  

    - 展開の種類に関する**全般情報**:  
        - **名前**は必須です  

        - さらに詳しく記述するための**管理者のコメント**  

        - 利用可能な**言語**  

    - **インストール プログラム**:展開の種類のインストールに必要なインストール プログラムとプロパティを指定します。  

    - **インストールの処理**:Configuration Manager でのこの展開の種類のインストール方法について、3 つのオプションのいずれかを選択します。 これらのオプションの詳細については、[ユーザー エクスペリエンス](#bkmk_dt-ux)に関する記述を参照してください。  

    - **自動 VPN 接続を使用する (構成されている場合)** :ユーザーがアプリを起動するデバイス上に VPN プロファイルを展開した場合は、アプリの開始時に VPN を接続します。 このオプションは Windows 8.1 および Windows Phone 8.1 専用です。 Windows Phone 8.1 デバイスでは、複数の VPN プロファイルをデバイスに展開する場合、自動 VPN 接続はサポートされません。 詳細については、[VPN プロファイル](../../protect/deploy-use/vpn-profiles.md)に関するページをご覧ください。  

4. **[次へ]** を選択して、「[Deployment type Content options](#bkmk_dt-content)」 (展開の種類のコンテンツ オプション) に進みます。  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a> 展開の種類の情報を手動で指定する  

1. 展開の種類の作成ウィザードの **[全般]** ページの **[種類]** ドロップダウン リストで、この展開の種類のアプリケーション インストール ファイルの種類を選びます。

2. **[展開の種類の情報を手動で指定する]** をオンにして、 **[次へ]** を選択します。

3. 展開の種類の作成ウィザードの **[全般情報]** ページで、展開の種類の **[名前]** を指定します。 必要に応じて、 **[管理者のコメント]** を指定し、この展開の種類の **[言語]** を選択してから **[次へ]** を選択します。  

4. 「[Deployment type Content options](#bkmk_dt-content)」 (展開の種類のコンテンツ オプション) に進みます。  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a> 展開の種類の**コンテンツ** オプション  

**[コンテンツ]** ページで、以下の情報を指定します。  

> [!Note]  
> 既存の展開の種類のプロパティを表示すると、これらのオプションの一部が **[コンテンツ]** タブや **[プログラム]** タブに示されます。  

- **コンテンツの場所**:この展開の種類のコンテンツの場所を指定するか、 **[参照]** を選んで展開の種類のコンテンツのフォルダーを選びます。  

    > [!IMPORTANT]  
    > サイト サーバー コンピューターのシステム アカウントには、指定されたコンテンツの場所に対するアクセス許可が必要です。  

  - **クライアント キャッシュの内容を保持する**:構成マネージャー クライアントでは、そのキャッシュで展開の種類のコンテンツが無期限に保持されます。 アプリが既にインストールされている場合でも、クライアントではコンテンツが保持されます。 このオプションは、Windows インストーラー ベースのソフトウェアなど、一部の展開に便利です。 Windows インストーラーでは、更新プログラムを適用するためにソース コンテンツのローカル コピーが必要です。 このオプションを選ぶと、利用可能なキャッシュ領域が減ります。 このオプションを選んだ場合、キャッシュに十分な空き領域がないと、後で大規模な展開に失敗する可能性があります。  

- **インストール プログラム**:インストール プログラムの名前と必要なインストール パラメーターを指定します。  

  - **インストール開始までの時間**:必要に応じて、展開の種類のインストール プログラムがあるフォルダーを指定します。 このフォルダーには、クライアントの絶対パスを指定することも、インストール ファイルがある配布ポイント フォルダーのパスを指定することもできます。  

- **プログラムのアンインストール**:必要に応じて、アンインストール プログラムの名前と必要なパラメーターを指定します。  

  - **開始までの時間**:必要に応じて、展開の種類のアンインストール プログラムがあるフォルダーを指定します。 このフォルダーには、クライアント上の絶対パスを指定できます。 または、パッケージが含まれるフォルダーの配布ポイント上の相対パスでもかまいません。  

- **プログラム修復**:Windows インストーラーとスクリプト インストーラーの展開の種類について、必要に応じて、修復プログラムの名前と必要なパラメーターを指定します。<!--1357866-->  

  - **修復の開始**:必要に応じて、展開の種類の修復プログラムがあるフォルダーを指定します。 このフォルダーには、クライアント上の絶対パスを指定できます。 または、パッケージが含まれるフォルダーの配布ポイント上の相対パスでもかまいません。  

- **64 ビット クライアント上で 32 ビット プロセスとしてインストールおよびアンインストール プログラムを実行する**:Windows ベースのコンピューターで 32 ビットのファイルとレジストリの場所を使用し、展開の種類のインストール プログラムを実行します。  

#### <a name="deployment-type-properties-content-options"></a>展開の種類プロパティの**コンテンツ** オプション

展開の種類のプロパティを表示すると、 **[コンテンツ]** タブにのみ次のオプションが示されます。

- **アンインストール コンテンツ設定**:  

  - **インストール コンテンツと同じ**:インストール コンテンツとアンインストール コンテンツが同じ場合は、このオプションを選びます。 これが既定のオプションです。  

  - **アンインストール コンテンツなし**:アプリケーションにアンインストール コンテンツが必要でない場合は、このオプションを選びます。  

  - **インストール コンテンツと異なる**:アンインストール コンテンツがインストール コンテンツと異なる場合は、このオプションを選びます。  

    - **アンインストール コンテンツの場所**:アプリケーションをアンインストールするために使用されるコンテンツへのネットワーク パスを指定します。  

- **既定サイトの境界グループからの配布ポイントの使用をクライアントに許可する**:コンテンツが現在または近隣境界グループの配布ポイントから利用できないときに、クライアントでサイトの既定の境界グループの配布ポイントからソフトウェアをダウンロードしてインストールするかどうかを指定します。  

- **展開オプション**:近隣または既定のサイト境界グループから配布ポイントを使用するときに、クライアントでアプリケーションをダウンロードするかどうかを指定します。  

- **同じサブネットにある他のクライアントとのコンテンツの共有を許可する**:コンテンツのダウンロードで BranchCache の使用を有効にするかどうかを指定します。 詳細については、「[BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache)」を参照してください。 BranchCache は、クライアントで常に有効になっています。 配布ポイントで BranchCache がサポートされている場合はクライアントでそれが使用されるため、この設定はバージョン 1802 で削除されました。  

### <a name="deployment-type-task-sequence-options"></a><a name="bkmk_dt-ts"></a> **タスク シーケンス**の展開の種類のオプション

<!--3555953-->

バージョン 2002 以降のタスク シーケンスの展開の種類の詳細については、「[タスク シーケンスの展開の種類](../get-started/creating-windows-applications.md#bkmk_tsdt)」を参照してください。

**[タスク シーケンス]** ページで次の情報を指定します。

- **インストールのタスクのシーケンス**:このアプリのインストール プロセスを実行するタスク シーケンスを選択します。

- **アンインストールのタスク シーケンス** (オプション):このアプリを削除するタスク シーケンスを選択します。

> [!TIP]  
> タスク シーケンスが一覧にない場合は、それに OS 展開や OS アップグレード手順が含まれないことを再確認します。 また、影響の大きいタスク シーケンスとしてマークされていないことも確認します。 詳細については、「[タスクシーケンスの展開の種類](../get-started/creating-windows-applications.md#bkmk_tsdt)」の前提条件を確認してください。

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a> 展開の種類の**検出方法**オプション

この手順では、展開の種類の存在を示す検出方法を設定します。 つまり、Windows デバイスに既にアプリケーションがインストールされているかどうかです。 検出方法を作成するには、次の 2 つの方法のいずれかを使用します。

- [この展開の種類が存在するかどうかを検出する規則を構成する](#bkmk_detect-rule)
- [カスタム スクリプトを使用してこの展開の種類が存在するかどうかを検出する](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a> この展開の種類が存在するかどうかを検出する規則を構成する

1. **[検出方法]** ページでは、 **[この展開の種類が存在するかどうかを検出する規則を構成する]** オプションが既定で選択されます。 **[句の追加]** を選択します。  

2. **[検出規則]** ダイアログ ボックスで、展開の種類の存在を検出する **[設定の種類]** を選択します。  

    - **ファイル システム**:指定したファイルまたはフォルダーがデバイスに存在するかどうかを検出します。 検出されると、アプリケーションがインストールされていることを示します。 次の詳細情報を指定します。  

        - **種類**:ファイルかフォルダーかを選びます。  

        - **パス** (必須):ファイルまたはフォルダーを含むデバイス上のローカル パスを入力するか参照します。 たとえば、`C:\Program Files` となります。 共有ネットワーク パスを指定することはできません。 **[参照]** を選択する場合は、ローカル ファイル システムを参照するか、参照する代表的なクライアントに接続します。  

        - **ファイル名またはフォルダー名** (必須):上記のパスで検出する特定のファイルまたはフォルダーの名前を指定します。 デバイス上でクライアントによってこのファイルまたはフォルダーが検出された場合、アプリケーションはデバイスにインストールされていると見なされます。  

        - **このファイル/フォルダーは 64 ビット システムの 32 ビット アプリケーションに関連している**:既定では、このオプションはオンです。 クライアントでは、まず、指定されたファイルまたはフォルダーについて、32 ビットのファイルの場所が確認されます。 ファイルやフォルダーが見つからない場合、クライアントでは次に 64 ビットの場所が検索されます。  

    - **レジストリ**:指定したレジストリ キーまたはレジストリ値がクライアント デバイスに存在するかどうかを検出します。 検出されると、アプリケーションがインストールされていることを示します。 次の詳細情報を指定します。  

        - **ハイブ** (必須):ドロップダウン リストからレジストリ ハイブを選択します。 たとえば、`HKEY_LOCAL_MACHINE` となります。  

        - **キー** (必須):上記のハイブで検索するレジストリ キーを指定します。 たとえば、`SOFTWARE\Microsoft\Office` となります。  

        - **値** (省略可能):上記のキーで検出する特定の値を入力します。 クライアントで (既定の) 値を検出する場合は、 **[検出に (既定の) レジストリ キー値を使用する]** オプションを有効にします。 値を入力するかこのオプションを有効にする場合は、 **[データの種類]** を選択する必要があります。  

        - **64 ビット システムでこのレジストリ キーを 32 ビット アプリケーションに関連付ける**:指定されたレジストリ キーについて、まず、32 ビット レジストリの場所を確認する場合は、このオプションを選択します。 レジストリ キーが見つからない場合、クライアントでは 64 ビットの場所が検索されます。  

    - **Windows インストーラー**:指定した Windows インストーラー ファイルがクライアント デバイスに存在するかどうかを検出します。 検出されると、アプリケーションがインストールされていることを示します。 クライアントで検出する MSI の**製品コード**を指定します。 **[参照]** を選択した場合は、製品コードの読み取り元の MSI ファイルを選択します。

3. [検出規則] ウィンドウの下部で、項目が存在する必要があるか規則を満たす必要があるかを指定します。 たとえば、ファイルで検出する場合、 **[このアプリケーションのプレゼンスを示すには、ターゲット システムにファイル システム設定が存在する必要がある]** オプションが既定で選択されます。 ファイルまたはフォルダーのプロパティに基づく検出の規則を作成する場合は、その他のオプションを選択します。 これらのプロパティには、変更日、作成日、バージョン、サイズが含まれます。 これらの規則は設定の種類ごとに異なります。  

4. **[OK]** を選択して、 **[検索規則]** ダイアログ ボックスを閉じます。  

展開の種類に対して複数の検出方法を作成する場合は、句をまとめてグループ化して、より複雑なロジックを作成できます。  

#### <a name="group-detection-clauses-optional"></a>検出の句をグループ化する " *(省略可能)* "

1. 展開の種類に対して、検出方法に関する句を 3 つ以上作成します。  

2. 2 つ以上の連続する句を選択した後、 **[グループ化]** を選択します。 関連付けた列にかっこが付いて表示されます。これによりグループの開始と終了が示されます。  

    例:

    | コネクタ  |  ( | 句           |  )  |
    |------------|----|------------------|-----|
    |            |    | MSI 製品コード |     |
    | または         | (  | file1.text が存在する|     |
    | および        |    | file2.txt が存在する | )   |

3. グループを削除するには、グループ化された句を選択した後、 **[グループ化解除]** を選択します。  

検出方法としてのカスタム スクリプトの使用に関する次のセクションに "*進みます*"。 または、展開の種類の[ユーザー エクスペリエンス](#bkmk_dt-ux) オプションまで "*スキップします*"。

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a> カスタム スクリプトを使用して展開の種類の存在を確認する  

1. **[検出方法]** ページで、 **[カスタム スクリプトを使用してこの展開の種類の存在を検出する]** を選択します。 次に、 **[編集]** を選択します。  

2. **[スクリプト エディター]** ダイアログ ボックスで、次の展開の種類を検出する **[スクリプトの種類]** を選択します: (PowerShell、VBScript、または JScript) を選択します。  

    > [!Note]  
    > Windows PowerShell スクリプトをアプリの検出方法として実行すると、Configuration Manager クライアントが `-NoProfile` パラメーターを使用して PowerShell を呼び出します。 このオプションでは、プロファイルなしで PowerShell が起動されます。 PowerShell プロファイルは、PowerShell の開始時に実行されるスクリプトです。 <!--3607762-->  

3. **[スクリプトの内容]** ボックスに使用するスクリプトを入力するか、既存のスクリプトの内容を貼り付けます。 保存されている既存のスクリプトを参照するには、 **[開く]** を選択します。 [スクリプトの内容] フィールドでテキストを削除するには、 **[クリア]** を選択します。 必要に応じて、 **[64 ビット クライアントで 32 ビット プロセスとしてスクリプトを実行する]** オプションを有効にします。  

    > [!NOTE]  
    > スクリプトの最大サイズは 32 KB です。  

4. **[OK]** を選択してスクリプトを保存し、 **[スクリプト エディター]** ダイアログ ボックスを閉じます。 展開の種類の作成ウィザードに戻ると、 **[スクリプトの種類]** フィールドと **[スクリプトの長さ]** フィールドがスクリプトに関する詳細で更新されます。

#### <a name="about-custom-script-detection-methods"></a>カスタム スクリプトの検出方法について  

Configuration Manager は、スクリプトの結果を調べます。 スクリプトによって標準出力 (STDOUT) ストリーム、標準エラー (STDERR) ストリーム、および終了コードに書き込まれた値を読み取ります。 スクリプトがゼロ以外の値で終了した場合、スクリプトは失敗しており、アプリケーション検出の状態は*不明* です。 終了コードがゼロであり、STDOUT にデータがある場合、アプリケーションの検出状態は*インストール済み* になります。

> [!TIP]
> 検出スクリプトを記述するときに、0 の終了コードを返すが、出力 (STDOUT のデータ) を返さない場合、アプリケーションがインストール済みとして検出されません。 詳細については、次の例を参照してください。

次の表を使って、スクリプトの出力から、アプリケーションがインストール済みかどうかを確認します。  

##### <a name="zero-exit-code"></a>ゼロの終了コード

|STDOUT|STDERR|スクリプトの結果|アプリケーション検出状態|
|---------|---------|---------|---------|
|空|空|成功|インストールされていない|
|空|空ではない|失敗|Unknown|
|空ではない|空|成功|インストール済み|
|空ではない|空ではない|成功|インストール済み|

##### <a name="non-zero-exit-code"></a>ゼロ以外の終了コード

|STDOUT|STDERR|スクリプトの結果|アプリケーション検出状態|
|---------|---------|---------|---------|
|空|空|失敗|Unknown|
|空|空ではない|失敗|Unknown|
|空ではない|空|失敗|Unknown|
|空ではない|空ではない|失敗|Unknown|

##### <a name="examples"></a>例

以下の PowerShell/VBScript の例を使用して、独自のアプリケーション検出スクリプトを記述します。  

**例 1**:スクリプトからゼロ以外の終了コードが返されます。 このコードは、スクリプトが正常に実行できなかったことを示します。 この場合、アプリケーション検出状態は不明です。  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**例 2**:スクリプトからゼロの終了コードが返されますが、STDERR の値は空ではありません。 この結果は、スクリプトが正常に実行できなかったことを示します。 この場合、アプリケーション検出状態は不明です。  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**例 3**:ゼロの終了コードが返され、スクリプトが正常に実行されたことが示されます。 しかし、STDOUT の値は空で、アプリケーションがインストールされていないことが示されます。  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**例 4**:ゼロの終了コードが返され、スクリプトが正常に実行されたことが示されます。 STDOUT の値は空ではなく、アプリケーションがインストールされていることが示されます。  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**例 5**:ゼロの終了コードが返され、スクリプトが正常に実行されたことが示されます。 STDOUT と STDERR の値は空ではなく、アプリケーションがインストールされていることが示されます。  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a> 展開の種類の**ユーザー エクスペリエンス** オプション

これらの設定は、クライアントがデバイスにアプリケーションをインストールする方法と、ユーザーに表示される内容を指定します。  

**[ユーザー側の表示と操作]** ページで、次の情報を指定します。  

- **インストールの動作**:ドロップダウン リストから、次のいずれかのオプションを選択します。  

  - **ユーザー用にインストール**:クライアントでは、アプリケーションの展開先であるユーザーのみを対象としてアプリケーションがインストールされます。  

  - **システム用にインストール**:クライアントではアプリケーションが 1 回だけインストールされます。 すべてのユーザーが利用できます。  

  - **リソースがデバイスの場合はシステム用に、それ以外の場合はユーザー用にインストールする**:アプリケーションをデバイスに展開する場合、クライアントではすべてのユーザーを対象にインストールが行われます。 アプリケーションをユーザーに展開する場合、クライアントではそのユーザーのみを対象にインストールが行われます。  

- **ログオン要件**:次のいずれかのオプションを選択します。  

  - **ユーザーがログオンしているときのみ**  

  - **ユーザーのログオン状態にかかわらず**  

  - **ユーザーがログオンしていないときのみ**  

    > [!NOTE]  
    > このオプションの既定値は **[ユーザーがログオンしているときのみ]** です。 **[インストールの動作]** ドロップダウン リストで **[ユーザー用にインストール]** を選んだ場合は、このオプションを変更できません。  

- **インストール プログラムの表示**:展開の種類をクライアント デバイスで実行するモードを指定します。 次のいずれかのオプションを選択します。  

  - **最大化**:展開の種類をクライアント デバイスで最大化して実行します。 ユーザーにはすべてのインストール動作が表示されます。  

  - **通常**:展開の種類をシステムとプログラムの既定のモードで実行します。 このモードが既定値です。  

  - **最小化**:展開の種類をクライアント デバイスで最小化して実行します。 ユーザーは通知エリアまたはタスクバーでインストール動作を確認できます。  

  - **非表示**:クライアント デバイスで展開の種類を非表示にします。 ユーザーにはインストール動作が表示されません。  

- **プログラムのインストールの表示および対話をユーザーに許可する**:展開の種類のインストールで、ユーザーがインストール オプションをセットアップできるようにするかどうかを指定します。  

    **[インストールの動作]** ドロップダウン リストで **[ユーザー用にインストール]** オプションを選んだ場合、このオプションは既定で有効になります。  

    > [!IMPORTANT]  
    > **[システム用にインストールする]** 動作を選んだ場合、この設定は省略可能です。 この変更は主として、ユーザーがタスク シーケンスの間にインストールと対話できるようにするためです。 たとえば、さまざまなオプションの入力をエンド ユーザーに求めるセットアップ プロセスを実行します。 一部のアプリケーション インストーラーでは、ユーザー プロンプトを消せなかったり、インストール プロセスでユーザーだけが知っている特定の構成値が求められたりする場合があります。 <!--1356976-->  
    >  
    > システム コンテキストでインストールし、インストールの操作をユーザーに許可することは、セキュリティで保護された構成ではありません。 詳細については、「[アプリケーション管理に関するセキュリティとプライバシー](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact)」をご覧ください。  

- **許容最長実行時間 (分)** :クライアント コンピューターで展開の種類を実行できる最長時間 (分単位) を指定します。 この設定はゼロより大きい整数として指定します。 既定値は 120 分 (2 時間) です。  

    この値は次の操作で使用します。  

  - 展開の種類の結果を監視するため。  

  - クライアント デバイスでメンテナンス期間を定義する場合に、展開の種類をインストールするかどうかを確認するため。 メンテナンス期間が設定されている場合は、 **[許可最長実行時間]** で指定した時間が、メンテナンス期間の残りに収まる場合にのみ、展開の種類が起動します。  

    > [!IMPORTANT]  
    > スケジュールされているメンテナンス期間より **[許可最長実行時間]** が長い場合は、競合が発生することがあります。 ユーザーが最長実行時間をメンテナンス期間より長く設定した場合は、その展開の種類は実行されません。  

- **インストールの推定時間 (分)** :展開の種類の推定インストール時間を指定します。 ソフトウェア センターではこの時間がユーザーに表示されます。  

#### <a name="deployment-type-properties-user-experience-options"></a>展開の種類プロパティの**ユーザー エクスペリエンス** オプション

展開の種類のプロパティを表示すると、 **[ユーザー エクスペリエンス]** タブにのみ次のオプションが示されます。

特定のインストール後の動作を適用します。 次のいずれかのオプションを選択します。  

- **リターン コードを基に動作を決定する**:[[リターン コード]](#bkmk_dt-return) タブで構成されたコードに基づいて、再起動を処理します。ソフトウェア センターには、"**再起動を必要とする可能性がある**" ことを示すメッセージが表示されます。 インストール中にユーザーがサインインすると、*展開の*ユーザー エクスペリエンス構成に応じて、プロンプトが表示されます。  

- **何もしない**:インストール後の再起動は不要です。 ソフトウェア センターでは、再起動は不要と報告されます。  

- **ソフトウェア インストール プログラムによってデバイスの再起動が強制実行されるようにする**:Configuration Manager で再起動の制御や開始を行うことはありませんが、実際のインストールでは警告なしでこれらが行われる場合があります。 インストーラーでの再起動の開始時に Configuration Manager がインストールの失敗を報告しないようにする場合は、この設定を使用します。 ソフトウェア センターには、"**再起動を必要とする可能性がある**" ことを示すメッセージが表示されます。  

- **構成マネージャー クライアントによって、デバイスの必須の再起動が強制実行されるようにする**:インストールが正常に行われてから、Configuration Manager によってデバイスの再起動が強制実行されます。 ソフトウェア センターでは、再起動が必要であることが報告されます。 インストール中にユーザーがサインインすると、*展開の*ユーザー エクスペリエンス構成に応じて、プロンプトが表示されます。  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a> 展開の種類の**要件**

Configuration Manager では、展開の種類のインストールの前に、デバイスでこれらの要件が確認されます。 要件を使用して、このアプリケーションを受信するデバイスまたはユーザーをさらに絞り込み、制御します。 たとえば、ユーザー コレクションにアプリケーションを展開する場合は、ここでアプリのハードウェア要件を指定します。

1. **[要件]** ページで、 **[追加]** を選択して **[要件の作成]** ダイアログ ボックスを開きます。  

2. **[カテゴリ]** ドロップダウン リストで、この要件が**デバイス**と**ユーザー**のどちらに対するものかを選びます。  

    前に作成したグローバル条件を使うには、 **[カスタム]** を選びます。 **[カスタム]** を選択した場合は、 **[作成]** を選択して新しいグローバル条件を作成することもできます。 グローバル条件の詳細については、「[グローバル条件を作成する方法](create-global-conditions.md)」を参照してください。  

    > [!IMPORTANT]  
    > アプリケーションをデバイス コレクションに展開する場合、クライアントはカテゴリ **[ユーザー]** と条件 **[プライマリ デバイス]** の要件を無視します。  

3. **[条件]** ドロップダウン リストで、ユーザーまたはデバイスがインストール要件を満たしているかどうかを評価するための条件を選択します。 この一覧の内容は、選択したカテゴリによって異なります。  

4. **[演算子]** ドロップダウン リストで、使う演算子を選びます。 この演算子は、選んだ条件と指定した値を比較します。 ユーザーまたはデバイスがインストール要件を満たしているかどうかが評価されます。 利用可能な演算子は選択された条件によって異なります。  

    > [!Note]  
    > 使用できる要件は、展開の種類で使用するデバイスの種類によって異なります。  

5. **[値]** ボックスで、比較に使用する値を指定します。 これらの値と、選んだ条件および演算子により、ユーザーまたはデバイスがインストール要件を満たすかどうかが評価されます。 利用可能な値は選択された条件および選択された演算子によって異なります。  

6. **[OK]** を選択して要件を保存し、 **[要件の作成]** ダイアログ ボックスを閉じます。  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a> 展開の種類の**依存関係**  

依存関係では、クライアントでこの展開の種類をインストールする前にインストールする必要がある、別のアプリケーションからの 1 つまたは複数の展開の種類が定義されます。

> [!IMPORTANT]  
> 展開の種類が別の展開の種類と依存関係にあり、この別の展開の種類にも依存関係がある場合があります。 チェーンでサポートされる依存関係の最大数は 5 つです。  

1. **[依存関係]** ページで、 **[追加]** を選択します。  

2. [依存関係の追加] ウィンドウで、**依存関係グループの名前**を入力します。 この名前は、このアプリケーションの依存関係グループを指します。  

3. [依存関係の追加] ウィンドウで、 **[追加]** を選択します。  

4. **[必須アプリケーションの指定]** ウィンドウで、依存関係として使用する利用可能なアプリケーションとその展開の種類を 1 つ以上選択します。  

    > [!TIP]  
    > **[表示]** を選択して、選択したアプリケーションまたは展開の種類のプロパティを表示します。  

5. **[OK]** を選択して **[必須アプリケーションの指定]** ウィンドウを閉じます。  

6. クライアントで依存アプリケーションを自動的にインストールする場合は、依存関係の横にある **[自動インストール]** を選択します。  

    > [!NOTE]  
    > クライアントで自動的にインストールする場合は、ユーザーが依存アプリケーションを展開する必要はありません。  

7. 複数の依存関係を追加する場合は、 **[優先順位を上げる]** ボタンと **[優先順位を下げる]** ボタンを使用します。 これらのアクションは、クライアントが各依存関係を評価する順序を変更します。  

8. **[OK]** を選択して **[依存関係の追加]** ウィンドウを閉じます。  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a> 展開の種類の**リターン コード**

> [!Note]  
> 展開の種類の作成ウィザードにこのページはありません。 既存の展開の種類のプロパティのタブのみです。  

展開の種類が完了したら、動作を制御するリターン コードを指定します。 たとえば、再起動が必要であることや、インストールが完了したことを通知します。

1. 展開の種類のプロパティ ウィンドウの **[リターン コード]** タブで、 **[追加]** を選択します。  

2. [リターン コードの追加] ウィンドウで、この展開の種類に必要な **[リターン コードの値]** を指定します。 この値は、`-2147483648` から `2147483647` までの正または負の整数です。  

3. ドロップダウン リストから **[コードの種類]** を選択します。 この設定では、この展開の種類からの指定されたリターン コードを Configuration Manager でどのように解釈されるかを定義します。 利用可能な種類は、展開の種類のテクノロジによって異なります。  

    - **成功 (リブートなし)** :展開の種類は正常にインストールされており、再起動は必要ありません。  

    - **失敗 (リブートなし)** :展開の種類のインストールに失敗しました。  

    - **ハード リブート**:展開の種類は正常にインストールされていますが、デバイスの再起動が必要になります。 デバイスが再起動されるまでは、他に何もインストールできません。  

    - **ソフト リブート**:展開の種類は正常にインストールされていますが、デバイスの再起動が要求されます。 デバイスが再起動する前に、他のインストールが行われることがあります。  

    - **高速リトライ**:デバイス上で既に別のインストールが進行中です。 クライアントでは 2 時間ごとに合計で 10 回、再試行されます。  

4. 必要に応じて、このリターン コードの **[名前]** と **[説明]** を入力します。

5. **[OK]** を選択し、[リターン コードの追加] ウィンドウを閉じます。  

#### <a name="example-non-zero-success"></a>例: 0 以外での成功

アプリケーションが正常にインストールされたときに `1` の終了コードを返すアプリケーションを展開します。 既定では、Configuration Manager でこのゼロ以外のリターン コードが失敗として検出されます。 `1` のリターン コード値を指定するか、 **[成功 (リブートなし)]** のコードの種類を選択します。 これで Configuration Manager では、この展開の種類について、そのリターン コードが成功と解釈されます。

#### <a name="default-return-codes"></a>既定のリターン コード

いくつかの展開の種類を作成するときに、Configuration Manager では、そのテクノロジに共通する以下のリターン コードが自動的に追加されます。  

##### <a name="windows-installer-msi-file"></a>Windows インストーラー (\*.msi ファイル)

|値    |コードの種類|
|---------|---------|
|0        |成功 (リブートなし)|
|1707     |成功 (リブートなし)|
|3010     |ソフト リブート|
|1641     |ハード リブート|
|1618     |高速リトライ|

##### <a name="script-installer"></a>スクリプト インストーラー

|値    |コードの種類|
|---------|---------|
|0        |成功 (リブートなし)|
|1641     |ハード リブート|
|3010     |ソフト リブート|
|1618     |高速リトライ|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Windows アプリケーション パッケージ (\*.appx、\*.appxbundle、\*.msix、\*.msixbundle)

|値    |コードの種類|
|---------|---------|
|15605    |高速リトライ|
|15618    |高速リトライ|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a> App-V の展開の種類の追加オプション  

仮想アプリケーション (App-V) 用の展開の種類に固有である追加オプションを構成します。  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a> App-V の展開の種類の**コンテンツ** オプション  

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** ノードを選択します。  

2. App-V の展開の種類のアプリケーションを選択し、 **[プロパティ]** を選択します。  

3. アプリケーションのプロパティで、 **[展開の種類]** タブに切り替えます。App-V の展開の種類を選択して、 **[編集]** を選択します。  

4. 展開の種類のプロパティで、 **[コンテンツ]** タブに切り替えます。必要に応じて、次のオプションを構成します。  

    - **クライアント キャッシュの内容を保持する**:構成マネージャー クライアントでは、そのキャッシュからこの展開の種類のコンテンツが削除されません。  

    - **起動前にコンテンツを App-V キャッシュに読み込む**:アプリケーションの起動前に、構成マネージャー クライアントで、この展開の種類用のすべてのコンテンツが App-V キャッシュに読み込まれます。 クライアントではキャッシュ内のコンテンツはピン留めされません。 必要に応じてコンテンツが削除されます。  

5. **[OK]** を選択して、展開の種類のプロパティを閉じます。 その後、 **[OK]** を選択してアプリケーションのプロパティを閉じます。  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a> App-V の展開の種類の**発行**オプション

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** ノードを選択します。  

2. App-V の展開の種類のアプリケーションを選択し、 **[プロパティ]** を選択します。  

3. アプリケーションのプロパティで、 **[展開の種類]** タブに切り替えます。App-V の展開の種類を選択して、 **[編集]** を選択します。  

4. 展開の種類のプロパティで、 **[発行]** タブに切り替えます。発行する仮想アプリケーションの項目を選択します。  

5. **[OK]** を選択して、展開の種類のプロパティを閉じます。 その後、 **[OK]** を選択してアプリケーションのプロパティを閉じます。  

## <a name="import-an-application"></a><a name="bkmk_import"></a> アプリケーションをインポートする  

アプリケーションを Configuration Manager にインポートするには、次の手順を使用します。

1. Configuration Manager コンソールで、 **[ソフトウェア ライブラリ]** ワークスペースに移動し、 **[アプリケーション管理]** を展開して **[アプリケーション]** ノードを選択します。  

2. リボンの **[ホーム]** タブにある **[作成]** グループで、 **[アプリケーションのインポート]** を選択します。  

3. アプリケーションのインポート ウィザードの **[全般]** ページで、インポートする**ファイル**へのネットワーク パスを指定します。 たとえば、`\\server\share\file.zip` となります。 このファイルは、エクスポートされた Configuration Manager アプリケーションの有効な圧縮アーカイブ (ZIP 形式) です。  

4. **[ファイルのコンテンツ]** ページで、このアプリケーションが既存のアプリケーションと重複している場合に行う操作を選びます。 新しいアプリケーションを作成するか、重複を無視して既存のアプリケーションに新しいバージョンを追加します。  

5. **[概要]** ページで、操作を確認し、ウィザードを終了します。  

新しいアプリケーションは **[アプリケーション]** ノードに表示されます。  

> [!TIP]  
> Windows PowerShell コマンドレットの **Import-CMApplication** は、上の手順と同じ機能があります。 詳細については、「[Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps)」をご覧ください。  

アプリケーションのエクスポート方法の詳細については、[アプリケーションの管理タスク](management-tasks-applications.md)に関するページを参照してください。

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a> サポートされる展開の種類  

Configuration Manager では、アプリケーションに対して次の種類の展開がサポートされています。

| 展開の種類名 | [説明] |
|--------------------------|----------------------|  
| **Windows インストーラー (\*.msi ファイル)** | Windows インストーラー ファイル。 |  
| **Windows アプリケーション パッケージ (\*.appx、\*.appxbundle、\*.msix、\*.msixbundle)** | Windows アプリケーション パッケージ ファイル (.appx)、Windows アプリ バンドル パッケージ (.appxbundle)、Windows 10 アプリケーション パッケージ (.msix)、または Windows 10 アプリケーション バンドル (.msixbundle)。<!--1357427--> |  
| **Windows アプリケーション パッケージ (Windows ストア内)** | Windows ストア内のアプリへのリンクを指定するか、ストアでアプリを参照して選びます。<sup>[注 1](#bkmk_note1)</sup> |  
| **スクリプト インストーラー** | コンテンツをインストールするか操作を行うために、Windows クライアントで実行されるスクリプトまたはプログラムを指定します。 setup.exe インストーラー、またはスクリプト ラッパーでは、この展開の種類を使用します。 |  
| **Microsoft Application Virtualization 4** | Microsoft App-V v4 のマニフェスト。 |  
| **Microsoft Application Virtualization 5** | Microsoft App-V v5 パッケージ ファイル。 |  
| **Windows Phone アプリケーション パッケージ (\*.xap ファイル)** | Windows Phone アプリ パッケージ ファイル。 |  
| **Windows Phone アプリケーション パッケージ (Windows Phone ストア内)** | Windows ストア内のアプリへのリンクを指定します。 |  
| **Mac OS X** | 構成マネージャー クライアントが実行されている macOS コンピューターの場合。 **CMAppUtil** ツールを使用して、.cmmac ファイルを作成します。 |  
| **Web アプリケーション** | Web アプリケーションへのリンクを指定します。 この展開の種類では、ユーザーのデバイスに Web アプリケーションへのショートカットをインストールします。 |  
| **MDM を介した Windows インストーラー (\*.msi)** | Windows インストーラー ベースのアプリを作成し、Windows 10 デバイスに展開します。 詳細については、「[MDM 登録済みの Windows 10 デバイスに Windows インストーラー アプリを展開する](../get-started/creating-windows-applications.md#bkmk_mdm-msi)」を参照してください。 |
| **タスク シーケンス** | バージョン 2002 以降では、タスク シーケンスを使用して複雑なアプリケーションをインストールまたはアンインストールします。 詳細については、「[タスク シーケンスの展開の種類](../get-started/creating-windows-applications.md#bkmk_tsdt)」を参照してください。 <!--3555953--> |

> [!NOTE]
> Configuration Manager コンソールには、他の展開の種類が表示される場合がありますが、これらはサポートされなくなったプラットフォーム用です。 詳細については、「[ハイブリッド MDM はどうなりましたか?](../../mdm/understand/what-happened-to-hybrid.md)」を参照してください。

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a> 注 1:Windows アプリケーション パッケージ (Windows ストア内)

アプリを Windows ストアへのリンクとして展開するには、グループ ポリシーの **[ストア アプリケーションをオフにする]** を構成します。 このポリシーを **[無効]** または **[未構成]** に設定します。 この設定を有効にした場合、クライアントでは、アプリケーションのダウンロードとインストールを行うために Windows ストアに接続することができません。

Windows クライアントでは常に、ストアへのリンクを使用する展開の種類が他の展開の種類より前に評価されます。 その後、クライアントでは優先度順に展開の種類が評価されます。

> [!TIP]
> 一部のストア リンクでは、アプリケーションの作成ウィザードで次のエラーが発生することがあります: "アプリケーションが無効です"。 たとえば、一部のストアの*おすすめアプリ*で、このエラーが発生することがあります。 この場合でも、ウィザードの **[全般]** ページで **[次へ]** を選択できます。 Configuration Manager でアプリが正しく作成され、問題なく展開できます。<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>次のステップ

Configuration Manager でアプリケーションを作成した後、次のステップでは[アプリケーションを展開](deploy-applications.md)します。

バージョン 1906 以降では、1 つの展開としてユーザーまたはデバイス コレクションに送信できるアプリケーションのグループを作成します。 詳しくは、「[アプリケーション グループの作成](create-app-groups.md)」をご覧ください。

さまざまな OS プラットフォームでのアプリケーションの作成の詳細については、以下の記事を参照してください。  

- [Windows アプリケーションの作成](../get-started/creating-windows-applications.md)
- [Mac アプリケーションの作成](../get-started/creating-mac-computer-applications.md)
- [Linux および UNIX のサーバー アプリケーションの作成](../get-started/creating-linux-and-unix-server-applications.md)
- [Windows Embedded アプリケーションの作成](../get-started/creating-windows-embedded-applications.md)
