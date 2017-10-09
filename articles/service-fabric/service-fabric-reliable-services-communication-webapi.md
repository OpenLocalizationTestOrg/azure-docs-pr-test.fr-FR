---
title: communication aaaService avec hello API Web ASP.NET | Documents Microsoft
description: "Découvrez comment détaillées à l’aide de communication du service tooimplement hello API Web ASP.NET avec OWIN auto-hébergement Bonjour API des Services fiables."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3fb18fcb141ada0d79a0acda3dccbc7fb044346d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="53519-103">Prise en main : services de l’API Web Service Fabric avec auto-hébergement OWIN</span><span class="sxs-lookup"><span data-stu-id="53519-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="53519-104">Azure Service Fabric place power de hello dans vos mains lorsque vous décidez comment vous souhaitez que votre toocommunicate services avec des utilisateurs et entre eux.</span><span class="sxs-lookup"><span data-stu-id="53519-104">Azure Service Fabric puts hello power in your hands when you're deciding how you want your services toocommunicate with users and with each other.</span></span> <span data-ttu-id="53519-105">Ce didacticiel se concentre sur l’implémentation de la communication de service à l’aide de l’API Web ASP.NET avec auto-hébergement OWIN (Open Web Interface for .NET) dans l’API Reliable Services de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="53519-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="53519-106">Nous verrons comment profondément hello communication enfichable de Services fiables API.</span><span class="sxs-lookup"><span data-stu-id="53519-106">We'll delve deeply into hello Reliable Services pluggable communication API.</span></span> <span data-ttu-id="53519-107">Nous allons également utiliser des API Web dans un tooshow exemple pas à pas vous comment tooset d’un écouteur de communication personnalisées.</span><span class="sxs-lookup"><span data-stu-id="53519-107">We'll also use Web API in a step-by-step example tooshow you how tooset up a custom communication listener.</span></span>

## <a name="introduction-tooweb-api-in-service-fabric"></a><span data-ttu-id="53519-108">Introduction tooWeb API dans l’infrastructure de Service</span><span class="sxs-lookup"><span data-stu-id="53519-108">Introduction tooWeb API in Service Fabric</span></span>
<span data-ttu-id="53519-109">API Web ASP.NET est une infrastructure de puissante et populaire pour bâtis APIs HTTP hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="53519-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of hello .NET Framework.</span></span> <span data-ttu-id="53519-110">Si vous n’êtes pas déjà familiarisé avec l’infrastructure de hello, consultez [mise en route avec ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn plus.</span><span class="sxs-lookup"><span data-stu-id="53519-110">If you're not already familiar with hello framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn more.</span></span>

<span data-ttu-id="53519-111">API Web dans le Service Fabric est hello même ASP.NET Web API, vous connaissez et appréciez.</span><span class="sxs-lookup"><span data-stu-id="53519-111">Web API in Service Fabric is hello same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="53519-112">Hello différence réside dans la façon de vous *hôte* une application API Web.</span><span class="sxs-lookup"><span data-stu-id="53519-112">hello difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="53519-113">Vous n’allez pas utiliser Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="53519-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="53519-114">toobetter comprendre la différence de hello, nous allons scindez-la en deux parties :</span><span class="sxs-lookup"><span data-stu-id="53519-114">toobetter understand hello difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="53519-115">application d’API Web Hello (y compris les contrôleurs et les modèles)</span><span class="sxs-lookup"><span data-stu-id="53519-115">hello Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="53519-116">hôte Hello (serveur web hello, généralement IIS)</span><span class="sxs-lookup"><span data-stu-id="53519-116">hello host (hello web server, usually IIS)</span></span>

