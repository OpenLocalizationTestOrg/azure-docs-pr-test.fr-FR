---
title: "S’inscrire à Office 365 avec un compte Azure | Microsoft Docs"
description: "Apprenez à créer un abonnement à Office 365 avec un compte Azure."
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: 1c6e277e321980aaf30f821dbb41c7eaf296b4cf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a><span data-ttu-id="fca86-103">Souscrire un abonnement Office 365 avec un compte Azure</span><span class="sxs-lookup"><span data-stu-id="fca86-103">Sign up for an Office 365 subscription with your Azure account</span></span>
<span data-ttu-id="fca86-104">Si vous êtes abonné à Azure, vous pouvez utiliser votre compte Azure pour souscrire un abonnement Office 365.</span><span class="sxs-lookup"><span data-stu-id="fca86-104">If you're Azure subscriber, you can use your Azure account to sign up for an Office 365 subscription.</span></span> <span data-ttu-id="fca86-105">Si vous faites partie d’une organisation qui a un abonnement Azure, vous pouvez créer des abonnements Office 365 pour les utilisateurs dans votre instance Azure Active Directory (Azure AD) existante.</span><span class="sxs-lookup"><span data-stu-id="fca86-105">If you're part of an organization that has an Azure subscription, you can create Office 365 subscriptions for users in your existing Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fca86-106">Inscrivez-vous à Office 365 avec un compte détenant les autorisations Administrateur général ou Administrateur de facturation dans votre locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fca86-106">Sign up to Office 365 using an account that has Global Admin or Billing Admin permissions in your Azure Active Directory tenant.</span></span> <span data-ttu-id="fca86-107">Pour plus d’informations, consultez les pages [Vérifier mes autorisations de compte dans Azure AD](#RoleInAzureAD) et [Attribution de rôles d’administrateur dans Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="fca86-107">For more information, see [Check my account permissions in Azure AD](#RoleInAzureAD) and [Assigning administrator roles in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="fca86-108">Si vous avez déjà à la fois un compte Office 365 et un abonnement Azure, vous pouvez [associer un locataire Office 365 à un abonnement Azure](billing-add-office-365-tenant-to-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="fca86-108">If you already have both an Office 365 account and an Azure subscription, you can [Associate an Office 365 tenant to an Azure subscription](billing-add-office-365-tenant-to-azure-subscription.md).</span></span>

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a><span data-ttu-id="fca86-109">Obtenir un abonnement Office 365 avec un compte Azure</span><span class="sxs-lookup"><span data-stu-id="fca86-109">Get an Office 365 subscription by using your Azure account</span></span>

1. <span data-ttu-id="fca86-110">Accédez à la [page de produit Office 365](https://products.office.com/business), puis sélectionnez un plan.</span><span class="sxs-lookup"><span data-stu-id="fca86-110">Go to the [Office 365 product page](https://products.office.com/business), and select a plan.</span></span>
2. <span data-ttu-id="fca86-111">Cliquez sur **Se connecter** dans le coin supérieur droit de la page.</span><span class="sxs-lookup"><span data-stu-id="fca86-111">Click **Sign in** on the upper-right corner of the page.</span></span>

    ![Capture d’écran de la page d’essai d’Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. <span data-ttu-id="fca86-113">Connectez-vous avec les informations d’identification de votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="fca86-113">Sign in with your Azure account credentials.</span></span> <span data-ttu-id="fca86-114">Si vous avez créé un abonnement pour votre organisation, utilisez un compte Azure membre du rôle de répertoire Administrateur général ou Administrateur de facturation dans votre client Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fca86-114">If you're creating a subscription for your organization, use an Azure account that's a member of the Global Admin or Billing Admin directory role in your Azure Active Directory tenant.</span></span>

    ![Capture d’écran de la connexion à Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. <span data-ttu-id="fca86-116">Cliquez sur **Essayez dès maintenant**.</span><span class="sxs-lookup"><span data-stu-id="fca86-116">Click **Try now**.</span></span>

    ![Capture d’écran confirmant votre commande d’Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. <span data-ttu-id="fca86-118">Sur la page du reçu de la commande, cliquez sur **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="fca86-118">On the order receipt page, click **Continue**.</span></span>

    ![Capture d’écran de la réception de la commande d’Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

<span data-ttu-id="fca86-120">Vous êtes prêt.</span><span class="sxs-lookup"><span data-stu-id="fca86-120">Now you're all set.</span></span> <span data-ttu-id="fca86-121">Si vous avez créé l’abonnement Office 365 pour votre organisation, suivez les étapes ci-dessous pour vérifier que vos utilisateurs Azure AD sont maintenant dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="fca86-121">If you created the Office 365 subscription for your organization, use the following steps to check that your Azure AD users are now in Office 365.</span></span>

1. <span data-ttu-id="fca86-122">Ouvrez le centre d’administration Office 365.</span><span class="sxs-lookup"><span data-stu-id="fca86-122">Open the Office 365 admin center.</span></span>
2. <span data-ttu-id="fca86-123">Développez la section **UTILISATEURS**, puis cliquez sur **Utilisateurs actifs**.</span><span class="sxs-lookup"><span data-stu-id="fca86-123">Expand **USERS**, and then click **Active Users**.</span></span>

    ![Capture d’écran des utilisateurs du centre d’administration Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

<span data-ttu-id="fca86-125">Une fois que vous êtes inscrit, l’abonnement à Office 365 est ajouté à l’instance Azure Active Directory à laquelle votre abonnement Azure appartient.</span><span class="sxs-lookup"><span data-stu-id="fca86-125">After you sign up, the Office 365 subscription is added to the same Azure Active Directory instance that your Azure subscription belongs to.</span></span> <span data-ttu-id="fca86-126">Pour plus d’informations, consultez les pages [En savoir plus sur les abonnements Azure et Office 365](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) et [Association des abonnements Azure avec Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="fca86-126">For more information, see [More about Azure and Office 365 subscriptions](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) and [How Azure subscriptions are associated with Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <span data-ttu-id="fca86-127"><a id="RoleInAzureAD"></a>Vérifier mes autorisations de compte dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="fca86-127"><a id="RoleInAzureAD"></a>Check my account permissions in Azure AD</span></span>
1. <span data-ttu-id="fca86-128">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fca86-128">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fca86-129">Cliquez sur **Plus de services**, puis recherchez **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fca86-129">Click **More services**, and then search for **Active Directory**.</span></span>

    ![Capture d’écran d’Active Directory sur le Portail Azure.](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. <span data-ttu-id="fca86-131">Cliquez sur**Utilisateurs et groupes** > **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="fca86-131">Click **Users and groups** > **All users**.</span></span>
4. <span data-ttu-id="fca86-132">Sélectionnez le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fca86-132">Select the user name.</span></span> 

    ![Capture d’écran montrant les utilisateurs d’Azure Active Directory.](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. <span data-ttu-id="fca86-134">Cliquez sur **Rôle de répertoire**.</span><span class="sxs-lookup"><span data-stu-id="fca86-134">Click **Directory role**.</span></span>
  
    ![Capture d’écran montrant le rôle de répertoire du Portail Azure.](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  <span data-ttu-id="fca86-136">Le rôle **Administrateur global** ou **Administrateur limité** > **Administrateur de facturation** est requis pour créer un abonnement Office 365 pour les utilisateurs dans votre instance d’Azure Active Directory existante.</span><span class="sxs-lookup"><span data-stu-id="fca86-136">The role **Global administrator** or **Limited administrator** > **Billing administrator** is required to create an Office 365 subscription for users in your existing Azure Active Directory.</span></span>

    ![Capture d’écran montrant le rôle de répertoire Administrateur de facturation du Portail Azure.](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="fca86-138">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="fca86-138">Need help?</span></span> <span data-ttu-id="fca86-139">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="fca86-139">Contact support.</span></span>
<span data-ttu-id="fca86-140">Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour obtenir une prise en charge rapide de votre problème.</span><span class="sxs-lookup"><span data-stu-id="fca86-140">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span> 
