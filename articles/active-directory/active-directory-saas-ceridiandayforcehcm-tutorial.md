---
title: "Didacticiel : Intégration d’Azure Active Directory à Ceridian Dayforce HCM | Microsoft docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Ceridian Dayforce HCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 7adf1eb3-d063-45d6-96a8-fd53b329b3f3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4d72f29b4e5e30ef8881806d789f6676fc541e2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ceridian-dayforce-hcm"></a>Didacticiel : Intégration d’Azure Active Directory à Ceridian Dayforce HCM

Dans ce didacticiel, vous apprendrez comment toointegrate HCM de Dayforce Ceridian avec Azure Active Directory (Azure AD).

Intégration Ceridian Dayforce HCM à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooCeridian Dayforce HCM.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCeridian HCM Dayforce (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Ceridian Dayforce HCM, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Ceridian Dayforce HCM pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Ceridian Dayforce HCM à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-ceridian-dayforce-hcm-from-hello-gallery"></a>Ajout de Ceridian Dayforce HCM à partir de la galerie de hello
intégration de hello tooconfigure de Ceridian Dayforce HCM dans Azure AD, vous devez tooadd Ceridian Dayforce HCM à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd HCM de Dayforce Ceridian à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Ceridian Dayforce HCM**, sélectionnez **Ceridian Dayforce HCM** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Liste des résultats de HCM de Dayforce Ceridian Bonjour](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Ceridian Dayforce HCM, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Ceridian Dayforce HCM est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Ceridian Dayforce HCM doit toobe établie.

Dans Ceridian Dayforce HCM, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Ceridian Dayforce HCM, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test Ceridian Dayforce HCM](#create-a-ceridian-dayforce-hcm-test-user)**  -toohave un équivalent de Britta Simon dans Ceridian Dayforce HCM qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Ceridian Dayforce HCM.

**tooconfigure Azure AD l’authentification unique avec Ceridian Dayforce HCM, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Ceridian Dayforce HCM** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_samlbase.png)

3. Sur hello **Ceridian Dayforce HCM domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_url.png)
    
    a. Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par vos utilisateurs sur toosign tooyour application de Ceridian Dayforce HCM.
    
    | Environnement | URL |
    | :-- | :-- |
    | Production | `https://sso.dayforcehcm.com/<DayforcehcmNamespace>` |
    | Test | `https://ssotest.dayforcehcm.com/<DayforcehcmNamespace>` |
    
    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :
    
    | Environnement | URL |
    | :-- | :-- |
    | Production | `https://ncpingfederate.dayforcehcm.com/sp` |
    | Test | `https://fs-test.dayforcehcm.com/sp` |
    
    c. Bonjour **URL de réponse** zone de texte, tapez l’URL hello utilisée par Azure AD toopost hello réponse.
    
    | Environnement | URL |
    | :-- | :-- |
    | Production | `https://ncpingfederate.dayforcehcm.com/sp/ACS.saml2` |
    | Test | `https://fs-test.dayforcehcm.com/sp/ACS.saml2` |
    
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel identificateur, les URL de réponse et les URL de connexion. Contact [équipe de support Client de HCM Ceridian Dayforce](https://www.ceridian.com/contact-us/index.html) tooget ces valeurs.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_certificate.png) 

5. Votre application Ceridian Dayforce HCM attend les assertions SAML hello dans un format spécifique. Travailler avec [équipe de support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) premier identificateur d’utilisateur corrects de hello tooidentify. Microsoft recommande d’utiliser hello **« name »** attribut sous la forme d’identificateur de l’utilisateur. Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attributs utilisateur** section sur la page d’intégration d’application. Hello suivant capture d’écran montre un exemple de cela.  

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_07.png)

6. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :
    
    | Nom de l'attribut  | Valeur de l’attribut |
    | --------------- | -------------------- |    
    | name  | user.extensionattribute2 |    

    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_attribute_05.png)
    
    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.

    c. Bonjour **valeur** liste, sélectionnez hello utilisateur attribut toouse pour votre implémentation.
    Par exemple, si vous voulez toouse hello EmployeeID comme identificateur d’utilisateur unique et si vous avez stocké la valeur de l’attribut hello Bonjour ExtensionAttribute2, puis sélectionnez **user.extensionattribute2**.
    
    d. Cliquez sur **OK**.

7. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_400.png)
    
8. Sur hello **Ceridian Dayforce HCM Configuration** , cliquez sur **configurer HCM de Dayforce Ceridian** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration de Ceridian Dayforce HCM](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_configure.png) 

9. tooconfigure l’authentification unique sur **Ceridian Dayforce HCM** côté, vous devez hello toosend téléchargé **Metadata XML** et **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** trop[équipe de support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html).

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-ceridian-dayforce-hcm-test-user"></a>Créer un utilisateur de test Ceridian Dayforce HCM

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Ceridian Dayforce HCM. Travailler avec hello [équipe de support Ceridian Dayforce HCM](https://www.ceridian.com/contact-us/index.html) utilisateurs tooget ajoutés Bonjour application de Ceridian Dayforce HCM. 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCeridian Dayforce HCM.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooCeridian Dayforce HCM, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Ceridian Dayforce HCM**.

    ![Configurer l’authentification unique](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCeridian Dayforce HCM.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooCeridian Dayforce HCM, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Ceridian Dayforce HCM**.

    ![lien de Ceridian Dayforce HCM Hello dans la liste des Applications hello](./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_ceridiandayforcehcm_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.  
Lorsque vous cliquez sur mosaïque Ceridian Dayforce HCM hello hello volet d’accès, vous devez obtenir l’application de Ceridian Dayforce HCM automatiquement signé sur tooyour. 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ceridiandayforcehcm-tutorial/tutorial_general_203.png

