---
title: アグリーメントメタデータリソース
description: AgreementMetadata リソースコレクションは、パートナーが顧客の同意を確認するために使用できる契約の種類について説明します。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094585"
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
