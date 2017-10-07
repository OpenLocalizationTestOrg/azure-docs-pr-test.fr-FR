---
title: "Didacticiel : Intégration d’Azure Active Directory avec Bonusly | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Bonusly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 29fea32a-fa20-47b2-9e24-26feb47b0ae6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 60ad06c028463af81a7901ab321c4ae9346798ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a>Didacticiel : Intégration d’Azure Active Directory avec Bonusly

Dans ce didacticiel, vous apprendrez comment toointegrate Bonusly avec Azure Active Directory (Azure AD).

Intégration Bonusly à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooBonusly
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBonusly (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Bonusly, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Bonusly pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Bonusly à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-bonusly-from-hello-gallery"></a>Ajout de Bonusly à partir de la galerie de hello
intégration de hello tooconfigure de Bonusly dans Azure AD, vous devez tooadd Bonusly à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Bonusly à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Bonusly**, sélectionnez **Bonusly** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Bonusly dans la liste des résultats hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Bonusly avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Bonusly est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Bonusly doit toobe établie.

Dans Bonusly, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Bonusly, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur test Bonusly](#create-a-bonusly-test-user)**  -toohave un équivalent de Britta Simon dans Bonusly est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Bonusly.

**tooconfigure Azure AD single sign-on avec Bonusly, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Bonusly** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_samlbase.png)

3. Sur hello **Bonusly de domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_url.png)

    Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://Bonus.ly/saml/<tenant-name>`

    > [!NOTE] 
    > valeur de Hello n’est pas réelle. Valeur de hello de mise à jour avec hello URL de réponse réelle. Contact [équipe de support Bonusly](https://Bonusly/contact) valeur hello de tooget.
 
4. Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur à partir du certificat de hello.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-bonus-tutorial/tutorial_general_400.png)

6. Sur hello **Configuration Bonusly** , cliquez sur **configurer Bonusly** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration de Bonusly](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_configure.png) 

7. Dans une autre fenêtre de navigateur, connectez-vous tooyour **Bonusly** client.

8. Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**, puis sélectionnez **intégrations et applications**.
   
    ![Section sociale Bonusly](./media/active-directory-saas-bonus-tutorial/ic773686.png "Bonusly")
9. Sous **Single Sign-On**, sélectionnez **SAML**.

10. Sur hello **SAML** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Page de boîte de dialogue Saml Bonusly](./media/active-directory-saas-bonus-tutorial/ic773687.png "Bonusly")
   
    a. Bonjour **URL cible de l’authentification unique IdP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.
   
    b. Bonjour **émetteur IdP** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure. 

    c. Bonjour **URL de connexion IdP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.

    d. Coller le **l’empreinte numérique** valeur copiée à partir du portail Azure dans hello **empreinte numérique du certificat** zone de texte.
   
11. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-bonus-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-bonus-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="create-a-bonusly-test-user"></a>Création d’un utilisateur de test Bonusly

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooBonusly, ils doivent être configurés dans Bonusly. Dans les cas de hello de Bonusly, cette configuration est une tâche manuelle.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre outil de création de compte utilisateur Bonusly ou API fournie par tooprovision Bonusly AAD comptes d’utilisateur.
>  

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Dans une fenêtre de navigateur web, ouvrez une session de client de Bonusly tooyour.

2. Cliquez sur **Settings**.
 
    ![Paramètres](./media/active-directory-saas-bonus-tutorial/ic781041.png "Paramètres")

3. Cliquez sur hello **utilisateurs et bonus** onglet.
   
    ![Users and bonuses](./media/active-directory-saas-bonus-tutorial/ic781042.png "Users and bonuses")

4. Cliquez sur **Manage Users**.
   
    ![Gestion des utilisateurs](./media/active-directory-saas-bonus-tutorial/ic781043.png "Gestion des utilisateurs")

5. Cliquez sur **Add User**.
   
    ![Ajouter un utilisateur](./media/active-directory-saas-bonus-tutorial/ic781044.png "Ajouter un utilisateur")

6. Sur hello **ajouter un utilisateur** boîte de dialogue, effectuer hello comme suit :
   
    ![Ajouter un utilisateur](./media/active-directory-saas-bonus-tutorial/ic781045.png "Ajouter un utilisateur")  

    a. Bonjour **prénom** zone de texte, entrez hello premier nom d’utilisateur comme **Brian**.

    b. Bonjour **nom** zone de texte, entrez le nom d’utilisateur comme hello **Simon**.
 
    c. Bonjour **messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .

    d. Cliquez sur **Enregistrer**.
   
     >[!NOTE]
     >titulaire du compte Azure AD Hello reçoit un message électronique qui inclut un compte de hello tooconfirm lien avant son activation.
     >  

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBonusly.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooBonusly, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Bonusly**.

    ![Hello Bonusly lien dans la liste des Applications hello](./media/active-directory-saas-bonus-tutorial/tutorial_bonusly_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur la vignette de Bonusly hello dans hello volet d’accès, vous devez obtenir les applications Bonusly tooyour automatiquement signé sur.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bonus-tutorial/tutorial_general_203.png

