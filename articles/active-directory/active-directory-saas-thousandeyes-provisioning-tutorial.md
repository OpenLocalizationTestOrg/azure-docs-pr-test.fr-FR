---
title: "Didacticiel : Configuration de ThousandEyes pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment configurer Azure Active Directory pour approvisionner et retirer automatiquement des comptes d’utilisateur sur ThousandEyes."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: mtillman
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: 2bff4dcb3e72113b2ae808959562e87823f8948b
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a>Didacticiel : Configuration de ThousandEyes pour approvisionner automatiquement des utilisateurs


L’objectif de ce didacticiel est de vous montrer les étapes à effectuer dans ThousandEyes et Azure AD pour approvisionner et retirer automatiquement des comptes d’utilisateur entre Azure AD et ThousandEyes. 

## <a name="prerequisites"></a>Composants requis

Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :

*   Un locataire Azure Active Directory
*   Un locataire ThousandEyes pour lequel au moins le [plan standard](https://www.thousandeyes.com/pricing) est activé 
*   Un compte d’utilisateur dans ThousandEyes doté d’autorisations d’administrateur 

> [!NOTE]
> L’intégration de l’approvisionnement d’Azure AD repose sur l’[API ThousandEyes SCIM](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), mise à la disposition des équipes de ThousandEyes qui relèvent au moins du plan standard.

## <a name="assigning-users-to-thousandeyes"></a>Affectation d’utilisateurs à ThousandEyes

Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées. Dans le cadre de l’approvisionnement automatique de comptes d’utilisateur, les utilisateurs et les groupes qui ont été « affectés » à une application dans Azure AD sont synchronisés. 

Avant de configurer et d’activer le service d’approvisionnement, vous devez déterminer quels utilisateurs et/ou groupes dans Azure AD représentent les utilisateurs qui ont besoin d’accéder à votre application ThousandEyes. Dès que vous avez fait votre choix, vous pouvez assigner ces utilisateurs à votre application ThousandEyes en suivant les instructions disponibles à la page suivante :

[Affecter un utilisateur ou un groupe à une application d’entreprise](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-thousandeyes"></a>Conseils importants concernant l’affectation d’utilisateurs à ThousandEyes

*   Il est recommandé de n’affecter qu’un seul utilisateur Azure AD à ThousandEyes afin de tester la configuration de l’approvisionnement. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Quand vous affectez un utilisateur à ThousandEyes, vous devez sélectionner le rôle **utilisateur** ou un autre rôle valide propre à l’application (si disponible) dans la boîte de dialogue d’affectation. Le rôle **Accès par défaut** ne fonctionne pas pour l’approvisionnement, et ces utilisateurs sont ignorés.


## <a name="configuring-user-provisioning-to-thousandeyes"></a>Configuration de l'approvisionnement d’utilisateurs pour ThousandEyes 

Cette section va vous guider afin de connecter votre instance Azure AD à l’API d’approvisionnement de comptes d’utilisateur de ThousandEyes, puis configurer le service d’approvisionnement pour créer, mettre à jour et désactiver des comptes d’utilisateur affectés dans ThousandEyes, en fonction des affectations d’utilisateurs et de groupes dans Azure AD.

> [!TIP]
> Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour ThousandEyes, grâce aux instructions disponibles dans le [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.


### <a name="configure-automatic-user-account-provisioning-to-thousandeyes-in-azure-ad"></a>Configurer l’approvisionnement automatique de comptes d’utilisateur pour ThousandEyes dans Azure AD


1. Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.

2. Si vous avez déjà configuré ThousandEyes pour l’authentification unique, recherchez votre instance de ThousandEyes à l’aide du champ de recherche. Sinon, sélectionnez **Ajouter** et recherchez **ThousandEyes** dans la galerie d’applications. Dans les résultats de la recherche, sélectionnez ThousandEyes, puis ajoutez-le à votre liste d’applications.

3. Sélectionnez votre instance de ThousandEyes, puis sélectionnez l’onglet **Approvisionnement**.

4. Définissez le **Mode d’approvisionnement** sur **Automatique**.

    ![Approvisionnement de ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. Dans la section **Informations d’identification de l’administrateur**, entrez le **jeton secret** généré par votre compte ThousandEyes (ce dernier se trouve dans votre compte ThousandEyes : **Sécurité et authentification**). 

    ![Approvisionnement de ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. Dans le portail Azure, cliquez sur **Tester la connexion** pour vous assurer qu’Azure AD peut se connecter à votre application ThousandEyes. Si la connexion échoue, vérifiez que votre compte ThousandEyes dispose des autorisations d’administrateur et réessayez l’étape 5.

7. Entrez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement dans le champ **E-mail de notification**, puis cochez la case « Envoyer une notification par e-mail en cas de défaillance ».

8. Cliquez sur **Enregistrer**. 

9. Dans la section Mappages, sélectionnez **Synchroniser les utilisateurs Azure Active Directory avec ThousandEyes**.

10. Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés à partir d’Azure AD vers ThousandEyes. Les attributs sélectionnés en tant que propriétés de **Correspondance** sont utilisés pour faire correspondre les comptes d’utilisateur dans ThousandEyes pour les opérations de mise à jour. Cliquez sur le bouton Enregistrer pour valider les modifications.

11. Pour activer le service d’approvisionnement Azure AD pour ThousandEyes, accédez à la section **Paramètres** et définissez le **Statut de l’approvisionnement** sur **Activé**.

12. Cliquez sur **Enregistrer**. 

Cette opération démarre la synchronisation initiale des utilisateurs et/ou des groupes affectés à ThousandEyes dans la section Utilisateurs et groupes. La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution. Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement, qui décrivent toutes les actions effectuées par le service d’approvisionnement.

Pour plus d’informations sur la lecture des journaux d’approvisionnement Azure AD, consultez [Création de rapports sur l’approvisionnement automatique de comptes d’utilisateur](https://docs.microsoft.com/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-enterprise-apps-manage-provisioning.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Étapes suivantes

* [Découvrez comment consulter les journaux et obtenir des rapports sur l’activité d’approvisionnement](active-directory-saas-provisioning-reporting.md)
