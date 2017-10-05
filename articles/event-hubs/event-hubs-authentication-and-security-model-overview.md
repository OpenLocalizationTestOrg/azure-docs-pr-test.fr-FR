---
title: "Vue d’ensemble du modèle de sécurité et d’authentification Azure Event Hubs| Microsoft Docs"
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
ms.openlocfilehash: 5abdbf70d4fdb2c7feb0f3537ecc0f2abf0775a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="ff43b-103">Présentation du modèle de sécurité et de l'authentification Event Hubs</span><span class="sxs-lookup"><span data-stu-id="ff43b-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="ff43b-104">Le modèle de sécurité Azure Event Hubs remplit les conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="ff43b-104">The Azure Event Hubs security model meets the following requirements:</span></span>

* <span data-ttu-id="ff43b-105">Seuls les clients qui présentent des informations d’identification valides peuvent envoyer des données à un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-105">Only clients that present valid credentials can send data to an event hub.</span></span>
* <span data-ttu-id="ff43b-106">Un client ne peut pas emprunter l’identité d’un autre client.</span><span class="sxs-lookup"><span data-stu-id="ff43b-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="ff43b-107">Il est possible d’empêcher un client non autorisé d’envoyer des données à un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-107">A rogue client can be blocked from sending data to an event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="ff43b-108">Authentification du client</span><span class="sxs-lookup"><span data-stu-id="ff43b-108">Client authentication</span></span>
<span data-ttu-id="ff43b-109">Le modèle de sécurité du hub d’événements est basé sur une combinaison de jetons de [signature d’accès partagé (SAS)](../service-bus-messaging/service-bus-sas.md) et d’*éditeurs d’événements*.</span><span class="sxs-lookup"><span data-stu-id="ff43b-109">The Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="ff43b-110">Un éditeur d’événements définit un point de terminaison virtuel pour un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="ff43b-111">L’éditeur ne peut être utilisé que pour envoyer des messages à un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-111">The publisher can only be used to send messages to an event hub.</span></span> <span data-ttu-id="ff43b-112">Il n'est pas possible de recevoir des messages à partir de l'éditeur.</span><span class="sxs-lookup"><span data-stu-id="ff43b-112">It is not possible to receive messages from a publisher.</span></span>

<span data-ttu-id="ff43b-113">En règle générale, un hub d’événements utilise un seul éditeur par client.</span><span class="sxs-lookup"><span data-stu-id="ff43b-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="ff43b-114">Tous les messages qui sont envoyés à l’un des éditeurs d’un hub d’événements sont empilés dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="ff43b-114">All messages that are sent to any of the publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="ff43b-115">Les éditeurs permettent un contrôle d’accès précis et une limitation.</span><span class="sxs-lookup"><span data-stu-id="ff43b-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="ff43b-116">Un jeton unique, qui est téléchargé sur le client, est affecté à chaque hub d’événement.</span><span class="sxs-lookup"><span data-stu-id="ff43b-116">Each Event Hubs client is assigned a unique token, which is uploaded to the client.</span></span> <span data-ttu-id="ff43b-117">Les jetons sont produits de façon à ce que chaque jeton unique donne accès à un éditeur unique différent.</span><span class="sxs-lookup"><span data-stu-id="ff43b-117">The tokens are produced such that each unique token grants access to a different unique publisher.</span></span> <span data-ttu-id="ff43b-118">Un client qui possède un jeton ne peut envoyer qu’à un seul éditeur, et à aucun autre.</span><span class="sxs-lookup"><span data-stu-id="ff43b-118">A client that possesses a token can only send to one publisher, but no other publisher.</span></span> <span data-ttu-id="ff43b-119">Si plusieurs clients partagent le même jeton, alors ils partagent un éditeur.</span><span class="sxs-lookup"><span data-stu-id="ff43b-119">If multiple clients share the same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="ff43b-120">Bien que cela soit déconseillé, il est possible d’équiper les appareils de jetons qui donnent un accès direct à un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-120">Although not recommended, it is possible to equip devices with tokens that grant direct access to an event hub.</span></span> <span data-ttu-id="ff43b-121">N’importe quel appareil qui détient ce jeton peut envoyer des messages directement dans ce hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="ff43b-122">Un appareil de ce type ne sera pas soumis à la limitation.</span><span class="sxs-lookup"><span data-stu-id="ff43b-122">Such a device will not be subject to throttling.</span></span> <span data-ttu-id="ff43b-123">En outre, il est impossible d’empêcher l’appareil d’effectuer des envois à ce hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-123">Furthermore, the device cannot be blacklisted from sending to that event hub.</span></span>

