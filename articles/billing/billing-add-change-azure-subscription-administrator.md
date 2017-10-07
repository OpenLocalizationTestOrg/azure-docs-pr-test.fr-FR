---
title: "rôles d’abonnement Azure admin aaaAdd ou modifier | Documents Microsoft"
description: "Décrit comment tooadd ou modifier Coadministrateur Azure, administrateur de Service et l’administrateur de compte"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>Ajouter ou modifier des rôles d’administrateur Azure qui gèrent les abonnement hello ou des services
Vous pouvez modifier hello Azure administrateur qui gère votre abonnement Azure ou gère hello Azure services utilisés dans votre abonnement. tooview les informations de facturation Azure et gérer des abonnements, vous devez vous connecter toohello [centre des comptes](https://account.windowsazure.com/Home/Index) comme hello administrateur de compte. 

## <a name="add-an-admin-for-a-subscription"></a>Ajout d’un administrateur à un abonnement
Vous pouvez ajouter un administrateur Azure Bonjour portail Azure ou Bonjour portail Azure classic.

**Portail Azure**

tooadd une personne en tant qu’administrateur d’un abonnement dans hello portail Azure, vous leur donnez rôle de propriétaire hello. rôle de propriétaire Hello peut uniquement gérer les ressources hello dans l’abonnement hello que vous avez attribué. Il n’a pas accès privilège tooother abonnements. Hello propriétaires que vous ajoutez via hello [portail Azure](https://portal.azure.com) ne peut pas gérer les ressources Bonjour [portail Azure classic](https://manage.windowsazure.com).

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, sélectionnez **abonnement** > *hello abonnement que vous souhaitez hello admin tooaccess*.

    ![Capture d’écran montrant l’abonnement sélectionné](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. Dans le panneau d’abonnement hello, sélectionnez **(IAM) de contrôle d’accès**.
4. Sélectionnez **Ajouter** > **Rôle** > **Propriétaire**. Tapez l’adresse de messagerie hello de hello utilisateur que vous souhaitez tooadd en tant que propriétaire, hello sélectionnez utilisateur, puis sélectionnez **enregistrer**.

    ![Capture d’écran qui illustre le rôle de propriétaire hello sélectionné](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Si vous souhaitez le compte de propriétaire tooadd hello en tant que coadministrateur, Bonjour **(IAM) de contrôle d’accès** page, cliquez avec le droit d’utilisateur de hello, puis sélectionnez **ajouter en tant que coadministrateur**. Cette fonctionnalité est désormais disponible sur le [portail Azure en version préliminaire](https://preview.portal.azure.com/). 

     ![Capture d’écran d’ajout d’un coadministrateur](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Vous devez utilisateur de tooadd hello « Propriétaire » en tant que coadministrateur si l’utilisateur hello doit toomanage hello services Azure dans [portail Azure classic](https://manage.windowsazure.com/).

    autorisations de coadministrateur tooremove hello, droit d’utilisateur de « coadministrateur » hello, puis sélectionnez **supprimer le coadministrateur**.

    ![Capture d’écran de suppression de coadministrateur](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**portail Azure Classic**

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/).
2. Dans le volet de navigation hello, sélectionnez **paramètres**> **administrateurs**> **ajouter**. </br>

    ![Capture d’écran qui illustre comment tooget toohello bouton Ajouter](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Hello de type adresse de messagerie de personne hello tooadd en tant que coadministrateur, puis sélectionnez abonnement hello que vous souhaitez hello coadministrateur tooaccess.</br>

    ![Capture d’écran montrant un abonnement sélectionné ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Hello suivant l’adresse de messagerie peut être ajoutée en tant que Coadministrateur :

* **compte Microsoft** (anciennement Windows Live ID) </br>
  Vous pouvez utiliser un toosign Account Microsoft tooall orienté client des produits Microsoft et cloud services, tels que Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone et Xbox LIVE.
* **Organizational account**</br>
  Un compte professionnel est un compte créé sous Azure Active Directory. adresse du compte de société Hello est au format :

    utilisateur@&lt;votre domaine&gt;.onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Modification de l’administrateur de services fédérés d’un abonnement
Uniquement hello administrateur de compte peut modifier hello administrateur de Service pour un abonnement.

1. Connectez-vous trop[centre des comptes Azure](https://account.windowsazure.com/subscriptions) à l’aide de hello administrateur de compte.
2. Sélectionnez l’abonnement hello toochange.
3. Sur le côté droit de hello, sélectionnez **modifier l’abonnement** détails. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. Bonjour **administrateur de SERVICE** , entrez l’adresse de messagerie hello Hello nouvel administrateur de Service. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>Modifier hello administrateur de compte
propriété tootransfer Hello tooanother compte Azure, consultez [transfert de la propriété d’un abonnement Azure](billing-subscription-transfer.md).

Nous vous recommandons vivement que vous ne pas supprimer ou renommer l’adresse de messagerie de l’administrateur de compte hello. Vous pouvez constater un comportement inattendu et indésirable par hello compte Azure. Peut ne pas être en mesure de tooAzure connectez-vous avec ce compte, apporter des modifications toohello compte ou gérer les ressources avec ce compte. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Vérifiez hello administrateur de compte de l’abonnement de hello
Si vous ne savez pas qui est administrateur de compte hello pour votre abonnement, utilisez hello suivant toofind étapes out.

  1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
  2. Dans le menu du Hub hello, sélectionnez **abonnement**.
  3. Sélectionnez l’abonnement hello souhaité toocheck, puis regardez sous **paramètres**.
  4. Sélectionner **Propriétés**. administrateur du compte d’abonnement de hello Hello s’affiche dans hello **Admin. compte** boîte.  

## <a name="types-of-azure-admin-accounts"></a>Types de comptes d’administrateur Azure
 Compte d’administrateur, administrateur de Service et coadministrateur sont hello trois types de rôles d’administrateur dans Microsoft Azure. Hello tableau suivant décrit différence hello entre ces trois rôles d’administration.

| Rôle administratif | Limite | Description |
| --- | --- | --- |
| Administrateur de compte |1 par compte Azure |Il s’agit hello personne souscrit ou acheter des abonnements Azure et est autorisé tooaccess hello [centre des comptes](https://account.windowsazure.com/Home/Index) et d’effectuer diverses tâches de gestion. Ceux-ci incluent les abonnements toocreate en mesure de, annuler les abonnements, remplacer la facturation hello pour un abonnement et modifier hello administrateur de Service. |
| Administrateur de services fédérés |1 par abonnement Azure |Ce rôle est services autorisés toomanage Bonjour [portail Azure](https://portal.azure.com). Par défaut, un nouvel abonnement, hello administrateur de compte est également hello administrateur de Service. |
| Coadministrateur (CA) Bonjour [portail Azure classic](https://manage.windowsazure.com) |200 par abonnement |Ce rôle a hello même des privilèges d’accès en tant que hello administrateur de Service, mais vous ne pouvez pas modifier l’association de hello de répertoires de tooAzure abonnements. |

Azure contrôle d’accès basé sur un rôle Active Directory (RBAC) permet aux utilisateurs toobe ajouté toomultiple rôles. Pour plus d’informations, consultez la rubrique [Contrôle d’accès en fonction du rôle Azure Active Directory](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Limitations et restrictions des comptes Administrateur
* Chaque abonnement est associé à un annuaire Azure AD (également appelé hello répertoire par défaut). toofind hello abonnement hello de répertoire par défaut est associé, l’accédez toohello [portail Azure classic](https://manage.windowsazure.com/), sélectionnez **paramètres** > **abonnements**. Vérifiez Bonjour abonnement ID toofind Bonjour répertoire par défaut.
* Si vous êtes connecté avec un Account Microsoft, vous pouvez uniquement ajouter des autres Accounts Microsoft ou des utilisateurs d’hello répertoire par défaut en tant que Coadministrateur.
* Si vous êtes connecté avec un compte professionnel, vous pouvez ajouter d’autres comptes professionnels de votre organisation en tant que coadministrateur. Par exemple, abby@contoso.com peut ajouter bob@contoso.com en tant qu’administrateur de services fédérés ou coadministrateur, mais ne peut pas ajouter john@notcontoso.com, sauf si john@notcontoso.com est l’annuaire par défaut. Les utilisateurs connectés avec des comptes professionnels peuvent continuer d’utilisateurs de Microsoft Account tooadd en tant qu’administrateur de services fédérés ou Coadministrateur.
* Maintenant qu’il est possible toosign dans tooAzure avec un compte professionnel, voici hello modifications tooService administrateur et les spécifications de compte de coadministrateur :

  | Méthode de connexion | Ajouter un compte ou des utilisateurs Microsoft dans l’annuaire par défaut en tant que coadministrateur ou administrateur de services fédérés ? | Ajouter un compte de société Bonjour même organisation en tant qu’autorité de certification ou SA ? | Ajouter un compte de société dans une autre organisation que le coadministrateur ou administrateur de services fédérés ? |
  | --- | --- | --- | --- |
  |  Compte Microsoft |Oui |Non |Non |
  |  Compte de société |Oui |Oui |Non |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>En savoir plus sur le contrôle d’accès aux ressources et Active Directory
* toolearn en savoir plus sur la façon dont l’accès aux ressources est contrôlé dans Microsoft Azure, consultez [présentation de l’accès aux ressources dans Azure](../active-directory/active-directory-understanding-resource-access.md).
* Pour plus d’informations sur Azure Active Directory, consultez les pages [Association des abonnements Azure avec Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) et [Affecter des rôles Administrateur dans Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
