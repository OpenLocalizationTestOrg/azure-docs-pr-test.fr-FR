---
title: "Didacticiel : Intégration d’Azure Active Directory à Amazon Web Services (AWS) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Amazon Web Services (AWS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7561c20b-2325-4d97-887f-693aa383c7be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 1b79572ace63f6174ce4fa014c49bf44bd728228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-amazon-web-services-aws"></a>Didacticiel : Intégration d’Azure Active Directory à Amazon Web Services (AWS)

Dans ce didacticiel, vous apprendrez comment toointegrate Amazon Web Services (AWS) avec Azure Active Directory (Azure AD).

Intégration Amazon Web Services (AWS) à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAmazon Web Services (AWS)
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAmazon Web Services (AWS) (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Amazon Web Services (AWS), it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Amazon Web Services (AWS).

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Amazon Web Services (AWS), vous devez hello éléments suivants :

- Un abonnement Azure AD
- Abonnement Amazon Web Services (AWS) avec authentification unique

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’Amazon Web Services (AWS) à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-amazon-web-services-aws-from-hello-gallery"></a>Ajout d’Amazon Web Services (AWS) à partir de la galerie de hello
intégration de hello tooconfigure Amazon Web Services (AWS) dans Azure AD, vous devez tooadd Amazon Web Services (AWS) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Amazon Web Services (AWS) à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[Azure Portal](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Amazon Web Services (AWS)**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_search.png)

5. Dans le volet de résultats hello, sélectionnez **Amazon Web Services (AWS)**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Amazon Web Services (AWS), en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello Amazon Web Services (AWS) est tooa dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello Amazon Web Services (AWS) doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** Amazon Web Services (AWS).

tooconfigure et test Azure AD l’authentification unique avec Amazon Web Services (AWS), vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Amazon Web Services](#creating-an-amazon-web-services-test-user)**  -toohave de Britta Simon dans Amazon Web Services (AWS) qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Amazon Web Services (AWS).

**tooconfigure Azure AD l’authentification unique avec Amazon Web Services (AWS), effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Amazon Web Services (AWS)** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_samlbase.png)

3. Sur hello **Amazon Web Services (AWS) domaine et les URL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_url.png)

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_certificate.png)

5. Hello application logicielle de Amazon Web Services (AWS) attend les assertions SAML hello dans un format spécifique. Veuillez configurer hello suivant des revendications pour cette application. Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application. Hello suivant capture d’écran montre un exemple de cela.

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_attribute.png)

6. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :
    
    | Nom de l'attribut  | Valeur de l’attribut | Espace de noms |
    | --------------- | --------------- | --------------- |
    | RoleSessionName | user.userprincipalname | https://aws.amazon.com/SAML/Attributes |
    | Rôle            | user.assignedroles |  https://aws.amazon.com/SAML/Attributes |
    
    >[!TIP]
    >Vous devez tooconfigure hello configuration de l’utilisateur dans Azure AD toofetch tous les rôles de hello du AWS Console. Reportez-vous hello provisionnement des étapes ci-dessous.

    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_04.png)

    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_attribute_05.png)

    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne. Ajouter la valeur de Namespace hello indiquées ci-dessus.
    
    d. Cliquez sur **OK**.

7. Cliquez sur **enregistrer** bouton Paramètres de hello toosave sur Azure.

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_400.png)

8. Dans une autre fenêtre de navigateur, site d’entreprise authentification tooyour Amazon Web Services (AWS) en tant qu’administrateur.

9. Cliquez sur **Console Home**.
   
    ![Configurer l’authentification unique][11]

10. Cliquez sur **IAM** à partir du service **Security, Identity & Compliance** (Sécurité, identité et conformité).
   
    ![Configurer l’authentification unique][12]

11. Cliquez sur **Identity Providers**, puis sur **Create Provider**.
   
    ![Configurer l’authentification unique][13]

12. Sur hello **configurer un fournisseur de** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Configurer l’authentification unique][14]
 
    a. Pour **Provider Type**, sélectionnez **SAML**.

    b. Bonjour **nom du fournisseur** zone de texte, tapez un nom de fournisseur (par exemple : *WAAD*).

    c. tooupload votre fichier de métadonnées téléchargé, cliquez sur **choisir un fichier**.

    d. Cliquez sur **Next Step**.

13. Sur hello **vérifier les informations de fournisseur** page de boîte de dialogue, cliquez sur **créer**. 
    
    ![Configurer l’authentification unique][15]

14. Cliquez sur **Roles**, puis sur **Create New Role**. 
    
    ![Configurer l’authentification unique][16]

15. Sur hello **définir un nom de rôle** boîte de dialogue, effectuer hello comme suit : 
    
    ![Configurer l’authentification unique][17] 

    a. Bonjour **nom de rôle** zone de texte, tapez un nom de rôle (par exemple : *TestUser*). 

    b. Cliquez sur **Next Step**.

16. Sur hello **sélectionner le Type de rôle** boîte de dialogue, effectuer hello comme suit : 
    
    ![Configurer l’authentification unique][18] 

    a. Sélectionnez **Role For Identity Provider Access**. 

    b. Bonjour **Grant Web Single Sign-On (WebSSO) tooSAML fournisseurs d’accès aux** , cliquez sur **sélectionnez**.

17. Sur hello **établir la confiance** boîte de dialogue, effectuer hello comme suit :  
    
    ![Configurer l’authentification unique][19] 

    a. En tant que fournisseur SAML, sélectionnez fournisseur SAML de hello que vous avez créé précédemment (par exemple : *WAAD*)
  
    b. Cliquez sur **Next Step**.

