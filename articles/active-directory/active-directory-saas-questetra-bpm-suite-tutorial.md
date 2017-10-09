---
title: "Didacticiel : Intégration d'Azure Active Directory à Questetra BPM Suite | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Questetra BPM Suite."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: fb6d5b73-e491-4dd2-92d6-94e5aba21465
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/14/2017
ms.author: jeedes
ms.openlocfilehash: 4907e3b5751cd79f994fbd2ebcb7faec4eac34e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-questetra-bpm-suite"></a>Didacticiel : Intégration d'Azure Active Directory avec Questetra BPM Suite
objectif Hello de ce didacticiel est tooshow vous comment toointegrate Suite de BPM Questetra avec Azure Active Directory (Azure AD).  
Intégration Questetra BPM Suite à Azure AD offre hello avantages suivants : 

* Vous pouvez contrôler dans Azure AD qui a accès tooQuestetra Suite BPM 
* Vous pouvez activer vos utilisateurs tooautomatically get connecté tooQuestetra Suite BPM (Single Sign-On) avec leurs comptes Azure AD
* Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
tooconfigure intégration d’Azure AD avec Questetra BPM Suite, vous devez hello éléments suivants :

* Un abonnement Azure AD
* Un abonnement [Questetra BPM Suite](https://senbon-imadegawa-988.questetra.net/) pour lequel l’authentification unique est activée

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.
> 
> 

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

* Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
* Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/). 

## <a name="scenario-description"></a>Description du scénario
objectif Hello de ce didacticiel est tooenable vous tootest Azure AD l’authentification unique dans un environnement de test.  
scénario Hello décrite dans ce didacticiel se compose de trois blocs de construction principaux :

1. Ajout de Questetra BPM Suite à partir de la galerie de hello 
2. Configuration et test de l’authentification unique Azure AD

## <a name="adding-questetra-bpm-suite-from-hello-gallery"></a>Ajout de Questetra BPM Suite à partir de la galerie de hello
intégration de hello tooconfigure de Questetra BPM Suite dans Azure AD, vous devez tooadd Questetra BPM Suite à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.

**tooadd Suite BPM de Questetra à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**. 
   
    ![Active Directory][1]

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications][2]

4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Applications][3]

5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Applications][4]

6. Dans la zone de recherche de hello, tapez **Questetra BPM Suite**.
   
    ![Applications][5]

7. Dans le volet de résultats hello, sélectionnez **Questetra BPM Suite**, puis cliquez sur **Complete** application hello de tooadd.

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
objectif Hello de cette section est tooshow comment tooconfigure et test Azure AD l’authentification unique avec Questetra BPM Suite en fonction d’un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello utilisateur de tooan Questetra BPM Suite dans Azure AD est. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Questetra BPM Suite doit toobe établie.  
Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Questetra BPM Suite.

tooconfigure et test Azure AD l’authentification unique avec Questetra BPM Suite, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
3. **[Création d’un utilisateur de test Questetra BPM Suite](#creating-a-questetra-bpm-suite-test-user)**  -toohave de Britta Simon dans Suite BPM Questetra qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
4. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
5. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuration de l’authentification unique Azure AD
Hello cette section vise tooenable Azure AD l’authentification unique sur Bonjour portail Azure classic et tooconfigure l’authentification unique dans votre application Questetra BPM Suite.

**tooconfigure Azure AD l’authentification unique avec Questetra BPM Suite, procédez hello comme suit :**

1. Bonjour portail Azure classic sur hello **Questetra BPM Suite** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer l’authentification unique sur**  boîte de dialogue.
   
    ![Configurer l’authentification unique][8]

2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooQuestetra Suite BPM** page, sélectionnez **Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Authentification unique Azure AD][9]

3. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d'entreprise **Questetra BPM Suite** en tant qu'administrateur.

4. Dans le menu hello haut de hello, cliquez sur **paramètres système**. 
   
    ![Authentification unique Azure AD][10]

5. tooopen hello **SingleSignOnSAML** , cliquez sur **SSO (SAML)**. 
   
    ![Authentification unique Azure AD][11]

6. Bonjour portail Azure classic sur hello **configurer les paramètres de l’application** boîte de dialogue de page, effectuer hello comme suit : 
   
    ![Configurer les paramètres d’application][13]
   
    a. Vous **Questetra BPM Suite** site d’entreprise, Bonjour section d’informations SP, hello de copie **URL ACS**, puis collez-la dans hello **URL de connexion** zone de texte.
   
    b. Vous **Questetra BPM Suite** site d’entreprise, Bonjour section d’informations SP, hello de copie **ID d’entité**, puis collez-la dans hello **URL de l’émetteur** zone de texte.
   
    c. Vous **Questetra BPM Suite** site d’entreprise, Bonjour section d’informations SP, hello de copie **URL ACS**, puis collez-la dans hello **URL de réponse** zone de texte.
   
    d. Cliquez sur **Suivant**.

7. Sur hello **configurer l’authentification unique à la Suite de BPM Questetra** , cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello localement sur votre ordinateur.
   
    ![Configurer l’authentification unique][14]

