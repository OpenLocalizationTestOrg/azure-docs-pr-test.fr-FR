---
title: "Didacticiel : Intégration d’Azure Active Directory à TimeOffManager | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de TimeOffManager."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3685912f-d5aa-4730-ab58-35a088fc1cc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: c871257bfb49883e31b1c4860a9d7faa70e9ab48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-timeoffmanager"></a>Didacticiel : Intégration d’Azure AD à TimeOffManager

Dans ce didacticiel, vous apprendrez comment toointegrate TimeOffManager avec Azure Active Directory (Azure AD).

Intégration de TimeOffManager à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooTimeOffManager
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTimeOffManager (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à TimeOffManager, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement TimeOffManager pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajouter des TimeOffManager à partir de la galerie de hello
2. Configurer et tester l’authentification unique Azure AD

## <a name="add-timeoffmanager-from-hello-gallery"></a>Ajouter des TimeOffManager à partir de la galerie de hello
intégration de hello tooconfigure de TimeOffManager dans Azure AD, vous devez tooadd TimeOffManager à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd TimeOffManager à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **TimeOffManager**, sélectionnez **TimeOffManager** à partir du Panneau de résultats, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Ajouter à partir de la galerie](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TimeOffManager, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans TimeOffManager est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans TimeOffManager doit toobe établie.

Dans TimeOffManager, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à TimeOffManager, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test de TimeOffManager](#create-a-timeoffmanager-test-user)**  -toohave un équivalent de Britta Simon dans TimeOffManager est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de TimeOffManager.

**tooconfigure Azure AD single sign-on avec TimeOffManager, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **TimeOffManager** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Authentification basée sur SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_samlbase.png)

3. Sur hello **TimeOffManager domaine et les URL** section, hello suivants :

     ![Section Domaine et URL TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_url.png)

    Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.timeoffmanager.com/cpanel/sso/consume.aspx?company_id=<companyid>`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour cette valeur avec l’URL de réponse réelle hello. Vous pouvez obtenir cette valeur à partir de **l’authentification unique sur la page Paramètres** qui est expliqué plus loin dans le didacticiel de hello ou un Contact [équipe de support technique de TimeOffManager](http://www.timeoffmanager.com/contact-us.aspx).
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Section Certificat de signature SAML](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_certificate.png) 

5. objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooTimeOffManger avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.
    
    Votre application TimeOffManger attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages. Hello suivant capture d’écran montre un exemple de cela.

    ![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_attrb.png "saml token attributes")
    
    | Nom de l'attribut | Valeur de l’attribut |
    | --- | --- |
    | Firstname |User.givenname |
    | Lastname |User.Surname |
    | Email |User.mail |
    
    a.  Pour chaque ligne de données dans la table hello ci-dessus, cliquez sur **ajouter un attribut utilisateur**.
    
    ![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb.png "saml token attributes")
    
    ![saml token attributes](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_addattrb1.png "saml token attributes")
    
    b.  Bonjour **nom de l’attribut** zone de texte, nom d’attribut type hello indiqué pour cette ligne.
    
    c.  Bonjour **valeur d’attribut** zone de texte, valeur de l’attribut select hello indiqué pour cette ligne.
    
    d.  Cliquez sur **OK**.
    
6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_400.png)

7. Sur hello **TimeOffManager Configuration** , cliquez sur **configurer de TimeOffManager** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Section Configuration de TimeOffManager](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_configure.png) 

8. Dans une autre fenêtre de navigateur web, connectez-vous au site de votre entreprise TimeOffManager en tant qu’administrateur.

9. Accédez trop**compte \> Options compte \> paramètres d’authentification unique**.
   
   ![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795917.png "paramètres d’authentification unique")
7. Bonjour **paramètres d’authentification unique** section, effectuer hello comme suit :
   
   ![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795918.png "paramètres d’authentification unique")
   
   a. Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez hello l’intégralité du certificat dans **certificat X.509** zone de texte.
   
   b. Dans **émetteur Idp** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.
   
   c. Dans **URL de point de terminaison IdP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.
   
   d. Dans **Enforce SAML**, sélectionnez **No**.
   
   e. Dans **Auto-Create Users**, sélectionnez **Yes**.
   
   f. Dans **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.
   
   g. Cliquez sur **Enregistrer les modifications**.

11. Dans **l’authentification unique sur les paramètres** page, de copier la valeur de hello **Assertion Consumer Service URL** et collez-le dans hello **URL de réponse** zone de texte sous **TimeOffManager Domaine et les URL** section dans le portail Azure. 

      ![Paramètres d’authentification unique](./media/active-directory-saas-timeoffmanager-tutorial/ic795915.png "paramètres d’authentification unique")

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Utilisateurs et groupes --> Tous les utilisateurs](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Bouton Ajouter](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-timeoffmanager-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="create-a-timeoffmanager-test-user"></a>Créer un utilisateur de test TimeOffManager

Dans l’ordre tooenable Azure AD les utilisateurs toolog à TimeOffManager, ils doivent être tooTimeOffManager mis en service.  

TimeOffManager prend en charge l’approvisionnement juste-à-temps des utilisateurs. Vous n’avez rien à faire.  

les utilisateurs de Hello sont automatiquement ajoutés pendant hello première connexion à l’aide de l’authentification unique sur.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre TimeOffManager utilisateur compte outil de création ou API fournie par TimeOffManager tooprovision comptes d’utilisateur Azure AD.
> 

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTimeOffManager.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooTimeOffManager, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **TimeOffManager**.

    ![TimeOffManager dans la liste des applications](./media/active-directory-saas-timeoffmanager-tutorial/tutorial_timeoffmanager_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque TimeOffManager hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour TimeOffManager application. Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-timeoffmanager-tutorial/tutorial_general_203.png

