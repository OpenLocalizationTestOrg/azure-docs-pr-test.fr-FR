---
title: "Didacticiel : Intégration d’Azure Active Directory avec InsideView | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et InsideView."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a>Didacticiel : Intégration d’Azure Active Directory à InsideView

Dans ce didacticiel, vous apprendrez comment toointegrate InsideView avec Azure Active Directory (Azure AD).

Intégration d’InsideView avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooInsideView
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooInsideView (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à InsideView, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement InsideView pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’InsideView à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-insideview-from-hello-gallery"></a>Ajout d’InsideView à partir de la galerie de hello
intégration de hello tooconfigure de InsideView dans tooAzure AD, vous devez tooadd InsideView à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd InsideView à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **InsideView**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. Dans le volet de résultats hello, sélectionnez **InsideView**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec InsideView, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans InsideView est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans InsideView doit toobe établie.

Dans InsideView, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec InsideView, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test InsideView](#creating-a-insideview-test-user)**  -toohave un équivalent de Britta Simon dans InsideView est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application InsideView.

**tooconfigure Azure AD single sign-on avec InsideView, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **InsideView** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. Sur hello **InsideView domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://my.insideview.com/iv/<STS Name>/login.iv`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour cette valeur avec l’URL de réponse réelle hello. Contact [équipe de support InsideView ](mailto:support@insideview.com) tooget cette valeur.
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Raw)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. Sur hello **InsideView Configuration** , cliquez sur **InsideView de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise InsideView tooyour en tant qu’administrateur.

8. Dans la barre d’outils de hello en haut de hello, cliquez sur **Admin**, **SingleSignOn Settings**, puis cliquez sur **Add SAML**.
   
   ![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")

9. Bonjour **ajouter un nouveau SAML** section, effectuer hello comme suit :

    ![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")
   
    a. Bonjour **Name STS** zone de texte, tapez un nom pour votre configuration.

    b. Dans **SamlP/WS-Fed de point de terminaison non sollicité** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.
    
    c. Ouvrez votre certificat codé en base 64, qui vous avez téléchargé à partir d’Azure hello copie portail, contenu de celui-ci dans le Presse-papiers, et le coller ensuite toohello **STS Certificate** zone de texte.

    d. Bonjour **Crm User Id Mapping** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
        
    e. Bonjour **Crm Email Mapping** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    f. Bonjour **Crm First Name Mapping** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.
    
    g. Bonjour **Crm lastName Mapping** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.  

    h. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 
 
### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-insideview-test-user"></a>Création d’un utilisateur de test InsideView

tooenable Azure AD les utilisateurs toolog dans tooInsideView, ils doivent être configurés dans tooInsideView. Dans le cas de hello d’InsideView, cette configuration est une tâche manuelle.

tooget utilisateurs ou des contacts créés dans InsideView, contactez [équipe de support InsideView](mailto:support@insideview.com).

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre InsideView utilisateur compte outil de création ou API fournie par InsideView tooprovision comptes d’utilisateur Azure AD.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooInsideView.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooInsideView, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **InsideView**.

    ![Configurer l’authentification unique](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque InsideView hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour InsideView application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

