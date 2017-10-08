---
title: "Didacticiel : Intégration d’Azure Active Directory à Bynder | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: a2a8477580d28fe422f2836f483dff286bc71c93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a>Didacticiel : Intégration d’Azure Active Directory avec Bynder
objectif Hello de ce didacticiel est tooshow vous comment toointegrate Bynder avec Azure Active Directory (Azure AD).

Intégration Bynder à Azure AD offre hello avantages suivants :

* Vous pouvez contrôler dans Azure AD qui a accès tooBynder
* Vous pouvez activer vos utilisateurs tooautomatically get tooBynder connecté-session unique (SSO) avec leurs comptes Azure AD
* Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
tooconfigure intégration d’Azure AD avec Bynder, vous devez hello éléments suivants :

* Un abonnement Azure AD
* Un abonnement Bynder pour lequel l’authentification unique est activée

>[!NOTE]
>tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production. 
> 

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

* Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
* Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
objectif Hello de ce didacticiel est tooenable vous tootest Microsoft Azure AD SSO dans un environnement de test.

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Bynder à partir de la galerie de hello
2. Configuration et test de l’authentification unique Microsoft Azure AD

## <a name="add-bynder-from-hello-gallery"></a>Ajouter des Bynder à partir de la galerie de hello
intégration de hello tooconfigure de Bynder dans Azure AD, vous devez tooadd Bynder à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Bynder à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**. 
   
    ![Active Directory][1]
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications][2]
4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Applications][3]
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Applications][4]
6. Dans la zone de recherche de hello, tapez **Bynder**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. Dans le volet de résultats hello, sélectionnez **Bynder**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![Sélection d’application hello dans la galerie de hello](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a>Configurer et tester l’authentification unique Microsoft Azure AD
objectif Hello de cette section est tooshow comment tooconfigure et test Microsoft Azure AD SSO avec Bynder en fonction d’un utilisateur de test appelé « Britta Simon ».

Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Bynder tooan l’utilisateur dans Azure AD est. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Bynder doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Bynder.

tooconfigure et test Microsoft Azure AD SSO avec Bynder, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration de Microsoft Azure AD l’authentification unique sur](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Microsoft Azure AD Single Sign-On with Britta Simon.
3. **[Création d’un utilisateur de test Bynder](#creating-a-bynder-test-user)**  -toohave de Britta Simon dans Bynder qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable toouse Britta Simon Microsoft Azure AD Single Sign-On.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-microsoft-azure-ad-sso"></a>Configuration de l’authentification unique Microsoft Azure AD
Dans cette section, vous activez l’authentification unique de Microsoft Azure AD dans le portail classique de hello et configurez l’authentification unique dans votre application Bynder.

**tooconfigure l’authentification unique de Microsoft Azure AD avec Bynder, effectuez hello comme suit :**

1. Dans le portail classique hello, sur hello **Bynder** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur** boîte de dialogue.
   
    ![Configurer l’authentification unique][6] 
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooBynder** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. Sur hello **configurer les paramètres de l’application** page de boîte de dialogue, si vous le souhaitez application hello tooconfigure **mode initialisée par IDP**, effectuer hello comme suit, puis cliquez sur **suivant**:
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.getbynder.com/sso/SAML/authenticate/`
  2. Cliquez sur **Suivant**.
4. Si vous le souhaitez application hello tooconfigure **mode initiée par SP** sur hello **configurer les paramètres de l’application** page de boîte de dialogue, puis cliquez sur hello **« (facultatifs) des paramètres avancé afficher »**, puis entrez hello **URL de connexion** et cliquez sur **suivant**.

    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.getbynder.com/login/`
  2. Cliquez sur **Suivant**.
  
   >[!NOTE]
   >valeur Hello hello URL de connexion de ce didacticiel est simplement un placeholfer. valeur réelle de tooget hello pour votre environnement, contactez Bynder.
   >

5. Sur hello **configurer l’authentification unique sur Bynder** page, effectuer hello comme suit, puis cliquez sur **suivant**:
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. Cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello sur votre ordinateur.
  2. Cliquez sur **Suivant**.
6. tooget SSO configuré pour votre application, contactez votre équipe de support Bynder. Attacher le fichier de métadonnées téléchargé hello et partagez-le avec tooset d’équipe Bynder configuration de SSO sur son côté.
7. Dans le portail classique hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.
   
    ![Authentification unique Azure AD][10]
8. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.  
   
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail classique de hello appelé Britta Simon.

![Créer un utilisateur Azure AD][20]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.
  2. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.
  3. Cliquez sur **Suivant**.
6. Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. Bonjour **prénom** zone de texte, type **Brian**.  
  2. Bonjour **nom** zone de texte, type, **Simon**. 
  3. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.
  4. Bonjour **rôle** liste, sélectionnez **utilisateur**.
  5. Cliquez sur **Suivant**.
7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. Notez la valeur hello hello **nouveau mot de passe**.
   2. Cliquez sur **Terminé**.   

### <a name="create-a-bynder-test-user"></a>Créer un utilisateur de test Bynder
objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Bynder. Bynder prend en charge l’approvisionnement juste-à-temps, option activée par défaut.

Vous n’avez aucune opération à effectuer dans cette section. Un nouvel utilisateur s’affichera pendant une tentative de tooaccess Bynder s’il n’existe pas encore.

>[!NOTE]
>Si vous devez manuellement toocreate un utilisateur, vous avez besoin d’équipe de support Bynder toocontact hello. 
> 

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD
objectif Hello de cette section est tooenabling Britta Simon toouse Azure SSO en accordant tooBynder de son accès.

   ![Affecter des utilisateurs][200]

**tooassign Britta Simon tooBynder, effectuez hello comme suit :**

1. Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.
   
    ![Affecter des utilisateurs][201]
2. Dans la liste des applications hello, sélectionnez **Bynder**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Affecter des utilisateurs][203]
4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.
5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a>Tester l’authentification unique
objectif Hello de cette section est tootest votre configuration de l’authentification unique de Microsoft Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Bynder hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Bynder application.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