<span data-ttu-id="ff43b-124">Tous les jetons sont signés avec une clé SAS.</span><span class="sxs-lookup"><span data-stu-id="ff43b-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="ff43b-125">En règle générale, tous les jetons sont signés avec la même clé.</span><span class="sxs-lookup"><span data-stu-id="ff43b-125">Typically, all tokens are signed with the same key.</span></span> <span data-ttu-id="ff43b-126">Les clients ne sont pas conscients de la clé. Cela empêche que d’autres clients fabriquent des jetons.</span><span class="sxs-lookup"><span data-stu-id="ff43b-126">Clients are not aware of the key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-the-sas-key"></a><span data-ttu-id="ff43b-127">Créer la clé SAP</span><span class="sxs-lookup"><span data-stu-id="ff43b-127">Create the SAS key</span></span>

<span data-ttu-id="ff43b-128">Lorsque vous créez un espace de noms Event Hubs, le service génère une clé SAS de 256 bits nommée **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="ff43b-128">When creating an Event Hubs namespace, the service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="ff43b-129">Cette clé accorde les droits d'envoi, d'écoute et de gestion pour l'espace de noms.</span><span class="sxs-lookup"><span data-stu-id="ff43b-129">This key grants send, listen, and manage rights to the namespace.</span></span> <span data-ttu-id="ff43b-130">Vous pouvez aussi créer des clés supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ff43b-130">You can also create additional keys.</span></span> <span data-ttu-id="ff43b-131">Nous vous recommandons de produire une clé qui accorde les droits d’envoi au hub d’événements spécifique.</span><span class="sxs-lookup"><span data-stu-id="ff43b-131">It is recommended that you produce a key that grants send permissions to the specific event hub.</span></span> <span data-ttu-id="ff43b-132">Pour le reste de cette rubrique, supposons que vous avez nommé cette clé **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="ff43b-132">For the remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="ff43b-133">L’exemple suivant crée une clé exclusivement pour l’envoi, lors de la création du hub d’événements :</span><span class="sxs-lookup"><span data-stu-id="ff43b-133">The following example creates a send-only key when creating the event hub:</span></span>

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending to that event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a><span data-ttu-id="ff43b-134">Générer des jetons</span><span class="sxs-lookup"><span data-stu-id="ff43b-134">Generate tokens</span></span>

<span data-ttu-id="ff43b-135">Vous pouvez générer des jetons à l'aide de la clé SAS.</span><span class="sxs-lookup"><span data-stu-id="ff43b-135">You can generate tokens using the SAS key.</span></span> <span data-ttu-id="ff43b-136">Vous ne devez produire qu’un seul jeton par client.</span><span class="sxs-lookup"><span data-stu-id="ff43b-136">You must produce only one token per client.</span></span> <span data-ttu-id="ff43b-137">Les jetons peuvent ensuite être générés à l'aide de la méthode suivante.</span><span class="sxs-lookup"><span data-stu-id="ff43b-137">Tokens can then be produced using the following method.</span></span> <span data-ttu-id="ff43b-138">Tous les jetons sont générés à l'aide de la clé **EventHubSendKey** .</span><span class="sxs-lookup"><span data-stu-id="ff43b-138">All tokens are generated using the **EventHubSendKey** key.</span></span> <span data-ttu-id="ff43b-139">Une URI unique est affectée à chaque jeton.</span><span class="sxs-lookup"><span data-stu-id="ff43b-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="ff43b-140">Lors de l'appel de cette méthode, l'URI doit être spécifiée en tant que `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="ff43b-140">When calling this method, the URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="ff43b-141">Pour tous les jetons, l'URI est identique, à l'exception de `PUBLISHER_NAME`, qui doit être différent pour chaque jeton.</span><span class="sxs-lookup"><span data-stu-id="ff43b-141">For all tokens, the URI is identical, with the exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="ff43b-142">Dans l’idéal, `PUBLISHER_NAME` représente l’ID du client qui reçoit ce jeton.</span><span class="sxs-lookup"><span data-stu-id="ff43b-142">Ideally, `PUBLISHER_NAME` represents the ID of the client that receives that token.</span></span>

<span data-ttu-id="ff43b-143">Cette méthode génère un jeton avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="ff43b-143">This method generates a token with the following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="ff43b-144">L'heure d'expiration du jeton est exprimée en secondes à partir du 1er janvier 1970.</span><span class="sxs-lookup"><span data-stu-id="ff43b-144">The token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="ff43b-145">Vous trouverez ci-dessous un exemple de jeton :</span><span class="sxs-lookup"><span data-stu-id="ff43b-145">The following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="ff43b-146">En règle générale, les jetons ont une durée de vie équivalente ou supérieure à la durée de vie du client.</span><span class="sxs-lookup"><span data-stu-id="ff43b-146">Typically, the tokens have a lifespan that resembles or exceeds the lifespan of the client.</span></span> <span data-ttu-id="ff43b-147">Si le client a la possibilité d’obtenir un nouveau jeton, il est possible d’utiliser des jetons avec une durée de vie plus courte.</span><span class="sxs-lookup"><span data-stu-id="ff43b-147">If the client has the capability to obtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="ff43b-148">Envoi de données</span><span class="sxs-lookup"><span data-stu-id="ff43b-148">Sending data</span></span>
<span data-ttu-id="ff43b-149">Une fois les jetons créés, chaque client est configuré avec son propre jeton unique.</span><span class="sxs-lookup"><span data-stu-id="ff43b-149">Once the tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="ff43b-150">Lorsque le client envoie des données dans un hub d’événements, il balise sa requête d’envoi avec le jeton.</span><span class="sxs-lookup"><span data-stu-id="ff43b-150">When the client sends data into an event hub, it tags its send request with the token.</span></span> <span data-ttu-id="ff43b-151">Pour empêcher un intrus de procéder à des écoutes clandestines et de voler le jeton, la communication entre le client et le hub d’événements doit avoir lieu sur un canal chiffré.</span><span class="sxs-lookup"><span data-stu-id="ff43b-151">To prevent an attacker from eavesdropping and stealing the token, the communication between the client and the event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="ff43b-152">Inscription des clients sur liste noire</span><span class="sxs-lookup"><span data-stu-id="ff43b-152">Blacklisting clients</span></span>
<span data-ttu-id="ff43b-153">Si un jeton est volé par un intrus, celui-ci peut emprunter l’identité du client à qui le jeton a été volé.</span><span class="sxs-lookup"><span data-stu-id="ff43b-153">If a token is stolen by an attacker, the attacker can impersonate the client whose token has been stolen.</span></span> <span data-ttu-id="ff43b-154">L’inscription d’un client sur liste noire le rend inutilisable, jusqu’à ce qu’il reçoive un nouveau jeton qui utilise un éditeur différent.</span><span class="sxs-lookup"><span data-stu-id="ff43b-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="ff43b-155">Authentification des applications principales</span><span class="sxs-lookup"><span data-stu-id="ff43b-155">Authentication of back-end applications</span></span>

