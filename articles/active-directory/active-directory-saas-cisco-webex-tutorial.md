---
title: "Didacticiel : Intégration d’Azure Active Directory à Cisco Webex | Microsoft Docs"
description: "Découvrez comment toouse Cisco Webex avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a>Didacticiel : Intégration d’Azure Active Directory à Cisco Webex
objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Cisco Webex.  
scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un locataire Cisco Webex

À l’issue de ce didacticiel, hello utilisateurs Azure AD que vous avez affectés tooCisco Webex sera en mesure de toosingle signe dans une application hello sur votre site d’entreprise Cisco Webex (service initiée par le fournisseur de session), ou à l’aide de hello [Introduction toohello Accéder au panneau de configuration](active-directory-saas-access-panel-introduction.md).

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

* Activation de l’intégration d’application hello pour Cisco Webex
* Configuration de l’authentification unique (SSO)
* Configuration de l'approvisionnement des utilisateurs
* Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scénario")

## <a name="enable-hello-application-integration-for-cisco-webex"></a>Activer l’intégration d’application hello pour Cisco Webex
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Cisco Webex.

**intégration d’application hello tooenable pour Cisco Webex, procédez hello comme suit :**

1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
   ![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")
4. Cliquez sur **ajouter** bas hello de page de hello.
   
   ![Ajouter une application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Ajouter une application")
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
   ![Ajouter une application à partir de la galerie](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Bonjour **zone de recherche**, type **Cisco Webex**.
   
   ![Galerie d’applications](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Galerie d’applications")
7. Dans le volet de résultats hello, sélectionnez **Cisco Webex**, puis cliquez sur **Complete** application hello de tooadd.
   
   ![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooCisco Webex avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.  

Dans le cadre de cette procédure, vous êtes toocreate requis un certificat codé en base 64. Si vous n’êtes pas familiarisé avec cette procédure, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello **Cisco Webex** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configurer l’authentification unique")
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooCisco Webex** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configurer l’authentification unique")
3. Sur hello **Configure App URL** page, effectuer hello comme suit, puis cliquez sur **suivant**.
   
   ![Configurer l’URL de l’application](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configurer l’URL de l’application")   
   1. Bonjour **URL de connexion** zone de texte, tapez l’URL de votre client Cisco Webex (par exemple : *http://contoso.webex.com*).
   2. Bonjour **URL de réponse Cisco Webex** zone de texte, type votre **URL AssertionConsumerService Cisco Webex** (par exemple : *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).
4. Sur hello **configurer l’authentification unique sur Cisco Webex** page, toodownload votre certificat, cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello sur votre ordinateur.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configurer l’authentification unique")
5. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Cisco Webex en tant qu’administrateur.
6. Dans le menu hello haut de hello, cliquez sur **Site Administration**.
   
   ![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")
7. Bonjour **gérer le Site** , cliquez sur **Configuration SSO**.
   
   ![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")
8. Dans la section de Configuration de SSO de Web fédéré de hello, procédez hello comme suit :
   
   ![Configuration de l’authentification unique web fédérée](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Configuration de l’authentification unique web fédérée")  
   1. À partir de hello **protocole Federation** liste, sélectionnez **SAML 2.0**.
   2. Créez un fichier **codé en base 64** à partir du certificat téléchargé.  
    >[!TIP]
    >Pour plus d’informations, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o)
    >  
   3. Ouvrez votre certificat codé en base 64 dans le bloc-notes, puis hello copie contenu de celui-ci.
   4. Cliquez sur **Import SAML Metadata**, puis collez votre certificat codé en base 64.
   5. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Cisco Webex** page de boîte de dialogue, hello de copie **URL de l’émetteur** valeur, puis collez-le dans hello **émetteur pour SAML (ID d’IdP)** zone de texte.
   6. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Cisco Webex** page de boîte de dialogue, hello de copie **URL de connexion distante** valeur, puis collez-le dans hello **connexion de Service d’authentification unique client URL** zone de texte.
   7. À partir de hello **NameID Format** liste, sélectionnez **adresse de messagerie**.
   8. Bonjour **AuthnContextClassRef** zone de texte, type **urn : oasis : noms : tc : SAML:2.0:ac:classes:Password**.
   9. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Cisco Webex** page de boîte de dialogue, hello de copie **URL de déconnexion distante** valeur, puis collez-le dans hello **déconnexion du Service client SSO URL** zone de texte.
   10. Cliquez sur **Update**.
9. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Cisco Webex** page de boîte de dialogue, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configurer l’authentification unique")
   
## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur

Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Cisco Webex, ils doivent être configurés dans Cisco Webex.  

* Dans les cas de hello de Cisco Webex, cette configuration est une tâche manuelle.

**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**

1. Connectez-vous à tooyour **Cisco Webex** client.
2. Accédez trop**gérer les utilisateurs \> ajouter un utilisateur**.
   
   ![Ajouter des utilisateurs](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Ajouter des utilisateurs")
3. Sur la section Ajouter un utilisateur de hello, procédez hello comme suit :
   
   ![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")   
   1. Dans la zone **Account Type**, sélectionnez **Host**.
   2. Tapez les informations de hello d’un utilisateur Azure AD existant dans hello suivant des zones de texte : **prénom, le nom**, **nom d’utilisateur**, **messagerie**, **mot de passe**, **Confirmer le mot de passe**.
   3. Cliquez sur **Add**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Cisco Webex utilisateur compte outil de création ou API fournie par Cisco Webex tooprovision des comptes d’utilisateur AAD. 
> 

## <a name="assign-users"></a>Affecter des utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

**tooassign utilisateurs tooCisco Webex, procédez hello comme suit :**

1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello **Cisco Webex** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
   ![Oui](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

