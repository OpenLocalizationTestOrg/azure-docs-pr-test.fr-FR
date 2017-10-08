---
title: "Didacticiel : Intégration d’Azure Active Directory à ServiceNow | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de ServiceNow et de ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: df6a07dd1aa437198fbdb9d0a04ea14f3a320249
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a>Didacticiel : Intégration d’Azure Active Directory à ServiceNow
Dans ce didacticiel, vous apprendrez comment toointegrate ServiceNow et ServiceNow Express avec Azure Active Directory (Azure AD).

Intégration de ServiceNow et ServiceNow Express avec Azure AD offre hello avantages suivants :

* Vous pouvez contrôler dans Azure AD qui a accès tooServiceNow et de ServiceNow Express
* Vous pouvez activer vos utilisateurs tooautomatically get connecté tooServiceNow et le ServiceNow Express (Single Sign-On) avec leurs comptes Azure AD
* Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure classic

Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).

## <a name="prerequisites"></a>Composants requis
tooconfigure intégration d’Azure AD avec ServiceNow et de ServiceNow Express, vous devez hello éléments suivants :

* Un abonnement Azure AD
* Pour ServiceNow, une instance ou un locataire ServiceNow, version Calgary ou supérieure
* Pour ServiceNow Express, une instance ServiceNow Express, version Helsinki ou supérieure
* client de ServiceNow Hello doit avoir hello [plusieurs fournisseur unique signe de plug-in](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) activé. Cette opération est possible en [envoyant une demande de service](https://hi.service-now.com). 

> [!NOTE]
> tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.
> 
> 

tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :

* Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.
* Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Description du scénario
Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test. scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :

1. Ajout de ServiceNow à partir de la galerie de hello
2. Configuration et test de l’authentification unique Azure AD pour ServiceNow ou ServiceNow Express

## <a name="adding-servicenow-from-hello-gallery"></a>Ajout de ServiceNow à partir de la galerie de hello
tooconfigure hello l’intégration de ServiceNow ou ServiceNow Express dans Azure AD, vous devez tooadd ServiceNow à partir de la liste de tooyour hello Galerie d’applications SaaS gérées. 

**tooadd ServiceNow à partir de la galerie hello, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**. 
   
    ![Active Directory][1]
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications][2]
4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Applications][3]
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Applications][4]
6. Dans la zone de recherche de hello, tapez **ServiceNow**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. Dans le volet de résultats hello, sélectionnez **ServiceNow**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuration et test de l’authentification unique Azure AD
Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec ServiceNow ou ServiceNow Express avec un utilisateur de test appelé « Britta Simon ».

Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ServiceNow est tooa utilisateur dans Azure AD. En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ServiceNow doit toobe établie.
Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ServiceNow. tooconfigure et test Azure AD l’authentification unique à ServiceNow, vous devez hello toocomplete suivant des blocs de construction :

