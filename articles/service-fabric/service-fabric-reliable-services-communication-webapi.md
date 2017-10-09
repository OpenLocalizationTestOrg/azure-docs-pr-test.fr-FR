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
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a>Prise en main : services de l’API Web Service Fabric avec auto-hébergement OWIN
Azure Service Fabric place power de hello dans vos mains lorsque vous décidez comment vous souhaitez que votre toocommunicate services avec des utilisateurs et entre eux. Ce didacticiel se concentre sur l’implémentation de la communication de service à l’aide de l’API Web ASP.NET avec auto-hébergement OWIN (Open Web Interface for .NET) dans l’API Reliable Services de Service Fabric. Nous verrons comment profondément hello communication enfichable de Services fiables API. Nous allons également utiliser des API Web dans un tooshow exemple pas à pas vous comment tooset d’un écouteur de communication personnalisées.

## <a name="introduction-tooweb-api-in-service-fabric"></a>Introduction tooWeb API dans l’infrastructure de Service
API Web ASP.NET est une infrastructure de puissante et populaire pour bâtis APIs HTTP hello .NET Framework. Si vous n’êtes pas déjà familiarisé avec l’infrastructure de hello, consultez [mise en route avec ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) toolearn plus.

API Web dans le Service Fabric est hello même ASP.NET Web API, vous connaissez et appréciez. Hello différence réside dans la façon de vous *hôte* une application API Web. Vous n’allez pas utiliser Microsoft Internet Information Services (IIS). toobetter comprendre la différence de hello, nous allons scindez-la en deux parties :

1. application d’API Web Hello (y compris les contrôleurs et les modèles)
2. hôte Hello (serveur web hello, généralement IIS)

Une application API Web elle-même ne change pas. Elle ne diffère pas des applications API Web que vous avez écrit Bonjour passées, et vous devez être en mesure de toosimply déplacer sur la plupart du code de votre application. Mais si vous avez été hébergement sur IIS, là où vous hébergez l’application hello peut être un peu différente de ce que vous êtes habitué. Avant de toohello partie d’hébergement, commençons par quelque chose de plus familiers : hello application d’API Web.

## <a name="create-hello-application"></a>Créer l’application hello
Commencez par créer une application Service Fabric, avec un seul service sans état, dans Visual Studio 2015.

Un modèle de Visual Studio pour un service sans état via l’API Web est tooyou disponible. Dans ce didacticiel, nous allons créer un projet d’API Web qui donnera le même résultat que si vous aviez sélectionné ce modèle.

Sélectionnez un toolearn de projet de Service sans état vide comment toobuild un projet d’API Web de toutes pièces, ou si vous démarrez avec un service sans état hello modèle API Web et simplement suivre son déroulement.  

première étape de Hello est toopull dans des packages NuGet pour API Web. package Hello nous souhaitons toouse est Microsoft.AspNet.WebApi.OwinSelfHost. Ce package comprend tous les packages d’API Web nécessaires hello et hello *hôte* packages. Ils auront leur importance plus tard.

Après avoir installé les packages hello, vous pouvez commencer la création de structure de projet Web API base hello. Si vous avez utilisé l’API Web, la structure de projet hello doit ressembler très familier. Commencez par ajouter un répertoire `Controllers` et un contrôleur de valeurs simple :

**ValuesController.cs**

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

Ensuite, ajoutez une classe de démarrage au routage hello projet racine tooregister hello, formateurs et tout autre programme d’installation de configuration. Il s’agit également où se branche API Web toohello *hôte*, qui sera revue plus tard. 

**Startup.cs**

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

C’est tout pour une partie d’application hello. À ce stade, nous avons configuré simplement hello base API Web disposition du projet. Jusqu'à présent, il ne doit pas différer beaucoup de projets d’API Web que peut avoir écrit Bonjour passées ou à partir du modèle d’API Web base hello. Votre logique métier s’intègre dans les modèles et des contrôleurs de hello, comme d’habitude.

Maintenant que devons-nous faire au niveau de l’hébergement pour pouvoir l’exécuter ?

