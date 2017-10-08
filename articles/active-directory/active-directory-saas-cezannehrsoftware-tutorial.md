---
title: "Didacticiel : Intégration d’Azure Active Directory avec le logiciel Cezanne HR | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les logiciels Cezanne HR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 3675acd8871d62c2277def8074f7aa39ac46e2a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a>Didacticiel : Intégration d’Azure Active Directory avec le logiciel Cezanne HR

Dans ce didacticiel, vous apprendrez comment toointegrate logiciel Cezanne HR avec Azure Active Directory (Azure AD).

Intégration du logiciel de Cezanne HR avec Azure AD fournit hello avantages suivants. Vous pouvez :

- Dans Azure AD qui a accès tooCezanne HR logiciel contrôle.
- Activer vos informations d’identification tooautomatically utilisateurs logiciel tooCezanne HR avec session unique (SSO) avec leurs comptes Azure AD.
- Gérer vos comptes dans un emplacement central : hello portail Azure.

toolearn savoir plus sur le logiciel en tant qu’une intégration d’application de service (SaaS) avec Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Cezanne HR logiciel, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement au logiciel Cezanne HR pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello étapes décrites dans ce didacticiel, nous vous recommandons de ne pas utiliser un environnement de production.

étapes de hello tootest dans ce didacticiel, suivez ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. 

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

* Ajout d’un logiciel de Cezanne HR à partir de la galerie de hello
* Configuration et test de l’authentification unique Azure AD

## <a name="add-cezanne-hr-software-from-hello-gallery"></a>Ajouter le logiciel de Cezanne HR à partir de la galerie de hello
intégration de hello tooconfigure du logiciel de Cezanne HR dans Azure AD, ajoutez le logiciel de Cezanne HR à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

tooadd Cezanne HR des logiciels à partir de la galerie hello, procédez comme hello suivant :