<span data-ttu-id="53519-117">Une application API Web elle-même ne change pas.</span><span class="sxs-lookup"><span data-stu-id="53519-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="53519-118">Elle ne diffère pas des applications API Web que vous avez écrit Bonjour passées, et vous devez être en mesure de toosimply déplacer sur la plupart du code de votre application.</span><span class="sxs-lookup"><span data-stu-id="53519-118">It's no different from Web API applications you may have written in hello past, and you should be able toosimply move over most of your application code.</span></span> <span data-ttu-id="53519-119">Mais si vous avez été hébergement sur IIS, là où vous hébergez l’application hello peut être un peu différente de ce que vous êtes habitué.</span><span class="sxs-lookup"><span data-stu-id="53519-119">But if you've been hosting on IIS, where you host hello application may be a little different from what you're used to.</span></span> <span data-ttu-id="53519-120">Avant de toohello partie d’hébergement, commençons par quelque chose de plus familiers : hello application d’API Web.</span><span class="sxs-lookup"><span data-stu-id="53519-120">Before we get toohello hosting part, let's start with something more familiar: hello Web API application.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="53519-121">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="53519-121">Create hello application</span></span>
<span data-ttu-id="53519-122">Commencez par créer une application Service Fabric, avec un seul service sans état, dans Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="53519-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="53519-123">Un modèle de Visual Studio pour un service sans état via l’API Web est tooyou disponible.</span><span class="sxs-lookup"><span data-stu-id="53519-123">A Visual Studio template for a stateless service using Web API is available tooyou.</span></span> <span data-ttu-id="53519-124">Dans ce didacticiel, nous allons créer un projet d’API Web qui donnera le même résultat que si vous aviez sélectionné ce modèle.</span><span class="sxs-lookup"><span data-stu-id="53519-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="53519-125">Sélectionnez un toolearn de projet de Service sans état vide comment toobuild un projet d’API Web de toutes pièces, ou si vous démarrez avec un service sans état hello modèle API Web et simplement suivre son déroulement.</span><span class="sxs-lookup"><span data-stu-id="53519-125">Select a blank Stateless Service project toolearn how toobuild a Web API project from scratch, or you can start with hello stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="53519-126">première étape de Hello est toopull dans des packages NuGet pour API Web.</span><span class="sxs-lookup"><span data-stu-id="53519-126">hello first step is toopull in some NuGet packages for Web API.</span></span> <span data-ttu-id="53519-127">package Hello nous souhaitons toouse est Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="53519-127">hello package we want toouse is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="53519-128">Ce package comprend tous les packages d’API Web nécessaires hello et hello *hôte* packages.</span><span class="sxs-lookup"><span data-stu-id="53519-128">This package includes all hello necessary Web API packages and hello *host* packages.</span></span> <span data-ttu-id="53519-129">Ils auront leur importance plus tard.</span><span class="sxs-lookup"><span data-stu-id="53519-129">This will be important later.</span></span>

<span data-ttu-id="53519-130">Après avoir installé les packages hello, vous pouvez commencer la création de structure de projet Web API base hello.</span><span class="sxs-lookup"><span data-stu-id="53519-130">After hello packages have been installed, you can begin building out hello basic Web API project structure.</span></span> <span data-ttu-id="53519-131">Si vous avez utilisé l’API Web, la structure de projet hello doit ressembler très familier.</span><span class="sxs-lookup"><span data-stu-id="53519-131">If you've used Web API, hello project structure should look very familiar.</span></span> <span data-ttu-id="53519-132">Commencez par ajouter un répertoire `Controllers` et un contrôleur de valeurs simple :</span><span class="sxs-lookup"><span data-stu-id="53519-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="53519-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="53519-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="53519-134">Ensuite, ajoutez une classe de démarrage au routage hello projet racine tooregister hello, formateurs et tout autre programme d’installation de configuration.</span><span class="sxs-lookup"><span data-stu-id="53519-134">Next, add a Startup class at hello project root tooregister hello routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="53519-135">Il s’agit également où se branche API Web toohello *hôte*, qui sera revue plus tard.</span><span class="sxs-lookup"><span data-stu-id="53519-135">This is also where Web API plugs in toohello *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="53519-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="53519-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="53519-137">C’est tout pour une partie d’application hello.</span><span class="sxs-lookup"><span data-stu-id="53519-137">That's it for hello application part.</span></span> <span data-ttu-id="53519-138">À ce stade, nous avons configuré simplement hello base API Web disposition du projet.</span><span class="sxs-lookup"><span data-stu-id="53519-138">At this point, we've set up just hello basic Web API project layout.</span></span> <span data-ttu-id="53519-139">Jusqu'à présent, il ne doit pas différer beaucoup de projets d’API Web que peut avoir écrit Bonjour passées ou à partir du modèle d’API Web base hello.</span><span class="sxs-lookup"><span data-stu-id="53519-139">So far, it shouldn't look much different from Web API projects you may have written in hello past or from hello basic Web API template.</span></span> <span data-ttu-id="53519-140">Votre logique métier s’intègre dans les modèles et des contrôleurs de hello, comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="53519-140">Your business logic goes in hello controllers and models as usual.</span></span>

