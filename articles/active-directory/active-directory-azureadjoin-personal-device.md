---
title: "Association d’un appareil personnel à votre organisation | Microsoft Docs"
description: "Explique la manière dont les utilisateurs peuvent inscrire leurs appareils Windows 10 personnels sur le réseau de leur entreprise, avec des étapes de déploiement pour un scénario de BYOD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 9f3d38f5-1cfd-43d4-97da-4fed1255a1ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 9418365ea18b065551448742b21c8b17a1749fc8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-personal-device-to-your-organization"></a><span data-ttu-id="4b69e-103">Association d’un appareil personnel à votre organisation</span><span class="sxs-lookup"><span data-stu-id="4b69e-103">Join a personal device to your organization</span></span>
## <a name="to-join-a-windows-10-device-to-your-organization"></a><span data-ttu-id="4b69e-104">Association d’un appareil Windows 10 à votre organisation</span><span class="sxs-lookup"><span data-stu-id="4b69e-104">To join a Windows 10 device to your organization</span></span>
1. <span data-ttu-id="4b69e-105">Dans le menu **Démarrer**, sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="4b69e-105">From the **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="4b69e-106">Sélectionnez **Comptes** puis cliquez sur **Votre compte**.</span><span class="sxs-lookup"><span data-stu-id="4b69e-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="4b69e-107">Cliquez sur **Ajouter un compte professionnel ou scolaire**puis saisissez votre compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="4b69e-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="4b69e-108">Sur la page de connexion pour votre organisation, entrez votre nom d’utilisateur et votre mot de passe, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b69e-108">On the sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="4b69e-109">Vous devrez ensuite relever un défi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="4b69e-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="4b69e-110">(Ce défi est configurable par un administrateur informatique).</span><span class="sxs-lookup"><span data-stu-id="4b69e-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="4b69e-111">Azure Active Directory (Azure AD) vérifie si l’appareil requiert l’inscription à la gestion des appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="4b69e-111">Azure Active Directory (Azure AD) checks whether the device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="4b69e-112">Windows enregistre l’appareil dans le répertoire de l’organisation dans Azure AD et l’inscrit dans la gestion des appareils mobiles, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="4b69e-112">Windows registers the device in the organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="4b69e-113">Si vous êtes un utilisateur géré, Windows vous dirige vers le bureau par le biais de la connexion automatique.</span><span class="sxs-lookup"><span data-stu-id="4b69e-113">If you are a managed user, Windows takes you to the desktop through the automatic sign-in.</span></span>
9. <span data-ttu-id="4b69e-114">Si vous êtes un utilisateur fédéré, vous accédez à l’écran d’ouverture de session Windows pour entrer vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="4b69e-114">If you are a federated user, you will be taken to a Windows sign-in screen to enter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="4b69e-115">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4b69e-115">Additional information</span></span>
* [<span data-ttu-id="4b69e-116">Windows 10 pour l’entreprise : plusieurs manières d’utiliser des appareils professionnels</span><span class="sxs-lookup"><span data-stu-id="4b69e-116">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="4b69e-117">Extension des fonctionnalités du cloud aux appareils Windows 10 via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="4b69e-117">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="4b69e-118">Authentification des identités sans mot de passe avec Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="4b69e-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="4b69e-119">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="4b69e-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="4b69e-120">Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="4b69e-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="4b69e-121">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="4b69e-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

