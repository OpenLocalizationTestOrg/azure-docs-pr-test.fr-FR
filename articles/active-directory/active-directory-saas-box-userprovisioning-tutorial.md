---
title: "Tutorial: Intégration d'Azure Active Directory à Box | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de zone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Didacticiel : Configuration de Box pour l’attribution automatique d’utilisateurs

objectif Hello de ce didacticiel est tooshow hello étapes tooperform dans la zone et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooBox.

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory.
*   Un abonnement Box pour lequel l’authentification unique est activée
*   Un compte d’utilisateur Box avec des autorisations d’administrateur d’équipe

## <a name="assigning-users-toobox"></a>Affectation d’utilisateurs tooBox 

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à l’application Box tooyour. Après choisi, vous pouvez attribuer à ces utilisateurs l’application Box tooyour en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Affecter des utilisateurs et des groupes
Hello **zone > utilisateurs et groupes** onglet Bonjour portail Azure vous permet de toospecify les utilisateurs et groupes doit avoir accès tooBox. Affectation d’un utilisateur ou un groupe, Bonjour suivant toooccur de choses :

* Azure AD autorise hello affecté utilisateur (soit par assignation directe ou l’appartenance au groupe) tooauthenticate tooBox. Si un utilisateur n’est pas affecté, Azure AD n’autorise pas les toosign dans tooBox et renvoie une erreur sur la page de connexion Azure AD hello.
* Une vignette de l’application pour la zone est ajoutée à l’utilisateur toohello [Lanceur d’applications](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).
* Si la configuration automatique est activée, hello affecté utilisateurs et/ou groupes sont ajoutés toohello configuration toobe de file d’attente configuré automatiquement.
  
  * Si seuls les objets utilisateur ont été configuré toobe configuré, puis tous les utilisateurs directement attribués sont placés dans la file d’attente de la mise en service hello et tous les utilisateurs qui sont membres des groupes affectées sont placés dans hello mise en service de file d’attente. 
  * Si les objets de groupe ont été configuré toobe configuré, tous les objets de groupe affecté sont approvisionné tooBox et tous les utilisateurs qui sont membres de ces groupes. les appartenances de groupe et utilisateur Hello sont conservés lors de tooBox en cours d’écriture.

Vous pouvez utiliser hello **attributs > Single Sign-On** onglet tooconfigure les attributs de l’utilisateur (ou les revendications) est présenté tooBox pendant l’authentification SAML et hello **attributs > approvisionnement** onglet tooconfigure le flux des attributs utilisateur et de groupe à partir d’Azure AD tooBox lors de la configuration des opérations.

### <a name="important-tips-for-assigning-users-toobox"></a>Conseils importants pour l’affectation d’utilisateurs tooBox 

*   Il est recommandé qu’une annonce Azure utilisateur attribué tooBox tootest hello service de la configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*   Lorsque vous affectez un toobox d’utilisateur, vous devez sélectionner un rôle d’utilisateur valide. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration.

## <a name="enable-automated-user-provisioning"></a>Activer l’approvisionnement automatique des utilisateurs

Cette section guide tout au long de la connexion du compte d’utilisateur de votre tooBox AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans la zone en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD.

Si la configuration automatique est activée, hello affecté utilisateurs et/ou groupes sont ajoutés toohello configuration toobe de file d’attente configuré automatiquement.
    
 * Si seuls les objets utilisateur sont configuré toobe configurée, puis directement les utilisateurs sont placés dans la file d’attente de la mise en service hello et tous les utilisateurs qui sont membres des groupes affectées sont placés dans hello mise en service de file d’attente. 
    
 * Si les objets de groupe ont été configuré toobe configuré, tous les objets de groupe affecté sont approvisionné tooBox et tous les utilisateurs qui sont membres de ces groupes. les appartenances de groupe et utilisateur Hello sont conservés lors de tooBox en cours d’écriture.

> [!TIP] 
> Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour la zone, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure compte le provisionnement utilisateur automatique :

objectif Hello de cette section est toooutline comment tooenable configuration d’utilisateur Active Directory de comptes de tooBox.

1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2. Si vous avez déjà configuré la zone pour l’authentification unique, recherchez votre instance de la zone à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **zone** dans la galerie d’applications hello. Activez la case à partir des résultats de recherche hello et ajoutez-le à la liste des applications tooyour.

3. Sélectionnez votre instance de la zone, puis hello **Provisioning** onglet.

4. Ensemble hello **Mode d’approvisionnement** trop**automatique**. 

    ![approvisionnement](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. Sous hello **informations d’identification administrateur** , cliquez sur **Authorize** tooopen une boîte de dialogue de connexion dans une nouvelle fenêtre de navigateur.

6. Sur hello **connexion toogrant accès tooBox** page, fournir des informations d’identification hello requis, puis cliquez sur **Authorize**. 
   
    ![Activer l’approvisionnement automatique des utilisateurs](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Activer l’approvisionnement automatique des utilisateurs")

7. Cliquez sur **Grant access tooBox** tooauthorize cette toohello opération et tooreturn portail Azure. 
   
    ![Activer l’approvisionnement automatique des utilisateurs](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Activer l’approvisionnement automatique des utilisateurs")

8. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter à l’application Box tooyour. Si hello connexion échoue, assurez-vous que votre compte Box a des autorisations d’administrateur d’équipe et essayez de hello **« Autoriser »** pas à pas.

9. Entrez hello adresse de messagerie d’une personne ou un groupe qui doit recevoir des notifications d’erreur approvisionnement hello **courrier électronique de Notification** champ et la case à cocher hello.

10. Cliquez sur **Enregistrer.**

11. Sous la section des mappages de hello, sélectionnez **tooBox de synchronisation Azure Active Directory Users.**

12. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooBox. Hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans la zone pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

13. tooenable hello service de configuration d’Azure AD de zone de modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres

14. Cliquez sur **Enregistrer.**

Qui démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooBox Bonjour les utilisateurs et la section groupes de hello. la synchronisation initiale Hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello service sur votre application de la zone de configuration.

Vous pouvez à présent créer un compte de test. Attendez que les minutes too20 tooverify hello compte a été synchronisé toobox.

Dans votre locataire Box, les utilisateurs synchronisés sont répertoriés sous **Managed Users** Bonjour **Console d’administration**.

![Statut d’intégration](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Statut d’intégration")


## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-box-tutorial.md)