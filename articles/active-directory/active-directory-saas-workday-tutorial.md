---
title: "Didacticiel : Intégration d’Azure Active Directory à Workday | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de la journée de travail."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a>Didacticiel : Intégration d’Azure Active Directory à Workday

Dans ce didacticiel, vous apprendrez comment toointegrate Workday avec Azure Active Directory (Azure AD).

Intégration de Workday à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooWorkday
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWorkday (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Workday, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Workday pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de journée de travail à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-workday-from-hello-gallery"></a>Ajout de journée de travail à partir de la galerie de hello
tooconfigure hello intégration de Workday dans Azure AD, vous devez tooadd journée de travail à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd journée de travail à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Workday**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. Dans le volet de résultats hello, sélectionnez **Workday**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Workday avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Workday est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Workday doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans la journée de travail.

tooconfigure et test Azure AD l’authentification unique avec une journée de travail, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Workday](#creating-a-workday-test-user)**  -toohave un équivalent de Britta Simon dans Workday est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de la journée de travail.

**tooconfigure Azure AD single sign-on avec Workday, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Workday** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. Sur hello **domaine de la journée de travail et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    a. Bonjour **URL de connexion** valeur hello de type en tant que zone de texte :`https://impl.workday.com/<tenant>/login-saml2.htmld`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://impl.workday.com/<tenant>/login-saml.htmld`

    > [!NOTE] 
    > Ces valeurs ne sont pas hello réel. Mettre à jour ces valeurs avec l’URL de connexion réel hello et URL de réponse. Votre URL de réponse doit avoir un sous-domaine (par exemple, www, wd2, wd3, wd3-impl, wd5, wd5-impl). Quelque chose comme « *http://www.myworkday.com* » fonctionnera, mais pas « *http://myworkday.com* ». Contact [équipe de support Workday Client](https://www.workday.com/en-us/partners-services/services/support.html) tooget ces valeurs. 
 

4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. Sur hello **Workday Configuration** , cliquez sur **configurer de Workday** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS>
7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Workday tooyour en tant qu’administrateur.

8. Accédez trop**Menu \> banc d’essai**.
   
    ![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")

9. Accédez trop**compte Administration**.
   
    ![Compte d’administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Compte d’administration")

10. Accédez trop**Edit Tenant Setup – Security**.
   
    ![Modifier la sécurité du locataire](./media/active-directory-saas-workday-tutorial/IC782925.png "Modifier la sécurité du locataire")

11. Bonjour **URL de Redirection** section, effectuer hello comme suit :
   
    ![URL de redirection](./media/active-directory-saas-workday-tutorial/IC7829581.png "URL de redirection")
   
    a. Cliquez sur le **signe plus**pour ajouter une ligne.
   
    b. Bonjour **URL de redirection de connexion** zone de texte et hello **URL de redirection Mobile** hello de type zone de texte **URL de connexion** vous avez entré sur hello **Workday domaine et URL** section Hello portail Azure.
   
    c. Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **URL de déconnexion**, puis collez-la dans hello **URL de redirection de déconnexion** zone de texte.
   
    d.  Dans **environnement** zone de texte, nom d’environnement de type hello.  

    >[!NOTE]
    > Hello valeur d’attribut d’environnement hello est liée toohello valeur URL hello du client :  
    >-Si le nom de domaine hello d’URL de locataire Workday hello commence par impl par exemple : *https://impl.workday.com/\<client\>/login-saml2.htmld*), hello **environnement** attribut doit être défini à tooImplementation.  
    >-Si le nom de domaine hello commence par quelque chose d’autre, vous devez toocontact [équipe de support Workday Client](https://www.workday.com/en-us/partners-services/services/support.html) mise en correspondance hello tooget **environnement** valeur.

12. Bonjour **le programme d’installation SAML** section, effectuer hello comme suit :
   
    ![Configuration de SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Configuration de SAML")
   
    a.  Sélectionnez **Enable SAML Authentication**.
   
    b.  Cliquez sur le **signe plus**pour ajouter une ligne.

13. Dans la section fournisseurs d’identité SAML de hello, procédez hello comme suit :
   
    ![Fournisseurs d’identité SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Fournisseurs d’identité SAML")
   
    a. Dans la zone de texte Nom de fournisseur d’identité hello, tapez un nom de fournisseur (par exemple : *SPInitiatedSSO*).
   
    b. Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **ID d’entité SAML** valeur, puis collez-le dans hello **émetteur** zone de texte.
   
    c. Sélectionnez **Enable Workday Initiated Logout**.
   
    d. Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **URL de déconnexion** valeur, puis collez-le dans hello **URL de demande de déconnexion** zone de texte.

    e. Cliquez sur **Certificat de clé publique du fournisseur d’identité**, puis sur **Créer**. 

    ![Créer](./media/active-directory-saas-workday-tutorial/IC782928.png "créer")

    f. Cliquez sur **Créer la clé publique x509**. 

    ![Créer](./media/active-directory-saas-workday-tutorial/IC782929.png "créer")


14. Bonjour **x509 d’afficher la clé publique** section, effectuer hello comme suit : 
   
    ![Afficher la clé publique x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Afficher la clé publique x509") 
   
    a. Bonjour **nom** zone de texte, tapez un nom pour votre certificat (par exemple : *EPI\_SP*).
   
    b. Bonjour **valide à partir du** zone de texte, hello type valide à partir de la valeur de l’attribut de votre certificat.
   
    c.  Bonjour **valide à** zone de texte, type hello valide tooattribute valeur de votre certificat.
   
    > [!NOTE]
    > Vous pouvez obtenir hello valide à partir de la date et hello toodate valide du certificat de hello téléchargé en double-cliquant dessus.  dates de Hello sont répertoriés sous hello **détails** onglet.
    > 
    >
   
    d.  Ouvrez votre certificat codé en base 64 dans le bloc-notes, puis hello copie contenu de celui-ci.
   
    e.  Bonjour **certificat** zone de texte, collez le contenu hello du Presse-papiers.
   
    f.  Cliquez sur **OK**.

15. Effectuez hello comme suit : 
   
    ![Configuration SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuration SSO")
   
    a.  Activer hello **x509 paire de clés privée**.
   
    b.  Bonjour **Service Provider ID** zone de texte, type **http://www.workday.com**.
   
    c.  Sélectionnez **Enable SP Initiated SAML Authentication**.
   
    d.  Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **SAML Sign-On URL du Service unique** valeur, puis collez-le dans hello **IdP SSO Service URL** zone de texte.
   
    e. Sélectionnez **Ne pas compresser la demande d’authentification initiée par le fournisseur de services**.
   
    f. Comme **Méthode de signature de la demande d’authentification**, sélectionnez **SHA256**. 
   
    ![Méthode de signature de demande la d’authentification](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Méthode de signature de la demande d’authentification") 
   
    g. Cliquez sur **OK**. 
   
    ![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE>

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
>

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-workday-test-user"></a>Création d’un utilisateur de test Workday

tooget un utilisateur de test dans Workday, vous devez toocontact hello [équipe de support Workday Client](https://www.workday.com/en-us/partners-services/services/support.html).
Hello [équipe de support Workday Client](https://www.workday.com/en-us/partners-services/services/support.html) crée un utilisateur de hello pour vous.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWorkday.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooWorkday, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Workday**.

    ![Configurer l’authentification unique](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

