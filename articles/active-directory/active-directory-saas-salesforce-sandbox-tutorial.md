---
title: "Didacticiel : intégration d’Azure Active Directory à Salesforce Sandbox | Microsoft Docs"
description: "Découvrez comment toouse Salesforce Sandbox avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Didacticiel : Intégration d’Azure Active Directory à Salesforce Sandbox

objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Salesforce Sandbox.  

>[!TIP]
>Pour les commentaires, consultez hello [page de support Azure](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Accordez sandbox hello capacité toocreate plusieurs copies de votre organisation dans des environnements distincts pour différentes raisons, notamment le développement, test et la formation, sans compromettre les données de salutation et toutes les applications dans votre production Salesforce organisation.  

Pour plus d’informations, consultez la page [Présentation de Sandbox](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un bac à sable (sandbox) dans Salesforce.com

Si vous n’avez encore un bac à sable valide dans Salesforce.com, vous devez toocontact Salesforce.

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

1. Activation de l’intégration d’application hello pour Salesforce Sandbox
2. Configuration de l’authentification unique (SSO)
3. Activation de votre domaine
4. Configuration de l'approvisionnement des utilisateurs
5. Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Scénario")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Activer l’intégration d’application hello pour Salesforce Sandbox
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Salesforce sandbox.

**intégration d’application hello tooenable pour Salesforce sandbox, procédez hello comme suit :**

1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
   ![Applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Applications")
4. tooopen hello **Galerie d’applications**, cliquez sur **ajouter une application**, puis cliquez sur **ajouter une application par mon organisation de toouse**.
   
   ![Comment vous souhaitez toodo ? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "Comment vous souhaitez toodo ?")
5. Bonjour **zone de recherche**, type **Salesforce Sandbox**.
   
   ![Galerie d’applications](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galerie d’applications")
6. Dans le volet de résultats hello, sélectionnez **Salesforce Sandbox**, puis cliquez sur **Complete** application hello de tooadd.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Salesforce Sandbox")
   
## <a name="configur-single-sign-on-sso"></a>Configuration de l’authentification unique (SSO)

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooSalesforce avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello **Salesforce Sandbox** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurer l’authentification unique")
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooSalesforce Sandbox** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Salesforce Sandbox")
3. Sur hello **Configure App URL** page hello **URL de connexion** zone de texte, tapez votre URL hello modèle `http://company.my.salesforce.com`, puis cliquez sur **suivant**.
   
   ![Configurer l’URL de l’application](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurer l’URL de l’application")
4. Si vous avez déjà configuré l’authentification unique pour une autre instance Salesforce Sandbox dans votre annuaire, vous devez également configurer hello **identificateur** toohave hello la même valeur que hello **URL de connexion**. 
 * Hello **identificateur** champ sont accessibles en vérifiant hello **afficher les paramètres avancés** case à cocher sur hello **Configure App URL** page de boîte de dialogue hello.
5. Sur hello **configurer l’authentification unique sur Salesforce Sandbox** , cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello sur votre ordinateur.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurer l’authentification unique")
6. Dans une autre fenêtre de navigateur web, connectez-vous à votre sandbox Salesforce en tant qu’administrateur.
7. Dans le menu hello haut de hello, cliquez sur **le programme d’installation**.
   
   ![Configuration](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Configuration")
8. Dans le volet de navigation hello hello gauche, cliquez sur **des contrôles de sécurité**, puis cliquez sur **paramètres d’authentification unique**.
   
   ![Paramètres d’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "paramètres d’authentification unique")
9. Sur la section de paramètres d’authentification unique de hello, procédez hello comme suit :
   
   ![Paramètres d’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "paramètres d’authentification unique")  
 1.  Sélectionnez **SAML Enabled**. 
 2.  Cliquez sur **Nouveau**.
10. Sur hello section de paramètres d’authentification unique SAML, procédez hello comme suit :
    
    ![SAML Single Sign On Settings (Paramètres d’authentification unique SAML)](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "SAML Single Sign On Settings (Paramètres d’authentification unique SAML)")  
 1. Dans la zone de texte Nom hello, tapez le nom de hello de configuration de hello (par exemple : *SPSSOWAAD\_Test*). 
 2. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Salesforce Sandbox** page de boîte de dialogue, hello de copie **URL de l’émetteur** valeur, puis collez-le dans hello **émetteur**zone de texte.
 3. Bonjour **Id d’entité** zone de texte, type **https://test.salesforce.com** s’il s’agit première instance Salesforce Sandbox hello, que vous ajoutez tooyour active. Si vous avez déjà ajouté une instance de bac à sable Salesforce, puis pour hello **ID d’entité** type Bonjour **URL de connexion**, qui doit être au format suivant :`http://company.my.salesforce.com`   
 4. Cliquez sur **Parcourir** hello de tooupload téléchargé le certificat.  
 5. En tant que **SAML Identity Type**, sélectionnez **Assertion contient hello ID de fédération à partir de l’objet utilisateur de hello**. 
 6. En tant que **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello Subject statement**.
 7. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Salesforce Sandbox** page de boîte de dialogue, hello de copie **URL de connexion distante** valeur, puis collez-le dans hello **fournisseur d’identité URL de connexion** zone de texte. 
 8. SFDC ne prend pas en charge la déconnexion SAML.  Pour résoudre ce problème, collez 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0' dans hello **Identity Provider Logout URL** zone de texte.
 9. Pour **Service Provider Initiated Request Binding (Liaison de demande initiée par le fournisseur de services)**, sélectionnez **HTTP POST**. 
 10. Cliquez sur **Enregistrer**.
11. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurer l’authentification unique")

## <a name="enable-your-domain"></a>Activer votre domaine
Cette section suppose que vous avez déjà créé un domaine.  Pour plus d’informations, consultez [Définition de votre nom de domaine](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable votre domaine, effectuer hello comme suit :**

1. Dans le volet de navigation gauche hello, cliquez sur **gestion des domaines**, puis cliquez sur **mon domaine.**
   
   ![Mon domaine](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "mon domaine")
   
   >[!NOTE]
   >Vérifiez que votre domaine a été correctement configuré. 
   > 
2. Bonjour **les paramètres de Page de connexion** , cliquez sur **modifier**, puis, en tant que **Service d’authentification**, sélectionnez nom hello Hello SAML unique Sign-On Setting de hello précédente et enfin cliquez sur **enregistrer**.
   
   ![Mon domaine](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "mon domaine")

Dès que vous avez un domaine configuré, vos utilisateurs doivent utiliser le bac à sable hello domaine URL toologin toohello Salesforce.  

valeur hello tooget hello URL, cliquez sur profil d’authentification unique hello que vous avez créé dans la section précédente de hello.

## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur
objectif Hello de cette section est toooutline mode tooenable l’approvisionnement des utilisateurs d’utilisateur Active Directory de comptes tooSalesforce Sandbox.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Dans le portail Salesforce hello, dans la barre de navigation supérieure hello, sélectionnez votre nom tooexpand votre menu utilisateur :
   
   ![My Settings (Mes paramètres)](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "My Settings (Mes paramètres)")
2. Dans votre menu utilisateur, sélectionnez **mes paramètres** tooopen votre **mes paramètres** page.
3. Dans le volet gauche de hello, cliquez sur **personnel** tooexpand hello section personnelle, puis cliquez sur **Reset My Security Token**:
   
   ![My Settings (Mes paramètres)](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "My Settings (Mes paramètres)")
4. Sur hello **Reset My Security Token** , cliquez sur **Reset Security Token** toorequest un e-mail contenant votre jeton de sécurité Salesforce.com.
   
   ![New Token (Nouveau jeton)](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "New Token (Nouveau jeton)")
5. Recherchez dans votre boîte de réception un courrier électronique provenant de Salesforce.com ayant pour objet «**salesforce.com.com security confirmation**» (confirmation de sécurité salesforce.com.com).
6. Passez en revue ce courrier électronique hello sécurité valeur du jeton.
7. Bonjour portail Azure classic sur hello **salesforce Sandbox** page d’intégration d’application, cliquez sur **configuration d’utilisateur** tooopen hello **configurer l’approvisionnement des utilisateurs**boîte de dialogue.
   
   ![Configurer l’approvisionnement de l’utilisateur](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "Configurer l’approvisionnement de l’utilisateur")
8. Sur hello **Entrez votre déploiement automatique d’utilisateur de Salesforce Sandbox informations d’identification tooenable** , fournissez hello suivant les paramètres de configuration :
   
   ![Salesforce Sandbox](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Salesforce Sandbox")   
 1. Bonjour **nom d’utilisateur Admin Salesforce Sandbox** zone de texte, tapez un bac à sable Salesforce compte nom a hello **administrateur système** profil dans Salesforce.com attribué.
 2. Bonjour **mot de passe Admin Salesforce Sandbox** zone de texte, un mot de passe type hello pour ce compte.
 3. Bonjour **jeton de sécurité utilisateur** zone de texte, collez hello valeur du jeton de sécurité.
 4. Cliquez sur **Validate** tooverify votre configuration.
 5. Cliquez sur hello **suivant** hello tooopen de bouton **Confirmation** page.
9. Sur hello **Confirmation** , cliquez sur **Complete** toosave votre configuration.
   
## <a name="assigning-users"></a>Affectation d’utilisateurs

tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

**tooassign utilisateurs tooSalesforce bac à sable, effectuez hello comme suit :**

1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello ** Salesforce Sandbox ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
   ![Oui](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Oui")

Vous devez maintenant attendre 10 minutes et vérifier que le compte de hello a été synchronisé tooSalesforce Sandbox.

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](https://msdn.microsoft.com/library/dn308586).

