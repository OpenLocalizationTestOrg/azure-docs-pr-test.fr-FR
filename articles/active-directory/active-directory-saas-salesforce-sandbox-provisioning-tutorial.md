---
title: "Didacticiel : intégration d’Azure Active Directory à Salesforce Sandbox | Microsoft Docs"
description: "Découvrez comment configurer une authentification unique entre Azure Active Directory et Salesforce Sandbox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: jeedes
ms.openlocfilehash: d0efcae50b18dc2626af5510bd47ff36a27ba718
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Didacticiel : configuration de Salesforce Sandbox pour provisionner automatiquement des utilisateurs

L’objectif de ce didacticiel est de présenter les étapes à effectuer dans Salesforce Sandbox et Azure AD permettant d’approvisionner et retirer automatiquement des comptes utilisateur d’Azure AD vers Salesforce Sandbox.

## <a name="prerequisites"></a>Composants requis

Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :

*   Un locataire Azure Active Directory.
*   Un abonné valide pour les éditions Salesforce Sandbox for Work ou Salesforce Sandbox for Education. Vous pouvez utiliser un compte d’essai gratuit pour chaque service.
*   Un compte d’utilisateur dans Salesforce Sandbox avec les autorisations d’administrateur d’équipe.

## <a name="assigning-users-to-salesforce-sandbox"></a>Assigner des utilisateurs à Salesforce Sandbox

Azure Active Directory utilise un concept appelé « affectations » pour déterminer les utilisateurs devant recevoir l’accès aux applications sélectionnées. Dans le cadre de l’approvisionnement automatique de comptes utilisateur, seuls les utilisateurs et les groupes qui ont été « assignés » à une application dans Azure AD sont synchronisés.

