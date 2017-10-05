---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP HANA Cloud Platform | Microsoft Docs"
description: "Apprenez à utiliser SAP HANA Cloud Platform avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore !"
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
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Didacticiel : Intégration d’Azure Active Directory avec SAP HANA Cloud Platform
L’objectif de ce didacticiel est de montrer comment intégrer Azure et SAP HANA Cloud Platform.

Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :

* Un abonnement Azure valide
* Un compte SAP HANA Cloud Platform

À l’issue de ce didacticiel, les utilisateurs d’Azure AD que vous avez affectés à SAP HANA Cloud Platform pourront s’authentifier de manière unique dans l’application (connexion initiée par le fournisseur du service) à l’aide de la [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Vous devez déployer votre propre application ou vous abonner à une application sur votre compte SAP HANA Cloud Platform pour tester l’authentification unique. Dans ce didacticiel, une application est déployée dans le compte.
> 
> 

Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :

1. Activation de l’intégration d’application pour SAP HANA Cloud Platform
2. Configuration de l’authentification unique (SSO)
3. Affectation d’un rôle à un utilisateur
4. Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scénario")

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a>Activation de l’intégration d’application pour SAP HANA Cloud Platform
Cette section décrit l’activation de l’intégration d’application pour SAP HANA Cloud Platform.

**Pour activer l’intégration d’applications pour SAP HANA Cloud Platform, procédez comme suit :**

1. Dans le volet de navigation gauche du portail de gestion Azure, cliquez sur **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.
3. Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.
   
    ![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")
4. Cliquez sur **Ajouter** en bas de la page.
   
    ![Ajouter une application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Ajouter une application")
5. Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.
   
    ![Ajouter une application à partir de la galerie](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Dans la **zone de recherche**, tapez **SAP HANA Cloud Platform**.
   
    ![Galerie d’applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galerie d’applications")
7. Dans le volet des résultats, sélectionnez **SAP HANA Cloud Platform**, puis cliquez sur **Terminer** pour ajouter l’application.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

Cette section explique comment permettre aux utilisateurs de s’authentifier sur SAP HANA Cloud Platform avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.

Dans le cadre de cette procédure, vous devez créer un fichier de certificat codé en base 64 sur votre locataire SAP HANA Cloud Platform.  

Si cette procédure ne vous est pas familière, consultez [Conversion d’un certificat binaire en fichier texte](http://youtu.be/PlgrzUZ-Y1o)

**Pour configurer l’authentification unique, procédez comme suit :**

1. Dans le portail Azure Classic, sur la page d’intégration d’application **SAP HANA Cloud Platform**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurer l’authentification unique")
2. Dans la page **Comment voulez-vous que les utilisateurs se connectent à SAP HANA Cloud Platform**, sélectionnez **Authentification unique Microsoft Azure AD**, puis cliquez sur **Suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurer l’authentification unique")
3. Dans une autre fenêtre de navigateur web, connectez-vous à SAP HANA Cloud Platform Cockpit à l’adresse \<https://account.\>landscape host.ondemand.com/cockpit (par ex. *https://account.hanatrial.ondemand.com/cockpit*).
4. Cliquez sur l’onglet **Trust** .
   
    ![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")
5. Dans la section de gestion d’approbation, procédez comme suit :
   
    ![Obtenir les métadonnées](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obtenir les métadonnées")
   
   1. Cliquez sur l’onglet **Local Service Provider** .
   2. Pour télécharger le fichier de métadonnées SAP HANA Cloud Platform, cliquez sur **Get Metadata**.
6. Dans le portail Azure Classic, dans la page **Configurer l’URL de l’application**, procédez comme suit, puis cliquez sur **Suivant**.
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurer l’URL de l’application")
   
   1. Dans la zone de texte **URL d’authentification**, entrez l’URL utilisée par vos utilisateurs pour se connecter à votre application **SAP HANA Cloud Platform**. Il s’agit de l’URL spécifique au compte d’une ressource protégée de votre application SAP HANA Cloud Platform. L’URL est au format suivant : *https://\<nomApplication\>\<nomCompte\>.\<hôte\>.ondemand.com/\<chemin\_vers\_ressource\_protégée\>* (par ex. : *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Il s’agit de l’URL de votre application SAP HANA Cloud Platform sur laquelle l’utilisateur doit s’authentifier.
     > 

   2. Ouvrez le fichier de métadonnées SAP HANA Cloud Platform téléchargé et recherchez la balise **ns3:AssertionConsumerService** .
   3. Copiez la valeur de l’attribut **Location** et collez-la dans la zone de texte **SAP HANA Cloud Platform Reply URL**.

7. Dans la page **Configurer l’authentification unique à SAP HANA Cloud Platform**, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier sur votre ordinateur.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurer l’authentification unique")
8. Sur SAP HANA Cloud Platform Cockpit, dans la section **Local Service Provider** , procédez comme suit :
   
    ![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")
   
  1. Cliquez sur **Modifier**.
  2. Comme **Configuration Type**, sélectionnez **Custom**.
  3. Pour **Local Provider Name**, laissez la valeur par défaut.
  4. Pour générer une paire de clés **Signature Key** et **Signing Certificate**, cliquez sur **Generate Key Pair**.
  5. Pour **Principal Propagation**, sélectionnez **Disabled**.
  6. Pour **Force Authentication**, sélectionnez **Disabled**.
  7. Cliquez sur **Enregistrer**.

9. Cliquez sur l’onglet **Trusted Identity Provider**, puis sur **Add Trusted Identity Provider**.
   
    ![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")
   
    >[!NOTE]
    >Pour gérer la liste de fournisseurs d’identité approuvés, vous devrez avoir choisi le type de configuration Custom dans la section Local Service Provider. Pour le type de configuration Default, vous disposez d’une approbation non modifiable et implicite au SAP ID Service. Pour None, vous n’avez aucun paramètre d’approbation.
    > 
    > 

10. Cliquez sur l’onglet **General**, puis sur **Browse** pour charger le fichier de métadonnées que vous avez téléchargé.
    
    ![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")
    
    >[!NOTE]
    >Après avoir téléchargé le fichier de métadonnées, les valeurs de **Single Sign-on URL**, **Single Logout URL** et de **Signing Certificate** sont remplies automatiquement.
    > 
    > 

11. Cliquez sur onglet **Attributes** .
12. Sous l’onglet **Attributes**, procédez comme suit :
    
    ![Attributs](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributs") 
  * Cliquez sur **Add Assertion-Based Attribute**, puis ajoutez les attributs basés sur une assertion suivants :
       
    | Assertion Attribute | Principal Attribute |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |firstname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |Lastname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |email 
   
     >[!NOTE]
     >La configuration des attributs dépend de la façon dont sont développées les applications sur HCP, en l’occurrence des attributs qu’elles attendent dans la réponse SAML et avec quel nom (Principal Attribute) elles accèdent à cet attribut dans le code.
     > 
     >  

    1.  L’attribut **Default Attribute** de la capture d’écran ne sert qu’à des fins d’illustration. Il n’est pas nécessaire de faire fonctionner le scénario.   
    2.  Les noms et valeurs de **Principal Attribute** dans la capture d’écran dépendent de la façon dont l’application est développée. Il est possible que votre application exige des mappages différents.
     
13. Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configure single sign-on at SAP HANA Cloud Platform**.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurer l’authentification unique")

###<a name="assertion-based-groups"></a>Groupes basés sur une assertion
Une étape facultative est de configurer des groupes basés sur une assertion pour votre fournisseur d’identité Azure Active Directory.

L’utilisation de SAP HANA Cloud Platform vous permet d’attribuer de manière dynamique un ou plusieurs utilisateurs à un ou plusieurs rôles dans vos applications SAP HANA Cloud Platform, en fonction des valeurs des attributs de l’assertion SAML 2.0. 

Par exemple, si l’assertion contient l’attribut « *contract=temporaire* », vous souhaiterez peut-être que tous les utilisateurs affectés soient ajoutés au groupe « *TEMPORAIRE* ». Le groupe «*TEMPORAIRE*» peut contenir un ou plusieurs rôles d’une ou plusieurs applications déployées dans votre compte SAP HANA Cloud Platform.
 
Utilisez des groupes basés sur une assertion quand vous voulez affecter simultanément plusieurs utilisateurs à un ou plusieurs rôles d’applications dans votre compte SAP HANA Cloud Platform. Si vous ne voulez affecter qu’un seul utilisateur ou un petit nombre d’utilisateurs à des rôles spécifiques, nous vous recommandons de les affecter directement dans l’onglet « **Autorisations** » de SAP HANA Cloud Platform Cockpit.

## <a name="assign-a-role-to-a-user"></a>Affecter un rôle à un utilisateur
Pour permettre aux utilisateurs d’Azure AD de se connecter à SAP HANA Cloud Platform, vous devez leur attribuer des rôles dans SAP HANA Cloud Platform.

**Pour affecter un rôle à un utilisateur, procédez comme suit :**

1. Connectez-vous à votre cockpit **SAP HANA Cloud Platform** .
2. Procédez comme suit :
   
   ![Autorisations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorisations")
   
  1. Cliquez sur **Authorization**.
  2. Cliquez sur l’onglet **Users** .
  3. Dans la zone de texte **User** , tapez l’adresse de messagerie de l’utilisateur.
  4. Cliquez sur **Assign** pour attribuer l’utilisateur à un rôle.
  5. Cliquez sur **Save**.

## <a name="assign-users"></a>Affecter des utilisateurs
Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.

**Pour affecter des utilisateurs à SAP HANA Cloud Platform, procédez comme suit :**

1. Dans le portail Azure Classic, créez un compte de test.
2. Dans la page d’intégration d’application **SAP HANA Cloud Platform**, cliquez sur **Affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.
   
   ![Oui](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Oui")

Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès. Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).

