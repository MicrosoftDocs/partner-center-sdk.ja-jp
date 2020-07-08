---
title: パートナー センターでサポートされている言語とロケール
description: パートナーセンターでサポートされている ISO2 と ISO3 のロケールの一覧。
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 38dad24ec1a10357bb60467dcdac2816aea89e91
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095030"
---
# <a name="partner-center-supported-languages-and-locales"></a>パートナー センターでサポートされている言語とロケール

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

一部のパートナーセンター Api では、ロケール、国、または地域を示す値が必要です。 たとえば、[パートナーセンターの REST ヘッダー](headers.md)の X ロケールでは、"言語-国" という形式の値が必要です ("en-us" は "English-米国" を示します)。

パートナーセンターマネージ Api では、 [CountryValidationRules](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules)クラスと OfferCategory、 [ServiceRequest、CountryCode](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode)、または[OfferCategory.Locale](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale)の各プロパティに、言語、国/地域 (ISO2 言語コードまたは ISO3 country/region コードの形式)、ロケール、またはカルチャ (国/地域コードと組み合わせた言語 ID) を示す文字列値が必要[です](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture)。

次の表は、パートナーセンターの Api でサポートされているカルチャと国際標準化機構 (ISO) の国コードを示しています。

| 国/地域                           | ISO Alpha 2 国コード | ISO Alpha 3 国コード | サポートされているカルチャ                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| アフガニスタン                              | AF                       | AFG                      | ps-AF/en-us                         |
| オーランド諸島                            | AX                       | より                      | sv-SE/en-us-US                         |
| アルバニア                                  | AL                       | ALB                      | sq-AL/en-us-US                         |
| アルジェリア                                  | DZ                       | DZA                      | ar-DZ/en-us-US                         |
| 米領サモア                           | AS                       | ASM                      | ja-JP                                 |
| アンドラ                                  | AD                       | AND                      | ca-ES/en-us                         |
| アンゴラ                                   | AO                       | 前                      | pt-PT/en-us-US                         |
| アンギラ                                 | AI                       | AIA                      | ja-JP                                 |
| 南極                               | AQ                       | ATA                      | ja-JP                                 |
| アンティグア・バーブーダ                      | AG                       | ATG                      | ja-JP                                 |
| アルゼンチン                                | AR                       | ARG                      | es-AR/en-us                         |
| アルメニア                                  | AM                       | ARM                      | hy-AM/en-us                         |
| アルバ                                    | AW                       | ABW                      | nl-NL/en-us                         |
| オーストラリア                                | AU                       | AUS                      | en-us/en-us                         |
| オーストリア                                  | AT                       | 自動                      | de/en-us                         |
| アゼルバイジャン                               | AZ                       | AZE                      | az-Latn-AZ/en-US                    |
| バハマ                                  | BS                       | BHS                      | en GB/en-us                         |
| バーレーン                                  | BH                       | BHR                      | ar-BH/en-us                         |
| バングラデシュ                               | BD                       | BGD                      | bn-BD/en-us                         |
| バルバドス                                 | BB                       | BRB                      | en GB/en-us                         |
| ベラルーシ                                  | BY                       | BLR                      | 使用者/en-us                         |
| ベルギー                                  | BE                       | BEL                      | fr-fr/nl-BE/en-us                 |
| ベリーズ                                   | BZ                       | BLZ                      | en-BZ/en-us                         |
| ベナン                                    | BJ                       | BEN                      | fr-fr/en-us                         |
| バミューダ                                  | BM                       | BMU                      | en GB/en-us                         |
| ブータン                                   | BT                       | BTN                      | ja-JP                                 |
| ボリビア                                  | BO                       | BOL                      | es-BO/en-us                         |
| ボネール島                                  | BQ                       | BES                      | nl-NL/en-us                         |
| ボスニア・ヘルツェゴビナ                   | BA                       | BIH                      | Latn-BA/en-us-US                    |
| ボツワナ                                 | BW                       | BWA                      | en GB/en-us                         |
| ブーベ島                            | BV                       | BVT                      | nb-いいえ/en-us                         |
| ブラジル                                   | BR                       | BRA                      | pt-BR/en-us-US                         |
| 英領インド洋地域           | IO                       | IoT                      | ja-JP                                 |
| 英領ヴァージン諸島                   | VG                       | VGB                      | ja-JP                                 |
| ブルネイ                                   | BN                       | BRN                      | BN/en-us                         |
| ブルガリア                                 | BG                       | BGR                      | bg-BG/en-us                         |
| ブルキナファソ                             | BF                       | BFA                      | fr-fr/en-us                         |
| ブルンジ                                  | BI                       | BDI                      | fr-fr/en-us                         |
| カーボベルデ                               | CV                       | CPV                      | pt-CV/en-us-US                         |
| カンボジア                                 | KH                       | KHM                      | km-KH/en-us                         |
| カメルーン                                 | CM                       | CMR                      | fr-fr/en-us                         |
| Canada                                   | CA                       | CAN                      | fr-fr/en-us                         |
| ケイマン諸島                           | KY                       | CYM                      | en GB/en-us                         |
| 中央アフリカ共和国                 | CF                       | CAF                      | fr-fr/en-us                         |
| チャド                                     | TD                       | TCD                      | fr-fr/en-us                         |
| チリ                                    | CL                       | CHL                      | es-CL/en-us                         |
| 中国                                    | CN                       | CHN                      | zh-tw-CN/en-US                         |
| クリスマス島                         | CX                       | .CXR                      | ja-JP                                 |
| ココス(キーリング)諸島                  | CC                       | CCK                      | ja-JP                                 |
| コロンビア                                 | CO                       | 行列                      | es-CO/en-us-US                         |
| コモロ                                  | KM                       | COM (COM)                      | fr-fr/en-us                         |
| コンゴ                                    | CG                       | 歯車                      | fr-fr/en-us                         |
| コンゴ民主共和国                              | CD                       | 代金引換払い                      | fr-fr/en-us                         |
| クック諸島                             | CK                       | COK                      | ja-JP                                 |
| コスタリカ                               | CR                       | CRI                      | es-CR/en-us                         |
| コートジボワール                            | CI                       | CIV                      | fr-fr/en-us                         |
| クロアチア                                  | HR                       | HRV                      | hr-HR/en-us-US                         |
| キュラソー島                                  | CW                       | CUW                      | nl-NL/en-us                         |
| キプロス                                   | CY                       | CYP                      | el-GR/en-us                         |
| チェコ                                  | CZ                       | CZE                      | cs-CS-CZ/en-us                         |
| デンマーク                                  | DK                       | DNK                      | da-DK/en-us                         |
| ジブチ                                 | DJ                       | DJI                      | fr-fr/en-us                         |
| ドミニカ                                 | DM                       | DMA                      | ja-JP                                 |
| ドミニカ共和国                       | DO                       | DOM                      | es-DO/en-us                         |
| エクアドル                                  | EC                       | ECU                      | es-EC/en-us-US                         |
| エジプト                                    | EG                       | ○                      | ar-例/en-us                         |
| エルサルバドル                              | SV                       | SLV                      | es-SV/en-us                         |
| 赤道ギニア                        | GQ                       | GNQ                      | es-ES/en-us                         |
| エリトリア                                  | ER                       | ERI                      | ar-SA/en-us-US                         |
| エストニア                                  | EE                       | 最も                      | et-EE/en-us                         |
| スワジランド                                 | SZ                       | SWZ                      | ja-JP                                 |
| エチオピア                                 | ET                       | ETH                      | am-ET/en-us                         |
| フォークランド諸島                         | FK (FK)                       | FLK                      | ja-JP                                 |
| フェロー諸島                            | FO                       | から                      | fo-FO/en-us                         |
| フィジー                                     | FJ                       | FJI                      | en GB/en-us                         |
| フィンランド                                  | FI                       | FIN                      | fi fi/sv-FI/en-us                 |
| フランス                                   | FR                       | FRA                      | fr-fr/en-us                         |
| 仏領ギアナ                            | GF                       | GUF                      | fr-fr/en-us                         |
| 仏領ポリネシア                         | PF                       | PYF                      | fr-fr/en-us                         |
| 仏領極南諸島              | TF                       | ATF                      | fr-fr/en-us                         |
| ガボン                                    | GA                       | GAB                      | fr-fr/en-us                         |
| ガンビア                                   | GM                       | GMB                      | ja-JP                                 |
| ジョージア                                  | GE                       | 地理的                      | ka-GE/en-us                         |
| ドイツ                                  | DE                       | DEU                      | de/en-us                         |
| ガーナ                                    | GH                       | GHA                      | en GB/en-us                         |
| ジブラルタル                                | GI                       | GIB                      | ja-JP                                 |
| ギリシャ                                   | GR                       | GRC                      | el-GR/en-us                         |
| グリーンランド                                | GL                       | GRL                      | da-DK/en-us                         |
| グレナダ                                  | GD                       | GRD                      | ja-JP                                 |
| グアドループ                               | GP                       | GLP                      | fr-fr/en-us                         |
| グアム                                     | GU                       | ガム                      | ja-JP                                 |
| グアテマラ                                | GT                       | GTM                      | es-GT/en-us                         |
| ガーンジー                                 | GG                       | GGY                      | ja-JP                                 |
| ギニア                                   | GN                       | GIN                      | fr-fr/en-us                         |
| ギニアビサウ                            | GW                       | GNB                      | pt-PT/en-us-US                         |
| ガイアナ                                   | GY                       | やつ                      | ja-JP                                 |
| ハイチ                                    | HT                       | HTI                      | fr-fr/en-us                         |
| ハード・マクドナルド諸島        | HM                       | HMD                      | ja-JP                                 |
| ホンジュラス                                 | HN                       | HND                      | es-HN/en-us                         |
| 香港特別行政区                            | HK                       | HKG                      | zh-tw-HK/en-us                         |
| ハンガリー                                  | HU                       | HUN                      | hu-HU/en-us                         |
| アイスランド                                  | IS                       | ISL                      | is-IS/en-us                         |
| インド                                    | IN                       | IND                      | en-us/hi IN/en-us-米国                 |
| インドネシア                                | id                       | IDN                      | id-ID/en-us                         |
| イラク                                     | IQ                       | IRQ●irq○                      | ar-IQ/en-us                         |
| アイルランド                                  | IE                       | IRL                      | en-IE/en-us                         |
| マン島                              | IM                       | IMN                      | ja-JP                                 |
| イスラエル                                   | IL                       | ISR                      | he-IL/en-us                         |
| イタリア                                    | IT                       | ITA                      | it/en-us                         |
| ジャマイカ                                  | JM                       | 紙                      | en-JM/en-us-US                         |
| ヤンマイエン島                                | XJ                       | XJA                      | nb-いいえ/en-us                         |
| 日本                                    | JP                       | JPN                      | ja-jp/en-us                         |
| ジャージー                                   | JE                       | JEY                      | ja-JP                                 |
| ヨルダン                                   | JO                       | JOR                      | ar-JO/en-us                         |
| カザフスタン                               | KZ                       | KAZ                      | kk-KZ/en-us-US                         |
| ケニア                                    | KE                       | たとえる                      | sw-KE/en-us                         |
| キリバス                                 | KI                       | KIR                      | ja-JP                                 |
| 韓国                                    | KR                       | KOR                      | ko-韓国/en-us                         |
| コソボ                                   | XK                       | XKS                      | ja-JP                                 |
| クウェート                                   | KW                       | KWT                      | ar-KW/en-us                         |
| キルギス                               | KG                       | KGZ                      | 中-KG/en-us                         |
| ラオス                                     | LA                       | ラオス人民                      | lo-LA/en-us-US                         |
| ラトビア                                   | LV                       | LVA                      | lv-LV/en-us                         |
| レバノン                                  | LB                       | LBN                      | ar-LB/en-us-US                         |
| レソト                                  | LS                       | LSO                      | ja-JP                                 |
| リベリア                                  | LR                       | LBR                      | ja-JP                                 |
| リビア                                    | LY                       | LBY                      | ar-かなり/en-us-米国                         |
| リヒテンシュタイン                            | LI                       | 任意                      | LI/en-us                         |
| リトアニア                                | LT                       | LTU                      | lt-LT/en-us                         |
| ルクセンブルク                               | LU                       | LUX                      | 逆 LU/fr-LU/en-us                 |
| 中華人民共和国マカオ特別行政区                                | MO                       | MAC                      | zh-tw-MO/en-us                         |
| マケドニア (旧ユーゴスラビア共和国)                          | MK                       | MKD                      | mk-MK/en-us                         |
| マダガスカル                               | MG                       | MDG                      | fr-fr/en-us                         |
| マラウイ                                   | MW                       | MWI                      | ja-JP                                 |
| マレーシア                                 | MY                       | MYS                      | en-us/en-us                         |
| モルディブ                                 | MV                       | MDV                      | dv-MV/en-us                         |
| マリ                                     | ML                       | .MLI                      | fr-fr/en-us                         |
| マルタ                                    | MT                       | MLT                      | mt-MT/en-us                         |
| マーシャル諸島                         | MH                       | MHL                      | ja-JP                                 |
| マルティニーク                               | MQ                       | MTQ                      | fr-fr/en-us                         |
| モーリタニア                               | MR                       | MRT.DLL                      | ar-SA/en-us-US                         |
| モーリシャス                                | MU                       | メモリ                      | en GB/en-us                         |
| マヨット                                  | YT                       | MYT                      | fr-fr/en-us                         |
| メキシコ                                   | MX                       | MEX                      | es-MX/en-us                         |
| ミクロネシア                               | FM                       | FSM                      | ja-JP                                 |
| モルドバ                                  | MD                       | MDA                      | ro-RO/en-us-US                         |
| モナコ                                   | MC                       | MCO                      | fr-MC/en-us                         |
| モンゴル                                 | MN                       | MNG                      | 最新-米国中/en-us                         |
| モンテネグロ                               | ME                       | MNE                      | Latn-ME/en-us                    |
| モントセラト                               | MS                       | MSR                      | ja-JP                                 |
| モロッコ                                  | MA                       | 3 月                      | ar-MA/en-us                         |
| モザンビーク                               | MZ                       | MOZ                      | pt-PT/en-us-US                         |
| ミャンマー                                  | mm                       | MMR                      | ja-JP                                 |
| ナミビア                                  | NA                       | NAM                      | en GB/en-us                         |
| ナウル                                    | NR                       | NRU                      | ja-JP                                 |
| ネパール                                    | NP                       | NPL                      | ne-NP/en-us                         |
| オランダ領アンティル                     | AN                       | あ                      | ja-JP                                 |
| オランダ                         | NL                       | NLD                      | nl-NL/en-us                         |
| ニューカレドニア                            | NC                       | NCL                      | fr-fr/en-us                         |
| ニュージーランド                              | NZ                       | NZL                      | en-us/en-us                         |
| ニカラグア                                | NI                       | NIC                      | es-NI/en-us                         |
| ニジェール                                    | NE                       | NER                      | fr-fr/en-us                         |
| ナイジェリア                                  | NG                       | NGA                      | ha-Latn/en-us                    |
| ニウエ                                     | NU                       | この                      | ja-JP                                 |
| ノーフォーク島                           | NF                       | (KB)                      | ja-JP                                 |
| 北マリアナ諸島                 | MP                       | MNP                      | ja-JP                                 |
| ノルウェー                                   | NO                       | NOR                      | nb-いいえ/en-us                         |
| オマーン                                     | OM                       | OMN                      | ar-OM/en-us-US                         |
| パキスタン                                 | PK                       | パック                      | お客様-PK/en-us                         |
| パラオ                                    | PW                       | PLW                      | ja-JP                                 |
| パレスチナ自治政府                    | PS                       | PSE                      | ar-SA/en-us-US                         |
| パナマ                                   | PA                       | PAN                      | es-PA/en-us                         |
| パプアニューギニア                         | PG                       | PNG                      | ja-JP                                 |
| パラグアイ                                 | PY                       | 慎重                      | es-.PY/en-us                         |
| ペルー                                     | PE                       | 各行                      | es-PE/en-us                         |
| フィリピン                              | PH                       | PHL                      | en PH/en-us                         |
| ピトケアン島                         | PN                       | PCN                      | ja-JP                                 |
| ポーランド                                   | PL                       | REGISTRY.POL                      | pl-PL/en-us                         |
| ポルトガル                                 | PT                       | PRT                      | pt-PT/en-us-US                         |
| プエルトリコ                              | PR                       | PRI                      | es-PR/en-us                         |
| カタール                                    | QA                       | QAT                      | ar-QA/en-us                         |
| レユニオン                                  | RE                       | REU                      | fr-fr/en-us                         |
| ルーマニア                                  | RO                       | ROU                      | ro-RO/en-us-US                         |
| ロシア                                   | RU                       | RUS                      | ru-RU/en-us                         |
| ルワンダ                                   | RW                       | RWA                      | rw-RW/en-us                         |
| サバ島                                     | XS                       | XSA                      | nl-NL/en-us                         |
| セントクリストファー・ネイビス                    | KN                       | KNA                      | en GB/en-us                         |
| セントルシア                              | LC                       | LCA                      | ja-JP                                 |
| サン・マルタン                             | MF                       | MAF                      | fr-fr/en-us                         |
| サンピエール・ミクロン                | PM                       | SPM                      | fr-fr/en-us                         |
| セントビンセント及びグレナディーン諸島         | VC                       | VCT                      | ja-JP                                 |
| サン・バルテルミー                         | BL                       | BLM                      | fr-fr/en-us                         |
| サモア                                    | WS                       | WSM が                      | ja-JP                                 |
| サンマリノ                               | SM                       | SMR                      | it/en-us                         |
| サントメ・プリンシペ                    | ST                       | .STP                      | pt-PT/en-us-US                         |
| サウジアラビア                             | SA                       | SAU                      | ar-SA/en-us-US                         |
| セネガル                                  | SN                       | SEN                      | wo-SN/en-us-US                         |
| セルビア                                   | RS                       | SRB                      | Latn-RS/sr-Cyrl-RS/en-us       |
| セーシェル                               | SC                       | SYC                      | ja-JP                                 |
| シエラレオネ                             | SL                       | SLE                      | ja-JP                                 |
| シンガポール                                | SG                       | SGP                      | en SG/zh-tw/en-us/en-us                 |
| シント・ユースタティウス島                           | XE                       | XSE                      | nl-NL/en-us                         |
| シント・マールテン                             | SX                       | SXM                      | ja-JP                                 |
| スロバキア                                 | SK                       | SVK                      | sk-SK/en-us-US                         |
| スロベニア                                 | SI                       | SVN                      | sl-SI/en-us                         |
| ソロモン諸島                          | SB                       | SLB                      | ja-JP                                 |
| ソマリア                                  | SO                       | SOM                      | ar-SA/en-us-US                         |
| 南アフリカ                             | ZA                       | ZAF                      | ZA/en-us                         |
| サウスジョージア・サウスサンドウィッチ諸島 | GS                       | SGS-THOMSON                      | ja-JP                                 |
| 南スーダン                              | SS                       | SSD                      | ja-JP                                 |
| スペイン                                    | ES                       | ESP                      | es-es/ca-es/eu-es/gl-es/en-us |
| スリランカ                                | LK                       | LKA                      | si-LK/en-us                         |
| セントヘレナ、アセンションおよびトリスタンダクーニャ   | SH                       | SHN                      | ja-JP                                 |
| スリナム                                 | SR                       | .SUR                      | nl-NL                                 |
| スバールバル諸島                                 | SJ                       | SJM                      | nb-いいえ/en-us                         |
| スウェーデン                                   | SE                       | SWE                      | sv-SE/en-us-US                         |
| スイス                              | CH                       | CHE                      | de-ch/fr/it-CH/en-us         |
| 台湾                                   | TW                       | TWN                      | zh-tw-TW/en-us-US                         |
| タジキスタン                               | TJ                       | TJK                      | tg-Cyrl-TJ/en-US                    |
| タンザニア                                 | TZ                       | TZA                      | en GB/en-us                         |
| タイ                                 | TH                       | THA                      | th-TH/en-us                         |
| ティモール・レステ                              | TL                       | TLS                      | pt-PT/en-us-US                         |
| トーゴ                                     | TG                       | TGO                      | fr-fr/en-us                         |
| トケラウ                                  | TK                       | TKL                      | ja-JP                                 |
| トンガ                                    | TO                       | ITEMS                      | ja-JP                                 |
| トリニダード・トバゴ                      | TT                       | TTO                      | en-us/en-us                         |
| チュニジア                                  | TN                       | TUN                      | ar-TN/en-us                         |
| トルコ                                   | TR                       | TUR                      | tr-TR/en-us-US                         |
| トルクメニスタン                             | TM                       | TKM                      | tk-TM/en-us                         |
| タークス・カイコス諸島                 | TC                       | TCA                      | ja-JP                                 |
| ツバル                                   | TV                       | TUV                      | ja-JP                                 |
| ウガンダ                                   | UG                       | UGA                      | en GB/en-us                         |
| ウクライナ                                  | UA                       | UKR                      | uk-UA/en-us                         |
| アラブ首長国連邦                     | AE                       | ARE                      | ar-AE/en-us-US                         |
| イギリス                           | GB                       | GBR                      | en GB/en-us                         |
| 米領小離島                    | UM                       | UMI                      | ja-JP                                 |
| 米国バージン諸島                      | VI                       | PR1-DBMS-VIR                      | ja-JP                                 |
| United States                            | US                       | 米国                      | en-us/es-US                         |
| ウルグアイ                                  | UY                       | URY                      | es-UY/en-us-US                         |
| ウズベキスタン                               | UZ                       | UZB                      | uz-Latn-UZ/en-us                    |
| バヌアツ                                  | VU                       | VUT                      | ja-JP                                 |
| バチカン市国                             | VA                       | VAT                      | it/en-us                         |
| ベネズエラ                                | VE                       | VEN                      | es-VE/en-us                         |
| ベトナム                                  | VN                       | VNM                      | vi-VN/en-us                         |
| ワリス・フテュナ諸島                        | WF                       | WLF                      | fr-fr/en-us                         |
| イエメン                                    | YE                       | YEM                      | ar/en-us-US                         |
| ザンビア                                   | ZM                       | ZMB                      | en GB/en-us                         |
| ジンバブエ                                 | ZW                       | ZWE                      | ZW/en-us                         |

