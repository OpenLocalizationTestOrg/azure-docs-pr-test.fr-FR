---
title: "Didacticiel : Intégration d’Azure Active Directory à Mimecast Admin Console | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Mimecast Admin Console."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 81c50614-f49b-4bbc-97d5-3cf77154305f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 5a04a5abd9ff30d484bce0a5c97a1d3e48b69e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-admin-console"></a>Didacticiel : Intégration d’Azure Active Directory à Mimecast Admin Console

Dans ce didacticiel, vous apprendrez comment toointegrate Mimecast Admin Console avec Azure Active Directory (Azure AD).

Intégration de Mimecast Admin Console avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooMimecast Console d’administration.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMimecast Console d’administration (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Mimecast Admin Console, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Mimecast Admin Console pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Mimecast Admin Console à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-mimecast-admin-console-from-hello-gallery"></a>Ajout de Mimecast Admin Console à partir de la galerie de hello
intégration de hello tooconfigure de Mimecast Admin Console dans Azure AD, vous devez tooadd Mimecast Admin Console à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Mimecast Admin Console à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Mimecast Admin Console**, sélectionnez **Mimecast Admin Console** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Liste des résultats de Mimecast Admin Console Bonjour](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Mimecast Admin Console sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Mimecast Admin Console est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la Console d’administration Mimecast hello doit toobe établie.

Dans la Console d’administration Mimecast, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique sur Mimecast Admin Console, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test de Mimecast Admin Console](#create-a-mimecast-admin-console-test-user)**  -toohave un équivalent de Britta Simon dans Mimecast Admin Console est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Mimecast Admin Console.

**tooconfigure Azure AD l’authentification unique sur Mimecast Admin Console, exécutez hello comme suit :**

1. Bonjour portail Azure, sur hello **Mimecast Admin Console** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_samlbase.png)

3. Sur hello **Mimecast Admin Console domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_url.png)

    Bonjour **URL de connexion** zone de texte, tapez l’URL hello :
    | |
    | -- |
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|

    > [!NOTE] 
    > Hello l’URL de connexion est spécifique de la région.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_400.png)

6. Sur hello **Mimecast Admin Console Configuration** , cliquez sur **configurer Mimecast Admin Console** tooopen **configurer l’authentification** fenêtre. Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration de Mimecast Admin Console](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_configure.png) 

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Mimecast Admin Console en tant qu’administrateur.

8. Accédez trop**Services \> Application**.

    ![Services](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794998.png "Services")

9. Cliquez sur **Authentication Profiles**.

    ![Profils d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic794999.png "Profils d’authentification")
    
10. Cliquez sur **New Authentication Profile**.

    ![Nouveaux profils d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795000.png "Nouveaux profils d’authentification")

11. Bonjour **profil d’authentification** section, effectuer hello comme suit :

    ![Profil d’authentification](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795015.png "Profil d’authentification")
    
    a. Bonjour **Description** zone de texte, tapez un nom pour votre configuration.
    
    b. Sélectionnez **Enforce SAML Authentication for Mimecast Admin Console**.
    
    c. Pour **Provider**, sélectionnez **Azure Active Directory**.
    
    d. Coller **ID d’entité SAML**, lequel vous avez copié à partir de hello portail Azure en hello **URL de l’émetteur** zone de texte.
    
    e. Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL de connexion** zone de texte.

    f. Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL de déconnexion** zone de texte.
    
    >[!NOTE]
    >Hello valeur de l’URL de connexion et la valeur de l’URL de déconnexion hello sont pour hello Mimecast Admin Console hello identiques.
    
    g. Ouvrez votre certificat de base-64 téléchargé à partir du portail Azure dans le bloc-notes, supprimez la première ligne de hello («*--*») et hello dernière ligne («*--*»), hello copie restant contenu de celui-ci dans le Presse-papiers, puis collez-la toohello **certificat de fournisseur d’identité (métadonnées)** zone de texte.
    
    h. Sélectionnez **Allow Single Sign On**.
    
    i. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985) 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-mimecast-admin-console-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Créer**.
 
### <a name="create-a-mimecast-admin-console-test-user"></a>Créer un utilisateur de test Mimecast Admin Console

Dans l’ordre tooenable Azure AD les utilisateurs toolog à Mimecast Admin Console, vous devez les configurer dans Mimecast Admin Console. Dans les cas de hello de Mimecast Admin Console, cette configuration est une tâche manuelle.

* Vous devez tooregister un domaine avant de pouvoir créer des utilisateurs.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Ouverture de session tooyour **Mimecast Admin Console** en tant qu’administrateur.
2. Accédez trop**répertoires \> interne**.
   
   ![Répertoires](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795003.png "Répertoires")
3. Cliquez sur **Register New Domain**.
   
   ![Enregistrer un nouveau domaine](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795004.png "Enregistrer un nouveau domaine")
4. Après avoir créé votre domaine, cliquez sur **New Address**.
   
   ![Nouvelle adresse](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795005.png "Nouvelle adresse")
5. Dans hello adresse boîte de dialogue Nouveau, effectuez hello comme suit :
   
   ![Enregistrer](./media/active-directory-saas-mimecast-admin-console-tutorial/ic795006.png "enregistrer")
   
   a. Hello de type **adresse de messagerie**, **nom Global**, **mot de passe**, et **confirmer le mot de passe** compte les attributs d’un Azure AD valide que vous souhaitez tooprovision dans hello relatives des zones de texte.

   b. Cliquez sur **Enregistrer**.

>[!NOTE]
>Vous pouvez utiliser tout autre outil de création de compte utilisateur Mimecast Admin Console ou API fournie par les comptes d’utilisateur Mimecast Admin Console tooprovision Azure AD. 

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMimecast Console d’administration.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooMimecast Console d’administration, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Mimecast Admin Console**.

    ![lien de Mimecast Admin Console Hello dans la liste des Applications hello](./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_mimecastadminconsole_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Mimecast Admin Console hello hello volet d’accès, vous devez obtenir l’application de Mimecast Admin Console automatiquement signé sur tooyour.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-admin-console-tutorial/tutorial_general_203.png

