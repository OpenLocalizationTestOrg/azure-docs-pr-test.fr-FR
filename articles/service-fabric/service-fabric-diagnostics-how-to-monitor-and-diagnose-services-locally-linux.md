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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

Surveillance, détection, diagnostic et résolution des problèmes permettent toocontinue de services avec l’expérience de l’utilisateur toohello perturbations minimales. L’analyse et le diagnostic sont essentiels dans un environnement de production réel déployé. Adoption d’un modèle semblable au cours du développement de services garantit que ce pipeline diagnostic hello fonctionne lorsque vous déplacez l’environnement de production tooa. Service Fabric facilite les diagnostics tooimplement service aux développeurs qui peut fonctionner en toute transparence aux configurations de développement local d’ordinateur unique et configurations de cluster de production réel.


## <a name="debugging-service-fabric-java-applications"></a>Débogage des applications Java Service Fabric

Pour les applications Java, [plusieurs frameworks de journalisation](http://en.wikipedia.org/wiki/Java_logging_framework) sont disponibles. Étant donné que `java.util.logging` est l’option par défaut de hello avec hello JRE, il est également utilisé pour hello [code exemples dans github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Hello discussion suivante explique comment tooconfigure hello `java.util.logging` framework.

À l’aide de java.util.logging, vous pouvez rediriger votre application enregistre toomemory, les flux de sortie, les fichiers de la console ou les sockets. Pour chacune de ces options, il existe gestionnaires par défaut déjà fournies dans le cadre de hello. Vous pouvez créer un `app.properties` Gestionnaire de fichier fichier tooconfigure hello pour votre application de tooredirect tous les journaux tooa des fichiers locaux.

Hello suivant extrait de code contient un exemple de configuration :

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

Bonjour Bonjour de pointe tooby dossier `app.properties` fichier doit exister. Après avoir hello `app.properties` fichier est créé, vous devez tooalso modifier votre script de point d’entrée, `entrypoint.sh` Bonjour `<applicationfolder>/<servicePkg>/Code/` propriété hello du dossier tooset `java.util.logging.config.file` trop`app.propertes` fichier. entrée de Hello doit ressembler à hello suivant extrait de code :

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


Cette configuration se traduit par la collecte des journaux suivant une rotation dans `/tmp/servicefabric/logs/`. fichier de journal Hello dans ce cas est nommé mysfapp%u.%g.log où :
* **%u** est un tooresolve numéro unique conflits entre les processus simultanés de Java.
* **%g** est toodistinguish numéro de génération hello entre la rotation des journaux.

Si aucun gestionnaire n’est explicitement configuré, Gestionnaire de la console hello est enregistré par défaut. Un peut afficher les journaux hello dans syslog sous /var/log/syslog.

Pour plus d’informations, consultez hello [code exemples dans github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Débogage des applications C# Service Fabric


Plusieurs infrastructures sont disponibles pour le suivi des applications CoreCLR sur Linux. Pour en savoir plus, consultez [GitHub : journalisation](http:/github.com/aspnet/logging).  EventSource étant, les développeurs familiers tooC #' cet article utilise EventSource pour le traçage dans les exemples de CoreCLR sur Linux.

première étape de Hello est tooinclude System.Diagnostics.Tracing afin que vous pouvez écrire vos journaux toomemory, flux de sortie ou des fichiers de la console.  Pour la journalisation à l’aide de la source d’événement, ajoutez hello suivant project.json tooyour de projet :

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

Vous pouvez utiliser un toolisten EventListener personnalisé pour l’événement de service hello et puis correctement les redirige les fichiers tootrace. Hello extrait de code suivant montre un exemple d’implémentation de journalisation à l’aide de la source d’événement et un EventListener personnalisé :


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


Hello extrait de code précédent génère des fichiers de tooa journaux hello dans `/tmp/MyServiceLog.txt`. Ce nom de fichier doit toobe correctement mises à jour. Au cas où vous souhaiteriez tooredirect hello journaux tooconsole, utilisez hello suivant extrait de code dans votre classe de EventListener personnalisé :

```csharp
public static TextWriter Out = Console.Out;
```

Hello exemples à [exemples c#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) utiliser EventSource et un fichier de tooa EventListener toolog événements personnalisé.



## <a name="next-steps"></a>Étapes suivantes
Hello ajouté le même code de traçage tooyour application fonctionne également avec les diagnostics hello de votre application sur un cluster Azure. Extraction de ces articles qui traitent de hello différentes options pour les outils hello et décrivent comment tooset de.
* [Mode de journalisation des toocollect avec Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md)
