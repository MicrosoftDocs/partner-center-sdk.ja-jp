---
title: アグリーメントメタデータリソース
description: AgreementMetadata リソースコレクションは、パートナーが顧客の同意を確認するために使用できる契約の種類について説明します。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: ccc726a74ca17082576b53c2b1edba085a1610bc
ms.sourcegitcommit: 685137f5dd204912efcb4c406a1bf02278ce5dae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81785121"
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

| プロパティ      | Type               | 説明                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | アグリーメントテンプレートの一意識別子。                                       |
| type          | string             | 契約の種類。 現在サポートされている値は、 **microsoft の Cloudagreement**と**Microsoft の顧客契約**(プレビュー) です。 |
| agreementLink | string             | アグリーメントテンプレートの URL。                                                    |
