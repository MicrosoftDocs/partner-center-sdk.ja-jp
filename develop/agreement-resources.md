---
title: 契約リソース
description: アグリーメントリソースは、Microsoft cloud customer Agreement を表します。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2cf620d63da14e014a17017006346f80a7a3fe4c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489262"
---
# <a name="agreement-resources"></a>契約リソース

適用対象:

- パートナー センター

**アグリーメント**リソースは、現在、Microsoft パブリッククラウドのパートナーセンターでのみサポートされています。 以下には適用されません。

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

**アグリーメント**リソースは、Microsoft cloud customer Agreement を表します。

## <a name="agreement"></a>契約

**アグリーメント**リソースは、パートナーによって提供される認定の詳細を表します。

| プロパティ       | 種類   | 説明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | string                         | パートナー組織の代わりに確認を提供する、パートナーテナント内のログインユーザーのオブジェクト識別子。 アプリ + ユーザー認証を使用してアグリーメントリソースを作成する場合、パートナーセンターは自動的に、アプリ + ユーザートークンから**userId**属性の値を取得します。                                                                             |
| primaryContact | [Contact](./utility-resources.md#contact) | Microsoft Cloud 契約に同意した顧客組織からのユーザーに関する情報 ( **firstName**、 **lastName**、 **email**、 **phoneNumber**など)。 |
| dateAgreed     | UTC 日時形式の文字列 | 顧客がアグリーメントに同意した日付。                                 |
| templateId     |string                          | 顧客が同意したアグリーメントの一意識別子。 |
| type           |string                          | 契約の種類。 現在サポートされている値は、 **microsoft の cloudagreement**と**Microsoft の顧客契約**です。|
| agreementLink  | string                         | アグリーメントテンプレートの URL。                                                    |
