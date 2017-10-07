---
title: "Didacticiel : Intégration d’Azure Active Directory à Citrix GoToMeeting | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>Didacticiel : Configuration de Citrix GoToMeeting pour l’attribution automatique des utilisateurs

objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans Citrix GoToMeeting et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooCitrix GoToMeeting.

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory.
*   Un abonnement Citrix GoToMeeting pour lequel l’authentification unique est activée
*   Un compte d’utilisateur Citrix GoToMeeting avec les autorisations d’administrateur d’équipe

## <a name="assigning-users-toocitrix-gotomeeting"></a>Affectation d’utilisateurs tooCitrix GoToMeeting

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD qui représentent des utilisateurs ayant besoin d’accès tooyour Citrix GoToMeeting application hello. Une fois choisi, vous pouvez attribuer ces tooyour utilisateurs Citrix GoToMeeting application en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>Conseils importants pour l’affectation d’utilisateurs tooCitrix GoToMeeting

*   Il est recommandé qu’un seul utilisateur Azure AD est attribué tooCitrix GoToMeeting tootest hello service de la configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooCitrix utilisateur GoToMeeting, vous devez sélectionner un rôle d’utilisateur valide. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.

## <a name="enable-automated-user-provisioning"></a>Activer l’approvisionnement automatique des utilisateurs

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre GoToMeeting tooCitrix AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver l’utilisateur affecté comptes dans Citrix GoToMeeting en fonction de l’utilisateur et de groupe affectation dans Azure AD.

> [!TIP]
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Citrix GoToMeeting, suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure compte le provisionnement utilisateur automatique :

1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2. Si vous avez déjà configuré Citrix GoToMeeting pour l’authentification unique, recherchez votre instance de Citrix GoToMeeting à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Citrix GoToMeeting** dans la galerie d’applications hello. Sélectionnez Citrix GoToMeeting à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

3. Sélectionnez votre instance de Citrix GoToMeeting, puis hello **Provisioning** onglet.

4. Ensemble hello **Provisioning** Mode trop**automatique**. 

    ![approvisionnement](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. Sous la section informations d’identification d’administrateur de hello, procédez hello comme suit :
   
    a. Bonjour **nom d’utilisateur Admin Citrix GoToMeeting** zone de texte, nom d’utilisateur de type hello d’un administrateur.

    b. Bonjour **mot de passe Admin Citrix GoToMeeting** zone de texte, hello mot de passe administrateur.

6. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure Azure AD peut se connecter tooyour Citrix GoToMeeting application. Si hello connexion échoue, assurez-vous que votre compte Citrix GoToMeeting dispose des autorisations d’administrateur d’équipe et essayez hello **« Informations d’identification d’administration »** pas à pas.

7. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.

8. Cliquez sur **Enregistrer.**

9. Sous la section des mappages de hello, sélectionnez **tooCitrix de synchronisation Azure Active Directory Users GoToMeeting.**

10. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooCitrix GoToMeeting. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Citrix GoToMeeting pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

11. tooenable hello service de configuration d’Azure AD pour Citrix GoToMeeting, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres

12. Cliquez sur **Enregistrer.**

Il démarre la synchronisation initiale de hello de tous les utilisateurs et/ou groupes affectés tooCitrix GoToMeeting dans la section utilisateurs et groupes de hello. la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre application Citrix GoToMeeting.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-citrix-gotomeeting-tutorial.md)