8. Vous **Questetra BPM Suite** site d’entreprise, effectuez hello comme suit : 
   
    ![Configurer l’authentification unique][15]
   
    a. Sélectionnez **Activer l'authentification unique**.
   
    b. Sur hello portail Azure classic, copiez hello **URL de l’émetteur** valeur, puis collez-le dans hello **ID d’entité** zone de texte.
   
    c. Sur hello portail Azure classic, copiez hello **-Service URL d’authentification** valeur, puis collez-le dans hello **URL de la page connexion** zone de texte.
   
    d. Sur hello portail Azure classic, copiez hello **URL de Service de déconnexion unique** valeur, puis collez-le dans hello **URL de la page de déconnexion** zone de texte.
   
    e. Bonjour **NameID format** zone de texte, type **urn : oasis : noms : tc : SAML:1.1:nameid-format : emailAddress**.

    f. Créez un fichier encodé en base 64 à partir du certificat téléchargé. 

    >[!TIP] 
    >Pour plus d’informations, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o).

    g. Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite dans hello **certificat de Validation** zone de texte. 

    h. Cliquez sur **Enregistrer**.

1. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**. 
   
    ![Qu’est-ce qu’Azure AD Connect ?][17]

2. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.  
   
    ![Qu’est-ce qu’Azure AD Connect ?][18]


### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
objectif Hello de cette section est toocreate un utilisateur de test dans le portail Azure classic appelé Britta Simon de hello.

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Créer un utilisateur de test Azure AD][100] 

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Créer un utilisateur de test Azure AD][101] 

4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**. 
   
    ![Créer un utilisateur de test Azure AD][102] 

5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Créer un utilisateur de test Azure AD][103]
   
    a. Dans **Type d’utilisateur**, sélectionnez **Nouvel utilisateur dans votre organisation**.
   
    b. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.
   
    c. Cliquez sur Suivant.

6. Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit : 
   
    ![Créer un utilisateur de test Azure AD][104] 
   
    a. Bonjour **prénom** zone de texte, type **Brian**. 
   
    b. Bonjour **nom** zone de texte, type, **Simon**.
   
    c. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.
   
    d. Bonjour **rôle** liste, sélectionnez **utilisateur**.
   
    e. Cliquez sur **Suivant**.

7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.
   
    ![Créer un utilisateur de test Azure AD][105]  

8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Créer un utilisateur de test Azure AD][106]   
   
    a. Notez la valeur hello hello **nouveau mot de passe**.
   
    b. Cliquez sur **Terminé**.   

### <a name="creating-a-questetra-bpm-suite-test-user"></a>Création d'un utilisateur de test Questetra BPM Suite
objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Questetra BPM Suite.

**toocreate un utilisateur appelé Britta Simon Questetra BPM suite effectuer hello comme suit :**

1. Site d’entreprise Questetra BPM Suite tooyour ouverture de session en tant qu’administrateur.
2. Accédez trop**paramètres système > liste de l’utilisateur > nouvel utilisateur**. 
3. Dans la boîte de dialogue Nouvel utilisateur hello, procédez hello comme suit : 
   
    ![Créer un utilisateur de test][300] 
   
    a. Bonjour **nom** zone de texte, tapez le nom d’utilisateur de Brian dans Azure AD.
   
    b. Bonjour **messagerie** zone de texte, tapez le nom d’utilisateur de Brian dans Azure AD.
   
    c. Bonjour **mot de passe** zone de texte, tapez un mot de passe.

4. Cliquez sur **Ajouter un nouvel utilisateur**.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD
objectif Hello de cette section est tooenabling toouse Britta Simon Azure l’authentification unique en accordant son tooQuestetra accès Suite BPM.

![Qu’est-ce qu’Azure AD Connect ?][200]

**tooassign Britta Simon tooQuestetra Suite BPM, effectuez hello comme suit :**

1. Dans hello Azure portail classique, la vue applications hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Qu’est-ce qu’Azure AD Connect ?][201]
2. Dans la liste des applications hello, sélectionnez **Questetra BPM Suite**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][205]
3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][202]
4. Dans la liste des utilisateurs hello, sélectionnez **Britta Simon**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][203]
5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.
   
    ![Qu’est-ce qu’Azure AD Connect ?][204]

### <a name="testing-single-sign-on"></a>Test de l’authentification unique
objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.  
Lorsque vous cliquez sur mosaïque Questetra BPM Suite hello hello volet d’accès, vous devez obtenir l’application de Questetra BPM Suite automatiquement signé sur tooyour.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->
[1]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_01.png


[8]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_06.png
[9]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_02.png
[10]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_03.png
[11]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_04.png
[12]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_05.png
[13]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_06.png
[14]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_07.png
[15]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_08.png
[16]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_09.png
[17]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_10.png
[18]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_08.png


[100]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_09.png 
[101]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_10.png 
[102]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_11.png 
[103]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_12.png 
[104]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_13.png 
[105]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_14.png 
[106]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_15.png 


[200]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_16.png 
[201]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_17.png 
[202]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_18.png
[203]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_19.png
[204]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/tutorial_general_20.png
[205]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_12.png

[300]: ./media/active-directory-saas-questetra-bpm-suite-tutorial/questera_bpm_suite_11.png 
