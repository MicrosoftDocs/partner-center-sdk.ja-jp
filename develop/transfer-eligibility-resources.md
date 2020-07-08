---
title: TransferEligibility リソース
description: パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡することを希望する場合に転送を作成します。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095985"
---
# <a name="transfereligibility-resources"></a>TransferEligibility リソース

**適用対象:**

- パートナー センター

パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡することを希望する場合に転送を作成します。

## <a name="transfereligibility"></a>TransferEligibility

TransferEligibility について説明します。

| プロパティ              | Type             | 説明                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | string           | 顧客のサブスクリプション識別子。                                                  |
| isEligible            | [bool]             | サブスクリプションが転送の対象であるかどうかを示します。                         |
| 理由                | string           | Reason プロパティは、サブスクリプションが譲渡に適合していない理由を示します。 |