<span data-ttu-id="53519-141">Maintenant que devons-nous faire au niveau de l’hébergement pour pouvoir l’exécuter ?</span><span class="sxs-lookup"><span data-stu-id="53519-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="53519-142">Hébergement du service</span><span class="sxs-lookup"><span data-stu-id="53519-142">Service hosting</span></span>
<span data-ttu-id="53519-143">Dans Service Fabric, votre service s’exécute dans un *processus hôte de service*, c’est-à-dire un fichier exécutable qui exécute le code de votre service.</span><span class="sxs-lookup"><span data-stu-id="53519-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="53519-144">Lorsque vous écrivez un service à l’aide de hello API des Services fiables, votre projet de service compile simplement le fichier exécutable tooan qui inscrit votre type de service et exécute votre code.</span><span class="sxs-lookup"><span data-stu-id="53519-144">When you write a service by using hello Reliable Services API, your service project just compiles tooan executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="53519-145">Ceci se vérifie dans la plupart des cas quand vous écrivez un service sur Service Fabric dans .NET.</span><span class="sxs-lookup"><span data-stu-id="53519-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="53519-146">Lorsque vous ouvrez le fichier Program.cs dans le projet de service sans état hello, vous devez voir :</span><span class="sxs-lookup"><span data-stu-id="53519-146">When you open Program.cs in hello stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="53519-147">Si l’air anormalement hello entrée point tooa console application, qui est, car il est.</span><span class="sxs-lookup"><span data-stu-id="53519-147">If that looks suspiciously like hello entry point tooa console application, that's because it is.</span></span>

<span data-ttu-id="53519-148">Des informations détaillées sur hello processus hôte de service et l’inscription du service sont abordée dans cet article hello.</span><span class="sxs-lookup"><span data-stu-id="53519-148">Further details about hello service host process and service registration are beyond hello scope of this article.</span></span> <span data-ttu-id="53519-149">Mais il est important tooknow pour maintenant que *votre code de service s’exécute dans son propre processus*.</span><span class="sxs-lookup"><span data-stu-id="53519-149">But it's important tooknow for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="53519-150">Auto-héberger l’API Web avec un hôte OWIN</span><span class="sxs-lookup"><span data-stu-id="53519-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="53519-151">Étant donné que le code de votre application d’API Web est hébergé dans son propre processus, comment vous accrochez serveur web de tooa ?</span><span class="sxs-lookup"><span data-stu-id="53519-151">Given that your Web API application code is hosted in its own process, how do you hook it up tooa web server?</span></span> <span data-ttu-id="53519-152">Entrez [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="53519-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="53519-153">OWIN est simplement un contrat entre les applications web .NET et les serveurs web.</span><span class="sxs-lookup"><span data-stu-id="53519-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="53519-154">En règle générale lorsqu’ASP.NET (haut tooMVC 5) est utilisé, application web de hello est étroitement couplées tooIIS via System.Web.</span><span class="sxs-lookup"><span data-stu-id="53519-154">Traditionally when ASP.NET (up tooMVC 5) is used, hello web application is tightly coupled tooIIS through System.Web.</span></span> <span data-ttu-id="53519-155">Toutefois, les API Web implémente OWIN, afin de pouvoir écrire une application web qui est dissociée de serveur web hello qui l’héberge.</span><span class="sxs-lookup"><span data-stu-id="53519-155">However, Web API implements OWIN, so you can write a web application that is decoupled from hello web server that hosts it.</span></span> <span data-ttu-id="53519-156">Pour cette raison, vous pouvez utiliser un serveur web OWIN *auto-hébergé* que vous pouvez démarrer dans votre propre processus.</span><span class="sxs-lookup"><span data-stu-id="53519-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="53519-157">Il s’intègre parfaitement avec hello Service Fabric modèle d’hébergement que nous venons de voir.</span><span class="sxs-lookup"><span data-stu-id="53519-157">This fits perfectly with hello Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="53519-158">Dans cet article, nous allons utiliser Katana en tant qu’hôte OWIN hello pour hello application d’API Web.</span><span class="sxs-lookup"><span data-stu-id="53519-158">In this article, we'll use Katana as hello OWIN host for hello Web API application.</span></span> <span data-ttu-id="53519-159">Katana est une implémentation d’hôte OWIN open source repose sur [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) et hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="53519-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="53519-160">toolearn plus d’informations sur les interconnexions, accédez toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="53519-160">toolearn more about Katana, go toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="53519-161">Pour une présentation rapide de le toouse Katana tooself-hôte Web API, consultez [utilisation OWIN tooSelf-hôte ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="53519-161">For a quick overview of how toouse Katana tooself-host Web API, see [Use OWIN tooSelf-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-hello-web-server"></a><span data-ttu-id="53519-162">Configurer le serveur web de hello</span><span class="sxs-lookup"><span data-stu-id="53519-162">Set up hello web server</span></span>
<span data-ttu-id="53519-163">Hello fiable API des Services fournit un point d’entrée de communication où vous pouvez incorporer dans les piles de communication qui permettent aux utilisateurs et service de clients tooconnect toohello :</span><span class="sxs-lookup"><span data-stu-id="53519-163">hello Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients tooconnect toohello service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="53519-164">serveur web de Hello (et une autre pile de communication que vous utilisez Bonjour futures, telles que les WebSockets) doivent utiliser hello ICommunicationListener interface toointegrate correctement avec hello système.</span><span class="sxs-lookup"><span data-stu-id="53519-164">hello web server (and any other communication stack you use in hello future, such as WebSockets) should use hello ICommunicationListener interface toointegrate correctly with hello system.</span></span> <span data-ttu-id="53519-165">raisons Hello seront deviennent plus évidents Bonjour comme suit.</span><span class="sxs-lookup"><span data-stu-id="53519-165">hello reasons for this will become more apparent in hello following steps.</span></span>

