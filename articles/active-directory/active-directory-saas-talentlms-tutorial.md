---
title: "Didacticiel :Intégration d’Azure Active Directory à TalentLMS | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 25538086602e58fbaab0fbf223f5b03908a74922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a>Didacticiel : Intégration d’Azure Active Directory à TalentLMS

Dans ce didacticiel, vous apprendrez comment toointegrate TalentLMS avec Azure Active Directory (Azure AD).

Intégration de TalentLMS à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooTalentLMS
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTalentLMS (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à TalentLMS, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement TalentLMS pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de TalentLMS à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-talentlms-from-hello-gallery"></a>Ajout de TalentLMS à partir de la galerie de hello
intégration de hello tooconfigure de TalentLMS dans Azure AD, vous devez tooadd TalentLMS à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd TalentLMS à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **TalentLMS**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. Dans le volet de résultats hello, sélectionnez **TalentLMS**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de TalentLMS avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans TalentLMS est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de TalentLMS hello doit toobe établie.

Dans TalentLMS, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à TalentLMS, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de TalentLMS](#creating-a-talentlms-test-user)**  -toohave un équivalent de Britta Simon dans TalentLMS est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de TalentLMS.

**tooconfigure Azure AD single sign-on avec TalentLMS, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **TalentLMS** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. Sur hello **TalentLMS domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.TalentLMSapp.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`http://<tenant-name>.talentlms.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de TalentLMS](https://www.talentlms.com/contact) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur à partir du certificat de hello.

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. Sur hello **TalentLMS Configuration** , cliquez sur **configurer de TalentLMS** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise TalentLMS tooyour en tant qu’administrateur.

8. Bonjour **compte et paramètres** , cliquez sur hello **utilisateurs** onglet.
   
    ![Compte et paramètres](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Compte et paramètres")

9. Cliquez sur **Single Sign-On (SSO)**.

10. Bonjour section Single Sign-On, effectuez hello comme suit :
   
    ![Authentification unique](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Authentification unique")   

    a. À partir de hello **type d’intégration SSO** liste, sélectionnez **SAML 2.0**.

    b. Bonjour **fournisseur d’identité (IDP)** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.
 
    c. Hello de coller **l’empreinte numérique** valeur à partir du portail Azure en hello **empreinte numérique du certificat** zone de texte.    

    d.  Bonjour **URL de connexion à distance** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.
 
    e. Bonjour **URL de déconnexion distante** zone de texte, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.

    f. Renseignez les suivant hello : 

    * Bonjour **TargetedID** zone de texte, type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`
     
    * Bonjour **prénom** zone de texte, type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`
    
    * Bonjour **nom** zone de texte, type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`
    
    * Bonjour **messagerie** zone de texte, type`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`
    
11. Cliquez sur **Enregistrer**.
 
> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-talentlms-test-user"></a>Création d’un utilisateur de test TalentLMS

tooenable Azure AD les utilisateurs toolog dans tooTalentLMS, vous devez les configurer dans TalentLMS. Dans les cas de hello de TalentLMS, cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **TalentLMS** client.

2. Cliquez sur **Users (Utilisateurs)**, puis sur **Add User (Ajouter un utilisateur)**.

3. Sur hello **ajouter un utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Ajouter un utilisateur](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Ajouter un utilisateur")  

    a. Bonjour **prénom** zone de texte, entrez hello premier nom d’utilisateur comme **Brian**.

    b. Bonjour **nom** zone de texte, entrez le nom d’utilisateur comme hello **Simon**.
 
    c. Bonjour **adresse de messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .

    d. Cliquez sur **Add User**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre TalentLMS utilisateur compte outil de création ou API fournie par TalentLMS tooprovision des comptes d’utilisateur AAD.
 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTalentLMS.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooTalentLMS, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **TalentLMS**.

    ![Configurer l’authentification unique](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello TalentLMS vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour TalentLMS application

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

