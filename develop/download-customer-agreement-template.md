---
title: Microsoft 顧客契約テンプレートのダウンロード リンクを取得する
description: Microsoft カスタマーアグリーメントテンプレートのダウンロードリンクを取得します。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8c794d264ad64a42fa6ca823ddfc3841248c01cd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098377"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Microsoft 顧客契約テンプレートのダウンロード リンクを取得する

**適用対象:**

- パートナー センター

**AgreementDocument**リソースは、現在、 *Microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 このリソースはに適用されません:

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、顧客の国と言語に基づいて、Microsoft カスタマーアグリーメントテンプレートをダウンロードするためのリンクを取得する方法について説明します。

## <a name="prerequisites"></a>前提条件

- パートナー センター .NET SDK を使用している場合、バージョン 1.14 以降が必要です。

- [パートナー センターの認証](./partner-center-authentication.md)に関するページで説明している資格情報。 このシナリオでは、アプリとユーザー認証のみがサポートされます。

- Microsoft カスタマーアグリーメントテンプレートが適用される顧客の国。

- Microsoft カスタマーアグリーメントテンプレートをローカライズする言語。

> [!IMPORTANT]
>
> - Microsoft 顧客契約は国によって異なります。 Microsoft カスタマーアグリーメントテンプレートをダウンロードするためのリンクを要求する場合は、顧客の所在地に基づいて正しい国を指定するようにしてください。 サポートされている国の一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。
>
> - 一部の国では、Microsoft カスタマー契約を複数の言語で利用できます。 最適なカスタマーエクスペリエンスを実現するには、お客様のニーズに最も合った言語を選択してください。 サポートされている言語の一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。
> - この方法は、Microsoft カスタマーアグリーメントでのみサポートされています。

## <a name="net"></a>.NET

Microsoft カスタマーアグリーメントテンプレートをダウンロードするためのリンクを取得するには、次のようにします。

1. Microsoft 顧客契約の契約メタデータを取得します。 Microsoft 顧客契約の **templateId** を取得する必要があります。 詳細については、「 [Microsoft Customer agreement の契約メタデータを取得する](get-customer-agreement-metadata.md)」を参照してください。

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. AgreementTemplates コレクションを使用します。

3. **ById**メソッドを呼び出し、Microsoft カスタマーアグリーメントの**templateId**を指定します。

4. **ドキュメント**プロパティを取得します。

5. **Bycountry**メソッドを呼び出し、契約テンプレートが適用される顧客の国を指定します。 メソッドが指定されていない場合、クエリの既定値は*US*です。 サポートされている国コードの一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。 このメソッドでは **、大文字と小文字が区別**されます。

6. **Bylanguage**メソッドを呼び出し、アグリーメントテンプレートのローカライズに使用する言語を指定します。 メソッドが指定されていない場合、または指定された国コードが指定された国でサポートされていない場合、クエリは既定で*en-us*に設定されます。 サポートされている言語コードの一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。

7. **Get**または**GetAsync**メソッドを呼び出します。

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

完全なサンプルは、[コンソールテストアプリ](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)プロジェクトの[GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs)クラスにあります。

## <a name="rest-request"></a>REST 要求

Microsoft カスタマーアグリーメントテンプレートをダウンロードするためのリンクを取得するには、次のようにします。

1. Microsoft 顧客契約の契約メタデータを取得します。 Microsoft 顧客契約の **templateId** を取得する必要があります。 詳細については、「 [Microsoft Customer agreement の契約メタデータを取得する](get-customer-agreement-metadata.md)」を参照してください。