1. Bonjour  **[portail Azure](https://portal.azure.com)**hello du volet gauche, dans Sélectionnez hello **Azure Active Directory** bouton. 

    ![bouton de « Azure Active Directory » Hello][1]

2. Sélectionnez **Applications d’entreprise** > **Toutes les applications**.

    ![lient Hello « Toutes les applications »][2]
    
3. tooadd une nouvelle application, en haut de hello Hello **toutes les applications** boîte de dialogue, sélectionnez **nouvelle application**.

    ![Hello « Nouvelle application » bouton][3]

4. Dans la zone de recherche de hello, tapez **Cezanne HR logiciel**.

    ![zone de recherche Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. Dans la liste des résultats hello, sélectionnez **Cezanne HR logiciel** , puis sélectionnez hello **ajouter** bouton application hello de tooadd.

    ![liste des résultats Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec le logiciel Cezanne HR, avec un utilisateur de test appelé « Britta Simon ».

Pour l’authentification unique toowork, Azure AD doit tooknow hello Cezanne HR équivalent toohello Azure AD utilisateur. En d’autres termes, vous devez établir une relation de lien entre un utilisateur Azure AD et un utilisateur hello Bonjour Cezanne HR logiciel.

relation de lien de hello tooestablish, affecter hello Cezanne HR logiciel **nom d’utilisateur** valeur comme hello Azure AD **nom d’utilisateur** valeur.

tooconfigure et test de l’authentification unique de Azure AD à l’aide de logiciels Cezanne HR, hello terminée après les blocs de construction.

### <a name="configure-azure-ad-sso"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous pouvez activer l’authentification unique de Azure AD Bonjour portail Azure et configurer l’authentification unique dans votre application Cezanne HR de manière hello suivante :

1. Bonjour portail Azure, sur hello **Cezanne HR logiciel** page d’intégration d’application, sélectionnez **l’authentification unique**.

    ![Hello « Sur l’authentification unique » de commande][4]

2. tooenable SSO, Bonjour **l’authentification unique** boîte de dialogue, sélectionnez hello **Mode** en tant que **SAML-authentification**.
 
    ![zone de « Mode » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. Sous **Cezanne HR logiciel domaine et les URL**, hello suivant :

    ![Hello « Cezanne HR logiciel et les URL de domaines » section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    a. Bonjour **URL de connexion** zone, tapez une URL qui a hello selon la syntaxe :`https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`

    b. Bonjour **URL de réponse** zone, tapez une URL qui a hello selon la syntaxe :`https://w3.cezanneondemand.com:443/<tenantid>`    
     
    > [!NOTE] 
    > Hello les valeurs précédentes ne sont pas réelles. Mettre à jour les URL de réponse réelle hello et URL de connexion hello. les valeurs hello tooobtain, contact hello [équipe du support client Cezanne HR logiciel](mailto:info@cezannehr.com).

4. Sous **le certificat de signature SAML**, sélectionnez **certificat (Base64)**, puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Hello section « Certificat de signature SAML »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. Sélectionnez **Enregistrer**.

    ![bouton « Enregistrer » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. Sous **Cezanne HR logiciel Configuration**, sélectionnez **configurer le logiciel HR Cezanne** tooopen hello **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML** et **SAML Single Sign-On Service** URL à partir de hello **aide-mémoire** section.

    ![Hello section « Configuration de logiciels Cezanne HR »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. Dans une fenêtre de navigateur web, connectez-vous sur le client de logiciel tooyour Cezanne HR en tant qu’administrateur.

8. Dans le volet gauche de hello, sélectionnez **le programme d’installation du système**. Sélectionnez **Paramètres de sécurité** > **Configuration d’authentification unique**.

    ![lien de « Seule Configuration d’authentification » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. Bonjour **autoriser toolog les utilisateurs à l’aide de hello suivant les services Single Sign-On (SSO)** volet, sélectionnez hello **SAML 2.0** case à cocher et sélectionnez hello **Configuration avancée** option.

    ![Options des services d’authentification unique](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. Sélectionnez **Ajouter**.

    ![bouton « Nouveau » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. Sous **fournisseurs d’identité SAML 2.0**, hello suivant :

    ![Hello section « Fournisseurs d’identité SAML 2.0 »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    a. Bonjour **nom d’affichage** , entrez le nom hello de votre fournisseur d’identité.

    b. Bonjour **identificateur d’entité** zone, collez hello **ID d’entité SAML** que vous avez copié à partir de hello portail Azure. 

    c. Bonjour **SAML liaison** zone de liste, sélectionnez **POST**.

    d. Bonjour **point de terminaison Service de jeton de sécurité** zone, collez hello **SAML Single Sign-On Service** URL que vous avez copié à partir de hello portail Azure. 
    
    e. Bonjour **nom de l’attribut ID utilisateur** , entrez `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.
    
    f. hello de tooupload téléchargé le certificat à partir d’Azure AD, sélectionnez hello **télécharger** bouton.
    
    g. Sélectionnez **OK**. 

12. Sélectionnez **Enregistrer**.

    ![bouton « Enregistrer » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> Lorsque vous définissez application hello, vous pouvez lire une version concise de hello précédant les instructions dans hello [portail Azure](https://portal.azure.com). Après avoir ajouté l’application hello de hello **Active Directory** > **des applications d’entreprise** section, sélectionnez hello **l’authentification unique** onglet. Hello d’accès incorporée documentation hello **Configuration** section. 

toolearn en savoir plus sur la fonctionnalité de documentation embedded hello, consultez [AD Azure incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
Dans cette section, vous créez utilisateur test Britta Simon Bonjour portail Azure.

![utilisateur de test Hello Britta Simon][100]

toocreate un utilisateur test dans Azure AD, procédez comme hello suivant :

1. Bonjour **portail Azure**hello du volet gauche, dans Sélectionnez hello **Azure Active Directory** bouton.

    ![bouton de « Azure Active Directory » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay d’utilisateurs, sélectionnez **utilisateurs et groupes** > **tous les utilisateurs**.
    
    ![lien Hello « Tous les utilisateurs »](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    Hello **tous les utilisateurs** boîte de dialogue s’ouvre.

3. tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter**.
 
    ![bouton « Ajouter » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. Bonjour **utilisateur** boîte de dialogue zone, hello suivant :
 
    ![boîte de dialogue Hello « Utilisateur »](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone utilisateur Britta Simon **adresse de messagerie**.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis sur valeur hello Remarque qui a été générée dans hello **mot de passe** boîte.

    d. Sélectionnez **Créer**.
 
### <a name="create-a-cezanne-hr-software-test-user"></a>Créer un utilisateur de test pour le logiciel Cezanne HR

tooenable Azure AD les utilisateurs toosign dans tooCezanne HR logiciel, vous devez les configurer dans Cezanne HR logiciel. Dans les cas de hello du logiciel de Cezanne HR, cette configuration est une tâche manuelle.

Configurer un compte d’utilisateur de manière hello suivante :

1.  Se connecter tooyour site d’entreprise Cezanne HR software en tant qu’administrateur.

2.  Dans le volet gauche de hello, sélectionnez **le programme d’installation de système** > **gérer les utilisateurs** > **ajouter un nouvel utilisateur**.

    ![lien de « Ajouter un nouvel utilisateur » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "nouvel utilisateur")

3.  Sous **détails de la personne**, hello suivant :

    ![Hello section « Détails de la personne »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "nouvel utilisateur")
    
    a. Paramétrez **Utilisateur interne** sur **Désactivé**.
    
    b. Bonjour **prénom** zone, l’utilisateur de type hello prénom, par exemple, **Brian**.  
 
    c. Bonjour **nom** boîte, de type hello nom de l’utilisateur, par exemple, **Simon**.
    
    d. Bonjour **messagerie** , tapez Bonjour son adresse électronique, par exemple, Brittasimon@contoso.com.

4.  Sous **les informations de compte**, hello suivant :

    ![Hello section « Informations de compte »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "nouvel utilisateur")
    
    a. Bonjour **nom d’utilisateur** , tapez Bonjour son adresse électronique, par exemple, Brittasimon@contoso.com.
    
    b. Bonjour **mot de passe** , tapez le mot de passe de l’utilisateur hello.
    
    c. Bonjour **rôle de sécurité** boîte, sélectionnez **HR Professionnel**.
    
    d. Sélectionnez **OK**.

5. Sur hello **l’authentification unique** onglet hello **SAML 2.0 identificateurs** section, sélectionnez **nouveau**.

    ![bouton « Nouveau » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "utilisateur")

6. Bonjour **fournisseur d’identité** zone de liste, sélectionnez votre fournisseur d’identité. Bonjour **identificateur de l’utilisateur** , entrez l’adresse de messagerie hello pour le compte de test utilisateur Britta Simon.

    ![Hello zones « Fournisseur d’identité » et « Identificateur d’utilisateur »](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "utilisateur")
    
7. Sélectionnez **Enregistrer**.

    ![bouton « Enregistrer » de Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "utilisateur")

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez l’utilisateur de test Britta Simon toouse Azure SSO en accordant l’accès tooCezanne HR logiciel.

![Accès de l’utilisateur de test][200] 

1. Bonjour portail Azure, ouvrez la vue des applications hello et passez toohello vue d’annuaire. Sélectionnez **Applications d’entreprise** > **Toutes les applications**.

    ![lient Hello « Toutes les applications »][201] 

2. Dans la liste des applications hello, sélectionnez **Cezanne HR logiciel**.

    ![liste des « Applications » Hello](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. Dans le menu hello hello gauche, sélectionnez **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Sélectionnez **Ajouter**. Ensuite, dans hello **ajouter l’affectation** boîte de dialogue, sélectionnez **utilisateurs et groupes**.

    ![Lien Utilisateurs et groupes][203]

5. Bonjour **utilisateurs et groupes** la boîte de dialogue hello **utilisateurs** liste, sélectionnez **Britta Simon**.

6. Bonjour **utilisateurs et groupes** boîte de dialogue, sélectionnez **sélectionnez**.

7. Bonjour **ajouter l’affectation** boîte de dialogue, sélectionnez **affecter**.
    
### <a name="test-sso"></a>Tester l’authentification unique (SSO)

Dans cette section, vous testez votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous sélectionnez la vignette de logiciel Cezanne HR hello Bonjour volet d’accès, vous vous connectez sur automatiquement tooyour application logicielle de Cezanne HR.

## <a name="next-steps"></a>Étapes suivantes

* [Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

