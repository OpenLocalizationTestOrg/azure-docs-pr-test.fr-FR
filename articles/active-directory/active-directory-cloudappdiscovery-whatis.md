---
title: "aaaFinding non managée à des applications de cloud avec Cloud App Discovery | Documents Microsoft"
description: Fournit des informations sur la recherche et la gestion des applications avec Cloud App Discovery, quels sont les avantages de hello et son fonctionnement.
services: active-directory
keywords: "détection d'applications cloud, gestion d'applications"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: db968bf5-22ae-489f-9c3e-14df6e1fef0a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 50c24af9bb400e4be11f4ad2d1de13d26f5467bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="fdee3-104">Détection des applications cloud non gérées avec Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="fdee3-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="fdee3-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="fdee3-105">Overview</span></span>
<span data-ttu-id="fdee3-106">Dans les entreprises modernes, les services informatiques sont souvent pas conscients de toutes les applications de cloud hello que les membres de leur organisation utilisent toodo leur travail.</span><span class="sxs-lookup"><span data-stu-id="fdee3-106">In modern enterprises, IT departments are often not aware of all hello cloud applications that members of their organization use toodo their work.</span></span> <span data-ttu-id="fdee3-107">Il est facile toosee pourquoi administrateurs auront des problèmes sur les données toocorporate de tout accès non autorisé, les fuites de données possibles et les autres risques de sécurité.</span><span class="sxs-lookup"><span data-stu-id="fdee3-107">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="fdee3-108">Négliger cet aspect peut sérieusement compliquer l’élaboration d'un plan visant à gérer ces risques de sécurité.</span><span class="sxs-lookup"><span data-stu-id="fdee3-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="fdee3-109">Cloud App Discovery est une fonctionnalité Premium d’Azure Active Directory (AD) qui permet à vos applications de cloud toodiscover utilisées par les personnes hello dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="fdee3-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you toodiscover cloud applications being used by hello people in your organization.</span></span>

<span data-ttu-id="fdee3-110">**Avec Cloud App Discovery, vous pouvez :**</span><span class="sxs-lookup"><span data-stu-id="fdee3-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="fdee3-111">Recherche des applications de cloud hello utilisées et que l’utilisation de mesures par nombre d’utilisateurs, le volume de trafic ou du nombre d’applications de toohello de demandes web.</span><span class="sxs-lookup"><span data-stu-id="fdee3-111">Find hello cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests toohello application.</span></span>
* <span data-ttu-id="fdee3-112">Identifiez les utilisateurs hello qui utilisent une application.</span><span class="sxs-lookup"><span data-stu-id="fdee3-112">Identify hello users that are using an application.</span></span>
* <span data-ttu-id="fdee3-113">exporter des données pour effectuer une analyse hors ligne ;</span><span class="sxs-lookup"><span data-stu-id="fdee3-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="fdee3-114">confier le contrôle de ces applications au service informatique et activer l'authentification unique pour la gestion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="fdee3-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="fdee3-115">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="fdee3-115">How it works</span></span>
1. <span data-ttu-id="fdee3-116">Des agents d'utilisation des applications sont installés sur les ordinateurs de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fdee3-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="fdee3-117">informations d’utilisation application Hello capturées par les agents hello sont envoyées via un canal sécurisé, chiffré toohello cloud découverte du service d’applications.</span><span class="sxs-lookup"><span data-stu-id="fdee3-117">hello application usage information captured by hello agents is sent over a secure, encrypted channel toohello cloud app discovery service.</span></span>
3. <span data-ttu-id="fdee3-118">Hello service Cloud App Discovery évalue les données hello et génère des rapports.</span><span class="sxs-lookup"><span data-stu-id="fdee3-118">hello Cloud App Discovery service evaluates hello data and generates reports.</span></span>

![Diagramme Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="fdee3-120">tooget démarrer avec Cloud App Discovery, consultez [mise en route a démarré avec Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="fdee3-120">tooget started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="fdee3-121">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="fdee3-121">Related articles</span></span>
* [<span data-ttu-id="fdee3-122">Considérations relatives à la confidentialité et à la sécurité de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="fdee3-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="fdee3-123">Guide de déploiement d’une stratégie de groupe Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="fdee3-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="fdee3-124">Guide de déploiement de Cloud App Discovery System Center</span><span class="sxs-lookup"><span data-stu-id="fdee3-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="fdee3-125">Paramètres de Registre de Cloud App Discovery pour les services de proxy avec ports personnalisés</span><span class="sxs-lookup"><span data-stu-id="fdee3-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="fdee3-126">Cloud App Discovery - Agent Changelog </span><span class="sxs-lookup"><span data-stu-id="fdee3-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="fdee3-127">Cloud App Discovery - Forum aux Questions</span><span class="sxs-lookup"><span data-stu-id="fdee3-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="fdee3-128">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fdee3-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

