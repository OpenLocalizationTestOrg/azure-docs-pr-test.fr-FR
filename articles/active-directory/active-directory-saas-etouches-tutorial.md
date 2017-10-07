---
title: "Didacticiel : Intégration d’Azure Active Directory à etouches | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et etouches."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 76cccaa8-859c-4c16-9d1d-8a6496fc7520
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 5f3ff7550e660b0fc52612140ca55061504b5edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-etouches"></a>Didacticiel : Intégration d’Azure Active Directory à etouches

Dans ce didacticiel, vous apprendrez comment etouches toointegrate avec Azure Active Directory (Azure AD).

Intégration etouches à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooetouches
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooetouches (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec etouches, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement etouches pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’etouches à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-etouches-from-hello-gallery"></a>Ajout d’etouches à partir de la galerie de hello
intégration de hello tooconfigure d’etouches dans Azure AD, vous devez etouches tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**etouches tooadd à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **etouches**, sélectionnez **etouches** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![etouches dans la liste des résultats hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec etouches avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans etouches est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans etouches doit toobe établie.

Dans etouches, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec etouches, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test etouches](#create-an-etouches-test-user)**  -toohave un homologue de Britta Simon dans etouches est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application etouches.

**tooconfigure Azure AD single sign-on avec etouches, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **etouches** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_samlbase.png)

3. Sur hello **etouches domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.eiseverywhere.com/saml/accounts/?sso&accountid=<ACCOUNTID>`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.eiseverywhere.com/<instance name>`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour de valeur de hello avec hello réel connectent URL et l’identificateur, qui est expliquée plus loin dans le didacticiel de hello.
    > 

4. etouches application attend les assertions SAML hello dans un format spécifique. Configurer hello suivant des revendications pour cette application. Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attribut utilisateur** de l’application hello. Hello suivant capture d’écran montre un exemple de cela. 

    ![Attribut utilisateur](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_attribute.png) 

5. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :
    
    | Nom de l'attribut | Valeur de l’attribut |
    | ------------------- | -------------------- |
    | Email | user.mail |    
    
    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Ajouter un attribut](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_04.png)

    ![Boîte de dialogue Ajouter un attribut](./media/active-directory-saas-etouches-tutorial/tutorial_attribute_05.png)

    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.

    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.
    
    d. Cliquez sur **OK**. 

6. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_certificate.png) 

7. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-etouches-tutorial/tutorial_general_400.png)

8. tooget SSO configuré pour votre application, effectuez hello dans l’application d’etouches hello comme suit : 

    ![Configuration d’etouches](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_06.png) 

    a. Connexion trop**etouches** application à l’aide de droits d’administrateur hello.
   
    b. Accédez toohello **SAML** Configuration.

    c. Bonjour **paramètres généraux** section et ouvrez votre certificat téléchargé à partir du portail Azure dans le bloc-notes, hello copie le contenu, puis collez-la dans la zone de texte hello IDP métadonnées. 

    d. Cliquez sur hello **Enregistrer & rester** bouton.
  
    e. Cliquez sur hello **mise à jour de métadonnées** bouton Bonjour section de métadonnées SAML. 

    f. S’ouvre hello page et effectuer l’authentification unique. Une fois hello SSO fonctionne, puis vous pouvez configurer de nom d’utilisateur hello.

    g. Dans le champ de nom d’utilisateur de hello, sélectionnez hello **emailaddress** comme indiqué dans l’image hello ci-dessous. 

    h. Hello de copie **ID d’entité SP** valeur et le coller dans hello **identificateur** zone de texte, qui se trouve dans **etouches domaine et les URL** section sur le portail Azure.

    i. Hello de copie **URL SSO / ACS** valeur et le coller dans hello **URL de connexion** zone de texte, qui se trouve dans **etouches domaine et les URL** section sur le portail Azure.
   
> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-etouches-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-etouches-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="create-an-etouches-test-user"></a>Créer un utilisateur de test etouches

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans etouches. Travailler avec [etouches Client prend en charge l’équipe](https://www.etouches.com/event-software/support/customer-support/) tooadd les utilisateurs de hello dans la plateforme d’etouches hello.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooetouches.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooetouches, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **etouches**.

    ![lien d’etouches Hello dans la liste des Applications hello](./media/active-directory-saas-etouches-tutorial/tutorial_etouches_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique


objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello etouches vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour etouches application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-etouches-tutorial/tutorial_general_203.png

