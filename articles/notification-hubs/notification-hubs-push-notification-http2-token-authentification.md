---
title: "aaaToken-(HTTP/2) l’authentification pour APNS dans Azure Notification Hubs | Documents Microsoft"
description: Cette rubrique explique comment tooleverage hello nouvelle authentification de jeton pour APNS
services: notification-hubs
documentationcenter: .net
author: kpiteira
manager: erikre
editor: 
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 05/17/2017
ms.author: kapiteir
ms.openlocfilehash: 3353d7f16033ce0b68edec9ee9aeb98f47faa1fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="token-based-http2-authentication-for-apns"></a>Authentification basée sur un jeton (HTTP/2) pour APNS
## <a name="overview"></a>Vue d'ensemble
Cet article décrit en détail comment toouse hello nouveau APNS HTTP/2 protocole avec le jeton d’authentification basée sur les.

Hello des avantages clés de l’utilisation du nouveau protocole de hello :
-   Génération de jeton est relativement vous soucier libre (comparés toocertificates)
-   Plus de date d’expiration : vous contrôlez vos jetons d’authentification et leur révocation
-   Charges utiles peuvent maintenant être des too4 Ko
- Les commentaires sont synchrones
-   Vous êtes sur le protocole de dernière d’Apple – certificats utilisent toujours le protocole binaire hello, qui est marquée pour l’abandon

L’utilisation de ce nouveau mécanisme peut être lancée en deux étapes et en quelques minutes :
1.  Obtenir les informations nécessaires hello à partir du portail de compte de développeur Apple hello
2.  Configurer votre concentrateur de notification avec les nouvelles informations de hello

Concentrateurs de notification est désormais tous ensemble toouse hello nouveau système d’authentification avec APNS. 

Notez que, si vous n’utilisez plus les informations d’identification de certificat pour APNS :
- Propriétés du jeton Hello remplacement votre certificat dans notre système.
- mais votre application continue tooreceive notifications en toute transparence.

## <a name="obtaining-authentication-information-from-apple"></a>Obtention d’informations d’authentification auprès d’Apple
l’authentification basée sur les jetons tooenable, vous devez hello propriétés suivantes à partir de votre compte de développeur Apple :
### <a name="key-identifier"></a>Identificateur de clé
identificateur de clé Hello peut être obtenu à partir de la page « Clés » de hello dans votre compte de développeur Apple

![](./media/notification-hubs-push-notification-http2-token-authentification/obtaining-auth-information-from-apple.png)

### <a name="application-identifier--application-name"></a>Identificateur de l’application et nom de l’application
nom de l’application Hello est disponible via la page de codes de l’application hello Bonjour compte de développeur. 
![](./media/notification-hubs-push-notification-http2-token-authentification/app-name.png)

identificateur de l’application Hello est disponible via la page de détails d’appartenance hello hello compte de développeur.
![](./media/notification-hubs-push-notification-http2-token-authentification/app-id.png)


### <a name="authentication-token"></a>Jeton d’authentification
jeton d’authentification Hello peut être téléchargé après avoir généré un jeton pour votre application. Pour plus d’informations sur comment toogenerate ce jeton, consultez trop[documentation pour développeurs d’Apple](http://help.apple.com/xcode/mac/current/#/dev11b059073?sub=dev1eb5dfe65).

## <a name="configuring-your-notification-hub-toouse-token-based-authentication"></a>Configuration de l’authentification basée sur les jetons de notification hub toouse
### <a name="configure-via-hello-azure-portal"></a>Configurer via hello portail Azure
jeton de tooenable en fonction de l’authentification dans le portail hello, ouvrez une session toohello portail Azure et accédez tooyour Hub de Notification > Services de Notification > Panneau de configuration APNS. 

Il existe une nouvelle propriété : *Mode d’authentification*. En sélectionnant le jeton vous permet de tooupdate votre concentrateur avec toutes les propriétés pertinentes hello du jeton.

![](./media/notification-hubs-push-notification-http2-token-authentification/azure-portal-apns-settings.png)

- Entrez les propriétés hello récupérés à partir de votre compte de développeur Apple, 
- choisissez votre mode d’application : Production ou Bac à sable (sandbox), 
- Cliquez sur Enregistrer tooupdate vos informations d’identification APNS. 

### <a name="configure-via-management-api-rest"></a>Configurer via l’API de gestion (REST)

Vous pouvez utiliser notre [API de gestion](https://msdn.microsoft.com/library/azure/dn495827.aspx) tooupdate votre notification hub toouse token d’authentification.
Selon qu’application hello que vous configurez est une application de Production ou de bac à sable (spécifiée dans votre compte de développeur Apple), utilisez un des points de terminaison hello correspondants :

- Point de terminaison sandbox : [https://api.development.push.apple.com:443/3/device](https://api.development.push.apple.com:443/3/device)
- Point de terminaison de production : [https://api.push.apple.com:443/3/device](https://api.push.apple.com:443/3/device)

> [!IMPORTANT]
> L’authentification basée sur un jeton nécessite la version d’API **2017-04 ou ultérieure**.
> 
> 

Voici un exemple d’un tooupdate de demande PUT un concentrateur avec l’authentification basée sur un jeton :


        PUT https://{namespace}.servicebus.windows.net/{Notification Hub}?api-version=2017-04
          "Properties": {
            "ApnsCredential": {
              "Properties": {
                "KeyId": "<Your Key Id>",
                "Token": "<Your Authentication Token>",
                "AppName": "<Your Application Name>",
                "AppId": "<Your Application Id>",
                "Endpoint":"<Sandbox/Production Endpoint>"
              }
            }
          }
        

### <a name="configure-via-hello-net-sdk"></a>Configurer via hello .NET SDK
Vous pouvez configurer votre concentrateur toouse authentification par jeton notre [dernière version du Kit de développement logiciel client](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/1.0.8). 

Voici un exemple de code illustrant l’utilisation correcte de hello :


        NamespaceManager nm = NamespaceManager.CreateFromConnectionString(_endpoint);
        string token = "YOUR TOKEN HERE";
        string keyId = "YOUR KEY ID HERE";
        string appName = "YOUR APP NAME HERE";
        string appId = "YOUR APP ID HERE";
        NotificationHubDescription desc = new NotificationHubDescription("PATH tooYOUR HUB");
        desc.ApnsCredential = new ApnsCredential(token, keyId, appId, appName);
        desc.ApnsCredential.Endpoint = @"https://api.development.push.apple.com:443/3/device";
        nm.UpdateNotificationHubAsync(desc);

## <a name="reverting-toousing-certificate-based-authentication"></a>Authentification basée sur certificat rétablissement toousing
Vous pouvez revenir à n’importe quel moment toousing authentification par certificat à l’aide de n’importe quel certificat précédent de hello méthode et en passant au lieu des propriétés de jeton hello. Qu’action remplace hello précédemment stockées les informations d’identification.