Avant de configurer et d’activer le service de provisionnement, vous devez déterminer quels utilisateurs ou groupes dans Azure AD ont besoin d’accéder à votre application Salesforce Sandbox. Une fois cette décision prise, vous pouvez affecter ces utilisateurs à votre application Salesforce Sandbox en suivant les instructions fournies dans [affecter un utilisateur ou un groupe à une application d’entreprise](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce-sandbox"></a>Conseils importants concernant l’assignation d’utilisateurs à Salesforce Sandbox

* Il est recommandé de n’assigner qu’un seul utilisateur Azure AD à Salesforce Sandbox afin de tester la configuration de l’approvisionnement. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

* Lorsque vous assignez un utilisateur à Salesforce Sandbox, vous devez sélectionner un rôle d’utilisateur valide. Le rôle « Accès par défaut » ne fonctionne pas pour l’approvisionnement.

> [!NOTE]
> Cette application importe des rôles personnalisés à partir de Salesforce Sandbox dans le cadre du processus d’approvisionnement. Il est possible que le client souhaite sélectionner ce processus lors de l’assignation des utilisateurs.

## <a name="enable-automated-user-provisioning"></a>Activer l’approvisionnement automatique des utilisateurs

Cette section va vous guider afin de connecter votre instance Azure AD à votre compte utilisateur Salesforce Sandbox qui fournit l’API. À l’aide de ce guide, vous pourrez aussi découvrir comment configurer le service d’approvisionnement pour créer, mettre à jour et désactiver des comptes utilisateur assignés dans Salesforce Sandbox, en fonction des attributions d’utilisateur et de groupe dans Azure AD.

>[!Tip]
>Vous pouvez également choisir d’activer l’authentification unique basée sur SAML pour Salesforce Sandbox, grâce aux instructions disponibles dans le [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="configure-automatic-user-account-provisioning"></a>Configurer l’approvisionnement automatique d’un compte utilisateur

Cette section décrit comment activer l’approvisionnement des utilisateurs des comptes d’utilisateurs Active Directory sur Salesforce Sandbox.

1. Dans le [portail Azure](https://portal.azure.com), accédez à la section **Azure Active Directory > Applications d’entreprise > Toutes les applications**.

2. Si vous avez déjà configuré Salesforce Sandbox pour l’authentification unique, recherchez votre instance de Salesforce Sandbox à l’aide du champ de recherche. Sinon, sélectionnez **Ajouter** et effectuer une recherche pour **Salesforce Sandbox** dans la galerie d’applications. Dans les résultats de la recherche, sélectionnez Salesforce Sandbox, puis ajoutez-la à votre liste d’applications.

3. Sélectionnez votre instance de Salesforce Sandbox, puis sélectionnez l’onglet **Approvisionnement**.

4. Définissez le **Mode d’approvisionnement** sur **Automatique**.

    ![approvisionnement](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. Dans la section **Informations d’identification de l’administrateur**, fournissez les paramètres de configuration suivants :
   
    a. Dans la zone de texte **Nom d’utilisateur administrateur Salesforce Sandbox**, entrez le nom d’un compte Salesforce Sandbox auquel le profil **Administrateur système** est assigné dans Salesforce.com.
   
    b. Dans la zone de texte **Mot de passe d’administrateur**, entrez le mot de passe de ce compte.

6. Pour obtenir le jeton de sécurité Salesforce Sandbox, ouvrez un nouvel onglet et connectez-vous au même compte Administrateur Salesforce Sandbox. Dans le coin supérieur droit de la page, cliquez sur votre nom, puis cliquez sur **Paramètres**.

     ![Activer l’approvisionnement automatique des utilisateurs](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Activer l’approvisionnement automatique des utilisateurs")

7. Dans le volet de navigation gauche, cliquez sur **Mes informations personnelles** pour développer la section associée, puis sur **Réinitialiser mon jeton de sécurité**.
  
    ![Activer l’approvisionnement automatique des utilisateurs](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Activer l’approvisionnement automatique des utilisateurs")

8. Sur la page **Réinitialiser le jeton de sécurité**, cliquez sur le bouton **Réinitialiser le jeton de sécurité**.

    ![Activer l’approvisionnement automatique des utilisateurs](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Activer l’approvisionnement automatique des utilisateurs")

9. Contrôlez la boîte de réception associée à ce compte d’administrateur. Vous allez recevoir un e-mail de la part de Salesforce Sandbox.com dans lequel se trouve le nouveau jeton de sécurité.

10. Copiez le jeton, accédez à votre fenêtre Azure AD et collez-le dans le champ **Jeton secret**.

11. Dans le portail Azure, cliquez sur **Tester la connexion** pour vous assurer qu’Azure AD peut se connecter à votre application Salesforce Sandbox.

12. Dans le champ **E-mail de notification**, saisissez l’adresse e-mail d’une personne ou d’un groupe qui doit recevoir les notifications d’erreur d’approvisionnement, puis cochez la case.

13. Cliquez sur **Enregistrer.**  
    
14.  Dans la section Mappages, sélectionnez **Synchroniser des utilisateurs Azure Active Directory avec Salesforce Sandbox**.

15. Dans la section **Mappages d’attributs**, passez en revue les attributs utilisateur qui sont synchronisés à partir d’Azure AD vers Salesforce Sandbox. Les attributs sélectionnés en tant que propriétés de **Correspondance** servent à faire correspondre les comptes utilisateur dans Salesforce Sandbox, en vue d’opérations de mise à jour. Cliquez sur le bouton Enregistrer pour valider les modifications.

16. Pour activer le service d’approvisionnement Azure AD pour Salesforce Sandbox, accédez à la section Paramètres et définissez l’**État de l’approvisionnement** sur **Activé**

17. Cliquez sur **Enregistrer.**

Cette commande démarre la synchronisation initiale des utilisateurs et/ou des groupes affectés à Salesforce Sandbox dans la section Utilisateurs et Groupes. La synchronisation initiale prend plus de temps que les synchronisations suivantes, qui se produisent environ toutes les 20 minutes, tant que le service est en cours d’exécution. Vous pouvez utiliser la section **Détails de la synchronisation** pour surveiller la progression et suivre les liens vers les rapports d’activité d’approvisionnement. Ces rapports décrivent toutes les actions effectuées par le service d’approvisionnement sur votre application Salesforce Sandbox.

Vous pouvez désormais créer un compte de test. Patientez jusqu’à 20 minutes avant de vérifier que le compte a bien été synchronisé avec Salesforce.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](https://docs.microsoft.com/azure/active-directory/active-directory-saas-salesforce-sandbox-tutorial)