<span data-ttu-id="53519-166">Commencez par créer une classe appelée OwinCommunicationListener qui implémente ICommunicationListener :</span><span class="sxs-lookup"><span data-stu-id="53519-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="53519-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="53519-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="53519-168">interface de ICommunicationListener Hello fournit trois méthodes toomanage un écouteur de communication pour votre service :</span><span class="sxs-lookup"><span data-stu-id="53519-168">hello ICommunicationListener interface provides three methods toomanage a communication listener for your service:</span></span>

* <span data-ttu-id="53519-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="53519-169">*OpenAsync*.</span></span> <span data-ttu-id="53519-170">Commence à écouter les demandes.</span><span class="sxs-lookup"><span data-stu-id="53519-170">Start listening for requests.</span></span>
* <span data-ttu-id="53519-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="53519-171">*CloseAsync*.</span></span> <span data-ttu-id="53519-172">Stoppe l’écoute des demandes, termine toutes les demandes en cours et s’arrête correctement.</span><span class="sxs-lookup"><span data-stu-id="53519-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="53519-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="53519-173">*Abort*.</span></span> <span data-ttu-id="53519-174">Annule tout et s’arrête immédiatement.</span><span class="sxs-lookup"><span data-stu-id="53519-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="53519-175">tooget démarré, ajouter des membres de classe privée pour l’écouteur de choses hello devez toofunction.</span><span class="sxs-lookup"><span data-stu-id="53519-175">tooget started, add private class members for things hello listener will need toofunction.</span></span> <span data-ttu-id="53519-176">Ces seront initialisés via le constructeur de hello et utilisés ultérieurement lorsque vous configurez hello à l’écoute des URL.</span><span class="sxs-lookup"><span data-stu-id="53519-176">These will be initialized through hello constructor and used later when you set up hello listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="53519-177">Implémenter OpenAsync</span><span class="sxs-lookup"><span data-stu-id="53519-177">Implement OpenAsync</span></span>
<span data-ttu-id="53519-178">tooset serveur web de hello, vous avez besoin de deux informations :</span><span class="sxs-lookup"><span data-stu-id="53519-178">tooset up hello web server, you need two pieces of information:</span></span>

* <span data-ttu-id="53519-179">*Préfixe du chemin de l'URL*.</span><span class="sxs-lookup"><span data-stu-id="53519-179">*A URL path prefix*.</span></span> <span data-ttu-id="53519-180">Bien que cette option est facultative, il est approprié pour vous tooset cette jusqu'à maintenant afin que vous pouvez en toute sécurité héberger plusieurs services web dans votre application.</span><span class="sxs-lookup"><span data-stu-id="53519-180">Although this is optional, it's good for you tooset this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="53519-181">*Un port*.</span><span class="sxs-lookup"><span data-stu-id="53519-181">*A port*.</span></span>

