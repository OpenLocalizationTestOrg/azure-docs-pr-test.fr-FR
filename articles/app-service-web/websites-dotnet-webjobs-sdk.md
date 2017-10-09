---
title: aaaWhat est hello Azure WebJobs SDK
description: "Une présentation toohello Kit de développement logiciel Azure WebJobs. Explique le hello SDK, scénarios classiques, qu'il est utile pour, et exemples de code."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>Nouveautés hello Azure WebJobs SDK
## <a id="overview"></a>Vue d’ensemble
Cet article explique ce que hello WebJobs SDK est, passe en revue quelques scénarios courants, il est utile pour et donne une vue d’ensemble de la façon dont vous l’utiliser dans votre code.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[Les tâches Web](websites-webjobs-resources.md) est une fonctionnalité du Service Azure App qui vous permet de toorun un programme ou un script Bonjour même contexte qu’une application web, une application API ou une application mobile. Hello d’objectif de hello [WebJobs SDK](websites-webjobs-resources.md) est toosimplify hello code que vous écrivez pour les tâches courantes qu’une tâche Web peut effectuer, telles que le traitement d’image, traitement de la file d’attente, agrégation RSS, maintenance des fichiers et de l’envoi des messages électroniques. Hello WebJobs SDK inclut des fonctionnalités intégrées pour de nombreux autres scénarios courants pour travailler avec le stockage Azure et Service Bus et pour la planification des tâches et la gestion des erreurs. En outre, il est conçu toobe extensible. Hello [WebJobs SDK est open source](https://github.com/Azure/azure-webjobs-sdk/)et qu’il existe un [référentiel open source pour les extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Hello WebJobs SDK inclut hello suivant des composants :

* **Packages NuGet**. Les packages NuGet que vous ajoutez le projet d’Application Console Visual Studio tooa fournissent un cadre qui utilise votre code en décorant vos méthodes avec des attributs de WebJobs SDK.
* **Tableau de bord**. Partie de hello WebJobs SDK est inclus dans Azure App Service et fournit une surveillance avancée et diagnostics pour les programmes qui utilisent les packages NuGet hello. Vous n’avez toowrite code toouse ces fonctionnalités d’analyse et de diagnostics.

## <a id="scenarios"></a>Scénarios
Voici quelques scénarios classiques, que vous pouvez gérer plus facilement avec hello Azure WebJobs SDK :

* Traitement d'images ou autres tâches imposant une forte charge au processeur. Une fonctionnalité courante des sites Web est hello capacité tooupload images ou des vidéos. Fréquence à laquelle vous souhaitez que de contenu de hello toomanipulate après son téléchargement, mais vous ne souhaitez pas toomake hello utilisateur Patientez pendant que vous effectuez qui.
* Traitement de files d'attente. Une méthode courante pour un toocommunicate de serveur frontal web avec un service principal est toouse les files d’attente. Lorsque le site Web de hello doit tooget le travail effectué, il transmet un message dans une file d’attente. Un service principal extrait les messages de la file d’attente hello et hello de travail. Vous pouvez utiliser les files d’attente pour le traitement d’image : par exemple, une fois que l’utilisateur de hello télécharge un nombre de fichiers, placez les noms de fichiers hello dans un toobe de message de file d’attente récupéré par le principal hello pour le traitement. Ou bien, vous pouvez utiliser la réactivité de files d’attente tooimprove site. Par exemple, au lieu d’écrire directement la base de données SQL tooa, écrivez la file d’attente tooa, indiquer à l’utilisateur de hello vous avez terminé et permettre de travailler hello principal service handle à latence élevée base de données relationnelle. Pour obtenir un exemple de file d’attente de traitement avec des processus de l’image, consultez hello [tâches Web SDK prise en main de didacticiel](websites-dotnet-webjobs-sdk-get-started.md).
* Agrégation RSS. Si vous avez un site qui gère une liste de flux RSS, vous pourriez extraire dans tous les articles hello à partir de flux hello dans un processus en arrière-plan.
* Maintenance de fichiers (par exemple, agrégation ou nettoyage de fichiers journaux).  Vous pouvez avoir des fichiers de journal en cours de création par plusieurs sites ou pour différentes périodes que vous souhaitez toocombine dans commande toorun les tâches d’analyse sur les. Ou vous souhaiterez peut-être tooschedule un tooclean hebdomadaire toorun de tâche des anciens fichiers journaux.
* Entrée dans des tables Azure. Vous avez stockés les fichiers et les objets BLOB et souhaitez tooparse les et stocker les données de hello dans les tables. fonction d’entrée Hello en l’écrivant un grand nombre de lignes (des millions dans certains cas) et hello WebJobs SDK rend possible tooimplement cette fonctionnalité facilement. Hello SDK fournit également une analyse en temps réel des indicateurs de progression comme nombre hello de lignes écrites dans la table de hello.
* Autres tâches longues que vous voulez toorun dans un thread d’arrière-plan, tel que [l’envoi d’e-mails](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Toutes les tâches que vous souhaitez toorun selon une planification, telle que l’exécution d’une opération de sauvegarde chaque nuit.

Dans la plupart de ces scénarios, vous voudrez tooscale un toorun d’application web sur plusieurs machines virtuelles, ce qui serait d’exécuter plusieurs tâches Web simultanément. Dans certains scénarios, cela peut entraîner hello même en cours de traitement des données plusieurs fois, mais cela n’est pas un problème lorsque vous utilisez la file d’attente intégrées de hello, blob et les déclencheurs de Service Bus de hello WebJobs SDK. Hello SDK garantit que vos fonctions seront traitées qu’une seule fois pour chaque message ou d’un objet blob.

Hello WebJobs SDK permet également de toohandle facilement les scénarios courants de gestion des erreurs. Vous pouvez configurer des alertes toosend notifications lorsqu’une fonction échoue, et vous pouvez définir des délais d’attente afin qu’une fonction est automatiquement annulée si elle ne se termine pas dans un délai spécifié.

## <a id="code"></a> Exemples de code
code Hello pour la gestion des tâches courantes qui fonctionnent avec le stockage Azure est simple. Dans votre Application de Console `Main` méthode que vous créez un `JobHost` objet qui coordonne hello appelle toomethods vous écrivez. Hello WebJobs SDK framework connaît lorsque toocall vos méthodes et le paramètre valeurs toouse selon hello WebJobs SDK attributs vous utilisez dans les. Hello SDK fournit *déclencheurs* qui spécifient les conditions qui provoquent hello fonction toobe est appelée, et *classeurs* qui spécifient comment tooget informations vers et depuis des paramètres de méthode.

Par exemple, hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attribut entraîne une toobe de la fonction appelée lorsqu’un message est reçu sur une file d’attente et si hello message est au format JSON pour un tableau d’octets ou un type personnalisé, le message de type hello est automatiquement désérialisé. Hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attribut déclenche un processus chaque fois qu’un nouvel objet blob est créé dans un compte de stockage Azure.

Voici un programme simple qui interroge une file d’attente et crée un objet blob pour chaque message de file d’attente reçu :

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

Hello `JobHost` objet est un conteneur pour un ensemble de fonctions d’arrière-plan. Hello `JobHost` objet moniteurs hello fonctionne, observe les événements qui déclenchent les et exécute les fonctions hello lorsque surviennent des événements de déclencheur. Vous appelez un `JobHost` méthode tooindicate si vous voulez hello conteneur processus toorun sur hello le thread actuel ou un thread d’arrière-plan. Dans l’exemple de hello, hello `RunAndBlock` méthode exécute les processus de hello en continu sur le thread en cours de hello.

Étant donné que hello `ProcessQueueMessage` méthode dans cet exemple a un `QueueTrigger` attribut, le déclencheur de hello pour cette fonction est réception hello d’un nouveau message de file d’attente. Hello `JobHost` objet surveille les nouveaux messages de file d’attente sur la file d’attente spécifiée hello (« webjobsqueue » dans cet exemple) et lorsqu’il en trouve, il appelle `ProcessQueueMessage`. 

Hello `QueueTrigger` attribut lie hello `inputText` toohello valeur du paramètre de message de file d’attente hello. Et hello `Blob` attribut lie un `TextWriter` blob de tooa objet nommé « blobname » dans un conteneur nommé « containername ».  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

fonction Hello utilise ensuite ces valeur hello toowrite des paramètres de l’objet blob toohello de message de file d’attente hello :

        writer.WriteLine(inputText);

fonctionnalités de déclencheur et le binder Hello Hello WebJobs SDK simplifient considérablement le code hello avoir toowrite. Hello code de bas niveau requis tooprocess files d’attente, objets BLOB, ou fichiers ou les tâches planifiée de tooinitiate, est réalisée pour vous par hello structure WebJobs SDK. Par exemple, infrastructure de hello crée les files d’attente qui n’existent pas encore, ouvre hello file d’attente, les messages de la file d’attente des lectures, supprime la file d’attente messages lorsque le traitement est terminé, crée des conteneurs d’objets blob qui n’existent pas encore, écrit tooblobs et ainsi de suite.

Hello exemple de code suivant montre une variété de déclencheurs dans une tâche Web : `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, et `ErrorTrigger`. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a>
Hello `TimerTrigger` attribut donne hello de capacité tootrigger fonctions toorun selon une planification. Vous pouvez planifier une tâche Web comme un entier à Azure ou la planification des fonctions individuelles d’un à l’aide de la tâche Web hello WebJobs SDK `TimerTrigger`. Voici un exemple de code.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

Pour plus d’exemples de code, consultez [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) dans le référentiel d’extensions azure-tâches Web-Kit de développement logiciel hello sur GitHub.com.

## <a name="extensibility"></a>Extensibilité
Vous n’êtes pas limité dans toobuilt fonctionnalité--hello WebJobs SDK vous permet de toowrite des déclencheurs personnalisés et des classeurs.  Par exemple, vous pouvez écrire des déclencheurs pour les événements du cache et les planifications périodiques. Un [référentiel open source](https://github.com/Azure/azure-webjobs-sdk-extensions) contient un [guide détaillé sur l’extensibilité de WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) et exemple code toohelp commencer, vous devez écrire vos propres déclencheurs et les classeurs.

## <a id="workerrole"></a>À l’aide de hello SDK WebJobs en dehors des tâches Web
Un programme qui utilise hello hello WebJobs SDK est une Application de Console standard et peut exécuter n’importe où--il ne dispose pas toorun comme une tâche Web. Vous pouvez tester les programme hello localement sur votre ordinateur de développement et vous pouvez l’exécuter dans un rôle de travail de Service Cloud ou un service Windows si vous préférez un de ces environnements de production. 

Toutefois, tableau de bord hello est uniquement disponible en tant qu’extension d’une application web de Service d’applications Azure. Si vous souhaitez toorun en dehors d’une tâche Web et toujours utilisez hello du tableau de bord, vous pouvez configurer un site web application toouse hello même compte de stockage que votre chaîne de connexion du tableau de bord WebJobs Kit de développement logiciel fait référence à, et le tableau de bord de cette application web WebJobs puis affichent des données sur la fonction exécution à partir de votre programme qui exécute un autre emplacement. Vous pouvez obtenir toohello du tableau de bord à l’aide de hello URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Pour plus d’informations, consultez [mise en route d’un tableau de bord pour un développement local avec hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), mais notez que le billet de blog hello affiche un ancien nom de chaîne de connexion. 

## <a id="nostorage"></a>Fonctionnalités du tableau de bord
Hello WebJobs SDK offre plusieurs avantages même si vous n’utilisez pas les déclencheurs de WebJobs SDK ou des classeurs :

* Vous pouvez appeler des fonctions de hello du tableau de bord.
* Vous pouvez relire des fonctions à partir de hello du tableau de bord.
* Vous pouvez afficher les journaux dans hello du tableau de bord, toohello lié la tâche Web particulier (journaux des applications, écrits à l’aide de Console.Out, Console.Error, Trace, etc.) ou de la liaison d’appel de fonction particulière toohello qui les a générés (journaux écrits à l’aide un `TextWriter` l’objet que hello que SDK passe toohello fonction en tant que paramètre). 

Pour plus d’informations, consultez [comment toomanually appeler une fonction](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) et [comment toowrite journaux](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Étapes suivantes
Pour plus d’informations sur hello WebJobs SDK, consultez [Azure WebJobs recommandé de ressources](http://go.microsoft.com/fwlink/?linkid=390226).

Pour plus d’informations sur hello dernières améliorations toohello WebJobs SDK, consultez hello [Notes de publication](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

