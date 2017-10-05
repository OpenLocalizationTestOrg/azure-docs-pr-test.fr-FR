---
title: "Comment gérer les paramètres d’activation de rôle | Microsoft Docs"
description: "Découvrez comment modifier les paramètres par défaut d’identités privilégiées avec l’extension Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="83b6f-103">Comment gérer les paramètres d'activation de rôle dans Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="83b6f-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="83b6f-104">Un administrateur de rôle privilégié peut personnaliser Azure AD Privileged Identity Management (PIM) dans son organisation, notamment modifier l’expérience d’un utilisateur qui active une attribution de rôle éligible.</span><span class="sxs-lookup"><span data-stu-id="83b6f-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="83b6f-105">Gérer les paramètres d'activation de rôle</span><span class="sxs-lookup"><span data-stu-id="83b6f-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="83b6f-106">Accédez à la [portail Azure](https://portal.azure.com) et sélectionnez l’application **Azure AD Privileged Identity Management** à partir du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="83b6f-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="83b6f-107">Sélectionnez **Gérer les rôles privilégiés** > **Paramètres** > **Rôles privilégiés**.</span><span class="sxs-lookup"><span data-stu-id="83b6f-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="83b6f-108">Choisissez le rôle dont vous souhaitez gérer les paramètres.</span><span class="sxs-lookup"><span data-stu-id="83b6f-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="83b6f-109">Sur la page des paramètres de chaque rôle, vous pouvez configurer plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="83b6f-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="83b6f-110">Ces paramètres affectent uniquement les utilisateurs qui sont des administrateurs éligibles et non des administrateurs permanents.</span><span class="sxs-lookup"><span data-stu-id="83b6f-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="83b6f-111">**Activations**: durée, en heures, pendant laquelle un rôle reste actif avant d’expirer.</span><span class="sxs-lookup"><span data-stu-id="83b6f-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="83b6f-112">Cette durée peut être comprise entre 1 et 72 heures.</span><span class="sxs-lookup"><span data-stu-id="83b6f-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="83b6f-113">**Notifications**: vous pouvez choisir si le système envoie ou non des messages électroniques aux administrateurs pour leur confirmer qu’ils ont activé un rôle.</span><span class="sxs-lookup"><span data-stu-id="83b6f-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="83b6f-114">Cette option peut être utile pour détecter les activations non autorisées ou illégitimes.</span><span class="sxs-lookup"><span data-stu-id="83b6f-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="83b6f-115">**Ticket d’incident/demande**: vous pouvez choisir si les administrateurs admissibles doivent ou non inclure un numéro de ticket lorsqu’ils activent leur rôle.</span><span class="sxs-lookup"><span data-stu-id="83b6f-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="83b6f-116">Cela peut être utile lorsque vous effectuez des audits d’accès à un rôle.</span><span class="sxs-lookup"><span data-stu-id="83b6f-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="83b6f-117">**Authentification multifacteur**: vous pouvez choisir si les utilisateurs doivent ou non vérifier leur identité via l’authentification multifacteur avant de pouvoir activer leurs rôles.</span><span class="sxs-lookup"><span data-stu-id="83b6f-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="83b6f-118">Une seule vérification est nécessaire par session, et non chaque fois qu’ils ont activé un rôle.</span><span class="sxs-lookup"><span data-stu-id="83b6f-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="83b6f-119">Il existe deux conseils à garder à l’esprit lorsque vous activez l’authentification multifacteur :</span><span class="sxs-lookup"><span data-stu-id="83b6f-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="83b6f-120">Les utilisateurs qui disposent de comptes Microsoft pour leurs adresses de messagerie (généralement @outlook.com, mais pas toujours) ne peut pas inscrire pour Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="83b6f-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="83b6f-121">Si vous souhaitez attribuer des rôles aux utilisateurs disposant de comptes Microsoft, vous devez les rendre administrateurs permanents ou désactiver l’authentification multifacteur pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="83b6f-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="83b6f-122">Vous ne pouvez pas désactiver l’authentification multifacteur pour les rôles à privilèges élevés pour Azure AD et Office 365.</span><span class="sxs-lookup"><span data-stu-id="83b6f-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="83b6f-123">Il s’agit d’une fonctionnalité de sécurité car ces rôles doivent être soigneusement protégés :</span><span class="sxs-lookup"><span data-stu-id="83b6f-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="83b6f-124">Administrateur d’application</span><span class="sxs-lookup"><span data-stu-id="83b6f-124">Application administrator</span></span>
  * <span data-ttu-id="83b6f-125">Administrateur du serveur proxy d’application</span><span class="sxs-lookup"><span data-stu-id="83b6f-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="83b6f-126">Administrateur de facturation</span><span class="sxs-lookup"><span data-stu-id="83b6f-126">Billing administrator</span></span>  
  * <span data-ttu-id="83b6f-127">Administrateur de conformité</span><span class="sxs-lookup"><span data-stu-id="83b6f-127">Compliance administrator</span></span>  
  * <span data-ttu-id="83b6f-128">Administrateur de services CRM</span><span class="sxs-lookup"><span data-stu-id="83b6f-128">CRM service administrator</span></span>
  * <span data-ttu-id="83b6f-129">Approbateur d’accès au référentiel sécurisé client</span><span class="sxs-lookup"><span data-stu-id="83b6f-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="83b6f-130">Enregistreur de répertoire</span><span class="sxs-lookup"><span data-stu-id="83b6f-130">Directory writer</span></span>  
  * <span data-ttu-id="83b6f-131">Administrateur Exchange</span><span class="sxs-lookup"><span data-stu-id="83b6f-131">Exchange administrator</span></span>  
  * <span data-ttu-id="83b6f-132">Administrateur général</span><span class="sxs-lookup"><span data-stu-id="83b6f-132">Global administrator</span></span>
  * <span data-ttu-id="83b6f-133">Administrateur de services Intune</span><span class="sxs-lookup"><span data-stu-id="83b6f-133">Intune service administrator</span></span>
  * <span data-ttu-id="83b6f-134">Administrateur de boîte aux lettres</span><span class="sxs-lookup"><span data-stu-id="83b6f-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="83b6f-135">Prise en charge de niveau 1 de partenaire</span><span class="sxs-lookup"><span data-stu-id="83b6f-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="83b6f-136">Prise en charge de niveau 2 de partenaire</span><span class="sxs-lookup"><span data-stu-id="83b6f-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="83b6f-137">Administrateur de rôle privilégié</span><span class="sxs-lookup"><span data-stu-id="83b6f-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="83b6f-138">Administrateur de sécurité</span><span class="sxs-lookup"><span data-stu-id="83b6f-138">Security administrator</span></span>  
  * <span data-ttu-id="83b6f-139">Administrateur SharePoint</span><span class="sxs-lookup"><span data-stu-id="83b6f-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="83b6f-140">Administrateur Skype Entreprise</span><span class="sxs-lookup"><span data-stu-id="83b6f-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="83b6f-141">Administrateur de compte d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="83b6f-141">User account administrator</span></span>  

<span data-ttu-id="83b6f-142">Pour plus d’informations sur l’utilisation de la solution MFA avec Privileged Identity Management, voir [Exigence de l’application de la solution MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="83b6f-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="83b6f-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="83b6f-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

