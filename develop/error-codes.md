---
title: パートナーセンターの REST エラーコード
description: パートナーセンターの Api からのエラーコードと成功応答の説明。
ms.assetid: 08AC1F2E-5847-4AD8-AE5B-0173C5DB589A
ms.date: 06/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 2bb945de632b0bf18eea73db739ad0aa6085eecc
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415642"
---
# <a name="partner-center-rest-error-codes"></a>パートナーセンターの REST エラーコード

適用対象

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンターの REST Api は、状態コードを含む JSON オブジェクトを返します。 このコードは、要求が成功したかどうか、または失敗した理由を示します。

## <a name="success-responses"></a>成功応答

**2xx**状態コードは、クライアントの要求が正常に受信、理解、および受け入れられたことを示します。

## <a name="error-codes"></a>エラー コード

次の**4xx**および**5xx**状態コードはエラーを示しています。

- 400: 要求が正しくありません
- 401: Unauthorized
- 403: 許可されていません
- 404: 見つかりません
- 405: メソッドは許可されていません
- 406: 許容できません
- 409: 競合、エラーコード
- 412: 前提条件に失敗しました
- 429: 要求が多すぎます
- 500: 内部サーバーエラー
- 501: 実装されていません
- 502: ゲートウェイが正しくありません
- 503: サービスを利用できません
- 504: ゲートウェイのタイムアウト

## <a name="error-responses"></a>エラー応答

**4xx**または**5xx**状態コードを含むすべての応答には、発生したエラー状態に関する追加情報を含むエラーメッセージが含まれています。

次の表とコードサンプルでは、エラー応答のスキーマについて説明します。

| Name        | 種類   | 説明                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| code        | string | 常に返されます。 発生したエラーの種類を示します。 null 以外。                                                                                  |
| description | string | 常に返されます。 エラーを詳しく説明し、追加のデバッグ情報を提供します。 null または空以外。 最大長は 1024 文字です。 |
| data        | array  | 一部のエラーの種類に対してのみ返されます。 エラーオブジェクトの一覧。                                                                                           |
| source      | string | 常に返されます。 エラーの発生元。                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
## }
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```
