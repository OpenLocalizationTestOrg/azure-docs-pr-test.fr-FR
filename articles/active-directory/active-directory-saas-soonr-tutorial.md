---
title: "Didacticiel : Intégration d’Azure Active Directory à Soonr Workplace | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail Soonr."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: f950b45d0beceab2fa17b7690c9de81ec6603089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a>Didacticiel : Intégration d’Azure Active Directory à Soonr Workplace

objectif Hello de ce didacticiel est tooshow vous comment toointegrate Soonr espace de travail avec Azure Active Directory (Azure AD).  
Intégration d’espace de travail Soonr à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSoonr espace de travail
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSoonr espace de travail (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’espace de travail Soonr, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Soonr Workplace pour lequel l’authentification unique est activée


> [!NOTE] 
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.


tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Description du scénario
objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.  
scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’espace de travail Soonr à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD


## <a name="adding-soonr-workplace-from-hello-gallery"></a>Ajout d’espace de travail Soonr à partir de la galerie de hello
intégration de hello tooconfigure Soonr espace de travail dans Azure AD, vous devez tooadd Soonr espace de travail à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Soonr espace de travail à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**. 

    ![Active Directory][1]

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.

    ![Applications][2]

4. Cliquez sur **ajouter** bas hello de page de hello.

    ![Applications][3]

5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
 
    ![Applications][4]

6. Dans la zone de recherche de hello, tapez **espace de travail Soonr**.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. Dans le volet de résultats hello, sélectionnez **espace de travail Soonr**, puis cliquez sur **Complete** application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
objectif Hello de cette section est tooshow comment tooconfigure et test Azure AD l’authentification unique avec l’espace de travail Soonr en fonction d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello utilisateur de tooan Soonr espace de travail dans Azure AD est. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’espace de travail Soonr hello doit toobe établie.  

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans l’espace de travail Soonr.

tooconfigure et test Azure AD l’authentification unique avec l’espace de travail Soonr, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test d’espace de travail Soonr](#creating-a-soonr-workplace-test-user)**  -toohave de Britta Simon dans l’espace de travail Soonr qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail classique de hello et configurez l’authentification unique dans votre application de l’espace de travail Soonr.


**tooconfigure Azure AD single sign-on avec Soonr, espace de travail, effectuez hello comme suit :**

1. Bonjour portail Azure classic sur hello **espace de travail Soonr** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**  boîte de dialogue.

    ![Configurer l’authentification unique][6] 

2. Sur hello **Comment souhaitez-vous toosign les utilisateurs sur l’espace de travail de tooSoonr** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :.

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle : `https://<server-name>.soonr.com/singlesignon/saml/SSO`.

    b. Cliquez sur **Suivant**.

    > [!NOTE] 
    > Notez qu’il ne s’agit pas de la valeur réelle hello. Vous avez tooupdate URL de connexion cette valeur avec hello réel. Espace de travail Soonr contact prend en charge team tooget cette valeur.

4. Sur hello **configurer l’authentification unique à l’espace de travail Soonr** , cliquez sur **télécharger des métadonnées** , puis enregistrez le fichier hello sur votre ordinateur :

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. tooget SSO configuré pour votre application, contactez votre équipe de support Soonr espace de travail et leur fournir des éléments suivants de hello : 

    hello • téléchargé **métadonnées** fichier

    • hello **URL de l’émetteur**

    • hello **URL SSO SAML**

    • hello **URL de Service de déconnexion unique**

    >[!NOTE]
    >Cette application est remplacée par <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">espace de travail Autotask</a> et vous pouvez faire référence <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">cela</a> didacticiel pour la configuration d’application hello avec Azure AD.
   
6. Bonjour portail Azure classic, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.

    ![Authentification unique Azure AD][10]

7. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.  
  
    ![Authentification unique Azure AD][11]



### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.  

![Créer un utilisateur Azure AD][20]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    a. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.

    b. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.

    c. Cliquez sur **Suivant**.

6.  Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    a. Bonjour **prénom** zone de texte, type **Brian**.  

    b. Bonjour **nom** zone de texte, type, **Simon**.

    c. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.

    d. Bonjour **rôle** liste, sélectionnez **utilisateur**.

    e. Cliquez sur **Suivant**.

7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    a. Notez la valeur hello hello **nouveau mot de passe**.

    b. Cliquez sur **Terminé**.   



### <a name="creating-a-soonr-workplace-test-user"></a>Création d’un utilisateur de test Soonr Workplace

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans l’espace de travail Soonr. Collaborez avec l’espace de travail Soonr prise en charge team toocreate un utilisateur dans la plateforme de hello. Vous pouvez augmenter le ticket de support hello avec Soonr de <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">ici</a>.


### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant son tooSoonr accès espace de travail.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSoonr espace de travail, effectuez hello comme suit :**

1. Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **espace de travail Soonr**.

    ![Configurer l’authentification unique](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.

    ![Affecter des utilisateurs][203] 

1. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.

2. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.

    ![Affecter des utilisateurs][205]



### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.  
Lorsque vous cliquez sur hello espace de travail Soonr vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur application de l’espace de travail Soonr tooyour.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
