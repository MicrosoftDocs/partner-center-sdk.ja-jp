---
title: パートナーセンター分析
description: パートナーセンター分析パブリック API ドキュメント。
ms.assetid: B605C1CD-FC40-4393-8588-55C8F0CAA51A
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6cb716010afa61f60f2eb5d7b3f56c4bc9f46adc
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416430"
---
# <a name="partner-center-analytics---resources"></a>パートナーセンター分析-リソース

**適用対象**

- Partner Center
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


Analytics API を使用すると、ユーザーエクスペリエンスに表示されているデータにプログラムでアクセスできます。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>の前提条件


- [パートナー センターの認証](partner-center-authentication.md)に関するページで説明している資格情報。 これらのシナリオでは、ユーザー資格情報のみを使用した認証がサポートされます。


## <a name="span-idazure_usage_analyticsspan-idazure_usage_analyticsspan-idazure_usage_analyticscsp-program-azure-usage-analytics"></a><span id="Azure_Usage_Analytics"/><span id="azure_usage_analytics"/><span id="AZURE_USAGE_ANALYTICS"/>CSP プログラム: Azure usage analytics

次のシナリオでは、Analytics API を使用して、パートナーセンターの Azure usage analytics のすべての情報を取得する方法について説明します。  

- [Azure の使用量分析情報をすべて取得する](get-all-azure-usage-analytics.md)  

