---
title: aaaDebug microservices Azure dans Linux | Documents Microsoft
description: "Découvrez comment toomonitor et diagnostiquer vos services écrits à l’aide de Microsoft Azure Service Fabric sur un ordinateur de développement local."
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
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="27b41-103">Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="27b41-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="27b41-104">Windows</span><span class="sxs-lookup"><span data-stu-id="27b41-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="27b41-105">Linux</span><span class="sxs-lookup"><span data-stu-id="27b41-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="27b41-106">Surveillance, détection, diagnostic et résolution des problèmes permettent toocontinue de services avec l’expérience de l’utilisateur toohello perturbations minimales.</span><span class="sxs-lookup"><span data-stu-id="27b41-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="27b41-107">L’analyse et le diagnostic sont essentiels dans un environnement de production réel déployé.</span><span class="sxs-lookup"><span data-stu-id="27b41-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="27b41-108">Adoption d’un modèle semblable au cours du développement de services garantit que ce pipeline diagnostic hello fonctionne lorsque vous déplacez l’environnement de production tooa.</span><span class="sxs-lookup"><span data-stu-id="27b41-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="27b41-109">Service Fabric facilite les diagnostics tooimplement service aux développeurs qui peut fonctionner en toute transparence aux configurations de développement local d’ordinateur unique et configurations de cluster de production réel.</span><span class="sxs-lookup"><span data-stu-id="27b41-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="27b41-110">Débogage des applications Java Service Fabric</span><span class="sxs-lookup"><span data-stu-id="27b41-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="27b41-111">Pour les applications Java, [plusieurs frameworks de journalisation](http://en.wikipedia.org/wiki/Java_logging_framework) sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="27b41-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="27b41-112">Étant donné que `java.util.logging` est l’option par défaut de hello avec hello JRE, il est également utilisé pour hello [code exemples dans github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="27b41-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="27b41-113">Hello discussion suivante explique comment tooconfigure hello `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="27b41-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="27b41-114">À l’aide de java.util.logging, vous pouvez rediriger votre application enregistre toomemory, les flux de sortie, les fichiers de la console ou les sockets.</span><span class="sxs-lookup"><span data-stu-id="27b41-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="27b41-115">Pour chacune de ces options, il existe gestionnaires par défaut déjà fournies dans le cadre de hello.</span><span class="sxs-lookup"><span data-stu-id="27b41-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="27b41-116">Vous pouvez créer un `app.properties` Gestionnaire de fichier fichier tooconfigure hello pour votre application de tooredirect tous les journaux tooa des fichiers locaux.</span><span class="sxs-lookup"><span data-stu-id="27b41-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="27b41-117">Hello suivant extrait de code contient un exemple de configuration :</span><span class="sxs-lookup"><span data-stu-id="27b41-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="27b41-118">Bonjour Bonjour de pointe tooby dossier `app.properties` fichier doit exister.</span><span class="sxs-lookup"><span data-stu-id="27b41-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="27b41-119">Après avoir hello `app.properties` fichier est créé, vous devez tooalso modifier votre script de point d’entrée, `entrypoint.sh` Bonjour `<applicationfolder>/<servicePkg>/Code/` propriété hello du dossier tooset `java.util.logging.config.file` trop`app.propertes` fichier.</span><span class="sxs-lookup"><span data-stu-id="27b41-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="27b41-120">entrée de Hello doit ressembler à hello suivant extrait de code :</span><span class="sxs-lookup"><span data-stu-id="27b41-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="27b41-121">Cette configuration se traduit par la collecte des journaux suivant une rotation dans `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="27b41-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="27b41-122">fichier de journal Hello dans ce cas est nommé mysfapp%u.%g.log où :</span><span class="sxs-lookup"><span data-stu-id="27b41-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="27b41-123">**%u** est un tooresolve numéro unique conflits entre les processus simultanés de Java.</span><span class="sxs-lookup"><span data-stu-id="27b41-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="27b41-124">**%g** est toodistinguish numéro de génération hello entre la rotation des journaux.</span><span class="sxs-lookup"><span data-stu-id="27b41-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="27b41-125">Si aucun gestionnaire n’est explicitement configuré, Gestionnaire de la console hello est enregistré par défaut.</span><span class="sxs-lookup"><span data-stu-id="27b41-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="27b41-126">Un peut afficher les journaux hello dans syslog sous /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="27b41-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="27b41-127">Pour plus d’informations, consultez hello [code exemples dans github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="27b41-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="27b41-128">Débogage des applications C# Service Fabric</span><span class="sxs-lookup"><span data-stu-id="27b41-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="27b41-129">Plusieurs infrastructures sont disponibles pour le suivi des applications CoreCLR sur Linux.</span><span class="sxs-lookup"><span data-stu-id="27b41-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="27b41-130">Pour en savoir plus, consultez [GitHub : journalisation](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="27b41-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="27b41-131">EventSource étant, les développeurs familiers tooC #' cet article utilise EventSource pour le traçage dans les exemples de CoreCLR sur Linux.</span><span class="sxs-lookup"><span data-stu-id="27b41-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="27b41-132">première étape de Hello est tooinclude System.Diagnostics.Tracing afin que vous pouvez écrire vos journaux toomemory, flux de sortie ou des fichiers de la console.</span><span class="sxs-lookup"><span data-stu-id="27b41-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="27b41-133">Pour la journalisation à l’aide de la source d’événement, ajoutez hello suivant project.json tooyour de projet :</span><span class="sxs-lookup"><span data-stu-id="27b41-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="27b41-134">Vous pouvez utiliser un toolisten EventListener personnalisé pour l’événement de service hello et puis correctement les redirige les fichiers tootrace.</span><span class="sxs-lookup"><span data-stu-id="27b41-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="27b41-135">Hello extrait de code suivant montre un exemple d’implémentation de journalisation à l’aide de la source d’événement et un EventListener personnalisé :</span><span class="sxs-lookup"><span data-stu-id="27b41-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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

        // TBD: Need tooadd method for sample event.

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


<span data-ttu-id="27b41-136">Hello extrait de code précédent génère des fichiers de tooa journaux hello dans `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="27b41-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="27b41-137">Ce nom de fichier doit toobe correctement mises à jour.</span><span class="sxs-lookup"><span data-stu-id="27b41-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="27b41-138">Au cas où vous souhaiteriez tooredirect hello journaux tooconsole, utilisez hello suivant extrait de code dans votre classe de EventListener personnalisé :</span><span class="sxs-lookup"><span data-stu-id="27b41-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="27b41-139">Hello exemples à [exemples c#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) utiliser EventSource et un fichier de tooa EventListener toolog événements personnalisé.</span><span class="sxs-lookup"><span data-stu-id="27b41-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="27b41-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="27b41-140">Next steps</span></span>
<span data-ttu-id="27b41-141">Hello ajouté le même code de traçage tooyour application fonctionne également avec les diagnostics hello de votre application sur un cluster Azure.</span><span class="sxs-lookup"><span data-stu-id="27b41-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="27b41-142">Extraction de ces articles qui traitent de hello différentes options pour les outils hello et décrivent comment tooset de.</span><span class="sxs-lookup"><span data-stu-id="27b41-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="27b41-143">Mode de journalisation des toocollect avec Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="27b41-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
