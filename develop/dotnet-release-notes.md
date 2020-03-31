---
title: パートナーセンターの .NET SDK リリースノート
description: パートナーセンター .NET SDK の最新バージョンのリリースノート。
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c924f691f9d0315d58cf53630776d532ebf8c089
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415679"
---
# <a name="net-sdk-release-notes"></a>.NET SDK のリリースノート

次のリリースノートは、 [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)の新しいバージョンで使用できます。 [.NET SDK のサンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)については、GitHub を参照してください。 .NET API ブラウザーでは、[パートナーセンターの .NET api リファレンス](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest)を見つけることができます。

## <a name="version-1152"></a>バージョン1.15.2

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v 1.15.2 が一般公開されました。 更新された REST Api と[GitHub サンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)も利用できます。 このバージョンには、次の変更が含まれています。

* パートナーアグリーメント
  * 間接プロバイダー[が間接リセラーの Microsoft パートナーアグリーメントの状態を確認](verify-indirect-reseller-mpa-status.md)する機能が追加されました。
* Products
  * 次の2つのインターフェイスは、誤って、Microsoft. ストアの名前空間に配置されました。 次に、これらは、"Microsoft......" という名前空間に配置されています。
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
