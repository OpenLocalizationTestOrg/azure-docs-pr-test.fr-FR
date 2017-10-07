---
title: "Didacticiel : Intégration d’Azure Active Directory à ADP eTime | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a>Didacticiel : Intégration d’Azure AD à ADP eTime

Dans ce didacticiel, vous apprendrez comment eTime toointegrate ADP avec Azure Active Directory (Azure AD).

Intégration ADP eTime à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooADP eTime
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooADP eTime (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec ADP eTime, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement ADP eTime pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de ADP eTime à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-adp-etime-from-hello-gallery"></a>Ajout de ADP eTime à partir de la galerie de hello
tooconfigure hello intégration de ADP eTime dans Azure AD, vous devez eTime de ADP tooadd à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**eTime tooadd ADP à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **ADP eTime**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. Dans le volet de résultats hello, sélectionnez **ADP eTime**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ADP eTime, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello ADP eTime est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ADP eTime doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ADP eTime.

tooconfigure et test Azure AD l’authentification unique avec ADP eTime, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test eTime ADP](#creating-an-adp-etime-test-user)**  -toohave un homologue de Britta Simon dans eTime ADP qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application d’eTime ADP.

**tooconfigure Azure AD single sign-on avec ADP eTime, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **ADP eTime** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. Sur hello **ADP eTime domaine et les URL** section, effectuer hello suivant l’étape :

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.adp.com`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer` 
 
    > [!NOTE] 
    > Ces valeurs ne sont pas hello réel. Mettre à jour ces valeurs avec l’URL de réponse réelle hello et l’identificateur. Contact [équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx) tooget ces valeurs.

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. Hello application eTime de ADP attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages. Hello suivant capture d’écran montre un exemple de cela. Hello nom de la revendication sera toujours **« PersonImmutableID »** et valeur hello dont nous avons mappé tooExtensionAttribute2 contenant hello EmployeeID d’utilisateur de hello. 

    Mappage de l’utilisateur à partir d’Azure AD tooADP eTime hello est effectuée sur hello EmployeeID ici, mais vous pouvez mapper cette valeur différents tooa également en fonction de vos paramètres d’application. Veuillez travail avec [équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx) toouse premier hello identificateur correct d’un utilisateur et mapper cette valeur avec hello **« PersonImmutableID »** de revendication.

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue, configurer des attributs de jeton SAML comme indiqué dans l’image de hello et effectuer hello comme suit :
    
    | Nom de l'attribut | Valeur de l’attribut |
    | ------------------- | -------------------- |    
    | PersonImmutableID | user.extensionattribute2 |
    
    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    b. Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.

    c. À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.
    
    d. Cliquez sur **OK**.

    > [!NOTE] 
    > Avant de pouvoir configurer assertion SAML de hello, vous devez toocontact votre [équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx) et demander la valeur hello d’attribut d’identificateur unique hello pour votre client. Vous avez besoin de cette revendication personnalisée hello valeur tooconfigure pour votre application. 

7. Sur hello **ADP eTime Configuration** , cliquez sur **configurer un ADP eTime** tooopen **configurer l’authentification** fenêtre.

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. tooconfigure l’authentification unique sur **ADP eTime** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx). 

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-adp-etime-test-user"></a>Création d’un utilisateur test ADP eTime

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans ADP eTime. Travailler avec [équipe de support ADP eTime](https://www.adp.com/contact-us/overview.aspx) utilisateurs hello tooadd compte d’eTime hello ADP. 
   
### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooADP eTime.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooADP eTime, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **ADP eTime**.

    ![Configurer l’authentification unique](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque eTime hello ADP hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour ADP eTime application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

