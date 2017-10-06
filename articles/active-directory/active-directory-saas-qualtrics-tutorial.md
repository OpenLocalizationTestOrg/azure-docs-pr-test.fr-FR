---
title: "Didacticiel : Intégration d’Azure Active Directory à Qualtrics | Microsoft Docs"
description: "Découvrez comment toouse Qualtrics avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a>Didacticiel : Intégration d’Azure Active Directory avec Qualtrics
objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure à Qualtrics.  

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un abonnement Qualtrics pour lequel l’authentification unique est activée

À l’issue de ce didacticiel, hello Azure AD utilisateurs tooQualtrics sera toosingle en mesure de l’authentification sur application hello à votre site d’entreprise Qualtrics (service initiée par le fournisseur de session) ou à l’aide de hello [Introduction toohello Accéder au panneau de configuration](active-directory-saas-access-panel-introduction.md).

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

1. Activation de l’intégration d’application hello pour Qualtrics
2. Configuration de l’authentification unique (SSO)
3. Configuration de l'approvisionnement des utilisateurs
4. Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scénario")

## <a name="enabling-hello-application-integration-for-qualtrics"></a>Activation de l’intégration d’application hello pour Qualtrics
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Qualtrics.

**intégration d’application hello tooenable pour Qualtrics, procédez hello comme suit :**

1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
   ![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")
4. Cliquez sur **ajouter** bas hello de page de hello.
   
   ![Ajouter une application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Ajouter une application")
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
   ![Ajouter une application à partir de la galerie](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Bonjour **zone de recherche**, type **Qualtrics**.
   
   ![Galerie d’applications](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Galerie d’applications")
7. Dans le volet de résultats hello, sélectionnez **Qualtrics**, puis cliquez sur **Complete** application hello de tooadd.
   
   ![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooQualtrics avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello **Qualtrics** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configurer l’authentification unique")
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooQualtrics** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configurer l’authentification unique")
3. Sur hello **Configure App URL** page hello **Qualtrics URL de connexion** zone de texte, tapez votre URL (par exemple : «*https://ssotest2ut1.qualtrics.com*»), puis cliquez sur **Suivant**.
   
   ![Configurer l’URL de l’application](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configurer l’URL de l’application")
4. Sur hello **configurer l’authentification unique sur Qualtrics** , cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier de métadonnées hello sur votre ordinateur.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configurer l’authentification unique")
5. Envoyer toohello de fichier de métadonnées hello équipe de support Qualtrics.
   
   >[!NOTE]
   >configuration de SSO Hello a toobe effectuée par l’équipe de support Qualtrics de hello. Vous recevez une notification dès que hello configuration a été effectuée.
   > 
   > 
6. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configurer l’authentification unique")
   
## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur

Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooQualtrics. Quand un utilisateur affecté tente de toolog à Qualtrics à l’aide du volet d’accès hello, Qualtrics vérifie l’existence d’un utilisateur de hello.  

Si aucun compte d'utilisateur n’est disponible, Qualtrics le crée automatiquement.

## <a name="assign-users"></a>Affecter des utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

**tooassign utilisateurs tooQualtrics, effectuez hello comme suit :**

1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello **Qualtrics** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
   ![Oui](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

