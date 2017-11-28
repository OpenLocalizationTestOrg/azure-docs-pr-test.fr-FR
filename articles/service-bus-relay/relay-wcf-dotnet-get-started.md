---
title: aaaGet en main de relais WCF de relais Azure dans .NET | Documents Microsoft
description: "Découvrez comment toouse Azure relais WCF transmet tooconnect deux applications hébergées dans des emplacements différents."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="09688-103">Comment toouse Azure relais WCF des relais avec .NET</span><span class="sxs-lookup"><span data-stu-id="09688-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="09688-104">Cet article décrit comment toouse hello service de relais d’Azure.</span><span class="sxs-lookup"><span data-stu-id="09688-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="09688-105">exemples de Hello sont écrites en c# et utilisent des API de Windows Communication Foundation (WCF) hello avec extensions contenues dans hello assembly Service Bus.</span><span class="sxs-lookup"><span data-stu-id="09688-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="09688-106">Pour plus d’informations sur les relais Azure, consultez hello [vue d’ensemble de Azure relais](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="09688-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="09688-107">Qu’est-ce que WCF Relay ?</span><span class="sxs-lookup"><span data-stu-id="09688-107">What is WCF Relay?</span></span>

<span data-ttu-id="09688-108">Bonjour Azure [ *WCF relais* ](relay-what-is-it.md) service vous permet de toobuild d’applications hybrides qui s’exécutent dans un centre de données Azure et votre propre environnement d’entreprise local.</span><span class="sxs-lookup"><span data-stu-id="09688-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="09688-109">Cela facilite le service de relais Hello en vous toosecurely exposer des services Windows Communication Foundation (WCF) qui résident dans un cloud entreprise réseau toohello public, sans avoir tooopen connexion via un pare-feu ou l’exigence infrastructure de réseau d’entreprise tooa modifications contraignant.</span><span class="sxs-lookup"><span data-stu-id="09688-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![Concepts du service WCF Relay](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="09688-111">Relais Azure vous permet de toohost les services WCF au sein de votre environnement d’entreprise existante.</span><span class="sxs-lookup"><span data-stu-id="09688-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="09688-112">Vous pouvez ensuite déléguer à l’écoute entrant sessions et demandes toothese services toohello service de relais WCF qui s’exécutent dans Azure.</span><span class="sxs-lookup"><span data-stu-id="09688-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="09688-113">Ainsi, vous tooexpose ces code tooapplication des services en cours d’exécution dans Azure, ou toomobile traitements ou les environnements de partenaires de l’extranet.</span><span class="sxs-lookup"><span data-stu-id="09688-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="09688-114">Relais vous permet de contrôler de toosecurely qui permettre accéder à ces services à un niveau de granularité fin.</span><span class="sxs-lookup"><span data-stu-id="09688-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="09688-115">Il fournit une fonctionnalité puissante et sécurisée de l’application tooexpose et les données à partir de vos solutions d’entreprise existantes et de tirer parti de celui-ci à partir du cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="09688-116">Cet article explique comment toouse Azure relais toocreate un service web WCF, exposés à l’aide d’une liaison de canal TCP, qui implémente une conversation sécurisée entre deux parties.</span><span class="sxs-lookup"><span data-stu-id="09688-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="09688-117">Obtenir hello du package NuGet Service Bus</span><span class="sxs-lookup"><span data-stu-id="09688-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="09688-118">Hello [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) est hello de tooget de façon plus simple hello API Service Bus et tooconfigure votre application avec toutes les dépendances du Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="09688-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="09688-119">package de NuGet tooinstall hello dans votre projet, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="09688-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="09688-120">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="09688-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="09688-121">Recherche de « Service Bus » et sélectionnez hello **Microsoft Azure Service Bus** élément.</span><span class="sxs-lookup"><span data-stu-id="09688-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="09688-122">Cliquez sur **installer** toocomplete hello installation, puis fermez hello suivant la boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="09688-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="09688-123">Exposer et consommer un service web SOAP avec TCP</span><span class="sxs-lookup"><span data-stu-id="09688-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="09688-124">tooexpose un service web de SOAP WCF existant pour la consommation externe, vous devez vous modifications toohello service liaisons et les adresses.</span><span class="sxs-lookup"><span data-stu-id="09688-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="09688-125">Cette opération peut nécessiter le fichier de configuration de tooyour de modifications, ou elle peut nécessiter des modifications du code, selon la façon dont vous avez installé et configuré vos services WCF.</span><span class="sxs-lookup"><span data-stu-id="09688-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="09688-126">Notez que WCF vous permet de toohave plusieurs points de terminaison de réseau sur hello même service, afin que vous puissiez conserver hello existante des points de terminaison internes lors de l’ajout de points de terminaison de relais externe d’accès à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="09688-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="09688-127">Dans cette tâche, vous générez un service WCF simple et ajoutez un tooit d’écouteur de relais.</span><span class="sxs-lookup"><span data-stu-id="09688-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="09688-128">Cet exercice une connaissance de Visual Studio et donc ne pas parcourt tous les détails de hello de création d’un projet.</span><span class="sxs-lookup"><span data-stu-id="09688-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="09688-129">Au lieu de cela, il se concentre sur le code de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="09688-130">Avant de commencer cette procédure, effectuez hello suivant tooset procédure de votre environnement :</span><span class="sxs-lookup"><span data-stu-id="09688-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="09688-131">Dans Visual Studio, créez une application console qui contient deux projets, « Client » et « Service », au sein de la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="09688-132">Ajouter les projets de tooboth de package NuGet Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="09688-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="09688-133">Ce package ajoute tous les projets de tooyour références hello assembly nécessaires.</span><span class="sxs-lookup"><span data-stu-id="09688-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="09688-134">Comment toocreate hello service</span><span class="sxs-lookup"><span data-stu-id="09688-134">How toocreate hello service</span></span>
<span data-ttu-id="09688-135">Commencez par créer service hello proprement dit.</span><span class="sxs-lookup"><span data-stu-id="09688-135">First, create hello service itself.</span></span> <span data-ttu-id="09688-136">Un service WCF se compose d'au moins trois parties distinctes :</span><span class="sxs-lookup"><span data-stu-id="09688-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="09688-137">Définition d’un contrat qui décrit les messages sont échangés et les opérations toobe appelé.</span><span class="sxs-lookup"><span data-stu-id="09688-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="09688-138">Implémentation de ce contrat.</span><span class="sxs-lookup"><span data-stu-id="09688-138">Implementation of that contract.</span></span>
* <span data-ttu-id="09688-139">Hôte qui héberge le service WCF de hello et expose plusieurs points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="09688-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="09688-140">les exemples de code Hello dans cette section adresse chacun de ces composants.</span><span class="sxs-lookup"><span data-stu-id="09688-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="09688-141">contrat de Hello définit une seule opération, `AddNumbers`, qui ajoute deux nombres et retourne le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="09688-142">Hello `IProblemSolverChannel` toomore de client hello interface permet de gérer facilement la durée de vie de proxy hello.</span><span class="sxs-lookup"><span data-stu-id="09688-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="09688-143">Il est recommandé de créer une interface de ce type.</span><span class="sxs-lookup"><span data-stu-id="09688-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="09688-144">Il s’agit d’une bonne idée tooput cette définition dans un fichier distinct du contrat de sorte que vous pouvez référencer ce fichier à partir de projets à la fois votre « Client » et « Service », mais vous pouvez également copier le code de hello dans les deux projets.</span><span class="sxs-lookup"><span data-stu-id="09688-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

<span data-ttu-id="09688-145">Avec le contrat hello en place, mise en œuvre hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="09688-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="09688-146">Configurer un hôte de service par programme</span><span class="sxs-lookup"><span data-stu-id="09688-146">Configure a service host programmatically</span></span>
<span data-ttu-id="09688-147">Avec le contrat de hello et l’implémentation en place, vous pouvez maintenant héberger le service de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="09688-148">Hébergement se produit à l’intérieur d’un [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) de l’objet, qui prend en charge la gestion des instances du service de hello et hôtes hello des points de terminaison qui écoutent les messages.</span><span class="sxs-lookup"><span data-stu-id="09688-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="09688-149">Hello de code suivant configure hello service avec un point de terminaison local régulière et un aspect de hello tooillustrate relais point de terminaison, côte à côte, des points de terminaison internes et externes.</span><span class="sxs-lookup"><span data-stu-id="09688-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="09688-150">Remplacez la chaîne de hello *espace de noms* de votre espace de noms et *yourKey* avec la clé SAS hello obtenu à l’étape d’installation précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="09688-151">Dans l’exemple de hello, vous créez deux points de terminaison qui se trouvent sur hello même implémentation de contrat.</span><span class="sxs-lookup"><span data-stu-id="09688-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="09688-152">L’un est local et l’autre projeté via Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="09688-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="09688-153">Hello principales différences entre eux sont des liaisons de hello ; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) pour hello local et [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) pour le point de terminaison de relais hello et les adresses de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="09688-154">point de terminaison local Hello possède une adresse de réseau local avec un port distinct.</span><span class="sxs-lookup"><span data-stu-id="09688-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="09688-155">point de terminaison de relais Hello possède une adresse de point de terminaison composée d’une chaîne de hello `sb`, votre nom d’espace de noms et le chemin d’accès de hello « solveur. »</span><span class="sxs-lookup"><span data-stu-id="09688-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="09688-156">Cela entraîne hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifiant le point de terminaison de service hello comme un point de terminaison TCP de Service Bus (relais) avec un nom DNS externe qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="09688-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="09688-157">Si vous placez le code hello en remplaçant les espaces réservés de hello en hello `Main` fonction Hello **Service** application, vous aurez un service fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="09688-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="09688-158">Si vous souhaitez que votre toolisten service exclusivement sur les relais hello, supprimez la déclaration de point de terminaison local hello.</span><span class="sxs-lookup"><span data-stu-id="09688-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="09688-159">Configurer un hôte de service dans le fichier App.config hello</span><span class="sxs-lookup"><span data-stu-id="09688-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="09688-160">Vous pouvez également configurer hôte hello à l’aide du fichier App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="09688-161">service Hello dans ce cas le code d’hébergement s’affiche dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="09688-162">définitions de point de terminaison Hello déplacement dans le fichier App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="09688-163">package NuGet de Hello a déjà ajouté une plage d’un fichier de définitions toohello App.config, qui sont des extensions de configuration hello requis pour le relais de Azure.</span><span class="sxs-lookup"><span data-stu-id="09688-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="09688-164">Hello suivant l’exemple, qui est hello exacte équivalent du code précédent de hello, doit apparaître directement sous hello **system.serviceModel** élément.</span><span class="sxs-lookup"><span data-stu-id="09688-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="09688-165">Cet exemple de code suppose que l’espace de noms C# de votre projet se nomme **Service**.</span><span class="sxs-lookup"><span data-stu-id="09688-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="09688-166">Remplacez les espaces réservés de hello avec votre nom d’espace de noms de relais et de la clé SAS.</span><span class="sxs-lookup"><span data-stu-id="09688-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

