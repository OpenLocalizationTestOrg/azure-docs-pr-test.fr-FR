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
# <a name="event-hubs-authentication-and-security-model-overview"></a><span data-ttu-id="e5277-103">Présentation du modèle de sécurité et de l'authentification Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e5277-103">Event Hubs authentication and security model overview</span></span>
<span data-ttu-id="e5277-104">modèle de sécurité Azure Event Hubs Hello répond aux hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="e5277-104">hello Azure Event Hubs security model meets hello following requirements:</span></span>

* <span data-ttu-id="e5277-105">Seuls les clients qui présentent des informations d’identification valides peuvent envoyer le concentrateur d’événements tooan données.</span><span class="sxs-lookup"><span data-stu-id="e5277-105">Only clients that present valid credentials can send data tooan event hub.</span></span>
* <span data-ttu-id="e5277-106">Un client ne peut pas emprunter l’identité d’un autre client.</span><span class="sxs-lookup"><span data-stu-id="e5277-106">A client cannot impersonate another client.</span></span>
* <span data-ttu-id="e5277-107">Un client non autorisé peut être bloqué à partir de l’envoi de concentrateur d’événements de tooan de données.</span><span class="sxs-lookup"><span data-stu-id="e5277-107">A rogue client can be blocked from sending data tooan event hub.</span></span>

