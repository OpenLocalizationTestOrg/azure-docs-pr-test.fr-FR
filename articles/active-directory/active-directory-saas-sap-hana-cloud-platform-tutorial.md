---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform | Microsoft Docs"
description: "Découvrez comment toouse SAP HANA Cloud Platform avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Didacticiel : Intégration d’Azure Active Directory avec SAP HANA Cloud Platform
objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et la plateforme Cloud SAP HANA.

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un compte SAP HANA Cloud Platform

À l’issue de ce didacticiel, hello utilisateurs Azure AD que vous avez affectés tooSAP HANA Cloud Platform sera toosingle en mesure de connexion dans l’application hello utilisant hello [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Vous devez toodeploy votre propre application ou s’abonner tooan application sur votre serveur SAP HANA Cloud Platform connectent tootest compte unique. Dans ce didacticiel, une application est déployée dans le compte de hello.
> 
> 

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

1. Activation de l’intégration d’application hello pour SAP HANA Cloud Platform
2. Configuration de l’authentification unique (SSO)
3. Affectation d’un utilisateur tooa de rôle
4. Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scénario")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>Activation de l’intégration d’application hello pour SAP HANA Cloud Platform
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour SAP HANA Cloud Platform.

**intégration d’application hello tooenable pour SAP HANA Cloud Platform, procédez hello comme suit :**

1. Bonjour portail de gestion Azure, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")
4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Ajouter une application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Ajouter une application")
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Ajouter une application à partir de la galerie](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Bonjour **zone de recherche**, type **SAP HANA Cloud Platform**.
   
    ![Galerie d’applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galerie d’applications")
7. Dans le volet de résultats hello, sélectionnez **SAP HANA Cloud Platform**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooSAP HANA Cloud Platform avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.

Dans le cadre de cette procédure, vous êtes tooupload requis un locataire de SAP HANA Cloud Platform tooyour certificat codé en base 64.  

Si vous n’êtes pas familiarisé avec cette procédure, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello **SAP HANA Cloud Platform** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique**boîte de dialogue.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurer l’authentification unique")
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooSAP HANA Cloud Platform** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurer l’authentification unique")
3. Dans une fenêtre de navigateur web, connectez-vous toohello Cockpit de plateforme Cloud SAP HANA à https://account. \<hôte du paysage\>.ondemand.com/cockpit (par exemple : *https://account.hanatrial.ondemand.com/cockpit*).
4. Cliquez sur hello **confiance** onglet.
   
    ![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")
5. Dans la section Gestion de confiance, effectuez hello comme suit :
   
    ![Obtenir les métadonnées](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obtenir les métadonnées")
   
   1. Cliquez sur hello **Local Service Provider** onglet.
   2. hello de toodownload fichier de métadonnées de plateforme Cloud SAP HANA, cliquez sur **obtenir les métadonnées**.
6. Portail de classique hello Active Azure, sur hello **Configure App URL** page, effectuer hello comme suit, puis cliquez sur **suivant**.
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurer l’URL de l’application")
   
   1. Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par votre toosign d’utilisateurs dans votre **SAP HANA Cloud Platform** application. Il s’agit de hello URL spécifique au compte d’une ressource protégée dans votre application SAP HANA Cloud Platform. URL Hello est basée sur hello modèle : *https://\<applicationName\>\<accountName\>.\< hôte de paysage\>.ondemand.com/\<chemin d’accès\_à\_protégé\_ressource\>*  (par exemple : *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Il s’agit d’URL de hello dans votre application de plateforme Cloud SAP HANA nécessitant hello utilisateur tooauthenticate.
     > 

   2. Ouvrez le fichier de métadonnées de plateforme Cloud SAP HANA hello téléchargé et recherchez hello **NS3 : assertionconsumerservice** balise.
   3. Copier la valeur hello Hello **emplacement** d’attribut, puis collez-le dans hello **URL de réponse SAP HANA Cloud Platform** zone de texte.

7. Sur hello **configurer l’authentification unique sur SAP HANA Cloud Platform** page, toodownload vos métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello sur votre ordinateur.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurer l’authentification unique")
8. Sur hello Cockpit de plateforme Cloud SAP HANA, Bonjour **Local Service Provider** section, effectuer hello comme suit :
   
    ![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")
   
  1. Cliquez sur **Modifier**.
  2. Comme **Configuration Type**, sélectionnez **Custom**.
  3. En tant que **Local Provider Name**, laissez la valeur par défaut de hello.
  4. toogenerate un **clé de signature** et un **certificat de signature de** paire de clés, cliquez sur **générer la paire de clés**.
  5. Pour **Principal Propagation**, sélectionnez **Disabled**.
  6. Pour **Force Authentication**, sélectionnez **Disabled**.
  7. Cliquez sur **Enregistrer**.

9. Cliquez sur hello **fournisseur d’identité approuvé** onglet, puis cliquez sur **ajouter un fournisseur d’identité approuvé**.
   
    ![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")
   
    >[!NOTE]
    >liste de hello toomanage de fournisseurs d’identité approuvés, vous devez toohave choisi hello type de configuration personnalisée dans hello section Local Service Provider. Pour le type de configuration par défaut, vous avez un Service d’ID SAP de toohello approbation non modifiable et implicite. Pour None, vous n’avez aucun paramètre d’approbation.
    > 
    > 

10. Cliquez sur hello **général** onglet, puis cliquez sur **Parcourir** hello de tooupload téléchargé le fichier de métadonnées.
    
    ![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")
    
    >[!NOTE]
    >Après avoir téléchargé le fichier de métadonnées hello, des valeurs hello **URL de connexion unique**, **URL de déconnexion unique** et **certificat de signature** sont remplis automatiquement.
    > 
    > 

11. Cliquez sur hello **attributs** onglet.
12. Sur hello **attributs** onglet, effectuez hello suivant l’étape :
    
    ![Attributs](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributs") 
  * Cliquez sur **based Attribute**, puis ajoutez hello suivant des attributs basés sur une assertion :
       
    | Assertion Attribute | Principal Attribute |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |firstname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |Lastname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |email 
   
     >[!NOTE]
     >configuration Hello d’attributs de hello dépend de l’ou les applications hello sur HCP sont développées, autrement dit, attributs attendus dans hello réponse SAML et sous le nom (attribut Principal) qu’ils accèdent à cet attribut dans le code hello.
     > 
     >  

    1.  Hello **attribut par défaut** Bonjour capture d’écran est uniquement à des fins d’illustration. Il n’est pas nécessaire de travail de scénario toomake hello.   
    2.  Hello les noms et valeurs des **attribut Principal** illustré hello capture d’écran dépendent de la façon dont l’application hello est développée. Il est possible que votre application exige des mappages différents.
     
13. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur SAP HANA Cloud Platform** page de boîte de dialogue, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete**.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurer l’authentification unique")

###<a name="assertion-based-groups"></a>Groupes basés sur une assertion
Une étape facultative est de configurer des groupes basés sur une assertion pour votre fournisseur d’identité Azure Active Directory.

À l’aide de groupes sur SAP HANA Cloud Platform vous permet d’affecter toodynamically un ou plus tooone d’utilisateurs ou de plusieurs rôles dans vos applications SAP HANA Cloud Platform, déterminés par les valeurs des attributs de hello SAML 2.0 assertion. 

Par exemple, si hello assertion contenant l’attribut de hello »*contrat = temporaire*«, vous pouvez tous les utilisateurs affectés toobe toohello ajouté groupe »*temporaire*». groupe de Hello »*temporaire*» peut contenir un ou plusieurs rôles à partir d’une ou plusieurs applications déployées dans votre compte SAP HANA Cloud Platform.
 
Utilisez des groupes basés sur une assertion toosimultaneously affecter plusieurs utilisateurs tooone ou plusieurs rôles d’applications dans votre compte SAP HANA Cloud Platform. Si vous ne souhaitez qu’un seul ou un petit nombre de rôles d’utilisateurs toospecific de tooassign, nous vous recommandons de les affecter directement dans hello »**autorisations**« onglet du cockpit de plateforme Cloud SAP HANA hello.

## <a name="assign-a-role-tooa-user"></a>Affecter un utilisateur tooa de rôle
Dans l’ordre tooenable Azure AD les utilisateurs toolog dans SAP HANA Cloud Platform, vous devez attribuer des rôles dans hello SAP HANA Cloud Platform toothem.

**tooassign un utilisateur tooa de rôle, effectuez hello comme suit :**

1. Connectez-vous à tooyour **SAP HANA Cloud Platform** cockpit.
2. Effectuez les opérations suivantes de hello :
   
   ![Autorisations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorisations")
   
  1. Cliquez sur **Authorization**.
  2. Cliquez sur hello **utilisateurs** onglet.
  3. Bonjour **utilisateur** zone de texte, adresse de messagerie de l’utilisateur de type hello.
  4. Cliquez sur **affecter** rôle tooa tooassign hello.
  5. Cliquez sur **Enregistrer**.

## <a name="assign-users"></a>Affecter des utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

**tooassign utilisateurs tooSAP HANA Cloud Platform, procédez hello comme suit :**

1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello **SAP HANA Cloud Platform** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
   ![Oui](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

