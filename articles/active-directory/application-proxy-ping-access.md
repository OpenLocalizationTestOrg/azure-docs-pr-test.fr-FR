---
title: "l’authentification basée sur les aaaHeader avec PingAccess pour le Proxy d’Application Azure AD | Documents Microsoft"
description: "Publier des applications avec authentification toosupport basée sur l’en-tête PingAccess et Proxy d’application."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 38fe3e7a41a71f4ae6c75f014e44c722f773bd22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="header-based-authentication-for-single-sign-on-with-application-proxy-and-pingaccess"></a>Authentification basée sur l’en-tête pour une authentification unique avec le proxy d’application et PingAccess

Proxy d’Application Active Directory Azure et PingAccess s’associent ensemble tooprovide les clients Azure Active Directory avec accès tooeven d’autres applications. PingAccess développe hello [offres de Proxy d’Application existantes](active-directory-application-proxy-get-started.md) tooapplications d’accès de l’authentification unique tooinclude qui utilisent des en-têtes pour l’authentification.

## <a name="what-is-pingaccess-for-azure-ad"></a>Présentation de PingAccess pour Azure AD

PingAccess pour Azure Active Directory est une offre de PingAccess qui permet l’accès aux utilisateurs toogive et uniques tooapplications authentification qui utilisent des en-têtes pour l’authentification. Le Proxy d’application traite ces applications comme tout autre, à l’aide de l’accès tooauthenticate Azure AD, puis en passant le trafic via le service du connecteur hello. PingAccess se situe devant les applications hello et traduit un en-tête de jeton d’accès hello d’Azure AD afin que l’application hello reçoit l’authentification hello au format hello que peut lire.

Vos utilisateurs ne remarquent différemment lorsqu’ils connectent toouse vos applications d’entreprise. Ils pourront toujours travailler depuis n’importe où et sur n’importe quel appareil. 

Étant donné que les connecteurs de Proxy d’Application hello diriger le trafic à distance des applications de tooall, quelle que soit leur type d’authentification, ils continuerons solde de tooload automatiquement, ainsi que.

## <a name="how-do-i-get-access"></a>Comment puis-je avoir accès ?

Comme ce scénario est possible grâce à un partenariat entre Azure Active Directory et PingAccess, vous avez besoin de licences pour les deux services. Toutefois, les abonnements Azure Active Directory Premium incluent une licence PingAccess de base qui couvre les applications de too20. Si vous devez toopublish plus de 20 applications basé sur l’en-tête, vous pouvez acheter une licence supplémentaire à partir de PingAccess. 

Pour plus d’informations, consultez la page [Éditions d’Azure Active Directory](active-directory-editions.md).

## <a name="publish-your-application-in-azure"></a>Publier votre application dans Azure

