---
title: リレーションシップのリソース
description: リレーションシップに関連するリソースについて説明します。
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b1d6d41256c081f3ef5ce7b27d89498839d8f5c8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488102"
---
# <a name="relationships-resources"></a>リレーションシップのリソース


**適用対象**

- パートナー センター

リレーションシップに関連するリソースについて説明します。

## <a name="span-idpartnerrelationshipspan-idpartnerrelationshipspan-idpartnerrelationshippartnerrelationship"></a><span id="PartnerRelationship"/><span id="partnerrelationship"/><span id="PARTNERRELATIONSHIP"/>PartnerRelationship


2つのパートナー間の関係を表します。

| プロパティ         | 種類                                                           | 説明                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | string                                                         | パートナー識別子。 パートナー id は、リレーションシップの "受信者" (差出人) 側にあるパートナーのテナント id を指定します。 |
| location         | string                                                         | パートナーの場所。                                                                                                                   |
| mpnId            | string                                                         | パートナーの Microsoft Partner Network (MPN) 識別子。                                                                                 |
| name             | string                                                         | パートナーの名前。                                                                                                                       |
| relationshipType | string                                                         | リレーションシップの種類。                                                                                                                      |
| state            | string                                                         | リレーションシップの状態 (例: "active")。                                                                                                 |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                                                                                       |

 

## <a name="span-idrelationshiprequestspan-idrelationshiprequestspan-idrelationshiprequestrelationshiprequest"></a><span id="RelationshipRequest"/><span id="relationshiprequest"/><span id="RELATIONSHIPREQUEST"/>RelationshipRequest


顧客がパートナーとの関係を確立するための URL を提供します。

| プロパティ   | 種類                                                           | 説明                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | string                                                         | リレーションシップ要求 URL。 |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。      |

 

 

 




