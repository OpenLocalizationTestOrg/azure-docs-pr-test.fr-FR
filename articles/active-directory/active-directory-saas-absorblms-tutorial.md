---
title: "Didacticiel : Intégration d’Azure Active Directory à Absorb LMS | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et absorber les LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ba9f1b3d-a4a0-4ff7-b0e7-428e0ed92142
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: a140a78a3a9474a6372a3ad4fb8251bd2452c990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-absorb-lms"></a>Didacticiel : Intégration d’Azure Active Directory avec Absorb LMS

Dans ce didacticiel, vous apprendrez comment toointegrate absorber LMS avec Azure Active Directory (Azure AD).

L’intégration d’absorber les LMS avec Azure AD offre hello avantages suivants :

- Vous pouvez contrôler dans Azure AD qui a accès tooAbsorb LMS
- Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAbsorb LMS (Single Sign-On) avec leurs comptes Azure AD
- Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez. [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis

tooconfigure intégration d’Azure AD à absorber les LMS, vous devez hello éléments suivants :

- Un abonnement Azure AD
- Un abonnement Absorb LMS pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

- N’utilisez pas votre environnement de production, sauf si cela est nécessaire.
- Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout LMS absorber à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-absorb-lms-from-hello-gallery"></a>Ajout LMS absorber à partir de la galerie de hello
tooconfigure hello intégration d’absorber les LMS dans tooAzure AD, vous devez tooadd absorber LMS à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd absorber LMS à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour ** [portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône. 

    ![bouton d’Azure Active Directory Hello][1]

2. Accédez trop**des applications d’entreprise**. Passez trop**toutes les applications**.

    ![panneau des applications Enterprise Hello][2]
    
3. tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.

    ![Nouveau bouton d’application Hello][3]

4. Dans la zone de recherche de hello, tapez **absorber les LMS**, sélectionnez **absorber les LMS** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.

    ![Absorber LMS dans la liste des résultats hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configurer et tester l’authentification unique Azure AD

Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Absorb LMS, avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans absorber les LMS est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans absorber les LMS doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans absorber les LMS.

tooconfigure et test Azure AD l’authentification unique avec absorber les LMS, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on) ** -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user) ** -tootest Azure AD single sign-on avec Britta Simon.
3. **[Créer un utilisateur de test absorber les LMS](#create-an-absorb-lms-test-user) ** -toohave un équivalent de Britta Simon dans LMS absorber qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.
4. **[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user) ** -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Tester l’authentification unique sur](#test-single-sign-on) ** -tooverify hello indique si les tâches de configuration.

### <a name="configure-azure-ad-single-sign-on"></a>Configurer l’authentification unique Azure AD

Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application absorber les LMS.

**tooconfigure Azure AD single sign-on avec absorber LMS, effectuez hello comme suit :**

1. Bonjour portail Azure, sur hello **absorber les LMS** page d’intégration d’application, cliquez sur **l’authentification unique**.

    ![Lien Configurer l’authentification unique][4]

2. Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_samlbase.png)

3. Sur hello **absorber le domaine LMS et URL** section, effectuer hello comme suit :

    ![Informations d’authentification unique dans Domaine et URL Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_url.png)

    a. Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.myabsorb.com/Account/SAML`

    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.myabsorb.com/Account/SAML`
     
    > [!NOTE] 
    > Ces valeurs ne sont pas hello réel. Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle. Contact [équipe de support Client de LMS absorber](https://www.absorblms.com/support) tooget ces valeurs. 

4. Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_certificate.png) 

6. Cliquez sur le bouton **Enregistrer** .

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/tutorial_general_400.png)
    
7. Sur hello **absorber les Configuration LMS** , cliquez sur **configurer un LMS absorber** tooopen **configurer l’authentification** fenêtre. Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**

    ![Configuration d’Absorb LMS](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_configure.png) 

8. Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise absorber les LMS tooyour en tant qu’administrateur.

9. Cliquez sur hello **icône compte** sur l’interface d’administration hello. 

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/1.png)

10. Cliquez sur **Paramètres du portail**.

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/2.png)
    
11. Cliquez sur hello **utilisateurs** onglet.

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/3.png)

