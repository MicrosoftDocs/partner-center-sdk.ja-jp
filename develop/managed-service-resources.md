---
title: 管理されたサービスリソース
description: 管理されたサービスとは、パートナーが管理者特権を委任したサービスです。 パートナーは、管理されたサービスの代理として、およびファイルサービス要求のサポートを提供できます。
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a4de6e373748026c56599f8e7153569f04a0c9cf
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82118648"
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
| AdminService  | Link | 管理サービスの URI。      |
| ServiceHealth | Link | サービス正常性 URI。     |
| ServiceTicket | Link | サービスチケットの URI。     |
| セルフ          | Link | 自己 URI。               |
| Next          | Link | 項目の次のページ。     |
| Previous      | Link | 項目の前のページ。 |

