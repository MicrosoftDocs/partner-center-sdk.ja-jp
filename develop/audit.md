---
title: 操作を監査する
description: 監査操作を使用して、パートナーセンターのアクティビティのレコードを取得します。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e31990df06a67d4f02b97dab8422ee498a09b43
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095399"
---
# <a name="audit-operations"></a>操作を監査する

パートナーセンターの Api は、パートナーセンターのアクティビティの記録を取得できるように、監査機能を提供します。

過去30日間の監査レコードを現在の日付から取得することも、開始日または終了日を含めることによって指定された日付範囲について取得することもできます。 ただし、パフォーマンス上の理由から、アクティビティログデータの可用性は過去90日間に制限されていることに注意してください。 現在の日付より前の開始日が90日を超える要求は、無効な要求例外 (エラーコード: 400) と適切なメッセージを受け取ります。

## <a name="retrieve-audit-records"></a>監査レコードの取得

パートナーのユーザーまたはアプリケーションによって実行される操作の詳細な監査レコードを取得します。

- [パートナー センター アクティビティのレコードを取得する](get-a-record-of-partner-center-activity-by-user.md)
- [リソースの監査](auditing-resources.md)