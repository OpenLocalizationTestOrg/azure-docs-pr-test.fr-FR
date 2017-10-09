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
# <a name="azure-relay-hybrid-connections-net-standard-api-overview"></a><span data-ttu-id="6e240-103">Présentation des API .NET standard pour les connexions hybrides Azure Relay</span><span class="sxs-lookup"><span data-stu-id="6e240-103">Azure Relay Hybrid Connections .NET Standard API overview</span></span>

<span data-ttu-id="6e240-104">Cet article récapitule certaines des clé hello Azure relais hybride connexions .NET Standard [API clientes](/dotnet/api/microsoft.azure.relay).</span><span class="sxs-lookup"><span data-stu-id="6e240-104">This article summarizes some of hello key Azure Relay Hybrid Connections .NET Standard [client APIs](/dotnet/api/microsoft.azure.relay).</span></span>
  
## <a name="relay-connection-string-builder"></a><span data-ttu-id="6e240-105">Générateur de chaînes de connexion Relay</span><span class="sxs-lookup"><span data-stu-id="6e240-105">Relay Connection String Builder</span></span>

<span data-ttu-id="6e240-106">Hello [RelayConnectionStringBuilder] [ RelayConnectionStringBuilder] classe met en forme des chaînes de connexion qui sont des connexions hybrides tooRelay spécifique.</span><span class="sxs-lookup"><span data-stu-id="6e240-106">hello [RelayConnectionStringBuilder][RelayConnectionStringBuilder] class formats connection strings that are specific tooRelay Hybrid Connections.</span></span> <span data-ttu-id="6e240-107">Vous pouvez l’utiliser format de hello tooverify de chaîne de connexion, ou toobuild une chaîne de connexion à partir de zéro.</span><span class="sxs-lookup"><span data-stu-id="6e240-107">You can use it tooverify hello format of a connection string, or toobuild a connection string from scratch.</span></span> <span data-ttu-id="6e240-108">Hello après pour obtenir un exemple de code, consultez :</span><span class="sxs-lookup"><span data-stu-id="6e240-108">See hello following code for an example:</span></span>

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

<span data-ttu-id="6e240-109">Vous pouvez également passer une connexion de chaîne directement toohello `RelayConnectionStringBuilder` (méthode).</span><span class="sxs-lookup"><span data-stu-id="6e240-109">You can also pass a connection string directly toohello `RelayConnectionStringBuilder` method.</span></span> <span data-ttu-id="6e240-110">Cette opération vous permet de tooverify chaîne de connexion hello est dans un format valide.</span><span class="sxs-lookup"><span data-stu-id="6e240-110">This operation enables you tooverify that hello connection string is in a valid format.</span></span> <span data-ttu-id="6e240-111">Si un des paramètres de hello ne sont pas valide, le constructeur de hello génère une `ArgumentException`.</span><span class="sxs-lookup"><span data-stu-id="6e240-111">If any of hello parameters are invalid, hello constructor generates an `ArgumentException`.</span></span>

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

## <a name="hybrid-connection-stream"></a><span data-ttu-id="6e240-112">Flux de connexion hybride</span><span class="sxs-lookup"><span data-stu-id="6e240-112">Hybrid Connection Stream</span></span>
<span data-ttu-id="6e240-113">Hello [HybridConnectionStream] [ HCStream] classe est toosend d’objet principal utilisé hello et recevoir des données à partir d’un point de terminaison de relais d’Azure, si vous travaillez avec un [HybridConnectionClient] [ HCClient], ou un [HybridConnectionListener][HCListener].</span><span class="sxs-lookup"><span data-stu-id="6e240-113">hello [HybridConnectionStream][HCStream] class is hello primary object used toosend and receive data from an Azure Relay endpoint, whether you are working with a [HybridConnectionClient][HCClient], or a [HybridConnectionListener][HCListener].</span></span>

### <a name="getting-a-hybrid-connection-stream"></a><span data-ttu-id="6e240-114">Obtention d’un flux de connexion hybride</span><span class="sxs-lookup"><span data-stu-id="6e240-114">Getting a Hybrid Connection Stream</span></span>

