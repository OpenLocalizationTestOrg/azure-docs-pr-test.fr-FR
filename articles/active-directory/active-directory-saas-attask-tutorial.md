---
title: "Didacticiel : Intégration d’Azure Active Directory avec @Task| Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 0840763622086a02a27cfafff3b741bc66cec498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a>Didacticiel : Intégration d'Azure Active Directory à @Task
objectif Hello de ce didacticiel est tooshow vous comment toointegrate @Task avec Azure Active Directory (Azure AD).  
Intégration @Task avec Azure AD vous fournit hello avantages suivants : 

* Vous pouvez contrôler dans Azure AD qui a accèstoo@Task
* Vous pouvez activer vos utilisateurs tooautomatically obtenir connecté too@Task (Single Sign-On) avec leurs comptes Azure AD
* Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
intégration tooconfigure Azure AD avec @Task, vous devez hello éléments suivants :

* Un abonnement Azure AD
* Un abonnement @Task pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.
> 
> 

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

* Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
* Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Description du scénario
objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.  
scénario Hello décrite dans ce didacticiel se compose de trois blocs de construction principaux :

1. Ajout de @Task à partir de la galerie de hello 
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-task-from-hello-gallery"></a>Ajout de @Task à partir de la galerie de hello
intégration de hello tooconfigure de @Task dans Azure AD, vous devez tooadd @Task à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd @Task à partir de la galerie hello, effectuez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**. 
   
    ![Active Directory][1] 
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications][2] 
4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Applications][3] 
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Applications][4] 
6. Dans la zone de recherche de hello, tapez  **@Task** .
   
    ![Applications][5] 
7. Dans le volet de résultats hello, sélectionnez  **@Task** , puis cliquez sur **Complete** application hello de tooadd.
   
    ![Applications][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
objectif de cette section Hello est tooshow vous comment tooconfigure et test Azure AD unique authentification avec @Task basé sur un utilisateur de test appelé « Brian Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello @Task utilisateur tooan dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans @Task doit toobe établie.   
Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans @Task.

tooconfigure et test Azure AD sur l’authentification unique avec @Task, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un @Tasktest utilisateur](#creating-a-halogen-software-test-user)**  -toohave un équivalent de Britta Simon dans @Taskthat est de sa représentation sous forme de toohello lié Azure AD.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD
Hello cette section vise tooenable Azure AD l’authentification unique sur Bonjour portail Azure classic et tooconfigure l’authentification unique dans votre @Task application.

**tooconfigure Azure AD l’authentification unique avec @Task, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello  **@Task**  page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**  boîte de dialogue.
   
    ![Configurer l’authentification unique][6] 
2. Sur hello **Comment voulez-vous telles que les utilisateurs toosign sur too@Task**  page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Authentification unique Azure AD][7] 
3. Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Configurer les paramètres d’application][8] 
   
     a. Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par vos utilisateurs sur toosign tooyour @Task application (par exemple :*https://<Tenant name>.attask-ondemand.com*).
   
     b. Cliquez sur **Suivant**.
4. Sur hello **configurer l’authentification unique à @Task**  , cliquez sur **télécharger des métadonnées**, enregistrez le fichier de métadonnées hello localement sur votre ordinateur, puis cliquez sur **suivant**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][9] 
5. Authentification tooyour @Task site d’entreprise en tant qu’administrateur.
6. Accédez trop**l’authentification unique sur la Configuration**.
7. Sur hello **Single Sign-On** boîte de dialogue, effectuer hello comme suit
   
    ![Configurer l’authentification unique][23]
   
    a. Comme **Type**, sélectionnez **SAML 2.0**.
   
    b. Sélectionnez **///ID fournisseur de services**.
   
    c. Sur hello portail Azure classic, copiez hello **URL de connexion distante**, puis collez-la dans hello **URL du portail de compte de connexion** zone de texte.
   
    d. Sur hello portail Azure classic, copiez hello **URL de Service de déconnexion unique**, puis collez-la dans hello **URL de déconnexion** zone de texte.
   
    e. Sur hello portail Azure classic, copiez hello **URL de modification du mot de passe**, puis collez-la dans hello **URL de modification du mot de passe** zone de texte.
   
    f. Cliquez sur **Enregistrer**.
8. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**. 
   
    ![Qu’est-ce qu’Azure AD Connect ?][10]
9. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.  
   
    ![Qu’est-ce qu’Azure AD Connect ?][11]

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.  

![Créer un utilisateur Azure AD][20]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**. 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit : 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    a. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.
   
    b. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.
   
    c. Cliquez sur **Suivant**.
6. Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit : 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    a. Bonjour **prénom** zone de texte, type **Brian**.  
   
    b. Bonjour **nom** zone de texte, type, **Simon**.
   
    c. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.
   
    d. Bonjour **rôle** liste, sélectionnez **utilisateur**.

    e. Cliquez sur **Suivant**.

7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    a. Notez la valeur hello hello **nouveau mot de passe**.
   
    b. Cliquez sur **Terminé**.   

### <a name="creating-an-task-test-user"></a>Création d’un utilisateur de test @Task
objectif Hello de cette section est toocreate un utilisateur nommé Britta Simon dans @Task.

**toocreate un utilisateur nommé Britta Simon dans @Task, effectuer hello comme suit :**

1. Ouverture de session tooyour @Task site d’entreprise en tant qu’administrateur.
2. Dans le menu hello haut de hello, cliquez sur **personnes**.
3. Cliquez sur **New Person**. 
4. Dans la boîte de dialogue nouvelle personne hello, procédez hello comme suit :
   
    ![Création d’un utilisateur de test @Task][21] 
   
    a. Bonjour **prénom** zone de texte, tapez « Brian ».
   
    b. Bonjour **nom** zone de texte, tapez « Simon ».
   
    c. Bonjour **adresse de messagerie** zone de texte, tapez l’adresse de messagerie Britta Simon dans Azure Active Directory.
   
    d. Cliquez sur **Add Person**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD
objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant l’accès too@Task.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon too@Task, effectuer hello comme suit :**

1. Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Affecter des utilisateurs][201] 
2. Dans la liste des applications hello, sélectionnez  **@Task** .
   
    ![Affecter des utilisateurs][202] 
3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Affecter des utilisateurs][203] 
4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.
5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.
   
    ![Affecter des utilisateurs][205]

### <a name="testing-single-sign-on"></a>Test de l’authentification unique
objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.  
Lorsque vous cliquez sur hello @Task vignette dans hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour @Task application.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






