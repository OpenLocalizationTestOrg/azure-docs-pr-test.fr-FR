---
title: "aaaCreate un serveur web frontal pour votre application Azure Service Fabric à l’aide d’ASP.NET Core | Documents Microsoft"
description: "Exposer votre site web de Service Fabric application toohello à l’aide d’un projet de ASP.NET Core et de la communication interservices via la communication à distance du Service."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="4ce1c-103">Créer un service web frontal pour votre application à l’aide d’ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4ce1c-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="4ce1c-104">Par défaut, les services Azure Service Fabric ne fournissent pas d’un site web toohello interface publique.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="4ce1c-105">tooexpose clients de tooHTTP de fonctionnalités de votre application, vous avez toocreate un site web de projet tooact comme point d’entrée et communiquer de tooyour il n’y a des services individuels.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="4ce1c-106">Dans ce didacticiel, nous reprendre là où nous se Bonjour [créer votre première application dans Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) didacticiel et ajouter un service web de ASP.NET Core devant hello avec état compteur de service.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="4ce1c-107">Si vous ne l’avez pas encore fait, revenez d’abord à ce didacticiel et suivez-le.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="4ce1c-108">Configurer votre environnement pour ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4ce1c-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="4ce1c-109">Vous devez toofollow Visual Studio 2017 avec ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="4ce1c-110">N’importe quelle édition fera l’affaire.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="4ce1c-111">Installer Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4ce1c-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="4ce1c-112">les applications ASP.NET Core pour Service Fabric toodevelop, vous devez avoir hello suivant les charges de travail installés :</span><span class="sxs-lookup"><span data-stu-id="4ce1c-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="4ce1c-113">**Développement Azure** (sous *Web &amp; Cloud*)</span><span class="sxs-lookup"><span data-stu-id="4ce1c-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="4ce1c-114">**Développement web et ASP.NET** (sous *Web &amp; Cloud*)</span><span class="sxs-lookup"><span data-stu-id="4ce1c-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="4ce1c-115">**Développement multiplateforme .NET Core** (sous *Autres jeux d’outils*)</span><span class="sxs-lookup"><span data-stu-id="4ce1c-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="4ce1c-116">Hello outils .NET Core pour Visual Studio 2015 sont n’est plus mis à jour, mais si vous utilisez encore Visual Studio 2015, vous devez toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installé.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="4ce1c-117">Ajouter une application de tooyour service ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4ce1c-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="4ce1c-118">ASP.NET Core est une infrastructure de développement web léger et inter-plateformes que vous pouvez utiliser l’interface utilisateur de web moderne toocreate et API web.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="4ce1c-119">Vous allez ajouter une application ASP.NET Web API projet tooour.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="4ce1c-120">Dans l’Explorateur de solutions, cliquez sur **Services** dans hello du projet d’application et choisissez **Ajouter > nouveau Service Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Ajout d’une application de service tooan existant][vs-add-new-service]
2. <span data-ttu-id="4ce1c-122">Sur hello **créer un Service** choisissez **ASP.NET Core** et lui donner un nom.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![Choix du service web ASP.NET dans la boîte de dialogue hello nouveau service][vs-new-service-dialog]

