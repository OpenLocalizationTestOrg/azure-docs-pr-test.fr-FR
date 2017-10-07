---
title: "Didacticiel : Intégration d’Azure Active Directory à Hightail | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Hightail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 2b36fcf8d5773255fdf89de2dccdceb95c032bd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a>Didacticiel : Intégration d’Azure Active Directory à Hightail

Dans ce didacticiel, vous apprendrez comment toointegrate Hightail avec Azure Active Directory (Azure AD).

Intégration Hightail à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooHightail
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHightail (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Hightail, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Hightail pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Hightail à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-hightail-from-hello-gallery"></a>Ajout de Hightail à partir de la galerie de hello
intégration de hello tooconfigure de Hightail dans Azure AD, vous devez tooadd Hightail à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Hightail à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Hightail**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_search.png)

5. Dans le volet de résultats hello, sélectionnez **Hightail**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Hightail avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Hightail est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Hightail doit toobe établie.

Dans Hightail, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Hightail, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Hightail](#creating-a-hightail-test-user)**  -toohave un équivalent de Britta Simon dans Hightail est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Hightail.

**tooconfigure Azure AD single sign-on avec Hightail, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Hightail** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_samlbase.png)

3. Sur hello **Hightail de domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url.png)

     Bonjour **URL de réponse** zone de texte, tapez l’URL hello en tant que :`https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`

    > [!NOTE] 
    > Hello valeur précédente n’est pas la valeur réelle. Vous mettrez à jour la valeur de hello avec l’URL de réponse réelle hello, qui est expliquée plus loin dans le didacticiel de hello.
 
4. Sur hello **Hightail de domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :
    
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_url1.png)

    a. Cliquez sur hello **afficher les paramètres d’URL avancés**.

    b. Bonjour **URL de connexion** zone de texte, tapez l’URL hello en tant que :`https://www.hightail.com/loginSSO`

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_certificate.png) 

5. Hightail application attend les assertions SAML hello dans un format spécifique. Veuillez configurer hello suivant des revendications pour cette application. Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Mémoire »** onglet de l’application hello. Hello suivant capture d’écran montre un exemple de cela. 

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_attribute.png) 

6. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :
    
    | Nom de l'attribut | Valeur de l’attribut |
    | ------------------- | -------------------- |
    | FirstName | user.givenname |
    | LastName | user.surname |
    | Email | user.mail |    
    | UserIdentity | user.mail |
    
    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_officespace_05.png)

    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.

    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.

    d. Laissez hello **Namespace** vide.
    
    e. Cliquez sur **OK**.

7. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_general_400.png)

8. Sur hello **Hightail de Configuration** , cliquez sur **configurer Hightail** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_configure.png) 

    >[!NOTE] 
    >Avant de configurer hello Single Sign On à l’application de Hightail, veuillez liste blanche votre domaine de messagerie avec Hightail d’équipe afin que tous les hello les utilisateurs qui sont à l’aide de ce domaine, utilisez l’authentification unique.


9. tooget SSO configuré pour votre application, vous devez locataire de Hightail toosign sur tooyour en tant qu’administrateur.
   
    a. Dans le menu hello haut de hello, cliquez sur hello **compte** onglet et sélectionnez **SAML de configurer**.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_001.png) 

    b. Sélectionnez la case à cocher hello de **activer l’authentification SAML**.

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_002.png) 

    c. Ouvrez votre certificat codé en base 64 dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **le certificat de signature de jetons SAML** zone de texte.

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_003.png) 

    d. Bonjour **SAML autorité (fournisseur d’identité)** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** copiés à partir du portail Azure.

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_004.png)

    e. Si vous le souhaitez application hello tooconfigure **mode initialisée par IDP** sélectionnez **« Journal dans initiée par le fournisseur d’identité (IdP) »**. En **mode lancé par le fournisseur de service**, sélectionnez **Service Provider (SP) initiated log in** (Connexion lancée par le fournisseur de service).

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_006.png)

    f. Copier l’URL de consommateur SAML hello pour votre instance et le coller dans **URL de réponse** zone de texte dans **Hightail de domaine et les URL** section sur le portail Azure.
    
    g. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hightail-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-hightail-test-user"></a>Création d’un utilisateur de test Hightail

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Hightail. 

Vous n’avez aucune opération à effectuer dans cette section. Hightail prend en charge l’approvisionnement des utilisateurs de juste-à-temps en fonction des revendications personnalisées hello. Si vous avez configuré des revendications personnalisées hello comme indiqué dans la section de hello  **[configuration Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  ci-dessus, un utilisateur est automatiquement créé dans une application hello qu’il n’existe pas encore. 

>[!NOTE]
>Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Hightail](mailto:support@hightail.com). 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHightail.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooHightail, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Hightail**.

    ![Configurer l’authentification unique](./media/active-directory-saas-hightail-tutorial/tutorial_hightail_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Hightail hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Hightail application.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hightail-tutorial/tutorial_general_203.png

