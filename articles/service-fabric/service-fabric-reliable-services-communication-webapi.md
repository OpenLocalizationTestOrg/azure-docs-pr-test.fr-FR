---
title: "Communication de service avec l’API Web ASP.NET | Microsoft Docs"
description: "Découvrez comment implémenter progressivement une communication de service à l’aide de l’API Web ASP.NET avec auto-hébergement OWIN dans l’API Reliable Services."
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
ms.openlocfilehash: 73b7e1c0cb93ae7c54780a3aab837b0e5bcdb0a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="596f1-103">Prise en main : services de l’API Web Service Fabric avec auto-hébergement OWIN</span><span class="sxs-lookup"><span data-stu-id="596f1-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="596f1-104">Azure Service Fabric vous laisse librement choisir comment vos services communiqueront avec les utilisateurs et entre eux.</span><span class="sxs-lookup"><span data-stu-id="596f1-104">Azure Service Fabric puts the power in your hands when you're deciding how you want your services to communicate with users and with each other.</span></span> <span data-ttu-id="596f1-105">Ce didacticiel se concentre sur l’implémentation de la communication de service à l’aide de l’API Web ASP.NET avec auto-hébergement OWIN (Open Web Interface for .NET) dans l’API Reliable Services de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="596f1-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="596f1-106">Nous allons approfondir l’étude de l’API de communication enfichable Reliable Services.</span><span class="sxs-lookup"><span data-stu-id="596f1-106">We'll delve deeply into the Reliable Services pluggable communication API.</span></span> <span data-ttu-id="596f1-107">Nous utiliserons également l’API Web dans un exemple pas à pas pour vous montrer comment configurer un écouteur de communication personnalisé.</span><span class="sxs-lookup"><span data-stu-id="596f1-107">We'll also use Web API in a step-by-step example to show you how to set up a custom communication listener.</span></span>

## <a name="introduction-to-web-api-in-service-fabric"></a><span data-ttu-id="596f1-108">Présentation de l’API Web dans Service Fabric</span><span class="sxs-lookup"><span data-stu-id="596f1-108">Introduction to Web API in Service Fabric</span></span>
<span data-ttu-id="596f1-109">L'API Web ASP.NET est une infrastructure populaire et puissante pour la création d'API HTTP sur l'infrastructure .NET.</span><span class="sxs-lookup"><span data-stu-id="596f1-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of the .NET Framework.</span></span> <span data-ttu-id="596f1-110">Si vous ne connaissez pas déjà cette infrastructure, consultez [Prise en main d’API Web ASP.NET 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="596f1-110">If you're not already familiar with the framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) to learn more.</span></span>

<span data-ttu-id="596f1-111">L'API Web dans Service Fabric est la même API Web ASP.NET que vous connaissez et appréciez.</span><span class="sxs-lookup"><span data-stu-id="596f1-111">Web API in Service Fabric is the same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="596f1-112">La différence réside dans la manière d’ *héberger* une application API Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-112">The difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="596f1-113">Vous n’allez pas utiliser Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="596f1-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="596f1-114">Pour mieux comprendre la différence, nous allons la décomposer en deux parties :</span><span class="sxs-lookup"><span data-stu-id="596f1-114">To better understand the difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="596f1-115">L’application API Web (y compris les contrôleurs et les modèles)</span><span class="sxs-lookup"><span data-stu-id="596f1-115">The Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="596f1-116">L'hôte (le serveur web, généralement IIS)</span><span class="sxs-lookup"><span data-stu-id="596f1-116">The host (the web server, usually IIS)</span></span>

