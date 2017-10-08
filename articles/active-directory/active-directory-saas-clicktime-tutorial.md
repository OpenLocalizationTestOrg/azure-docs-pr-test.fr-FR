---
title: "Didacticiel : Intégration d’Azure Active Directory à ClickTime | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a>Didacticiel : Intégration d’Azure Active Directory à ClickTime

Dans ce didacticiel, vous apprendrez comment toointegrate ClickTime avec Azure Active Directory (Azure AD).

Intégration de ClickTime à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooClickTime
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooClickTime (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à ClickTime, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement ClickTime pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de ClickTime à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-clicktime-from-hello-gallery"></a>Ajout de ClickTime à partir de la galerie de hello
tooconfigure hello intégration de ClickTime dans Azure AD, vous devez tooadd ClickTime à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd ClickTime à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **ClickTime**, sélectionnez **ClickTime** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Liste des résultats de ClickTime Bonjour](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ClickTime, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ClickTime est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ClickTime doit toobe établie.

Dans ClickTime, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à ClickTime, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test de ClickTime](#create-a-clicktime-test-user)**  -toohave un équivalent de Britta Simon dans ClickTime est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de ClickTime.

**tooconfigure Azure AD single sign-on avec ClickTime, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **ClickTime** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. Sur hello **ClickTime domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL en tant que :`https://app.clicktime.com/sp/`
    
    b. Bonjour **URL de réponse** modèles de zone de texte, tapez une URL à l’aide de hello suivant : 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. Sur hello **ClickTime Configuration** , cliquez sur **configurer de ClickTime** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration de ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise ClickTime en tant qu’administrateur.

8. Dans la barre d’outils de hello en haut de hello, cliquez sur **préférences**, puis cliquez sur **paramètres de sécurité**.

9. Bonjour **préférences de l’authentification unique** configuration section, effectuer hello comme suit :
   
    ![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")
   
    a.  Sélectionnez **Autoriser** la connexion à l’aide de l’authentification unique (SSO) avec **Azure AD**.
   
    b. Bonjour **point de terminaison de fournisseur d’identité** zone de texte, collez **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.
   
    c.  Ouvrez hello **certificat codé en base 64** téléchargé à partir du portail Azure dans **bloc-notes**, copier le contenu de hello, puis collez-le dans hello **certificat X.509** zone de texte.
   
    d.  Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Créer**.
 
### <a name="create-a-clicktime-test-user"></a>Créer un utilisateur de test ClickTime

Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à ClickTime, vous devez les configurer dans ClickTime.  
Dans les cas de hello de ClickTime, cette configuration est une tâche manuelle.

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre ClickTime utilisateur compte outil de création ou API fournie par ClickTime tooprovision comptes d’utilisateur Azure AD.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**
1. Connectez-vous à tooyour **ClickTime** client.
2. Dans la barre d’outils de hello en haut de hello, cliquez sur **société**, puis cliquez sur **personnes**.
   
    ![Personnes](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Personnes")
3. Cliquez sur **Add Person**.
   
    ![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")
4. Dans la section nouveau contact de hello, procédez hello comme suit :
   
    ![Personnes](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Personnes")
   
    a.  Bonjour **nom complet** zone de texte, tapez nom complet d’utilisateur comme **Britta Simon**. 
  
    b.  Bonjour **adresse de messagerie** par courrier électronique de type hello d’utilisateur de zone de texte, comme  **brittasimon@contoso.com** .
       
    > [!NOTE]
    > Si vous le souhaitez, vous pouvez définir des propriétés supplémentaires de l’objet person hello.
   
    c.  Cliquez sur **Enregistrer**.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooClickTime.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooClickTime, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **ClickTime**.

    ![Lien ClickTimne dans la liste des Applications hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque ClickTime hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour ClickTime application.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

