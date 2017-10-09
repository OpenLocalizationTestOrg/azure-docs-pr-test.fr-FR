---
title: "Didacticiel : Intégration d’Azure Active Directory à Syncplicity | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a>Didacticiel : Intégration d’Azure Active Directory à Syncplicity

Dans ce didacticiel, vous apprendrez comment toointegrate Syncplicity avec Azure Active Directory (Azure AD).

Intégration de Syncplicity avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSyncplicity
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSyncplicity (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Syncplicity, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Syncplicity pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Syncplicity à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-syncplicity-from-hello-gallery"></a>Ajout de Syncplicity à partir de la galerie de hello
intégration de hello tooconfigure de Syncplicity dans Azure AD, vous devez tooadd Syncplicity à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Syncplicity à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Syncplicity**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. Dans le volet de résultats hello, sélectionnez **Syncplicity**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Syncplicity à l’aide d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Syncplicity est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans Syncplicity hello doit toobe établie.

Dans Syncplicity, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Syncplicity, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Syncplicity](#creating-a-syncplicity-test-user)**  -toohave un équivalent de Britta Simon dans Syncplicity est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Syncplicity.

**tooconfigure Azure AD single sign-on avec Syncplicity, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Syncplicity** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. Sur hello **Syncplicity domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.syncplicity.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.syncplicity.com/sp`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de Syncplicity](https://www.syncplicity.com/contact-us) tooget ces valeurs. 
 

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. Sur hello **Syncplicity Configuration** , cliquez sur **configurer de Syncplicity** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. Connectez-vous à tooyour **Syncplicity** client.

8. Dans le menu hello haut de hello, cliquez sur **admin**, sélectionnez **paramètres**, puis cliquez sur **un domaine personnalisé et l’authentification unique sur**.
   
    ![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")

9. Sur hello **Single Sign-On (SSO)** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Authentification unique \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")   

    a. Bonjour **un domaine personnalisé** zone de texte, nom du type hello de votre domaine.
  
    b. Sélectionnez **Enabled** dans **Single Sign-On Status**.

    c. Bonjour **Id d’entité** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.

    d. Bonjour **URL de la page connexion** zone de texte, hello de coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.

    e. Bonjour **Logout page URL** zone de texte, hello de coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.

    f. Dans **certificat de fournisseur d’identité**, cliquez sur **choisir un fichier**, puis téléchargez le certificat hello dont vous avez téléchargé à partir de hello portail Azure. 

    g. Cliquez sur **ENREGISTRER LES MODIFICATIONS**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-syncplicity-test-user"></a>Création d’un utilisateur de test Syncplicity
Pour AAD utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service tooSyncplicity application. Cette section décrit comment les comptes utilisateur de toocreate AAD dans Syncplicity.

**tooprovision un tooSyncplicity de compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **Syncplicity** locataire (par exemple : `https://company.Syncplicity.com`).

2. Cliquez sur **admin** et sélectionnez **Comptes d’utilisateur**.

3. Cliquez sur **AJOUTER UN UTILISATEUR**.
   
    ![Gestion des utilisateurs](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Gestion des utilisateurs")

4. Hello de type **adresses comprises de messagerie** d’un compte AAD que vous souhaitez tooprovision, sélectionnez **utilisateur** en tant que **rôle**, puis cliquez sur **suivant**.
   
    ![Informations du compte](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Informations du compte")
   
    >[!NOTE]
    >titulaire du compte AAD Hello Obtient un message électronique contenant un lien de tooconfirm et activer le compte de hello. 
    > 

5. Sélectionnez un groupe dans votre société dont votre nouvel utilisateur doit devenir membre, puis cliquez sur **SUIVANT**.
   
    ![Appartenance de groupe](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Appartenance de groupe")
   
    >[!NOTE]
    >Si aucun groupe n’est répertorié, cliquez sur **SUIVANT**. 
    > 

6. Sélectionnez les dossiers hello vous comme tooplace sous contrôle de Syncplicity sur l’ordinateur de l’utilisateur hello et puis cliquez sur **suivant**.
   
    ![Dossiers Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Dossiers Syncplicity")

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Syncplicity utilisateur compte outil de création ou API fournie par Syncplicity tooprovision des comptes d’utilisateur AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSyncplicity.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSyncplicity, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Syncplicity**.

    ![Configurer l’authentification unique](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Syncplicity hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Syncplicity application.
## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

