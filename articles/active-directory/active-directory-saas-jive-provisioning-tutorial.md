---
title: "Didacticiel : Intégration d’Azure Active Directory à Jive | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>Didacticiel : Configuration de Jive pour l’approvisionnement des utilisateurs

objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Jive et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooJive.

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory.
*   Un abonnement Jive pour lequel l’authentification unique est activée.
*   Un compte utilisateur dans Jive avec les autorisations d’administrateur d’équipe.

## <a name="assigning-users-toojive"></a>Affectation d’utilisateurs tooJive

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD qui représentent des utilisateurs qui doivent accéder aux tooyour Jive application hello. Après choisi, vous pouvez attribuer à ces applications de Jive tooyour les utilisateurs en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>Conseils importants pour l’affectation d’utilisateurs tooJive

*   Il est recommandé qu’un seul utilisateur Azure AD avoir tooJive tootest hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooJive d’utilisateur, vous devez sélectionner un rôle d’utilisateur valide. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.

## <a name="enable-user-provisioning"></a>Activer l’approvisionnement des utilisateurs

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooJive AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Jive en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.

> [!TIP]
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Jive, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="tooconfigure-user-account-provisioning"></a>approvisionnement des comptes utilisateur tooconfigure :

objectif Hello de cette section est toooutline mode tooenable l’approvisionnement des utilisateurs d’utilisateur Active Directory de comptes tooJive.
Dans le cadre de cette procédure, vous êtes tooprovide requis un jeton de sécurité utilisateur que vous avez besoin de toorequest jive.com.

1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2. Si vous avez déjà configuré Jive pour l’authentification unique, recherchez votre instance de Jive à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Jive** dans la galerie d’applications hello. Sélectionnez Jive à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

3. Sélectionnez votre instance de Jive, puis hello **Provisioning** onglet.

4. Ensemble hello **Mode d’approvisionnement** trop**automatique**. 

    ![approvisionnement](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. Sous hello **informations d’identification administrateur** section, fournissez hello suivant les paramètres de configuration :
   
    a. Bonjour **nom d’utilisateur Admin Jive** zone de texte, tapez un Jive compte nom a hello **administrateur système** profil dans Jive.com attribué.
   
    b. Bonjour **mot de passe administrateur Jive** zone de texte, un mot de passe type hello pour ce compte.
   
    c. Bonjour **URL du client Jive** zone de texte, tapez l’URL client Jive hello.
      
      > [!NOTE]
      > URL de locataire Jive Hello est utilisé par votre toolog d’organisation dans tooJive.  
      > En règle générale, les URL hello a hello suivant le format : **www.\< organisation\>. jive.com**.          

6. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Jive application.

7. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello ci-dessous.

8. Cliquez sur **Enregistrer.**

9. Sous la section des mappages de hello, sélectionnez **tooJive de synchronisation Azure Active Directory Users.**

10. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooJive. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Jive pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

11. tooenable hello service de configuration d’Azure AD pour Jive, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres

12. Cliquez sur **Enregistrer.**

Il démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooJive Bonjour les utilisateurs et la section groupes de hello. la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service dans votre application de Jive.

Vous pouvez à présent créer un compte de test. Attendez que les minutes too20 tooverify hello compte a été synchronisé tooJive.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-jive-tutorial.md)