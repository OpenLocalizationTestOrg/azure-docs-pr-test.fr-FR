---
title: "Didacticiel : Intégration d’Azure Active Directory à Clarizen | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a>Didacticiel : Intégration d’Azure Active Directory à Clarizen

Dans ce didacticiel, vous apprendrez comment toointegrate Azure Active Directory (Azure AD) à Clarizen. Ceci permet d’intégration vous hello suivants avantages :

- Vous pouvez contrôler, dans Azure AD, qui a accès tooClarizen.
- Vous pouvez activer votre toobe utilisateurs automatiquement connecté tooClarizen (SSO) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central, hello portail Azure.

scénario Hello dans ce didacticiel se compose de deux tâches principales :

1. Ajouter Clarizen à partir de la galerie de hello.
2. Configurez et testez l’authentification unique Azure AD.

Pour plus d’informations sur l’intégration d’applications SaaS (software as a service) à Azure AD, consultez l’article [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
tooconfigure intégration d’Azure AD à Clarizen, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Clarizen activé pour l’authentification unique

étapes de hello tootest dans ce didacticiel, suivez ces recommandations :

- Testez l’authentification unique Azure AD dans un environnement de test. N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous ne disposez pas d’un environnement de test Azure AD, vous pouvez [vous inscrire pour un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="add-clarizen-from-hello-gallery"></a>Ajouter des Clarizen à partir de la galerie de hello
intégration de hello tooconfigure de Clarizen dans Azure AD, ajoutez Clarizen à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

1. Bonjour [portail Azure](https://portal.azure.com)hello du volet gauche, cliquez sur dans hello **Azure Active Directory** icône.

    ![Icône Azure Active Directory][1]

2. Cliquez sur **Applications d’entreprise**. Puis cliquez sur **Toutes les applications**.

    ![Sélection des options « Applications d’entreprise » et « Toutes les applications »][2]

3. Cliquez sur hello **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![bouton « Ajouter » de Hello][3]

4. Dans la zone de recherche de hello, tapez **Clarizen**.

    ![Taper « Clarizen » dans la zone de recherche hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. Dans le volet de résultats hello, sélectionnez **Clarizen**, puis cliquez sur **ajouter** application hello de tooadd.

    ![Sélection de Clarizen dans le volet de résultats hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Bonjour les sections suivantes, vous configurez et testez Azure AD l’authentification unique sur Clarizen en fonction de l’utilisateur de test hello Britta Simon.

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Clarizen est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Clarizen doit toobe établie. Vous établissez cette relation de lien en assignant la valeur hello **nom d’utilisateur** dans Azure AD en tant que valeur hello **nom d’utilisateur** dans Clarizen.

tooconfigure et test Azure AD l’authentification unique avec l’occurrence, hello terminée après les blocs de construction :

1. **[Configurer Azure AD l’authentification unique sur](#configure-azure-ad-single-sign-on)**  tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  tootest AD Azure l’authentification unique avec Britta Simon.
3. **[Créer un utilisateur de test de Clarizen](#create-a-clarizen-test-user)**  toohave de Britta Simon dans Clarizen qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD
Activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Clarizen.

1. Bonjour portail Azure, sur hello **Clarizen** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Sélection de l’option « Authentification unique »][4]

2. Bonjour **l’authentification unique** boîte de dialogue, pour **Mode**, sélectionnez **SAML-authentification** tooenable l’authentification unique.

    ![Sélection de l’option « Authentification basée sur SAML »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. Bonjour **Clarizen domaine et les URL** section, effectuer hello comme suit :

    ![Zones d’identificateur et d’URL de réponse](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    a. Bonjour **identificateur** zone, type valeur hello : **Clarizen**

    b. Bonjour **URL de réponse** , tapez une URL à l’aide de hello modèle : **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**

    > [!NOTE]
    > Ils ne sont pas des valeurs réelles hello. Avoir identificateur réel de toouse hello et URL de réponse. Ici, nous vous suggérons d’utiliser hello de valeur unique d’une chaîne comme identificateur de hello. tooget hello valeurs réelles, contact hello [équipe de support technique de Clarizen](https://success.clarizen.com/hc/en-us/requests/new).

4. Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.

    ![Sélection de l’option « Créer un certificat »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. Bonjour **créer un nouveau certificat** boîte de dialogue zone, cliquez sur icône du calendrier hello et sélectionnez une date d’expiration. Cliquez ensuite sur **Enregistrer**.

    ![Sélection et enregistrement d’une date d’expiration](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. Bonjour **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat**, puis cliquez sur **enregistrer**.

    ![En sélectionnant la case à cocher pour l’activation d’un nouveau certificat hello hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. Bonjour **le certificat de substitution** boîte de dialogue, cliquez sur **OK**.

    ![En cliquant sur « OK » les tooconfirm que vous souhaitez toomake hello certificat active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. Bonjour **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![En cliquant sur le téléchargement de hello toostart « Certificat (Base64) »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. Bonjour **Clarizen Configuration** , cliquez sur **configurer de Clarizen** tooopen hello **configurer l’authentification** fenêtre.

    ![Sélection de l’option « Configurer Clarizen »](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Fenêtre « Configurer l’authentification », incluant les URL et les fichiers](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. Dans une fenêtre de navigateur web, connectez-vous dans un site d’entreprise Clarizen tooyour en tant qu’administrateur.

11. Cliquez sur votre nom d’utilisateur, puis sur **Settings** (Paramètres).

    ![Sélection de l’option « Settings » (Paramètres) sous votre nom d’utilisateur](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings") (Paramètres)

12. Cliquez sur hello **paramètres globaux** onglet. Ensuite, suivant trop**authentification fédérée**, cliquez sur **modifier**.

    ![Onglet « Global Settings » (Paramètres globaux)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings") (Paramètres globaux)

13. Bonjour **authentification fédérée** boîte de dialogue, exécutez hello comme suit :

    ![Boîte de dialogue « Federated Authentication » (Authentification fédérée)](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication") (Authentification fédérée)

    a. Sélectionnez **Activer l'authentification fédérée**.

    b. Cliquez sur **télécharger** tooupload votre certificat téléchargé.

    c. Bonjour **URL de connexion** , entrez la valeur hello **SAML Sign-On URL du Service unique** à partir de la fenêtre de configuration d’application hello Azure AD.

    d. Bonjour **URL de déconnexion** , entrez la valeur hello **URL de déconnexion** à partir de la fenêtre de configuration d’application hello Azure AD.

    e. Sélectionnez **Use POST**.

    f. Cliquez sur **Save**.

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
Bonjour portail Azure, créez un utilisateur de test appelé Britta Simon.

![Nom et adresse de messagerie de l’utilisateur de test hello Azure AD][100]

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** icône.

    ![Icône Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. Cliquez sur **utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.

    ![Sélection des options « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.

    ![bouton « Ajouter » de Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![Boîte de dialogue « Utilisateur » renseignée avec le nom, l’adresse e-mail et le mot de passe](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, l’adresse de messagerie de type hello Hello compte de Britta Simon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello **mot de passe**.

    d. Cliquez sur **Create**.

### <a name="create-a-clarizen-test-user"></a>Créer un utilisateur de test Clarizen
tooenable le toosign les utilisateurs Azure AD dans tooClarizen, vous devez configurer des comptes d’utilisateur. Dans les cas de hello d’occurrence, cette configuration est une tâche manuelle.

1. Se connecter tooyour site d’entreprise Clarizen en tant qu’administrateur.

2. Cliquez sur **People**.

    ![Sélection de l’option « People » (Contacts)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People") (Contacts)

3. Cliquez sur **Invite User**.

    ![Bouton « Invite User » (Inviter un utilisateur)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users") (Inviter un utilisateur)

4. Bonjour **inviter des personnes** boîte de dialogue, exécutez hello comme suit :

    ![Boîte de dialogue « Invite People » (Inviter un contact)](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People") (Inviter un contact)

    a. Bonjour **messagerie** zone, l’adresse de messagerie de type hello Hello compte de Britta Simon.

    b. Cliquez sur **Invite**.

    > [!NOTE]
    > titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD
Activer toouse Britta Simon Azure l’authentification unique en accordant tooClarizen de son accès.

![Utilisateur de test affecté][200]

1. Dans hello portail Azure, ouvrez la vue des applications hello, vue de répertoire toohello, cliquez sur **des applications d’entreprise**, puis cliquez sur **toutes les applications**.

    ![Sélection des options « Applications d’entreprise » et « Toutes les applications »][201]

2. Dans la liste des applications hello, sélectionnez **Clarizen**.

    ![Sélection de Clarizen dans la liste de hello](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. Dans le volet gauche de hello, cliquez sur **utilisateurs et groupes**.

    ![Sélection de l’option « Utilisateurs et groupes »][202]

4. Cliquez sur hello **ajouter** bouton. Ensuite, dans hello **ajouter l’affectation** boîte de dialogue, sélectionnez **utilisateurs et groupes**.

    ![bouton « Ajouter » de Hello et de la boîte de dialogue « Ajouter l’affectation » hello][203]

5. Bonjour **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans liste hello des utilisateurs.

6. Bonjour **utilisateurs et groupes** boîte de dialogue, cliquez sur hello **sélectionnez** bouton.

7. Bonjour **ajouter l’affectation** boîte de dialogue, cliquez sur hello **affecter** bouton.

### <a name="test-single-sign-on"></a>Tester l’authentification unique
Tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Clarizen hello hello volet d’accès, vous devez être connecté automatiquement dans tooyour Clarizen application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