<span data-ttu-id="53519-182">Avant d’obtenir un port pour le serveur web de hello, il est important de comprendre que le Service Fabric fournit une couche d’application qui agit comme une mémoire tampon entre votre application et le système d’exploitation sous-jacent hello qu’il exécute sur.</span><span class="sxs-lookup"><span data-stu-id="53519-182">Before you get a port for hello web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and hello underlying operating system that it runs on.</span></span> <span data-ttu-id="53519-183">Par conséquent, Service Fabric fournit un moyen tooconfigure *points de terminaison* pour vos services.</span><span class="sxs-lookup"><span data-stu-id="53519-183">As such, Service Fabric provides a way tooconfigure *endpoints* for your services.</span></span> <span data-ttu-id="53519-184">L’infrastructure de service garantit que les points de terminaison sont disponibles pour votre toouse de service.</span><span class="sxs-lookup"><span data-stu-id="53519-184">Service Fabric ensures that endpoints are available for your service toouse.</span></span> <span data-ttu-id="53519-185">De cette manière, vous n’avez pas tooconfigure les vous-même Bonjour sous-jacent d’environnement du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="53519-185">This way, you don't have tooconfigure them yourself in hello underlying OS environment.</span></span> <span data-ttu-id="53519-186">Vous pouvez facilement héberger votre application de Service Fabric dans différents environnements sans avoir toomake n’importe quelle application tooyour de modifications.</span><span class="sxs-lookup"><span data-stu-id="53519-186">You can easily host your Service Fabric application in different environments without having toomake any changes tooyour application.</span></span> <span data-ttu-id="53519-187">(Par exemple, vous pouvez héberger hello même application dans Azure ou dans votre centre de données.)</span><span class="sxs-lookup"><span data-stu-id="53519-187">(For example, you can host hello same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="53519-188">Configurer un point de terminaison HTTP dans  PackageRoot\ServiceManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="53519-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="53519-189">Cette étape est importante, car le processus hôte de service hello s’exécute sous les informations d’identification limitées (Service réseau sur Windows).</span><span class="sxs-lookup"><span data-stu-id="53519-189">This step is important because hello service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="53519-190">Cela signifie que votre service ne dispose tooset d’accès d’un point de terminaison HTTP sur son propre.</span><span class="sxs-lookup"><span data-stu-id="53519-190">This means that your service won't have access tooset up an HTTP endpoint on its own.</span></span> <span data-ttu-id="53519-191">À l’aide de configuration de point de terminaison hello, Service Fabric sait tooset de liste de contrôle d’accès (ACL) hello pour hello URL hello service écoutera.</span><span class="sxs-lookup"><span data-stu-id="53519-191">By using hello endpoint configuration, Service Fabric knows tooset up hello proper access control list (ACL) for hello URL that hello service will listen on.</span></span> <span data-ttu-id="53519-192">Points de terminaison tooconfigure, service Fabric fournit également un emplacement standard.</span><span class="sxs-lookup"><span data-stu-id="53519-192">Service Fabric also provides a standard place tooconfigure endpoints.</span></span>

<span data-ttu-id="53519-193">De retour dans OwinCommunicationListener.cs, vous pouvez commencer à implémenter OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="53519-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="53519-194">Il s’agit où vous démarrez le serveur web de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-194">This is where you start hello web server.</span></span> <span data-ttu-id="53519-195">Tout d’abord, obtenir des informations de point de terminaison hello et créer des URL de hello hello service écoute sur.</span><span class="sxs-lookup"><span data-stu-id="53519-195">First, get hello endpoint information and create hello URL that hello service will listen on.</span></span> <span data-ttu-id="53519-196">Hello URL sera différente selon que le port d’écoute hello est utilisée dans un service sans état ou d’un service avec état.</span><span class="sxs-lookup"><span data-stu-id="53519-196">hello URL will be different depending on whether hello listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="53519-197">Pour un service avec état, port d’écoute hello doit toocreate unique adresse pour chaque réplica de service avec état. il est à l’écoute sur.</span><span class="sxs-lookup"><span data-stu-id="53519-197">For a stateful service, hello listener needs toocreate a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="53519-198">Pour les services sans état, l’adresse de hello peut être beaucoup plus simple.</span><span class="sxs-lookup"><span data-stu-id="53519-198">For stateless services, hello address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="53519-199">Notez que « http://+ » est utilisé ici.</span><span class="sxs-lookup"><span data-stu-id="53519-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="53519-200">Il s’agit de toomake assurer que le serveur web hello est à l’écoute sur toutes les adresses disponibles, y compris localhost, nom de domaine complet et l’IP hello.</span><span class="sxs-lookup"><span data-stu-id="53519-200">This is toomake sure that hello web server is listening on all available addresses, including localhost, FQDN, and hello machine IP.</span></span>