## <a name="service-hosting"></a>Hébergement du service
Dans Service Fabric, votre service s’exécute dans un *processus hôte de service*, c’est-à-dire un fichier exécutable qui exécute le code de votre service. Lorsque vous écrivez un service à l’aide de hello API des Services fiables, votre projet de service compile simplement le fichier exécutable tooan qui inscrit votre type de service et exécute votre code. Ceci se vérifie dans la plupart des cas quand vous écrivez un service sur Service Fabric dans .NET. Lorsque vous ouvrez le fichier Program.cs dans le projet de service sans état hello, vous devez voir :

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

Si l’air anormalement hello entrée point tooa console application, qui est, car il est.

Des informations détaillées sur hello processus hôte de service et l’inscription du service sont abordée dans cet article hello. Mais il est important tooknow pour maintenant que *votre code de service s’exécute dans son propre processus*.

## <a name="self-host-web-api-with-an-owin-host"></a>Auto-héberger l’API Web avec un hôte OWIN
Étant donné que le code de votre application d’API Web est hébergé dans son propre processus, comment vous accrochez serveur web de tooa ? Entrez [OWIN](http://owin.org/). OWIN est simplement un contrat entre les applications web .NET et les serveurs web. En règle générale lorsqu’ASP.NET (haut tooMVC 5) est utilisé, application web de hello est étroitement couplées tooIIS via System.Web. Toutefois, les API Web implémente OWIN, afin de pouvoir écrire une application web qui est dissociée de serveur web hello qui l’héberge. Pour cette raison, vous pouvez utiliser un serveur web OWIN *auto-hébergé* que vous pouvez démarrer dans votre propre processus. Il s’intègre parfaitement avec hello Service Fabric modèle d’hébergement que nous venons de voir.

Dans cet article, nous allons utiliser Katana en tant qu’hôte OWIN hello pour hello application d’API Web. Katana est une implémentation d’hôte OWIN open source repose sur [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) et hello Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).

> [!NOTE]
> toolearn plus d’informations sur les interconnexions, accédez toohello [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana). Pour une présentation rapide de le toouse Katana tooself-hôte Web API, consultez [utilisation OWIN tooSelf-hôte ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).
> 
> 

## <a name="set-up-hello-web-server"></a>Configurer le serveur web de hello
Hello fiable API des Services fournit un point d’entrée de communication où vous pouvez incorporer dans les piles de communication qui permettent aux utilisateurs et service de clients tooconnect toohello :

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

serveur web de Hello (et une autre pile de communication que vous utilisez Bonjour futures, telles que les WebSockets) doivent utiliser hello ICommunicationListener interface toointegrate correctement avec hello système. raisons Hello seront deviennent plus évidents Bonjour comme suit.

Commencez par créer une classe appelée OwinCommunicationListener qui implémente ICommunicationListener :

**OwinCommunicationListener.cs**

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

interface de ICommunicationListener Hello fournit trois méthodes toomanage un écouteur de communication pour votre service :

* *OpenAsync*. Commence à écouter les demandes.
* *CloseAsync*. Stoppe l’écoute des demandes, termine toutes les demandes en cours et s’arrête correctement.
* *Abort*. Annule tout et s’arrête immédiatement.

tooget démarré, ajouter des membres de classe privée pour l’écouteur de choses hello devez toofunction. Ces seront initialisés via le constructeur de hello et utilisés ultérieurement lorsque vous configurez hello à l’écoute des URL.

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

## <a name="implement-openasync"></a>Implémenter OpenAsync
tooset serveur web de hello, vous avez besoin de deux informations :

* *Préfixe du chemin de l'URL*. Bien que cette option est facultative, il est approprié pour vous tooset cette jusqu'à maintenant afin que vous pouvez en toute sécurité héberger plusieurs services web dans votre application.
* *Un port*.

