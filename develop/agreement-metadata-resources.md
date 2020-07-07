---
title: アグリーメントメタデータリソース
description: AgreementMetadata リソースコレクションは、パートナーが顧客の同意を確認するために使用できる契約の種類について説明します。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 642c3d079020d423db48aa8d3e1c0c1e12280fe3
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022608"
---
# <a name="agreement-metadata-resources"></a>アグリーメントメタデータリソース

**適用対象:**

- パートナー センター

**AgreementMetaData**リソースは、現在、 *Microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 このリソースは、以下には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**AgreementMetaData**コレクションは、すべてのアグリーメントの種類に関するメタデータを提供します。 パートナーは、このコレクションを使用して、契約に対する顧客の同意の確認を行うことができます。 **AgreementMetaData**コレクションは、両方のアグリーメントの種類 (**Microsoft Cloud Agreement**と**Microsoft Customer agreement**) のメタデータを返します。

## <a name="agreementmetadata"></a>AgreementMetaData

返されるアグリーメントメタデータには、次のプロパティが含まれます。

| プロパティ      | 種類               | 説明                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | アグリーメントテンプレートの一意識別子。                                       |
| 型          | string             | 契約の種類。 現在サポートされている値は、 **microsoft の Cloudagreement**と**Microsoft の顧客契約**(プレビュー) です。 |
| agreementLink | string             | アグリーメントテンプレートの URL。                                                    |
