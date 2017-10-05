---
title: "Prise en main de l’API de création de rapports Azure AD dans le portail Azure Classic | Microsoft Docs"
description: "Prise en main de l'API de création de rapports Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="51de4-103">Prise en main de l’API de création de rapports Azure AD dans le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="51de4-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="51de4-104">*Cette rubrique fait partie du guide [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="51de4-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="51de4-105">Azure Active Directory vous fournit plusieurs rapports.</span><span class="sxs-lookup"><span data-stu-id="51de4-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="51de4-106">Les données de ces rapports peuvent être très utiles pour vos applications, telles que les systèmes SIEM, l’audit et les outils d’analyse décisionnelle.</span><span class="sxs-lookup"><span data-stu-id="51de4-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="51de4-107">Les API de création de rapports Azure AD fournissent un accès par programme aux données via un ensemble d’API REST.</span><span class="sxs-lookup"><span data-stu-id="51de4-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="51de4-108">Vous pouvez appeler ces API à partir de divers outils et langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="51de4-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="51de4-109">Cet article vous fournit les informations dont vous avez besoin pour vous familiariser avec l’API de création de rapports Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51de4-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="51de4-110">Dans la section suivante, vous trouverez plus d’informations sur l’utilisation des API d’audit et de connexion.</span><span class="sxs-lookup"><span data-stu-id="51de4-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="51de4-111">Pour toutes les autres API, consultez l’article [Rapports et événements Azure AD (préversion)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview).</span><span class="sxs-lookup"><span data-stu-id="51de4-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="51de4-112">Si vous avez des questions, des problèmes ou des commentaires, veuillez contacter [Aide à la création de rapports AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="51de4-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="51de4-113">Carte d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="51de4-113">Learning map</span></span>
1. <span data-ttu-id="51de4-114">**Préparer** : avant de pouvoir tester les exemples d’API, vous devez respecter la [configuration requise pour accéder à l’API de création de rapports Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="51de4-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="51de4-115">**Explorer** : faites-vous une première impression des API de création de rapports :</span><span class="sxs-lookup"><span data-stu-id="51de4-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="51de4-116">Utilisation des exemples pour l’API d’audit</span><span class="sxs-lookup"><span data-stu-id="51de4-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="51de4-117">Utilisation des exemples pour l’API de création de rapports sur l’activité de connexion</span><span class="sxs-lookup"><span data-stu-id="51de4-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="51de4-118">**Personnaliser** : créez votre propre solution :</span><span class="sxs-lookup"><span data-stu-id="51de4-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="51de4-119">Utilisation de la référence d’API d’audit</span><span class="sxs-lookup"><span data-stu-id="51de4-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="51de4-120">Utilisation de la référence d’API de création de rapports sur l’activité de connexion</span><span class="sxs-lookup"><span data-stu-id="51de4-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="51de4-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="51de4-121">Next Steps</span></span>
<span data-ttu-id="51de4-122">Si vous voulez consulter l’ensemble des points de terminaison de l’API Azure AD Graph disponibles, accédez à [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="51de4-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

