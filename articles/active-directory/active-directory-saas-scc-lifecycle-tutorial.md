---
title: "Didacticiel : Intégration d’Azure Active Directory avec SCC LifeCycle | Microsoft Docs"
description: "Découvrez comment toouse SCC LifeCycle avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a>Didacticiel : Intégration d’Azure AD avec SCC LifeCycle
objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et de SCC LifeCycle.  

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un abonnement SCC LifeCycle pour lequel l’authentification unique est activée

À l’issue de ce didacticiel, hello Azure AD utilisateurs tooSCC cycle de vie sera toosingle en mesure de connexion dans l’application hello sur votre site d’entreprise SCC LifeCycle (service initiée par le fournisseur de session), ou à l’aide de hello [Introduction Volet d’accès de toohello](active-directory-saas-access-panel-introduction.md).

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

1. Activation de l’intégration d’application hello pour SCC LifeCycle
2. Configuration de l’authentification unique (SSO)
3. Configuration de l'approvisionnement des utilisateurs
4. Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scénario")

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a>Activer l’intégration d’application hello pour SCC LifeCycle
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour SCC LifeCycle.

**intégration d’application hello tooenable pour SCC LifeCycle, procédez hello comme suit :**

1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
    ![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")
4. Cliquez sur **ajouter** bas hello de page de hello.
   
    ![Ajouter une application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Ajouter une application")
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
    ![Ajouter une application à partir de la galerie](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Bonjour **zone de recherche**, type **SCC LifeCycle**.
   
    ![Galerie d’applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Galerie d’applications")
7. Dans le volet de résultats hello, sélectionnez **SCC LifeCycle**, puis cliquez sur **Complete** application hello de tooadd.
   
    ![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooSCC du cycle de vie avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello **SCC LifeCycle** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello ** configurer Single Sign On ** boîte de dialogue.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configurer l’authentification unique")
2. Sur hello **Comment souhaitez-vous toosign les utilisateurs sur le cycle de vie de tooSCC** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configurer l’authentification unique")
3. Sur hello **Configure App URL** page hello **URL de connexion** zone de texte, tapez l’URL hello utilisé par votre toosign utilisateurs sur tooyour application SCC LifeCycle à l’aide de hello suivant le modèle «*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*», puis cliquez sur **suivant**.
   
    ![Configurer l’URL de l’application](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configurer l’URL de l’application")
4. Sur hello **configurer l’authentification unique sur SCC LifeCycle** , cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier de métadonnées localement sur votre ordinateur.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configurer l’authentification unique")
5. Transférer ce tooSCC de fichier de métadonnées équipe de Support du cycle de vie.
   
   >[!NOTE]
   >L’authentification unique a toobe activé par l’équipe de support technique SCC LifeCycle de hello.
   > 
   > 

6. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
   
    ![Configurer l’authentification unique](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configurer l’authentification unique")
   
## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur

Dans l’ordre tooenable Azure AD les utilisateurs toolog à SCC LifeCycle, ils doivent être configurés à SCC LifeCycle. Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooSCC du cycle de vie.

Lorsqu’un toolog tentatives utilisateur affecté à SCC LifeCycle, un compte SCC LifeCycle est créé automatiquement si nécessaire.

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre SCC LifeCycle utilisateur compte outil de création ou API fournie par SCC LifeCycle tooprovision des comptes d’utilisateur AAD.
> 
> 

## <a name="assign-users"></a>Affecter des utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

**les utilisateurs de tooassign tooSCC du cycle de vie, effectuer hello comme suit :**

1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello ** SCC LifeCycle ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
    ![Affecter des utilisateurs](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
    ![Oui](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

