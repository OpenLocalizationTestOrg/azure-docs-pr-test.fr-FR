---
title: "Vue d’ensemble des API de nœud Azure Relay | Microsoft Docs"
description: "Vue d’ensemble des API de nœud Relay"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b7d6e822-7c32-4cb5-a4b8-df7d009bdc85
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 28526c05c7f364f0fcaaa362fc97857f850040ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="dd7ae-103">Vue d’ensemble des API de nœud pour les connexions hybrides Relay</span><span class="sxs-lookup"><span data-stu-id="dd7ae-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="dd7ae-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dd7ae-104">Overview</span></span>

<span data-ttu-id="dd7ae-105">Le package de nœud [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) pour les connexions hybrides Azure Relay repose sur le package NPM [« ws »](https://www.npmjs.com/package/ws) ainsi qu’il l’étend.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-105">The [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends the ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="dd7ae-106">Ce package réexporte toutes les exportations du package de base et ajoute de nouvelles exportations qui permettent l’intégration avec la fonctionnalité de connexions hybrides du service Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-106">This package re-exports all exports of that base package and adds new exports that enable integration with the Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="dd7ae-107">Les applications existantes de type `require('ws')` peuvent également utiliser ce package avec `require('hyco-ws')`. Cela permet des scénarios hybrides dans lesquels une application écoute les connexions WebSocket en local depuis « l’intérieur du pare-feu » en même temps que via des connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside the firewall" and via Hybrid Connections, all at the same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="dd7ae-108">Documentation</span><span class="sxs-lookup"><span data-stu-id="dd7ae-108">Documentation</span></span>

<span data-ttu-id="dd7ae-109">Les API sont [documentées dans le package principal « ws »](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="dd7ae-109">The APIs are [documented in the main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="dd7ae-110">Cet article décrit en quoi ce package diffère du package de base.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="dd7ae-111">Les principales différences entre le package de base et le package « hyco-ws » sont qu’il ajoute quelques méthodes d’assistance et une nouvelle classe de serveur laquelle est exportée via `require('hyco-ws').RelayedServer`.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-111">The key differences between the base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="dd7ae-112">Méthodes d’assistance du package</span><span class="sxs-lookup"><span data-stu-id="dd7ae-112">Package helper methods</span></span>

<span data-ttu-id="dd7ae-113">Plusieurs méthodes utilitaires sont disponibles dans l’exportation du package. Vous pouvez les référencer comme suit :</span><span class="sxs-lookup"><span data-stu-id="dd7ae-113">There are several utility methods available on the package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="dd7ae-114">Ces méthodes d’assistance doivent être utilisées avec ce package. Toutefois, elles peuvent également être utilisées par un serveur de nœud pour l’activation de clients web ou de périphérique et la création d’écouteurs ou d’expéditeurs.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-114">The helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients to create listeners or senders.</span></span> <span data-ttu-id="dd7ae-115">Le serveur utilise ces méthodes en leur transférant des URI qui intègrent des jetons de durée de vie limitée.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-115">The server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="dd7ae-116">Ces URI peuvent également être utilisés avec des piles WebSocket courantes qui ne prennent pas en charge la définition d’en-têtes HTTP pour le protocole de transfert WebSocket.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for the WebSocket handshake.</span></span> <span data-ttu-id="dd7ae-117">L’intégration de jetons d’autorisation dans l’URI est principalement prise en charge pour les scénarios d’utilisation externes à la bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-117">Embedding authorization tokens into the URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="dd7ae-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="dd7ae-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="dd7ae-119">Crée un URI d’écouteur de connexion hybride Azure Relay valide pour l’espace de noms et le chemin d’accès indiqués.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-119">Creates a valid Azure Relay Hybrid Connection listener URI for the given namespace and path.</span></span> <span data-ttu-id="dd7ae-120">Cet URI peut ensuite être utilisé avec la version Relay de la classe WebSocketServer.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-120">This URI can then be used with the relay version of the WebSocketServer class.</span></span>

- <span data-ttu-id="dd7ae-121">`namespaceName` (obligatoire) : nom de domaine qualifié de l’espace de noms Azure Relay à utiliser.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-121">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="dd7ae-122">`path` (obligatoire) : nom d’une connexion hybride Azure Relay existante dans cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-122">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="dd7ae-123">`token` (facultatif) : jeton d’accès Azure Relay précédemment publié et intégré à l’URI d’écouteur (voir l’exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="dd7ae-123">`token` (optional) - a previously issued Relay access token that is embedded in the listener URI (see the following example).</span></span>
- <span data-ttu-id="dd7ae-124">`id` (facultatif) : identificateur de suivi qui permet un suivi des diagnostics de bout en bout des demandes.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="dd7ae-125">La valeur `token` est facultative et doit être utilisée uniquement quand il est impossible d’envoyer des en-têtes HTTP avec le protocole de transfert WebSocket, comme c’est le cas avec la pile W3C WebSocket.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-125">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="dd7ae-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="dd7ae-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="dd7ae-127">Crée un URI d’envoi de connexion hybride Azure Relay valide pour l’espace de noms et le chemin d’accès indiqués.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-127">Creates a valid Azure Relay Hybrid Connection send URI for the given namespace and path.</span></span> <span data-ttu-id="dd7ae-128">Cet URI peut être utilisé avec un client WebSocket quel qu’il soit.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="dd7ae-129">`namespaceName` (obligatoire) : nom de domaine qualifié de l’espace de noms Azure Relay à utiliser.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-129">`namespaceName` (required) - the domain-qualified name of the Azure Relay namespace to use.</span></span>
- <span data-ttu-id="dd7ae-130">`path` (obligatoire) : nom d’une connexion hybride Azure Relay existante dans cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-130">`path` (required) - the name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="dd7ae-131">`token` (facultatif) : jeton d’accès Azure Relay précédemment publié et intégré à l’URI d’envoi (voir l’exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="dd7ae-131">`token` (optional) - a previously issued Relay access token that is embedded in the send URI (see the following example).</span></span>
- <span data-ttu-id="dd7ae-132">`id` (facultatif) : identificateur de suivi qui permet un suivi des diagnostics de bout en bout des demandes.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="dd7ae-133">La valeur `token` est facultative et doit être utilisée uniquement quand il est impossible d’envoyer des en-têtes HTTP avec le protocole de transfert WebSocket, comme c’est le cas avec la pile W3C WebSocket.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-133">The `token` value is optional and should only be used when it is not possible to send HTTP headers along with the WebSocket handshake, as is the case with the W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="dd7ae-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="dd7ae-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="dd7ae-135">Crée un jeton de signature d’accès partagé Azure Relay pour l’URI cible, la règle de signature d’accès partagé et la clé de règle de signature d’accès partagé indiqués. Ce jeton est valide pendant le nombre de secondes mentionné ou pendant une heure à partir de l’instant présent si l’argument d’expiration est omis.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-135">Creates an Azure Relay Shared Access Signature (SAS) token for the given target URI, SAS rule, and SAS rule key that is valid for the given number of seconds or for an hour from the current instant if the expiry argument is omitted.</span></span>

- <span data-ttu-id="dd7ae-136">`uri` (obligatoire) : URI pour lequel le jeton doit être émis.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-136">`uri` (required) - the URI for which the token is to be issued.</span></span> <span data-ttu-id="dd7ae-137">L’URI est normalisé et utilise le schéma HTTP. Les informations de chaîne de requête sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-137">The URI is normalized to use the HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="dd7ae-138">`ruleName` (obligatoire) : nom de règle SAS pour l’entité représentée par l’URI indiqué ou pour l’espace de noms représenté par la portion d’hôte URI.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-138">`ruleName` (required) - SAS rule name for either the entity represented by the given URI, or for the namespace represented by the URI host portion.</span></span>
- <span data-ttu-id="dd7ae-139">`key` (obligatoire) : clé valide pour la règle de signature d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-139">`key` (required) - valid key for the SAS rule.</span></span> 
- <span data-ttu-id="dd7ae-140">`expirationSeconds` (facultatif) : nombre de secondes avant expiration du jeton généré.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-140">`expirationSeconds` (optional) - the number of seconds until the generated token should expire.</span></span> <span data-ttu-id="dd7ae-141">Si aucune valeur n’est indiquée, la valeur par défaut est 1 heure (3600).</span><span class="sxs-lookup"><span data-stu-id="dd7ae-141">If not specified, the default is 1 hour (3600).</span></span>

<span data-ttu-id="dd7ae-142">Le jeton émis confère les droits associés à la règle SAS indiquée pour la durée définie.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-142">The issued token confers the rights associated with the specified SAS rule for the given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="dd7ae-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="dd7ae-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="dd7ae-144">Fonctionnellement parlant, cette méthode équivaut à la méthode `createRelayToken` décrite précédemment, à ceci près qu’elle renvoie le jeton après l’avoir ajouté à l’URI d’entrée.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-144">This method is functionally equivalent to the `createRelayToken` method documented previously, but returns the token correctly appended to the input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="dd7ae-145">Class ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="dd7ae-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="dd7ae-146">La classe `hycows.RelayedServer` constitue une alternative à la classe `ws.Server` qui n’écoute pas sur le réseau local, mais délègue l’écoute au service Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-146">The `hycows.RelayedServer` class is an alternative to the `ws.Server` class that does not listen on the local network, but delegates listening to the Azure Relay service.</span></span>

<span data-ttu-id="dd7ae-147">Ces deux classes sont en grande partie compatibles, en ce sens qu’une application existante qui utilise la classe `ws.Server` peut facilement être modifiée pour utiliser la version relayée.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-147">The two classes are mostly contract compatible, meaning that an existing application using the `ws.Server` class can easily be changed to use the relayed version.</span></span> <span data-ttu-id="dd7ae-148">Les principales différences résident dans le constructeur et dans les options disponibles.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-148">The main differences are in the constructor and in the available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="dd7ae-149">Constructeur</span><span class="sxs-lookup"><span data-stu-id="dd7ae-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="dd7ae-150">Le constructeur `RelayedServer` ne prend pas en charge les mêmes arguments que le constructeur `Server`, car il n’est ni un écouteur autonome ni intégrable dans une infrastructure d’écouteur HTTP existante.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-150">The `RelayedServer` constructor supports a different set of arguments than the `Server`, because it is not a standalone listener, or able to be embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="dd7ae-151">Il existe également moins d’options disponibles dans la mesure où la gestion WebSocket est en grande partie déléguée au service Relay.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-151">There are also fewer options available since the WebSocket management is largely delegated to the Relay service.</span></span>

<span data-ttu-id="dd7ae-152">Arguments du constructeur :</span><span class="sxs-lookup"><span data-stu-id="dd7ae-152">Constructor arguments:</span></span>

- <span data-ttu-id="dd7ae-153">`server` (obligatoire) : URI complet d’un nom de connexion hybride sur lequel écouter et habituellement construit avec la méthode d’assistance WebSocket.createRelayListenUri().</span><span class="sxs-lookup"><span data-stu-id="dd7ae-153">`server` (required) - the fully qualified URI for a Hybrid Connection name on which to listen, usually constructed with the WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="dd7ae-154">`token` (obligatoire) : cet argument conserve une chaîne de jeton précédemment émise ou une fonction de rappel qui peut être appelée pour obtenir une telle chaîne de jeton.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called to obtain such a token string.</span></span> <span data-ttu-id="dd7ae-155">L’option de rappel est recommandée, car elle permet un renouvellement des jetons.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-155">The callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="dd7ae-156">Événements</span><span class="sxs-lookup"><span data-stu-id="dd7ae-156">Events</span></span>

<span data-ttu-id="dd7ae-157">Les instances `RelayedServer` émettent trois événements qui vous permettent de gérer les demandes entrantes, d’établir des connexions et de détecter les conditions d’erreur.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-157">`RelayedServer` instances emit three events that enable you to handle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="dd7ae-158">Vous devez vous abonner à l’événement `connect` pour traiter les messages.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-158">You must subscribe to the `connect` event to handle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="dd7ae-159">headers</span><span class="sxs-lookup"><span data-stu-id="dd7ae-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="dd7ae-160">L’événement `headers` est déclenché juste avant l’acceptation d’une connexion entrante, ce qui permet de modifier les en-têtes à envoyer au client.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-160">The `headers` event is raised just before an incoming connection is accepted, enabling modification of the headers to send to the client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="dd7ae-161">connection</span><span class="sxs-lookup"><span data-stu-id="dd7ae-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="dd7ae-162">Émis lorsqu’une nouvelle connexion WebSocket est acceptée.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="dd7ae-163">L’objet est de type `ws.WebSocket`, tout comme avec le package de base.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-163">The object is of type `ws.WebSocket`, same as with the base package.</span></span>


##### <a name="error"></a><span data-ttu-id="dd7ae-164">error</span><span class="sxs-lookup"><span data-stu-id="dd7ae-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="dd7ae-165">Si le serveur sous-jacent émet une erreur, il est transféré ici.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-165">If the underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="dd7ae-166">Programmes d’assistance</span><span class="sxs-lookup"><span data-stu-id="dd7ae-166">Helpers</span></span>

<span data-ttu-id="dd7ae-167">Pour simplifier le démarrage d’un serveur relayé et l’abonnement aux connexions entrantes, le package expose une fonction d’assistance simple, qui est également utilisée dans les exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="dd7ae-167">To simplify starting a relayed server and immediately subscribing to incoming connections, the package exposes a simple helper function, which is also used in the examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="dd7ae-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="dd7ae-168">createRelayedListener</span></span>

```JavaScript
var WebSocket = require('hyco-ws');

var wss = WebSocket.createRelayedServer(
    {
        server: WebSocket.createRelayListenUri(ns, path),
        token: function() { return WebSocket.createRelayToken('http://' + ns, keyrule, key); }
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(JSON.parse(event.data));
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
});
``` 

##### <a name="createrelayedserver"></a><span data-ttu-id="dd7ae-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="dd7ae-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="dd7ae-170">Cette méthode appelle le constructeur pour créer une nouvelle instance RelayedServer, puis abonne le rappel fourni à l’événement de « connexion ».</span><span class="sxs-lookup"><span data-stu-id="dd7ae-170">This method calls the constructor to create a new instance of the RelayedServer and then subscribes the provided callback to the 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="dd7ae-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="dd7ae-171">relayedConnect</span></span>

<span data-ttu-id="dd7ae-172">Par une mise en miroir du programme d’assistance `createRelayedServer` en fonction, `relayedConnect` crée une connexion client, puis s’abonne à l’événement d’« ouverture » sur le socket correspondant.</span><span class="sxs-lookup"><span data-stu-id="dd7ae-172">Simply mirroring the `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes to the 'open' event on the resulting socket.</span></span>

```JavaScript
var uri = WebSocket.createRelaySendUri(ns, path);
WebSocket.relayedConnect(
    uri,
    WebSocket.createRelayToken(uri, keyrule, key),
    function (socket) {
        ...
    }
);
```

## <a name="next-steps"></a><span data-ttu-id="dd7ae-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dd7ae-173">Next steps</span></span>
<span data-ttu-id="dd7ae-174">Pour en savoir plus sur Azure Relay, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="dd7ae-174">To learn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="dd7ae-175">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="dd7ae-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="dd7ae-176">API Relay disponibles</span><span class="sxs-lookup"><span data-stu-id="dd7ae-176">Available Relay APIs</span></span>](relay-api-overview.md)
