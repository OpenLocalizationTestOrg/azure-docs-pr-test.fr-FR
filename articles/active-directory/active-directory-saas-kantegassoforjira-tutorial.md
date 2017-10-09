---
title: "Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour JIRA | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Kantega SSO pour JIRA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2af4891-e3c8-43b3-bdcb-0500c493e9b4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 67894cc55ef91d0991c62e0e4f1be712723cb474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-jira"></a>Didacticiel : Intégration d’Azure Active Directory avec Kantega SSO pour JIRA

Dans ce didacticiel, vous apprendrez comment toointegrate Kantega SSO pour JIRA avec Azure Active Directory (Azure AD).

Intégration Kantega SSO pour JIRA à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooKantega SSO pour JIRA
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKantega SSO pour JIRA (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Kantega SSO pour JIRA, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Kantega SSO pour JIRA pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Kantega SSO pour JIRA à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-kantega-sso-for-jira-from-hello-gallery"></a>Ajout de Kantega SSO pour JIRA à partir de la galerie de hello
intégration de hello tooconfigure de Kantega SSO pour JIRA dans Azure AD, vous devez tooadd Kantega SSO pour JIRA à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Kantega SSO pour JIRA à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Kantega SSO pour JIRA**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_search.png)

5. Dans le volet de résultats hello, sélectionnez **Kantega SSO pour JIRA**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kantega SSO pour JIRA sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Kantega SSO pour JIRA est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Kantega SSO pour JIRA doit toobe établie.

Dans Kantega SSO pour JIRA, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Kantega SSO pour JIRA, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un Kantega SSO pour tester un utilisateur JIRA](#creating-a-kantega-sso-for-jira-test-user)**  -toohave un équivalent de Britta Simon dans Kantega SSO pour JIRA est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre Kantega SSO pour les applications JIRA.

**tooconfigure Azure AD l’authentification unique avec Kantega SSO pour JIRA, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Kantega SSO pour JIRA** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_samlbase.png)

3. Dans **IDP** initiée par le mode, hello **Kantega SSO pour JIRA domaine et les URL** section effectuer hello suivant l’étape :

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url1.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

4. Dans **SP** mode initié, cocher **afficher les paramètres d’URL avancés** et effectuer hello suivant l’étape :

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_url2.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. Ces valeurs sont reçus pendant la configuration hello du plug-in Jira, qui est expliquée plus loin dans le didacticiel de hello.

5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_400.png)
    
7. Dans une fenêtre de navigateur web, connectez-vous tooyour JIRA sur le serveur local en tant qu’administrateur.

8. Pointez sur représentant une roue dentée et cliquez sur hello **modules complémentaires**.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon1.png)

9. Sous l’onglet Modules complémentaires, cliquez sur **Find new add-ons** (Trouver de nouveaux modules complémentaires). Recherche **Kantega SSO pour JIRA (SAML & Kerberos)** et cliquez sur **installer** bouton tooinstall hello nouveau plug-in SAML.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon2.png)

10. installation du plug-in Hello démarre.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon3.png)

11. Une fois l’installation de hello est terminée. Cliquez sur **Fermer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon33.png)

12. Cliquez sur **Gérer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon34.png)
    
13. Le nouveau plug-in est répertorié sous **INTÉGRATIONS**. Cliquez sur **configurer** tooconfigure hello nouveau plug-in.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon35.png)

14. Bonjour **SAML** section. Sélectionnez **Azure Active Directory (Azure AD)** de hello **ajouter le fournisseur d’identité** liste déroulante.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon4.png)

15. Sélectionnez le niveau d’abonnement **De base**.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon5.png)     

16. Sur hello **propriétés de l’application** section, procédez comme suit : 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon6.png)

    a. Hello de copie **URI ID d’application** valeur et l’utiliser en tant que **identificateur, les URL de réponse et les URL de connexion** sur hello **Kantega SSO pour JIRA domaine et les URL** section dans le portail Azure.

    b. Cliquez sur **Suivant**.

17. Sur hello **importation de métadonnées** section, procédez comme suit : 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon7.png)

    a. Sélectionnez **Metadata file on my computer** (Fichier de métadonnées sur mon ordinateur), puis chargez le fichier de métadonnées que vous avez téléchargé à partir du portail Azure.

    b. Cliquez sur **Suivant**.

18. Sur hello **nom et l’authentification unique emplacement** section, procédez comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon8.png)
    
    a. Ajoutez le nom du fournisseur d’identité de hello dans **nom de fournisseur d’identité** zone de texte (par exemple, Azure AD).

    b. Cliquez sur **Suivant**.

19. Vérifier le certificat de signature hello et cliquez sur **suivant**.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon9.png)

20. Sur hello **des comptes d’utilisateur JIRA** section, procédez comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon10.png)

    a. Sélectionnez **créer des utilisateurs dans l’annuaire interne de JIRA si nécessaire** et entrez le nom de hello approprié du groupe de hello pour les utilisateurs (peut être non plusieurs. groupes séparés par des virgules).

    b. Cliquez sur **Suivant**.

21. Cliquez sur **Terminer**.   

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon11.png)

22. Sur hello **connu des domaines pour Azure AD** section, procédez comme suit : 

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/addon12.png)

    a. Sélectionnez **connu domaines** à partir du Panneau de gauche hello de page de hello.

    b. Entrez le nom de domaine Bonjour **connu domaines** zone de texte.

    c. Cliquez sur **Enregistrer**. 

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kantegassoforjira-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-kantega-sso-for-jira-test-user"></a>Création d’un utilisateur de test Kantega SSO pour JIRA

tooenable Azure AD les utilisateurs toolog dans tooJIRA, vous devez les configurer dans JIRA. Dans Kantega SSO pour JIRA, cet approvisionnement est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Ouvrez une session dans tooyour JIRA sur le serveur local en tant qu’administrateur.

2. Pointez sur représentant une roue dentée et cliquez sur hello **gestion des utilisateurs**.

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforjira-tutorial/user1.png) 

3. Sous l’onglet **User management** (Gestion des utilisateurs), cliquez sur **Create user** (Créer un utilisateur).

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforjira-tutorial/user2.png) 

4. Sur hello **« Créer un utilisateur »** boîte de dialogue de page, effectuer hello comme suit :

    ![Ajouter un employé](./media/active-directory-saas-kantegassoforjira-tutorial/user3.png) 

    a. Bonjour **adresse de messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.

    b. Bonjour **nom complet** zone de texte, nom complet du type d’utilisateur hello comme Britta Simon.

    c. Bonjour **nom d’utilisateur** par courrier électronique de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.

    d. Bonjour **mot de passe** zone de texte, un mot de passe hello type d’utilisateur.

    e. Cliquez sur **Create User** (Créer un utilisateur).   

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKantega SSO pour JIRA.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooKantega SSO pour JIRA, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Kantega SSO pour JIRA**.

    ![Configurer l’authentification unique](./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_kantegassoforjira_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello Kantega SSO pour vignette JIRA Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Kantega SSO pour l’application de JIRA.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforjira-tutorial/tutorial_general_203.png
