---
title: "Didacticiel : Intégration d’Azure Active Directory à Zendesk | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a>Didacticiel : Intégration d’Azure Active Directory à Zendesk

Dans ce didacticiel, vous apprendrez comment toointegrate Zendesk avec Azure Active Directory (Azure AD).

Intégration de Zendesk à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooZendesk
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZendesk (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Zendesk, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement pour lequel l’authentification unique à Zendesk est activée


> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.


tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Zendesk à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD


## <a name="adding-zendesk-from-hello-gallery"></a>Ajout de Zendesk à partir de la galerie de hello
tooconfigure hello intégration de Zendesk dans Azure AD, vous devez tooadd Zendesk à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Zendesk à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[Azure Portal](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Zendesk**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. Dans le volet de résultats hello, sélectionnez **Zendesk**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zendesk, sur un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zendesk est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zendesk doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Zendesk.

tooconfigure et test Azure AD l’authentification unique à Zendesk, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Zendesk](#creating-a-zendesk-test-user)**  -toohave un équivalent de Britta Simon dans Zendesk est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Zendesk.

**tooconfigure Azure AD single sign-on avec Zendesk, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Zendesk** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. Sur hello **Zendesk domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    a. Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<subdomain>.zendesk.com`

    b. Bonjour **identificateur** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<subdomain>.zendesk.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec l’URL de connexion réel hello et URL d’identificateur. Contact [équipe de support technique de Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget ces valeurs. 

4. Zendesk attend les assertions SAML hello dans un format spécifique. Absence d’attribut SAML obligatoire, mais si vous le souhaitez, vous pouvez ajouter un attribut à partir de **attributs utilisateur** section par hello suivant étapes ci-dessous : 

     ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    a. Cliquez sur hello **afficher et modifier tous les hello autres attributs** case à cocher.
     
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    b. Cliquez sur hello **ajouter un attribut** tooopen **ajouter un attribut** boîte de dialogue.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    c. Bonjour **nom** zone de texte, nom d’attribut de type hello (par exemple **emailaddress**).
    
    d. À partir de hello **valeur** liste, la valeur de l’attribut select hello (en tant que **user.mail**).
    
    e. Cliquez sur **OK**.
 
    > [!NOTE] 
    > Vous utilisez les attributs tooadd extension attributs qui ne sont pas dans Azure AD par défaut. Cliquez sur [les attributs d’utilisateur qui peuvent être définis dans SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello la liste complète des SAML attributs **Zendesk** accepte. 

5. Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. Sur hello **Zendesk Configuration** , cliquez sur **configurer de Zendesk** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zendesk en tant qu’administrateur.

8. Cliquez sur **Admin**.

9. Dans le volet de navigation gauche hello, cliquez sur **paramètres**, puis cliquez sur **sécurité**.

10. Sur hello **sécurité** page, effectuer hello comme suit : 
   
     ![Sécurité](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Sécurité")

    ![Authentification unique](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Authentification unique")

     a. Cliquez sur hello **administration et Agents** onglet.

     b. Sélectionnez **Single sign-on (SSO) and SAML**, puis **SAML**.

     c. Dans **URL SSO SAML** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure. 

     d. Dans **URL de déconnexion distante** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.
        
     e. Dans **empreinte numérique du certificat** zone de texte, collez hello **l’empreinte numérique** valeur de certificat que vous avez copié à partir du portail Azure.
     
     f. Cliquez sur **Save**.

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**. 

### <a name="creating-a-zendesk-test-user"></a>Création d’un utilisateur de test Zendesk

toolog d’utilisateurs tooenable Azure AD dans **Zendesk**, ils doivent être configurés dans **Zendesk**.  
En fonction du rôle hello affecté dans les applications hello, hello son comportement attendu :

 1. Les comptes de **l’utilisateur final** sont automatiquement approvisionnés lors de la connexion.
 2. **Agent** et **Admin** comptes doivent toobe configuré manuellement dans **Zendesk** avant de vous connecter.
 
**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **Zendesk** client.

2. Sélectionnez hello **liste de clients** onglet.

3. Sélectionnez hello **utilisateur** onglet, puis cliquez sur **ajouter**.
   
    ![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")
4. Tapez l’adresse de messagerie hello d’un compte Azure AD existant que vous souhaitez tooprovision, puis cliquez **enregistrer**.
   
    ![Nouvel utilisateur](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nouvel utilisateur")

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre Zendesk utilisateur compte outil de création ou API fournie par Zendesk tooprovision des comptes d’utilisateur AAD.


### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZendesk.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooZendesk, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Zendesk**.

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Zendesk hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Zendesk application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
