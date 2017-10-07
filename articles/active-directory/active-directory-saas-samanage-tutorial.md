---
title: "Didacticiel : Intégration d’Azure Active Directory avec Samanage | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a>Didacticiel : Intégration d’Azure Active Directory à Samanage

Dans ce didacticiel, vous apprendrez comment toointegrate Samanage avec Azure Active Directory (Azure AD).

Intégration de Samanage à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooSamanage
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSamanage (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à Samanage, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Samanage pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Samanage à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-samanage-from-hello-gallery"></a>Ajout de Samanage à partir de la galerie de hello
intégration de hello tooconfigure de Samanage dans Azure AD, vous devez tooadd Samanage à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Samanage à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **Samanage**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. Dans le volet de résultats hello, sélectionnez **Samanage**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Samanage sur un utilisateur de test nommé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Samanage est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Samanage doit toobe établie.

Dans Samanage, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique à Samanage, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de Samanage](#creating-a-samanage-test-user)**  -toohave un équivalent de Britta Simon dans Samanage est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Samanage.

**tooconfigure Azure AD single sign-on avec Samanage, procédez hello comme suit :**

1. Bonjour portail Azure, sur hello **Samanage** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. Sur hello **Samanage domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<Company Name>.samanage.com/saml_login/<Company Name>`

    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<Company Name>.samanage.com`

    > [!NOTE] 
    > Il ne s’agit pas de valeurs réelles. Mettre à jour ces valeurs avec l’URL de connexion réel hello et identificateur, qui est expliquée plus loin dans le didacticiel de hello. Pour plus de détails, contactez l’[équipe de support technique Samanage](https://www.samanage.com/support).    
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. Sur hello **Samanage Configuration** , cliquez sur **configurer de Samanage** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et l’ID d’entité SAML** de hello **section de référence rapide.**

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Samanage en tant qu’administrateur.

8. Cliquez sur **Dashboard** et sélectionnez **Setup** dans le volet de navigation de gauche.
   
    ![Tableau de bord](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Tableau de bord")

9. Cliquez sur **Single Sign-On**.
   
    ![Authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Authentification unique")

10. Accédez trop**connexion à l’aide de SAML** section, effectuer hello comme suit :
   
    ![Connexion avec SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Connexion avec SAML")
 
    a. Cliquez sur **Enable Single Sign-On with SAML**(Activer l’authentification unique avec SAML).  
 
    b. Bonjour **URL du fournisseur d’identité** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.    
 
    c. Confirmer hello **URL de connexion** correspondances hello **URL de connexion** de **Samanage domaine et les URL** section dans le portail Azure.
 
    d. Bonjour **URL de déconnexion** zone de texte, entrez la valeur hello **URL de déconnexion** dont vous avez copié à partir du portail Azure.
 
    e. Bonjour **SAML émetteur** zone de texte, URI de l’id de l’application hello de type défini dans votre fournisseur d’identité.
 
    f. Ouvrez votre certificat codé en base 64 téléchargé à partir du portail Azure dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **collez votre x.509 de fournisseur d’identité certificat ci-dessous** zone de texte.
 
    g. Cliquez sur **Create users if they do not exist in Samanage**(Créer des utilisateurs s’ils n’existent pas dans Samanage).
 
    h. Cliquez sur **Update**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)
 
### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.
 
### <a name="creating-a-samanage-test-user"></a>Création d’un utilisateur de test Samanage

tooenable Azure AD les utilisateurs toolog dans tooSamanage, vous devez les configurer sur Samanage.  
Dans les cas de hello de Samanage, cette configuration est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Connectez-vous à votre site d’entreprise Samanage en tant qu’administrateur.

2. Cliquez sur **Dashboard** et sélectionnez **Setup** dans le volet de navigation gauche.
   
    ![Configuration](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Configuration")

3. Cliquez sur hello **utilisateurs** onglet
   
    ![Utilisateurs](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Utilisateurs")

4. Cliquez sur **New User**.
   
    ![Nouvel utilisateur](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Nouvel utilisateur")

5. Hello de type **nom** et hello **adresse de messagerie** d’un compte Azure Active Directory tooprovision et cliquez sur **créer un utilisateur**.
   
    ![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")
   
   >[!NOTE]
   >titulaire du compte Azure Active Directory Hello sera reçoivent un e-mail et suivez les leur compte d’un tooconfirm lien avant son activation. Vous pouvez utiliser n’importe quel autre Samanage utilisateur compte outil de création ou API fournie par Samanage tooprovision Azure Active Directory des comptes d’utilisateur.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSamanage.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooSamanage, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Samanage**.

    ![Configurer l’authentification unique](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Samanage hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Samanage application.
Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