このシナリオでは、 [Azure の使用](#azure_usage)リソースのコレクションに分析情報が返されます。 

## <a name="span-idazure_usagespan-idazure_usagespan-idazure_usageazure-usage-resource"></a>Azure usage resource <span id="AZURE_USAGE"/><span id="azure_usage"/><span id="Azure_Usage"/>

Azure の使用に関するすべての分析データを表します。

| プロパティ | 種類 | 説明 |
|----------|------|-------------|
| 顧客 Tenantid | string | 顧客のテナント識別子。 |
| customerName | string | 顧客名。 |
| subscriptionId | string | サブスクリプション識別子。 |
| subscriptionName | string | サブスクリプション名。 |
| 日付 | string | 使用日。 |
| resourceLocation | string | データセンターの場所 (西ヨーロッパなど)。 |
| MeterCategory | string | 測定カテゴリ、データ管理など。 |
| meterSubcategory カテゴリ | string | 測定サブカテゴリ (geo 冗長など)。 |
| meterUnit | string | 測定単位 (ギガバイトや時間など)。 | 
| ReservationOrderId | string | Azure VM の予約済みインスタンスの予約順序。 |
| reservationId | string | 特定の RI 順序での予約インスタンス。 |
| serviceType | string | 仮想マシンの種類を示します。 たとえば、Standard_E4s_v3 のようにします。 |
| quantity | long | メーター単位で使用される数値を示します。 |


## <a name="span-idindirect_resellers_analyticsspan-idindirect_resellers_analyticsspan-idindirect_resellers_analyticscsp-program-indirect-resellers-analytics"></a><span id="Indirect_Resellers_Analytics"/><span id="indirect_resellers_analytics"/><span id="INDIRECT_RESELLERS_ANALYTICS"/>CSP プログラム: 間接リセラー分析

次のシナリオでは、Analytics API を使用して、すべてのパートナーセンターの間接リセラーの分析情報を取得する方法について説明します。  

- [間接顧客の分析情報をすべて取得する](get-all-indirect-resellers-analytics.md)  

このシナリオでは、[間接リセラー](#indirect_resellers)リソースのコレクションに分析情報が返されます。 


## <a name="span-idindirect_resellersspan-idindirect_resellersspan-ididirect_resellersindirect-resellers-resource"></a><span id="Indirect_Resellers"/><span id="indirect_resellers"/><span id="IDIRECT_RESELLERS"/>間接リセラーリソース

間接リセラーのすべての分析データを表します。

| プロパティ | 種類 | 説明 |
|----------|------|-------------|
| partnerTenantId | string | 間接リセラーデータを取得するパートナーのテナント ID。 |
| id | string | 間接リセラー ID。 |
| name | string | 間接リセラーデータを取得するパートナーの名前。 |
| market | string | 間接リセラーデータを取得するパートナーの市場。 |
| firstSubscriptionCreationDate | UTC 日時形式の文字列 | 間接リセラーデータを取得する最初のサブスクリプションの作成日。 |
| latestSubscriptionCreationDate | UTC 日時形式の文字列 | 最新のサブスクリプションの作成日。 |
| firstSubscriptionEndDate | UTC 日時形式の文字列 | サブスクリプションが初めて終了したとき。 |
| latestSubscriptionEndDate | UTC 日時形式の文字列 | 任意のサブスクリプションが終了した最後の日付。 |
| firstSubscriptionSuspendedDate | UTC 日時形式の文字列 | サブスクリプションが初めて中断されたとき。 |
| latestSubscriptionSuspendedDate | UTC 日時形式の文字列 | サブスクリプションが中断された最後の日付。 |
| firstSubscriptionDeprovisionedDate | UTC 日時形式の文字列 | サブスクリプションが初めてプロビジョニング解除されたとき。 |
| latestSubscriptionDeprovisionedDate | UTC 日時形式の文字列 | サブスクリプションがプロビジョニング解除された最後の日付。 |
| subscriptionCount | double | すべての付加価値再販業者のサブスクリプション数 |
| licenseCount | double | すべての付加価値再販業者のライセンス数 |
| indirectResellerCount | double | 間接リセラー数 |


## <a name="span-idsubscription_analyticsspan-idsubscription_analyticsspan-idsubscription_analyticscsp-program-subscription-analytics"></a><span id="Subscription_Analytics"/><span id="subscription_analytics"/><span id="SUBSCRIPTION_ANALYTICS"/>CSP プログラム: サブスクリプション分析

次のシナリオでは、Analytics API を使用して、すべてのパートナーセンターのサブスクリプション分析情報を取得したり、検索クエリでフィルター処理したり、日付や用語でグループ化したりする方法について説明します。  

- [サブスクリプションの分析情報をすべて取得する](get-all-subscription-analytics.md)  
- [検索クエリでフィルター処理されたサブスクリプションの分析情報を取得する](get-subscription-analytics-by-search-query.md)  
- [日付またはご契約条件でグループ化されたサブスクリプションの分析情報を取得する](get-subscription-analytics-grouped-by-dates-or-terms.md)  

これらすべてのシナリオでは、[サブスクリプション](#subscription)リソースのコレクションで分析情報が返されます。 


## <a name="span-idsubscriptionspan-idsubscriptionspan-idsubscriptionsubscription-resource"></a><span id="Subscription"/><span id="subscription"/><span id="SUBSCRIPTION"/>サブスクリプションリソース


サブスクリプションのすべての分析データを表します。


|         プロパティ          |              種類              |                                                                      説明                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     顧客 Tenantid      |             string             |                                              顧客のテナントを識別する GUID 形式の文字列。                                              |
|       customerName        |             string             |                                                               顧客の名前。                                                                |
|      顧客市場       |             string             |                                                 顧客が事業を行っている国/地域。                                                 |
|            id             |             string             |                                                              サブスクリプション識別子。                                                              |
|          状態           |             string             |                                          サブスクリプションの状態: "ACTIVE"、"中断"、または "プロビジョニング解除"。                                           |
|        productName        |             string             |                                                                製品の名前。                                                                |
|     subscriptionType      |             string             |       サブスクリプションの種類。 **注**: このフィールドでは大文字と小文字が区別されます。 サポートされている値は、"Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS" です。       |
|     autoRenewEnabled      |            boolean             |                                         サブスクリプションが自動的に更新されるかどうかを示す値です。                                          |
|         パートナー         |             string             | MPN ID です。 ダイレクトリセラーの場合、これはパートナーの MPN ID になります。 間接リセラーの場合、これは間接リセラーの MPN ID になります。 |
|       friendlyName        |             string             |                                                             サブスクリプションの名前です。                                                              |
|        partnerName        |             string             |                                              サブスクリプションが購入されたパートナーの名前                                               |
|       providerName        |             string             |            間接リセラーのサブスクリプショントランザクションの場合、プロバイダー名はサブスクリプションを購入した間接プロバイダーになります。             |
|    And rateplancharge.effectivestartdate     | UTC 日時形式の文字列 |                                                           サブスクリプションが開始された日付。                                                            |
|     Commitの Enddate     | UTC 日時形式の文字列 |                                                            サブスクリプションが終了する日付。                                                             |
|    currentStateEndDate    | UTC 日時形式の文字列 |                                           サブスクリプションの現在の状態が変更される日付。                                            |
| trialToPaidConversionDate | UTC 日時形式の文字列 |                                 サブスクリプションが試用から有料に変換される日付。 既定値は null です。                                 |
|      trialStartDate       | UTC 日時形式の文字列 |                                サブスクリプションの試用期間が開始された日付。 既定値は null です。                                 |
|       trialEndDate        | UTC 日時形式の文字列 |                                  サブスクリプションの試用期間が終了した日付。 既定値は null です。                                  |
|       Lastの終了日       | UTC 日時形式の文字列 |                                        サブスクリプションが最後に使用された日付。 既定値は null です。                                        |
|     deprovisionedDate     | UTC 日時形式の文字列 |                                      サブスクリプションがプロビジョニング解除された日付。 既定値は null です。                                      |
|      lastRenewalDate      | UTC 日時形式の文字列 |                                       サブスクリプションが最後に更新された日付は、既定値は null になります。                                       |
|       licenseCount        |             number             |                                                             ライセンスの合計数。                                                              |
|     subscriptionCount     |             number             |                        サブスクリプションの数。 注: この値は、集計クエリの応答にのみ表示されます。                         |

## <a name="span-idsearch_analyticsspan-idsearch_analyticsspan-idsearch_analyticssearch-analytics"></a><span id="Search_Analytics"/><span id="search_analytics"/><span id="SEARCH_ANALYTICS"/>検索分析

> [!NOTE]  
> CSP プログラムのメンバーシップは、検索分析を取得するためには必要ありません。

次のシナリオでは、Analytics API を使用して、すべてのパートナーセンター検索分析情報を取得する方法について説明します。  

- [検索の分析情報をすべて取得する](get-all-search-analytics.md)  

このシナリオでは、[検索](#search_resource)リソースのコレクションに分析情報が返されます。 


## <a name="span-idsearch_resourcespan-idsearch_resourcespan-idsearch_resourcesearch-resource"></a><span id="Search_Resource"/><span id="search_resource"/><span id="SEARCH_RESOURCE"/>検索リソース

検索のすべての分析データを表します。

| プロパティ | 種類 | 説明 |  
|----------|------|-------------|  
| 仕入 | string | 請求先の会社名。 |
| contactButtonClicked クリックされました | ブール値 | [Contact] ボタンがクリックされたかどうかを示します。 |
| keywordCountry | string | 検索で指定された国。 |
| 表示の表示 | ブール値 | 検索の詳細が表示されたかどうかを示します。 |
| keywordIndustryFocus | string | 医療などで検索する業界。 |
| mpnId | string | Microsoft Partner Network (MPN) ID です。 ダイレクトリセラーの場合、これはパートナーの MPN ID になります。 間接リセラーの場合、これは間接リセラーの MPN ID になります。 |
| partnerMarket | string | パートナーがビジネスを運営するロケール。 |
| keywordProduct | string | 検索で指定された製品。 |
| referralSubmitted | ブール値 | 紹介が送信されたかどうかを示します。 |
| searchDate | UTC 日時形式の文字列 | 検索クエリが発生した日付。 |
| keywordSearchText | string | 検索で指定されたテキスト。 |
| searchResultPageViews | long | パートナーが検索結果に登場した回数。 集計にのみ応答の一部。
| contactClicks クリック | long | [Contact] ボタンがクリックされた回数。 集計にのみ応答の一部。
| referralCount | long | 検索から生成された参照の数。 集計にのみ応答の一部。
| profileViews | long | パートナープロファイルが表示された回数。 集計にのみ応答の一部。


## <a name="span-idreferral_analyticsspan-idreferral_analyticsspan-idreferral_analyticsreferrals-analytics"></a><span id="Referral_Analytics"/><span id="referral_analytics"/><span id="REFERRAL_ANALYTICS"/>紹介分析

> [!NOTE]  
> CSP プログラムのメンバーシップは、紹介分析を取得するためには必要ありません。

次のシナリオでは、Analytics API を使用して、すべてのパートナーセンターの紹介分析情報を取得する方法について説明します。  

- [紹介の分析情報をすべて取得する](get-all-referrals-analytics.md)  

このシナリオでは、[参照](#referrals)リソースのコレクションに分析情報が返されます。 

> [!NOTE]  
> 照会分析は、21Vianet が運用するパートナーセンターでは利用できません。 


## <a name="span-idreferralsspan-idreferralsspan-idreferralsreferrals-resource"></a><span id="Referrals"/><span id="referrals"/><span id="REFERRALS"/>参照リソース

紹介のすべての分析データを表します。

| プロパティ | 種類 | 説明 |
|----------|------|-------------|
| id | string | 顧客のテナント識別子。  |
| 状態 | string | 紹介が顧客に対しているかどうかを示します。  |
| 顧客市場 | string | 顧客が事業を行っている国/地域。 |
| customerName | string | 顧客の名前。 |
| 顧客 Orgsize | string | 顧客の組織内の従業員の数を示す範囲。 たとえば、"10to50employees" のようになります。 |
| acceptedDate | UTC 日時形式の文字列 | 紹介が受け入れられた日付。 |
| acknowledgedDate | UTC 日時形式の文字列 | 参照が確認された日付。 |
| archivedDate | UTC 日時形式の文字列 | 参照がアーカイブされた日付。 |
| declinedDate | UTC 日時形式の文字列 | 参照が拒否された日付。 |
| expiredDate | UTC 日時形式の文字列 | 参照の有効期限が切れた日付。 |
| lostDate | UTC 日時形式の文字列 | 参照が失われた日付。 |
| missedDate | UTC 日時形式の文字列 | 参照が見つからなかった日付。 |
| createdDate | UTC 日時形式の文字列 | 参照が作成された日付。 |
| skippedDate | UTC 日時形式の文字列 | 参照がスキップされた日付。 |
| wonDate | UTC 日時形式の文字列 | 参照が受注された日付。 |
| partnerMarket | string |  パートナーが事業を行っている国/地域。 |  
