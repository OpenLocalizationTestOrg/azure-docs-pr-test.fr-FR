---
title: aaaJoin une organisation de tooyour appareil personnel | Documents Microsoft
description: "Explique comment les utilisateurs peuvent inscrire leur personnel Windows 10 appareils tootheir réseau d’entreprise et fournit les étapes de déploiement pour un scénario BYOD."
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
ms.openlocfilehash: 979e2461dd9ad0438aa402a0a3223cc84c4c625c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-personal-device-tooyour-organization"></a><span data-ttu-id="c4d55-103">Joindre une organisation de tooyour appareil personnel</span><span class="sxs-lookup"><span data-stu-id="c4d55-103">Join a personal device tooyour organization</span></span>
## <a name="toojoin-a-windows-10-device-tooyour-organization"></a><span data-ttu-id="c4d55-104">organisation de tooyour périphérique toojoin Windows 10</span><span class="sxs-lookup"><span data-stu-id="c4d55-104">toojoin a Windows 10 device tooyour organization</span></span>
1. <span data-ttu-id="c4d55-105">À partir de hello **Démarrer** menu, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="c4d55-105">From hello **Start** menu, select **Settings**.</span></span>
2. <span data-ttu-id="c4d55-106">Sélectionnez **Comptes** puis cliquez sur **Votre compte**.</span><span class="sxs-lookup"><span data-stu-id="c4d55-106">Select **Accounts**, and then click **Your account**.</span></span>
3. <span data-ttu-id="c4d55-107">Cliquez sur **Ajouter un compte professionnel ou scolaire**puis saisissez votre compte professionnel.</span><span class="sxs-lookup"><span data-stu-id="c4d55-107">Click **Add Work or School account**, and then type in your organizational account.</span></span>
4. <span data-ttu-id="c4d55-108">Sur hello-page de connexion pour votre organisation, entrez votre nom d’utilisateur et un mot de passe, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4d55-108">On hello sign-in page for your organization, enter your user name and password, and then click **OK**.</span></span>
5. <span data-ttu-id="c4d55-109">Vous devrez ensuite relever un défi Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="c4d55-109">You will be prompted for a multi-factor authentication challenge.</span></span> <span data-ttu-id="c4d55-110">(Ce défi est configurable par un administrateur informatique).</span><span class="sxs-lookup"><span data-stu-id="c4d55-110">(This challenge is configurable by an IT administrator.)</span></span>
6. <span data-ttu-id="c4d55-111">Azure Active Directory (Azure AD) vérifie si le périphérique de hello requiert inscription de gestion des appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="c4d55-111">Azure Active Directory (Azure AD) checks whether hello device requires mobile device management enrollment.</span></span>
7. <span data-ttu-id="c4d55-112">Windows enregistre l’appareil de hello dans l’annuaire de l’organisation hello dans Azure AD et s’inscrit dans la gestion des appareils mobiles, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="c4d55-112">Windows registers hello device in hello organization’s directory in Azure AD and enrolls it in mobile device management, if appropriate.</span></span>
8. <span data-ttu-id="c4d55-113">Si vous êtes un utilisateur géré, Windows effectue le bureau toohello via hello automatique connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="c4d55-113">If you are a managed user, Windows takes you toohello desktop through hello automatic sign-in.</span></span>
9. <span data-ttu-id="c4d55-114">Si vous êtes un utilisateur fédéré, vous serez prises tooa Windows connectez-vous écran tooenter vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="c4d55-114">If you are a federated user, you will be taken tooa Windows sign-in screen tooenter your credentials.</span></span>

## <a name="additional-information"></a><span data-ttu-id="c4d55-115">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c4d55-115">Additional information</span></span>
* [<span data-ttu-id="c4d55-116">Windows 10 pour les entreprises hello : appareils toouse de méthodes de travail</span><span class="sxs-lookup"><span data-stu-id="c4d55-116">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="c4d55-117">Extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="c4d55-117">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="c4d55-118">Authentification des identités sans mot de passe avec Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="c4d55-118">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="c4d55-119">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="c4d55-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="c4d55-120">Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="c4d55-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="c4d55-121">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="c4d55-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

