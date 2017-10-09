---
title: "aaaAzure relais d’authentification et autorisation | Documents Microsoft"
description: "Vue d’ensemble de l’authentification par signature d’accès partagé (SAP) dans Azure Relay"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Authentification et autorisation Azure Relay
Les applications peuvent s’authentifier tooAzure de relais à l’aide de l’authentification de Signature d’accès partagé (SAS). Similaire trop[messagerie Service Bus](../service-bus-messaging/service-bus-authentication-and-authorization.md), l’authentification SAP permet d’applications tooauthenticate toohello service de relais d’Azure à l’aide d’une clé d’accès configurée sur l’espace de noms de relais hello. Vous pouvez ensuite utiliser cette clé toogenerate un jeton de Signature d’accès partagé que les clients peuvent utiliser service de relais tooauthenticate toohello.

## <a name="shared-access-signature-authentication"></a>Authentification avec une signature d’accès partagé
[L’authentification SAP](../service-bus-messaging/service-bus-sas.md) toogrant vous permet à un utilisateur l’accès tooAzure relais des ressources avec des droits spécifiques. L’authentification SAP implique une configuration de hello d’une clé de chiffrement avec les droits correspondants sur une ressource. Les clients peuvent ensuite obtenir l’accès toothat ressource à l’aide d’un jeton SAS, qui se compose d’un URI en cours d’accès de la ressource hello et un délai d’expiration signé avec hello configuré la clé.

Vous pouvez configurer des clés pour SAP dans un espace de noms Relay. Contrairement à la messagerie Service Bus, les [connexions hybrides Relay](relay-hybrid-connections-protocol.md) prennent en charge les expéditeurs non autorisés ou anonymes. Vous pouvez activer l’accès anonyme pour l’entité de hello lorsque vous créez, comme indiqué dans hello suivant capture d’écran de portail de hello :

![][0]

toouse SAS, vous pouvez configurer un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objet sur un espace de noms de relais qui se compose des éléments suivants de hello :

* *KeyName* qui identifie la règle de hello.
* *PrimaryKey* est une clé de chiffrement utilisée toosign/valider les jetons SAP.
* *SecondaryKey* est une clé de chiffrement utilisée toosign/valider les jetons SAP.
* *Droits* représentant la collection de hello d’écouter, envoyer ou gérer les droits accordés.

Règles d’autorisation configurées au niveau d’espace de noms hello peuvent accorder l’accès tooall les connexions de relais dans un espace de noms pour les clients avec des jetons signés à l’aide de la clé correspondante de hello. Les too12 ces règles d’autorisation peuvent être configurés sur un espace de noms de relais. Par défaut, un élément [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) avec tous les droits est configuré pour chaque espace de noms dès sa mise en service initiale.

tooaccess une entité, les clients hello requiert un jeton SAP généré à l’aide d’un spécifique [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). un jeton SAS Hello est généré à l’aide de hello HMAC-SHA256 d’une chaîne de ressource se compose d’une ressource de hello accès toowhich URI est demandé et expiration avec une clé de chiffrement associée à la règle d’autorisation hello.

Prise en charge de l’authentification SAP pour Azure relais est inclus dans les versions du Kit de développement .NET Azure hello 2.0 et versions ultérieures. SAP inclut l’assistance pour [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Toutes les API qui acceptent une chaîne de connexion en tant que paramètre incluent la prise en charge des chaînes de connexion des services SAS.

## <a name="next-steps"></a>Étapes suivantes
- Pour plus d’informations sur la signature d’accès partagé (SAP), consultez [Authentification de Service Bus avec les signatures d’accès partagé](../service-bus-messaging/service-bus-sas.md).
- Consultez hello [connexions hybrides de relais Azure protocole guide](relay-hybrid-connections-protocol.md) pour des informations détaillées sur hello capacité de connexions hybrides.
- Pour obtenir les informations correspondantes sur les autorisations et l’authentification de la messagerie Service Bus, consultez [Authentification et autorisation Service Bus](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png