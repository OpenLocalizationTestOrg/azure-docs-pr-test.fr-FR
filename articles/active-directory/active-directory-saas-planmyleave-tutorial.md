---
title: "Didacticiel : Intégration d’Azure Active Directory à PlanMyLeave | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et PlanMyLeave."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b0d31cbe-7ae2-488b-9cf3-4927391fa744
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: jeedes
ms.openlocfilehash: 44a6782e44ef22fc957544960be1742f9eed6e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-planmyleave"></a>Didacticiel : Intégration de PlanMyLeave à Azure Active Directory

Dans ce didacticiel, vous apprendrez comment toointegrate PlanMyLeave avec Azure Active Directory (Azure AD).

Intégration PlanMyLeave à Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooPlanMyLeave
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPlanMyLeave (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD avec PlanMyLeave, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement PlanMyLeave pour lequel l’authentification unique est activée


> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.


tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).


## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de PlanMyLeave à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD


## <a name="adding-planmyleave-from-hello-gallery"></a>Ajout de PlanMyLeave à partir de la galerie de hello
intégration de hello tooconfigure de PlanMyLeave dans Azure AD, vous devez tooadd PlanMyLeave à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd PlanMyLeave à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![Active Directory][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![Applications][2]
    
3. Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.

    ![Applications][3]

4. Dans la zone de recherche de hello, tapez **PlanMyLeave**.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_001.png)

5. Dans le volet de résultats hello, sélectionnez **PlanMyLeave**, puis cliquez sur **ajouter** bouton application hello de tooadd.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec PlanMyLeave avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans PlanMyLeave est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans PlanMyLeave doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans PlanMyLeave.

tooconfigure et test Azure AD l’authentification unique avec PlanMyLeave, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test PlanMyLeave](#creating-a-planmyleave-test-user)**  -toohave de Britta Simon dans PlanMyLeave qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application PlanMyLeave.

**tooconfigure Azure AD single sign-on avec PlanMyLeave, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, sur hello **PlanMyLeave** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** page de boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.
 
    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_01.png)

3. Sur hello **PlanMyLeave domaine et les URL** section, effectuer hello comme suit :

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_02.png)

    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company-name>.planmyleave.com/Login.aspx`
    
    b. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company-name>.planmyleave.com`

    > [!NOTE] 
    > Notez qu’il s’agit pas des valeurs réelles hello. Vous avez tooupdate ces valeurs avec hello réel connectent URL et l’identificateur. Contact [équipe de support PlanMyLeave](mailto:support@planmyleave.com) tooget ces valeurs.

4. Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_03.png)     

5. Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**. Ensuite, cliquez sur le bouton **Enregistrer**.

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_300.png)

6. Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_04.png)

7. Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_general_400.png)

8. Sur hello **le certificat de signature SAML** , cliquez sur **certificat (base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_05.png) 

9. Sur hello **PlanMyLeave Configuration** , cliquez sur **PlanMyLeave de configurer** tooopen **configurer l’authentification** fenêtre.

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_06.png) 

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_07.png)

10. Dans une autre fenêtre de navigateur web, connectez-vous à votre locataire PlanMyLeave en tant qu’administrateur.

11. Accédez trop**le programme d’installation du système**. Puis sur hello **gestion de la sécurité** cliquez sur la section **paramètres SAML de l’entreprise** .

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_002.png) 

12. Sur hello **paramètres SAML** , cliquez sur icône de l’éditeur.

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_003.png)

13. Sur hello **mise à jour les paramètres SAML** section, effectuer hello comme suit :

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_004.png)

    a.  Bonjour **URL de connexion** zone de texte, placez la valeur hello **SAML Sign-On URL du Service unique** à partir de la fenêtre de configuration d’application Azure AD.

    b.  Ouvrez votre fichier de certificat téléchargé dans le bloc-notes, copiez uniquement hello contenu entre hello---Begin Certificate---et---End certificate---de celui-ci dans le Presse-papiers et collez-la toohello **certificat** zone de texte.

    c. Définissez »**est activé**« trop »**Oui**».

    d. Cliquez sur **Save**.



### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.

![Créer un utilisateur Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_01.png) 

2. Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-planmyleave-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**. 



### <a name="creating-a-planmyleave-test-user"></a>Création d’un utilisateur de test PlanMyLeave

objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans PlanMyLeave. PlanMyLeave prend en charge l’approvisionnement juste-à-temps, option activée par défaut.

Vous n’avez aucune opération à effectuer dans cette section. Un nouvel utilisateur s’affichera pendant une tentative de tooaccess PlanMyLeave s’il n’existe pas encore.

> [!NOTE]
> Si vous devez manuellement toocreate un utilisateur, vous devez toocontact [équipe de support PlanMyLeave](mailto:support@planmyleave.com).



### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooPlanMyLeave de son accès.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooPlanMyLeave, effectuez hello comme suit :**

1. Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **PlanMyLeave**.

    ![Configurer l’authentification unique](./media/active-directory-saas-planmyleave-tutorial/tutorial_planmyleave_50.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![Affecter des utilisateurs][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![Affecter des utilisateurs][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    


### <a name="testing-single-sign-on"></a>Test de l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque PlanMyLeave hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour PlanMyLeave application.


## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-planmyleave-tutorial/tutorial_general_203.png