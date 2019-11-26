---
title: Get a download link for the Microsoft Customer Agreement template
description: Get a download link for Microsoft Customer Agreement template.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 76b0b6ceb20504ad0f9903027ac61feca78c3970
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489962"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Get a download link for the Microsoft Customer Agreement template

適用対象:

- パートナー センター

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource doesn't apply to:

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

This article describes how to get a link to download the Microsoft Customer Agreement template, based on the customer's country and language.

## <a name="prerequisites"></a>前提条件

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario only supports App+User authentication.
- The customer's country to which the Microsoft Customer Agreement template applies.
- The language in which the Microsoft Customer Agreement template should be localized.

> [!IMPORTANT]
> - The Microsoft Customer Agreement is country-specific. When requesting for a link to download the Microsoft Customer Agreement template, Be sure to specify the correct country based on customer's location. or list of supported countries, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
> - For some countries, the Microsoft Customer Agreement is available in multiple languages. For best customer experience, pick the language that best match the customer's needs. For list of supported languages, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
> - This method is only supported with the Microsoft Customer Agreement. You cannot use it to get a download link for Microsoft Cloud Agreement template.

## <a name="net"></a>.NET の場合

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Use the IAggregatePartner.AgreementTemplates collection.
3. Call the **ById** method and specify the **templateId** of the Microsoft Customer Agreement.
4. Fetch the **Document** property.
5. Call the **ByCountry** method and specify the customer's country to which the agreement template applies. The query defaults to *US* if the method isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages). This method is **case-sensitive**.
6. Call the **ByLanguage** method and specify the language which the agreement template should be localized in. The query defaults to *en-US* if the method isn't specified or the country code specified isn't supported for the country specified. For list of supported language codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages)
7. Call the **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;

string customerCountry = "US";

string languageForLocalization = "en-US";

