---
title: "Didacticiel : Intégration d’Azure Active Directory à AppDynamics | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a>Didacticiel : Intégration d’Azure Active Directory à AppDynamics

Dans ce didacticiel, vous allez apprendre à intégrer AppDynamics à Azure Active Directory (Azure AD).

L’intégration d’AppDynamics à Azure AD vous offre les avantages suivants :

- Dans Azure AD, vous pouvez contrôler qui a accès à AppDynamics
- Vous pouvez autoriser les utilisateurs à se connecter automatiquement à AppDynamics (via l’authentification unique) avec leur compte Azure AD
- Vous pouvez gérer vos comptes à partir d’un emplacement central : le portail Azure

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Prérequis

Pour configurer l’intégration d’Azure AD à AppDynamics, vous avez besoin des éléments suivants :

- Un abonnement Azure AD
- Un abonnement AppDynamics pour lequel l’authentification unique est activée

> [!NOTE]
> Pour tester les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.

Vous devez en outre suivre les recommandations ci-dessous :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. Le scénario décrit dans ce didacticiel se compose des deux sections principales suivantes :

1. Ajout d’AppDynamics à partir de la galerie
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-appdynamics-from-the-gallery"></a>Ajout d’AppDynamics à partir de la galerie
Pour configurer l’intégration d’AppDynamics à Azure AD, vous devez ajouter AppDynamics à partir de la galerie à votre liste d’applications SaaS gérées.

**Pour ajouter AppDynamics à partir de la galerie, effectuez les étapes suivantes :**

