---
title: "Didacticiel : Intégration d’Azure Active Directory avec SSO SAML pour Jira par résolution GmbH | Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et SAML SSO pour Jira par résolution GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: a3436a9aa25640e931a61b5ba4a62611e6e07890
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a>Didacticiel : Intégration d’Azure Active Directory avec SSO SAML pour Jira par résolution GmbH

Dans ce didacticiel, vous apprendrez comment toointegrate SAML SSO pour Jira par résolution GmbH avec Azure Active Directory (Azure AD).

Intégration SAML SSO pour Jira par résolution GmbH avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSAML SSO pour Jira par résolution GmbH
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAML SSO pour Jira par résolution GmbH (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec SAML SSO pour Jira par résolution GmbH, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Une authentification unique SSO SAML pour Jira de resolution GmbH sur un abonnement activé

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de SAML SSO pour Jira par résolution GmbH à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-hello-gallery"></a>Ajout de SAML SSO pour Jira par résolution GmbH à partir de la galerie de hello
tooconfigure hello intégration de SAML SSO pour Jira par résolution GmbH dans Azure AD, vous devez tooadd SAML SSO pour Jira par résolution GmbH à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd SAML SSO pour Jira par résolution GmbH à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **SAML SSO pour Jira par résolution GmbH**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. Dans le volet de résultats hello, sélectionnez **SAML SSO pour Jira par résolution GmbH**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SSO SAML pour Jira de resolution GmbH, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SAML SSO pour Jira par résolution GmbH est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un hello utilisateur dans SAML SSO pour Jira par résolution GmbH doit toobe établie.

Dans SAML SSO pour Jira par résolution GmbH, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et tester Azure AD l’authentification unique avec SAML SSO Jira par résolution GmbH, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un SAML SSO pour Jira par l’utilisateur de test de résolution GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)**  -toohave un équivalent de Britta Simon dans SAML SSO pour Jira par résolution GmbH est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre SAML SSO pour Jira par résolution GmbH application.

**tooconfigure Azure AD l’authentification unique avec SAML SSO pour Jira par résolution GmbH, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **SAML SSO pour Jira par résolution GmbH** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. Sur hello **SAML SSO pour Jira par résolution GmbH domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`

4. Cliquez sur **Afficher les paramètres d’URL avancés**. Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/samlsso`
     
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. Contact [équipe de support SAML SSO pour Jira par résolution GmbH Client](https://www.resolution.de/go/support) tooget ces valeurs. 

5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. Dans une fenêtre de navigateur web, connectez-vous tooyour **SAML SSO pour Jira par le portail d’administration résolution GmbH** en tant qu’administrateur.

8. Pointez sur représentant une roue dentée et cliquez sur hello **modules complémentaires**.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. Vous êtes redirigé tooAdministrator la page d’accès. Entrez hello **mot de passe** et cliquez sur **confirmer** bouton.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. Sous l’onglet Modules complémentaires, cliquez sur **Find new add-ons** (Trouver de nouveaux modules complémentaires). Recherche **SAML authentification unique (SSO) pour JIRA** et cliquez sur **installer** bouton tooinstall hello nouveau plug-in SAML.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. installation du plug-in Hello démarre. Cliquez sur **Fermer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. Cliquez sur **Gérer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. Cliquez sur **configurer** tooconfigure hello nouveau plug-in.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. Sur **SAML SingleSignOn plug-in Configuration** , cliquez sur **ajouter le fournisseur d’identité supplémentaires** bouton Paramètres de hello tooconfigure de fournisseur d’identité.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. Sur cette page, procédez comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    a. Ajouter **nom** Hello fournisseur d’identité (par exemple, Azure AD).
    
    b. Ajouter **Description** Hello fournisseur d’identité (par exemple, Azure AD).

    c. Cliquez sur **XML** et sélectionnez hello **métadonnées** fichier, qui vous avez téléchargé à partir du portail Azure.

    d. Cliquez sur le bouton **Charger**.

    e. Il lit les métadonnées de IdP hello et renseigne les champs hello en surbrillance dans la capture d’écran de hello.   

16. Cliquez sur **enregistrer les paramètres** bouton Paramètres de hello toosave.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a>Création d’un utilisateur de test pour SSO SAML pour Jira de resolution GmbH

tooenable Azure AD les utilisateurs toolog dans tooSAML SSO pour Jira par résolution GmbH, ils doivent être configurés dans SAML SSO pour Jira par résolution GmbH.  
Dans SSO SAML pour Jira de resolution GmbH, cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Ouvrez une session dans tooyour SAML SSO pour Jira par le site d’entreprise GmbH résolution en tant qu’administrateur.

2. Pointez sur représentant une roue dentée et cliquez sur hello **gestion des utilisateurs**.

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. Vous êtes redirigé tooAdministrator accès page tooenter **mot de passe** et cliquez sur **confirmer** bouton.

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. Sous l’onglet **User management** (Gestion des utilisateurs), cliquez sur **Create user** (Créer un utilisateur).

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. Sur hello **« Créer un utilisateur »** boîte de dialogue de page, effectuer hello comme suit :

    ![Ajouter un employé](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    a. Bonjour **adresse de messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.

    b. Bonjour **nom complet** zone de texte, nom complet du type d’utilisateur hello comme Britta Simon.

    c. Bonjour **nom d’utilisateur** par courrier électronique de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.

    d. Bonjour **mot de passe** zone de texte, un mot de passe hello type d’utilisateur.

    e. Cliquez sur **Create User** (Créer un utilisateur).   

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAML SSO pour Jira par résolution GmbH.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSAML SSO pour Jira par résolution GmbH, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **SAML SSO pour Jira par résolution GmbH**.

    ![Configurer l’authentification unique](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello SAML SSO pour Jira en mosaïque GmbH résolution hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour SAML SSO pour Jira par résolution GmbH application.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

