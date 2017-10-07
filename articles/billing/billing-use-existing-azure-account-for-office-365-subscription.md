---
title: aaaSign pour Office 365 avec un compte Azure | Documents Microsoft
description: "Découvrez comment abonnement toocreate un Office 365 à l’aide d’un compte Azure"
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
ms.openlocfilehash: d19e1c1edff0b9658b639e796a72bbf4e87b9c3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a>Souscrire un abonnement Office 365 avec un compte Azure
Si vous êtes abonné à Azure, vous pouvez utiliser votre toosign compte Azure pour un abonnement Office 365. Si vous faites partie d’une organisation qui a un abonnement Azure, vous pouvez créer des abonnements Office 365 pour les utilisateurs dans votre instance Azure Active Directory (Azure AD) existante. Inscrivez-vous tooOffice 365 à l’aide d’un compte qui dispose des autorisations d’administrateur général ou administrateur de facturation de votre client Azure Active Directory. Pour plus d’informations, consultez les pages [Vérifier mes autorisations de compte dans Azure AD](#RoleInAzureAD) et [Attribution de rôles d’administrateur dans Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

Si vous avez déjà un compte Office 365 et un abonnement Azure, vous pouvez [associer un tooan du locataire Office 365 abonnement Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a>Obtenir un abonnement Office 365 avec un compte Azure

1. Accédez toohello [page de produit Office 365](https://products.office.com/business), puis sélectionnez un plan.
2. Cliquez sur **connectez-vous** sur hello haut à droite de la page de hello.

    ![Capture d’écran de la page d’essai d’Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. Connectez-vous avec les informations d’identification de votre compte Azure. Si vous créez un abonnement pour votre organisation, utilisez un compte Azure qui est membre du rôle d’annuaire hello administrateur général ou administrateur de facturation dans votre client Azure Active Directory.

    ![Capture d’écran de la connexion à Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. Cliquez sur **Essayez dès maintenant**.

    ![Capture d’écran confirmant votre commande d’Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. Sur la page de réception de la commande hello, cliquez sur **continuer**.

    ![Capture d’écran de réception de la commande hello Office 365](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

Vous êtes prêt. Si vous avez créé l’abonnement de hello Office 365 pour votre organisation, utilisez hello suivant toocheck étapes que vos utilisateurs Azure AD sont maintenant dans Office 365.

1. Ouvrez le centre d’administration hello Office 365.
2. Développez la section **UTILISATEURS**, puis cliquez sur **Utilisateurs actifs**.

    ![Capture d’écran d’aux utilisateurs de hello Office 365 admin center](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

Une fois que vous vous inscrivez, hello abonnement Office 365 est ajouté toohello même instance d’Azure Active Directory appartenant à votre abonnement Azure. Pour plus d’informations, consultez les pages [En savoir plus sur les abonnements Azure et Office 365](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) et [Association des abonnements Azure avec Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a id="RoleInAzureAD"></a>Vérifier mes autorisations de compte dans Azure AD
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **Plus de services**, puis recherchez **Active Directory**.

    ![Capture d’écran de Active Directory Bonjour portail Azure](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. Cliquez sur**Utilisateurs et groupes** > **Tous les utilisateurs**.
4. Sélectionnez le nom d’utilisateur hello. 

    ![Capture d’écran qui affiche les utilisateurs d’Azure Active Directory hello](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. Cliquez sur **Rôle de répertoire**.
  
    ![Capture d’écran qui illustre le rôle d’annuaire portail Azure hello](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  rôle de Hello **administrateur Global** ou **administrateur limité** > **administrateur de facturation** toocreate requis n’est un abonnement Office 365 pour les utilisateurs dans votre annuaire Active Directory Azure existant.

    ![Capture d’écran montrant le rôle de répertoire Administrateur de facturation du Portail Azure.](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement. 
