---
title: "Didacticiel : Intégration d’Azure Active Directory à Autotask Workplace | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’espace de travail Autotask."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9a7ff71-c389-4169-aafd-d7a505244797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 7f820f24e8e9493fa2e1c075f2ef61d7eaa84f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-autotask-workplace"></a>Didacticiel : Intégration d’Azure Active Directory à Autotask Workplace

Dans ce didacticiel, vous apprendrez comment toointegrate Autotask espace de travail avec Azure Active Directory (Azure AD).

Intégration d’espace de travail Autotask à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAutotask espace de travail
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAutotask espace de travail (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’espace de travail Autotask, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Autotask Workplace pour lequel l’authentification unique est activée
- Vous devez être un administrateur ou un super administrateur dans Workplace.
- Vous devez disposer d’un compte d’administrateur Bonjour Azure AD.
- les utilisateurs Hello qui utilisent cette fonctionnalité doivent disposer de comptes dans l’espace de travail et hello Azure AD, et leurs adresses de messagerie pour les deux doivent correspondre.

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’espace de travail Autotask à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-autotask-workplace-from-hello-gallery"></a>Ajout d’espace de travail Autotask à partir de la galerie de hello
intégration de hello tooconfigure Autotask espace de travail dans Azure AD, vous devez tooadd Autotask espace de travail à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Autotask espace de travail à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **espace de travail Autotask**, sélectionnez **espace de travail Autotask** à partir du volet de résultats, puis sur **ajouter** bouton application de hello tooadd.

    ![Espace de travail Autotask Bonjour la liste des résultats](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Autotask Workplace, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’espace de travail Autotask est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’espace de travail Autotask hello doit toobe établie.

Dans l’espace de travail Autotask, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec l’espace de travail Autotask, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test d’espace de travail Autotask](#create-an-autotask-workplace-test-user)**  -toohave un équivalent de Britta Simon dans l’espace de travail Autotask qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de l’espace de travail Autotask.

**tooconfigure Azure AD single sign-on avec Autotask, espace de travail, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **espace de travail Autotask** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_samlbase.png)

3. Si vous le souhaitez application hello tooconfigure **IDP** initiée par le mode, effectuer hello comme suit sur hello **URL et le domaine d’espace de travail Autotask** section :

    ![Informations d’authentification unique dans Domaine et URL Autotask Workplace pour IDP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.awp.autotask.net/singlesignon/saml/metadata`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.awp.autotask.net/singlesignon/saml/SSO`

4. Si vous le souhaitez application hello tooconfigure **SP** mode initié, cocher **afficher les paramètres d’URL avancés** et effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL Autotask Workplace pour SP](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_url1.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.awp.autotask.net/loginsso`
     
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. Contact [équipe de support Client d’espace de travail Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) tooget ces valeurs. 

5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_400.png)

7. Dans une fenêtre de navigateur web, connectez-vous à l’aide en ligne de tooWorkplace hello informations d’identification d’administrateur.

    >[!Note]
    >Lorsque vous configurez hello IdP, un sous-domaine devez toobe spécifié. sous-domaine correct tooconfirm hello tooWorkplace de connexion en ligne. Une fois connecté, assurez-vous de sous-domaine de toohello Remarque dans l’URL de hello.
    >sous-domaine de Hello fait partie de hello entre hello « https:// » et «.awp.autotask.net/ » et doit être nous, Europe, autorité de certification ou de l’Australie.

8. Accédez trop**Configuration** > **Single Sign-On** et effectuer hello comme suit :

    ![Configuration de l’authentification unique Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig1.png)
 
    a. Sélectionnez hello **fichier de métadonnées XML** option et télécharger hello **Metadata XML** téléchargé à partir du portail Azure.

    b. Cliquez sur **Activer l’authentification unique**.
    
    ![Configuration de l’approbation d’authentification unique Autotask](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskssoconfig2.png)

    c. Sélectionnez hello **vérifier ces informations sont correctes et faire confiance à cette IdP** case à cocher.

    d. Cliquez sur **Approuver**.
     
>[!Note]
>Si vous avez besoin d’aide à la configuration d’espace de travail Autotask, consultez [cette page](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) assistance tooget avec votre compte de l’espace de travail.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-autotaskworkplace-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.

### <a name="create-an-autotask-workplace-test-user"></a>Créer un utilisateur de test Autotask Workplace

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Autotask. Collaborez avec [équipe de support technique d’espace de travail Autotask](https://awp.autotask.net/help/Content/0_HOME/Support_for_End_Clients.htm) utilisateurs hello tooadd hello plateforme de l’espace de travail Autotask.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAutotask espace de travail.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooAutotask espace de travail, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **espace de travail Autotask**.

    ![Hello lien Autotask espace de travail dans la liste des Applications hello](./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_autotaskworkplace_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello espace de travail Autotask vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur application de l’espace de travail Autotask tooyour.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-autotaskworkplace-tutorial/tutorial_general_203.png

