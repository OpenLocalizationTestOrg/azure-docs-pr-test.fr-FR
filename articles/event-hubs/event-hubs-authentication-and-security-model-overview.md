---
title: "aaaOverview du modèle de sécurité et d’authentification Azure Event Hubs | Documents Microsoft"
description: "Présentation du modèle de sécurité et de l'authentification Event Hubs."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>Présentation du modèle de sécurité et de l'authentification Event Hubs
modèle de sécurité Azure Event Hubs Hello répond aux hello suivant les exigences :

* Seuls les clients qui présentent des informations d’identification valides peuvent envoyer le concentrateur d’événements tooan données.
* Un client ne peut pas emprunter l’identité d’un autre client.
* Un client non autorisé peut être bloqué à partir de l’envoi de concentrateur d’événements de tooan de données.

## <a name="client-authentication"></a>Authentification du client
modèle de sécurité de concentrateurs d’événements Hello est basé sur une combinaison de [Signature d’accès partagé (SAS)](../service-bus-messaging/service-bus-sas.md) jetons et *éditeurs d’événements*. Un éditeur d’événements définit un point de terminaison virtuel pour un hub d’événements. serveur de publication Hello peut uniquement être utilisé toosend concentrateur d’événements de messages tooan. Il n’est pas possible de tooreceive des messages à partir d’un serveur de publication.

En règle générale, un hub d’événements utilise un seul éditeur par client. Tous les messages sont envoyés tooany des éditeurs hello d’un concentrateur d’événements sont empilés dans le concentrateur d’événements. Les éditeurs permettent un contrôle d’accès précis et une limitation.

Chaque client de concentrateurs d’événements reçoit un jeton unique, qui est téléchargé toohello client. les jetons de Hello sont produits de telle sorte que chaque jeton donne accès tooa différents unique de l’éditeur. Un client qui possède un jeton peut uniquement envoyer tooone le serveur de publication, mais aucun autre serveur de publication. Si plusieurs clients partage hello même jeton, puis chacun d’eux partage sur un serveur de publication.

Ne pas recommandée, mais il est possible tooequip les appareils avec des jetons qui accordent le concentrateur d’événements tooan un accès direct. N’importe quel appareil qui détient ce jeton peut envoyer des messages directement dans ce hub d’événements. Un tel appareil ne sera pas toothrottling de l’objet. En outre, les appareils hello ne peut pas être empêché d’envoyer le concentrateur d’événements toothat.

Tous les jetons sont signés avec une clé SAS. En règle générale, tous les jetons sont signés avec hello même clé. Les clients ne connaissent pas de clé de hello ; Cela empêche des autres clients de fabriquer des jetons.

### <a name="create-hello-sas-key"></a>Créer la clé SAS de hello

Lorsque vous créez un espace de noms du service Event Hubs, service de hello génère une clé SAS de 256 bits nommée **RootManageSharedAccessKey**. Cette clé permet d’envoi, écoute et gérer l’espace de noms toohello droits. Vous pouvez aussi créer des clés supplémentaires. Il est recommandé de produire une clé qui permet d’envoyer concentrateur d’événements spécifique toohello autorisations. Pour le reste de hello de cette rubrique, il est supposé que vous avez nommé cette clé **EventHubSendKey**.

Hello l’exemple suivant crée une clé d’envoi uniquement lors de la création du concentrateur d’événements hello :

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>Générer des jetons

Vous pouvez générer des jetons à l’aide de la clé SAS hello. Vous ne devez produire qu’un seul jeton par client. Les jetons peuvent alors être générés à l’aide de hello suivant de méthode. Tous les jetons sont générés à l’aide de hello **EventHubSendKey** clé. Une URI unique est affectée à chaque jeton.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Lorsque vous appelez cette méthode, hello URI doit être spécifié en tant que `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Pour tous les jetons, hello URI est identique, à l’exception de hello de `PUBLISHER_NAME`, qui doit être différent pour chaque jeton. Dans l’idéal, `PUBLISHER_NAME` représente hello ID du client hello qui reçoit ce jeton.

Cette méthode génère un jeton avec hello suivant structure :

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

heure d’expiration du jeton de Hello est exprimée en secondes à partir du 1er janvier 1970. Hello Voici un exemple de jeton :

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

En règle générale, les jetons hello ont une durée de vie similaire ou supérieure de durée de vie hello du client de hello. Si les client hello a hello capacité tooobtain un nouveau jeton, jetons avec une durée de vie inférieure peuvent être utilisés.

### <a name="sending-data"></a>Envoi de données
Une fois que les jetons hello ont été créées, chaque client est configuré avec son propre jeton unique.

Lorsque le client de hello envoie les données dans un concentrateur d’événements, il balises sa demande d’envoi avec le jeton de hello. tooprevent une personne malveillante d’écouter et de voler le jeton de hello, communication hello entre le client de hello et le concentrateur d’événements hello de doit se produire sur un canal chiffré.

### <a name="blacklisting-clients"></a>Inscription des clients sur liste noire
Si un jeton est volé par une personne malveillante, hello peut emprunter l’identité client hello dont le jeton a été volé. L’inscription d’un client sur liste noire le rend inutilisable, jusqu’à ce qu’il reçoive un nouveau jeton qui utilise un éditeur différent.

## <a name="authentication-of-back-end-applications"></a>Authentification des applications principales

applications principales tooauthenticate qui consomment des données hello générées par les clients de concentrateurs d’événements, le service Event Hubs utilise un modèle de sécurité qui est le modèle toohello similaire qui est utilisé pour les rubriques Service Bus. Un groupe de consommateurs de concentrateurs d’événements est tooa équivalente de la rubrique abonnement tooa Service Bus. Un client peut créer un groupe de consommateurs si le groupe de consommateurs hello demande toocreate hello est accompagné d’un jeton que de gérer des privilèges pour le concentrateur d’événements hello ou pour toowhich d’espace de noms hello concentrateur d’événements hello appartient. Un client est autorisé à tooconsume des données à partir d’un groupe de consommateurs si la demande de réception hello sont accompagnées par un jeton qu’accorde des droits sur ce groupe de consommateurs de réception, hello concentrateur d’événements, ou le concentrateur d’événements hello espace de noms toowhich hello appartient.

version actuelle de Hello du Bus de Service ne prend pas en charge les règles SAS pour les abonnements individuels. Hello que va de même pour les groupes de consommateurs de concentrateurs d’événements. Prise en charge SAS sera ajouté pour les deux fonctionnalités Bonjour futures.

En absence de hello d’authentification SAP des groupes de consommateurs individuels, vous pouvez utiliser tous les groupes de consommateurs SAS clés toosecure avec une clé commune. Cette approche permet à une application tooconsume les données de groupes de consommateurs hello d’un concentrateur d’événements.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les concentrateurs d’événements, consultez hello rubriques suivantes :

* [Vue d’ensemble des hubs d’événements]
* [Présentation des signatures d’accès partagé]
* [Exemples d’applications qui utilisent des Event Hubs]

[Vue d’ensemble des hubs d’événements]: event-hubs-what-is-event-hubs.md
[Exemples d’applications qui utilisent des Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Présentation des signatures d’accès partagé]: ../service-bus-messaging/service-bus-sas.md

