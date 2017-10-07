---
title: "ressources de documentation aaaAzure tâches Web"
description: "Recommandé de ressources d’apprentissage comment toouse tâches Web Azure et hello du Kit de développement logiciel Azure WebJobs."
services: app-service
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: ed005e56-4334-4641-a5e5-15435c2be36b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/25/2017
ms.author: glenga
ms.openlocfilehash: 6616a9d97c9637ec64cb8743dded6ba409a521ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-webjobs-documentation-resources"></a>Ressources de documentation relatives à Azure WebJobs
## <a name="overview"></a>Vue d'ensemble
Cette rubrique renvoie toodocumentation des ressources concernant la manière toouse tâches Web Azure et hello du Kit de développement logiciel Azure WebJobs. Les tâches Web Azure fournissent un script de toorun facilement ou programmes en tant qu’arrière-plan processus dans le contexte de hello d’un [application de Service de l’application web, application API, application mobile ou](../app-service/app-service-value-prop-what-is.md). Vous pouvez charger et exécuter un fichier exécutable comme cmd, bat, exe (.NET), ps1, sh, php, py, js et jar. Ces programmes s’exécutent en tant que tâches WebJobs selon une planification (cron) ou en continu.

Hello d’objectif de hello [WebJobs SDK](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk) est toosimplify hello code que vous écrivez pour les tâches courantes qu’une tâche Web peut effectuer, telles que le traitement d’image, traitement de la file d’attente, agrégation RSS, maintenance des fichiers et de l’envoi des messages électroniques. Hello WebJobs SDK inclut des fonctionnalités intégrées pour de nombreux autres scénarios courants pour travailler avec le stockage Azure et Service Bus et pour la planification des tâches et la gestion des erreurs. En outre, il a conçu toobe extensible et il existe un [référentiel open source pour les extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview). [Les fonctions Azure](../azure-functions/functions-overview.md) (actuellement en version préliminaire) est basé sur une version de hello WebJobs SDK qui fonctionne avec c# script, Node.js et autres langages. 

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

La création, le déploiement et la gestion des tâches web WebJobs sont parfaitement compatibles avec les outils intégrés dans Visual Studio. Vous pouvez créer les tâches web à partir de modèles, les publier et les gérer (les exécuter, les arrêter, les analyser et les déboguer). 

tableau de bord WebJobs Hello Bonjour portail Azure fournit de puissantes fonctions de gestion qui vous donnent un contrôle total sur l’exécution de hello de tâches Web, y compris hello capacité tooinvoke des fonctions individuelles dans les tâches Web. tableau de bord Hello affiche également les exécutions de la fonction et la sortie de journalisation. 

