---
title: "Didacticiel : Intégration de Azure Active Directory à MobileIron | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et MobileIron."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: 3e4bbd5b-290e-4951-971b-ec0c1c11aaa2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/9/2017
ms.author: jeedes
ms.openlocfilehash: 214cc59b0a0d1cb55758e11f7fa87c8457531113
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobileiron"></a>Didacticiel : Intégration de Azure Active Directory à MobileIron

Dans ce didacticiel, vous allez apprendre à intégrer MobileIron à Azure Active Directory (Azure AD).

L’intégration de MobileIron dans Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à MobileIron.
- Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à MobileIron (par le biais de l’authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

Pour configurer l’intégration de Azure AD à MobileIron, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement MobileIron pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de MobileIron à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-mobileiron-from-the-gallery"></a>Ajout de MobileIron à partir de la galerie
Pour configurer l’intégration de MobileIron à Azure AD, vous devez ajouter MobileIron à partir de la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter MobileIron à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Bouton Azure Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Panneau Applications d’entreprise][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Bouton Nouvelle application][3]

4. Dans la zone de recherche, tapez **MobileIron**, sélectionnez **MobileIron** dans le volet de résultats, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![MobileIron dans la liste des résultats](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec MobileIron avec un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur MobileIron équivalent dans Azure AD. En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur MobileIron associé doit être établie.

Dans MobileIron, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique avec Azure AD avec MobileIron, vous devez compléter les blocs de construction suivants :

1. **[Configurer l’authentification unique Azure AD](#configure-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Créer un utilisateur de test MobileIron](#create-a-mobileiron-test-user)** pour avoir un équivalent de Britta Simon dans MobileIron, lié à la représentation Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test Azure AD](#assign-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Tester l’authentification unique](#test-single-sign-on)** : pour vérifier si la configuration fonctionne.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application MobileIron.

**Pour configurer l’authentification unique Azure AD avec MobileIron, procédez comme suit :**

1. Dans le Portail Azure, sur la page d’intégration de l’application **MobileIron**, cliquez sur **Authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_samlbase.png)

3. Dans la section **Domaines et URL MobileIron**, suivez les étapes ci-dessous si vous souhaitez configurer l’application en mode initié par **IDP**:

    ![Informations d’authentification unique dans Domaine et URL MobileIron](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_url.png)

    a. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://www.mobileiron.com/<key>`

    b. Dans la zone de texte **URL de réponse** , tapez une URL au format suivant : `https://<host>.mobileiron.com/saml/SSO/alias/<key>`

4. Si vous souhaitez configurer l’application en **mode démarré par le fournisseur de service**, cochez **Afficher les paramètres d’URL avancés**, puis effectuez les étapes suivantes :

    ![Authentification unique dans Domaine et URL MobileIron](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_url1.png)

    Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<host>.mobileiron.com/user/login.html`
    
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’identificateur, l’URL de réponse et l’URL de connexion réels. Vous obtiendrez les valeurs de la clé et de l’hôte à partir du portail d’administration de MobileIron, expliqué plus loin dans le didacticiel.

5. Dans la section **Certificat de signature SAML**, cliquez sur **Métadonnées XML** puis enregistrez le fichier de métadonnées sur votre ordinateur.

    ![Lien Téléchargement de certificat](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-mobileiron-tutorial/tutorial_general_400.png)

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise MobileIron en tant qu’administrateur.

8. Accédez à **Admin** > **Identité**.

   * Sélectionnez l’option **AAD** dans le champ **Informations sur la configuration de fournisseur d’identité cloud**.

    ![Bouton Administrateur de la page Configurer l’authentification unique](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_admin.png)

9. Copiez les valeurs de la **clé** et de l’**hôte** et collez-les pour terminer les URL dans la section **Domaine et URL MobileIron** dans le portail Azure.

    ![Bouton Administrateur de la page Configurer l’authentification unique](./media/active-directory-saas-mobileiron-tutorial/key.png)

10. Dans le champ **Exporter le fichier de métadonnées de AAD et l’importer dans MobileIron Cloud**, cliquez sur **Choisir un fichier** pour charger les métadonnées téléchargées à partir du portail Azure. Cliquez sur **Fait** une fois le chargement terminé.
 
    ![Bouton de métadonnées d’administrateur de la page Configurer l’authentification unique](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_adminmetadata.png)

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

   ![Créer un utilisateur de test Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.

    ![Bouton Azure Active Directory](./media/active-directory-saas-mobileiron-tutorial/create_aaduser_01.png)

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.

    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-mobileiron-tutorial/create_aaduser_02.png)

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.

    ![Bouton Ajouter](./media/active-directory-saas-mobileiron-tutorial/create_aaduser_03.png)

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :

    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-mobileiron-tutorial/create_aaduser_04.png)

    a. Dans la zone **Nom**, tapez **BrittaSimon**.

    b. Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.

    c. Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.

    d. Cliquez sur **Créer**.
  
### <a name="create-a-mobileiron-test-user"></a>Créer un utilisateur de test MobileIron

Pour se connecter à MobileIron, les utilisateurs de Azure AD doivent être approvisionnés dans MobileIron.  
Dans le cas de MobileIron, l’approvisionnement est une tâche manuelle.

**Pour approvisionner un compte d’utilisateur, procédez comme suit :**

1. Connectez-vous au site d’entreprise MobileIron en tant qu’administrateur.

2. Accédez à **Utilisateurs**, puis cliquez sur **Ajouter** > **un utilisateur unique**.

    ![Bouton utilisateur de la page Configurer l’authentification unique](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_user.png)

3. Dans la boîte de dialogue **« Utilisateur unique »**, procédez comme suit :

    ![Bouton Ajouter un utilisateur de la page Configurer l’authentification unique](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_useradd.png)

    a. Dans la zone de texte **Adresse e-mail**, saisissez l’adresse e-mail de l’utilisateur, par exemple brittasimon@contoso.com.

    b. Dans la zone de texte **Prénom**, saisissez le prénom de l’utilisateur, par exemple Britta.

    c. Dans la zone de texte **Nom**, saisissez le nom de famille de l’utilisateur, par exemple Simon.
    
    d. Cliquez sur **Done**.  

### <a name="assign-the-azure-ad-test-user"></a>Affecter l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à MobileIron.

![Attribuer le rôle utilisateur][200] 

**Pour affecter Britta Simon à MobileIron, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **MobileIron**.

    ![Lien MobileIron dans la liste des applications](./media/active-directory-saas-mobileiron-tutorial/tutorial_mobileiron_app.png)  

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Lien « Utilisateurs et groupes »][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Volet Ajouter une attribution][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Quand vous cliquez sur la vignette MobileIron dans le volet d’accès, vous devez être connecté automatiquement à votre application MobileIron.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobileiron-tutorial/tutorial_general_203.png

