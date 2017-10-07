---
title: "Didacticiel : Intégration d’Azure Active Directory à Central Desktop | Microsoft Docs"
description: "Découvrez comment toouse Central Desktop avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a>Didacticiel : Intégration d’Azure Active Directory à Central Desktop
objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de Central Desktop. scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un abonnement Central Desktop pour lequel l’authentification unique est activée / locataire Central Desktop

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

* Activation de l’intégration d’application hello pour Central Desktop
* Configuration de l’authentification unique (SSO)
* Configuration de l'approvisionnement des utilisateurs
* Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scénario")

## <a name="enable-hello-application-integration-for-central-desktop"></a>Activer l’intégration d’application hello pour Central Desktop
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Central Desktop.

**intégration d’application hello tooenable pour Central Desktop, procédez hello comme suit :**

1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
   ![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")
4. Cliquez sur **ajouter** bas hello de page de hello.
   
   ![Ajouter une application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Ajouter une application")
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
   ![Ajouter une application à partir de la galerie](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Bonjour **zone de recherche**, type **Central Desktop**.
   
   ![Galerie d’applications](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Galerie d’applications")
7. Dans le volet de résultats hello, sélectionnez **Central Desktop**, puis cliquez sur **Complete** application hello de tooadd.
   
   ![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooCentral bureau avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.

Dans le cadre de cette procédure, vous êtes tooupload requis un client de bureau Central tooyour certificat codé en base 64.  
Si vous n’êtes pas familiarisé avec cette procédure, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o).

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello **Central Desktop** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello ** configurer Single Sign On ** boîte de dialogue.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configurer l’authentification unique")
2. Sur hello **Comment souhaitez-vous toosign les utilisateurs sur le bureau de tooCentral** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configurer l’authentification unique")
3. Sur hello **Configure App URL** page, effectuer hello comme suit, puis cliquez sur **suivant**: 
   
   1. Bonjour **Central Desktop URL de connexion** zone de texte, tapez l’URL de votre client Central Desktop hello (par exemple : *http://contoso.centraldesktop.com*).
   2. Dans la zone de texte URL de réponse Central Desktop hello, tapez votre URL AssertionConsumerService de Central Desktop (par exemple : https://contoso.centraldesktop.com/saml2-assertion.php).
   
   >[!NOTE]
   >Vous pouvez obtenir la valeur de hello à partir des métadonnées de hello central desktop (par exemple : *http://contoso.centraldesktop.com*).
   >  
   
   ![Configurer l’URL de l’application](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configurer l’URL de l’application")
4. Sur hello **configurer l’authentification unique sur Central Desktop** page, toodownload votre certificat, cliquez sur **télécharger le certificat**, puis enregistrez le fichier de certificat hello sur votre ordinateur.
   
  ![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configurer l’authentification unique")
5. Connectez-vous à tooyour **Central Desktop** client.
6. Accédez trop**paramètres**, cliquez sur **avancé**, puis cliquez sur **Single Sign On**.
   
  ![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")
7. Sur hello **Single Sign On Settings** page, effectuer hello comme suit :
   
  ![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")
   
  1. Sélectionnez **Activer l’authentification unique SAMLv2**.
  2. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Central Desktop** page, hello de copie **URL de l’émetteur** valeur, puis collez-le dans hello **URL SSO** zone de texte.
  3. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Central Desktop** page, hello de copie **URL de connexion distante** valeur, puis collez-le dans hello **URL de connexion SSO**zone de texte.
  4. Bonjour portail Azure classic sur hello **configurer l’authentification unique sur Central Desktop** page, hello de copie **URL de Service de déconnexion unique** valeur, puis collez-le dans hello **URL de déconnexion de SSO** zone de texte.
8. Bonjour **méthode de vérification de Signature de Message** section, effectuer hello comme suit :
   
   ![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")
   
  1. Sélectionnez **Certificate**.
  2. À partir de hello **certificat SSO** liste, sélectionnez **RSH SHA256**.
  3. Créez un fichier texte à partir du certificat hello téléchargé, hello copie le contenu des fichiers de texte hello et le coller ensuite dans hello **certificat SSO** champ.  
     >[!TIP]
     >Pour plus d’informations, consultez [comment tooconvert un fichier binaire du certificat dans un fichier texte](http://youtu.be/PlgrzUZ-Y1o)
      >  
   4. Sélectionnez **afficher une page de connexion de lien tooyour SAMLv2**.
9. Cliquez sur **Update**.
10. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
    
    ![Configurer l’authentification unique](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configurer l’authentification unique")
    
## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur

Pour AAD utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service toohello application Central Desktop. Cette section décrit comment les comptes utilisateur d’AAD toocreate dans Central Desktop.

**tooprovision tooCentral de comptes utilisateur Desktop :**
1. Ouvrez une session dans tooyour client Central Desktop.
2. Accédez trop**personnes \> membres internes**.
3. Cliquez sur **Ajouter des membres internes**.
   
  ![Personnes](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Personnes")
4. Bonjour **adresse de messagerie des nouveaux membres** zone de texte, tapez un compte AAD, vous souhaitez tooprovision, puis cliquez sur **suivant**.
   
  ![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")
5. Cliquez sur **Add Internal member(s)**.
   
  ![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")
   
   >[!NOTE]
   >les utilisateurs de Hello que vous avez ajouté recevront un message électronique contenant un lien de confirmation dont ils ont besoin de compte de tooclick tooactivate hello.
   > 

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Central Desktop utilisateur compte outil de création ou API fournie par Central Desktop tooprovision des comptes d’utilisateur AAD
>  

## <a name="assign-users"></a>Affecter des utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

**tooassign utilisateurs tooCentral bureau, effectuez hello comme suit :**

1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello **Central Desktop** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
   ![Oui](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

