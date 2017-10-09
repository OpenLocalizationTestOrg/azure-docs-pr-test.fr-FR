---
title: "Didacticiel : Intégration d’Azure Active Directory à Replicon | Microsoft Docs"
description: "Découvrez comment toouse Replicon avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>Didacticiel : Intégration d’Azure Active Directory à Replicon
objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Replicon. scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un locataire Replicon

À l’issue de ce didacticiel, hello Azure AD utilisateurs tooReplicon sera toosingle en mesure de l’authentification sur application hello à votre site d’entreprise Replicon (service initiée par le fournisseur de session) ou à l’aide de hello [Introduction toohello accès Panneau de configuration](active-directory-saas-access-panel-introduction.md).

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

1. Activation de l’intégration d’application hello pour Replicon
2. Configuration de l’authentification unique (SSO)
3. Configuration de l'approvisionnement des utilisateurs
4. Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scénario")

## <a name="enable-hello-application-integration-for-replicon"></a>Activer l’intégration d’application hello pour Replicon
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Replicon.

**intégration d’application hello tooenable pour Replicon, procédez hello comme suit :**

1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")
4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Ajouter une application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Ajouter une application")
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Ajouter une application à partir de la galerie](./media/active-directory-saas-replicon-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Bonjour **zone de recherche**, type **Replicon**.
   
    ![Galerie d’applications](./media/active-directory-saas-replicon-tutorial/IC777799.png "Galerie d’applications")
7. Dans le volet de résultats hello, sélectionnez **Replicon**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooReplicon avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello **Replicon** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configurer l’authentification unique")
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooReplicon** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configurer l’authentification unique")
3. Sur hello **Configure App URL** page, effectuer hello comme suit :
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configurer l’URL de l’application")
  1. Bonjour **URL de connexion Replicon** zone de texte, tapez l’URL de votre client Replicon (par exemple : *https://na2.replicon.com/company/saml2/sp-sso/post*).
  2. Bonjour **URL de réponse Replicon** zone de texte, tapez votre URL Replicon **AssertionConsumerService** URL (par exemple : *https://global.replicon.com/ ! / saml2/entreprise/sso/post*).  
      
     >[!NOTE]
     >Vous pouvez obtenir hello URL à partir des métadonnées Replicon hello : **https://global.replicon.com/ ! /saml2/\<YourCompanyKey\>**.
     > 
     > 
 
  3. Cliquez sur **Suivant**.

4. Sur hello **configurer l’authentification unique sur Replicon** page, toodownload vos métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez les métadonnées hello sur votre ordinateur.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configurer l’authentification unique")
5. Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Replicon en tant qu’administrateur.

6. tooconfigure SAML 2.0, effectuez hello comme suit :
   
    ![Activer l’authentification SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Activer l’authentification SAML")
  
  1. toodisplay hello **EnableSAML Authentication2** boîte de dialogue, ajouter hello suivant tooyour URL, après votre clé d’entreprise : **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**  
    * Hello Voici schéma hello de hello des URL complète :  
   **https://na2.replicon.com/\<CléDeVotreEntreprise\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**
   2. Cliquez sur hello  **+**  tooexpand hello **v20Configuration** section.
   3. Cliquez sur hello  **+**  tooexpand hello **metaDataConfiguration** section.
   4. Cliquez sur **choisir un fichier**, tooselect votre fichier XML de métadonnées de fournisseur identité, puis cliquez sur **Submit**.

7. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configurer l’authentification unique")
   
## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur

Dans l’ordre tooenable le toolog d’utilisateurs Azure AD à Replicon, ils doivent être configurés dans Replicon.  

Dans les cas de hello de Replicon, cette configuration est une tâche manuelle.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Dans une fenêtre de navigateur web, connectez-vous à votre site d’entreprise Replicon en tant qu’administrateur.
2. Accédez trop**Administration \> utilisateurs**.
   
    ![Utilisateurs](./media/active-directory-saas-replicon-tutorial/IC777806.png "Utilisateurs")
3. Cliquez sur **+Add User**.
   
    ![Ajouter un utilisateur](./media/active-directory-saas-replicon-tutorial/IC777807.png "Ajouter un utilisateur")
4. Bonjour **profil utilisateur** section, effectuer hello comme suit :
   
    ![Profil utilisateur](./media/active-directory-saas-replicon-tutorial/IC777808.png "Profil utilisateur")
   
  1. Bonjour **nom de connexion** zone de texte, hello de type Azure AD adresse de messagerie de l’utilisateur hello Azure AD que vous tooprovision.
  2. Pour **Authentication Type**, sélectionnez **SSO**.
  3. Bonjour **service** zone de texte, tapez le département de l’utilisateur hello.
  4. Pour **Employee Type**, sélectionnez **Administrator**.
  5. Cliquez sur **Save User Profile**.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Replicon utilisateur compte outil de création ou API fournie par Replicon tooprovision des comptes d’utilisateur AAD.
> 
> 

## <a name="assign-users"></a>Affecter des utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

**tooassign utilisateurs tooReplicon, effectuer hello comme suit :**

1. Bonjour portail Azure classic, créez un compte de test.

2. Sur hello **Replicon** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
    ![Affecter des utilisateurs](./media/active-directory-saas-replicon-tutorial/IC777809.png "Affecter des utilisateurs")

3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
    ![Oui](./media/active-directory-saas-replicon-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