<span data-ttu-id="596f1-117">Une application API Web elle-même ne change pas.</span><span class="sxs-lookup"><span data-stu-id="596f1-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="596f1-118">Elle ne diffère pas des applications API Web que vous avez éventuellement écrites par le passé, et vous devriez pouvoir facilement réutiliser la plupart du code de votre application.</span><span class="sxs-lookup"><span data-stu-id="596f1-118">It's no different from Web API applications you may have written in the past, and you should be able to simply move over most of your application code.</span></span> <span data-ttu-id="596f1-119">Mais si vous avez utilisé un hébergement sur IIS, l’emplacement auquel vous hébergez l’application risque d’être légèrement différent de celui auquel vous êtes habitué.</span><span class="sxs-lookup"><span data-stu-id="596f1-119">But if you've been hosting on IIS, where you host the application may be a little different from what you're used to.</span></span> <span data-ttu-id="596f1-120">Avant de passer à la partie sur l’hébergement, commençons par la partie la plus connue : l’application API Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-120">Before we get to the hosting part, let's start with something more familiar: the Web API application.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="596f1-121">Création de l'application</span><span class="sxs-lookup"><span data-stu-id="596f1-121">Create the application</span></span>
<span data-ttu-id="596f1-122">Commencez par créer une application Service Fabric, avec un seul service sans état, dans Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="596f1-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="596f1-123">Vous avez à votre disposition un modèle Visual Studio pour un service sans état utilisant une API Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-123">A Visual Studio template for a stateless service using Web API is available to you.</span></span> <span data-ttu-id="596f1-124">Dans ce didacticiel, nous allons créer un projet d’API Web qui donnera le même résultat que si vous aviez sélectionné ce modèle.</span><span class="sxs-lookup"><span data-stu-id="596f1-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="596f1-125">Sélectionnez un projet Service sans état vide pour découvrir comment créer un projet d’API Web, ou vous pouvez commencer avec le modèle d’API Web de service sans état et suivre simplement la procédure indiquée.</span><span class="sxs-lookup"><span data-stu-id="596f1-125">Select a blank Stateless Service project to learn how to build a Web API project from scratch, or you can start with the stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="596f1-126">La première étape consiste à extraire certains packages NuGet pour l'API Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-126">The first step is to pull in some NuGet packages for Web API.</span></span> <span data-ttu-id="596f1-127">Le package que nous voulons utiliser est Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="596f1-127">The package we want to use is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="596f1-128">Ce package comprend tous les packages d’API Web et les packages *hôtes* nécessaires.</span><span class="sxs-lookup"><span data-stu-id="596f1-128">This package includes all the necessary Web API packages and the *host* packages.</span></span> <span data-ttu-id="596f1-129">Ils auront leur importance plus tard.</span><span class="sxs-lookup"><span data-stu-id="596f1-129">This will be important later.</span></span>

<span data-ttu-id="596f1-130">Avec les packages installés, vous pouvez commencer à créer la structure de base du projet d’API Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-130">After the packages have been installed, you can begin building out the basic Web API project structure.</span></span> <span data-ttu-id="596f1-131">Si vous avez déjà utilisé des API Web, la structure du projet doit sembler très familière.</span><span class="sxs-lookup"><span data-stu-id="596f1-131">If you've used Web API, the project structure should look very familiar.</span></span> <span data-ttu-id="596f1-132">Commencez par ajouter un répertoire `Controllers` et un contrôleur de valeurs simple :</span><span class="sxs-lookup"><span data-stu-id="596f1-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="596f1-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="596f1-133">**ValuesController.cs**</span></span>

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

<span data-ttu-id="596f1-134">Ensuite, ajoutez une classe de démarrage à la racine du projet pour inscrire le routage, les formateurs et tout autre programme d’installation de configuration.</span><span class="sxs-lookup"><span data-stu-id="596f1-134">Next, add a Startup class at the project root to register the routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="596f1-135">C'est également depuis cet endroit que l'API Web se connecte à l'*hôte*, ce que nous reverrons ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="596f1-135">This is also where Web API plugs in to the *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="596f1-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="596f1-136">**Startup.cs**</span></span>

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

<span data-ttu-id="596f1-137">C'est tout pour la partie de l'application.</span><span class="sxs-lookup"><span data-stu-id="596f1-137">That's it for the application part.</span></span> <span data-ttu-id="596f1-138">À ce stade, nous avons simplement configuré la disposition du projet de base de l’API Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-138">At this point, we've set up just the basic Web API project layout.</span></span> <span data-ttu-id="596f1-139">Jusqu’ici, comparé aux projets d’API Web que vous avez éventuellement écrits par le passé ou au modèle d’API Web de base, ce projet ne doit pas avoir l’air très différent.</span><span class="sxs-lookup"><span data-stu-id="596f1-139">So far, it shouldn't look much different from Web API projects you may have written in the past or from the basic Web API template.</span></span> <span data-ttu-id="596f1-140">Votre logique métier est appliquée comme d'habitude aux contrôleurs et aux modèles.</span><span class="sxs-lookup"><span data-stu-id="596f1-140">Your business logic goes in the controllers and models as usual.</span></span>

