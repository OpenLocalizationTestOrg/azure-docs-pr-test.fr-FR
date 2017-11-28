---
title: "paramètres de l’activation du rôle aaaHow toomanage | Documents Microsoft"
description: "Découvrez comment toochange hello les paramètres par défaut pour les identités privilégiées avec hello extension d’Azure Active Directory Privileged Identity Management."
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
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="3eb89-103">Comment les paramètres de l’activation de rôle toomanage dans Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="3eb89-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="3eb89-104">Un administrateur de rôle privilégié peut personnaliser Azure AD Privileged Identity Management (PIM) dans leur organisation, notamment en modifiant l’expérience hello pour un utilisateur qui est d’activer une attribution de rôle éligible.</span><span class="sxs-lookup"><span data-stu-id="3eb89-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="3eb89-105">Gérer les paramètres de l’activation de rôle hello</span><span class="sxs-lookup"><span data-stu-id="3eb89-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="3eb89-106">Accédez toohello [portail Azure](https://portal.azure.com) et sélectionnez hello **Azure AD Privileged Identity Management** application à partir du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="3eb89-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="3eb89-107">Sélectionnez **Gérer les rôles privilégiés** > **Paramètres** > **Rôles privilégiés**.</span><span class="sxs-lookup"><span data-stu-id="3eb89-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="3eb89-108">Choisissez le rôle de hello dont les paramètres souhaités toomanage.</span><span class="sxs-lookup"><span data-stu-id="3eb89-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="3eb89-109">Sur la page de paramètres hello pour chaque rôle, il existe un nombre de paramètres que vous pouvez configurer.</span><span class="sxs-lookup"><span data-stu-id="3eb89-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="3eb89-110">Ces paramètres affectent uniquement les utilisateurs qui sont des administrateurs éligibles et non des administrateurs permanents.</span><span class="sxs-lookup"><span data-stu-id="3eb89-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="3eb89-111">**Les activations**: hello durée, en heures, pendant laquelle un rôle reste actif avant son expiration.</span><span class="sxs-lookup"><span data-stu-id="3eb89-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="3eb89-112">Cette durée peut être comprise entre 1 et 72 heures.</span><span class="sxs-lookup"><span data-stu-id="3eb89-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="3eb89-113">**Notifications**: vous pouvez choisir ou non système de hello envoie tooadmins e-mails confirmant qu’ils ont activé un rôle.</span><span class="sxs-lookup"><span data-stu-id="3eb89-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="3eb89-114">Cette option peut être utile pour détecter les activations non autorisées ou illégitimes.</span><span class="sxs-lookup"><span data-stu-id="3eb89-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="3eb89-115">**Ticket d’incident/demande**: vous pouvez choisir ou non toorequire administrateurs éligibles tooinclude un ticket de numéro de leur activation de leur rôle.</span><span class="sxs-lookup"><span data-stu-id="3eb89-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="3eb89-116">Cela peut être utile lorsque vous effectuez des audits d’accès à un rôle.</span><span class="sxs-lookup"><span data-stu-id="3eb89-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="3eb89-117">**L’authentification multifacteur**: vous pouvez choisir ou non toorequire utilisateurs tooverify leur identité avec l’authentification Multifacteur, avant de pouvoir activer leurs rôles.</span><span class="sxs-lookup"><span data-stu-id="3eb89-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="3eb89-118">Ils ont uniquement tooverify ce qu’une seule fois par session, pas chaque fois qu’ils activer un rôle.</span><span class="sxs-lookup"><span data-stu-id="3eb89-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="3eb89-119">Il existe deux tookeep de conseils à l’esprit lorsque vous activez l’authentification Multifacteur :</span><span class="sxs-lookup"><span data-stu-id="3eb89-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="3eb89-120">Les utilisateurs qui disposent de comptes Microsoft pour leurs adresses de messagerie (généralement @outlook.com, mais pas toujours) ne peut pas inscrire pour Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="3eb89-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="3eb89-121">Si vous souhaitez toousers de rôles tooassign avec des comptes Microsoft, vous devez les rendre administrateurs permanents ou désactiver l’authentification Multifacteur pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="3eb89-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="3eb89-122">Vous ne pouvez pas désactiver l’authentification multifacteur pour les rôles à privilèges élevés pour Azure AD et Office 365.</span><span class="sxs-lookup"><span data-stu-id="3eb89-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="3eb89-123">Il s’agit d’une fonctionnalité de sécurité car ces rôles doivent être soigneusement protégés :</span><span class="sxs-lookup"><span data-stu-id="3eb89-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="3eb89-124">Administrateur d’application</span><span class="sxs-lookup"><span data-stu-id="3eb89-124">Application administrator</span></span>
  * <span data-ttu-id="3eb89-125">Administrateur du serveur proxy d’application</span><span class="sxs-lookup"><span data-stu-id="3eb89-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="3eb89-126">Administrateur de facturation</span><span class="sxs-lookup"><span data-stu-id="3eb89-126">Billing administrator</span></span>  
  * <span data-ttu-id="3eb89-127">Administrateur de conformité</span><span class="sxs-lookup"><span data-stu-id="3eb89-127">Compliance administrator</span></span>  
  * <span data-ttu-id="3eb89-128">Administrateur de services CRM</span><span class="sxs-lookup"><span data-stu-id="3eb89-128">CRM service administrator</span></span>
  * <span data-ttu-id="3eb89-129">Approbateur d’accès au référentiel sécurisé client</span><span class="sxs-lookup"><span data-stu-id="3eb89-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="3eb89-130">Enregistreur de répertoire</span><span class="sxs-lookup"><span data-stu-id="3eb89-130">Directory writer</span></span>  
  * <span data-ttu-id="3eb89-131">Administrateur Exchange</span><span class="sxs-lookup"><span data-stu-id="3eb89-131">Exchange administrator</span></span>  
  * <span data-ttu-id="3eb89-132">Administrateur général</span><span class="sxs-lookup"><span data-stu-id="3eb89-132">Global administrator</span></span>
  * <span data-ttu-id="3eb89-133">Administrateur de services Intune</span><span class="sxs-lookup"><span data-stu-id="3eb89-133">Intune service administrator</span></span>
  * <span data-ttu-id="3eb89-134">Administrateur de boîte aux lettres</span><span class="sxs-lookup"><span data-stu-id="3eb89-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="3eb89-135">Prise en charge de niveau 1 de partenaire</span><span class="sxs-lookup"><span data-stu-id="3eb89-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="3eb89-136">Prise en charge de niveau 2 de partenaire</span><span class="sxs-lookup"><span data-stu-id="3eb89-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="3eb89-137">Administrateur de rôle privilégié</span><span class="sxs-lookup"><span data-stu-id="3eb89-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="3eb89-138">Administrateur de sécurité</span><span class="sxs-lookup"><span data-stu-id="3eb89-138">Security administrator</span></span>  
  * <span data-ttu-id="3eb89-139">Administrateur SharePoint</span><span class="sxs-lookup"><span data-stu-id="3eb89-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="3eb89-140">Administrateur Skype Entreprise</span><span class="sxs-lookup"><span data-stu-id="3eb89-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="3eb89-141">Administrateur de compte d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="3eb89-141">User account administrator</span></span>  

<span data-ttu-id="3eb89-142">Pour plus d’informations sur l’utilisation de l’authentification Multifacteur avec PIM consultez [comment tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="3eb89-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="3eb89-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3eb89-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

