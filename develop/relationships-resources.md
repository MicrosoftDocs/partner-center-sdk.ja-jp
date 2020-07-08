---
title: リレーションシップのリソース
description: リレーションシップに関連するリソースについて説明します。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094928"
---
# <a name="relationships-resources"></a>リレーションシップのリソース

**適用対象**

- パートナー センター

リレーションシップに関連するリソースについて説明します。

## <a name="partnerrelationship"></a>PartnerRelationship

2つのパートナー間の関係を表します。

| プロパティ         | Type                                                           | 説明                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | string                                                         | パートナー識別子。 パートナー id は、リレーションシップの "受信者" (差出人) 側にあるパートナーのテナント id を指定します。 |
| location         | string                                                         | パートナーの場所。                                                                                                                   |
| mpnId            | string                                                         | パートナーの Microsoft Partner Network (MPN) 識別子。                                                                                 |
| name             | string                                                         | パートナーの名前。                                                                                                                       |
| relationshipType | string                                                         | リレーションシップの種類。                                                                                                                      |
| state            | string                                                         | リレーションシップの状態 (など `active` )。                                                                                                 |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

顧客がパートナーとの関係を確立するための URL を提供します。

| プロパティ   | Type                                                           | 説明                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | string                                                         | リレーションシップ要求 URL。 |
| 属性 | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。      |
