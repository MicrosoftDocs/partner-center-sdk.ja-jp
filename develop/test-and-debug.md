---
title: テストとデバッグ
description: コードをテストするには、パートナーセンター (および対応するトークン) で統合サンドボックスアカウントを使用する必要があります。これにより、会社が支払いを行う新しい料金が誤って発生することはありません。
ms.assetid: 0A84F92F-CE66-42DF-B686-4D9E6FFECB16
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 4773474582c1eac17291c0021be1b4d085c57ed3
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487982"
---
# <a name="test-and-debug"></a>テストとデバッグ


**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

コードをテストするには、パートナーセンター (および対応するトークン) で統合サンドボックスアカウントを使用する必要があります。これにより、会社が支払いを行う新しい料金が誤って発生することはありません。 この運用環境 (TiP) 環境の詳細については、「[パートナーセンターでの API アクセスの設定](set-up-api-access-in-partner-center.md)」を参照してください。

## <a name="span-idintegration_sandbox_constraintsspan-idintegration_sandbox_constraintsspan-idintegration_sandbox_constraintsintegration-sandbox-constraints"></a><span id="Integration_sandbox_constraints"/><span id="integration_sandbox_constraints"/><span id="INTEGRATION_SANDBOX_CONSTRAINTS"/>統合サンドボックスの制約

自動ビルド検証テストを実行する場合、運用環境でテストを実施する場合、または統合サンドボックスで手動テストを実行する場合は、統合サンドボックスの上限に近づいている可能性があります。 これらの制限は、75のお客様、1人の顧客につき5つのサブスクリプション、サブスクリプションあたり25座席です。 

これは、少なくとも25台のシートを超える接続クライアント要件がある、サンドボックス内のプランを取得できないことを意味します。 これには、試用版も含まれます。 

### <a name="azure-plan"></a>Azure プラン
既定では、パートナーは、サンドボックスアカウントを使用して Azure プランをプロビジョニングすることはできません。 サンドボックスアカウントを使用してこれを行う必要があるパートナーは、アクセスするために適用する必要があります。 アクセスを申請するには、Microsoft アカウント manager またはビジネス連絡先に連絡してください。 サンドボックスアカウント内のプロビジョニング Microsoft Azure (0145P) サブスクリプションへのアクセスが既に適用されているパートナーは、再度アクセスするために適用する必要はありません。 Azure プランを自動的にプロビジョニングするためのアクセス権が付与されます。

Azure プランをプロビジョニングするためにサンドボックスアカウントが承認されているパートナーには、次の制限が適用されます。

- 各サンドボックスパートナーアカウントは、すべての顧客テナントに対して最大10個の Azure プランを持つことができます (プランが顧客間でどのように分散されているかは関係ありません)。
- ダイレクト請求パートナーは、顧客テナントごとに最大1つの Azure プランを作成できます。
- 間接プロバイダーは、顧客テナントごとに最大3つの Azure プランを作成できます (異なる間接リセラーがレコードのパートナーとして指定されている場合)。
- 各 Azure プランには、最大3つの Azure サブスクリプションを含めることができます。
- サンドボックスアカウントの各 CSP Azure サブスクリプションは、データセンターごとに4つの仮想マシン (VM) コアに制限されています。 そのため、4個を超える VM コアを必要とする VM Sku をプロビジョニングすることはできません。 GPU コアなどの特定の特殊化された VM Sku も除外されます。
- 各サンドボックスパートナーアカウントには、すべての Azure プランの請求サイクルあたり $2000 (USD) の使用制限があります。 パートナーが使用制限に達すると、次の請求サイクルまで、すべての Azure プランが一時的に無効になります。

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>クラウドソリューションプロバイダー (CSP) の Azure サブスクリプションプラン 
CSP の Azure サブスクリプションプランは、既定ではサンドボックスアカウントには使用できなくなりました。 これには、Microsoft パブリッククラウド、ドイツのクラウドおよび政府クラウドの CSP の Azure サブスクリプションについて、0146P、0146P、米国政府-0146P がそれぞれ含まれます。 サンドボックス アカウントでこれらのプランにアクセスする必要があるパートナーは、アクセスを申請する必要があります。 アクセスを申請するには、Microsoft アカウント manager またはビジネス連絡先に連絡してください。 

CSP アカウントが Azure サブスクリプションのプランに対して承認されているパートナーの場合、次の制限が適用されます。  

 - 最大で375のアクティブなサブスクリプション (顧客ごとに75の顧客 x 5 サブスクリプション) を使用できます。 ただし、CSP Azure サブスクリプションとして使用できるのは10個のみです。  
 - CSP Azure サブスクリプションが Azure の使用量の $200 に達すると、そのリソースは次の請求サイクルまで一時的に無効になります。 まだアクティブなサブスクリプションと見なされ、10個のアクティブな Azure サブスクリプションの制限に対してカウントされます。  
 - サンドボックスアカウントの各 CSP Azure サブスクリプションは、データセンターごとに4つの仮想マシン (VM) コアに制限されています。 そのため、4個を超える VM コアを必要とする VM Sku をプロビジョニングすることはできません。 GPU コアなどの特定の特殊化された VM Sku も除外されます。  