<span data-ttu-id="596f1-141">Maintenant que devons-nous faire au niveau de l’hébergement pour pouvoir l’exécuter ?</span><span class="sxs-lookup"><span data-stu-id="596f1-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="596f1-142">Hébergement du service</span><span class="sxs-lookup"><span data-stu-id="596f1-142">Service hosting</span></span>
<span data-ttu-id="596f1-143">Dans Service Fabric, votre service s’exécute dans un *processus hôte de service*, c’est-à-dire un fichier exécutable qui exécute le code de votre service.</span><span class="sxs-lookup"><span data-stu-id="596f1-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="596f1-144">Quand vous écrivez un service à l’aide de l’API Reliable Services, votre projet de service se compile juste en un fichier exécutable qui inscrit votre type de service et exécute votre code.</span><span class="sxs-lookup"><span data-stu-id="596f1-144">When you write a service by using the Reliable Services API, your service project just compiles to an executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="596f1-145">Ceci se vérifie dans la plupart des cas quand vous écrivez un service sur Service Fabric dans .NET.</span><span class="sxs-lookup"><span data-stu-id="596f1-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="596f1-146">Quand vous ouvrez Program.cs dans le projet de service sans état, vous devriez voir :</span><span class="sxs-lookup"><span data-stu-id="596f1-146">When you open Program.cs in the stateless service project, you should see:</span></span>

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

<span data-ttu-id="596f1-147">Si cela ressemble étrangement au point d'entrée d'une application console, c'est parce c'est le cas.</span><span class="sxs-lookup"><span data-stu-id="596f1-147">If that looks suspiciously like the entry point to a console application, that's because it is.</span></span>

<span data-ttu-id="596f1-148">Il n’appartient pas à cet article de donner plus de détails sur le processus hôte de service et l’inscription du service.</span><span class="sxs-lookup"><span data-stu-id="596f1-148">Further details about the service host process and service registration are beyond the scope of this article.</span></span> <span data-ttu-id="596f1-149">Mais il est important de savoir à ce stade que *votre code de service s’exécute dans son propre processus*.</span><span class="sxs-lookup"><span data-stu-id="596f1-149">But it's important to know for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="596f1-150">Auto-héberger l’API Web avec un hôte OWIN</span><span class="sxs-lookup"><span data-stu-id="596f1-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="596f1-151">Étant donné que le code de votre application API Web est hébergé dans son propre processus, comment se connecter à un serveur web ?</span><span class="sxs-lookup"><span data-stu-id="596f1-151">Given that your Web API application code is hosted in its own process, how do you hook it up to a web server?</span></span> <span data-ttu-id="596f1-152">Entrez [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="596f1-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="596f1-153">OWIN est simplement un contrat entre les applications web .NET et les serveurs web.</span><span class="sxs-lookup"><span data-stu-id="596f1-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="596f1-154">Traditionnellement avec ASP.NET (jusqu’à MVC 5), l’application web est étroitement liée à IIS via System.Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-154">Traditionally when ASP.NET (up to MVC 5) is used, the web application is tightly coupled to IIS through System.Web.</span></span> <span data-ttu-id="596f1-155">Toutefois, l’API Web implémente OWIN, ce qui vous permet d’écrire une application web dissociée du serveur web qui l’héberge.</span><span class="sxs-lookup"><span data-stu-id="596f1-155">However, Web API implements OWIN, so you can write a web application that is decoupled from the web server that hosts it.</span></span> <span data-ttu-id="596f1-156">Pour cette raison, vous pouvez utiliser un serveur web OWIN *auto-hébergé* que vous pouvez démarrer dans votre propre processus.</span><span class="sxs-lookup"><span data-stu-id="596f1-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="596f1-157">Il s’intègre parfaitement avec le modèle d’hébergement Service Fabric que nous venons de décrire.</span><span class="sxs-lookup"><span data-stu-id="596f1-157">This fits perfectly with the Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="596f1-158">Dans cet article, nous utiliserons Katana comme hôte OWIN pour l'application de l'API Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-158">In this article, we'll use Katana as the OWIN host for the Web API application.</span></span> <span data-ttu-id="596f1-159">Katana est une implémentation d’hôte OWIN open source basée sur [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) et sur l’[API de serveur HTTP](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx) de Windows.</span><span class="sxs-lookup"><span data-stu-id="596f1-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and the Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="596f1-160">Pour en savoir plus sur Katana, accédez au [site Katana](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="596f1-160">To learn more about Katana, go to the [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="596f1-161">Pour obtenir un aperçu rapide de l’utilisation de Katana pour auto-héberger l’API Web, consultez [Use OWIN to Self-Host ASP.NET Web API (Utiliser OWIN pour auto-héberger une API Web ASP.NET 2)](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="596f1-161">For a quick overview of how to use Katana to self-host Web API, see [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-the-web-server"></a><span data-ttu-id="596f1-162">Configurer le serveur web</span><span class="sxs-lookup"><span data-stu-id="596f1-162">Set up the web server</span></span>
<span data-ttu-id="596f1-163">L’API Reliable Services fournit un point d’entrée de communication dans lequel vous pouvez connecter des piles de communication pour permettre à des utilisateurs et à des clients de se connecter au service :</span><span class="sxs-lookup"><span data-stu-id="596f1-163">The Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients to connect to the service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="596f1-164">Le serveur web (et toute autre pile de communication que vous pouvez utiliser à l’avenir, comme WebSockets) doit utiliser l’interface ICommunicationListener pour s’intégrer correctement au système.</span><span class="sxs-lookup"><span data-stu-id="596f1-164">The web server (and any other communication stack you use in the future, such as WebSockets) should use the ICommunicationListener interface to integrate correctly with the system.</span></span> <span data-ttu-id="596f1-165">Les raisons de cette mesure deviendront plus évidentes dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="596f1-165">The reasons for this will become more apparent in the following steps.</span></span>