#### <a name="listener"></a><span data-ttu-id="6e240-115">Écouteur</span><span class="sxs-lookup"><span data-stu-id="6e240-115">Listener</span></span>
<span data-ttu-id="6e240-116">À l’aide d’un [HybridConnectionListener][HCListener], vous pouvez obtenir un objet `HybridConnectionStream` comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e240-116">Using a [HybridConnectionListener][HCListener], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var listener = new HybridConnectionListener(csb.ToString());
// Open a connection toohello Relay endpoint
await listener.OpenAsync();
// Get a `HybridConnectionStream`
var hybridConnectionStream = await listener.AcceptConnectionAsync();
```

#### <a name="client"></a><span data-ttu-id="6e240-117">Client</span><span class="sxs-lookup"><span data-stu-id="6e240-117">Client</span></span>
<span data-ttu-id="6e240-118">À l’aide d’un [HybridConnectionClient][HCClient], vous pouvez obtenir un objet `HybridConnectionStream` comme suit :</span><span class="sxs-lookup"><span data-stu-id="6e240-118">Using a [HybridConnectionClient][HCClient], you can obtain a `HybridConnectionStream` object as follows:</span></span>

```csharp
// Use hello RelayConnectionStringBuilder tooget a valid connection string
var client = new HybridConnectionClient(csb.ToString());
// Open a connection toohello Relay endpoint and get a `HybridConnectionStream`
var hybridConnectionStream = await client.CreateConnectionAsync();
```

### <a name="receiving-data"></a><span data-ttu-id="6e240-119">Réception de données</span><span class="sxs-lookup"><span data-stu-id="6e240-119">Receiving data</span></span>
<span data-ttu-id="6e240-120">Hello [HybridConnectionStream] [ HCStream] classe permet la communication bidirectionnelle.</span><span class="sxs-lookup"><span data-stu-id="6e240-120">hello [HybridConnectionStream][HCStream] class enables two-way communication.</span></span> <span data-ttu-id="6e240-121">Dans la plupart des cas, vous recevez en continu à partir de flux de données hello.</span><span class="sxs-lookup"><span data-stu-id="6e240-121">In most cases, you continuously receive from hello stream.</span></span> <span data-ttu-id="6e240-122">Si vous lisez le texte à partir de flux de hello, vous pouvez également toouse une [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) objet, ce qui simplifie l’analyse de données de salutation.</span><span class="sxs-lookup"><span data-stu-id="6e240-122">If you are reading text from hello stream, you may also want toouse a [StreamReader](https://msdn.microsoft.com/library/system.io.streamreader(v=vs.110).aspx) object, which enables easier parsing of hello data.</span></span> <span data-ttu-id="6e240-123">Par exemple, vous pouvez lire les données sous forme de texte plutôt que sous forme de `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="6e240-123">For example, you can read data as text, rather than as `byte[]`.</span></span>

<span data-ttu-id="6e240-124">Hello de code suivant lit des lignes de texte hello flux jusqu'à ce qu’une annulation est demandée :</span><span class="sxs-lookup"><span data-stu-id="6e240-124">hello following code reads individual lines of text from hello stream until a cancellation is requested:</span></span>

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

### <a name="sending-data"></a><span data-ttu-id="6e240-125">Envoi de données</span><span class="sxs-lookup"><span data-stu-id="6e240-125">Sending data</span></span>
<span data-ttu-id="6e240-126">Une fois que vous avez établi une connexion, vous pouvez envoyer un point de terminaison de relais toohello message.</span><span class="sxs-lookup"><span data-stu-id="6e240-126">Once you have a connection established, you can send a message toohello Relay endpoint.</span></span> <span data-ttu-id="6e240-127">Étant donné que hérite de l’objet de connexion hello [flux](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), envoyer vos données comme un `byte[]`.</span><span class="sxs-lookup"><span data-stu-id="6e240-127">Because hello connection object inherits [Stream](https://msdn.microsoft.com/library/system.io.stream(v=vs.110).aspx), send your data as a `byte[]`.</span></span> <span data-ttu-id="6e240-128">Hello suivant montre l’exemple de comment toodo cela :</span><span class="sxs-lookup"><span data-stu-id="6e240-128">hello following example shows how toodo this:</span></span>

```csharp
var data = Encoding.UTF8.GetBytes("hello");
await clientConnection.WriteAsync(data, 0, data.Length);
```

<span data-ttu-id="6e240-129">Toutefois, si vous souhaitez toosend texte directement, sans avoir besoin de chaîne de hello tooencode chaque fois, vous pouvez encapsuler hello `hybridConnectionStream` de l’objet avec un [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) objet.</span><span class="sxs-lookup"><span data-stu-id="6e240-129">However, if you want toosend text directly, without needing tooencode hello string each time, you can wrap hello `hybridConnectionStream` object with a [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) object.</span></span>

```csharp
// hello StreamWriter object only needs toobe created once
var textWriter = new StreamWriter(hybridConnectionStream);
await textWriter.WriteLineAsync("hello");
```

## <a name="next-steps"></a><span data-ttu-id="6e240-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6e240-130">Next steps</span></span>
<span data-ttu-id="6e240-131">toolearn en savoir plus sur Azure relais, consultez ces liens :</span><span class="sxs-lookup"><span data-stu-id="6e240-131">toolearn more about Azure Relay, visit these links:</span></span>

* [<span data-ttu-id="6e240-132">Informations de référence sur Microsoft.Azure.Relay</span><span class="sxs-lookup"><span data-stu-id="6e240-132">Microsoft.Azure.Relay reference</span></span>](/dotnet/api/microsoft.azure.relay)
* [<span data-ttu-id="6e240-133">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="6e240-133">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="6e240-134">API Relay disponibles</span><span class="sxs-lookup"><span data-stu-id="6e240-134">Available Relay APIs</span></span>](relay-api-overview.md)

[RelayConnectionStringBuilder]: /dotnet/api/microsoft.azure.relay.relayconnectionstringbuilder
[HCStream]: /dotnet/api/microsoft.azure.relay.hybridconnectionstream
[HCClient]: /dotnet/api/microsoft.azure.relay.hybridconnectionclient
[HCListener]: /dotnet/api/microsoft.azure.relay.hybridconnectionlistener