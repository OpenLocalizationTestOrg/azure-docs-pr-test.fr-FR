---
title: aaaOverview Hello Azure relais .NET Standard API | Documents Microsoft
description: "Vue d’ensemble des API .NET standard Relay"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b1da9ac1-811b-4df7-a22c-ccd013405c40
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: c90e00e809bd44eb0fbbff5eb03dfc8afa486523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a>Présentation des API .NET standard pour les connexions hybrides Azure Relay

Cet article récapitule certaines des clé hello Azure relais hybride connexions .NET Standard [API clientes](/dotnet/api/microsoft.azure.relay).
  
## <a name="relay-connection-string-builder"></a>Générateur de chaînes de connexion Relay

Hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] classe met en forme des chaînes de connexion qui sont des connexions hybrides tooRelay spécifique. Vous pouvez l’utiliser format de hello tooverify de chaîne de connexion, ou toobuild une chaîne de connexion à partir de zéro. Hello après pour obtenir un exemple de code, consultez :

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of hello Hybrid Connection}";
var sharedAccessKeyName = "{SAS key name}";
var sharedAccessKey = "{SAS key value}";

var connectionStringBuilder = new RelayConnectionStringBuilder()
{
    Endpoint = endpoint,
    EntityPath = entityPath,
    SharedAccessKeyName = sasKeyName,
    SharedAccessKey = sasKeyValue
};
```

Vous pouvez également passer une connexion de chaîne directement toohello `RelayConnectionStringBuilder` (méthode). Cette opération vous permet de tooverify chaîne de connexion hello est dans un format valide. Si un des paramètres de hello ne sont pas valide, le constructeur de hello génère une `ArgumentException`.

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare hello connectionStringBuilder so that it can be used outside of hello loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create hello connectionStringBuilder using hello supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a>Flux de connexion hybride
Hello [HybridConnectionStream] [ HCStream] classe est toosend d’objet principal utilisé hello et recevoir des données à partir d’un point de terminaison de relais d’Azure, si vous travaillez avec un [HybridConnectionClient] [ HCClient], ou un [HybridConnectionListener][HCListener].

### <a name="getting-a-hybrid-connection-stream"></a>Obtention d’un flux de connexion hybride

#### <a name="listener"></a>Écouteur
À l’aide d’un [HybridConnectionListener][HCListener], vous pouvez obtenir un objet `HybridConnectionStream` comme suit :

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a>Client
À l’aide d’un [HybridConnectionClient][HCClient], vous pouvez obtenir un objet `HybridConnectionStream` comme suit :

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a>Réception de données
Hello [HybridConnectionStream] [ HCStream] classe permet la communication bidirectionnelle. Dans la plupart des cas, vous recevez en continu à partir de flux de données hello. Si vous lisez le texte à partir de flux de hello, vous pouvez également toouse une [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) objet, ce qui simplifie l’analyse de données de salutation. Par exemple, vous pouvez lire les données sous forme de texte plutôt que sous forme de `byte[]`.

Hello de code suivant lit des lignes de texte hello flux jusqu'à ce qu’une annulation est demandée :

```csharp
// Create a CancellationToken, so that we can cancel hello while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from hello 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of hello processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a>Envoi de données
Une fois que vous avez établi une connexion, vous pouvez envoyer un point de terminaison de relais toohello message. Étant donné que hérite de l’objet de connexion hello [flux](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), envoyer vos données comme un `byte[]`. Hello suivant montre l’exemple de comment toodo cela :

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

Toutefois, si vous souhaitez toosend texte directement, sans avoir besoin de chaîne de hello tooencode chaque fois, vous pouvez encapsuler hello `hybridConnectionStream` de l’objet avec un [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) objet.

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur Azure relais, consultez ces liens :

* [Informations de référence sur Microsoft.Azure.Relay](/dotnet/api/microsoft.azure.relay)
* [Qu’est-ce qu’Azure Relay ?](relay-what-is-it.md)
* [API Relay disponibles](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener