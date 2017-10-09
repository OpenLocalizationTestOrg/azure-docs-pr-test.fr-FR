---
title: "aaaManage tooAzure de l’accès à l’aide de rôles de facturation | Documents Microsoft"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="3b218-102">Gérer les informations de toobilling d’accès pour Azure à l’aide du contrôle d’accès basé sur un rôle</span><span class="sxs-lookup"><span data-stu-id="3b218-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="3b218-103">Vous pouvez accorder l’accès pour Azure toomembers informations facturation de votre équipe en affectant une des hello suivant abonnement tooyour de rôles utilisateur : administrateur de compte, administrateur de Service, coadministrateur, propriétaire, collaborateur, lecteur et lecteur de facturation.</span><span class="sxs-lookup"><span data-stu-id="3b218-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="3b218-104">Ils auraient pas accès toobilling informations Bonjour [portail Azure](https://portal.azure.com/), et ils peuvent utiliser hello [API de facturation](billing-usage-rate-card-overview.md) tooprogrammatically obtenir factures (une fois choisi-entrant) et les détails d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3b218-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="3b218-105">Pour plus d’informations sur les utilisateurs pouvant accorder des rôles, et sur ce que les rôles permettent de faire, consultez [Rôles dans Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="3b218-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="3b218-106"><a name="opt-in"></a>Autoriser des utilisateurs supplémentaires tooaccess factures</span><span class="sxs-lookup"><span data-stu-id="3b218-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="3b218-107">Hello administrateur de compte doit s’abonner à l’aide de hello [portail Azure](https://portal.azure.com/) autoriser l’accès tooinvoices pour d’autres utilisateurs et via l’API.</span><span class="sxs-lookup"><span data-stu-id="3b218-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="3b218-108">Comme hello administrateur de compte, sélectionnez votre abonnement à partir de hello [panneau d’abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3b218-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="3b218-109">Sélectionnez **factures** , puis **tooinvoices d’accès**.</span><span class="sxs-lookup"><span data-stu-id="3b218-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Capture d’écran montre comment accéder à tooinvoices toodelegate](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="3b218-111">Activer **sur** les accès hello suivie de l’enregistrement des modifications de hello, tooallow des utilisateurs dans l’abonnement rôles étendus toodownload facture.</span><span class="sxs-lookup"><span data-stu-id="3b218-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Capture d’écran montre marche / arrêt toodelegate accès tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="3b218-113">Si vous activez permet d’administrateur de Service, coadministrateur, propriétaire, collaborateur, lecteur et de facturation de lecteur sur les factures PDF hello abonnement toodownload Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3b218-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="3b218-114">Toutefois, les factures antérieures à 2016 de décembre sont toohello uniquement disponible administrateur de compte pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="3b218-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="3b218-115">Hello administrateur de compte peut également configurer toohave les factures envoyées par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="3b218-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="3b218-116">toolearn, voir [obtenir votre facture par courrier électronique](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="3b218-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="3b218-117">Ajout de rôle de lecteur de facturation toohello utilisateurs</span><span class="sxs-lookup"><span data-stu-id="3b218-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="3b218-118">rôle de lecteur de facturation Hello dispose d’informations de facturation toosubscription accès en lecture seule dans le portail Azure et aucun tooservices accès tels que les machines virtuelles et les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="3b218-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="3b218-119">Affecter toosomeone de rôle de lecteur de facturation hello qui doit accéder aux informations de facturation toohello mais pas hello capacité toomanage Azure services.</span><span class="sxs-lookup"><span data-stu-id="3b218-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="3b218-120">Ce rôle convient aux utilisateurs d’une organisation qui procèdent uniquement à la gestion financière et des coûts pour des abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="3b218-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="3b218-121">Sélectionnez votre abonnement à partir de hello [panneau d’abonnements](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3b218-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="3b218-122">Sélectionnez **Contrôle d’accès (IAM)**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="3b218-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Capture d’écran montre IAM dans le panneau d’abonnement hello](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="3b218-124">Choisissez **lecteur de facturation** Bonjour **sélectionner un rôle** page.</span><span class="sxs-lookup"><span data-stu-id="3b218-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Capture d’écran montre la facturation de lecteur dans la vue de fenêtre contextuelle hello](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="3b218-126">Type de messagerie hello pour utilisateur hello souhaité tooinvite, puis cliquez sur **OK** invitation de hello toosend.</span><span class="sxs-lookup"><span data-stu-id="3b218-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Capture d’écran tooenter messagerie tooinvite une personne](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="3b218-128">Suivez les instructions de toolog de courrier électronique d’invitation hello dans comme un lecteur de facturation.</span><span class="sxs-lookup"><span data-stu-id="3b218-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Capture d’écran que hello du lecteur de facturation peut voir dans le portail Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="3b218-130">fonctionnalité de lecteur de facturation Hello est en version préliminaire et ne prend pas en charge les abonnements de l’entreprise (EA) ou non globale clouds.</span><span class="sxs-lookup"><span data-stu-id="3b218-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="3b218-131">Ajout de rôles d’utilisateurs tooother</span><span class="sxs-lookup"><span data-stu-id="3b218-131">Adding users tooother roles</span></span>

<span data-ttu-id="3b218-132">Les utilisateurs d’autres rôles, tels que Propriétaire ou Collaborateur, peuvent non seulement accéder aux informations de facturation, mais également à des services Azure.</span><span class="sxs-lookup"><span data-stu-id="3b218-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="3b218-133">toomanage ces rôles, consultez [ajouter ou modifier les rôles administrateur Azure qui gèrent les abonnement hello ou services](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="3b218-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="3b218-134">Qui peut accéder à hello [centre des comptes](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="3b218-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="3b218-135">Centre des comptes toohello pouvez vous connecter uniquement hello administrateur de compte.</span><span class="sxs-lookup"><span data-stu-id="3b218-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="3b218-136">Hello administrateur de compte est propriétaire légal de hello d’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="3b218-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="3b218-137">Par défaut, hello personne inscrit ou acheté hello abonnement Azure est hello administrateur de compte, à moins que hello [la propriété d’abonnement a été transférée](billing-subscription-transfer.md) toosomebody else.</span><span class="sxs-lookup"><span data-stu-id="3b218-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="3b218-138">Hello administrateur de compte peut créer des abonnements, annuler les abonnements, modifiez l’adresse de facturation hello pour un abonnement et gérer les stratégies d’accès pour l’abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="3b218-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="3b218-139">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="3b218-139">Need help?</span></span> <span data-ttu-id="3b218-140">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="3b218-140">Contact support.</span></span>

<span data-ttu-id="3b218-141">Si vous en avez d’autres questions, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.</span><span class="sxs-lookup"><span data-stu-id="3b218-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
