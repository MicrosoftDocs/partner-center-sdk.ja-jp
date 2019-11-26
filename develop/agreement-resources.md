---
title: Agreement resources
description: The Agreement resource represents a Microsoft cloud customer agreement.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2cf620d63da14e014a17017006346f80a7a3fe4c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489262"
---
# <a name="agreement-resources"></a>Agreement resources

適用対象:

- パートナー センター

The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. 以下には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

The **Agreement** resource represents a Microsoft cloud customer agreement.

## <a name="agreement"></a>契約

The **Agreement** resource represents the details of certification provided by the partner.

| プロパティ       | タスクバーの検索ボックスに   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | string                         | Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization. When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.                                                                             |
| primaryContact | [Contact](./utility-resources.md#contact) | Information about the user from the customer organization that accepted the Microsoft Cloud Agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional). |
| dateAgreed     | string in UTC date time format | The date when the customer accepted the agreement.                                 |
| templateId     |string                          | Unique identifier of the agreement that the customer accepted. |
| type           |string                          | Agreement type. Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.|
| agreementLink  | string                         | URL for the agreement template.                                                    |
