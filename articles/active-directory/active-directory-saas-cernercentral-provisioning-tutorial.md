---
title: "Didacticiel : Configuration de Cerner Central pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory | Microsoft Docs"
description: "Découvrez comment tooconfigure Azure Active Directory tooautomatically configurer la liste de tooa d’utilisateurs dans le centre de Cerner."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>Didacticiel : Configuration de Cerner Central pour l’approvisionnement automatique d’utilisateurs

objectif Hello de ce didacticiel est tooshow vous hello étapes que vous devez tooperform dans le centre de Cerner et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir de la liste d’utilisateur Azure AD tooa Cerner central. 


## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un client Azure Active Directory
*   Un locataire Cerner Central 

> [!NOTE]
> Azure Active Directory s’intègre à Cerner les Central à l’aide de hello [SCIM](http://www.simplecloud.info/) protocole.

## <a name="assigning-users-toocerner-central"></a>Affectation d’utilisateurs tooCerner Central

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD sont synchronisés. 

Avant de configurer et de l’activation de hello service de configuration, vous devez décider quels utilisateurs ou des groupes dans Azure AD représentent des utilisateurs hello besoin d’accès tooCerner Central. Une fois décidé, vous pouvez attribuer ces tooCerner utilisateurs Central en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>Conseils importants pour l’affectation d’utilisateurs tooCerner Central

*   Il est recommandé qu’un seul utilisateur Azure AD avoir tooCerner tootest centrale hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

* Une fois le test initial terminé pour un seul utilisateur, Cerner centre recommande d’attribuer hello intégralité de la liste des utilisateurs, tooaccess liste utilisateur de n’importe quel Cerner la solution (pas seulement Cerner Central) toobe configuré tooCerner.  Autres solutions Cerner tirer parti de cette liste d’utilisateurs dans la liste des utilisateurs hello.

*   Lorsque vous affectez un tooCerner utilisateur Central, vous devez sélectionner hello **utilisateur** rôle dans la boîte de dialogue attribution hello. Les utilisateurs dotés du rôle de « Accès par défaut » hello sont exclus de l’approvisionnement.


## <a name="configuring-user-provisioning-toocerner-central"></a>Configuration tooCerner centre de configuration de l’utilisateur

Cette section vous guide à travers de la connexion de liste d’utilisateur de votre centre de tooCerner Azure AD à l’aide du compte d’utilisateur de Cerner SCIM API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver l’utilisateur affecté en fonction des comptes dans le centre de Cerner lors de l’attribution d’utilisateurs et de groupes dans Azure AD.

> [!TIP]
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Cerner Central, suivant les instructions hello fournies dans [portail Azure (https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que ces deux fonctionnalités se complètent. Pour plus d’informations, consultez hello [didacticiel l’authentification unique de le Cerner Central](active-directory-saas-cernercentral-tutorial.md).


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>compte d’utilisateur automatique de tooconfigure tooCerner centre de configuration dans Azure AD :


Dans l’ordre tooprovision utilisateur comptes tooCerner Central, seront peut-être toorequest un compte de système de Cerner centre de Cerner et générer un jeton de porteur OAuth que Azure AD peut utiliser de point de terminaison de tooconnect tooCerner SCIM. Il est également recommandé que l’intégration de hello être effectuée dans un environnement de bac à sable Cerner avant de déployer tooproduction.

1.  première étape de Hello est personnes de hello tooensure gestion hello Cerner et intégration d’Azure AD ont un compte CernerCare, qui est requis tooaccess hello documentation nécessaire toocomplete hello instructions. Si nécessaire, utilisez l’URL de hello ci-dessous toocreate CernerCare comptes dans chaque environnement applicable.

   * Bac à sable : https://sandboxcernercare.com/accounts/create

   * Production : https://cernercare.com/accounts/create  

2.  Vous devez ensuite créer un compte système pour Azure AD. Utilisez les instructions de hello ci-dessous toorequest un compte système de votre environnement de bac à sable et de production.

   * Instructions : https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * Bac à sable : https://sandboxcernercentral.com/system-accounts/

   * Production : https://cernercentral.com/system-accounts/

3.  Générez ensuite un jeton du porteur OAuth pour chacun de vos comptes système. toodo, suivez les instructions hello ci-dessous.

   * Instructions : https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * Bac à sable : https://sandboxcernercentral.com/system-accounts/

   * Production : https://cernercentral.com/system-accounts/

4. Enfin, vous devez les ID de domaine liste tooacquire utilisateur pour les deux environnements de production et de bac à sable hello dans la configuration de Cerner toocomplete hello. Pour plus d’informations sur la façon de tooacquire, consultez : https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM. 

5. Vous pouvez maintenant configurer tooCerner de comptes utilisateur Azure AD tooprovision. Connectez-vous à toohello [portail Azure](https://portal.azure.com)et recherchez toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

6. Si vous avez déjà configuré Cerner Central pour l’authentification unique, recherchez votre instance de Cerner les Central à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Cerner centre** dans la galerie d’applications hello. Sélectionnez Cerner Central à partir des résultats de recherche hello et ajouter tooyour la liste des applications.

7.  Sélectionnez votre instance de Cerner Central, puis sélectionnez hello **Provisioning** onglet.

8.  Ensemble hello **Mode d’approvisionnement** trop**automatique**.

   ![Approvisionnement Central Cerner](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  Renseignez hello suivant champs sous **informations d’identification administrateur**:

   * Bonjour **URL de client** , entrez une URL au format hello ci-dessous, en remplaçant « Liste-domaine-ID utilisateur » avec l’ID de domaine hello vous avez acquis à l’étape 4 de #.

> Bac à sable : https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> Production : https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * Bonjour **Secret jeton** , indiquez le jeton de support OAuth hello générés à l’étape #3 et cliquez sur **tester la connexion**.

   * Vous devez voir une notification de réussite supérieurdroit côté hello de votre portail.

10. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello ci-dessous.

11. Cliquez sur **Enregistrer**. 

12. Bonjour **des mappages d’attributs** section, passez en revue les utilisateur hello et toobe d’attributs de groupe synchronisés à partir d’Azure AD tooCerner Central. Hello attributs sélectionnés en tant que **correspondance** propriétés sont utilisées toomatch hello des comptes d’utilisateur et les groupes dans Cerner Centre pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

13. tooenable hello service de configuration d’Azure AD pour Cerner Central, modification hello **état d’approvisionnement** trop**sur** Bonjour **paramètres** section

14. Cliquez sur **Enregistrer**. 

Cela démarre la synchronisation initiale hello de tous les utilisateurs et/ou groupes affectés tooCerner Central dans la section utilisateurs et groupes de hello. la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que hello service de configuration d’Azure AD est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service sur votre application de centre de Cerner l’approvisionnement.

Pour plus d’informations sur l’approvisionnement hello Azure AD tooread du mode de connexion, consultez [création de rapports sur la configuration de compte automatique d’utilisateurs](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Cerner Central: Publishing identity data using Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD) (Cerner Central : Publication des données d’identité à l’aide d’Azure AD)
* [Tutorial: Configuring Cerner Central for single sign-on with Azure Active Directory](active-directory-saas-cernercentral-tutorial.md) (Didacticiel : Configuration de Cerner Central pour l’authentification unique avec Azure Active Directory)
* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-enterprise-apps-manage-provisioning.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Étapes suivantes
* [Découvrez comment tooreview se connecte et obtenir des rapports sur l’activité de configuration](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).
