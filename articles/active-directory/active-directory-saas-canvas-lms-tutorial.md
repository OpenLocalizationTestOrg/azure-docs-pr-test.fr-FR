---
title: "Didacticiel : Intégration d’Azure Active Directory à Canvas Lms | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Canvas LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a>Didacticiel : Intégration d’Azure Active Directory à Canvas LMS

Dans ce didacticiel, vous apprendrez comment toointegrate canevas avec Azure Active Directory (Azure AD).

Intégration de zone de dessin à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooCanvas
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooCanvas (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Canvas, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Canvas pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de zone de dessin à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-canvas-from-hello-gallery"></a>Ajout de zone de dessin à partir de la galerie de hello
intégration de hello tooconfigure de zone de dessin dans Azure AD, vous devez tooadd zone de dessin à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd zone à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **canevas**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. Dans le volet de résultats hello, sélectionnez **canevas**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Canvas au moyen d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans la zone de dessin est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans la zone de dessin hello doit toobe établie.

Dans la zone de dessin, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec une zone de dessin, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test canevas](#creating-a-canvas-test-user)**  -toohave un équivalent de Britta Simon dans la zone de dessin qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de la zone de dessin.

**tooconfigure Azure AD authentification unique avec une zone de dessin, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **canevas** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. Sur hello **URL et le domaine de la zone de dessin** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.instructure.com`

    b. Bonjour **identificateur** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<tenant-name>.instructure.com/saml2`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de la zone de dessin](https://community.canvaslms.com/community/help) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. Sur hello **Configuration de la zone de dessin** , cliquez sur **configurer la zone de dessin** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de modification du mot de passe, l’URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise tooyour canevas en tant qu’administrateur.

8. Accédez trop**cours \> comptes gérés \> Microsoft**.
   
    ![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")

9. Dans le volet de navigation hello hello gauche, sélectionnez **authentification**, puis cliquez sur **Add New SAML Config**.
   
    ![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")

10. Sur la page d’intégration en cours de hello, procédez hello comme suit :
   
    ![Intégration actuelle](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Intégration actuelle")

    a. Dans **IdP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.

    b. Dans **Log On URL** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.

    c. Dans **URL de déconnexion** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.

    d. Dans **Change Password Link** zone de texte, valeur hello coller **URL de modification du mot de passe** dont vous avez copié à partir du portail Azure. 

    e. Dans **empreinte numérique du certificat** zone de texte, collez hello **l’empreinte numérique** valeur de certificat que vous avez copié à partir du portail Azure.      
        
    f. À partir de hello **Login Attribute** liste, sélectionnez **NameID**.

    g. À partir de hello **Identifier Format** liste, sélectionnez **emailAddress**.

    h. Cliquez sur **Save Authentication Settings**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="creating-a-canvas-test-user"></a>Création d’un utilisateur de test Canvas

tooenable Azure AD les utilisateurs toolog dans tooCanvas, vous devez les configurer dans la zone de dessin.

En l’occurrence, cet approvisionnement d’utilisateur est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **canevas** client.

2. Accédez trop**cours \> comptes gérés \> Microsoft**.
   
   ![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")

3. Cliquez sur **Utilisateurs**.
   
   ![Utilisateurs](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Utilisateurs")

4. Cliquez sur **Add New User**.
   
   ![Utilisateurs](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Utilisateurs")

5. Dans Ajouter une page de boîte de dialogue Nouvel utilisateur de hello, procédez hello comme suit :
   
   ![Ajouter un utilisateur](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Ajouter un utilisateur")
   
   a. Bonjour **nom complet** zone de texte, entrez hello les nom d’utilisateur comme **BrittaSimon**.

   b. Bonjour **messagerie** zone de texte, entrez hello adresse de messagerie de l’utilisateur comme  **brittasimon@contoso.com** .

   c. Bonjour **connexion** zone de texte, entrez l’adresse de messagerie de l’utilisateur hello Azure AD comme  **brittasimon@contoso.com** .

   d. Sélectionnez **E-mail de l’utilisateur sur la création de ce compte hello**.

   e. Cliquez sur **Add User**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre zone de dessin utilisateur compte outil de création ou API fournie par Canvas tooprovision des comptes d’utilisateur AAD.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooCanvas.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooCanvas, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **canevas**.

    ![Configurer l’authentification unique](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque du canevas hello Bonjour volet d’accès, vous devez obtenir l’application de zone de dessin tooyour automatiquement signé sur.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

