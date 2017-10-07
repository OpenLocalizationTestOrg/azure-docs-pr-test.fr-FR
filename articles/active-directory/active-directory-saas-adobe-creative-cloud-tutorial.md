---
title: "Didacticiel : Intégration d’Azure Active Directory à Adobe Creative Cloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Cloud créatifs d’Adobe."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9ba1171e-56b1-4475-b308-58637d35e5a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 5e66255e9785465974a23cd3ef79c24e28c0250f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-creative-cloud"></a>Didacticiel : Intégration d’Azure Active Directory à Adobe Creative Cloud

Dans ce didacticiel, vous apprendrez comment toointegrate Adobe Creative Cloud avec Azure Active Directory (Azure AD).

Intégration Cloud créatifs d’Adobe à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAdobe Cloud créatifs
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAdobe Cloud créatifs (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec Cloud créatifs d’Adobe, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Adobe Creative Cloud pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout Cloud créatifs Adobe à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-adobe-creative-cloud-from-hello-gallery"></a>Ajout Cloud créatifs Adobe à partir de la galerie de hello
tooconfigure hello intégration de Cloud créatifs d’Adobe dans Azure AD, vous devez tooadd Cloud créatifs d’Adobe à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Adobe de Cloud créatifs à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Cloud créatifs d’Adobe**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_000.png)

5. Dans le volet de résultats hello, sélectionnez **Cloud créatifs d’Adobe**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Adobe Creative Cloud, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Cloud créatifs d’Adobe est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le Cloud de Creative Adobe hello doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans le Cloud créatifs d’Adobe.

tooconfigure et test Azure AD l’authentification unique avec Cloud créatifs d’Adobe, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Cloud créatifs d’Adobe](#creating-an-adobe-creative-cloud-test-user)**  -toohave de Britta Simon dans Adobe Creative Cloud qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application Cloud créatifs d’Adobe.

**tooconfigure Azure AD l’authentification unique avec Cloud créatifs d’Adobe, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **Cloud créatifs d’Adobe** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_01.png)

3. Sur hello **Adobe Creative Cloud domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url1.png)

    a. Bonjour **identificateur** valeur hello de type en tant que zone de texte :`https://www.okta.com/saml2/service-provider/<token>`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.okta.com/auth/saml20/accauthlinktest`

    > [!NOTE] 
    > Notez qu’il s’agit pas des valeurs réelles hello. Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle. Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur. Si vous devez manuellement toocreate un utilisateur, vous avez besoin d’équipe de support technique du Cloud créatifs d’Adobe toocontact hello.

4. Sur hello **Adobe Creative Cloud domaine et les URL** section, effectuer hello comme suit si vous le souhaitez application hello tooconfigure **SP** en mode initié par :

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_url2.png)

    a. Cliquez sur hello **afficher les paramètres d’URL avancés** option

    b. Bonjour **URL de connexion** valeur hello de type en tant que zone de texte :`https://adobe.com`

5. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_05.png) 

6. Sur hello **Configuration du Cloud Creative Adobe** , cliquez sur **configurer le Cloud créatifs Adobe** tooopen **configurer l’authentification** fenêtre. Copiez hello **Id d’entité SAML** et **URL du Service SSO SAML** à partir de la section de référence rapide.

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_06.png) 

7. Dans une fenêtre de navigateur web, client de Cloud créatifs d’Adobe tooyour ouverture de session en tant qu’administrateur.

8.  Accédez trop**identité** hello du volet de navigation gauche et cliquez sur votre domaine. Puis exécutez hello comme suit **l’authentification unique sur une Configuration requise** section.

    ![Paramètres](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_001.png "Paramètres")

9. Cliquez sur **Parcourir** hello de tooupload téléchargé certificat auprès d’Azure AD trop**certificat IDP**.

10. Bonjour **émetteur IDP** zone de texte, placez la valeur hello **Id d’entité SAML** que vous avez copié à partir de **configurer l’authentification** section dans le portail Azure.

11. Bonjour **URL de connexion IDP** zone de texte, placez la valeur hello **URL du Service SSO SAML** que vous avez copié à partir de **configurer l’authentification** section dans le portail Azure.

12. Sélectionnez **HTTP - Redirection** en tant que **Liaison IDP**.

13. Sélectionnez **Adresse de messagerie** en tant que **Paramètre de connexion utilisateur**.
 
14. Cliquez sur le bouton **Enregistrer** .

15. tableau de bord Hello présente maintenant hello XML **« Télécharger des métadonnées »** fichier. Il contient les URL EntityDescriptor et AssertionConsumerService d’Adobe. Veuillez ouvrir le fichier de hello et configurez-les dans hello application Azure AD.

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_002.png)

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_003.png)

    a. Hello d’utilisation EntityDescriptor valeur Adobe fourni pour **identificateur** sur hello **configurer les paramètres de l’application** boîte de dialogue.

    b. Hello d’utilisation AssertionConsumerService valeur Adobe fourni pour **URL de réponse** sur hello **configurer les paramètres de l’application** boîte de dialogue.
 
### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**. 

### <a name="creating-an-adobe-creative-cloud-test-user"></a>Création d’un utilisateur d’Adobe Creative Cloud

Dans l’ordre tooenable Azure AD les utilisateurs toolog dans le Cloud créatifs d’Adobe, vous devez les configurer dans le Cloud créatifs d’Adobe.  
Dans les cas de hello de Cloud créatifs d’Adobe, cette configuration est une tâche manuelle.

**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**

1. Ouvrez une session dans tooyour site d’entreprise Cloud créatifs d’Adobe en tant qu’administrateur.

2. Cliquez sur **People**.

    ![Personnes](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_001.png "Personnes")

3. Cliquez sur **Invite User**.

    ![Inviter des utilisateurs](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_002.png "inviter des utilisateurs")

4. Sur hello **inviter des personnes** boîte de dialogue de page, effectuer hello comme suit :

    ![Inviter des personnes](./media/active-directory-saas-adobe-creative-cloud-tutorial/create_aaduser_003.png "inviter des personnes")

    a. Bonjour **messagerie** zone de texte, tapez Bonjour adresse de messagerie du compte de Britta Simon.
    
    b. Cliquez sur **Invite**.

    > [!NOTE]
    > titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooAdobe accès Cloud créatifs.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooAdobe Cloud créatifs, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Cloud créatifs d’Adobe**.

    ![Configurer l’authentification unique](./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_adobe-creative-cloud_50.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Cloud créatifs d’Adobe hello hello volet d’accès, vous devez obtenir l’application de Cloud créatifs d’Adobe tooyour automatiquement signé sur.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-creative-cloud-tutorial/tutorial_general_203.png