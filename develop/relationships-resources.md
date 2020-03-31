---
title: リレーションシップのリソース
description: リレーションシップに関連するリソースについて説明します。
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 8050b8afa3b92007dbcad2869050b6f2a8c248f7
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415468"
---
# <a name="relationships-resources"></a>リレーションシップのリソース


**適用対象**

- Partner Center

リレーションシップに関連するリソースについて説明します。

## <a name="span-idpartnerrelationshipspan-idpartnerrelationshipspan-idpartnerrelationshippartnerrelationship"></a><span id="PartnerRelationship"/><span id="partnerrelationship"/><span id="PARTNERRELATIONSHIP"/>PartnerRelationship


2つのパートナー間の関係を表します。

| プロパティ         | 種類                                                           | 説明                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | string                                                         | パートナー識別子。 パートナー id は、リレーションシップの "受信者" (差出人) 側にあるパートナーのテナント id を指定します。 |
| 位置         | string                                                         | パートナーの場所。                                                                                                                   |
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

 

 

 




