---
title: 管理されたサービスリソース
description: 管理されたサービスとは、パートナーが管理者特権を委任したサービスです。 パートナーは、管理されたサービスの代理として、およびファイルサービス要求のサポートを提供できます。
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5b25e0f82c25d5af3bbad4c989e0bb1310af1a40
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416466"
---
# <a name="managed-service-resources"></a>管理されたサービスリソース


**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

管理されたサービスとは、パートナーが管理者特権を委任したサービスです。 パートナーは、管理されたサービスの代理として、およびファイルサービス要求のサポートを提供できます。

## <a name="span-idmanagedservicespan-idmanagedservicespan-idmanagedservicemanagedservice"></a><span id="ManagedService"/><span id="managedservice"/><span id="MANAGEDSERVICE"/>ManagedService


管理されたサービスについて説明します。

| プロパティ   | 種類                | 説明                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | マネージドサービス id。                                  |
| Name       | string              | 管理されたサービスの名前。                         |
| GroupName  | string              | サービスが属しているグループの名前。      |
| Links      | ManagedServiceLinks | マネージサービスに対応するリソースリンク。 |
| 属性 | ResourceAttributes  | アグリーメントに対応するメタデータ属性。  |

 

## <a name="span-idmanagedservicelinksspan-idmanagedservicelinksspan-idmanagedservicelinksmanagedservicelinks"></a><span id="ManagedServiceLinks"/><span id="managedservicelinks"/><span id="MANAGEDSERVICELINKS"/>ManagedServiceLinks


代理管理者権限を持つパートナーがサービスのサポートを提供できるようにするリンクが含まれています。

| プロパティ      | 種類 | 説明                 |
|---------------|------|-----------------------------|
| AdminService  | リンク | 管理サービスの URI。      |
| ServiceHealth | リンク | サービス正常性 URI。     |
| ServiceTicket | リンク | サービスチケットの URI。     |
| Self (自己)          | リンク | 自己 URI。               |
| 次へ          | リンク | 項目の次のページ。     |
| 前へ      | リンク | 項目の前のページ。 |

 

 

 




