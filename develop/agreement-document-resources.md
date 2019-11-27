---
title: 契約ドキュメントのリソース
description: AgreementDocument リソースは、アグリーメントドキュメントを表します。
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
# <a name="agreement-document-resources"></a>契約ドキュメントのリソース

適用対象:

- パートナー センター

**AgreementDocument**リソースは、現在、 *Microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 このリソースは、次には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**AgreementDocument**リソースは、プレビューとダウンロードに使用できる Microsoft agreement ドキュメントを表します。

## <a name="agreementdocument"></a>AgreementDocument

**AgreementDocument**リソースには、次のプロパティが含まれています。

| プロパティ       | 種類   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | string | このドキュメントが適用される国または地域。 |
| 言語 | string | このドキュメントがローカライズされる言語。 |
| displayUri | string | ブラウザーでアグリーメントドキュメントをプレビューするためのリンク。  |
| downloadUri |string | 契約ドキュメントをダウンロードするためのリンク (Microsoft Word 形式)。 |
