---
title: "Didacticiel : Intégration d’Azure Active Directory à FirmPlay - Employee Advocacy for Recruiting | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et FirmPlay - préconisation employé de recrutement."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a6799629-7546-43f8-a966-956db32864b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f143e0bb8f2a42de880d77e5f033694ce3f09cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-firmplay---employee-advocacy-for-recruiting"></a>Didacticiel : Intégration d’Azure Active Directory à FirmPlay - Employee Advocacy for Recruiting

Dans ce didacticiel, vous apprendrez comment toointegrate FirmPlay - préconisation employé pour recrutement avec Azure Active Directory (Azure AD).

Intégration FirmPlay - préconisation employé pour recrutement avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooFirmPlay - préconisation employé de recrutement
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFirmPlay - préconisation employé pour recrutement (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec FirmPlay - préconisation employé de recrutement, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement FirmPlay - Employee Advocacy for Recruiting pour lequel l’authentification unique est activée


> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.


tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de FirmPlay - préconisation employé pour recrutement à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD


## <a name="adding-firmplay---employee-advocacy-for-recruiting-from-hello-gallery"></a>Ajout de FirmPlay - préconisation employé pour recrutement à partir de la galerie de hello
intégration de hello tooconfigure de FirmPlay - préconisation employé pour recrutement dans Azure AD, vous devez tooadd FirmPlay - préconisation employé pour recrutement à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd FirmPlay - préconisation employé pour recrutement à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **FirmPlay - préconisation employé pour recrutement**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_001.png)

5. Dans le volet de résultats hello, sélectionnez **FirmPlay - préconisation employé pour recrutement**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec FirmPlay - Employee Advocacy for Recruiting avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans FirmPlay - préconisation employé pour recrutement est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans FirmPlay - préconisation employé pour recrutement doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans FirmPlay - préconisation employé de recrutement.

tooconfigure et test Azure AD l’authentification unique avec FirmPlay - préconisation employé de recrutement, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un FirmPlay - préconisation employé pour l’utilisateur de test de recrutement](#creating-a-firmplay---employee-advocacy-for-recruiting-test-user)**  -toohave un équivalent de Britta Simon dans FirmPlay : préconisation employé pour recrutement qui est liée de sa représentation sous forme de toohello Azure AD.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre FirmPlay - préconisation employé pour les applications de recrutement.

**tooconfigure Azure AD l’authentification unique avec FirmPlay - préconisation employé pour recrutement, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **FirmPlay - préconisation employé pour recrutement** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_01.png)

3. Sur hello **FirmPlay - préconisation employé pour le domaine de recrutement et URL** section hello **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<your-subdomain>.firmplay.com/`

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_02.png)

    > [!NOTE] 
    > Notez qu’il ne s’agit pas de la valeur réelle hello. Vous avez tooupdate URL de connexion cette valeur avec hello réel. Contact [FirmPlay - préconisation employé pour l’équipe de support technique de recrutement](mailto:engineering@firmplay.com) tooget cette valeur. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_03.png)   

5. Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**. Ensuite, cliquez sur le bouton **Enregistrer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_general_300.png)

6. Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_04.png)

7. Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_general_400.png)

8. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur. 

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_05.png) 

9. Sur hello **FirmPlay - préconisation employé pour la Configuration de recrutement** , cliquez sur **FirmPlay configurer - préconisation employé pour recrutement** tooopen **configurer l’authentification**boîte de dialogue.

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_06.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_07.png)

10. tooget l’authentification unique configurée pour votre application, contactez [FirmPlay - préconisation employé pour l’équipe de support technique de recrutement](mailto:engineering@firmplay.com) et leur fournir des éléments suivants de hello : 

    hello • téléchargé **fichier de certificat**

    • hello **SAML Sign-On URL du Service unique**

    • hello **ID d’entité SAML**

    • hello **URL de déconnexion**
  

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-firmplay-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**. 



### <a name="creating-a-firmplay---employee-advocacy-for-recruiting-test-user"></a>Création d’un utilisateur de test FirmPlay - Employee Advocacy for Recruiting

Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans FirmPlay - Employee Advocacy for Recruiting. Collaborez avec [FirmPlay - préconisation employé pour l’équipe de support technique de recrutement](mailto:engineering@firmplay.com) utilisateurs hello tooadd hello FirmPlay - préconisation employé pour la plateforme de recrutement.


### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooFirmPlay accès - préconisation employé de recrutement.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooFirmPlay - préconisation employé pour recrutement, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **FirmPlay - préconisation employé pour recrutement**.

    ![Configurer l’authentification unique](./media/active-directory-saas-firmplay-tutorial/tutorial_firmplay_50.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    


### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello FirmPlay - préconisation employé pour la vignette de recrutement Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour FirmPlay - préconisation employé pour les applications de recrutement.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-firmplay-tutorial/tutorial_general_203.png