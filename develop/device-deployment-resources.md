---
title: デバイス展開のリソース
description: パートナーセンターのデバイスの展開に関連するリソース。
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a464cdad3979c305df16a3bdc9133ce70a7ac688
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094105"
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
| policySettings       | 文字列の配列                             | ポリシー設定は、"none"、"oem プレインストールを削除する \_ \_ "、"oobe \_ ユーザー \_ はローカル管理者ではありません"、" \_ \_ \_ 簡易 \_ 設定をスキップする"、"oem 登録をスキップする"、" \_ \_ eula をスキップする" \_ です。    |
| createdDate          | UTC 日時形式の文字列               | ポリシーが作成された日付と時刻。                                            |
| lastModifiedDate     | UTC 日時形式の文字列               | ポリシーが最後に変更された日付と時刻。                                      |
| 属性           | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。                                            |

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
| 属性          | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                                 |

## <a name="batchuploaddetails"></a>BatchUploadDetails

**Batchuploaddetails**は、デバイスの一覧にある各デバイスに関する情報のデバイスバッチアップロードの状態を示します。

| プロパティ        | Type     | 説明                                                                  |
|-----------------|----------|------------------------------------------------------------------------------|
| batchTrackingId | string   | アップロードされたデバイスのバッチに関連付けられている GUID 形式の文字列。 |
| 状態          | string   | バッチアップロードの状態: "不明"、"キューに登録済み"、"処理中"、"完了"、 \_ " \_ エラーが発生しました"。 |
| startedTime     | UTC 日時形式の文字列 | バッチのアップロード処理が開始された日付と時刻。   |
| completedTime   | UTC 日時形式の文字列  | バッチのアップロード処理が完了した日付と時刻。   |
| デバイスの状態   | [Deviceuploaddetails](#deviceuploaddetails)リソースの配列 | 各デバイス情報のアップロードの状態を示すオブジェクトの配列です。 |
| 属性      | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。  |

## <a name="deviceuploaddetails"></a>DeviceUploadDetails

**Deviceuploaddetails**は、デバイスに関する情報のアップロードの状態を示します。

| プロパティ         | Type                    | 説明                                 |
|------------------|-------------------------|---------------------------------------------|
| deviceId         | string                  | デバイスに関連付けられている GUID 形式の文字列。 |
| serialNumber     | string                  | デバイスに一意に関連付けられているシリアル番号。 |
| productKey       | string                  | デバイスに一意に関連付けられているプロダクトキー。 |
| 状態           | string                  | デバイス情報のアップロードの状態: "進行中"、"完了"、" \_ \_ エラーが発生しました"。 |
| errorCode        | string                  | デバイスのアップロードに失敗した場合に返される HTTP 状態エラーコード。 |
| errorDescription | string                  | デバイスのアップロードに失敗した場合の HTTP エラーの説明。 |
| 属性       | [ResourceAttributes](utility-resources.md#resourceattributes) | メタデータ属性。   |

## <a name="devicebatch"></a>DeviceBatch

**Devicebatch**は、デバイスのコレクションを表します。

| プロパティ     | Type                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| id           | string                                                         | デバイスのバッチに関連付けられている GUID 形式の文字列。 |
| createdBy    | string                                                         | コレクションを作成したテナントの名前。                   |
| creationDate | UTC 日時形式の文字列                                 | コレクションが作成されたデータと時刻。                    |
| deviceCount  | number                                                         | コレクション内のデバイスの数。                              |
| デバイスのリンク  | [リンク](utility-resources.md#link)                              | このバッチに含まれるデバイスへのリンク。                        |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |

## <a name="devicebatchcreationrequest"></a>Devicebatchの要求

**Devicebatchの要求**は、デバイスのバッチを作成してデバイスを設定するために必要な情報を提供します。

| プロパティ     | Type                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| batchId      | string                                                         | デバイスのバッチに関連付けられている GUID 形式の文字列。 |
| devices      | [デバイス](#device)オブジェクトの配列                             | 各オブジェクトはデバイスを指定します。 デバイスを識別するための次のようなフィールドの組み合わせが許可されます: ハードウェアハッシュ + productKey、ハードウェアハッシュ + シリアル、ハードウェアハッシュ + productKey + シリアル数、ハードウェアハッシュのみ、productKey のみ、シリアル + oemManufacturerName + modelName。 |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |

## <a name="devicepolicyupdaterequest"></a>DevicePolicyUpdateRequest

**Devicepolicyupdaterequest** 、ポリシーを使用してデバイスの一覧を更新するために必要な情報を提供します。

| プロパティ     | Type                                                           | 説明                                                           |
|--------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| devices      | [デバイス](#device)オブジェクトの配列                             | 各オブジェクトはデバイスを指定します。 次のプロパティが必要です: Id、ポリシー。 |
| 属性   | [ResourceAttributes](utility-resources.md#resourceattributes)  | メタデータ属性。                                              |
