---
title: "Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Secure | Microsoft Docs"
description: "Découvrez comment toouse TOPdesk - Secure avec Azure Active Directory tooenable l’authentification unique, l’approvisionnement automatisé et bien plus encore !."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a>Didacticiel : Intégration d’Azure Active Directory à TOPdesk - Secure
objectif Hello de ce didacticiel est d’intégration de hello tooshow d’Azure et de TOPdesk - Secure.  
scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un abonnement TOPdesk - Secure pour lequel l’authentification unique est activée

Quand ils auront terminé ce didacticiel, les utilisateurs de hello Azure AD vous avez affecté tooTOPdesk - sécurisé va être toosingle en mesure de l’authentification sur application hello à TOPdesk - site d’entreprise sécurisé (service initiée par le fournisseur de session), ou à l’aide de hello [Introduction Volet d’accès de toohello](active-directory-saas-access-panel-introduction.md).

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

1. Activation de l’intégration d’application hello pour TOPdesk - Secure
2. Configuration de l'authentification unique
3. Configuration de l'approvisionnement des utilisateurs
4. Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scénario")

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a>Activation de l’intégration d’application hello pour TOPdesk - Secure
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour TOPdesk - Secure.

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a>intégration d’application hello tooenable pour TOPdesk - Secure, procédez hello comme suit :
1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")

2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.

3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")

4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Ajouter une application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Ajouter une application")