12. Effectuez hello suivant les étapes tooaccess hello l’authentification unique sur les champs de configuration :

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/4.png)

    a. Sélectionnez hello approprié **Mode**.

    b. Ouvrez hello de certificat que vous avez téléchargé à partir de hello portail Azure dans le bloc-notes, supprimez hello **---BEGIN CERTIFICATE---** et **---END CERTIFICATE---** balise, puis collez hello restant contenu dans Hello **clé** zone de texte.
    
    c. Bonjour **Id de propriété**, sélectionnez hello attribut approprié que vous avez configurée comme hello identificateur utilisateur Bonjour Azure AD (par exemple, si le nom d’utilisateur principal hello est sélectionné dans Azure AD, puis le nom d’utilisateur soit sélectionnée ici.)

    d. Bonjour **URL de connexion**, collez hello **« SAML Sign-On URL du Service unique »** valeur que vous avez copié à partir de hello **configurer l’authentification** fenêtre Hello portail Azure.

    e. Bonjour **URL de déconnexion**, collez hello **« URL de déconnexion »** valeur que vous avez copié à partir de hello **configurer l’authentification** fenêtre Hello portail Azure.

13. Activez **« Autoriser uniquement la connexion SSO »**.

    ![Configurer l’authentification unique](./media/active-directory-saas-absorblms-tutorial/5.png)

14. Cliquez sur **Save** (Enregistrer).

> [!TIP]
> Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !  Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello ** Configuration** section bas hello. Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Créer un utilisateur de test Azure AD

objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.

![Créer un utilisateur de test Azure AD][100]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_01.png) 

2. liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-absorblms-tutorial/create_aaduser_02.png) 

3. En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_03.png) 

4. Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-absorblms-tutorial/create_aaduser_04.png) 

    a. Bonjour **nom** zone de texte, type **BrittaSimon**.

    b. Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.

    c. Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.

    d. Cliquez sur **Create**.

### <a name="create-an-absorb-lms-test-user"></a>Créer un utilisateur de test Absorb LMS

tooenable Azure AD les utilisateurs toolog dans tooAbsorb LMS, ils doivent être configurés dans tooAbsorb LMS.  
Pour Absorb LMS, l’approvisionnement est une tâche manuelle.

**tooprovision un compte d’utilisateur, effectuez hello comme suit :**

1. Ouvrez une session dans tooyour site d’entreprise absorber les LMS en tant qu’administrateur.

2. Cliquez sur l’onglet **Users** (Utilisateurs).

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_users.png)

3. Cliquez sur **utilisateurs** sous hello **utilisateurs** onglet.

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_userssub.png)

4.  Sélectionnez **User** (Utilisateur) dans la liste déroulante **Add New** (Ajouter nouveau).

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/absorblms_createuser.png)

5. Sur hello **ajouter un utilisateur** page, effectuer hello comme suit :

    ![Inviter des personnes](./media/active-directory-saas-absorblms-tutorial/user.png)

    a. Bonjour **prénom** zone de texte, nom du premier type hello comme Brian.

    b. Bonjour **nom** zone de texte, tapez nom de famille hello comme Simon.
    
    c. Bonjour **nom d’utilisateur** zone de texte, nom d’utilisateur de type hello comme Britta Simon.

    d. Bonjour **mot de passe** zone de texte, un mot de passe type hello de Britta Simon.

    e. Bonjour **confirmer le mot de passe** hello de type zone de texte mot de passe.
    
    f. Définissez-le comme **ACTIVE** (Actif).   

6. Cliquez sur **Save** (Enregistrer).
 
### <a name="assign-hello-azure-ad-test-user"></a>Affecter l’utilisateur de test hello Azure AD

Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAbsorb LMS.

![Attribuer le rôle d’utilisateur hello][200]

**tooassign Britta Simon tooAbsorb LMS, effectuez hello comme suit :**

1. Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.

    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **absorber les LMS**.

    ![lien d’absorber les LMS Hello dans la liste des Applications hello](./media/active-directory-saas-absorblms-tutorial/tutorial_absorblms_app.png) 

3. Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. Cliquez sur le bouton **Ajouter**. Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.

    ![volet d’ajouter l’affectation de Hello][203]

5. Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.

6. Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.

7. Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.
    
### <a name="test-single-sign-on"></a>Tester l’authentification unique

Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.

Cliquez sur hello absorber les LMS vignette Bonjour volet d’accès, vous obtiendrez une application d’absorber les LMS automatiquement signé sur tooyour. Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).

## <a name="additional-resources"></a>Ressources supplémentaires

* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-absorblms-tutorial/tutorial_general_203.png

