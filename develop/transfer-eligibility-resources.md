---
title: TransferEligibility リソース
description: パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡することを希望する場合に転送を作成します。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 32ea176b079c48d7c48d114f6cfc96468699928f
ms.sourcegitcommit: e39e8dccf25020cccda8bcea83b72e7ef8a6a7c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84489189"
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
| isEligible            | bool             | サブスクリプションが転送の対象であるかどうかを示します。                         |
| 理由                | string           | Reason プロパティは、サブスクリプションが譲渡に適合していない理由を示します。 |