Avant d’obtenir un port pour le serveur web de hello, il est important de comprendre que le Service Fabric fournit une couche d’application qui agit comme une mémoire tampon entre votre application et le système d’exploitation sous-jacent hello qu’il exécute sur. Par conséquent, Service Fabric fournit un moyen tooconfigure *points de terminaison* pour vos services. L’infrastructure de service garantit que les points de terminaison sont disponibles pour votre toouse de service. De cette manière, vous n’avez pas tooconfigure les vous-même Bonjour sous-jacent d’environnement du système d’exploitation. Vous pouvez facilement héberger votre application de Service Fabric dans différents environnements sans avoir toomake n’importe quelle application tooyour de modifications. (Par exemple, vous pouvez héberger hello même application dans Azure ou dans votre centre de données.)

Configurer un point de terminaison HTTP dans  PackageRoot\ServiceManifest.xml :

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

Cette étape est importante, car le processus hôte de service hello s’exécute sous les informations d’identification limitées (Service réseau sur Windows). Cela signifie que votre service ne dispose tooset d’accès d’un point de terminaison HTTP sur son propre. À l’aide de configuration de point de terminaison hello, Service Fabric sait tooset de liste de contrôle d’accès (ACL) hello pour hello URL hello service écoutera. Points de terminaison tooconfigure, service Fabric fournit également un emplacement standard.

De retour dans OwinCommunicationListener.cs, vous pouvez commencer à implémenter OpenAsync. Il s’agit où vous démarrez le serveur web de hello. Tout d’abord, obtenir des informations de point de terminaison hello et créer des URL de hello hello service écoute sur. Hello URL sera différente selon que le port d’écoute hello est utilisée dans un service sans état ou d’un service avec état. Pour un service avec état, port d’écoute hello doit toocreate unique adresse pour chaque réplica de service avec état. il est à l’écoute sur. Pour les services sans état, l’adresse de hello peut être beaucoup plus simple. 

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

Notez que « http://+ » est utilisé ici. Il s’agit de toomake assurer que le serveur web hello est à l’écoute sur toutes les adresses disponibles, y compris localhost, nom de domaine complet et l’IP hello.

Hello OpenAsync implémentation est une des raisons les plus importantes hello pourquoi les serveur web de hello (ou une pile de communication) est implémentée comme un ICommunicationListener, plutôt que son ouvre directement à partir de `RunAsync()` dans le service hello. valeur de retour Hello OpenAsync est adresse hello hello du serveur web est à l’écoute sur. Lorsque cette adresse est renvoyée toohello système, il enregistre les adresse hello avec service de hello. L’infrastructure de service fournit une API qui permet aux clients et autres toothen services demandera cette adresse par nom de service. Ceci est important, car l’adresse du service hello n’est pas statique. Les services sont déplacés dans le cluster hello pour à des fins de disponibilité et de l’équilibrage de la ressource. Il s’agit de mécanisme hello qui permet aux clients hello tooresolve adresse pour un service d’écoute.

Dans cette optique, OpenAsync démarre le serveur web de hello et retourne l’adresse hello qu’il écoute. Notez qu’il écoute sur « http://+ », mais avant OpenAsync renvoie l’adresse de hello, hello « + » est remplacé par hello IP ou nom de domaine complet du nœud hello que cours. adresse Hello qui est retourné par cette méthode est ce qui est inscrit avec le système de hello. Il s’agit également de celle que les clients et autres services voient quand ils recherchent l’adresse d’un service. Pour les clients toocorrectly connexion tooit, ils ont besoin d’une adresse IP ou le nom de domaine complet réel dans l’adresse de hello.

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

Notez que cela fait référence à la classe de démarrage hello qui a été passé dans toohello OwinCommunicationListener dans le constructeur de hello. Cette instance de démarrage est utilisée par les messages hello toobootstrap du serveur hello web application d’API Web.

Hello `ServiceEventSource.Current.Message()` ligne apparaît dans la fenêtre des événements de Diagnostic hello plus tard, lorsque vous exécutez hello application tooconfirm que le serveur web hello a démarré avec succès.

## <a name="implement-closeasync-and-abort"></a>Implémenter CloseAsync et Abort
Enfin, implémentez CloseAsync et Abort serveur web de hello toostop. serveur web de Hello peut être arrêtée en supprimant le handle de serveur hello qui a été créé au cours de OpenAsync.

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

