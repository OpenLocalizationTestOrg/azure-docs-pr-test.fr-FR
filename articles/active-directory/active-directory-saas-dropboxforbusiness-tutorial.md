---
title: "Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 63502412-758b-4b46-a580-0e8e130791a1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3f33a43ca8fbd60486d7a400ae8246af768376ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dropbox-for-business"></a>Didacticiel : Intégration d'Azure Active Directory à Dropbox for Business

Dans ce didacticiel, vous apprendrez comment toointegrate Dropbox for Business avec Azure Active Directory (Azure AD).

Intégration de Dropbox for Business à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooDropbox for Business
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDropbox entreprise (SSO) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Dropbox for Business, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Dropbox for Business pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Dropbox for Business à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-dropbox-for-business-from-hello-gallery"></a>Ajout de Dropbox for Business à partir de la galerie de hello
intégration de hello tooconfigure de Dropbox for Business dans Azure AD, vous devez tooadd Dropbox for Business à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Dropbox for Business à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Dropbox for Business**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_search.png)

5. Dans le volet de résultats hello, sélectionnez **Dropbox for Business**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Dropbox for Business, en tirant parti d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Dropbox for Business est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur en Dropbox for Business hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Dropbox for Business.

tooconfigure et test Azure AD l’authentification unique avec Dropbox for Business, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un dossier d’échange pour l’utilisateur de test entreprise](#creating-a-dropbox-for-business-test-user)**  -toohave un équivalent de Britta Simon dans Dropbox for Business est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre Dropbox pour l’application d’entreprise.

**tooconfigure Azure AD single sign-on avec Dropbox for Business, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Dropbox for Business** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_samlbase.png)

3. Sur hello **Dropbox pour le domaine d’entreprise et les URL** section, effectuer hello comme suit :

    a. Ouverture de session tooyour Dropbox pour le client de l’entreprise. 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769509.png "Configurer l’authentification unique")
   
    b. Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **Console d’administration**. 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769510.png "Configurer l’authentification unique")
   
    c. Sur hello **Console d’administration**, cliquez sur **authentification** dans le volet de navigation gauche hello. 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769511.png "Configurer l’authentification unique")
   
    d. Bonjour **l’authentification unique** section, sélectionnez **activer l’authentification unique sur**, puis cliquez sur **plus** tooexpand cette section.  
   
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769512.png "Configurer l’authentification unique")
   
    e. Copier l’URL de hello ensuite trop**les utilisateurs peuvent se connecter en entrant leur adresse de messagerie ou ils peuvent accéder directement à**. 
    
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/ic769513.png)
    
    f. Sur hello portail Azure, Bonjour **URL de connexion** zone de texte, collez hello URL.

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_url.png)

     Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.dropbox.com/sso/<id>`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour la valeur de hello avec hello Sign-on URL réelle vous obtenez à partir de la section de l’authentification unique. Contact [Dropbox pour l’équipe de support Client Business](https://www.dropbox.com/business/contact) tooget cette valeur. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_400.png)

6. Sur hello **Dropbox for Business Configuration** , cliquez sur **configurer de Dropbox for Business** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_configure.png) 

7. tooconfigure l’authentification unique sur **Dropbox for Business** côté, allez sur votre client Dropbox for Business, Bonjour **l’authentification unique** section Hello **authentification** page, Effectuez hello comme suit : 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/IC769516.png "Configurer l’authentification unique")
   
    a. Cliquez sur **Obligatoire**.
   
    b. Bonjour portail Azure, sur hello **configurer l’authentification** fenêtre, hello de copie **SAML Sign-On URL du Service unique** valeur, puis collez-le dans hello **URL de connexion** zone de texte.

    c. Cliquez sur **choisir un certificat**, puis recherchez tooyour **fichier de certificat codé en Base64**.

    d. Cliquez sur **enregistrer les modifications** configuration de hello toocomplete sur votre client DropBox for Business.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_01.png) 

2.  liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-dropboxforbusiness-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-dropbox-for-business-test-user"></a>Création d’un utilisateur de test Dropbox for Business

Dans cette section, un utilisateur appelé Britta Simon est créé dans Dropbox for Business. Dropbox for Business prend en charge l’approvisionnement juste-à-temps, option activée par défaut.

Vous n’avez aucune opération à effectuer dans cette section. Si un utilisateur n’existe pas déjà dans Dropbox for Business, un nouveau est créé lorsque vous essayez de tooaccess Dropbox for Business.

>[!Note]
>Si vous avez besoin de toocreate un utilisateur manuellement, contactez [Dropbox pour l’équipe de support Client d’entreprise](https://www.dropbox.com/business/contact) 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDropbox for Business.

![Affecter des utilisateurs][200] 

**tooassign tooDropbox Britta Simon for Business, procédez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Dropbox for Business**.

    ![Configurer l’authentification unique](./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_dropboxforbusiness_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello Dropbox de vignette Business Bonjour volet d’accès, vous devez obtenir la page de connexion de votre Dropbox pour l’application d’entreprise.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-dropboxforbusiness-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dropboxforbusiness-tutorial/tutorial_general_203.png

