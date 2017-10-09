---
title: "Didacticiel : intégration d’Azure Active Directory à IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et IBM Kenexa enquête Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: cf7ed886b4418ac396ca7056827ee10fd7a19ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Didacticiel : intégration d’Azure Active Directory à IBM Kenexa Survey Enterprise

Dans ce didacticiel, vous apprendrez comment toointegrate IBM Kenexa enquête Enterprise avec Azure Active Directory (Azure AD).

Intégration IBM Kenexa enquête Enterprise à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooIBM Kenexa enquête Enterprise.
- Vous pouvez activer vos informations d’identification tooautomatically utilisateurs tooIBM Kenexa enquête Enterprise à l’aide de l’authentification unique (SSO) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus sur les logiciels en tant qu’une intégration d’application de service (SaaS) avec Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec IBM Kenexa enquête Enterprise, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement IBM Kenexa Survey Enterprise pour lequel l’authentification unique est activée

> [!NOTE]
> Lorsque vous testez les étapes hello dans ce didacticiel, nous vous recommandons de ne pas utiliser un environnement de production.

étapes de hello tootest dans ce didacticiel, suivez ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans le didacticiel de hello se compose de deux blocs de construction principaux :

* Ajout d’IBM Kenexa enquête entreprise à partir de la galerie de hello
* Configuration et test de l’authentification unique Azure AD

## <a name="add-ibm-kenexa-survey-enterprise-from-hello-gallery"></a>Ajouter IBM Kenexa enquête entreprise à partir de la galerie de hello
tooconfigure l’intégration d’entreprise d’enquête IBM Kenexa hello dans Azure AD, ajouter IBM Kenexa enquête entreprise à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

tooadd IBM Kenexa enquête entreprise à partir de la galerie hello, procédez comme hello suivant :

1. Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, cliquez sur dans hello **Azure Active Directory** bouton. 

    ![bouton d’Azure Active Directory Hello][1]

2. Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd une application, cliquez sur hello **nouvelle application** bouton.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **IBM Kenexa enquête entreprise**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. Dans la liste des résultats hello, sélectionnez **IBM Kenexa enquête entreprise**, puis cliquez sur hello **ajouter** bouton application hello de tooadd.

    ![IBM Kenexa enquête Enterprise dans la liste des résultats hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec IBM Kenexa Survey Enterprise au moyen d’un utilisateur de test appelé « Britta Simon ».

Pour l’authentification unique toowork, Azure AD doit équivalent de tooidentify hello IBM Kenexa enquête entreprise utilisateur dans Azure AD. En d’autres termes, Azure AD doit établir un lien entre un utilisateur Azure AD et un utilisateur associé dans IBM Kenexa Survey Enterprise.

relation de lien de hello tooestablish, attribuer une valeur hello Hello **nom d’utilisateur** dans IBM Kenexa enquête entreprise en tant que valeur hello Hello **nom d’utilisateur** dans Azure AD.

tooconfigure et test de l’authentification unique d’Azure AD avec IBM Kenexa enquête Enterprise, hello complète des blocs de construction dans hello deux sections suivantes.

### <a name="configure-azure-ad-sso"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure Active Directory SSO Bonjour portail Azure et configurez l’authentification unique dans votre application d’entreprise d’enquête IBM Kenexa en procédant comme suit de hello :

1. Bonjour portail Azure, sur hello **IBM Kenexa enquête entreprise** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique dans IBM Kenexa Survey Enterprise][4]

