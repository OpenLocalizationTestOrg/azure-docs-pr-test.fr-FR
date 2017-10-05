---
title: "Windows 10 pour l’entreprise : plusieurs manières d’utiliser des appareils professionnels | Microsoft Docs"
description: "Vue d’ensemble du déploiement des appareils Windows 10 pour les entreprises et de l’intégration à Azure Active Directory pour le cloud Windows. Comparaison des différentes méthodes d’approvisionnement et d’utilisation d’un appareil dans une entreprise via le portail Azure."
keywords: "Services cloud de Windows, Windows sur Azure Active Directory, appareils Windows 10 sur Azure, appareils Windows Azure"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2cb9ab6a-55b6-4658-b7f2-6e05ae015e1b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 804156048a7596f9937098e6fe762f424526473c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-10-for-the-enterprise-ways-to-use-devices-for-work"></a><span data-ttu-id="667ab-105">Windows 10 pour l’entreprise : plusieurs manières d’utiliser des appareils professionnels</span><span class="sxs-lookup"><span data-stu-id="667ab-105">Windows 10 for the enterprise: Ways to use devices for work</span></span>
<span data-ttu-id="667ab-106">Windows 10 vous permet de tirer parti d’Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="667ab-106">Windows 10 gives you the ability to leverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="667ab-107">Vous pouvez connecter des appareils Windows 10 à Azure AD afin que les utilisateurs puissent se connecter à Windows avec des comptes Azure AD ou en ajoutant leur ID Azure pour accéder aux ressources et aux applications métier.</span><span class="sxs-lookup"><span data-stu-id="667ab-107">You can connect Windows 10 devices to Azure AD so that users can sign in to Windows by using Azure AD accounts or by adding their Azure IDs to gain access to business apps and resources.</span></span>

![Azure Active Directory avec le cloud Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="667ab-109">Intégration des appareils Windows 10 à Azure Active Directory : Plan du contenu</span><span class="sxs-lookup"><span data-stu-id="667ab-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="667ab-110">Les rubriques suivantes fournissent des indications sur l’utilisation des différentes fonctionnalités des appareils Windows 10 au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="667ab-110">The following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="667ab-111">Rubriques</span><span class="sxs-lookup"><span data-stu-id="667ab-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="667ab-112">Prise en main</span><span class="sxs-lookup"><span data-stu-id="667ab-112">Getting started</span></span> |[<span data-ttu-id="667ab-113">Utilisation d’appareils Windows 10 sur votre lieu de travail</span><span class="sxs-lookup"><span data-stu-id="667ab-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="667ab-114">Extension des fonctionnalités du cloud aux appareils Windows 10 via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="667ab-114">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="667ab-115">Authentification des identités sans mot de passe avec Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="667ab-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="667ab-116">Déploiement</span><span class="sxs-lookup"><span data-stu-id="667ab-116">Deployment</span></span> |[<span data-ttu-id="667ab-117">Scénarios d’utilisation et considérations relatives au déploiement pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="667ab-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="667ab-118">Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="667ab-118">Connecting domain-joined devices to Azure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="667ab-119">Activation de Microsoft Passport for Work dans l’organisation</span><span class="sxs-lookup"><span data-stu-id="667ab-119">Enabling Microsoft Passport for work in the organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="667ab-120">Activer Enterprise State Roaming pour Windows 10</span><span class="sxs-lookup"><span data-stu-id="667ab-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="667ab-121">Tâches de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="667ab-121">User tasks</span></span> |[<span data-ttu-id="667ab-122">Configuration d’un nouvel appareil Windows 10 avec Azure AD lors de l’installation</span><span class="sxs-lookup"><span data-stu-id="667ab-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="667ab-123">Configuration d’un appareil Windows 10 avec Azure AD à partir du menu des paramètres</span><span class="sxs-lookup"><span data-stu-id="667ab-123">Setting up a Windows 10 device with Azure AD from the settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="667ab-124">Association d’un appareil Windows 10 personnel à votre organisation</span><span class="sxs-lookup"><span data-stu-id="667ab-124">Joining a personal Windows 10 device to your organization</span></span>](active-directory-azureadjoin-personal-device.md) |

