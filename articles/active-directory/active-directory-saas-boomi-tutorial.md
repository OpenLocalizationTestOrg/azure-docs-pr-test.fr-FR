---
title: "Didacticiel : Intégration d’Azure Active Directory à Boomi | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Boomi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8e05afa9-2eda-4975-a0cc-6d408065860f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ce64a4561697d311a8c7b1b244315bb552c5cfb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-boomi"></a>Didacticiel : Intégration d’Azure Active Directory à Boomi

Dans ce didacticiel, vous apprendrez comment toointegrate Boomi avec Azure Active Directory (Azure AD).

Intégration de Boomi à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooBoomi
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBoomi (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Boomi, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Boomi pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Boomi à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-boomi-from-hello-gallery"></a>Ajout de Boomi à partir de la galerie de hello
intégration de hello tooconfigure de Boomi dans Azure AD, vous devez tooadd Boomi à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Boomi à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Boomi**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_search.png)

5. Dans le volet de résultats hello, sélectionnez **Boomi**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Boomi avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Boomi est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Boomi doit toobe établie.

En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Boomi, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Boomi](#creating-a-boomi-test-user)**  -toohave un équivalent de Britta Simon dans Boomi est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Boomi.

**tooconfigure Azure AD single sign-on avec Boomi, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Boomi** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_samlbase.png)

3. Sur hello **Boomi domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_url.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://platform.boomi.com/sso/<accountname>/saml`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://platform.boomi.com/sso/<accountname>/saml`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle. Contact [équipe de support technique de Boomi](https://boomi.com/company/contact/) tooget ces valeurs.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_certificate.png)

4. Application de Boomi attend les assertions SAML hello dans un format spécifique. Veuillez configurer hello suivant des revendications pour cette application. Vous pouvez gérer les valeurs de ces attributs hello depuis hello »**attributs utilisateur**« section sur la page d’intégration d’application. Hello suivant capture d’écran montre un exemple de cela.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_attribute.png)

5. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, pour chaque ligne de la table hello ci-dessous, effectuer hello comme suit :

    | Nom de l'attribut | Valeur de l’attribut |
    | -------------- | --------------- |
    | FEDERATION_ID | user.mail |
    
    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_04.png)
    
    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_attribute_05.png)
    
    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.
    
    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.
    
    d. Cliquez sur **OK**.

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_general_400.png)

7. Sur hello **Boomi Configuration** , cliquez sur **configurer de Boomi** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_configure.png) 

8. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Boomi en tant qu’administrateur. 

9. Accédez trop**nom de la société** et accédez trop**configurer**.

10. Cliquez sur hello **Options SSO** onglet et suivez les étapes ci-dessous.

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_11.png)

    a. Cochez la case **Enable SAML Single Sign-On**.

    b. Cliquez sur **importation** hello de tooupload téléchargé certificat auprès d’Azure AD trop**certificat de fournisseur d’identité**.
    
    c. Bonjour **Identity Provider Login URL** zone de texte, placez la valeur hello **SAML Sign-On URL du Service unique** à partir de la fenêtre de configuration d’application Azure AD.

    d. Dans **Federation Id Location** (Emplacement ID de fédération), sélectionnez le bouton radio **Federation Id is in FEDERATION_ID Attribute element** (L’ID de fédération se trouve dans l’élément d’attribut FEDERATION_ID). 

    e. Cliquez sur le bouton **Enregistrer** .

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-boomi-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-boomi-test-user"></a>Création d’un utilisateur de test Boomi

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans tooBoomi, vous devez les configurer dans Boomi. Dans les cas de hello d’occurrence, cette configuration est une tâche manuelle.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision un compte d’utilisateur, effectuez hello comme suit :

1. Ouvrez une session dans tooyour site d’entreprise Boomi en tant qu’administrateur.

2. Une fois connecté, accédez trop**gestion des utilisateurs** et accédez trop**utilisateurs**.

    ![Utilisateurs](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_001.png "Utilisateurs")

3. Cliquez sur  **+**  icône et hello **rôles d’utilisateur Ajouter/Mettre à jour** boîte de dialogue s’ouvre.

    ![Utilisateurs](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_002.png "Utilisateurs")

    ![Utilisateurs](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_003.png "Utilisateurs")

    a. Bonjour **adresse de messagerie utilisateur** par courrier électronique de type hello d’utilisateur de zone de texte, comme BrittaSimon@contoso.com.
    
    b. Bonjour **prénom** type hello premier nom d’utilisateur comme Brian zone de texte.

    c. Bonjour **nom** zone de texte, type hello nom d’utilisateur comme Simon.
    
    d. Entrez l’utilisateur hello **ID de fédération**. Chaque utilisateur doit avoir un ID de fédération qui identifie de façon unique utilisateur hello dans le compte de hello.
    
    e. Affecter hello **utilisateur Standard** utilisateur toohello de rôle. N’attribuez pas le rôle d’administrateur hello car qui lui donnent accès atmosphère normal, ainsi que des accès de l’authentification unique.
    
    f. Cliquez sur **OK**.
    
    > [!NOTE]
    > utilisateur de Hello pas reçoit un message de notification accueil contenant un mot de passe qui peut être utilisé toolog dans toohello AtomSphere compte, car son mot de passe est géré via le fournisseur d’identité hello. Vous pouvez utiliser n’importe quel autre Boomi utilisateur compte outil de création ou API fournie par Boomi tooprovision des comptes d’utilisateur AAD. 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBoomi.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooBoomi, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Boomi**.

    ![Configurer l’authentification unique](./media/active-directory-saas-boomi-tutorial/tutorial_boomi_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Boomi hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Boomi application.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-boomi-tutorial/tutorial_general_203.png

