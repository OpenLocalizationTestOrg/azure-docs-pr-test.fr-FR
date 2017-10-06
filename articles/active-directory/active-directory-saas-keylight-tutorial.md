---
title: "Didacticiel : Intégration d’Azure Active Directory avec LockPath Keylight | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 5485aeb068ba6fbdb4ea9bfc89d401e00c5b1d29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a>Didacticiel : Intégration d’Azure Active Directory avec LockPath Keylight

Dans ce didacticiel, vous apprendrez comment toointegrate LockPath Keylight avec Azure Active Directory (Azure AD).

Intégration LockPath Keylight à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooLockPath Keylight
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLockPath Keylight (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec LockPath Keylight, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement LockPath Keylight pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de LockPath Keylight à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-lockpath-keylight-from-hello-gallery"></a>Ajout de LockPath Keylight à partir de la galerie de hello
intégration de hello tooconfigure de LockPath Keylight dans Azure AD, vous devez tooadd LockPath Keylight à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd LockPath Keylight à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **LockPath Keylight**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. Dans le volet de résultats hello, sélectionnez **LockPath Keylight**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LockPath Keylight sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello LockPath Keylight est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LockPath Keylight doit toobe établie.

Dans LockPath Keylight, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec LockPath Keylight, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test LockPath Keylight](#creating-a-lockpath-keylight-test-user)**  -toohave un équivalent de Britta Simon dans LockPath Keylight qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LockPath Keylight.

**tooconfigure Azure AD single sign-on avec LockPath Keylight, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **LockPath Keylight** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. Sur hello **LockPath Keylight domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.keylightgrc.com/`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.keylightgrc.com`

    c. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.keylightgrc.com/Login.aspx`
    
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. Contact [équipe de support Client de Keylight LockPath](https://www.lockpath.com/contact/) tooget ces valeurs. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. Sur hello **LockPath Keylight Configuration** , cliquez sur **configurer le LockPath Keylight** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. tooenable SSO dans LockPath Keylight, effectuez hello comme suit :
   
    a. Authentification tooyour compte LockPath Keylight en tant qu’administrateur.
    
    b. Dans le menu hello haut de hello, cliquez sur **personne**, puis sélectionnez **Keylight le programme d’installation**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/401.png) 

    c. Dans le treeview hello sur hello gauche, cliquez sur **SAML**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/402.png) 

    d. Sur hello **paramètres SAML** boîte de dialogue, cliquez sur **modifier**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/404.png) 

8. Sur hello **modifier les paramètres SAML** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    a. Définissez **l’authentification SAML** trop**Active**.

    b. Hello de coller **SAML Sign-On URL du Service unique** valeur sur laquelle vous avez copié à partir de hello portail Azure en hello **Identity Provider Login URL** zone de texte.

    c. Hello de coller **URL de Service de déconnexion unique** valeur sur laquelle vous avez copié à partir de hello portail Azure en hello **Identity Provider Logout URL** zone de texte.

    d. Cliquez sur **choisir un fichier** tooselect votre LockPath Keylight téléchargé de certificat, puis cliquez sur **ouvrir** certificat de hello tooupload.

    e. Définissez **emplacement de l’Id d’utilisateur SAML** trop**élément NameIdentifier de l’instruction de sujet hello**.
    
    f. Fournir hello **fournisseur de services Keylight** à l’aide de hello modèle : **https://&lt;CompanyName&gt;. keylightgrc.com**.
    
    g. Définissez **les utilisateurs de la configuration automatique** trop**Active**.

    h. Définissez **type de compte de la configuration automatique** trop**utilisateur complet**.

    i. Définissez **Auto-provision security role** (Configuration automatique du rôle de sécurité), sélectionnez **Standard User with SAML** (Utilisateur standard avec SAML).
    
    j. Définissez **Auto-provision security config** (Configuration automatique des paramètres de sécurité), sélectionnez **Standard User Configuration** (Configuration utilisateur standard).
     
    k. Bonjour **attribut Email** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    l. Bonjour **prénom attribut** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    m. Bonjour **attribut de nom** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.
    
    n. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-lockpath-keylight-test-user"></a>Création d’un utilisateur de test LockPath Keylight

Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans LockPath Keylight. LockPath Keylight prend en charge l’approvisionnement juste-à-temps, option activée par défaut.

Vous n’avez aucune opération à effectuer dans cette section. Un nouvel utilisateur est créé lors de l’accès LockPath Keylight si l’utilisateur de hello n’existe pas encore. 

>[!NOTE]
>Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support LockPath Keylight Client](https://www.lockpath.com/contact/). 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLockPath Keylight.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooLockPath Keylight, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **LockPath Keylight**.

    ![Configurer l’authentification unique](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello LockPath Keylight vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour LockPath Keylight application. 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

