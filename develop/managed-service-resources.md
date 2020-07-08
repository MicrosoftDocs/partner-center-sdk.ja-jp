---
title: 管理されたサービスリソース
description: 管理されたサービスとは、パートナーが管理者特権を委任したサービスです。 パートナーは、管理されたサービスの代理として、およびファイルサービス要求のサポートを提供できます。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094794"
---
# <a name="managed-service-resources"></a>管理されたサービスリソース

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

管理されたサービスとは、パートナーが管理者特権を委任したサービスです。 パートナーは、管理されたサービスの代理として、およびファイルサービス要求のサポートを提供できます。

## <a name="managedservice"></a>ManagedService

管理されたサービスについて説明します。

| プロパティ   | Type                | 説明                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | マネージドサービス id。                                  |
| 名前       | string              | 管理されたサービスの名前。                         |
| GroupName  | string              | サービスが属しているグループの名前。      |
| リンク      | ManagedServiceLinks | マネージサービスに対応するリソースリンク。 |
| 属性 | ResourceAttributes  | アグリーメントに対応するメタデータ属性。  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

代理管理者権限を持つパートナーがサービスのサポートを提供できるようにするリンクが含まれています。

| プロパティ      | Type | 説明                 |
|---------------|------|-----------------------------|
| AdminService  | リンク | 管理サービスの URI。      |
| ServiceHealth | リンク | サービス正常性 URI。     |
| ServiceTicket | リンク | サービスチケットの URI。     |
| セルフ          | リンク | 自己 URI。               |
| 次へ          | リンク | 項目の次のページ。     |
| 前へ      | リンク | 項目の前のページ。 |

