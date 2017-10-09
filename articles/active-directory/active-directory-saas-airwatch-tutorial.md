---
title: "Didacticiel : Intégration d’Azure Active Directory à AirWatch | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et AirWatch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 96a3bb1c-96c6-40dc-8ea0-060b0c2a62e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e5230d5a36824778a4d9804dadf9f13a0d11a68d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-airwatch"></a>Didacticiel : Intégration d’Azure Active Directory à AirWatch

Dans ce didacticiel, vous apprendrez comment toointegrate AirWatch avec Azure Active Directory (Azure AD).

Intégration d’AirWatch à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAirWatch
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAirWatch (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à AirWatch, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement AirWatch pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout d’AirWatch à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-airwatch-from-hello-gallery"></a>Ajout d’AirWatch à partir de la galerie de hello
intégration de hello tooconfigure d’AirWatch dans Azure AD, vous devez tooadd AirWatch à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd AirWatch à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **AirWatch**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_search.png)

5. Dans le volet de résultats hello, sélectionnez **AirWatch**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec AirWatch, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans AirWatch est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans AirWatch doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans AirWatch.

tooconfigure et test Azure AD l’authentification unique avec AirWatch, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test AirWatch](#creating-a-airwatch-test-user)**  -toohave un équivalent de Britta Simon dans AirWatch est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application AirWatch.

**tooconfigure Azure AD single sign-on avec AirWatch, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **AirWatch** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_samlbase.png)

3. Sur hello **AirWatch domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.awmdm.com/AirWatch/Login?gid=companycode`

    b. Bonjour **identificateur** valeur hello de type en tant que zone de texte`AirWatch`

    > [!NOTE] 
    > Cette valeur n’est pas hello réel. Mettre à jour cette valeur avec l’URL de connexion réel hello. Contact [équipe de support Client de AirWatch](http://www.air-watch.com/company/contact-us/) tooget cette valeur. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_certificate.png) 

5. Sur hello **AirWatch Configuration** , cliquez sur **AirWatch de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_configure.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_general_400.png)
<CS>
7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise AirWatch tooyour en tant qu’administrateur.

8. Dans le volet de navigation gauche hello, cliquez sur **comptes**, puis cliquez sur **administrateurs**.
   
   ![Administrateurs](./media/active-directory-saas-airwatch-tutorial/ic791920.png "Administrateurs")

9. Développez hello **paramètres** menu, puis sur **Services Active Directory**.
   
   ![Paramètres](./media/active-directory-saas-airwatch-tutorial/ic791921.png "Paramètres")

10. Cliquez sur hello **utilisateur** onglet hello **Base DN** zone de texte, tapez votre nom de domaine, puis cliquez sur **enregistrer**.
   
   ![Utilisateur](./media/active-directory-saas-airwatch-tutorial/ic791922.png "Utilisateur")

11. Cliquez sur hello **Server** onglet.
   
   ![Serveur](./media/active-directory-saas-airwatch-tutorial/ic791923.png "Serveur")

12. Effectuez hello comme suit :
    
    ![Télécharger](./media/active-directory-saas-airwatch-tutorial/ic791924.png "Télécharger")   
    
    a. Pour **Directory Type**, sélectionnez **None**.

    b. Sélectionnez **Use SAML For Authentication**.

    c. tooupload hello certificat téléchargé, cliquez sur **télécharger**.

13. Bonjour **demande** section, effectuer hello comme suit :
    
    ![Demande](./media/active-directory-saas-airwatch-tutorial/ic791925.png "Demande")  

    a. Pour **Request Binding Type**, sélectionnez **POST**.

    b. Bonjour portail Azure, sur hello **configurer l’authentification unique sur Airwatch** page de boîte de dialogue, hello de copie **SAML Sign-On URL du Service unique** valeur, puis collez-le dans hello **fournisseur d’identité Seule l’URL de connexion** zone de texte.

    c. Pour **NameID Format**, sélectionnez **Email Address**.

    d. Cliquez sur **Enregistrer**.

14. Cliquez sur hello **utilisateur** onglet à nouveau.
    
    ![Utilisateur](./media/active-directory-saas-airwatch-tutorial/ic791926.png "Utilisateur")

15. Bonjour **attribut** section, effectuer hello comme suit :
    
    ![Attribut](./media/active-directory-saas-airwatch-tutorial/ic791927.png "Attribut")

    a. Bonjour **identificateur d’objet** zone de texte, type **http://schemas.microsoft.com/identity/claims/objectidentifier**.

    b. Bonjour **nom d’utilisateur** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    c. Bonjour **nom d’affichage** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    d. Bonjour **prénom** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname**.

    e. Bonjour **nom** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname**.

    f. Bonjour **messagerie** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    g. Cliquez sur **Save**.

<CE>

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-airwatch-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-airwatch-test-user"></a>Création d’un utilisateur de test AirWatch

tooenable Azure AD les utilisateurs toolog dans tooAirWatch, ils doivent être configurés dans tooAirWatch.

* Dans le cas d’AirWatch, cet approvisionnement est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à tooyour **AirWatch** site d’entreprise en tant qu’administrateur.
2. Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **comptes**, puis cliquez sur **utilisateurs**.
   
   ![Utilisateurs](./media/active-directory-saas-airwatch-tutorial/ic791929.png "Utilisateurs")
3. Bonjour **utilisateurs** menu, cliquez sur **mode liste**, puis cliquez sur **ajouter \> ajouter un utilisateur**.
   
   ![Ajouter un utilisateur](./media/active-directory-saas-airwatch-tutorial/ic791930.png "Ajouter un utilisateur")
4. Sur hello **Ajouter / modifier un utilisateur** boîte de dialogue, effectuer hello comme suit :

   ![Ajouter un utilisateur](./media/active-directory-saas-airwatch-tutorial/ic791931.png "Ajouter un utilisateur")   
   1. Hello de type **nom d’utilisateur**, **mot de passe**, **confirmer le mot de passe**, **prénom**, **nom**,  **Adresse de messagerie** d’un Azure valide compte Active Directory que vous voulez tooprovision dans hello relatives des zones de texte.
   2. Cliquez sur **Enregistrer**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre AirWatch utilisateur compte outil de création ou API fournie par AirWatch tooprovision des comptes d’utilisateur AAD.
>  

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAirWatch.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooAirWatch, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **AirWatch**.

    ![Configurer l’authentification unique](./media/active-directory-saas-airwatch-tutorial/tutorial_airwatch_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-airwatch-tutorial/tutorial_general_203.png

