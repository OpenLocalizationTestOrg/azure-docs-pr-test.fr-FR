---
title: "Didacticiel : Intégration d’Azure Active Directory à MOVEit Transfer - Azure AD integration | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et transfert MOVEit - intégration d’Azure AD."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8ff7102d-be73-4888-ae81-d8e3d01dd534
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 5bbe4f2d952bd45c4d58d55ffc3467b4eb871fd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-moveit-transfer---azure-ad-integration"></a>Didacticiel : Intégration d’Azure Active Directory à MOVEit Transfer - Azure AD integration

Dans ce didacticiel, vous apprendrez comment toointegrate MOVEit transfert - intégration d’Azure AD avec Azure Active Directory (Azure AD).

Intégration de transfert MOVEit - intégration d’Azure AD avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooMOVEit transfert - intégration d’Azure AD.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMOVEit transfert - intégration d’Azure AD (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec transfert MOVEit - intégration d’Azure AD, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement MOVEit Transfer - Azure AD integration pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de transfert MOVEit - intégration d’Azure AD à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-moveit-transfer---azure-ad-integration-from-hello-gallery"></a>Ajout de transfert MOVEit - intégration d’Azure AD à partir de la galerie de hello
intégration de hello tooconfigure de transfert de MOVEit - intégration d’Azure AD dans Azure AD, vous devez tooadd MOVEit transfert - intégration d’Azure AD à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd MOVEit transfert - intégration d’Azure AD à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **MOVEit transfert - intégration d’Azure AD**, sélectionnez **MOVEit transfert - intégration d’Azure AD** à partir du volet de résultats, puis sur **ajouter** hello tooadd de bouton application.

    ![Transfert de MOVEit - intégration d’Azure AD dans la liste des résultats hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec MOVEit Transfer - Azure AD integration avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans MOVEit transfert - intégration d’Azure AD est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans MOVEit transfert - intégration d’Azure AD doit toobe établie.

Dans transfert MOVEit - intégration d’Azure AD, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec transfert MOVEit - intégration d’Azure AD, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un transfert MOVEit - utilisateur de test d’intégration Azure AD](#create-a-moveit-transfer---azure-ad-integration-test-user)**  intégration d’Azure AD - toohave de Britta Simon dans MOVEit transfert contrepartie - qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre transfert MOVEit - application d’intégration Azure AD.

**tooconfigure Azure AD single sign-on avec MOVEit transfert - intégration d’Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **MOVEit transfert - intégration d’Azure AD** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_samlbase.png)

3. Sur hello **MOVEit transfert - URL et intégration d’Azure AD domaine** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://contoso.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://contoso.com/<tenatid>`

    c. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://contoso.com/<tenatid>/SAML/SSO/HTTP-Post`    
     
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. Vous pouvez faire référence à ces valeurs ultérieurement en **URL du Service fournisseur de métadonnées** section ou contactez [MOVEit transfert - équipe de prise en charge des clients Azure AD intégration](https://community.ipswitch.com/s/support) tooget ces valeurs.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_400.png)
    
6. Ouverture de session tooyour client de transfert de MOVEit en tant qu’administrateur.

7. Dans le volet de navigation gauche hello, cliquez sur **paramètres**.

    ![Section Paramètres côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_000.png)

8. Cliquez sur le lien **Authentification unique** qui se trouve sous **Stratégies de sécurité -> Authentification des utilisateurs**.

    ![Stratégies de sécurité côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_001.png)

9. Cliquez sur le document de métadonnées du lien toodownload hello hello URL des métadonnées.

    ![URL de métadonnées du fournisseur de service](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_002.png)
    
    * Vérifiez **entityID** correspond à **identificateur** Bonjour **MOVEit transfert - URL et intégration d’Azure AD domaine** section.
    * Vérifiez **AssertionConsumerService** emplacement URL correspond à **URL de réponse** Bonjour **MOVEit transfert - URL et intégration d’Azure AD domaine** section.
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_007.png)

10. Cliquez sur **ajouter un fournisseur d’identité** bouton tooadd un nouveau fournisseur d’identité fédérée.

    ![Ajouter un fournisseur d’identité](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_003.png)

11. Cliquez sur **Parcourir...**  tooselect hello du fichier de métadonnées que vous avez téléchargé à partir du portail Azure, puis cliquez sur **ajouter un fournisseur d’identité** hello de tooupload téléchargé le fichier.

    ![Fournisseur d’identité SAML](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_004.png)

12. Sélectionnez «**Oui**» en tant que **activé** Bonjour **modifier les paramètres de fournisseur d’identité fédérée...**  page, puis cliquez sur **enregistrer**.

    ![Paramètres de fournisseur d’identité fédérée](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_005.png)

13. Bonjour **modifier fédéré identité du fournisseur de paramètres utilisateur** page, effectuer hello suivant des actions :
    
    ![Modifier les paramètres de fournisseur d’identité fédérée](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_006.png)
    
    a. Sélectionnez **SAML NameID** comme **Nom de connexion**.
    
    b. Sélectionnez **autres** en tant que **nom complet** et Bonjour **nom de l’attribut** zone de texte, insérez les valeur hello : `http://schemas.microsoft.com/identity/claims/displayname`.
    
    c. Sélectionnez **autres** en tant que **messagerie** et Bonjour **nom de l’attribut** zone de texte, insérez les valeur hello : `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.
    
    d. Sélectionnez **Oui** sous **Auto-create account on signon** (Créer automatiquement un compte lors de l’authentification).
    
    e. Cliquez sur le bouton **Enregistrer** .

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-moveittransfer-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-moveit-transfer---azure-ad-integration-test-user"></a>Créer un utilisateur de test MOVEit Transfer - Azure AD integration

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans transfert MOVEit - intégration d’Azure AD. MOVEit Transfer - Azure AD integration prend en charge l’approvisionnement juste-à-temps que vous avez activé. Vous n’avez aucune opération à effectuer dans cette section. Un nouvel utilisateur est créé au cours d’une tentative de tooaccess MOVEit transfert - intégration d’Azure AD s’il n’existe pas encore.

>[!NOTE]
>Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [MOVEit transfert - équipe de prise en charge des clients Azure AD intégration](https://community.ipswitch.com/s/support).

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMOVEit transfert - intégration d’Azure AD.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooMOVEit transfert - intégration d’Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **MOVEit transfert - intégration d’Azure AD**.

    ![Hello MOVEit transfert - intégration d’Azure AD de lien dans la liste des Applications hello](./media/active-directory-saas-moveittransfer-tutorial/tutorial_moveittransfer_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello MOVEit transfert - vignette de l’intégration d’Azure AD dans hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour MOVEit transfert - application d’intégration Azure AD. 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-moveittransfer-tutorial/tutorial_general_203.png