> [!Important]  
> 2018年8月1日より前にサンドボックスアカウントを使用してプロビジョニングされた既存の CSP Azure サブスクリプションはすべてサポートされなくなり、10月16日から2018年10月31日の間にマイクロソフトによってプロビジョニング解除されます。 サブスクリプションがプロビジョン解除されると、再度有効化することはできず、関連付けられたデータにもアクセスできなくなります。 これらのサブスクリプションで重要なデータを格納しているパートナーは、2018 年 10 月 16日までにデータをバックアップしておいてください。

### <a name="azure-reserved-vm-instance"></a>Azure 予約 VM インスタンス  

サンドボックスアカウントを使用して[Azure 予約 VM インスタンスを購入](purchase-azure-reservations.md)している場合、お客様ごとに VM インスタンスは2つに制限されます。 また、次の Azure 予約 VM インスタンスの製品 Sku からのみ選択できます。 

| 製品タイトル  | ［有効日］  | Sku のタイトル                                               | 領域 [ArmRegionName] | インスタンスキー [ArmSkuName] | Duration | 従量課金メーター Id       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B シリーズ       | 12/1/2017 0:00  | 予約 VM インスタンス、Standard_B1s、韓国南部、1年    | KoreaSouth             | Standard_B1s | 1年    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B シリーズ       | 12/1/2017 0:00  | 予約 VM インスタンス、Standard_B1s、米国東部、1年     | eastus                 | Standard_B1s | 1年    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B シリーズ       | 12/1/2017 0:00  | 予約 VM インスタンス、Standard_B1s、米国西部2、1年   | westus2                | Standard_B1s | 1年    | 222e39f5-e99f47 fa3-a323-f4640297788 8 |
| B シリーズ       | 12/1/2017 0:00  | 予約 VM インスタンス、Standard_B1s、米国中北部、1年    | northcentralus | Standard_B1s | 1年    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B シリーズ       | 12/1/2017 0:00  | 予約 VM インスタンス、Standard_B1s、CA 東部、1年間     | CanadaEast             | Standard_B1s | 1年    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |
     
### <a name="subscriptions-for-commercial-marketplace-products"></a>商用 marketplace 製品のサブスクリプション

運用環境では、[商用 Marketplace SaaS 製品へのサブスクリプションを作成](create-subscription-azure-marketplace-products.md)した後で、パートナーセンターからパーソナライズされたアクティベーションリンクを取得し、発行者のサイトにアクセスしてセットアッププロセスを完了する必要があります。 サブスクリプションの課金は、セットアップの完了後にのみ開始されます。

CSP サンドボックス環境では、Isv との統合はありません。 パートナーセンターからライセンス認証リンクを取得しようとすると、ダミーリンクが返されます。 このダミーリンクを使用して、発行元のサイトでセットアッププロセスを完了することはできません。 統合サンドボックスアカウントを使用して、商用 marketplace SaaS 製品へのサブスクリプションの課金をテストするには、「[商用 marketplace 製品のサンドボックスサブスクリプションをアクティブ化](activate-sandbox-subscription-azure-marketplace-products.md)する」を参照してください。 アクティブ化が成功すると、サブスクリプションの課金が開始されます。


テストの実行の終了時にクリーンアップを行うには、次のテストのラウンドのための領域があります。次のトピックを参照してください。

- [統合サンドボックスから顧客アカウントを削除する](delete-a-customer-account-from-the-integration-sandbox.md)

- [サブスクリプションの数量を減らす](change-the-quantity-of-a-subscription.md)

- [サブスクリプションを中断](suspend-a-subscription.md)して、削除できるようにします。

## <a name="span-idbest_practices_for_rest_developmentspan-idbest_practices_for_rest_developmentspan-idbest_practices_for_rest_developmentbest-practices-for-rest-development"></a><span id="Best_practices_for_REST_development"/><span id="best_practices_for_rest_development"/><span id="BEST_PRACTICES_FOR_REST_DEVELOPMENT"/>REST 開発のベストプラクティス


- ネットワークトレースツールを使用すると、要求、応答、および応答の HTTP 状態コードにエラーがあったかどうかを確認できます。 エラー処理の詳細については、「[パートナーセンターの REST エラーコード](error-codes.md)」を参照してください。

- パートナーセンター REST API に対する呼び出しごとに新しい関連付け ID を使用します。 これにより、ログ記録が向上し、デバッグ中に役立ちます。 詳細については、「[パートナーセンターの REST ヘッダー](headers.md)」を参照してください。

## <a name="span-idtroubleshooting_tips_for_common_rest_problemsspan-idtroubleshooting_tips_for_common_rest_problemsspan-idtroubleshooting_tips_for_common_rest_problemstroubleshooting-tips-for-common-rest-problems"></a>一般的な REST の問題に関するトラブルシューティングのヒントを <span id="Troubleshooting_tips_for_common_REST_problems"/><span id="troubleshooting_tips_for_common_rest_problems"/><span id="TROUBLESHOOTING_TIPS_FOR_COMMON_REST_PROBLEMS"/>


- URL と API バージョンを含む、すべてのヘッダープロパティを確認します。

- 必要に応じて、適切に書式設定されたプロパティが含まれていることを確認します。

- 配列の書式設定が正しくないことが一般的なエラーです。

- **Etag**は一時的なものであるため、保存しないでください。 関数呼び出しで**etag**が必要な場合は、リソースをもう一度取得して最新の**etag**値を使用します。 **Etag**の値は、文字列のように二重引用符で囲む必要があります。

    ```
    If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
    ```

 

 




