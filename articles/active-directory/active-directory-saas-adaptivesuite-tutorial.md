---
title: "Didacticiel : Intégration d’Azure Active Directory à Adaptative Suite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de la Suite adaptative."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 13af9d00-116a-41b8-8ca0-4870b31e224c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: af309c27ab74098c1e229c80adb11c96dc2774fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adaptive-suite"></a>Didacticiel : Intégration d’Azure Active Directory à Adaptative Suite

Dans ce didacticiel, vous apprendrez comment toointegrate Suite adaptative avec Azure Active Directory (Azure AD).

Intégration Suite adaptative à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAdaptive Suite
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAdaptive Suite (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Suite adaptative, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Adaptive Suite pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Suite adaptative à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-adaptive-suite-from-hello-gallery"></a>Ajout de Suite adaptative à partir de la galerie de hello
intégration de hello tooconfigure de Suite adaptative dans Azure AD, vous devez tooadd Suite adaptative à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Suite adaptative à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Suite adaptative**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_search.png)

5. Dans le volet de résultats hello, sélectionnez **Suite adaptative**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Adaptive Suite, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Suite adaptative est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la Suite adaptative hello doit toobe établie.

Dans la Suite adaptative, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Suite adaptative, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Suite adaptative](#creating-an-adaptive-suite-test-user)**  -toohave un équivalent de Britta Simon dans Suite adaptative qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Suite adaptative.

**tooconfigure Azure AD single sign-on avec Suite adaptative, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Suite adaptative** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_samlbase.png)

3. Sur hello **adaptative Suite de domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_url.png)

    Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://login.adaptiveinsights.com:443/samlsso/<unique-id>`

    >[!NOTE]
    > Vous pouvez obtenir cette valeur à partir de hello Suite adaptative **SAML SSO Settings** page.
    >  

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_400.png)

6. Sur hello **Configuration de la Suite adaptative** , cliquez sur **configurer la Suite adaptative** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_configure.png) 

7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise tooyour Suite adaptative en tant qu’administrateur.

8. Accédez trop**Admin**.
   
    ![Administrateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administrateur")

9. Bonjour **utilisateurs et rôles** , cliquez sur **gérer les paramètres de l’authentification unique SAML**.
   
    ![Gérer les paramètres d’authentification unique de SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805645.png "Gérer les paramètres d’authentification unique de SAML")

10. Sur hello **SAML SSO Settings** page, effectuer hello comme suit :
   
    ![Paramètres d’authentification unique de SAML](./media/active-directory-saas-adaptivesuite-tutorial/IC805646.png "Paramètres d’authentification unique de SAML")

    a. Bonjour **nom de fournisseur d’identité** zone de texte, tapez un nom pour votre configuration.
    
    b. Hello de coller **ID d’entité SAML** valeur copiée à partir du portail Azure dans hello **fournisseur d’identité de l’entité** zone de texte.
  
    c. Hello de coller **SAML Sign-On URL du Service unique** valeur copiée à partir du portail Azure dans hello **fournisseur d’identité URL SSO** zone de texte.
  
    d. Hello de coller **SAML Sign-On URL du Service unique** valeur copiée à partir du portail Azure dans hello **URL de déconnexion personnalisé** zone de texte.
  
    e. tooupload votre certificat téléchargé, cliquez sur **choisir un fichier**.
  
    f. Sélectionnez hello qui suit, pour :
    * Pour **SAML user id**, sélectionnez **User’s Adaptive Insights user name**.
    * Pour **SAML user id location**, sélectionnez **User id in NameID of Subject**.
    * Pour **SAML NameID format**, sélectionnez **Email address**.
    * Pour **Enable SAML**, sélectionnez **Allow SAML SSO and direct Adaptive Insights login**.
    
    g. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adaptivesuite-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-adaptive-suite-test-user"></a>Création d’un utilisateur de test Adaptive Suite

tooenable Azure AD les utilisateurs toolog dans tooAdaptive Suite, vous devez les configurer dans Suite adaptative.  

* Dans les cas de hello de Suite adaptative, cette configuration est une tâche manuelle.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :** 

1. Connectez-vous à tooyour **Suite adaptative** site d’entreprise en tant qu’administrateur.
2. Accédez trop**Admin**.
   
   ![Administrateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805644.png "Administrateur")
3. Bonjour **utilisateurs et rôles** , cliquez sur **ajouter un utilisateur**.
   
   ![Ajouter un utilisateur](./media/active-directory-saas-adaptivesuite-tutorial/IC805648.png "Ajouter un utilisateur")
4. Bonjour **nouvel utilisateur** section, effectuer hello comme suit :
   
   ![Envoyer](./media/active-directory-saas-adaptivesuite-tutorial/IC805649.png "Envoyer")   

   a. Hello de type **nom**, **connexion**, **messagerie**, **mot de passe** d’un utilisateur Azure Active Directory valide que vous souhaitez tooprovision dans hello liée zones de texte.
  
   b. Sélectionnez un **rôle**.
  
   c. Cliquez sur **Envoyer**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Suite adaptative utilisateur compte outil de création ou API fournie par la Suite adaptative tooprovision des comptes d’utilisateur AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAdaptive Suite.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooAdaptive Suite, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Suite adaptative**.

    ![Configurer l’authentification unique](./media/active-directory-saas-adaptivesuite-tutorial/tutorial_adaptivesuite_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre Microsoft Azure AD Single Sign-On configuration à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Suite adaptative hello hello volet d’accès, vous devez obtenir l’application de Suite adaptative tooyour automatiquement signé sur.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adaptivesuite-tutorial/tutorial_general_203.png

