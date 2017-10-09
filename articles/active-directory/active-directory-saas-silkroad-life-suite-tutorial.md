---
title: "Didacticiel : Intégration d’Azure Active Directory à SilkRoad Life Suite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SilkRoad vie Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 3cd92319-7964-41eb-8712-444f5c8b4d15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/10/2017
ms.author: jeedes
ms.openlocfilehash: 07367282ab42b7332f166d64743b4b447aec4935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-silkroad-life-suite"></a>Didacticiel : Intégration d’Azure Active Directory à SilkRoad Life Suite
objectif Hello de ce didacticiel est tooshow vous comment toointegrate Suite de durée de vie SilkRoad avec Azure Active Directory (Azure AD). 

Intégration SilkRoad vie Suite à Azure AD offre hello avantages suivants : 

* Vous pouvez contrôler dans Azure AD qui a accès tooSilkRoad Suite de la durée de vie 
* Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSilkRoad vie Suite-session unique (SSO) avec leurs comptes Azure AD

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
tooconfigure intégration d’Azure AD avec SilkRoad vie Suite, vous devez hello éléments suivants :

* Un abonnement Azure AD
* Un abonnement SilkRoad Life Suite pour lequel l’authentification unique est activée

>[!NOTE]
>tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production. 
> 

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

* Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
* Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Description du scénario
objectif Hello de ce didacticiel est tooenable vous tootest Azure AD SSO dans un environnement de test.

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de SilkRoad vie Suite à partir de la galerie de hello 
2. Configuration et test de l’authentification unique Azure AD

## <a name="add-silkroad-life-suite-from-hello-gallery"></a>Ajouter SilkRoad vie Suite à partir de la galerie de hello
tooconfigure hello intégration de la Suite de durée de vie SilkRoad dans Azure AD, vous devez tooadd SilkRoad vie Suite à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd SilkRoad Suite de durée de vie à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**. 
   
    ![Active Directory][1]

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications][2]

4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Applications][3]

5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Applications][4]

6. Dans la zone de recherche de hello, tapez **SilkRoad vie Suite**.
   
    ![Applications][5]

7. Dans le volet de résultats hello, sélectionnez **SilkRoad vie Suite**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![Applications][50]

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
objectif Hello de cette section est tooshow comment tooconfigure et l’authentification unique d’Azure AD avec SilkRoad vie Suite de tests en fonction d’un utilisateur de test appelé « Britta Simon ».

Pour l’authentification unique toowork, Azure AD doit tooknow quel utilisateur d’équivalent hello utilisateur de tooan SilkRoad vie Suite dans Azure AD est. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la Suite de durée de vie SilkRoad hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans SilkRoad vie Suite.

tooconfigure et test Azure AD l’authentification unique avec SilkRoad vie Suite, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD l’authentification unique sur](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test SilkRoad vie Suite](#creating-a-silkroad-life-suite-test-user)**  -toohave un équivalent de Britta Simon dans la Suite de durée de vie SilkRoad de sa représentation sous forme de toohello lié Azure AD.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD
Hello cette section vise tooenable Azure AD SSO Bonjour portail Azure classic et tooconfigure l’authentification unique dans votre application SilkRoad vie Suite.

**tooconfigure Azure AD l’authentification unique avec SilkRoad vie Suite, procédez hello comme suit :**

1. Site d’entreprise SilkRoad tooyour ouverture de session en tant qu’administrateur. 

  >[!NOTE] 
  > tooobtain accès toohello application Suite d’authentification de la durée de vie SilkRoad pour configurer la fédération avec Microsoft Azure AD, contactez votre prise en charge SilkRoad ou SilkRoad Services.
  > 

2. Accédez trop**fournisseur de services**, puis cliquez sur **détails de la fédération**. 
   
    ![Authentification unique Azure AD][10] 

3. Cliquez sur **télécharger les métadonnées de fédération**, puis enregistrez le fichier de métadonnées hello sur votre ordinateur.
   
    ![Authentification unique Azure AD][11] 

4. Bonjour portail Azure classic sur hello **SilkRoad vie Suite** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**  boîte de dialogue.
   
    ![Configurer l’authentification unique][6] 

5. Sur hello **Comment souhaitez-vous toosign les utilisateurs sur la Suite de la durée de vie de tooSilkRoad** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Authentification unique Azure AD][7] 

6. Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Authentification unique Azure AD][8]   
 1. Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par votre site de Suite de durée de vie de SilkRoad tooyour toosign sur les utilisateurs (par exemple : *https://defcompanytest-test-redcarpet.silkroad-eng.com/Authentication/*).  
 2. Ouvrez hello téléchargé **Silkroad** fichier de métadonnées. 
 3. Recherchez hello **AssertionConsumerService** balise, puis hello de copie **emplacement** attribut.         
   
    ![Authentification unique Azure AD][21] 
 4. Collez la valeur de hello hello **URL de réponse** zone de texte.  
 5. Cliquez sur **Suivant**.

6. Sur hello **configurer l’authentification unique à la Suite de durée de vie SilkRoad** page, effectuer hello comme suit :
   
    ![Authentification unique Azure AD][9]  
 1. Cliquez sur Télécharger le certificat, puis enregistrez le fichier hello sur votre ordinateur.  
 2. Cliquez sur **Suivant**.

7. Dans votre application **SilkRoad**, cliquez sur **Authentication Sources** (Sources d’authentification).
   
    ![Authentification unique Azure AD][12] 

8. Cliquez sur **Add Authentication Source**(Ajouter une source d’authentification). 
   
    ![Authentification unique Azure AD][13] 

9. Bonjour **ajouter une Source de l’authentification** section, effectuer hello comme suit : 
   
    ![Authentification unique Azure AD][14]  
 1. Sous **Option 2 - fichier de métadonnées**, cliquez sur **Parcourir** hello de tooupload téléchargé le fichier de métadonnées.  
 2. Cliquez sur **Create Identity Provider using File Data**.

10. Bonjour **Sources d’authentification** , cliquez sur **modifier**. 
    
     ![Authentification unique Azure AD][15] 

11. Sur hello **modifier la Source de l’authentification** boîte de dialogue, effectuer hello comme suit : 
    
     ![Authentification unique Azure AD][16] 
 1. Pour l’option **Enabled**, sélectionnez **Yes**.   
 2. Bonjour **IdP Description** zone de texte, tapez une description pour votre configuration (par exemple : *Azure AD SSO*).  
 3. Bonjour **IdP nom** zone de texte, tapez un nom de configuration de tooyour spécifique (par exemple : *Azure SP*).  
 4. Cliquez sur **Enregistrer**.

12. Désactivez toutes les autres sources d’authentification. 
    
     ![Authentification unique Azure AD][17]

13. Bonjour portail Azure classic sur hello **Single sign-on confirmation** , cliquez sur **suivant**.  
    
     ![Authentification unique Azure AD][18]

14. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.
    
     ![Authentification unique Azure AD][19]

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.

![Créer un utilisateur Azure AD][20]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_09.png)  

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_03.png) 

4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**. 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_04.png) 

5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit : 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_05.png)  
 1. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.  
 2. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**. 
 3. Cliquez sur **Suivant**.

6. Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit : 
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_06.png)  
 1. Bonjour **prénom** zone de texte, type **Brian**.    
 2. Bonjour **nom** zone de texte, type, **Simon**. 
 3. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**. 
 4. Bonjour **rôle** liste, sélectionnez **utilisateur**.
 5. Cliquez sur **Suivant**.

7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_07.png) 

8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-silkroad-life-suite-tutorial/create_aaduser_08.png)  
 1. Notez la valeur hello hello **nouveau mot de passe**. 
 2. Cliquez sur **Terminé**.   

### <a name="create-a-silkroad-life-suite-test-user"></a>Créer un utilisateur de test SilkRoad Life Suite
objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans SilkRoad vie Suite. Brian doit avoir un ID de l’authentification unique (parfois appelée tooas un *AuthParam*) qui correspond à de Brian **emailaddress** dans Azure AD.

**toocreate un utilisateur appelé Britta Simon SilkRoad vie suite effectuer hello comme suit :**

- Demandez à votre toocreate équipe de support SilkRoad vie Suite à un utilisateur qui a comme **ID de l’authentification unique** hello attribut même valeur que hello **emailaddress** de Britta Simon dans Azure AD.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD
objectif Hello de cette section est tooenable Britta Simon toouse Azure SSO en accordant son tooSilkRoad accès Suite de la durée de vie.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSilkRoad Suite de la durée de vie, effectuez hello comme suit :**

1. Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **SilkRoad vie Suite**.
   
    ![Affecter des utilisateurs][202] 

3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Affecter des utilisateurs][203] 

4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.

5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.
   
    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a>Tester l’authentification unique
objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.  

Lorsque vous cliquez sur mosaïque SilkRoad vie Suite hello hello volet d’accès, vous devez obtenir l’application de Suite de durée de vie de SilkRoad automatiquement signé sur tooyour.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_01.png
[50]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_02.png

[6]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_03.png
[8]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_04.png
[9]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_05.png
[10]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_06.png
[11]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_07.png
[12]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_08.png
[13]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_09.png
[14]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_10.png
[15]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_11.png
[16]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_12.png
[17]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_13.png
[18]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_06.png
[19]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_07.png


[20]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_15.png


[200]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_silkroad_14.png
[203]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-silkroad-life-suite-tutorial/tutorial_general_205.png





