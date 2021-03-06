---
title: Microsoft Intune での Windows 10 用の配信の最適化設定 - Azure | Microsoft Docs
description: Intune で管理する Windows 10 デバイスで配信の最適化を使用する方法を構成します。 Intune では、デバイス構成プロファイルを作成してインターネットから更新プログラムをインストールします。 また、既存の更新プログラム リングを配信の最適化プロファイルに置き換える方法についても確認します。
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 4d491a3210229d5dd6c74ccaed7f44c4ae4eb83c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990062"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Microsoft Intune での配信の最適化設定

Intune では、ご利用の Windows 10 デバイスに合わせて配信の最適化設定を使用することで、そのデバイスでアプリケーションおよび更新プログラムをダウンロードする際に消費される帯域幅が削減されます。 デバイスの構成プロファイルの一部として、配信の最適化を構成します。  

この記事では、デバイスの構成プロファイルの一部として配信の最適化の設定を構成する方法について説明します。 プロファイルを作成したら、次に、そのプロファイルをご利用の Windows 10 デバイスに割り当てるか、展開します。

Intune でサポートされる配信の最適化設定の一覧については、「[Intune 用の配信最適化の設定](delivery-optimization-settings.md)」を参照してください。  

Windows 10 での配信の最適化について学習するには、Windows ドキュメントの[配信の最適化更新プログラム](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization)に関するページを参照してください。  

## <a name="create-the-profile"></a>プロファイルの作成

1. [Microsoft Endpoint Manager 管理センター](https://go.microsoft.com/fwlink/?linkid=2109431)にサインインします。

2. **[デバイス]**  >  **[構成プロファイル]**  >  **[プロファイルの作成]** の順に選択します。

3. 次のプロパティを入力します。

   - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
   - **[プロファイル]** : **[配信の最適化]** を選択します。

4. **[作成]** を選択します。

5. **[Basics]\(基本\)** で次のプロパティを入力します。

   - **名前**:新しいプロファイルのわかりやすい名前を入力します。
   - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

6. **[次へ]** を選択します。

7. **[構成設定]** ページで、更新プログラムやアプリをダウンロードする方法を定義します。 使用可能な設定については、「[Intune 用の配信最適化の設定](delivery-optimization-settings.md)」を参照してください。

   設定の構成が完了したら、 **[次へ]** を選択します。

8. **[スコープ (タグ)]** タブで **[スコープ タグを選択]** を選択し、 *[タグを選択する]* ウィンドウを開いて、プロファイルにスコープ タグを割り当てます。
  
   **[次へ]** を選択して続行します。

9. **[割り当て]** ページで、このプロファイルを受け取るグループを選択します。 プロファイルの割り当ての詳細については、[ユーザーおよびデバイス プロファイルの割り当て](../configuration/device-profile-assign.md)に関するページを参照してください。

   **[次へ]** を選択します。

10. **[適用性ルール]** ページで、 **[ルール]** 、 **[プロパティ]** 、 **[値]** オプションを使用して、割り当てられたグループ内でこのプロファイルを適用する方法を定義します。

11. **[確認および作成]** ページで、完了したら、 **[作成]** を選択します。 プロファイルが作成され、一覧に表示されます。

次に各デバイスがチェックインするときに、ポリシーが適用されます。

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Windows 10 更新リングから配信の最適化を削除する

配信の最適化は、以前はソフトウェア更新リングの一部として構成されていました。 2019 年 2 月以降、配信の最適化設定は、配信の最適化デバイス構成プロファイルの一部として構成されます。これには、デバイスへのソフトウェア更新プログラムの配信よりも影響がある追加の設定が含まれています。 まだ行っていない場合は、配信の最適化設定を *[未構成]* に設定して更新リングから削除し、配信の最適化プロファイルを使用して、使用可能なオプションのより大きな範囲を管理します。

1. 配信の最適化のデバイス構成プロファイルを作成します。

    1. Microsoft Endpoint Manager 管理センターで、 **[デバイス]** 、 **[構成プロファイル]** 、 **[プロファイルの作成]** の順に選択します。
    2. 次のプロパティを入力します。

        - **[プラットフォーム]** : **[Windows 10 以降]** を選択します。
        - **[プロファイル]** : **[配信の最適化]** を選択します。

    3. **[作成]** を選択します。
    4. **[Basics]\(基本\)** で次のプロパティを入力します。

        - **名前**:新しいプロファイルのわかりやすい名前を入力します。
        - **説明**:プロファイルの説明を入力します。 この設定は省略可能ですが、推奨されます。

    5. **[次へ]** を選択します。
    6. **[構成設定]**  >  **[ダウンロード モード]** で、ご利用のデバイスに適用する設定を変更する必要が*ない限り*、既存のソフトウェア更新プログラム リングで使用されているものと同じモードを選択します。 次のようなオプションがあります。

        - **未構成**
        - **HTTP のみ、ピアリングなし**
        - **HTTP blended with peering behind the same NAT (HTTP と同じ NAT でのピアリングの組み合わせ)**
        - **HTTP blended with peering across a private group (HTTP とプライベート グループでのピアリングの組み合わせ)**
        - **HTTP とインターネット ピアリングの組み合わせ**
        - **ピアリングなしの簡易ダウンロード モード**
        - **バイパス モード**

    7. 管理する[追加の設定](delivery-optimization-settings.md)を構成し、プロファイルの作成を続行します。

        **[割り当て]** で、既存のソフトウェア更新プログラム リングと同じデバイスおよびユーザーに、この新しいプロファイルを割り当てます。 詳細については、[プロファイルの割り当て](device-profile-assign.md)に関するページを参照してください。

2. 既存のソフトウェアのリングの構成を解除します。

    1. Microsoft Endpoint Manager 管理センターで、 **[ソフトウェア更新]** 、[Windows 10 更新リング] の順に進みます。
    2. 一覧から更新プログラム リングを選択します。
    3. 設定で、 **[配信の最適化ダウンロード モード]** を **[未構成]** に設定します。
    4. **[Ok]**  >  変更を **[保存]** します。

## <a name="next-steps"></a>次のステップ

[プロファイルを割り当て](device-profile-assign.md)た後、[その状態を監視](device-profile-monitor.md)します。

Intune 用の[配信の最適化の設定](delivery-optimization-settings.md)を表示します。
