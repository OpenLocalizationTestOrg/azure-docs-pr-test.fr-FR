---
title: "Didacticiel : Intégration d’Azure Active Directory à Benefitsolver | Microsoft Docs"
description: "Découvrez comment toouse Benefitsolver avec Azure Active Directory tooenable single sign-on, l’approvisionnement automatisé et bien plus encore !"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Didacticiel : Intégration d’Azure Active Directory à Benefitsolver
objectif Hello de ce didacticiel est l’intégration hello tooshow d’Azure et Benefitsolver.  

scénario de Hello décrite dans ce didacticiel part du principe que vous avez déjà hello éléments suivants :

* Un abonnement Azure valide
* Un abonnement Benefitsolver pour lequel l’authentification unique est activée

À l’issue de ce didacticiel, hello Azure AD utilisateurs tooBenefitsolver sera toosingle en mesure de l’authentification sur application hello utilisant hello [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

scénario Hello décrite dans ce didacticiel se compose de hello suivant des blocs de construction :

1. Activation de l’intégration d’application hello pour Benefitsolver
2. Configuration de l’authentification unique (SSO)
3. Configuration de l'approvisionnement des utilisateurs
4. Affectation d’utilisateurs

![Scénario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scénario")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Activation de l’intégration d’application hello pour Benefitsolver
objectif Hello de cette section est toooutline comment intégration d’application hello tooenable pour Benefitsolver.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>intégration d’application hello tooenable pour Benefitsolver, effectuez hello comme suit :
1. Bonjour portail Azure classic, dans le volet de navigation gauche hello, cliquez sur **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. À partir de hello **répertoire** liste, répertoire sélectionnez hello pour lequel vous souhaitez tooenable intégration d’annuaire.
3. vue d’applications de hello tooopen, dans la vue active de hello, cliquez sur **Applications** dans le menu du haut hello.
   
   ![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")
4. Cliquez sur **ajouter** bas hello de page de hello.
   
   ![Ajouter une application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Ajouter une application")
5. Sur hello **comment vous souhaitez toodo** boîte de dialogue, cliquez sur **ajouter une application à partir de la galerie de hello**.
   
   ![Ajouter une application à partir de la galerie](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Ajouter une application à partir de la galerie")
6. Bonjour **zone de recherche**, type **Benefitsolver**.
   
   ![Galerie d’applications](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galerie d’applications")
7. Dans le volet de résultats hello, sélectionnez **Benefitsolver**, puis cliquez sur **Complete** application hello de tooadd.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Configurer l’authentification unique

objectif Hello de cette section est toooutline comment tooenable utilisateurs tooauthenticate tooBenefitsolver avec leur compte dans Azure AD en utilisant la fédération basée sur le protocole SAML de hello.  

Votre application Benefitsolver attend les assertions SAML hello dans un format spécifique, ce qui vous oblige à tooyour de mappages d’attributs personnalisés tooadd **attributs du jeton saml** configuration. 

Hello suivant capture d’écran montre un exemple de cela.

![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributs")

**tooconfigure sur l’authentification unique, effectuer hello comme suit :**

1. Bonjour portail Azure classic sur hello **Benefitsolver** page d’intégration d’application, cliquez sur **configurer l’authentification unique sur** tooopen hello **configurer Single Sign On** boîte de dialogue.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurer l’authentification unique")
2. Sur hello **Comment souhaitez-vous toosign utilisateurs sur tooBenefitsolver** page, sélectionnez **Microsoft Azure AD Single Sign-On**, puis cliquez sur **suivant**.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurer l’authentification unique")
3. Sur hello **configurer les paramètres de l’application** page, effectuer hello comme suit :
   
   ![Configurer les paramètres d’application](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurer les paramètres d’application")
   
   1. Bonjour **URL de connexion** zone de texte, type **http://azure.benefitsolver.com**.
   2. Bonjour **URL de réponse** zone de texte, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Cliquez sur **Suivant**.
4. Sur hello **configurer l’authentification unique sur Benefitsolver** page, toodownload vos métadonnées, cliquez sur **télécharger des métadonnées**, puis enregistrez le fichier de métadonnées hello localement sur votre ordinateur.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurer l’authentification unique")
5. Envoyer l’équipe de support technique du fichier tooyour Benefitsolver hello téléchargé métadonnées.
   
   >[!NOTE]
   >Votre équipe de support Benefitsolver a configuration de SSO réelle toodo hello. Vous recevrez une notification dès que l’authentification unique aura été activée pour votre abonnement.
   >

6. Sur le portail Azure classic de hello, sélectionnez la confirmation de la configuration de l’authentification unique hello, puis cliquez sur **Complete** tooclose hello **configurer Single Sign On** boîte de dialogue.
   
   ![Configurer l’authentification unique](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurer l’authentification unique")
7. Dans le menu hello haut de hello, cliquez sur **attributs** tooopen hello **attributs du jeton SAML** boîte de dialogue.
   
   ![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributs")
8. mappages d’attributs tooadd hello requis, effectuez hello comme suit :
   
   ![Attributs](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributs")
   
   | Nom de l'attribut | Valeur de l’attribut |
   | --- | --- |
   | ClientID |Vous devez tooget de cette valeur à partir de votre équipe de support Benefitsolver. |
   | ClientKey |Vous devez tooget de cette valeur à partir de votre équipe de support Benefitsolver. |
   | LogoutURL |Vous devez tooget de cette valeur à partir de votre équipe de support Benefitsolver. |
   | EmployeeID |Vous devez tooget de cette valeur à partir de votre équipe de support Benefitsolver. |
   
   1. Pour chaque ligne de données dans la table hello ci-dessus, cliquez sur **ajouter un attribut utilisateur**.
   2. Bonjour **nom de l’attribut** zone de texte, nom d’attribut type hello indiqué pour cette ligne.
   3. Bonjour **valeur d’attribut** zone de texte, valeur de l’attribut select hello indiqué pour cette ligne.
   4. Cliquez sur **Terminé**.
9. Cliquez sur **Appliquer les modifications**.

## <a name="configure-user-provisioning"></a>Configurer l'approvisionnement de l'utilisateur
Dans l’ordre tooenable Azure AD les utilisateurs toolog dans Benefitsolver, ils doivent être configurés dans Benefitsolver.  

Dans les cas de hello de Benefitsolver, les données sur les employés sont dans votre application remplie via un fichier de recensement, à partir de votre système de ressources humaines (généralement nuit).  

>[!NOTE]
>Vous pouvez utiliser n’importe quel autre Benefitsolver utilisateur compte outil de création ou API fournie par Benefitsolver tooprovision des comptes d’utilisateur AAD. 
> 

## <a name="assigning-users"></a>Affectation d’utilisateurs
tootest votre configuration, vous devez toogrant hello Azure AD les utilisateurs à l’aide de votre tooit d’accès aux applications en leur attribuant des tooallow.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign utilisateurs tooBenefitsolver, effectuer hello comme suit :
1. Bonjour portail Azure classic, créez un compte de test.
2. Sur hello ** Benefitsolver ** page d’intégration d’application, cliquez sur **affecter des utilisateurs**.
   
   ![Affecter des utilisateurs](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Affecter des utilisateurs")
3. Sélectionnez votre utilisateur de test, cliquez sur **affecter**, puis cliquez sur **Oui** tooconfirm votre affectation.
   
   ![Oui](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Oui")

Si vous souhaitez tootest vos paramètres d’authentification unique, ouvrez hello panneau d’accès. Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).

