---
title: "Vue d’ensemble des API .NET standard Azure Relay | Microsoft Docs"
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
ms.openlocfilehash: f3f4a2e721b1a75a5b92a5c17a9939c7013340d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="1eaa6-103">Présentation des API .NET standard pour les connexions hybrides Azure Relay</span><span class="sxs-lookup"><span data-stu-id="1eaa6-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="1eaa6-104">Cet article passe en revue les principales [API clientes](/dotnet/api/microsoft.azure.relay) .NET standard pour les connexions hybrides Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-104">This article summarizes some of the key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="1eaa6-105">Générateur de chaînes de connexion Relay</span><span class="sxs-lookup"><span data-stu-id="1eaa6-105">Relay Connection String Builder</span></span>

<span data-ttu-id="1eaa6-106">La classe [RelayConnectionStringBuilder][RelayConnectionStringBuilder] met en forme des chaînes de connexion propres aux connexions hybrides Relay.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-106">The [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific to Relay Hybrid Connections.</span></span> <span data-ttu-id="1eaa6-107">Vous pouvez l’utiliser pour vérifier le format d’une chaîne de connexion ou pour créer une chaîne de connexion à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-107">You can use it to verify the format of a connection string, or to build a connection string from scratch.</span></span> <span data-ttu-id="1eaa6-108">Le code suivant montre un exemple :</span><span class="sxs-lookup"><span data-stu-id="1eaa6-108">See the following code for an example:</span></span>

```csharp
var endpoint = "{Relay namespace}";
var entityPath = "{Name of the Hybrid Connection}";
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

<span data-ttu-id="1eaa6-109">Vous pouvez également transmettre une chaîne de connexion directement à la méthode `RelayConnectionStringBuilder`.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-109">You can also pass a connection string directly to the `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="1eaa6-110">Cette opération vous permet de vérifier que le format de la chaîne de connexion est valide.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-110">This operation enables you to verify that the connection string is in a valid format.</span></span> <span data-ttu-id="1eaa6-111">Si des paramètres ne sont pas valides, le constructeur génère une `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-111">If any of the parameters are invalid, the constructor generates an `ArgumentException`.</span></span>

```csharp
var myConnectionString = "{RelayConnectionString}";
// Declare the connectionStringBuilder so that it can be used outside of the loop if needed
RelayConnectionStringBuilder connectionStringBuilder;
try
{
    // Create the connectionStringBuilder using the supplied connection string
    connectionStringBuilder = new RelayConnectionStringBuilder(myConnectionString);
}
catch (ArgumentException ae)
{
    // Perform some error handling
}
```

## <a name="hybrid-connection-stream"></a><span data-ttu-id="1eaa6-112">Flux de connexion hybride</span><span class="sxs-lookup"><span data-stu-id="1eaa6-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="1eaa6-113">La classe [HybridConnectionStream][HCStream] est l’objet principal utilisé pour envoyer et recevoir des données à partir d’un point de terminaison Azure Relay si vous travaillez avec un [HybridConnectionClient][HCClient] ou un [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="1eaa6-113">The [HybridConnectionStream][HCStream] class is the primary object used to send and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="1eaa6-114">Obtention d’un flux de connexion hybride</span><span class="sxs-lookup"><span data-stu-id="1eaa6-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="1eaa6-115">Écouteur</span><span class="sxs-lookup"><span data-stu-id="1eaa6-115">Listener</span></span>
<span data-ttu-id="1eaa6-116">À l’aide d’un [HybridConnectionListener][HCListener], vous pouvez obtenir un objet `HybridConnectionStream` comme suit :</span><span class="sxs-lookup"><span data-stu-id="1eaa6-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection to the Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="1eaa6-117">Client</span><span class="sxs-lookup"><span data-stu-id="1eaa6-117">Client</span></span>
<span data-ttu-id="1eaa6-118">À l’aide d’un [HybridConnectionClient][HCClient], vous pouvez obtenir un objet `HybridConnectionStream` comme suit :</span><span class="sxs-lookup"><span data-stu-id="1eaa6-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use the RelayConnectionStringBuilder to get a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection to the Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="1eaa6-119">Réception de données</span><span class="sxs-lookup"><span data-stu-id="1eaa6-119">Receiving data</span></span>
<span data-ttu-id="1eaa6-120">La classe [HybridConnectionStream][HCStream] permet une communication bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-120">The [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="1eaa6-121">Dans la plupart des cas, vous recevez en continu à partir du flux.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-121">In most cases, you continuously receive from the stream.</span></span> <span data-ttu-id="1eaa6-122">Si vous lisez du texte à partir du flux, vous pouvez également utiliser un objet [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx), qui facilite l’analyse des données.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-122">If you are reading text from the stream, you may also want to use a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of the data.</span></span> <span data-ttu-id="1eaa6-123">Par exemple, vous pouvez lire les données sous forme de texte plutôt que sous forme de `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="1eaa6-124">Le code suivant lit des lignes individuelles de texte à partir du flux jusqu’à ce qu’une annulation soit demandée :</span><span class="sxs-lookup"><span data-stu-id="1eaa6-124">The following code reads individual lines of text from the stream until a cancellation is requested:</span></span>

```csharp
// Create a CancellationToken, so that we can cancel the while loop
var cancellationToken = new CancellationToken();
// Create a StreamReader from the 'hybridConnectionStream`
var streamReader = new StreamReader(hybridConnectionStream);

while (!cancellationToken.IsCancellationRequested)
{
    // Read a line of input until a newline is encountered
    var line = await streamReader.ReadLineAsync();
    if (string.IsNullOrEmpty(line))
    {
        // If there's no input data, we will signal that 
        // we will no longer send data on this connection
        // and then break out of the processing loop.
        await hybridConnectionStream.ShutdownAsync(cancellationToken);
        break;
    }
}
```

### <a name="sending-data"></a><span data-ttu-id="1eaa6-125">Envoi de données</span><span class="sxs-lookup"><span data-stu-id="1eaa6-125">Sending data</span></span>
<span data-ttu-id="1eaa6-126">Une fois qu’une connexion a été établie, vous pouvez envoyer un message au point de terminaison Relay.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-126">Once you have a connection established, you can send a message to the Relay endpoint.</span></span> <span data-ttu-id="1eaa6-127">Parce que l’objet de connexion hérite de la classe [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), envoyez vos données sous forme de `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="1eaa6-127">Because the connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="1eaa6-128">L’exemple suivant vous montre comment procéder :</span><span class="sxs-lookup"><span data-stu-id="1eaa6-128">The following example shows how to do this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="1eaa6-129">Toutefois, si vous souhaitez envoyer du texte directement, sans avoir à coder la chaîne à chaque fois, vous pouvez encapsuler l’objet `hybridConnectionStream` avec un objet [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="1eaa6-129">However, if you want to send text directly, without needing to encode the string each time, you can wrap the `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// The StreamWriter object only needs to be created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="1eaa6-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1eaa6-130">Next steps</span></span>
<span data-ttu-id="1eaa6-131">Pour en savoir plus sur Azure Relay, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="1eaa6-131">To learn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="1eaa6-132">Informations de référence sur Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="1eaa6-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="1eaa6-133">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="1eaa6-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="1eaa6-134">API Relay disponibles</span><span class="sxs-lookup"><span data-stu-id="1eaa6-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener