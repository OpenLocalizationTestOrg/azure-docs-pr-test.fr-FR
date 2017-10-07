---
title: "Didacticiel : Intégration d’Azure Active Directory à Help Scout | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Scout d’aide."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 58edd140eb1eb5980796ca743b5f7acd891729a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a>Didacticiel : Intégration d’Azure Active Directory à Help Scout

Dans ce didacticiel, vous découvrez comment toointegrate aider conseiller avec Azure Active Directory (Azure AD).

Vous obtenez hello avantages suivants à partir de l’intégration Scout d’aider à Azure AD :

- Dans Azure AD, vous pouvez contrôler qui a accès tooHelp Scout.
- Vous pouvez signer automatiquement dans votre tooHelp utilisateurs Scout à l’aide de l’authentification unique et un compte d’utilisateur Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central, hello portail Azure.

toolearn savoir plus sur le logiciel en tant qu’une intégration d’application de service (SaaS) avec Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooset d’intégration d’Azure AD avec Scout d’aide, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Help Scout, avec authentification unique activée 

> [!NOTE]
> Si vous testez les étapes hello dans ce didacticiel, nous vous recommandons de ne pas les tester dans un environnement de production.

Recommandations pour le test des étapes de hello dans ce didacticiel :

- N’utilisez pas votre environnement de production, à moins que cela ne soit nécessaire.
- Si vous ne disposez pas d’un environnement d’essai Azure AD, vous pouvez [obtenir un essai gratuit d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. 

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajouter Scout d’aide à partir de la galerie de hello.
2. Configurez et testez l’authentification unique Azure AD.

## <a name="add-help-scout-from-hello-gallery"></a>Ajouter Scout d’aide à partir de la galerie de hello
tooset intégration hello d’aider les Scout avec Azure AD, dans la galerie hello, ajoutez la liste de tooyour de Scout d’aide des applications SaaS gérées.

tooadd Scout d’aide à partir de la galerie de hello :

1. Bonjour [portail Azure](https://portal.azure.com)hello du menu de gauche, dans Sélectionnez **Azure Active Directory**. 

    ![bouton d’Azure Active Directory Hello][1]

2. Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.

    ![page des applications Enterprise Hello][2]
    
3. tooadd une nouvelle application, sélectionnez **nouvelle application**.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, entrez **Scout d’aide**. Dans les résultats de recherche de hello, sélectionnez **Scout d’aide**, puis sélectionnez **ajouter**.

    ![Aide Scout dans la liste des résultats hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Help Scout pour un utilisateur de test nommé *Britta Simon*.

Pour toowork de l’authentification unique, Azure AD doit utilisateur tooknow hello Azure AD équivalent Scout d’aide. Une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’aide de Scout hello doit être établie.

relation, dans l’aide Scout, de liens tooestablish hello pour **nom d’utilisateur**, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD.

tooconfigure et test Azure AD l’authentification unique avec aide Scout, hello complète tâches suivantes :

1. [Configurer l’authentification unique Azure AD](#set-up-azure-ad-single-sign-on). Définit un toouse utilisateur cette fonctionnalité.
2. [Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user). Tests AD Azure authentification unique avec l’utilisateur hello Britta Simon.
3. [Créer un utilisateur de test Help Scout](#create-a-help-scout-test-user). Crée un équivalent de Britta Simon Scout aide qui est lié toohello la représentation sous forme de Azure AD de l’utilisateur de hello.
4. [Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user). Définit les toouse Britta Simon Azure AD l’authentification unique.
5. [Tester l’authentification unique](#test-single-sign-on). Vérifie que la configuration hello fonctionne.

### <a name="set-up-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous configurer Azure AD l’authentification unique sur Bonjour portail Azure. Ensuite, vous configurerez l’authentification unique dans votre application Help Scout.

tooset d’Azure AD single sign-on avec Scout d’aide :

1. Bonjour portail Azure, sur hello **Scout d’aide** page d’intégration d’application, sélectionnez **l’authentification unique**.
 
    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** page, pour **Mode**, sélectionnez **SAML-authentification**.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. Sous **URL et aider à un domaine Scout**, si vous souhaitez tooset des application hello en mode initié par IDP, hello complète comme suit :

    1. Bonjour **identificateur** , entrez une URL qui pointe hello modèle :`urn:auth0:helpscout:<instancename>`

    2. Bonjour **URL de réponse** , entrez une URL qui pointe hello modèle :`https://helpscout.auth0.com/login/callback?connection=<instancename>`

    ![Informations d’authentification unique dans Domaine et URL Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. Si vous souhaitez tooset des application hello en mode initié par le Service Pack, sélectionnez hello **afficher les paramètres d’URL avancés** case à cocher, puis hello suivant :

    * Bonjour **URL de connexion** , entrez une URL qui pointe hello suivant le format :`https://secure.helpscout.net/members/login/`

    ![Informations d’authentification unique dans Domaine et URL Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > les valeurs Hello dans ces URL sont fins de démonstration uniquement. Mettre à jour les valeurs hello avec hello identificateur réel URL et l’URL de réponse. Ces valeurs, contactez le tooget [équipe de support Scout d’aide](mailto:help@helpscout.com). 

5. Sous **le certificat de signature SAML**, sélectionnez **Metadata XML**, puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. Sélectionnez **Enregistrer**.

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. tooset des unique authentification côté de hello Scout d’aide, envoyez hello téléchargé métadonnées XML fichier toohello [équipe de support Scout d’aide](mailto:help@helpscout.com). équipe de support Hello Scout d’aide applique ce paramètre afin que hello SAML session connexion unique est correctement des deux côtés.

> [!TIP]
> Vous pouvez lire une version concise de ces instructions Bonjour [portail Azure](https://portal.azure.com), alors que vous configurez votre application ! Après avoir ajouté l’application hello en sélectionnant **Active Directory** > **des Applications d’entreprise**, sélectionnez hello **Single Sign-On** onglet. Vous pouvez accéder à documentation hello incorporé Bonjour **Configuration** section, au bas de hello de page de hello. Pour plus d’informations, consultez la page [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

Dans cette section, Bonjour portail Azure, vous créez un utilisateur de test nommé Britta Simon.

![Créer un utilisateur de test Azure AD][100]

toocreate un utilisateur test dans Azure AD :

1. Bonjour portail Azure, dans le menu de gauche hello, sélectionnez **Azure Active Directory**.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay d’utilisateurs, sélectionnez **utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**.

    ![Sélectionnez Utilisateurs et groupes, puis Tous les utilisateurs.](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, en haut de hello Hello **tous les utilisateurs** page, sélectionnez **ajouter**.

    ![bouton Ajouter de Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, hello complète comme suit :

    1. Bonjour **nom** , entrez **BrittaSimon**.

    2. Bonjour **nom d’utilisateur** , entrez l’adresse de messagerie hello d’utilisateur Britta Simon.

    3. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    4. Sélectionnez **Créer**.

        ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a>Créer un utilisateur de test Help Scout

objet Hello de cette section est toocreate un utilisateur nommé Britta Simon dans Scout d’aide. Help Scout prend en charge l’approvisionnement juste-à-temps (JIT), activé par défaut.

Dans cette section, il n’existe aucun toocomplete action ou une tâche. Si un utilisateur n’existe pas déjà dans l’aide de Scout, un nouveau est créé lorsque vous essayez de tooaccess Scout d’aide.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous permettre à l’utilisateur hello Britta Simon toouse Azure AD l’authentification unique en accordant hello utilisateur compte accès tooHelp Scout.

![Attribuer le rôle d’utilisateur hello][200] 

tooassign Britta Simon tooHelp Scout :

1. Bonjour portail Azure, ouvrez la vue des applications hello et passez toohello vue d’annuaire. Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Scout d’aide**.

    ![lien d’aide les Scout Hello dans la liste des Applications hello](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. Dans le menu de gauche hello, sélectionnez **utilisateurs et groupes**.

    ![Hello les utilisateurs et groupes lien][202]

4. Sélectionnez **Ajouter**. Ensuite, sous hello **ajouter l’affectation** page, sélectionnez **utilisateurs et groupes**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur hello **utilisateurs et groupes** page, dans la liste de hello des utilisateurs, sélectionnez **Britta Simon**.

6. Sur hello **utilisateurs et groupes** page, sélectionnez **sélectionnez**.

7. Sur hello **ajouter l’affectation** page, sélectionnez **affecter**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide du volet d’accès hello.

Lorsque vous sélectionnez la vignette d’aider les Scout hello hello panneau d’accès, vous devez être connecté automatiquement dans tooyour application de Scout d’aide.

Pour plus d’informations sur le volet d’accès, consultez [volet d’accès toohello Introduction](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

