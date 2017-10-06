---
title: "Didacticiel : Intégration d’Azure Active Directory dans Asana | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Asana."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 837e38fe-8f55-475c-87f4-6394dc1fee2b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: jeedes
ms.openlocfilehash: 9ac35dedc809b2b3dfb461d92a5afb066ccdedde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asana"></a>Didacticiel : Intégration d’Azure Active Directory dans Asana

Dans ce didacticiel, vous apprendrez comment toointegrate Asana avec Azure Active Directory (Azure AD).

Intégration Asana à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAsana
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAsana (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Asana, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Asana avec authentification unique activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Asana à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-asana-from-hello-gallery"></a>Ajout de Asana à partir de la galerie de hello
intégration de hello tooconfigure de Asana dans Azure AD, vous devez tooadd Asana à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Asana à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Asana**, sélectionnez **Asana** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Asana, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Asana est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Asana doit toobe établie.

Dans Asana, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Asana, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test Asana](#create-an-asana-test-user)**  -toohave un équivalent de Britta Simon dans Asana est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Asana.

**tooconfigure Azure AD single sign-on avec Asana, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Asana** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-asana-tutorial/tutorial_asana_samlbase.png)

3. Sur hello **Asana domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez l’URL :`https://app.asana.com/`

    b. Bonjour **identificateur** zone de texte, valeur de type :`https://app.asana.com/`
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_certificate.png)
    
5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-asana-tutorial/tutorial_general_400.png)

6. Sur hello **Asana Configuration** , cliquez sur **Asana de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration d’Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_configure.png) 

7. Dans une autre fenêtre de navigateur, l’authentification tooyour Asana application. tooconfigure SSO dans Asana, les paramètres d’espace de travail accès hello en cliquant sur le nom d’espace de travail hello sur hello coin supérieur droit de l’écran hello. Ensuite, cliquez sur le **\<nom de votre espace de travail\> Paramètres**. 
   
    ![Paramètre d’authentification unique Asana](./media/active-directory-saas-asana-tutorial/tutorial_asana_09.png)

8. Sur hello **paramètres de l’organisation** fenêtre, cliquez sur **Administration**. Ensuite, cliquez sur **membres doivent se connecter via SAML** configuration de SSO tooenable hello. Hello effectuer hello comme suit :
   
    ![Configurer les paramètres d’authentification unique](./media/active-directory-saas-asana-tutorial/tutorial_asana_10.png)  

     a. Bonjour **URL de la page connexion** zone de texte, collez hello **SAML Sign-On URL du Service unique**.

     b. Cliquez avec le bouton droit sur le certificat hello téléchargé à partir du portail Azure, puis ouvrir le fichier de certificat hello à l’aide du bloc-notes ou votre éditeur de texte préféré. Copier le contenu entre hello hello commencer et hello titre de certificat de fin et le coller dans hello **certificat X.509** zone de texte.

9. Cliquez sur **Enregistrer**. Accédez trop[guide Asana pour configurer l’authentification unique](https://asana.com/guide/help/premium/authentication#gl-saml) si vous avez besoin d’aide.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-asana-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asana-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-asana-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="create-an-asana-test-user"></a>Créer un utilisateur de test Asana

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Asana.

1. Sur **Asana**, accédez toohello **équipes** section sur le panneau gauche hello. Cliquez sur hello ainsi que le bouton de connexion. 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-asana-tutorial/tutorial_asana_12.png) 

2. Tapez par courrier électronique hello britta.simon@contoso.com dans hello de zone de texte, puis sélectionnez **inviter**.

3. Cliquez sur **Send Invite**(Envoyer l’invitation). nouvel utilisateur de Hello recevront un message électronique dans son compte de messagerie. Elle sera peut-être toocreate et valider le compte de hello.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAsana.

![Attribuer le rôle d’utilisateur hello][200]

**tooassign Britta Simon tooAsana, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Asana**.

    ![lien de Asana Hello dans la liste des Applications hello](./media/active-directory-saas-asana-tutorial/tutorial_asana_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

objectif Hello de cette section est tootest votre Azure AD single sign-on.

Atteindre la page de connexion tooAsana. Dans la zone de texte adresse de messagerie hello, insérer l’adresse de messagerie hello britta.simon@contoso.com. Zone de texte de mot de passe hello vides et cliquez sur **journal dans**. Vous serez redirigé tooAzure AD de page de connexion. Entrez vos informations d’identification Azure AD. Vous êtes maintenant connecté à Asana.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-asana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asana-tutorial/tutorial_general_203.png
[10]: ./media/active-directory-saas-asana-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-asana-tutorial/tutorial_general_070.png
