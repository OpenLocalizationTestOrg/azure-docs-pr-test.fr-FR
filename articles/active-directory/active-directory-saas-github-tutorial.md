---
title: "Didacticiel : Intégration d’Azure Active Directory à GitHub | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et GitHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4395bd95-05de-4deb-87a5-dc3bc8ac4d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 688779de4e6627e49c0e3e8a7576f2f8c7a81ab1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-github"></a>Didacticiel : Intégration d’Azure Active Directory à GitHub

Dans ce didacticiel, vous apprendrez comment toointegrate GitHub avec Azure Active Directory (Azure AD).

Intégration de GitHub à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooGitHub
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooGitHub (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à GitHub, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement GitHub pour lequel l’authentification unique est activée


> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.


tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de GitHub à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD


## <a name="adding-github-from-hello-gallery"></a>Ajout de GitHub à partir de la galerie de hello
tooconfigure hello intégration de GitHub dans Azure AD, vous devez tooadd GitHub à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd GitHub à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **GitHub.com**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search02.png)

5. Dans le volet de résultats hello, sélectionnez **GitHub**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/tutorial_github_search_result02.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec GitHub, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans GitHub est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans GitHub doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans GitHub.

tooconfigure et test Azure AD l’authentification unique avec GitHub, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test GitHub](#creating-a-GitHub-test-user)**  -toohave de Britta Simon dans GitHub qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application de GitHub.

**tooconfigure Azure AD single sign-on avec GitHub, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **GitHub** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_01.png)

3. Sur hello **GitHub domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_saml011.png)

    a. Bonjour **URL de connexion** valeur hello de type en tant que zone de texte :`https://github.com/orgs/<entity-id>/sso`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://github.com/orgs/<entity-id>`

    > [!NOTE] 
    > Notez qu’il s’agit pas des valeurs réelles hello. Vous avez tooupdate ces valeurs avec hello réel chanter sur URL et l’identificateur. Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur. Accédez à tooGitHub Admin section tooretrieve ces valeurs. 

4. Sur hello **attributs utilisateur** section, sélectionnez **identificateur de l’utilisateur** comme user.mail.

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_attribute_new01.png)
    
5. Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_03.png)

6. Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**. Ensuite, cliquez sur le bouton **Enregistrer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_general_300.png)

7. Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_04.png)

8. Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_general_400.png)

9. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_05.png) 

10. Sur hello **GitHub Configuration** , cliquez sur **configurer GitHub** tooopen **configurer l’authentification** fenêtre.

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_06.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_07.png)

11. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise GitHub en tant qu’administrateur.

12. Accédez trop**paramètres** et cliquez sur **sécurité**

    ![Paramètres](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_03.png)

13. Vérifiez hello **activer l’authentification SAML** zone, révélant hello Single Sign-on configuration les champs. Ensuite, utilisez hello unique authentification URL valeur tooupdate hello unique URL de connexion sur la configuration d’Azure AD.

    ![Paramètres](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_13.png)

14. Configurer hello champs qui suivent :

    a. **URL de connexion**: entrez **SAML SSO Service URL** de hello **configurer GitHub** section sur Azure AD

    b. **Émetteur**: entrez **ID d’entité SAML** de hello **configurer GitHub** section sur Azure AD

    c. **Certificat public**: hello ouvrir téléchargé le certificat à partir d’Azure AD dans un contenu hello bloc-notes, puis copiez notamment « BEGIN CERTIFICATE » et « END CERTIFICATE »

    ![Paramètres](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_051.png)

15. Cliquez sur **configuration SAML du Test** tooconfirm qui aucune des échecs de validation ou des erreurs lors de l’authentification unique.

    ![Paramètres](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_06.png)

16. Cliquez sur **Enregistrer**.

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-github-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**. 


### <a name="creating-a-github-test-user"></a>Création d’un utilisateur de test GitHub

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans GitHub, ils doivent être configurés dans GitHub.  
Dans les cas de hello de GitHub, cette configuration est une tâche manuelle.

**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**

1. Ouvrez une session dans tooyour GitHub site d’entreprise en tant qu’administrateur.

2. Cliquez sur **People**.

    ![Personnes](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_08.png "Personnes")

3. Cliquez sur **Invite member**.

    ![Inviter des utilisateurs](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_09.png "inviter des utilisateurs")

4. Sur hello **invitation membre** boîte de dialogue de page, effectuer hello comme suit :

    a. Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie du compte de Britta Simon.

    ![Inviter des personnes](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_10.png "inviter des personnes")
    
    b. Cliquez sur **Send Invitation**.

    ![Inviter des personnes](./media/active-directory-saas-github-tutorial/tutorial_github_config_github_11.png "inviter des personnes")

    > [!NOTE]
    > titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.


### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooGitHub de son accès.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooGitHub, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **GitHub.com**.

    ![Configurer l’authentification unique](./media/active-directory-saas-github-tutorial/tutorial_github_search_result021.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    


### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque GitHub hello hello volet d’accès, vous devez obtenir tooyour connecté GitHub application. Vous allez être journalisation comme un compte d’organisation mais puis besoin toolog avec votre compte personnel.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-github-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-github-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-github-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-github-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-github-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-github-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-github-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-github-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-github-tutorial/tutorial_general_203.png