<span data-ttu-id="596f1-166">Commencez par créer une classe appelée OwinCommunicationListener qui implémente ICommunicationListener :</span><span class="sxs-lookup"><span data-stu-id="596f1-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="596f1-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="596f1-167">**OwinCommunicationListener.cs**</span></span>

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

<span data-ttu-id="596f1-168">L'interface ICommunicationListener fournit trois méthodes permettant de gérer un écouteur de communication pour votre service :</span><span class="sxs-lookup"><span data-stu-id="596f1-168">The ICommunicationListener interface provides three methods to manage a communication listener for your service:</span></span>

* <span data-ttu-id="596f1-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="596f1-169">*OpenAsync*.</span></span> <span data-ttu-id="596f1-170">Commence à écouter les demandes.</span><span class="sxs-lookup"><span data-stu-id="596f1-170">Start listening for requests.</span></span>
* <span data-ttu-id="596f1-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="596f1-171">*CloseAsync*.</span></span> <span data-ttu-id="596f1-172">Stoppe l’écoute des demandes, termine toutes les demandes en cours et s’arrête correctement.</span><span class="sxs-lookup"><span data-stu-id="596f1-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="596f1-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="596f1-173">*Abort*.</span></span> <span data-ttu-id="596f1-174">Annule tout et s’arrête immédiatement.</span><span class="sxs-lookup"><span data-stu-id="596f1-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="596f1-175">Pour commencer, ajoutez les membres de classe privée pour les éléments dont l’écouteur a besoin pour fonctionner.</span><span class="sxs-lookup"><span data-stu-id="596f1-175">To get started, add private class members for things the listener will need to function.</span></span> <span data-ttu-id="596f1-176">Ces éléments sont initialisés par le biais du constructeur et utilisés ultérieurement quand vous configurez l’URL d’écoute.</span><span class="sxs-lookup"><span data-stu-id="596f1-176">These will be initialized through the constructor and used later when you set up the listening URL.</span></span>

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

## <a name="implement-openasync"></a><span data-ttu-id="596f1-177">Implémenter OpenAsync</span><span class="sxs-lookup"><span data-stu-id="596f1-177">Implement OpenAsync</span></span>
<span data-ttu-id="596f1-178">Pour configurer le serveur web, vous avez besoin de deux informations :</span><span class="sxs-lookup"><span data-stu-id="596f1-178">To set up the web server, you need two pieces of information:</span></span>

* <span data-ttu-id="596f1-179">*Préfixe du chemin de l'URL*.</span><span class="sxs-lookup"><span data-stu-id="596f1-179">*A URL path prefix*.</span></span> <span data-ttu-id="596f1-180">Bien que facultatif, il est judicieux de le configurer maintenant pour pouvoir héberger en toute sécurité plusieurs services web dans votre application.</span><span class="sxs-lookup"><span data-stu-id="596f1-180">Although this is optional, it's good for you to set this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="596f1-181">*Un port*.</span><span class="sxs-lookup"><span data-stu-id="596f1-181">*A port*.</span></span>

