---
title: アグリーメントメタデータリソース
description: AgreementMetadata リソースコレクションは、パートナーが顧客の同意を確認するために使用できる契約の種類について説明します。
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
# <a name="agreement-metadata-resources"></a>アグリーメントメタデータリソース

適用対象:

- パートナー センター

**AgreementMetaData**リソースは、現在、 *Microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 このリソースは、以下には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**AgreementMetaData**コレクションは、すべてのアグリーメントの種類に関するメタデータを提供します。 パートナーは、このコレクションを使用して、契約に対する顧客の同意の確認を行うことができます。 現時点では、 **AgreementMetaData**コレクションは、1つのアグリーメントの種類 ( **Microsoft Cloud アグリーメント**) のメタデータのみを返します。

## <a name="agreementmetadata"></a>AgreementMetaData

返されるアグリーメントメタデータには、次のものが含まれます。

| プロパティ      | 種類               | 説明                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | アグリーメントテンプレートの一意識別子。                                       |
| type          | string             | 契約の種類。 現在サポートされている値は、 **microsoft の Cloudagreement**と**Microsoft の顧客契約**(プレビュー) です。 |
| agreementLink | string             | アグリーメントテンプレートの URL。                                                    |