<span data-ttu-id="09688-167">Après avoir apporté ces modifications, les service hello démarre comme avant, mais avec deux points de terminaison dynamiques : un utilisateur local et un à l’écoute dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="09688-168">Créer hello client</span><span class="sxs-lookup"><span data-stu-id="09688-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="09688-169">Configuration d’un client par programme</span><span class="sxs-lookup"><span data-stu-id="09688-169">Configure a client programmatically</span></span>
<span data-ttu-id="09688-170">service de hello tooconsume, vous pouvez construire un client WCF à l’aide un [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) objet.</span><span class="sxs-lookup"><span data-stu-id="09688-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="09688-171">Service Bus utilise un modèle de sécurité basée sur un jeton, implémenté à l'aide de SAS.</span><span class="sxs-lookup"><span data-stu-id="09688-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="09688-172">Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) classe représente un fournisseur de jetons de sécurité avec les méthodes de fabrique intégrées qui retournent des fournisseurs de jeton bien connus.</span><span class="sxs-lookup"><span data-stu-id="09688-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="09688-173">exemple Hello utilise hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) acquisition de hello toohandle méthode de jeton SAS approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="09688-174">clé et le nom hello sont celles obtenues à partir du portail hello comme décrit dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="09688-175">First, de référence ou de copie hello `IProblemSolver` de contrat de code à partir du service de hello dans votre projet client.</span><span class="sxs-lookup"><span data-stu-id="09688-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="09688-176">Ensuite, remplacez le code hello Bonjour `Main` méthode hello du client de, à nouveau en remplaçant texte hello avec votre espace de noms de relais et de la clé SAS.</span><span class="sxs-lookup"><span data-stu-id="09688-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="09688-177">Vous pouvez à présent générer client de hello et service hello, exécutez-les (exécution de service de hello tout d’abord), et les clients hello appelle hello service et imprime **9**.</span><span class="sxs-lookup"><span data-stu-id="09688-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="09688-178">Vous pouvez exécuter hello client et le serveur sur des ordinateurs différents, même sur des réseaux, et les communications hello continueront de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="09688-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="09688-179">Hello client code peut également s’exécuter localement ou dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="09688-180">Configuration d’un client dans le fichier App.config hello</span><span class="sxs-lookup"><span data-stu-id="09688-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="09688-181">Hello suivant de code montre comment le client de hello tooconfigure à l’aide de hello fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="09688-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="09688-182">définitions de point de terminaison Hello déplacement dans le fichier App.config de hello.</span><span class="sxs-lookup"><span data-stu-id="09688-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="09688-183">exemple suivant, qui est hello même en tant que code hello répertoriée précédemment, Hello doit apparaître directement sous hello `<system.serviceModel>` élément.</span><span class="sxs-lookup"><span data-stu-id="09688-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="09688-184">Ici, comme auparavant, vous devez remplacer des espaces réservés hello avec votre espace de noms de relais et de la clé SAS.</span><span class="sxs-lookup"><span data-stu-id="09688-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a><span data-ttu-id="09688-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09688-185">Next steps</span></span>
<span data-ttu-id="09688-186">Maintenant que vous avez appris les notions de base de hello de relais d’Azure, suivez ces liens de toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="09688-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="09688-187">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="09688-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="09688-188">Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="09688-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="09688-189">Télécharger les exemples de Service Bus à partir [exemples Azure] [ Azure samples] ou consultez hello [vue d’ensemble des exemples de Service Bus][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="09688-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
