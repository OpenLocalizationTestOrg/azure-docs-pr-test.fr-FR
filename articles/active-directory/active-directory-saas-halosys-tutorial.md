---
title: "Didacticiel : intégration d’Azure Active Directory à Halosys | Microsoft Docs"
description: "Découvrez comment toouse Halosys avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 42a0eb7c-5cb7-44a9-b00b-b0e7df4b63e8
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 18043ed1b6f7ab45c59cfd36252bef1621618e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halosys"></a>Didacticiel : intégration d’Azure Active Directory à Halosys

Dans ce didacticiel, vous apprendrez comment toointegrate Halosys avec Azure Active Directory (Azure AD).

Intégration Halosys à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooHalosys
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHalosys (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Halosys, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Halosys pour lequel l’authentification unique est activée


> [!NOTE] 
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.


tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Halosys à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD


## <a name="adding-halosys-from-hello-gallery"></a>Ajout de Halosys à partir de la galerie de hello
intégration de hello tooconfigure de Halosys dans Azure AD, vous devez tooadd Halosys à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Halosys à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.

    ![Active Directory][1]
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.

    ![Applications][2]

4. Cliquez sur **ajouter** bas hello de page de hello.

    ![Applications][3]

5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.

    ![Applications][4]

6. Dans la zone de recherche de hello, tapez **Halosys**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_01.png)
    
7. Dans le volet de résultats hello, sélectionnez **Halosys**, puis cliquez sur **Complete** application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_011.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Halosys avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Halosys est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Halosys doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Halosys.

tooconfigure et test Azure AD l’authentification unique avec Halosys, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Halosys](#creating-a-halosys-test-user)**  -toohave de Britta Simon dans Halosys qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail classique de hello et configurez l’authentification unique dans votre application Halosys.


**tooconfigure Azure AD single sign-on avec Halosys, effectuez hello comme suit :**

1. Dans le portail classique hello, sur hello **Halosys** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur** boîte de dialogue.
     
    ![Configurer l’authentification unique][6] 

2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooHalosys** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_03.png) 

3. Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_04.png) 

    a. Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par votre application de Halosys tooyour toosign sur les utilisateurs à l’aide de hello modèle : `https://<company-name>.Halosys.com/client-api/api`.

    b.In hello **URL d’identificateur** zone de texte, tapez l’URL hello Bonjour modèle : `https://<company-name>.Halosys.com`. 
         
4. Sur hello **configurer l’authentification unique sur Halosys** , cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello sur votre ordinateur :

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_05.png)
   
5. tooget SSO configuré pour votre application, contactez l’équipe de support Halosys et leur fournir des éléments suivants de hello :

    hello • téléchargé **fichier de métadonnées**
    
    • hello **URL SSO SAML**
    

6. Dans le portail classique hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.
    
    ![Authentification unique Azure AD][10]

7. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.  
 
    ![Authentification unique Azure AD][11]


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
Dans cette section, vous créez un utilisateur de test dans le portail classique de hello appelé Britta Simon.


![Créer un utilisateur Azure AD][20]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_09.png) 

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_03.png) 

4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_04.png) 

5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit : ![création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_05.png) 

    a. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.

    b. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.

    c. Cliquez sur **Suivant**.

6.  Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit : ![création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_06.png) 

    a. Bonjour **prénom** zone de texte, type **Brian**.  

    b. Bonjour **nom** zone de texte, type, **Simon**.

    c. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.

    d. Bonjour **rôle** liste, sélectionnez **utilisateur**.

    e. Cliquez sur **Suivant**.

7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_07.png) 

8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-Halosys-tutorial/create_aaduser_08.png) 

    a. Notez la valeur hello hello **nouveau mot de passe**.

    b. Cliquez sur **Terminé**.   



### <a name="creating-a-halosys-test-user"></a>Création d’un utilisateur de test Halosys

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Halosys. Collaborez avec Halosys prise en charge team tooadd hello utilisateurs dans la plateforme de Halosys hello.


### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooHalosys de son accès.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooHalosys, effectuez hello comme suit :**

1. Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Halosys**.

    ![Configurer l’authentification unique](./media/active-directory-saas-Halosys-tutorial/tutorial_Halosys_50.png) 

3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.

    ![Affecter des utilisateurs][203]

4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.

5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.

    ![Affecter des utilisateurs][205]


### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello Halosys vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Halosys application.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-Halosys-tutorial/tutorial_general_205.png
