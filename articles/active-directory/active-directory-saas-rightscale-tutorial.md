---
title: "Didacticiel : Intégration d’Azure Active Directory avec RightScale | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et RightScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 222c4414a9f736a3589b4cdd0ed934696f6c31ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a>Didacticiel : Intégration d’Azure Active Directory avec RightScale

Dans ce didacticiel, vous allez apprendre à intégrer RightScale avec Azure Active Directory (Azure AD).

L’intégration de RightScale avec Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à RightScale.
- Vous pouvez autoriser les utilisateurs à se connecter automatiquement à RightScale (par le biais de l’authentification unique) avec leur compte Azure AD.
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Conditions préalables

Pour configurer l’intégration d’Azure AD avec RightScale, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement RightScale pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout de RightScale à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-rightscale-from-the-gallery"></a>Ajout de RightScale à partir de la galerie
Pour configurer l’intégration de RightScale à Azure AD, vous devez ajouter RightScale à partir de la galerie à votre liste d’applications SaaS managées.

**Pour ajouter RightScale à partir de la galerie, procédez comme suit :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, tapez **RightScale**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. Dans le volet de résultats, sélectionnez **RightScale**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RightScale sur un utilisateur de test nommé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur RightScale équivalent à l’utilisateur dans Azure AD. En d’autres termes, une relation entre l’utilisateur Azure AD et l’utilisateur RightScale associé doit être établie.

Dans RightScale, affectez la valeur du **nom d’utilisateur** dans Azure AD comme valeur du **Username** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec RightScale, vous devez suivre les indications des sections suivantes :

1. **[Configuration de l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur de test RightScale](#creating-a-rightscale-test-user)** pour avoir un équivalent de Britta Simon dans RightScale lié à la représentation Azure AD associée.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application RightScale.

**Pour configurer l’authentification unique Azure AD avec RightScale, procédez comme suit :**

1. Dans le portail Azure, dans la page d’intégration de l’application **RightScale**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. Dans la section **Domaine et URL RightScale**, si vous souhaitez configurer l’application en **mode initialisé IDP** vous n’avez rien à faire, car l’application est déjà pré-intégrée avec Azure.

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. Dans la section **Domaine et URL RightScale**, si vous souhaitez configurer l’application en **mode initié SP**, procédez comme suit :
    
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    a. Cliquez sur l’option **Afficher les paramètres d’URL avancés**.

    b. Dans la zone de texte **URL d’authentification**, saisissez l’URL : `https://login.rightscale.com/`.

5. Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. Dans la section **Configuration de RightScale**, cliquez sur **Configurer RightScale** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez l’**ID d’entité SAML et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS>
8. Pour que l’authentification unique soit configurée pour votre application, vous devez vous connecter à votre locataire RightScale en tant qu’administrateur.

    a. Dans le menu situé en haut, cliquez sur l’onglet **Paramètres** et sélectionnez **Authentification unique**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    b. Cliquez sur le bouton « **nouveau** » pour ajouter **vos fournisseurs d’identité SAML**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    c. Dans la zone de texte **Nom d'affichage**, entrez le nom de votre société.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    d. Sélectionnez **Allow RightScale-initiated SSO using a discovery hint** et entrez votre **nom de domaine** dans la zone de texte située dessous.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    e. Collez la valeur de l’**URL du service d’authentification unique SAML** que vous avez copiée sur le portail Azure vers **SAML SSO Endpoint** dans RightScale.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    f. Collez la valeur de l’**ID d’entité SAML** que vous avez copiée sur le portail Azure vers **SAML EntityID** dans RightScale.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    g. Cliquez sur le bouton **Explorateur** pour charger le certificat que vous avez téléchargé à partir du portail Azure.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    h. Cliquez sur **Save**.
<CE>
> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-rightscale-test-user"></a>Création d’un utilisateur de test RightScale

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans RightScale. Collaborez avec l’[équipe de support technique RightScale](mailto:support@rightscale.com) pour ajouter les utilisateurs dans la plateforme RightScale.

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à RightScale.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à RightScale, procédez comme suit :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **RightScale**.

    ![Configurer l’authentification unique](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.  

Quand vous cliquez sur la mosaïque RightScale dans le volet d’accès, vous devez être connecté automatiquement à votre application RightScale.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

