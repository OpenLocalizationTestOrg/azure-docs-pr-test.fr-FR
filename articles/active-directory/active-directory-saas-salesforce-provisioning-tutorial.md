---
title: "Didacticiel : Intégration d’Azure Active Directory à Salesforce | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la force de vente."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Didacticiel : configuration de Salesforce pour approvisionner automatiquement des utilisateurs

objectif Hello de ce didacticiel est tooshow hello étapes tooperform requis dans Salesforce et Azure AD tooautomatically approvisionner et configurer des comptes d’utilisateur à partir d’Azure AD tooSalesforce.

## <a name="prerequisites"></a>Composants requis

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

*   Un locataire Azure Active Directory.
*   Vous devez posséder un abonné valide pour les éditions Salesforce for Work ou Salesforce for Education. Vous pouvez utiliser un compte d’essai gratuit pour chaque service.
*   Un compte d’utilisateur dans Salesforce avec les autorisations d’administrateur d’équipe.

## <a name="assigning-users-toosalesforce"></a>Affectation d’utilisateurs tooSalesforce

Azure Active Directory utilise un concept appelé toodetermine « affectations » les utilisateurs qui doivent recevoir l’accès tooselected applications. Dans le contexte de hello de configuration de compte automatique d’utilisateurs, seuls les utilisateurs de hello et les groupes qui ont été « affectés » application tooan dans Azure AD est synchronisé.

Avant de configurer et de l’activation de hello service de configuration, vous devez toodecide quels utilisateurs ou des groupes dans Azure AD représentent hello utilisateurs qui doivent accéder à application Salesforce de tooyour. Après choisi, vous pouvez attribuer à ces applications de force de vente tooyour les utilisateurs en suivant les instructions hello ici :

