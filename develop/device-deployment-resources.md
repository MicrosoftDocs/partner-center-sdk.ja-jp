---
title: デバイス展開のリソース
description: パートナーセンターのデバイスの展開に関連するリソース。
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5aaf4c9dc80b681c274c68af3439654e27e27be7
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81664616"
---
# <a name="device-deployment-resources"></a>デバイス展開のリソース

**適用対象:**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター

次のリソースは、デバイスの展開に関連しています。

## <a name="configurationpolicy"></a>ConfigurationPolicy

**Configurationpolicy**は、構成ポリシーに関する情報を提供します。

| プロパティ             | Type                                                           | 説明                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | string                                       | ポリシーを識別する GUID 形式の文字列。                                  |
| name                 | string                                       | ポリシーのフレンドリ名。                                                    |
| category             | string                                       | カテゴリです。                                                                        |
| description          | string                                       | ポリシーの説明。                                                              |
| devicesAssignedCount | number                                       | このポリシーに割り当てられているデバイスの数。                                       |
| policySettings       | 文字列の配列                             | ポリシー設定は、"none"、"oem\_\_プレインストールを削除する"、\_"\_oobe\_ユーザー\_はローカル管理者で\_は\_ありません"、\_"\_簡易設定をスキップする\_"、"oem 登録をスキップする"、"eula をスキップする" です。    |
| createdDate          | UTC 日時形式の文字列               | ポリシーが作成された日付と時刻。                                            |
| lastModifiedDate     | UTC 日時形式の文字列               | ポリシーが最後に変更された日付と時刻。                                      |
| attributes           | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                            |

## <a name="device"></a>Device

**デバイスに**関する情報を提供します。

| プロパティ            | Type                                                           | 説明                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | string                                                         | デバイスを識別する GUID 形式の文字列。                      |
| serialNumber        | string                                                         | デバイスに一意に関連付けられているシリアル番号。                   |
| productKey          | string                                                         | デバイスに一意に関連付けられているプロダクトキー。                     |
| ハードウェアハッシュ        | string                                                         | デバイスに一意に関連付けられたハードウェアハッシュ。                   |
| modelName           | string                                                         | デバイスに関連付けられているモデル名。                               |
| oemManufacturerName | string                                                         | デバイスに関連付けられている OEM 製造元の名前。             |
| policies            | オブジェクトの配列                                               | デバイスに割り当てられているポリシーの一覧。                             |
| uploadedDate        | UTC 日時形式の文字列                                 | デバイスの詳細がアップロードされた日付と時刻。                      |
| allowedOperations   | 文字列の配列                                               | デバイスを GET、PATCH、DELETE として同期することが許可されている HTTP メソッドの一覧。 |
| attributes          | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**Batchuploaddetails**は、デバイスの一覧にある各デバイスに関する情報のデバイスバッチアップロードの状態を示します。

| プロパティ        | Type     | 説明                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | string   | アップロードされたデバイスのバッチに関連付けられている GUID 形式の文字列。 |
| status          | string   | バッチアップロードの状態: "不明"、"キューに登録済み"、"処理中"、"完了"、\_"\_エラーが発生しました"。 |
| startedTime     | UTC 日時形式の文字列 | バッチのアップロード処理が開始された日付と時刻。   |
| completedTime   | UTC 日時形式の文字列  | バッチのアップロード処理が完了した日付と時刻。   |
| デバイスの状態   | [Deviceuploaddetails](#deviceuploaddetails)リソースの配列 | 各デバイス情報のアップロードの状態を示すオブジェクトの配列です。 |
| attributes      | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**Deviceuploaddetails**は、デバイスに関する情報のアップロードの状態を示します。

| プロパティ         | Type                    | 説明                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | string                  | デバイスに関連付けられている GUID 形式の文字列。 |
| serialNumber     | string                  | デバイスに一意に関連付けられているシリアル番号。 |
| productKey       | string                  | デバイスに一意に関連付けられているプロダクトキー。 |
| status           | string                  | デバイス情報のアップロードの状態: "進行中"、"完了"、"エラーが発生\_し\_ました"。 |
| errorCode        | string                  | デバイスのアップロードに失敗した場合に返される HTTP 状態エラーコード。 |
| errorDescription | string                  | デバイスのアップロードに失敗した場合の HTTP エラーの説明。 |
| attributes       | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。   |

## <a name="devicebatch"></a>DeviceBatch

**Devicebatch**は、デバイスのコレクションを表します。

| プロパティ     | Type                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | string                                                         | デバイスのバッチに関連付けられている GUID 形式の文字列。 |
| createdBy    | string                                                         | コレクションを作成したテナントの名前。                   |
| creationDate | UTC 日時形式の文字列                                 | コレクションが作成されたデータと時刻。                    |
| deviceCount  | number                                                         | コレクション内のデバイスの数。                              |
| デバイスのリンク  | [リンク](utility-resources.md#link)                              | このバッチに含まれるデバイスへのリンク。                        |
| attributes   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |

## <a name="devicebatchcreationrequest"></a>Devicebatchの要求

**Devicebatchの要求**は、デバイスのバッチを作成してデバイスを設定するために必要な情報を提供します。

| プロパティ     | Type                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | string                                                         | デバイスのバッチに関連付けられている GUID 形式の文字列。 |
| devices      | [デバイス](#device)オブジェクトの配列                             | 各オブジェクトはデバイスを指定します。 デバイスを識別するための次のようなフィールドの組み合わせが許可されます: ハードウェアハッシュ + productKey、ハードウェアハッシュ + シリアル、ハードウェアハッシュ + productKey + シリアル数、ハードウェアハッシュのみ、productKey のみ、シリアル + oemManufacturerName + modelName。 |
| attributes   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**Devicepolicyupdaterequest** 、ポリシーを使用してデバイスの一覧を更新するために必要な情報を提供します。

| プロパティ     | Type                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | [デバイス](#device)オブジェクトの配列                             | 各オブジェクトはデバイスを指定します。 次のプロパティが必要です: Id、ポリシー。 |
| attributes   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |
