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
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a>Créer un service web frontal pour votre application à l’aide d’ASP.NET Core
Par défaut, les services Azure Service Fabric ne fournissent pas d’un site web toohello interface publique. tooexpose clients de tooHTTP de fonctionnalités de votre application, vous avez toocreate un site web de projet tooact comme point d’entrée et communiquer de tooyour il n’y a des services individuels.

Dans ce didacticiel, nous reprendre là où nous se Bonjour [créer votre première application dans Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) didacticiel et ajouter un service web de ASP.NET Core devant hello avec état compteur de service. Si vous ne l’avez pas encore fait, revenez d’abord à ce didacticiel et suivez-le.

## <a name="set-up-your-environment-for-aspnet-core"></a>Configurer votre environnement pour ASP.NET Core

Vous devez toofollow Visual Studio 2017 avec ce didacticiel. N’importe quelle édition fera l’affaire. 

 - [Installer Visual Studio 2017](https://www.visualstudio.com/)

les applications ASP.NET Core pour Service Fabric toodevelop, vous devez avoir hello suivant les charges de travail installés :
 - **Développement Azure** (sous *Web &amp; Cloud*)
 - **Développement web et ASP.NET** (sous *Web &amp; Cloud*)
 - **Développement multiplateforme .NET Core** (sous *Autres jeux d’outils*)

>[!Note] 
>Hello outils .NET Core pour Visual Studio 2015 sont n’est plus mis à jour, mais si vous utilisez encore Visual Studio 2015, vous devez toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installé.

## <a name="add-an-aspnet-core-service-tooyour-application"></a>Ajouter une application de tooyour service ASP.NET Core
ASP.NET Core est une infrastructure de développement web léger et inter-plateformes que vous pouvez utiliser l’interface utilisateur de web moderne toocreate et API web. 

Vous allez ajouter une application ASP.NET Web API projet tooour.

1. Dans l’Explorateur de solutions, cliquez sur **Services** dans hello du projet d’application et choisissez **Ajouter > nouveau Service Service Fabric**.
   
    ![Ajout d’une application de service tooan existant][vs-add-new-service]
2. Sur hello **créer un Service** choisissez **ASP.NET Core** et lui donner un nom.
   
    ![Choix du service web ASP.NET dans la boîte de dialogue hello nouveau service][vs-new-service-dialog]

3. page suivante de Hello fournit un ensemble d’ASP.NET Core modèles de projet. Notez que ceux-ci sont hello même choix que vous verriez si vous avez créé un projet ASP.NET Core en dehors d’une application Service Fabric, avec une petite quantité de code supplémentaire tooregister hello service avec le runtime du Service Fabric hello. Pour ce didacticiel, sélectionnez **API web**. Toutefois, vous pouvez appliquer hello même concepts toobuilding une application web complète.
   
    ![Choix du type de projet ASP.NET][vs-new-aspnet-project-dialog]
   
    Une fois votre projet d’API web créé, vous devriez avoir deux services dans votre application. À mesure que vous toobuild votre application, vous pouvez ajouter davantage de services Bonjour exactement identique. Chacun peut être mis à niveau et faire l'objet d'un contrôle de version indépendamment.

## <a name="run-hello-application"></a>Exécutez l’application hello
tooget une idée de ce que nous avons terminé, nous allons déployer hello nouvelle application et prendre un aspect au comportement par défaut hello hello du modèle de l’API Web ASP.NET principale fournit.

1. Appuyez sur F5 dans Visual Studio toodebug hello application.
2. Lorsque le déploiement est terminé, Visual Studio lance une racine toohello navigateur hello service de l’API Web ASP.NET. modèle de l’API Web ASP.NET principale Hello ne fournit pas par défaut pour la racine de hello, donc vous devez voir une erreur 404 dans le navigateur de hello.
3. Ajouter `/api/values` emplacement toohello dans le navigateur de hello. Il appelle hello `Get` méthode sur hello ValuesController dans le modèle d’API Web hello. Il renvoie la réponse par défaut hello fournie par le modèle hello--un tableau JSON qui contient deux chaînes :
   
    ![Valeurs par défaut retournées par le modèle d’API web ASP.NET Core][browser-aspnet-template-values]
   
    Fin de hello du didacticiel de hello, cette page est sélectionnée par valeur la plus récente compteur hello à partir de notre service avec état, au lieu de hello chaînes par défaut.

## <a name="connect-hello-services"></a>Connecter les services de hello
Service Fabric fournit une flexibilité complète sur votre façon de communiquer avec Reliable Services. Dans une seule application, vous pouvez avoir des services accessibles via TCP, d'autres services accessibles via une API REST HTTP et encore d'autres services qui sont accessibles via des sockets web. Pour plus d’informations sur les options hello disponibles et les inconvénients hello, consultez [communiquer avec les services](service-fabric-connect-and-communicate-with-services.md). Dans ce didacticiel, nous utilisons [communication à distance du Service Service Fabric](service-fabric-reliable-services-communication-remoting.md), fourni dans le Kit de développement logiciel de hello.

Bonjour approche de la communication à distance du Service (modélisée sur les appels de procédure distante ou RPC), vous définissez un tooact interface en tant que contrat public de hello pour le service de hello. Ensuite, vous utilisez ce toogenerate interface une classe proxy pour interagir avec le service de hello.

### <a name="create-hello-remoting-interface"></a>Créer l’interface de communication à distance hello
Commençons par créer hello interface tooact comme contrat hello entre un service avec état hello et d’autres services, dans ce cas hello projet de web ASP.NET Core. Cette interface doit être partagée par tous les services qui utilisent les appels RPC toomake, donc nous allons la créer dans son propre projet de bibliothèque de classes.

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre solution et choisissez **Ajoutez** > **Nouveau projet**.

2. Choisissez hello **Visual C#** entrée Bonjour gauche du volet de navigation et sélectionnez hello **bibliothèque de classes** modèle. Vérifiez cette version de .NET Framework hello est définie trop**4.5.2**.
   
    ![Création d’un projet d’interface de votre service avec état][vs-add-class-library-project]

3. Installer hello **Microsoft.ServiceFabric.Services.Remoting** package NuGet. Recherchez **Microsoft.ServiceFabric.Services.Remoting** dans hello NuGet package manager et l’installer pour tous les projets dans la solution de hello qui utilisent la communication à distance du Service, y compris :
   - projet de bibliothèque de classes Hello qui contient l’interface de service hello
   - projet de Service de Stateful Hello
   - Hello projet de service web ASP.NET Core
   
    ![Ajout du package NuGet de Services hello][vs-services-nuget-package]

4. Dans la bibliothèque de classes hello, créez une interface avec une méthode unique, `GetCountAsync`, et d’étendre l’interface hello de `Microsoft.ServiceFabric.Services.Remoting.IService`. interface de communication à distance Hello doit dériver de cette interface tooindicate qu’il s’agit d’une interface de communication à distance du Service.
   
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

### <a name="implement-hello-interface-in-your-stateful-service"></a>Implémenter l’interface hello dans votre service avec état
Maintenant que nous avons défini l’interface de hello, nous devons tooimplement dans un service avec état hello.

1. Dans votre service avec état, ajoutez le projet de bibliothèque de classes toohello référence qui contient l’interface de hello.
   
    ![Ajout d’un projet de bibliothèque de classes toohello référence dans un service avec état hello][vs-add-class-library-reference]
2. Localiser hello classe qui hérite de `StatefulService`, tel que `MyStatefulService`et l’étendre tooimplement hello `ICounter` interface.
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. Désormais implémenter hello seule méthode qui est définie dans hello `ICounter` interface, `GetCountAsync`.
   
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

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a>Exposer un service avec état hello à l’aide d’un écouteur de la communication à distance du service
Avec hello `ICounter` interface implémentée, étape finale de hello est le canal de communication tooopen hello la communication à distance du Service. Pour les services avec état, Service Fabric fournit une méthode remplaçable appelée `CreateServiceReplicaListeners`. Avec cette méthode, vous pouvez spécifier un ou plusieurs écouteurs de communication, en fonction de type hello de communication que vous souhaitez tooenable pour votre service.

> [!NOTE]
> méthode équivalente Hello pour l’ouverture d’un services de toostateless de canal de communication est appelée `CreateServiceInstanceListeners`.

Dans ce cas, nous remplacer hello `CreateServiceReplicaListeners` méthode et fournir une instance de `ServiceRemotingListener`, ce qui crée un point de terminaison RPC ne peut être appelé à partir de clients via `ServiceProxy`.  

Hello `CreateServiceRemotingListener` méthode d’extension sur hello `IService` interface vous permet de tooeasily créer un `ServiceRemotingListener` avec tous les paramètres par défaut. toouse cette méthode d’extension, assurez-vous d’avoir hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` espace de noms importé. 

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


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a>Utiliser hello ServiceProxy classe toointeract hello service
Notre service avec état est désormais trafic tooreceive prêt à partir d’autres services via RPC. Par conséquent, tout ce qui reste consiste à ajouter toocommunicate de code hello avec lui de hello service web ASP.NET.

1. Dans votre projet ASP.NET, ajouter une bibliothèque de classes toohello référence contenant hello `ICounter` interface.

2. Précédemment, vous avez ajouté hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello projet ASP.NET. Ce package fournit hello `ServiceProxy` classe que vous pouvez utiliser toomake RPC appelle toohello un service avec état. Assurez-vous que ce package NuGet est installé dans le projet de service web ASP.NET Core de hello.

4. Bonjour **contrôleurs** dossier, ouvrez hello `ValuesController` classe. Notez que hello `Get` méthode retourne actuellement simplement un tableau de chaîne codée en dur de « value1 » et « value2 »--qui correspond à ce que nous avons vu plus haut dans le navigateur de hello. Remplacez cette implémentation hello suivant de code :
   
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
   
    Hello première ligne de code est la clé hello. toocreate hello ICounter proxy toohello service avec état, vous devez tooprovide deux informations : un nom de hello et les ID de partition de service de hello.
   
    Vous pouvez utiliser des services avec état tooscale partitionnement en fractionnant leur état dans des compartiments différents, selon une clé que vous définissez, tel qu’un ID de client ou le code postal. Dans notre application complexe, un service avec état hello a uniquement une partition, afin de la clé de hello n’a pas d’importance. N’importe quelle touche que vous fournissez entraîne toohello même partition. toolearn en savoir plus sur le partitionnement des services, consultez [comment toopartition Service des Services de Fabric fiables](service-fabric-concepts-partitioning.md).
   
    nom du service Hello est un URI de l’infrastructure du formulaire hello : /&lt;application_name&gt;/&lt;service_name&gt;.
   
    Avec ces deux types d’informations, l’infrastructure de Service peuvent identifier machine hello qui doivent recevoir les demandes. Hello `ServiceProxy` classe gère également de façon transparente les cas de hello où hello ordinateur qui héberge la partition de service avec état hello connaît une défaillance et un autre ordinateur doit être promue tootake sa place. Rend cette abstraction hello toodeal du code client avec d’autres services beaucoup plus simples.
   
    Une fois les proxy hello, nous appelons simplement hello `GetCountAsync` méthode et retourne son résultat.

5. Appuyez sur F5 à nouveau toorun hello modifié application. Comme précédemment, Visual Studio lance automatiquement racine de toohello hello navigateur de projet web de hello. Ajoutez le chemin d’accès de hello « api/valeurs », et vous devez voir hello valeur actuelle du compteur retourné.
   
    ![valeur de compteur avec état Hello affiché dans l’Explorateur de hello][browser-aspnet-counter-value]
   
    Actualiser le navigateur de hello régulièrement toosee hello compteur valeur mise à jour.

## <a name="kestrel-and-weblistener"></a>Kestrel et WebListener

Bonjour serveur de web ASP.NET Core par défaut, appelé Kestrel, est [non prises en charge pour gérer le trafic internet direct](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel). Par conséquent, hello modèle de service sans état ASP.NET Core pour Service Fabric utilise [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) par défaut. 

toolearn en savoir plus sur Kestrel et WebListener dans les services de l’infrastructure de Service, consultez trop[ASP.NET Core dans Service des Services de Fabric fiables](service-fabric-reliable-services-communication-aspnetcore.md).

## <a name="connecting-tooa-reliable-actor-service"></a>Connexion de service d’acteur fiable tooa
Ce didacticiel s'est concentré sur l'ajout d'un serveur web frontal communiquant avec un service avec état. Toutefois, vous pouvez suivre un tooactors de tootalk modèle très similaires. Lorsque vous créez un projet Reliable Actor, Visual Studio génère automatiquement un projet d’interface pour vous. Vous pouvez utiliser ce toogenerate interface un proxy d’acteur dans toocommunicate de projet web hello avec acteur de hello. canal de communication Hello est fourni automatiquement. Vous n’avez pas besoin toodo n’est pas défini qui est équivalent tooestablishing un `ServiceRemotingListener` comme vous l’avez fait pour un service avec état hello dans ce didacticiel.

## <a name="how-web-services-work-on-your-local-cluster"></a>Fonctionnement des services web sur votre cluster local
En règle générale, vous pouvez déployer exactement hello même Service Fabric application tooa avec plusieurs ordinateurs de cluster que vous avez déployé votre cluster local et hautement avec la certitude qu’elle fonctionne comme prévu. Il s’agit, car votre cluster local est simplement une configuration de cinq nœuds est réduit tooa un seul ordinateur.

Lorsqu’il s’agit des services de tooweb, toutefois, il est une nuance de clé. Lorsque votre cluster se trouve derrière un équilibreur de charge, comme il le fait dans Azure, vous devez vous assurer que vos services web sont déployés sur tous les ordinateurs depuis l’équilibrage de charge hello alternées simplement le trafic sur plusieurs ordinateurs de hello. Cela en définissant un hello `InstanceCount` pour hello service toohello valeur spéciale « -1 ».

En revanche, lorsque vous exécutez un service web localement, vous devez tooensure que seule une instance du service de hello est en cours d’exécution. Dans le cas contraire, vous exécutez en conflit à partir de plusieurs processus qui sont à l’écoute sur hello même chemin d’accès et le port. Par conséquent, le nombre d’instances de hello web service doit être défini trop « 1 » pour les déploiements locaux.

toolearn tooconfigure des valeurs différentes pour un autre environnement, voir [la gestion des paramètres d’application de plusieurs environnements](service-fabric-manage-multiple-environment-app-configuration.md).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez configuré un serveur web frontal pour votre application avec ASP.NET Core, consultez [ASP.NET Core dans le modèle Reliable Services de Service Fabric](service-fabric-reliable-services-communication-aspnetcore.md) pour comprendre comment ASP.NET Core fonctionne avec Service Fabric.

Ensuite, [plus d’informations sur la communication avec les services](service-fabric-connect-and-communicate-with-services.md) en général tooget a terminé d’image de la manière dont service communication fonctionne dans l’infrastructure de Service.

Une fois que vous avez une bonne compréhension du fonctionne de la communication avec le service, [créer un cluster dans Azure et de déployer votre cloud de toohello application](service-fabric-cluster-creation-via-portal.md).

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
