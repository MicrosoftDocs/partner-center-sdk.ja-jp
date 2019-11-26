---
title: Microsoft カスタマーアグリーメントテンプレートのダウンロードリンクを取得する
description: Microsoft カスタマーアグリーメントテンプレートのダウンロードリンクを取得します。
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
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Microsoft カスタマーアグリーメントテンプレートのダウンロードリンクを取得する

適用対象:

- パートナー センター

**AgreementDocument**リソースは、現在、 *Microsoft パブリッククラウド*のパートナーセンターでのみサポートされています。 このリソースはに適用されません:

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

この記事では、顧客の国と言語に基づいて、Microsoft カスタマーアグリーメントテンプレートをダウンロードするためのリンクを取得する方法について説明します。

## <a name="prerequisites"></a>前提条件

- パートナーセンター .NET SDK を使用している場合は、バージョン1.14 以降が必要です。
- 「[パートナーセンターの認証](./partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、アプリとユーザー認証のみがサポートされます。
- Microsoft カスタマーアグリーメントテンプレートが適用される顧客の国。
- Microsoft カスタマーアグリーメントテンプレートをローカライズする言語。

> [!IMPORTANT]
> - Microsoft カスタマーアグリーメントは、国によって異なります。 Microsoft カスタマーアグリーメントテンプレートをダウンロードするためのリンクを要求する場合は、顧客の所在地に基づいて正しい国を指定するようにしてください。 サポートされている国の一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。
> - 一部の国では、Microsoft カスタマー契約を複数の言語で利用できます。 最適なカスタマーエクスペリエンスを実現するには、お客様のニーズに最も合った言語を選択してください。 サポートされている言語の一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。
> - この方法は、Microsoft カスタマーアグリーメントでのみサポートされています。 Microsoft Cloud アグリーメントテンプレートのダウンロードリンクを取得するために使用することはできません。

## <a name="net"></a>.NET

Microsoft カスタマーアグリーメントテンプレートをダウンロードするためのリンクを取得するには、次のようにします。

1. Microsoft カスタマーアグリーメントの契約メタデータを取得します。 Microsoft カスタマーアグリーメントの**templateId**を取得する必要があります。 詳細については、「 [Microsoft Customer agreement の契約メタデータを取得する](get-customer-agreement-metadata.md)」を参照してください。

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
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

var agreementDocument = partnerOperations.AgreementTemplates.ById(microsoftCustomerAgreementDetails.TemplateId).Document.ByCountry(customerCountry).ByLanguage(languageForLocalization).Get();
```

完全なサンプルは、[コンソールテストアプリ](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)プロジェクトの[GetAgreementDocument](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDocument.cs)クラスにあります。


## <a name="rest-request"></a>REST 要求

Microsoft カスタマーアグリーメントテンプレートをダウンロードするためのリンクを取得するには、次のようにします。

1. Microsoft カスタマーアグリーメントの契約メタデータを取得します。 Microsoft カスタマーアグリーメントの**templateId**を取得する必要があります。 詳細については、「 [Microsoft Customer agreement の契約メタデータを取得する](get-customer-agreement-metadata.md)」を参照してください。
2. REST 要求を作成して、 [ **AgreementDocument**リソース](./agreement-document-resources.md)をフェッチします。 例については、「[要求構文](#request-syntax)の例」を参照してください。 次の情報を指定する必要があります。
    - Microsoft カスタマーアグリーメントの**templateId** 。
    - Microsoft カスタマー契約テンプレートが適用される国。
    - Microsoft カスタマーアグリーメントテンプレートをローカライズする言語。

### <a name="request-syntax"></a>要求の構文

このリソースには次の要求構文を使用します。

| メソッド | 要求 URI |
|--------|---------------------------------------------------------------------|
| GET | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document? language = {language} & country = {COUNTRY} HTTP/1.1 |

### <a name="uri-parameters"></a>URI パラメーター

要求では、次の URI パラメーターを使用できます。

| 名前                   | 種類   | 必須 | 説明                                 |
|------------------------|--------|----------|---------------------------------------------|
| 契約テンプレート-id  | string | 〇      | 契約の種類を表す一意の識別子。 Microsoft Customer Agreement の契約メタデータを取得することによって、templateId for Microsoft Customer Agreement を取得できます。 詳細については、「 [Microsoft Customer agreement の契約メタデータを取得する](./get-customer-agreement-metadata.md)」を参照してください。 このパラメーターでは **、大文字と小文字が区別**されます。|
| country                | string | X       | アグリーメントテンプレートを適用する国を指定します。 パラメーターが指定されていない場合、クエリの既定値は*US*です。 サポートされている国コードの一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。|
| 言語               | string | X       | アグリーメントテンプレートのローカライズに使用する言語を指定します。 パラメーターが指定されていない場合、または指定された国に対して指定された国コードがサポートされていない場合、クエリの既定値は*en-us*です。 サポートされている国コードの一覧については、[サポートされている国と言語の一覧](#list-of-supported-countries-and-languages)を参照してください。|

### <a name="request-headers"></a>要求ヘッダー

詳細については、「[パートナーセンターの REST ヘッダー](headers.md)」を参照してください。

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

## <a name="rest-response"></a>REST 応答

成功した場合、このメソッドは応答本文で[ **AgreementDocument**リソース](./agreement-document-resources.md)を返します。

リソースには、ライセンステンプレートをダウンロードするために使用できる URL 文字列を含む**downloaduri**プロパティがあります。 クエリを作成するたびに、別のリンクが返されます。 このリンクは、5分後に有効期限が切れます。

### <a name="response-success-and-error-codes"></a>応答成功およびエラーコード

各応答には、成功、失敗、および追加のデバッグ情報を示す HTTP ステータスコードが付属しています。

ネットワークトレースツールを使用して、このコード、エラーの種類、およびその他のパラメーターを読み取ります。 完全な一覧については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

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

| Country                   | 国番号   | サポートされている言語コード |
|------------------------|--------|----------|
| オーランド諸島 | AX | en-US |
| アフガニスタン | AF | en-US |
| アルバニア | AL | en-US |
| アルジェリア | DZ | en-us, fr-fr, en-us, en-us |
| 米領サモア | AS | en-US |
| アンドラ | AD | en-US |
| アンゴラ | AO | en-us、pt-PT |
| アンギラ | AI | en-US |
| 南極 | 以降 | en-US |
| アンティグア・バーブーダ | AG | en-US |
| アルゼンチン | AR | en-us、es |
| アルメニア | AM | en-US |
| アルバ | AW | en-US |
| オーストラリア | AU | en-US |
| オーストリア | AT | en-us、de |
| アゼルバイジャン | AZ | en-US |
| バハマ | BS | en-US |
| バーレーン | BH | en-us、ar-SA |
| バングラデシュ | BD | en-US |
| バルバドス | BB | en-US |
| ベラルーシ | BY | en-us、ru-RU |
| ベルギー | BE | en-us、nl-NL |
| ベリーズ | BZ | en-us、es |
| ベナン | BJ | en-US |
| バミューダ諸島 | BM.EXE | en-US |
| ブータン | BT | en-US |
| ボリビア | BO | en-us、es |
| ボネール島 | BQ | en-US |
| ボスニア・ヘルツェゴビナ | BA | en-US |
| ボツワナ | BW | en-US |
| ブーベ島 | BV | en-US |
| ブラジル | BR | en-us、pt-BR |
| 英領インド洋地域 | IO | en-US |
| 英領バージン諸島 | VG | en-US |
| ブルネイ | BN | en-US |
| ブルガリア | BG | en-us、bg-BG |
| ブルキナファソ | BF | en-US |
| ブルンジ | POWER | en-US |
| コートジボワール | CI | en-us、fr-fr |
| カーボベルデ | CV | en-us、pt-PT |
| カンボジア | KH | en-US |
| カメルーン | CM | en-us、fr-fr |
| カナダ | CA | en-us、fr-fr |
| ケイマン諸島 | アヒル | en-us、en-us |
| 中央アフリカ共和国 | CF | en-US |
| チャド | TD | en-US |
| チリ | CL | en-us、es |
| クリスマス島 | シリーズ | en-US |
| ココス諸島 | CC | en-US |
| コロンビア | CO | en-us、es |
| コモロ | KM | en-US |
| コンゴ民主共和国 | CD | en-US |
| コンゴ共和国 | 抗力 | en-US |
| クック諸島 | CK | en-US |
| コスタリカ | CR | en-us、es |
| クロアチア | HR | en-us、hr-HR |
| キュラソー島 | 数量 | en-US |
| キプロス | CY | en-US |
| Czechia | CZ | en-us, cs-CS-CZ |
| デンマーク | DK | en-us、da-DK |
| ジブチ | DJ | en-US |
| ドミニカ国 | DATA | en-US |
| ドミニカ共和国 | DO | en-us、es |
| エクアドル | EC | en-US |
| エジプト | EG | en-us、ar-SA |
| エルサルバドル | SV | en-us、es |
| 赤道ギニア | GQ | en-US |
| エリトリア | 壁紙 | en-US |
| エストニア | EE | en-us、et-EE |
| eSwatini | SZ | en-US |
| エチオピア | ET | en-US |
| フォークランド諸島 | FK (FK) | en-US |
| フェロー諸島 | FO | en-US |
| フィジー諸島 | FJ | en-US |
| フィンランド | FI | en-us、fi FI |
| フランス | FR | en-us、fr-fr |
| フランス領ギアナ | GF | en-us、fr-fr  |
| フランス領ポリネシア | PF | en-US |
| 仏領極南諸島 | WORKSPACES | en-US |
| ガボン | GA | en-US |
| ガンビア | GM | en-US |
| ジョージア | GE | en-US |
| ドイツ | DE | en-us、de |
| ガーナ | GH | en-US |
| ジブラルタル | GI | en-US |
| ギリシャ | GR | en-us、el-GR |
| グリーンランド | GL | en-US |
| グレナダ | GD | en-US |
| グアドループ | GP | en-US |
| グアム | GU | en-US |
| グアテマラ | GT | en-us、es |
| ガーンジー島 | GG | en-US |
| ギニア | GN | en-US |
| ギニアビサウ | GW | en-US |
| ガイアナ | GY | en-US |
| ハイチ | HT | en-US |
| ハード・マクドナルド諸島 | HM | en-US |
| ホンジュラス | HN | en-us、es |
| 香港特別行政区 | HK | en-us、zh-tw-HK |
| ハンガリー | HU | en-us、hu-HU |
| アイスランド | IS | en-US |
| インド | IN | en-us、こんにちは |
| インドネシア | ID | en-us、id-ID |
| イラク | IQ | en-us、ar-SA |
| アイルランド | Internet Explorer | en-US |
| マン島 | IM | en-US |
| イスラエル | IL | en-us、he |
| イタリア | IT | en-us、it |
| ジャマイカ | JM | en-US |
| ヤンマイエン島 | XJ | en-US |
| 日本 | JP | en-us、ja-jp |
| ジャージー島 | JE | en-US |
| ヨルダン | JO | en-us、ar-SA |
| カザフスタン | KZ | en-us、kk-KZ |
| ケニア | KE | en-US |
| キリバス | KI | en-US |
| 韓国 | KR | en-us、ko-韓国 |
| コソボ | XK | en-US |
| クウェート | KW | en-us、ar-SA |
| キルギス | KG | en-us、ru-RU |
| ラオス | LA | en-US |
| ラトビア | LV | en-us、lv-LV |
| レバノン | LB | en-us、ar-SA |
| レソト | AVL | en-US |
| リベリア | LR | en-US |
| リビア | LY | en-us、ar-SA |
| リヒテンシュタイン | & | en-us、de |
| リトアニア | LT | en-us、lt-LT |
| ルクセンブルク | LU | en-us、fr-fr |
| マカオ | 月 | en-us、zh-tw-HK |
| マケドニア (旧ユーゴスラビア共和国) | MK | en-US |
| マダガスカル | MG | en-US |
| マラウイ | MW | en-US |
| マレーシア | MY | en-us、ms-MY |
| モルディブ | MV | en-US |
| マリ | ML | en-US |
| マルタ | MT | en-US |
| マーシャル諸島 | MH | en-US |
| マルチニーク島 | MQ | en-US |
| モーリタニア | MR | en-US |
| モーリシャス | MU | en-us、ar-SA |
| マイヨット島 | YT | en-US |
| メキシコ | MX | en-us、es |
| ミクロネシア | 今 | en-US |
| モルドバ | MD | en-us、ro-RO |
| モナコ | [MC] | en-us、fr-fr |
| モンゴル | MN | en-US |
| モンテネグロ | ME | en-US |
| モンセラット | MS | en-US |
| モロッコ | MA | en-us, fr-fr, en-us, en-us |
| モザンビーク | MZ | en-US |
| ミャンマー | MM | en-US |
| ナミビア | 該当なし | en-US |
| ナウル | NR | en-US |
| ネパール | NP | en-US |
| オランダ | NL | en-us、nl-NL |
| ニューカレドニア | 加工 | en-US |
| ニュージーランド | NZ | en-US |
| ニカラグア | NI | en-us、es |
| ニジェール | NE | en-US |
| ナイジェリア | NG | en-US |
| ニウエ | ニュー | en-US |
| ノーフォーク島 | ユーティリティー | en-US |
| 北マリアナ諸島 | MP | en-US |
| ノルウェー | 使用不可 | en-us、nb-いいえ |
| オマーン | OM | en-us、ar-SA |
| パキスタン | PK | en-US |
| パラオ | PW | en-US |
| パレスチナ自治政府 | PS | en-US |
| パナマ | PA | en-us、es |
| パプアニューギニア | 画面 | en-US |
| パラグアイ | PY | en-us、es |
| ペルー | PE | en-us、es |
| フィリピン | PH | en-US |
| ピトケアン島 | PN | en-US |
| ポーランド | PL | en-us、pl-PL |
| ポルトガル | PT | en-us、pt-PT |
| プエルトリコ | PR | en-us、en-us |
| カタール | QA | en-us、ar-SA |
| レユニオン | RE | en-US |
| ルーマニア | RO | en-us、ro-RO |
| ロシア | RU | en-us、ru-RU |
| ルワンダ | RW | en-us、fr-fr |
| サントメ・プリンシペ | ST | en-us、fr-fr |
| サバ島 | XS | en-US |
| サン・バルテルミー | BL | en-US |
| セントクリストファー・ネイビス | KN | en-US |
| セントルシア | 小 | en-us、en-us |
| サンマルタン島 | メイン | en-us、en-us |
| サンピエール・ミクロン | PM | en-US |
| セントビンセントおよびグレナディーン諸島 | VC-1 | en-US |
| サモア | WS | en-US |
| サンマリノ | MANAGER | en-US |
| サウジアラビア | SA | en-US |
| セネガル | SN | en-us、fr-fr |
| セルビア | RS | en-us、Latn、英語 (米国) |
| セーシェル | SC | en-US |
| シエラレオネ | SL | en-US |
| シンガポール | SG | en-us、zh-tw |
| シント・ユースタティウス島 | XE | en-US |
| シント・マールテン島 | SX | en-us、en-us |
| スロバキア | SK | en-us、sk-SK |
| スロベニア | SI | en-us、sl-SI |
| ソロモン諸島 | SB | en-US |
| ソマリア | だから | en-US |
| 南アフリカ | ZA | en-US |
| サウスジョージア・サウスサンドウィッチ諸島 | GS | en-US |
| 南スーダン | 秒 | en-US |
| スペイン | ES | en-us、es ES、en-us、en-us、en-us |
| スリランカ | LK | en-US |
| セントヘレナ、アセンションおよびトリスタンダクーニャ | 悪夢 | en-US |
| スリナム | SR | en-US |
| スバールバル諸島 | SJ | en-US |
| スウェーデン | SE | en-us、sv-SE |
| スイス | CH | en-us、fr-fr、en-us、en-us (en-us) |
| 台湾 | TW | en-us、zh-tw-HK |
| タジキスタン | TJ | en-US |
| タンザニア | TZ | en-US |
| タイ | TH | en-us、th |
| ティモール・レステ | TL | en-US |
| トーゴ | TG | en-US |
| トケラウ諸島 | TK | en-US |
| トンガ | TO | en-US |
| トリニダードトバゴ | TT | en-US |
| チュニジア | TN | en-us, fr-fr, en-us, en-us |
| トルコ | TR | en-us、tr-TR |
| トルクメニスタン | メモリ | en-US |
| タークス・カイコス諸島 | フィールド | en-US |
| ツバル | TV | en-US |
| 合衆国領有小離島 | UM | en-US |
| 米領バージン諸島 | VI | en-US |
| ウガンダ | UG | en-US |
| ウクライナ | UA | en-us、uk-UA |
| アラブ首長国連邦 | AE | en-us、ar-SA |
| イギリス | GB | en-US |
| 米国 | US | en-US |
| ウルグアイ | UY | en-us、es |
| ウズベキスタン | UZ | en-us、ru-RU |
| バヌアツ | VU | en-US |
| バチカン市国 | VA | en-US |
| ベネズエラ | VE | en-us、es |
| ベトナム | VN | en-us、vi-VN |
| ワリス・フテュナ諸島 | WF | en-US |
| イエメン | なん信仰 | en-us、ar-SA |
| ザンビア | ZM | en-US |
| ジンバブエ | ZW | en-US |


