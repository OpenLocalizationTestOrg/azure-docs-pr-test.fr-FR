---
title: "Didacticiel : Intégration d’Azure Active Directory à Confluence SAML SSO by Microsoft | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’authentification unique SAML de Confluence par Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: ace23800e3908c8125052b4a2edcaae71f19935d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a>Didacticiel : Intégration d’Azure Active Directory à Confluence SAML SSO by Microsoft

Dans ce didacticiel, vous apprendrez comment toointegrate SSO SAML de Confluence par Microsoft avec Azure Active Directory (Azure AD).

Intégration de l’authentification unique SAML de Confluence par Microsoft à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooConfluence SSO SAML par Microsoft
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooConfluence SSO SAML par Microsoft (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec l’authentification unique SAML de Confluence par Microsoft, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Application de serveur confluence installée sur un serveur Windows 64 bits (localement ou sur le cloud hello IaaS infrastructure)
- L’activation du HTTPS dans le serveur
- Remarque hello pris en charge les versions du plug-in Confluence sont mentionnées dans section.
- Serveur de confluence est accessible sur internet particulièrement tooAzure page de connexion d’Active Directory pour l’authentification et doit en mesure de tooreceive hello jeton d’Azure AD
- La création d’informations d’identification administrateur dans Confluence
- La désactivation de WebSudo dans Confluence
- Utilisateur créé dans hello application de serveur Confluence de test

> [!NOTE]
> les étapes tootest hello dans ce didacticiel, nous déconseillons à l’aide d’un environnement de production confluence. Tester l’intégration hello d’abord dans le développement ou l’environnement d’application hello, puis utilisez hello production environnement de mise en lots.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de [l’offre d’essai](https://azure.microsoft.com/pricing/free-trial/) d’une durée d’un mois.

## <a name="supported-versions-of-confluence"></a>Versions de Confluence prises en charge 

Les versions suivantes de Confluence sont actuellement prises en charge :

- Confluence : too5.10 5.0

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de l’authentification unique SAML de Confluence par Microsoft à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-confluence-saml-sso-by-microsoft-from-hello-gallery"></a>Ajout de l’authentification unique SAML de Confluence par Microsoft à partir de la galerie de hello
tooconfigure hello intégration de l’authentification unique SAML de Confluence par Microsoft dans Azure AD, vous devez tooadd SSO SAML de Confluence par Microsoft à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd SSO SAML de Confluence par Microsoft à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **SSO SAML de Confluence par Microsoft**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. Dans le volet de résultats hello, sélectionnez **SSO SAML de Confluence par Microsoft**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Confluence SAML SSO by Microsoft, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans l’authentification unique SAML de Confluence par Microsoft est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans l’authentification unique SAML de Confluence par Microsoft hello doit toobe établie.

Dans l’authentification unique SAML Confluence par Microsoft, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec l’authentification unique SAML de Confluence par Microsoft, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’une authentification unique SAML de Confluence par l’utilisateur de test Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)**  -toohave un équivalent de Britta Simon dans l’authentification unique SAML de Confluence par Microsoft, qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre authentification unique SAML de Confluence par application de Microsoft.

**tooconfigure Azure AD l’authentification unique avec l’authentification unique SAML de Confluence par Microsoft, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **SSO SAML de Confluence par Microsoft** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. Sur hello **SSO SAML de Confluence par domaine Microsoft et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<domain:port>/plugins/servlet/saml/auth`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<domain:port>/`

    c. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<domain:port>/plugins/servlet/saml/auth`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. Le port est facultatif s’il s’agit d’une URL nommée. Ces valeurs sont reçus pendant la configuration hello du plug-in Confluence, qui est expliquée plus loin dans le didacticiel de hello.
 

4. toogenerate hello **métadonnées** url, effectuer hello comme suit :

    a. Cliquez sur **Inscriptions des applications**.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    b. Cliquez sur **points de terminaison** tooopen **points de terminaison** boîte de dialogue.  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    c. Cliquez sur hello copie bouton toocopy **DOCUMENT de métadonnées de fédération** url et collez-le dans le bloc-notes.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    d. Maintenant accédez toohello page de propriétés de **SSO SAML de Confluence par Microsoft** et copie Bonjour **Id d’Application** à l’aide de **copie** bouton et collez-le dans le bloc-notes.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    e. Générer hello **URL de métadonnées** à l’aide de hello modèle : `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` et copiez cette valeur dans le bloc-notes, tel qu’il est utilisé ultérieurement pour la configuration de hello du plug-in hello.

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. Contact [Microsoft](mailto:waadpartners@microsoft.com) avec hello informations pour le plug-in de hello Confluence suivantes.
    
    *   Nom du client :
    *   Nom du domaine principal :
    *   Azure AD Premium : Oui/non (plug-in sera disponible tooall client de hello gratuit, Basic et Premium SKU)
    *   Nombre d’utilisateurs qui vont utiliser cette intégration :
    *   Version de Confluence :
    *   Commentaires :

7. Dans une fenêtre de navigateur web, ouvrez une session dans l’instance de Confluence tooyour en tant qu’administrateur.

8. Pointez sur représentant une roue dentée et cliquez sur hello **modules complémentaires**.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. Sous l’onglet Add-ons (Modules complémentaires), cliquez sur **Manage add-ons** (Gérer les modules complémentaires).

    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. Charger manuellement les plug-in hello fourni par Microsoft. Une fois que le plug-in hello est installé, il apparaît dans **utilisateur installé** section modules complémentaires de **gérer le module complémentaire** section.

11. Cliquez sur **configurer** tooconfigure hello nouveau plug-in.

12. Effectuez les opérations suivantes dans la page de configuration :

    ![Configurer l’authentification unique](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    a. Dans **URL de métadonnées** coller hello **URL de métadonnées** généré à partir d’Azure AD et cliquez sur hello **résoudre** bouton. Il lit les URL des métadonnées IdP hello et remplit toutes les informations de champs hello.

    > [!Note]
    > Par défaut, l’emplacement de l’identificateur d’utilisateur SAML est défini sur l’élément NameIdentifier. Vous pouvez modifier cette option d’attribut tooan et entrez le nom de l’attribut approprié hello.

    > [!TIP]
    > Vérifiez qu’un seul certificat mappé par rapport à l’application hello afin qu’il n’existe aucune erreur dans la résolution des métadonnées de hello. S’il existe plusieurs certificats, lors de la résolution des métadonnées de hello, admin Obtient une erreur.
    
    b. Hello de copie **identificateur, URL de réponse et l’URL de connexion** les valeurs et les coller dans **identificateur, URL de réponse et l’URL de connexion** zones de texte respectivement dans **SSO SAML de Confluence par domaine Microsoft et les URL**  section sur le portail Azure.

    c. Dans **nom de bouton de connexion** nom de type hello du bouton de votre organisation souhaite toosee des utilisateurs hello sur l’écran de connexion.

    d. Dans **les emplacements des ID utilisateur SAML** sélectionnez **ID d’utilisateur est dans l’élément NameIdentifier de hello Hello Subject statement** ou **ID utilisateur est dans un élément Attribute**.  Cet ID a un id d’utilisateur Confluence toobe hello. Si l’id d’utilisateur hello n’est pas mis en correspondance, système ne permet pas de toolog d’utilisateurs dans. 
    
    e. Si vous sélectionnez **ID utilisateur est dans un élément Attribute** option, puis dans **nom de l’attribut** nom de hello de type zone de texte d’attribut hello lorsque l’Id d’utilisateur est attendu. 

    f. Si vous utilisez un domaine fédéré de hello (par exemple, ADFS, etc.) auprès d’Azure AD, puis cliquez sur hello **activer la découverte de domaine d’accueil** option et configurer hello **nom de domaine**.
    
    g. Dans **nom de domaine** hello domaine nom de type ici en cas de connexion de base de ADFS hello.

    h. Vérifiez **activer la déconnexion unique** si vous souhaitez toolog out d’Azure AD quand un utilisateur se déconnecte de Confluence. 

    i. Cliquez sur **enregistrer** bouton Paramètres de hello toosave.


> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a>Création d’un utilisateur de test Confluence SAML SSO by Microsoft

tooenable Azure AD les utilisateurs toolog dans tooConfluence sur le serveur local, ils doivent être configurés dans Confluence SAML SSO par Microsoft. Pour Confluence SAML SSO by Microsoft, l’attribution des utilisateurs se fait manuellement.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Ouvrez une session dans tooyour Confluence sur le serveur local en tant qu’administrateur.

2. Pointez sur représentant une roue dentée et cliquez sur hello **gestion des utilisateurs**.

    ![Ajouter un employé](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. Dans la section Utilisateurs, cliquez sur l’onglet **Add users** (Ajouter des utilisateurs). Sur hello **« Ajouter un utilisateur »** boîte de dialogue de page, effectuer hello comme suit :

    ![Ajouter un employé](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    a. Bonjour **nom d’utilisateur** zone de texte, par courrier électronique de type hello d’utilisateur comme Britta Simon.

    b. Bonjour **nom complet** zone de texte, nom complet de type hello d’utilisateur comme Britta Simon.

    c. Bonjour **messagerie** adresse de messagerie de type hello d’utilisateur de zone de texte, comme Brittasimon@contoso.com.

    d. Bonjour **mot de passe** zone de texte, type hello mot de passe Britta Simon.

    e. Cliquez sur **confirmer le mot de passe** entrer à nouveau le mot de passe hello.
    
    f. Cliquez sur le bouton **Ajouter**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooConfluence SSO SAML par Microsoft.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooConfluence SSO SAML par Microsoft, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **SSO SAML de Confluence par Microsoft**.

    ![Configurer l’authentification unique](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello Confluence SAML SSO par vignette Microsoft Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Confluence SAML SSO par application de Microsoft.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

