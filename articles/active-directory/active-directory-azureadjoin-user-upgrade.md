---
title: "aaaSet d’un périphérique Windows 10 avec Azure AD à partir des paramètres | Documents Microsoft"
description: "Explique comment les utilisateurs peuvent participer tooAzure AD via le menu Paramètres de hello."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: b844e1d9-ad43-4e4a-a398-5c4a43bf2f5c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d6485228338db571cc01f913c99fbba49e0bb74a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="f0d7c-103">Configuration d’un appareil Windows 10 avec Azure AD à partir des paramètres</span><span class="sxs-lookup"><span data-stu-id="f0d7c-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="f0d7c-104">Si vous êtes déjà à l’aide de Windows 7 ou Windows 8 et que votre ordinateur ou le périphérique a été mis à niveau tooWindows 10, vous pouvez joindre tooAzure Active Directory (Azure AD) via le menu Paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded tooWindows 10, you can join tooAzure Active Directory (Azure AD) through hello Settings menu.</span></span>

## <a name="toojoin-tooazure-ad-from-hello-settings-menu"></a><span data-ttu-id="f0d7c-105">toojoin tooAzure AD à partir du menu Paramètres de hello</span><span class="sxs-lookup"><span data-stu-id="f0d7c-105">toojoin tooAzure AD from hello Settings menu</span></span>
1. <span data-ttu-id="f0d7c-106">À partir de hello **Démarrer** menu, cliquez sur hello **paramètres** icône.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-106">From hello **Start** menu, click hello **Settings** charm.</span></span>
2. <span data-ttu-id="f0d7c-107">Accédez à **Paramètres**, sélectionnez **Système**->**Info produit**->**Rejoindre Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="f0d7c-108"><center>
   ![Rejoindre Azure AD à partir du menu Paramètres de hello](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png)</center></span><span class="sxs-lookup"><span data-stu-id="f0d7c-108"><center>
![Join Azure AD from hello Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="f0d7c-109">Cliquez sur **continuer** dans la fenêtre de message hello Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-109">Click **Continue** in hello Azure AD Join message window.</span></span>
   
   <span data-ttu-id="f0d7c-110"><center>
   ![Fenêtre de message Joindre Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png)</center></span><span class="sxs-lookup"><span data-stu-id="f0d7c-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="f0d7c-111">Indiquez vos informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="f0d7c-112">Cette expérience de connexion inclut toutes les étapes de hello sont l’authentification toocomplete requis.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-112">This sign-in experience will include all hello steps that are required toocomplete authentication.</span></span> <span data-ttu-id="f0d7c-113">Si vous faites partie d’un locataire fédéré, votre administrateur vous fournira avec l’expérience de fédération hello qui est hébergé par votre organisation.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-113">If you are part of a federated tenant, your administrator will provide you with hello federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="f0d7c-114"><center>
   ![Indiquer les informations d’identification de connexion](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="f0d7c-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="f0d7c-115">Si votre organisation a configuré l’authentification multifacteur Azure pour joindre tooAzure AD, fournir le second facteur de hello avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-115">If your organization has configured Azure Multi-Factor Authentication for joining tooAzure AD, provide hello second factor before proceeding.</span></span>
6. <span data-ttu-id="f0d7c-116">Cliquez sur **accepter** sur hello **autoriser cette toobe périphérique géré** écran.</span><span class="sxs-lookup"><span data-stu-id="f0d7c-116">Click **Accept** on hello **Allow this device toobe managed** screen.</span></span>
7. <span data-ttu-id="f0d7c-117">Vous devez voir le message de type hello « votre appareil est maintenant organisation jointes tooyour dans Azure AD ».</span><span class="sxs-lookup"><span data-stu-id="f0d7c-117">You should see hello message "Your device is now joined tooyour organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="f0d7c-118">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f0d7c-118">Additional information</span></span>
* [<span data-ttu-id="f0d7c-119">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="f0d7c-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="f0d7c-120">Se connecter tooAzure de périphériques joints au domaine Active Directory pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="f0d7c-120">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="f0d7c-121">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="f0d7c-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="f0d7c-122">Authentification des identités sans mot de passe avec Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="f0d7c-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

