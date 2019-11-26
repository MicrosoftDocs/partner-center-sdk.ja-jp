---
title: Audit operations
description: Get a record of Partner Center activity using auditing operations.
ms.assetid: C6337A08-6009-4F12-A7A3-B1CA1AE016A1
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 34da264b465a7b9634c18d4355d3b136dfcd0761
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489162"
---
# <a name="audit-operations"></a>Audit operations

The Partner Center APIs provide auditing features so you can get a record of Partner Center activity.

You can retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date. Note, however, that for performance reasons activity log data availability is limited to the previous 90 days. Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.

## <a name="retrieve-audit-records"></a>Retrieve audit records

Get detailed historical audit records of operations performed by a partner user or application:

- [パートナー センター アクティビティのレコードを取得する](get-a-record-of-partner-center-activity-by-user.md)
- [Auditing resources](auditing-resources.md)