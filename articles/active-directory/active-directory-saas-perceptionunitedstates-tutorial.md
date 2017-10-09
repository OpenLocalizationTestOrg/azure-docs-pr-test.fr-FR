---
title: "Didacticiel : Intégration d’Azure Active Directory à Perception United States (Non-UltiPro) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la Perception United States (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Didacticiel : Intégration d’Azure Active Directory à Perception United States (Non-UltiPro)

Dans ce didacticiel, vous apprendrez comment toointegrate Perception United States (Non-UltiPro) avec Azure Active Directory (Azure AD).

Intégration Perception United States (Non-UltiPro) à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooPerception États-Unis (Non-UltiPro).
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPerception États-Unis (Non-UltiPro) (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Perception États-Unis (Non-UltiPro), vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Perception United States (Non-UltiPro) pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Perception United States (Non-UltiPro) à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a>Ajout de Perception United States (Non-UltiPro) à partir de la galerie de hello
intégration de hello tooconfigure de Perception États-Unis (Non-UltiPro) dans Azure AD, vous devez tooadd Perception United States (Non-UltiPro) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Perception United States (Non-UltiPro) à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Perception United States (Non-UltiPro)**, sélectionnez **Perception United States (Non-UltiPro)** à partir du volet de résultats, puis sur **ajouter** tooadd de bouton application Hello.

    ![Perception United States (Non-UltiPro) dans la liste des résultats hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Perception United States (Non-UltiPro) grâce à un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Perception États-Unis (Non-UltiPro) est tooa dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Perception États-Unis (Non-UltiPro) doit toobe établie.

Dans Perception États-Unis (Non-UltiPro), affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Perception États-Unis (Non-UltiPro), vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test Perception United States (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave un équivalent de Britta Simon dans Perception États-Unis (Non-UltiPro) qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Perception United States (Non-UltiPro).

**tooconfigure Azure AD de l’authentification unique avec Perception États-Unis (Non-UltiPro), effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Perception United States (Non-UltiPro)** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. Sur hello **Perception United States (Non-UltiPro) domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification Domaine et URL Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://perception.kanjoya.com/sp`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > valeur de Hello n’est pas réelle. Vous mettrez à jour la valeur de hello avec l’URL de réponse réelle hello, qui est expliquée plus loin dans le didacticiel de hello.
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. Sur hello **Perception United States (Non-UltiPro) Configuration** , cliquez sur **configurer Perception États-Unis (Non-UltiPro)** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML** de hello **section de référence rapide.**

    a. Hello **Perception United States (Non-UltiPro)** requiert l’application hello **ID d’entité SAML** toobe uri de valeur, qui vous avez copié, encodé. lien de suivant de hello utilisation tooget valeur de l’uri encodé hello, :**http://www.url-encode-decode.com/**.

    b. Après obtention d’uri de hello valeur encodée associer hello **URL de réponse** comme indiqué ci-dessous :

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Hello Coller au-dessus de la valeur Bonjour **URL de réponse** zone de texte dans **Perception United States (Non-UltiPro) domaine et les URL** section.

    ![Configuration de Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. Dans une autre fenêtre de navigateur, connectez-vous sur le site d’entreprise tooyour Perception United States (Non-UltiPro) en tant qu’administrateur.

8. Dans la barre d’outils principale hello, cliquez sur **les paramètres de compte**.

    ![Utilisateur Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. Sur hello **les paramètres de compte** page, effectuer hello comme suit :

    ![Utilisateur Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. Bonjour **nom de la société** zone de texte, nom du type hello Hello **entreprise**.
    
    b. Bonjour **nom de compte** zone de texte, nom du type hello Hello **compte**.

    c. Dans **réponse par défaut-tooEmail** zone de texte, hello type valide **E-mail**.

    d. Sélectionnez le **fournisseur d’identité d’authentification unique** **SAML 2.0**.

10. Sur hello **Configuration SSO** page, effectuer hello comme suit :

    ![Configuration de l’authentification unique Perception United States (Non-UltiPro)](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Sélectionnez le **type de NameID SAML** **E-MAIL**.

    b. Bonjour **nom de Configuration de l’authentification unique** nom hello du type de zone de texte votre **Configuration**.
    
    c. Dans **nom de fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure. 

    d. Dans **SAML domaine textbox**, entrez le domaine hello comme  **@contoso.com** .

    e. Cliquez sur **télécharger à nouveau** hello de tooupload **Metadata XML** fichier.

    f. Cliquez sur **Update**.


> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Créer un utilisateur de test Perception United States (Non-UltiPro)

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Perception United States (Non-UltiPro). Travailler avec [équipe de support Perception United States (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd les utilisateurs de hello dans la plateforme de Perception United States (Non-UltiPro) hello.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPerception États-Unis (Non-UltiPro).

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign tooPerception Britta Simon États-Unis (Non-UltiPro), exécutez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Perception United States (Non-UltiPro)**.

    ![lien de Perception United States (Non-UltiPro) Hello dans la liste des Applications hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Perception United States (Non-UltiPro) hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Perception United States (Non-UltiPro) application.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

