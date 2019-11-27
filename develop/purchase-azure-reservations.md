---
title: Azure Reservations を購入する
description: パートナーセンター API を使用して、既存の Microsoft Azure サブスクリプション (0145P) または Azure プランを通じて、お客様向けの Azure 予約を購入できます。
ms.assetid: 1BCDA7B8-93FC-4AAC-94E0-B15BFC95737F
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 85e6325054c6a5dc257ac7a70169fa020a68345d
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488132"
---
# <a name="purchase-azure-reservations"></a>Azure Reservations を購入する

適用対象:

- パートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンター API を使用して顧客の Azure 予約を購入するには、既存の Microsoft Azure (**MS AZR-0145P**) サブスクリプションまたは azure プランが必要です。

> [!NOTE]  
> 次の市場では Azure Reservations を利用できません。
>  
> | 利用できないマーケット            | &nbsp;                            | &nbsp;                                   |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | オーランド諸島                  | グリーンランド                         | パプアニューギニア                         |
> | 米領サモア                 | グレナダ                           | ピトケアン島                         |
> | アンドラ                        | グアドループ                        | レユニオン                                  |
> | アンギラ                       | グアム                              | ロシア連邦                       |
> | 南極                     | ガーンジー島                          | サバ島                                     |
> | アンティグア・バーブーダ            | ギニア                            | サン・バルテルミー                         |
> | アルバ                          | ギニアビサウ                     | セントルシア                              |
> | ベナン                          | ガイアナ                            | サンマルタン島                             |
> | ブータン                         | ハイチ                             | サンピエール・ミクロン                |
> | ボネール島                        | ハード・マクドナルド諸島 | セントビンセントおよびグレナディーン諸島         |
> | ブーベ島                  | マン島                       | サモア                                    |
> | ブラジル                         | ヤンマイエン島                         | サンマリノ                               |
> | 英領インド洋地域 | ジャージー島                            | サントメ・プリンシペ                    |
> | 英領バージン諸島         | キリバス                          | セーシェル                               |
> | ブルキナファソ                   | コソボ                            | シエラレオネ                             |
> | ブルンジ                        | ラオス                              | シント・ユースタティウス島                           |
> | カンボジア                       | レソト                           | シント・マールテン島                             |
> | 中央アフリカ共和国       | リベリア                           | ソロモン諸島                          |
> | チャド                           | マダガスカル                        | ソマリア                                  |
> | 中国                          | マラウイ                            | サウスジョージア・サウスサンドウィッチ諸島 |
> | クリスマス島               | モルディブ                          | 南スーダン                              |
> | ココス諸島        | マリ                              | セントヘレナ、アセンションおよびトリスタンダクーニャ   |
> | コモロ                        | マーシャル諸島                  | スリナム                                 |
> | コンゴ共和国                          | マルチニーク島                        | スバールバル諸島                                 |
> | コンゴ民主共和国                    | モーリタニア                        | スワジランド                                |
> | クック諸島                   | マイヨット島                           | ティモール・レステ                              |
> | ジブチ                       | ミクロネシア                        | トーゴ                                     |
> | ドミニカ国                       | モンセラット                        | トケラウ諸島                                  |
> | 赤道ギニア              | モザンビーク                        | トンガ                                    |
> | エリトリア                        | ミャンマー                           | タークス・カイコス諸島                 |
> | フォークランド諸島               | ナウル                             | ツバル                                   |
> | フランス領ギアナ                  | ニューカレドニア                     | 合衆国領有小離島                    |
> | フランス領ポリネシア               | ニジェール                             | バヌアツ                                  |
> | 仏領極南諸島    | ニウエ                              | バチカン市国                             |
> | ガボン                          | ノーフォーク島                    | ワリス・フテュナ諸島                        |
> | ガンビア                         | 北マリアナ諸島          | イエメン                                    |
> | ジブラルタル                      | パラオ                             | &nbsp;                                   |
>  

## <a name="prerequisites"></a>前提条件

- 「[パートナーセンターの認証](partner-center-authentication.md)」で説明されている資格情報。 このシナリオでは、スタンドアロンアプリとアプリ + ユーザー資格情報の両方を使用した認証がサポートされています。
- 顧客識別子。 顧客の ID を持っていない場合は、[顧客] リストから顧客を選択し、[アカウント] を選択して、Microsoft ID を保存することで、パートナーセンターで ID を検索できます。
- アクティブな CSP Azure サブスクリプションまたは Azure プランのサブスクリプション ID。

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Microsoft Azure 予約を購入する方法

