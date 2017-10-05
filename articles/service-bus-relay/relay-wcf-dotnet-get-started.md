---
title: Prise en main des relais WCF Azure Relay dans .NET | Microsoft Docs
description: "Découvrez comment utiliser les relais WCF Azure Relay pour connecter deux applications hébergées à des emplacements différents."
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
ms.openlocfilehash: 1af1ac78398d65e6a87f0d24d6198f3dfbc82ffd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="4a9b9-103">Comment utiliser les relais WCF Azure Relay avec .NET</span><span class="sxs-lookup"><span data-stu-id="4a9b9-103">How to use Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="4a9b9-104">Cet article explique comment utiliser le service Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-104">This article describes how to use the Azure Relay service.</span></span> <span data-ttu-id="4a9b9-105">Les exemples sont écrits en C# et utilisent l’API WCF (Windows Communication Foundation) avec les extensions contenues dans l’assembly Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-105">The samples are written in C# and use the Windows Communication Foundation (WCF) API with extensions contained in the Service Bus assembly.</span></span> <span data-ttu-id="4a9b9-106">Pour plus d’informations sur Azure Relay, consultez la page [Vue d’ensemble d’Azure Relay](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="4a9b9-106">For more information about Azure relay, see the [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="4a9b9-107">Qu’est-ce que WCF Relay ?</span><span class="sxs-lookup"><span data-stu-id="4a9b9-107">What is WCF Relay?</span></span>

<span data-ttu-id="4a9b9-108">Le service Azure [*WCF Relay*](relay-what-is-it.md) vous permet de créer des applications hybrides qui s’exécutent à la fois dans un centre de données Azure et dans votre propre environnement d’entreprise local.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-108">The Azure [*WCF Relay*](relay-what-is-it.md) service enables you to build hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="4a9b9-109">Le service Relay facilite ce processus en offrant la possibilité d’exposer en toute sécurité les services WCF (Windows Communication Foundation) qui résident dans un réseau d’entreprise sur le cloud public, sans avoir à ouvrir une connexion de pare-feu ni à exiger des modifications intrusives dans une infrastructure de réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-109">The relay service facilitates this by enabling you to securely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or requiring intrusive changes to a corporate network infrastructure.</span></span>

![Concepts du service WCF Relay](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="4a9b9-111">Azure Relay vous permet d’héberger des services WCF au sein de votre environnement d’entreprise actuel.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-111">Azure Relay enables you to host WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="4a9b9-112">Vous pouvez ensuite déléguer au service Relay s’exécutant dans Azure l’écoute des sessions et des demandes entrantes adressées à ces services WCF.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-112">You can then delegate listening for incoming sessions and requests to these WCF services to the relay service running within Azure.</span></span> <span data-ttu-id="4a9b9-113">Cela vous permet d'exposer ces services au code d'application s'exécutant dans Azure, à des travailleurs itinérants ou à des environnements extranet de partenaires.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-113">This enables you to expose these services to application code running in Azure, or to mobile workers or extranet partner environments.</span></span> <span data-ttu-id="4a9b9-114">Relay vous permet de contrôler de manière précise et sécurisée les utilisateurs autorisés à accéder à ces services.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-114">Relay enables you to securely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="4a9b9-115">Il offre un moyen efficace et sûr d'exposer les fonctionnalités et les données applicatives de vos solutions d'entreprise existantes et d'en tirer profit depuis le cloud.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-115">It provides a powerful and secure way to expose application functionality and data from your existing enterprise solutions and take advantage of it from the cloud.</span></span>

<span data-ttu-id="4a9b9-116">Cet article explique comment utiliser Azure Relay pour créer un service web WCF, exposé à l’aide d’une liaison de canal TCP, qui implémente une conversation sécurisée entre deux parties.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-116">This article discusses how to use Azure Relay to create a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-the-service-bus-nuget-package"></a><span data-ttu-id="4a9b9-117">Obtention du package NuGet Service Bus</span><span class="sxs-lookup"><span data-stu-id="4a9b9-117">Get the Service Bus NuGet package</span></span>
<span data-ttu-id="4a9b9-118">Le [package NuGet Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus) est le moyen le plus simple de se procurer l’API Service Bus et de configurer votre application avec toutes les dépendances Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-118">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span></span> <span data-ttu-id="4a9b9-119">Pour installer le package NuGet dans votre projet, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="4a9b9-119">To install the NuGet package in your project, do the following:</span></span>

1. <span data-ttu-id="4a9b9-120">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Références**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="4a9b9-121">Recherchez « Service Bus » et sélectionnez l’élément **Microsoft Azure Service Bus** .</span><span class="sxs-lookup"><span data-stu-id="4a9b9-121">Search for "Service Bus" and select the **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="4a9b9-122">Cliquez sur **Installer** pour terminer l’installation, puis fermez la boîte de dialogue suivante :</span><span class="sxs-lookup"><span data-stu-id="4a9b9-122">Click **Install** to complete the installation, then close the following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="4a9b9-123">Exposer et consommer un service web SOAP avec TCP</span><span class="sxs-lookup"><span data-stu-id="4a9b9-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="4a9b9-124">Pour exposer un service Web SOAP WCF existant pour une consommation externe, vous devez apporter des modifications aux liaisons et aux adresses du service.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-124">To expose an existing WCF SOAP web service for external consumption, you must make changes to the service bindings and addresses.</span></span> <span data-ttu-id="4a9b9-125">Vous pouvez ainsi être amené à modifier votre fichier de configuration ou votre code, selon la façon dont vous avez défini et configuré vos services WCF.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-125">This may require changes to your configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="4a9b9-126">Notez que WCF vous permet de disposer de plusieurs points de terminaison réseau sur un même service. Vous pouvez donc conserver les points de terminaison internes existants et ajouter en même temps des points de terminaison de relais pour l’accès externe.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-126">Note that WCF allows you to have multiple network endpoints over the same service, so you can retain the existing internal endpoints while adding relay endpoints for external access at the same time.</span></span>

<span data-ttu-id="4a9b9-127">Dans cette tâche, vous créez un service WCF simple et y ajoutez un écouteur de relais.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-127">In this task, you build a simple WCF service and add a relay listener to it.</span></span> <span data-ttu-id="4a9b9-128">Cet exercice part du principe que vous utilisez déjà Visual Studio, vous ne serez donc pas guidé pour la création de projet.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all the details of creating a project.</span></span> <span data-ttu-id="4a9b9-129">Il porte essentiellement sur le code.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-129">Instead, it focuses on the code.</span></span>

<span data-ttu-id="4a9b9-130">Avant d’effectuer ces étapes, exécutez la procédure suivante pour configurer votre environnement :</span><span class="sxs-lookup"><span data-stu-id="4a9b9-130">Before starting these steps, complete the following procedure to set up your environment:</span></span>

1. <span data-ttu-id="4a9b9-131">Dans Visual Studio, créez une application de console contenant deux projets (« Client » et « Service ») dans la solution.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within the solution.</span></span>
2. <span data-ttu-id="4a9b9-132">Ajoutez le package Service Bus NuGet pour les deux projets.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-132">Add the Service Bus NuGet package to both projects.</span></span> <span data-ttu-id="4a9b9-133">Ce package ajoute toutes les références d’assembly nécessaires à vos projets.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-133">This package adds all the necessary assembly references to your projects.</span></span>

### <a name="how-to-create-the-service"></a><span data-ttu-id="4a9b9-134">Création du service</span><span class="sxs-lookup"><span data-stu-id="4a9b9-134">How to create the service</span></span>
<span data-ttu-id="4a9b9-135">Pour commencer, créez le service proprement dit.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-135">First, create the service itself.</span></span> <span data-ttu-id="4a9b9-136">Un service WCF se compose d'au moins trois parties distinctes :</span><span class="sxs-lookup"><span data-stu-id="4a9b9-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="4a9b9-137">Définition d'un contrat décrivant la nature des messages échangés et des opérations à appeler.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-137">Definition of a contract that describes what messages are exchanged and what operations are to be invoked.</span></span>
* <span data-ttu-id="4a9b9-138">Implémentation de ce contrat.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-138">Implementation of that contract.</span></span>
* <span data-ttu-id="4a9b9-139">Hôte hébergeant ce service WCF et exposant plusieurs points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-139">Host that hosts the WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="4a9b9-140">Les exemples de code présentés dans cette section portent sur chacun de ces composants.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-140">The code examples in this section address each of these components.</span></span>

<span data-ttu-id="4a9b9-141">Le contrat définit une seule opération, `AddNumbers`, qui ajoute deux nombres et renvoie le résultat.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-141">The contract defines a single operation, `AddNumbers`, that adds two numbers and returns the result.</span></span> <span data-ttu-id="4a9b9-142">L'interface `IProblemSolverChannel` permet au client de gérer plus facilement la durée de vie du proxy.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-142">The `IProblemSolverChannel` interface enables the client to more easily manage the proxy lifetime.</span></span> <span data-ttu-id="4a9b9-143">Il est recommandé de créer une interface de ce type.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="4a9b9-144">De même, vous avez tout intérêt à placer cette définition de contrat dans un fichier distinct de façon à pouvoir y faire référence dans les deux projets (« Client » et « Service »). Vous pouvez également copier le code dans les deux projets.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-144">It's a good idea to put this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy the code into both projects.</span></span>

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

<span data-ttu-id="4a9b9-145">Une fois que le contrat est en place, l’implémentation se déroule de la façon suivante :</span><span class="sxs-lookup"><span data-stu-id="4a9b9-145">With the contract in place, the implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="4a9b9-146">Configurer un hôte de service par programme</span><span class="sxs-lookup"><span data-stu-id="4a9b9-146">Configure a service host programmatically</span></span>
<span data-ttu-id="4a9b9-147">Maintenant que le contrat et l'implémentation sont en place, vous pouvez héberger le service.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-147">With the contract and implementation in place, you can now host the service.</span></span> <span data-ttu-id="4a9b9-148">L’hébergement se situe à l’intérieur d’un objet [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx), qui se charge de gérer les instances du service et héberge les points de terminaison qui écoutent les messages.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of the service and hosts the endpoints that listen for messages.</span></span> <span data-ttu-id="4a9b9-149">Le code suivant configure le service avec, d’une part, un point de terminaison local normal et, d’autre part, un point de terminaison de relais, pour illustrer la mise en correspondance, côte à côte, des points de terminaison internes et externes.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-149">The following code configures the service with both a regular local endpoint and a relay endpoint to illustrate the appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="4a9b9-150">Remplacez la chaîne *namespace* par le nom de votre espace de noms et *yourKey* par la clé SAP que vous avez obtenue à l’étape de configuration précédente.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-150">Replace the string *namespace* with your namespace name and *yourKey* with the SAS key that you obtained in the previous setup step.</span></span>

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

Console.WriteLine("Press ENTER to close");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="4a9b9-151">Dans l'exemple, vous créez deux points de terminaison dans le cadre de l'implémentation du même contrat.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-151">In the example, you create two endpoints that are on the same contract implementation.</span></span> <span data-ttu-id="4a9b9-152">L’un est local et l’autre projeté via Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="4a9b9-153">Leurs principales différences sont les liaisons : [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) pour le point de terminaison local, et [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) pour les adresses et le point de terminaison de relais.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-153">The key differences between them are the bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for the local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for the relay endpoint and the addresses.</span></span> <span data-ttu-id="4a9b9-154">Le point de terminaison local possède une adresse réseau locale avec un port distinct.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-154">The local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="4a9b9-155">Le point de terminaison de relais possède une adresse de point de terminaison constituée de la chaîne `sb`, du nom de votre espace de noms et du chemin « solver ».</span><span class="sxs-lookup"><span data-stu-id="4a9b9-155">The relay endpoint has an endpoint address composed of the string `sb`, your namespace name, and the path "solver."</span></span> <span data-ttu-id="4a9b9-156">L’URI obtenu est le suivant : `sb://[serviceNamespace].servicebus.windows.net/solver`, lequel identifie le point de terminaison du service comme un point de terminaison TCP Service Bus (relais) associé à un nom DNS externe complet.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-156">This results in the URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying the service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="4a9b9-157">Si vous insérez le code en remplaçant les espaces réservés dans la fonction `Main` de l’application **Service**, vous obtiendrez un service fonctionnel.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-157">If you place the code replacing the placeholders into the `Main` function of the **Service** application, you will have a functional service.</span></span> <span data-ttu-id="4a9b9-158">Si vous voulez que votre service écoute exclusivement sur le relais, supprimez la déclaration du point de terminaison local.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-158">If you want your service to listen exclusively on the relay, remove the local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-the-appconfig-file"></a><span data-ttu-id="4a9b9-159">Configurer un hôte de service dans le fichier App.config</span><span class="sxs-lookup"><span data-stu-id="4a9b9-159">Configure a service host in the App.config file</span></span>
<span data-ttu-id="4a9b9-160">Vous pouvez également configurer l'hôte à l'aide du fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-160">You can also configure the host using the App.config file.</span></span> <span data-ttu-id="4a9b9-161">Dans ce cas, le code d’hébergement de service s’affiche dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-161">The service hosting code in this case appears in the next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER to close");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="4a9b9-162">Les définitions de point de terminaison se déplacent dans le fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-162">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="4a9b9-163">Le package NuGet a déjà ajouté au fichier App.config une plage de définitions qui sont les extensions de la configuration nécessaire pour Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-163">The NuGet package has already added a range of definitions to the App.config file, which are the required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="4a9b9-164">L’exemple suivant, équivalent exact du code précédent, doit figurer juste en dessous de l’élément **system.serviceModel**.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-164">The following example, which is the exact equivalent of the previous code, should appear directly beneath the **system.serviceModel** element.</span></span> <span data-ttu-id="4a9b9-165">Cet exemple de code suppose que l’espace de noms C# de votre projet se nomme **Service**.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="4a9b9-166">Remplacez les espaces réservés par le nom de votre espace de noms de relais et la clé SAS associée.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-166">Replace the placeholders with your relay namespace name and SAS key.</span></span>

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

<span data-ttu-id="4a9b9-167">Une fois ces modifications effectuées, le service démarre comme précédemment, mais avec deux points de terminaison actifs : l'un local et l'autre écoutant dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-167">After you make these changes, the service starts as it did before, but with two live endpoints: one local and one listening in the cloud.</span></span>

### <a name="create-the-client"></a><span data-ttu-id="4a9b9-168">Création du client</span><span class="sxs-lookup"><span data-stu-id="4a9b9-168">Create the client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="4a9b9-169">Configuration d’un client par programme</span><span class="sxs-lookup"><span data-stu-id="4a9b9-169">Configure a client programmatically</span></span>
<span data-ttu-id="4a9b9-170">Pour consommer le service, vous pouvez construire un client WCF à l’aide d’un objet [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a9b9-170">To consume the service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="4a9b9-171">Service Bus utilise un modèle de sécurité basée sur un jeton, implémenté à l'aide de SAS.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="4a9b9-172">La classe [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) représente un fournisseur de jetons de sécurité dont les méthodes de fabrique intégrées renvoient des fournisseurs de jetons bien connus.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-172">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="4a9b9-173">L’exemple suivant utilise la méthode [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) pour gérer l’acquisition du jeton SAP approprié.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-173">The following example uses the [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to handle the acquisition of the appropriate SAS token.</span></span> <span data-ttu-id="4a9b9-174">Le nom et la clé sont ceux obtenus sur le portail comme indiqué dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-174">The name and key are those obtained from the portal as described in the previous section.</span></span>

<span data-ttu-id="4a9b9-175">Tout d'abord, référencez ou copiez le code du contrat `IProblemSolver` du service dans votre projet client.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-175">First, reference or copy the `IProblemSolver` contract code from the service into your client project.</span></span>

<span data-ttu-id="4a9b9-176">Ensuite, remplacez le code dans la méthode `Main` du client, en remplaçant de nouveau le texte d’espace réservé par votre espace de noms de relais et la clé SAP associée.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-176">Then, replace the code in the `Main` method of the client, again replacing the placeholder text with your relay namespace and SAS key.</span></span>

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

<span data-ttu-id="4a9b9-177">Vous pouvez maintenant créer le client et le service, les exécuter (en commençant par le service) ; le client appelle alors le service et imprime **9**.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-177">You can now build the client and the service, run them (run the service first), and the client calls the service and prints **9**.</span></span> <span data-ttu-id="4a9b9-178">Vous pouvez exécuter le client et le serveur sur différents ordinateurs, voire sur des réseaux, la communication fonctionnera toujours.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-178">You can run the client and server on different machines, even across networks, and the communication will still work.</span></span> <span data-ttu-id="4a9b9-179">Le code client peut également être exécuté dans le cloud ou en local.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-179">The client code can also run in the cloud or locally.</span></span>

#### <a name="configure-a-client-in-the-appconfig-file"></a><span data-ttu-id="4a9b9-180">Configuration d’un client dans le fichier App.config</span><span class="sxs-lookup"><span data-stu-id="4a9b9-180">Configure a client in the App.config file</span></span>
<span data-ttu-id="4a9b9-181">Vous pouvez également configurer le client à l’aide du fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-181">The following code shows how to configure the client using the App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="4a9b9-182">Les définitions de point de terminaison se déplacent dans le fichier App.config.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-182">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="4a9b9-183">L’exemple suivant, identique au code présenté précédemment, doit figurer juste au-dessous de l’élément `<system.serviceModel>`.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-183">The following example, which is the same as the code listed previously, should appear directly beneath the `<system.serviceModel>` element.</span></span> <span data-ttu-id="4a9b9-184">Comme précédemment, vous devez remplacer les espaces réservés par l’espace de noms de relais et la clé SAS associée.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-184">Here, as before, you must replace the placeholders with your relay namespace and SAS key.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4a9b9-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4a9b9-185">Next steps</span></span>
<span data-ttu-id="4a9b9-186">Maintenant que vous connaissez les principes de base d’Azure Relay, suivez ces liens pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="4a9b9-186">Now that you've learned the basics of Azure Relay, follow these links to learn more.</span></span>

* [<span data-ttu-id="4a9b9-187">Qu’est-ce qu’Azure Relay ?</span><span class="sxs-lookup"><span data-stu-id="4a9b9-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="4a9b9-188">Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="4a9b9-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="4a9b9-189">Téléchargez des exemples Service Bus à la page [Exemples Azure][Azure samples] ou consultez la [vue d’ensemble des exemples Service Bus][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="4a9b9-189">Download Service Bus samples from [Azure samples][Azure samples] or see the [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md
