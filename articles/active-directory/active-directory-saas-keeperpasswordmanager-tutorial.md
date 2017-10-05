---
title: "Didacticiel : Intégration d’Azure Active Directory à Keeper Password Manager & Digital Vault | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et Keeper Password Manager & Digital Vault."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1a98f6a-2dae-4734-bdbf-4fba742a61d2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 36504a281756b980e3348e7f892ba08821873b52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-keeper-password-manager--digital-vault"></a>Didacticiel : Intégration d’Azure Active Directory à Keeper Password Manager & Digital Vault

Dans ce didacticiel, vous allez apprendre à intégrer Keeper Password Manager & Digital Vault à Azure Active Directory (Azure AD).

L’intégration de Keeper Password Manager & Digital Vault à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à Keeper Password Manager & Digital Vault.
- Vous pouvez autoriser les utilisateurs à se connecter automatiquement à Keeper Password Manager & Digital Vault (via l’authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

Pour configurer l’intégration d’Azure AD à Keeper Password Manager & Digital Vault, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement Keeper Password Manager & Digital Vault pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de Keeper Password Manager & Digital Vault à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-keeper-password-manager--digital-vault-from-the-gallery"></a>Ajout de Keeper Password Manager & Digital Vault à partir de la galerie
Pour configurer l’intégration de Keeper Password Manager & Digital Vault à Azure AD, vous devez ajouter Keeper Password Manager & Digital Vault à partir de la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter Keeper Password Manager & Digital Vault à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, tapez **Keeper Password Manager & Digital Vault**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_search.png)

5. Dans le volet de résultats, sélectionnez **Keeper Password Manager & Digital Vault**, puis cliquez sur **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur Keeper Password Manager & Digital Vault équivalent dans Azure AD. En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur Keeper Password Manager & Digital Vault associé doit être établie.

Dans Keeper Password Manager & Digital Vault, assignez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault, vous devez suivre les indications des sections suivantes :

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur de test Keeper Password Manager & Digital Vault](#creating-a-keeperpasswordmanager-test-user)** : pour avoir un équivalent de Britta Simon dans Keeper Password Manager & Digital Vault lié à la représentation Azure AD associée.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application Keeper Password Manager & Digital Vault.

**Pour configurer l’authentification unique Azure AD avec Keeper Password Manager & Digital Vault, procédez comme suit :**

1. Dans le portail Azure, sur la page d’intégration de l’application **Keeper Password Manager & Digital Vault**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_samlbase.png)

3. Dans la section **Domaine et URL Keeper Password Manager & Digital Vault**, procédez comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://{SSO CONNECT SERVER}/sso-connect/saml/login`

    b. Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://{SSO CONNECT SERVER}/sso-connect/saml/sso`

    c. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://{SSO CONNECT SERVER}/sso-connect`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de réponse et l’URL de connexion réelles. Pour obtenir ces valeurs, contactez [l’équipe de support technique de Keeper Password Manager & Digital Vault](https://keepersecurity.com/contact.html). 

4. Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_400.png)
    
6. Dans la section **Configuration de Keeper Password Manager & Digital Vault**, cliquez sur **Configurer Keeper Password Manager & Digital Vault** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez **l’URL de déconnexion, l’ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_configure.png) 

7. Pour configurer l’authentification unique côté **Keeper Password Manager & Digital Vault**, suivez les instructions fournies dans le [guide de prise en charge de Keeper](https://keepersecurity.com/assets/pdf/SettingupAzurewithKeeperSSOConnect.pdf).

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-keeperpasswordmanager-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-keeper-password-manager--digital-vault-test-user"></a>Création d’un utilisateur de test Keeper Password Manager & Digital Vault

Pour se connecter à Keeper Password Manager & Digital Vault, les utilisateurs d’Azure AD doivent être approvisionnés dans Keeper Password Manager & Digital Vault. L’application prend en charge la configuration d’utilisateur juste-à-temps, et après authentification, les utilisateurs sont créés automatiquement dans l’application. Si vous voulez configurer des utilisateurs manuellement, vous pouvez contacter le [support de Keeper](https://keepersecurity.com/contact.html).

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous autorisez Britta Simon à utiliser l’authentification unique Azure en accordant l’accès à Keeper Password Manager & Digital Vault.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à Keeper Password Manager & Digital Vault, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **Keeper Password Manager & Digital Vault**.

    ![Configurer l’authentification unique](./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_keeper_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Lorsque vous cliquez sur la vignette Keeper Password Manager & Digital Vault dans le volet d’accès, vous devez accéder à la page de connexion de l’application Keeper Password Manager & Digital Vault. Après vous être authentifié, vous devez accéder à l’application. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keeperpasswordmanager-tutorial/tutorial_general_203.png

