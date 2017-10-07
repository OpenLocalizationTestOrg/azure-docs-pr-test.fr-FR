---
title: communication aaaService avec hello ASP.NET Core | Documents Microsoft
description: "Découvrez comment toouse ASP.NET de base dans les Services fiables et sans état."
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
ms.date: 05/02/2017
ms.author: vturecek
ms.openlocfilehash: 6e6a83ab04390150292f63de5d9b51d290284e50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a>ASP.NET Core dans le modèle Reliable Services de Service Fabric

ASP.NET Core est une nouvelle infrastructure open source et multiplateforme destinée à générer des applications modernes connectées à Internet basées sur le cloud, comme des applications web, des applications IoT et des serveurs principaux mobiles. 

Cet article est un toohosting guide détaillé des services ASP.NET Core dans Service Fabric des Services fiables à l’aide de hello **Microsoft.ServiceFabric.AspNetCore.** * ensemble des packages NuGet.

Pour un didacticiel de présentation d’ASP.NET Core dans Service Fabric et pour des instructions de configuration de votre environnement de développement, voir [Création d’un serveur web frontal pour votre application à l’aide d’ASP.NET Core](service-fabric-add-a-web-frontend.md).

reste Hello de cet article suppose que vous connaissez déjà ASP.NET Core. Si non, nous vous conseillons de lire hello [notions de base ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/index).

## <a name="aspnet-core-in-hello-service-fabric-environment"></a>ASP.NET Core dans un environnement de Service Fabric hello

Alors que les applications ASP.NET Core peuvent exécuter sur .NET Core ou sur hello sur que .NET Framework complet, actuellement les services de Fabric de Service peut s’exécuter uniquement hello .NET Framework complet. Cela signifie que lorsque vous générez un service ASP.NET Core pour Service Fabric, vous devez toujours cibler hello .NET Framework complet.

L’infrastructure ASP.NET Core peut être utilisée de deux manières dans Service Fabric :
 - **Hébergée en tant qu’exécutable invité**. Il s’agit principalement utilisé toorun ASP.NET Core applications existantes sur l’infrastructure de Service sans aucune modification de code.
 - **Exécutée dans un service Reliable Service**. Cela permet une meilleure intégration avec le runtime du Service Fabric hello et avec état ASP.NET Core services.

reste Hello de cet article explique comment toouse ASP.NET Core à l’intérieur d’un Service fiable à l’aide de hello des composants d’intégration ASP.NET Core fournis avec hello SDK de l’infrastructure de Service. 

## <a name="service-fabric-service-hosting"></a>Hébergement du service Service Fabric

Dans Service Fabric, une ou plusieurs instances et/ou un ou plusieurs réplicas de votre service s’exécutent dans un *processus hôte de service*, un fichier exécutable qui exécute le code de votre service. Vous, en tant qu’auteur de service, propre processus hôte de service hello et Service Fabric active et il surveille.

ASP.NET traditionnel (haut tooMVC 5) est étroitement couplées tooIIS via System.Web.dll. ASP.NET Core fournit une séparation entre le serveur web de hello et votre application web. Cela permet toobe d’applications web portable entre les différents serveurs web et également toobe de serveurs web *auto-hébergé*, ce qui signifie que vous pouvez démarrer un serveur web dans votre propre processus, en tant que processus tooa opposés détenu par le web dédié logiciel serveur telles que IIS. 

Dans l’ordre toocombine un service Service Fabric et ASP.NET, comme un exécutable invité ou dans un Service fiable, vous devez être en mesure de toostart ASP.NET à l’intérieur de votre processus hôte de service. ASP.NET Core auto-hébergement vous permet de toodo cela.

## <a name="hosting-aspnet-core-in-a-reliable-service"></a>Hébergement d’ASP.NET Core dans un service Reliable Service
En règle générale, les applications ASP.NET Core auto-hébergé créent WebHost dans le point d’entrée d’une application, par exemple hello `static void Main()` méthode dans `Program.cs`. Dans ce cas, le cycle de vie de hello Hello WebHost est lié toohello le cycle de vie du processus de hello.

![Hébergement d’ASP.NET Core dans un processus][0]

