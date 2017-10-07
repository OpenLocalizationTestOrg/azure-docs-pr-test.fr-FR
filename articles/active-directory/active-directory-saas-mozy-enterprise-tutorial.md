---
title: "Didacticiel : Intégration d’Azure Active Directory avec Mozy Enterprise | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Mozy Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 489b5e62-85c2-45c9-8766-326632d48114
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: bab0df4f3621b784cd8edfda3c8e10fe5a7ced9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mozy-enterprise"></a>Didacticiel : Intégration d’Azure Active Directory avec Mozy Enterprise

Dans ce didacticiel, vous apprendrez comment toointegrate Mozy Enterprise avec Azure Active Directory (Azure AD).

Intégration de Mozy Enterprise à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooMozy Enterprise
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMozy entreprise (SSO) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Mozy Enterprise, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Mozy Enterprise pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Mozy Enterprise à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-mozy-enterprise-from-hello-gallery"></a>Ajout de Mozy Enterprise à partir de la galerie de hello
intégration de hello tooconfigure de Mozy Enterprise à Azure AD, vous devez tooadd Mozy Enterprise à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Mozy Enterprise à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Mozy Enterprise**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_search.png)

5. Dans le volet de résultats hello, sélectionnez **Mozy Enterprise**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mozy Enterprise avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Mozy Enterprise est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Mozy Enterprise doit toobe établie.

Dans Mozy Enterprise, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Mozy Enterprise, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Mozy Enterprise](#creating-a-mozy-enterprise-test-user)**  -toohave un équivalent de Britta Simon dans Mozy Enterprise qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Mozy Enterprise.

**tooconfigure Azure AD single sign-on avec Mozy Enterprise, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Mozy Enterprise** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_samlbase.png)

3. Sur hello **URL et le domaine d’entreprise Mozy** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_url.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenantname>.Mozyenterprise.com`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour de cette valeur avec hello URL de connexion réel. Contact [équipe de support technique de Mozy Enterprise Client](http://support.mozy.com/) tooget cette valeur.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_400.png)

6. Sur hello **Mozy Enterprise Configuration** , cliquez sur **configurer Mozy Enterprise** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_configure.png) 

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Mozy Enterprise en tant qu’administrateur.

8. Bonjour **Configuration** , cliquez sur **stratégie d’authentification**.
   
   ![Stratégie d’authentification](./media/active-directory-saas-mozy-enterprise-tutorial/ic777314.png "Stratégie d’authentification")

9. Sur hello **stratégie d’authentification** section, effectuer hello comme suit :
   
   ![Stratégie d’authentification](./media/active-directory-saas-mozy-enterprise-tutorial/ic777315.png "Stratégie d’authentification")
   
   a. Sélectionnez **Directory Service** comme **Provider**.
   
   b. Sélectionnez **Use LDAP Push**.
   
   c. Cliquez sur hello **l’authentification SAML** onglet.
   
   d. Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL d’authentification** zone de texte.
   
   e. Coller **ID d’entité SAML**, lequel vous avez copié à partir de hello portail Azure en hello **point de terminaison SAML** zone de texte.
   
   f. Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez hello l’intégralité du certificat dans **certificat SAML** zone de texte.
   
   g. Sélectionnez **activer authentification unique pour les administrateurs des toolog avec leurs informations d’identification réseau**.
   
   h. Cliquez sur **Enregistrer les modifications**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-mozy-enterprise-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-mozy-enterprise-test-user"></a>Création d’un utilisateur de test Mozy Enterprise

Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Mozy Enterprise, vous devez les configurer dans Mozy Enterprise. Dans les cas de hello de Mozy Enterprise, cette configuration est une tâche manuelle.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Mozy Enterprise utilisateur compte outil de création ou API fournie par Mozy Enterprise tooprovision des comptes d’utilisateur AAD.

**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**

1. Connectez-vous à tooyour **Mozy Enterprise** client.

2. Cliquez sur **Users**, puis sur **Add New User**.
   
   ![Utilisateurs](./media/active-directory-saas-mozy-enterprise-tutorial/ic777317.png "Utilisateurs")
   
   >[!NOTE]
   >Hello **ajouter un nouvel utilisateur** option n’est affichée uniquement si **Mozy** est sélectionné en tant que fournisseur hello sous **stratégie d’authentification**. Si l’authentification SAML est configurée, puis hello utilisateurs sont ajoutés automatiquement lors de leur première connexion via l’authentification unique sur.
    
3. Sur hello nouvelle boîte de dialogue utilisateur, effectuez hello comme suit :
   
   ![Ajouter des utilisateurs](./media/active-directory-saas-mozy-enterprise-tutorial/ic777318.png "ajouter des utilisateurs")
   
   a. À partir de hello **choisir un groupe** , sélectionnez un groupe.
   
   b. À partir de hello **quel type d’utilisateur** , sélectionnez un type.
   
   c. Bonjour **nom d’utilisateur** zone de texte Nom hello du type d’utilisateur de hello Azure AD.
   
   d. Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie de l’utilisateur de hello Azure AD.
   
   e. Sélectionnez **Send user instruction email**.
   
   f. Cliquez sur **Add User(s)**.

     >[!NOTE]
     > Après avoir créé un utilisateur de hello, un e-mail sera envoyé utilisateur Azure AD toohello qui inclut un compte de hello tooconfirm lien avant son activation.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMozy Enterprise.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooMozy Enterprise, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Mozy Enterprise**.

    ![Configurer l’authentification unique](./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_mozyenterprise_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello Mozy Enterprise vignette Bonjour volet d’accès, vous devez obtenir la page de connexion de l’application de Mozy Enterprise.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mozy-enterprise-tutorial/tutorial_general_203.png

