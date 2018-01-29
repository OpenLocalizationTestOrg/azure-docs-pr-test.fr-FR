---
title: "Didacticiel : Intégration d’Azure Active Directory à LINE WORKS | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et LINE WORKS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jeedes
ms.openlocfilehash: b15f5d02a7baff0bc56f2928f73822214c595ab0
ms.sourcegitcommit: 1d423a8954731b0f318240f2fa0262934ff04bd9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/05/2018
---
# <a name="tutorial-azure-active-directory-integration-with-line-works"></a>Didacticiel : Intégration d’Azure Active Directory à LINE WORKS

Dans ce didacticiel, vous allez apprendre à intégrer LINE WORKS à Azure Active Directory (Azure AD).

L’intégration de LINE WORKS à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à LINE WORKS.
- Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à LINE WORKS (via l’authentification unique) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Conditions préalables

Pour configurer l’intégration d’Azure AD à LINE WORKS, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement LINE WORKS pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de LINE WORKS à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-line-works-from-the-gallery"></a>Ajout de LINE WORKS à partir de la galerie
Pour configurer l’intégration de LINE WORKS à Azure AD, vous devez ajouter LINE WORKS à partir de la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter LINE WORKS à partir de la galerie, effectuez les étapes suivantes :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Bouton Azure Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Panneau Applications d’entreprise][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Bouton Nouvelle application][3]

4. Dans la zone de recherche, tapez **LINE WORKS**, sélectionnez **LINE WORKS** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![LINE WORKS dans la liste des résultats](./media/active-directory-saas-lineworks-tutorial/tutorial_lineworks_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LINE WORKS, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur LINE WORKS équivalent dans Azure AD. En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur LINE WORKS associé doit être établie.

Dans LINE WORKS, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec LINE WORKS, vous devez suivre les indications des sections suivantes :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Créer un utilisateur de test LINE WORKS](#create-a-line-works-test-user)** pour avoir un équivalent de Britta Simon dans LINE WORKS lié à la représentation Azure AD associée.
4. **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application LINE WORKS.

**Pour configurer l’authentification unique Azure AD avec LINE WORKS, effectuez les étapes suivantes :**

1. Dans le portail Azure, sur la page d’intégration de l’application **LINE WORKS**, cliquez sur **Authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-lineworks-tutorial/tutorial_lineworks_samlbase.png)

3. Dans la section **Domaine et URL LINE WORKS**, effectuez les étapes suivantes :

    ![Informations d’authentification unique dans Domaine et URL LINE WORKS](./media/active-directory-saas-lineworks-tutorial/tutorial_lineworks_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://auth.worksmobile.com/d/login/{domain}/?userId={ID@domain}`

    b. Dans la zone de texte **Identificateur**, entrez la valeur : `worksmobile.com`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettez à jour cette valeur avec l’URL d’authentification réelle. Contactez [l’équipe de support client LINE WORKS](mailto:dl_ssoinfo@worksmobile.com) pour obtenir cette valeur.

4. Dans la section **Certificat de signature SAML**, cliquez sur **Certificat (brut)**, puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Lien de téléchargement du certificat](./media/active-directory-saas-lineworks-tutorial/tutorial_lineworks_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-lineworks-tutorial/tutorial_general_400.png)

6. Dans la section **Configuration de LINE WORKS**, cliquez sur **Configurer LINE WORKS** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**

    ![Configuration de LINE WORKS](./media/active-directory-saas-lineworks-tutorial/tutorial_lineworks_configure.png) 

7. Pour configurer l’authentification unique côté **LINE WORKS**, vous devez envoyer le **fichier certificat téléchargé, l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à [l’équipe de support LINE WORKS](mailto:dl_ssoinfo@worksmobile.com). Celles-ci configurent ensuite ce paramètre pour que la connexion SSO SAML soit définie correctement des deux côtés.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

   ![Créer un utilisateur de test Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.

    ![Bouton Azure Active Directory](./media/active-directory-saas-lineworks-tutorial/create_aaduser_01.png)

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-lineworks-tutorial/create_aaduser_02.png)

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.

    ![Bouton Ajouter](./media/active-directory-saas-lineworks-tutorial/create_aaduser_03.png)

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-lineworks-tutorial/create_aaduser_04.png)

    a. Dans la zone **Nom**, tapez **BrittaSimon**.

    b. Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.

    c. Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="create-a-line-works-test-user"></a>Création d’un utilisateur de test LINE WORKS

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans LINE WORKS. Contactez [l’équipe de support LINE WORKS](mailto:dl_ssoinfo@worksmobile.com) pour ajouter les utilisateurs sur la plateforme LINE WORKS.

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à LINE WORKS.

![Attribuer le rôle utilisateur][200] 

**Pour affecter Britta Simon à LINE WORKS, effectuez les étapes suivantes :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **LINE WORKS**.

    ![Lien LINE WORKS dans la liste des applications](./media/active-directory-saas-lineworks-tutorial/tutorial_lineworks_app.png)  

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Lien « Utilisateurs et groupes »][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Volet Ajouter une attribution][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Quand vous cliquez sur la vignette LINE WORKS dans le panneau d’accès, vous devriez être connecté automatiquement à votre application LINE WORKS.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lineworks-tutorial/tutorial_general_203.png

