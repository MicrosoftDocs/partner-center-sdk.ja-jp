---
title: 監査操作
description: 監査操作を使用して、パートナーセンターのアクティビティのレコードを取得します。
ms.assetid: C6337A08-6009-4F12-A7A3-B1CA1AE016A1
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 36b20d41d3313a1151c45177f4c74ed0b44b180d
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413224"
---
# <a name="audit-operations"></a>監査操作

パートナーセンターの Api は、パートナーセンターのアクティビティの記録を取得できるように、監査機能を提供します。

過去30日間の監査レコードを現在の日付から取得することも、開始日または終了日を含めることによって指定された日付範囲について取得することもできます。 ただし、パフォーマンス上の理由から、アクティビティログデータの可用性は過去90日間に制限されていることに注意してください。 現在の日付より前の開始日が90日を超える要求は、無効な要求例外 (エラーコード: 400) と適切なメッセージを受け取ります。

## <a name="retrieve-audit-records"></a>監査レコードの取得

パートナーのユーザーまたはアプリケーションによって実行される操作の詳細な監査レコードを取得します。

- [パートナー センター アクティビティのレコードを取得する](get-a-record-of-partner-center-activity-by-user.md)
- [リソースの監査](auditing-resources.md)