---
title: デバイスを登録した場合に会社が確認できる情報
description: IT 部門でマネージド デバイスについて確認できることとできないことについて説明します。
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/11/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: 740d9b68a0101e04e6bf690d09ecce7eaff4509e
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107326"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>デバイスを登録した場合に組織が確認できる情報

Microsoft Intune にデバイスを登録しても、組織はユーザーの個人情報を閲覧できません。 デバイスを登録すると、デバイスのモデルやシリアル番号など、デバイスに関する特定の情報を閲覧するアクセス許可が組織に付与されます。 組織はこの情報を使用して、デバイス上の会社データを保護します。

**組織が閲覧できない情報:**

- 通話と Web 閲覧の履歴
- 電子メールとテキスト メッセージ
- 連絡先
- 予定表
- パスワード
- フォト アプリやカメラ ロールの内容を含む、画像
- ファイル

**組織が常に閲覧できる情報:**

- デバイス モデル (例: Google Pixel)
- デバイスの製造元 (例: Microsoft)
- オペレーティング システムとバージョン (例: iOS 12.0.1)
- アプリ インベントリとアプリの名前 (Microsoft Word など)。 個人用デバイス上では、組織はマネージド アプリ インベントリのみを閲覧できます。 会社が所有しているデバイスでは、組織はすべてのアプリ インベントリを閲覧できます。
- デバイスの所有者
- デバイス名
- デバイスのシリアル番号
- IMEI

 > [!NOTE]
 > Android Enterprise のフル マネージド専用デバイスの場合、すべてのアプリ インベントリを表示することはできません。
 
 > [!NOTE]
 > アプリは、次のいずれかの方法でインストールされると、**マネージド アプリ**と見なされます。
 > 1. ユーザーが、Intune 管理者によって**利用可能**として公開された後、ポータル サイト アプリからインストールする。
 > 2. アプリは、Intune 管理者によって**必須**として公開され、デバイスにインストールされている。 
 >
 > 組織の IT 管理者またはサポート担当者であり、Intune でのアプリ管理に関する詳細情報が必要な場合は、「[管理されていないアプリ、マネージド アプリ、MAM アプリの機能について理解する](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/understanding-the-capabilities-of-unmanaged-apps-managed-apps/ba-p/249164)」を参照してください。
    
**組織が閲覧できる可能性がある情報:**

- 電話番号:会社所有のデバイスの場合、ユーザーの完全な電話番号を確認できます。 個人所有のデバイスの場合、組織が確認できるのは、ユーザーの電話番号の最後の 4 桁のみです。 個々のデバイスの所有権の種類は、 **[デバイスの詳細]** ページで確認できます。
- デバイスの記憶域スペース: 必要なアプリをインストールできない場合、組織がユーザーのデバイスの記憶域の容量を確認し、容量が少なすぎるかどうかを判断することがあります。  
- 場所:会社が所有しているデバイスの場合、組織は紛失したデバイスの場所を確認できます。 個人が所有しているデバイスの場合、紛失した監視対象の iOS デバイスを見つけようとしない限り、組織はデバイスの場所を確認することはできません。 監視対象のデバイスに関する詳細については、[Apple iOS のドキュメント](https://go.microsoft.com/fwlink/?linkid=853816)を確認してください。  
- アプリ インベントリの詳細:組織が Mobile Threat Defense を使用している場合、ユーザーの iOS デバイス上にあるアプリの詳細を閲覧することができます。 Mobile Threat Defense の詳細については、[こちら](set-up-mobile-threat-defense.md)をご覧ください。 それ以外の場合、個人が所有しているデバイスでは、組織はマネージド アプリ インベントリのみを確認できます。 会社が所有しているデバイスでは、組織はすべてのアプリ インベントリを確認できます。
- ネットワーク情報: Android デバイスのネットワーク接続情報の一部は、組織のサポートが入手できる場合があります。 たとえば、デバイスを特定の建物内に維持するように組織が定めている場合、デバイスでは接続先のネットワークが識別されます。 
