---
title: "Didacticiel : intégration d’Azure Active Directory à Druva | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a>Didacticiel : Intégration d’Azure Active Directory à Druva

Dans ce didacticiel, vous apprendrez comment toointegrate Druva avec Azure Active Directory (Azure AD).

Intégration de Druva à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooDruva.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDruva (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Druva, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Druva pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Druva à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-druva-from-hello-gallery"></a>Ajout de Druva à partir de la galerie de hello
intégration de hello tooconfigure de Druva dans Azure AD, vous devez tooadd Druva à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Druva à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Druva**, sélectionnez **Druva** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Liste des résultats de Druva Bonjour](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Druva, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Druva est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Druva doit toobe établie.

Dans Druva, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Druva, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test de Druva](#create-a-druva-test-user)**  -toohave un équivalent de Britta Simon dans Druva est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Druva.

**tooconfigure Azure AD single sign-on avec Druva, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Druva** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. Sur hello **Druva domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://cloud.druva.com/home`

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. Votre application Druva attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton SAML** configuration. 

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans hello précédant l’image et effectuer hello comme suit :

    | Nom de l'attribut      | Valeur de l’attribut      |
    | ------------------- | -------------------- |
    | insync\_auth\_token |Entrez la valeur générée de jeton de hello |
    
    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.

    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne. valeur générée du jeton Hello est expliquée plus loin dans le didacticiel.
    
    d. Cliquez sur **OK**.    

7. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. Sur hello **Druva Configuration** , cliquez sur **configurer de Druva** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. Dans une fenêtre de navigateur web, ouvrez une session dans le site de société Druva tooyour en tant qu’administrateur.

10. Accédez trop**gérer \> paramètres**.

    ![Paramètres](./media/active-directory-saas-druva-tutorial/ic795091.png "Paramètres")

11. Dans la boîte de dialogue Paramètres d’authentification unique hello, procédez hello comme suit :

    ![Paramètres d’authentification unique](./media/active-directory-saas-druva-tutorial/ic795092.png "paramètres d’authentification unique")
    
    a. Coller **SAML Sign-On URL du Service unique** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **ID Provider Login URL** zone de texte.
    
    b. Coller **URL de déconnexion** valeur, ce qui vous avez copié à partir de hello portail Azure en hello **ID Provider Logout URL** zone de texte.
    
     c. Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **ID fournisseur certificat** zone de texte
     
     d. tooopen hello **paramètres** , cliquez sur **enregistrer**.

12. Sur hello **paramètres** , cliquez sur **générer un jeton SSO**.

    ![Paramètres](./media/active-directory-saas-druva-tutorial/ic795093.png "Paramètres")

13. Sur hello **unique authentification jeton d’authentification** boîte de dialogue, effectuer hello comme suit :

    ![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")
    
    a. Cliquez sur **copie**, coller copié la valeur Bonjour **valeur** textbox Bonjour **ajouter un attribut** section.
    
    b. Cliquez sur **Fermer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-druva-test-user"></a>Créer un utilisateur de test Druva

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooDruva, vous devez les configurer dans Druva. Dans les cas de hello de Druva, cette configuration est une tâche manuelle.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Connectez-vous à tooyour **Druva** site d’entreprise en tant qu’administrateur.

2. Accédez trop**gérer \> utilisateurs**.
   
   ![Gestion des utilisateurs](./media/active-directory-saas-druva-tutorial/ic795097.png "Gestion des utilisateurs")

3. Cliquez sur **Create New**.
   
   ![Gestion des utilisateurs](./media/active-directory-saas-druva-tutorial/ic795098.png "Gestion des utilisateurs")

4. Dans la boîte de dialogue Créer un nouvel utilisateur hello, procédez hello comme suit :
   
   ![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")
   
   a. Bonjour **adresse de messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .
   
   b. Bonjour **nom** zone de texte, entrez hello les nom d’utilisateur comme **BrittaSimon**.
   
   c. Cliquez sur **Create User**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Druva utilisateur compte outil de création ou API fournie par Druva tooprovision comptes d’utilisateur Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDruva.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooDruva, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Druva**.

    ![lien de Druva Hello dans la liste des Applications hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Druva hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Druva application.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

