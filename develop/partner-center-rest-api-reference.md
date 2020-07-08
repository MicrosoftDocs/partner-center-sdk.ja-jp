---
title: パートナー センター REST API リファレンス
description: パートナーセンター REST API は、CSP パートナーが既存の CRM または請求ソフトウェアを、顧客アカウントの管理、注文の配置、サブスクリプションの管理、およびサポート要求の処理を行う Microsoft システムと統合するのに役立ちます。
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: adab62c38d46c5ec0fbaf9fd7c7a03936788890c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094663"
---
# <a name="partner-center-rest-api-reference"></a>パートナー センター REST API リファレンス

**適用対象:**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

## <a name="partner-center-rest-api"></a>パートナー センター REST API

パートナーセンター REST API は、クラウドソリューションプロバイダー (CSP) パートナーが、顧客アカウントの管理、注文の配置、サブスクリプションの管理、およびサポート要求の処理を行う Microsoft システムと既存の CRM または課金ソフトウェアを統合するのに役立ちます。

API が実行できる操作 (サンプルコードを含む) の詳細については、「バックグラウンドの概要」を含む、[シナリオ](scenarios.md)に関するトピックを参照してください。

コーディングを開始する前に、「[はじめ](get-started.md)に」のトピックを参照してください。 この記事には、テストと実稼働アカウントの設定、認証の機能の取得、およびサンプルコードの検索に関する情報が含まれています。

## <a name="topics"></a>トピック

| トピック | 説明 |
| ----- | ----------- |
| [パートナー センター REST URL](partner-center-rest-urls.md) | 異なるバージョンのパートナーセンターの REST API エンドポイントを定義します。 |
| [パートナー センター REST ヘッダー](headers.md) | REST API によって使用される要求ヘッダーと応答ヘッダーを定義します。 |
| [パートナー センター REST リソース](partner-center-rest-resources.md) | REST API を使用するために必要なオブジェクトを表す JSON 構造体を定義します。 |
| [パートナー センター REST イベント](partner-center-webhook-events.md) | パートナーセンター webhook によってサポートされる REST リソース変更イベントを定義します。 |
| [パートナー センターでサポートされている言語とロケール](partner-center-supported-languages-and-locales.md) | パートナーセンターの Api でサポートされているロケール、言語、および国/地域コードを一覧表示します。 |
| [パートナー センター Webhook](partner-center-webhooks.md) | イベントの受信方法、コールバックの認証方法、およびパートナーセンターの webhook Api を使用してイベント登録を作成、表示、更新する方法について説明します。 |