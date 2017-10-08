---
title: "Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Didacticiel : Configuration de Dropbox for Business pour approvisionner automatiquement des utilisateurs

objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Dropbox pour l’entreprise et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooDropbox for Business.

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory.
*   Un abonnement Dropbox for Business pour lequel l’authentification unique est activée.
*   Un compte d’utilisateur dans Dropbox for Business avec les autorisations d’administrateur d’équipe.

## <a name="assigning-users-toodropbox-for-business"></a>Affectation d’utilisateurs tooDropbox for Business

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello des utilisateurs qui doivent accéder aux tooyour Dropbox pour l’application d’entreprise. Après choisi, vous pouvez attribuer ces tooyour utilisateurs Dropbox pour l’application d’entreprise en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>Conseils importants pour l’affectation d’utilisateurs tooDropbox for Business

*   Il est recommandé qu’un seul utilisateur Azure AD est attribué tooDropbox pour hello de tootest entreprise service de la configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooDropbox utilisateur pour l’entreprise, vous devez sélectionner un rôle d’utilisateur valide. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration...

## <a name="enable-automated-user-provisioning"></a>Activer l’approvisionnement automatique des utilisateurs

Cette section vous guide à travers de la connexion de votre tooDropbox Azure AD pour le compte d’utilisateur d’entreprise à l’API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Dropbox for Business en fonction de l’utilisateur et de groupe affectation dans Azure AD.

>[!Tip]
>Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Dropbox for Business, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure compte le provisionnement utilisateur automatique :

1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2. Si vous avez déjà configuré Dropbox for Business pour l’authentification unique, recherchez votre instance de Dropbox for Business à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Dropbox for Business** dans la galerie d’applications hello. Sélectionnez Dropbox for Business à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

3. Sélectionnez votre instance de Dropbox for Business, puis hello **Provisioning** onglet.

4. Ensemble hello **Mode d’approvisionnement** trop**automatique**. 

    ![approvisionnement](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. Sous hello **informations d’identification administrateur** , cliquez sur **Authorize**. Cela permet d’ouvrir une boîte de dialogue de connexion à Dropbox for Business dans une nouvelle fenêtre de navigateur.

6. Sur hello **connexion toolink de tooDropbox avec Azure AD** boîte de dialogue de connexion tooyour Dropbox pour le client de l’entreprise.

     ![Approvisionnement d'utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Approvisionnement d’utilisateurs")

7. Vérifiez que vous aimeriez toogive Azure Active Directory autorisation toomake modifications tooyour Dropbox pour le client de l’entreprise. Cliquez sur **Autoriser**.
    
      ![Approvisionnement d'utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Approvisionnement d’utilisateurs")

8. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure Azure AD peut se connecter tooyour Dropbox pour l’application d’entreprise. Si hello connexion échoue, vérifiez votre Dropbox pour le compte d’entreprise a des autorisations d’administrateur d’équipe et essayez de hello **« Autoriser »** pas à pas.

9. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.

10. Cliquez sur **Enregistrer.**

11. Sous la section des mappages de hello, sélectionnez **tooDropbox de synchronisation Azure Active Directory Users pour entreprises.**

12. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir de Azure AD tooDropbox for Business. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Dropbox for Business pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

13. tooenable hello service de configuration d’Azure AD pour Dropbox for Business, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres

14. Cliquez sur **Enregistrer.**

Il démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooDropbox entreprise Bonjour les utilisateurs et la section groupes de hello. la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre Dropbox pour l’application d’entreprise.

Vous pouvez à présent créer un compte de test. Attendez que les minutes too20 tooverify hello compte a été synchronisé tooDropbox for Business.

Si le cycle d'approvisionnement d'utilisateur a abouti, l'état associé est indiqué.

![Affecter des utilisateurs](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Affecter des utilisateurs")


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-dropboxforbusiness-tutorial.md)