## <a name="getstarted"></a>Mise en route avec les tâches Web, hello WebJobs SDK
* [Introduction tooAzure tâches Web](http://www.hanselman.com/blog/IntroducingWindowsAzureWebJobs.aspx)
* [Azure WebJobs est extraordinaire, utilisez-le dès maintenant !](http://www.troyhunt.com/2015/01/azure-webjobs-are-awesome-and-you.html) (Billet de blog de Troy Hunt).
* [Fonctionnalités Azure WebJobs](https://azure.microsoft.com/blog/2014/10/22/webjobs-goes-into-full-production/)
* [Nouveautés hello WebJobs SDK](websites-dotnet-webjobs-sdk.md)
* [Conseils de travaux d’arrière-plan par Microsoft Patterns and Practices](https://docs.microsoft.com/azure/architecture/best-practices/background-jobs)
* [Annonce hello 1.1.0 RTM de Microsoft Azure SDK Webjob](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/)
* [Prise en main hello Azure WebJobs SDK](websites-dotnet-webjobs-sdk-get-started.md)
* [Comment toouse Azure file d’attente de stockage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [Comment toouse Azure stockage d’objets blob par hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [Comment toouse Azure table storage avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [Comment toouse Azure Service Bus avec hello WebJobs SDK](websites-dotnet-webjobs-sdk-service-bus.md)
* [Aide-mémoire du Kit de développement logiciel (SDK) Azure WebJobs (téléchargement au format PDF)](https://go.microsoft.com/fwlink/p/?linkid=845558)
* [Documentation sur les paramètres de WebJobs dans GitHub](https://github.com/projectkudu/kudu/wiki/Web-jobs)
* Vidéos
  * [Les tâches Web, hello WebJobs SDK](http://channel9.msdn.com/Shows/Cloud+Cover/Episode-153-WebJobs-with-Pranav-Rastogi?utm_source=dlvr.it&utm_medium=twitter)
  * [Série de vidéos Azure WebJobs sur Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)
  * [Présentation des outils de WebJobs pour Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Outils de WebJobs et débogage distant](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster)
  * [Mise à jour d'Azure WebJobs avec Pranav Rastogi - Extensibilité dans la version 1.1](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-183-Azure-WebJobs-Update-with-Pranav-Rastogi)

Voir aussi hello les sections suivantes [les tâches de déploiement Web](#deploy) et [test et débogage de tâches Web](#debug).

## <a name="deploy"></a>Déploiement de WebJobs
* [Comment tooDeploy les tâches Web Azure à l’aide de Visual Studio](websites-dotnet-deploy-webjobs.md)
* [Comment la toodeploy à l’aide de tâches Web hello portail Azure](web-sites-create-web-jobs.md)
* [Activation de la ligne de commande ou livraison en continu d’Azure WebJobs](https://azure.microsoft.com/blog/2014/08/18/enabling-command-line-or-continuous-delivery-of-azure-webjobs/)
* [Déploiement d’un tooAzure d’application console .NET à l’aide des tâches Web de GIT](http://blog.amitapple.com/post/73574681678/git-deploy-console-app/)
* [Déploiement d’un tooAzure F # WebJob](http://blogs.msdn.com/b/dave_crooks_dev_blog/archive/2015/02/18/deploying-f-web-job-to-azure.aspx)
* [Déploiement de services personnalisés en tant que tâches web Azure](http://withouttheloop.com/articles/2015-06-23-deploying-custom-services-as-azure-webjobs/)
* Vidéos
  * [Présentation des outils de WebJobs pour Visual Studio](http://channel9.msdn.com/Shows/Web+Camps+TV/Introducing-WebJobs-Tooling-for-Visual-Studio-with-Brady-Gaster) 
  * [Outils de WebJobs et débogage distant](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="schedule"></a>Planification de WebJobs
* [Bonjour Azure WebJob boîte de dialogue Ajouter](websites-dotnet-deploy-webjobs.md#configure)
* [Créer une tâche Web planifiée dans hello portail Azure](web-sites-create-web-jobs.md#CreateScheduled)
* [Raccorder un tooa de tâche du planificateur tâche Web](http://blog.davidebbo.com/2015/05/scheduled-webjob.html)
* [Planification de tâches web Azure avec des expressions cron](http://blog.amitapple.com/post/2015/06/scheduling-azure-webjobs/)
* [Planification différentes fonctions de la tâche Web à l’aide de hello TimerTrigger du Kit de développement logiciel tâches Web](websites-dotnet-webjobs-sdk.md#schedule)

## <a name="debug"></a>Test et débogage de WebJobs
* [Nouvelles fonctionnalités de développement et de débogage pour Azure WebJobs dans Visual Studio](http://blogs.msdn.com/b/webdev/archive/2014/11/12/new-developer-and-debugging-features-for-azure-webjobs-in-visual-studio.aspx)
* [Hello d’affichage tableau de bord WebJobs](websites-dotnet-webjobs-sdk-get-started.md#view-the-webjobs-sdk-dashboard)
* [Comment toowrite se connecte à l’aide de hello WebJobs SDK et de les afficher dans le tableau de bord de hello](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs)
* [Débogage à distance de WebJobs](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebugwj)
* [Qui a écrit cet objet blob ?](http://blogs.msdn.com/b/jmstall/archive/2014/02/19/who-wrote-that-blob.aspx) 
* [Code interactif Bonjour Cloud d’hébergement](http://blogs.msdn.com/b/jmstall/archive/2014/04/26/hosting-interactive-code-in-the-cloud.aspx)
* [Ajout de Trace tooAzure tâches Web](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx)
* [Analyser, diagnostiquer et dépanner Microsoft Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md)
* Vidéos
  * [Outils de WebJobs et débogage distant](http://channel9.msdn.com/Shows/Web+Camps+TV/WebJobs-GA-Series-Episode-1-WebJobs-Tooling-with-Brady-Gaster) 

## <a name="scale"></a>Mise à l’échelle de WebJobs
* [Mise à l’échelle de votre application web avec Sites Web Azure](http://msdn.microsoft.com/magazine/dn786914.aspx)
* [Azure App Service : création de l’architecture d’applications web prêtes à être utilisées par les entreprises à grande échelle](https://channel9.msdn.com/Events/Build/2014/3-626). Couvre mise à l’échelle d’applications web avec les tâches Web, y compris hello WebJobs SDK.
* Vidéos
  * [Montée en puissance des tâches web](http://channel9.msdn.com/Shows/Azure-Friday/Azure-WebJobs-105-Scaling-out-Web-Jobs)

## <a name="additional"></a>Autres ressources liées à WebJobs
* [Billet de blog GA sur Azure WebJobs de Magnus Mårtensson](http://magnusmartensson.com/azure-webjobs-ga)
* [Exécution de tâches web Powershell sur Azure App Service](http://blogs.msdn.com/b/nicktrog/archive/2014/01/22/running-powershell-web-jobs-on-azure-websites.aspx)
* [Réception d’une notification à la fin de la tâche web déclenchée par Azure](http://blog.amitapple.com/post/2014/03/webjobs-notification/)
* [Stratégie de rétention de sauvegarde d’une application web avec WebJobs](https://azure.microsoft.com/blog/2014/04/28/simple-web-site-backup-retention-policy-with-webjobs/)
* [Lenteur d’Azure Web Apps et de Cloud Services à la première requête](http://wp.sjkp.dk/windows-azure-websites-and-cloud-services-slow-on-first-request/). Montre comment toouse WebJobs toosimulate hello fonctionnalité AlwaysOn qui est disponible uniquement pour la tarification Standard hello.
* [Arrêt progressif de WebJobs](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.U72Il_5OWUl). Pour plus d’informations sur l’arrêt progressif du Kit de développement logiciel (SDK) WebJobs, consultez la rubrique [Arrêt progressif](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).
* [Sauvegardes automatiques avec Azure WebJobs et AzCopy](http://markjbrown.com/azure-webjobs-azcopy/)
* Vidéos
  * [Vidéos sur WebJobs de Magnus Mårtensson](https://www.youtube.com/playlist?list=PLqp1ZOYYUSd81yEzMYLTw8cz91wx_LU9r)
  * [Série de vidéos Azure WebJobs sur Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="additionalsdk"></a>Ressources supplémentaires du Kit de développement logiciel (SDK) WebJobs
* [Notes de publication du Kit de développement logiciel (SDK) WebJobs](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes)
* [Code source du Kit de développement logiciel (SDK) WebJobs](https://github.com/Azure/azure-webjobs-sdk)
* [Extensions de WebJobs SDK de code source](https://github.com/Azure/azure-webjobs-sdk-extensions), avec [modèle d’extensibilité toohello guide détaillé](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).  
* [Code source du script du Kit de développement logiciel (SKDK) WebJobs](https://github.com/Azure/azure-webjobs-sdk-script/) (utilisé pour [Azure Functions](../azure-functions/functions-overview.md))
* [La tâche Web tooupload FREB fichiers tooAzure stockage à l’aide de hello WebJobs SDK](http://thenextdoorgeek.com/post/WAWS-WebJob-to-upload-FREB-files-to-Azure-Storage-using-the-WebJobs-SDK)
* [Hébergement Azure webjobs en dehors d’Azure, hébergé par hello journalisation avantages d’Azure la tâche Web](http://bypassion.dk/?p=510)
* [Création d’un outil d’importation de données avec Azure WebJobs](http://www.freshconsulting.com/building-data-import-tool-azure-webjobs/)
* [Vue d’ensemble d’Azure Functions](../azure-functions/functions-overview.md)
* Vidéos
  * [Série de vidéos Azure WebJobs sur Channel 9](http://channel9.msdn.com/Tags/azurefridaywebjobs)

## <a name="samples"></a>Exemple d’application WebJobs
* [Exemples d’applications fournies par l’équipe des tâches Web hello sur GitHub](https://github.com/azure/azure-webjobs-sdk-samples)
* [Application Web Azure simple avec WebJobs Backend à l’aide de hello WebJobs SDK](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb)
* [SiteMonitR](http://code.msdn.microsoft.com/SiteMonitR-dd4fcf77). Illustre l'utilisation des tâches web WebJobs planifiées et liées aux événements. Consultez billet de blog hello [reconstruction hello SiteMonitR à l’aide du Kit de développement logiciel Azure WebJobs](http://www.bradygaster.com/post/rebuilding-the-sitemonitr-using-windows-azure-webjobs).

## <a name="blogs"></a>Blogs
* [Blog Azure](/blog)
* [Blog d’Amit Apple](http://blog.amitapple.com/). Se concentre sur les tâches Web (pas hello SDK).
* [Blog de Magnus Mårtensson](http://magnusmartensson.com/)

## <a name="gethelp"></a>Obtention d’aide sur WebJobs
* [StackOverflow pour WebJobs](http://stackoverflow.com/questions/tagged/azure-webjobs)
* [StackOverflow pour hello WebJobs SDK](http://stackoverflow.com/questions/tagged/azure-webjobssdk)
* [StackOverflow pour Azure Functions](http://stackoverflow.com/questions/tagged/azure-functions)
* [Forum Azure et ASP.NET](http://forums.asp.net/1247.aspx)
* [Forum sur Azure App Service Web Apps (en anglais)](http://social.msdn.microsoft.com/Forums/azure/home?forum=windowsazurewebsitespreview)
* [Site UserVoice d’Azure Web Apps](https://feedback.azure.com/forums/169385-websites/)
* [Twitter](http://twitter.com/). Utilisez hello #sqlhelp #AzureWebJobs.
* [Signaler un problème ou un bogue WebJobs](https://github.com/projectkudu/kudu/wiki/Reporting-WebJobs-issues)

