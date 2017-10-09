---
title: "Didacticiel : Intégration d’Azure Active Directory à Coupa | Microsoft Docs"
description: "Découvrez comment toouse Coupa avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Didacticiel : Intégration d’Azure Active Directory à Coupa
objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Coupa.  
scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un abonnement Coupa pour lequel l’authentification unique (SSO) est activée

À l’issue de ce didacticiel, hello Azure AD utilisateurs tooCoupa sera toosingle en mesure de l’authentification sur application hello utilisant hello [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

* Activation de l’intégration d’application hello pour Coupa
* Configuration de l'authentification unique
* Configuration de l'approvisionnement des utilisateurs
* Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scénario")

## <a name="enable-hello-application-integration-for-coupa"></a>Activer l’intégration d’application hello pour Coupa
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Coupa.

**intégration d’application hello tooenable pour Coupa, procédez hello comme suit :**

1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
   ![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")
4. Cliquez sur **ajouter** bas hello de page de hello.
   
   ![Ajouter une application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Ajouter une application")
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
   ![Ajouter une application à partir de la galerie](./media/active-directory-saas-coupa-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Bonjour **zone de recherche**, type **Coupa**.
   
   ![Galerie d’applications](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galerie d’applications")
7. Dans le volet de résultats hello, sélectionnez **Coupa**, puis cliquez sur **Complete** application hello de tooadd.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooCoupa avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.  

Configuration de l’authentification unique pour Coupa nécessite que vous tooretrieve une valeur d’empreinte numérique à partir d’un certificat. Si vous n’êtes pas familiarisé avec cette procédure, consultez [comment tooretrieve valeur d’empreinte numérique d’un certificat](http://youtu.be/YKQF266SAxI).

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Se connecter tooyour site d’entreprise Coupa en tant qu’administrateur.
2. Accédez trop**le programme d’installation \> pour contrôler la sécurité**.
   
   ![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")
3. toodownload hello Coupa métadonnées fichier tooyour ordinateur, cliquez sur **télécharger et importer des métadonnées de Service Pack**.
   
   ![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")
4. Dans une autre fenêtre de navigateur, connectez-vous toohello portail Azure classic.
5. Sur hello **Coupa** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurer l’authentification unique")
6. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooCoupa** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurer l’authentification unique")
7. Sur hello **Configure App URL** page, effectuer hello comme suit :
   
   ![Configurer l’URL de l’application](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurer l’URL de l’application")   
   1. Bonjour **URL de connexion** zone de texte, tapez l’URL utilisée par votre toosign utilisateurs sur tooyour application Coupa (par exemple : «*http://company.Coupa.com*»).
   2. Ouvrez votre fichier de métadonnées Coupa téléchargé et copiez hello **AssertionConsumerService index/URL**.
   3. Bonjour **URL de réponse Coupa** zone de texte, collez hello **AssertionConsumerService index/URL** valeur.
   4. Cliquez sur **Suivant**.
8. Sur hello **configurer l’authentification unique sur Coupa** page, toodownload votre fichier de métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello localement sur votre ordinateur.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurer l’authentification unique")
9. Sur le site d’entreprise Coupa hello, accédez trop**le programme d’installation \> pour contrôler la sécurité**.
   
   ![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")
10. Bonjour **se connecter à l’aide des informations d’identification Coupa** section, effectuer hello comme suit :  

   ![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials") 
   1. Sélectionnez **Log in using SAML**.
   2. Cliquez sur **Parcourir** tooupload votre fichier de métadonnées téléchargé Azure Active.
   3. Cliquez sur **Enregistrer**.
11. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
    
   ![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurer l’authentification unique")
    
## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur

Dans l’ordre tooenable Azure AD les utilisateurs toolog à Coupa, vous devez les configurer dans Coupa.  

* Dans les cas de hello de Coupa, cette configuration est une tâche manuelle.

**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**

1. Connectez-vous à tooyour **Coupa** site d’entreprise en tant qu’administrateur.
2. Dans le menu hello haut de hello, cliquez sur **le programme d’installation**, puis cliquez sur **utilisateurs**.
   
   ![Utilisateurs](./media/active-directory-saas-coupa-tutorial/IC791908.png "Utilisateurs")
3. Cliquez sur **Create**.
   
   ![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")
4. Bonjour **utilisateur créer** section, effectuer hello comme suit :
   
   ![Détails de l’utilisateur](./media/active-directory-saas-coupa-tutorial/IC791910.png "Détails de l’utilisateur")
   
   1. Hello de type **connexion**, **prénom**, **nom**, **ID de connexion unique**, **messagerie** attributs d’un compte Azure Active Directory valide, que vous voulez tooprovision dans hello relatives des zones de texte.
   2. Cliquez sur **Créer**.   
   >[!NOTE]
   >détenteur du compte de Hello Azure Active Directory reçoit un e-mail avec un compte de hello tooconfirm lien avant son activation. 
   > 

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Coupa utilisateur compte outil de création ou API fournie par Coupa tooprovision des comptes d’utilisateur AAD. 
> 

## <a name="assign-users"></a>Affecter des utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

**tooassign utilisateurs tooCoupa, effectuer hello comme suit :**

1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello ** Coupa ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-coupa-tutorial/IC791911.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
   ![Oui](./media/active-directory-saas-coupa-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

