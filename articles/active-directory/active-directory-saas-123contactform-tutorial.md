---
title: "Didacticiel : Intégration d’Azure Active Directory à 123ContactForm | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 931255887845edd1aa7f53b9051a82a2f898e055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a>Didacticiel : Intégration d’Azure Active Directory à 123ContactForm

Dans ce didacticiel, vous apprendrez comment 123ContactForm toointegrate avec Azure Active Directory (Azure AD).

Intégration 123ContactForm à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès too123ContactForm
- Vous pouvez activer vos utilisateurs tooautomatically get connecté too123ContactForm (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec 123ContactForm, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement 123ContactForm pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de 123ContactForm à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-123contactform-from-hello-gallery"></a>Ajout de 123ContactForm à partir de la galerie de hello
intégration de hello tooconfigure de 123ContactForm dans Azure AD, vous devez 123ContactForm tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**123ContactForm tooadd à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **123ContactForm**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. Dans le volet de résultats hello, sélectionnez **123ContactForm**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec 123ContactForm pour un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans 123ContactForm est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans 123ContactForm doit toobe établie.

Dans 123ContactForm, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec 123ContactForm, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test 123ContactForm](#creating-a-123contactform-test-user)**  -toohave un homologue de Britta Simon dans 123ContactForm est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application 123ContactForm.

**tooconfigure Azure AD single sign-on avec 123ContactForm, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **123ContactForm** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. Sur hello **123ContactForm domaine et les URL** section, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url1.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`

4. Si vous le souhaitez application hello tooconfigure **mode initiée par SP**, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url2.png)

    a. Cliquez sur hello **afficher les paramètres d’URL avancés** option

    b. Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Vous devez tooupdate ces valeur réelle URL et identificateur qui est expliquée plus loin dans le didacticiel de hello.
    
5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. tooconfigure l’authentification unique sur **123ContactForm** côté, accédez trop[https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) et effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    a. Bonjour **messagerie** zone de texte, par courrier électronique de type hello de hello, utilisateur ex : **BrittaSimon@Contoso.com**.

    b. Cliquez sur **télécharger** et parcourir hello fichier XML de Metadata, que vous avez téléchargé à partir du portail Azure.

    c. Cliquez sur **Envoyer le formulaire**.

8. Sur hello **Microsoft Azure AD l’authentification unique sur - Configurer les paramètres application** effectuer hello comme suit :
    
    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/url3.png)

    a. Si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, hello de copie **identificateur** pour votre instance de valeur et le coller dans **identificateur** zone de texte dans **123ContactForm domaine et les URL** section sur le portail Azure.
    
    b. Si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, hello de copie **URL de réponse** pour votre instance de valeur et le coller dans **URL de réponse** zone de texte dans **123ContactForm domaine et les URL** section sur le portail Azure.

    c. Si vous le souhaitez application hello tooconfigure **mode initiée par SP**, hello de copie **URL de connexion** pour votre instance de valeur et le coller dans **URL de connexion** zone de texte dans **123ContactForm domaine et les URL** section sur le portail Azure.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-123contactform-test-user"></a>Création d’un utilisateur de test 123ContactForm

Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification seront créées automatiquement dans l’application hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès too123ContactForm.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon too123ContactForm, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **123ContactForm**.

    ![Configurer l’authentification unique](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque 123ContactForm hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour 123ContactForm application.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

