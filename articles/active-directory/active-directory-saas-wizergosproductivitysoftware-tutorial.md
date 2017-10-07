---
title: "Didacticiel : Intégration d’Azure Active Directory avec Wizergos Productivity Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les logiciels de productivité Wizergos."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: acc04396-13c5-4c24-ab9a-30fbc9234ebd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/20/2017
ms.author: jeedes
ms.openlocfilehash: cdd186c38c426dde404ed8bb84700faf9c8c1a46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wizergos-productivity-software"></a>Didacticiel : Intégration d’Azure Active Directory avec Wizergos Productivity Software
objectif Hello de ce didacticiel est tooshow vous comment toointegrate Wizergos des logiciels de productivité avec Azure Active Directory (Azure AD).

Intégration des logiciels de productivité Wizergos à Azure AD offre hello avantages suivants :

* Vous pouvez contrôler dans Azure AD qui a accès tooWizergos logiciels de productivité
* Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWizergos logiciels de productivité-session unique (SSO) avec leurs comptes Azure AD
* Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
tooconfigure intégration d’Azure AD avec des logiciels de productivité Wizergos, vous devez hello éléments suivants :

* Un abonnement Azure AD
* Un abonnement Wizergos Productivity Software pour lequel l’authentification unique est activée

>[!NOTE]
>tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production. 
> 

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

* Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
* Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
objectif Hello de ce didacticiel est tooenable vous tootest Azure AD SSO dans un environnement de test.

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’un logiciel de productivité Wizergos à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-wizergos-productivity-software-from-hello-gallery"></a>Ajout d’un logiciel de productivité Wizergos à partir de la galerie de hello
intégration de hello tooconfigure Wizergos de logiciels de productivité dans Azure AD, vous devez tooadd Wizergos la productivité des logiciels à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Wizergos des logiciels de productivité à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**. 
   
    ![Active Directory][1]
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications][2]
4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Applications][3]
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Applications][4]
6. Dans la zone de recherche de hello, tapez **Wizergos productivité logiciel**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_01.png)
7. Dans le volet de résultats hello, sélectionnez **logiciels de productivité Wizergos**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![Sélection d’application hello dans la galerie de hello](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_001.png)

## <a name="configure-and-test-azure-ad-sso"></a>Configurer et tester l’authentification unique Azure AD
objectif Hello de cette section est tooshow comment tooconfigure et tester l’authentification unique d’Azure AD avec des logiciels de productivité Wizergos en fonction d’un utilisateur de test appelé « Britta Simon ».

Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur équivalent hello Wizergos productivité tooan utilisateur dans Azure AD est. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le logiciel de productivité Wizergos hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** Wizergos productivité logiciel.

tooconfigure et test Azure AD l’authentification unique avec BynWizergos productivité Softwareder, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD l’authentification unique sur](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de logiciels de productivité Wizergos](#creating-a-wizergos-productivity-software-test-user)**  -toohave de Britta Simon Wizergos productivité logiciel qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-sso"></a>Configuration de l’authentification unique Azure AD
Dans cette section, vous activez Azure AD l’authentification unique dans le portail classique de hello et configurez l’authentification unique dans votre application Wizergos productivité.

**tooconfigure Azure AD l’authentification unique avec le logiciel de productivité Wizergos, effectuez hello comme suit :**

1. Dans le portail classique hello, sur hello **logiciels de productivité Wizergos** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**boîte de dialogue.
   
    ![Configurer l’authentification unique][6] 
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooWizergos logiciels de productivité** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**:
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_03.png)
3. Sur hello **configurer les paramètres de l’application** page de boîte de dialogue, cliquez sur **suivant**:
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_04.png)
4. Sur hello **configurer l’authentification unique au niveau des logiciels de productivité Wizergos** , cliquez sur **télécharger le certificat**, puis enregistrez le fichier hello sur votre ordinateur :
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_05.png)
5. Dans une fenêtre de navigateur web, client de logiciels de productivité Wizergos tooyour ouverture de session en tant qu’administrateur.
6. Dans le menu de hamburger hello, sélectionnez **Admin**.
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_000.png)
7. Dans le menu de gauche de la page Admin (Administrateur), sélectionnez **AUTHENTICATION** (AUTHENTIFICATION), puis cliquez sur **Azure AD**.
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_002.png)
8. Effectuer hello comme suit **authentification** section.
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_003.png)
  1. Cliquez sur **télécharger** hello tooupload de bouton téléchargé un certificat auprès d’Azure AD. 
  2. Bonjour **URL de l’émetteur** zone de texte placer la valeur hello **URL de l’émetteur** à partir de l’Assistant configuration d’application Azure AD.
  3. Bonjour **URL de connexion unique** zone de texte placer la valeur hello **-Service URL d’authentification** à partir de l’Assistant configuration d’application Azure AD.
  4. Bonjour **URL de déconnexion unique** zone de texte placer la valeur hello **URL de Service de déconnexion unique** à partir de l’Assistant configuration d’application Azure AD.
  5. Cliquez sur le bouton **Enregistrer** .
9. Dans le portail classique hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.
   
    ![Authentification unique Azure AD][10]
10. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.  
    
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail classique de hello appelé Britta Simon.

![Créer un utilisateur Azure AD][20]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_09.png)
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_03.png)
4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_04.png)
5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_05.png) 
  1. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.
  2. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.
  3. Cliquez sur **Suivant**.
6. Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_06.png)
  1. Bonjour **prénom** zone de texte, type **Brian**.  
  2. Bonjour **nom** zone de texte, type, **Simon**.
  3. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.
  4. Bonjour **rôle** liste, sélectionnez **utilisateur**.
  5. Cliquez sur **Suivant**.
7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_07.png)
8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/create_aaduser_08.png)
  1. Notez la valeur hello hello **nouveau mot de passe**.
  2. Cliquez sur **Terminé**.   

### <a name="create-a-wizergos-productivity-software-test-user"></a>Créer un utilisateur de test Wizergos Productivity Software
Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Wizergos Productivity Software. Collaborez avec l’équipe de support des logiciels de productivité Wizergos via [ support@wizergos.com ](emailTo:support@wizergos.com) tooadd les utilisateurs de hello dans la plateforme de logiciels de productivité Wizergos hello.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD
objectif Hello de cette section est tooenabling Britta Simon toouse Azure SSO en accordant son tooWizergos accès aux logiciels de productivité.

  ![Affecter des utilisateurs][200]

**tooassign Britta Simon tooWizergos logiciels de productivité, effectuez hello comme suit :**

1. Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.
   
    ![Affecter des utilisateurs][201]
2. Dans la liste des applications hello, sélectionnez **Wizergos productivité logiciel**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_wizergosproductivitysoftware_50.png)
3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Affecter des utilisateurs][203]
4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.
5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a>Tester l’authentification unique
objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque de logiciels de productivité Wizergos hello Bonjour volet d’accès, vous devez obtenir l’application de logiciels de productivité Wizergos automatiquement signé sur tooyour.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-wizergosproductivitysoftware-tutorial/tutorial_general_205.png
