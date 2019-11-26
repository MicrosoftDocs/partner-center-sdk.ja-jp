---
title: Device deployment resources
description: Resources related to Partner Center device deployment.
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1aecf66907d8e39ae3015ba7a7735942555d1d1c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489952"
---
# <a name="device-deployment-resources"></a>Device deployment resources

適用対象:

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

The following resources are related to device deployment.

## <a name="configurationpolicy"></a>ConfigurationPolicy

**ConfigurationPolicy** provides information about a configuration policy.

| プロパティ             | タスクバーの検索ボックスに                                                           | 説明                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | string                                       | A GUID-formatted string that identifies the policy.                                  |
| 名前                 | string                                       | The friendly name for the policy.                                                    |
| category             | string                                       | The category.                                                                        |
| 説明          | string                                       | The policy description.                                                              |
| devicesAssignedCount | number                                       | The number of devices assigned to this policy.                                       |
| policySettings       | 文字列の配列                             | The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip\_oem\_registration", "skip\_eula".    |
| createdDate          | string in UTC date-time format               | The date and time the policy was created.                                            |
| lastModifiedDate     | string in UTC date-time format               | The date and time the policy was last modified.                                      |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                            |

## <a name="device"></a>デバイス

**Device** provides information about a device.

| プロパティ            | タスクバーの検索ボックスに                                                           | 説明                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | string                                                         | A GUID-formatted string that identifies the device.                      |
| serialNumber        | string                                                         | The serial number uniquely associated with the device.                   |
| productKey          | string                                                         | The product key uniquely associated with the device.                     |
| hardwareHash        | string                                                         | The hardware hash uniquely associated with the device.                   |
| modelName           | string                                                         | The model name associated with the device.                               |
| oemManufacturerName | string                                                         | The name of the OEM manufacturer associated with the device.             |
| ポリシー            | オブジェクトの配列                                               | The list of policies assigned to the device.                             |
| uploadedDate        | string in UTC date-time format                                 | The date and time the device details were uploaded.                      |
| allowedOperations   | 文字列の配列                                               | The list of HTTP methods allowed on a device sync as GET, PATCH, DELETE. |
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**BatchUploadDetails** describes the status of a device batch upload of information about each device in a list of devices.

| プロパティ        | タスクバーの検索ボックスに     | 説明                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | string   | A GUID-formatted string that is associated with the batch of devices uploaded. |
| status          | string   | The status of the batch upload: "unknown","queued","processing","finished","finished\_with\_errors". |
| startedTime     | string in UTC date-time format | The date and time that the batch upload process started.   |
| completedTime   | string in UTC date-time format  | The date and time that the batch upload process completed.   |
| devicesStatus   | array of [DeviceUploadDetails](#deviceuploaddetails) resources | An array of objects that specify the status of each device information upload. |
| 属性      | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**DeviceUploadDetails** describes the status of an upload of information about a device.

| プロパティ         | タスクバーの検索ボックスに                    | 説明                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | string                  | A GUID-formatted string that is associated with the device. |
| serialNumber     | string                  | The serial number uniquely associated with the device. |
| productKey       | string                  | The product key uniquely associated with the device. |
| status           | string                  | The status of the device information upload: "in-progress", "finished", "finished\_with\_errors". |
| errorCode        | string                  | The HTTP status error code returned if the device upload fails. |
| errorDescription | string                  | The HTTP error description if the device upload fails. |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.   |

## <a name="devicebatch"></a>DeviceBatch

**DeviceBatch** represents a collection of devices.

| プロパティ     | タスクバーの検索ボックスに                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | string                                                         | A GUID-formatted string that is associated with the batch of devices. |
| createdBy    | string                                                         | The name of the tenant that created the collection.                   |
| creationDate | string in UTC date-time format                                 | The data and time that the collection was created.                    |
| deviceCount  | number                                                         | The number of devices in the collection.                              |
| devicesLink  | [Link](utility-resources.md#link)                              | A link to the devices contained in this batch.                        |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## <a name="devicebatchcreationrequest"></a>DeviceBatchCreationRequest

**DeviceBatchCreationRequest** provides the information required to create a device batch and populates it with devices.

| プロパティ     | タスクバーの検索ボックスに                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | string                                                         | A GUID-formatted string that is associated with the batch of devices. |
| devices      | array of [Device](#device) objects                             | Each object specifies a device. The following combinations of fields for identifying a device are accepted: hardwareHash + productKey, hardwareHash + serialNumber, hardwareHash + productKey + serialNumber, hardwareHash only, productKey only, serialNumber + oemManufacturerName + modelName. |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**DevicePolicyUpdateRequest** provides the information required to update a list of devices with a policy.

| プロパティ     | タスクバーの検索ボックスに                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | array of [Device](#device) objects                             | Each object specifies a device. The following properties are required: Id, Policies. |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | The metadata attributes.                                              |
