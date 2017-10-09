---
title: "Didacticiel : Intégration d’Azure Active Directory avec InTime | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 63652f0f098aeac95e89a2500b46a18440e34698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a>Didacticiel : Intégration d’Azure Active Directory avec InTime

Dans ce didacticiel, vous apprendrez comment toointegrate InTime avec Azure Active Directory (Azure AD).

Intégration InTime à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooInTime.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooInTime (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec InTime, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement InTime pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de InTime à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-intime-from-hello-gallery"></a>Ajout de InTime à partir de la galerie de hello
tooconfigure hello intégration de InTime dans Azure AD, vous devez tooadd InTime à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd InTime à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **InTime**, sélectionnez **InTime** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![InTime dans la liste des résultats hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec InTime, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello InTime est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans InTime doit toobe établie.

Dans InTime, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec InTime, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur test InTime](#create-a-intime-test-user)**  -toohave un équivalent de Britta Simon dans InTime est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application InTime.

**tooconfigure Azure AD single sign-on avec InTime, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **InTime** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. Sur hello **InTime de domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://intime6.intimesoft.com/mytime/login/login.xhtml`

    b. Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://auth.intimesoft.com/auth/realms/master`

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. Votre application InTime attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages. Hello suivant capture d’écran montre un exemple de cela. Hello la valeur par défaut de **identificateur de l’utilisateur** est **user.userprincipalname** mais InTime attend ce toobe mappée avec une adresse de messagerie de l’utilisateur hello. Pour cela, vous pouvez utiliser **user.mail** d’attribut à partir de la liste de hello ou utiliser la valeur d’attribut approprié hello en fonction de votre configuration de l’organisation 

    ![Configurer l’attribut](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. Sur hello **Configuration InTime** , cliquez sur **configurer InTime** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration d’InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. tooconfigure l’authentification unique sur **InTime** côté, vous devez hello toosend téléchargé **Metadata XML**, **URL de déconnexion et SAML Sign-On URL du Service unique** trop[Équipe de support inTime](mailto:hdollard@intimesoft.com). Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-intime-test-user"></a>Créer un utilisateur de test InTime

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans InTime. Travailler avec [équipe de support InTime](mailto:hdollard@intimesoft.com) utilisateurs hello tooadd plateforme InTime de hello. Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooInTime.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooInTime, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **InTime**.

    ![Hello InTime lien dans la liste des Applications hello](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur la vignette de InTime hello dans hello volet d’accès, vous devez obtenir la page de connexion hello de votre application InTime. Cliquez sur hello **connexion** bouton, une série de IdPs sera affichée sur une liste de boutons. Cliquez sur **nom de l’IDP** donné par [équipe de support InTime](mailto:hdollard@intimesoft.com) toologin dans votre application InTime. Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png
