---
title: "aaaPublish Bureau à distance avec le Proxy d’application Azure AD | Documents Microsoft"
description: "Traite des principes de base hello des connecteurs de Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>Publier le Bureau à distance avec le proxy d’application Azure AD

Cet article décrit comment toodeploy Services Bureau à distance (RDS) avec le Proxy d’Application afin que les utilisateurs distants peuvent toujours être productifs.

Hello destiné à cet article s’adresse :
- Clients actuels Proxy d’Application Azure AD qui veulent des utilisateurs finaux de plusieurs applications tootheir toooffer en publiant des applications locales via les Services Bureau à distance.
- Clients de Services Bureau à distance en cours qui souhaitent surface d’attaque hello tooreduce de leur déploiement à l’aide du Proxy d’Application Azure AD. Ce scénario fournit un ensemble limité de vérification en deux étapes et tooRDS des contrôles d’accès conditionnel.

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>Manière dont le Proxy d’Application s’intègre dans le déploiement des services Bureau à distance standard hello

Un déploiement RDS standard inclut divers services du rôle Bureau à distance s’exécutant sur Windows Server. Examinez hello [architecture des Services Bureau à distance](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), il existe plusieurs options de déploiement. Hello différence la plus évidente entre hello [déploiement des services Bureau à distance avec le Proxy d’Application Azure AD](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (illustrée dans hello suivant schéma) et hello autres options de déploiement de ce scénario de Proxy d’Application hello a permanent sortant connexion à partir du serveur hello en cours d’exécution du service Connecteur hello. Les autres déploiements comportent des connexions entrantes ouvertes via un équilibreur de charge.

![Application réside de Proxy entre hello RDS VM et hello internet public](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

Dans un déploiement services Bureau à distance, rôle de Web des services Bureau à distance hello et le rôle de passerelle Bureau à distance de hello exécutent sur les ordinateurs sur Internet. Ces points de terminaison exposés pour hello suivant raisons :
- Web du Bureau à distance fournit les utilisateur hello un toosign de point de terminaison public dans et vue hello différentes applications sur site et ils peuvent accéder aux ordinateurs de bureau. Lors de la sélection d’une ressource, une connexion RDP est créée à l’aide d’application native hello sur hello du système d’exploitation.
- Passerelle Bureau à distance est fourni dans l’image de hello une fois qu’un utilisateur lance la connexion RDP de hello. Hello passerelle Bureau à distance gère le trafic RDP de hello chiffré franchissant hello Internet et le traduit toohello serveur local qui hello utilisateur se connecte. Dans ce scénario, hello du trafic hello que reçoit de passerelle Bureau à distance provient hello Proxy d’Application Azure AD.

>[!TIP]
>Si vous n’avez pas déployé les services Bureau à distance avant ou que vous souhaitez plus d’informations avant de commencer, découvrez comment trop[déployer en toute transparence des services Bureau à distance avec le Gestionnaire de ressources Azure et Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).

## <a name="requirements"></a>Configuration requise

- Les deux hello Web du Bureau à distance et passerelle Bureau à distance points de terminaison doivent se trouver sur hello même ordinateur et avec une racine commune. Web du Bureau à distance et passerelle Bureau à distance seront publié en tant qu’une seule application afin de disposer d’une expérience d’authentification unique entre les applications de hello deux.

- Vous devez déjà avoir [déployé RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure) et [activé le proxy d’application](active-directory-application-proxy-enable.md).

- Ce scénario part du principe que vos utilisateurs finaux passent par Internet Explorer sur les ordinateurs de bureau Windows 7 ou Windows 10 qui se connectent via la page Web du Bureau à distance de hello. Si vous avez besoin toosupport autres systèmes d’exploitation, consultez [prise en charge pour d’autres configurations de client](#support-for-other-client-configurations).

  >[!NOTE]
  >La mise à jour Windows 10 Creators Update n’est pas prise en charge actuellement.

- Dans Internet Explorer, activer un module complémentaire de hello ActiveX des services Bureau à distance.

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>Déployer le scénario de services Bureau à distance et de Proxy d’Application mixte hello

Après avoir configuré les services Bureau à distance et de Proxy d’Application Azure AD pour votre environnement, suivez les deux solutions hello étapes toocombine hello. Ces étapes vous guide lors hello deux web orientées services Bureau à distance points de terminaison (Web du Bureau à distance et passerelle Bureau à distance) de publication en tant qu’applications et ensuite diriger le trafic sur votre toogo des services Bureau à distance via le Proxy d’Application.

### <a name="publish-hello-rd-host-endpoint"></a>Publier le point de terminaison hôte hello Bureau à distance

1. [Publier une nouvelle application de Proxy d’Application](application-proxy-publish-azure-portal.md) avec hello valeurs suivantes :
   - URL interne : https://\<rdhost\>.com /, où \<rdhost\> est racine commun hello partageant Web du Bureau à distance et passerelle Bureau à distance.
   - URL externe : Ce champ est automatiquement rempli selon le nom hello de l’application hello, mais vous pouvez la modifier. Vos utilisateurs passera toothis URL lorsqu’ils accèdent à RDS.
   - Méthode de pré-authentification : Azure Active Directory
   - Traduire des URL dans les en-têtes : Non
2. Affecter des utilisateurs toohello publié l’application de bureau à distance. Assurez-vous que tous ont accès tooRDS, trop.
3. Laissez hello unique méthode d’authentification pour l’application hello en tant que **AD Azure l’authentification unique sur désactivé**. Les utilisateurs sont invités à tooauthenticate une fois tooAzure AD et une fois tooRD Web, mais ils présentent une seule session tooRD passerelle.
4. Accédez trop**Azure Active Directory** > **inscriptions d’application** > *votre application* > **deparamètres**.
5. Sélectionnez **propriétés** et mise à jour hello **URL de la page d’accueil** champ toopoint tooyour Bureau à distance point de terminaison Web (telle que https://\<rdhost\>.com/RDWeb).

### <a name="direct-rds-traffic-tooapplication-proxy"></a>Diriger le trafic de services Bureau à distance tooApplication Proxy

Connecter le déploiement des services Bureau à distance toohello en tant qu’administrateur et modifier le nom du serveur de passerelle Bureau à distance pour le déploiement de hello hello. Cela garantit que les connexions passent par hello Proxy d’Application Azure AD.

1. Connecter le serveur de services Bureau à distance de toohello rôle Broker pour les connexions Bureau à distance de hello en cours d’exécution.
2. Lancez le **Gestionnaire de serveur**.
3. Sélectionnez **Services Bureau à distance** à partir du volet gauche de hello hello.
4. Sélectionnez **Vue d’ensemble**.
5. Dans la section vue d’ensemble du déploiement de hello, sélectionnez le menu déroulant de hello et choisissez **modifier les propriétés de déploiement**.
6. Dans l’onglet de passerelle Bureau à distance hello, modifiez hello **nom du serveur** champ toohello URL externe que vous définissez pour le point de terminaison de hôte hello Bureau à distance dans le Proxy d’Application.
7. Hello de modification **méthode d’ouverture de session** champ trop**l’authentification du mot de passe**.

  ![Écran Propriétés de déploiement sur RDS](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. Pour chaque collection, exécutez hello commande suivante. Remplacez *\<yourcollectionname\>* et *\<proxyfrontendurl\>* par vos propres informations. Cette commande active l’authentification unique entre Site Web Bureau à distance et Passerelle Bureau à distance, et optimise les performances :

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **Par exemple :**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. modification de hello tooverify de propriétés RDP personnalisées de hello, ainsi que contenu du fichier vue hello RDP qui vont être téléchargé à partir de RDWeb pour cette collection, exécutez hello de commande suivante :
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

Maintenant que vous avez configuré le Bureau à distance, le Proxy d’Application Azure AD est prise en charge en tant que composant du côté internet hello de RDS. Vous pouvez supprimer hello d’autres points de terminaison publics sur internet sur vos ordinateurs de bureau à distance Web et de passerelle Bureau à distance.

## <a name="test-hello-scenario"></a>Scénario de test de hello

Tester le scénario hello avec Internet Explorer sur un ordinateur Windows 7 ou 10.

1. Atteindre l’URL externe de toohello vous configurez, ou de localiser votre application hello [MyApps panneau](https://myapps.microsoft.com).
2. Vous êtes invité tooauthenticate tooAzure Active Directory. Utilisez un compte que vous avez affecté toohello application.
3. Vous êtes invité tooauthenticate tooRD Web.
4. Une fois l’authentification des services Bureau à distance est terminée, vous pouvez sélectionner hello application bureautique ou vous le souhaitez et commencer à travailler.

## <a name="support-for-other-client-configurations"></a>Prise en charge pour d’autres configurations client

configuration de Hello décrite dans cet article s’applique aux utilisateurs sur Windows 7 ou 10, Internet Explorer plus un module complémentaire de hello ActiveX des services Bureau à distance. Toutefois, le cas échéant, vous pouvez prendre en charge d’autres systèmes d’exploitation et navigateurs. différence de Hello réside dans la méthode d’authentification hello que vous utilisez.

| Méthode d’authentification | Configuration client prise en charge |
| --------------------- | ------------------------------ |
| Pré-authentification    | Windows 7/10 avec Internet Explorer + module complémentaire ActiveX Service de données distant |
| PassThrough | Les systèmes d’exploitation qui prend en charge les applications de bureau à distance Microsoft hello |

flux de pré-authentification Hello offre plusieurs avantages de sécurité de flux de relais hello. Avec la pré-authentification, vous pouvez exploiter les fonctionnalités d’authentification Azure AD, telles que l’authentification unique, l’accès conditionnel et la vérification en deux étapes pour vos ressources locales. Vous garantissez également que seul le trafic authentifié atteint votre réseau.

toouse l’authentification, il sont simplement deux modifications toohello étapes répertoriées dans cet article :
1. Dans [publier le point de terminaison hôte hello Bureau à distance](#publish-the-rd-host-endpoint) l’étape 1, définir la méthode de pré-authentification hello trop**Passthrough**.
2. Dans [services Bureau à distance directe du trafic tooApplication Proxy](#direct-rds-traffic-to-application-proxy), ignorez l’étape 8 entièrement.

## <a name="next-steps"></a>Étapes suivantes

[Activer tooSharePoint l’accès à distance avec le Proxy d’Application Azure AD](application-proxy-enable-remote-access-sharepoint.md)  
[Considérations de sécurité pour l’accès aux applications à distance à l’aide du proxy d’application Azure AD](application-proxy-security-considerations.md)
