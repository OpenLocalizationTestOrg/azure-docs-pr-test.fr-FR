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
# <a name="relay-hybrid-connections-node-api-overview"></a>Vue d’ensemble des API de nœud pour les connexions hybrides Relay

## <a name="overview"></a>Vue d'ensemble

Hello [ `hyco-ws` ](https://www.npmjs.com/package/hyco-ws) package de nœud pour les connexions hybrides de relais Azure repose sur et étend hello ['ws'](https://www.npmjs.com/package/ws) package NPM. Ce package nouveau exporte toutes les exportations de ce package de base et ajoute de nouvelles exportations qui permettent l’intégration avec la fonctionnalité de connexions hybrides de service de relais d’Azure hello. 

Les applications existantes qui `require('ws')` pouvez utiliser ce package avec `require('hyco-ws')` au lieu de cela, ce qui permet également des scénarios hybrides dans lesquels une application peut écouter les connexions de WebSocket localement à partir de « à l’intérieur du pare-feu de hello » et via des connexions hybrides, tout à Hello même temps.
  
## <a name="documentation"></a>Documentation

Hello API sont [documentés dans le package du principal 'ws' hello](https://github.com/websockets/ws/blob/master/doc/ws.md). Cet article décrit en quoi ce package diffère du package de base. 

Bonjour principales différences entre le package de base hello et cette 'ws-hyco' est qu’il ajoute une nouvelle classe de serveur, exportée `require('hyco-ws').RelayedServer`et quelques méthodes d’assistance.

### <a name="package-helper-methods"></a>Méthodes d’assistance du package

Plusieurs méthodes d’utilitaire sont disponibles lors de l’exportation de package hello que vous pouvez le référencer comme suit :

```JavaScript
const WebSocket = require('hyco-ws');

var listenUri = WebSocket.createRelayListenUri('namespace.servicebus.windows.net', 'path');
listenUri = WebSocket.appendRelayToken(listenUri, 'ruleName', '...key...')
...

```

méthodes d’assistance de Hello sont utilisées avec ce package, mais peuvent également servir à un serveur de nœud pour l’activation des écouteurs de toocreate les clients web ou un appareil ou des expéditeurs. serveur de Hello utilise ces méthodes en les passant l’URI qui incorporent des jetons de courte durée de vie. Ces URI peut également être utilisé avec les piles de WebSocket communs qui ne prennent pas en charge les définir les en-têtes HTTP pour le protocole de transfert WebSocket hello. Incorporation des jetons d’autorisation dans hello QU'URI est pris en charge principalement pour ces scénarios d’utilisation de la bibliothèque externe. 

#### <a name="createrelaylistenuri"></a>createRelayListenUri

```JavaScript
var uri = createRelayListenUri([namespaceName], [path], [[token]], [[id]])
```

Crée un écouteur de la connexion hybride Azure relais URI valid pour hello donné l’espace de noms et le chemin d’accès. Cet URI peut ensuite être utilisé avec la version de relais hello Hello WebSocketServer classe.

- `namespaceName`(obligatoire) - hello nom qualifié de domaine de toouse d’espace de noms hello Azure relais.
- `path`(obligatoire) - hello nom d’une connexion hybride de relais Azure existante dans cet espace de noms.
- `token`(facultatif) : un accès de relais précédemment émis de jeton qui est incorporé dans l’écouteur hello URI (voir hello exemple suivant).
- `id` (facultatif) : identificateur de suivi qui permet un suivi des diagnostics de bout en bout des demandes.

Hello `token` valeur est facultative et ne doit être utilisée quand il n’est pas possible toosend HTTP des en-têtes, ainsi que le protocole de transfert WebSocket hello, comme dans les cas de hello avec la pile de W3C WebSocket hello.                  


#### <a name="createrelaysenduri"></a>createRelaySendUri
 
```JavaScript
var uri = createRelaySendUri([namespaceName], [path], [[token]], [[id]])
```

Crée un envoi de la connexion hybride Azure relais URI valid pour hello donné l’espace de noms et le chemin d’accès. Cet URI peut être utilisé avec un client WebSocket quel qu’il soit.

- `namespaceName`(obligatoire) - hello nom qualifié de domaine de toouse d’espace de noms hello Azure relais.
- `path`(obligatoire) - hello nom d’une connexion hybride de relais Azure existante dans cet espace de noms.
- `token`(facultatif) : un jeton d’accès précédemment émis relais qui est incorporé dans hello envoyer URI (voir hello exemple suivant).
- `id` (facultatif) : identificateur de suivi qui permet un suivi des diagnostics de bout en bout des demandes.

Hello `token` valeur est facultative et ne doit être utilisée quand il n’est pas possible toosend HTTP des en-têtes, ainsi que le protocole de transfert WebSocket hello, comme dans les cas de hello avec la pile de W3C WebSocket hello.                   


#### <a name="createrelaytoken"></a>createRelayToken 

```JavaScript
var token = createRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Crée un jeton d’Azure relais partagé Signature d’accès (SAP) pour URI cible de hello donné, SAP et clé de la règle SAS valide pour hello étant donné un nombre de secondes ou pendant une heure à partir de hello actuel instantanée si hello expiration argument est omis.

- `uri`(obligatoire) - hello URI pour le hello jeton est toobe émis. Hello URI est le schéma HTTP toouse normalisée hello et informations de chaîne de requête sont supprimées.
- `ruleName`(obligatoire) - nom de l’entité hello représentée par hello donné d’URI de règles SAS, ou pour hello espace de noms représenté par hello partie hôte de l’URI.
- `key`(obligatoire) - clé valide pour la règle SAS hello. 
- `expirationSeconds`(facultatif) : nombre hello de secondes jusqu'à ce que hello générée jeton doit expirer. Si non spécifié, par défaut de hello est 1 heure (3 600).

jeton de Hello émis confère des droits hello associés hello spécifié règle SAS pour hello étant donné la durée.

#### <a name="appendrelaytoken"></a>appendRelayToken

```JavaScript
var uri = appendRelayToken([uri], [ruleName], [key], [[expirationSeconds]])
```

Cette méthode est fonctionnellement équivalent toohello `createRelayToken` méthode décrites précédemment, mais retourne hello URI d’entrée correctement ajouté toohello jeton.

### <a name="class-wsrelayedserver"></a>Class ws.RelayedServer

Hello `hycows.RelayedServer` classe est une autre toohello `ws.Server` classe qui n’écoute pas sur le réseau local de hello, mais délègue écoute toohello service de relais d’Azure.

classes de Hello deux sont principalement les contrat compatible, ce qui signifie qu’une application existante à l’aide de hello `ws.Server` classe peut être facilement la version de hello relayée toouse modifiées. Hello principales différences résident dans le constructeur de hello et dans les options disponibles hello.

#### <a name="constructor"></a>Constructeur  

```JavaScript 
var ws = require('hyco-ws');
var server = ws.RelayedServer;

var wss = new server(
    {
        server: ws.createRelayListenUri(ns, path),
        token: function() { return ws.createRelayToken('http://' + ns, keyrule, key); }
    });
```

Hello `RelayedServer` constructeur prend en charge un ensemble différent d’arguments que hello `Server`, car il n’est pas un écouteur d’autonome ou en mesure de toobe incorporée dans une infrastructure d’écouteur HTTP existante. Il existe également moins d’options disponibles dans la mesure où hello gestion du WebSocket est en grande partie déléguée toohello service de relais.

Arguments du constructeur :

- `server`(obligatoire) - hello complet URI pour un nom de connexion hybride sur le toolisten, généralement construite avec la méthode d’assistance de WebSocket.createRelayListenUri() de hello.
- `token`(obligatoire) - cet argument conserve une chaîne de jeton émise précédemment ou une fonction de rappel qui peut être appelée tooobtain telle une chaîne de jeton. option de rappel Hello est recommandée, car elle permet de renouvellement de jeton.

#### <a name="events"></a>Événements

`RelayedServer`instances émettent trois événements qui permettent de vous toohandle les demandes entrantes, établissent des connexions et détectent des conditions d’erreur. Vous devez vous abonner toohello `connect` toohandle messages d’événement. 

##### <a name="headers"></a>headers

```JavaScript 
function(headers)
```

Hello `headers` événement est déclenché juste avant qu’une connexion entrante est acceptée, l’activation de la modification du client de toohello toosend hello en-têtes. 

##### <a name="connection"></a>connection

```JavaScript
function(socket)
```

Émis lorsqu’une nouvelle connexion WebSocket est acceptée. objet de Hello est de type `ws.WebSocket`, le même qu’avec le package de base hello.


##### <a name="error"></a>error

```JavaScript
function(error)
```

Si le serveur sous-jacent de hello émet une erreur, il est transféré ici.  

#### <a name="helpers"></a>Programmes d’assistance

toosimplify à partir d’un serveur relayé et immédiatement abonnement tooincoming connexions, hello package expose une fonction d’assistance simple, qui est également utilisée dans les exemples hello, comme suit :

##### <a name="createrelayedlistener"></a>createRelayedListener

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

##### <a name="createrelayedserver"></a>createRelayedServer

```javascript
var server = createRelayedServer([options], [connectCallback] )
```

Cette méthode appelle hello constructeur toocreate une nouvelle instance de hello RelayedServer et puis s’abonne événement de hello fourni rappel toohello « connexion ».
 
##### <a name="relayedconnect"></a>relayedConnect

Simplement la mise en miroir hello `createRelayedServer` helper dans la fonction, `relayedConnect` crée une connexion de client et s’abonne toohello les événements « ouvert » sur le socket résultant de hello.

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

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur Azure relais, consultez ces liens :
* [Qu’est-ce qu’Azure Relay ?](relay-what-is-it.md)
* [API Relay disponibles](relay-api-overview.md)
