---
title: "Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail | Documents Microsoft"
description: "Vue d’ensemble du déploiement des appareils Windows 10 pour les entreprises et comment toointegrate avec Azure Active Directory pour hello Windows sur le cloud. Contraste hello différentes façons un périphérique peut être configuré et utilisé dans une entreprise via hello portail Azure."
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
ms.openlocfilehash: 95b452bc5ba3937e16de769275a59c77cb821e23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-10-for-hello-enterprise-ways-toouse-devices-for-work"></a><span data-ttu-id="caeca-105">Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail</span><span class="sxs-lookup"><span data-stu-id="caeca-105">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>
<span data-ttu-id="caeca-106">Windows 10 permet de vous hello capacité tooleverage Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="caeca-106">Windows 10 gives you hello ability tooleverage Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="caeca-107">Vous pouvez vous connecter à Windows 10 appareils tooAzure AD afin que les utilisateurs peuvent se connecter tooWindows à l’aide de comptes Azure AD ou en ajoutant leurs ID de Azure toogain accès toobusiness applications et leurs ressources.</span><span class="sxs-lookup"><span data-stu-id="caeca-107">You can connect Windows 10 devices tooAzure AD so that users can sign in tooWindows by using Azure AD accounts or by adding their Azure IDs toogain access toobusiness apps and resources.</span></span>

![Azure Active Directory avec le cloud Windows](./media/active-directory-azureadjoin/windows10-overview.png)

## <a name="integrating-windows-10-devices-with-azure-active-directory--a-content-map"></a><span data-ttu-id="caeca-109">Intégration des appareils Windows 10 à Azure Active Directory : Plan du contenu</span><span class="sxs-lookup"><span data-stu-id="caeca-109">Integrating Windows 10 devices with Azure Active Directory--a content map</span></span>
<span data-ttu-id="caeca-110">Hello rubriques suivantes fournit des informations sur les différentes fonctionnalités des appareils Windows 10 dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="caeca-110">hello following topics provide insights into different capabilities of Windows 10 devices in your organization.</span></span>

|  | <span data-ttu-id="caeca-111">Rubriques</span><span class="sxs-lookup"><span data-stu-id="caeca-111">Topics</span></span> |
| --- | --- |
| <span data-ttu-id="caeca-112">Prise en main</span><span class="sxs-lookup"><span data-stu-id="caeca-112">Getting started</span></span> |[<span data-ttu-id="caeca-113">Utilisation d’appareils Windows 10 sur votre lieu de travail</span><span class="sxs-lookup"><span data-stu-id="caeca-113">Using Windows 10 devices in your workplace</span></span>](active-directory-azureadjoin-windows10-devices.md) <br> <br> [<span data-ttu-id="caeca-114">Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="caeca-114">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-overview.md) <br> <br> [<span data-ttu-id="caeca-115">Authentification des identités sans mot de passe avec Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="caeca-115">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md) |
| <span data-ttu-id="caeca-116">Déploiement</span><span class="sxs-lookup"><span data-stu-id="caeca-116">Deployment</span></span> |[<span data-ttu-id="caeca-117">Scénarios d’utilisation et considérations relatives au déploiement pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="caeca-117">Usage scenarios and deployment considerations for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md) <br><br> [<span data-ttu-id="caeca-118">Expériences de connexion tooAzure de périphériques joints au domaine Active Directory pour Windows 10</span><span class="sxs-lookup"><span data-stu-id="caeca-118">Connecting domain-joined devices tooAzure AD, for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)<br><br>[<span data-ttu-id="caeca-119">L’activation de Microsoft Passport pour travailler dans l’organisation de hello</span><span class="sxs-lookup"><span data-stu-id="caeca-119">Enabling Microsoft Passport for work in hello organization</span></span>](active-directory-azureadjoin-passport-deployment.md)<br><br> [<span data-ttu-id="caeca-120">Activer Enterprise State Roaming pour Windows 10</span><span class="sxs-lookup"><span data-stu-id="caeca-120">Enabling Enterprise State Roaming for Windows 10</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)<br><br> |
| <span data-ttu-id="caeca-121">Tâches de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="caeca-121">User tasks</span></span> |[<span data-ttu-id="caeca-122">Configuration d’un nouvel appareil Windows 10 avec Azure AD lors de l’installation</span><span class="sxs-lookup"><span data-stu-id="caeca-122">Setting up a new Windows 10 device with Azure AD during setup</span></span>](active-directory-azureadjoin-user-frx.md) <br><br> [<span data-ttu-id="caeca-123">Configuration d’un périphérique Windows 10 avec Azure AD à partir du menu Paramètres de hello</span><span class="sxs-lookup"><span data-stu-id="caeca-123">Setting up a Windows 10 device with Azure AD from hello settings menu</span></span>](active-directory-azureadjoin-user-upgrade.md) <br><br> [<span data-ttu-id="caeca-124">Joindre une organisation de tooyour appareil Windows 10 personnelle</span><span class="sxs-lookup"><span data-stu-id="caeca-124">Joining a personal Windows 10 device tooyour organization</span></span>](active-directory-azureadjoin-personal-device.md) |

