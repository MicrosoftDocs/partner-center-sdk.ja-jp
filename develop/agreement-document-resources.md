---
title: 契約ドキュメントのリソース
description: AgreementDocument リソースは、アグリーメントドキュメントを表します。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 233277daece48cebe434ea3f458fd98fe6436de7
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022602"
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

| プロパティ       | 種類   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | string | このドキュメントが適用される国または地域。 |
| language | string | このドキュメントがローカライズされる言語。 |
| displayUri | string | ブラウザーでアグリーメントドキュメントをプレビューするためのリンク。  |
| downloadUri |string | 契約ドキュメントをダウンロードするためのリンク (Microsoft Word 形式)。 |
