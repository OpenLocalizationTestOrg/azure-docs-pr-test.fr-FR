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
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>Associer un tooan du locataire Office 365 abonnement Azure
Lier vos abonnements Azure et Office 365 distincts afin que vous pouvez accéder à des clients de hello Office 365 à partir de votre abonnement Azure. toolink vos abonnements, connectez-vous tooAzure avec hello compte d’administrateur de service Azure, ajoutez un répertoire et ajout d’un locataire Azure Active Directory de hello Office 365 comptes professionnels toohello.

Si vous souhaitez un abonnement Office 365 pour les utilisateurs de votre instance d’Azure Active Directory ou que vous possédez un compte Office 365, mais pas un compte Azure, consultez [Inscription à Azure avec un compte Office 365](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Avant de commencer
* Vous devez disposer des informations d’identification de hello d’administrateur de service d’abonnement Azure hello. Comptes de coadministrateurs ne peut pas effectuer une partie des étapes hello dans cet article. toochange votre administrateur de service, consultez [comment tooadd ou modifier les rôles administrateur Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* Vous devez disposer des informations d’identification hello d’un administrateur général du client Office 365 de hello.
* adresse de messagerie Hello d’administrateur de service hello ne doit pas être dans le client Office 365 de hello.
* adresse de messagerie Hello d’administrateur de service hello ne doit pas correspondre à celui de n’importe quel administrateur général du client de hello Office 365.
* Si vous utilisez une adresse de messagerie qui est un compte Microsoft et un compte professionnel, modifier temporairement hello administrateur de services fédérés de votre abonnement Azure de toouse un autre compte Microsoft. Vous pouvez créer un compte Microsoft à hello [page d’abonnement de compte Microsoft](https://signup.live.com/).

## <a name="link-office-365-tenant-tooazure-subscription"></a>Lier un abonnement de tooAzure locataire Office 365
tooassociate hello Office 365 client toohello abonnement Azure, procédez comme suit :

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>Étape 1 : Ajouter Office 365 client tooyour abonnement Azure

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) avec les informations d’identification d’administrateur de service hello.

    ![Capture d’écran de la connexion à Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Dans le volet gauche de hello, sélectionnez **ACTIVE DIRECTORY**. Vous ne doit pas voir les locataire hello Office 365. Si vous le voyez pas, passez trop[étape 2 : modifier le répertoire hello associé hello abonnement Azure](#Step2).
   
   ![Capture d’écran de l’entrée Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Sélectionnez **NOUVEAU** > **ANNUAIRE** > **CRÉATION PERSONNALISÉE**.
   
    ![Capture d’écran de la création personnalisée Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Sur hello **ajouter un annuaire** sous **active**, sélectionnez **utiliser un annuaire existant**. Puis sélectionnez **je suis prêt toobe me déconnecter**, puis sélectionnez **Complete** ![icône Terminer](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Capture d’écran de « Utiliser un annuaire existant »](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Une fois que vous êtes déconnecté, connectez-vous avec les informations d’identification de l’administrateur global hello de votre client Office 365.
   
    ![Capture d’écran de la connexion d’administrateur général Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Sélectionnez **Continuer**.
   
    ![Capture d’écran de vérification](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Sélectionnez **Se déconnecter maintenant**.
   
    ![Capture d’écran de la déconnexion](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) avec les informations d’identification d’administrateur de service hello.
   
    ![Capture d’écran de la connexion à Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Vous devez voir votre client Office 365 dans le tableau de bord hello.
   
    ![Capture d’écran du tableau de bord](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>Étape 2 : Modifier le répertoire hello associé hello abonnement Azure
   
1. Sélectionnez **Paramètres**.
   
    ![Capture d’écran de l’icône des paramètres du portail Azure Classic](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Sélectionnez votre abonnement Azure, puis sélectionnez **MODIFIER L’ANNUAIRE**.

    ![Capture d’écran Modifier l’annuaire de l’abonnement Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Sélectionnez **Suivant** ![Icône Suivant](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    ![Capture d’écran de « Modification hello annuaire associé »](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Passez en revue les comptes hello affectée. Tous les coadministrateurs et [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md) utilisateurs avec accès assigné à dans les groupes de ressources existant hello sont supprimés. Hello qui vous avertissent mentionne uniquement la suppression de hello de coadministrateurs.
      
    ![Capture d’écran hello comptes de coadministrateurs toobe supprimé.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Capture d’écran présentant un toobe de compte d’utilisateur exemple supprimé.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Sélectionnez **Terminer** ![icône Terminer](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>Étape 3 : Ajoutez votre compte professionnel Office 365 en tant que client de coadministrateurs toohello Azure Active Directory
   
1. Sélectionnez hello **administrateurs** onglet, puis sélectionnez **ajouter**.
   
    ![Capture d’écran de l’onglet Administrateurs dans les paramètres du portail Azure Classic](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Entrez un compte de société de votre client Office 365, sélectionnez hello abonnement Azure, puis **Complete** ![icône Terminer](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Capture d’écran de la boîte de dialogue d’ajout de coadministrateur Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Revenir en arrière toohello **administrateurs** onglet. Vous devez voir le compte de société hello affiché en tant que coadministrateur.
   
    ![Capture d’écran de l’onglet Administrateurs](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  TooAzure d’accès de test avec un compte de coadministrateur hello.
   
    a. Déconnectez-vous hello portail Azure classic.
   
    b. Ouvrez hello [portail Azure](https://portal.azure.com/).
   
    c. Entrez les informations d’identification hello de coadministrateur hello et sélectionnez **connectez-vous**.
   
    ![Capture d’écran de la page de connexion à Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.


