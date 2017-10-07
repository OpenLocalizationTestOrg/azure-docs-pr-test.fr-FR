---
title: "Didacticiel : Intégration d’Azure Active Directory à Zoho | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: 5d1c196d3b97babab196f509ea68e7d61523a7e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a>Didacticiel : Intégration d’Azure Active Directory à Zoho

Dans ce didacticiel, vous apprendrez comment toointegrate Zoho avec Azure Active Directory (Azure AD).

Intégration Zoho à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooZoho.
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZoho (Single Sign-On) avec leurs comptes Azure AD.
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

intégration d’Azure AD avec Zoho de tooconfigure, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Zoho pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de Zoho à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-zoho-from-hello-gallery"></a>Ajout de Zoho à partir de la galerie de hello
intégration de hello tooconfigure de Zoho dans Azure AD, vous devez tooadd Zoho à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Zoho à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **Zoho**, sélectionnez **Zoho** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Liste des résultats de Zoho Bonjour](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zoho avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zoho est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zoho doit toobe établie.

Dans Zoho, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.

tooconfigure et test Azure AD l’authentification unique avec Zoho, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test Zoho](#create-a-zoho-test-user)**  -toohave un équivalent de Britta Simon dans Zoho est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Zoho.

**tooconfigure Azure AD single sign-on avec Zoho, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **Zoho** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. Sur hello **Zoho domaine et les URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.zohomail.com`

    > [!NOTE] 
    > Cette valeur n’est pas la valeur réelle. Mettre à jour de cette valeur avec hello URL de connexion réel. Contact [équipe de support Client de Zoho](https://www.zoho.com/mail/contact.html) tooget cette valeur. 
 
4. Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. Sur hello **Zoho Configuration** , cliquez sur **Zoho de configurer** tooopen **configurer l’authentification** fenêtre. Hello de copie **SAML Sign-On URL du Service unique, URL de modification du mot de passe et URL de déconnexion** de hello **section de référence rapide.**

    ![Configuration de Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zoho Mail en tant qu’administrateur.

8. Accédez toohello **le panneau de configuration**.
   
    ![Control Panel (Panneau de configuration)](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel (Panneau de configuration)")

9. Cliquez sur hello **l’authentification SAML** onglet.
   
    ![Authentification SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Authentification SAML")

10. Bonjour **détails de l’authentification SAML** section, effectuer hello comme suit :
   
    ![Détails d’authentification SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Détails d’authentification SAML")
   
    a. Bonjour **URL de connexion** zone de texte, collez **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.
   
    b. Bonjour **URL de déconnexion** zone de texte, collez **URL de déconnexion** dont vous avez copié à partir du portail Azure.
   
    c. Bonjour **URL de modification du mot de passe** zone de texte, collez **URL de modification du mot de passe** dont vous avez copié à partir du portail Azure.
       
    d. Ouvrez votre certificat codé en base 64 téléchargé à partir du portail Azure dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **PublicKey** zone de texte.
   
    e. Comme **Algorithme**, sélectionnez **RSA**.
   
    f. Cliquez sur **OK**.

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

   ![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.

    ![bouton Ajouter de Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    a. Bonjour **nom** , tapez **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.

    c. Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.

    d. Cliquez sur **Create**.
 
### <a name="create-a-zoho-test-user"></a>Créer un utilisateur de test Zoho

Dans l’ordre tooenable Azure AD les utilisateurs toolog à Zoho Mail, vous devez les configurer dans Zoho Mail. Dans les cas de hello de Zoho Mail, cette configuration est une tâche manuelle.

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre Zoho Mail utilisateur compte outil de création ou API fournie par Zoho Mail tooprovision des comptes d’utilisateur AAD.

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a>tooprovision un compte d’utilisateur, effectuez hello comme suit :

1. Connectez-vous à tooyour **Zoho Mail** site d’entreprise en tant qu’administrateur.

2. Accédez trop**le panneau de configuration \> de messagerie et de documents**.

3. Accédez trop**détails de l’utilisateur \> ajouter un utilisateur**.
   
    ![Ajouter un utilisateur](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Ajouter un utilisateur")

4. Sur hello **ajouter des utilisateurs** boîte de dialogue, effectuer hello comme suit :
   
    ![Ajouter un utilisateur](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Ajouter un utilisateur")
   
    a. Bonjour **prénom** zone de texte, type hello premier nom d’utilisateur comme **Brian**.

    b. Bonjour **nom** zone de texte, type hello nom d’utilisateur comme **Simon**.

    c. Bonjour **ID de courrier électronique** zone de texte, id de courrier électronique de type hello d’utilisateur comme  **brittasimon@contoso.com** .

    d. Bonjour **mot de passe** zone de texte, entrez le mot de passe d’utilisateur.
   
    e. Cliquez sur **OK**.  
      
    > [!NOTE]
    > titulaire du compte Azure Active Directory Hello recevra un e-mail avec un compte de hello tooconfirm lien avant son activation.

### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZoho.

![Attribuer le rôle d’utilisateur hello][200] 

**tooassign Britta Simon tooZoho, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **Zoho**.

    ![lien de Zoho Hello dans la liste des Applications hello](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202]

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque Zoho hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Zoho application.
Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

