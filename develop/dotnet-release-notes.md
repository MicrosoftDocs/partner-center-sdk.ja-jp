---
title: パートナーセンターの .NET SDK リリースノート
description: パートナーセンター .NET SDK の最新バージョンのリリースノート。
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 082364100a922cd12e93d36c378435c2ef283842
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927309"
---
# <a name="net-sdk-release-notes"></a>.NET SDK のリリースノート

次のリリースノートは、 [Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)の新しいバージョンで使用できます。 [.NET SDK のサンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)については、GitHub を参照してください。 .NET API ブラウザーでは、 [パートナーセンターの .NET api リファレンス](/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) を見つけることができます。

## <a name="version-1162"></a>バージョン1.16.2

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 が一般公開されました。 [GitHub サンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)を更新することもできます。 このバージョンには、次の変更が含まれています。

* 監査レコードに対してサポートされている操作の種類を更新します。 新しく追加されたものは次のとおりです。
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * Delete? 顧客
  * CreateRelatedReferral
  * UpdateRelatedReferral

* サービス要求の作成が非推奨となりました
* サポートトピックは非推奨となりました


## <a name="version-1161"></a>バージョン1.16.1

[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 が一般公開されました。 [GitHub サンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples)を更新することもできます。 このバージョンには、次の変更が含まれています。

既存の Microsoft Partner Center SDK を .NET Framework から .NET Standard 2.0 プラットフォームに移行しました。 これにより、.NET Framework 4.6.1 以降を使用して、SDK と既存のアプリケーションとの互換性が確保されます。 SDK では、.NET Core 2.0 以降がサポートされます。 既存のアプリケーションに移植する前に、 [.net 実装サポート](/dotnet/standard/net-standard) を確認してください。   


## <a name="version-1153"></a>バージョン1.15.3
[Microsoft Partner Center .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 が一般公開されました。 更新された REST Api と [GitHub サンプル](https://github.com/Microsoft/Partner-Center-DotNet-Samples) も利用できます。 このバージョンには、次の変更が含まれています。

* パートナーアグリーメント
  * 間接プロバイダー [が間接リセラーの Microsoft パートナーアグリーメントの状態を確認](verify-indirect-reseller-mpa-status.md)する機能が追加されました。
* 製品
  * 次の2つのインターフェイスは、誤って、Microsoft. ストアの名前空間に配置されました。 次に、これらは、"Microsoft......" という名前空間に配置されています。
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
