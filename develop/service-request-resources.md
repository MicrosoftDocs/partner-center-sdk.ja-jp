---
title: サービスリクエストリソース
description: パートナーは、パートナーに代わってサービス要求を送信して、Microsoft が提供する中断サービスを報告したり、提供できない他のテクニカルサポートを要求したりすることができます。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 072f9eddaf9d854f1dcc8cc65f7928b6c95700fa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095255"
---
# <a name="service-request-resources"></a>サービスリクエストリソース

**適用対象**

- パートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーは、パートナーに代わってサービス要求を送信して、Microsoft が提供する中断サービスを報告したり、提供できない他のテクニカルサポートを要求したりすることができます。

## <a name="servicerequest"></a>ServiceRequest

パートナーによって提出されたサービス要求を示します。これには、要求の進行状況も含まれます。

| プロパティ         | Type                                                          | 説明                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| タイトル            | string                                                        | サービス要求のタイトル。                                                           |
| 説明      | 文字列                                                        | 説明です。                                                                     |
| 重大度         | string                                                        | 重大度: "unknown"、"critical"、"中"、または "最小"。                       |
| サポートトピック Id   | string                                                        | サポートトピックの id。                                                         |
| サポートトピック名 | string                                                        | サポートトピックの名前。                                                       |
| Id               | string                                                        | サービス要求の id。                                                       |
| 状態           | string                                                        | サービス要求の状態: "none"、"open"、"closed"、または "attention \_ 必要"。 |
| Organization     | [ServiceRequestOrganization](#servicerequestorganization)     | サービス要求が作成される組織。                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | サービスリクエストに関する主要連絡先。                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | サービスリクエストの変更については、"最終更新者" に問い合わせます。                        |
| ProductName      | string                                                        | サービス要求に対応する製品の名前。                     |
| ProductId        | string                                                        | 製品の id。                                                               |
| CreatedDate      | date                                                          | サービス要求の作成日。                                          |
| LastModifiedDate | date                                                          | サービス要求が最後に変更された日付。                                 |
| LastClosedDate   | date                                                          | サービス要求が最後に閉じられた日付。                                   |
| FileLinks        | [FileInfo](utility-resources.md#fileinfo)リソースの配列 | サービス要求に関連するファイルリンクのコレクション。                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | 既存のサービス要求にメモを追加できます。                                  |
| メモ            | [ServiceRequestNotes](#servicerequestnote)の配列           | サービス要求に追加されるメモのコレクション。                                  |
| CountryCode      | string                                                        | サービス要求に対応する国。                                    |
| 属性       | ResourceAttributes                                            | サービス要求に対応するメタデータ属性。                        |

## <a name="servicerequestcontact"></a>ServiceRequestContact

サービスリクエストを作成または変更する連絡先を表します。

| プロパティ     | Type                                                      | 説明                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| Organization | [ServiceRequestOrganization](#servicerequestorganization) | サービス要求が作成される組織。 |
| ContactId    | string                                                    | 連絡先の一意の id。                               |
| LastName     | string                                                    | 連絡先の姓。                          |
| FirstName    | string                                                    | 連絡先の名。                         |
| 電子メール        | string                                                    | 連絡先の電子メール。                              |
| PhoneNumber  | string                                                    | 連絡先の電話番号。                       |

## <a name="servicerequestnote"></a>ServiceRequestNote

サービス要求に添付されているメモを記述します。

| プロパティ      | Type   | 説明                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | string | メモの作成者の名前。         |
| CreatedDate   | date   | メモが作成された日付と時刻。 |
| Text          | string | メモのテキスト。                        |

## <a name="servicerequestorganization"></a>ServiceRequestOrganization

サービス要求が作成される組織について説明します。

| プロパティ    | Type   | 説明                           |
|-------------|--------|---------------------------------------|
| Id          | string | 組織の一意の id。    |
| 名前        | string | 組織の名前です。         |
| PhoneNumber | string | 組織の電話番号。 |

## <a name="supporttopic"></a>SupportTopic

サポートトピックについて説明します。 サービスリクエストは、迅速かつ効率的に処理されるように、サポートトピックを指定します。

| プロパティ    | Type               | 説明                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| 名前        | string             | サポートトピックの名前。                                |
| Description | 文字列             | サポートトピックの説明。                         |
| Id          | string             | サポートトピックの一意の id。                           |
| 属性  | ResourceAttributes | サービス要求に対応するメタデータ属性。 |

