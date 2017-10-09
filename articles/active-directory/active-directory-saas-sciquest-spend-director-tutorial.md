---
title: "Didacticiel : intégration d’Azure Active Directory à SciQuest Spend Director| Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le directeur de dépenses SciQuest."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 9fab641b-292e-4bef-91d1-8ccc4f3a0c1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 47c46f1297054fd96b86c1d8c66e1a55ec151497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sciquest-spend-director"></a>Didacticiel : Intégration d’Azure Active Directory avec SciQuest Spend Director
objectif Hello de ce didacticiel est tooshow vous comment toointegrate SciQuest dépenses directeur avec Azure Active Directory (Azure AD).  
Intégration du directeur de dépenses SciQuest à Azure AD offre hello avantages suivants : 

* Vous pouvez contrôler dans Azure AD qui a accès tooSciQuest directeur de dépense 
* Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSciQuest directeur dépense (Single Sign-On) avec leurs comptes Azure AD
* Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
tooconfigure intégration d’Azure AD avec le directeur de dépenses SciQuest, vous devez hello éléments suivants :

* Un abonnement Azure AD
* Un abonnement SciQuest Spend Director pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.
> 
> 

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

* Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
* Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Description du scénario
objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.  
scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout du directeur de dépenses SciQuest à partir de la galerie de hello 
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-sciquest-spend-director-from-hello-gallery"></a>Ajout du directeur de dépenses SciQuest à partir de la galerie de hello
intégration de hello tooconfigure du directeur de dépenses SciQuest dans Azure AD, vous devez tooadd directeur de dépenses SciQuest à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd SciQuest dépenses directeur à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**. 
   
    ![Active Directory][1]

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications][2]

4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Applications][3]

5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Applications][4]

6. Dans la zone de recherche de hello, tapez **sciQuest dépenses directeur**.
   
    ![Applications][5]

7. Dans le volet de résultats hello, sélectionnez **directeur de dépenses SciQuest**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![Applications][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
objectif Hello de cette section est tooshow comment tooconfigure et test Azure AD l’authentification unique avec le directeur de dépenses SciQuest en fonction d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans directeur de dépenses SciQuest tooan l’utilisateur dans Azure AD est. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le directeur de dépenses SciQuest hello doit toobe établie.  
Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** directeur de dépenses SciQuest.

tooconfigure et test Azure AD l’authentification unique avec le directeur de dépenses SciQuest, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD unique Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test du directeur de dépenses SciQuest](#creating-a-halogen-software-test-user)**  -toohave de Britta Simon SciQuest dépenses directeur est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-single-sign-on"></a>Configuration de l’authentification unique Azure AD
Hello cette section vise tooenable Azure AD l’authentification unique sur Bonjour portail Azure classic et tooconfigure l’authentification unique dans votre application Directeur de dépenses SciQuest.

**tooconfigure Azure AD l’authentification unique avec le directeur de dépenses SciQuest, effectuez hello comme suit :**

1. Bonjour portail Azure classic sur hello **directeur de dépenses SciQuest** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**boîte de dialogue.
   
    ![Configurer l’authentification unique][8]

2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooSciQuest dépense directeur** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Authentification unique Azure AD][9]

3. Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit : 
   
    ![Configurer les paramètres d’application][10]
   
     a. Bonjour **URL de connexion** zone de texte, tapez l’URL utilisée par votre toosign d’utilisateurs dans l’application Directeur de dépenses SciQuest tooyour à l’aide de hello modèle : *https://.* SciQuest.com/.**
   
     b. Bonjour **URL de réponse** zone de texte, hello de type même valeur que vous avez tapé dans hello **URL de connexion** zone de texte. 
   
     c. Cliquez sur **Suivant**.

4. Sur hello **configurer l’authentification unique au directeur de dépenses SciQuest** , cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier de métadonnées hello localement sur votre ordinateur.
   
    ![Qu’est-ce qu’Azure AD Connect ?][11]

5. Contactez SciQuest prise en charge tooenable cette méthode d’authentification à l’aide de métadonnées de hello ci-dessus téléchargé.

6. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue. 
   
    ![Qu’est-ce qu’Azure AD Connect ?][15]

7. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.  

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][100] 

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][101] 

4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**. 
   
    ![Qu’est-ce qu’Azure AD Connect ?][102] 

5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Qu’est-ce qu’Azure AD Connect ?][103] 
   
    a. Dans **Type d’utilisateur**, sélectionnez **Nouvel utilisateur dans votre organisation**.
   
    b. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.
   
    c. Cliquez sur **Suivant**.

6. Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit : 
   
    ![Qu’est-ce qu’Azure AD Connect ?][104] 
   
    a. Bonjour **prénom** zone de texte, type **Brian**.  
   
    b. Bonjour **nom** txtbox, type, **Simon**.
   
    c. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.
   
    d. Bonjour **rôle** liste, sélectionnez **utilisateur**.
   
    e. Cliquez sur **Suivant**.

7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][105]  

8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Qu’est-ce qu’Azure AD Connect ?][106]   
   
    a. Notez la valeur hello hello **nouveau mot de passe**.
   
    b. Cliquez sur **Terminé**.   

### <a name="creating-a-sciquest-spend-director-test-user"></a>Création d’un utilisateur de test SciQuest Spend Director
objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon directeur de dépenses SciQuest.

Vous devez toocontact votre équipe de support du directeur de dépenses SciQuest et que vous les fournissez des détails de hello sur votre tooget de compte de test de que sa création.

Sinon, vous pouvez également tirer parti de l’approvisionnement juste-à-temps, une fonctionnalité d’authentification unique prise en charge par SciQuest Spend Director.  
Si l’approvisionnement juste-à-temps est activé, SciQuest Spend Director crée les utilisateurs automatiquement, si nécessaire, lors d’une tentative d’authentification unique. Cette fonctionnalité élimine la nécessité de hello toomanually créer équivalent de l’authentification unique des utilisateurs.

tooget juste-à-temps de configuration activé, vous devez toocontact vous êtes directeur de dépenses SciQuest votre équipe.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD
objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant son tooSciQuest accès directeur de dépense.

![Qu’est-ce qu’Azure AD Connect ?][200]

**tooassign Britta Simon tooSciQuest directeur de dépense, effectuez hello comme suit :**

1. Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Qu’est-ce qu’Azure AD Connect ?][201]

2. Dans la liste des applications hello, sélectionnez **directeur de dépenses SciQuest**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][202]

3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][203]

4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][204]

5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][205]

### <a name="testing-single-sign-on"></a>Test de l’authentification unique
objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.  
Lorsque vous cliquez sur mosaïque du directeur de dépenses SciQuest hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour directeur de dépenses SciQuest application.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_01.png
[6]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_05.png
[8]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_07.png
[10]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_08.png
[11]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_03.png
[15]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_04.png

[100]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_15.png 
[200]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_sciquest_spend_director_06.png
[203]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_18.png
[204]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_19.png
[205]: ./media/active-directory-saas-sciquest-spend-director-tutorial/tutorial_general_20.png

