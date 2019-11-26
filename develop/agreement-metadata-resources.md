---
title: Agreement metadata resources
description: The AgreementMetadata resource collection describes agreement types that partners can use to provide confirmation of customer acceptance.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b147b44d4f4c1d986f7e3290c71ddbf0af54de70
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488712"
---
# <a name="agreement-metadata-resources"></a>Agreement metadata resources

適用対象:

- パートナー センター

The **AgreementMetaData** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource isn't applicable to:

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

The **AgreementMetaData** collection provides metadata about all the agreement types. Partners can use this collection to provide confirmation of customer acceptance of agreements. Currently, the **AgreementMetaData** collection only returns metadata for one agreement type, which is the **Microsoft Cloud Agreement**.

## <a name="agreementmetadata"></a>AgreementMetaData

Agreement metadata returned includes the following:

| プロパティ      | タスクバーの検索ボックスに               | 説明                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | Unique identifier of an agreement template.                                       |
| type          | string             | Agreement type. Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview). |
| agreementLink | string             | URL for the agreement template.                                                    |
