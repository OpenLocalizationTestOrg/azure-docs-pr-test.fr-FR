---
title: "Didacticiel : intégration d’Azure Active Directory à Splunk Enterprise et Splunk Cloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Splunk Enterprise et Splunk Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: 9bb6817cb31dce684cd9cc1c567fa3efc8906ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a>Didacticiel : Intégration d’Azure Active Directory avec Splunk Enterprise et Splunk Cloud

Dans ce didacticiel, vous apprendrez comment toointegrate Splunk entreprise et Splunk Cloud avec Azure Active Directory (Azure AD).

Intégration Splunk Enterprise et Splunk Cloud à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSplunk Enterprise et Splunk Cloud
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSplunk Enterprise et Splunk Cloud-session unique (SSO) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Splunk Enterprise et Splunk Cloud, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Splunk Enterprise ou Splunk Cloud avec l’authentification unique activée


>[!NOTE]
>tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.
>

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Splunk Enterprise et Splunk Cloud à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD


## <a name="add-splunk-enterprise-and-splunk-cloud-from-hello-gallery"></a>Ajouter des Splunk Enterprise et Splunk Cloud à partir de la galerie de hello
tooconfigure hello intégration d’entreprise de Splunk et Splunk Cloud dans Azure AD, vous devez tooadd Splunk Enterprise Splunk Cloud de liste de tooyour hello galerie des applications et gérées SaaS.

**tooadd Splunk entreprise et Splunk Cloud à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.

    ![Active Directory][1]

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.

    ![Applications][2]

4. Cliquez sur **ajouter** bas hello de page de hello.

    ![Applications][3]

5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.

    ![Applications][4]

6. Dans la zone de recherche de hello, tapez **Splunk Enterprise ou Splunk Cloud**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. Dans le volet de résultats hello, sélectionnez **Splunk Enterprise et Splunk Cloud**, puis cliquez sur **Complete** application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Splunk Enterprise et Splunk Cloud, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur hello équivalent Splunk Enterprise et Splunk Cloud est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Splunk Enterprise et Splunk Cloud doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** Splunk Enterprise et Splunk Cloud.

tooconfigure et test Azure AD l’authentification unique avec Splunk Enterprise et Splunk Cloud, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD l’authentification unique sur](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Splunk Enterprise et Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  -toohave de Britta Simon dans Splunk entreprise et Splunk Cloud qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez l’authentification unique de Azure AD dans le portail classique de hello et configurez l’authentification unique dans votre application d’entreprise de Splunk et Splunk Cloud.


**tooconfigure Azure AD l’authentification unique avec Splunk Enterprise et Splunk nuage, effectuez hello comme suit :**

1. Dans le portail classique hello, sur hello **Splunk Enterprise et Splunk Cloud** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur** boîte de dialogue.
     
    ![Configurer l’authentification unique][6] 

2. Sur hello **Comment voulez-vous que toosign les utilisateurs sur tooSplunk Enterprise et Splunk Cloud** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. Sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. Bonjour **URL de connexion** zone de texte, tapez l’URL hello utilisée par vos utilisateurs sur toosign tooyour Splunk entreprise et votre application Splunk Cloud à l’aide de hello modèle :`https://<splunkserverUrl>/en-US/app/launcher/home`
  2. Bonjour **identificateur** zone de texte, tapez l’URL de votre serveur Splunk hello.
  3. Bonjour **URL de réponse** zone de texte, tapez l’URL hello avec hello modèle :`https://<splunkserver>/saml/acs`
  4. Cliquez sur **Suivant**.
 
4. Sur hello **configurer l’authentification unique à Splunk Enterprise et Splunk Cloud** page, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. Cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello sur votre ordinateur.
  2. Cliquez sur **Suivant**.

5. tooget SSO configuré pour votre application, contactez Splunk entreprise et l’équipe de support Splunk Cloud et par qui suit hello :

    * Hello téléchargé **federaton métadonnées**
6. Dans le portail classique hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**.
    
    ![Authentification unique Azure AD][10]

7. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.  
 
    ![Authentification unique Azure AD][11]

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
Dans cette section, vous créez un utilisateur de test dans le portail classique de hello appelé Britta Simon.

![Créer un utilisateur Azure AD][20]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.
  2. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.
  3. Cliquez sur **Suivant**.

6.  Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :
  
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. Bonjour **prénom** zone de texte, type **Brian**.  
  2. Bonjour **nom** zone de texte, type, **Simon**.
  3. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.
  4. Bonjour **rôle** liste, sélectionnez **utilisateur**.
  5. Cliquez sur **Suivant**.

7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. Notez la valeur hello hello **nouveau mot de passe**.
  2. Cliquez sur **Terminé**.   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a>Créer un utilisateur de test Splunk Enterprise et Splunk Cloud

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Splunk Enterprise et Splunk Cloud. Collaborez avec Splunk Enterprise et Splunk Cloud prise en charge team tooadd hello utilisateurs hello Splunk Enterprise et Splunk Cloud platform.


### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez Britta Simon toouse SSOy Azure accorder son accès tooSplunk Enterprise et le Cloud de Splunk.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSplunk Enterprise et Splunk nuage, effectuez hello comme suit :**

1. Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Splunk Enterprise et Splunk Cloud**.

    ![Configurer l’authentification unique](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.

    ![Affecter des utilisateurs][203]

4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.

5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.

    ![Affecter des utilisateurs][205]

### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous testez votre SSOonfiguration d’Active Directory Azure à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello Splunk Enterprise et vignette Splunk Cloud Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Splunk Enterprise et Splunk Cloud une application.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
