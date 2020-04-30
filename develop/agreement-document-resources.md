---
title: 契約ドキュメントのリソース
description: AgreementDocument リソースは、アグリーメントドキュメントを表します。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 21035d465094ab306d65ce3f24a006a97bf96354
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81665158"
---
# <a name="agreement-document-resources"></a>契約ドキュメントのリソース

**適用対象:**

- パートナー センター

**AgreementDocument**リソースは、現在、 *Microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 このリソースは、次には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**AgreementDocument**リソースは、プレビューとダウンロードに使用できる Microsoft agreement ドキュメントを表します。

## <a name="agreementdocument"></a>AgreementDocument

**AgreementDocument**リソースには、次のプロパティが含まれています。

| プロパティ       | Type   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | string | このドキュメントが適用される国または地域。 |
| language | string | このドキュメントがローカライズされる言語。 |
| displayUri | string | ブラウザーでアグリーメントドキュメントをプレビューするためのリンク。  |
| downloadUri |string | 契約ドキュメントをダウンロードするためのリンク (Microsoft Word 形式)。 |