Toutefois, point d’entrée application hello n’est pas hello bon endroit toocreate WebHost dans un Service fiable, parce que le point d’entrée application hello est utilisée uniquement tooregister un service de type avec le runtime du Service Fabric hello, afin qu’il peut créer des instances de ce service type. Hello WebHost doit être créé dans un Service fiable lui-même. Dans le processus hôte de service hello, instances de service et/ou de réplicas peuvent subir plusieurs cycles de vie. 

Une instance du service Reliable Service est représentée par votre classe de service dérivant de `StatelessService` ou `StatefulService`. pile de communication Hello pour un service est contenue dans un `ICommunicationListener` mise en œuvre dans votre classe de service. Hello `Microsoft.ServiceFabric.Services.AspNetCore.*` les packages NuGet contiennent des implémentations de `ICommunicationListener` que Démarrer et gérer hello ASP.NET Core WebHost pour Kestrel ou WebListener dans un Service fiable.

![Hébergement d’ASP.NET Core dans un service Reliable Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a>Écouteurs ICommunicationListeners d’ASP.NET Core
Hello `ICommunicationListener` implémentations pour Kestrel et WebListener Bonjour `Microsoft.ServiceFabric.Services.AspNetCore.*` les packages NuGet ont des modèles d’utilisation similaires mais effectuer légèrement différentes actions spécifiques tooeach web server. 

Les deux écouteurs de communication fournissent un constructeur qui accepte hello arguments suivants :
 - **`ServiceContext serviceContext`**: hello `ServiceContext` objet qui contient des informations sur hello service en cours d’exécution.
 - **`string endpointName`**: nom hello d’un `Endpoint` configuration dans ServiceManifest.xml. Il s’agit principalement où diffèrent des écouteurs de communication hello deux : WebListener **requiert** un `Endpoint` configuration, n’est pas le cas de Kestrel.
 - **`Func<string, AspNetCoreCommunicationListener, IWebHost> build`** : expression lambda que vous implémentez dans laquelle vous créez et retournez un `IWebHost`. Cela vous permet de tooconfigure `IWebHost` moyen hello vous le feriez normalement dans une application ASP.NET Core. Hello lambda fournit une URL qui est générée pour vous en fonction de l’intégration de Service Fabric hello options que vous utilisez et hello `Endpoint` configuration que vous fournissez. Que URL puis peut être modifié ou utilisé en tant que-est le serveur web de hello toostart.

## <a name="service-fabric-integration-middleware"></a>Intergiciel (middleware) d’intégration à Service Fabric
Hello `Microsoft.ServiceFabric.Services.AspNetCore` package NuGet inclut hello `UseServiceFabricIntegration` méthode d’extension sur `IWebHostBuilder` qui ajoute l’intergiciel (middleware) Service Fabric prenant en charge. Cet intergiciel (middleware) configure hello Kestrel ou WebListener `ICommunicationListener` tooregister une URL de service unique avec hello l’infrastructure de Service d’affectation de noms de Service, puis valide les clients tooensure de demandes de clients se connectent toohello bon service. Cela est nécessaire dans un environnement hôte partagés tels que l’infrastructure de Service, où plusieurs applications web peuvent exécuter sur hello même physique ou virtuel, mais n’utilisent pas de nom d’hôte unique, tooprevent clients par erreur connexion toohello un mauvais service. Ce scénario est décrit plus en détail dans la section suivante de hello.

### <a name="a-case-of-mistaken-identity"></a>Cas d’erreur d’identité
Quel que soit le protocole utilisé, les réplicas de service écoutent sur une combinaison IP:port unique. Une fois qu’un réplica de service a démarré à l’écoute sur un point de terminaison IP : port, il signale cette toohello d’adresse de point de terminaison Service Service Fabric d’affectation de noms dans lequel il peut être détecté par les clients ou d’autres services. Si les services utilisent des ports affectés dynamiquement une application, un réplica de service peuvent utiliser par coïncidence hello même point de terminaison IP : port d’un autre service qui a été précédemment sur hello même physique ou virtuel. Cela peut entraîner un client toomistakely connecter toohello un mauvais service. Cela peut se produire si hello suivant la séquence d’événements se produire :

 1. Le service A écoute sur 10.0.0.1:30000 via HTTP. 
 2. Le client résout le service A et obtient l’adresse 10.0.0.1:30000.
 3. Un nœud différent du tooa se déplace du service.
 4. Service B est placé sur 10.0.0.1 et par coïncidence utilise hello même port 30000.
 5. Client tente de tooconnect tooservice A avec l’adresse mise en cache 10.0.0.1:30000.
 6. Client est maintenant connecté tooservice B ne pas vous en rendre compte est connecté toohello un mauvais service.

Cela peut provoquer des bogues à des moments aléatoires qui peuvent être difficile toodiagnose. 

### <a name="using-unique-service-urls"></a>Utilisation d’URL de service uniques
tooprevent, services peut valider un toohello de point de terminaison Service d’affectation de noms avec un identificateur unique et puis vérifiez que l’identificateur unique lors des demandes de client. Il s’agit d’une action de coopération entre les services dans un environnement approuvé de client non hostile. Cette action ne permet pas d’authentification de service sécurisée dans un environnement de client hostile.

Dans un environnement approuvé, hello intergiciel (middleware) qui est ajouté par hello `UseServiceFabricIntegration` méthode ajoute automatiquement une adresse de toohello identificateur unique qui est validée toohello d’affectation de noms Service et vérifie que l’identificateur à chaque demande. Si l’identificateur de hello ne correspond pas, hello intergiciel (middleware) retourne immédiatement une réponse HTTP 410 supprimé.

Les services qui utilisent un port attribué dynamiquement doivent avoir recours à cet intergiciel (middleware).

Les services qui utilisent un port unique fixe ne connaissent pas ce problème dans un environnement coopératif. Un port unique fixe est généralement utilisé pour externe services nécessitant un port bien connu pour tooconnect d’applications client à. Par exemple, la plupart des applications web accessibles sur Internet utilisent les ports 80 ou 443 pour les connexions de navigateur web. Dans ce cas, identificateur hello ne doit pas être activée.

Hello diagramme suivant montre les flux de demandes hello avec intergiciel (middleware) hello activé :

![Intégration d’ASP.NET Core à Service Fabric][2]

Kestrel et WebListener `ICommunicationListener` implémentations utilisent ce mécanisme Bonjour exactement identique. Bien que WebListener pouvez différencier en interne les demandes en fonction des chemins d’accès URL uniques à l’aide de hello sous-jacent *http.sys* la fonctionnalité, qui est de la fonctionnalité de partage de port *pas* utilisé par hello WebListener `ICommunicationListener` implémentation car qui entraînerait des codes d’état erreur HTTP 503 et HTTP 404 dans scénario hello décrits précédemment. Qui à son tour rend très difficile pour intention de hello clients toodetermine d’erreur de hello, comme HTTP 503 et HTTP 404 sont déjà tooindicate couramment utilisé autres erreurs. Par conséquent, à la fois Kestrel et WebListener `ICommunicationListener` normaliser les implémentations sur un intergiciel (middleware) hello fournie par hello `UseServiceFabricIntegration` méthode d’extension pour que les clients doivent uniquement tooperform un point de terminaison de résoudre l’action sur les réponses HTTP 410.

## <a name="weblistener-in-reliable-services"></a>WebListener dans Reliable Services
WebListener peut être utilisé dans un Service fiable en important hello **Microsoft.ServiceFabric.AspNetCore.WebListener** package NuGet. Ce package contient `WebListenerCommunicationListener`, une implémentation de `ICommunicationListener`, qui vous permet de toocreate un WebHost de noyaux de ASP.NET à l’intérieur d’un Service fiable à l’aide de WebListener en tant que serveur web de hello.

WebListener repose sur hello [API du serveur HTTP Windows](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx). Cette méthode utilise hello *http.sys* pilote du noyau utilisé par IIS tooprocess HTTP demande et acheminer tooprocesses les applications web en cours d’exécution. Cela permet à plusieurs processus sur hello même ordinateur physique ou virtuel toohost web applications sur hello même port, par un chemin d’URL unique ou un nom d’hôte de lever l’ambiguïté. Ces fonctionnalités sont utiles dans l’infrastructure de Service pour l’hébergement de plusieurs sites Web Bonjour même cluster.

Hello diagramme suivant illustre comment WebListener utilise hello *http.sys* pilote du noyau de Windows pour le partage de port :

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a>WebListener dans un service sans état
toouse `WebListener` dans un service sans état, substituez hello `CreateServiceInstanceListeners` méthode et retournez un `WebListenerCommunicationListener` instance :

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a>WebListener dans un service avec état

`WebListenerCommunicationListener`n’est actuellement pas conçu pour une utilisation dans les services avec état échéance toocomplications avec hello sous-jacent *http.sys* la fonctionnalité de partage de port. Pour plus d’informations, consultez hello suivant la section sur l’allocation de port dynamique avec WebListener. Pour les services avec état, Kestrel est hello recommandé de serveur web.

### <a name="endpoint-configuration"></a>Configuration du point de terminaison

Un `Endpoint` configuration est requise pour les serveurs web qui utilisent hello API de serveur HTTP de Windows, y compris WebListener. Serveurs Web qui utilisent hello Windows HTTP Server API doivent réserver tout d’abord leur URL avec *http.sys* (cela se produit généralement avec hello [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) outil). Cette action requiert des privilèges élevés dont vos services sont dépourvus par défaut. Hello options « http » ou « https » pour hello `Protocol` propriété Hello `Endpoint` configuration dans *ServiceManifest.xml* sont utilisées spécifiquement tooinstruct hello Service Fabric runtime tooregister une URL avec *http.sys* à votre place à l’aide de hello [ *caractère générique fort* ](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) préfixe d’URL.

Par exemple, tooreserve `http://+:80` pour un service, hello configuration suivante doit être utilisée dans ServiceManifest.xml :

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

Et le nom du point de terminaison hello doit être passé toohello `WebListenerCommunicationListener` constructeur :

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a>Utiliser WebListener avec un port statique
toouse un port statique avec WebListener, indiquez le numéro de port de hello Bonjour `Endpoint` configuration :

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a>Utiliser WebListener avec un port dynamique
toouse un port affecté dynamiquement avec WebListener, omettez hello `Port` propriété Bonjour `Endpoint` configuration :

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

Notez qu’un port dynamique alloué par une configuration `Endpoint` fournit un seul port *par processus hôte*. Hello actuel Service Fabric modèle d’hébergement permet à plusieurs toobe d’instances et/ou des réplicas de service hébergé dans hello même processus, ce qui signifie que chacun d’eux sera partagent hello même port lors de l’allocation via hello `Endpoint` configuration. Plusieurs instances de WebListener peuvent partager un port à l’aide de hello sous-jacent *http.sys* port partage de la fonctionnalité, mais qui n’est pas pris en charge par `WebListenerCommunicationListener` en raison de complications toohello elle introduit pour les demandes du client. Pour l’utilisation de ports dynamiques, Kestrel est hello recommandé de serveur web.

## <a name="kestrel-in-reliable-services"></a>Kestrel dans Reliable Services
Kestrel peut être utilisé dans un Service fiable en important hello **Microsoft.ServiceFabric.AspNetCore.Kestrel** package NuGet. Ce package contient `KestrelCommunicationListener`, une implémentation de `ICommunicationListener`, qui vous permet de toocreate un WebHost de noyaux de ASP.NET à l’intérieur d’un Service fiable à l’aide de Kestrel en tant que serveur web de hello.

Kestrel est un serveur web multiplateforme pour ASP.NET Core basé sur libuv, une bibliothèque d’E/S asynchrone multiplateforme. Contrairement à WebListener, Kestrel n’utilise pas de gestionnaire de points de terminaison centralisé comme *http.sys*. Et contrairement à WebListener, Kestrel ne prend pas en charge le partage de port entre plusieurs processus. Chaque instance de Kestrel doit utiliser un port unique.

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a>Kestrel dans un service sans état
toouse `Kestrel` dans un service sans état, substituez hello `CreateServiceInstanceListeners` méthode et retournez un `KestrelCommunicationListener` instance :

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a>Kestrel dans un service avec état
toouse `Kestrel` dans un service avec état, substituez hello `CreateServiceReplicaListeners` méthode et retournez un `KestrelCommunicationListener` instance :

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

Dans cet exemple, une instance de singleton `IReliableStateManager` est fournie de conteneur d’injection de dépendance toohello WebHost. Cela n’est pas strictement nécessaire, mais il vous permet de toouse `IReliableStateManager` et fiable de Collections dans vos méthodes d’action de contrôleur MVC.

Notez qu’un `Endpoint` nom de configuration est **pas** fourni trop`KestrelCommunicationListener` dans un service avec état. Cela est expliqué en détail dans hello suivant la section.

### <a name="endpoint-configuration"></a>Configuration du point de terminaison
Un `Endpoint` configuration n’est pas requis toouse Kestrel. 

Kestrel est un serveur web autonome simple ; Contrairement à WebListener (ou HttpListener), il n’a pas besoin une `Endpoint` configuration dans *ServiceManifest.xml* , car il ne nécessite pas de toostarting préalable de URL d’inscription. 

#### <a name="use-kestrel-with-a-static-port"></a>Utiliser Kestrel avec un port statique
Un port statique peut être configuré dans hello `Endpoint` configuration de ServiceManifest.xml pour une utilisation avec Kestrel. Même si cela n’est pas rigoureusement nécessaire, cela confère deux avantages potentiels :
 1. Si le port de hello n’est pas comprise dans la plage de ports d’application hello, il est ouvert via le pare-feu du système d’exploitation hello par l’infrastructure de Service.
 2. tooyou URL fournie par le biais de Hello `KestrelCommunicationListener` utilise ce port.

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

Si un `Endpoint` est configuré, son nom doit être passé dans hello `KestrelCommunicationListener` constructeur : 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

Si un `Endpoint` configuration n’est pas utilisée, omettez le nom hello Bonjour `KestrelCommunicationListener` constructeur. Dans ce cas, un port dynamique est utilisé. Consultez la section suivante de hello pour plus d’informations.

#### <a name="use-kestrel-with-a-dynamic-port"></a>Utiliser Kestrel avec un port dynamique
Kestrel ne peut pas utiliser l’attribution automatique du port hello de hello `Endpoint` configuration dans ServiceManifest.xml, car l’attribution automatique du port d’un `Endpoint` configuration affecte un port unique par *processus hôte de* , et un processus hôte unique peut contenir plusieurs instances de Kestrel. Comme Kestrel ne prend pas en charge le partage de port, cela ne fonctionne pas, car chaque instance de Kestrel doit être ouverte sur un port unique.

attribution de port dynamique toouse avec Kestrel, omettez simplement hello `Endpoint` configuration dans ServiceManifest.xml et vous ne passez pas un toohello de nom de point de terminaison `KestrelCommunicationListener` constructeur :

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

Dans cette configuration, `KestrelCommunicationListener` sélectionne automatiquement un port inutilisé à partir de la plage de ports d’application hello.

## <a name="scenarios-and-configurations"></a>Scénarios et configurations
Cette section décrit les scénarios suivants de hello ainsi hello recommandé de combinaison de serveur web, la configuration de port, les options d’intégration de Service Fabric et divers paramètres tooachieve un service fonctionne correctement :
 - Service sans état d’ASP.NET Core exposé en externe
 - Service sans état d’ASP.NET Core interne uniquement
 - Service avec état d’ASP.NET Core interne uniquement

Un **exposé en externe** service est une tâche qui expose un point de terminaison accessible à partir de hors cluster hello, généralement par le biais d’un équilibreur de charge.

Un **interne uniquement** service est un point de terminaison de dont est accessible uniquement à partir d’au sein du cluster de hello.

> [!NOTE]
> Points de terminaison généralement ne doivent pas être un service avec état exposé toohello Internet. Clusters qui se trouvent derrière des équilibreurs de charge qui ne sont pas conscients de résolution de service Service Fabric, par exemple hello équilibrage de charge Azure, seront les services avec état tooexpose impossible, car l’équilibrage de charge hello ne sera pas en mesure de toolocate et acheminer le trafic toohello réplica de service avec état approprié. 

### <a name="externally-exposed-aspnet-core-stateless-services"></a>Services sans état d’ASP.NET Core exposés en externe
WebListener est hello recommandé de serveur web pour les services frontaux qui exposent des points de terminaison externes, connecté à Internet HTTP sur Windows. Il offre une meilleure protection contre les attaques et prend en charge les fonctionnalités non gérées par Kestrel, par exemple l’authentification Windows et le partage de port. 

Pour le moment, Kestrel n’est pas pris en charge en tant que serveur Edge (accessible sur Internet). Un serveur proxy inverse tels que IIS ou Nginx doit être utilisé toohandle trafic hello Internet public.
 
Lorsque toohello exposé Internet, un service sans état doit utiliser un point de terminaison connu et stable qui est accessible via un équilibrage de charge. Il s’agit d’URL de hello vous fournira toousers de votre application. Hello configuration suivante est recommandée :

|  |  | **Remarques** |
| --- | --- | --- |
| Serveur web | WebListener | Si le service de hello est uniquement exposé tooa réseau approuvé, un intranet Kestrel peut être utilisé. Dans le cas contraire, WebListener avère hello préféré. |
| Configuration du port | statique | Un port statique connu doit être configuré dans hello `Endpoints` configuration de ServiceManifest.xml, par exemple 80 pour HTTP et 443 pour HTTPS. |
| ServiceFabricIntegrationOptions | Aucun | Hello `ServiceFabricIntegrationOptions.None` option doit être utilisée lors de la configuration d’intergiciel (middleware) de l’infrastructure de Service intégration afin que le service de hello ne tente pas de toovalidate les demandes entrantes pour un identificateur unique. Les utilisateurs externes de votre application ne saura pas hello ses informations d’identification utilisées par l’intergiciel (middleware) hello. |
| Nombre d'instances | -1 | En cas d’usage typique, nombre d’instances hello définition doit être défini trop « -1 » afin qu’une instance soit disponible sur tous les nœuds qui reçoivent le trafic à partir d’un équilibreur de charge. |

Si plusieurs services exposés en externe partagent hello même ensemble de nœuds, un chemin d’accès URL unique mais stable doit être utilisé. Cela est possible en modifiant les URL de hello fournie lors de la configuration IWebHost. Notez que cela s’applique tooWebListener uniquement.

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a>Service d’ASP.NET Core sans état interne uniquement
Les services sans état qui sont appelées uniquement à partir de cluster de hello doivent utiliser des URL uniques et attribué dynamiquement des ports tooensure une coopération entre plusieurs services. Hello configuration suivante est recommandée :

|  |  | **Remarques** |
| --- | --- | --- |
| Serveur web | Kestrel | Bien que WebListener peut être utilisé pour les services sans état internes, Kestrel est hello recommandé server tooallow tooshare d’instances multiples service un ordinateur hôte.  |
| Configuration du port | affecté de manière dynamique | Plusieurs réplicas d’un service avec état peuvent partager un processus hôte ou un système d’exploitation hôte, et nécessitent donc des ports uniques. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Avec l’attribution de port dynamique, ce paramètre empêche le problème de l’identité hello à tort comme décrit précédemment. |
| InstanceCount | any | nombre d’instances Hello définition peut être défini service hello de tooany valeur toooperate nécessaire. |

### <a name="internal-only-stateful-aspnet-core-service"></a>Service d’ASP.NET Core avec état interne uniquement
Les services avec état qui sont appelées uniquement à partir de cluster de hello doivent utiliser des ports affectés dynamiquement tooensure une coopération entre plusieurs services. Hello configuration suivante est recommandée :

|  |  | **Remarques** |
| --- | --- | --- |
| Serveur web | Kestrel | Hello `WebListenerCommunicationListener` n’est pas conçu pour une utilisation par les services avec état dans lequel les réplicas partagent un processus hôte. |
| Configuration du port | affecté de manière dynamique | Plusieurs réplicas d’un service avec état peuvent partager un processus hôte ou un système d’exploitation hôte, et nécessitent donc des ports uniques. |
| ServiceFabricIntegrationOptions | UseUniqueServiceUrl | Avec l’attribution de port dynamique, ce paramètre empêche le problème de l’identité hello à tort comme décrit précédemment. |

## <a name="next-steps"></a>Étapes suivantes
[Débogage de votre application Service Fabric à l’aide de Visual Studio](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
