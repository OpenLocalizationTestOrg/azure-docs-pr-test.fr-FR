---
title: "Didacticiel : Intégration d’Azure Active Directory à Procore SSO | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’authentification unique Procore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9818edd3-48c0-411d-b05a-3ec805eafb2e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: bb918617f18ba3f44ddde469e6fc411977752f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-procore-sso"></a>Didacticiel : Intégration d’Azure Active Directory à Procore SSO

Dans ce didacticiel, vous apprendrez comment toointegrate Procore l’authentification unique avec Azure Active Directory (Azure AD).

Intégration SSO Procore à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooProcore SSO
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooProcore l’authentification unique (SSO) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

<!--## Overview

tooenable single sign-on with Procore SSO, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Procore SSO.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’authentification unique Procore, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Procore SSO pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de l’authentification unique Procore à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-procore-sso-from-hello-gallery"></a>Ajout de l’authentification unique Procore à partir de la galerie de hello
tooconfigure hello intégration de l’authentification unique Procore dans Azure AD, vous devez tooadd Procore de l’authentification unique à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Procore l’authentification unique à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Procore SSO**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_search.png)

5. Dans le volet de résultats hello, sélectionnez **SSO Procore**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Procore SSO avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SSO Procore est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’authentification unique Procore hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Procore de l’authentification unique.

tooconfigure et test Azure AD l’authentification unique avec l’authentification unique Procore, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de l’authentification unique Procore](#creating-a-procore-sso-test-user)**  -toohave de Britta Simon dans Procore l’authentification unique qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application SSO Procore.

**tooconfigure Azure AD authentification unique avec l’authentification unique Procore, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **SSO Procore** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_samlbase.png)

3. Sur hello **Procore domaine d’authentification unique et les URL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_url.png)

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_general_400.png)

6. Sur hello **Procore Configuration SSO** , cliquez sur **configurer la SSO Procore** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_configure.png) 

7. tooconfigure l’authentification unique sur **Procore SSO** côté, le site de société procore tooyour de connexion en tant qu’administrateur.

8. Dans liste déroulante de boîte à outils hello vers le bas, cliquez sur **Admin** page des paramètres de l’authentification unique tooopen hello.

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/procore_tool_admin.png)

9. Hello coller des valeurs dans les zones hello comme décrit ci-dessous :

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/procore_setting_admin.png)    

    a. Bonjour **émetteur URL d’authentification unique** zone, collez hello ID d’entité SAML copié à partir de hello portail Azure.

    b. Bonjour **SAML cible URL de connexion de** zone, collez hello SAML Sign-On URL du Service unique provenant de hello portail Azure.

    c. Ouvrez maintenant hello **Metadata XML** téléchargé au-dessus de hello portail Azure et de la copie du certificat de hello dans la balise hello nommée **X509Certificate**. Hello de coller copiées valeur hello **certificat Single Sign On x509** boîte.

10. Cliquez sur **Enregistrer les modifications**.

11. Après ces paramètres, vous avez besoin de toosend hello **nom de domaine** (par exemple **contoso.com**) à laquelle vous vous connectez à toohello Procore [équipe de Support Procore](https://support.procore.com/) et ils seront Activer l’authentification unique fédérée pour ce domaine.

<!--### Next steps

tooensure users can sign-in tooProcore SSO after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Procore SSO prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooProcore SSO in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Procore SSO users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-procoresso-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-procore-sso-test-user"></a>Création d’un utilisateur de test Procore SSO

Veuillez suivre hello ci-dessous les étapes toocreate un utilisateur de test Procore sur son côté.

1. Connexion tooyour procore site d’entreprise en tant qu’administrateur.  

2. Dans liste déroulante de boîte à outils hello vers le bas, cliquez sur **répertoire** page de répertoire tooopen hello entreprise.

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_sso_directory.png)

3. Cliquez sur **ajouter une personne** formulaire de hello tooopen et entrez exécuter suivantes options -

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_add.png)

    a. Bonjour **prénom** zone de texte, nom d’utilisateur de type comme **Brian**.

    b. Bonjour **nom** zone de texte, nom d’utilisateur de type comme **Simon**.

    c. Bonjour **adresse de messagerie** adresse de messagerie de l’utilisateur du type de zone de texte, comme  **BrittaSimon@contoso.com** .

    d. Sélectionnez **Modèle d’autorisation** pour **Appliquer le modèle d’autorisation plus tard**.

    e. Cliquez sur **Créer**.

4. Vérifier et mettre à jour les détails de hello hello ajoutés récemment contact.

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_check.png)

5. Cliquez sur **enregistrer et envoyer une invitation** (si une invitation par courrier est requise) ou **enregistrer** (enregistrer directement) d’inscription des utilisateurs toocomplete hello.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/Procore_user_save.png)    

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooProcore accès SSO.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooProcore SSO, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Procore SSO**.

    ![Configurer l’authentification unique](./media/active-directory-saas-procoresso-tutorial/tutorial_procoresso_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès. Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586). Lorsque vous cliquez sur mosaïque SSO Procore hello hello volet d’accès, vous devez obtenir l’application de l’authentification unique Procore tooyour automatiquement signé sur.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-procoresso-tutorial/tutorial_general_203.png

