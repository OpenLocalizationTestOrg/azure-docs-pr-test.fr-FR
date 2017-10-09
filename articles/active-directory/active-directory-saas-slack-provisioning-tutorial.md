---
title: "Didacticiel : Configuration de Slack pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooSlack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>Didacticiel : Configuration de Slack pour l’approvisionnement automatique d’utilisateurs


objectif de ce didacticiel Hello est tooshow vous hello étapes que vous devez tooperform dans la marge et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooSlack. 

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un client Azure Active Directory
*   Une marge de locataire avec hello [Plus plan](https://aadsyncfabric.slack.com/pricing) ou mieux activé 
*   Un compte d’utilisateur dans Slack avec les autorisations d’administrateur d’équipe 

Remarque : hello mise en service d’intégration de Azure AD s’appuie sur hello [Slack SCIM API](https://api.slack.com/scim) qui est équipes tooSlack disponible sur hello Plus plan ou supérieures.

## <a name="assigning-users-tooslack"></a>Affectation d’utilisateurs tooSlack

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD seront synchronisés. 

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de marge tooyour. Après choisi, vous pouvez attribuer à ces applications de marge tooyour utilisateurs en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>Conseils importants pour l’affectation d’utilisateurs tooSlack

*   Il est recommandé qu’un seul utilisateur Azure AD avoir tooSlack tootest hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooSlack d’utilisateur, vous devez sélectionner hello **utilisateur** ou le rôle « Groupe » dans la boîte de dialogue attribution hello. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.


## <a name="configuring-user-provisioning-tooslack"></a>Configuration tooSlack de configuration de l’utilisateur 

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooSlack AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans la marge en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.

**Conseil :** vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Slack, suivant les instructions de hello fournies dans (portail Azure) [https://portal.azure.com]. L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>compte d’utilisateur automatique de tooconfigure tooSlack de configuration dans Azure AD :


1)  Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2) Si vous avez déjà configuré la marge pour l’authentification unique, recherchez votre instance de la marge à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Slack** dans la galerie d’applications hello. Sélectionnez la marge à partir des résultats de recherche hello et l’ajouter tooyour la liste des applications.

3)  Sélectionnez votre instance de marge, puis hello **Provisioning** onglet.

4)  Ensemble hello **Mode d’approvisionnement** trop**automatique**.

![Approvisionnement Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  Sous hello **informations d’identification administrateur** , cliquez sur **Authorize**. Une boîte de dialogue d’autorisation Slack s’ouvre dans une nouvelle fenêtre de navigateur. 

6) Dans la nouvelle fenêtre de hello, connectez-vous à Slack à l’aide de votre compte d’administrateur d’équipe. hello résultant d’autorisation boîte de dialogue, sélectionnez hello Slack équipe que vous souhaitez la préparation de tooenable, puis sélectionnez **Authorize**. Une fois terminée, retournez toohello toocomplete portail Azure hello est mise en service de configuration.

![Boîte de dialogue d’autorisation](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter à application de marge tooyour. Si hello connexion échoue, assurez-vous que votre compte Slack dispose d’autorisations d’administrateur d’équipe et recommencez hello à nouveau l’étape « Autoriser ».

8) Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello ci-dessous.

9) Cliquez sur **Enregistrer**. 

10) Sous la section des mappages de hello, sélectionnez **tooSlack de synchronisation Azure Active Directory Users**.

11) Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui seront synchronisés à partir d’Azure AD tooSlack. Notez que hello attributs sélectionnés en tant que **correspondance** propriétés se trouvent les comptes d’utilisateur hello toomatch utilisé dans la marge pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

12) tooenable hello service de configuration d’Azure AD pour Slack, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section

13) Cliquez sur **Enregistrer**. 

Ceci démarrera la synchronisation initiale d’utilisateurs et/ou groupes affectés tooSlack Bonjour les utilisateurs et la section groupes de hello. Notez que la synchronisation initiale hello a tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 10 minutes environ, tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service dans votre application de marge.

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[Facultatif] Configuration d’objet groupe tooSlack de configuration 

Si vous le souhaitez, vous pouvez activer l’approvisionnement des objets de groupe à partir d’Azure AD tooSlack hello. Cela est différent de « affectation de groupes d’utilisateurs », dans cet objet de groupe réel hello en outre tooits membres seront répliquées à partir d’Azure AD tooSlack. Par exemple, si vous avez un groupe nommé « Mon groupe » dans Azure AD, un groupe identique nommé « Mon groupe » est créé dans Slack.

### <a name="tooenable-provisioning-of-group-objects"></a>tooenable mise en service des objets de groupe :

1) Sous la section des mappages de hello, sélectionnez **tooSlack de synchroniser les groupes Azure Active Directory**.

2) Dans le panneau de mappage d’attribut hello, définissez activé tooYes.

3) Bonjour **des mappages d’attributs** section, passez en revue les attributs de groupe hello qui seront synchronisés à partir d’Azure AD tooSlack. Notez que hello attributs sélectionnés en tant que **correspondance** propriétés seront des groupes de hello toomatch utilisé dans la marge pour les opérations de mise à jour. 

4) Cliquez sur **Enregistrer**.

Ce résultat dans n’importe quel tooSlack d’objets attribués groupe Bonjour **utilisateurs et groupes** section complètement synchronisés à partir d’Azure AD tooSlack. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service dans votre application de marge.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-enterprise-apps-manage-provisioning.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
