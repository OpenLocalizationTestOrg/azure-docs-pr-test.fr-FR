---
title: "Didacticiel : Intégration d’Azure Active Directory à Coupa | Microsoft Docs"
description: "Apprenez à utiliser Coupa avec Azure Active Directory pour activer l’authentification unique, l’approvisionnement automatique et bien plus encore."
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
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a>Didacticiel : Intégration d’Azure Active Directory à Coupa
L’objectif de ce didacticiel est de montrer comment intégrer Azure et Coupa.  
Le scénario décrit dans ce didacticiel part du principe que vous disposez des éléments suivants :

* Un abonnement Azure valide
* Un abonnement Coupa pour lequel l’authentification unique (SSO) est activée

À l’issue de ce didacticiel, les utilisateurs d’Azure AD que vous avez affectés à Coupa pourront s’authentifier de manière unique dans l’application à l’aide de la [Présentation du volet d’accès](active-directory-saas-access-panel-introduction.md).

Le scénario décrit dans ce didacticiel se compose des blocs de construction suivants :

* Activation de l’intégration d’applications pour Coupa
* Configuration de l'authentification unique
* Configuration de l'approvisionnement des utilisateurs
* Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scénario")

## <a name="enable-the-application-integration-for-coupa"></a>Activer l’intégration d’applications pour Coupa
Cette section décrit l’activation de l’intégration d’applications pour Coupa.

**Pour activer l’intégration d’applications pour Coupa, suivez les étapes ci-dessous :**

1. Dans le volet de navigation gauche du portail Azure Classic, cliquez sur **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")
2. Dans la liste **Annuaire** , sélectionnez l'annuaire pour lequel vous voulez activer l'intégration d'annuaire.
3. Pour ouvrir la vue des applications, dans la vue d'annuaire, cliquez sur **Applications** dans le menu du haut.
   
   ![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")
4. Cliquez sur **Ajouter** en bas de la page.
   
   ![Ajouter une application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Ajouter une application")
5. Dans la boîte de dialogue **Que voulez-vous faire ?**, cliquez sur **Ajouter une application à partir de la galerie**.
   
   ![Ajouter une application à partir de la galerie](./media/active-directory-saas-coupa-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Dans la **zone de recherche**, tapez **Coupa**.
   
   ![Galerie d’applications](./media/active-directory-saas-coupa-tutorial/IC791898.png "Galerie d’applications")
7. Dans le volet des résultats, sélectionnez **Coupa**, puis cliquez sur **Terminer** pour ajouter l’application.
   
   ![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

Cette section explique comment permettre aux utilisateurs de s’authentifier sur Coupa avec leur compte Azure AD en utilisant la fédération basée sur le protocole SAML.  

La configuration de l’authentification unique pour Coupa vous oblige à récupérer une valeur d’empreinte numérique dans un certificat. Si cette procédure ne vous est pas familière, consultez [Comment récupérer la valeur d’empreinte numérique d’un certificat](http://youtu.be/YKQF266SAxI).

**Pour configurer l’authentification unique, procédez comme suit :**

1. Connectez-vous à votre site d’entreprise Coupa en tant qu’administrateur.
2. Accédez à **Setup \> Security controls**.
   
   ![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")
3. Pour télécharger le fichier de métadonnées Coupa sur votre ordinateur, cliquez sur **Download and import SP metadata**.
   
   ![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")
4. Dans une autre fenêtre du navigateur, connectez-vous au portail Azure Classic.
5. Sur la page d’intégration d’applications **Coupa**, cliquez sur **Configurer l’authentification unique** pour ouvrir la boîte de dialogue **Configurer l’authentification unique**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configurer l’authentification unique")
6. Dans la page **Comment voulez-vous que les utilisateurs se connectent à Coupa**, sélectionnez **Authentification unique avec Microsoft Azure AD**, puis cliquez sur **Suivant**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configurer l’authentification unique")
7. Dans la page **Configurer l’URL de l’application** , procédez comme suit :
   
   ![Configurer l’URL de l’application](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configurer l’URL de l’application")   
   1. Dans la zone de texte **URL de connexion**, tapez l’URL utilisée par vos utilisateurs pour se connecter à votre application Coupa (par exemple, « *http://company.Coupa.com* »).
   2. Ouvrez votre fichier de métadonnées Coupa téléchargé, puis copiez la valeur **AssertionConsumerService index/URL**.
   3. Dans la zone de texte **URL de réponse Coupa**, collez la valeur **AssertionConsumerService index/URL**.
   4. Cliquez sur **Suivant**.
8. Dans la page **Configurer l’authentification unique sur Coupa**, pour télécharger votre fichier de métadonnées, cliquez sur **Télécharger les métadonnées**, puis enregistrez le fichier en local sur votre ordinateur.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configurer l’authentification unique")
9. Sur le site d’entreprise Coupa, accédez à **Setup \> Security controls**.
   
   ![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")
10. Dans la section **Log in using Coupa credentials** , procédez comme suit :  

   ![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials") 
   1. Sélectionnez **Log in using SAML**.
   2. Cliquez sur **Browse** pour charger le fichier de métadonnées Azure Active Directory téléchargé.
   3. Cliquez sur **Save**.
11. Dans le portail Azure Classic, sélectionnez la confirmation de la configuration de l’authentification unique, puis cliquez sur **Terminer** pour fermer la boîte de dialogue **Configurer l’authentification unique**.
    
   ![Configurer l’authentification unique](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configurer l’authentification unique")
    
## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur

Pour se connecter à Coupa, les utilisateurs d’Azure AD doivent être approvisionnés dans Coupa.  

* Dans le cas de Coupa, l’approvisionnement est une tâche manuelle.

**Pour configurer l'approvisionnement des utilisateurs, procédez comme suit :**

1. Connectez-vous à votre site d’entreprise **Coupa** en tant qu’administrateur.
2. Dans le menu situé en haut, cliquez sur **Setup**, puis sur **Users**.
   
   ![Utilisateurs](./media/active-directory-saas-coupa-tutorial/IC791908.png "Utilisateurs")
3. Cliquez sur **Create**.
   
   ![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")
4. Dans la section **User Create** , procédez comme suit :
   
   ![Détails de l’utilisateur](./media/active-directory-saas-coupa-tutorial/IC791910.png "Détails de l’utilisateur")
   
   1. Tapez l’ID de connexion, le prénom, le nom, l’ID d’authentification unique et l’adresse électronique d’un compte Azure Active Directory valide que vous souhaitez approvisionner dans les zones de texte **Login**, **First name**, **Last Name**, **Single Sign-On ID** et **Email**.
   2. Cliquez sur **Create**.   
   >[!NOTE]
   >Le titulaire du compte Azure Active Directory reçoit un message électronique contenant un lien pour confirmer le compte et l’activer. 
   > 

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre outil ou API de création de compte d’utilisateur fourni par Coupa pour approvisionner des comptes d’utilisateurs AAD. 
> 

## <a name="assign-users"></a>Affecter des utilisateurs
Pour tester votre configuration, vous devez autoriser les utilisateurs d’Azure AD concernés à accéder à votre application.

**Pour affecter des utilisateurs à Coupa, suivez les étapes ci-dessous :**

1. Dans le portail Azure Classic, créez un compte de test.
2. Sur la ** Coupa ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-coupa-tutorial/IC791911.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **Affecter**, puis sur **Oui** pour confirmer votre affectation.
   
   ![Oui](./media/active-directory-saas-coupa-tutorial/IC767830.png "Oui")

Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès. Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).