3. <span data-ttu-id="4ce1c-124">page suivante de Hello fournit un ensemble d’ASP.NET Core modèles de projet.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="4ce1c-125">Notez que ceux-ci sont hello même choix que vous verriez si vous avez créé un projet ASP.NET Core en dehors d’une application Service Fabric, avec une petite quantité de code supplémentaire tooregister hello service avec le runtime du Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="4ce1c-126">Pour ce didacticiel, sélectionnez **API web**.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="4ce1c-127">Toutefois, vous pouvez appliquer hello même concepts toobuilding une application web complète.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![Choix du type de projet ASP.NET][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="4ce1c-129">Une fois votre projet d’API web créé, vous devriez avoir deux services dans votre application.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="4ce1c-130">À mesure que vous toobuild votre application, vous pouvez ajouter davantage de services Bonjour exactement identique.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="4ce1c-131">Chacun peut être mis à niveau et faire l'objet d'un contrôle de version indépendamment.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="4ce1c-132">Exécutez l’application hello</span><span class="sxs-lookup"><span data-stu-id="4ce1c-132">Run hello application</span></span>
<span data-ttu-id="4ce1c-133">tooget une idée de ce que nous avons terminé, nous allons déployer hello nouvelle application et prendre un aspect au comportement par défaut hello hello du modèle de l’API Web ASP.NET principale fournit.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="4ce1c-134">Appuyez sur F5 dans Visual Studio toodebug hello application.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="4ce1c-135">Lorsque le déploiement est terminé, Visual Studio lance une racine toohello navigateur hello service de l’API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="4ce1c-136">modèle de l’API Web ASP.NET principale Hello ne fournit pas par défaut pour la racine de hello, donc vous devez voir une erreur 404 dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="4ce1c-137">Ajouter `/api/values` emplacement toohello dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="4ce1c-138">Il appelle hello `Get` méthode sur hello ValuesController dans le modèle d’API Web hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="4ce1c-139">Il renvoie la réponse par défaut hello fournie par le modèle hello--un tableau JSON qui contient deux chaînes :</span><span class="sxs-lookup"><span data-stu-id="4ce1c-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![Valeurs par défaut retournées par le modèle d’API web ASP.NET Core][browser-aspnet-template-values]
   
    <span data-ttu-id="4ce1c-141">Fin de hello du didacticiel de hello, cette page est sélectionnée par valeur la plus récente compteur hello à partir de notre service avec état, au lieu de hello chaînes par défaut.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="4ce1c-142">Connecter les services de hello</span><span class="sxs-lookup"><span data-stu-id="4ce1c-142">Connect hello services</span></span>
<span data-ttu-id="4ce1c-143">Service Fabric fournit une flexibilité complète sur votre façon de communiquer avec Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="4ce1c-144">Dans une seule application, vous pouvez avoir des services accessibles via TCP, d'autres services accessibles via une API REST HTTP et encore d'autres services qui sont accessibles via des sockets web.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="4ce1c-145">Pour plus d’informations sur les options hello disponibles et les inconvénients hello, consultez [communiquer avec les services](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="4ce1c-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="4ce1c-146">Dans ce didacticiel, nous utilisons [communication à distance du Service Service Fabric](service-fabric-reliable-services-communication-remoting.md), fourni dans le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="4ce1c-147">Bonjour approche de la communication à distance du Service (modélisée sur les appels de procédure distante ou RPC), vous définissez un tooact interface en tant que contrat public de hello pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="4ce1c-148">Ensuite, vous utilisez ce toogenerate interface une classe proxy pour interagir avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="4ce1c-149">Créer l’interface de communication à distance hello</span><span class="sxs-lookup"><span data-stu-id="4ce1c-149">Create hello remoting interface</span></span>
<span data-ttu-id="4ce1c-150">Commençons par créer hello interface tooact comme contrat hello entre un service avec état hello et d’autres services, dans ce cas hello projet de web ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="4ce1c-151">Cette interface doit être partagée par tous les services qui utilisent les appels RPC toomake, donc nous allons la créer dans son propre projet de bibliothèque de classes.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="4ce1c-152">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre solution et choisissez **Ajoutez** > **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="4ce1c-153">Choisissez hello **Visual C#** entrée Bonjour gauche du volet de navigation et sélectionnez hello **bibliothèque de classes** modèle.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="4ce1c-154">Vérifiez cette version de .NET Framework hello est définie trop**4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![Création d’un projet d’interface de votre service avec état][vs-add-class-library-project]

3. <span data-ttu-id="4ce1c-156">Installer hello **Microsoft.ServiceFabric.Services.Remoting** package NuGet.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="4ce1c-157">Recherchez **Microsoft.ServiceFabric.Services.Remoting** dans hello NuGet package manager et l’installer pour tous les projets dans la solution de hello qui utilisent la communication à distance du Service, y compris :</span><span class="sxs-lookup"><span data-stu-id="4ce1c-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="4ce1c-158">projet de bibliothèque de classes Hello qui contient l’interface de service hello</span><span class="sxs-lookup"><span data-stu-id="4ce1c-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="4ce1c-159">projet de Service de Stateful Hello</span><span class="sxs-lookup"><span data-stu-id="4ce1c-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="4ce1c-160">Hello projet de service web ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="4ce1c-160">hello ASP.NET Core web service project</span></span>
   
    ![Ajout du package NuGet de Services hello][vs-services-nuget-package]

4. <span data-ttu-id="4ce1c-162">Dans la bibliothèque de classes hello, créez une interface avec une méthode unique, `GetCountAsync`, et d’étendre l’interface hello de `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="4ce1c-163">interface de communication à distance Hello doit dériver de cette interface tooindicate qu’il s’agit d’une interface de communication à distance du Service.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="4ce1c-164">Implémenter l’interface hello dans votre service avec état</span><span class="sxs-lookup"><span data-stu-id="4ce1c-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="4ce1c-165">Maintenant que nous avons défini l’interface de hello, nous devons tooimplement dans un service avec état hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="4ce1c-166">Dans votre service avec état, ajoutez le projet de bibliothèque de classes toohello référence qui contient l’interface de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![Ajout d’un projet de bibliothèque de classes toohello référence dans un service avec état hello][vs-add-class-library-reference]
2. <span data-ttu-id="4ce1c-168">Localiser hello classe qui hérite de `StatefulService`, tel que `MyStatefulService`et l’étendre tooimplement hello `ICounter` interface.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="4ce1c-169">Désormais implémenter hello seule méthode qui est définie dans hello `ICounter` interface, `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="4ce1c-170">Exposer un service avec état hello à l’aide d’un écouteur de la communication à distance du service</span><span class="sxs-lookup"><span data-stu-id="4ce1c-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="4ce1c-171">Avec hello `ICounter` interface implémentée, étape finale de hello est le canal de communication tooopen hello la communication à distance du Service.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="4ce1c-172">Pour les services avec état, Service Fabric fournit une méthode remplaçable appelée `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="4ce1c-173">Avec cette méthode, vous pouvez spécifier un ou plusieurs écouteurs de communication, en fonction de type hello de communication que vous souhaitez tooenable pour votre service.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="4ce1c-174">méthode équivalente Hello pour l’ouverture d’un services de toostateless de canal de communication est appelée `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="4ce1c-175">Dans ce cas, nous remplacer hello `CreateServiceReplicaListeners` méthode et fournir une instance de `ServiceRemotingListener`, ce qui crée un point de terminaison RPC ne peut être appelé à partir de clients via `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="4ce1c-176">Hello `CreateServiceRemotingListener` méthode d’extension sur hello `IService` interface vous permet de tooeasily créer un `ServiceRemotingListener` avec tous les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="4ce1c-177">toouse cette méthode d’extension, assurez-vous d’avoir hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` espace de noms importé.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="4ce1c-178">Utiliser hello ServiceProxy classe toointeract hello service</span><span class="sxs-lookup"><span data-stu-id="4ce1c-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="4ce1c-179">Notre service avec état est désormais trafic tooreceive prêt à partir d’autres services via RPC.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="4ce1c-180">Par conséquent, tout ce qui reste consiste à ajouter toocommunicate de code hello avec lui de hello service web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="4ce1c-181">Dans votre projet ASP.NET, ajouter une bibliothèque de classes toohello référence contenant hello `ICounter` interface.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="4ce1c-182">Précédemment, vous avez ajouté hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello projet ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="4ce1c-183">Ce package fournit hello `ServiceProxy` classe que vous pouvez utiliser toomake RPC appelle toohello un service avec état.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="4ce1c-184">Assurez-vous que ce package NuGet est installé dans le projet de service web ASP.NET Core de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="4ce1c-185">Bonjour **contrôleurs** dossier, ouvrez hello `ValuesController` classe.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="4ce1c-186">Notez que hello `Get` méthode retourne actuellement simplement un tableau de chaîne codée en dur de « value1 » et « value2 »--qui correspond à ce que nous avons vu plus haut dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="4ce1c-187">Remplacez cette implémentation hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="4ce1c-187">Replace this implementation with hello following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="4ce1c-188">Hello première ligne de code est la clé hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="4ce1c-189">toocreate hello ICounter proxy toohello service avec état, vous devez tooprovide deux informations : un nom de hello et les ID de partition de service de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="4ce1c-190">Vous pouvez utiliser des services avec état tooscale partitionnement en fractionnant leur état dans des compartiments différents, selon une clé que vous définissez, tel qu’un ID de client ou le code postal.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="4ce1c-191">Dans notre application complexe, un service avec état hello a uniquement une partition, afin de la clé de hello n’a pas d’importance.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="4ce1c-192">N’importe quelle touche que vous fournissez entraîne toohello même partition.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="4ce1c-193">toolearn en savoir plus sur le partitionnement des services, consultez [comment toopartition Service des Services de Fabric fiables](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="4ce1c-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="4ce1c-194">nom du service Hello est un URI de l’infrastructure du formulaire hello : /&lt;application_name&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="4ce1c-195">Avec ces deux types d’informations, l’infrastructure de Service peuvent identifier machine hello qui doivent recevoir les demandes.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="4ce1c-196">Hello `ServiceProxy` classe gère également de façon transparente les cas de hello où hello ordinateur qui héberge la partition de service avec état hello connaît une défaillance et un autre ordinateur doit être promue tootake sa place.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="4ce1c-197">Rend cette abstraction hello toodeal du code client avec d’autres services beaucoup plus simples.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="4ce1c-198">Une fois les proxy hello, nous appelons simplement hello `GetCountAsync` méthode et retourne son résultat.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="4ce1c-199">Appuyez sur F5 à nouveau toorun hello modifié application.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="4ce1c-200">Comme précédemment, Visual Studio lance automatiquement racine de toohello hello navigateur de projet web de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="4ce1c-201">Ajoutez le chemin d’accès de hello « api/valeurs », et vous devez voir hello valeur actuelle du compteur retourné.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![valeur de compteur avec état Hello affiché dans l’Explorateur de hello][browser-aspnet-counter-value]
   
    <span data-ttu-id="4ce1c-203">Actualiser le navigateur de hello régulièrement toosee hello compteur valeur mise à jour.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="4ce1c-204">Kestrel et WebListener</span><span class="sxs-lookup"><span data-stu-id="4ce1c-204">Kestrel and WebListener</span></span>

<span data-ttu-id="4ce1c-205">Bonjour serveur de web ASP.NET Core par défaut, appelé Kestrel, est [non prises en charge pour gérer le trafic internet direct](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="4ce1c-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="4ce1c-206">Par conséquent, hello modèle de service sans état ASP.NET Core pour Service Fabric utilise [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) par défaut.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="4ce1c-207">toolearn en savoir plus sur Kestrel et WebListener dans les services de l’infrastructure de Service, consultez trop[ASP.NET Core dans Service des Services de Fabric fiables](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="4ce1c-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="4ce1c-208">Connexion de service d’acteur fiable tooa</span><span class="sxs-lookup"><span data-stu-id="4ce1c-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="4ce1c-209">Ce didacticiel s'est concentré sur l'ajout d'un serveur web frontal communiquant avec un service avec état.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="4ce1c-210">Toutefois, vous pouvez suivre un tooactors de tootalk modèle très similaires.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="4ce1c-211">Lorsque vous créez un projet Reliable Actor, Visual Studio génère automatiquement un projet d’interface pour vous.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="4ce1c-212">Vous pouvez utiliser ce toogenerate interface un proxy d’acteur dans toocommunicate de projet web hello avec acteur de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="4ce1c-213">canal de communication Hello est fourni automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="4ce1c-214">Vous n’avez pas besoin toodo n’est pas défini qui est équivalent tooestablishing un `ServiceRemotingListener` comme vous l’avez fait pour un service avec état hello dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="4ce1c-215">Fonctionnement des services web sur votre cluster local</span><span class="sxs-lookup"><span data-stu-id="4ce1c-215">How web services work on your local cluster</span></span>
<span data-ttu-id="4ce1c-216">En règle générale, vous pouvez déployer exactement hello même Service Fabric application tooa avec plusieurs ordinateurs de cluster que vous avez déployé votre cluster local et hautement avec la certitude qu’elle fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="4ce1c-217">Il s’agit, car votre cluster local est simplement une configuration de cinq nœuds est réduit tooa un seul ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="4ce1c-218">Lorsqu’il s’agit des services de tooweb, toutefois, il est une nuance de clé.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="4ce1c-219">Lorsque votre cluster se trouve derrière un équilibreur de charge, comme il le fait dans Azure, vous devez vous assurer que vos services web sont déployés sur tous les ordinateurs depuis l’équilibrage de charge hello alternées simplement le trafic sur plusieurs ordinateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="4ce1c-220">Cela en définissant un hello `InstanceCount` pour hello service toohello valeur spéciale « -1 ».</span><span class="sxs-lookup"><span data-stu-id="4ce1c-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="4ce1c-221">En revanche, lorsque vous exécutez un service web localement, vous devez tooensure que seule une instance du service de hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="4ce1c-222">Dans le cas contraire, vous exécutez en conflit à partir de plusieurs processus qui sont à l’écoute sur hello même chemin d’accès et le port.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="4ce1c-223">Par conséquent, le nombre d’instances de hello web service doit être défini trop « 1 » pour les déploiements locaux.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="4ce1c-224">toolearn tooconfigure des valeurs différentes pour un autre environnement, voir [la gestion des paramètres d’application de plusieurs environnements](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="4ce1c-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ce1c-225">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ce1c-225">Next steps</span></span>
<span data-ttu-id="4ce1c-226">Maintenant que vous avez configuré un serveur web frontal pour votre application avec ASP.NET Core, consultez [ASP.NET Core dans le modèle Reliable Services de Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) pour comprendre comment ASP.NET Core fonctionne avec Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="4ce1c-227">Ensuite, [plus d’informations sur la communication avec les services](service-fabric-connect-and-communicate-with-services.md) en général tooget a terminé d’image de la manière dont service communication fonctionne dans l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="4ce1c-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="4ce1c-228">Une fois que vous avez une bonne compréhension du fonctionne de la communication avec le service, [créer un cluster dans Azure et de déployer votre cloud de toohello application](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4ce1c-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows
