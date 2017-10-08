---
title: "Didacticiel : intégration d’Azure Active Directory à Google Apps dans Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a>Didacticiel : Intégration d’Azure Active Directory à Google Apps

Dans ce didacticiel, vous apprendrez comment toointegrate Google Apps avec Azure Active Directory (Azure AD).

Intégration de Google Apps à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooGoogle applications
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooGoogle (Single Sign-On), les applications avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus d’informations sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Google Apps, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Google pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de l’essai d’un mois ici : [Offre d’essai](https://azure.microsoft.com/pricing/free-trial/).

## <a name="video-tutorial"></a>Didacticiel vidéo
Comment tooEnable Single Sign-On tooGoogle des applications dans les 2 Minutes :

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a>Forum Aux Questions (FAQ)
1. **Q : Les Chromebooks et les autres appareils Chrome sont-ils compatibles avec l’authentification unique Azure AD ?**
   
    R : Oui, les utilisateurs sont en mesure de toosign dans leurs appareils Chromebook à l’aide de leurs informations d’identification Azure AD. Consultez cet [article du support technique Google Apps](https://support.google.com/chrome/a/answer/6060880) pour en savoir plus sur les raisons de la double demande de saisie des informations d’identification.

2. **Q : si j’activer l’authentification unique, les utilisateurs de s’être toouse en mesure de leur toosign d’informations d’identification Azure AD dans tous les produits Google, telles que la classe de Google, GMail, Google Drive, YouTube et ainsi de suite ?**
   
    R : Oui, en fonction de [les applications de Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) vous choisissez tooenable ou désactiver pour votre organisation.

3. **Q : Puis-je activer l’authentification unique pour uniquement un sous-ensemble de mes utilisateurs Google Apps ?**
   
    R : non, activer l’authentification unique sur immédiatement nécessite tous les votre tooauthenticate d’utilisateurs de Google Apps avec leurs informations d’identification Azure AD. Étant donné que Google Apps ne prend en charge plusieurs fournisseurs d’identité, le fournisseur d’identité pour votre environnement de Google Apps hello peut être Azure AD ou Google--mais pas les deux à hello même temps.

4. **Q : si un utilisateur est connecté via Windows, sont qu'elles authentifient automatiquement les applications tooGoogle sans mise en route invité à entrer un mot de passe ?**
   
    R : Ce scénario peut être activé par le biais de deux options. Tout d’abord, les utilisateurs peuvent se connecter aux appareils Windows 10 via [Azure Active Directory Join](active-directory-azureadjoin-overview.md). Vous pouvez également les utilisateurs pourraient s’appareils Windows, qui sont joints au domaine de tooan locale Active Directory qui a été activé pour une seule session tooAzure AD via un [les Services de fédération Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) déploiement. Les deux options nécessitent un tooperform les étapes de hello Bonjour suivant didacticiel tooenable l’authentification unique entre Azure AD et Google Apps.

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Google Apps à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-google-apps-from-hello-gallery"></a>Ajout de Google Apps à partir de la galerie de hello
tooconfigure hello intégration de Google Apps dans Azure AD, vous devez tooadd Google Apps à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Google Apps à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Google Apps**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. Dans le volet de résultats hello, sélectionnez **Google Apps**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, configurez et testez l’authentification unique Azure AD avec Google Apps sur un utilisateur test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Google Apps est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Google Apps doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Google Apps.

tooconfigure et test Azure AD l’authentification unique avec Google Apps, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Google Apps](#creating-a-google-apps-test-user)**  -toohave un équivalent de Britta Simon dans Google Apps qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Google Apps.

**tooconfigure Azure AD single sign-on avec Google Apps, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Google Apps** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. Sur hello **URL et le domaine Google Apps** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://mail.google.com/a/<yourdomain>`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour la valeur de hello avec l’URL de connexion réel hello. Contactez hello [équipe de support technique de Google](https://www.google.com/contact/).
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **certificat** , puis enregistrez le certificat de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. Sur hello **Google Apps Configuration** , cliquez sur **configurer Google Apps** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, SAML Sign-On URL du Service unique et modifier une URL de mot de passe** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à hello [Google Apps Admin Console](http://admin.google.com/) à l’aide de votre compte d’administrateur.

8. Cliquez sur **Security**. Si vous ne voyez pas le lien de hello, il peut être masquée sous hello **plus de contrôles** menu bas hello écran hello.
   
    ![Cliquez sur Sécurité.][10]

9. Sur hello **sécurité** , cliquez sur **configurer l’authentification unique (SSO).**
   
    ![Cliquez sur Authentification unique.][11]

10. Effectuez hello les modifications de configuration suivantes :
   
    ![Configurer l’authentification unique][12]
   
    a. Sélectionnez **Configurer l'authentification unique avec un fournisseur d'identité tiers**.

    b. Dans le **URL de la page connexion** champ dans Google Apps, collez la valeur hello **unique Sign-On URL du Service**, lequel vous avez copié à partir du portail Azure.

    c. Bonjour **URL de la page de déconnexion** champ dans Google Apps, collez la valeur hello **URL de déconnexion**, lequel vous avez copié à partir du portail Azure. 

    d. Bonjour **modifier l’URL de mot de passe** champ dans Google Apps, collez la valeur hello **modifier l’URL de mot de passe**, lequel vous avez copié à partir du portail Azure. 

    e. Dans Google Apps, pourquoi **certificat de vérification**, télécharger le certificat hello que vous avez téléchargé à partir du portail Azure.

    f. Cliquez sur **Enregistrer les modifications**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-google-apps-test-user"></a>Création d’un utilisateur de test Google Apps

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Google Apps logiciel. Google Apps prend en charge l’approvisionnement automatique, qui est activé par défaut. Vous n’avez aucune opération à effectuer dans cette section. Si un utilisateur n’existe pas déjà dans Google Apps logiciel, un nouveau est créé lorsque vous essayez de tooaccess logiciel des applications de Google.

>[!NOTE] 
>Si vous avez besoin de toocreate un utilisateur manuellement, contactez hello [équipe de support technique de Google](https://www.google.com/contact/).

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès à des applications de tooGoogle.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooGoogle applications, effectuer hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Google Apps**.

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, tootest votre seule paramètres d’authentification, ouvrez hello volet d’accès au [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), puis connectez-vous à un compte de test hello, puis cliquez sur **Google Apps** vignette Bonjour panneau d’accès.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)
* [Configurer l’approvisionnement de l’utilisateur](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png