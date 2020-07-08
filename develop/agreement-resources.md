---
title: 契約リソース
description: アグリーメントリソースは、Microsoft cloud customer Agreement を表します。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 742436648079ca0870400b6fb305138226d1de5c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095873"
---
# <a name="agreement-resources"></a>契約リソース

**適用対象:**

- パートナー センター

**アグリーメント**リソースは、現在、Microsoft パブリッククラウドのパートナーセンターでのみサポートされています。 次の場合には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**アグリーメント**リソースは、Microsoft cloud customer Agreement を表します。

## <a name="agreement"></a>契約

**アグリーメント**リソースは、パートナーによって提供される認定の詳細を表します。

| プロパティ       | Type   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | string                         | パートナー組織の代わりに確認を提供する、パートナーテナント内のログインユーザーのオブジェクト識別子。 アプリ + ユーザー認証を使用してアグリーメントリソースを作成する場合、パートナーセンターは自動的に、アプリ + ユーザートークンから**userId**属性の値を取得します。                                                                             |
| primaryContact | [Contact](./utility-resources.md#contact) | 契約に同意した顧客組織からのユーザーに関する情報。たとえば、 **firstName**、 **lastName**、 **email**、 **phoneNumber** (省略可能) です。 |
| dateAgreed     | UTC 日時形式の文字列 | 顧客が契約に同意した日付。                                 |
| templateId     |string                          | 顧客が同意したアグリーメントの一意識別子。 |
| type           |string                          | 契約の種類。 現在サポートされている値は、 **microsoft の cloudagreement**と**Microsoft の顧客契約**です。|
| agreementLink  | string                         | アグリーメントテンプレートの URL。                                                    |