<span data-ttu-id="53519-201">Hello OpenAsync implémentation est une des raisons les plus importantes hello pourquoi les serveur web de hello (ou une pile de communication) est implémentée comme un ICommunicationListener, plutôt que son ouvre directement à partir de `RunAsync()` dans le service hello.</span><span class="sxs-lookup"><span data-stu-id="53519-201">hello OpenAsync implementation is one of hello most important reasons why hello web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in hello service.</span></span> <span data-ttu-id="53519-202">valeur de retour Hello OpenAsync est adresse hello hello du serveur web est à l’écoute sur.</span><span class="sxs-lookup"><span data-stu-id="53519-202">hello return value from OpenAsync is hello address that hello web server is listening on.</span></span> <span data-ttu-id="53519-203">Lorsque cette adresse est renvoyée toohello système, il enregistre les adresse hello avec service de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-203">When this address is returned toohello system, it registers hello address with hello service.</span></span> <span data-ttu-id="53519-204">L’infrastructure de service fournit une API qui permet aux clients et autres toothen services demandera cette adresse par nom de service.</span><span class="sxs-lookup"><span data-stu-id="53519-204">Service Fabric provides an API that allows clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="53519-205">Ceci est important, car l’adresse du service hello n’est pas statique.</span><span class="sxs-lookup"><span data-stu-id="53519-205">This is important because hello service address is not static.</span></span> <span data-ttu-id="53519-206">Les services sont déplacés dans le cluster hello pour à des fins de disponibilité et de l’équilibrage de la ressource.</span><span class="sxs-lookup"><span data-stu-id="53519-206">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="53519-207">Il s’agit de mécanisme hello qui permet aux clients hello tooresolve adresse pour un service d’écoute.</span><span class="sxs-lookup"><span data-stu-id="53519-207">This is hello mechanism that allows clients tooresolve hello listening address for a service.</span></span>

<span data-ttu-id="53519-208">Dans cette optique, OpenAsync démarre le serveur web de hello et retourne l’adresse hello qu’il écoute.</span><span class="sxs-lookup"><span data-stu-id="53519-208">With that in mind, OpenAsync starts hello web server and returns hello address that it's listening on.</span></span> <span data-ttu-id="53519-209">Notez qu’il écoute sur « http://+ », mais avant OpenAsync renvoie l’adresse de hello, hello « + » est remplacé par hello IP ou nom de domaine complet du nœud hello que cours.</span><span class="sxs-lookup"><span data-stu-id="53519-209">Note that it listens on "http://+", but before OpenAsync returns hello address, hello "+" is replaced with hello IP or FQDN of hello node it is currently on.</span></span> <span data-ttu-id="53519-210">adresse Hello qui est retourné par cette méthode est ce qui est inscrit avec le système de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-210">hello address that is returned by this method is what's registered with hello system.</span></span> <span data-ttu-id="53519-211">Il s’agit également de celle que les clients et autres services voient quand ils recherchent l’adresse d’un service.</span><span class="sxs-lookup"><span data-stu-id="53519-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="53519-212">Pour les clients toocorrectly connexion tooit, ils ont besoin d’une adresse IP ou le nom de domaine complet réel dans l’adresse de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-212">For clients toocorrectly connect tooit, they need an actual IP or FQDN in hello address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="53519-213">Notez que cela fait référence à la classe de démarrage hello qui a été passé dans toohello OwinCommunicationListener dans le constructeur de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-213">Note that this references hello Startup class that was passed in toohello OwinCommunicationListener in hello constructor.</span></span> <span data-ttu-id="53519-214">Cette instance de démarrage est utilisée par les messages hello toobootstrap du serveur hello web application d’API Web.</span><span class="sxs-lookup"><span data-stu-id="53519-214">This startup instance is used by hello web server toobootstrap hello Web API application.</span></span>

