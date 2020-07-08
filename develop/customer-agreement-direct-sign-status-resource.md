---
title: 顧客契約の直接の署名 (直接受け入れ) の状態。
description: DirectSignedCustomerAgreementStatus リソースは、顧客契約の直接の署名 (直接受け入れ) の状態を表します。
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094311"
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

| プロパティ       | Type   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| isSigned | boolean | カスタマーアグリーメントが顧客によって直接署名 (受け入れ) されているかどうかを示します。 |
