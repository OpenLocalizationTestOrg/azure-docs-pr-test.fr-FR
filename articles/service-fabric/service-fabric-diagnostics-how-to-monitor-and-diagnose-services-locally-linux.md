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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

L’analyse, la détection, le diagnostic et la résolution des problèmes permettent aux services de fonctionner avec une interruption minimale de l’expérience utilisateur. L’analyse et le diagnostic sont essentiels dans un environnement de production réel déployé. L’adoption d’un modèle similaire pendant le développement de services garantit le fonctionnement du pipeline de diagnostic lors du passage à un environnement de production. Service Fabric facilite pour les développeurs de service l’implémentation de diagnostics qui peuvent fonctionner parfaitement aussi bien sur une configuration de développement d’ordinateur local unique que sur une configuration réelle de cluster de production.


## <a name="debugging-service-fabric-java-applications"></a>Débogage des applications Java Service Fabric

Pour les applications Java, [plusieurs frameworks de journalisation](http://en.wikipedia.org/wiki/Java_logging_framework) sont disponibles. Comme `java.util.logging` est l’option par défaut avec l’environnement JRE, elle est également utilisée pour les [exemples de code dans GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).  La suite de cette section explique comment configurer le framework `java.util.logging` .

À l’aide de java.util.logging, vous pouvez rediriger vos journaux d’application vers la mémoire, des flux de sortie, des fichiers de console ou des sockets. Pour chacune de ces options, des gestionnaires par défaut sont déjà fournis dans le framework. Vous pouvez créer un fichier `app.properties` pour configurer le gestionnaire de fichiers de votre application de sorte qu’il redirige tous les journaux dans un fichier local.

L’extrait de code suivant contient un exemple de configuration :

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

Le dossier vers lequel pointe le fichier `app.properties` doit exister. Une fois le fichier `app.properties` créé, vous devez également modifier votre script de point d’entrée, `entrypoint.sh`, dans le dossier `<applicationfolder>/<servicePkg>/Code/` afin de définir la propriété `java.util.logging.config.file` sur le fichier `app.propertes`. L’entrée doit se présenter comme l’extrait de code suivant :

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


Cette configuration se traduit par la collecte des journaux suivant une rotation dans `/tmp/servicefabric/logs/`. Dans ce cas, le fichier journal est nommé mysfapp%u.%g.log, où :
* **%u** est un nombre unique utilisé pour résoudre les conflits entre des processus Java simultanés.
* **%g** est le numéro de génération permettant de différencier des journaux de rotation.

Si aucun gestionnaire n’est configuré explicitement, le gestionnaire de la console est inscrit. Les journaux sont accessible sous /var/log/syslog.

Pour plus d’informations, consultez les [exemples de code dans GitHub](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Débogage des applications C# Service Fabric


Plusieurs infrastructures sont disponibles pour le suivi des applications CoreCLR sur Linux. Pour en savoir plus, consultez [GitHub : journalisation](http:/github.com/aspnet/logging).  EventSource étant familier pour les développeurs C#, cet article utilise EventSource pour le suivi dans des exemples de CoreCLR sur Linux.

La première étape consiste à inclure System.Diagnostics.Tracing afin que vous puissiez écrire vos journaux dans une mémoire, des flux de sortie ou des fichiers de console.  Pour la journalisation à l’aide d’EventSource, ajoutez le projet suivant à votre project.json :

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

Vous pouvez utiliser un EventListener personnalisé pour écouter l’événement de service, puis le rediriger de manière appropriée vers des fichiers de trace. L’extrait de code suivant montre un exemple d’implémentation de la journalisation à l’aide d’EventSource et d’un EventListener personnalisé :


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


L’extrait de code précédent sort les journaux dans un fichier `/tmp/MyServiceLog.txt`. Ce nom de fichier doit être correctement mis à jour. Au cas où vous souhaitez rediriger les journaux vers la console, utilisez l’extrait de code suivant dans votre classe EventListener personnalisée :

```csharp
public static TextWriter Out = Console.Out;
```

Les exemples dans [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) utilisent EventSource et un EventListener personnalisé pour consigner des événements dans un fichier.



## <a name="next-steps"></a>Étapes suivantes
Le code de suivi ajouté à votre application fonctionne également pour le diagnostic de votre application sur un cluster Microsoft Azure. Consultez ces articles qui traitent des différentes options pour les outils et décrivent comment les configurer.
* [Collecte des journaux avec Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md)