Azure 予約を追加するアクティブな CSP Azure サブスクリプションを特定したら、次の手順を使用して購入します。

1. [有効化](#enablement)-アクティブな CSP azure サブスクリプションを登録して、azure 予約を購入できるようにします。
2. [[検出](#discovery)]-購入する Azure 予約製品と sku を検索して選択し、その可用性を確認します。
3. [注文の送信](#order-submission)-注文の品目を含むショッピングカートを作成して送信します。
4. [注文の詳細を取得](#get-order-details)する-注文の詳細、顧客のすべての注文、または請求サイクルの種類別の注文を表示します。

Azure の予約を購入した後、次のシナリオでは、Azure 予約の権利に関する情報を取得してライフサイクルを管理する方法と、残高明細書、請求書、および請求書の概要を取得する方法について説明します。

- [ライフサイクル管理](#lifecycle-management)
- [請求書と調整](#invoice-and-reconciliation)

## <a name="enablement"></a>有効化

有効化とは、サブスクリプションを登録して Azure 予約 VM インスタンスに既存の Microsoft Azure (**MS AZR-0145P**) サブスクリプションを関連付け、azure 予約に有効にすることです。 登録は Azure Reserved VM Instances を購入するための前提条件です。

次の理由により、サブスクリプションが必要です。

1. お客様がリソースをデプロイする資格があるかどうかを確認し、リージョンで Azure Reserved VM Instances を購入します。
2. サブスクリプションでのデプロイの容量の優先順位を指定します。 これは、 **[容量優先度]** オプションが選択されている単一のスコープ Azure Reserved VM Instances にのみ適用されます。

Azure 予約を追加するアクティブなサブスクリプションを特定したら、サブスクリプションを登録して Azure の予約に有効にする必要があります。 既存の[サブスクリプション](subscription-resources.md)リソースを登録して Azure 予約の順序付けを有効にする方法については、「[サブスクリプションを登録](register-a-subscription.md)する」を参照してください。

サブスクリプションを登録した後、登録の状態を確認して、登録プロセスが完了したことを確認する必要があります。 これを行うには、「[サブスクリプションの登録状態を取得](get-subscription-registration-status.md)する」を参照してください。

> [!NOTE]  
> Azure プランを使用して顧客の Microsoft Azure 予約を購入する場合は、まず Azure プランを登録する必要があります。 Microsoft Azure (**0145P**) サブスクリプションと同様に、Azure プランはパートナーセンターの[サブスクリプション](subscription-resources.md)リソースによって表されます。 そのため、同じ[サブスクリプション登録](register-a-subscription.md)方法を使用して、Azure プランを登録できます。

## <a name="discovery"></a>情報表示

サブスクリプションで Azure 予約を購入できるようになったら、次のパートナーセンター API モデルを使用して、製品と Sku を選択し、その可用性を確認することができます。

- [Product](product-resources.md#product) -購入可能な商品またはサービスのグループ化構成体。 製品自体は購入可能なの項目ではありません。
- [Sku](product-resources.md#sku) -製品の購入可能な在庫保持ユニット (sku)。 これらは、製品のさまざまな形状を表します。
- [可用性](product-resources.md#availability)-SKU を購入できるようにする構成 (国、通貨、業界セグメントなど)。

Azure 予約を購入する前に、次の手順を実行します。

1. 購入する製品と SKU を特定して取得します。 これを行うには、まず製品と Sku を一覧表示します。または、製品と SKU の Id が既にわかっている場合は、それらを選択します。

    - [製品の一覧を取得する (国別)](get-a-list-of-products.md)
    - [製品 ID を使用して製品を取得する](get-a-product-by-id.md)
    - [製品の Sku の一覧を取得する (国別)](get-a-list-of-skus-for-a-product.md)
    - [SKU ID を使用して SKU を取得する](get-a-sku-by-id.md)

2. SKU のインベントリを確認します。 この手順は、 **InventoryCheck**の前提条件でタグ付けされている sku にのみ必要です。

    - [インベントリの確認](check-inventory.md)

3. [SKU](product-resources.md#sku)の[可用性](product-resources.md#availability)を取得します。 注文を配置するときに、可用性の**Catalogitemid**が必要になります。 この値を取得するには、次の Api のいずれかを使用します。

    - [SKU に使用できる機能の一覧を取得する (国別)](get-a-list-of-availabilities-for-a-sku.md)
    - [可用性 ID を使用して可用性を取得する](get-an-availability-by-id.md)

> [!IMPORTANT]  
> 各 Microsoft Azure 予約製品には、Microsoft Azure (**0145P**) サブスクリプションと Azure プランに対して異なる利用能力があります。 (国別に[) 製品の一覧を取得](get-a-list-of-products.md)したり、(国ごとに)[製品の sku の](get-a-list-of-skus-for-a-product.md)一覧を取得したり、Azure プランにのみ適用される[sku (国別)](get-a-list-of-availabilities-for-a-sku.md)の利用可能な機能の一覧を取得したりするには、"reservationScope = AzurePlan" パラメーターを指定します。

## <a name="order-submission"></a>注文の送信

Azure 予約注文を送信するには、次の手順を実行します。

1. 購入するカタログアイテムのコレクションを保持するカートを作成します。 [カート](cart-resources.md)を作成すると、同じ[順序](order-resources.md)で一緒に購入できるものに基づいて[カートの品目](cart-resources.md#cartlineitem)が自動的にグループ化されます。

    - [ショッピングカートを作成する](create-a-cart.md)
    - [ショッピングカートを更新する](update-a-cart.md)

2. カートをチェックアウトします。 カートをチェックアウトすると、[注文](order-resources.md)が作成されます。

    - [カートをチェックアウトする](checkout-a-cart.md)

## <a name="get-order-details"></a>注文の詳細を取得する

Azure 予約注文を作成したら、注文 ID を使用して個々の注文の詳細を取得したり、顧客の注文の一覧を取得したりできます。 注文が送信されてから顧客の注文の一覧に表示されるまでに、最大15分の遅延が発生することに注意してください。

- 注文 ID を使用して個々の注文の詳細を取得します。 「 [ID で注文を取得する](get-an-order-by-id.md)」を参照してください。

- 顧客 ID を使用して顧客の注文の一覧を取得します。 「[顧客の注文をすべて取得する](get-all-of-a-customer-s-orders.md)」を参照してください。

- [請求サイクルの種類](product-resources.md#billingcycletype)によって顧客の注文の一覧を取得するには、Azure 予約注文 (1 回限りの料金) と年間または月単位または月単位で請求される注文を個別に一覧表示します。 「[顧客と請求サイクルの種類別の注文の一覧を取得する](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)」を参照してください。

## <a name="lifecycle-management"></a>ライフサイクルの管理

パートナーセンターで Azure の予約のライフサイクルを管理する過程で、Azure 予約の[権利](entitlement-resources.md)に関する情報を取得し、予約注文 ID を使用して予約の詳細を取得することができます。 これを行う方法の例については、「[権利の取得](get-a-collection-of-entitlements.md)」を参照してください。   

## <a name="invoice-and-reconciliation"></a>請求書と調整

次のシナリオでは、顧客の[請求書](invoice-resources.md)をプログラムで表示し、Azure 予約の1回限りの料金を含むアカウントの残高と概要を取得する方法について説明します。  

**残高と支払い**定期的な料金と1回限りの (Azure 予約) 料金のバランスを取る既定の通貨の種類で現在のアカウント残高を取得する方法については、「[現在のアカウント残高を取得](get-the-reseller-s-current-account-balance.md)する」を参照してください。

**複数通貨の残高と支払い**現在のアカウント残高と、顧客の通貨の種類ごとに1回だけ課金される請求書の概要を含む請求書の概要を取得するには、「[請求書の概要を取得](get-invoice-summaries.md)する」を参照してください。

**請求書**定期的な料金と1回の課金の両方を示す請求書のコレクションを取得するには、「[請求書のコレクションを取得](get-a-collection-of-invoices.md)する」を参照してください。 

**1 つの請求書**請求書 ID を使用して特定の請求書を取得するには、「 [ID で請求書を取得](get-invoice-by-id.md)する」を参照してください。  

**調整**特定の請求書 ID の請求書明細項目の詳細 (調整行項目) のコレクションを取得するには、「[請求書明細項目を取得](get-invoiceline-items.md)する」を参照してください。  

**PDF として請求書をダウンロード**する請求書 ID を使用して PDF 形式で請求書明細書を取得するには、「 [invoice ステートメントを取得](get-invoice-statement.md)する」を参照してください。
