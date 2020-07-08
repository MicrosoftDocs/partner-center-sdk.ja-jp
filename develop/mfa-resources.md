---
title: パートナーのセキュリティ要件に関するリソース
description: パートナーのセキュリティ要件を満たすための multi-factor authentication (MFA) の導入の詳細について説明します。
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 5eb77c3c10e95c9dc835cfe05e014b9256531b51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094767"
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
| IpAddress                           | string          | ソース IP アドレス                        |
| ObjectId                            | string          | ユーザー オブジェクト ID                           |
| TenantId                            | string          | CSP テナント ID                            |
| プリンシパル                                 | string          | ユーザー プリンシパル名                      |
| ApplicationId                       | string          | アプリケーション                         |
| MfaCompliant                        | [bool]            | MFA の有無にかかわらず要求を示す |
