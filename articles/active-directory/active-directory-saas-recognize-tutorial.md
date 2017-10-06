---
title: "Didacticiel : intégration d’Azure Active Directory à Recognize | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de reconnaissance."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cfad939e-c8f4-45a0-bd25-c4eb9701acaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: f33fc3959f72f875b8c5c4f0abd4e9b6737ca615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-recognize"></a>Didacticiel : Intégration d’Azure Active Directory à Recognize

Dans ce didacticiel, vous apprendrez comment toointegrate reconnaître avec Azure Active Directory (Azure AD).

Intégration de reconnaître à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooRecognize
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRecognize (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

intégration d’Azure AD de tooconfigure avec reconnaissance, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Recognize pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de reconnaître à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-recognize-from-hello-gallery"></a>Ajout de reconnaître à partir de la galerie de hello
tooconfigure hello intégration de reconnaître dans Azure AD, vous devez tooadd reconnaître à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd reconnaître à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **reconnaître**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_search.png)

5. Dans le volet de résultats hello, sélectionnez **reconnaître**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Recognize sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello reconnaître est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de reconnaître hello doit toobe établie.

Dans le reconnaître, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD sur l’authentification unique avec reconnaissance, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de reconnaître](#creating-a-recognize-test-user)**  -toohave un équivalent de Britta Simon dans reconnaître est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de reconnaître.

**tooconfigure Azure AD single sign-on avec reconnaissance, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **reconnaître** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_samlbase.png)

3. Sur hello **reconnaît le domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://recognizeapp.com/<your-domain>/saml/sso`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://recognizeapp.com/<your-domain>`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de reconnaître](mailto:support@recognizeapp.com) pour obtenir l’URL de connexion et que vous pouvez obtenir valeur de l’identificateur en ouvrant hello URL du Service fournisseur de métadonnées à partir de la section de paramètres d’authentification unique est expliquée plus loin dans le didacticiel de hello de hello. . 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_general_400.png)

6. Sur hello **reconnaître une Configuration** , cliquez sur **configurer reconnaît** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_configure.png) 

7. Dans une fenêtre de navigateur web, client de reconnaître tooyour ouverture de session en tant qu’administrateur.

8. Dans le coin supérieur droit hello, cliquez sur **Menu**. Accédez trop**administrateur de l’entreprise**.
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_000.png)

9. Dans le volet de navigation gauche hello, cliquez sur **paramètres**.
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_001.png)

10. Effectuer hello comme suit **paramètres d’authentification unique** section.
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_002.png)
    
    a. Pour **Activer l’authentification unique**, sélectionnez **Activé**.

    b. Bonjour **IDP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.
    
    c. Bonjour **url cible de l’authentification unique** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.
    
    d. Bonjour **Slo cible url** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure. 
    
    e. Ouvrez votre téléchargé **certificat (Base64)** dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez-la toohello **certificat** zone de texte.
    
    f. Cliquez sur hello **enregistrer les paramètres** bouton. 

11. En regard de hello **paramètres d’authentification unique** section, copiez l’URL hello sous **url des métadonnées de fournisseur de Service**.
   
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_003.png)

12. Ouvrez hello **lien URL de métadonnées** sous un document de métadonnées de navigateur vide toodownload hello. Puis copiez hello EntityDescriptor value(entityID) du fichier de hello et collez-le dans **identificateur** zone de texte dans **section reconnaît le domaine et les URL** sur le portail Azure.
    
    ![Configurer l’authentification unique côté application](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_004.png)

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-recognize-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-recognize-test-user"></a>Création d’un utilisateur de test Recognize

Dans l’ordre tooenable Azure AD les utilisateurs toolog à reconnaître, vous devez les configurer dans reconnaître. Dans les cas de hello de reconnaître, cette configuration est une tâche manuelle.

Cette application ne prend pas en charge l’approvisionnement SCIM, mais inclut une autre synchronisation de l’autre utilisateur qui approvisionne les utilisateurs. 

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à votre site d’entreprise Recognize en tant qu’administrateur.

2. Dans le coin supérieur droit hello, cliquez sur **Menu**. Accédez trop**administrateur de l’entreprise**.

3. Dans le volet de navigation gauche hello, cliquez sur **paramètres**.

4. Effectuer hello comme suit **synchronisation utilisateur** section.
   
   ![Nouvel utilisateur](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_005.png "Nouvel utilisateur")
   
   a. Pour l’option **Synchronisation activée**, sélectionnez **Activé**.
   
   b. Pour **Choisir le fournisseur de synchronisation**, sélectionnez **Microsoft / Office 365**.
   
   c. Cliquez sur **Run User Sync (Exécuter la synchronisation des utilisateurs)**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRecognize.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooRecognize, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **reconnaître**.

    ![Configurer l’authentification unique](./media/active-directory-saas-recognize-tutorial/tutorial_recognize_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque de reconnaître hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour reconnaître application. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-recognize-tutorial/tutorial_general_203.png

