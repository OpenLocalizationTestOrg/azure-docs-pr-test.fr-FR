---
title: "Didacticiel : Configuration de LinkedIn Lookup pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooLinkedIn recherche."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 3e41abb8af00715f70e5a14d9d26ff600c10f492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-lookup-for-automatic-user-provisioning"></a>Didacticiel : Configuration de LinkedIn Lookup pour approvisionner automatiquement des utilisateurs


objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans recherche de LinkedIn et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooLinkedIn recherche. 

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un client Azure Active Directory
*   Un locataire LinkedIn Lookup 
*   Un compte d’administrateur dans la recherche de LinkedIn avec accès toohello LinkedIn centre des comptes

> [!NOTE]
> Azure Active Directory s’intègre à la recherche de LinkedIn à l’aide de hello [SCIM](http://www.simplecloud.info/) protocole.

## <a name="assigning-users-toolinkedin-lookup"></a>Affectation d’utilisateurs tooLinkedIn recherche

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD seront synchronisés. 

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent des utilisateurs ayant besoin d’accès tooLinkedIn recherche hello. Une fois choisi, vous pouvez attribuer ces tooLinkedIn utilisateurs recherche en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-lookup"></a>Conseils importants pour l’affectation d’utilisateurs tooLinkedIn recherche

*   Il est recommandé qu’un seul utilisateur Azure AD avoir hello de tootest tooLinkedIn recherche mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooLinkedIn utilisateur recherche, vous devez sélectionner hello **utilisateur** rôle dans la boîte de dialogue attribution hello. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.


## <a name="configuring-user-provisioning-toolinkedin-lookup"></a>Configuration tooLinkedIn recherche de configuration de l’utilisateur

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre recherche tooLinkedIn Azure AD SCIM API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver l’utilisateur affecté comptes dans la recherche de LinkedIn basés sur des utilisateurs et de groupes affectation dans Azure AD.

> [!TIP]
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour la recherche LinkedIn, suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-lookup-in-azure-ad"></a>compte d’utilisateur automatique de tooconfigure tooLinkedIn recherche de configuration dans Azure AD :


première étape de Hello est tooretrieve votre jeton d’accès LinkedIn. Si vous êtes administrateur d’entreprise, vous pouvez approvisionner vous-même un jeton d’accès. Dans votre centre de gestion, accédez trop**paramètres &gt; paramètres globaux** et ouvrez hello **SCIM le programme d’installation** Panneau de configuration.

> [!NOTE]
> Si vous accédez au centre des comptes hello directement plutôt que via un lien, vous pouvez également accéder à l’aide de hello comme suit.

1)  Connectez-vous tooAccount Center.

2)  Sélectionnez **Administrateur &gt; Paramètres d’administration**.

3)  Cliquez sur **avancé des intégrations** sur le volet gauche hello. Vous êtes dirigé toohello centre des comptes.

4)  Cliquez sur **+ ajouter une nouvelle configuration de SCIM** et suivez la procédure de hello en remplissant chaque champ.

> Si l’affectation automatique de licences n’est pas activée, cela signifie que seules les données utilisateur sont synchronisées.

![Approvisionnement LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_1.PNG)

> Lorsque l’attribution autolicense est activée, vous devez toonote l’instance d’application et le type de licence. Les licences sont attribuées sur un premier arrivé, traiter tout d’abord base jusqu'à ce que toutes les licences hello sont effectuées.

![Approvisionnement LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_2.PNG)

5)  Cliquez sur **Générer un jeton**. Vous devez voir votre affichage de jeton d’accès sous hello **jeton d’accès** champ.

6)  Enregistrez votre accès au jeton tooyour Presse-papiers ou un ordinateur avant de quitter la page de hello.

7) Ensuite, connectez-vous à toohello [portail Azure](https://portal.azure.com), puis accédez toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

8) Si vous avez déjà configuré LinkedIn recherche pour l’authentification unique, recherchez votre instance de recherche LinkedIn à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **LinkedIn recherche** dans la galerie d’applications hello. Sélectionnez LinkedIn recherche à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

9)  Sélectionnez votre instance de la recherche LinkedIn, puis hello **Provisioning** onglet.

10) Ensemble hello **Mode d’approvisionnement** trop**automatique**.

![Approvisionnement LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_3.PNG)

11)  Renseignez hello suivant champs sous **informations d’identification administrateur** :

* Bonjour **URL de client** , saisissez https://api.linkedin.com.

* Bonjour **Secret jeton** , indiquez le jeton d’accès hello générés à l’étape 1 et cliquez sur **tester la connexion** .

* Vous devez voir une notification de réussite supérieurdroit côté hello de votre portail.

12) Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello ci-dessous.

13) Cliquez sur **Enregistrer**. 

14) Bonjour **des mappages d’attributs** section, passez en revue les attributs d’utilisateur et groupe hello qui seront synchronisés à partir d’Azure AD tooLinkedIn recherche. Notez que hello attributs sélectionnés en tant que **correspondance** propriétés seront utilisées toomatch hello des comptes d’utilisateur et les groupes dans LinkedIn recherche pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

![Approvisionnement LinkedIn Lookup](./media/active-directory-saas-linkedinlookup-provisioning-tutorial/linkedin_4.PNG)

15) tooenable hello service de configuration d’Azure AD pour la recherche LinkedIn, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section

16) Cliquez sur **Enregistrer**. 

Cela permet de démarrer la synchronisation initiale hello de tous les utilisateurs et/ou groupes affectés tooLinkedIn recherche dans la section utilisateurs et groupes de hello. Notez que la synchronisation initiale hello a tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service dans votre application de recherche de LinkedIn.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-enterprise-apps-manage-provisioning.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
