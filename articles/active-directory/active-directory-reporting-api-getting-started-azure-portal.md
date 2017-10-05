---
title: "Prise en main de l’API de création de rapports Azure AD | Microsoft Docs"
description: "Prise en main de l'API de création de rapports Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 9944cbd2b1b7c4acb18d37da1394c0bbc170f77d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="8fd2b-103">Prise en main de l’API de création de rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8fd2b-103">Getting started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="8fd2b-104">Azure Active Directory vous fournit plusieurs rapports.</span><span class="sxs-lookup"><span data-stu-id="8fd2b-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="8fd2b-105">Les données de ces rapports peuvent être très utiles pour vos applications, telles que les systèmes SIEM, l’audit et les outils d’analyse décisionnelle.</span><span class="sxs-lookup"><span data-stu-id="8fd2b-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="8fd2b-106">Les API de création de rapports Azure AD fournissent un accès par programme aux données via un ensemble d’API REST.</span><span class="sxs-lookup"><span data-stu-id="8fd2b-106">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="8fd2b-107">Vous pouvez appeler ces API à partir de divers outils et langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="8fd2b-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="8fd2b-108">Cet article vous fournit les informations dont vous avez besoin pour vous familiariser avec l’API de création de rapports Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8fd2b-108">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="8fd2b-109">Dans la section suivante, vous trouverez plus d’informations sur l’utilisation des API d’audit et de connexion.</span><span class="sxs-lookup"><span data-stu-id="8fd2b-109">In the next section, you find more details about using the audit and sign-in APIs.</span></span> 

<span data-ttu-id="8fd2b-110">Pour consulter les questions les plus fréquentes, lisez notre [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="8fd2b-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="8fd2b-111">En cas de problème, [Envoyez un ticket de support](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="8fd2b-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="8fd2b-112">Carte d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="8fd2b-112">Learning map</span></span>
1. <span data-ttu-id="8fd2b-113">**Préparer** : avant de pouvoir tester les exemples d’API, vous devez respecter la [configuration requise pour accéder à l’API de création de rapports Azure AD](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8fd2b-113">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="8fd2b-114">**Explorer** : faites-vous une première impression des API de création de rapports :</span><span class="sxs-lookup"><span data-stu-id="8fd2b-114">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="8fd2b-115">Utilisation des exemples pour l’API d’audit</span><span class="sxs-lookup"><span data-stu-id="8fd2b-115">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="8fd2b-116">Utilisation des exemples pour l’API de création de rapports sur l’activité de connexion</span><span class="sxs-lookup"><span data-stu-id="8fd2b-116">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="8fd2b-117">**Personnaliser** : créez votre propre solution :</span><span class="sxs-lookup"><span data-stu-id="8fd2b-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="8fd2b-118">Utilisation de la référence d’API d’audit</span><span class="sxs-lookup"><span data-stu-id="8fd2b-118">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="8fd2b-119">Utilisation de la référence d’API de création de rapports sur l’activité de connexion</span><span class="sxs-lookup"><span data-stu-id="8fd2b-119">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="8fd2b-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8fd2b-120">Next Steps</span></span>
<span data-ttu-id="8fd2b-121">Si vous voulez consulter l’ensemble des points de terminaison de l’API Azure AD Graph disponibles, utilisez ce lien : [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="8fd2b-121">If you are curious to see all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

