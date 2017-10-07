---
title: "Didacticiel : configuration de GitHub pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooGitHub."
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
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a>Didacticiel : configuration de GitHub pour l’approvisionnement automatique d’utilisateurs


objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans GitHub et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooGitHub. 

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory
*   Un locataire Github avec hello [offre commerciale](https://help.github.com/articles/organization-billing-plans/#business-plan) ou mieux activé 
*   Un compte d’utilisateur dans GitHub avec des autorisations d’administrateur 

> [!NOTE]
> Hello mise en service d’intégration de Azure AD s’appuie sur hello [GitHub SCIM API](https://developer.github.com/v3/scim/), qui est disponible tooGithub équipes sur le plan d’entreprise hello ou supérieures.

## <a name="assigning-users-toogithub"></a>Affectation d’utilisateurs tooGitHub

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé. 

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de GitHub tooyour. Après choisi, vous pouvez attribuer à ces applications de GitHub tooyour les utilisateurs en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a>Conseils importants pour l’affectation d’utilisateurs tooGitHub

*   Il est recommandé qu’un seul utilisateur Azure AD est attribué tooGitHub tootest hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooGitHub d’utilisateur, vous devez sélectionner soit hello **utilisateur** rôle, ou un autre valide spécifique à l’application (si disponible) dans la boîte de dialogue attribution hello. Hello **accès par défaut** rôle ne fonctionne pas pour la configuration, et ces utilisateurs sont ignorés.


## <a name="configuring-user-provisioning-toogithub"></a>Configuration tooGitHub de configuration de l’utilisateur 

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooGitHub AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans GitHub en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.

> [!TIP]
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour GitHub, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a>Configurer le compte d’automatique de l’utilisateur de configuration tooGitHub dans Azure AD


1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2. Si vous avez déjà configuré GitHub pour l’authentification unique, recherchez votre instance de GitHub à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **GitHub** dans la galerie d’applications hello. Sélectionnez GitHub à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

3. Sélectionnez votre instance de GitHub, puis hello **Provisioning** onglet.

4. Ensemble hello **Mode d’approvisionnement** trop**automatique**.

    ![Approvisionnement GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. Sous hello **informations d’identification administrateur** , cliquez sur **Authorize**. Cette opération ouvre une boîte de dialogue d’autorisation GitHub dans une nouvelle fenêtre du navigateur. 

6. Dans la nouvelle fenêtre de hello, connectez-vous à GitHub à l’aide de votre compte d’administrateur. Hello résultant d’autorisation boîte de dialogue, sélectionnez équipe de GitHub hello que vous souhaitez la préparation de tooenable, puis sélectionnez **Authorize**. Une fois terminée, retournez toohello toocomplete portail Azure hello est mise en service de configuration.

    ![Boîte de dialogue d’autorisation](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. Bonjour portail Azure, d’entrée **URL de client** et cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour GitHub application. Si hello connexion échoue, vérifiez votre compte GitHub dispose des autorisations administratives et **URl de client** vous entrez correctement, puis essayez de hello à nouveau l’étape « Autoriser » (vous pouvez constituer **URL de client** par règle : « https : //api.github.com/scim/v2/organizations/ + < Organizations_name > », vous pouvez trouver votre organisation sous votre compte GitHub : **paramètres** > **organisations**).

    ![Boîte de dialogue d’autorisation](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher de vérification hello « envoient une notification par courrier électronique lorsqu’une défaillance se produit ».

9. Cliquez sur **Enregistrer**. 

10. Sous la section des mappages de hello, sélectionnez **tooGitHub de synchronisation Azure Active Directory Users**.

11. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooGitHub. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans GitHub pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

12. tooenable hello service de configuration d’Azure AD pour GitHub, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section

13. Cliquez sur **Enregistrer**. 

Cette opération démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooGitHub Bonjour les utilisateurs et la section groupes de hello. la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service de configuration.

Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-enterprise-apps-manage-provisioning.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Étapes suivantes

* [Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration](active-directory-saas-provisioning-reporting.md)
