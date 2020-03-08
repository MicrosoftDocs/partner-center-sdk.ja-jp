---
title: アグリーメントメタデータリソース
description: AgreementMetadata リソースコレクションは、パートナーが顧客の同意を確認するために使用できる契約の種類について説明します。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7ba318054d9df22023564fe3796833e49f87282e
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78899652"
---
# <a name="agreement-metadata-resources"></a>アグリーメントメタデータリソース

適用対象

- Partner Center

**AgreementMetaData**リソースは、現在、 *Microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 このリソースは、以下には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**AgreementMetaData**コレクションは、すべてのアグリーメントの種類に関するメタデータを提供します。 パートナーは、このコレクションを使用して、契約に対する顧客の同意の確認を行うことができます。 **AgreementMetaData**コレクションは、両方のアグリーメントの種類 (**Microsoft Cloud Agreement**と**Microsoft Customer agreement**) のメタデータを返します。

## <a name="agreementmetadata"></a>AgreementMetaData

返されるアグリーメントメタデータには、次のものが含まれます。

| プロパティ      | 種類               | 説明                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | アグリーメントテンプレートの一意識別子。                                       |
| 型          | string             | 契約の種類。 現在サポートされている値は、 **microsoft の Cloudagreement**と**Microsoft の顧客契約**(プレビュー) です。 |
| agreementLink | string             | アグリーメントテンプレートの URL。                                                    |
