---
title: パートナーセンターでサポートされている言語とロケール
description: パートナーセンターでサポートされている ISO2 と ISO3 のロケールの一覧。
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: bf12829decaebd8525ef0a51a7856c75aa69785d
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416381"
---
# <a name="partner-center-supported-languages-and-locales"></a>パートナーセンターでサポートされている言語とロケール


**適用対象**

- Partner Center
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
| 米領サモア                           | AS                       | ASM                      | en-US                                 |
| アンドラ                                  | AD                       | AND                      | ca-ES/en-us                         |
| アンゴラ                                   | AO                       | 前                      | pt-PT/en-us-US                         |
| アンギラ                                 | AI                       | AIA                      | en-US                                 |
| 南極                               | 以降                       | ATA                      | en-US                                 |
| アンティグア・バーブーダ                      | AG                       | ATG                      | en-US                                 |
| アルゼンチン                                | AR                       | ARG                      | es-AR/en-us                         |
| アルメニア                                  | AM                       | ARM                      | hy-AM/en-us                         |
| アルバ                                    | AW                       | ABW                      | nl-NL/en-us                         |
| オーストラリア                                | AU                       | オーストラリア                      | en-us/en-us                         |
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
| バミューダ諸島                                  | BM.EXE                       | BMU                      | en GB/en-us                         |
| ブータン                                   | BT                       | BTN                      | en-US                                 |
| ボリビア                                  | BO                       | BOL                      | es-BO/en-us                         |
| ボネール島                                  | BQ                       | BES                      | nl-NL/en-us                         |
| ボスニア・ヘルツェゴビナ                   | BA                       | BIH                      | Latn-BA/en-us-US                    |
| ボツワナ                                 | BW                       | BWA                      | en GB/en-us                         |
| ブーベ島                            | BV                       | BVT                      | nb-いいえ/en-us                         |
| ブラジル                                   | BR                       | BRA                      | pt-BR/en-us-US                         |
| 英領インド洋地域           | IO                       | IOT                      | en-US                                 |
| 英領バージン諸島                   | VG                       | VGB                      | en-US                                 |
| ブルネイ                                   | BN                       | BRN                      | BN/en-us                         |
| ブルガリア                                 | BG                       | BGR                      | bg-BG/en-us                         |
| ブルキナファソ                             | BF                       | BFA                      | fr-fr/en-us                         |
| ブルンジ                                  | POWER                       | BDI                      | fr-fr/en-us                         |
| カーボベルデ                               | CV                       | CPV                      | pt-CV/en-us-US                         |
| カンボジア                                 | KH                       | KHM                      | km-KH/en-us                         |
| カメルーン                                 | CM                       | CMR                      | fr-fr/en-us                         |
| カナダ                                   | CA                       | より                      | fr-fr/en-us                         |
| ケイマン諸島                           | アヒル                       | CYM                      | en GB/en-us                         |
| 中央アフリカ共和国                 | CF                       | CAF                      | fr-fr/en-us                         |
| チャド                                     | TD                       | TCD                      | fr-fr/en-us                         |
| チリ                                    | CL                       | CHL                      | es-CL/en-us                         |
| 中国                                    | CN                       | CHN                      | zh-tw-CN/en-US                         |
| クリスマス島                         | シリーズ                       | .CXR                      | en-US                                 |
| ココス諸島                  | [CC]                       | CCK                      | en-US                                 |
| コロンビア                                 | CO                       | 行列                      | es-CO/en-us-US                         |
| コモロ                                  | KM                       | COM                      | fr-fr/en-us                         |
| コンゴ共和国                                    | 抗力                       | 歯車                      | fr-fr/en-us                         |
| コンゴ民主共和国                              | CD                       | 代金引換払い                      | fr-fr/en-us                         |
| クック諸島                             | CK                       | COK                      | en-US                                 |
| コスタリカ                               | CR                       | CRI                      | es-CR/en-us                         |
| コートジボワール                            | CI                       | CIV                      | fr-fr/en-us                         |
| クロアチア                                  | HR                       | HRV                      | hr-HR/en-us-US                         |
| キュラソー島                                  | 数量                       | CUW                      | nl-NL/en-us                         |
| キプロス                                   | CY                       | CYP                      | el-GR/en-us                         |
| Czechia                                  | CZ                       | CZE                      | cs-CS-CZ/en-us                         |
| デンマーク                                  | DK                       | DNK                      | da-DK/en-us                         |
| ジブチ                                 | DJ                       | DJI                      | fr-fr/en-us                         |
| ドミニカ国                                 | DM                       | DMA                      | en-US                                 |
| ドミニカ共和国                       | DO                       | DOM                      | es-DO/en-us                         |
| エクアドル                                  | EC                       | ECU                      | es-EC/en-us-US                         |
| エジプト                                    | EG                       | ○                      | ar-例/en-us                         |
| エルサルバドル                              | SV                       | SLV                      | es-SV/en-us                         |
| 赤道ギニア                        | GQ                       | GNQ                      | es-ES/en-us                         |
| エリトリア                                  | 壁紙                       | ERI                      | ar-SA/en-us-US                         |
| エストニア                                  | EE                       | 最も                      | et-EE/en-us                         |
| eSwatini                                 | SZ                       | SWZ                      | en-US                                 |
| エチオピア                                 | ET                       | ETH                      | am-ET/en-us                         |
| フォークランド諸島                         | FK (FK)                       | FLK                      | en-US                                 |
| フェロー諸島                            | FO                       | から                      | fo-FO/en-us                         |
| フィジー諸島                                     | FJ                       | FJI                      | en GB/en-us                         |
| フィンランド                                  | FI                       | FIN                      | fi fi/sv-FI/en-us                 |
| France                                   | FR                       | FRA                      | fr-fr/en-us                         |
| フランス領ギアナ                            | GF                       | GUF                      | fr-fr/en-us                         |
| フランス領ポリネシア                         | PF                       | PYF                      | fr-fr/en-us                         |
| 仏領極南諸島              | TF                       | ATF                      | fr-fr/en-us                         |
| ガボン                                    | GA                       | GAB                      | fr-fr/en-us                         |
| ガンビア                                   | GM                       | GMB                      | en-US                                 |
| Georgia                                  | GE                       | 地理的                      | ka-GE/en-us                         |
| Germany                                  | DE                       | DEU                      | de/en-us                         |
| ガーナ                                    | GH                       | GHA                      | en GB/en-us                         |
| ジブラルタル                                | GI                       | GIB                      | en-US                                 |
| ギリシャ                                   | GR                       | GRC                      | el-GR/en-us                         |
| グリーンランド                                | GL                       | GRL                      | da-DK/en-us                         |
| グレナダ                                  | GD                       | GRD                      | en-US                                 |
| グアドループ                               | GP                       | GLP                      | fr-fr/en-us                         |
| グアム                                     | GU                       | ガム                      | en-US                                 |
| グアテマラ                                | GT                       | GTM                      | es-GT/en-us                         |
| ガーンジー島                                 | GG                       | GGY                      | en-US                                 |
| ギニア                                   | GN                       | GIN                      | fr-fr/en-us                         |
| ギニアビサウ                            | GW                       | GNB                      | pt-PT/en-us-US                         |
| ガイアナ                                   | GY                       | やつ                      | en-US                                 |
| ハイチ                                    | HT                       | HTI                      | fr-fr/en-us                         |
| ハード・マクドナルド諸島        | HM                       | HMD                      | en-US                                 |
| ホンジュラス                                 | HN                       | HND                      | es-HN/en-us                         |
| 香港                            | HK                       | HKG                      | zh-tw-HK/en-us                         |
| ハンガリー                                  | HU                       | HUN                      | hu-HU/en-us                         |
| アイスランド                                  | IS                       | ISL                      | is-IS/en-us                         |
| インド                                    | IN                       | IND                      | en-us/hi IN/en-us-米国                 |
| インドネシア                                | ID                       | IDN                      | id-ID/en-us                         |
| イラク                                     | IQ                       | IRQ●irq○                      | ar-IQ/en-us                         |
| アイルランド                                  | IE                       | IRL                      | en-IE/en-us                         |
| マン島                              | IM                       | IMN                      | en-US                                 |
| イスラエル                                   | IL                       | ISR                      | he-IL/en-us                         |
| イタリア                                    | IT                       | ITA                      | it/en-us                         |
| ジャマイカ                                  | JM                       | 紙                      | en-JM/en-us-US                         |
| ヤンマイエン島                                | XJ                       | XJA                      | nb-いいえ/en-us                         |
| Japan                                    | JP                       | JPN                      | ja-jp/en-us                         |
| ジャージー島                                   | JE                       | JEY                      | en-US                                 |
| ヨルダン                                   | JO                       | JOR                      | ar-JO/en-us                         |
| カザフスタン                               | KZ                       | KAZ                      | kk-KZ/en-us-US                         |
| ケニア                                    | KE                       | たとえる                      | sw-KE/en-us                         |
| キリバス                                 | KI                       | KIR                      | en-US                                 |
| Korea                                    | KR                       | KOR                      | ko-韓国/en-us                         |
| コソボ                                   | XK                       | XKS                      | en-US                                 |
| クウェート                                   | KW                       | KWT                      | ar-KW/en-us                         |
| キルギス                               | KG                       | KGZ                      | 中-KG/en-us                         |
| ラオス                                     | LA                       | ラオス人民                      | lo-LA/en-us-US                         |
| ラトビア                                   | LV                       | LVA                      | lv-LV/en-us                         |
| レバノン                                  | LB                       | LBN                      | ar-LB/en-us-US                         |
| レソト                                  | AVL                       | LSO                      | en-US                                 |
| リベリア                                  | LR                       | LBR                      | en-US                                 |
| リビア                                    | LY                       | LBY                      | ar-かなり/en-us-米国                         |
| リヒテンシュタイン                            | &AMP;                       | 任意                      | LI/en-us                         |
| リトアニア                                | LT                       | LTU                      | lt-LT/en-us                         |
| ルクセンブルク                               | LU                       | LUX                      | 逆 LU/fr-LU/en-us                 |
| マカオ                                | 月                       | MAC                      | zh-tw-MO/en-us                         |
| マケドニア (旧ユーゴスラビア共和国)                          | MK                       | MKD                      | mk-MK/en-us                         |
| マダガスカル                               | MG                       | MDG                      | fr-fr/en-us                         |
| マラウイ                                   | MW                       | MWI                      | en-US                                 |
| マレーシア                                 | MY                       | MYS                      | en-us/en-us                         |
| モルディブ                                 | MV                       | MDV                      | dv-MV/en-us                         |
| マリ                                     | ML                       | .MLI                      | fr-fr/en-us                         |
| マルタ                                    | MT                       | MLT                      | mt-MT/en-us                         |
| マーシャル諸島                         | MH                       | MHL                      | en-US                                 |
| マルチニーク島                               | MQ                       | MTQ                      | fr-fr/en-us                         |
| モーリタニア                               | MR                       | MRT.DLL                      | ar-SA/en-us-US                         |
| モーリシャス                                | MU                       | メモリ                      | en GB/en-us                         |
| マイヨット島                                  | YT                       | MYT                      | fr-fr/en-us                         |
| メキシコ                                   | MX                       | MEX                      | es-MX/en-us                         |
| ミクロネシア                               | 今                       | FSM                      | en-US                                 |
| モルドバ                                  | MD                       | MDA                      | ro-RO/en-us-US                         |
| モナコ                                   | MC                       | MCO                      | fr-MC/en-us                         |
| モンゴル                                 | MN                       | MNG                      | 最新-米国中/en-us                         |
| モンテネグロ                               | ME                       | MNE                      | Latn-ME/en-us                    |
| モンセラット                               | MS                       | MSR                      | en-US                                 |
| モロッコ                                  | MA                       | 月                      | ar-MA/en-us                         |
| モザンビーク                               | MZ                       | MOZ                      | pt-PT/en-us-US                         |
| ミャンマー                                  | MM                       | MMR                      | en-US                                 |
| ナミビア                                  | 該当なし                       | ベトナム                      | en GB/en-us                         |
| ナウル                                    | NR                       | NRU                      | en-US                                 |
| ネパール                                    | NP                       | NPL                      | ne-NP/en-us                         |
| オランダ領アンティル                     | 込み                       | あ                      | en-US                                 |
| オランダ、                         | NL                       | NLD                      | nl-NL/en-us                         |
| ニューカレドニア                            | 加工                       | NCL                      | fr-fr/en-us                         |
| ニュージーランド                              | NZ                       | NZL                      | en-us/en-us                         |
| ニカラグア                                | NI                       | NIC                      | es-NI/en-us                         |
| ニジェール                                    | NE                       | デザイナー                      | fr-fr/en-us                         |
| ナイジェリア                                  | NG                       | NGA                      | ha-Latn/en-us                    |
| ニウエ                                     | ニュー                       | この                      | en-US                                 |
| ノーフォーク島                           | ユーティリティー                       | (KB)                      | en-US                                 |
| 北マリアナ諸島                 | MP                       | MNP                      | en-US                                 |
| ノルウェー                                   | 使用不可                       | NOR                      | nb-いいえ/en-us                         |
| オマーン                                     | OM                       | OMN                      | ar-OM/en-us-US                         |
| パキスタン                                 | PK                       | パック                      | お客様-PK/en-us                         |
| パラオ                                    | PW                       | PLW                      | en-US                                 |
| パレスチナ自治政府                    | PS                       | PSE                      | ar-SA/en-us-US                         |
| パナマ                                   | PA                       | PAN                      | es-PA/en-us                         |
| パプアニューギニア                         | 画面                       | PNG                      | en-US                                 |
| パラグアイ                                 | PY                       | 慎重                      | es-.PY/en-us                         |
| ペルー                                     | PE                       | 各行                      | es-PE/en-us                         |
| フィリピン                              | PH                       | PHL                      | en PH/en-us                         |
| ピトケアン島                         | PN                       | PCN                      | en-US                                 |
| ポーランド                                   | PL                       | REGISTRY.POL                      | pl-PL/en-us                         |
| ポルトガル                                 | PT                       | PRT                      | pt-PT/en-us-US                         |
| プエルトリコ                              | PR                       | PRI                      | es-PR/en-us                         |
| カタール                                    | 品質保証                       | QAT                      | ar-QA/en-us                         |
| レユニオン                                  | RE                       | REU                      | fr-fr/en-us                         |
| ルーマニア                                  | RO                       | ROU                      | ro-RO/en-us-US                         |
| ロシア                                   | RU                       | RUS                      | ru-RU/en-us                         |
| ルワンダ                                   | RW                       | RWA                      | rw-RW/en-us                         |
| サバ島                                     | XS                       | XSA                      | nl-NL/en-us                         |
| セントクリストファー・ネイビス                    | KN                       | KNA                      | en GB/en-us                         |
| セントルシア                              | 小                       | LCA                      | en-US                                 |
| サンマルタン島                             | メイン                       | MAF                      | fr-fr/en-us                         |
| サンピエール・ミクロン                | PM                       | SPM                      | fr-fr/en-us                         |
| セントビンセントおよびグレナディーン諸島         | VC                       | VCT                      | en-US                                 |
| サン・バルテルミー                         | BL                       | BLM                      | fr-fr/en-us                         |
| サモア                                    | WS                       | WSM が                      | en-US                                 |
| サンマリノ                               | MANAGER                       | SMR                      | it/en-us                         |
| サントメ・プリンシペ                    | ST                       | .STP                      | pt-PT/en-us-US                         |
| サウジアラビア                             | SA                       | SAU                      | ar-SA/en-us-US                         |
| セネガル                                  | SN                       | SEN                      | wo-SN/en-us-US                         |
| セルビア                                   | RS                       | SRB                      | Latn-RS/sr-Cyrl-RS/en-us       |
| セーシェル                               | SC                       | SYC                      | en-US                                 |
| シエラレオネ                             | SL                       | SLE                      | en-US                                 |
| シンガポール                                | SG                       | SGP                      | en SG/zh-tw/en-us/en-us                 |
| シント・ユースタティウス島                           | XE                       | XSE                      | nl-NL/en-us                         |
| シント・マールテン島                             | SX                       | SXM                      | en-US                                 |
| スロバキア                                 | SK                       | SVK                      | sk-SK/en-us-US                         |
| スロベニア                                 | SI                       | SVN                      | sl-SI/en-us                         |
| ソロモン諸島                          | SB                       | SLB                      | en-US                                 |
| ソマリア                                  | SO                       | SOM                      | ar-SA/en-us-US                         |
| 南アフリカ                             | ZA                       | ZAF                      | ZA/en-us                         |
| サウスジョージア・サウスサンドウィッチ諸島 | GS                       | SGS-THOMSON                      | en-US                                 |
| 南スーダン                              | 秒                       | SSD                      | en-US                                 |
| スペイン                                    | ES                       | ESP                      | es-es/ca-es/eu-es/gl-es/en-us |
| スリランカ                                | LK                       | LKA                      | si-LK/en-us                         |
| セントヘレナ、アセンションおよびトリスタンダクーニャ   | 悪夢                       | SHN                      | en-US                                 |
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
| トケラウ諸島                                  | TK                       | TKL                      | en-US                                 |
| トンガ                                    | TO                       | ITEMS                      | en-US                                 |
| トリニダード・トバゴ                      | TT                       | する                      | en-us/en-us                         |
| チュニジア                                  | TN                       | TUN                      | ar-TN/en-us                         |
| トルコ                                   | TR                       | TUR                      | tr-TR/en-us-US                         |
| トルクメニスタン                             | TM                       | TKM                      | tk-TM/en-us                         |
| タークス・カイコス諸島                 | フィールド                       | TCA                      | en-US                                 |
| ツバル                                   | テレビ                       | TUV                      | en-US                                 |
| ウガンダ                                   | UG                       | UGA                      | en GB/en-us                         |
| ウクライナ                                  | UA                       | UKR                      | uk-UA/en-us                         |
| アラブ首長国連邦                     | AE                       | は                      | ar-AE/en-us-US                         |
| イギリス                           | GB                       | GBR                      | en GB/en-us                         |
| 合衆国領有小離島                    | UM                       | UMI                      | en-US                                 |
| 米領バージン諸島                      | VI                       | PR1-DBMS-VIR                      | en-US                                 |
| 米国                            | US                       | 海岸                      | en-us/es-US                         |
| ウルグアイ                                  | UY                       | URY                      | es-UY/en-us-US                         |
| ウズベキスタン                               | UZ                       | UZB                      | uz-Latn-UZ/en-us                    |
| バヌアツ                                  | VU                       | VUT                      | en-US                                 |
| バチカン市国                             | VA                       | VAT                      | it/en-us                         |
| ベネズエラ                                | VE                       | VEN                      | es-VE/en-us                         |
| ベトナム                                  | VN                       | VNM                      | vi-VN/en-us                         |
| ワリス・フテュナ諸島                        | WF                       | WLF                      | fr-fr/en-us                         |
| イエメン                                    | なん信仰                       | YEM                      | ar/en-us-US                         |
| ザンビア                                   | ZM                       | ZMB                      | en GB/en-us                         |
| ジンバブエ                                 | ZW                       | ZWE                      | ZW/en-us                         |

