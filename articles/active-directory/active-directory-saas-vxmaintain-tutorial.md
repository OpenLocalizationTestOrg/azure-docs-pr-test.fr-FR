---
title: "Didacticiel : Intégrer Azure Active Directory dans vxMaintain | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et vxMaintain."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 841a1066-593c-4603-9abe-f48496d73d10
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 937ea276d898986fc5a953c96fddabdc8940309f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-vxmaintain"></a>Didacticiel : Intégrer Azure Active Directory dans vxMaintain

Dans ce didacticiel, vous apprendrez comment vxMaintain toointegrate avec Azure Active Directory (Azure AD).

Cette intégration offre plusieurs avantages importants. Vous pouvez :

- Contrôle dans Azure AD qui a accès toovxMaintain.
- Activer vos informations d’identification tooautomatically utilisateurs toovxMaintain avec l’authentification unique (SSO) à l’aide de leurs comptes Azure AD.
- Gérer vos comptes dans un emplacement central : hello portail Azure.

toolearn en savoir plus sur l’intégration de l’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec vxMaintain, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement vxMaintain dans lequel l’authentification unique (SSO) est incluse

> [!NOTE]
> Lorsque vous testez les étapes hello dans ce didacticiel, nous vous recommandons de ne pas utiliser un environnement de production.

étapes de hello tootest dans ce didacticiel, suivez ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. 

scénario Hello décrivant ce didacticiel se compose de deux blocs de construction principaux :

* Ajout de vxMaintain à partir de la galerie de hello
* Configuration et test de l’authentification unique Azure AD

## <a name="add-vxmaintain-from-hello-gallery"></a>Ajouter des vxMaintain à partir de la galerie de hello
intégration de hello tooconfigure de vxMaintain avec Azure AD, vous devez vxMaintain tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

vxMaintain tooadd à partir de la galerie hello, procédez comme hello suivant :

1. Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, dans Sélectionnez hello **Azure Active Directory** bouton. 

    ![bouton d’Azure Active Directory Hello][1]

2. Sélectionnez **Applications d’entreprise** > **Toutes les applications**.

    ![volet de « Applications d’entreprise » Hello][2]
    
3. tooadd une application, Bonjour **toutes les applications** boîte de dialogue, sélectionnez **nouvelle application**.

    ![Hello « Nouvelle application » bouton][3]

4. Dans la zone de recherche de hello, tapez **vxMaintain**.

    ![liste déroulante de « Seul Mode d’authentification » Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_search.png)

