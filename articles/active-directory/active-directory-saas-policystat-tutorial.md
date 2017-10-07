---
title: "Didacticiel : Intégration d’Azure Active Directory avec PolicyStat | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 868053cd0d37359fd9b4aeb93dba42cbbaa09845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a>Didacticiel : Intégration d’Azure Active Directory avec PolicyStat

Dans ce didacticiel, vous apprendrez comment toointegrate PolicyStat avec Azure Active Directory (Azure AD).

Intégration PolicyStat à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooPolicyStat
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPolicyStat (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec PolicyStat, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement PolicyStat pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de PolicyStat à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-policystat-from-hello-gallery"></a>Ajout de PolicyStat à partir de la galerie de hello
intégration de hello tooconfigure de PolicyStat dans Azure AD, vous devez tooadd PolicyStat à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd PolicyStat à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **PolicyStat**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. Dans le volet de résultats hello, sélectionnez **PolicyStat**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PolicyStat sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans PolicyStat est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans PolicyStat doit toobe établie.

Dans PolicyStat, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec PolicyStat, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test PolicyStat](#creating-a-policystat-test-user)**  -toohave un équivalent de Britta Simon dans PolicyStat est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application PolicyStat.

**tooconfigure Azure AD single sign-on avec PolicyStat, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **PolicyStat** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. Sur hello **PolicyStat domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.policystat.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.policystat.com/saml2/metadata/`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur. Contact [équipe de support Client de PolicyStat](http://www.policystat.com/support/) tooget ces valeurs. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooPolicyStat avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.

    Hello PolicyStat application attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton SAML** configuration.  

     Hello suivant capture d’écran montre un exemple de cela.

     ![Attributs](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributs")

6. mappages d’attributs tooadd hello requis, effectuez hello comme suit :

    | Nom de l'attribut    |   Valeur de l’attribut |
    |------------------- | -------------------- |
    | uid | ExtractMailPrefix([mail]) |
    
    a. Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    b. Bonjour **nom de l’attribut** zone de texte, type **uid**.

    c. Bonjour **valeur d’attribut** zone de texte, sélectionnez **ExtractMailPrefix()**.    
   
    d. À partir de hello **Mail** liste, sélectionnez **User.mail**.
    
    e. Cliquez sur **OK**.

7. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise PolicyStat en tant qu’administrateur.

9. Cliquez sur hello **Admin** onglet, puis cliquez sur **Configuration de l’authentification unique** dans le volet de navigation gauche.
   
    ![Menu administrateur](./media/active-directory-saas-policystat-tutorial/ic808633.png "Menu administrateur")

10. Bonjour **le programme d’installation** section, sélectionnez **activer l’authentification intégration de l’unique**.
   
    ![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808634.png "Configuration de l’authentification unique")

11. Cliquez sur **configurer les attributs**, puis, dans hello **configurer les attributs** section, effectuer hello comme suit :
   
    ![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808635.png "Configuration de l’authentification unique")
   
    a. Bonjour **attribut Username** zone de texte, type **uid**.

    b. Bonjour **prénom attribut** zone de texte, type **firstname** d’utilisateur **Brian**.

    c. Bonjour **attribut de nom** zone de texte, type **lastname** d’utilisateur **Simon**.

    d. Bonjour **attribut Email** zone de texte, type **emailaddress** d’utilisateur  **BrittaSimon@contoso.com** .

    e. Cliquez sur **Enregistrer les modifications**.

12. Cliquez sur **votre IDP Metadata**, puis, dans hello **votre IDP Metadata** section, effectuer hello comme suit :
   
    ![Configuration de l’authentification unique](./media/active-directory-saas-policystat-tutorial/ic808636.png "Configuration de l’authentification unique")
   
    a. Ouvrez votre fichier de métadonnées téléchargé, les hello copie contenu, puis collez-le dans hello **vos métadonnées du fournisseur d’identité** zone de texte.

    b. Cliquez sur **Enregistrer les modifications**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-policystat-test-user"></a>Création d’un utilisateur de test PolicyStat

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans PolicyStat, ils doivent être configurés dans PolicyStat.  

PolicyStat prend en charge l’approvisionnement juste-à-temps des utilisateurs. Cela signifie, vous ne devez pas manuellement les utilisateurs de hello tooadd tooPolicyStat. les utilisateurs de Hello seront ajoutés automatiquement lors de leur première connexion via l’authentification unique.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre PolicyStat utilisateur compte outil de création ou API fournie par PolicyStat tooprovision comptes d’utilisateur Azure AD.
> 

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPolicyStat.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooPolicyStat, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **PolicyStat**.

    ![Configurer l’authentification unique](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque PolicyStat hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour PolicyStat application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

