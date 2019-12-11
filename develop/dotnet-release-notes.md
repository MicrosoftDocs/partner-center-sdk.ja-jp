---
title: パートナーセンターの .NET SDK リリースノート
description: パートナーセンター .NET SDK の最新バージョンのリリースノート。
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2b98c6ef23b08947a7dec219ba40b7e19a3e5026
ms.sourcegitcommit: 7e5e3590931010eb0e0fef3e7f6d5d7d084a69ba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995619"
---
# <a name="net-sdk-release-notes"></a>.NET SDK のリリースノート

次のリリースノートは、 [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)の新しいバージョンで使用できます。 [.NET SDK のサンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)については、GitHub を参照してください。 .NET API ブラウザーでは、[パートナーセンターの .NET api リファレンス](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest)を見つけることができます。

## <a name="version-1152"></a>バージョン1.15.2

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v 1.15.2 が一般公開されました。 更新された REST Api と[GitHub サンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)も利用できます。 このバージョンには、次の変更が含まれています。

* パートナーアグリーメント
  * 間接プロバイダー[が間接リセラーの Microsoft パートナーアグリーメントの状態を確認](verify-indirect-reseller-mpa-status.md)する機能が追加されました。
* Products (製品)
  * 次の2つのインターフェイスは、誤って、Microsoft. ストアの名前空間に配置されました。 次に、これらは、"Microsoft......" という名前空間に配置されています。
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
