---
title: "Didacticiel : Intégration d’Azure Active Directory à Land Gorilla Client | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et terrestres Gorilla."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a>Didacticiel : Intégration d’Azure Active Directory à Land Gorilla Client

Dans ce didacticiel, vous apprendrez comment toointegrate Client de Gorilla terrestres avec Azure Active Directory (Azure AD).

Intégrant terrestres Gorilla Client Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooLand Gorilla Client
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLand Client Gorilla (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).


## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec terres Gorilla Client, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Land Gorilla Client pour lequel l’authentification unique est activée


> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.


tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout du Client Gorilla terrestres à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD


## <a name="adding-land-gorilla-client-from-hello-gallery"></a>Ajout du Client Gorilla terrestres à partir de la galerie de hello
tooconfigure hello intégration du Client de Gorilla terrestres dans Azure AD, vous devez le Client de Gorilla tooadd terrestres à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Client de Gorilla terrestres à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **terrestres Gorilla Client**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. Dans le volet de résultats hello, sélectionnez **terrestres Gorilla Client**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Land Gorilla Client avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans terrestres Gorilla Client est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans terrestres Gorilla Client doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans terrestres Gorilla Client.

tooconfigure et test Azure AD l’authentification unique avec terres Gorilla Client, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec groupe limité.
3. **[Création d’un utilisateur de test terrestres Gorilla](#creating-a-land-gorilla-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application cliente de Gorilla terrestres.

**tooconfigure Azure AD l’authentification unique avec terres Gorilla Client, exécutez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **terrestres Gorilla Client** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. Sur hello **URL et domaine de Client Gorilla terrestres** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    a. Bonjour **identificateur** zone de texte, valeur hello du type à l’aide de hello modèle : 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide d’une des hello modèle :

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > Notez qu’il s’agit pas des valeurs réelles hello. Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle. Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur. Contact [équipe terrestres Gorilla Client](https://www.landgorilla.com/support/) tooget ces valeurs. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. configuration de SSO tooget complète pour votre application à fin terrestres Gorilla, contactez [équipe de support Client de Gorilla terrestres](https://www.landgorilla.com/support/) et fournissez-leur hello téléchargé **» Metadata XML** fichier.


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**. 

### <a name="creating-a-land-gorilla-test-user"></a>Création d’un utilisateur de test Land Gorilla

Collaborez avec [équipe de support terrestres Gorilla](https://www.landgorilla.com/support/) tooadd les utilisateurs de hello dans la plateforme de terrains Gorilla hello.
    
### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooLand accès Gorilla Client.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooLand Gorilla Client, exécutez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **terrestres Gorilla Client**.

    ![Configurer l’authentification unique](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    


### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque terrestres Gorilla Client hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour application terrestres Gorilla cliente.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
