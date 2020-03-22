---
title: デバイス展開のリソース
description: パートナーセンターのデバイスの展開に関連するリソース。
ms.assetid: DF237297-7956-42EE-8F09-4304F6EFBF26
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 1aecf66907d8e39ae3015ba7a7735942555d1d1c
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083159"
---
# <a name="device-deployment-resources"></a>デバイス展開のリソース

適用対象

- Partner Center
- Microsoft Cloud ドイツのパートナー センター

次のリソースは、デバイスの展開に関連しています。

## <a name="configurationpolicy"></a>ConfigurationPolicy

**Configurationpolicy**は、構成ポリシーに関する情報を提供します。

| プロパティ             | 種類                                                           | 説明                                                        |
|----------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| id                   | string                                       | ポリシーを識別する GUID 形式の文字列。                                  |
| name                 | string                                       | ポリシーのフレンドリ名。                                                    |
| category             | string                                       | カテゴリ。                                                                        |
| description          | string                                       | ポリシーの説明。                                                              |
| devicesAssignedCount | number                                       | このポリシーに割り当てられているデバイスの数。                                       |
| policySettings       | 文字列の配列                             | ポリシー設定は、"none"、"remove\_oem\_プレインストール"、"oobe\_ユーザー\_\_ローカル\_管理者"、"\_の高速\_設定をスキップ"、"\_oem\_の登録をスキップ"、"\_eula をスキップ" です。    |
| createdDate          | UTC 日時形式の文字列               | ポリシーが作成された日付と時刻。                                            |
| lastModifiedDate     | UTC 日時形式の文字列               | ポリシーが最後に変更された日付と時刻。                                      |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                            |

## <a name="device"></a>デバイス

**デバイスに**関する情報を提供します。

| プロパティ            | 種類                                                           | 説明                                                              |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| id                  | string                                                         | デバイスを識別する GUID 形式の文字列。                      |
| serialNumber        | string                                                         | デバイスに一意に関連付けられているシリアル番号。                   |
| productKey          | string                                                         | デバイスに一意に関連付けられているプロダクトキー。                     |
| ハードウェアハッシュ        | string                                                         | デバイスに一意に関連付けられたハードウェアハッシュ。                   |
| modelName           | string                                                         | デバイスに関連付けられているモデル名。                               |
| oemManufacturerName | string                                                         | デバイスに関連付けられている OEM 製造元の名前。             |
| ポリシー            | オブジェクトの配列                                               | デバイスに割り当てられているポリシーの一覧。                             |
| uploadedDate        | UTC 日時形式の文字列                                 | デバイスの詳細がアップロードされた日付と時刻。                      |
| allowedOperations   | 文字列の配列                                               | デバイスを GET、PATCH、DELETE として同期することが許可されている HTTP メソッドの一覧。 |
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**Batchuploaddetails**は、デバイスの一覧にある各デバイスに関する情報のデバイスバッチアップロードの状態を示します。

| プロパティ        | 種類     | 説明                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | string   | アップロードされたデバイスのバッチに関連付けられている GUID 形式の文字列。 |
| 状態          | string   | バッチアップロードの状態: "不明"、"キューに登録済み"、"処理中"、"完了"、"完了した\_\_エラー"。 |
| startedTime     | UTC 日時形式の文字列 | バッチのアップロード処理が開始された日付と時刻。   |
| completedTime   | UTC 日時形式の文字列  | バッチのアップロード処理が完了した日付と時刻。   |
| デバイスの状態   | [Deviceuploaddetails](#deviceuploaddetails)リソースの配列 | 各デバイス情報のアップロードの状態を示すオブジェクトの配列です。 |
| 属性      | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**Deviceuploaddetails**は、デバイスに関する情報のアップロードの状態を示します。

| プロパティ         | 種類                    | 説明                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | string                  | デバイスに関連付けられている GUID 形式の文字列。 |
| serialNumber     | string                  | デバイスに一意に関連付けられているシリアル番号。 |
| productKey       | string                  | デバイスに一意に関連付けられているプロダクトキー。 |
| 状態           | string                  | デバイス情報のアップロードの状態: "進行中"、"完了"、"完了した\_と\_エラー"。 |
| errorCode        | string                  | デバイスのアップロードに失敗した場合に返される HTTP 状態エラーコード。 |
| errorDescription | string                  | デバイスのアップロードに失敗した場合の HTTP エラーの説明。 |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。   |

## <a name="devicebatch"></a>DeviceBatch

**Devicebatch**は、デバイスのコレクションを表します。

| プロパティ     | 種類                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | string                                                         | デバイスのバッチに関連付けられている GUID 形式の文字列。 |
| createdBy    | string                                                         | コレクションを作成したテナントの名前。                   |
| creationDate | UTC 日時形式の文字列                                 | コレクションが作成されたデータと時刻。                    |
| deviceCount  | number                                                         | コレクション内のデバイスの数。                              |
| デバイスのリンク  | [Link](utility-resources.md#link)                              | このバッチに含まれるデバイスへのリンク。                        |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |

## <a name="devicebatchcreationrequest"></a>Devicebatchの要求

**Devicebatchの要求**は、デバイスのバッチを作成してデバイスを設定するために必要な情報を提供します。

| プロパティ     | 種類                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | string                                                         | デバイスのバッチに関連付けられている GUID 形式の文字列。 |
| devices      | [デバイス](#device)オブジェクトの配列                             | 各オブジェクトはデバイスを指定します。 デバイスを識別するための次のフィールドの組み合わせが受け入れられます: ハードウェアハッシュ + productKey、ハードウェアハッシュ + シリアル、ハードウェアハッシュ + productKey + シリアル数、ハードウェアハッシュのみ、productKey のみ、シリアル + oemManufacturerName +modelName. |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**Devicepolicyupdaterequest** 、ポリシーを使用してデバイスの一覧を更新するために必要な情報を提供します。

| プロパティ     | 種類                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | [デバイス](#device)オブジェクトの配列                             | 各オブジェクトはデバイスを指定します。 次のプロパティが必要です: Id、ポリシー。 |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |
