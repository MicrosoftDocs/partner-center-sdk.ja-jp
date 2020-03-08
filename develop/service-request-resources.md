---
title: サービスリクエストリソース
description: パートナーは、パートナーに代わってサービス要求を送信して、Microsoft が提供する中断サービスを報告したり、提供できない他のテクニカルサポートを要求したりすることができます。
ms.assetid: E9FBF7D8-A7E8-4DC6-B370-8339B9EE16B7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e1fab576e69242a50549efc719f98eafad1ad9de
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78899929"
---
# <a name="service-request-resources"></a>サービスリクエストリソース


**適用対象**

- Partner Center
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーは、パートナーに代わってサービス要求を送信して、Microsoft が提供する中断サービスを報告したり、提供できない他のテクニカルサポートを要求したりすることができます。

## <a name="span-idservicerequestspan-idservicerequestspan-idservicerequestservicerequest"></a><span id="ServiceRequest"/><span id="servicerequest"/><span id="SERVICEREQUEST"/>ServiceRequest


パートナーによって提出されたサービス要求を示します。これには、要求の進行状況も含まれます。

| プロパティ         | 種類                                                          | 説明                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| タイトル            | string                                                        | サービス要求のタイトル。                                                           |
| 説明      | string                                                        | 説明。                                                                     |
| Severity         | string                                                        | 重大度: "unknown"、"critical"、"中"、または "最小"。                       |
| サポートトピック Id   | string                                                        | サポートトピックの id。                                                         |
| サポートトピック名 | string                                                        | サポートトピックの名前。                                                       |
| Id               | string                                                        | サービス要求の id。                                                       |
| 状態           | string                                                        | サービス要求の状態: "none"、"open"、"closed"、または "attention\_が必要"。 |
| 組織     | [ServiceRequestOrganization](#servicerequestorganization)     | サービス要求が作成される組織。                               |
| primaryContact   | [ServiceRequestContact](#servicerequestcontact)               | サービスリクエストに関する主要連絡先。                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | サービスリクエストの変更については、"最終更新者" に問い合わせます。                        |
| ProductName      | string                                                        | サービス要求に対応する製品の名前。                     |
| ProductId        | string                                                        | 製品の id。                                                               |
| CreatedDate      | date                                                          | サービス要求の作成日。                                          |
| LastModifiedDate | date                                                          | サービス要求が最後に変更された日付。                                 |
| LastClosedDate   | date                                                          | サービス要求が最後に閉じられた日付。                                   |
| FileLinks        | [FileInfo](utility-resources.md#fileinfo)リソースの配列 | サービス要求に関連するファイルリンクのコレクション。                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | 既存のサービス要求にメモを追加できます。                                  |
| 説明            | [ServiceRequestNotes](#servicerequestnote)の配列           | サービス要求に追加されるメモのコレクション。                                  |
| CountryCode      | string                                                        | サービス要求に対応する国。                                    |
| 属性       | ResourceAttributes                                            | サービス要求に対応するメタデータ属性。                        |

 

## <a name="span-idservicerequestcontactspan-idservicerequestcontactspan-idservicerequestcontactservicerequestcontact"></a><span id="ServiceRequestContact"/><span id="servicerequestcontact"/><span id="SERVICEREQUESTCONTACT"/>ServiceRequestContact


サービスリクエストを作成または変更する連絡先を表します。

| プロパティ     | 種類                                                      | 説明                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| 組織 | [ServiceRequestOrganization](#servicerequestorganization) | サービス要求が作成される組織。 |
| ContactId    | string                                                    | 連絡先の一意の id。                               |
| LastName     | string                                                    | 連絡先の姓。                          |
| FirstName    | string                                                    | 連絡先の名。                         |
| Email        | string                                                    | 連絡先の電子メール。                              |
| PhoneNumber  | string                                                    | 連絡先の電話番号。                       |

 

## <a name="span-idservicerequestnotespan-idservicerequestnotespan-idservicerequestnoteservicerequestnote"></a><span id="ServiceRequestNote"/><span id="servicerequestnote"/><span id="SERVICEREQUESTNOTE"/>ServiceRequestNote


サービス要求に添付されているメモを記述します。

| プロパティ      | 種類   | 説明                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | string | メモの作成者の名前。         |
| CreatedDate   | date   | メモが作成された日付と時刻。 |
| Text          | string | メモのテキスト。                        |

 

## <a name="span-idservicerequestorganizationspan-idservicerequestorganizationspan-idservicerequestorganizationservicerequestorganization"></a><span id="ServiceRequestOrganization"/><span id="servicerequestorganization"/><span id="SERVICEREQUESTORGANIZATION"/>ServiceRequestOrganization


サービス要求が作成される組織について説明します。

| プロパティ    | 種類   | 説明                           |
|-------------|--------|---------------------------------------|
| Id          | string | 組織の一意の id。    |
| Name        | string | 組織の名前。         |
| PhoneNumber | string | 組織の電話番号。 |

 

## <a name="span-idsupporttopicspan-idsupporttopicspan-idsupporttopicsupporttopic"></a><span id="SupportTopic"/><span id="supporttopic"/><span id="SUPPORTTOPIC"/>SupportTopic


サポートトピックについて説明します。 サービスリクエストは、迅速かつ効率的に処理されるように、サポートトピックを指定します。

| プロパティ    | 種類               | 説明                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| Name        | string             | サポートトピックの名前。                                |
| 説明 | string             | サポートトピックの説明。                         |
| Id          | string             | サポートトピックの一意の id。                           |
| 属性  | ResourceAttributes | サービス要求に対応するメタデータ属性。 |

 

 

 




