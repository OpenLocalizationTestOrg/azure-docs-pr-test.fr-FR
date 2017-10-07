---
title: "Vue d’ensemble d’Enterprise State Roaming | Microsoft Docs"
description: "Fournit des informations sur les paramètres Enterprise State Roaming dans les périphériques Windows. Enterprise State Roaming fournit aux utilisateurs une expérience unifiée sur leurs appareils Windows et réduit le temps nécessaire à la configuration d’un nouveau périphérique."
services: active-directory
keywords: "Qu’est-ce que Enterprise State Roaming, la synchronisation d’entreprise et Windows cloud"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 83b3b58f-94c1-4ab0-be05-20e01f5ae3f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: b3c01f8d332d26e92dc3052681a4b2c95142d440
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-state-roaming-overview"></a><span data-ttu-id="3674a-105">Présentation d’Enterprise State Roaming</span><span class="sxs-lookup"><span data-stu-id="3674a-105">Enterprise State Roaming overview</span></span>
<span data-ttu-id="3674a-106">Avec Windows 10, les utilisateurs [Azure Active Directory (Azure AD)](active-directory-whatis.md) ont la possibilité de synchroniser en toute sécurité leurs paramètres utilisateur et les données de paramètres d’application dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="3674a-106">With Windows 10, [Azure Active Directory (Azure AD)](active-directory-whatis.md) users gain the ability to securely synchronize their user settings and application settings data to the cloud.</span></span> <span data-ttu-id="3674a-107">Enterprise State Roaming fournit aux utilisateurs une expérience unifiée sur leurs appareils Windows et réduit le temps nécessaire à la configuration d’un nouveau périphérique.</span><span class="sxs-lookup"><span data-stu-id="3674a-107">Enterprise State Roaming provides users with a unified experience across their Windows devices and reduces the time needed for configuring a new device.</span></span> <span data-ttu-id="3674a-108">Enterprise State Roaming fonctionne comme la [synchronisation des paramètres de consommateur](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) présentée dans Windows 8.</span><span class="sxs-lookup"><span data-stu-id="3674a-108">Enterprise State Roaming operates similar to the standard [consumer settings sync](http://windows.microsoft.com/en-US/windows-8/sync-settings-pcs) that was first introduced in Windows 8.</span></span> <span data-ttu-id="3674a-109">En outre, Enterprise State Roaming offre :</span><span class="sxs-lookup"><span data-stu-id="3674a-109">Additionally, Enterprise State Roaming offers:</span></span>

* <span data-ttu-id="3674a-110">**Séparation des données d’entreprise des données client** : les organisations maîtrisent leurs données, et les données d’entreprise ne sont pas mélangées dans le compte cloud client ou aucune donnée client ne figure dans le compte cloud d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="3674a-110">**Separation of corporate and consumer data** – Organizations are in control of their data, and there is no mixing of corporate data in a consumer cloud account or consumer data in an enterprise cloud account.</span></span>
* <span data-ttu-id="3674a-111">**Sécurité renforcée** : les données sont automatiquement chiffrées avant de quitter l’appareil Windows 10 de l’utilisateur à l’aide d’Azure Rights Management (Azure RMS) et les données restent chiffrées au repos dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="3674a-111">**Enhanced security** – Data is automatically encrypted before leaving the user’s Windows 10 device by using Azure Rights Management (Azure RMS), and data stays encrypted at rest in the cloud.</span></span> <span data-ttu-id="3674a-112">Tout le contenu reste chiffré au repos dans le cloud, à l’exception des espaces de noms tels que les noms de paramètres et les noms d’application Windows.</span><span class="sxs-lookup"><span data-stu-id="3674a-112">All content stays encrypted at rest in the cloud, except for the namespaces, like settings names and Windows app names.</span></span>  
* <span data-ttu-id="3674a-113">**Meilleure gestion et meilleure surveillance** : vous offre plus de contrôle et de visibilité sur qui synchronise les paramètres dans votre organisation et sur quels appareils à travers l’intégration du portail Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3674a-113">**Better management and monitoring** – Provides control and visibility over who syncs settings in your organization and on which devices through the Azure AD portal integration.</span></span> 

<span data-ttu-id="3674a-114">Enterprise State Roaming est disponible dans plusieurs régions Azure.</span><span class="sxs-lookup"><span data-stu-id="3674a-114">Enterprise State Roaming is available in multiple Azure regions.</span></span> <span data-ttu-id="3674a-115">Pour consulter la liste à jour des régions disponibles, voir la page [Régions Azure - Services par région](https://azure.microsoft.com/regions/#services) sous Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3674a-115">You can find the updated list of available regions on the [Azure Services by Regions](https://azure.microsoft.com/regions/#services) page under Azure Active Directory.</span></span>

| <span data-ttu-id="3674a-116">Article</span><span class="sxs-lookup"><span data-stu-id="3674a-116">Article</span></span> | <span data-ttu-id="3674a-117">Description</span><span class="sxs-lookup"><span data-stu-id="3674a-117">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="3674a-118">Activer Enterprise State Roaming dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3674a-118">Enable Enterprise State Roaming in Azure Active Directory</span></span>](active-directory-windows-enterprise-state-roaming-enable.md) |<span data-ttu-id="3674a-119">Enterprise State Roaming est disponible pour toute organisation ayant souscrit un abonnement premium à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3674a-119">Enterprise State Roaming is available to any organization with a Premium Azure Active Directory (Azure AD) subscription.</span></span> <span data-ttu-id="3674a-120">Pour plus de détails sur l’obtention d’un abonnement Azure AD, consultez la page [du produit Azure AD](https://azure.microsoft.com/services/active-directory) .</span><span class="sxs-lookup"><span data-stu-id="3674a-120">For more details on how to get an Azure AD subscription, see the [Azure AD product](https://azure.microsoft.com/services/active-directory) page.</span></span> |
| [<span data-ttu-id="3674a-121">FAQ sur l’itinérance des paramètres et des données</span><span class="sxs-lookup"><span data-stu-id="3674a-121">Settings and data roaming FAQ</span></span>](active-directory-windows-enterprise-state-roaming-faqs.md) |<span data-ttu-id="3674a-122">Cette rubrique répond à certaines questions que les administrateurs informatiques peuvent se poser sur les paramètres et la synchronisation des données d’application.</span><span class="sxs-lookup"><span data-stu-id="3674a-122">This topic answers some questions IT administrators might have about settings and app data sync.</span></span> |
| [<span data-ttu-id="3674a-123">Paramètres de stratégie de groupe et de MDM pour la synchronisation des paramètres</span><span class="sxs-lookup"><span data-stu-id="3674a-123">Group policy and MDM settings for settings sync</span></span>](active-directory-windows-enterprise-state-roaming-group-policy-settings.md) |<span data-ttu-id="3674a-124">Windows 10 fournit les paramètres de stratégie de groupe et de gestion d’appareil mobile (MDM) pour limiter la synchronisation des paramètres.</span><span class="sxs-lookup"><span data-stu-id="3674a-124">Windows 10 provides Group Policy and mobile device management (MDM) policy settings to limit settings sync.</span></span> |
| [<span data-ttu-id="3674a-125">Référence des paramètres d’itinérance Windows 10</span><span class="sxs-lookup"><span data-stu-id="3674a-125">Windows 10 roaming settings reference</span></span>](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md) |<span data-ttu-id="3674a-126">Voici une liste complète de tous les paramètres destinés à l’itinérance et/ou à la sauvegarde dans Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3674a-126">The following is a complete list of all the settings that will be roamed and/or backed-up in Windows 10.</span></span> |
| [<span data-ttu-id="3674a-127">Dépannage</span><span class="sxs-lookup"><span data-stu-id="3674a-127">Troubleshooting</span></span>](active-directory-windows-enterprise-state-roaming-troubleshooting.md) |<span data-ttu-id="3674a-128">Cette rubrique présente certaines étapes de base pour la résolution des problèmes et contient une liste de problèmes connus.</span><span class="sxs-lookup"><span data-stu-id="3674a-128">This topic goes through some basic steps for troubleshooting, and contains a list of known issues.</span></span> |
