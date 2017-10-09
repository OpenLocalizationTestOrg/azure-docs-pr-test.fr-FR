---
title: "Didacticiel : Intégration d’Azure Active Directory avec Igloo Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 406405d4faa6e56f1005a61e69a29ef2ef2eb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a>Didacticiel : Intégration d’Azure Active Directory avec Igloo Software

Dans ce didacticiel, vous apprendrez comment toointegrate Igloo Software avec Azure Active Directory (Azure AD).

Intégration de Igloo Software à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooIgloo logiciel
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooIgloo logiciels (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Igloo Software, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Igloo Software pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Igloo Software à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-igloo-software-from-hello-gallery"></a>Ajout de Igloo Software à partir de la galerie de hello
intégration de hello tooconfigure de Igloo Software dans Azure AD, vous devez tooadd Igloo Software à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Igloo Software à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Igloo Software**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. Dans le volet de résultats hello, sélectionnez **Igloo Software**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Igloo Software à l’aide d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Igloo Software est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Igloo Software doit toobe établie.

Dans Igloo Software, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Igloo Software, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Igloo Software](#creating-an-igloo-software-test-user)**  -toohave un équivalent de Britta Simon dans Igloo Software qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Igloo Software.

**tooconfigure Azure AD single sign-on avec Igloo Software, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Igloo Software** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. Sur hello **Igloo Software domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.igloocommmunities.com`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.igloocommmunities.com/saml.digest`

    c. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.igloocommmunities.com/saml.digest`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec hello réel identificateur, URL de réponse et URL de connexion. Contact [équipe de support Client de Igloo Software](https://www.igloosoftware.com/services/support) tooget ces valeurs. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. Sur hello **Igloo Software Configuration** , cliquez sur **configurer Igloo Software** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Igloo Software tooyour en tant qu’administrateur.

8. Accédez toohello **le panneau de configuration**.
   
     ![Control Panel (Panneau de configuration)](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel (Panneau de configuration)")

9. Bonjour **appartenance** , cliquez sur **paramètres de connexion**.
   
    ![Sign in Settings (Paramètres de connexion)](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings (Paramètres de connexion)")

10. Dans la section de Configuration de SAML de hello, cliquez sur **configurer l’authentification SAML**.
   
    ![Configuration SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Configuration SAML")
   
11. Bonjour **Configuration générale** section, effectuer hello comme suit :
   
    ![General Configuration (Configuration générale)](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration (Configuration générale)")

    a. Bonjour **nom de la connexion** zone de texte, tapez un nom personnalisé pour votre configuration.
   
    b. Bonjour **URL de connexion IdP** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.
   
    c. Bonjour **URL de déconnexion IdP** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.
    
    d. Pour **Logout Response and Request HTTP Type** (Type de réponse de déconnexion et de requête HTTP), sélectionnez **POST**.
   
    e. Ouvrez votre **base-64** certificat dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat Public** zone de texte.
    
12. Bonjour **réponse et la Configuration de l’authentification**, effectuer hello comme suit :
    
    ![Response and Authentication Configuration (Configuration de la réponse et de l’authentification)](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration (Configuration de la réponse et de l’authentification)")
  
      a. Pour **Fournisseur d’identité**, sélectionnez **Microsoft ADFS**.
      
      b. Pour **Type d’identificateur**, sélectionnez **Adresse de messagerie**. 

      c. Bonjour **attribut Email** zone de texte, type **emailaddress**.

      d. Bonjour **prénom attribut** zone de texte, type **givenname**.

      e. Bonjour **attribut de nom** zone de texte, type **surname**.

13. Effectuez hello étapes toocomplete hello configuration suivante :
    
    ![Création d’utilisateurs à l’authentification](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Création d’utilisateurs à l’authentification") 

     a. Pour **Création d’utilisateurs à l’authentification**, sélectionnez **Create a new user in your site when they sign in** (Créer un nouvel utilisateur sur votre site au moment de la connexion).

     b. Pour **Paramètres de connexion**, sélectionnez **Use SAML button on “Sign in” screen** (Utiliser le bouton SAML sur l’écran de connexion).

     c. Cliquez sur **Enregistrer**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-an-igloo-software-test-user"></a>Création d’un utilisateur de test Igloo Software

Il n’existe aucun élément d’action pour l’utilisateur tooconfigure vous tooIgloo logiciel de configuration.  

Quand un utilisateur affecté tente toolog dans tooIgloo logiciels à l’aide du volet d’accès hello, Igloo Software vérifie l’existence d’un utilisateur de hello.  Si aucun compte d’utilisateur n’est disponible, Igloo Software le crée automatiquement.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooIgloo logiciel.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooIgloo logiciel, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Igloo Software**.

    ![Configurer l’authentification unique](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque de Igloo Software hello Bonjour volet d’accès, vous devez obtenir l’application de Igloo Software tooyour automatiquement signé sur.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