<span data-ttu-id="53519-215">Hello `ServiceEventSource.Current.Message()` ligne apparaît dans la fenêtre des événements de Diagnostic hello plus tard, lorsque vous exécutez hello application tooconfirm que le serveur web hello a démarré avec succès.</span><span class="sxs-lookup"><span data-stu-id="53519-215">hello `ServiceEventSource.Current.Message()` line will appear in hello Diagnostic Events window later, when you run hello application tooconfirm that hello web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="53519-216">Implémenter CloseAsync et Abort</span><span class="sxs-lookup"><span data-stu-id="53519-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="53519-217">Enfin, implémentez CloseAsync et Abort serveur web de hello toostop.</span><span class="sxs-lookup"><span data-stu-id="53519-217">Finally, implement both CloseAsync and Abort toostop hello web server.</span></span> <span data-ttu-id="53519-218">serveur web de Hello peut être arrêtée en supprimant le handle de serveur hello qui a été créé au cours de OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="53519-218">hello web server can be stopped by disposing hello server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="53519-219">Dans cet exemple d’implémentation, CloseAsync et Abort simplement arrêteront le serveur web de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-219">In this implementation example, both CloseAsync and Abort simply stop hello web server.</span></span> <span data-ttu-id="53519-220">Vous pouvez choisir tooperform un arrêt plus naturellement coordonné de serveur web hello CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="53519-220">You may opt tooperform a more gracefully coordinated shutdown of hello web server in CloseAsync.</span></span> <span data-ttu-id="53519-221">Par exemple, l’arrêt hello pouvait attendre de toobe de demandes en cours s’est terminée avant de retourner de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-221">For example, hello shutdown could wait for in-flight requests toobe completed before hello return.</span></span>