[Affecter une application d’entreprise tooan utilisateur ou un groupe](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>Conseils importants pour l’affectation d’utilisateurs tooSalesforce

*   Il est recommandé qu’un seul utilisateur Azure AD est attribué tooSalesforce tootest hello est mise en service de configuration. Les autres utilisateurs et/ou groupes peuvent être affectés ultérieurement.

*  Lorsque vous affectez un tooSalesforce d’utilisateur, vous devez sélectionner un rôle d’utilisateur valide. rôle de « Accès par défaut » Hello ne fonctionne pas pour la configuration

    > [!NOTE]
    > Cette application importe des rôles personnalisés à partir de la force de vente dans le cadre de processus, le client hello souhaitant tooselect lors de l’affectation d’utilisateurs d’approvisionnement de hello

## <a name="enable-automated-user-provisioning"></a>Activer l’approvisionnement automatique des utilisateurs

Cette section vous guide à travers de la connexion du compte d’utilisateur de votre tooSalesforce AD Azure API de configuration et configurez hello toocreate du service de configuration, de mettre à jour et de désactiver les comptes d’utilisateur affecté dans Salesforce en fonction de l’affectation d’utilisateurs et de groupes dans Azure AD .

>[!Tip]
>Vous pouvez également choisir tooenabled basé sur SAML Single Sign-On pour Salesforce, en suivant les instructions hello fournies dans [portail Azure](https://portal.azure.com). L’authentification unique peut être configurée indépendamment de l’approvisionnement automatique, bien que chacune de ces deux fonctionnalités compléte l’autre.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure compte le provisionnement utilisateur automatique :

objectif Hello de cette section est toooutline mode tooenable l’approvisionnement des utilisateurs d’utilisateur Active Directory de comptes tooSalesforce.

1. Bonjour [portail Azure](https://portal.azure.com), parcourir toohello **Azure Active Directory > applications d’entreprise > toutes les applications** section.

2. Si vous avez déjà configuré la force de vente pour l’authentification unique, recherchez votre instance de la force de vente à l’aide du champ de recherche hello. Sinon, sélectionnez **ajouter** et recherchez **Salesforce** dans la galerie d’applications hello. Sélectionnez la force de vente à partir des résultats de recherche hello et l’ajouter tooyour la liste des applications.

3. Sélectionnez votre instance de force de vente, puis sélectionnez hello **Provisioning** onglet.

4. Ensemble hello **Mode d’approvisionnement** trop**automatique**. 
![Approvisionnement](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. Sous hello **informations d’identification administrateur** section, fournissez hello suivant les paramètres de configuration :
   
    a. Bonjour **nom d’utilisateur Admin** zone de texte, tapez une force de vente de compte nom a hello **administrateur système** profil dans Salesforce.com attribué.
   
    b. Bonjour **mot de passe administrateur** zone de texte, un mot de passe type hello pour ce compte.

6. tooget votre jeton de sécurité Salesforce, ouvrez un nouvel onglet et que vous connectez hello même compte d’administrateur de Salesforce. Sur hello coin supérieur droit de la page de hello, cliquez sur votre nom, puis cliquez sur **mes paramètres**.

     ![Activer l’approvisionnement automatique des utilisateurs](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Activer l’approvisionnement automatique des utilisateurs")
7. Dans le volet de navigation gauche hello, cliquez sur **personnel** tooexpand hello section associée, puis cliquez sur **Reset My Security Token**.
  
    ![Activer l’approvisionnement automatique des utilisateurs](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Activer l’approvisionnement automatique des utilisateurs")
8. Sur hello **Reset My Security Token** , cliquez sur **Reset Security Token** bouton.

    ![Activer l’approvisionnement automatique des utilisateurs](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Activer l’approvisionnement automatique des utilisateurs")
9. Vérifiez hello boîte de réception associé à ce compte d’administrateur. Recherchez un message électronique à partir de Salesforce.com qui contient le nouveau jeton de sécurité hello.
10. Copiez hello jeton, accédez tooyour fenêtre d’Azure AD et collez-le dans hello **Socket jeton** champ.

11. Bonjour portail Azure, cliquez sur **tester la connexion** tooensure AD Azure peut se connecter tooyour Salesforce application.

12. Bonjour **Notification par courrier électronique** , entrez l’adresse de messagerie hello d’une personne ou un groupe qui doit recevoir des notifications de d’erreur et la case hello ci-dessous.

13. Cliquez sur **Enregistrer.**  
    
14.  Sous la section des mappages de hello, sélectionnez **tooSalesforce de synchronisation Azure Active Directory Users.**

15. Bonjour **des mappages d’attributs** section, passez en revue les attributs utilisateur hello qui sont synchronisés à partir d’Azure AD tooSalesforce. Notez que hello attributs sélectionnés en tant que **correspondance** propriétés sont des comptes d’utilisateur hello toomatch utilisés dans Salesforce pour les opérations de mise à jour. Sélectionnez toocommit de bouton hello enregistrer toutes les modifications.

16. tooenable hello service de configuration d’Azure AD pour Salesforce, modification hello **état d’approvisionnement** trop**sur** Bonjour section de paramètres

17. Cliquez sur **Enregistrer.**

Démarre la synchronisation initiale d’utilisateurs et/ou groupes affectés tooSalesforce Bonjour les utilisateurs et la section groupes de hello. Notez que la synchronisation initiale hello prend tooperform plus de temps que les synchronisations suivantes, qui se produisent toutes les 20 minutes environ tant que service de hello est en cours d’exécution. Vous pouvez utiliser hello **détails de synchronisation** section toomonitor cours et suivre des rapports d’activité tooprovisioning des liens, qui décrivent toutes les actions effectuées par hello mise en service du service sur votre application Salesforce.

Vous pouvez à présent créer un compte de test. Attendez que les minutes too20 tooverify hello compte a été synchronisé tooSalesforce.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Gestion de l’approvisionnement de comptes d’utilisateur pour les applications d’entreprise](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’authentification unique](active-directory-saas-salesforce-tutorial.md)