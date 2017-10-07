---
title: "Didacticiel : Intégration d’Azure Active Directory à RFPIO | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et RFPIO."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: e0c692276276edd8f859e73d81cf54d75a65957a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Didacticiel : Intégration d’Azure Active Directory à RFPIO

Dans ce didacticiel, vous apprendrez comment toointegrate RFPIO avec Azure Active Directory (Azure AD).

Intégration RFPIO à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler qui dans Azure AD qui a accès tooRFPIO.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooRFPIO (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central--hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec RFPIO, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement RFPIO pour lequel l’authentification unique est activée.

> [!NOTE]
> Nous ne vous recommandons d’utiliser une procédure de production environnement tootest hello dans ce didacticiel.

étapes de hello tootest dans ce didacticiel, suivez ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario de Hello est décrit dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de RFPIO à partir de la galerie de hello.
2. Configuration et test de l’authentification unique Azure AD

## <a name="add-rfpio-from-hello-gallery"></a>Ajouter des RFPIO à partir de la galerie de hello
intégration de hello tooconfigure de RFPIO dans Azure AD, vous devez tooadd RFPIO à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

### <a name="tooadd-rfpio-from-hello-gallery"></a>tooadd RFPIO à partir de la galerie de hello

1. Bonjour  **[portail Azure](https://portal.azure.com)**, sur hello du volet de navigation gauche, sélectionnez hello **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.

    ![Applications][2]
    
3. tooadd une nouvelle application, sélectionnez hello **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **RFPIO**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_search.png)

5. Dans le volet de résultats hello, sélectionnez **RFPIO**, puis sélectionnez hello **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec RFPIO, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quelle relation hello est entre équivalent dans RFPIO un utilisateur et dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans RFPIO doit toobe établie.

Dans RFPIO, affecter la valeur de hello de **nom d’utilisateur** dans Azure AD en tant que valeur hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec RFPIO, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**--tooenable votre toouse utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**--tootest Azure AD l’authentification unique avec Britta Simon.
3. **[Créer un utilisateur de test RFPIO](#creating-a-rfpio-test-user)**  toohave--un équivalent de Britta Simon dans RFPIO est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assigning-the-azure-ad-test-user)**tooenable--Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#testing-single-sign-on)**  --tooverify si hello configuration fonctionne.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application RFPIO.

**tooconfigure Azure AD single sign-on avec RFPIO, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **RFPIO** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_samlbase.png)

3. Sur hello **RFPIO domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url.png)

    a. Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://www.rfpio.com`

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Cliquez sur **Afficher les paramètres d’URL avancés**.

    c. Bonjour **relais état** zone de texte Entrez une valeur de chaîne. Contact [RFPIO l’équipe de support](https://www.rfpio.com/contact/) tooget cette valeur. 

4. Cliquez sur **Afficher les paramètres d’URL avancés**. Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :   

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_url2.png)

    Bonjour **URL de connexion** zone de texte, tapez l’URL hello :`https://www.app.rfpio.com`

5. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_general_400.png)

7. Dans une fenêtre de navigateur web, connexion toohello **RFPIO** site Web en tant qu’administrateur.

8. Cliquez sur la liste déroulante de hello en bas à gauche.

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app1.png)

9. Cliquez sur hello **paramètres de l’organisation**. 

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app2.png)

10. Cliquez sur hello **intégration et fonctionnalités**.

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app4.png)

11. Bonjour **Configuration de l’authentification unique SAML** cliquez sur **modifier**.

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app3.png)

12. Dans cette section, procédez comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app5.png)
    
    a. Copier le contenu de hello Hello **XML de métadonnées téléchargé** et collez-le dans hello **configuration d’identité** champ.

    > [!NOTE]
    >hello toocopy contenu de téléchargé **Metadata XML** utilisez **bloc-notes ++** ou appropriée **éditeur XML**. 

    b. Cliquez sur **Valider**.

    c. Après avoir fait de cliquer sur **Validate**, retourner **SAML(Enabled)** tooon.

    d. Cliquez sur **Envoyer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-rfpio-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="create-a-rfpio-test-user"></a>Créer un utilisateur de test RFPIO

tooenable Azure AD les utilisateurs toolog dans tooRFPIO, vous devez les configurer dans RFPIO.  
Dans les cas de hello de RFPIO, cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Ouvrez une session dans tooyour site d’entreprise RFPIO en tant qu’administrateur.

2. Cliquez sur la liste déroulante de hello en bas à gauche.

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app1.png)

3. Cliquez sur hello **paramètres de l’organisation**. 

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app2.png)

4. Cliquez sur **MEMBRES DE L’ÉQUIPE**.

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app6.png)

5. Cliquez sur **AJOUTER DES MEMBRES**.

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app7.png)

6. Bonjour **ajouter de nouveaux membres** section. Procédez comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/app8.png)

    a. Entrée **adresse de messagerie** Bonjour **Entrez une adresse de messagerie par ligne** champ.

    b. Sélectionnez le **Rôle** selon vos besoins.

    c. Cliquez sur **AJOUTER DES MEMBRES**.
        
    > [!NOTE]
    > titulaire du compte Azure Active Directory Hello reçoit un message électronique et suit un tooconfirm de lier leur compte avant son activation.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooRFPIO.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooRFPIO, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **RFPIO**.

    ![Configurer l’authentification unique](./media/active-directory-saas-rfpio-tutorial/tutorial_rfpio_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous testez votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello RFPIO vignette dans le volet d’accès de hello, vous devez obtenir l’application de RFPIO tooyour automatiquement signé sur.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de toointegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rfpio-tutorial/tutorial_general_203.png

