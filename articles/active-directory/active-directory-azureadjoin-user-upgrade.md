---
title: "Configuration d’un appareil Windows 10 avec Azure AD à partir des paramètres | Microsoft Docs"
description: "Explique comment les utilisateurs peuvent rejoindre Azure AD via le menu Paramètres."
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
ms.openlocfilehash: 5a3963f16b471ad1ca8681b22a1a027935400465
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-windows-10-device-with-azure-ad-from-settings"></a><span data-ttu-id="1b265-103">Configuration d’un appareil Windows 10 avec Azure AD à partir des paramètres</span><span class="sxs-lookup"><span data-stu-id="1b265-103">Set up a Windows 10 device with Azure AD from Settings</span></span>
<span data-ttu-id="1b265-104">Si vous utilisez déjà Windows 7 ou Windows 8 et que votre ordinateur ou appareil a été mis à niveau vers Windows 10, vous pouvez le joindre à Azure Active Directory (Azure AD) avec le menu Paramètres.</span><span class="sxs-lookup"><span data-stu-id="1b265-104">If you are already using Windows 7 or Windows 8, and your computer or device has been upgraded to Windows 10, you can join to Azure Active Directory (Azure AD) through the Settings menu.</span></span>

## <a name="to-join-to-azure-ad-from-the-settings-menu"></a><span data-ttu-id="1b265-105">Joindre votre ordinateur à Azure AD à partir du menu Paramètres</span><span class="sxs-lookup"><span data-stu-id="1b265-105">To join to Azure AD from the Settings menu</span></span>
1. <span data-ttu-id="1b265-106">Dans le menu **Démarrer**, cliquez sur l’icône **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="1b265-106">From the **Start** menu, click the **Settings** charm.</span></span>
2. <span data-ttu-id="1b265-107">Accédez à **Paramètres**, sélectionnez **Système**->**Info produit**->**Rejoindre Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="1b265-107">From **Settings**, select     **System**->**About**->**Join Azure AD**.</span></span>
   
   <span data-ttu-id="1b265-108"><center>
   ![Joindre votre ordinateur à Azure AD à partir du menu Paramètres](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span><span class="sxs-lookup"><span data-stu-id="1b265-108"><center>
![Join Azure AD from the Settings menu](./media/active-directory-azureadjoin/active-directory-azureadjoin-settings.png) </center></span></span>
3. <span data-ttu-id="1b265-109">Cliquez sur **Continuer** dans la fenêtre de message Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="1b265-109">Click **Continue** in the Azure AD Join message window.</span></span>
   
   <span data-ttu-id="1b265-110"><center>
   ![Fenêtre de message Joindre Azure AD](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span><span class="sxs-lookup"><span data-stu-id="1b265-110"><center>
![Join Azure AD message window](./media/active-directory-azureadjoin/active-directory-azureadjoin-message.png) </center></span></span>
4. <span data-ttu-id="1b265-111">Indiquez vos informations d’identification de connexion.</span><span class="sxs-lookup"><span data-stu-id="1b265-111">Provide your sign-in credentials.</span></span> <span data-ttu-id="1b265-112">Ce processus de connexion inclut toutes les étapes requises pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="1b265-112">This sign-in experience will include all the steps that are required to complete authentication.</span></span> <span data-ttu-id="1b265-113">Si vous faites partie d’un client fédéré, votre administrateur vous proposera un processus hébergé par votre organisation.</span><span class="sxs-lookup"><span data-stu-id="1b265-113">If you are part of a federated tenant, your administrator will provide you with the federation experience that's hosted by your organization.</span></span>
   <span data-ttu-id="1b265-114"><center>
   ![Indiquer les informations d’identification de connexion](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)</center></span><span class="sxs-lookup"><span data-stu-id="1b265-114"><center>
![Provide sign-in credentials](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png) </center></span></span>
5. <span data-ttu-id="1b265-115">Si votre organisation a configuré Azure Multi-Factor Authentication pour joindre vos appareils à Azure AD, vous devrez fournir le second facteur avant de pouvoir continuer.</span><span class="sxs-lookup"><span data-stu-id="1b265-115">If your organization has configured Azure Multi-Factor Authentication for joining to Azure AD, provide the second factor before proceeding.</span></span>
6. <span data-ttu-id="1b265-116">Cliquez sur **Accepter** sur l’écran **Autoriser la gestion de ce périphérique**.</span><span class="sxs-lookup"><span data-stu-id="1b265-116">Click **Accept** on the **Allow this device to be managed** screen.</span></span>
7. <span data-ttu-id="1b265-117">Le message « Votre appareil est maintenant joint à votre organisation dans Azure AD » doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="1b265-117">You should see the message "Your device is now joined to your organization in Azure AD".</span></span>

## <a name="additional-information"></a><span data-ttu-id="1b265-118">Informations supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1b265-118">Additional information</span></span>
* [<span data-ttu-id="1b265-119">En savoir plus sur les scénarios d’utilisation pour Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="1b265-119">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="1b265-120">Connecter des appareils joints au domaine à Azure AD pour des expériences Windows 10</span><span class="sxs-lookup"><span data-stu-id="1b265-120">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="1b265-121">Configuration d’Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="1b265-121">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
* [<span data-ttu-id="1b265-122">Authentification des identités sans mot de passe avec Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="1b265-122">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)

