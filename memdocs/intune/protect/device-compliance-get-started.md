---
title: Microsoft Intune - Azure のデバイス コンプライアンス ポリシー | Microsoft Docs
description: コンプライアンス ポリシーの設定や Microsoft Intune のデバイス コンプライアンス ポリシーなどの、コンプライアンス ポリシーの使用を開始します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 832ddbde9e3cf4782c7d3867ad6a09cc250960c7
ms.sourcegitcommit: e713f8f4ba2ff453031c9dfc5bfd105ab5d00cd9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86088328"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>コンプライアンス ポリシーを使用して、Intune で管理するデバイスのルールを設定する

Intune のようなモバイル デバイス管理 (MDM) ソリューションでは、組織のデータを保護するために、ユーザーやデバイスがいくつかの要件を満たすことを要求します。 Intune では、この機能は "*コンプライアンス ポリシー*" と呼ばれています。

Intune のコンプライアンス ポリシーとは次のようなものです。

- 準拠ユーザーおよびデバイスであるために満たす必要があるルールや設定を定義します。
- 非準拠のデバイスに適用されるアクションが含まれます。 非準拠に対するアクションにより、ユーザーに非準拠の条件を通知し、非準拠のデバイスでデータを保護することができます。
- [条件付きアクセスと組み合わせ](#integrate-with-conditional-access)、ルールを満たしておらず、非準拠の印が付けられたユーザーとデバイスをブロックできます。

  条件付きアクセスは、サードパーティ モバイル デバイス管理パートナーで管理しているデバイスからのコンプライアンスの状態データとも連動できます。 この機能を有効にするには、Azure AD と Intune の両方にパートナーのサポートを追加します。 詳細については、デバイス コンプライアンス パートナーのサポートを追加する方法に関するページを参照してください。 

Intune のコンプライアンス ポリシーには、次の 2 つの部分があります。

- **コンプライアンス ポリシー設定** – すべてのデバイスが受信する組み込みのコンプライアンス ポリシーのような、テナント全体の設定です。 コンプライアンス ポリシー設定では、デバイス コンプライアンス ポリシーを受信していないデバイスが準拠しているかどうかなど、Intune 環境でのコンプライアンス ポリシーの動作のベースラインを設定します。

- **デバイス コンプライアンス ポリシー** – 構成し、ユーザーまたはデバイスのグループに展開するプラットフォーム固有のルーです。  これらのルールは、最小オペレーティング システムやディスク暗号化の使用などの、デバイスの要件を定義します。 準拠したデバイスと見なされるには、これらの規則を満たす必要があります。

他の Intune ポリシーと同様に、デバイスのコンプライアンス ポリシーの評価は、デバイスが Intune にチェックインするタイミングと、[ポリシーとプロファイルの更新サイクル](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned)によって異なります。

## <a name="compliance-policy-settings"></a>コンプライアンス ポリシーの設定

*コンプライアンス ポリシー設定* は、Intune のコンプライアンス サービスがデバイスとどのように対話するかを決定する、テナント全体の設定です。 これらの設定は、デバイス コンプライアンス ポリシーで構成する設定とは異なります。

コンプライアンス ポリシーの設定を管理するには、[Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインし、 **[エンドポイント セキュリティ]**  >  **[デバイスのポリシー準拠]**  >  **[コンプライアンス ポリシー設定]** の順に移動します。

コンプライアンス ポリシー設定には、次の設定が含まれます。

- **[コンプライアンス ポリシーが割り当てられていないデバイスをマークする]**

  この設定は、デバイス コンプライアンス ポリシーが割り当てられていないデバイスを Intune がどのように処理するかを決定します。 この設定には次の 2 つの値があります。
  - **準拠** ("*既定値*"): このセキュリティ機能はオフになっています。 デバイス コンプライアンス ポリシーが送信されていないデバイスは "*準拠*" と見なされます。
  - **準拠していない**: このセキュリティ機能はオンになっています。 デバイス コンプライアンス ポリシーが受信されていないデバイスは、準拠していないと見なされます。

  デバイス コンプライアンス ポリシーで条件付きアクセスを使用する場合は、この設定を "**準拠していない**" に変更して、準拠していると確認されたデバイスのみがリソースにアクセスできるようにすることをお勧めします。

  ポリシーが割り当てられていないためにエンド ユーザーが準拠していない場合、[ポータル サイト アプリ](../apps/company-portal-app.md)には [コンプライアンス ポリシーが割り当てられていません] と表示されます。

- **[脱獄の高度な検出]** (*iOS/iPadOS のみに適用*)

  この設定は、脱獄されたデバイスをブロックするデバイス コンプライアンス ポリシーの対象となるデバイスでのみ動作します。  (iOS/iPadOS の [[デバイスの正常性](compliance-policy-create-ios.md#device-health)] 設定を参照してください)。

  この設定には次の 2 つの値があります。

  - **無効** (*既定値*): このセキュリティ機能はオフになっています。 この設定は、脱獄されたデバイスをブロックするデバイス コンプライアンス ポリシーを受信するデバイスには影響しません。
  - **有効**: このセキュリティ機能はオンになっています。 脱獄されたデバイスをブロックするデバイス コンプライアンス ポリシーを受信するデバイスは、[脱獄の高度な検出] を使用します。

  適用可能な iOS/iPadOS デバイスで有効になっている場合、デバイスは次を実行します。

  - OS レベルで位置情報サービスを有効にします。
  - ポータル サイトで常に位置情報サービスを使用できるようにします。
  - 位置情報サービスを使用して、バックグラウンドで脱獄の検出をより頻繁にトリガーします。 ユーザーの場所データは Intune では保存されません。

  [脱獄の高度な検出] では、次の場合に評価を実行します。

  - ポータル サイト アプリが開いている
  - デバイスが約 500 メートル以上の距離を物理的に大きく移動している。 位置が大幅に変わるごとに確実に脱獄検出チェックを実行することは、その時点のデバイスのネットワーク接続に依存するため、Intune では保証できません。

  iOS 13 以降でこの機能を使用するには、ポータル サイトによるバックグラウンドでの位置の使用を引き続き許可することを確認するメッセージがデバイスから表示されるたびに、"*常に許可*" を選択する必要があります。 ユーザーが位置へのアクセスを常に許可せず、この設定が構成されたポリシーが適用されている場合、そのデバイスは非準拠としてマークされます。

- **[コンプライアンス状態の有効期間 (日)]**

  受信したすべてのコンプライアンス ポリシーについて、デバイスが正常に報告する必要がある期間を指定します。 有効期限が切れる前にデバイスがポリシーのコンプライアンス状態を報告できなかった場合、デバイスは非準拠として扱われます。

  既定では、期間は 30 日に設定されます。 1 日から 120 日の期間を構成できます。

  有効期間の設定に、デバイスのコンプライアンスの詳細を表示できます。 [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインし、 **[デバイス]**  >  **[監視]**  >  **[コンプライアンスの設定]** の順に移動します。 この設定の名前は、 *[設定]* 列の **[アクティブ]** の名前です。  この情報および関連するコンプライアンス状態ビューの詳細については、「[デバイス コンプライアンスを監視する](compliance-policy-monitor.md)」を参照してください。

## <a name="device-compliance-policies"></a>デバイス コンプライアンス ポリシー

Intune のデバイス コンプライアンス ポリシーは次を行います。

- 準拠ユーザーおよびマネージド デバイスであるために満たす必要があるルールや設定を定義します。 ルールの例として、デバイスで最小 OS バージョンを実行している必要があります。また、脱獄されたりルート化されたりしておらず、Intune と統合されている脅威管理ソフトウェアで指定された "*脅威レベル*" を超えていない必要があります。
- コンプライアンス ルールを満たしていないデバイスに適用されるアクションをサポートします。 アクションの例として、リモートでのロックや、デバイスの状態に関する電子メールをデバイスのユーザーに送信して修正できるようにする、などがあります。
- ユーザー グループ内のユーザー、またはデバイス グループ内のデバイスに展開します。 コンプライアンス ポリシーがユーザーに展開されると、すべてのユーザーのデバイスのコンプライアンスがチェックされます。 このシナリオでのデバイス グループの使用は、コンプライアンス レポートに役立ちます。

条件付きアクセスを使用する場合、条件付きアクセス ポリシーはデバイスのコンプライアンス結果を使用して、準拠していないデバイスからのリソースへのアクセスをブロックできます。

デバイス コンプライアンス ポリシーで指定できる設定は、ポリシーの作成時に選択したプラットフォームの種類によって異なります。 デバイス プラットフォームごとに異なる設定がサポートされており、プラットフォームの種類ごとに個別のポリシーが必要です。  

次の項目は、デバイスの構成ポリシーのさまざまな側面に特化した記事にリンクしています。

- [**非準拠に対するアクション**](actions-for-noncompliance.md) - 各デバイス コンプライアンス ポリシーには、非準拠に対するアクションが 1 つ以上含まれています。 これらのアクションは、ポリシーで設定した条件を満たしていないデバイスに適用されるルールです。

  既定では、各デバイス コンプライアンス ポリシーには、ポリシー ルールに適合しない場合にデバイスを非準拠としてマークするアクションが含まれます。 その後、ポリシーは、そのアクションに対して設定したスケジュールに基づいて、構成済みの非準拠に対する追加アクションをデバイスに適用します。

  非準拠に対するアクションは、デバイスが準拠していない場合にユーザーに警告したり、デバイス上のデータを保護したりするのに役立ちます。 アクションの例を次に示します。

  - 非準拠デバイスに関する詳細情報が含まれているユーザーおよびグループに**電子メール アラートを送信します**。 非準拠とマークされた直後に電子メールを送信し、デバイスが準拠状態になるまで定期的に電子メールを送信するポリシーを構成することができます。
  - しばらくの間準拠していない**デバイスをリモートでロックします**。
  - しばらくの間準拠していない**デバイスを廃止します**。 このアクションにより、Intune 管理からデバイスが削除され、デバイスからすべての会社データが削除されます。

- [**ネットワークの場所の構成**](use-network-locations.md) - Android デバイスでサポートされています。"*ネットワークの場所*" を構成してその場所をデバイス コンプライアンス ルールとして使用することができます。 この種類のルールでは、デバイスが指定したネットワークの外部にある場合や、ネットワークから退出する場合に、デバイスに非準拠のフラグを設定できます。 場所のルールを指定する前に、ネットワークの場所を構成する必要があります。

- [**ポリシーの作成**](create-compliance-policy.md) – この記事の情報を参考にして前提条件を確認し、オプションを設定してルールを構成し、非準拠に対するアクションを指定して、ポリシーをグループに割り当てることができます。 この記事には、ポリシーの更新時間に関する情報も含まれています。

  さまざまなデバイス プラットフォームでのデバイスのコンプライアンス設定を参照してください。

  - [Android](compliance-policy-create-android.md)
  - [Android エンタープライズ](compliance-policy-create-android-for-work.md)
  - [Android](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 以降](compliance-policy-create-windows-8-1.md)
  - [Windows 10 以降](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>コンプライアンス状態を監視する

Intune には、デバイスのコンプライアンス状態を監視し、ポリシーとデバイスの詳細を確認できるデバイス コンプライアンス ダッシュボードが含まれています。 このダッシュボードの詳細については、[デバイス コンプライアンスの監視](compliance-policy-monitor.md)に関する記事を参照してください。

## <a name="integrate-with-conditional-access"></a>条件付きアクセスと統合する

条件付きアクセスを使用する場合は、デバイス コンプライアンス ポリシーの結果を使用するための条件付きアクセス ポリシーを構成して、組織のリソースにアクセスできるデバイスを決定できます。 このアクセスの制御は、デバイス コンプライアンス ポリシーに含める非準拠に対するアクションとは別のものとして追加されます。

デバイスが Intune に登録されると Azure AD に登録されます。 デバイスのコンプライアンス状態が Azure AD に報告されます。 条件付きアクセス ポリシーのアクセスの制御が "*Require device to be marked as compliant\(デバイスは準拠としてマーク済みである必要があります\)* " に設定されている場合、条件付きアクセスでは、そのコンプライアンス状態を使用して、電子メールやその他の組織のリソースへのアクセスを許可するかブロックするかを決定します。

条件付きアクセス ポリシーが設定されたデバイスのコンプライアンス状態を使用する場合は、テナントで "*コンプライアンス ポリシーが割り当てられていないデバイスをマークする*" がどのように構成されているかを確認します。これは [[コンプライアンス ポリシー設定]](#compliance-policy-settings) で管理します。

デバイス コンプライアンス ポリシーが設定された条件付きアクセスを使用する方法の詳細については、「[デバイスベースの条件付きアクセス](conditional-access-intune-common-ways-use.md#device-based-conditional-access)」を参照してください

次の Azure AD のドキュメントで条件付きアクセスの詳細を参照してください。

- [条件付きアクセスとは](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [デバイス ID とは](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>さまざまなプラットフォームでの非準拠と条件付きアクセスに関するリファレンス

次の表では、条件付きアクセス ポリシーとコンプライアンス ポリシーを使用する場合に非準拠設定をどのように管理するかについて説明しています。

- **修復**: デバイス オペレーティング システムによってコンプライアンスが適用されます。 たとえば、ユーザーは PIN を設定するように強制されます。

- **検疫済み**: デバイス オペレーティング システムによってコンプライアンスは適用されません。 たとえば、Android デバイスと Android エンタープライズ デバイスでは、ユーザーはデバイスの暗号化を強制されません。 デバイスが準拠していない場合、次のアクションが行われます。
  - ユーザーに条件付きアクセス ポリシーを適用すると、デバイスがブロックされます。
  - ポータル サイト アプリでは、コンプライアンスの問題についてユーザーに通知します。

---------------------------

|**ポリシー設定**| **プラットフォーム** |
| --- | ----|
| **PIN またはパスワードの構成** | - **Android 4.0 以降**: 検疫済み<br>- **Samsung KNOX Standard 4.0 以降**: 検疫済み<br>- **Android エンタープライズ**: 検疫済み  <br>  <br>- **iOS 8.0 以降**: 修復<br>- **macOS 10.11 以降**: 修復  <br>  <br>- **Windows 8.1 以降**: 修復<br>- **Windows Phone 8.1 以降**: 修復|
| **デバイスの暗号化** | - **Android 4.0 以降**: 検疫済み<br>- **Samsung KNOX Standard 4.0 以降**: 検疫済み<br>- **Android エンタープライズ**: 検疫済み<br><br>- **iOS 8.0 以降**: 修復 (PIN の設定による)<br>- **macOS 10.11 以降**: 修復 (PIN の設定による)<br><br>- **Windows 8.1 以降**: 適用できません<br>- **Windows Phone 8.1 以降**: 修復 |
| **脱獄またはルート化されたデバイス** | - **Android 4.0 以降**: 検疫済み (設定ではありません)<br>- **Samsung KNOX Standard 4.0 以降**: 検疫済み (設定ではありません)<br>- **Android エンタープライズ**: 検疫済み (設定ではありません)<br><br>- **iOS 8.0 以降**: 検疫済み (設定ではありません)<br>- **macOS 10.11 以降**: 適用できません<br><br>- **Windows 8.1 以降**: 適用できません<br>- **Windows Phone 8.1 以降**: 適用できません |
| **電子メールのプロファイル** | - **Android 4.0 以降**: 適用できません<br>- **Samsung KNOX Standard 4.0 以降**: 適用できません<br>- **Android エンタープライズ**: 適用できません<br><br>- **iOS 8.0 以降**: 検疫済み<br>- **macOS 10.11 以降**: 検疫済み<br><br>- **Windows 8.1 以降**: 適用できません<br>- **Windows Phone 8.1 以降**: 適用できません |
| **最小 OS バージョン** | - **Android 4.0 以降**: 検疫済み<br>- **Samsung KNOX Standard 4.0 以降**: 検疫済み<br>- **Android エンタープライズ**: 検疫済み<br><br>- **iOS 8.0 以降**: 検疫済み<br>- **macOS 10.11 以降**: 検疫済み<br><br>- **Windows 8.1 以降**: 検疫済み<br>- **Windows Phone 8.1 以降**: 検疫済み |
| **最大 OS バージョン** | - **Android 4.0 以降**: 検疫済み<br>- **Samsung KNOX Standard 4.0 以降**: 検疫済み<br>- **Android エンタープライズ**: 検疫済み<br><br>- **iOS 8.0 以降**: 検疫済み<br>- **macOS 10.11 以降**: 検疫済み<br><br>- **Windows 8.1 以降**: 検疫済み<br>- **Windows Phone 8.1 以降**: 検疫済み |
| **Windows 正常性構成証明書** | - **Android 4.0 以降**: 適用できません<br>- **Samsung KNOX Standard 4.0 以降**: 適用できません<br>- **Android エンタープライズ**: 適用できません<br><br>- **iOS 8.0 以降**: 適用できません<br>- **macOS 10.11 以降**: 適用できません<br><br>- **Windows 10 および Windows 10 Mobile**: 検疫済み<br>- **Windows 8.1 以降**: 検疫済み<br>- **Windows Phone 8.1 以降**: 適用できません |

---------------------------

## <a name="next-steps"></a>次のステップ

- Android デバイスで使用するために[場所を構成する](../protect/use-network-locations.md)
- [ポリシーを作成して展開](../protect/create-compliance-policy.md)し、前提条件を確認する
- [デバイス コンプライアンスを監視する](../protect/compliance-policy-monitor.md)
- [Microsoft Intune でのデバイス ポリシーとプロファイルの一般的な質問、イシューと解決策](../configuration/device-profile-troubleshoot.md)
- 「[ポリシー エンティティのリファレンス](../developer/reports-ref-policy.md)」には、Intune データ ウェアハウス ポリシー エンティティに関する情報が含まれます
