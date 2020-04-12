---
title: TransferEligibility リソース
description: パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡する必要がある場合に、転送を作成します。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 739631a4870268001c14f95490985ba18896e418
ms.sourcegitcommit: 4b1c10f91962861244c9349d5b9a9ba354b35b24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2020
ms.locfileid: "81220718"
---
# <a name="transfereligibility-resources"></a>TransferEligibility リソース

適用対象

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーは、顧客がパートナーとのサブスクリプションを別のパートナーに譲渡する必要がある場合に、転送を作成します。

## <a name="transfereligibility"></a>TransferEligibility

TransferEligibility について説明します。

| プロパティ              | 種類             | 説明                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | string           | 顧客のサブスクリプション識別子。                                                  |
| isEligible            | bool             | サブスクリプションが転送の対象であるかどうかを示します。                         |
| 原因                | string           | サブスクリプションが転送に適合しない場合は、ineligiblity を説明する理由。 |