2. REST 要求を作成して、 [ **AgreementDocument**リソース](./agreement-document-resources.md)をフェッチします。 例については、「[要求構文](#request-syntax)の例」を参照してください。 次の情報を指定する必要があります。

    - Microsoft カスタマーアグリーメントの**templateId** 。
    - Microsoft カスタマー契約テンプレートが適用される国。
    - Microsoft カスタマーアグリーメントテンプレートをローカライズする言語。

### <a name="request-syntax"></a>要求の構文

このリソースには次の要求構文を使用します。

| Method | 要求 URI |
|--------|---------------------------------------------------------------------|
| GET | [* \{ baseURL \} *](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document? language = {language} &country = {country} HTTP/1.1 |

### <a name="uri-parameters"></a>URI パラメーター

要求では、次の URI パラメーターを使用できます。

| 名前                   | Type   | 必須 | 説明                                 |
|------------------------|--------|----------|---------------------------------------------|
| 契約テンプレート-id  | string | はい      | 契約の種類を表す一意の識別子。 Microsoft 顧客契約の契約メタデータを取得することで、Microsoft 顧客契約の templateId を取得できます。 詳細については、「 [Microsoft Customer agreement の契約メタデータを取得する](./get-customer-agreement-metadata.md)」を参照してください。 このパラメーターでは **、大文字と小文字が区別**されます。|
| country                | string | いいえ       | アグリーメントテンプレートを適用する国を指定します。 パラメーターが指定されていない場合、クエリの既定値は*US*です。 サポートされている国コードの一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。|
| language               | 文字列 | いいえ       | アグリーメントテンプレートのローカライズに使用する言語を指定します。 パラメーターが指定されていない場合、または指定された国に対して指定された国コードがサポートされていない場合、クエリの既定値は*en-us*です。 サポートされている国コードの一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。|

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナー センター REST ヘッダー](headers.md)」を参照してください。

### <a name="request-body"></a>[要求本文]

[なし] :

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で[ **AgreementDocument**リソース](./agreement-document-resources.md)を返します。

リソースには、ライセンステンプレートをダウンロードするために使用できる URL 文字列を含む**downloaduri**プロパティがあります。 クエリを作成するたびに、別のリンクが返されます。 このリンクは、5分後に有効期限が切れます。

### <a name="response-success-and-error-codes"></a>応答の成功とエラーのコード

各応答には、成功または失敗を示す HTTP ステータス コードと、追加のデバッグ情報が付属しています。

このコード、エラーの種類、追加のパラメーターを読み取るには、ネットワーク トレース ツールを使用します。 完全な一覧については、[パートナー センターの REST エラーコード](error-codes.md)に関する記事を参照してください。

### <a name="response-example"></a>応答の例

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## <a name="list-of-supported-countries-and-languages"></a>サポートされている国と言語の一覧

> [!IMPORTANT]
> 国コードプロパティでは、大文字と小文字が区別されます。 次の表で指定されている正しい文字種を使用してください。

| 国                   | 国番号   | サポートされている言語コード |
|------------------------|--------|----------|
| オーランド諸島 | AX | ja-JP |
| アフガニスタン | AF | ja-JP |
| アルバニア | AL | ja-JP |
| アルジェリア | DZ | en-us, fr-fr, en-us, en-us |
| 米領サモア | AS | ja-JP |
| アンドラ | AD | ja-JP |
| アンゴラ | AO | en-us、pt-PT |
| アンギラ | AI | ja-JP |
| 南極 | AQ | ja-JP |
| アンティグア・バーブーダ | AG | ja-JP |
| アルゼンチン | AR | en-us、es |
| アルメニア | AM | ja-JP |
| アルバ | AW | ja-JP |
| オーストラリア | AU | ja-JP |
| オーストリア | AT | en-us、de |
| アゼルバイジャン | AZ | ja-JP |
| バハマ | BS | ja-JP |
| バーレーン | BH | en-us、ar-SA |
| バングラデシュ | BD | ja-JP |
| バルバドス | BB | ja-JP |
| ベラルーシ | BY | en-US、ru-RU |
| ベルギー | BE | en-us、nl-NL |
| ベリーズ | BZ | en-us、es |
| ベナン | BJ | ja-JP |
| バミューダ | BM | ja-JP |
| ブータン | BT | ja-JP |
| ボリビア | BO | en-us、es |
| ボネール島 | BQ | ja-JP |
| ボスニア・ヘルツェゴビナ | BA | ja-JP |
| ボツワナ | BW | ja-JP |
| ブーベ島 | BV | ja-JP |
| ブラジル | BR | en-us、pt-BR |
| 英領インド洋地域 | IO | ja-JP |
| 英領ヴァージン諸島 | VG | ja-JP |
| ブルネイ | BN | ja-JP |
| ブルガリア | BG | en-us、bg-BG |
| ブルキナファソ | BF | ja-JP |
| ブルンジ | BI | ja-JP |
| コートジボワール | CI | en-US、fr-FR |
| カーボベルデ | CV | en-us、pt-PT |
| カンボジア | KH | ja-JP |
| カメルーン | CM | en-US、fr-FR |
| Canada | CA | en-US、fr-FR |
| ケイマン諸島 | KY | en-us、en-us |
| 中央アフリカ共和国 | CF | ja-JP |
| チャド | TD | ja-JP |
| チリ | CL | en-us、es |
| クリスマス島 | CX | ja-JP |
| ココス(キーリング)諸島 | CC | ja-JP |
| コロンビア | CO | en-us、es |
| コモロ | KM | ja-JP |
| コンゴ民主共和国 | CD | ja-JP |
| コンゴ | CG | ja-JP |
| クック諸島 | CK | ja-JP |
| コスタリカ | CR | en-us、es |
| クロアチア | HR | en-us、hr-HR |
| キュラソー島 | CW | ja-JP |
| キプロス | CY | ja-JP |
| チェコ | CZ | en-us, cs-CS-CZ |
| デンマーク | DK | en-us、da-DK |
| ジブチ | DJ | ja-JP |
| ドミニカ | DM | ja-JP |
| ドミニカ共和国 | DO | en-us、es |
| エクアドル | EC | ja-JP |
| エジプト | EG | en-us、ar-SA |
| エルサルバドル | SV | en-us、es |
| 赤道ギニア | GQ | ja-JP |
| エリトリア | ER | ja-JP |
| エストニア | EE | en-us、et-EE |
| スワジランド | SZ | ja-JP |
| エチオピア | ET | ja-JP |
| フォークランド諸島 | FK (FK) | ja-JP |
| フェロー諸島 | FO | ja-JP |
| フィジー | FJ | ja-JP |
| フィンランド | FI | en-us、fi FI |
| フランス | FR | en-US、fr-FR |
| 仏領ギアナ | GF | en-US、fr-FR  |
| 仏領ポリネシア | PF | ja-JP |
| 仏領極南諸島 | TF | ja-JP |
| ガボン | GA | ja-JP |
| ガンビア | GM | ja-JP |
| ジョージア | GE | ja-JP |
| ドイツ | DE | en-us、de |
| ガーナ | GH | ja-JP |
| ジブラルタル | GI | ja-JP |
| ギリシャ | GR | en-us、el-GR |
| グリーンランド | GL | ja-JP |
| グレナダ | GD | ja-JP |
| グアドループ | GP | ja-JP |
| グアム | GU | ja-JP |
| グアテマラ | GT | en-us、es |
| ガーンジー | GG | ja-JP |
| ギニア | GN | ja-JP |
| ギニアビサウ | GW | ja-JP |
| ガイアナ | GY | ja-JP |
| ハイチ | HT | ja-JP |
| ハード・マクドナルド諸島 | HM | ja-JP |
| ホンジュラス | HN | en-us、es |
| 香港特別行政区 | HK | en-us、zh-tw-HK |
| ハンガリー | HU | en-us、hu-HU |
| アイスランド | IS | ja-JP |
| インド | IN | en-us、こんにちは |
| インドネシア | id | en-us、id-ID |
| イラク | IQ | en-us、ar-SA |
| アイルランド | IE | ja-JP |
| マン島 | IM | ja-JP |
| イスラエル | IL | en-us、he |
| イタリア | IT | en-us、it |
| ジャマイカ | JM | ja-JP |
| ヤンマイエン島 | XJ | ja-JP |
| 日本 | JP | en-us、ja-jp |
| ジャージー | JE | ja-JP |
| ヨルダン | JO | en-us、ar-SA |
| カザフスタン | KZ | en-us、kk-KZ |
| ケニア | KE | ja-JP |
| キリバス | KI | ja-JP |
| 韓国 | KR | en-us、ko-韓国 |
| コソボ | XK | ja-JP |
| クウェート | KW | en-us、ar-SA |
| キルギス | KG | en-US、ru-RU |
| ラオス | LA | ja-JP |
| ラトビア | LV | en-us、lv-LV |
| レバノン | LB | en-us、ar-SA |
| レソト | LS | ja-JP |
| リベリア | LR | ja-JP |
| リビア | LY | en-us、ar-SA |
| リヒテンシュタイン | LI | en-us、de |
| リトアニア | LT | en-us、lt-LT |
| ルクセンブルク | LU | en-US、fr-FR |
| 中華人民共和国マカオ特別行政区 | MO | en-us、zh-tw-HK |
| マケドニア (旧ユーゴスラビア共和国) | MK | ja-JP |
| マダガスカル | MG | ja-JP |
| マラウイ | MW | ja-JP |
| マレーシア | MY | en-us、ms-MY |
| モルディブ | MV | ja-JP |
| マリ | ML | ja-JP |
| マルタ | MT | ja-JP |
| マーシャル諸島 | MH | ja-JP |
| マルティニーク | MQ | ja-JP |
| モーリタニア | MR | ja-JP |
| モーリシャス | MU | en-us、ar-SA |
| マヨット | YT | ja-JP |
| メキシコ | MX | en-us、es |
| ミクロネシア | FM | ja-JP |
| モルドバ | MD | en-us、ro-RO |
| モナコ | MC | en-US、fr-FR |
| モンゴル | MN | ja-JP |
| モンテネグロ | ME | ja-JP |
| モントセラト | MS | ja-JP |
| モロッコ | MA | en-us, fr-fr, en-us, en-us |
| モザンビーク | MZ | ja-JP |
| ミャンマー | mm | ja-JP |
| ナミビア | NA | ja-JP |
| ナウル | NR | ja-JP |
| ネパール | NP | ja-JP |
| オランダ | NL | en-us、nl-NL |
| ニューカレドニア | NC | ja-JP |
| ニュージーランド | NZ | ja-JP |
| ニカラグア | NI | en-us、es |
| ニジェール | NE | ja-JP |
| ナイジェリア | NG | ja-JP |
| ニウエ | NU | ja-JP |
| ノーフォーク島 | NF | ja-JP |
| 北マリアナ諸島 | MP | ja-JP |
| ノルウェー | NO | en-us、nb-いいえ |
| オマーン | OM | en-us、ar-SA |
| パキスタン | PK | ja-JP |
| パラオ | PW | ja-JP |
| パレスチナ自治政府 | PS | ja-JP |
| パナマ | PA | en-us、es |
| パプアニューギニア | PG | ja-JP |
| パラグアイ | PY | en-us、es |
| ペルー | PE | en-us、es |
| フィリピン | PH | ja-JP |
| ピトケアン島 | PN | ja-JP |
| ポーランド | PL | en-us、pl-PL |
| ポルトガル | PT | en-us、pt-PT |
| プエルトリコ | PR | en-us、en-us |
| カタール | QA | en-us、ar-SA |
| レユニオン | RE | ja-JP |
| ルーマニア | RO | en-us、ro-RO |
| ロシア | RU | en-US、ru-RU |
| ルワンダ | RW | en-US、fr-FR |
| サントメ・プリンシペ | ST | en-US、fr-FR |
| サバ島 | XS | ja-JP |
| サン・バルテルミー | BL | ja-JP |
| セントクリストファー・ネイビス | KN | ja-JP |
| セントルシア | LC | en-us、en-us |
| サン・マルタン | MF | en-us、en-us |
| サンピエール・ミクロン | PM | ja-JP |
| セントビンセント及びグレナディーン諸島 | VC | ja-JP |
| サモア | WS | ja-JP |
| サンマリノ | SM | ja-JP |
| サウジアラビア | SA | ja-JP |
| セネガル | SN | en-US、fr-FR |
| セルビア | RS | en-us、Latn、英語 (米国) |
| セーシェル | SC | ja-JP |
| シエラレオネ | SL | ja-JP |
| シンガポール | SG | en-us、zh-tw |
| シント・ユースタティウス島 | XE | ja-JP |
| シント・マールテン | SX | en-us、en-us |
| スロバキア | SK | en-us、sk-SK |
| スロベニア | SI | en-us、sl-SI |
| ソロモン諸島 | SB | ja-JP |
| ソマリア | SO | ja-JP |
| 南アフリカ | ZA | ja-JP |
| サウスジョージア・サウスサンドウィッチ諸島 | GS | ja-JP |
| 南スーダン | SS | ja-JP |
| スペイン | ES | en-us、es ES、en-us、en-us、en-us |
| スリランカ | LK | ja-JP |
| セントヘレナ、アセンションおよびトリスタンダクーニャ | SH | ja-JP |
| スリナム | SR | ja-JP |
| スバールバル諸島 | SJ | ja-JP |
| スウェーデン | SE | en-us、sv-SE |
| スイス | CH | en-us、fr-fr、en-us、en-us (en-us) |
| 台湾 | TW | en-us、zh-tw-HK |
| タジキスタン | TJ | ja-JP |
| タンザニア | TZ | ja-JP |
| タイ | TH | en-us、th |
| ティモール・レステ | TL | ja-JP |
| トーゴ | TG | ja-JP |
| トケラウ | TK | ja-JP |
| トンガ | TO | ja-JP |
| トリニダード・トバゴ | TT | ja-JP |
| チュニジア | TN | en-us, fr-fr, en-us, en-us |
| トルコ | TR | en-us、tr-TR |
| トルクメニスタン | TM | ja-JP |
| タークス・カイコス諸島 | TC | ja-JP |
| ツバル | TV | ja-JP |
| 米領小離島 | UM | ja-JP |
| 米国バージン諸島 | VI | ja-JP |
| ウガンダ | UG | ja-JP |
| ウクライナ | UA | en-us、uk-UA |
| アラブ首長国連邦 | AE | en-us、ar-SA |
| イギリス | GB | ja-JP |
| United States | US | ja-JP |
| ウルグアイ | UY | en-us、es |
| ウズベキスタン | UZ | en-US、ru-RU |
| バヌアツ | VU | ja-JP |
| バチカン市国 | VA | ja-JP |
| ベネズエラ | VE | en-us、es |
| ベトナム | VN | en-us、vi-VN |
| ワリス・フテュナ諸島 | WF | ja-JP |
| イエメン | YE | en-us、ar-SA |
| ザンビア | ZM | ja-JP |
| ジンバブエ | ZW | ja-JP |
