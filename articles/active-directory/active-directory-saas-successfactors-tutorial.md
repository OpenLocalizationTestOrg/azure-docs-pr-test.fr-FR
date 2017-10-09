---
title: "Didacticiel : Intégration d’Azure Active Directory à SuccessFactors | Microsoft Docs"
description: "Découvrez comment toouse SuccessFactors avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 3f7895d7d5e26fda27f555ae2f14a1645b50dcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a>Didacticiel : Intégration d’Azure Active Directory à SuccessFactors
objectif Hello de ce didacticiel est tooshow vous comment toointegrate SuccessFactors avec Azure Active Directory (Azure AD).

Intégration de SuccessFactors à Azure AD offre hello avantages suivants :

* Vous pouvez contrôler dans Azure AD qui a accès tooSuccessFactors
* Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSuccessFactors (Single Sign-On) avec leurs comptes Azure AD
* Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
tooconfigure intégration d’Azure AD avec SuccessFactors, vous devez hello éléments suivants :

* Un abonnement Azure valide
* Un locataire SuccessFactors

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.
> 
> 

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

* Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
* Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.

scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de SuccessFactors à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-successfactors-from-hello-gallery"></a>Ajout de SuccessFactors à partir de la galerie de hello
intégration de hello tooconfigure de SuccessFactors dans Azure AD, vous devez tooadd SuccessFactors à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd SuccessFactors à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
    ![Configuration de l'authentification unique][1]
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Configuration de l'authentification unique][2]
4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Applications][3]
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Configuration de l'authentification unique][4]
6. Bonjour **zone de recherche**, type **SuccessFactors**.
   
    ![Configuration de l'authentification unique][5]
7. Dans le volet de résultats hello, sélectionnez **SuccessFactors**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![Configuration de l'authentification unique][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
objectif Hello de cette section est tooshow comment tooconfigure et test Azure AD l’authentification unique avec SuccessFactors en fonction d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans SuccessFactors tooan l’utilisateur dans Azure AD est. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans SuccessFactors doit toobe établie.

Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans SuccessFactors.

tooconfigure et test Azure AD l’authentification unique avec SuccessFactors, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test de SuccessFactors](#creating-a-successfactors-test-user)**  -toohave de Britta Simon dans SuccessFactors qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD
Dans cette section, vous activez Azure AD l’authentification unique dans le portail classique de hello et configurez l’authentification unique dans votre application SuccessFactors.

**tooconfigure Azure AD single sign-on avec SuccessFactors, procédez hello comme suit :**

1. Bonjour portail Azure classic sur hello **SuccessFactors** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.
   
    ![Configuration de l'authentification unique][7]
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooSuccessFactors** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Configuration de l'authentification unique][8]
3. Sur hello **Configure App URL** page, effectuer hello comme suit, puis cliquez sur **suivant**.
   
    ![Configuration de l'authentification unique][9]
   
    a. Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide d’une des hello suivant des modèles : 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    b. Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide d’une des hello suivant des modèles : 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    c. Cliquez sur **Suivant**. 

    > [!NOTE]
    > Notez qu’il s’agit pas des valeurs réelles hello. Vous avez tooupdate ces valeurs avec URL hello URL de connexion et de réponse réelle. Ces valeurs, contactez le tooget [équipe de support technique SuccessFactors](https://www.successfactors.com/en_us/support.html).

1. Sur hello **configurer l’authentification unique sur SuccessFactors** , cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello localement sur votre ordinateur.
   
    ![Configuration de l'authentification unique][10]

2. Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail d’administration SuccessFactors** en tant qu’administrateur.

3. Visitez **sécurité de l’Application** et native trop**l’authentification unique sur la fonctionnalité**. 

4. Placer n’importe quelle valeur Bonjour **réinitialiser le jeton** et cliquez sur **enregistrer le jeton** tooenable SSO SAML.
   
    ![Configuration de l’authentification unique côté application][11]

    > [!NOTE] 
    > Cette valeur est uniquement utilisée comme hello sur commutateur marche/arrêt. Si aucune valeur n’est enregistrée, hello SAML SSO est activé. Si une valeur vide est enregistrée hello SAML SSO est désactivé.

1. Capture d’écran de toobelow natif et effectuer hello suivant des actions.
   
    ![Configuration de l’authentification unique côté application][12]
   
    a. Sélectionnez hello **SAML v2 SSO** case d’option
   
    b. Définissez hello SAML assertion tiers Name(e.g. SAml issuer + company name).
   
    c. Bonjour **SAML émetteur** zone de texte placer la valeur hello **URL de l’émetteur** à partir de l’Assistant configuration d’application Azure AD.
   
    d. Sélectionnez **Response(Customer Generated/IdP/AP)** (Réponse (générée par le client/fournisseur d’identité/point d’accès)) pour **Require Mandatory Signature** (Exiger une signature obligatoire).
   
    e. Sélectionnez **Enabled** (Activé) dans le champ **Enable SAML Flag** (Activer l’indicateur SAML).
   
    f. Sélectionnez **No** (Non) dans le champ **Login Request Signature(SF Generated/SP/RP)** (Signature de la demande de connexion (générée par SF/fournisseur de services/fournisseur de ressources)).
   
    g. Sélectionnez **Browser/Post Profile** (Navigateur/Post-profilage) en tant que **profil SAML**.
   
    h. Sélectionnez **No** (Non) dans le champ **Enforce Certificate Valid Period** (Appliquer la période valide du certificat).
   
    i. Copier le contenu du fichier de certificat téléchargé hello hello, puis collez-le dans hello **certificat de vérification SAML** zone de texte.

    > [!NOTE] 
    > contenu du certificat Hello doit avoir des balises de certificat certificat et de fin de début.

1. Accédez tooSAML V2, puis exécutez hello comme suit :
   
    ![Configuration de l’authentification unique côté application][13]
   
    a. Sélectionnez **Yes** (Oui) dans **Support SP-initiated Global Logout** (Prendre en charge la déconnexion globale initiée par le fournisseur de services).
   
    b. Bonjour **Global URL de Service de déconnexion (destination LogoutRequest)** zone de texte placer la valeur hello **URL de déconnexion distante** à partir de l’Assistant configuration d’application Azure AD.
   
    c. Sélectionnez **No** (Non) dans **Require sp must encrypt all NameID element** (Exiger que le fournisseur de services chiffre tous les éléments NameID).
   
    d. Sélectionnez **unspecified** (non spécifié) dans **NameID Format** (Format NameID).
   
    e. Sélectionnez **Yes** (Oui) dans **Enable sp initiated login (AuthnRequest)** (Activer la connexion initiée par le fournisseur de services (AuthnRequest)).
   
    f. Bonjour **demande d’envoi que l’émetteur de société** zone de texte placer la valeur hello **URL de connexion distante** à partir de l’Assistant configuration d’application Azure AD.
2. Procédez comme suit si vous souhaitez que les noms d’utilisateur de connexion toomake hello respecter la casse,.
   
    a. Visitez **paramètres de la société**(près du bas hello).
   
    b. Sélectionnez la case à cocher près de **Enable Non-Case-Sensitive Username**(Activer le non-respect de la casse pour les noms d’utilisateur).
   
    c. Cliquez sur **Enregistrer**.
   
    ![Configurer l’authentification unique][29]

    > [!NOTE] 
    > Si vous essayez tooenable, système de hello vérifie si un nom de connexion SAML en double sera créé. Par exemple, si le client de hello possède des noms d’utilisateur, Utilisateur1 et user1. Si vous désactivez le respect de la casse, ces noms deviennent des doublons. système de Hello vous donne un message d’erreur et n’active pas la fonctionnalité de hello. Hello client devra toochange un des noms d’utilisateur hello afin qu’il est orthographié réellement différents. 

1. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
   
    ![Applications][14]
2. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.
   
    ![Applications][15]

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail classique de hello appelé Britta Simon.

![Créer un utilisateur Azure AD][16]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Création d’un utilisateur de test Azure AD][17]
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Création d’un utilisateur de test Azure AD][18]
4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.
   
    ![Création d’un utilisateur de test Azure AD][19]
5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD][20]
   
    a. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.
   
    b. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.
   
    c. Cliquez sur **Suivant**.
6. Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD][21]
   
    a. Bonjour **prénom** zone de texte, type **Brian**.  
   
    b. Bonjour **nom** zone de texte, type, **Simon**.
   
    c. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.
   
    d. Bonjour **rôle** liste, sélectionnez **utilisateur**.
   
    e. Cliquez sur **Suivant**.
7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.
   
    ![Création d’un utilisateur de test Azure AD][22]
8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD][23]
   
    a. Notez la valeur hello hello **nouveau mot de passe**.
   
    b. Cliquez sur **Terminé**.  

### <a name="creating-a-successfactors-test-user"></a>Création d’un utilisateur de test SuccessFactors
Dans l’ordre tooenable Azure AD les utilisateurs toolog à SuccessFactors, vous devez les configurer dans SuccessFactors.  
Dans les cas de hello de SuccessFactors, cette configuration est une tâche manuelle.

les utilisateurs tooget créés dans SuccessFactors, vous devez toocontact hello [équipe de support technique SuccessFactors](https://www.successfactors.com/en_us/support.html).

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD
objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant tooSuccessFactors de son accès.

![Affecter des utilisateurs][24]

**tooassign Britta Simon tooSuccessFactors, effectuez hello comme suit :**

1. Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.
   
    ![Affecter des utilisateurs][25]
2. Dans la liste des applications hello, sélectionnez **SuccessFactors**.
   
    ![Configurer l’authentification unique][26]
3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Affecter des utilisateurs][27]
4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.
5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.
   
    ![Affecter des utilisateurs][28]

### <a name="testing-single-sign-on"></a>Test de l’authentification unique
objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur hello SuccessFactors vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application SuccessFactors.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
