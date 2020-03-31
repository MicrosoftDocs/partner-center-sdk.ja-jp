---
title: 顧客契約の直接の署名 (直接受け入れ) の状態。
description: DirectSignedCustomerAgreementStatus リソースは、顧客契約の直接の署名 (直接受け入れ) の状態を表します。
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 539d395aa096632dd7e15edeb2b2c98035c191ca
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412462"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>顧客契約の直接の署名 (直接受け入れ) の状態

適用対象

- Partner Center

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
