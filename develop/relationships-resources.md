---
title: リレーションシップのリソース
description: リレーションシップに関連するリソースについて説明します。
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3e444653a8b5acd5dafbebe8e4526c50e7951155
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124434"
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
| state            | string                                                         | リレーションシップの状態 (など`active`)。                                                                                                 |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

顧客がパートナーとの関係を確立するための URL を提供します。

| プロパティ   | Type                                                           | 説明                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | string                                                         | リレーションシップ要求 URL。 |
| attributes | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。      |