5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Ajouter une application à partir de la galerie](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Ajouter une application à partir de la galerie")

6. Bonjour **zone de recherche**, type **TOPdesk - Secure**.
   
    ![Galerie d’applications](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Galerie d’applications")

7. Dans le volet de résultats hello, sélectionnez **TOPdesk - Secure**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")

## <a name="configuring-single-sign-on"></a>Configuration de l'authentification unique
objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooTOPdesk - Secure avec leur compte dans Azure AD en utilisant la fédération basée sur hello protocole SAML.  
Configurer l’authentification unique pour TOPdesk - Secure nécessite que vous tooupload un fichier d’icône de logo. fichier d’icône tooget hello, équipe de support technique TOPdesk hello contact.

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a>tooconfigure sur l’authentification unique, effectuer hello comme suit :
1. Ouverture de session tooyour **TOPdesk - Secure** site d’entreprise en tant qu’administrateur.
2. Bonjour **TOPdesk** menu, cliquez sur **paramètres**.
   
    ![Paramètres](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Paramètres")

3. Cliquez sur **Login Settings**.
   
    ![Paramètres de connexion](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Paramètres de connexion")

4. Développez hello **les paramètres de connexion** menu, puis sur **général**.
   
    ![Général](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Général")

5. Bonjour **Secure** section Hello **connexion SAML** configuration section, effectuer hello comme suit :
   
    ![Paramètres techniques](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Paramètres techniques")
   
    a. Cliquez sur **télécharger** toodownload hello du fichier de métadonnées publiques et les enregistrer localement sur votre ordinateur.
   
    b. Ouvrez le fichier de métadonnées hello et recherchez hello **AssertionConsumerService** nœud.
    
    ![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")
   
    c. Hello de copie **AssertionConsumerService** valeur.  
      
    > [!NOTE]
    > Vous devez serez hello valeur Bonjour **Configure App URL** section plus loin dans ce didacticiel.
    > 
    > 

6. Dans une autre fenêtre de navigateur web, connectez-vous à votre **portail Azure Classic** en tant qu’administrateur.

7. Sur hello **TOPdesk - Secure** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello ** configurer Single Sign On ** boîte de dialogue.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configurer l’authentification unique")

8. Sur hello **Comment voulez-vous comme toosign utilisateurs sur tooTOPdesk - Secure** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configurer l’authentification unique")

9. Sur hello **Configure App URL** page, effectuer hello comme suit :
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configurer l’URL de l’application")
   
    a. Bonjour **TOPdesk - Secure URL de connexion** zone de texte, tapez l’URL hello utilisé par votre toosign d’utilisateurs dans votre application TOPdesk - Secure (par exemple : «*https://qssolutions.topdesk.net*»).
   
    b. Bonjour **TOPdesk – URL de réponse publique** zone de texte, collez hello **TOPdesk - Secure AssertionConsumerService URL** (par exemple : «*https://qssolutions.topdesk.net/tas/public/login/saml*")
   
    c. Cliquez sur **Suivant**.

10. Sur hello **configurer l’authentification unique sur TOPdesk - Secure** page, toodownload votre fichier de métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier hello localement sur votre ordinateur.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configurer l’authentification unique")

11. toocreate un fichier de certificat, effectuez hello comme suit :
    
    ![Certificat](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificat")
    
    a. Fichier de métadonnées téléchargé hello ouvert.
    b. Développez hello **RoleDescriptor** nœud qui a un **xsi : type** de **fed : ApplicationServiceType**.
    c. Copier la valeur hello Hello **X509Certificate** nœud.
    d. Hello enregistrer copié **X509Certificate** valeur localement sur votre ordinateur dans un fichier.

12. Sur votre TOPdesk - Secure site d’entreprise, Bonjour **TOPdesk** menu, cliquez sur **paramètres**.
    
    ![Paramètres](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Paramètres")

13. Cliquez sur **Login Settings**.
    
    ![Paramètres de connexion](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Paramètres de connexion")

14. Développez hello **les paramètres de connexion** menu, puis sur **général**.
    
    ![Général](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Général")

15. Bonjour **Public** , cliquez sur **ajouter**.
    
    ![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")

16. Sur hello **l’assistant configuration de SAML** boîte de dialogue de page, effectuer hello comme suit :
    
    ![Assistant de configuration SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Assistant de configuration SAML")
    
    a. tooupload vos métadonnées téléchargée un fichier, sous **les métadonnées de fédération**, cliquez sur **Parcourir**.

    b. tooupload fichier de votre certificat, sous **Certificate (RSA)**, cliquez sur **Parcourir**.

    c. fichier de logo hello tooupload que vous avez obtenu à partir de l’équipe de support technique TOPdesk hello sous **icône du Logo**, cliquez sur **Parcourir**.

    d. Bonjour **attribut nom d’utilisateur** zone de texte, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.

    e. Bonjour **nom d’affichage** zone de texte, tapez un nom pour votre configuration.

    f. Cliquez sur **Enregistrer**.

17. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configurer l’authentification unique")

## <a name="configuring-user-provisioning"></a>Configuration de l'approvisionnement des utilisateurs
Dans l’ordre tooenable Azure AD les utilisateurs toolog à TOPdesk - sécurisé, vous devez les configurer dans TOPdesk - Secure.  
Dans le cas de hello de TOPdesk -, cette configuration est une tâche manuelle.

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a>configuration, de l’utilisateur tooconfigure effectuer hello comme suit :
1. Ouverture de session tooyour **TOPdesk - Secure** site d’entreprise en tant qu’administrateur.
2. Dans le menu hello haut de hello, cliquez sur **TOPdesk \> nouveau \> les fichiers de prise en charge \> opérateur**.
   
    ![Operator (Opérateur)](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator (Opérateur)")

3. Sur hello **nouvel opérateur** boîte de dialogue, effectuer hello comme suit :
   
    ![New Operator (Nouvel opérateur)](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator (Nouvel opérateur)")
   
    a. Cliquez sur Général hello.
   
    b. Bonjour **Surname** zone de texte Hello **général** section, le type hello nom d’un compte Azure Active Directory valide que vous souhaitez tooprovision.
   
    c. Sélectionnez un **Site** compte hello Bonjour **emplacement** section.
   
    d. Bonjour **nom de connexion** zone de texte Hello **TOPdesk Login** , tapez un nom de connexion pour votre utilisateur.
   
    e. Cliquez sur **Enregistrer**.

> [!NOTE]
> Vous pouvez utiliser n’importe quel autre TOPdesk - compte d’utilisateur sécurisé de création ou API fournies par TOPdesk - Secure tooprovision des comptes d’utilisateur AAD.
> 
> 

## <a name="assigning-users"></a>Affectation d’utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a>tooassign utilisateurs tooTOPdesk - Secure, procédez de hello comme suit :
1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello ** TOPdesk - Secure ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
    ![Affecter des utilisateurs](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Affecter des utilisateurs")

3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
    ![Oui](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