Cet article est destiné aux personnes qui publient une application avec ce scénario pour hello première fois. Il décrit comment tooget démarrer avec l’Application et PingAccess, en outre toohello procédure de publication. Si vous avez déjà configuré les deux services mais que vous souhaitez un rappel sur hello étapes de publication, vous pouvez ignorer l’installation du connecteur hello et déplacer sur trop[ajouter votre tooAzure application AD avec le Proxy d’Application](#add-your-app-to-Azure-AD-with-Application-Proxy).

>[!NOTE]
>Étant donné que ce scénario est un partenariat entre Azure AD et PingAccess, certaines des instructions de hello existent sur hello site Ping identité.

### <a name="install-an-application-proxy-connector"></a>Installer un connecteur Application Proxy

Si vous avez activé le Proxy d’Application et un connecteur êtes installé, vous pouvez ignorer cette section et passer trop[ajouter votre tooAzure application AD avec le Proxy d’Application](#add-your-app-to-azure-ad-with-application-proxy).

connecteur de Proxy d’Application Hello est un serveur Windows service qui dirige le trafic à partir de votre tooyour employés distants hello les applications publiées. Pour plus d’instructions d’installation, consultez [activer le Proxy d’Application Bonjour Azure portal](active-directory-application-proxy-enable.md).

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’un administrateur global.
2. Sélectionnez **Azure Active Directory** > **Application Proxy**.
3. Sélectionnez **télécharger Connector** téléchargement du connecteur Proxy d’Application toostart hello. Suivez les instructions d’installation hello.

   ![Activer le Proxy d’Application et de télécharger le connecteur de hello](./media/application-proxy-ping-access/install-connector.png)

4. Téléchargement de hello connector doit activer automatiquement le Proxy d’Application pour votre annuaire, mais si pas, vous pouvez sélectionner **activer le Proxy d’Application**.


### <a name="add-your-app-tooazure-ad-with-application-proxy"></a>Ajouter votre tooAzure application AD avec le Proxy d’Application

Il existe deux actions que vous avez besoin de tootake Bonjour portail Azure. Tout d’abord, vous devez toopublish votre application avec le Proxy d’Application. Ensuite, vous devez toocollect des informations sur l’application hello que vous pouvez utiliser au cours des étapes de PingAccess hello.

Suivez ces étapes toopublish votre application. Pour obtenir plus de détails sur les étapes 1 à 8, consultez [Publier des applications avec le Proxy d’application Azure AD](application-proxy-publish-azure-portal.md).

1. Si vous n’avez pas dans la dernière section de hello, connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’un administrateur global.
2. Sélectionnez **Azure Active Directory (Azure Active Directory)** > **Enterprise applications (Applications d’entreprise)**.
3. Sélectionnez **ajouter** haut hello du Panneau de hello.
4. Sélectionnez **On-premises application (Application locale)**.
5. Complétez les champs hello requis avec des informations sur votre nouvelle application. Utilisez hello suivant pour les paramètres de hello :
   - **URL interne**: fournissez URL hello qui compte plusieurs phases d’inscription d’application toohello dans la page lorsque vous êtes sur le réseau d’entreprise de hello. Pour ce scénario connecteur de hello doit tootreat hello PingAccess proxy en tant que page de serveur frontal hello de l’application hello. Utilisez le format suivant : `https://<host name of your PA server>:<port>`. port de Hello est 3000 par défaut, mais vous pouvez le configurer dans PingAccess.
   - **Méthode de pré-authentification** : Azure Active Directory
   - **Traduire des URL dans les en-têtes** : Non

   >[!NOTE]
   >S’il s’agit de votre première application, utilisez le port 3000 toostart et reviendrons tooupdate ce paramètre si vous modifiez votre configuration PingAccess. S’il s’agit de votre application de la deuxième ou version ultérieure, cela devez toomatch hello écouteur que vous avez configuré dans PingAccess. Découvrez plus en détail les [écouteurs dans PingAccess](https://documentation.pingidentity.com/pingaccess/pa31/index.shtml#Listeners.html).

6. Sélectionnez **ajouter** bas hello du Panneau de hello. Votre application est ajoutée, et menu de démarrage rapide de hello s’ouvre.
7. Dans le menu de démarrage rapide de hello, sélectionnez **affecter un utilisateur pour le test**et ajoutez au moins un utilisateur toohello application. Assurez-vous que ce compte de test a accès toohello local application.
8. Sélectionnez **affecter** affectation d’utilisateurs test toosave hello.
9. Dans le panneau de gestion d’application de hello, sélectionnez **l’authentification unique**.
10. Choisissez **basée sur l’en-tête de l’authentification** à partir du menu déroulant de hello. Sélectionnez **Enregistrer**.

   >[!TIP]
   >S’il s’agit de la première fois à l’aide basée sur l’en-tête de l’authentification unique sur, vous devez tooinstall PingAccess. toomake que votre abonnement Azure est automatiquement associé à votre installation PingAccess, utiliser la liaison sur cette toodownload page d’ouverture de session unique PingAccess hello. Vous pouvez ouvrir le site de téléchargement hello maintenant ou ultérieurement toothis page. 

   ![Sélectionner l’authentification basée sur un en-tête](./media/application-proxy-ping-access/sso-header.PNG)

11. Fermez le panneau des applications Enterprise hello ou faites défiler le menu de Azure Active Directory hello moyen toohello tooreturn gauche toohello tous les.
12. Sélectionnez **Inscriptions d’applications**.

   ![Sélectionner Inscriptions d’applications](./media/application-proxy-ping-access/app-registrations.png)

13. Application hello sélectionnez vous venez d’ajouter, puis **URL de réponse**.

   ![Sélectionner URL de réponse](./media/application-proxy-ping-access/reply-urls.png)

14. Vérifiez toosee si les URL externe hello cette application attribué tooyour vous à l’étape 5 est dans la liste des URL de réponse hello. Si tel n’est pas le cas, ajoutez-la maintenant.
15. Dans le panneau de paramètres d’application de hello, sélectionnez **autorisations requises**.

  ![Sélectionner Autorisations requises](./media/application-proxy-ping-access/required-permissions.png)

16. Sélectionnez **Ajouter**. Pour les API de hello, choisissez **Windows Azure Active Directory**, puis **sélectionnez**. Pour les autorisations de hello, choisissez **en lecture et écriture de toutes les applications** et **se connecter et lire le profil utilisateur**, puis **sélectionnez** et **fait**.  

  ![Sélectionner les autorisations](./media/application-proxy-ping-access/select-permissions.png)

### <a name="collect-information-for-hello-pingaccess-steps"></a>Collecter les informations relatives aux étapes hello PingAccess

1. Dans le panneau des paramètres de l’application, sélectionnez **Propriétés**. 

  ![Sélectionner Propriétés](./media/application-proxy-ping-access/properties.png)

2. Enregistrer hello **Id d’Application** valeur. Cela est utilisé pour l’ID de client hello lorsque vous configurez PingAccess.
3. Dans le panneau de paramètres d’application de hello, sélectionnez **clés**.

  ![Sélectionner Clés](./media/application-proxy-ping-access/Keys.png)

4. Créer une clé en entrant une description de la clé et en choisissant une date d’expiration à partir du menu déroulant de hello.
5. Sélectionnez **Enregistrer**. Un GUID apparaît dans hello **valeur** champ.

  Enregistrer cette valeur à présent, comme vous ne serez pas en mesure de toosee à nouveau après que vous fermez cette fenêtre.

  ![Créer une clé](./media/application-proxy-ping-access/create-keys.png)

6. Fermez le panneau des enregistrements de l’application hello ou faites défiler le menu de Azure Active Directory hello moyen toohello tooreturn gauche toohello tous les.
7. Sélectionner **Propriétés**.
8. Enregistrer hello **ID de répertoire** GUID.

### <a name="optional---update-graphapi-toosend-custom-fields"></a>Facultatif : toosend GraphAPI de mise à jour des champs personnalisés

Pour obtenir la liste des jetons de sécurité qu’envoie Azure AD pour l’authentification, consultez [Référence sur les jetons Azure AD](./develop/active-directory-token-and-claims.md). Si vous avez besoin d’une revendication personnalisée qui envoie les autres jetons, utilisez le champ de l’application hello GraphAPI tooset *acceptMappedClaims* trop**True**. Vous pouvez utiliser l’Explorateur d’Azure AD Graph ou dans MS Graph toomake cette configuration. 

Cet exemple utilise l’Explorateur Graph :

```
PATCH https://graph.windows.net/myorganization/applications/<object_id_GUID_of_your_application> 

{
  "acceptMappedClaims":true
}
```

## <a name="download-pingaccess-and-configure-your-app"></a>Télécharger PingAccess et configurer votre application

Maintenant que vous avez terminé toutes les étapes de configuration d’Azure Active Directory hello, vous pouvez déplacer sur tooconfiguring PingAccess. 

Hello des instructions détaillées pour hello PingAccess inclus dans ce scénario continuer Bonjour documentation de l’identité de la commande Ping, [PingAccess de configurer pour Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html).

Ces étapes vous guident tout au long des processus hello d’obtention d’un compte PingAccess si vous n’en avez pas encore, l’installation hello PingAccess Server et la création d’une connexion du fournisseur d’Azure AD OIDC avec hello ID de répertoire que vous avez copié à partir de hello portail Azure. Ensuite, vous utilisez les valeurs de clé et les ID d’Application hello toocreate une Session Web sur PingAccess. Enfin, vous pouvez configurer le mappage d’identité et créer un hôte virtuel, le site et l’application.

### <a name="test-your-app"></a>Test de l'application

Une fois toutes ces étapes effectuées, votre application doit être opérationnelle. tootest, ouvrez un navigateur et accédez toohello URL externe que vous avez créé lorsque vous avez publié l’application hello dans Azure. Compte de test hello connectez-vous à cette application toohello attribué vous.

## <a name="next-steps"></a>Étapes suivantes

- [Configurer PingAccess pour Azure AD](https://docs.pingidentity.com/bundle/paaad_m_ConfigurePAforMSAzureADSolution_paaad43/page/pa_c_PAAzureSolutionOverview.html)
- [Comment le proxy d’application Azure AD fournit-il une authentification unique ?](application-proxy-sso-overview.md)
- [Résoudre les problèmes du proxy d’application](active-directory-application-proxy-troubleshoot.md)
