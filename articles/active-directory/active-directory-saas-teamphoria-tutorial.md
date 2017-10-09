---
title: "Didacticiel : intégration d’Azure Active Directory à Teamphoria | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a>Didacticiel : Intégration d’Azure Active Directory à Teamphoria

Dans ce didacticiel, vous apprendrez comment toointegrate Teamphoria avec Azure Active Directory (Azure AD).

Intégration Teamphoria à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooTeamphoria
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTeamphoria (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Teamphoria, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Teamphoria pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Teamphoria à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-teamphoria-from-hello-gallery"></a>Ajout de Teamphoria à partir de la galerie de hello
intégration de hello tooconfigure de Teamphoria dans Azure AD, vous devez tooadd Teamphoria à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Teamphoria à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Teamphoria**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. Dans le volet de résultats hello, sélectionnez **Teamphoria**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Teamphoria avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Teamphoria est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Teamphoria doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Teamphoria.

tooconfigure et test Azure AD l’authentification unique avec Teamphoria, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Teamphoria](#creating-a-teamphoria-test-user)**  -toohave de Britta Simon dans Teamphoria qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application Teamphoria.

**tooconfigure Azure AD single sign-on avec Teamphoria, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **Teamphoria** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. Sur hello **Teamphoria domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez l’URL hello hello suivant le modèle à l’aide de :`https://<sub-domain>.teamphoria.com/login`  

    > [!NOTE] 
    > Notez qu’il s’agit pas des valeurs réelles hello. Vous avez défini ces valeurs avec hello tooupdate URL de connexion réel. Contact [équipe de support Client de Teamphoria](https://www.teamphoria.com/) tooget hello Sign-on URL. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le certificat de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. Sur hello **Teamphoria Configuration** , cliquez sur **Teamphoria de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. tooconfigure l’authentification unique sur **Teamphoria** côté, l’application de Teamphoria tooyour de connexion en tant qu’administrateur.

8. Accédez trop**administrateur paramètres** option dans la barre d’outils de gauche hello et sous hello hello configurer un onglet cliquez sur **l’authentification unique** fenêtre de configuration de l’authentification unique tooopen hello.

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. Cliquez sur **Ajouter nouveau fournisseur d’identité** option sous forme de hello tooopen hello coin supérieur droit pour ajouter des paramètres hello pour l’authentification unique.

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. Entrez les détails de hello dans les champs de hello comme décrit ci-dessous :

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    a. **Le nom complet** : entrez le nom d’affichage de hello du plug-in hello sur la page d’administration hello.

    b. **NOM du bouton** : nom hello d’onglet hello qui s’affiche sur la page de connexion hello pour la connexion via l’authentification unique.

    c. **CERTIFICAT** : hello ouvrir certificat précédemment téléchargés de hello portail Azure dans le bloc-notes, copiez le contenu de hello du hello même et collez-le ici dans la zone de hello.

    d. **POINT d’entrée** : hello de coller **SAML Sign-On URL du Service unique** copiés hello formulaire antérieur portail Azure.

    e. Basculer les option hello trop**ON** , puis cliquez sur **enregistrer**. 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-teamphoria-test-user"></a>Création d’un utilisateur de test Teamphoria

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans Teamphoria, ils doivent être configurés dans Teamphoria. Dans les cas de hello de Teamphoria, cette configuration est une tâche manuelle.

**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**

1. Ouvrez une session dans tooyour Teamphoria site d’entreprise en tant qu’administrateur.

2. Cliquez sur **ADMIN** les paramètres de barre d’outils de gauche hello et sous hello **gérer** onglet cliquez **utilisateurs** page d’administration tooopen hello pour les utilisateurs.

    ![Ajouter un employé](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. Cliquez sur hello **manuel inviter** option.

    ![Inviter des personnes](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. Dans cette page, effectuez l’action suivante. 
    
    ![Inviter des personnes](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    a. Bonjour **adresse de messagerie** zone de texte, hello **adresse de messagerie** de BrittaSimon.

    b. Bonjour **prénom** zone de texte, type **Brian**.

    c. Bonjour **nom** zone de texte, type **Simon**.

    d. Cliquez sur **INVITE 1 USER** (Inviter l’utilisateur 1). L’utilisateur doit tooaccept hello invitation tooget est créé dans le système de hello.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooTeamphoria de son accès.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooTeamphoria, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Teamphoria**.

    ![Configurer l’authentification unique](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès. Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