5. Dans la liste des résultats hello, sélectionnez **vxMaintain**, puis sélectionnez **ajouter**.

    ![lien de vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec vxMaintain au moyen d’un utilisateur de test appelé « Britta Simon ».

Pour l’authentification unique toowork, Azure AD doit utilisateur d’Azure AD toohello tooknow hello vxMaintain équivalent. Autrement dit, vous devez établir une relation de lien entre hello correspondant vxMaintain utilisateur et Azure AD hello.

relation de lien de hello tooestablish, affecter hello vxMaintain **nom d’utilisateur** valeur comme hello Azure AD **nom d’utilisateur** valeur.

tooconfigure et test de l’authentification unique de Azure AD à l’aide de vxMaintain, hello terminée après les blocs de construction.

### <a name="configure-azure-ad-sso"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous pouvez les activer l’authentification unique de Azure AD Bonjour portail Azure et configurer l’authentification unique dans votre application vxMaintain de manière hello suivante :

1. Bonjour portail Azure, sur hello **vxMaintain** page d’intégration d’application, sélectionnez **l’authentification unique**.

    ![Hello « Sur l’authentification unique » de commande][4]

2. tooenable SSO, Bonjour **Mode d’authentification unique** la liste déroulante, sélectionnez **SAML-authentification**.
 
    ![Hello commande « SAML-authentification »](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_samlbase.png)

3. Sous **vxMaintain domaine et les URL**, hello suivant :

    ![Hello vxMaintain section URL et de domaine](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_url.png)

    a. Bonjour **identificateur** zone, tapez une URL qui a hello selon la syntaxe :`https://<company name>.verisae.com`

    b. Bonjour **URL de réponse** zone, tapez une URL qui a hello selon la syntaxe :`https://<company name>.verisae.com/DataNett/action/ssoConsume/mobile?_log=true`

    > [!NOTE] 
    > Hello les valeurs précédentes ne sont pas réelles. Mettre à jour avec l’identificateur de réel hello et URL de réponse. les valeurs hello tooobtain, contact hello [équipe de support vxMaintain](http://www.verisae.com/contact-us).
 
4. Sous **le certificat de signature SAML**, sélectionnez **Metadata XML**, puis enregistrez ordinateur de tooyour de fichier de métadonnées hello.

    ![Hello section « Certificat de signature SAML »](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_certificate.png) 

5. Sélectionnez **Enregistrer**.

    ![bouton Enregistrer de Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_400.png)

6. tooconfigure **vxMaintain** SSO, hello envoi téléchargé **Metadata XML** toohello de fichiers [équipe de support vxMaintain](http://www.verisae.com/contact-us).

> [!TIP]
> Lorsque vous définissez application hello, vous pouvez lire une version concise de hello précédant les instructions dans hello [portail Azure](https://portal.azure.com). Après avoir ajouté l’application hello de hello **Active Directory** > **des Applications d’entreprise** section, sélectionnez hello **Single Sign-On** onglet, puis hello d’accès incorporé documentation hello **Configuration** section. 
>
>toolearn en savoir plus sur la fonctionnalité de documentation embedded hello, consultez [la gestion de l’authentification unique pour les applications d’entreprise](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
Dans cette section, vous créez utilisateur test Britta Simon Bonjour portail Azure en procédant comme suit de hello :

![utilisateur de test Hello Azure AD][100]

1. Bonjour **portail Azure**hello du volet gauche, dans Sélectionnez hello **Azure Active Directory** bouton.

    ![bouton de « Azure Active Directory » Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_01.png) 

2. toodisplay une liste des utilisateurs, accédez trop**utilisateurs et groupes** > **tous les utilisateurs**.
    
    ![lien Hello « Tous les utilisateurs »](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_02.png)  
    Hello **tous les utilisateurs** boîte de dialogue s’ouvre. 

3. tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter**.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_03.png) 

4. Bonjour **utilisateur** boîte de dialogue zone, hello suivant :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-vxmaintain-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur de test Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis sur valeur hello Remarque qui a été générée dans hello **mot de passe** boîte.

    d. Sélectionnez **Créer**.
 
### <a name="create-a-vxmaintain-test-user"></a>Créer un utilisateur de test vxMaintain

Dans cette section, vous allez créer un utilisateur de test appelé Britta Simon dans vxMaintain. utilisateurs tooadd dans la plate-forme vxMaintain hello, travailler avec les [équipe de support vxMaintain](http://www.verisae.com/contact-us). Avant d’utiliser l’authentification unique, créer et activer les utilisateurs de hello.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez l’utilisateur de test Britta Simon toouse Azure SSO en accordant l’accès toovxMaintain. Par conséquent, toodo hello suivant :

![Utilisateur de test dans la liste nom complet de hello][200] 

1. Bonjour Azure portal **Applications** afficher, accédez trop**active** vue > **des applications d’entreprise** > **detouteslesapplications**.

    ![lient Hello « Toutes les applications »][201] 

2. Bonjour **Applications** liste, sélectionnez **vxMaintain**.

    ![lien de vxMaintain Hello](./media/active-directory-saas-vxmaintain-tutorial/tutorial_vxmaintain_app.png) 

3. Dans le volet gauche de hello, sélectionnez **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Sélectionnez **ajouter** , puis, dans hello **ajouter l’affectation** volet, sélectionnez **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][203]

5. Bonjour **utilisateurs et groupes** la boîte de dialogue hello **utilisateurs** liste, sélectionnez **Britta Simon**, puis sélectionnez hello **sélectionnez** bouton.

7. Bonjour **ajouter l’affectation** boîte de dialogue, sélectionnez **affecter**.
    
### <a name="test-your-azure-ad-single-sign-on"></a>Tester votre authentification unique Azure AD

Dans cette section, vous testez votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

En sélectionnant hello **vxMaintain** vignette dans le volet d’accès de hello doit connecter tooyour vxMaintain application automatiquement.

Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="next-steps"></a>Étapes suivantes

* [Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-vxmaintain-tutorial/tutorial_general_203.png

