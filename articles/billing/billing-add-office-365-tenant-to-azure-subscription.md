---
title: client aaaUse un Office 365 avec un abonnement Azure | Documents Microsoft
description: "Découvrez comment tooadd un Office 365 directory (locataire) tooan abonnement Azure."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="87c72-103">Associer un tooan du locataire Office 365 abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="87c72-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="87c72-104">Lier vos abonnements Azure et Office 365 distincts afin que vous pouvez accéder à des clients de hello Office 365 à partir de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="87c72-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="87c72-105">toolink vos abonnements, connectez-vous tooAzure avec hello compte d’administrateur de service Azure, ajoutez un répertoire et ajout d’un locataire Azure Active Directory de hello Office 365 comptes professionnels toohello.</span><span class="sxs-lookup"><span data-stu-id="87c72-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="87c72-106">Si vous souhaitez un abonnement Office 365 pour les utilisateurs de votre instance d’Azure Active Directory ou que vous possédez un compte Office 365, mais pas un compte Azure, consultez [Inscription à Azure avec un compte Office 365](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="87c72-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="87c72-107">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="87c72-107">Before you begin</span></span>
* <span data-ttu-id="87c72-108">Vous devez disposer des informations d’identification de hello d’administrateur de service d’abonnement Azure hello.</span><span class="sxs-lookup"><span data-stu-id="87c72-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="87c72-109">Comptes de coadministrateurs ne peut pas effectuer une partie des étapes hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="87c72-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="87c72-110">toochange votre administrateur de service, consultez [comment tooadd ou modifier les rôles administrateur Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="87c72-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="87c72-111">Vous devez disposer des informations d’identification hello d’un administrateur général du client Office 365 de hello.</span><span class="sxs-lookup"><span data-stu-id="87c72-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="87c72-112">adresse de messagerie Hello d’administrateur de service hello ne doit pas être dans le client Office 365 de hello.</span><span class="sxs-lookup"><span data-stu-id="87c72-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="87c72-113">adresse de messagerie Hello d’administrateur de service hello ne doit pas correspondre à celui de n’importe quel administrateur général du client de hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="87c72-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="87c72-114">Si vous utilisez une adresse de messagerie qui est un compte Microsoft et un compte professionnel, modifier temporairement hello administrateur de services fédérés de votre abonnement Azure de toouse un autre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="87c72-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="87c72-115">Vous pouvez créer un compte Microsoft à hello [page d’abonnement de compte Microsoft](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="87c72-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="87c72-116">Lier un abonnement de tooAzure locataire Office 365</span><span class="sxs-lookup"><span data-stu-id="87c72-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="87c72-117">tooassociate hello Office 365 client toohello abonnement Azure, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="87c72-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="87c72-118">Étape 1 : Ajouter Office 365 client tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="87c72-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="87c72-119">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) avec les informations d’identification d’administrateur de service hello.</span><span class="sxs-lookup"><span data-stu-id="87c72-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Capture d’écran de la connexion à Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="87c72-121">Dans le volet gauche de hello, sélectionnez **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="87c72-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="87c72-122">Vous ne doit pas voir les locataire hello Office 365.</span><span class="sxs-lookup"><span data-stu-id="87c72-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="87c72-123">Si vous le voyez pas, passez trop[étape 2 : modifier le répertoire hello associé hello abonnement Azure](#Step2).</span><span class="sxs-lookup"><span data-stu-id="87c72-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Capture d’écran de l’entrée Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="87c72-125">Sélectionnez **NOUVEAU** > **ANNUAIRE** > **CRÉATION PERSONNALISÉE**.</span><span class="sxs-lookup"><span data-stu-id="87c72-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Capture d’écran de la création personnalisée Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="87c72-127">Sur hello **ajouter un annuaire** sous **active**, sélectionnez **utiliser un annuaire existant**.</span><span class="sxs-lookup"><span data-stu-id="87c72-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="87c72-128">Puis sélectionnez **je suis prêt toobe me déconnecter**, puis sélectionnez **Complete** ![icône Terminer](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="87c72-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Capture d’écran de « Utiliser un annuaire existant »](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="87c72-130">Une fois que vous êtes déconnecté, connectez-vous avec les informations d’identification de l’administrateur global hello de votre client Office 365.</span><span class="sxs-lookup"><span data-stu-id="87c72-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Capture d’écran de la connexion d’administrateur général Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="87c72-132">Sélectionnez **Continuer**.</span><span class="sxs-lookup"><span data-stu-id="87c72-132">Select **Continue**.</span></span>
   
    ![Capture d’écran de vérification](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="87c72-134">Sélectionnez **Se déconnecter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="87c72-134">Select **Sign out now**.</span></span>
   
    ![Capture d’écran de la déconnexion](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="87c72-136">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) avec les informations d’identification d’administrateur de service hello.</span><span class="sxs-lookup"><span data-stu-id="87c72-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Capture d’écran de la connexion à Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="87c72-138">Vous devez voir votre client Office 365 dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="87c72-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![Capture d’écran du tableau de bord](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="87c72-140"><a name="Step2"></a>Étape 2 : Modifier le répertoire hello associé hello abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="87c72-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="87c72-141">Sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="87c72-141">Select **Settings**.</span></span>
   
    ![Capture d’écran de l’icône des paramètres du portail Azure Classic](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="87c72-143">Sélectionnez votre abonnement Azure, puis sélectionnez **MODIFIER L’ANNUAIRE**.</span><span class="sxs-lookup"><span data-stu-id="87c72-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Capture d’écran Modifier l’annuaire de l’abonnement Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="87c72-145">Sélectionnez **Suivant** ![Icône Suivant](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="87c72-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Capture d’écran de « Modification hello annuaire associé »](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="87c72-147">Passez en revue les comptes hello affectée.</span><span class="sxs-lookup"><span data-stu-id="87c72-147">Review hello affected accounts.</span></span> <span data-ttu-id="87c72-148">Tous les coadministrateurs et [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md) utilisateurs avec accès assigné à dans les groupes de ressources existant hello sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="87c72-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="87c72-149">Hello qui vous avertissent mentionne uniquement la suppression de hello de coadministrateurs.</span><span class="sxs-lookup"><span data-stu-id="87c72-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![Capture d’écran hello comptes de coadministrateurs toobe supprimé.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Capture d’écran présentant un toobe de compte d’utilisateur exemple supprimé.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="87c72-152">Sélectionnez **Terminer** ![icône Terminer](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="87c72-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="87c72-153">Étape 3 : Ajoutez votre compte professionnel Office 365 en tant que client de coadministrateurs toohello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="87c72-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="87c72-154">Sélectionnez hello **administrateurs** onglet, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="87c72-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Capture d’écran de l’onglet Administrateurs dans les paramètres du portail Azure Classic](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="87c72-156">Entrez un compte de société de votre client Office 365, sélectionnez hello abonnement Azure, puis **Complete** ![icône Terminer](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="87c72-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Capture d’écran de la boîte de dialogue d’ajout de coadministrateur Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="87c72-158">Revenir en arrière toohello **administrateurs** onglet. Vous devez voir le compte de société hello affiché en tant que coadministrateur.</span><span class="sxs-lookup"><span data-stu-id="87c72-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![Capture d’écran de l’onglet Administrateurs](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="87c72-160">TooAzure d’accès de test avec un compte de coadministrateur hello.</span><span class="sxs-lookup"><span data-stu-id="87c72-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="87c72-161">a.</span><span class="sxs-lookup"><span data-stu-id="87c72-161">a.</span></span> <span data-ttu-id="87c72-162">Déconnectez-vous hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="87c72-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="87c72-163">b.</span><span class="sxs-lookup"><span data-stu-id="87c72-163">b.</span></span> <span data-ttu-id="87c72-164">Ouvrez hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="87c72-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="87c72-165">c.</span><span class="sxs-lookup"><span data-stu-id="87c72-165">c.</span></span> <span data-ttu-id="87c72-166">Entrez les informations d’identification hello de coadministrateur hello et sélectionnez **connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="87c72-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Capture d’écran de la page de connexion à Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="87c72-168">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="87c72-168">Need help?</span></span> <span data-ttu-id="87c72-169">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="87c72-169">Contact support.</span></span>
<span data-ttu-id="87c72-170">Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.</span><span class="sxs-lookup"><span data-stu-id="87c72-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


