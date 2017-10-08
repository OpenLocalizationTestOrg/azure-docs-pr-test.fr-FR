---
title: "Didacticiel : Intégration d’Azure Active Directory avec Picturepark | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 3d826d3f73aad2f0d123f8697c6caafad7bc926a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a>Didacticiel : Intégration d’Azure Active Directory avec Picturepark

Dans ce didacticiel, vous apprendrez comment toointegrate Picturepark avec Azure Active Directory (Azure AD).

Intégration de Picturepark à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooPicturepark
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPicturepark (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Picturepark, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Picturepark pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Picturepark à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-picturepark-from-hello-gallery"></a>Ajout de Picturepark à partir de la galerie de hello
intégration de hello tooconfigure de Picturepark dans Azure AD, vous devez tooadd Picturepark à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Picturepark à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Picturepark**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. Dans le volet de résultats hello, sélectionnez **Picturepark**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Picturepark sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Picturepark est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Picturepark doit toobe établie.

Dans Picturepark, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Picturepark, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Picturepark](#creating-a-picturepark-test-user)**  -toohave un équivalent de Britta Simon dans Picturepark est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Picturepark.

**tooconfigure Azure AD single sign-on avec Picturepark, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Picturepark** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. Sur hello **Picturepark domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.picturepark.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle : 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de Picturepark](https://picturepark.com/about/contact/) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. Sur hello **Picturepark Configuration** , cliquez sur **configurer de Picturepark** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Picturepark en tant qu’administrateur.

8. Dans la barre d’outils de hello en haut de hello, cliquez sur **outils d’administration**, puis cliquez sur **Console de gestion**.
   
    ![Console de gestion](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Console de gestion")

9. Cliquez sur **Authentication**, puis sur **Identity providers**.
   
    ![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")

10. Bonjour **configuration du fournisseur d’identité** section, effectuer hello comme suit :
   
    ![Configuration du fournisseur d’identité](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Configuration du fournisseur d’identité")
   
    a. Cliquez sur **Add**.
  
    b. Entrez un nom pour votre configuration.
   
    c. Sélectionnez **Set as default**.
   
    d. Dans **URI de l’émetteur** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.
   
    e. Dans **empreinte numérique d’émetteur approuvé** zone de texte, valeur hello coller **l’empreinte numérique** dont vous avez copié à partir de **le certificat de signature SAML** section. 

11. Cliquez sur **JoinDefaultUsersGroup**.

12. tooset hello **Emailaddress** attribut Bonjour **revendication** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` et cliquez sur **enregistrer**.

      ![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-picturepark-test-user"></a>Création d’un utilisateur de test Picturepark

Dans l’ordre tooenable Azure AD les utilisateurs toolog à Picturepark, vous devez les configurer dans Picturepark. Dans les cas de hello de Picturepark, cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **Picturepark** client.

2. Dans la barre d’outils de hello en haut de hello, cliquez sur **outils d’administration**, puis cliquez sur **utilisateurs**.
   
    ![Utilisateurs](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Utilisateurs")

3. Bonjour **vue d’ensemble des utilisateurs** , cliquez sur **nouveau**.
   
    ![Gestion des utilisateurs](./media/active-directory-saas-picturepark-tutorial/ic795068.png "gestion des utilisateurs")

4. Sur hello **Create User** boîte de dialogue, effectuer hello suivant les étapes d’un utilisateur Azure Active Directory valide souhaité tooprovision :
   
    ![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")
   
    a. Bonjour **adresse de messagerie** hello de type zone de texte **adresse de messagerie** d’utilisateur de hello  **BrittaSimon@contoso.com** .  
   
    b. Bonjour **mot de passe** et **confirmer le mot de passe** zones de texte, hello de type **mot de passe** de BrittaSimon. 
   
    c. Bonjour **prénom** hello de type zone de texte **prénom** d’utilisateur de hello **Brian**. 
   
    d. Bonjour **nom** hello de type zone de texte **nom** d’utilisateur de hello **Simon**.
   
    e. Bonjour **société** hello de type zone de texte **nom de la société** d’utilisateur de hello. 
   
    f. Bonjour **pays** zone de texte, sélectionnez hello **pays** d’utilisateur de hello.
  
    g. Bonjour **ZIP** hello de type zone de texte **code postal** de ville de hello.
   
    h. Bonjour **Ville** hello de type zone de texte **nom de Ville** d’utilisateur de hello.

    i. Sélectionnez une langue dans **Language**.
   
    j. Cliquez sur **Créer**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Picturepark utilisateur compte outil de création ou API fournie par Picturepark tooprovision comptes d’utilisateur Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPicturepark.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooPicturepark, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Picturepark**.

    ![Configurer l’authentification unique](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Picturepark hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Picturepark application. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

