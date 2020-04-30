---
title: パートナー センター REST リソース
description: このセクションでは、パートナーセンター REST API を使用して要求を作成し、応答を解析するために必要な JSON 要素の定義について説明します。
ms.assetid: E7C51D19-C6A7-4A4C-9F17-B4D39195972A
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e452681406a717ef618808b4b699cda5f6684931
ms.sourcegitcommit: f71c7fb2fef51ac7ca0a28717d5f7276bd20ec56
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2020
ms.locfileid: "82559042"
---
# <a name="partner-center-rest-resources"></a>パートナー センター REST リソース

**適用対象**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

このセクションでは、パートナーセンター REST API を使用して要求を作成し、応答を解析するために必要な JSON 要素の定義について説明します。 サンプルコードなど、これらの要素の使用方法の詳細については、「[シナリオ](scenarios.md)」と「[パートナーセンターのサンプル](partner-center-samples.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><a href="analytics-resources.md">Analytics</a></td>
<td><ul>
<li>PartnerLicensesDeploymentInsights</li>
<li>PartnerLicensesUsageInsights</li>
<li>CustomerLicensesDeploymentInsights</li>
<li>PartnerLicensesUsageInsights</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="auditing-resources.md">監査</a></td>
<td><ul>
<li>AuditRecord</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="azure-rate-card-resources.md">Azure 料金カード</a></td>
<td><ul>
<li>AzureRateCard</li>
<li>AzureMeter</li>
<li>AzureOfferTerm</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="azure-utilization-record-resources.md">Azure 使用率レコード</a></td>
<td><ul>
<li>AzureUtilizationRecord</li>
<li>Remove-azureresource</li>
<li>AzureInstanceData</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="cart-resources.md">カート</a></td>
<td><ul>
<li>カート</li>
<li>CartLineItem</li>
<li>CartError</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="conversions-resources.md">変換</a></td>
<td><ul>
<li>変換</li>
<li>ConversionError</li>
<li>ConversionResult</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="country-information-resources.md">CountryInformation</a></td>
<td><ul>
<li>CountryInformation</li>
<li>CountryValidationRules</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="customer-resources.md">顧客</a></td>
<td><ul>
<li>Customer</li>
<li>顧客企業プロファイル</li>
<li>顧客のプロファイル</li>
<li>顧客の Relationshiprequest</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="customer-usage-resources.md">顧客の使用量の予算</a></td>
<td><ul>
<li>CustomerMonthlyUsageRecord</li>
<li>CustomerUsageSummary</li>
<li>PartnerUsageSummary</li>
<li>SpendingBudget</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="entitlement-resources.md">エンタイトルメント</a></td>
<td><ul>
<li>Entitlement</li>
<li>ReferenceOrder</li>
<li>EntitlementType</li>
<li>アーティファクト</li>
<li>ArtifactType</li>
<li>VirtualMachineReservedInstanceArtifact</li>
<li>VirtualMachineReservedInstanceArtifactDetails</li>
<li>VirtualMachineReservation</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="invoice-resources.md">請求書</a></td>
<td><ul>
<li>請求書</li>
<li>InvoiceDetail</li>
<li>InvoiceLineItem</li>
<li>InvoiceSummary</li>
<li>InvoiceSummaryDetail</li>
<li>InvoiceSummaries</li>
<li>Licenseベースの Lineitem</li>
<li>その他の方法</li>
<li>InvoiceStatement</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="license-resources.md">ライセンス</a></td>
<td><ul>
<li>ライセンス</li>
<li>LicenseUpdate</li>
<li>LicenseAssignment</li>
<li>LicenseWarning</li>
<li>ProductSku</li>
<li>ServicePlan</li>
<li>SubscribedSku</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="managed-service-resources.md">ManagedService</a></td>
<td><ul>
<li>ManagedService</li>
<li>ManagedServiceLinks</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="offer-resources.md">プラン</a></td>
<td><ul>
<li>プラン</li>
<li>OfferCategory</li>
<li>OfferLinks</li>
<li>OfferProduct</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="order-resources.md">注文</a></td>
<td><ul>
<li>Order</li>
<li>OrderLineItem</li>
<li>OrderLinks</li>
<li>OrderLineItemLinks</li>
<li>OrderStatus</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="profile-resources.md">プロファイル</a></td>
<td><ul>
<li>BillingProfile</li>
<li>LegalBusinessProfile</li>
<li>MpnProfile</li>
<li>組織のプロファイル</li>
<li>SupportProfile</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="product-resources.md">製品</a></td>
<td><ul>
<li>Product</li>
<li>ItemType</li>
<li>ProductLinks</li>
<li>Sku</li>
<li>可用性</li>
<li>InventoryCheckRequest</li>
<li>InventoryItem</li>
<li>InventoryRestriction</li>
<li>BillingCycleType</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="relationships-resources.md">リレーションシップ</a></td>
<td><ul>
<li>PartnerRelationship</li>
<li>RelationshipRequest</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="self-serve-policy-resources.md">SelfServePolicy</a></td>
<td><ul>
<li>ServiceCostsSummary</li>
<li>ServiceCostsLineItem</li>
<li>ServiceCostsSummaryLinks</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="service-costs-resources.md">ServiceCosts</a></td>
<td><ul>
<li>ServiceCostsSummary</li>
<li>ServiceCostsLineItem</li>
<li>ServiceCostsSummaryLinks</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="service-request-resources.md">ServiceRequest</a></td>
<td><ul>
<li>ServiceRequest</li>
<li>ServiceRequestContact</li>
<li>ServiceRequestNote</li>
<li>ServiceRequestOrganization</li>
<li>SupportTopic</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="subscription-resources.md">サブスクリプション</a></td>
<td><ul>
<li>サブスクリプション</li>
<li>SubscriptionLinks</li>
<li>Subscriptionのプロビジョニングステータス</li>
<li>SubscriptionRegistrationStatus</li>
<li>サポート連絡先</li>
<li>RegisterSubscription</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="subscription-usage-resources.md">サブスクリプションの使用状況</a></td>
<td><ul>
<li>SubscriptionDailyUsageRecord <em>(Obsolete)</em></li>
<li>SubscriptionMonthlyUsageRecord</li>
<li>SubscriptionUsageSummary</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="upgrade-resources.md">アップグレード</a></td>
<td><ul>
<li>アップグレード</li>
<li>UpgradeError</li>
<li>UpgradeResult</li>
<li>UserLicenseError</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="user-resources.md">ユーザー</a></td>
<td><ul>
<li>User</li>
<li>CustomerUser</li>
<li>ユーザー</li>
<li>UserMember</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="utility-resources.md">ユーティリティのリソース</a></td>
<td><ul>
<li>Address</li>
<li>Contact</li>
<li>FieldFilter</li>
<li>FileInfo</li>
<li>Link</li>
<li>PasswordProfile</li>
<li>ResourceLinks</li>
<li>ResourceAttributes</li>
<li>SecureString</li>
<li>ValidationCode</li>
</ul></td>
</tr>
</tbody>
</table>