## <a name="start-hello-web-server"></a><span data-ttu-id="53519-222">Démarrer le serveur web de hello</span><span class="sxs-lookup"><span data-stu-id="53519-222">Start hello web server</span></span>
<span data-ttu-id="53519-223">Vous êtes maintenant prêt toocreate et retournez une instance de serveur web de OwinCommunicationListener toostart hello.</span><span class="sxs-lookup"><span data-stu-id="53519-223">You're now ready toocreate and return an instance of OwinCommunicationListener toostart hello web server.</span></span> <span data-ttu-id="53519-224">Dans la classe de Service (WebService.cs) de hello, substituez hello `CreateServiceInstanceListeners()` méthode :</span><span class="sxs-lookup"><span data-stu-id="53519-224">Back in hello Service class (WebService.cs), override hello `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="53519-225">Cela est hello où les API Web *application* et hello OWIN *hôte* enfin respecter.</span><span class="sxs-lookup"><span data-stu-id="53519-225">This is where hello Web API *application* and hello OWIN *host* finally meet.</span></span> <span data-ttu-id="53519-226">l’hôte Hello (OwinCommunicationListener) est une instance donnée de hello *application* (API Web) via hello classe de démarrage.</span><span class="sxs-lookup"><span data-stu-id="53519-226">hello host (OwinCommunicationListener) is given an instance of hello *application* (Web API) via hello Startup class.</span></span> <span data-ttu-id="53519-227">Ensuite, Service Fabric gère son cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="53519-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="53519-228">Ce même modèle peut généralement être suivi d'une pile de communication.</span><span class="sxs-lookup"><span data-stu-id="53519-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="53519-229">Assemblage</span><span class="sxs-lookup"><span data-stu-id="53519-229">Put it all together</span></span>
<span data-ttu-id="53519-230">Dans cet exemple, vous n’avez pas besoin toodo n’est pas défini dans hello `RunAsync()` méthode, donc ce remplacement peut être simplement supprimé.</span><span class="sxs-lookup"><span data-stu-id="53519-230">In this example, you don't need toodo anything in hello `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="53519-231">implémentation du service final Hello doit être très simple.</span><span class="sxs-lookup"><span data-stu-id="53519-231">hello final service implementation should be very simple.</span></span> <span data-ttu-id="53519-232">Il n’a besoin que d’écouteur de communications toocreate hello :</span><span class="sxs-lookup"><span data-stu-id="53519-232">It only needs toocreate hello communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="53519-233">Hello complète `OwinCommunicationListener` classe :</span><span class="sxs-lookup"><span data-stu-id="53519-233">hello complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed tooopen endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="53519-234">Maintenant que vous avez placé tous les éléments de hello en place, votre projet doit ressembler à une application Web API standard avec les points d’entrée de l’API des Services fiables et un hôte OWIN.</span><span class="sxs-lookup"><span data-stu-id="53519-234">Now that you have put all hello pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="53519-235">Exécuter et se connecter via un navigateur web</span><span class="sxs-lookup"><span data-stu-id="53519-235">Run and connect through a web browser</span></span>
<span data-ttu-id="53519-236">Si ce n'est déjà fait, [configurez votre environnement de développement](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="53519-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="53519-237">Vous pouvez désormais générer et déployer votre service.</span><span class="sxs-lookup"><span data-stu-id="53519-237">You can now build and deploy your service.</span></span> <span data-ttu-id="53519-238">Appuyez sur **F5** dans Visual Studio toobuild et déployer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="53519-238">Press **F5** in Visual Studio toobuild and deploy hello application.</span></span> <span data-ttu-id="53519-239">Dans la fenêtre des événements de Diagnostic hello, vous devez voir un message qui indique que le serveur web hello ouvert sur http://localhost:8281 /.</span><span class="sxs-lookup"><span data-stu-id="53519-239">In hello Diagnostic Events window, you should see a message that indicates that hello web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="53519-240">Si le port de hello a déjà été ouvert par un autre processus sur votre ordinateur, vous pouvez voir ici une erreur.</span><span class="sxs-lookup"><span data-stu-id="53519-240">If hello port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="53519-241">Cela indique que cet écouteur hello n’a pas pu être ouvert.</span><span class="sxs-lookup"><span data-stu-id="53519-241">This indicates that hello listener couldn't be opened.</span></span> <span data-ttu-id="53519-242">Si tel est le cas de hello, essayez d’utiliser un port différent pour la configuration de point de terminaison hello dans ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="53519-242">If that's hello case, try using a different port for hello endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="53519-243">Une fois que le service de hello est en cours d’exécution, ouvrez un navigateur et accédez trop[http://localhost:8281/api/valeurs](http://localhost:8281/api/values) tootest il.</span><span class="sxs-lookup"><span data-stu-id="53519-243">Once hello service is running, open a browser and navigate too[http://localhost:8281/api/values](http://localhost:8281/api/values) tootest it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="53519-244">Montée en charge</span><span class="sxs-lookup"><span data-stu-id="53519-244">Scale it out</span></span>
<span data-ttu-id="53519-245">Évolution généralement d’applications web sans état signifie l’ajout de plusieurs ordinateurs et lancer des applications web hello sur les.</span><span class="sxs-lookup"><span data-stu-id="53519-245">Scaling out stateless web apps typically means adding more machines and spinning up hello web apps on them.</span></span> <span data-ttu-id="53519-246">Moteur d’orchestration de l’infrastructure de service peut faire cela pour vous chaque fois que les nouveaux nœuds sont ajoutés tooa cluster.</span><span class="sxs-lookup"><span data-stu-id="53519-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added tooa cluster.</span></span> <span data-ttu-id="53519-247">Lorsque vous créez des instances d’un service sans état, vous pouvez spécifier le nombre de hello d’instances, vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="53519-247">When you create instances of a stateless service, you can specify hello number of instances you want toocreate.</span></span> <span data-ttu-id="53519-248">L’infrastructure de service place ce nombre d’instances sur des nœuds de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-248">Service Fabric places that number of instances on nodes in hello cluster.</span></span> <span data-ttu-id="53519-249">Et il permet de s’assurer toocreate pas plus d’une instance sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="53519-249">And it makes sure not toocreate more than one instance on any one node.</span></span> <span data-ttu-id="53519-250">Vous pouvez également demander à Service Fabric tooalways créer une instance sur chaque nœud, en spécifiant **-1** pour le nombre d’instances hello.</span><span class="sxs-lookup"><span data-stu-id="53519-250">You can also instruct Service Fabric tooalways create an instance on every node by specifying **-1** for hello instance count.</span></span> <span data-ttu-id="53519-251">Cela garantit que chaque fois que vous ajoutez des nœuds tooscale à votre cluster, une instance de votre service sans état est créée sur les nouveaux nœuds de hello.</span><span class="sxs-lookup"><span data-stu-id="53519-251">This guarantees that whenever you add nodes tooscale out your cluster, an instance of your stateless service will be created on hello new nodes.</span></span> <span data-ttu-id="53519-252">Cette valeur est une propriété d’instance de service hello, donc elle est définie lorsque vous créez une instance de service.</span><span class="sxs-lookup"><span data-stu-id="53519-252">This value is a property of hello service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="53519-253">Pour ce faire, vous pouvez utiliser PowerShell :</span><span class="sxs-lookup"><span data-stu-id="53519-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="53519-254">Vous pouvez également le faire quand vous définissez un service par défaut dans un projet de service sans état Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="53519-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="53519-255">Pour plus d’informations sur comment toocreate application et les instances de service, consultez [déployer une application](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="53519-255">For more information on how toocreate application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="53519-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53519-256">Next steps</span></span>
[<span data-ttu-id="53519-257">Débogage de votre application Service Fabric à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53519-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

