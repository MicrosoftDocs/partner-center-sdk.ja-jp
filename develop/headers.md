---
title: パートナーセンターの REST ヘッダー
description: 次の HTTP 要求および応答ヘッダーは、パートナーセンターの REST API によってサポートされています。
ms.assetid: 38A43A4C-EC31-4554-A747-0DC04B77CB99
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f5adf9a458148c1e68cf17a3014cb1931e8860be
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487112"
---
# <a name="partner-center-rest-headers"></a>パートナーセンターの REST ヘッダー


**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

次の HTTP 要求および応答ヘッダーは、パートナーセンターの REST API によってサポートされています。 すべての API 呼び出しがすべてのヘッダーを受け入れるとは限りません。

## <a name="span-idrequest_headersspan-idrequest_headersspan-idrequest_headersrequest-headers"></a><span id="Request_headers"/><span id="request_headers"/><span id="REQUEST_HEADERS"/>要求ヘッダー


次の HTTP 要求ヘッダーは、パートナーセンター REST API によってサポートされています。

| Header                       | 説明                                                                                                                                                                                                                                                                            | 値の種類 |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 権限               | 必須。 ベアラー &lt;トークン&gt;形式の認証トークン。                                                                                                                                                                                                                    | string     |
| 受入                      | 要求と応答の種類として "application/json" を指定します。                                                                                                                                                                                                                           | string     |
| MS-RequestId:                | Id の有効性を保証するために使用される、呼び出しの一意の識別子。 タイムアウトの場合、再試行の呼び出しには同じ値を含める必要があります。 応答を受信したとき (成功または失敗)、次の呼び出しで値をリセットする必要があります。                                            | GUID       |
| MS CorrelationId:            | 呼び出しの一意の識別子。ログとネットワークトレースで、エラーのトラブルシューティングに役立ちます。 すべての呼び出しに対して値をリセットする必要があります。 すべての操作にこのヘッダーを含める必要があります。 詳細については、「[テストおよびデバッグ](test-and-debug.md)」の相関 ID 情報を参照してください。 | GUID       |
| MS-コントラクトのバージョン:         | 必須。 要求された API のバージョンを指定します。一般に、「[シナリオ](scenarios.md)」セクションで特に指定されていない限り、api バージョン: v1 です。                                                                                                                                  | string     |
| 一致する場合:                    | 同時実行制御に使用されます。 一部の API 呼び出しでは、If-match ヘッダーを使用して ETag を渡す必要があります。 通常、ETag はリソース上にあるため、最新の情報を取得する必要があります。 詳細については、「[テストおよびデバッグ](test-and-debug.md)」の ETag 情報を参照してください。                | string     |
| MS PartnerCenter-アプリケーション | (省略可能)。 REST API パートナーセンターを使用しているアプリケーションの名前を指定します。                                                                                                                                                                                             | string     |
| X-ロケール:                    | (省略可能)。 レートが返される言語を指定します。 既定値は "en-us" です。 サポートされている値の一覧については、「[パートナーセンターでサポートされている言語とロケール](partner-center-supported-languages-and-locales.md)」を参照してください。                                                                                                                                                                                                  | string     |

 

## <a name="span-idresponse_headersspan-idresponse_headersspan-idresponse_headersresponse-headers"></a><span id="Response_headers"/><span id="response_headers"/><span id="RESPONSE_HEADERS"/>応答ヘッダー


次の HTTP 応答ヘッダーは、パートナーセンター REST API によって返される場合があります。

| Header            | 説明                                                                                                                                                                                                                                 | 値の種類 |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 受入           | 要求と応答の種類として "application/json" を指定します。                                                                                                                                                                                | string     |
| MS-RequestId:     | Id の有効性を保証するために使用される、呼び出しの一意の識別子。 タイムアウトの場合、再試行の呼び出しには同じ値を含める必要があります。 応答を受信したとき (成功または失敗)、次の呼び出しで値をリセットする必要があります。 | GUID       |
| MS CorrelationId: | 呼び出しの一意の識別子。エラーをトラブルシューティングするためのログとネットワークトレースに役立ちます。 すべての呼び出しに対して値をリセットする必要があります。 すべての操作にこのヘッダーを含める必要があります。                                                       | GUID       |

 

 

 




