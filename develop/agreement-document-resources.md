---
title: Agreement document resources
description: The AgreementDocument resource represents an agreement document.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9ac079822a2ddb45310148c16101fa25a38ec492
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488932"
---
# <a name="agreement-document-resources"></a>Agreement document resources

適用対象:

- パートナー センター

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource not applicable to:

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.

## <a name="agreementdocument"></a>AgreementDocument

An **AgreementDocument** resource includes the following properties:

| プロパティ       | タスクバーの検索ボックスに   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | string | The country or market to which this document applies. |
| 言語 | string | The language in which this document is localized. |
| displayUri | string | A link to preview the agreement document in a browser.  |
| downloadUri |string | A link to download the agreement document (in Microsoft Word format). |