18. Sur hello **vérifier une approbation de rôle** boîte de dialogue, cliquez sur **étape suivante**.
    
    ![Configurer l’authentification unique][32]

19. Sur hello **attacher une stratégie** boîte de dialogue, cliquez sur **étape suivante**.
    
    ![Configurer l’authentification unique][33]

20. Sur hello **révision** boîte de dialogue, effectuer hello comme suit :
    
    ![Configurer l’authentification unique][34]
 
    a. Cliquez sur **Create Role**.

    b. Créez autant de rôles en fonction des besoins et les mapper toohello fournisseur d’identité.

21. Maintenant configurer hello l’approvisionnement d’utilisateurs toofetch tous les rôles de hello du AWS

    a. Dans la connexion à la Console de AWS hello avec votre compte racine

    b. Dans hello coin supérieur droit sur votre nom, puis sur hello **mes informations d’identification de sécurité** option. Un écran contenant un message d’avertissement s’affiche. Cliquez sur le bouton de hello **informations d’identification de sécurité** bouton toopass hello écran.
        
       ![Configurer l’authentification unique][36]

       ![Configurer l’authentification unique][37]

    c. Bonjour clés d’accès de section, cliquez sur hello **créer de nouvelle clé d’accès** bouton. Cette opération génère hello ID clé d’accès et une valeur de jeton.
    
       ![Configurer l’authentification unique][38]

    d. Copiez ces deux valeurs et téléchargez-les, pour ne pas les perdre.

    e. Bonjour portail Azure, sur la page d’intégration d’application hello Amazon Web Services (AWS), cliquez sur **Provisioning**.
        
       ![Configurer l’authentification unique][35]

    f. Définir le mode d’approvisionnement hello trop**automatique**
        
       ![Configurer l’authentification unique][39]

    g. En hello **clientsecret** et **Secret jeton** collez les valeurs correspondantes hello, qui vous avez copié à partir de la Console de AWS.
    
    h. Vous pouvez cliquer sur hello **tester la connexion** bouton connectivité de hello tootest. Une fois qu’il réussit vous pouvez démarrer hello mise en service du connecteur.
       
       ![Configurer l’authentification unique][40]

    i. À présent activer hello état d’approvisionnement trop**sur**. Cela démarre l’extraction des rôles de hello à partir de l’application hello.

       ![Configurer l’authentification unique][41]

    > [!NOTE]
    > Service de configuration d’Active Directory Azure s’exécute chaque après certains rôles de hello toosync temps de AWS. Vous devez voir hello tout fournisseur d’identité relié les rôles AWS dans Azure AD et vous pouvez les utiliser lors de l’affectation hello application toousers ou des groupes.

<!--### Next steps

tooensure users can sign-in tooAmazon Web Services (AWS) after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Amazon Web Services (AWS) prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooAmazon Web Services (AWS) in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Amazon Web Services (AWS) users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-amazon-web-service-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-amazon-web-services-test-user"></a>Création d’un utilisateur de test pour Amazon Web Services

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooAmazon Web Services (AWS), vous devez les configurer dans Amazon Web Services (AWS). Dans les cas de hello Amazon Web Services (AWS), cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **Amazon Web Services (AWS)** site d’entreprise en tant qu’administrateur.

2. Cliquez sur hello **accueil de la Console** icône. 
   
    ![Configurer l’authentification unique][11]

3. Cliquez sur Identity and Access Management. 
   
    ![Configurer l’authentification unique][28]

4. Bonjour du tableau de bord, cliquez sur **utilisateurs**, puis cliquez sur **créer de nouveaux utilisateurs**. 
   
    ![Configurer l’authentification unique][29]

5. Dans la boîte de dialogue Créer un utilisateur hello, procédez hello comme suit : 
   
    ![Configurer l’authentification unique][30]   
    
    a. Bonjour **Entrez les noms d’utilisateur** zones de texte, tapez le nom d’utilisateur Brita Simon (userprincipalname) dans Azure AD.

    b. Cliquez sur **Create** (Créer).
        
### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooAmazon accès Web Services (AWS).

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooAmazon Web Services (AWS), effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Amazon Web Services (AWS)**.

    ![Configurer l’authentification unique](./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Sur **sélectionner un rôle** onglet, le rôle approprié de hello select pour l’utilisateur de hello. Tous ces rôles sont affichées avec le nom de rôle hello et le nom de fournisseur d’identité. Ainsi, vous pouvez facilement identifier les rôles AWS hello.

8. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello Amazon Web Services (AWS) vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application d’Amazon Web Services (AWS). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_203.png
[11]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795031.png
[12]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795032.png
[13]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795033.png
[14]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795034.png
[15]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795035.png
[16]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795022.png
[17]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795023.png
[18]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795024.png
[19]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795025.png
[20]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950351.png
[21]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_80.png
[22]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950352.png
[23]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_81.png
[24]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950353.png
[25]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_general_15.png

[28]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950321.png
[29]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795037.png
[30]: ./media/active-directory-saas-amazon-web-service-tutorial/ic795038.png
[32]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950251.png
[33]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950252.png
[34]: ./media/active-directory-saas-amazon-web-service-tutorial/ic7950253.png
[35]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning.png
[36]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials.png
[37]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_securitycredentials_continue.png
[38]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_createnewaccesskey.png
[39]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_automatic.png
[40]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_testconnection.png
[41]: ./media/active-directory-saas-amazon-web-service-tutorial/tutorial_amazonwebservices_provisioning_on.png
