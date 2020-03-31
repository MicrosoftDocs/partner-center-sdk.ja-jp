---
title: リソースのアップグレード
description: ソースサブスクリプションからターゲットサブスクリプションへのユーザーのアップグレードに使用されるリソースについて説明します。
ms.assetid: 869007B3-D6D4-4E79-B4F0-445CA5D88D2C
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d75d81dffbe30633038c03cec2cdf85e05536eb9
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414523"
---
# <a name="upgrade-resources"></a>リソースのアップグレード


**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

ソースサブスクリプションからターゲットサブスクリプションへのユーザーのアップグレードに使用されるリソースについて説明します。

## <a name="span-idupgradespan-idupgradespan-idupgradeupgrade"></a><span id="Upgrade"/><span id="upgrade"/><span id="UPGRADE"/>のアップグレード


個々のアップグレードリソースの動作について説明します。

| プロパティ      | 種類                   | 説明                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | プラン                  | ターゲットサブスクリプションのプラン。                                                        |
| UpgradeType   | string                 | アップグレードの種類としては、"none"、"upgrade\_only"、または "upgrade\_with\_license\_transfer" があります。         |
| isEligible    | boolean                | アップグレードを実行できるかどうかを識別します。                                                  |
| 数量      | 整数                | 購入する新しいプランの定量化。 既定値は、ソースサブスクリプションの数量です。 |
| UpgradeErrors | UpgradeErrors の配列 | 必要に応じて、アップグレードを実行できない理由。                                      |
| 属性    | ResourceAttributes     | アップグレードに対応するメタデータ属性。                                        |

 

## <a name="span-idupgradeerrorspan-idupgradeerrorspan-idupgradeerrorupgradeerror"></a><span id="UpgradeError"/><span id="upgradeerror"/><span id="UPGRADEERROR"/>UpgradeError


アップグレードを実行できない理由について説明します。

| プロパティ          | 種類               | 説明                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| コード              | string             | 問題に関連付けられているエラーコード: "その他の"、"委任された\_管理者\_アクセス許可\_無効"、"サブスクリプション\_ステータス\_がアクティブではありません"、"競合する\_サービス\_\_"、"ユーザー\_コンテキスト\_が必要"、"サブスクリプション\_\_\_を\_して\_\_\_\_アップグレード\_\_、"サブスクリプション\_ターゲット\_提供\_が見つかりませ\_ん"、または "サブスクリプション\_\_プロビジョニングされていません"。 |
| 説明       | string             | エラーを説明するわかりやすいテキスト。                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | string             | エラーに関する追加情報。                                                                                                                                                                                                                                                                                                                                                         |
| 属性        | ResourceAttributes | エラーに対応するメタデータ属性。                                                                                                                                                                                                                                                                                                                                             |

 

## <a name="span-idupgraderesultspan-idupgraderesultspan-idupgraderesultupgraderesult"></a><span id="UpgradeResult"/><span id="upgraderesult"/><span id="UPGRADERESULT"/>UpgradeResult


サブスクリプションのアップグレードプロセスの結果について説明します。

| プロパティ             | 種類                        | 説明                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | string                      | ソースサブスクリプションの識別子です。                                           |
| TargetSubscriptionID | string                      | ターゲットサブスクリプションの識別子です。                                           |
| UpgradeType          | string                      | アップグレードの種類としては、"none"、"upgrade\_only"、または "upgrade\_with\_license\_transfer" があります。 |
| UpgradeErrors        | UpgradeErrors の配列      | 必要に応じて、アップグレードの実行中に attemption 中にエラーが発生しました。           |
| LicenseErrors        | UserLicenseErrrors の配列 | ユーザーライセンスを移行しようとしたときにエラーが発生しました (該当する場合)。          |
| 属性           | ResourceAttributes          | ライセンスに対応するメタデータ属性。                                |

 

## <a name="span-iduserlicenseerrorspan-iduserlicenseerrorspan-iduserlicenseerroruserlicenseerror"></a><span id="UserLicenseError"/><span id="userlicenseerror"/><span id="USERLICENSEERROR"/>UserLicenseError


失敗したユーザーライセンスの譲渡に起因するエラーについて説明します。

| プロパティ     | 種類                   | 説明                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | string                 | ユーザーオブジェクトを識別する一意の。                                 |
| Name         | string                 | ユーザーの名前。                                                     |
| Email        | string                 | ユーザーの電子メール。                                                    |
| エラー       | ServiceFaults の配列 | ユーザーライセンスの転送を実行しようとしたときにスローされた例外の一覧。 |
| 属性   | ResourceAttributes     | ライセンスに対応するメタデータ属性。                     |

 

 

 