2. Bonjour **l’authentification unique** la boîte de dialogue hello **Mode** boîte, sélectionnez **SAML-authentification** tooenable SSO.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. Bonjour **URL et le domaine d’entreprise enquête IBM Kenexa** section, effectuer hello comme suit :

    ![Informations d’authentification unique de domaine et d’URL d’IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    a. Bonjour **identificateur** zone de texte, tapez un URL avec hello modèle :`https://surveys.kenexa.com/<companycode>`

    b. Bonjour **URL de réponse** zone de texte, tapez un URL avec hello modèle :`https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Hello les valeurs précédentes ne sont pas réelles. Mettre à jour avec l’identificateur de réel hello et URL de réponse. tooobtain hello valeurs réelles, contact hello [équipe de support technique IBM Kenexa enquête entreprise](https://www.ibm.com/support/home/?lnk=fcw).

4. Sous **le certificat de signature SAML**, cliquez sur **certificat (Base64)**, puis enregistrez ordinateur de tooyour de fichier de certificat hello.

    ![lien de téléchargement du certificat (Base64) Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    Hello application d’entreprise d’enquête IBM Kenexa attend les assertions de sécurité Assertions Markup Language (SAML) tooreceive hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé toohello configuration des mappages de vos attributs du jeton SAML. Hello valeur de revendication d’identificateur d’utilisateur hello en réponse de hello doit correspondre à hello ID de l’authentification unique est configuré dans le système de Kenexa hello. toomap hello identificateur d’utilisateur approprié dans votre organisation en tant que l’authentification unique Internet Datagram Protocol (IDP), travailler avec hello [équipe de support technique IBM Kenexa enquête entreprise](https://www.ibm.com/support/home/?lnk=fcw). 

    Par défaut, AD Azure définit identificateur hello de l’utilisateur en tant que valeur de nom principal (UPN) utilisateur hello. Vous pouvez modifier cette valeur sur hello **attribut** onglet, comme indiqué dans hello suivant capture d’écran. intégration de Hello fonctionne uniquement après avoir terminé hello mappage correctement.
    
    ![boîte de dialogue des attributs utilisateur Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png) 

5. Cliquez sur **Enregistrer**.

    ![Hello configurer l’authentification unique sur bouton Enregistrer](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. tooopen hello **configurer l’authentification** fenêtre, sous **Configuration d’entreprise enquête IBM Kenexa**, cliquez sur **configurer IBM Kenexa enquête entreprise**. 
 
    ![lien d’entreprise d’enquête configurer IBM Kenexa Hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. Hello de copie **URL de déconnexion**, **ID d’entité SAML**, et **SAML-Service URL d’authentification** valeurs hello **aide-mémoire** section.

8. Bonjour **configurer l’authentification** fenêtre, sous **aide-mémoire**, hello de copie **URL de déconnexion**, **ID d’entité SAML**, et  **SAML-Service URL d’authentification** valeurs.

9. tooconfigure SSO sur hello **IBM Kenexa enquête entreprise** côté, envoyer hello téléchargé **certificat (Base64)**, **URL de déconnexion**, **ID d’entité SAML**, et **SAML-Service URL d’authentification** valeurs toohello [équipe de support technique IBM Kenexa enquête entreprise](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> Vous pouvez faire référence tooa la version concise de ces instructions Bonjour [portail Azure](https://portal.azure.com) lors de la configuration de l’application hello. Après avoir ajouté l’application hello de hello **Active Directory** > **des Applications d’entreprise** , cliquez simplement sur hello **l’authentification unique** onglet, puis accédez à Hello incorporé documentation via hello **Configuration** section à hello fin. toolearn en savoir plus sur la fonctionnalité de documentation embedded hello, consultez [AD Azure incorporé documentation](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
Dans cette section, vous créez utilisateur test Britta Simon Bonjour portail Azure en procédant comme suit de hello :

![Créer un utilisateur de test Azure AD][100]

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>Créer un utilisateur de test IBM Kenexa Survey Enterprise

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans IBM Kenexa Survey Enterprise. 

toocreate les utilisateurs de hello système IBM Kenexa enquête Enterprise et hello de mappage des ID de l’authentification unique pour les, vous pouvez travailler avec hello [équipe de support technique IBM Kenexa enquête entreprise](https://www.ibm.com/support/home/?lnk=fcw). Cette valeur d’ID de l’authentification unique doit également être mappé la valeur de l’identificateur utilisateur toohello d’Azure AD. Vous pouvez modifier ce paramètre par défaut sur hello **attribut** onglet.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez utilisateur Britta Simon toouse Azure SSO en accordant l’accès tooIBM Kenexa enquête Enterprise.

![Attribuer le rôle d’utilisateur hello][200] 

l’utilisateur tooassign Britta Simon tooIBM Kenexa enquête entreprise, hello suivant :

1. Bonjour portail Azure, ouvrez hello **Applications** afficher, accédez toohello **active** afficher, sélectionnez **des applications d’entreprise**, puis cliquez sur **toutes les applications**.

    ![Hello « applications d’entreprise » et les liens « Toutes les applications »][201] 

2. Bonjour **Applications** liste, sélectionnez **IBM Kenexa enquête entreprise**.

    ![lien d’IBM Kenexa enquête entreprise Hello dans la liste des Applications hello](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. Dans le volet gauche de hello, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Cliquez sur hello **ajouter** bouton, puis, dans hello **ajouter l’affectation** volet, sélectionnez **utilisateurs et groupes**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Bonjour **utilisateurs et groupes** la boîte de dialogue hello **utilisateurs** liste, sélectionnez **Britta Simon**.

6. Bonjour **utilisateurs et groupes** boîte de dialogue, cliquez sur hello **sélectionnez** bouton.

7. Bonjour **ajouter l’affectation** boîte de dialogue, cliquez sur hello **affecter** bouton.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous testez votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello **IBM Kenexa enquête entreprise** vignette dans hello volet d’accès, vous devez être connecté automatiquement dans tooyour application d’entreprise d’enquête IBM Kenexa.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
