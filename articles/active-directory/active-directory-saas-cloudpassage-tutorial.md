---
title: "Didacticiel : Intégration d’Azure Active Directory avec CloudPassage | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et CloudPassage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfe1f14e-74e4-4680-ac9e-f7355e1c94cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 32fb007b90f071626c9b40fb5afc341dd3c1ae99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cloudpassage"></a>Didacticiel : Intégration d’Azure Active Directory avec CloudPassage

Dans ce didacticiel, vous apprendrez comment toointegrate CloudPassage avec Azure Active Directory (Azure AD).

Intégration CloudPassage à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooCloudPassage
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCloudPassage (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec CloudPassage, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement CloudPassage pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de CloudPassage à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-cloudpassage-from-hello-gallery"></a>Ajout de CloudPassage à partir de la galerie de hello
intégration de hello tooconfigure de CloudPassage dans Azure AD, vous devez tooadd CloudPassage à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd CloudPassage à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour ** [portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **CloudPassage**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_search.png)

5. Dans le volet de résultats hello, sélectionnez **CloudPassage**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec CloudPassage avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans CloudPassage est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans CloudPassage doit toobe établie.

Dans CloudPassage, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec CloudPassage, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on) ** -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user) ** -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test CloudPassage](#creating-a-cloudpassage-test-user) ** -toohave un équivalent de Britta Simon dans CloudPassage est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on) ** -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application CloudPassage.

**tooconfigure Azure AD single sign-on avec CloudPassage, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **CloudPassage** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_samlbase.png)

3. Sur hello **CloudPassage domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://portal.cloudpassage.com/saml/init/accountid`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle : `https://portal.cloudpassage.com/saml/consume/accountid`. Vous pouvez obtenir la valeur de cet attribut en cliquant sur **documentation d’installation de l’authentification unique** Bonjour **paramètres d’authentification unique** section de votre portail CloudPassage.

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_05.png)
     
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec l’URL de réponse réelle hello et URL de connexion. Contact [équipe de support Client de CloudPassage](https://www.cloudpassage.com/company/contact/) tooget ces valeurs. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_certificate.png) 

5. Votre application CloudPassage attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.   
Hello suivant capture d’écran montre un exemple de cela.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_25.png) 

6. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :

    | Nom de l'attribut | Valeur de l’attribut |
    | --- | --- |
    | firstname |user.givenname |
    | lastname |user.surname |
    | email |user.mail |
    
    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_attribute_05.png)
    
    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.

    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.
    
    d. Cliquez sur **OK**.

7. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_400.png)
    
8. Sur hello **CloudPassage Configuration** , cliquez sur **CloudPassage de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_configure.png) 

9. Dans une autre fenêtre de navigateur, site d’entreprise CloudPassage tooyour ouverture de session en tant qu’administrateur.

10. Dans le menu hello haut de hello, cliquez sur **paramètres**, puis cliquez sur **Site Administration**. 
   
    ![Configurer l’authentification unique][12]

11. Cliquez sur hello **les paramètres d’authentification** onglet. 
   
    ![Configurer l’authentification unique][13]

12. Bonjour **paramètres d’authentification unique** section, effectuer hello comme suit : 
   
    ![Configurer l’authentification unique][14]

    a. Cochez la case **Activer l’authentification unique (SSO) (Documentation de configuration de l’authentification unique)**.
    
    b. Coller **ID d’entité SAML** dans hello **URL de l’émetteur SAML** zone de texte.
  
    c. Coller **SAML Sign-On URL du Service unique** dans hello **URL de point de terminaison SAML** zone de texte.
  
    d. Coller **URL de déconnexion** dans hello **page d’accueil de déconnexion** zone de texte.
  
    e. Ouvrez votre certificat téléchargé dans le bloc-notes, hello copie le contenu des certificats téléchargés dans le Presse-papiers et le coller ensuite dans hello **certificat x 509** zone de texte.
  
    f. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello ** Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-cloudpassage-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-cloudpassage-test-user"></a>Création d’un utilisateur de test CloudPassage

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans CloudPassage.

**toocreate un utilisateur appelé Britta Simon dans CloudPassage, effectuez hello comme suit :**

1. Authentification tooyour **CloudPassage** site d’entreprise en tant qu’administrateur. 

2. Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**, puis cliquez sur **Site Administration**. 
   
   ![Création d’un utilisateur de test CloudPassage][22] 

3. Cliquez sur hello **utilisateurs** onglet, puis cliquez sur **ajouter un nouvel utilisateur**. 
   
   ![Création d’un utilisateur de test CloudPassage][23]

4. Bonjour **ajouter un nouvel utilisateur** section, effectuer hello comme suit : 
   
   ![Création d’un utilisateur de test CloudPassage][24]
    
    a. Bonjour **prénom** zone de texte, tapez Brian. 
  
    b. Bonjour **nom** zone de texte, tapez Simon.
  
    c. Bonjour **nom d’utilisateur** zone de texte, hello **messagerie** zone de texte et hello **retapez le courrier électronique** zone de texte, tapez le nom d’utilisateur de Brian dans Azure AD.
  
    d. En tant que **Type d’accès**, sélectionnez **Activer l’accès portail Halo**.
  
    e. Cliquez sur **Add**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCloudPassage.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooCloudPassage, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **CloudPassage**.

    ![Configurer l’authentification unique](./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque CloudPassage hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour CloudPassage application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_07.png
[13]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_08.png
[14]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_09.png
[15]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_10.png
[22]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_15.png
[23]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_16.png
[24]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_cloudpassage_17.png

[100]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cloudpassage-tutorial/tutorial_general_203.png

