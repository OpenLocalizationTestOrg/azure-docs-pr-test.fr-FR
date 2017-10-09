---
title: "Didacticiel : intégration d’Azure Active Directory à T&E Express | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de T & E Express."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: B42374E5-2559-4309-8EF2-820BEE7EBB0C
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: jeedes
ms.openlocfilehash: 9a568ace8dbc75fadbf37554996b1b597a813d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-te-express"></a>Didacticiel : Intégration d’Azure Active Directory à T&E Express

Dans ce didacticiel, vous apprendrez comment toointegrate T & E Express avec Azure Active Directory (Azure AD).

Intégration de T & E Express avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a tooT d’accès & E Express
- Vous pouvez activer votre tooT utilisateurs tooautomatically get connecté & E Express (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec T & E Express, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement T&E Express pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de T & E Express à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-te-express-from-hello-gallery"></a>Ajout de T & E Express à partir de la galerie de hello
tooconfigure hello intégration de T & E Express dans Azure AD, vous devez tooadd T & E Express à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd T & E Express à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **T & E Express**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_search.png)

5. Dans le volet de résultats hello, sélectionnez **T & E Express**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec T&E Express avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans T & E Express est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans T & E Express toobe besoins établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans T & E Express.

tooconfigure et test Azure AD l’authentification unique avec T & E Express, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test T & E Express](#creating-a-te-express-test-user)**  -toohave de Britta Simon dans T & E Express qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application T & E Express.

**tooconfigure Azure AD l’authentification unique avec T & E Express, procédez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **T & E Express** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_samlbase.png)

3. Sur hello **domaine Express d’E & T et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_url.png)

    a. Bonjour **identificateur** valeur hello de type en tant que zone de texte :`https://<domain>.tyeexpress.com`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<domain>.tyeexpress.com/authorize/samlConsume.aspx`

    > [!NOTE] 
    > Notez qu’il s’agit pas des valeurs réelles hello. Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle. Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur. Contact [T & E Express prend en charge team](http://www.tyeexpress.com/contacto.aspx) tooget ces valeurs.

5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_400.png)

8. tooconfigure l’authentification unique sur **T & E Express** côté, connexion toohello T & E express une application sans SAML unique de session à l’aide des informations d’identification d’administrateur.

9. Sous hello **Admin** onglet, cliquez sur **domaine SAML** page de paramètres SAML tooOpen hello.

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tye-SAML.png)

10. Sélectionnez hello **Activar(Activate)** option à partir de **non** trop**SI(Yes)**. Bonjour **métadonnées du fournisseur d’identité** zone de texte, collez hello métadonnées XML que vous avez donwloaded à partir du portail Azure.

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tyeAdmin.png)

11. Cliquez sur hello **Guardar(Save)** bouton Paramètres de hello toosave. 


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tyeexpress-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-te-express-test-user"></a>Création d’un utilisateur de test T&E Express

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans T & E Express, ils doivent être configurés dans T & E Express.  
En l’occurrence, cet approvisionnement est une tâche manuelle.

**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**

1. Ouvrez une session dans tooyour T & E Express site d’entreprise en tant qu’administrateur.

2. Sous la balise de l’administrateur, cliquez sur page maître pour les utilisateurs tooopen hello les utilisateurs.

    ![Ajouter un employé](./media/active-directory-saas-tyeexpress-tutorial/tye-adminusers.png)

3. Dans la page d’accueil hello, cliquez sur  **+**  les utilisateurs de tooadd hello.

    ![Ajouter un employé](./media/active-directory-saas-tyeexpress-tutorial/tye-usershome.png)

4. Entrez toutes les informations obligatoires hello comme demandé dans le formulaire de hello et cliquez sur hello bouton toosave hello détails d’enregistrement.

    ![Ajouter un employé](./media/active-directory-saas-tyeexpress-tutorial/tye-usersadd.png)

    ![Ajouter un employé](./media/active-directory-saas-tyeexpress-tutorial/tye-userssave.png)


### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooT d’accès & E Express.

![Affecter des utilisateurs][200] 

**tooassign tooT de Britta Simon & E Express, procédez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **T & E Express**.

    ![Configurer l’authentification unique](./media/active-directory-saas-tyeexpress-tutorial/tutorial_tyeexpress_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello T & E Express mosaïque hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour T & E Express l’application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tyeexpress-tutorial/tutorial_general_203.png
