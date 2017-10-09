---
title: "Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le Service de sécurité Web Symantec (WSS)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d6e4d893-1f14-4522-ac20-0c73b18c72a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 9f02b3d4ce2073110c55af4b567b0e3b5a88404f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-symantec-web-security-service-wss"></a>Didacticiel : Intégration d’Azure Active Directory à Symantec Web Security Service (WSS)

Dans ce didacticiel, vous allez apprendre comment toointegrate votre Service de sécurité Web Symantec (WSS) compte avec votre compte Azure Active Directory (Azure AD) afin de WSS peut authentifier un utilisateur final configuré Bonjour Azure AD à l’aide de l’authentification SAML et appliquer l’utilisateur ou règles de stratégie de groupe.

Intégration de Service de sécurité Web Symantec (WSS) avec Azure AD offre hello avantages suivants :

- Gérez tous les utilisateurs finaux de hello et les groupes utilisés par votre compte WSS à partir de votre portail Azure AD. 

- Autoriser le hello fin utilisateurs tooauthenticate eux-mêmes dans WSS à l’aide de leurs informations d’identification Azure AD.

- Activer la mise en œuvre hello d’utilisateur et groupe de règles de stratégie de niveau définis dans votre compte WSS.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Symantec Security Service WSS (Web), vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un compte Symantec Web Security Service (WSS)

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un compte WSS est actuellement utilisé à des fins de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas le compte WSS qui est actuellement utilisé à des fins de production pour ce test, sauf si c’est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous allez configurer votre Azure AD tooenable unique authentification tooWSS à l’aide des informations d’identification de l’utilisateur final hello définies dans votre compte Azure AD.
scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’application de Service de sécurité Web Symantec (WSS) hello à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-symantec-web-security-service-wss-from-hello-gallery"></a>Ajout de Service de sécurité Web Symantec (WSS) à partir de la galerie de hello
intégration de hello tooconfigure de Symantec Security Service WSS (Web) dans Azure AD, vous devez tooadd Symantec Security Service WSS (Web) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Symantec Security Service WSS (Web) à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Symantec Web sécurité Service (WSS)**, sélectionnez **Symantec Web sécurité Service (WSS)** à partir du volet de résultats, puis sur **ajouter** hello tooadd de bouton application.

    ![Symantec Security Service WSS (Web) dans la liste des résultats hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD auprès de Symantec Web Security Service (WSS) avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Symantec Web sécurité Service (WSS) est tooa dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Symantec Security Service WSS (Web) doit toobe établie.

Dans Symantec Web sécurité Service (WSS), affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Symantec Security Service WSS (Web), vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test du Service de sécurité Web Symantec (WSS)](#create-a-symantec-web-security-service-wss-test-user)**  -toohave un équivalent de Britta Simon dans Symantec Security Service WSS (Web) qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Service de sécurité Web Symantec (WSS).

**tooconfigure Azure AD l’authentification unique avec Symantec Web sécurité Service (WSS), effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Symantec Web sécurité Service (WSS)** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_samlbase.png)

3. Sur hello **URL et le domaine de Service (WSS) de sécurité Web Symantec** section, effectuer hello comme suit :

    ![Informations d’authentification unique Domaine et URL Symantec Web Security Service (WSS)](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_url.png)

    a. Bonjour **identificateur** zone de texte, tapez l’URL hello :`https://saml.threatpulse.net:8443/saml/saml_realm`

    b. Bonjour **URL de réponse** zone de texte, tapez l’URL hello :`https://saml.threatpulse.net:8443/saml/saml_realm/bcsamlpost`

    > [!NOTE]
    > Veuillez contacter hello [équipe de support Client de Service de sécurité Web Symantec (WSS)](https://www.symantec.com/contact-us) si des valeurs hello hello **identificateur** et **URL de réponse** ne fonctionnent pas pour une raison quelconque.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-symantec-tutorial/tutorial_general_400.png)
    
6. tooconfigure l’authentification unique sur hello au niveau de Service de sécurité Web Symantec (WSS), consultez la documentation en ligne de toohello WSS. Hello téléchargé **Metadata XML** fichier devez toobe importé dans le portail WSS hello. Contact hello [équipe de support du Service de sécurité Web Symantec (WSS)](https://www.symantec.com/contact-us) si vous avez besoin d’assistance à la configuration de hello sur le portail WSS hello.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-symantec-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-symantec-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-symantec-web-security-service-wss-test-user"></a>Créer un utilisateur de test Symantec Web Security Service (WSS)

Dans cette section, vous créez un utilisateur appelé Britta Simon dans Symantec Web Security Service (WSS). nom d’utilisateur de fin correspondante Hello peut être créée manuellement dans le portail WSS hello ou vous pouvez attendre hello utilisateurs/groupes configurés dans le portail WSS toohello hello Azure AD toobe synchronisé après quelques minutes (environ 15 minutes). Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique. Hello adresse IP publique de machine hello utilisateur final, qui sera utilisé toobrowse des sites Web a également besoin toobe configuré dans le portail du Service de sécurité Web Symantec (WSS) hello.

> [!NOTE]
> Veuillez [cliquez ici](http://www.bing.com/search?q=my+ip+address&qs=AS&pq=my+ip+a&sc=8-7&cvid=29A720C95C78488CA3F9A6BA0B3F98C5&FORM=QBLH&sp=1) tooget votre machine de publique IPaddress.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSymantec sécurité Service WSS (Web).

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooSymantec Web sécurité Service (WSS), effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Symantec Web sécurité Service (WSS)**.

    ![lien de Service de sécurité Web Symantec (WSS) Hello dans la liste des Applications hello](./media/active-directory-saas-symantec-tutorial/tutorial_symantecwebsecurityservicewss_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous testerez fonctionnalité d’authentification unique hello maintenant que vous avez configuré votre toouse de compte WSS votre Azure AD pour l’authentification SAML.

Après avoir configuré votre trafic tooproxy de navigateur web tooWSS, lorsque vous ouvrez votre navigateur web et que vous essayez toobrowse tooa site, puis vous allez être redirigé toohello authentification Azure page. Entrez des informations d’identification de hello de l’utilisateur final de test hello qui a été configuré Bonjour Azure AD (autrement dit, BrittaSimon) et le mot de passe correspondant. Une fois authentifié, vous serez en mesure de toobrowse toohello site que vous avez choisi. Devez-vous créer une règle de stratégie sur hello WSS côté tooblock BrittaSimon de parcourir le site particulier de tooa puis de la page de bloc WSS hello doit s’afficher lorsque vous essayez de toobrowse toothat site en tant qu’utilisateur BrittaSimon.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-symantec-tutorial/tutorial_general_203.png