<span data-ttu-id="596f1-182">Avant d’obtenir un port pour le serveur web, il est important de comprendre que Service Fabric fournit une couche Application qui sert de tampon entre votre application et le système d’exploitation sous-jacent sur lequel elle s’exécute.</span><span class="sxs-lookup"><span data-stu-id="596f1-182">Before you get a port for the web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and the underlying operating system that it runs on.</span></span> <span data-ttu-id="596f1-183">Par conséquent, Service Fabric permet de configurer des *points de terminaison* pour vos services.</span><span class="sxs-lookup"><span data-stu-id="596f1-183">As such, Service Fabric provides a way to configure *endpoints* for your services.</span></span> <span data-ttu-id="596f1-184">Service Fabric garantit la disponibilité des points de terminaison pour votre service.</span><span class="sxs-lookup"><span data-stu-id="596f1-184">Service Fabric ensures that endpoints are available for your service to use.</span></span> <span data-ttu-id="596f1-185">Ainsi, vous n’êtes pas obligé de les configurer vous-même dans l’environnement du système d’exploitation sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="596f1-185">This way, you don't have to configure them yourself in the underlying OS environment.</span></span> <span data-ttu-id="596f1-186">Vous pouvez facilement héberger votre application Service Fabric dans différents environnements sans avoir à apporter de modifications à votre application.</span><span class="sxs-lookup"><span data-stu-id="596f1-186">You can easily host your Service Fabric application in different environments without having to make any changes to your application.</span></span> <span data-ttu-id="596f1-187">(Par exemple, vous pouvez héberger la même application dans Azure ou dans votre propre centre de données).</span><span class="sxs-lookup"><span data-stu-id="596f1-187">(For example, you can host the same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="596f1-188">Configurer un point de terminaison HTTP dans  PackageRoot\ServiceManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="596f1-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="596f1-189">Cette étape est importante car le processus hôte de service s’exécute sous des informations d’identification limitées (Service réseau sous Windows).</span><span class="sxs-lookup"><span data-stu-id="596f1-189">This step is important because the service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="596f1-190">Cela signifie que votre service n’a pas d’accès pour configurer un point de terminaison HTTP tout seul.</span><span class="sxs-lookup"><span data-stu-id="596f1-190">This means that your service won't have access to set up an HTTP endpoint on its own.</span></span> <span data-ttu-id="596f1-191">En utilisant la configuration du point de terminaison, Service Fabric sait comment configurer la liste de contrôle d’accès (ACL) pour l’URL que le service va écouter.</span><span class="sxs-lookup"><span data-stu-id="596f1-191">By using the endpoint configuration, Service Fabric knows to set up the proper access control list (ACL) for the URL that the service will listen on.</span></span> <span data-ttu-id="596f1-192">Service Fabric fournit également un emplacement standard pour configurer des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="596f1-192">Service Fabric also provides a standard place to configure endpoints.</span></span>

<span data-ttu-id="596f1-193">De retour dans OwinCommunicationListener.cs, vous pouvez commencer à implémenter OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="596f1-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="596f1-194">C’est ici que vous démarrez le serveur web.</span><span class="sxs-lookup"><span data-stu-id="596f1-194">This is where you start the web server.</span></span> <span data-ttu-id="596f1-195">Tout d'abord, récupérez les informations du point de terminaison et créez l'URL sur laquelle le service écoutera.</span><span class="sxs-lookup"><span data-stu-id="596f1-195">First, get the endpoint information and create the URL that the service will listen on.</span></span> <span data-ttu-id="596f1-196">L’URL sera différente selon que l’écouteur est utilisé dans un service sans état ou un service avec état.</span><span class="sxs-lookup"><span data-stu-id="596f1-196">The URL will be different depending on whether the listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="596f1-197">Pour un service avec état, l’écouteur doit créer une adresse unique pour chaque réplica de service avec état qu’il écoute.</span><span class="sxs-lookup"><span data-stu-id="596f1-197">For a stateful service, the listener needs to create a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="596f1-198">Pour les services sans état, l’adresse peut être beaucoup plus simple.</span><span class="sxs-lookup"><span data-stu-id="596f1-198">For stateless services, the address can be much simpler.</span></span> 

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

<span data-ttu-id="596f1-199">Notez que « http://+ » est utilisé ici.</span><span class="sxs-lookup"><span data-stu-id="596f1-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="596f1-200">Cette opération permet de s’assurer que le serveur web écoute toutes les adresses disponibles, y compris l’hôte local, le nom de domaine complet et l’adresse IP de l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="596f1-200">This is to make sure that the web server is listening on all available addresses, including localhost, FQDN, and the machine IP.</span></span>