Dans cet exemple d’implémentation, CloseAsync et Abort simplement arrêteront le serveur web de hello. Vous pouvez choisir tooperform un arrêt plus naturellement coordonné de serveur web hello CloseAsync. Par exemple, l’arrêt hello pouvait attendre de toobe de demandes en cours s’est terminée avant de retourner de hello.

## <a name="start-hello-web-server"></a>Démarrer le serveur web de hello
Vous êtes maintenant prêt toocreate et retournez une instance de serveur web de OwinCommunicationListener toostart hello. Dans la classe de Service (WebService.cs) de hello, substituez hello `CreateServiceInstanceListeners()` méthode :

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

Cela est hello où les API Web *application* et hello OWIN *hôte* enfin respecter. l’hôte Hello (OwinCommunicationListener) est une instance donnée de hello *application* (API Web) via hello classe de démarrage. Ensuite, Service Fabric gère son cycle de vie. Ce même modèle peut généralement être suivi d'une pile de communication.

## <a name="put-it-all-together"></a>Assemblage
Dans cet exemple, vous n’avez pas besoin toodo n’est pas défini dans hello `RunAsync()` méthode, donc ce remplacement peut être simplement supprimé.

implémentation du service final Hello doit être très simple. Il n’a besoin que d’écouteur de communications toocreate hello :

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

Hello complète `OwinCommunicationListener` classe :

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

Maintenant que vous avez placé tous les éléments de hello en place, votre projet doit ressembler à une application Web API standard avec les points d’entrée de l’API des Services fiables et un hôte OWIN.

## <a name="run-and-connect-through-a-web-browser"></a>Exécuter et se connecter via un navigateur web
Si ce n'est déjà fait, [configurez votre environnement de développement](service-fabric-get-started.md).

Vous pouvez désormais générer et déployer votre service. Appuyez sur **F5** dans Visual Studio toobuild et déployer l’application hello. Dans la fenêtre des événements de Diagnostic hello, vous devez voir un message qui indique que le serveur web hello ouvert sur http://localhost:8281 /.

> [!NOTE]
> Si le port de hello a déjà été ouvert par un autre processus sur votre ordinateur, vous pouvez voir ici une erreur. Cela indique que cet écouteur hello n’a pas pu être ouvert. Si tel est le cas de hello, essayez d’utiliser un port différent pour la configuration de point de terminaison hello dans ServiceManifest.xml.
> 
> 

Une fois que le service de hello est en cours d’exécution, ouvrez un navigateur et accédez trop[http://localhost:8281/api/valeurs](http://localhost:8281/api/values) tootest il.

## <a name="scale-it-out"></a>Montée en charge
Évolution généralement d’applications web sans état signifie l’ajout de plusieurs ordinateurs et lancer des applications web hello sur les. Moteur d’orchestration de l’infrastructure de service peut faire cela pour vous chaque fois que les nouveaux nœuds sont ajoutés tooa cluster. Lorsque vous créez des instances d’un service sans état, vous pouvez spécifier le nombre de hello d’instances, vous souhaitez toocreate. L’infrastructure de service place ce nombre d’instances sur des nœuds de cluster de hello. Et il permet de s’assurer toocreate pas plus d’une instance sur chaque nœud. Vous pouvez également demander à Service Fabric tooalways créer une instance sur chaque nœud, en spécifiant **-1** pour le nombre d’instances hello. Cela garantit que chaque fois que vous ajoutez des nœuds tooscale à votre cluster, une instance de votre service sans état est créée sur les nouveaux nœuds de hello. Cette valeur est une propriété d’instance de service hello, donc elle est définie lorsque vous créez une instance de service. Pour ce faire, vous pouvez utiliser PowerShell :

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

Vous pouvez également le faire quand vous définissez un service par défaut dans un projet de service sans état Visual Studio :

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

Pour plus d’informations sur comment toocreate application et les instances de service, consultez [déployer une application](service-fabric-deploy-remove-applications.md).

## <a name="next-steps"></a>Étapes suivantes
[Débogage de votre application Service Fabric à l’aide de Visual Studio](service-fabric-debugging-your-application.md)

