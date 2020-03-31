---
title: パートナーセンターの REST ヘッダー
description: 次の HTTP 要求および応答ヘッダーは、パートナーセンターの REST API によってサポートされています。
ms.assetid: 38A43A4C-EC31-4554-A747-0DC04B77CB99
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e58c10b43021d344e2dbe0ba5b6b698c04d0124e
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416557"
---
# <a name="partner-center-rest-headers"></a>パートナーセンターの REST ヘッダー


**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次の HTTP 要求および応答ヘッダーは、パートナーセンターの REST API によってサポートされています。 すべての API 呼び出しがすべてのヘッダーを受け付けるとは限りません。

## <a name="span-idrequest_headersspan-idrequest_headersspan-idrequest_headersrequest-headers"></a><span id="Request_headers"/><span id="request_headers"/><span id="REQUEST_HEADERS"/>要求ヘッダー


次の HTTP 要求ヘッダーは、パートナーセンター REST API によってサポートされています。

| ヘッダー                       | 説明                                                                                                                                                                                                                                                                            | 値の種類 |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 承認:               | 必須。 ベアラー &lt;トークン&gt;形式の認証トークン。                                                                                                                                                                                                                    | string     |
| 受入                      | 要求と応答の種類 "application/json" を指定します。                                                                                                                                                                                                                           | string     |
| MS-RequestId:                | 呼び出しの一意識別子。ID の有効性を保証するために使用されます。 タイムアウトの場合、再試行の呼び出しに同じ値を含める必要があります。 応答 (成功またはビジネス失敗) を受信したら、次の呼び出しのために値をリセットする必要があります。                                            | GUID       |
| MS CorrelationId:            | 呼び出しの一意識別子。エラーのトラブルシューティングのためにログやネットワーク トレースを調べる際に役立ちます。 呼び出しごとに値をリセットする必要があります。 すべての操作にこのヘッダーを含める必要があります。 詳細については、「[テストおよびデバッグ](test-and-debug.md)」の相関 ID 情報を参照してください。 | GUID       |
| MS-コントラクトのバージョン:         | 必須。 要求された API のバージョンを指定します。一般に、「[シナリオ](scenarios.md)」セクションで特に指定されていない限り、api バージョン: v1 です。                                                                                                                                  | string     |
| If-Match:                    | コンカレンシー制御に使用します。 一部の API 呼び出しでは、If-Match ヘッダーを介して ETag を渡す必要があります。 通常、ETag はリソース上にあるため、最新のものを GET する必要があります。 詳細については、「[テストおよびデバッグ](test-and-debug.md)」の ETag 情報を参照してください。                | string     |
| MS PartnerCenter-アプリケーション | 省略可。 REST API パートナーセンターを使用しているアプリケーションの名前を指定します。                                                                                                                                                                                             | string     |
| X-ロケール:                    | 省略可。 レートが返される言語を指定します。 既定値は "en-us" です。 サポートされている値の一覧については、「[パートナーセンターでサポートされている言語とロケール](partner-center-supported-languages-and-locales.md)」を参照してください。                                                                                                                                                                                                  | string     |

 

## <a name="span-idresponse_headersspan-idresponse_headersspan-idresponse_headersresponse-headers"></a><span id="Response_headers"/><span id="response_headers"/><span id="RESPONSE_HEADERS"/>応答ヘッダー


次の HTTP 応答ヘッダーは、パートナーセンター REST API によって返される場合があります。

| ヘッダー            | 説明                                                                                                                                                                                                                                 | 値の種類 |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 受入           | 要求と応答の種類 "application/json" を指定します。                                                                                                                                                                                | string     |
| MS-RequestId:     | 呼び出しの一意識別子。ID の有効性を保証するために使用されます。 タイムアウトの場合、再試行の呼び出しに同じ値を含める必要があります。 応答 (成功またはビジネス失敗) を受信したら、次の呼び出しのために値をリセットする必要があります。 | GUID       |
| MS CorrelationId: | 呼び出しの一意識別子。エラーのトラブルシューティングのためにログやネットワーク トレースを調べる際に役立ちます。 呼び出しごとに値をリセットする必要があります。 すべての操作にこのヘッダーを含める必要があります。                                                       | GUID       |

 

 

 




