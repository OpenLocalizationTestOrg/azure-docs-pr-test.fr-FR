---
title: "Didacticiel : intégration d’Azure Active Directory à SkyDesk Email | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et par courrier électronique SkyDesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a9d0bbcb-ddb5-473f-a4aa-028ae88ced1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: 19c670a60f581a2be55b74eacdb5393a36e38be3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skydesk-email"></a>Didacticiel : Intégration d’Azure Active Directory à SkyDesk Email

Dans ce didacticiel, vous apprendrez comment envoyer par courrier électronique SkyDesk toointegrate avec Azure Active Directory (Azure AD).

Intégration SkyDesk E-mail à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSkyDesk par courrier électronique
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSkyDesk par courrier électronique (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec SkyDesk adresse de messagerie, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement SkyDesk Email pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici [Offre d’essai](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de SkyDesk messagerie à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-skydesk-email-from-hello-gallery"></a>Ajout de SkyDesk messagerie à partir de la galerie de hello
tooconfigure hello intégration des messages électroniques de SkyDesk dans Azure AD, vous devez tooadd SkyDesk messagerie à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd messagerie SkyDesk à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **SkyDesk E-mail**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_search.png)

5. Dans le volet de résultats hello, sélectionnez **SkyDesk messagerie**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de SkyDesk Email, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello par courrier électronique SkyDesk est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur par courrier électronique SkyDesk hello doit toobe établie.

Courrier électronique SkyDesk, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec SkyDesk adresse de messagerie, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test par courrier électronique SkyDesk](#creating-a-skydesk-email-test-user)**  -toohave un équivalent de Britta Simon par courrier électronique SkyDesk qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de messagerie de SkyDesk.

**tooconfigure Azure AD authentification unique avec les E-mails SkyDesk effectuer hello comme suit :**

1. Bonjour portail Azure, sur hello **SkyDesk messagerie** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_samlbase.png)

3. Sur hello **URL et le domaine de messagerie SkyDesk** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_url.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://mail.skydesk.jp/portal/<companyname>`

    > [!NOTE] 
    > valeur de Hello n’est pas réelle. Valeur de hello de mise à jour avec hello URL de connexion réel. Contact [équipe de support Client de messagerie SkyDesk](https://www.skydesk.sg/support/) valeur hello de tooget. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_400.png)

6. Sur hello **Configuration des E-mails SkyDesk** , cliquez sur **configurer la messagerie de SkyDesk** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_configure.png) 

7. tooenable SSO dans **SkyDesk messagerie**, effectuer hello comme suit :

    a. Authentification tooyour SkyDesk courriel en tant qu’administrateur.

    b. Dans le menu hello haut de hello, cliquez sur **le programme d’installation**, puis sélectionnez **Org**. 
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_51.png)
  
    c. Cliquez sur **domaines** à partir du volet de gauche hello.
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_53.png)

    d. Cliquez sur **Add Domain**.
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_54.png)

    e. Entrez votre nom de domaine et vérifiez hello domaine.
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_55.png)

    f. Cliquez sur **l’authentification SAML** à partir du volet de gauche hello.
    
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_52.png)

8. Sur hello **l’authentification SAML** boîte de dialogue de page, effectuer hello comme suit :
   
      ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_56.png)
   
    >[!NOTE]
    >authentification basée sur les toouse SAML, vous devez avoir **vérifié domaine** ou **portail URL** le programme d’installation. Vous pouvez définir le portail de hello URL avec un nom unique hello.
    > 
    > 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_57.png)

    a. Bonjour **URL de connexion** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.
   
    b. Bonjour **déconnexion** zone de texte URL, valeur hello coller **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.

    c. **Modifier l’URL de mot de passe** est facultative, vous pouvez donc laisser cette valeur vide.

    d. Cliquez sur **obtenir une clé à partir du fichier** tooselect votre certificat téléchargé dans le portail Azure, puis cliquez sur **ouvrir** certificat de hello tooupload.

    e. Comme **Algorithme**, sélectionnez **RSA**.

    f. Cliquez sur **Ok** modifications de hello toosave.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-skydeskemail-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-skydesk-email-test-user"></a>Création d’un utilisateur de test SkyDesk Email

Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SkyDesk Email.

1. Cliquez sur **accès utilisateur** de hello gauche du panneau par courrier électronique SkyDesk et puis entrez votre nom d’utilisateur. 

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_58.png)

>[!NOTE] 
>Si vous avez besoin des utilisateurs en bloc de toocreate, vous devez toocontact hello [équipe de support Client de messagerie SkyDesk](https://www.skydesk.sg/support/).


### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSkyDesk par courrier électronique.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSkyDesk par courrier électronique, exécutez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **SkyDesk E-mail**.

    ![Configurer l’authentification unique](./media/active-directory-saas-skydeskemail-tutorial/tutorial_skydeskemail_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello SkyDesk messagerie vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur application de messagerie de SkyDesk tooyour.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skydeskemail-tutorial/tutorial_general_203.png

