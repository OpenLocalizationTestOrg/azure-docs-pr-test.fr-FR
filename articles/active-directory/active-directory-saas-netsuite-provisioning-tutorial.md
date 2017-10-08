---
title: "Didacticiel : Intégration d’Azure Active Directory à Netsuite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Netsuite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8a6d3994-ee33-4a6f-b0a2-9d0389467f16
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 5bb2989c1296b9f2abc9e8c84855731adc484aab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-netsuite-for-automatic-user-provisioning"></a>Didacticiel : Configuration de Netsuite pour l’approvisionnement automatique d’utilisateurs

objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Netsuite et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooNetsuite.

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory.
*   Un abonnement Netsuite pour lequel l’authentification unique est activée.
*   Un compte utilisateur dans Netsuite avec les autorisations d’administrateur d’équipe.

## <a name="assigning-users-toonetsuite"></a>Affectation d’utilisateurs tooNetsuite

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD sont synchronisés.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder aux tooyour Netsuite application. Après choisi, vous pouvez attribuer à ces applications de Netsuite tooyour les utilisateurs en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toonetsuite"></a>Conseils importants pour l’affectation d’utilisateurs tooNetsuite

*   Il est recommandé qu’un seul utilisateur Azure AD est attribué tooNetsuite tootest hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooNetsuite d’utilisateur, vous devez sélectionner un rôle d’utilisateur valide. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.

## <a name="enable-user-provisioning"></a>Activer l’approvisionnement des utilisateurs

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooNetsuite AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Netsuite en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.

> [!TIP] 
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Netsuite, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="tooconfigure-user-account-provisioning"></a>approvisionnement des comptes utilisateur tooconfigure :

objectif Hello de cette section est toooutline mode tooenable l’approvisionnement des utilisateurs d’utilisateur Active Directory de comptes tooNetsuite.

1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2. Si vous avez déjà configuré Netsuite pour l’authentification unique, recherchez votre instance de Netsuite à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Netsuite** dans la galerie d’applications hello. Sélectionnez Netsuite à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

3. Sélectionnez votre instance de Netsuite, puis hello **Provisioning** onglet.

4. Ensemble hello **Mode d’approvisionnement** trop**automatique**. 

    ![approvisionnement](./media/active-directory-saas-netsuite-provisioning-tutorial/provisioning.png)

5. Sous hello **informations d’identification administrateur** section, fournissez hello suivant les paramètres de configuration :
   
    a. Bonjour **nom d’utilisateur Admin** zone de texte, tapez un Netsuite compte nom a hello **administrateur système** profil dans Netsuite.com attribué.
   
    b. Bonjour **mot de passe administrateur** zone de texte, un mot de passe type hello pour ce compte.
      
6. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Netsuite application.

7. Bonjour **Notification par courrier électronique** , entrez l’adresse de messagerie hello d’une personne ou un groupe qui doit recevoir des notifications de d’erreur et case à cocher hello.

8. Cliquez sur **Enregistrer.**

9. Sous la section des mappages de hello, sélectionnez **tooNetsuite de synchronisation Azure Active Directory Users.**

10. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooNetsuite. Notez que hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Netsuite pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

11. tooenable hello service de configuration d’Azure AD pour Netsuite, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres

12. Cliquez sur **Enregistrer.**

Il démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooNetsuite Bonjour les utilisateurs et la section groupes de hello. Notez que la synchronisation initiale hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre application Netsuite.

Vous pouvez à présent créer un compte de test. Attendez que les minutes too20 tooverify hello compte a été synchronisé tooNetsuite.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-netsuite-tutorial.md)