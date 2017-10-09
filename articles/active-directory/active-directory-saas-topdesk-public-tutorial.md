---
title: "Didacticiel : Intégration d’Azure Active Directory avec TOPdesk - Public | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de TOPdesk - Public."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0873299f-ce70-457b-addc-e57c5801275f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ef0dd06157ecc3b33814590039f5cbae64e8c916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---public"></a>Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Public

Dans ce didacticiel, vous apprendrez comment toointegrate TOPdesk - Public avec Azure Active Directory (Azure AD).

Intégration de TOPdesk - Public auprès d’Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooTOPdesk - Public.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTOPdesk - Public (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à TOPdesk - Public, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement TOPdesk - Public pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de TOPdesk - Public à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-topdesk---public-from-hello-gallery"></a>Ajout de TOPdesk - Public à partir de la galerie de hello
intégration de hello tooconfigure de TOPdesk - Public dans Azure AD, vous devez tooadd TOPdesk - Public à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd TOPdesk - Public à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **TOPdesk - Public**, sélectionnez **TOPdesk - Public** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Liste des résultats de TOPdesk - Public Bonjour](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec TOPdesk - Public avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans TOPdesk - Public est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans TOPdesk - Public doit toobe établie.

Dans TOPdesk - Public, attribuer une valeur hello Hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et tester Azure AD single sign-on avec TOPdesk - Public, que vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un TOPdesk - Public test utilisateur](#create-a-topdesk---public-test-user)**  - toohave un équivalent de Britta Simon dans TOPdesk - Public qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application TOPdesk - Public.

**tooconfigure Azure AD l’authentification unique à TOPdesk - Public, effectuer hello comme suit :**

1. Bonjour portail Azure, sur hello **TOPdesk - Public** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_samlbase.png)

3. Sur hello **TOPdesk - URL et du domaine Public** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.topdesk.net`
    
    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.topdesk.net/tas/public/login/verify`

    c. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.topdesk.net/tas/public/login/saml`
     
    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. L’URL de réponse est expliquée plus loin dans le didacticiel. Contact [TOPdesk - équipe de support Client Public](https://help.topdesk.com/saas/enterprise/user/) tooget ces valeurs.  

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_400.png)
    
6. Sur hello **TOPdesk - Public Configuration** , cliquez sur **configurer TOPdesk - Public** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration de TOPdesk - Public](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_configure.png) 

7. Ouverture de session tooyour **TOPdesk - Public** site d’entreprise en tant qu’administrateur.

8. Bonjour **TOPdesk** menu, cliquez sur **paramètres**.
   
    ![Paramètres](./media/active-directory-saas-topdesk-public-tutorial/ic790598.png "Paramètres")

9. Cliquez sur **Login Settings**.
   
    ![Paramètres de connexion](./media/active-directory-saas-topdesk-public-tutorial/ic790599.png "Paramètres de connexion")

10. Développez hello **les paramètres de connexion** menu, puis sur **général**.
   
    ![Général](./media/active-directory-saas-topdesk-public-tutorial/ic790600.png "Général")

11. Bonjour **Public** section Hello **connexion SAML** configuration section, effectuer hello comme suit :
   
    ![Paramètres techniques](./media/active-directory-saas-topdesk-public-tutorial/ic790601.png "Paramètres techniques")
   
    a. Cliquez sur **télécharger** toodownload hello du fichier de métadonnées publiques et les enregistrer localement sur votre ordinateur.
   
    b. Ouvrez le fichier de métadonnées hello téléchargé et recherchez hello **AssertionConsumerService** nœud.

    ![AssertionConsumerService](./media/active-directory-saas-topdesk-public-tutorial/ic790619.png "AssertionConsumerService")
   
    c. Hello de copie **AssertionConsumerService** valeur, collez cette valeur Bonjour **URL de réponse** zone de texte dans **TOPdesk - URL et du domaine Public** section.      
   
12. toocreate un fichier de certificat, effectuez hello comme suit :
    
    ![Certificat](./media/active-directory-saas-topdesk-public-tutorial/ic790606.png "Certificat")
    
    a. Hello ouvrir téléchargé le fichier de métadonnées à partir du portail Azure.
    
    b. Développez hello **RoleDescriptor** nœud qui a un **xsi : type** de **fed : ApplicationServiceType**.
    
    c. Copier la valeur hello Hello **X509Certificate** nœud.
    
    d. Hello enregistrer copié **X509Certificate** valeur localement sur votre ordinateur dans un fichier.

13. Bonjour **Public** , cliquez sur **ajouter**.
    
    ![Connexion SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790625.png "Connexion SAML")

14. Sur hello **l’assistant configuration de SAML** boîte de dialogue de page, effectuer hello comme suit :
    
    ![Assistant de configuration SAML](./media/active-directory-saas-topdesk-public-tutorial/ic790608.png "Assistant de configuration SAML")
    
    a. tooupload vos métadonnées téléchargée de fichiers à partir du portail Azure, sous **les métadonnées de fédération**, cliquez sur **Parcourir**.

    b. tooupload fichier de votre certificat, sous **Certificate (RSA)**, cliquez sur **Parcourir**.

    c. fichier de logo hello tooupload que vous avez obtenu à partir de l’équipe de support technique TOPdesk hello sous **icône du Logo**, cliquez sur **Parcourir**.

    d. Bonjour **attribut nom d’utilisateur** zone de texte, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.

    e. Bonjour **nom d’affichage** zone de texte, tapez un nom pour votre configuration.

    f. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-topdesk-public-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-topdesk---public-test-user"></a>Créer un utilisateur de test TOPdesk - Public

Dans l’ordre tooenable Azure AD les utilisateurs toolog à TOPdesk - Public, vous devez les configurer dans TOPdesk - Public.  
Dans le cas de hello de TOPdesk - Public, cette configuration est une tâche manuelle.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>configuration, de l’utilisateur tooconfigure effectuer hello comme suit :
1. Ouverture de session tooyour **TOPdesk - Public** site d’entreprise en tant qu’administrateur.

2. Dans le menu hello haut de hello, cliquez sur **TOPdesk \> nouveau \> les fichiers de prise en charge \> personne**.
   
    ![Personne](./media/active-directory-saas-topdesk-public-tutorial/ic790628.png "Personne")

3. Dans la boîte de dialogue nouvelle personne hello, procédez hello comme suit :
   
    ![Nouvelle personne](./media/active-directory-saas-topdesk-public-tutorial/ic790629.png "Nouvelle personne")
   
    a. Cliquez sur Général hello.

    b. Bonjour **Surname** zone de texte, tapez le nom d’utilisateur hello comme Simon
 
    c. Sélectionnez un **Site** pour le compte de hello.
 
    d. Cliquez sur **Enregistrer**.

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre TOPdesk - outil de création de compte utilisateur publique ou une autre API fournies par TOPdesk - Public tooprovision Azure AD des comptes d’utilisateur.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTOPdesk - Public.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooTOPdesk - Public, effectuer hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **TOPdesk - Public**.

    ![Hello TOPdesk - Public de lien dans la liste des Applications hello](./media/active-directory-saas-topdesk-public-tutorial/tutorial_topdesk-public_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello TOPdesk - Public vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour TOPdesk - Public application.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-topdesk-public-tutorial/tutorial_general_203.png