<span data-ttu-id="ff43b-156">Pour authentifier des applications principales qui consomment les données générées par les clients Event Hubs, Event Hubs utilise un modèle de sécurité qui est similaire au modèle utilisé pour les rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ff43b-156">To authenticate back-end applications that consume the data generated by Event Hubs clients, Event Hubs employs a security model that is similar to the model that is used for Service Bus topics.</span></span> <span data-ttu-id="ff43b-157">Un groupe de consommateurs Event Hubs est équivalent à un abonnement à une rubrique Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ff43b-157">An Event Hubs consumer group is equivalent to a subscription to a Service Bus topic.</span></span> <span data-ttu-id="ff43b-158">Un client peut créer un groupe de consommateurs si la requête de création du groupe de consommateurs est accompagnée d’un jeton qui accorde des droits de gestion pour le hub d’événements ou pour l’espace de noms auxquels appartient le hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-158">A client can create a consumer group if the request to create the consumer group is accompanied by a token that grants manage privileges for the event hub, or for the namespace to which the event hub belongs.</span></span> <span data-ttu-id="ff43b-159">Un client est autorisé à consommer des données à partir d’un groupe de consommateurs si la requête de réception est accompagnée d’un jeton qui accorde des droits de réception pour ce groupe de consommateurs, le hub d’événements ou l’espace de noms auxquels appartient le hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-159">A client is allowed to consume data from a consumer group if the receive request is accompanied by a token that grants receive rights on that consumer group, the event hub, or the namespace to which the event hub belongs.</span></span>

<span data-ttu-id="ff43b-160">La version actuelle de Service Bus ne prend pas en charge les règles SAS pour les abonnements individuels.</span><span class="sxs-lookup"><span data-stu-id="ff43b-160">The current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="ff43b-161">Il en va de même pour les groupes de consommateurs de hubs d'événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-161">The same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="ff43b-162">La prise en charge SAS sera ajoutée ultérieurement pour ces deux fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="ff43b-162">SAS support will be added for both features in the future.</span></span>

<span data-ttu-id="ff43b-163">En l'absence d'authentification SAS pour les groupes de consommateurs individuels, vous pouvez utiliser des clés SAS pour sécuriser tous les groupes de consommateurs avec une clé commune.</span><span class="sxs-lookup"><span data-stu-id="ff43b-163">In the absence of SAS authentication for individual consumer groups, you can use SAS keys to secure all consumer groups with a common key.</span></span> <span data-ttu-id="ff43b-164">Cette approche permet à une application de consommer des données à partir de n’importe quel groupe de consommateurs d’un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="ff43b-164">This approach enables an application to consume data from any of the consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff43b-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ff43b-165">Next steps</span></span>
<span data-ttu-id="ff43b-166">Pour plus d’informations sur Event Hubs, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="ff43b-166">To learn more about Event Hubs, visit the following topics:</span></span>

* <span data-ttu-id="ff43b-167">[Vue d’ensemble des hubs d’événements]</span><span class="sxs-lookup"><span data-stu-id="ff43b-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="ff43b-168">[Présentation des signatures d’accès partagé]</span><span class="sxs-lookup"><span data-stu-id="ff43b-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="ff43b-169">[Exemples d’applications qui utilisent des Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="ff43b-169">[Sample applications that use Event Hubs]</span></span>

<span data-ttu-id="ff43b-170">[Vue d’ensemble des hubs d’événements]: event-hubs-what-is-event-hubs.md</span><span class="sxs-lookup"><span data-stu-id="ff43b-170">[Event Hubs overview]: event-hubs-what-is-event-hubs.md</span></span>
<span data-ttu-id="ff43b-171">[Exemples d’applications qui utilisent des Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span><span class="sxs-lookup"><span data-stu-id="ff43b-171">[Sample applications that use Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples</span></span>
<span data-ttu-id="ff43b-172">[Présentation des signatures d’accès partagé]: ../service-bus-messaging/service-bus-sas.md</span><span class="sxs-lookup"><span data-stu-id="ff43b-172">[Overview of Shared Access Signatures]: ../service-bus-messaging/service-bus-sas.md</span></span>

