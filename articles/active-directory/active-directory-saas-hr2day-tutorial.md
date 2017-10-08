---
title: "Didacticiel : Intégration d’Azure Active Directory avec HR2day by Merces | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et HR2day par Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 257233767e1fddbaf115878cb0455acf61b2f5f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a>Didacticiel : Intégration d’Azure Active Directory avec HR2day by Merces

Dans ce didacticiel, vous apprendrez comment toointegrate HR2day par Merces avec Azure Active Directory (Azure AD).

Intégration HR2day par Merces à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a tooHR2day d’accès par Merces.
- Vous pouvez autoriser les utilisateurs tooautomatically obtenir signée tooHR2day de Merces avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central--hello portail Azure.

Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec HR2day par Merces, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement HR2day by Merces pour lequel l’authentification unique est activée

> [!NOTE]
> Nous ne recommandons pas à l’aide d’un Bonjour de tootest environnement production les étapes de ce didacticiel.

étapes de hello tootest dans ce didacticiel, suivez ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Obtenez [un mois d’évaluation gratuite d’Azure AD](https://azure.microsoft.com/pricing/free-trial/) si vous n’y avez pas encore accès.  

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario de Hello est décrite ici se compose de deux blocs de construction principaux :

1. Ajout de HR2day par Merces à partir de la galerie de hello.
2. Configuration et test de l’authentification unique Azure AD

## <a name="add-hr2day-by-merces-from-hello-gallery"></a>Ajouter des HR2day par Merces à partir de la galerie de hello
intégration de hello tooconfigure de HR2day par Merces dans Azure AD, ajouter HR2day par Merces à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd HR2day par Merces à partir de la galerie hello, prenez hello comme suit :**

1. Bonjour [portail Azure](https://portal.azure.com), sur hello du volet de navigation gauche, sélectionnez hello **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd une nouvelle application, sélectionnez hello **nouvelle application** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **HR2day par Merces**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. Dans le volet de résultats hello, sélectionnez **HR2day par Merces**, puis sélectionnez hello **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HR2day by Merces avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow qui est hello équivalent utilisateur dans HR2day par Merces tooa utilisateur dans Azure AD. En d’autres termes, vous devez tooestablish un lien entre un utilisateur Azure AD et un utilisateur hello dans HR2day par Merces.

Dans HR2day par Merces, attribuez hello **nom d’utilisateur** dans Azure AD trop **nom d’utilisateur** relation de hello tooestablish.

tooconfigure et test Azure AD l’authentification unique avec HR2day par Merces, vous devez hello toocomplete suivant des blocs de construction :

1. [Configurer Azure AD l’authentification unique sur](#configuring-azure-ad-single-sign-on): activer votre toouse les utilisateurs de cette fonctionnalité.
2. [Créer un utilisateur de test Azure AD](#creating-an-azure-ad-test-user) : Tester l’authentification unique Azure AD avec Britta Simon.
3. [Créer un HR2day par l’utilisateur de test Merces](#creating-an-hr2day-by-merces-test-user): créer un équivalent de Britta Simon dans HR2day par Merces est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. [Affecter l’utilisateur de test hello Azure AD](#assigning-the-azure-ad-test-user): toouse activer Britta Simon Azure AD l’authentification unique.
5. [Tester l’authentification unique sur](#testing-single-sign-on): vérifier si la configuration de hello fonctionne.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre HR2day par Merces application.

**tooconfigure Azure AD single sign-on avec HR2day par Merces, prenez hello comme suit :**

1. Bonjour portail Azure, sur hello **HR2day par Merces** page d’intégration d’application, sélectionnez **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. tooenable l’authentification unique, Bonjour **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification**.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. Bonjour **HR2day par l’URL et le domaine de Merces** conservez hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    a. Bonjour **URL de connexion** zone, tapez une URL à l’aide de hello modèle : `https://<tenantname>.force.com/<instancename>`.

    b. Bonjour **identificateur** zone, tapez une URL à l’aide de hello modèle : `https://hr2day.force.com/<companyname>`.

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec l’URL de connexion réel hello et identificateur. Contact hello [HR2day par l’équipe de support client Merces](mailto:servicedesk@merces.nl) tooget ces valeurs. 
 


4. Sur hello **le certificat de signature SAML** section, sélectionnez **Certificate(Base64)**, puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. Cette section décrit comment tooenable utilisateurs tooauthenticate tooHR2day par Merces avec leur compte dans Azure AD. Pour cela, ils en utilisant la fédération basée sur hello protocole SAML.

    Votre HR2day par Merces application attend les assertions SAML hello dans un format spécifique, ce qui vous oblige le jeton SAML tooyour tooadd attribut personnalisé mappages. Hello suivant capture d’écran montre un exemple de cela. 

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    Avant de pouvoir configurer assertion SAML de hello, vous devez contacter hello [HR2day par l’équipe de support Client de Merces](mailto:servicedesk@merces.nl) et demander la valeur hello d’attribut d’identificateur unique hello pour votre client. Vous avez besoin de cette procédure de hello toocomplete valeur dans la section suivante de hello. 

6. Bonjour **l’authentification unique** la boîte de dialogue hello **attributs utilisateur** section, configurer des attributs de jeton SAML hello comme indiqué dans hello suivant l’image. Ensuite, extrayez hello comme suit.
    
      | Nom de l’attribut    |   Valeur de l’attribut |  
    | ------------------- | -------------------- |    
    | ATTR_LOGINCLAIM | join([mail],"102938475Z","@" |
    
      a. tooopen hello **ajouter un attribut** boîte de dialogue, sélectionnez **ajouter un attribut**.

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    b. Bonjour **nom** , tapez **ATTR_LOGINCLAIM**.

    c. À partir de hello **valeur** liste, sélectionnez **Join()**.

    d. À partir de hello **String1** liste, sélectionnez **user.mail**.

    e. Pour **chaîne2**, tapez l’identificateur hello est fournie par votre équipe HR2day.

    f. Bonjour **séparateur** , tapez  **@** .
    
    g. Sélectionnez **OK**.

7. Sélectionnez hello **enregistrer** bouton.

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. Bonjour **HR2day par la Configuration de Merces** section, sélectionnez **HR2day de configurer par Merces** tooopen hello **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion**, **ID d’entité SAML**, et **SAML Sign-On URL du Service unique** de hello **aide-mémoire** section.

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. tooconfigure SSO pour hello de votre application, contactez [HR2day par l’équipe de support client Merces](mailTo:servicedesk@merces.nl). Attacher hello téléchargé **Certificate(Base64)** tooyour e-mail du fichier. Fournissent également hello **URL de déconnexion**, **ID d’entité SAML**, et **SAML Sign-On URL du Service unique** afin qu’ils peuvent être configurés pour l’intégration de l’authentification unique.

    > [!NOTE]
    >Indiquez toohello Merces équipe qui a besoin de cette intégration hello toobe ID d’entité avec le modèle de hello **https://hr2day.force.com/INSTANCENAME**.

    > [!TIP]
    >Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après avoir ajouté cette application à partir de hello **Active Directory** > **des Applications d’entreprise** section, sélectionnez hello **Single Sign-On** onglet. Hello d’accès incorporée documentation via hello **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello Bonjour [AD Azure incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, prenez hello comme suit :**

1. Bonjour **portail Azure**, sur hello du volet de navigation gauche, sélectionnez hello **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis sélectionnez **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, sélectionnez **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. Bonjour **utilisateur** boîte de dialogue, hello prennent comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** boîte, hello de type **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe**et noter le mot de passe hello.

    d. Sélectionnez **Créer**.
 
### <a name="create-an-hr2day-by-merces-test-user"></a>Créer un utilisateur test HR2day by Merces

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans HR2day par Merces. les utilisateurs de hello tooadd dans un compte hello HR2day, travailler avec hello [HR2day par l’équipe de support client Merces](mailto:servicedesk@merces.nl). 

> [!NOTE]
> Si vous avez besoin de toocreate un utilisateur manuellement, contactez hello [HR2day par l’équipe de support client Merces](mailto:servicedesk@merces.nl).

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooHR2day d’accès par Merces.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooHR2day par Merces, prenez hello comme suit :**

1. Bonjour Azure applications de portail, ouvrez hello voir, allez toohello vue d’annuaire et passez trop**des applications d’entreprise**. Ensuite, sélectionnez **Toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **HR2day par Merces**.

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. Dans le menu hello hello gauche, sélectionnez **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Sélectionnez hello **ajouter** bouton. Ensuite, dans hello **ajouter l’affectation** boîte de dialogue, sélectionnez **utilisateurs et groupes**.

    ![Affecter des utilisateurs][203]

5. Bonjour **utilisateurs et groupes** la boîte de dialogue hello **utilisateurs** liste, sélectionnez **Britta Simon**.

6. Cliquez sur hello **sélectionnez** bouton.

7. Bonjour **ajouter l’affectation** boîte de dialogue, sélectionnez **affecter**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

objectif de cette section Hello est tootest votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.  

Lorsque vous sélectionnez hello HR2day en mosaïque Merces Bonjour volet d’accès, vous automatiquement obtenez connecté tooyour HR2day par Merces application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

