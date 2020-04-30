---
title: 顧客契約の直接の署名 (直接受け入れ) の状態。
description: DirectSignedCustomerAgreementStatus リソースは、顧客契約の直接の署名 (直接受け入れ) の状態を表します。
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 23397ab479f32879b00c04a817ef889221a6f091
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81665985"
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