1. Dans le volet de navigation gauche du **[portail Azure](https://portal.azure.com)**, cliquez sur l’icône **Azure Active Directory**. 

    ![Active Directory][1]

2. Accédez à **Applications d’entreprise**. Accédez ensuite à **Toutes les applications**.

    ![Applications][2]
    
3. Pour ajouter l’application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche, tapez **AppDynamics**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. Dans le panneau de résultats, sélectionnez **AppDynamics**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec AppDynamics, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur AppDynamics équivalent dans Azure AD. En d’autres termes, une relation entre un utilisateur Azure AD et un utilisateur AppDynamics associé doit être établie.

Dans AppDynamics, affectez la valeur de **nom d’utilisateur** dans Azure AD comme valeur de **nom d’utilisateur** pour établir la relation.

Pour configurer et tester l’authentification unique Azure AD avec AppDynamics, vous devez suivre les indications des sections suivantes :

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** pour permettre à vos utilisateurs d’utiliser cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)** pour tester l’authentification unique Azure AD avec Britta Simon.
3. **[Création d’un utilisateur test AppDynamics](#creating-an-appdynamics-test-user)** pour avoir un équivalent de Britta Simon dans AppDynamics lié à la représentation Azure AD de l’utilisateur.
4. **[Affectation de l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user)** pour permettre à Britta Simon d’utiliser l’authentification unique Azure AD.
5. **[Testing Single Sign-On](#testing-single-sign-on)** pour vérifier si la configuration fonctionne.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application AppDynamics.

**Pour configurer l’authentification unique Azure AD avec AppDynamics, effectuez les étapes suivantes :**

1. Dans le portail Azure, dans la page d’intégration de l’application **AppDynamics**, cliquez sur **Authentification unique**.

    ![Configurer l’authentification unique][4]

2. Dans la boîte de dialogue **Authentification unique**, pour le **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. Dans la section **Domaine et URL AppDynamics**, effectuez les étapes suivantes :

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    a. Dans la zone de texte **URL de connexion**, tapez une URL au format suivant : `https://<companyname>.saas.appdynamics.com`

    b. Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://<companyname>.saas.appdynamics.com/controller`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels. Pour obtenir ces valeurs, contactez l’[équipe de support technique AppDynamics](https://www.appdynamics.com/support/). 
 
4. Dans la section **Certificat de signature SAML**, cliquez sur **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. Dans la section **Configuration de AppDynamics**, cliquez sur **Configurer AppDynamics** pour ouvrir la fenêtre **Configurer l’authentification**. Copiez **l’URL de déconnexion et l’URL du service d’authentification unique SAML** à partir de la **section Référence rapide**.

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise AppDynamics en tant qu’administrateur.

8. Dans la barre d’outils située en haut, cliquez sur **Paramètres**, puis sur **Administration**.
   
    ![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")

9. Cliquez sur l’onglet **Authentication Provider** .
   
    ![Fournisseur d’authentification](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Fournisseur d’authentification")

10. Dans la section **Authentication Provider** , procédez comme suit :
   
    ![Configuration SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Configuration SAML")   

    a. Dans **Fournisseur d’authentification**, sélectionnez **SAML**.

    b. Dans la zone de texte **URL de connexion**, collez la valeur de **URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.

    c. Dans la zone de texte **URL de déconnexion**, collez la valeur de **URL de déconnexion** que vous avez copiée à partir du portail Azure.
       
    d. Ouvrez votre certificat codé en base 64 dans le Bloc-notes, copiez son contenu dans le Presse-papiers, puis collez-le dans la zone de texte **Certificat**.

    e. Cliquez sur **Enregistrer**.

     ![Enregistrer](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "enregistrer")

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.  Après avoir ajouté cette application à partir de la section **Active Directory > Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** en bas. Vous pouvez en savoir plus sur la fonctionnalité de documentation incorporée ici : [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.

![Créer un utilisateur Azure AD][100]

**Pour créer un utilisateur de test dans Azure AD, procédez comme suit :**

1. Dans le panneau de navigation gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. Dans la boîte de dialogue **Utilisateur**, procédez comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    a. Dans la zone de texte **Nom**, entrez **BrittaSimon**.

    b. Dans la zone de texte **Nom d’utilisateur**, tapez **l’adresse e-mail** de Britta Simon.

    c. Sélectionnez **Afficher le mot de passe** et notez la valeur du **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-an-appdynamics-test-user"></a>Création d’un utilisateur de test AppDynamics

Pour permettre aux utilisateurs Azure AD de se connecter à AppDynamics, vous devez les approvisionner dans AppDynamics. En l’occurrence, cet approvisionnement est une tâche manuelle.

**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**

1. Connectez-vous à votre site d’entreprise AppDynamics en tant qu’administrateur.

2. Accédez à **Utilisateurs**, puis cliquez sur **+** pour ouvrir la boîte de dialogue **Créer un utilisateur**.
   
    ![Utilisateurs](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Utilisateurs")

3. Dans la section **Créer un utilisateur** , procédez comme suit :
   
    ![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")
   
    a. Tapez le **nom d’utilisateur**, le **nom**, **l’adresse e-mail**, le **nouveau mot de passe** et la **confirmation du nouveau mot de passe** d’un compte AAD valide que vous souhaitez approvisionner dans les zones de texte correspondantes.

    b. Cliquez sur **Enregistrer**.

    >[!NOTE]
    >Vous pouvez utiliser tout autre outil ou n’importe quelle API de création de compte d’utilisateur fournis par AppDynamics pour approvisionner des comptes d’utilisateur Azure Active Directory.

### <a name="assigning-the-azure-ad-test-user"></a>Affectation de l’utilisateur de test Azure AD

Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à AppDynamics.

![Affecter des utilisateurs][200] 

**Pour affecter Britta Simon à AppDynamics, effectuez les étapes suivantes :**

1. Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, accédez à **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications, sélectionnez **AppDynamics**.

    ![Configurer l’authentification unique](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. Dans le menu de gauche, cliquez sur **Utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Dans la boîte de dialogue **Utilisateurs et groupes**, sélectionnez **Britta Simon** dans la liste des utilisateurs.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.

Quand vous cliquez sur la vignette AppDynamics dans le volet d’accès, vous devez être connecté automatiquement à votre application AppDynamics.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

