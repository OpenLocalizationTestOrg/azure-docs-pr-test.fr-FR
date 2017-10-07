---
title: "Didacticiel : intégration d’Azure Active Directory à iLMS | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et iLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: da0936de23afcd5a4213aa6f699165f9bfa82c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Didacticiel : Intégration d’Azure Active Directory à iLMS

Dans ce didacticiel, vous apprendrez comment iLMS toointegrate avec Azure Active Directory (Azure AD).

Intégration iLMS à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooiLMS
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooiLMS (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec iLMS, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement iLMS pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’iLMS à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-ilms-from-hello-gallery"></a>Ajout d’iLMS à partir de la galerie de hello
intégration de hello tooconfigure d’iLMS dans Azure AD, vous devez iLMS tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**iLMS tooadd à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **iLMS**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_search.png)

5. Dans le volet de résultats hello, sélectionnez **iLMS**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec iLMS avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans iLMS est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans iLMS doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans iLMS.

tooconfigure et test Azure AD l’authentification unique avec iLMS, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test iLMS](#creating-an-ilms-test-user)**  -toohave un homologue de Britta Simon dans iLMS qui est de sa représentation sous forme de toohello lié Azure AD.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application iLMS.

**tooconfigure Azure AD single sign-on avec iLMS, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **iLMS** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_samlbase.png)

3. Sur hello **iLMS domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url.png)

    a. Bonjour **identificateur** zone de texte, collez hello **identificateur** vous copiez à partir de valeur **fournisseur de services** section des paramètres SAML dans le portail d’administration iLMS.

    b. Bonjour **URL de réponse** zone de texte, collez hello **(URL) du point de terminaison** vous copiez à partir de valeur **fournisseur de services** section des paramètres SAML dans le portail d’administration iLMS ayant des éléments suivants de hello modèle`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`

    >[!Note]
    >« 123456 » est un exemple de valeur d’identificateur.

4. Vérifiez **afficher les paramètres d’URL avancés**, si vous le souhaitez application hello tooconfigure **SP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_url1.png)

    Bonjour **URL de connexion** zone de texte, collez hello **(URL) du point de terminaison** vous copiez à partir de valeur **fournisseur de services** section des paramètres SAML dans le portail d’administration iLMS en tant que`https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`     

5. tooenable JIT approvisionnement, iLMS application attend les assertions SAML hello dans un format spécifique. Configurer hello suivant des revendications pour cette application. Vous pouvez gérer les valeurs de ces attributs hello depuis hello **attributs utilisateur** section sur la page d’intégration d’application. Hello suivant capture d’écran montre un exemple de cela.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/4.png)
    
    Créer **département, région** et **Division** les attributs et ajouter le nom hello de ces attributs dans iLMS. Tous les attributs présentés ci-dessus sont requis.    

    > [!NOTE] 
    > Vous avez tooenable **créer un compte d’utilisateur Un-recognized** dans iLMS toomap ces attributs. Suivez les instructions de hello [ici](http://support.inspiredelearning.com/customer/portal/articles/2204526) tooget une idée sur la configuration des attributs hello.

6. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :
    
    | Nom de l'attribut | Valeur de l’attribut |
    | ---------------| --------------- |    
    | division | user.department |
    | region | user.state |
    | department | user.jobtitle |

    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_05.png)
    
    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.
    
    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.
    
    d. Cliquez sur **OK**.

7. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_certificate.png) 

8. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-iLMS-tutorial/tutorial_general_400.png)

9. Dans une fenêtre de navigateur web, connectez-vous tooyour **portail d’administration iLMS** en tant qu’administrateur.

10. Cliquez sur **SSO:SAML** sous **paramètres** tooopen SAML paramètres et effectuer hello comme suit :
    
    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/1.png) 

    a. Développez hello **fournisseur de services** section et copie hello **identificateur** et **(URL) du point de terminaison** valeur.

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/2.png) 

    b. Sous la section **Fournisseur d’identité**, cliquez sur **importer les métadonnées**.
    
    c. Sélectionnez hello **métadonnées** fichier téléchargé à partir du portail Azure à partir de **le certificat de signature SAML** section.

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Si vous souhaitez tooenable JIT configuration toocreate iLMS de comptes pour annuler-reconnaître les utilisateurs, procédez comme suit :
        
       - Cochez **Créer un compte utilisateur non reconnu**.
       
       ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Mapper les attributs de hello dans Azure AD avec des attributs hello dans iLMS. Dans la colonne d’attribut hello, spécifiez hello attributs nom ou hello par défaut.

    e. Accédez trop**les règles d’entreprise** onglet et effectuer hello comme suit : 
        
       ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/5.png)

       - Vérifiez **créer des régions Un-recognized, Divisions et services** toocreate régions, Divisions et des services qui n’existent pas déjà au moment de hello de l’authentification unique.
        
       - Vérifiez **mise à jour les profils utilisateur pendant connectez-vous** toospecify si hello profil utilisateur est mise à jour à chaque ouverture de session unique. 
        
       - Si hello **« Mise à jour vide valeurs pour Non champs de profil utilisateur obligatoire »** option est activée, les champs facultatifs qui sont vides lors de la connexion dans seront également provoquent hello iLMS profil utilisateur toocontain des valeurs vides pour ces champs.
        
       - Vérifiez **envoyer un E-mail de Notification d’erreur** et entrez le courriel hello d’utilisateur de hello tooreceive hello erreur notification par courrier électronique.

11. Cliquez sur **enregistrer** bouton Paramètres de hello toosave.

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/save.png)

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ilms-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-ilms-test-user"></a>Création d’un utilisateur de test iLMS

Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello. JIT fonctionnera, si vous avez cliqué sur hello **créer un compte d’utilisateur Un-recognized** case à cocher au cours du paramètre de configuration de SAML au portail d’administration iLMS.

Si vous avez besoin de toocreate un utilisateur manuellement, puis procédez comme suit :

1. Ouvrez une session dans le site d’entreprise tooyour iLMS en tant qu’administrateur.

2. Cliquez sur **« Inscrire un utilisateur »** sous **utilisateurs** onglet tooopen **inscrire un utilisateur** page. 
   
   ![Ajouter un employé](./media/active-directory-saas-ilms-tutorial/3.png)

3. Sur hello **« Inscrire un utilisateur »** page, effectuer hello comme suit.

    ![Ajouter un employé](./media/active-directory-saas-ilms-tutorial/create_testuser_add.png)

    a. Bonjour **prénom** prénom de type hello Brian zone de texte.
   
    b. Bonjour **nom** zone de texte, hello de type nom Simon.

    c. Bonjour **ID de courrier électronique** zone de texte, tapez Bonjour adresse de messagerie du compte de Britta Simon.

    d. Bonjour **région** liste déroulante, la valeur hello select pour la région.

    e. Bonjour **Division** liste déroulante, la valeur hello select de division.

    f. Bonjour **service** liste déroulante, la valeur hello select pour le service.

    g. Cliquez sur **Enregistrer**.

    > [!NOTE] 
    > Vous pouvez envoyer toouser de messagerie de l’inscription en sélectionnant **envoyer un message d’inscription** case à cocher.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooiLMS de son accès.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooiLMS, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **iLMS**.

    ![Configurer l’authentification unique](./media/active-directory-saas-ilms-tutorial/tutorial_ilms_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello iLMS vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour iLMS application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ilms-tutorial/tutorial_general_203.png

