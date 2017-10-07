---
title: "Tutorial: Intégration d'Azure Active Directory à Moxtra | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Moxtra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2aed2d4b-1dcd-4839-8fed-9419d107c61c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 82e2fcc390ba508e86a3992ec1c81d0a0ffed96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moxtra"></a>Didacticiel : Intégration d'Azure Active Directory avec Moxtra

Dans ce didacticiel, vous apprendrez comment toointegrate Moxtra avec Azure Active Directory (Azure AD).

Intégration Moxtra à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooMoxtra
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMoxtra (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure moxtra intégration d’Azure AD, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Moxtra pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Moxtra à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-moxtra-from-hello-gallery"></a>Ajout de Moxtra à partir de la galerie de hello
intégration de hello tooconfigure de Moxtra dans Azure AD, vous devez tooadd Moxtra à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Moxtra à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Moxtra**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_search.png)

5. Dans le volet de résultats hello, sélectionnez **Moxtra**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Moxtra, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Moxtra est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Moxtra doit toobe établie.

Dans Moxtra, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique sur moxtra, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Moxtra](#creating-a-moxtra-test-user)**  -toohave un équivalent de Britta Simon dans Moxtra est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Moxtra.

**tooconfigure Azure AD l’authentification unique sur moxtra, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Moxtra** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_samlbase.png)

3. Sur hello **Moxtra domaine et les URL** section, effectuer hello suivant l’étape :

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_url.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://www.moxtra.com/service/#login`

4. Moxtra application attend les assertions SAML hello dans un format spécifique. Configurer hello suivant des revendications pour cette application. Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application. Hello suivant capture d’écran montre un exemple de cette configuration. 

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_attributes.png)
    
5. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :
    
    | Nom de l'attribut | Valeur de l’attribut |
    | ------------------- | -------------------- |    
    | firstname | user.givenname |
    | lastname | user.surname |
    | idpid    | < ID d’entité SAML > 

    > [!Note]
    > Hello valeur **idpid** attribut n’est pas réel. Vous pouvez obtenir la valeur réelle de hello de **aide-mémoire** sous **Moxtra Configuration**.
    
    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_04.png)

    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_attribute_05.png)

    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.

    d. Cliquez sur **OK**.
    
5. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_general_400.png)

7. Sur hello **Moxtra Configuration** , cliquez sur **Moxtra de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_configure.png) 

8. Dans une autre fenêtre de navigateur, connectez-vous sur le site d’entreprise tooyour Moxtra en tant qu’administrateur.

9. Dans la barre d’outils de hello en hello gauche, cliquez sur **Console d’administration > SAML Single Sign-on**, puis cliquez sur **nouveau**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_06.png) 

10. Sur hello **SAML** page, effectuer hello comme suit :
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_08.png)   
 
    a. Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : *SAML*). 
  
    b. Bonjour **IdP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure. 
 
    c. Dans **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure. 
 
    d. Bonjour **AuthnContextClassRef** zone de texte, type **urn : oasis : noms : tc : SAML:2.0:ac:classes:Password**. 
 
    e. Bonjour **NameID Format** zone de texte, type **urn : oasis : noms : tc : SAML:1.1:nameid-format : emailAddress**. 
 
    f. Ouvrir certificat dont vous avez téléchargé à partir du portail Azure dans le bloc-notes, copier le contenu de hello et collez-le à hello **certificat** zone de texte.    
 
    g. Dans la zone de domaine hello SAML par courrier électronique, tapez votre domaine de messagerie SAML.    
  
    >[!NOTE]
    >domaine de hello tooverify toosee hello étapes, cliquez sur hello »**i**» ci-dessous.

    h. Cliquez sur **Update**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-moxtra-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-moxtra-test-user"></a>Création d'un utilisateur de test Moxtra

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Moxtra.

**toocreate un utilisateur appelé Britta Simon dans Moxtra, effectuez hello comme suit :**

1. Se connecter tooyour Moxtra site d’entreprise en tant qu’administrateur.

2. Dans la barre d’outils de hello en hello gauche, cliquez sur **Console d’administration > Gestion des utilisateurs**, puis **ajouter un utilisateur**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_10.png) 

3. Sur hello **ajouter un utilisateur** boîte de dialogue, effectuer hello comme suit :
  
    a. Bonjour **prénom** zone de texte, type **Brian**.
  
    b. Bonjour **nom** zone de texte, type **Simon**.
  
    c. Bonjour **messagerie** zone de texte, type d’adresse de messagerie de Brian même que sur le portail Azure.
  
    d. Bonjour **Division** zone de texte, type **Dev**.
  
    e. Bonjour **service** zone de texte, type **informatique**.
  
    f. Sélectionnez **Administrateur**.
  
    g. Cliquez sur **Add**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMoxtra.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooMoxtra, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Moxtra**.

    ![Configurer l’authentification unique](./media/active-directory-saas-moxtra-tutorial/tutorial_moxtra_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Moxtra hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Moxtra application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moxtra-tutorial/tutorial_general_203.png

