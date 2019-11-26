---
title: Partner Center supported languages and locales
description: List of ISO2 and ISO3 supported locales for Partner Center.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6b066c4afb87656717327e57cef94ab84eb93309
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488292"
---
# <a name="partner-center-supported-languages-and-locales"></a>Partner Center supported languages and locales


**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

Some Partner Center APIs require a value indicating a locale, country or region. For example, the [Partner Center REST header](headers.md) X-Locale requires a value often in the format "language-country" ("en-US" indicates "English - United States").

In the Partner Center managed APIs, the [CountryValidationRules](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) class and the [OfferCategory.Locale](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest.CountryCode](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode), or [CustomerBillingProfile.Culture](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) properties require string values that indicate a language or country/region (in the form of an ISO2 language code or ISO3 country/region code), a locale, or a culture (a language ID combined with a country/region code).

The following table lists the cultures and International Standards Organization (ISO) country codes that are supported in the Partner Center APIs. 


| 国/地域                           | ISO Alpha 2 Country Code | ISO Alpha 3 Country Code | Supported Culture(s)                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| アフガニスタン                              | AF                       | AFG                      | ps-AF / en-US                         |
| オーランド諸島                            | AX                       | ALA                      | sv-SE / en-US                         |
| アルバニア                                  | AL                       | ALB                      | sq-AL / en-US                         |
| アルジェリア                                  | DZ                       | DZA                      | ar-DZ / en-US                         |
| 米領サモア                           | AS                       | ASM                      | ja-JP                                 |
| アンドラ                                  | AD                       | および                      | ca-ES / en-US                         |
| アンゴラ                                   | AO                       | AGO                      | pt-PT / en-US                         |
| アンギラ                                 | AI                       | AIA                      | ja-JP                                 |
| 南極                               | AQ                       | ATA                      | ja-JP                                 |
| アンティグア・バーブーダ                      | AG                       | ATG                      | ja-JP                                 |
| アルゼンチン                                | AR                       | ARG                      | es-AR / en-US                         |
| アルメニア                                  | AM                       | ARM                      | hy-AM / en-US                         |
| アルバ                                    | AW                       | ABW                      | nl-NL / en-US                         |
| オーストラリア                                | AU                       | AUS                      | en-AU / en-US                         |
| オーストリア                                  | AT                       | AUT                      | de-AT / en-US                         |
| アゼルバイジャン                               | AZ                       | AZE                      | az-Latn-AZ / en-US                    |
| バハマ                                  | BS                       | BHS                      | en-GB / en-US                         |
| バーレーン                                  | BH                       | BHR                      | ar-BH / en-US                         |
| バングラデシュ                               | BD                       | BGD                      | bn-BD / en-US                         |
| バルバドス                                 | BB                       | BRB                      | en-GB / en-US                         |
| ベラルーシ                                  | BY                       | BLR                      | be-BY / en-US                         |
| ベルギー                                  | BE                       | BEL                      | fr-BE / nl-BE / en-US                 |
| ベリーズ                                   | BZ                       | BLZ                      | en-BZ / en-US                         |
| ベナン                                    | BJ                       | BEN                      | fr-FR / en-US                         |
| バミューダ諸島                                  | BM                       | BMU                      | en-GB / en-US                         |
| ブータン                                   | BT                       | BTN                      | ja-JP                                 |
| ボリビア                                  | BO                       | BOL                      | es-BO / en-US                         |
| ボネール島                                  | BQ                       | BES                      | nl-NL / en-US                         |
| ボスニア・ヘルツェゴビナ                   | BA                       | BIH                      | bs-Latn-BA / en-US                    |
| ボツワナ                                 | BW                       | BWA                      | en-GB / en-US                         |
| ブーベ島                            | BV                       | BVT                      | nb-NO / en-US                         |
| ブラジル                                   | BR                       | BRA                      | pt-BR / en-US                         |
| 英領インド洋地域           | IO                       | IOT                      | ja-JP                                 |
| 英領バージン諸島                   | VG                       | VGB                      | ja-JP                                 |
| ブルネイ                                   | BN                       | BRN                      | ms-BN / en-US                         |
| ブルガリア                                 | BG                       | BGR                      | bg-BG / en-US                         |
| ブルキナファソ                             | BF                       | BFA                      | fr-FR / en-US                         |
| ブルンジ                                  | BI                       | BDI                      | fr-FR / en-US                         |
| カーボベルデ                               | CV                       | CPV                      | pt-CV / en-US                         |
| カンボジア                                 | KH                       | KHM                      | km-KH / en-US                         |
| カメルーン                                 | CM                       | CMR                      | fr-FR / en-US                         |
| カナダ                                   | CA                       | CAN                      | fr-CA / en-US                         |
| ケイマン諸島                           | KY                       | CYM                      | en-GB / en-US                         |
| 中央アフリカ共和国                 | CF                       | CAF                      | fr-FR / en-US                         |
| チャド                                     | TD                       | TCD                      | fr-FR / en-US                         |
| チリ                                    | CL                       | CHL                      | es-CL / en-US                         |
| 中国                                    | CN                       | CHN                      | zh-CN / en-US                         |
| クリスマス島                         | CX                       | CXR                      | ja-JP                                 |
| ココス諸島                  | CC                       | CCK                      | ja-JP                                 |
| コロンビア                                 | CO                       | COL                      | es-CO / en-US                         |
| コモロ                                  | KM                       | COM                      | fr-FR / en-US                         |
| コンゴ共和国                                    | CG                       | COG                      | fr-FR / en-US                         |
| コンゴ民主共和国                              | CD                       | COD                      | fr-FR / en-US                         |
| クック諸島                             | CK                       | COK                      | ja-JP                                 |
| コスタリカ                               | CR                       | CRI                      | es-CR / en-US                         |
| コートジボワール                            | CI                       | CIV                      | fr-FR / en-US                         |
| クロアチア                                  | HR                       | HRV                      | hr-HR / en-US                         |
| キュラソー島                                  | CW                       | CUW                      | nl-NL / en-US                         |
| キプロス                                   | CY                       | CYP                      | el-GR / en-US                         |
| Czechia                                  | CZ                       | CZE                      | cs-CZ / en-US                         |
| デンマーク                                  | DK                       | DNK                      | da-DK / en-US                         |
| ジブチ                                 | DJ                       | DJI                      | fr-FR / en-US                         |
| ドミニカ国                                 | DM                       | DMA                      | ja-JP                                 |
| ドミニカ共和国                       | DO                       | DOM                      | es-DO / en-US                         |
| エクアドル                                  | EC                       | ECU                      | es-EC / en-US                         |
| エジプト                                    | EG                       | EGY                      | ar-EG / en-US                         |
| エルサルバドル                              | SV                       | SLV                      | es-SV / en-US                         |
| 赤道ギニア                        | GQ                       | GNQ                      | es-ES / en-US                         |
| エリトリア                                  | ER                       | ERI                      | ar-SA / en-US                         |
| エストニア                                  | EE                       | EST                      | et-EE / en-US                         |
| eSwatini                                 | SZ                       | SWZ                      | ja-JP                                 |
| エチオピア                                 | ET                       | ETH                      | am-ET / en-US                         |
| フォークランド諸島                         | FK                       | FLK                      | ja-JP                                 |
| フェロー諸島                            | FO                       | FRO                      | fo-FO / en-US                         |
| フィジー諸島                                     | FJ                       | FJI                      | en-GB / en-US                         |
| フィンランド                                  | FI                       | FIN                      | fi-FI / sv-FI / en-US                 |
| フランス                                   | FR                       | FRA                      | fr-FR / en-US                         |
| フランス領ギアナ                            | GF                       | GUF                      | fr-FR / en-US                         |
| フランス領ポリネシア                         | PF                       | PYF                      | fr-FR / en-US                         |
| 仏領極南諸島              | TF                       | ATF                      | fr-FR / en-US                         |
| ガボン                                    | GA                       | GAB                      | fr-FR / en-US                         |
| ガンビア                                   | GM                       | GMB                      | ja-JP                                 |
| ジョージア                                  | GE                       | GEO                      | ka-GE / en-US                         |
| ドイツ                                  | DE                       | DEU                      | de-DE / en-US                         |
| ガーナ                                    | GH                       | GHA                      | en-GB / en-US                         |
| ジブラルタル                                | GI                       | GIB                      | ja-JP                                 |
| ギリシャ                                   | GR                       | GRC                      | el-GR / en-US                         |
| グリーンランド                                | GL                       | GRL                      | da-DK / en-US                         |
| グレナダ                                  | GD                       | GRD                      | ja-JP                                 |
| グアドループ                               | GP                       | GLP                      | fr-FR / en-US                         |
| グアム                                     | GU                       | GUM                      | ja-JP                                 |
| グアテマラ                                | GT                       | GTM                      | es-GT / en-US                         |
| ガーンジー島                                 | GG                       | GGY                      | ja-JP                                 |
| ギニア                                   | GN                       | GIN                      | fr-FR / en-US                         |
| ギニアビサウ                            | GW                       | GNB                      | pt-PT / en-US                         |
| ガイアナ                                   | GY                       | GUY                      | ja-JP                                 |
| ハイチ                                    | HT                       | HTI                      | fr-FR / en-US                         |
| ハード・マクドナルド諸島        | HM                       | HMD                      | ja-JP                                 |
| ホンジュラス                                 | HN                       | HND                      | es-HN / en-US                         |
| 香港特別行政区                            | HK                       | HKG                      | zh-HK / en-US                         |
| ハンガリー                                  | HU                       | HUN                      | hu-HU / en-US                         |
| アイスランド                                  | IS                       | ISL                      | is-IS / en-US                         |
| インド                                    | IN                       | IND                      | en-IN / hi-IN / en-US                 |
| インドネシア                                | ID                       | IDN                      | id-ID / en-US                         |
| イラク                                     | IQ                       | IRQ                      | ar-IQ / en-US                         |
| アイルランド                                  | Internet Explorer                       | IRL                      | en-IE / en-US                         |
| マン島                              | IM                       | IMN                      | ja-JP                                 |
| イスラエル                                   | IL                       | ISR                      | he-IL / en-US                         |
| イタリア                                    | IT                       | ITA                      | it-IT / en-US                         |
| ジャマイカ                                  | JM                       | JAM                      | en-JM / en-US                         |
| ヤンマイエン島                                | XJ                       | XJA                      | nb-NO / en-US                         |
| 日本                                    | JP                       | JPN                      | ja-JP / en-US                         |
| ジャージー島                                   | JE                       | JEY                      | ja-JP                                 |
| ヨルダン                                   | JO                       | JOR                      | ar-JO / en-US                         |
| カザフスタン                               | KZ                       | KAZ                      | kk-KZ / en-US                         |
| ケニア                                    | KE                       | KEN                      | sw-KE / en-US                         |
| キリバス                                 | KI                       | KIR                      | ja-JP                                 |
| 韓国                                    | KR                       | KOR                      | ko-KR / en-US                         |
| コソボ                                   | XK                       | XKS                      | ja-JP                                 |
| クウェート                                   | KW                       | KWT                      | ar-KW / en-US                         |
| キルギス                               | KG                       | KGZ                      | ky-KG / en-US                         |
| ラオス                                     | LA                       | LAO                      | lo-LA / en-US                         |
| ラトビア                                   | LV                       | LVA                      | lv-LV / en-US                         |
| レバノン                                  | LB                       | LBN                      | ar-LB / en-US                         |
| レソト                                  | LS                       | LSO                      | ja-JP                                 |
| リベリア                                  | LR                       | LBR                      | ja-JP                                 |
| リビア                                    | LY                       | LBY                      | ar-LY / en-US                         |
| リヒテンシュタイン                            | LI                       | LIE                      | de-LI / en-US                         |
| リトアニア                                | LT                       | LTU                      | lt-LT / en-US                         |
| ルクセンブルク                               | LU                       | LUX                      | de-LU / fr-LU / en-US                 |
| マカオ                                | MO                       | MAC                      | zh-MO / en-US                         |
| マケドニア (旧ユーゴスラビア共和国)                          | MK                       | MKD                      | mk-MK / en-US                         |
| マダガスカル                               | MG                       | MDG                      | fr-FR / en-US                         |
| マラウイ                                   | MW                       | MWI                      | ja-JP                                 |
| マレーシア                                 | MY                       | MYS                      | en-MY / en-US                         |
| モルディブ                                 | MV                       | MDV                      | dv-MV / en-US                         |
| マリ                                     | ML                       | MLI                      | fr-FR / en-US                         |
| マルタ                                    | MT                       | MLT                      | mt-MT / en-US                         |
| マーシャル諸島                         | MH                       | MHL                      | ja-JP                                 |
| マルチニーク島                               | MQ                       | MTQ                      | fr-FR / en-US                         |
| モーリタニア                               | [MR]                       | MRT                      | ar-SA / en-US                         |
| モーリシャス                                | MU                       | MUS                      | en-GB / en-US                         |
| マイヨット島                                  | YT                       | MYT                      | fr-FR / en-US                         |
| メキシコ                                   | MX                       | MEX                      | es-MX / en-US                         |
| ミクロネシア                               | FM                       | FSM                      | ja-JP                                 |
| モルドバ                                  | MD                       | MDA                      | ro-RO / en-US                         |
| モナコ                                   | [MC]                       | MCO                      | fr-MC / en-US                         |
| モンゴル国                                 | MN                       | MNG                      | mn-MN / en-US                         |
| モンテネグロ                               | ME                       | MNE                      | sr-Latn-ME / en-US                    |
| モンセラット                               | [MS]                       | MSR                      | ja-JP                                 |
| モロッコ                                  | MA                       | MAR                      | ar-MA / en-US                         |
| モザンビーク                               | MZ                       | MOZ                      | pt-PT / en-US                         |
| ミャンマー                                  | MM                       | MMR                      | ja-JP                                 |
| ナミビア                                  | 該当なし                       | NAM                      | en-GB / en-US                         |
| ナウル                                    | NR                       | NRU                      | ja-JP                                 |
| ネパール                                    | NP                       | NPL                      | ne-NP / en-US                         |
| オランダ領アンティル                     | AN                       | ANT                      | ja-JP                                 |
| Netherlands, The                         | NL                       | NLD                      | nl-NL / en-US                         |
| ニューカレドニア                            | NC                       | NCL                      | fr-FR / en-US                         |
| ニュージーランド                              | NZ                       | NZL                      | en-NZ / en-US                         |
| ニカラグア                                | NI                       | NIC                      | es-NI / en-US                         |
| ニジェール                                    | NE                       | NER                      | fr-FR / en-US                         |
| ナイジェリア                                  | NG                       | NGA                      | ha-Latn-NG / en-US                    |
| ニウエ                                     | NU                       | NIU                      | ja-JP                                 |
| ノーフォーク島                           | NF                       | NFK                      | ja-JP                                 |
| 北マリアナ諸島                 | MP                       | MNP                      | ja-JP                                 |
| ノルウェー                                   | 使用不可                       | NOR                      | nb-NO / en-US                         |
| オマーン                                     | OM                       | OMN                      | ar-OM / en-US                         |
| パキスタン                                 | PK                       | PAK                      | ur-PK / en-US                         |
| パラオ                                    | PW                       | PLW                      | ja-JP                                 |
| パレスチナ自治政府                    | PS                       | PSE                      | ar-SA / en-US                         |
| パナマ                                   | PA                       | PAN                      | es-PA / en-US                         |
| パプアニューギニア                         | PG                       | PNG                      | ja-JP                                 |
| パラグアイ                                 | PY                       | PRY                      | es-PY / en-US                         |
| ペルー                                     | PE                       | PER                      | es-PE / en-US                         |
| フィリピン                              | PH                       | PHL                      | en-PH / en-US                         |
| ピトケアン島                         | PN                       | PCN                      | ja-JP                                 |
| ポーランド                                   | PL                       | POL                      | pl-PL / en-US                         |
| ポルトガル                                 | PT                       | PRT                      | pt-PT / en-US                         |
| プエルトリコ                              | PR                       | PRI                      | es-PR / en-US                         |
| カタール                                    | QA                       | QAT                      | ar-QA / en-US                         |
| レユニオン                                  | RE                       | REU                      | fr-FR / en-US                         |
| ルーマニア                                  | RO                       | ROU                      | ro-RO / en-US                         |
| ロシア連邦                                   | RU                       | RUS                      | ru-RU / en-US                         |
| ルワンダ                                   | RW                       | RWA                      | rw-RW / en-US                         |
| サバ島                                     | XS                       | XSA                      | nl-NL / en-US                         |
| セントクリストファー・ネイビス                    | KN                       | KNA                      | en-GB / en-US                         |
| セントルシア                              | LC                       | LCA                      | ja-JP                                 |
| サンマルタン島                             | MF                       | MAF                      | fr-FR / en-US                         |
| サンピエール・ミクロン                | PM                       | SPM                      | fr-FR / en-US                         |
| セントビンセントおよびグレナディーン諸島         | VC                       | VCT                      | ja-JP                                 |
| Saint-Barthélemy                         | BL                       | BLM                      | fr-FR / en-US                         |
| サモア                                    | WS                       | WSM                      | ja-JP                                 |
| サンマリノ                               | SM                       | SMR                      | it-IT / en-US                         |
| サントメ・プリンシペ                    | ST                       | STP                      | pt-PT / en-US                         |
| サウジアラビア                             | SA                       | SAU                      | ar-SA / en-US                         |
| セネガル                                  | SN                       | SEN                      | wo-SN / en-US                         |
| セルビア                                   | RS                       | SRB                      | sr-Latn-RS / sr-Cyrl-RS / en-US       |
| セーシェル                               | SC                       | SYC                      | ja-JP                                 |
| シエラレオネ                             | SL                       | SLE                      | ja-JP                                 |
| シンガポール                                | SG                       | SGP                      | en-SG / zh-SG / en-US                 |
| シント・ユースタティウス島                           | XE                       | XSE                      | nl-NL / en-US                         |
| シント・マールテン島                             | SX                       | SXM                      | ja-JP                                 |
| スロバキア                                 | SK                       | SVK                      | sk-SK / en-US                         |
| スロベニア                                 | SI                       | SVN                      | sl-SI / en-US                         |
| ソロモン諸島                          | SB                       | SLB                      | ja-JP                                 |
| ソマリア                                  | SO                       | SOM                      | ar-SA / en-US                         |
| 南アフリカ                             | ZA                       | ZAF                      | en-ZA / en-US                         |
| サウスジョージア・サウスサンドウィッチ諸島 | GS                       | SGS                      | ja-JP                                 |
| 南スーダン                              | SS                       | SSD                      | ja-JP                                 |
| スペイン                                    | ES                       | ESP                      | es-ES / ca-ES / eu-ES / gl-ES / en-US |
| スリランカ                                | LK                       | LKA                      | si-LK / en-US                         |
| セントヘレナ、アセンションおよびトリスタンダクーニャ   | SH                       | SHN                      | ja-JP                                 |
| スリナム                                 | SR                       | SUR                      | nl-NL                                 |
| スバールバル諸島                                 | SJ                       | SJM                      | nb-NO / en-US                         |
| スウェーデン                                   | SE                       | SWE                      | sv-SE / en-US                         |
| スイス                              | CH                       | CHE                      | de-CH / fr-CH / it-CH / en-US         |
| 台湾                                   | TW                       | TWN                      | zh-TW / en-US                         |
| タジキスタン                               | TJ                       | TJK                      | tg-Cyrl-TJ / en-US                    |
| タンザニア                                 | TZ                       | TZA                      | en-GB / en-US                         |
| タイ                                 | TH                       | THA                      | th-TH / en-US                         |
| ティモール・レステ                              | TL                       | TLS                      | pt-PT / en-US                         |
| トーゴ                                     | TG                       | TGO                      | fr-FR / en-US                         |
| トケラウ諸島                                  | TK                       | TKL                      | ja-JP                                 |
| トンガ                                    | TO                       | TON                      | ja-JP                                 |
| トリニダードトバゴ                      | TT                       | TTO                      | en-TT / en-US                         |
| チュニジア                                  | TN                       | TUN                      | ar-TN / en-US                         |
| トルコ                                   | TR                       | TUR                      | tr-TR / en-US                         |
| トルクメニスタン                             | TM                       | TKM                      | tk-TM / en-US                         |
| タークス・カイコス諸島                 | TC                       | TCA                      | ja-JP                                 |
| ツバル                                   | TV                       | TUV                      | ja-JP                                 |
| ウガンダ                                   | UG                       | UGA                      | en-GB / en-US                         |
| ウクライナ                                  | UA                       | UKR                      | uk-UA / en-US                         |
| アラブ首長国連邦                     | AE                       | ARE                      | ar-AE / en-US                         |
| 英国                           | GB                       | GBR                      | en-GB / en-US                         |
| 合衆国領有小離島                    | UM                       | UMI                      | ja-JP                                 |
| 米領バージン諸島                      | VI                       | VIR                      | ja-JP                                 |
| 米国                            | US                       | USA                      | en-US / es-US                         |
| ウルグアイ                                  | UY                       | URY                      | es-UY / en-US                         |
| ウズベキスタン                               | UZ                       | UZB                      | uz-Latn-UZ / en-US                    |
| バヌアツ                                  | VU                       | VUT                      | ja-JP                                 |
| バチカン市国                             | VA                       | VAT                      | it-IT / en-US                         |
| ベネズエラ                                | VE                       | VEN                      | es-VE / en-US                         |
| ベトナム                                  | VN                       | VNM                      | vi-VN / en-US                         |
| ワリス・フテュナ諸島                        | WF                       | WLF                      | fr-FR / en-US                         |
| イエメン                                    | YE                       | YEM                      | ar-YE / en-US                         |
| ザンビア                                   | ZM                       | ZMB                      | en-GB / en-US                         |
| ジンバブエ                                 | ZW                       | ZWE                      | en-ZW / en-US                         |