var agreementDocument = partnerOperations.AgreementTemplates.ById(microsoftCustomerAgreementDetails.TemplateId).Document.ByCountry(customerCountry).ByLanguage(languageForLocalization).Get();
```

A complete sample can be found in the [GetAgreementDocument](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDocument.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.


## <a name="rest-request"></a>REST request

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).
2. Create a REST request to fetch an [**AgreementDocument** resource](./agreement-document-resources.md). For an example, see the [request syntax](#request-syntax) example. You must specify the following information:
    - The **templateId** of the Microsoft Customer Agreement.
    - The country to which the Microsoft Customer Agreement template applies.
    - The language in which the Microsoft Customer Agreement template should be localized.

### <a name="request-syntax"></a>要求の構文

Use the following request syntax for this resource:

| メソッド | 要求 URI |
|--------|---------------------------------------------------------------------|
| GET | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### <a name="uri-parameters"></a>URI パラメーター

You can use the following URI parameters with your request:

| 名前                   | タスクバーの検索ボックスに   | 必須かどうか | 説明                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | string | [はい]      | Unique identifier of the agreement type. You can obtain the templateId for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md). This parameter is **case-sensitive**.|
| country                | string | 必須ではない       | Indicates the country to which the agreement template applies. The query defaults to *US* if the parameter isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|
| 言語               | string | 必須ではない       | Indicates the language in which the agreement template should be localized. The query defaults to *en-US* if the parameter isn't specified or the country code specified in't supported for the country specified. For list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>要求ヘッダー

For more information, see [Partner Center REST headers](headers.md).

### <a name="request-body"></a>要求本文

なし。

### <a name="request-example"></a>要求の例

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST response

If successful, this method returns an [**AgreementDocument** resource](./agreement-document-resources.md) in the response body.

The resource has a **downloadUri** property, which contains a URL string that can be used to download the agreement template. A different link is returned each time you make a query. This link expires after five minutes.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information.

Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

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

## <a name="list-of-supported-countries-and-languages"></a>List of supported countries and languages

> [!IMPORTANT]
> The country code property is case-sensitive. Please sure to use the correct casing specified in the table below.

| Country                   | 国番号   | Supported language code(s) |
|------------------------|--------|----------|
| オーランド諸島 | AX | ja-JP |
| アフガニスタン | AF | ja-JP |
| アルバニア | AL | ja-JP |
| アルジェリア | DZ | en-US, fr-FR, en-US |
| 米領サモア | AS | ja-JP |
| アンドラ | AD | ja-JP |
| アンゴラ | AO | en-US, pt-PT |
| アンギラ | AI | ja-JP |
| 南極 | AQ | ja-JP |
| アンティグア・バーブーダ | AG | ja-JP |
| アルゼンチン | AR | en-US, es-ES |
| アルメニア | AM | ja-JP |
| アルバ | AW | ja-JP |
| オーストラリア | AU | ja-JP |
| オーストリア | AT | en-US, de-DE |
| アゼルバイジャン | AZ | ja-JP |
| バハマ | BS | ja-JP |
| バーレーン | BH | en-US, ar-SA |
| バングラデシュ | BD | ja-JP |
| バルバドス | BB | ja-JP |
| ベラルーシ | BY | en-US, ru-RU |
| ベルギー | BE | en-US, nl-NL |
| ベリーズ | BZ | en-US, es-ES |
| ベナン | BJ | ja-JP |
| バミューダ諸島 | BM | ja-JP |
| ブータン | BT | ja-JP |
| ボリビア | BO | en-US, es-ES |
| ボネール島 | BQ | ja-JP |
| ボスニア・ヘルツェゴビナ | BA | ja-JP |
| ボツワナ | BW | ja-JP |
| ブーベ島 | BV | ja-JP |
| ブラジル | BR | en-US, pt-BR |
| 英領インド洋地域 | IO | ja-JP |
| 英領バージン諸島 | VG | ja-JP |
| ブルネイ | BN | ja-JP |
| ブルガリア | BG | en-US, bg-BG |
| ブルキナファソ | BF | ja-JP |
| ブルンジ | BI | ja-JP |
| コートジボワール | CI | en-US, fr-FR |
| カーボベルデ | CV | en-US, pt-PT |
| カンボジア | KH | ja-JP |
| カメルーン | CM | en-US, fr-FR |
| カナダ | CA | en-US, fr-FR |
| ケイマン諸島 | KY | en-US, en-US |
| 中央アフリカ共和国 | CF | ja-JP |
| チャド | TD | ja-JP |
| チリ | CL | en-US, es-ES |
| クリスマス島 | CX | ja-JP |
| ココス諸島 | CC | ja-JP |
| コロンビア | CO | en-US, es-ES |
| コモロ | KM | ja-JP |
| コンゴ民主共和国 | CD | ja-JP |
| コンゴ共和国 | CG | ja-JP |
| クック諸島 | CK | ja-JP |
| コスタリカ | CR | en-US, es-ES |
| クロアチア | HR | en-US, hr-HR |
| キュラソー島 | CW | ja-JP |
| キプロス | CY | ja-JP |
| Czechia | CZ | en-US, cs-CZ |
| デンマーク | DK | en-US, da-DK |
| ジブチ | DJ | ja-JP |
| ドミニカ国 | DM | ja-JP |
| ドミニカ共和国 | DO | en-US, es-ES |
| エクアドル | EC | ja-JP |
| エジプト | EG | en-US, ar-SA |
| エルサルバドル | SV | en-US, es-ES |
| 赤道ギニア | GQ | ja-JP |
| エリトリア | ER | ja-JP |
| エストニア | EE | en-US, et-EE |
| eSwatini | SZ | ja-JP |
| エチオピア | ET | ja-JP |
| フォークランド諸島 | FK | ja-JP |
| フェロー諸島 | FO | ja-JP |
| フィジー諸島 | FJ | ja-JP |
| フィンランド | FI | en-US, fi-FI |
| フランス | FR | en-US, fr-FR |
| フランス領ギアナ | GF | en-US, fr-FR  |
| フランス領ポリネシア | PF | ja-JP |
| 仏領極南諸島 | TF | ja-JP |
| ガボン | GA | ja-JP |
| ガンビア | GM | ja-JP |
| ジョージア | GE | ja-JP |
| ドイツ | DE | en-US, de-DE |
| ガーナ | GH | ja-JP |
| ジブラルタル | GI | ja-JP |
| ギリシャ | GR | en-US, el-GR |
| グリーンランド | GL | ja-JP |
| グレナダ | GD | ja-JP |
| グアドループ | GP | ja-JP |
| グアム | GU | ja-JP |
| グアテマラ | GT | en-US, es-ES |
| ガーンジー島 | GG | ja-JP |
| ギニア | GN | ja-JP |
| ギニアビサウ | GW | ja-JP |
| ガイアナ | GY | ja-JP |
| ハイチ | HT | ja-JP |
| ハード・マクドナルド諸島 | HM | ja-JP |
| ホンジュラス | HN | en-US, es-ES |
| 香港特別行政区 | HK | en-US, zh-HK |
| ハンガリー | HU | en-US, hu-HU |
| アイスランド | IS | ja-JP |
| インド | IN | en-US, hi-IN |
| インドネシア | ID | en-US, id-ID |
| イラク | IQ | en-US, ar-SA |
| アイルランド | Internet Explorer | ja-JP |
| マン島 | IM | ja-JP |
| イスラエル | IL | en-US, he-IL |
| イタリア | IT | en-US, it-IT |
| ジャマイカ | JM | ja-JP |
| ヤンマイエン島 | XJ | ja-JP |
| 日本 | JP | en-US, ja-JP |
| ジャージー島 | JE | ja-JP |
| ヨルダン | JO | en-US, ar-SA |
| カザフスタン | KZ | en-US, kk-KZ |
| ケニア | KE | ja-JP |
| キリバス | KI | ja-JP |
| 韓国 | KR | en-US, ko-KR |
| コソボ | XK | ja-JP |
| クウェート | KW | en-US, ar-SA |
| キルギス | KG | en-US, ru-RU |
| ラオス | LA | ja-JP |
| ラトビア | LV | en-US, lv-LV |
| レバノン | LB | en-US, ar-SA |
| レソト | LS | ja-JP |
| リベリア | LR | ja-JP |
| リビア | LY | en-US, ar-SA |
| リヒテンシュタイン | LI | en-US, de-DE |
| リトアニア | LT | en-US, lt-LT |
| ルクセンブルク | LU | en-US, fr-FR |
| マカオ | MO | en-US, zh-HK |
| マケドニア (旧ユーゴスラビア共和国) | MK | ja-JP |
| マダガスカル | MG | ja-JP |
| マラウイ | MW | ja-JP |
| マレーシア | MY | en-US, ms-MY |
| モルディブ | MV | ja-JP |
| マリ | ML | ja-JP |
| マルタ | MT | ja-JP |
| マーシャル諸島 | MH | ja-JP |
| マルチニーク島 | MQ | ja-JP |
| モーリタニア | [MR] | ja-JP |
| モーリシャス | MU | en-US, ar-SA |
| マイヨット島 | YT | ja-JP |
| メキシコ | MX | en-US, es-ES |
| ミクロネシア | FM | ja-JP |
| モルドバ | MD | en-US, ro-RO |
| モナコ | [MC] | en-US, fr-FR |
| モンゴル国 | MN | ja-JP |
| モンテネグロ | ME | ja-JP |
| モンセラット | [MS] | ja-JP |
| モロッコ | MA | en-US, fr-FR, en-US |
| モザンビーク | MZ | ja-JP |
| ミャンマー | MM | ja-JP |
| ナミビア | 該当なし | ja-JP |
| ナウル | NR | ja-JP |
| ネパール | NP | ja-JP |
| オランダ | NL | en-US, nl-NL |
| ニューカレドニア | NC | ja-JP |
| ニュージーランド | NZ | ja-JP |
| ニカラグア | NI | en-US, es-ES |
| ニジェール | NE | ja-JP |
| ナイジェリア | NG | ja-JP |
| ニウエ | NU | ja-JP |
| ノーフォーク島 | NF | ja-JP |
| 北マリアナ諸島 | MP | ja-JP |
| ノルウェー | 使用不可 | en-US, nb-NO |
| オマーン | OM | en-US, ar-SA |
| パキスタン | PK | ja-JP |
| パラオ | PW | ja-JP |
| パレスチナ自治政府 | PS | ja-JP |
| パナマ | PA | en-US, es-ES |
| パプアニューギニア | PG | ja-JP |
| パラグアイ | PY | en-US, es-ES |
| ペルー | PE | en-US, es-ES |
| フィリピン | PH | ja-JP |
| ピトケアン島 | PN | ja-JP |
| ポーランド | PL | en-US, pl-PL |
| ポルトガル | PT | en-US, pt-PT |
| プエルトリコ | PR | en-US, en-US |
| カタール | QA | en-US, ar-SA |
| レユニオン | RE | ja-JP |
| ルーマニア | RO | en-US, ro-RO |
| ロシア連邦 | RU | en-US, ru-RU |
| ルワンダ | RW | en-US, fr-FR |
| サントメ・プリンシペ | ST | en-US, fr-FR |
| サバ島 | XS | ja-JP |
| Saint-Barthélemy | BL | ja-JP |
| セントクリストファー・ネイビス | KN | ja-JP |
| セントルシア | LC | en-US, en-US |
| サンマルタン島 | MF | en-US, en-US |
| サンピエール・ミクロン | PM | ja-JP |
| セントビンセントおよびグレナディーン諸島 | VC | ja-JP |
| サモア | WS | ja-JP |
| サンマリノ | SM | ja-JP |
| サウジアラビア | SA | ja-JP |
| セネガル | SN | en-US, fr-FR |
| セルビア | RS | en-US, sr-Latn-RS, en-US |
| セーシェル | SC | ja-JP |
| シエラレオネ | SL | ja-JP |
| シンガポール | SG | en-US, zh-SG |
| シント・ユースタティウス島 | XE | ja-JP |
| シント・マールテン島 | SX | en-US, en-US |
| スロバキア | SK | en-US, sk-SK |
| スロベニア | SI | en-US, sl-SI |
| ソロモン諸島 | SB | ja-JP |
| ソマリア | SO | ja-JP |
| 南アフリカ | ZA | ja-JP |
| サウスジョージア・サウスサンドウィッチ諸島 | GS | ja-JP |
| 南スーダン | SS | ja-JP |
| スペイン | ES | en-US, es-ES, en-US, en-US |
| スリランカ | LK | ja-JP |
| セントヘレナ、アセンションおよびトリスタンダクーニャ | SH | ja-JP |
| スリナム | SR | ja-JP |
| スバールバル諸島 | SJ | ja-JP |
| スウェーデン | SE | en-US, sv-SE |
| スイス | CH | en-US, fr-FR, en-US, en-US |
| 台湾 | TW | en-US, zh-HK |
| タジキスタン | TJ | ja-JP |
| タンザニア | TZ | ja-JP |
| タイ | TH | en-US, th-TH |
| ティモール・レステ | TL | ja-JP |
| トーゴ | TG | ja-JP |
| トケラウ諸島 | TK | ja-JP |
| トンガ | TO | ja-JP |
| トリニダードトバゴ | TT | ja-JP |
| チュニジア | TN | en-US, fr-FR, en-US |
| トルコ | TR | en-US, tr-TR |
| トルクメニスタン | TM | ja-JP |
| タークス・カイコス諸島 | TC | ja-JP |
| ツバル | TV | ja-JP |
| 合衆国領有小離島 | UM | ja-JP |
| 米領バージン諸島 | VI | ja-JP |
| ウガンダ | UG | ja-JP |
| ウクライナ | UA | en-US, uk-UA |
| アラブ首長国連邦 | AE | en-US, ar-SA |
| 英国 | GB | ja-JP |
| 米国 | US | ja-JP |
| ウルグアイ | UY | en-US, es-ES |
| ウズベキスタン | UZ | en-US, ru-RU |
| バヌアツ | VU | ja-JP |
| バチカン市国 | VA | ja-JP |
| ベネズエラ | VE | en-US, es-ES |
| ベトナム | VN | en-US, vi-VN |
| ワリス・フテュナ諸島 | WF | ja-JP |
| イエメン | YE | en-US, ar-SA |
| ザンビア | ZM | ja-JP |
| ジンバブエ | ZW | ja-JP |


