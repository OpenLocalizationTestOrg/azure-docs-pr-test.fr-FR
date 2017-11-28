---
title: "Détection des applications cloud non gérées avec Cloud App Discovery | Microsoft Docs"
description: Fournit une vue d'ensemble de la recherche et de la gestion d'applications avec Cloud App Discovery, ainsi que des informations sur ses avantages et son fonctionnement.
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
ms.openlocfilehash: 6284ff5bac8edbc19561d0916adef153526dfbe3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="finding-unmanaged-cloud-applications-with-cloud-app-discovery"></a><span data-ttu-id="008c4-104">Détection des applications cloud non gérées avec Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="008c4-104">Finding unmanaged cloud applications with Cloud App Discovery</span></span>
## <a name="overview"></a><span data-ttu-id="008c4-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="008c4-105">Overview</span></span>
<span data-ttu-id="008c4-106">Dans les entreprises modernes, les services informatiques n’ont souvent pas connaissance de toutes les applications cloud utilisées par les membres de l’organisation pour effectuer leur travail.</span><span class="sxs-lookup"><span data-stu-id="008c4-106">In modern enterprises, IT departments are often not aware of all the cloud applications that members of their organization use to do their work.</span></span> <span data-ttu-id="008c4-107">Il est facile de comprendre pourquoi les administrateurs s’inquiètent d’un accès non autorisé aux données d'entreprise, de possibles fuites de données et autres risques de sécurité.</span><span class="sxs-lookup"><span data-stu-id="008c4-107">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> <span data-ttu-id="008c4-108">Négliger cet aspect peut sérieusement compliquer l’élaboration d'un plan visant à gérer ces risques de sécurité.</span><span class="sxs-lookup"><span data-stu-id="008c4-108">This lack of awareness can make creating a plan for dealing with these security risks seem daunting.</span></span>

<span data-ttu-id="008c4-109">Cloud App Discovery est une fonctionnalité Premium d’Azure Active Directory (AD) qui vous permet de détecter les applications cloud utilisées par les membres de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="008c4-109">Cloud App Discovery is a feature of Azure Active Directory (AD) Premium that enables you to discover cloud applications being used by the people in your organization.</span></span>

<span data-ttu-id="008c4-110">**Avec Cloud App Discovery, vous pouvez :**</span><span class="sxs-lookup"><span data-stu-id="008c4-110">**With Cloud App Discovery, you can:**</span></span>

* <span data-ttu-id="008c4-111">détecter les applications cloud utilisées et mesurer l’utilisation par nombre d’utilisateurs, volume de trafic ou nombre de demandes web à l’application ;</span><span class="sxs-lookup"><span data-stu-id="008c4-111">Find the cloud applications being used and measure that usage by number of users, volume of traffic or number of web requests to the application.</span></span>
* <span data-ttu-id="008c4-112">identifier les utilisateurs d’une application ;</span><span class="sxs-lookup"><span data-stu-id="008c4-112">Identify the users that are using an application.</span></span>
* <span data-ttu-id="008c4-113">exporter des données pour effectuer une analyse hors ligne ;</span><span class="sxs-lookup"><span data-stu-id="008c4-113">Export data for offline analysis.</span></span>
* <span data-ttu-id="008c4-114">confier le contrôle de ces applications au service informatique et activer l'authentification unique pour la gestion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="008c4-114">Bring these applications under IT control and enable single sign on for user management.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="008c4-115">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="008c4-115">How it works</span></span>
1. <span data-ttu-id="008c4-116">Des agents d'utilisation des applications sont installés sur les ordinateurs de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="008c4-116">Application usage agents are installed on user's computers.</span></span>
2. <span data-ttu-id="008c4-117">Les informations sur l’utilisation des applications capturées par les agents sont envoyées via un canal sécurisé et chiffré au service Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="008c4-117">The application usage information captured by the agents is sent over a secure, encrypted channel to the cloud app discovery service.</span></span>
3. <span data-ttu-id="008c4-118">Celui-ci évalue les données et génère des rapports.</span><span class="sxs-lookup"><span data-stu-id="008c4-118">The Cloud App Discovery service evaluates the data and generates reports.</span></span>

![Diagramme Cloud App Discovery](./media/active-directory-cloudappdiscovery/cad01.png)

<span data-ttu-id="008c4-120">Pour prendre en main Cloud App Discovery, consultez [Prise en main de Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span><span class="sxs-lookup"><span data-stu-id="008c4-120">To get started with Cloud App Discovery, see [Getting Started With Cloud App Discovery](http://social.technet.microsoft.com/wiki/contents/articles/30962.getting-started-with-cloud-app-discovery.aspx)</span></span>

## <a name="related-articles"></a><span data-ttu-id="008c4-121">Articles connexes</span><span class="sxs-lookup"><span data-stu-id="008c4-121">Related articles</span></span>
* [<span data-ttu-id="008c4-122">Considérations relatives à la confidentialité et à la sécurité de Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="008c4-122">Cloud App Discovery Security and Privacy Considerations</span></span>](active-directory-cloudappdiscovery-security-and-privacy-considerations.md)  
* [<span data-ttu-id="008c4-123">Guide de déploiement d’une stratégie de groupe Cloud App Discovery</span><span class="sxs-lookup"><span data-stu-id="008c4-123">Cloud App Discovery Group Policy Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30965.cloud-app-discovery-group-policy-deployment-guide.aspx)
* [<span data-ttu-id="008c4-124">Guide de déploiement de Cloud App Discovery System Center</span><span class="sxs-lookup"><span data-stu-id="008c4-124">Cloud App Discovery System Center Deployment Guide</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/30968.cloud-app-discovery-system-center-deployment-guide.aspx)
* [<span data-ttu-id="008c4-125">Paramètres de Registre de Cloud App Discovery pour les services de proxy avec ports personnalisés</span><span class="sxs-lookup"><span data-stu-id="008c4-125">Cloud App Discovery Registry Settings for Proxy Servers with Custom Ports</span></span>](active-directory-cloudappdiscovery-registry-settings-for-proxy-services.md)
* [<span data-ttu-id="008c4-126">Cloud App Discovery - Agent Changelog </span><span class="sxs-lookup"><span data-stu-id="008c4-126">Cloud App Discovery Agent Changelog </span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24616.cloud-app-discovery-agent-changelog.aspx)
* [<span data-ttu-id="008c4-127">Cloud App Discovery - Forum aux Questions</span><span class="sxs-lookup"><span data-stu-id="008c4-127">Cloud App Discovery Frequently Asked Questions</span></span>](http://social.technet.microsoft.com/wiki/contents/articles/24037.cloud-app-discovery-frequently-asked-questions.aspx)
* [<span data-ttu-id="008c4-128">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="008c4-128">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

