---
title: "Didacticiel : Intégration d’Azure Active Directory avec LinkedIn Learning | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’apprentissage de LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d5857070-bf79-4bd3-9a2a-4c1919a74946
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: jeedes
ms.openlocfilehash: 14610a25132ed0ccf5892cad6ccc4e1ef03ff280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-learning"></a>Didacticiel : Intégration d’Azure Active Directory à LinkedIn Learning

Dans ce didacticiel, vous apprendrez comment toointegrate Learning LinkedIn avec Azure Active Directory (Azure AD).

Intégration LinkedIn Learning à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooLinkedIn d’apprentissage
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLinkedIn Learning (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec LinkedIn Learning, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement LinkedIn Learning pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de LinkedIn Learning à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-linkedin-learning-from-hello-gallery"></a>Ajout de LinkedIn Learning à partir de la galerie de hello
tooconfigure hello intégration de LinkedIn Learning dans Azure AD, vous devez tooadd LinkedIn Learning à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Learning LinkedIn à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **LinkedIn Learning**. Dans le volet de résultats, cliquez sur **LinkedIn Learning** application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LinkedIn Learning avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans LinkedIn Learning est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LinkedIn Learning doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** LinkedIn pour la formation.

tooconfigure et test Azure AD l’authentification unique avec LinkedIn Learning, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test LinkedIn Learning](#creating-a-linkedin-learning-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application LinkedIn Learning.

**tooconfigure Azure AD single sign-on avec LinkedIn apprentissage, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **LinkedIn Learning** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedin_01.png)

3. Dans une fenêtre de navigateur web, client LinkedIn Learning de tooyour de session en tant qu’administrateur.

4. Dans le **Centre des comptes**, cliquez sur **Paramètres globaux** sous **Paramètres**. En outre, sélectionnez **Learning - par défaut** à partir de la liste déroulante de hello.

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_01.png)

5. Cliquez sur **ou cliquez ici tooload et copie des champs individuels à partir de l’écran de hello** et copie **Id d’entité** et **Url d’accès ACS (Assertion Consumer)**

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_03.png)

6. Sur le portail Azure, sous **LinkedIn Learning domaine et les URL**, effectuer hello comme suit si vous souhaitez que l’authentification unique de tooconfigure dans **initialisée par IdP** mode

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_01.png)

    a. Bonjour **identificateur** zone de texte, entrez hello **ID d’entité** copiés à partir du portail de LinkedIn 

    b. Bonjour **URL de réponse** zone de texte, entrez hello **Url d’accès ACS (Assertion Consumer)** copiés à partir du portail de LinkedIn

7. Si vous souhaitez que l’authentification unique de tooconfigure dans **initiée par SP**, puis cliquez sur option Afficher les URL avancées du paramètre dans la section de configuration hello et configurer des URL de connexion hello avec hello modèle :

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=learning&applicationInstanceId=<InstanceId>`

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_signon_02.png)   
    
8. Votre application LinkedIn Learning attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages. Hello suivant capture d’écran montre un exemple de cela. Hello la valeur par défaut de **identificateur de l’utilisateur** est **user.userprincipalname** mais LinkedIn Learning attend ce toobe mappée avec une adresse de messagerie de l’utilisateur hello. Pour cela, vous pouvez utiliser **user.mail** d’attribut à partir de la liste de hello ou utiliser la valeur d’attribut approprié hello en fonction de la configuration de votre organisation. 

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/updateusermail.png)
    
9. Dans **attributs utilisateur** , cliquez sur **afficher et modifier tous les autres attributs utilisateur** et définir les attributs de hello. utilisateur de Hello a besoin de revendications de quatre tooadd nommées **messagerie**, **service**, **firstname**, et **lastname** et valeur de hello est toobe mappée avec **user.mail**, **user.department**, **user.givenname**, et **user.surname** respectivement

    | Nom de l'attribut | Valeur de l’attribut |
    | --- | --- |
    | email| user.mail |    
    | department| user.department |
    | firstname| user.givenname |
    | lastname| user.surname |
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/userattribute.png)
    
    a. Cliquez sur **ajouter un attribut** boîte de dialogue attribut tooopen hello.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_04.png)

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/tutorial_attribute_05.png)
    
    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.
    
    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.
    
    d. Cliquez sur **OK**.

10. Effectuer hello comme suit sur hello **nom** attribut -

    a. Cliquez sur hello de hello attribut tooopen **modifier l’attribut** fenêtre.

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinLearning-tutorial/url_update.png)

    b. Supprimer la valeur d’URL de hello de hello **espace de noms**.
    
    c. Cliquez sur **Ok** paramètre hello de toosave.

11. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_certificate.png) 

12. Cliquez sur **Save**.

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_400.png)

13. Accédez trop**paramètres d’administration LinkedIn** section. Téléchargement des fichiers XML hello téléchargé à partir de hello portail Azure en cliquant sur option de fichier XML de télécharger hello.

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_metadata_03.png)

14. Cliquez sur **sur** tooenable SSO. État de l’authentification unique à partir de **non connecté** trop**connecté**

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinlearning-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**. 

### <a name="creating-a-linkedin-learning-test-user"></a>Création d’un utilisateur de test LinkedIn Learning

L’application LinkedIn Learning prend en charge Juste-à-temps l’approvisionnement des utilisateurs et après l’authentification utilisateurs sont automatiquement créés dans l’application hello. Dans page de paramètres d’administration hello sur le commutateur de portail hello retournement LinkedIn Learning hello **automatiquement attribuer des licences** tooactive tooenable juste en temps de préparation et cela affectera également un utilisateur toohello de licence.
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinLearning-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLinkedIn d’apprentissage.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooLinkedIn de formation, effectuer hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **LinkedIn Learning**.

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinlearning-tutorial/tutorial-linkedinlearning_0001.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque LinkedIn Learning hello hello volet d’accès, vous devez obtenir la page d’authentification Azure hello et sur après authentification réussie, vous devez obtenir dans votre application LinkedIn Learning.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinlearning-tutorial/tutorial_general_203.png