1. **[Configuration d’Azure AD Single Sign-On pour ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
2. **[Configuration d’Azure AD Single Sign-On pour ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.
3. **[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.
4. **[Création d’un utilisateur de test ServiceNow](#creating-a-servicenow-test-user)**  -toohave de Britta Simon dans ServiceNow qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.
5. **[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.
6. **[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.

> [!NOTE]
> Si vous souhaitez tooconfigure ServiceNow omettez l’étape 2. De même, si vous souhaitez tooconfigure ServiceNow Express omettez l’étape 1.
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a>Configuration de l’authentification unique Azure AD pour ServiceNow
1. Dans le portail classique hello Azure AD, sur hello **ServiceNow** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue .
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurer l’authentification unique")

2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooServiceNow** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurer l’authentification unique")

3. Sur hello **configurer les paramètres de l’application** page, effectuer hello comme suit :
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurer l’URL de l’application")
   
    a. Bonjour **ServiceNow URL de connexion** zone de texte, tapez l’URL utilisée par votre application de ServiceNow sur toosign tooyour utilisateurs hello modèle : `https://<instance-name>.service-now.com`.
   
    b. Bonjour **identificateur** zone de texte, tapez l’URL utilisée par votre application de ServiceNow sur toosign tooyour utilisateurs hello modèle : `https://<instance-name>.service-now.com`.
   
    c. Cliquez sur **Suivant**

4. toohave Azure AD est automatiquement configurer ServiceNow pour l’authentification SAML, entrez votre nom d’instance ServiceNow, le nom d’utilisateur administrateur et le mot de passe administrateur Bonjour **configurer automatiquement l’authentification unique sur** écran et cliquez sur  *Configurer*. Notez que ce nom d’utilisateur administrateur de hello fourni doit avoir hello **security_admin** rôle attribué dans ServiceNow pour cette toowork. Dans le cas contraire, toomanually configurer ServiceNow toouse Azure AD comme fournisseur d’identité SAML, cliquez sur **configurer manuellement l’application hello pour l’authentification unique sur**, puis cliquez sur **suivant** et hello terminée étapes suivantes.
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurer l’URL de l’application")

5. Sur hello **configurer l’authentification unique auprès de ServiceNow** , cliquez sur **télécharger le certificat**, enregistrez le fichier de certificat hello localement sur votre ordinateur.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurer l’authentification unique")

6. Authentification tooyour application ServiceNow en tant qu’administrateur.

7. Activer hello *intégration - plusieurs fournisseur d’authentification programme d’installation unique* plug-in en suivant hello les étapes suivantes :
   
    a. Dans le volet de navigation hello sur le côté gauche de hello, accédez trop**définition système** section, puis cliquez sur **plug-ins**.
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activer le plug-in")
   
    b. Recherchez *Integration - Multiple Provider Single Sign-On Installer* (Intégration - Programme d’installation de l’authentification unique à plusieurs fournisseurs).
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activer le plug-in")
   
    c. Sélectionnez le plug-in hello. Cliquez avec le bouton droit et sélectionnez **Activate/Upgrade** (Activer/Mettre à niveau).
   
    d. Cliquez sur hello **activer** bouton.

8. Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **propriétés**.  
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configurer l’URL de l’application")

9. Sur hello **plusieurs propriétés de l’authentification unique de fournisseur** boîte de dialogue, effectuer hello comme suit :
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configurer l’URL de l’application")
   
    a. Pour **Enable multiple provider SSO**, sélectionnez **Yes**.
   
    b. En tant que **activer obtenue de la journalisation du débogage hello plusieurs fournisseur SSO integration**, sélectionnez **Oui**.
   
    c. Dans **champ hello sur utilisateur de hello table...**  zone de texte, type **nom_utilisateur**.
   
    d. Cliquez sur **Enregistrer**.

10. Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **x509 certificats**.
    
     ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configurer l’authentification unique")

11. Sur hello **certificats X.509** boîte de dialogue, cliquez sur **nouveau**.
    
     ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configurer l’authentification unique")

12. Sur hello **certificats X.509** boîte de dialogue, effectuer hello comme suit :
    
     ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurer l’authentification unique")
    
     a. Cliquez sur **Nouveau**.
    
     b. Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : **TestSAML2.0**).
    
     c. Sélectionnez **Active**.
    
     d. Pour **Format**, sélectionnez **PEM**.
    
     e. Pour **Type**, sélectionnez **Trust Store Cert**.
    
     f. Ouvrez votre certificat codé en Base64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **PEM Certificate** zone de texte.
    
     g. Cliquez sur **Update**.

13. Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **fournisseurs d’identité**.
    
     ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configurer l’authentification unique")

14. Sur hello **fournisseurs d’identité** boîte de dialogue, cliquez sur **nouveau**:
    
     ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configurer l’authentification unique")

15. Sur hello **fournisseurs d’identité** boîte de dialogue, cliquez sur **SAML2 mise à jour 1 ?**:
    
     ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configurer l’authentification unique")

16. Dans la boîte de dialogue Propriétés de mise à jour 1 SAML2 hello, procédez hello comme suit :
    
     ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configurer l’authentification unique")

    a. Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : **SAML 2.0**).

    b. Bonjour **champ utilisateur** zone de texte, type **messagerie** ou **nom_utilisateur**, selon le champ utilisé toouniquely identifier les utilisateurs dans votre déploiement de ServiceNow. 

    > [!NOTE] 
    > Vous pouvez tooemit de configuration Azure AD un ID d’utilisateur hello Azure AD (nom d’utilisateur principal) ou que vous hello adresse de messagerie comme hello identificateur unique dans le jeton SAML de hello en va de toohello **ServiceNow > attributs > Single Sign-On** section de Hello portail Azure classic et mappage hello souhaité champ toohello **nameidentifier** attribut. valeur de Hello pour l’attribut sélectionné de hello dans Azure AD (par exemple, nom d’utilisateur principal) doit correspondre à valeur hello stocké dans ServiceNow pour le champ hello entrée (par exemple, nom_utilisateur)

    c. Dans le portail classique de hello Azure AD, copiez hello **ID fournisseur d’identité** valeur, puis collez-le dans hello **URL du fournisseur d’identité** zone de texte.

    d. Dans le portail classique de hello Azure AD, copiez hello **URL de la demande d’authentification** valeur, puis collez-le dans hello **AuthnRequest du fournisseur d’identité** zone de texte.

    e. Dans le portail classique de hello Azure AD, copiez hello **URL de Service de déconnexion unique** valeur, puis collez-le dans hello **'s SingleLogoutRequest du fournisseur d’identité** zone de texte.

    f. Bonjour **ServiceNow Homepage** zone de texte, tapez l’URL de votre page d’accueil d’instance ServiceNow hello.

    > [!NOTE] 
    > page d’accueil d’instance Hello ServiceNow est une concaténation de votre **URL de client ServieNow** et **/navpage.do** (par exemple :`https://fabrikam.service-now.com/navpage.do`).

    g. Bonjour **ID d’entité / émetteur** zone de texte, tapez l’URL de votre locataire ServiceNow hello.

    h. Bonjour **Audience URL** zone de texte, tapez l’URL de votre locataire ServiceNow hello. 

    i. Bonjour **une liaison de protocole pour ' s SingleLogoutRequest hello d’IDP** zone de texte, type **urn : oasis : noms : tc : SAML:2.0:bindings:HTTP-rediriger**.

    j. Bonjour NameID Policy la zone de texte, tapez **urn : oasis : noms : tc : SAML:1.1:nameid-format : non spécifiée**.

    k. Désélectionnez **Créer une classe de contexte d’authentification**.

    l. Bonjour **the AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`. Cela n’est nécessaire que si votre organisation utilise uniquement le cloud. Si vous utilisez des services ADFS ou MFA locaux pour l’authentification, vous ne devez pas configurer cette valeur. 

    m. Dans la zone de texte **Variation d’horloge**, entrez **60**.

    n. Pour **Script d’authentification unique**, sélectionnez **MultiSSO_SAML2_Update1**.

    o. En tant que **x509 certificat**, sélectionnez certificats hello que vous avez créé à l’étape précédente de hello.

    p. Cliquez sur **Envoyer**. 

1. Sur le portail classique hello Azure AD, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**. 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurer l’authentification unique")

2. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurer l’authentification unique")

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a>Configuration de l’authentification unique Azure AD pour ServiceNow Express
1. Dans le portail classique hello Azure AD, sur hello **ServiceNow** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue .
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configurer l’authentification unique")

2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooServiceNow** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configurer l’authentification unique")

3. Sur hello **configurer les paramètres de l’application** page, effectuer hello comme suit :
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configurer l’URL de l’application")
   
    a. Bonjour **ServiceNow URL de connexion** zone de texte, tapez l’URL utilisée par votre application de ServiceNow sur toosign tooyour utilisateurs hello modèle : `https://<instance-name>.service-now.com`.
   
    b. Bonjour **URL de l’émetteur** zone de texte, tapez l’URL utilisée par votre application de ServiceNow sur toosign tooyour utilisateurs hello modèle `https://<instance-name>.service-now.com`.
   
    c. Cliquez sur **Suivant**

4. Cliquez sur **configurer manuellement l’application hello pour l’authentification unique sur**, puis cliquez sur **suivant** hello complète comme suit.
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configurer l’URL de l’application")

5. Sur hello **configurer l’authentification unique auprès de ServiceNow** , cliquez sur **télécharger le certificat**, enregistrez le fichier de certificat hello localement sur votre ordinateur, puis cliquez sur **suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configurer l’authentification unique")

6. Authentification tooyour application ServiceNow Express en tant qu’administrateur.

7. Dans le volet de navigation hello sur le côté gauche de hello, cliquez sur **Single Sign-On**.  
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configurer l’URL de l’application")

8. Sur hello **Single Sign-On** boîte de dialogue, cliquez sur icône de configuration hello sur supérieur hello droite et définissez hello propriétés suivantes :
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configurer l’URL de l’application")
   
    a. Activer/désactiver **activer plusieurs fournisseur SSO** toohello droite.
   
    b. Activer/désactiver **activer l’enregistrement pour hello plusieurs fournisseur d’intégration de l’authentification unique de débogage** toohello droite.
   
    c. Dans **champ hello sur utilisateur de hello table...**  zone de texte, type **nom_utilisateur**.
9. Sur hello **Single Sign-On** boîte de dialogue, cliquez sur **ajouter un nouveau certificat**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configurer l’authentification unique")
10. Sur hello **certificats X.509** boîte de dialogue, effectuer hello comme suit :
    
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configurer l’authentification unique")
    
    a. Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : **TestSAML2.0**).
    
    b. Sélectionnez **Active**.
    
    c. Pour **Format**, sélectionnez **PEM**.
    
    d. Pour **Type**, sélectionnez **Trust Store Cert**.
    
    e. Créez un fichier codé en base64 à partir du certificat téléchargé.
    
    > [!NOTE]
    > Pour plus d’informations, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o).
    > 
    > 
    
    f. Ouvrez votre certificat codé en Base64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **PEM Certificate** zone de texte.
    
    g. Cliquez sur **Update**.
11. Sur hello **Single Sign-On** boîte de dialogue, cliquez sur **ajouter un nouveau IdP**.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configurer l’authentification unique")
12. Sur hello **Ajouter nouveau fournisseur d’identité** boîte de dialogue, sous **configurer le fournisseur d’identité**, effectuer hello comme suit :
    
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configurer l’authentification unique")

    a. Bonjour **nom** zone de texte, tapez un nom pour votre configuration (par exemple : **SAML 2.0**).

    b. Dans le portail classique de hello Azure AD, copiez hello **ID fournisseur d’identité** valeur, puis collez-le dans hello **URL du fournisseur d’identité** zone de texte.

    c. Dans le portail classique de hello Azure AD, copiez hello **URL de la demande d’authentification** valeur, puis collez-le dans hello **AuthnRequest du fournisseur d’identité** zone de texte.

    d. Dans le portail classique de hello Azure AD, copiez hello **URL de Service de déconnexion unique** valeur, puis collez-le dans hello **'s SingleLogoutRequest du fournisseur d’identité** zone de texte.

    e. En tant que **certificat de fournisseur d’identité**, sélectionnez certificats hello que vous avez créé à l’étape précédente de hello.


1. Cliquez sur **paramètres avancés**et sous **des propriétés supplémentaires du fournisseur d’identité**, effectuer hello comme suit :
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configurer l’authentification unique")
   
    a. Bonjour **une liaison de protocole pour ' s SingleLogoutRequest hello d’IDP** zone de texte, type **urn : oasis : noms : tc : SAML:2.0:bindings:HTTP-rediriger**.
   
    b. Bonjour **NameID Policy** zone de texte, type **urn : oasis : noms : tc : SAML:1.1:nameid-format : non spécifiée**.    
   
    c. Bonjour **the AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.
   
    d. Désélectionnez **Créer une classe de contexte d’authentification**.

2. Sous **des propriétés de fournisseur de Service supplémentaires**, effectuer hello comme suit :
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configurer l’authentification unique")
   
    a. Bonjour **ServiceNow Homepage** zone de texte, tapez l’URL de votre page d’accueil d’instance ServiceNow hello.
   
    > [!NOTE]
    > page d’accueil d’instance Hello ServiceNow est une concaténation de votre **URL de client ServieNow** et **/navpage.do** (par exemple : `https://fabrikam.service-now.com/navpage.do`).
    > 
    > 
   
    b. Bonjour **ID d’entité / émetteur** zone de texte, tapez l’URL de votre locataire ServiceNow hello.
   
    c. Bonjour **URI d’Audience** zone de texte, tapez l’URL de votre locataire ServiceNow hello. 
   
    d. Dans la zone de texte **Variation d’horloge**, entrez **60**.
   
    e. Bonjour **champ utilisateur** zone de texte, type **messagerie** ou **nom_utilisateur**, selon le champ utilisé toouniquely identifier les utilisateurs dans votre déploiement de ServiceNow.
   
    > [!NOTE]
    > Vous pouvez tooemit de configuration Azure AD un ID d’utilisateur hello Azure AD (nom d’utilisateur principal) ou que vous hello adresse de messagerie comme hello identificateur unique dans le jeton SAML de hello en va de toohello **ServiceNow > attributs > Single Sign-On** section de Hello portail Azure classic et mappage hello souhaité champ toohello **nameidentifier** attribut. valeur de Hello pour l’attribut sélectionné de hello dans Azure AD (par exemple, nom d’utilisateur principal) doit correspondre à valeur hello stocké dans ServiceNow pour le champ hello entrée (par exemple, nom_utilisateur)
    > 
    > 
   
    f. Cliquez sur **Enregistrer**. 

3. Sur le portail classique hello Azure AD, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **suivant**. 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configurer l’authentification unique")

4. Sur hello **Single sign-on confirmation** , cliquez sur **Complete**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configurer l’authentification unique")

## <a name="configuring-user-provisioning"></a>Configuration de l'approvisionnement des utilisateurs
objectif Hello de cette section est toooutline mode tooenable l’approvisionnement des utilisateurs d’utilisateur Active Directory de comptes tooServiceNow.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>configuration, de l’utilisateur tooconfigure effectuer hello comme suit :
1. Dans hello classique portail de gestion Azure, sur hello **ServiceNow** page d’intégration d’application, cliquez sur **configuration d’utilisateur**. 
   
    ![Approvisionnement d'utilisateurs](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Approvisionnement d’utilisateurs")

2. Sur hello **Entrez votre déploiement automatique d’utilisateur de ServiceNow informations d’identification tooenable** , fournissez hello suivant les paramètres de configuration :
   
     a. Bonjour **nom de l’Instance ServiceNow** zone de texte, le nom d’instance de type hello ServiceNow.
   
     b. Bonjour **nom d’utilisateur Admin ServiceNow** zone de texte, nom du type hello Hello compte d’administrateur ServiceNow.
   
     c. Bonjour **mot de passe Admin ServiceNow** zone de texte, un mot de passe type hello pour ce compte.
   
     d. Cliquez sur **valider** tooverify votre configuration.
   
     e. Cliquez sur hello **suivant** hello tooopen de bouton **étapes** page.
   
     f. Si vous souhaitez tooprovision tous les utilisateurs toothis application, sélectionnez «**approvisionner automatiquement tous les comptes d’utilisateur dans l’application de hello Active toothis**». 
   
    ![Étapes suivantes](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Étapes suivantes")
   
     g. Sur hello **étapes** , cliquez sur **Complete** toosave votre configuration.

### <a name="creating-an-azure-ad-test-user"></a>Création d’un utilisateur de test Azure AD
Dans cette section, vous créez un utilisateur de test dans le portail classique de hello appelé Britta Simon.

![Créer un utilisateur Azure AD][20]

**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**

1. Bonjour **portail Azure classic**, on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. liste de hello toodisplay d’utilisateurs, dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. tooopen hello **ajouter un utilisateur** boîte de dialogue, dans la barre d’outils de hello en bas de hello, cliquez sur **ajouter un utilisateur**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. Sur hello **faites-nous part de cet utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    a. Dans Type d’utilisateur, sélectionnez Nouvel utilisateur dans votre organisation.
   
    b. Bonjour, nom d’utilisateur **zone de texte**, type **BrittaSimon**.
   
    c. Cliquez sur **Suivant**.

6. Sur hello **profil utilisateur** boîte de dialogue de page, effectuer hello comme suit :
   
   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   a. Bonjour **prénom** zone de texte, type **Brian**.  
   
   b. Bonjour **nom** zone de texte, type, **Simon**.
   
   c. Bonjour **nom d’affichage** zone de texte, type **Britta Simon**.
   
   d. Bonjour **rôle** liste, sélectionnez **utilisateur**.
   
   e. Cliquez sur **Suivant**.

7. Sur hello **mot de passe temporaire Get** page de boîte de dialogue, cliquez sur **créer**.
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. Sur hello **mot de passe temporaire Get** boîte de dialogue de page, effectuer hello comme suit :
   
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    a. Notez la valeur hello hello **nouveau mot de passe**.
   
    b. Cliquez sur **Terminé**.   

### <a name="creating-a-servicenow-test-user"></a>Création d’un utilisateur de test ServiceNow
Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans ServiceNow. Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans ServiceNow. Si vous ne savez pas comment tooadd un dans votre ServiceNow ou le ServiceNow Express compte d’utilisateur, contactez l’équipe de support technique ServiceNow.

### <a name="assigning-hello-azure-ad-test-user"></a>Affectation d’utilisateur de test hello Azure AD
Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooServiceNow de son accès.

![Affecter des utilisateurs][200] 

**tooassign Britta Simon tooServiceNow, effectuez hello comme suit :**

1. Sur le portail classique hello, cliquez sur la vue applications hello tooopen, dans la vue active de hello, **Applications** dans le menu du haut hello.
   
    ![Affecter des utilisateurs][201] 

2. Dans la liste des applications hello, sélectionnez **ServiceNow**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. Dans le menu hello haut de hello, cliquez sur **utilisateurs**.
   
    ![Affecter des utilisateurs][203] 

4. Dans la liste de tous les utilisateurs de hello, sélectionnez **Britta Simon**.

5. Dans la barre d’outils de hello en bas de hello, cliquez sur **affecter**.
   
    ![Affecter des utilisateurs][205]

### <a name="testing-single-sign-on"></a>Test de l’authentification unique
objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.

Lorsque vous cliquez sur mosaïque ServiceNow hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour ServiceNow application.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
