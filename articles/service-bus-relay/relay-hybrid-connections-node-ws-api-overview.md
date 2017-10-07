---
title: "aaaOverview Hello API de nœud Azure relais | Documents Microsoft"
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
ms.openlocfilehash: d231acc854be0eaa965dec0229cf63b08ff27067
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="relay-hybrid-connections-node-api-overview"></a><span data-ttu-id="316b4-103">Vue d’ensemble des API de nœud pour les connexions hybrides Relay</span><span class="sxs-lookup"><span data-stu-id="316b4-103">Relay Hybrid Connections Node API overview</span></span>

## <a name="overview"></a><span data-ttu-id="316b4-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="316b4-104">Overview</span></span>

<span data-ttu-id="316b4-105">Hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) package de nœud pour les connexions hybrides de relais Azure repose sur et étend hello ['ws'](https://www.npmjs.com/package/ws) package NPM.</span><span class="sxs-lookup"><span data-stu-id="316b4-105">hello [`hyco-ws`](https://www.npmjs.com/package/hyco-ws) Node package for Azure Relay Hybrid Connections is built on and extends hello ['ws'](https://www.npmjs.com/package/ws) NPM package.</span></span> <span data-ttu-id="316b4-106">Ce package nouveau exporte toutes les exportations de ce package de base et ajoute de nouvelles exportations qui permettent l’intégration avec la fonctionnalité de connexions hybrides de service de relais d’Azure hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-106">This package re-exports all exports of that base package and adds new exports that enable integration with hello Azure Relay service Hybrid Connections feature.</span></span> 

<span data-ttu-id="316b4-107">Les applications existantes qui `require('ws')` pouvez utiliser ce package avec `require('hyco-ws')` au lieu de cela, ce qui permet également des scénarios hybrides dans lesquels une application peut écouter les connexions de WebSocket localement à partir de « à l’intérieur du pare-feu de hello » et via des connexions hybrides, tout à Hello même temps.</span><span class="sxs-lookup"><span data-stu-id="316b4-107">Existing applications that `require('ws')` can use this package with `require('hyco-ws')` instead, which also enables hybrid scenarios in which an application can listen for WebSocket connections locally from "inside hello firewall" and via Hybrid Connections, all at hello same time.</span></span>
  
## <a name="documentation"></a><span data-ttu-id="316b4-108">Documentation</span><span class="sxs-lookup"><span data-stu-id="316b4-108">Documentation</span></span>

<span data-ttu-id="316b4-109">Hello API sont [documentés dans le package du principal 'ws' hello](https://github.com/websockets/ws/blob/master/doc/ws.md).</span><span class="sxs-lookup"><span data-stu-id="316b4-109">hello APIs are [documented in hello main 'ws' package](https://github.com/websockets/ws/blob/master/doc/ws.md).</span></span> <span data-ttu-id="316b4-110">Cet article décrit en quoi ce package diffère du package de base.</span><span class="sxs-lookup"><span data-stu-id="316b4-110">This article describes how this package differs from that baseline.</span></span> 

<span data-ttu-id="316b4-111">Bonjour principales différences entre le package de base hello et cette 'ws-hyco' est qu’il ajoute une nouvelle classe de serveur, exportée `require('hyco-ws').RelayedServer`et quelques méthodes d’assistance.</span><span class="sxs-lookup"><span data-stu-id="316b4-111">hello key differences between hello base package and this 'hyco-ws' is that it adds a new server class, exported via `require('hyco-ws').RelayedServer`, and a few helper methods.</span></span>

### <a name="package-helper-methods"></a><span data-ttu-id="316b4-112">Méthodes d’assistance du package</span><span class="sxs-lookup"><span data-stu-id="316b4-112">Package helper methods</span></span>

<span data-ttu-id="316b4-113">Plusieurs méthodes d’utilitaire sont disponibles lors de l’exportation de package hello que vous pouvez le référencer comme suit :</span><span class="sxs-lookup"><span data-stu-id="316b4-113">There are several utility methods available on hello package export that you can reference as follows:</span></span>

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

<span data-ttu-id="316b4-114">méthodes d’assistance de Hello sont utilisées avec ce package, mais peuvent également servir à un serveur de nœud pour l’activation des écouteurs de toocreate les clients web ou un appareil ou des expéditeurs.</span><span class="sxs-lookup"><span data-stu-id="316b4-114">hello helper methods are for use with this package, but can also be used by a Node server for enabling web or device clients toocreate listeners or senders.</span></span> <span data-ttu-id="316b4-115">serveur de Hello utilise ces méthodes en les passant l’URI qui incorporent des jetons de courte durée de vie.</span><span class="sxs-lookup"><span data-stu-id="316b4-115">hello server uses these methods by passing them URIs that embed short-lived tokens.</span></span> <span data-ttu-id="316b4-116">Ces URI peut également être utilisé avec les piles de WebSocket communs qui ne prennent pas en charge les définir les en-têtes HTTP pour le protocole de transfert WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-116">These URIs can also be used with common WebSocket stacks that do not support setting HTTP headers for hello WebSocket handshake.</span></span> <span data-ttu-id="316b4-117">Incorporation des jetons d’autorisation dans hello QU'URI est pris en charge principalement pour ces scénarios d’utilisation de la bibliothèque externe.</span><span class="sxs-lookup"><span data-stu-id="316b4-117">Embedding authorization tokens into hello URI is supported primarily for those library-external usage scenarios.</span></span> 

#### <a name="createrelaylistenuri"></a><span data-ttu-id="316b4-118">createRelayListenUri</span><span class="sxs-lookup"><span data-stu-id="316b4-118">createRelayListenUri</span></span>

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="316b4-119">Crée un écouteur de la connexion hybride Azure relais URI valid pour hello donné l’espace de noms et le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="316b4-119">Creates a valid Azure Relay Hybrid Connection listener URI for hello given namespace and path.</span></span> <span data-ttu-id="316b4-120">Cet URI peut ensuite être utilisé avec la version de relais hello Hello WebSocketServer classe.</span><span class="sxs-lookup"><span data-stu-id="316b4-120">This URI can then be used with hello relay version of hello WebSocketServer class.</span></span>

- <span data-ttu-id="316b4-121">`namespaceName`(obligatoire) - hello nom qualifié de domaine de toouse d’espace de noms hello Azure relais.</span><span class="sxs-lookup"><span data-stu-id="316b4-121">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="316b4-122">`path`(obligatoire) - hello nom d’une connexion hybride de relais Azure existante dans cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="316b4-122">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="316b4-123">`token`(facultatif) : un accès de relais précédemment émis de jeton qui est incorporé dans l’écouteur hello URI (voir hello exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="316b4-123">`token` (optional) - a previously issued Relay access token that is embedded in hello listener URI (see hello following example).</span></span>
- <span data-ttu-id="316b4-124">`id` (facultatif) : identificateur de suivi qui permet un suivi des diagnostics de bout en bout des demandes.</span><span class="sxs-lookup"><span data-stu-id="316b4-124">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="316b4-125">Hello `token` valeur est facultative et ne doit être utilisée quand il n’est pas possible toosend HTTP des en-têtes, ainsi que le protocole de transfert WebSocket hello, comme dans les cas de hello avec la pile de W3C WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-125">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                  


#### <a name="createrelaysenduri"></a><span data-ttu-id="316b4-126">createRelaySendUri</span><span class="sxs-lookup"><span data-stu-id="316b4-126">createRelaySendUri</span></span>
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

<span data-ttu-id="316b4-127">Crée un envoi de la connexion hybride Azure relais URI valid pour hello donné l’espace de noms et le chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="316b4-127">Creates a valid Azure Relay Hybrid Connection send URI for hello given namespace and path.</span></span> <span data-ttu-id="316b4-128">Cet URI peut être utilisé avec un client WebSocket quel qu’il soit.</span><span class="sxs-lookup"><span data-stu-id="316b4-128">This URI can be used with any WebSocket client.</span></span>

- <span data-ttu-id="316b4-129">`namespaceName`(obligatoire) - hello nom qualifié de domaine de toouse d’espace de noms hello Azure relais.</span><span class="sxs-lookup"><span data-stu-id="316b4-129">`namespaceName` (required) - hello domain-qualified name of hello Azure Relay namespace toouse.</span></span>
- <span data-ttu-id="316b4-130">`path`(obligatoire) - hello nom d’une connexion hybride de relais Azure existante dans cet espace de noms.</span><span class="sxs-lookup"><span data-stu-id="316b4-130">`path` (required) - hello name of an existing Azure Relay Hybrid Connection in that namespace.</span></span>
- <span data-ttu-id="316b4-131">`token`(facultatif) : un jeton d’accès précédemment émis relais qui est incorporé dans hello envoyer URI (voir hello exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="316b4-131">`token` (optional) - a previously issued Relay access token that is embedded in hello send URI (see hello following example).</span></span>
- <span data-ttu-id="316b4-132">`id` (facultatif) : identificateur de suivi qui permet un suivi des diagnostics de bout en bout des demandes.</span><span class="sxs-lookup"><span data-stu-id="316b4-132">`id` (optional) - a tracking identifier that enables end-to-end diagnostics tracking of requests.</span></span>

<span data-ttu-id="316b4-133">Hello `token` valeur est facultative et ne doit être utilisée quand il n’est pas possible toosend HTTP des en-têtes, ainsi que le protocole de transfert WebSocket hello, comme dans les cas de hello avec la pile de W3C WebSocket hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-133">hello `token` value is optional and should only be used when it is not possible toosend HTTP headers along with hello WebSocket handshake, as is hello case with hello W3C WebSocket stack.</span></span>                   


#### <a name="createrelaytoken"></a><span data-ttu-id="316b4-134">createRelayToken</span><span class="sxs-lookup"><span data-stu-id="316b4-134">createRelayToken</span></span> 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="316b4-135">Crée un jeton d’Azure relais partagé Signature d’accès (SAP) pour URI cible de hello donné, SAP et clé de la règle SAS valide pour hello étant donné un nombre de secondes ou pendant une heure à partir de hello actuel instantanée si hello expiration argument est omis.</span><span class="sxs-lookup"><span data-stu-id="316b4-135">Creates an Azure Relay Shared Access Signature (SAS) token for hello given target URI, SAS rule, and SAS rule key that is valid for hello given number of seconds or for an hour from hello current instant if hello expiry argument is omitted.</span></span>

- <span data-ttu-id="316b4-136">`uri`(obligatoire) - hello URI pour le hello jeton est toobe émis.</span><span class="sxs-lookup"><span data-stu-id="316b4-136">`uri` (required) - hello URI for which hello token is toobe issued.</span></span> <span data-ttu-id="316b4-137">Hello URI est le schéma HTTP toouse normalisée hello et informations de chaîne de requête sont supprimées.</span><span class="sxs-lookup"><span data-stu-id="316b4-137">hello URI is normalized toouse hello HTTP scheme, and query string information is stripped.</span></span>
- <span data-ttu-id="316b4-138">`ruleName`(obligatoire) - nom de l’entité hello représentée par hello donné d’URI de règles SAS, ou pour hello espace de noms représenté par hello partie hôte de l’URI.</span><span class="sxs-lookup"><span data-stu-id="316b4-138">`ruleName` (required) - SAS rule name for either hello entity represented by hello given URI, or for hello namespace represented by hello URI host portion.</span></span>
- <span data-ttu-id="316b4-139">`key`(obligatoire) - clé valide pour la règle SAS hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-139">`key` (required) - valid key for hello SAS rule.</span></span> 
- <span data-ttu-id="316b4-140">`expirationSeconds`(facultatif) : nombre hello de secondes jusqu'à ce que hello générée jeton doit expirer.</span><span class="sxs-lookup"><span data-stu-id="316b4-140">`expirationSeconds` (optional) - hello number of seconds until hello generated token should expire.</span></span> <span data-ttu-id="316b4-141">Si non spécifié, par défaut de hello est 1 heure (3 600).</span><span class="sxs-lookup"><span data-stu-id="316b4-141">If not specified, hello default is 1 hour (3600).</span></span>

<span data-ttu-id="316b4-142">jeton de Hello émis confère des droits hello associés hello spécifié règle SAS pour hello étant donné la durée.</span><span class="sxs-lookup"><span data-stu-id="316b4-142">hello issued token confers hello rights associated with hello specified SAS rule for hello given duration.</span></span>

#### <a name="appendrelaytoken"></a><span data-ttu-id="316b4-143">appendRelayToken</span><span class="sxs-lookup"><span data-stu-id="316b4-143">appendRelayToken</span></span>

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

<span data-ttu-id="316b4-144">Cette méthode est fonctionnellement équivalent toohello `createRelayToken` méthode décrites précédemment, mais retourne hello URI d’entrée correctement ajouté toohello jeton.</span><span class="sxs-lookup"><span data-stu-id="316b4-144">This method is functionally equivalent toohello `createRelayToken` method documented previously, but returns hello token correctly appended toohello input URI.</span></span>

### <a name="class-wsrelayedserver"></a><span data-ttu-id="316b4-145">Class ws.RelayedServer</span><span class="sxs-lookup"><span data-stu-id="316b4-145">Class ws.RelayedServer</span></span>

<span data-ttu-id="316b4-146">Hello `hycows.RelayedServer` classe est une autre toohello `ws.Server` classe qui n’écoute pas sur le réseau local de hello, mais délègue écoute toohello service de relais d’Azure.</span><span class="sxs-lookup"><span data-stu-id="316b4-146">hello `hycows.RelayedServer` class is an alternative toohello `ws.Server` class that does not listen on hello local network, but delegates listening toohello Azure Relay service.</span></span>

<span data-ttu-id="316b4-147">classes de Hello deux sont principalement les contrat compatible, ce qui signifie qu’une application existante à l’aide de hello `ws.Server` classe peut être facilement la version de hello relayée toouse modifiées.</span><span class="sxs-lookup"><span data-stu-id="316b4-147">hello two classes are mostly contract compatible, meaning that an existing application using hello `ws.Server` class can easily be changed toouse hello relayed version.</span></span> <span data-ttu-id="316b4-148">Hello principales différences résident dans le constructeur de hello et dans les options disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-148">hello main differences are in hello constructor and in hello available options.</span></span>

#### <a name="constructor"></a><span data-ttu-id="316b4-149">Constructeur</span><span class="sxs-lookup"><span data-stu-id="316b4-149">Constructor</span></span>  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

<span data-ttu-id="316b4-150">Hello `RelayedServer` constructeur prend en charge un ensemble différent d’arguments que hello `Server`, car il n’est pas un écouteur d’autonome ou en mesure de toobe incorporée dans une infrastructure d’écouteur HTTP existante.</span><span class="sxs-lookup"><span data-stu-id="316b4-150">hello `RelayedServer` constructor supports a different set of arguments than hello `Server`, because it is not a standalone listener, or able toobe embedded into an existing HTTP listener framework.</span></span> <span data-ttu-id="316b4-151">Il existe également moins d’options disponibles dans la mesure où hello gestion du WebSocket est en grande partie déléguée toohello service de relais.</span><span class="sxs-lookup"><span data-stu-id="316b4-151">There are also fewer options available since hello WebSocket management is largely delegated toohello Relay service.</span></span>

<span data-ttu-id="316b4-152">Arguments du constructeur :</span><span class="sxs-lookup"><span data-stu-id="316b4-152">Constructor arguments:</span></span>

- <span data-ttu-id="316b4-153">`server`(obligatoire) - hello complet URI pour un nom de connexion hybride sur le toolisten, généralement construite avec la méthode d’assistance de WebSocket.createRelayListenUri() de hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-153">`server` (required) - hello fully qualified URI for a Hybrid Connection name on which toolisten, usually constructed with hello WebSocket.createRelayListenUri() helper method.</span></span>
- <span data-ttu-id="316b4-154">`token`(obligatoire) - cet argument conserve une chaîne de jeton émise précédemment ou une fonction de rappel qui peut être appelée tooobtain telle une chaîne de jeton.</span><span class="sxs-lookup"><span data-stu-id="316b4-154">`token` (required) - this argument holds either a previously issued token string or a callback function that can be called tooobtain such a token string.</span></span> <span data-ttu-id="316b4-155">option de rappel Hello est recommandée, car elle permet de renouvellement de jeton.</span><span class="sxs-lookup"><span data-stu-id="316b4-155">hello callback option is preferred, as it enables token renewal.</span></span>

#### <a name="events"></a><span data-ttu-id="316b4-156">Événements</span><span class="sxs-lookup"><span data-stu-id="316b4-156">Events</span></span>

<span data-ttu-id="316b4-157">`RelayedServer`instances émettent trois événements qui permettent de vous toohandle les demandes entrantes, établissent des connexions et détectent des conditions d’erreur.</span><span class="sxs-lookup"><span data-stu-id="316b4-157">`RelayedServer` instances emit three events that enable you toohandle incoming requests, establish connections, and detect error conditions.</span></span> <span data-ttu-id="316b4-158">Vous devez vous abonner toohello `connect` toohandle messages d’événement.</span><span class="sxs-lookup"><span data-stu-id="316b4-158">You must subscribe toohello `connect` event toohandle messages.</span></span> 

##### <a name="headers"></a><span data-ttu-id="316b4-159">headers</span><span class="sxs-lookup"><span data-stu-id="316b4-159">headers</span></span>

```JavaScript 
function(headers)
```

<span data-ttu-id="316b4-160">Hello `headers` événement est déclenché juste avant qu’une connexion entrante est acceptée, l’activation de la modification du client de toohello toosend hello en-têtes.</span><span class="sxs-lookup"><span data-stu-id="316b4-160">hello `headers` event is raised just before an incoming connection is accepted, enabling modification of hello headers toosend toohello client.</span></span> 

##### <a name="connection"></a><span data-ttu-id="316b4-161">connection</span><span class="sxs-lookup"><span data-stu-id="316b4-161">connection</span></span>

```JavaScript
function(socket)
```

<span data-ttu-id="316b4-162">Émis lorsqu’une nouvelle connexion WebSocket est acceptée.</span><span class="sxs-lookup"><span data-stu-id="316b4-162">Emitted when a new WebSocket connection is accepted.</span></span> <span data-ttu-id="316b4-163">objet de Hello est de type `ws.WebSocket`, le même qu’avec le package de base hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-163">hello object is of type `ws.WebSocket`, same as with hello base package.</span></span>


##### <a name="error"></a><span data-ttu-id="316b4-164">error</span><span class="sxs-lookup"><span data-stu-id="316b4-164">error</span></span>

```JavaScript
function(error)
```

<span data-ttu-id="316b4-165">Si le serveur sous-jacent de hello émet une erreur, il est transféré ici.</span><span class="sxs-lookup"><span data-stu-id="316b4-165">If hello underlying server emits an error, it is forwarded here.</span></span>  

#### <a name="helpers"></a><span data-ttu-id="316b4-166">Programmes d’assistance</span><span class="sxs-lookup"><span data-stu-id="316b4-166">Helpers</span></span>

<span data-ttu-id="316b4-167">toosimplify à partir d’un serveur relayé et immédiatement abonnement tooincoming connexions, hello package expose une fonction d’assistance simple, qui est également utilisée dans les exemples hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="316b4-167">toosimplify starting a relayed server and immediately subscribing tooincoming connections, hello package exposes a simple helper function, which is also used in hello examples, as follows:</span></span>

##### <a name="createrelayedlistener"></a><span data-ttu-id="316b4-168">createRelayedListener</span><span class="sxs-lookup"><span data-stu-id="316b4-168">createRelayedListener</span></span>

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

##### <a name="createrelayedserver"></a><span data-ttu-id="316b4-169">createRelayedServer</span><span class="sxs-lookup"><span data-stu-id="316b4-169">createRelayedServer</span></span>

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

<span data-ttu-id="316b4-170">Cette méthode appelle hello constructeur toocreate une nouvelle instance de hello RelayedServer et puis s’abonne événement de hello fourni rappel toohello « connexion ».</span><span class="sxs-lookup"><span data-stu-id="316b4-170">This method calls hello constructor toocreate a new instance of hello RelayedServer and then subscribes hello provided callback toohello 'connection' event.</span></span>
 
##### <a name="relayedconnect"></a><span data-ttu-id="316b4-171">relayedConnect</span><span class="sxs-lookup"><span data-stu-id="316b4-171">relayedConnect</span></span>

<span data-ttu-id="316b4-172">Simplement la mise en miroir hello `createRelayedServer` helper dans la fonction, `relayedConnect` crée une connexion de client et s’abonne toohello les événements « ouvert » sur le socket résultant de hello.</span><span class="sxs-lookup"><span data-stu-id="316b4-172">Simply mirroring hello `createRelayedServer` helper in function, `relayedConnect` creates a client connection and subscribes toohello 'open' event on hello resulting socket.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="316b4-173">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="316b4-173">Next steps</span></span>
<span data-ttu-id="316b4-174">toolearn en savoir plus sur Azure relais, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="316b4-174">toolearn more about Azure Relay, visit these links:</span></span>
* [<span data-ttu-id="316b4-175">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="316b4-175">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="316b4-176">API Relay disponibles</span><span class="sxs-lookup"><span data-stu-id="316b4-176">Available Relay APIs</span></span>](relay-api-overview.md)