## <a name="client-authentication"></a><span data-ttu-id="e5277-108">Authentification du client</span><span class="sxs-lookup"><span data-stu-id="e5277-108">Client authentication</span></span>
<span data-ttu-id="e5277-109">modèle de sécurité de concentrateurs d’événements Hello est basé sur une combinaison de [Signature d’accès partagé (SAS)](../service-bus-messaging/service-bus-sas.md) jetons et *éditeurs d’événements*.</span><span class="sxs-lookup"><span data-stu-id="e5277-109">hello Event Hubs security model is based on a combination of [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens and *event publishers*.</span></span> <span data-ttu-id="e5277-110">Un éditeur d’événements définit un point de terminaison virtuel pour un hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="e5277-110">An event publisher defines a virtual endpoint for an event hub.</span></span> <span data-ttu-id="e5277-111">serveur de publication Hello peut uniquement être utilisé toosend concentrateur d’événements de messages tooan.</span><span class="sxs-lookup"><span data-stu-id="e5277-111">hello publisher can only be used toosend messages tooan event hub.</span></span> <span data-ttu-id="e5277-112">Il n’est pas possible de tooreceive des messages à partir d’un serveur de publication.</span><span class="sxs-lookup"><span data-stu-id="e5277-112">It is not possible tooreceive messages from a publisher.</span></span>

<span data-ttu-id="e5277-113">En règle générale, un hub d’événements utilise un seul éditeur par client.</span><span class="sxs-lookup"><span data-stu-id="e5277-113">Typically, an event hub employs one publisher per client.</span></span> <span data-ttu-id="e5277-114">Tous les messages sont envoyés tooany des éditeurs hello d’un concentrateur d’événements sont empilés dans le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="e5277-114">All messages that are sent tooany of hello publishers of an event hub are enqueued within that event hub.</span></span> <span data-ttu-id="e5277-115">Les éditeurs permettent un contrôle d’accès précis et une limitation.</span><span class="sxs-lookup"><span data-stu-id="e5277-115">Publishers enable fine-grained access control and throttling.</span></span>

<span data-ttu-id="e5277-116">Chaque client de concentrateurs d’événements reçoit un jeton unique, qui est téléchargé toohello client.</span><span class="sxs-lookup"><span data-stu-id="e5277-116">Each Event Hubs client is assigned a unique token, which is uploaded toohello client.</span></span> <span data-ttu-id="e5277-117">les jetons de Hello sont produits de telle sorte que chaque jeton donne accès tooa différents unique de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="e5277-117">hello tokens are produced such that each unique token grants access tooa different unique publisher.</span></span> <span data-ttu-id="e5277-118">Un client qui possède un jeton peut uniquement envoyer tooone le serveur de publication, mais aucun autre serveur de publication.</span><span class="sxs-lookup"><span data-stu-id="e5277-118">A client that possesses a token can only send tooone publisher, but no other publisher.</span></span> <span data-ttu-id="e5277-119">Si plusieurs clients partage hello même jeton, puis chacun d’eux partage sur un serveur de publication.</span><span class="sxs-lookup"><span data-stu-id="e5277-119">If multiple clients share hello same token, then each of them shares a publisher.</span></span>

<span data-ttu-id="e5277-120">Ne pas recommandée, mais il est possible tooequip les appareils avec des jetons qui accordent le concentrateur d’événements tooan un accès direct.</span><span class="sxs-lookup"><span data-stu-id="e5277-120">Although not recommended, it is possible tooequip devices with tokens that grant direct access tooan event hub.</span></span> <span data-ttu-id="e5277-121">N’importe quel appareil qui détient ce jeton peut envoyer des messages directement dans ce hub d’événements.</span><span class="sxs-lookup"><span data-stu-id="e5277-121">Any device that holds this token can send messages directly into that event hub.</span></span> <span data-ttu-id="e5277-122">Un tel appareil ne sera pas toothrottling de l’objet.</span><span class="sxs-lookup"><span data-stu-id="e5277-122">Such a device will not be subject toothrottling.</span></span> <span data-ttu-id="e5277-123">En outre, les appareils hello ne peut pas être empêché d’envoyer le concentrateur d’événements toothat.</span><span class="sxs-lookup"><span data-stu-id="e5277-123">Furthermore, hello device cannot be blacklisted from sending toothat event hub.</span></span>

<span data-ttu-id="e5277-124">Tous les jetons sont signés avec une clé SAS.</span><span class="sxs-lookup"><span data-stu-id="e5277-124">All tokens are signed with a SAS key.</span></span> <span data-ttu-id="e5277-125">En règle générale, tous les jetons sont signés avec hello même clé.</span><span class="sxs-lookup"><span data-stu-id="e5277-125">Typically, all tokens are signed with hello same key.</span></span> <span data-ttu-id="e5277-126">Les clients ne connaissent pas de clé de hello ; Cela empêche des autres clients de fabriquer des jetons.</span><span class="sxs-lookup"><span data-stu-id="e5277-126">Clients are not aware of hello key; this prevents other clients from manufacturing tokens.</span></span>

### <a name="create-hello-sas-key"></a><span data-ttu-id="e5277-127">Créer la clé SAS de hello</span><span class="sxs-lookup"><span data-stu-id="e5277-127">Create hello SAS key</span></span>

<span data-ttu-id="e5277-128">Lorsque vous créez un espace de noms du service Event Hubs, service de hello génère une clé SAS de 256 bits nommée **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="e5277-128">When creating an Event Hubs namespace, hello service generates a 256-bit SAS key named **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="e5277-129">Cette clé permet d’envoi, écoute et gérer l’espace de noms toohello droits.</span><span class="sxs-lookup"><span data-stu-id="e5277-129">This key grants send, listen, and manage rights toohello namespace.</span></span> <span data-ttu-id="e5277-130">Vous pouvez aussi créer des clés supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="e5277-130">You can also create additional keys.</span></span> <span data-ttu-id="e5277-131">Il est recommandé de produire une clé qui permet d’envoyer concentrateur d’événements spécifique toohello autorisations.</span><span class="sxs-lookup"><span data-stu-id="e5277-131">It is recommended that you produce a key that grants send permissions toohello specific event hub.</span></span> <span data-ttu-id="e5277-132">Pour le reste de hello de cette rubrique, il est supposé que vous avez nommé cette clé **EventHubSendKey**.</span><span class="sxs-lookup"><span data-stu-id="e5277-132">For hello remainder of this topic, it is assumed that you named this key **EventHubSendKey**.</span></span>

<span data-ttu-id="e5277-133">Hello l’exemple suivant crée une clé d’envoi uniquement lors de la création du concentrateur d’événements hello :</span><span class="sxs-lookup"><span data-stu-id="e5277-133">hello following example creates a send-only key when creating hello event hub:</span></span>

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

### <a name="generate-tokens"></a><span data-ttu-id="e5277-134">Générer des jetons</span><span class="sxs-lookup"><span data-stu-id="e5277-134">Generate tokens</span></span>

<span data-ttu-id="e5277-135">Vous pouvez générer des jetons à l’aide de la clé SAS hello.</span><span class="sxs-lookup"><span data-stu-id="e5277-135">You can generate tokens using hello SAS key.</span></span> <span data-ttu-id="e5277-136">Vous ne devez produire qu’un seul jeton par client.</span><span class="sxs-lookup"><span data-stu-id="e5277-136">You must produce only one token per client.</span></span> <span data-ttu-id="e5277-137">Les jetons peuvent alors être générés à l’aide de hello suivant de méthode.</span><span class="sxs-lookup"><span data-stu-id="e5277-137">Tokens can then be produced using hello following method.</span></span> <span data-ttu-id="e5277-138">Tous les jetons sont générés à l’aide de hello **EventHubSendKey** clé.</span><span class="sxs-lookup"><span data-stu-id="e5277-138">All tokens are generated using hello **EventHubSendKey** key.</span></span> <span data-ttu-id="e5277-139">Une URI unique est affectée à chaque jeton.</span><span class="sxs-lookup"><span data-stu-id="e5277-139">Each token is assigned a unique URI.</span></span>

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

<span data-ttu-id="e5277-140">Lorsque vous appelez cette méthode, hello URI doit être spécifié en tant que `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span><span class="sxs-lookup"><span data-stu-id="e5277-140">When calling this method, hello URI should be specified as `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`.</span></span> <span data-ttu-id="e5277-141">Pour tous les jetons, hello URI est identique, à l’exception de hello de `PUBLISHER_NAME`, qui doit être différent pour chaque jeton.</span><span class="sxs-lookup"><span data-stu-id="e5277-141">For all tokens, hello URI is identical, with hello exception of `PUBLISHER_NAME`, which should be different for each token.</span></span> <span data-ttu-id="e5277-142">Dans l’idéal, `PUBLISHER_NAME` représente hello ID du client hello qui reçoit ce jeton.</span><span class="sxs-lookup"><span data-stu-id="e5277-142">Ideally, `PUBLISHER_NAME` represents hello ID of hello client that receives that token.</span></span>

<span data-ttu-id="e5277-143">Cette méthode génère un jeton avec hello suivant structure :</span><span class="sxs-lookup"><span data-stu-id="e5277-143">This method generates a token with hello following structure:</span></span>

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

<span data-ttu-id="e5277-144">heure d’expiration du jeton de Hello est exprimée en secondes à partir du 1er janvier 1970.</span><span class="sxs-lookup"><span data-stu-id="e5277-144">hello token expiration time is specified in seconds from Jan 1, 1970.</span></span> <span data-ttu-id="e5277-145">Hello Voici un exemple de jeton :</span><span class="sxs-lookup"><span data-stu-id="e5277-145">hello following is an example of a token:</span></span>

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

<span data-ttu-id="e5277-146">En règle générale, les jetons hello ont une durée de vie similaire ou supérieure de durée de vie hello du client de hello.</span><span class="sxs-lookup"><span data-stu-id="e5277-146">Typically, hello tokens have a lifespan that resembles or exceeds hello lifespan of hello client.</span></span> <span data-ttu-id="e5277-147">Si les client hello a hello capacité tooobtain un nouveau jeton, jetons avec une durée de vie inférieure peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="e5277-147">If hello client has hello capability tooobtain a new token, tokens with a shorter lifespan can be used.</span></span>

### <a name="sending-data"></a><span data-ttu-id="e5277-148">Envoi de données</span><span class="sxs-lookup"><span data-stu-id="e5277-148">Sending data</span></span>
<span data-ttu-id="e5277-149">Une fois que les jetons hello ont été créées, chaque client est configuré avec son propre jeton unique.</span><span class="sxs-lookup"><span data-stu-id="e5277-149">Once hello tokens have been created, each client is provisioned with its own unique token.</span></span>

<span data-ttu-id="e5277-150">Lorsque le client de hello envoie les données dans un concentrateur d’événements, il balises sa demande d’envoi avec le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="e5277-150">When hello client sends data into an event hub, it tags its send request with hello token.</span></span> <span data-ttu-id="e5277-151">tooprevent une personne malveillante d’écouter et de voler le jeton de hello, communication hello entre le client de hello et le concentrateur d’événements hello de doit se produire sur un canal chiffré.</span><span class="sxs-lookup"><span data-stu-id="e5277-151">tooprevent an attacker from eavesdropping and stealing hello token, hello communication between hello client and hello event hub must occur over an encrypted channel.</span></span>

### <a name="blacklisting-clients"></a><span data-ttu-id="e5277-152">Inscription des clients sur liste noire</span><span class="sxs-lookup"><span data-stu-id="e5277-152">Blacklisting clients</span></span>
<span data-ttu-id="e5277-153">Si un jeton est volé par une personne malveillante, hello peut emprunter l’identité client hello dont le jeton a été volé.</span><span class="sxs-lookup"><span data-stu-id="e5277-153">If a token is stolen by an attacker, hello attacker can impersonate hello client whose token has been stolen.</span></span> <span data-ttu-id="e5277-154">L’inscription d’un client sur liste noire le rend inutilisable, jusqu’à ce qu’il reçoive un nouveau jeton qui utilise un éditeur différent.</span><span class="sxs-lookup"><span data-stu-id="e5277-154">Blacklisting a client renders that client unusable until it receives a new token that uses a different publisher.</span></span>

## <a name="authentication-of-back-end-applications"></a><span data-ttu-id="e5277-155">Authentification des applications principales</span><span class="sxs-lookup"><span data-stu-id="e5277-155">Authentication of back-end applications</span></span>

<span data-ttu-id="e5277-156">applications principales tooauthenticate qui consomment des données hello générées par les clients de concentrateurs d’événements, le service Event Hubs utilise un modèle de sécurité qui est le modèle toohello similaire qui est utilisé pour les rubriques Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e5277-156">tooauthenticate back-end applications that consume hello data generated by Event Hubs clients, Event Hubs employs a security model that is similar toohello model that is used for Service Bus topics.</span></span> <span data-ttu-id="e5277-157">Un groupe de consommateurs de concentrateurs d’événements est tooa équivalente de la rubrique abonnement tooa Service Bus.</span><span class="sxs-lookup"><span data-stu-id="e5277-157">An Event Hubs consumer group is equivalent tooa subscription tooa Service Bus topic.</span></span> <span data-ttu-id="e5277-158">Un client peut créer un groupe de consommateurs si le groupe de consommateurs hello demande toocreate hello est accompagné d’un jeton que de gérer des privilèges pour le concentrateur d’événements hello ou pour toowhich d’espace de noms hello concentrateur d’événements hello appartient.</span><span class="sxs-lookup"><span data-stu-id="e5277-158">A client can create a consumer group if hello request toocreate hello consumer group is accompanied by a token that grants manage privileges for hello event hub, or for hello namespace toowhich hello event hub belongs.</span></span> <span data-ttu-id="e5277-159">Un client est autorisé à tooconsume des données à partir d’un groupe de consommateurs si la demande de réception hello sont accompagnées par un jeton qu’accorde des droits sur ce groupe de consommateurs de réception, hello concentrateur d’événements, ou le concentrateur d’événements hello espace de noms toowhich hello appartient.</span><span class="sxs-lookup"><span data-stu-id="e5277-159">A client is allowed tooconsume data from a consumer group if hello receive request is accompanied by a token that grants receive rights on that consumer group, hello event hub, or hello namespace toowhich hello event hub belongs.</span></span>

<span data-ttu-id="e5277-160">version actuelle de Hello du Bus de Service ne prend pas en charge les règles SAS pour les abonnements individuels.</span><span class="sxs-lookup"><span data-stu-id="e5277-160">hello current version of Service Bus does not support SAS rules for individual subscriptions.</span></span> <span data-ttu-id="e5277-161">Hello que va de même pour les groupes de consommateurs de concentrateurs d’événements.</span><span class="sxs-lookup"><span data-stu-id="e5277-161">hello same holds true for Event Hubs consumer groups.</span></span> <span data-ttu-id="e5277-162">Prise en charge SAS sera ajouté pour les deux fonctionnalités Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="e5277-162">SAS support will be added for both features in hello future.</span></span>

<span data-ttu-id="e5277-163">En absence de hello d’authentification SAP des groupes de consommateurs individuels, vous pouvez utiliser tous les groupes de consommateurs SAS clés toosecure avec une clé commune.</span><span class="sxs-lookup"><span data-stu-id="e5277-163">In hello absence of SAS authentication for individual consumer groups, you can use SAS keys toosecure all consumer groups with a common key.</span></span> <span data-ttu-id="e5277-164">Cette approche permet à une application tooconsume les données de groupes de consommateurs hello d’un concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="e5277-164">This approach enables an application tooconsume data from any of hello consumer groups of an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5277-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5277-165">Next steps</span></span>
<span data-ttu-id="e5277-166">toolearn en savoir plus sur les concentrateurs d’événements, consultez hello rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="e5277-166">toolearn more about Event Hubs, visit hello following topics:</span></span>

* <span data-ttu-id="e5277-167">[Vue d’ensemble des hubs d’événements]</span><span class="sxs-lookup"><span data-stu-id="e5277-167">[Event Hubs overview]</span></span>
* <span data-ttu-id="e5277-168">[Présentation des signatures d’accès partagé]</span><span class="sxs-lookup"><span data-stu-id="e5277-168">[Overview of Shared Access Signatures]</span></span>
* <span data-ttu-id="e5277-169">[Exemples d’applications qui utilisent des Event Hubs]</span><span class="sxs-lookup"><span data-stu-id="e5277-169">[Sample applications that use Event Hubs]</span></span>

[Vue d’ensemble des hubs d’événements]: event-hubs-what-is-event-hubs.md
[Exemples d’applications qui utilisent des Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Présentation des signatures d’accès partagé]: ../service-bus-messaging/service-bus-sas.md

