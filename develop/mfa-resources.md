---
title: パートナーのセキュリティ要件に関するリソース
description: パートナーのセキュリティ要件を満たすための multi-factor authentication (MFA) の導入の詳細について説明します。
ms.assetid: 1A8C28E2-2E67-41DA-B451-5A052FF12115
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.date: 05/29/2020
ms.openlocfilehash: 0a1e57d057c3a9c81fca85c3625e652467d05638
ms.sourcegitcommit: 9c3c915b79846917b2075be632d5b9b013f53a27
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84186330"
---
# <a name="partner-security-requirements-resources"></a>パートナーのセキュリティ要件に関するリソース

**適用対象:**

- パートナー センター

この記事では、組織がパートナーのセキュリティ要件を満たすために役立つ、multi-factor authentication (MFA) の導入の詳細について説明します。 

## <a name="portal-request-without-mfa"></a>MFA を使用しないポータル要求

MFA 認証を使用せずにパートナーセンターポータルにアクセスするユーザーを指定します。

| プロパティ                            | Type            | Description                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | string          | ユーザーオブジェクト ID                        |
| TenantId                            | string          | CSP テナント ID                         |
| プリンシパル                                 | string          | ユーザー プリンシパル名                   |
| Lastnonmfacompliの Logindatetime    | DATETIME        | MFA を使用しない最新のユーザーログイン |


## <a name="api-request-summarized-by-application"></a>アプリケーション別に要約される API 要求

アプリ + ユーザー資格情報によって行われた API 要求の概要。要求日とアプリケーション Id で集計されます。

| プロパティ                            | Type            | 説明               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | DATETIME        | API 要求日          |
| MfaCompliantRequestCount            | long            | MFA を使用した要求数    |
| TotalRequestCount                   | long            | 合計要求数       |
| ApplicationId                       | string          | アプリケーション ID        |
| ApplicationName                     | string          | アプリケーション名      |


## <a name="api-request-details"></a>API 要求の詳細

アプリ + ユーザー資格情報によって行われた API 要求。 

| プロパティ                            | Type            | 説明                              |
|-------------------------------------|-----------------|------------------------------------------|
| RequestId                           | string          | MS-RequestId                             |
| CorrelationId                       | string          | MS-CorrelationId                         |
| OperationName                       | string          | 要求メソッドを使用した API パス         |
| RequestDateTime                     | DateTime        | API 要求時間                     |
| IpAddress                           | string          | 送信元 IP アドレス                        |
| ObjectId                            | string          | ユーザー オブジェクト ID                           |
| TenantId                            | string          | CSP テナント ID                            |
| プリンシパル                                 | string          | ユーザー プリンシパル名                      |
| ApplicationId                       | string          | アプリケーション                         |
| MfaCompliant                        | bool            | MFA の有無にかかわらず要求を示す |
