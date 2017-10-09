---
title: "Didacticiel : Configuration de LucidChart pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically disposition et la disposition de l’utilisateur des comptes tooLucidChart."
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
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a>Didacticiel : configuration de LucidChart pour l’approvisionnement automatique d’utilisateurs


objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans LucidChart et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooLucidChart. 

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory
*   Un locataire LucidChart avec hello [plan d’entreprise](https://www.lucidchart.com/user/117598685#/subscriptionLevel) ou mieux activé 
*   Un compte utilisateur dans LucidChart avec des autorisations d’administrateur 

## <a name="assigning-users-toolucidchart"></a>Affectation d’utilisateurs tooLucidChart

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé. 

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application de LucidChart tooyour. Après choisi, vous pouvez attribuer à ces applications de LucidChart tooyour les utilisateurs en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a>Conseils importants pour l’affectation d’utilisateurs tooLucidChart

*   Il est recommandé qu’un seul utilisateur Azure AD est attribué tooLucidChart tootest hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un tooLucidChart d’utilisateur, vous devez sélectionner soit hello **utilisateur** rôle, ou un autre valide spécifique à l’application (si disponible) dans la boîte de dialogue attribution hello. Hello **accès par défaut** rôle ne fonctionne pas pour la configuration, et ces utilisateurs sont ignorés.


## <a name="configuring-user-provisioning-toolucidchart"></a>Configuration tooLucidChart de configuration de l’utilisateur 

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooLucidChart AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans LucidChart en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD .

> [!TIP]
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour LucidChart, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a>Configurer le compte d’automatique de l’utilisateur de configuration tooLucidChart dans Azure AD


1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2. Si vous avez déjà configuré LucidChart pour l’authentification unique, recherchez votre instance de LucidChart à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **LucidChart** dans la galerie d’applications hello. Sélectionnez LucidChart à partir des résultats de recherche hello et ajoutez-le tooyour la liste des applications.

3. Sélectionnez votre instance de LucidChart, puis hello **Provisioning** onglet.

4. Ensemble hello **Mode d’approvisionnement** trop**automatique**.

    ![Approvisionnement de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. Sous hello **informations d’identification administrateur** section, entrée hello **Secret jeton** généré par le compte de votre LucidChart (vous pouvez rechercher le jeton de hello sous votre compte : **Team**  >  **Intégration de l’application** > **SCIM**). 

    ![Approvisionnement de LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour LucidChart application. Si hello connexion échoue, vérifiez que votre compte de LucidChart a des autorisations d’administrateur et recommencez l’étape 5.

7. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher de vérification hello « envoient une notification par courrier électronique lorsqu’une défaillance se produit ».

8. Cliquez sur **Enregistrer**. 

9. Sous la section des mappages de hello, sélectionnez **tooLucidChart de synchronisation Azure Active Directory Users**.

10. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooLucidChart. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans LucidChart pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

11. tooenable hello service de configuration d’Azure AD pour LucidChart, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section

12. Cliquez sur **Enregistrer**. 

Cette opération démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooLucidChart Bonjour les utilisateurs et la section groupes de hello. la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service de configuration.

Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-enterprise-apps-manage-provisioning.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Étapes suivantes

* [Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration](active-directory-saas-provisioning-reporting.md)