<span data-ttu-id="596f1-201">L’implémentation d’OpenAsync est l’une des principales raisons pour lesquelles le serveur web (ou une pile de communication) est implémenté comme élément ICommunicationListener au lieu d’être simplement ouvert directement à partir de `RunAsync()` dans le service.</span><span class="sxs-lookup"><span data-stu-id="596f1-201">The OpenAsync implementation is one of the most important reasons why the web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in the service.</span></span> <span data-ttu-id="596f1-202">La valeur de retour d'OpenAsync est l'adresse sur laquelle le serveur web écoute.</span><span class="sxs-lookup"><span data-stu-id="596f1-202">The return value from OpenAsync is the address that the web server is listening on.</span></span> <span data-ttu-id="596f1-203">Lorsque cette adresse est renvoyée au système, elle enregistre auprès du service.</span><span class="sxs-lookup"><span data-stu-id="596f1-203">When this address is returned to the system, it registers the address with the service.</span></span> <span data-ttu-id="596f1-204">Service Fabric fournit une API qui permet aux clients et à d’autres services de rechercher cette adresse par nom de service.</span><span class="sxs-lookup"><span data-stu-id="596f1-204">Service Fabric provides an API that allows clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="596f1-205">Ceci est important, car l’adresse du service n’est pas statique.</span><span class="sxs-lookup"><span data-stu-id="596f1-205">This is important because the service address is not static.</span></span> <span data-ttu-id="596f1-206">Les services se déplacent dans le cluster à des fins d’équilibrage des ressources et de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="596f1-206">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="596f1-207">Ce mécanisme permet aux clients de résoudre l'adresse d'écoute pour un service.</span><span class="sxs-lookup"><span data-stu-id="596f1-207">This is the mechanism that allows clients to resolve the listening address for a service.</span></span>

<span data-ttu-id="596f1-208">Dans cette optique, OpenAsync démarre le serveur web et retourne l’adresse qu’il écoute.</span><span class="sxs-lookup"><span data-stu-id="596f1-208">With that in mind, OpenAsync starts the web server and returns the address that it's listening on.</span></span> <span data-ttu-id="596f1-209">Notez qu’il écoute « http://+ », mais avant qu’OpenAsync ne retourne l’adresse, le « + » est remplacé par l’adresse IP ou le nom de domaine complet du nœud actuel.</span><span class="sxs-lookup"><span data-stu-id="596f1-209">Note that it listens on "http://+", but before OpenAsync returns the address, the "+" is replaced with the IP or FQDN of the node it is currently on.</span></span> <span data-ttu-id="596f1-210">L’adresse retournée par cette méthode est celle enregistrée dans le système.</span><span class="sxs-lookup"><span data-stu-id="596f1-210">The address that is returned by this method is what's registered with the system.</span></span> <span data-ttu-id="596f1-211">Il s’agit également de celle que les clients et autres services voient quand ils recherchent l’adresse d’un service.</span><span class="sxs-lookup"><span data-stu-id="596f1-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="596f1-212">Pour pouvoir s'y connecter, les clients ont besoin de l'IP ou du nom de domaine complet de l'adresse.</span><span class="sxs-lookup"><span data-stu-id="596f1-212">For clients to correctly connect to it, they need an actual IP or FQDN in the address.</span></span>

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
        this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="596f1-213">Notez que ces derniers font référence à la classe de démarrage transmise à OwinCommunicationListener dans le constructeur.</span><span class="sxs-lookup"><span data-stu-id="596f1-213">Note that this references the Startup class that was passed in to the OwinCommunicationListener in the constructor.</span></span> <span data-ttu-id="596f1-214">Cette instance de démarrage est utilisée par le serveur web pour amorcer l’application API Web.</span><span class="sxs-lookup"><span data-stu-id="596f1-214">This startup instance is used by the web server to bootstrap the Web API application.</span></span>

<span data-ttu-id="596f1-215">La ligne `ServiceEventSource.Current.Message()` apparaît ultérieurement dans la fenêtre Événements de diagnostic, quand vous exécutez l’application pour confirmer que le serveur web a correctement démarré.</span><span class="sxs-lookup"><span data-stu-id="596f1-215">The `ServiceEventSource.Current.Message()` line will appear in the Diagnostic Events window later, when you run the application to confirm that the web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="596f1-216">Implémenter CloseAsync et Abort</span><span class="sxs-lookup"><span data-stu-id="596f1-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="596f1-217">Enfin, implémentez à la fois CloseAsync et Abort pour arrêter le serveur web.</span><span class="sxs-lookup"><span data-stu-id="596f1-217">Finally, implement both CloseAsync and Abort to stop the web server.</span></span> <span data-ttu-id="596f1-218">Le serveur web peut être arrêté en supprimant le handle de serveur créé pendant OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="596f1-218">The web server can be stopped by disposing the server handle that was created during OpenAsync.</span></span>

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

