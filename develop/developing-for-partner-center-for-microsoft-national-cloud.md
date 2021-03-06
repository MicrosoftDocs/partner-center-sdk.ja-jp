---
title: Microsoft National クラウドのパートナーセンター向けの開発
description: パートナーセンター向けのパートナーセンター向けの開発時のパートナーセンターの SDK の違い。
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7882846de0c591b21fe73345f560613f535d1788
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "91007700"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>Microsoft National クラウドのパートナーセンター向けの開発

**適用対象:**

- 21Vianet が運営するパートナー センター
- Microsoft Cloud ドイツのパートナー センター
- 米国政府機関向け Microsoft Cloud のパートナー センター

パートナーセンターには、SDK ドキュメントの1つのセットがあります。 ただし、一部の機能は、Microsoft National クラウドのパートナーセンターのバージョンでは利用できない場合があります。

開発者は、次のバージョンのパートナーセンターの SDK に対する変更を考慮する必要があります。

- [21Vianet が運営するパートナー センター](#partner-center-operated-by-21vianet)
- [Microsoft Cloud ドイツのパートナー センター](#partner-center-for-microsoft-cloud-germany)
- [Microsoft Cloud for US Government のパートナー センター](#partner-center-for-microsoft-cloud-for-us-government)

各パートナーセンターの SDK 記事には、該当するパートナーセンターのバージョンが一覧表示されます。 各管理リファレンス記事には、「 **要件** 」セクションで該当するパートナーセンターのバージョンも記載されています。

## <a name="partner-center-operated-by-21vianet"></a>21Vianet が運営するパートナー センター

21Vianet が運営するパートナー *センター* とパートナー *センター* 間のパートナーの違いは、次のとおりです。

- 顧客ユーザーまたは完全なパートナーユーザーのパスワードをプログラムによってリセットすることはできません。

- Azure に対するサブスクリプションは使用できません。

- 顧客のユーザーのライセンスを管理することはできません。 代わりに、顧客は Office 365 管理センターを使用してライセンスを管理する必要があります。

- すべてのサポートリクエストは、21Vianet が運営するパートナーセンターを通じて管理されます。 サービスリクエストとサービスの更新は適用されません。

## <a name="partner-center-for-microsoft-cloud-germany"></a>Microsoft Cloud ドイツのパートナー センター

> [!IMPORTANT]
> お客様のニーズの変化に基づいて、ドイツのクラウド戦略は、グローバルクラウドサービスと一貫性のあるドイツの新しいクラウドリージョンの配信に焦点を当てます。 この焦点に合わせて、今後 Microsoft では、現在利用可能な Microsoft Cloud ドイツからの新しい顧客を受け入れたり、新しいサービスを展開することはありません。 既存のお客様は、現在提供されている現在のクラウドサービスを引き続き使用できます。このサービスは、必要なセキュリティ更新プログラムによって維持されます。
>
> 今後、新しい顧客は、現在利用可能なヨーロッパの地域を利用するか、または利用可能になった時点でドイツの新しい地域を利用することができます。 詳細については、[Microsoft によるドイツの新しいデータセンターからのクラウド サービスの提供](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/)に関するページを参照してください。

*Microsoft Cloud ドイツの*パートナー*センター*とパートナーセンター間のパートナーの違いは次のとおりです。

- パートナーは、顧客の組織のユーザーを作成したり、ロールを割り当てたりすることはできません。
  - パートナーはフィールドを読み取ることができますが、作成または更新することはできません。
  - パートナーは、Office 365 管理センターまたは Azure portal を使用して、顧客のユーザーを手動で作成または更新する必要があります。 [Azure Active Directory のドキュメント](/azure/active-directory/)を参照してください。

- Microsoft Cloud ドイツポータルまたは Api のパートナーセンターを使用して、顧客のユーザーのライセンスを管理することはできません。 代わりに、Office 365 管理センターまたは Azure Active (近日対応予定) のライセンス管理を使用してライセンスを管理する必要があります。
  - (省略可能) Azure AD Graph API を使用できます。 「 [ユーザーにライセンスを割り当てる」を](/graph/api/user-assignlicense)参照してください。 Microsoft Cloud ドイツのパートナーセンターでは、ではなく、グラフエンドポイントを使用してください `https://graph.cloudapi.de` `https://graph.windows.net` 。

- 顧客ユーザーまたは完全なパートナーユーザーのパスワードをプログラムによってリセットすることはできません。 Office 365 管理センターまたは Azure portal を使用します。 「 [Azure Active Directory でのユーザーのパスワードのリセット](/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal)」を参照してください。 手順1では、Microsoft Cloud ドイツの Azure portal にサインインする必要があります。

- 開発者は、パートナーセンターのアプリにパートナーセンターの API/SDK 機能を統合するために、アプリ ID を手動で登録する必要があります (Microsoft Cloud ドイツ)。 詳細については、「 [Microsoft National Cloud のパートナーセンターのアプリの詳細を登録](create-apps-for-partner-center-for-microsoft-national-clouds.md)する」を参照してください。

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>米国政府機関向け Microsoft Cloud のパートナー センター

パートナー *センター* とパートナーセンター間のパートナーが *米国政府向け Microsoft Cloud の* 違いは次のとおりです。

- Office 365 サブスクリプションは、現在、米国政府の Microsoft Cloud のパートナーセンターではご利用いただけません。

- 米国政府向けの Microsoft Cloud をサポートしている既存のパートナーは、パートナーセンターで米国政府向け Microsoft Cloud の新しいアカウントを作成する必要があります。

- 米国政府機関のお客様の Microsoft Cloud は、1つのパートナーを使用する必要があります。
  - 米国政府向けのシナリオにおいて Microsoft Cloud 内の既存の顧客とのマルチチャネルおよびマルチパートナーおよび要求の関係は適用されません。 Office 365 は現在使用できないため、この制限があります。

- パートナーは、顧客の組織のユーザーを作成したり、ロールを割り当てたりすることはできません。
  - パートナーはフィールドを読み取ることができますが、作成または更新することはできません。 パートナーは、Azure portal で顧客のユーザーを手動で作成または更新する必要があります。 [Azure Active Directory のドキュメント](/azure/active-directory/)を参照してください。

- 顧客ユーザーまたは完全なパートナーユーザーのパスワードをプログラムによってリセットすることはできません。 Azure portal を使用します。 「 [Azure Active Directory でのユーザーのパスワードのリセット](/azure/active-directory/active-directory-users-reset-password-azure-portal)」を参照してください。 手順 1. では、米国政府向け Microsoft Cloud の Azure portal にサインインする必要があります。

- 米国政府向け Microsoft Cloud のパートナーセンターの REST エンドポイントは、パートナーセンターの場合と同じ `https://api.partnercenter.microsoft.com` です。

- 開発者は、パートナーセンターのアプリにパートナーセンターの API/SDK 機能を統合するために、アプリ ID を手動で登録して、米国政府向けの Microsoft Cloud を行う必要があります。 詳細については、「 [Microsoft National Cloud のパートナーセンターのアプリの詳細を登録](create-apps-for-partner-center-for-microsoft-national-clouds.md)する」を参照してください。
