---
title: 顧客契約の直接の署名 (直接受け入れ) の状態。
description: DirectSignedCustomerAgreementStatus リソースは、顧客契約の直接の署名 (直接受け入れ) の状態を表します。
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 7575d5654cd8de9a65d4ee9ed484ff8cc0df2b0e
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022619"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>顧客契約の直接の署名 (直接受け入れ) の状態

**適用対象:**

- パートナー センター

**DirectSignedCustomerAgreementStatus**リソースは、現在、Microsoft パブリッククラウドのパートナーセンターでのみサポートされています。

このリソースは次のものには適用され*ません*。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**DirectSignedCustomerAgreementStatus**リソースは、顧客契約の直接同意の状態を表します。

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

**DirectSignedCustomerAgreementStatus**リソースには、次のプロパティが含まれています。

| プロパティ       | 種類   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| isSigned | boolean | カスタマーアグリーメントが顧客によって直接署名 (受け入れ) されているかどうかを示します。 |
