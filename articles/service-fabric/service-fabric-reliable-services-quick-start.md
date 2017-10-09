---
title: "aaaCreate votre première application de Service Fabric en C# | Documents Microsoft"
description: "Introduction toocreating une application Microsoft Azure Service Fabric avec et sans état des services."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a>Prise en main de Reliable Services
> [!div class="op_single_selector"]
> * [C# sur Windows](service-fabric-reliable-services-quick-start.md)
> * [Java sur Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

Une application Azure Service Fabric contient un ou plusieurs services qui exécutent votre code. Ce guide vous montre comment toocreate avec et sans état des applications de Service Fabric avec [des Services fiables](service-fabric-reliable-services-introduction.md).  Cette vidéo Microsoft Virtual Academy montre également comment toocreate un service fiable sans état :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965">  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a>Concepts de base
tooget en main des Services fiables, vous seulement devez toounderstand quelques concepts de base :

* **Type de service** : il s’agit de l’implémentation de votre service. Il est défini par la classe hello vous écrivez qui étend `StatelessService` et tout autre code ou les dépendances utilisés ici, avec un nom et un numéro de version.
* **Instance de service nommée**: toorun votre service, vous créez des instances nommées de votre type de service, beaucoup comme vous créez des instances d’objet d’un type de classe. Une instance de service a un nom sous forme de hello d’un URI à l’aide de hello « fabric : / « schéma, tel que « fabric : / MyApp/MyService ».
* **Hôte de service**: hello nommé des instances de service que vous créez toorun nécessaire à l’intérieur d’un processus hôte. hôte de service Hello est simplement un processus dans lequel les instances de votre service peuvent exécuter.
* **Inscription du service** : l’inscription rassemble tous les éléments. Hello service type doit être inscrit avec hello Service Fabric runtime dans un service hôte tooallow Service Fabric toocreate ses instances toorun.  

## <a name="create-a-stateless-service"></a>Création d'un service sans état
Un service sans état est un type de service est actuellement la norme hello dans les applications de cloud. Il est considéré comme sans état, car le service hello lui-même ne contienne pas de données qui doit toobe stockées de manière fiable ou hautement disponible. Si une instance d’un service sans état est arrêtée, tout son état interne est perdu. Dans ce type de service, état doit être persistante tooan magasin externe, telles que les Tables Azure ou d’une base de données SQL, pour qu’il toobe apportées hautement fiable et disponible.

Lancez Visual Studio 2015 ou Visual Studio 2017 en tant qu’administrateur et créez un projet d’application Service Fabric nommé *HelloWorld*:

![Utilisez toocreate de boîte dialogue hello nouveau projet une nouvelle application de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

Créez ensuite un projet de service sans état nommé *HelloWorldStateless*:

![Dans la deuxième boîte de dialogue hello, créez un projet de service sans état](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

Votre solution contient maintenant deux projets :

* *HelloWorld*. Il s’agit de hello *application* projet qui contient votre *services*. Il contient également le manifeste de l’application hello décrivant application hello, ainsi que d’un nombre de scripts PowerShell qui vous aident à toodeploy votre application.
* *HelloWorldStateless*. Il s’agit de projet de service hello. Il contient d’implémentation de service sans état hello.

## <a name="implement-hello-service"></a>Implémenter le service de hello
Ouvrez hello **HelloWorldStateless.cs** fichier dans le projet de service hello. Dans Service Fabric, un service peut exécuter n’importe quelle logique métier. API de service Hello fournit deux points d’entrée pour votre code :

* Une méthode de point d’entrée de durée indéterminée appelée *RunAsync*avec laquelle vous pouvez commencer l’exécution de toute charge de travail, y compris les charges de travail de calcul de longue durée.

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* Un point d’entrée de communication où vous pouvez connecter votre pile de communication, notamment ASP.NET Core. C’est là que vous pouvez commencer à recevoir des demandes des utilisateurs et des autres services.

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

Dans ce didacticiel, nous allons nous concentrer sur hello `RunAsync()` méthode point d’entrée. C’est là que vous pouvez commencer immédiatement à exécuter votre code.
modèle de projet Hello inclut un exemple d’implémentation de `RunAsync()` qui incrémente un compteur propagée.

> [!NOTE]
> Pour plus d’informations sur la façon dont la pile toowork avec une communication, consultez [services API Web du Service Fabric avec OWIN auto-hébergement](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a>RunAsync
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

plateforme de Hello appelle cette méthode lorsqu’une instance d’un service est tooexecute endroit et est prêt. Pour un service sans état, cela signifie simplement lors de l’instance de service hello est ouverte. Un jeton d’annulation est fourni toocoordinate lorsque votre instance de service doit toobe fermé. Dans l’infrastructure de Service, ce cycle d’ouverture/fermeture d’une instance de service peut se produire plusieurs fois sur la durée de vie hello du service de hello dans sa globalité. Il existe diverses raisons à cela, notamment :

* système de Hello déplace vos instances de service pour l’équilibrage des ressources.
* Des erreurs surviennent dans votre code.
* application Hello ou système est mis à niveau.
* matériel sous-jacent de Hello connaît une panne.

Cette orchestration est gérée par hello système tookeep votre service hautement disponible et correctement à charge équilibrée.

`RunAsync()` ne doit pas se bloquer de façon synchrone. Votre implémentation de RunAsync doit retourner une tâche ou await sur n’importe quel toocontinue d’exécution des opérations longues ou blocage tooallow hello. Remarque Bonjour `while(true)` boucle dans l’exemple précédent hello, qui retourne une tâche `await Task.Delay()` est utilisé. Si votre charge de travail doit se bloquer de façon synchrone, vous devez planifier une tâche avec `Task.Run()` dans votre implémentation de `RunAsync`.

L’annulation de votre charge de travail est un effort conjoint orchestré par hello fourni le jeton d’annulation. système de Hello attend votre tooend tâche (par la réussite, l’annulation ou erreur) avant de poursuivre. Il est important toohonor hello annulation jeton, terminer un travail et quitter `RunAsync()` aussi rapidement que possible lorsque le système de hello demande l’annulation.

Dans cet exemple de service sans état, nombre de hello est stocké dans une variable locale. Mais comme il s’agit d’un service sans état, valeur hello stockée existe uniquement pour hello en cours du cycle de vie de son instance de service. Lorsque le service de hello déplace ou redémarre, la valeur de hello est perdue.

## <a name="create-a-stateful-service"></a>Création d'un service avec état
Service Fabric introduit un nouveau type de service qui est avec état. Un service avec état permettre conserver l’état fiable dans service hello lui-même, colocalisé avec le code hello qui l’utilise. État est hautement disponible par l’infrastructure de Service sans confirmation hello besoin toopersist tooan externe le magasin d’état.

tooconvert une valeur de compteur de toohighly sans état disponible et permanente, même lorsque le service de hello déplace ou redémarre, vous devez un service avec état.

Dans hello même *HelloWorld* application, vous pouvez ajouter un nouveau service en cliquant sur les références de Services hello dans le projet d’application hello et en sélectionnant **Ajouter -> nouveau Service Service Fabric**.

![Ajouter un tooyour service application Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

Sélectionnez **Service avec état** et nommez-le *HelloWorldStateful*. Cliquez sur **OK**.

![Utilisez toocreate de boîte dialogue hello nouveau projet un nouveau service avec état Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

Votre application devez maintenant avoir deux services : hello service sans état *HelloWorldStateless* et un service avec état hello *HelloWorldStateful*.

Un service avec état a hello même points d’entrée comme un service sans état. Hello principale différence est la disponibilité de hello d’un *fournisseur d’état* qui peuvent stocker l’état fiable. L’infrastructure de service est fourni avec une implémentation de fournisseur d’état appelée [Collections fiable](service-fabric-reliable-services-reliable-collections.md), ce qui vous permet de créer des structures de données répliquées via hello fiable Gestionnaire d’état. Un Reliable Service avec état utilise ce fournisseur d’état par défaut.

Ouvrez **HelloWorldStateful.cs** dans *HelloWorldStateful*, qui contient hello RunAsync méthode :

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a>RunAsync
`RunAsync()` fonctionne de la même façon dans les services avec ou sans état. Toutefois, dans un service avec état, plateforme de hello exécute une tâche supplémentaire de votre part avant d’exécuter `RunAsync()`. Ce travail peut notamment s’assurer de ce gestionnaire d’état fiable hello et fiable de Collections sont toouse prêt.

### <a name="reliable-collections-and-hello-reliable-state-manager"></a>Fiable des Collections et hello fiable Gestionnaire d’état
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) est une implémentation de dictionnaire qui vous permet de stocker l’état de tooreliably dans le service hello. Avec l’infrastructure de Service et les Collections fiable, vous pouvez stocker des données directement dans votre service sans avoir besoin de hello pour un magasin persistant externe. Les Reliable Collections rendent vos données hautement disponibles. Pour ce faire, Service Fabric crée et gère plusieurs *réplicas* de votre service pour vous. Il fournit également une API qui résume les complexités hello éloignée de la gestion de ces réplicas et les transitions d’état.

Les collections fiables peuvent stocker n’importe quel type .NET, y compris vos types personnalisés, avec quelques inconvénients :

* Service Fabric rend votre état hautement disponible par *réplication* stockage de vos données toolocal disque l’état entre les nœuds et fiable sur chaque réplica. Cela signifie que tout ce qui est stocké dans les Reliable Collections doit être *sérialisable*. Par défaut, les Collections fiables utilisent [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) pour la sérialisation, il est donc important toomake assurer que vos types sont [pris en charge par le sérialiseur de contrat de données de hello](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) lorsque vous utilisez la valeur par défaut de hello sérialiseur.
* Les objets sont répliqués à des fins de haute disponibilité quand vous envoyez des transactions sur des collections fiables. Les objets stockés dans les collections fiables sont conservés dans la mémoire locale de votre service. Cela signifie que vous disposez d’un objet de toohello référence locale.
  
   Il est important que vous mute pas les instances locales de ces objets sans effectuer une opération de mise à jour de collection fiable de hello dans une transaction. Il s’agit, car les instances de toolocal de modifications d’objets ne seront pas répliquées automatiquement. Vous devez Réinsérez les objet hello dans le dictionnaire de hello ou utilisez une des hello *mettre à jour* méthodes sur le dictionnaire de hello.

Hello Gestionnaire d’état fiable gère les Collections fiable pour vous. Vous pouvez simplement demander hello fiable Gestionnaire d’état pour un regroupement fiable par nom à tout moment et en tout lieu dans votre service. Hello fiable Gestionnaire d’état permet de s’assurer que vous obtenez une référence arrière. Nous ne recommandé d’enregistrer les références d’instances de collection tooreliable dans les variables de membre de classe ou de propriétés. Une attention particulière doit prendre tooensure hello référence est définie tooan instance à tout moment dans le cycle de vie hello service. Hello Gestionnaire d’état fiable gère ce travail pour vous, et il est optimisé pour les visites de répétitions.

### <a name="transactional-and-asynchronous-operations"></a>Opérations transactionnelles et asynchrones
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

Collections fiables possèdent de nombreuses hello mêmes opérations que leurs `System.Collections.Generic` et `System.Collections.Concurrent` équivalents, excepté LINQ. Les opérations sur les Reliable Collections sont asynchrones. Il s’agit, car les opérations d’écriture avec des Collections fiable effectuer tooreplicate d’opérations d’e/s et rendre persistantes des données toodisk.

Les opérations des Reliable Collections sont *transactionnelles*. Ainsi, vous pouvez conserver un état cohérent entre plusieurs Reliable Collections et opérations. Par exemple, vous pouvez enlever un élément de travail à partir d’une file d’attente fiable, effectuer une opération sur lui et enregistrer le résultat de hello dans un dictionnaire fiable, toutes les tâches dans une transaction unique. Il est considéré comme une opération atomique, et elle garantit que toute l’opération hello réussira ou annule toute l’opération hello. Si une erreur se produit une fois que vous enlever les éléments hello mais avant d’enregistrer le résultat de hello, hello toute transaction est annulée et l’élément hello conserve dans la file d’attente hello pour le traitement.

## <a name="run-hello-application"></a>Exécutez l’application hello
Nous renvoyons maintenant toohello *HelloWorld* application. Vous pouvez désormais générer et déployer vos services. Lorsque vous appuyez sur **F5**, votre application sera cluster local de tooyour générées et déployées.

Après le démarrage en cours d’exécution des services hello, vous pouvez afficher les événements de suivi d’événements pour Windows (ETW) hello généré dans un **des événements de Diagnostic** fenêtre. Notez que les événements hello affichés sont à partir d’un service sans état hello et un service avec état dans une application hello hello. Vous pouvez interrompre le flux de données hello en cliquant sur hello **suspendre** bouton. Vous pouvez ensuite examiner les détails hello d’un message en développant ce message.

> [!NOTE]
> Avant d’exécuter application hello, assurez-vous que vous disposez d’un cluster de développement local en cours d’exécution. Extraire hello [mise en route](service-fabric-get-started.md) pour plus d’informations sur la configuration de votre environnement local.
> 
> 

![Afficher les événements de diagnostic dans Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a>Étapes suivantes
[Déboguer votre application Service Fabric dans Visual Studio](service-fabric-debugging-your-application.md)

[Prise en main : services de l’API Web Service Fabric avec auto-hébergement OWIN](service-fabric-reliable-services-communication-webapi.md)

[En savoir plus sur les Collections fiables](service-fabric-reliable-services-reliable-collections.md)

[Déployer une application](service-fabric-deploy-remove-applications.md)

[Mise à niveau de l’application](service-fabric-application-upgrade.md)

[Référence du développeur pour les services fiables](https://msdn.microsoft.com/library/azure/dn706529.aspx)

