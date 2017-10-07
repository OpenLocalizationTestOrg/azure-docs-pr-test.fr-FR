---
title: "Didacticiel : Intégration d’Azure Active Directory avec IdeaScale | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a>Didacticiel : Intégration d’Azure Active Directory à IdeaScale

Dans ce didacticiel, vous apprendrez comment toointegrate IdeaScale avec Azure Active Directory (Azure AD).

Intégration d’IdeaScale à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooIdeaScale
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooIdeaScale (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à IdeaScale, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement IdeaScale pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’IdeaScale à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-ideascale-from-hello-gallery"></a>Ajout d’IdeaScale à partir de la galerie de hello
intégration de hello tooconfigure de IdeaScale dans Azure AD, vous devez tooadd IdeaScale à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd IdeaScale à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **IdeaScale**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. Dans le volet de résultats hello, sélectionnez **IdeaScale**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec IdeaScale à l’aide d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans IdeaScale est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans IdeaScale doit toobe établie.

En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à IdeaScale, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test IdeaScale](#creating-an-ideascale-test-user)**  -toohave un équivalent de Britta Simon dans IdeaScale est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application IdeaScale.

**tooconfigure Azure AD single sign-on avec IdeaScale, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **IdeaScale** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. Sur hello **IdeaScale domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.ideascale.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de IdeaScale](http://support.ideascale.com/) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. Sur hello **IdeaScale Configuration** , cliquez sur **IdeaScale de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et l’ID d’entité SAML** de hello **section de référence rapide**.

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise IdeaScale tooyour en tant qu’administrateur.

8. Accédez trop**paramètres de la Communauté**.
   
    ![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")

9. Accédez trop**sécurité \> les paramètres d’authentification unique**.
   
    ![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")

10. Pour **Single-Signon Type**, sélectionnez **SAML 2.0**.
   
    ![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")

11. Sur hello **les paramètres d’authentification unique** boîte de dialogue, effectuer hello comme suit :
   
    ![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")
   
    a. Dans **SAML IdP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.

    b. Copier le contenu de hello de votre fichier de métadonnées téléchargé à partir du portail Azure et collez-le dans hello **SAML IdP Metadata** zone de texte.

    c. Dans **Logout Success URL** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.

    d. Cliquez sur **Enregistrer les modifications**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-ideascale-test-user"></a>Création d’un utilisateur de test IdeaScale

tooenable Azure AD les utilisateurs toolog en l’occurrence, ils doivent être configurés dans tooIdeaScale. Dans le cas de hello d’IdeaScale, cette configuration est une tâche manuelle.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Connectez-vous à tooyour **IdeaScale** site d’entreprise en tant qu’administrateur.

2. Accédez trop**paramètres de la Communauté**.
   
    ![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")

3. Accédez trop**les paramètres de base \> membre gestion**.

4. Cliquez sur **Add Member**.
   
    ![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")

5. Dans la section Add New Member de hello, procédez hello comme suit :
   
    ![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")
   
    a. Bonjour **les adresses de messagerie** zone de texte, tapez Bonjour adresse de messagerie d’un compte AAD valide que vous souhaitez tooprovision.
   
    b. Cliquez sur **Enregistrer les modifications**. 
   
    >[!NOTE]
    >titulaire du compte Azure Active Directory Hello Obtient un message électronique avec un compte de hello tooconfirm lien avant son activation.
      
>[!NOTE]
>Vous pouvez utiliser n’importe quel autre IdeaScale utilisateur compte outil de création ou API fournie par IdeaScale tooprovision des comptes d’utilisateur AAD.
 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooIdeaScale.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooIdeaScale, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **IdeaScale**.

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique


objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque IdeaScale hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour IdeaScale application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

