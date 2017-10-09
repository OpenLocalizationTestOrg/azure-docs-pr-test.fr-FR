---
title: "Didacticiel : intégration d’Azure Active Directory à Tableau Server | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et le serveur du Tableau."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c1917375-08aa-445c-a444-e22e23fa19e0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: feb2087bd6ae6ddcb920901e6719688fc95ae287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tableau-server"></a>Didacticiel : Intégration d’Azure Active Directory à Tableau Server

Dans ce didacticiel, vous apprendrez comment toointegrate Server Tableau avec Azure Active Directory (Azure AD).

Intégration du serveur du Tableau à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooTableau Server
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooTableau Server (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec le serveur du Tableau, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Tableau Server pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout du serveur de Tableau à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-tableau-server-from-hello-gallery"></a>Ajout du serveur de Tableau à partir de la galerie de hello
tooconfigure hello intégration du serveur du Tableau dans Azure AD, vous devez tooadd serveur du Tableau à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd serveur du Tableau à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Tableau Server**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_search.png)

5. Dans le volet de résultats hello, sélectionnez **Tableau Server**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Tableau Server grâce à un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le serveur du Tableau est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le Tableau serveur hello doit toobe établie.

Dans le serveur du Tableau, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec le serveur du Tableau, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test du serveur du Tableau](#creating-a-tableau-server-test-user)**  -toohave un équivalent de Britta Simon dans le serveur de Tableau qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de serveur du Tableau.

**tooconfigure Azure AD-authentification avec le serveur du Tableau, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Tableau Server** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_samlbase.png)

3. Sur hello **URL et le domaine du serveur Tableau** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://azure.<domain name>.link`
    
    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://azure.<domain name>.link`

    c. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://azure.<domain name>.link/wg/saml/SSO/index.html`
     
    > [!NOTE] 
    > Hello valeurs précédentes ne sont pas des valeurs réelles. Une version ultérieure, mise à jour les valeurs hello avec URL réelle de hello et l’identificateur de la page de configuration du serveur du Tableau hello. 

4. Application de serveur de tableau attend les assertions SAML hello dans un format spécifique. Configurer hello suivant des revendications pour cette application. Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Attributs utilisateur »** section sur la page d’intégration d’application. Hello capture d’écran suivante montre un exemple de hello même.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/3.png)
    
5. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image ci-dessus hello et effectuer hello comme suit :
    
    | Nom de l'attribut | Valeur de l’attribut |
    | ---------------| --------------- |    
    | username | *user.displayname* |

    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_officespace_05.png)
    
    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.
    
    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.
    
    d. Cliquez sur **OK**.


6. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_certificate.png) 

7. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_general_400.png)
<CS>
8. tooget SSO configuré pour votre application, vous devez tooyour toosign sur les clients de serveur du Tableau en tant qu’administrateur.
   
   a. Dans la configuration du serveur du Tableau hello, cliquez sur hello **SAML** onglet.
  
    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_001.png) 
  
   b. Sélectionnez la case à cocher hello de **SAML d’utilisation pour l’authentification unique sur**.
   
   c. URL de renvoi du serveur du tableau : hello URL serveur du Tableau utilisateurs accéderont à, telles que http://tableau_server. L’utilisation de l’URL http://localhost n’est pas recommandée. L’utilisation d’une URL avec une barre oblique finale (par exemple, http://tableau_server/) n’est pas prise en charge. Copie **URL de renvoi du serveur du Tableau** et collez-le tooAzure AD **URL de connexion** zone de texte dans **URL et le domaine du serveur Tableau** section.
   
   d. ID d’entité SAML : ID d’entité hello identifie de façon unique votre toohello d’installation de serveur du Tableau IdP. Vous pouvez entrer l’URL du serveur Tableau à nouveau ici, si vous le souhaitez, mais il n’a pas toobe URL du serveur de votre Tableau. Copie **ID d’entité SAML** et collez-le tooAzure AD **identificateur** zone de texte dans **URL et le domaine du serveur Tableau** section.
     
   e. Cliquez sur hello **exporter le fichier de métadonnées** et ouvrez-le dans l’application de l’éditeur de texte hello. Localiser des URL de Service de consommateur Assertion avec Http Post et Index 0 et copier l’URL hello. Maintenant collez-le tooAzure AD **URL de réponse** zone de texte dans **URL et le domaine du serveur Tableau** section.
   
   f. Rechercher le fichier de métadonnées de fédération téléchargé à partir du portail Azure, puis le télécharger dans hello **fichier de métadonnées de fournisseur d’identité SAML**.
   
   g. Cliquez sur hello **OK** bouton dans la page de Configuration du serveur Tableau hello.
   
    >[!NOTE] 
    >Client ont tooupload n’importe quel certificat dans la configuration de l’authentification unique SAML de Tableau serveur hello et sera obtenir ignoré Bonjour flux d’authentification unique.
    >Si vous avez besoin d’aide configuration SAML sur le serveur du Tableau, consultez l’article de toothis [SAML de configurer](http://onlinehelp.tableau.com/current/server/en-us/config_saml.htm).
    >
<CE>

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-tableauserver-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-tableau-server-test-user"></a>Création d’un utilisateur de test Tableau Server

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans le serveur du Tableau. Vous devez tooprovision tous les utilisateurs de hello du serveur du Tableau hello. 

Ce nom d’utilisateur de l’utilisateur de hello doit correspondre à valeur hello que vous avez configurée dans l’attribut personnalisé de hello Azure AD de **nom d’utilisateur**. Avec hello correct de mappage de l’intégration hello doit fonctionner [configuration Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).

>[!NOTE]
>Si vous devez manuellement toocreate un utilisateur, vous avez besoin d’administrateur de serveur du Tableau toocontact hello dans votre organisation.
> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooTableau Server.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooTableau Server, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Tableau Server**.

    ![Configurer l’authentification unique](./media/active-directory-saas-tableauserver-tutorial/tutorial_tableauserver_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur vignette de Tableau serveur hello Bonjour volet d’accès, vous devez obtenir l’application de serveur du Tableau tooyour automatiquement signé sur.
Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tableauserver-tutorial/tutorial_general_203.png

