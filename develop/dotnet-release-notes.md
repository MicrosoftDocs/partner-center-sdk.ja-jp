---
title: パートナーセンターの .NET SDK リリースノート
description: パートナーセンター .NET SDK の最新バージョンのリリースノート。
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fe63c5bf5a7d3114f8914d432a64099e009698e6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098407"
---
# <a name="net-sdk-release-notes"></a>.NET SDK のリリースノート

次のリリースノートは、 [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)の新しいバージョンで使用できます。 [.NET SDK のサンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)については、GitHub を参照してください。 .NET API ブラウザーでは、[パートナーセンターの .NET api リファレンス](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest)を見つけることができます。

## <a name="version-1153"></a>バージョン1.15.3

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v 1.15.3 が一般公開されました。 更新された REST Api と[GitHub サンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)も利用できます。 このバージョンには、次の変更が含まれています。

* パートナーアグリーメント
  * 間接プロバイダー[が間接リセラーの Microsoft パートナーアグリーメントの状態を確認](verify-indirect-reseller-mpa-status.md)する機能が追加されました。
* 製品
  * 次の2つのインターフェイスは、誤って、Microsoft. ストアの名前空間に配置されました。 次に、これらは、"Microsoft......" という名前空間に配置されています。
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