<span data-ttu-id="596f1-219">Dans cet exemple d’implémentation, CloseAsync et Abort arrêtent tout simplement le serveur web.</span><span class="sxs-lookup"><span data-stu-id="596f1-219">In this implementation example, both CloseAsync and Abort simply stop the web server.</span></span> <span data-ttu-id="596f1-220">Vous pouvez choisir d’effectuer un arrêt plus élégamment coordonné du serveur web dans CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="596f1-220">You may opt to perform a more gracefully coordinated shutdown of the web server in CloseAsync.</span></span> <span data-ttu-id="596f1-221">Par exemple, l’arrêt peut attendre que les demandes en cours d’exécution soient terminées avant le retour.</span><span class="sxs-lookup"><span data-stu-id="596f1-221">For example, the shutdown could wait for in-flight requests to be completed before the return.</span></span>

## <a name="start-the-web-server"></a><span data-ttu-id="596f1-222">Démarrer le serveur web</span><span class="sxs-lookup"><span data-stu-id="596f1-222">Start the web server</span></span>
<span data-ttu-id="596f1-223">Vous êtes maintenant prêt à créer et à renvoyer une instance OwinCommunicationListener pour démarrer le serveur web.</span><span class="sxs-lookup"><span data-stu-id="596f1-223">You're now ready to create and return an instance of OwinCommunicationListener to start the web server.</span></span> <span data-ttu-id="596f1-224">De retour dans la classe de service (WebService.cs), remplacez la méthode `CreateServiceInstanceListeners()` :</span><span class="sxs-lookup"><span data-stu-id="596f1-224">Back in the Service class (WebService.cs), override the `CreateServiceInstanceListeners()` method:</span></span>

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

<span data-ttu-id="596f1-225">C’est là que l’*application* API web et l’*hôte* OWIN finissent par se rencontrer.</span><span class="sxs-lookup"><span data-stu-id="596f1-225">This is where the Web API *application* and the OWIN *host* finally meet.</span></span> <span data-ttu-id="596f1-226">L’hôte (OwinCommunicationListener) reçoit une instance de *l’application* (API Web) via la classe de démarrage.</span><span class="sxs-lookup"><span data-stu-id="596f1-226">The host (OwinCommunicationListener) is given an instance of the *application* (Web API) via the Startup class.</span></span> <span data-ttu-id="596f1-227">Ensuite, Service Fabric gère son cycle de vie.</span><span class="sxs-lookup"><span data-stu-id="596f1-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="596f1-228">Ce même modèle peut généralement être suivi d'une pile de communication.</span><span class="sxs-lookup"><span data-stu-id="596f1-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="596f1-229">Assemblage</span><span class="sxs-lookup"><span data-stu-id="596f1-229">Put it all together</span></span>
<span data-ttu-id="596f1-230">Dans cet exemple, vous n’avez rien à faire dans la méthode `RunAsync()`. Vous pouvez donc tout simplement supprimer cette substitution.</span><span class="sxs-lookup"><span data-stu-id="596f1-230">In this example, you don't need to do anything in the `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="596f1-231">L’implémentation du service finale doit être très simple.</span><span class="sxs-lookup"><span data-stu-id="596f1-231">The final service implementation should be very simple.</span></span> <span data-ttu-id="596f1-232">Il suffit de créer l’écouteur de communication :</span><span class="sxs-lookup"><span data-stu-id="596f1-232">It only needs to create the communication listener:</span></span>

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

<span data-ttu-id="596f1-233">Voici la classe `OwinCommunicationListener` complète :</span><span class="sxs-lookup"><span data-stu-id="596f1-233">The complete `OwinCommunicationListener` class:</span></span>

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
                this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

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

