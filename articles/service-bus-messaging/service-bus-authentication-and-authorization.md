---
title: "aaaAzure Bus de Service d’authentification et autorisation | Documents Microsoft"
description: "Authentifier les applications tooService Bus avec l’authentification de Signature d’accès partagé (SAS)."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Authentification et de autorisation Service Bus

Les applications peuvent s’authentifier tooAzure Bus de Service à l’aide de la Signature d’accès partagé (SAS) l’authentification. Partagé Signature d’accès d’authentification permet aux applications tooauthenticate tooService Bus à l’aide d’une clé d’accès configurée sur l’espace de noms hello ou sur l’entité hello sont associés à des droits d’accès spécifiques. Vous pouvez ensuite utiliser cette clé toogenerate un jeton de Signature d’accès partagé que les clients peuvent utiliser tooauthenticate tooService Bus.

> [!IMPORTANT]
> Vous devez utiliser SAS au lieu d’Azure Active Directory Access Control (également appelé Access Control Service ou ACS), car ACS est aujourd’hui déprécié. SAS offre un schéma d’authentification simple, flexible et facile à utiliser pour Service Bus. Les applications peuvent utiliser SAS dans des scénarios dans lesquels ils n’avez pas besoin notion de hello toomanage d’un « utilisateur. autorisé » Pour plus d’informations, consultez [ce billet de blog](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)

## <a name="shared-access-signature-authentication"></a>Authentification avec une signature d’accès partagé

[L’authentification SAP](service-bus-sas.md) toogrant vous permet à un utilisateur l’accès tooService Bus des ressources avec des droits spécifiques. L’authentification SAP dans le Bus de Service implique une configuration de hello d’une clé de chiffrement avec les droits correspondants sur une ressource de Service Bus. Les clients peuvent ensuite obtenir l’accès toothat ressource à l’aide d’un jeton SAS, qui se compose d’un URI en cours d’accès de la ressource hello et un délai d’expiration signé avec hello configuré la clé.

Vous pouvez configurer des clés pour SAS dans un espace de noms Service Bus. clé de Hello s’applique à des entités de messagerie tooall dans cet espace de noms. Vous pouvez également configurer des clés sur les rubriques et files d’attente Service Bus. SAP est également pris en charge par [Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md).

toouse SAS, vous pouvez configurer un [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objet sur un espace de noms, une file d’attente ou une rubrique. Cette règle se compose de hello suivant d’éléments :

* *KeyName* qui identifie la règle de hello.
* *PrimaryKey* est une clé de chiffrement utilisée toosign/valider les jetons SAP.
* *SecondaryKey* est une clé de chiffrement utilisée toosign/valider les jetons SAP.
* *Droits* représentant la collection de hello d’écouter, envoyer ou gérer les droits accordés.

Règles d’autorisation configurées au niveau d’espace de noms hello peuvent accorder l’accès tooall des entités dans un espace de noms pour les clients avec des jetons signés à l’aide de la clé correspondante de hello. Les too12 ces règles d’autorisation peuvent être configurés sur un espace de noms, une file d’attente ou une rubrique Service Bus. Par défaut, un élément [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) avec tous les droits est configuré pour chaque espace de noms dès sa mise en service initiale.

tooaccess une entité, les clients hello requiert un jeton SAP généré à l’aide d’un spécifique [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). un jeton SAS Hello est généré à l’aide de hello HMAC-SHA256 d’une chaîne de ressource se compose d’une ressource de hello accès toowhich URI est demandé et expiration avec une clé de chiffrement associée à la règle d’autorisation hello.

L’authentification SAP pour Service Bus est inclus dans les versions du Kit de développement .NET Azure hello 2.0 et versions ultérieures. SAP inclut l’assistance pour [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Toutes les API qui acceptent une chaîne de connexion en tant que paramètre incluent la prise en charge des chaînes de connexion des services SAS.

## <a name="next-steps"></a>Étapes suivantes

- Pour plus d’informations sur la signature d’accès partagé (SAP), consultez [Authentification de Service Bus avec les signatures d’accès partagé](service-bus-sas.md).
- [Modifie les espaces de noms tooACS activé.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Pour obtenir les informations correspondantes sur les autorisations et l’authentification Azure Relay, consultez [Authentification et autorisation Azure Relay](../service-bus-relay/relay-authentication-and-authorization.md). 

