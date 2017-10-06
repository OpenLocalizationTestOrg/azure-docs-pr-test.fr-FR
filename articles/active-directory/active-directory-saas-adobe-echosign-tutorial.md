---
title: "Didacticiel : Intégration d’Azure Active Directory à Adobe Sign | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de connexion d’Adobe."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a>Didacticiel : Intégration d’Azure Active Directory à Adobe Sign

Dans ce didacticiel, vous apprendrez comment toointegrate Adobe signer avec Azure Active Directory (Azure AD).

Intégration d’Adobe connexion à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAdobe signe
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAdobe signe (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec informations d’identification Adobe, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Adobe Sign pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de l’authentification à partir de la galerie de hello Adobe
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-adobe-sign-from-hello-gallery"></a>Ajout de l’authentification à partir de la galerie de hello Adobe
tooconfigure hello intégration d’Adobe signe dans Azure AD, vous devez tooadd Adobe signe à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Adobe de connexion à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Adobe signe**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. Dans le volet de résultats hello, sélectionnez **Adobe signe**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Adobe Sign au moyen d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Adobe signe est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Adobe signe doit toobe établie.

Dans Adobe signe, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec une connexion d’Adobe, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de connexion d’Adobe](#creating-an-adobe-sign-test-user)**  -toohave un équivalent de Britta Simon dans Adobe de connexion qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de connexion d’Adobe.

**tooconfigure Azure AD l’authentification unique sur Adobe signe, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Adobe signe** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. Sur hello **URL et le domaine d’authentification Adobe** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.echosign.com/`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.echosign.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de connexion d’Adobe](https://helpx.adobe.com/in/contact/support.html) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. Sur hello **Adobe signe Configuration** , cliquez sur **configurer l’authentification Adobe** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Adobe signe tooyour en tant qu’administrateur.

8. Dans le menu hello haut de hello, cliquez sur **compte**, puis, dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **paramètres SAML** sous **les paramètres de compte**.
   
   ![Compte](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Compte")

9. Dans la section Paramètres SAML de hello, procédez hello comme suit :
   
   ![Paramètres SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Paramètres SAML")
   
   a. Pour **SAML Mode** (Mode SAML), sélectionnez **SAML Mandatory** (SAML obligatoire).
   
   b. Sélectionnez **toolog autoriser les administrateurs de comptes EchoSign à l’aide de leurs informations d’identification EchoSign**.
   
   c. Pour **User Creation** (Création d’utilisateurs), sélectionnez **Automatically add users authenticated through SAML** (Ajouter automatiquement les utilisateurs authentifiés avec SAML).

10. Poursuivez en effectuant hello suivant les étapes :

       ![Paramètres SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Paramètres SAML")

    a. Coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure en hello **IdP Entity ID** zone de texte.
    
    b. Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure en hello **URL de connexion IdP** zone de texte.
   
    c. Coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure en hello **URL de déconnexion IdP** zone de texte.

    d. Ouvrez votre téléchargé **Certificate(Base64)** dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et collez-la toohello **certificat IdP** zone de texte

    e. Cliquez sur **Enregistrer les modifications**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-an-adobe-sign-test-user"></a>Création d’un utilisateur de test Adobe Sign

tooenable Azure AD les utilisateurs toolog dans tooAdobe de connexion, vous devez les configurer dans Adobe signe. Dans les cas de hello du signe d’Adobe, cette configuration est une tâche manuelle.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Adobe connexion utilisateur compte outil de création ou API fournie par Adobe signe tooprovision des comptes d’utilisateur AAD. 

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **Adobe signe** site d’entreprise en tant qu’administrateur.

2. Dans le menu hello haut de hello, cliquez sur **compte**, puis, dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **utilisateurs et groupes**, puis cliquez sur **créer un nouvel utilisateur**.
   
   ![Compte](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Compte")
   
3. Bonjour **créer un nouvel utilisateur** section, effectuer hello comme suit :
   
   ![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")
   
   a. Hello de type **adresse de messagerie**, **prénom**, et **nom** d’un compte AAD valide que vous voulez tooprovision dans hello relatives des zones de texte.
   
   b. Cliquez sur **Create User**.

>[!NOTE]
>titulaire du compte Azure Active Directory Hello reçoit un message électronique qui inclut un compte de hello tooconfirm lien avant son activation. 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAdobe signe.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooAdobe de connexion, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Adobe signe**.

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Lorsque vous cliquez sur hello Adobe signe vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour signer d’Adobe application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

