---
title: Managed service resources
description: Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 32cc11190425c2cdfdbf6c793ef75091915e5d69
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486902"
---
# <a name="managed-service-resources"></a>Managed service resources


**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.

## <a name="span-idmanagedservicespan-idmanagedservicespan-idmanagedservicemanagedservice"></a><span id="ManagedService"/><span id="managedservice"/><span id="MANAGEDSERVICE"/>ManagedService


Describes a managed service.

| プロパティ   | タスクバーの検索ボックスに                | 説明                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | The managed service id.                                  |
| 名前       | string              | The name of the managed service.                         |
| GroupName  | string              | The name of the group to which the service belongs.      |
| Links      | ManagedServiceLinks | The resource links corresponding to the managed service. |
| 属性 | ResourceAttributes  | The metadata attributes corresponding to the agreement.  |

 

## <a name="span-idmanagedservicelinksspan-idmanagedservicelinksspan-idmanagedservicelinksmanagedservicelinks"></a><span id="ManagedServiceLinks"/><span id="managedservicelinks"/><span id="MANAGEDSERVICELINKS"/>ManagedServiceLinks


Contains the links that allow the partner with delegated admin permissions to provide support for the service.

| プロパティ      | タスクバーの検索ボックスに | 説明                 |
|---------------|------|-----------------------------|
| AdminService  | [リンク] | The admin service URI.      |
| ServiceHealth | [リンク] | The service health URI.     |
| ServiceTicket | [リンク] | The service ticket URI.     |
| Self (自己)          | [リンク] | The self URI.               |
| [次へ]          | [リンク] | The next page of items.     |
| Previous      | [リンク] | The previous page of items. |

 

 

 