<span data-ttu-id="596f1-234">Maintenant que tous les composants sont en place, votre projet doit ressembler à une application API Web type, avec des points d’entrée d’API Reliable Services et un hôte OWIN.</span><span class="sxs-lookup"><span data-stu-id="596f1-234">Now that you have put all the pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="596f1-235">Exécuter et se connecter via un navigateur web</span><span class="sxs-lookup"><span data-stu-id="596f1-235">Run and connect through a web browser</span></span>
<span data-ttu-id="596f1-236">Si ce n'est déjà fait, [configurez votre environnement de développement](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="596f1-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="596f1-237">Vous pouvez désormais générer et déployer votre service.</span><span class="sxs-lookup"><span data-stu-id="596f1-237">You can now build and deploy your service.</span></span> <span data-ttu-id="596f1-238">Appuyez sur **F5** dans Visual Studio pour générer et déployer l'application.</span><span class="sxs-lookup"><span data-stu-id="596f1-238">Press **F5** in Visual Studio to build and deploy the application.</span></span> <span data-ttu-id="596f1-239">Dans la fenêtre Événements de diagnostic, un message doit apparaître et indiquer que le serveur web s’est ouvert sur http://localhost:8281/.</span><span class="sxs-lookup"><span data-stu-id="596f1-239">In the Diagnostic Events window, you should see a message that indicates that the web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="596f1-240">Si le port a déjà été ouvert par un autre processus sur votre ordinateur, une erreur risque d’apparaître ici.</span><span class="sxs-lookup"><span data-stu-id="596f1-240">If the port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="596f1-241">Elle indique que l’écouteur n’a pas pu être ouvert.</span><span class="sxs-lookup"><span data-stu-id="596f1-241">This indicates that the listener couldn't be opened.</span></span> <span data-ttu-id="596f1-242">Dans ce cas, essayez d’utiliser un autre port pour la configuration du point de terminaison dans le fichier ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="596f1-242">If that's the case, try using a different port for the endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="596f1-243">Une fois le service en cours d’exécution, ouvrez un navigateur et accédez à [http://localhost:8281/api/values](http://localhost:8281/api/values) pour le tester.</span><span class="sxs-lookup"><span data-stu-id="596f1-243">Once the service is running, open a browser and navigate to [http://localhost:8281/api/values](http://localhost:8281/api/values) to test it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="596f1-244">Montée en charge</span><span class="sxs-lookup"><span data-stu-id="596f1-244">Scale it out</span></span>
<span data-ttu-id="596f1-245">La montée en charge d’applications web sans état implique généralement l’ajout d’ordinateurs supplémentaires sur lesquels les applications web seront exécutées.</span><span class="sxs-lookup"><span data-stu-id="596f1-245">Scaling out stateless web apps typically means adding more machines and spinning up the web apps on them.</span></span> <span data-ttu-id="596f1-246">Le moteur d'orchestration de Service Fabric peut réaliser cette opération chaque fois que de nouveaux nœuds sont ajoutés à un cluster.</span><span class="sxs-lookup"><span data-stu-id="596f1-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added to a cluster.</span></span> <span data-ttu-id="596f1-247">Quand vous créez des instances d’un service sans état, vous pouvez spécifier le nombre d’instances à générer.</span><span class="sxs-lookup"><span data-stu-id="596f1-247">When you create instances of a stateless service, you can specify the number of instances you want to create.</span></span> <span data-ttu-id="596f1-248">Service Fabric place ce nombre d’instances sur les nœuds du cluster,</span><span class="sxs-lookup"><span data-stu-id="596f1-248">Service Fabric places that number of instances on nodes in the cluster.</span></span> <span data-ttu-id="596f1-249">en veillant à ne pas créer plusieurs instances sur un même nœud.</span><span class="sxs-lookup"><span data-stu-id="596f1-249">And it makes sure not to create more than one instance on any one node.</span></span> <span data-ttu-id="596f1-250">Vous pouvez également demander à Service Fabric de toujours créer une instance sur chaque nœud en spécifiant **-1** comme nombre d’instances.</span><span class="sxs-lookup"><span data-stu-id="596f1-250">You can also instruct Service Fabric to always create an instance on every node by specifying **-1** for the instance count.</span></span> <span data-ttu-id="596f1-251">Cela garantit que chaque fois que vous ajoutez des nœuds pour faire évoluer votre cluster, une instance de votre service sans état sera créée sur les nouveaux nœuds.</span><span class="sxs-lookup"><span data-stu-id="596f1-251">This guarantees that whenever you add nodes to scale out your cluster, an instance of your stateless service will be created on the new nodes.</span></span> <span data-ttu-id="596f1-252">Cette valeur est une propriété de l’instance de service, elle est donc définie quand vous créez une instance de service.</span><span class="sxs-lookup"><span data-stu-id="596f1-252">This value is a property of the service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="596f1-253">Pour ce faire, vous pouvez utiliser PowerShell :</span><span class="sxs-lookup"><span data-stu-id="596f1-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="596f1-254">Vous pouvez également le faire quand vous définissez un service par défaut dans un projet de service sans état Visual Studio :</span><span class="sxs-lookup"><span data-stu-id="596f1-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="596f1-255">Pour plus d’informations sur la façon de créer des instances d’application et de service, consultez [Déployer une application](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="596f1-255">For more information on how to create application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="596f1-256">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="596f1-256">Next steps</span></span>
[<span data-ttu-id="596f1-257">Débogage de votre application Service Fabric à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="596f1-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

