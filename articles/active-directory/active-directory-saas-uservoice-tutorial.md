---
title: "Didacticiel : Intégration d’Azure Active Directory à UserVoice | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a>Didacticiel : Intégration d’Azure Active Directory à UserVoice

Dans ce didacticiel, vous apprendrez comment toointegrate UserVoice avec Azure Active Directory (Azure AD).

Intégration de UserVoice à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooUserVoice.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooUserVoice (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à UserVoice, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement UserVoice pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de UserVoice à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-uservoice-from-hello-gallery"></a>Ajout de UserVoice à partir de la galerie de hello
intégration de hello tooconfigure de UserVoice dans Azure AD, vous devez tooadd UserVoice à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd UserVoice à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **UserVoice**, sélectionnez **UserVoice** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Liste des résultats de UserVoice Bonjour](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec UserVoice, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans UserVoice est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans UserVoice doit toobe établie.

Dans UserVoice, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec UserVoice, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test UserVoice](#create-a-uservoice-test-user)**  -toohave un équivalent de Britta Simon dans UserVoice est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de UserVoice.

**tooconfigure Azure AD single sign-on avec UserVoice, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **UserVoice** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. Sur hello **UserVoice domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.UserVoice.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.UserVoice.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de UserVoice](https://www.uservoice.com/) tooget ces valeurs.

4. Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. Sur hello **UserVoice Configuration** , cliquez sur **UserVoice de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration de UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise UserVoice tooyour en tant qu’administrateur.

8. Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**, puis sélectionnez **portail Web** à partir du menu de hello.
   
    ![Section Paramètres côté application](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Paramètres")

9. Sur hello **portail Web** onglet hello **l’authentification utilisateur** , cliquez sur **modifier** tooopen hello **modifier l’authentification utilisateur** boîte de dialogue page.
   
    ![Onglet Portail Web](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Portail Web")

10. Sur hello **modifier l’authentification utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Modifier l’authentification utilisateur](./media/active-directory-saas-uservoice-tutorial/ic777521.png "modifier l’authentification utilisateur")
   
    a. Cliquez sur **Single Sign-On (SSO)**.
 
    b. Hello de coller **SAML Sign-On URL du Service unique** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **SSO distant connectez-vous** zone de texte.

    c. Hello de coller **URL de déconnexion** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **déconnexion à distance de l’authentification unique de zone de texte**.
 
    d. Hello de coller **l’empreinte numérique** valeur, qui vous avez copié à partir du portail Azure dans le **empreinte de certificat SHA1 actuelle** zone de texte.
    
    e. Cliquez sur **Save authentication settings**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-uservoice-test-user"></a>Créer un utilisateur de test UserVoice

tooenable Azure AD les utilisateurs toolog dans tooUserVoice, vous devez les configurer dans UserVoice. Dans les cas de hello de UserVoice, cette configuration est une tâche manuelle.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision un compte d’utilisateur, effectuez hello comme suit :
1. Connectez-vous à tooyour **UserVoice** client.

2. Accédez trop**paramètres**.
   
    ![Paramètres](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Paramètres")

3. Cliquez sur **General**.

4. Cliquez sur **Agents and permissions**.
   
    ![Agents et autorisations](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents et autorisations")

5. Cliquez sur **Add admins**.
   
    ![Ajouter des administrateurs](./media/active-directory-saas-uservoice-tutorial/ic777813.png "ajouter des administrateurs")

6. Sur hello **inviter des administrateurs** boîte de dialogue, effectuer hello comme suit :
   
    ![Inviter des administrateurs](./media/active-directory-saas-uservoice-tutorial/ic777814.png "inviter des administrateurs")
   
    a. Dans la zone de texte hello des messages électroniques, tapez adresse de messagerie hello de hello compte tooprovision, puis cliquez sur **ajouter**.
   
    b. Cliquez sur **Invite**.

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre UserVoice utilisateur compte outil de création ou API fournie par UserVoice tooprovision des comptes d’utilisateur AAD.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooUserVoice.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooUserVoice, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **UserVoice**.

    ![lien de UserVoice Hello dans la liste des Applications hello](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque UserVoice hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour UserVoice application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

