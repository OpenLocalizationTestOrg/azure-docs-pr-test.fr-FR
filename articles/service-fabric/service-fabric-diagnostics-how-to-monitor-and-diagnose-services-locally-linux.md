---
title: "Déboguer les microservices Azure dans Linux | Microsoft Docs"
description: "Découvrez comment analyser et diagnostiquer vos services écrits à l’aide de Microsoft Azure Service Fabric sur un ordinateur de développement local."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4bc73f581f4855ebc724df19dd56fab8bf103854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="06d1d-103">Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="06d1d-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="06d1d-104">Windows</span><span class="sxs-lookup"><span data-stu-id="06d1d-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="06d1d-105">Linux</span><span class="sxs-lookup"><span data-stu-id="06d1d-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="06d1d-106">L’analyse, la détection, le diagnostic et la résolution des problèmes permettent aux services de fonctionner avec une interruption minimale de l’expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="06d1d-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="06d1d-107">L’analyse et le diagnostic sont essentiels dans un environnement de production réel déployé.</span><span class="sxs-lookup"><span data-stu-id="06d1d-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="06d1d-108">L’adoption d’un modèle similaire pendant le développement de services garantit le fonctionnement du pipeline de diagnostic lors du passage à un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="06d1d-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="06d1d-109">Service Fabric facilite pour les développeurs de service l’implémentation de diagnostics qui peuvent fonctionner parfaitement aussi bien sur une configuration de développement d’ordinateur local unique que sur une configuration réelle de cluster de production.</span><span class="sxs-lookup"><span data-stu-id="06d1d-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="06d1d-110">Débogage des applications Java Service Fabric</span><span class="sxs-lookup"><span data-stu-id="06d1d-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="06d1d-111">Pour les applications Java, [plusieurs frameworks de journalisation](http://en.wikipedia.org/wiki/Java_logging_framework) sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="06d1d-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="06d1d-112">Comme `java.util.logging` est l’option par défaut avec l’environnement JRE, elle est également utilisée pour les [exemples de code dans GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="06d1d-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="06d1d-113">La suite de cette section explique comment configurer le framework `java.util.logging` .</span><span class="sxs-lookup"><span data-stu-id="06d1d-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="06d1d-114">À l’aide de java.util.logging, vous pouvez rediriger vos journaux d’application vers la mémoire, des flux de sortie, des fichiers de console ou des sockets.</span><span class="sxs-lookup"><span data-stu-id="06d1d-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="06d1d-115">Pour chacune de ces options, des gestionnaires par défaut sont déjà fournis dans le framework.</span><span class="sxs-lookup"><span data-stu-id="06d1d-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="06d1d-116">Vous pouvez créer un fichier `app.properties` pour configurer le gestionnaire de fichiers de votre application de sorte qu’il redirige tous les journaux dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="06d1d-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="06d1d-117">L’extrait de code suivant contient un exemple de configuration :</span><span class="sxs-lookup"><span data-stu-id="06d1d-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="06d1d-118">Le dossier vers lequel pointe le fichier `app.properties` doit exister.</span><span class="sxs-lookup"><span data-stu-id="06d1d-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="06d1d-119">Une fois le fichier `app.properties` créé, vous devez également modifier votre script de point d’entrée, `entrypoint.sh`, dans le dossier `<applicationfolder>/<servicePkg>/Code/` afin de définir la propriété `java.util.logging.config.file` sur le fichier `app.propertes`.</span><span class="sxs-lookup"><span data-stu-id="06d1d-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="06d1d-120">L’entrée doit se présenter comme l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="06d1d-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="06d1d-121">Cette configuration se traduit par la collecte des journaux suivant une rotation dans `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="06d1d-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="06d1d-122">Dans ce cas, le fichier journal est nommé mysfapp%u.%g.log, où :</span><span class="sxs-lookup"><span data-stu-id="06d1d-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="06d1d-123">**%u** est un nombre unique utilisé pour résoudre les conflits entre des processus Java simultanés.</span><span class="sxs-lookup"><span data-stu-id="06d1d-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="06d1d-124">**%g** est le numéro de génération permettant de différencier des journaux de rotation.</span><span class="sxs-lookup"><span data-stu-id="06d1d-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="06d1d-125">Si aucun gestionnaire n’est configuré explicitement, le gestionnaire de la console est inscrit.</span><span class="sxs-lookup"><span data-stu-id="06d1d-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="06d1d-126">Les journaux sont accessible sous /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="06d1d-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="06d1d-127">Pour plus d’informations, consultez les [exemples de code dans GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="06d1d-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="06d1d-128">Débogage des applications C# Service Fabric</span><span class="sxs-lookup"><span data-stu-id="06d1d-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="06d1d-129">Plusieurs infrastructures sont disponibles pour le suivi des applications CoreCLR sur Linux.</span><span class="sxs-lookup"><span data-stu-id="06d1d-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="06d1d-130">Pour en savoir plus, consultez [GitHub : journalisation](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="06d1d-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="06d1d-131">EventSource étant familier pour les développeurs C#, cet article utilise EventSource pour le suivi dans des exemples de CoreCLR sur Linux.</span><span class="sxs-lookup"><span data-stu-id="06d1d-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="06d1d-132">La première étape consiste à inclure System.Diagnostics.Tracing afin que vous puissiez écrire vos journaux dans une mémoire, des flux de sortie ou des fichiers de console.</span><span class="sxs-lookup"><span data-stu-id="06d1d-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="06d1d-133">Pour la journalisation à l’aide d’EventSource, ajoutez le projet suivant à votre project.json :</span><span class="sxs-lookup"><span data-stu-id="06d1d-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="06d1d-134">Vous pouvez utiliser un EventListener personnalisé pour écouter l’événement de service, puis le rediriger de manière appropriée vers des fichiers de trace.</span><span class="sxs-lookup"><span data-stu-id="06d1d-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="06d1d-135">L’extrait de code suivant montre un exemple d’implémentation de la journalisation à l’aide d’EventSource et d’un EventListener personnalisé :</span><span class="sxs-lookup"><span data-stu-id="06d1d-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need to add method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="06d1d-136">L’extrait de code précédent sort les journaux dans un fichier `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="06d1d-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="06d1d-137">Ce nom de fichier doit être correctement mis à jour.</span><span class="sxs-lookup"><span data-stu-id="06d1d-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="06d1d-138">Au cas où vous souhaitez rediriger les journaux vers la console, utilisez l’extrait de code suivant dans votre classe EventListener personnalisée :</span><span class="sxs-lookup"><span data-stu-id="06d1d-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="06d1d-139">Les exemples dans [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) utilisent EventSource et un EventListener personnalisé pour consigner des événements dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="06d1d-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="06d1d-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06d1d-140">Next steps</span></span>
<span data-ttu-id="06d1d-141">Le code de suivi ajouté à votre application fonctionne également pour le diagnostic de votre application sur un cluster Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="06d1d-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="06d1d-142">Consultez ces articles qui traitent des différentes options pour les outils et décrivent comment les configurer.</span><span class="sxs-lookup"><span data-stu-id="06d1d-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="06d1d-143">Collecte des journaux avec Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="06d1d-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
