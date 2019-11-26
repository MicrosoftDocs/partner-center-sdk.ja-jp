---
title: Entitlement resources
description: Describes resources related to entitlement.
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: dc291e4d286e6eeeb1ce4ae6faeb965f59bb1c33
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74490092"
---
# <a name="entitlement-resources"></a>Entitlement resources


**Applies To**

- パートナー センター
- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター


## <a name="span-identitlementspan-identitlementspan-identitlemententitlement"></a><span id="Entitlement"/><span id="entitlement"/><span id="ENTITLEMENT"/>Entitlement


This resource represents the products to which the customer has right to use because of partner purchase on items from the catalog. 

| プロパティ | タスクバーの検索ボックスに | 説明 |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | The order reference which resulted in the entitlement. |
| productId | string | The ID of the product. |
| skuID | string | The ID of the SKU. |
| quantity | 整数 | The quantity of entitlements (excludes Unfulfilled/Transfered entitlements). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | The list of entitlement quantity details (the number of items and status of each quantity). |
| entitlementType | string | The type of entitlement. (Updated to string from [EntitlementType](#entitlementtype) in SDK 1.8.) |
| entitledArtifacts | IEnumerable<[Artifact](#artifact)> | The list of artifacts associated with the entitlement. |
| IncludedEntitlements | IEnumerable<[Entitlement](#artifact)> | The list of entitlements which are implicitly included as a result of the ProductId / SkuId purchase from catalog. |
| ExpiryDate | string in UTC date-time format  | The entitlement expiry date (if applicable). |


## <a name="span-idreferenceorderspan-idreferenceorderspan-idreferenceorderreferenceorder"></a><span id="ReferenceOrder"/><span id="referenceorder"/><span id="REFERENCEORDER"/>ReferenceOrder

The order reference of an entitlement. 

| プロパティ | タスクバーの検索ボックスに | 説明 |
|----------|------|-------------|
| id | string | The ID of the referenced order. |
| lineItemId | string | The ID of the referenced order line item. |
| alternateId | string | The alternate ID of the referenced order line item. |


## <a name="span-idquantitydetailspan-idquantitydetailspan-idquantitydetailquantitydetail"></a><span id="QuantityDetail"/><span id="quantitydetail"/><span id="QUANTITYDETAIL"/>QuantityDetail

Represents the details of an entitlement quantity.

| プロパティ | タスクバーの検索ボックスに | 説明 |
|----------|------|-------------|
| quantity | 整数 | The number of items. |
| status | string | The status of quantity. |


## <a name="span-identitlementtypespan-identitlementtypespan-identitlementtypeentitlementtype"></a><span id="EntitlementType"/><span id="entitlementtype"/><span id="ENTITLEMENTTYPE"/>EntitlementType

> [!IMPORTANT]  
> Deprecated in SDK v1.9

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the type of entitlement.

| Value | 説明 |
|-------|-------------|
| ソフトウェア | Indicates entitlement type related to software. |
| VirtualMachineReservedInstance | Indicates entitlement type related to Azure Reserved Virtual Machine Instances. |


## <a name="span-idartifactspan-idartifactspan-idartifactartifact"></a><span id="Artifact"/><span id="artifact"/><span id="ARTIFACT"/>Artifact

The artifact associated with the entitlement.  

| プロパティ | タスクバーの検索ボックスに | 説明 |
|----------|------|-------------|
| artifactType | string | The type of artifact. (Updated to string from [ArtifactType](#artifacttype) in SDK V1.8) |
| dynamicAttributes | Dictionary&lt;string, object&gt; | Dynamic attributes containing artifacttype specific values. For example when artifactType = "reservedinstance", this will contain "reservationType" = "virtualmachines" or "reservationType" = "sqldatabases" denoting virtual machine reserved instance or Azure SQL reserved instance. (Available starting in SDK v1.9) |


## <a name="span-idartifacttypespan-idartifacttypespan-idartifacttypeartifacttype"></a><span id="ArtifactType"/><span id="artifacttype"/><span id="ARTIFACTTYPE"/>ArtifactType

> [!IMPORTANT]  
> Deprecated in SDK v1.9

An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the type of entitlement artifact.

| Value                          | 説明                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Indicates the artifact aids with retrieval of Azure Reserved Virtual Machine Instances. |


## <a name="span-idreservedinstanceartifactspan-idreservedinstanceartifactspan-idreservedinstanceartifactreservedinstanceartifact"></a><span id="ReservedInstanceArtifact"/><span id="reservedinstanceartifact"/><span id="RESERVEDINSTANCEARTIFACT"/>ReservedInstanceArtifact

The artifact associated with an Azure Reserved Instance entitlement. It inherits from the [Artifact](#artifact) class. 

| プロパティ   | タスクバーの検索ボックスに                           | 説明                                        |
|------------|--------------------------------|----------------------------------------------------|
| link       | [Link](./utility-resources.md#link) | The link to get all associated artifact details.   |
| resourceID | string                         | The ID of the Azure reservation order or resource. |


## <a name="span-idreservedinstanceartifactdetailsspan-idreservedinstanceartifactdetailsspan-idreservedinstanceartifactdetailsreservedinstanceartifactdetails"></a><span id="ReservedInstanceArtifactDetails"/><span id="reservedinstanceartifactdetails"/><span id="RESERVEDINSTANCEARTIFACTDETAILS"/>ReservedInstanceArtifactDetails

Represents the entity returned upon invocation of the Azure Reserved Instance artifact link. 


|   プロパティ   |           タスクバーの検索ボックスに           |                          説明                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     type     |          string          |                     The type of artifact.                     |
| reservations | IEnumerable<Reservation> | Indicates the Azure resource or reservation order identifier. |

## <a name="span-idreservationspan-idreservationspan-idreservationreservation"></a><span id="Reservation"/><span id="reservation"/><span id="RESERVATION"/>Reservation

Represents an individual reservation.

| プロパティ          | タスクバーの検索ボックスに                           | 説明                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | string                         | The ID of the reservation.                                         |
| scopeType         | string                         | The type of scope associated with the virtual machine reservation. |
| displayName       | string                         | The display name of the reservation.                               |
| appliedScopes     | IEnumerable                    | The list of applied scopes associated with the reservation. (Only available when scopeType is not shared.) |
| quantity          | 整数                            | The number of virtual machines in the reservation.                 |
| expiryDateTime    | string in UTC date-time format | The expiry date of the reservation.                                |
| effectiveDateTime | string in UTC date-time format | The effective date of the reservation.                             |
| provisioningState | string                         | The provisioning state of the reservation.                         |


## <a name="span-idvirtualmachinereservedinstanceartifactspan-idvirtualmachinereservedinstanceartifactspan-idvirtualmachinereservedartifactvirtualmachinereservedinstanceartifact"></a><span id="VirtualMachineReservedInstanceArtifact"/><span id="virtualmachinereservedinstanceartifact"/><span id="VIRTUALMACHINERESERVEDARTIFACT"/>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]  
> Deprecated in SDK v1.9

The artifact associated with an Azure Reserved Virtual Machine Instance entitlement. It inherits from the [Artifact](#artifact) class.  

| プロパティ   | タスクバーの検索ボックスに                              | 説明                                        |
|------------|-----------------------------------|----------------------------------------------------|
| link       | [Link](utility-resources.md#link) | The link to get all associated artifact details.   |
| resourceID | string                            | The ID of the Azure reservation order or resource. |


## <a name="span-idvirtualmachinereservedinstanceartifactdetailsspan-idvirtualmachinereservedinstanceartifactdetailsspan-idvirtualmachinereservedartifactdetailsvirtualmachinereservedinstanceartifactdetails"></a><span id="VirtualMachineReservedInstanceArtifactDetails"/><span id="virtualmachinereservedinstanceartifactdetails"/><span id="VIRTUALMACHINERESERVEDARTIFACTDETAILS"/>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]  
> Deprecated in SDK v1.9

Represents the entity returned upon invocation of the Azure Reserved Virtual Machine Instance artifact link.  

| プロパティ                    | タスクバーの検索ボックスに                                                                 | 説明           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| type                        | [ArtifactType](#artifacttype)                                        | The type of artifact. |
| virtualMachineReservations  | IEnumerable<[VirtualMachineReservation](#virtualmachinereservation)> | Indicates the Azure resource or reservation order identifier. |


## <a name="span-idvirtualmachinereservationspan-idvirtualmachinereservationspan-idvirtualmachinereservationvirtualmachinereservation"></a><span id="VirtualMachineReservation"/><span id="virtualmachinereservation"/><span id="VIRTUALMACHINERESERVATION"/>VirtualMachineReservation

> [!IMPORTANT]  
> Deprecated in SDK v1.9

Represents an individual virtual machine reservation.


|     プロパティ      |              タスクバーの検索ボックスに              |                                                説明                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         The ID of the reservation.                                         |
|     scopeType     |             string             |                     The type of scope associated with the virtual machine reservation.                     |
|    displayName    |             string             |                                    The display name of the reservation.                                    |
|   appliedScopes   |      IEnumerable<string>       | The list of applied scopes associated with the reservation. (Only available when scopeType is not shared.) |
|     quantity      |              整数               |                             The number of virtual machines in the reservation.                             |
|  expiryDateTime   | string in UTC date-time format |                                    The expiry date of the reservation.                                     |
| effectiveDateTime | string in UTC date-time format |                                   The effective date of the reservation.                                   |
| provisioningState |             string             |                                 The provisioning state of the reservation.                                 |

