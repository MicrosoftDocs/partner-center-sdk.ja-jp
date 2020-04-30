---
title: TransferEligibility リソース
description: パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡することを希望する場合に転送を作成します。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cb0ba6a4ff0daf6fa3ed04561aeb997822b5bc2b
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124320"
---
# <a name="transfereligibility-resources"></a>TransferEligibility リソース

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡することを希望する場合に転送を作成します。

## <a name="transfereligibility"></a>TransferEligibility

TransferEligibility について説明します。

| プロパティ              | Type             | 説明                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | string           | 顧客のサブスクリプション識別子。                                                  |
| isEligible            | [bool]             | サブスクリプションが転送の対象であるかどうかを示します。                         |
| 理由                | string           | Reason プロパティは、サブスクリプションが譲渡に適合していない理由を示します。 |