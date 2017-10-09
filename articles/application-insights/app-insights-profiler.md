---
title: les applications web en direct aaaProfiling sur Azure avec Application Insights | Documents Microsoft
description: "Identifier le chemin réactif hello dans votre code de serveur web avec un faible encombrement profileur."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Profilage des applications web dynamiques Azure avec Application Insights

*Cette fonctionnalité d’Application Insights est disponible pour les App Services, et disponible en aperçu pour Compute.*

Découvrez combien de temps passé dans chaque méthode dans votre application web dynamique à l’aide de hello profilage de l’outil de [Azure Application Insights](app-insights-overview.md). Il vous montre les profils détaillés d’en direct les demandes qui ont été pris en charge par votre application et met en évidence hello 'chemin réactif » qui est à l’aide de hello essentiel du temps. Il sélectionne automatiquement des exemples associés à des temps de réponse différents. Générateur de profils Hello utilise la surcharge de toominimize différentes techniques.

Hello profileur actuellement fonctionne pour ASP.NET web applications qui s’exécutent sur des Services d’application Azure au moins hello Basic niveau tarifaire. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Activer le Générateur de profils hello

[Installez Application Insights](app-insights-asp-net.md) dans votre code. S’il est déjà installé, assurez-vous que vous avez la version la plus récente hello. (toodo, avec le bouton droit de votre projet dans l’Explorateur de solutions, choisissez Gérer les packages NuGet. Sélectionnez Mises à jour et mettez à jour tous les packages.) Redéployez votre application.

*Vous utilisez ASP.NET Core ? [Cliquez ici](#aspnetcore).*

Dans [https://portal.azure.com](https://portal.azure.com), ouvrez la ressource d’Application Insights hello pour votre application web. Ouvrez **Performances** et cliquez sur **Activer Application Insights Profiler...**.

![Cliquez sur la bannière de profileur hello activer][enable-profiler-banner]

Ou bien, vous pouvez toujours cliquer sur **configurer** tooview état, activer ou désactiver hello du Générateur de profils.

![Dans le panneau de performances hello, cliquez sur Configurer][performance-blade]

Les applications web configurées avec Application Insights sont listées dans le panneau Configurer. Suivez les instructions tooinstall hello Profiler l’agent si nécessaire. Si aucune application web n’est encore configurée avec Application Insights, cliquez sur *Ajouter des applications liées*.

Hello d’utilisation *activer le Générateur de profils* ou *désactiver le Générateur de profils* boutons dans hello configurer panneau toocontrol hello Profiler sur toutes vos applications web lié.



![Panneau Configurer][linked app services]

profiler hello toostop ou redémarrage d’une instance du Service d’applications individuelles, vous la trouverez **Bonjour ressource du Service d’application**, dans **tâches Web**. toodelete il, consultez sous **Extensions**.

![Désactiver le profileur pour des tâches web][disable-profiler-webjob]

Nous vous recommandons d’avoir hello Profiler activé sur tous les toodiscover de vos applications web des performances des problèmes dès que possible.

Si vous utilisez l’application web tooyour WebDeploy toodeploy modifications, vérifiez que vous excluez hello **App_Data** dossier soient supprimés lors du déploiement. Dans le cas contraire, hello les fichiers de l’extension du Générateur de profils sont supprimés lorsque vous déployez ensuite hello web application tooAzure.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>En utilisant le profileur avec les machines virtuelles Azure et les ressources de calcul (version préliminaire)

Lorsque vous [activez Application Insights pour les services d’application Azure en cours d’exécution](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), le profileur est automatiquement disponible. (Si vous déjà activé l’Application Insights pour la ressource de hello, vous devrez peut-être tooupdate toohello TVA version via hello **configurer** Assistant.)

Il existe un [version d’évaluation de hello du Générateur de profils pour les ressources de calcul Azure](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>limites

rétention des données Hello par défaut est 5 jours. 10 Go maximum reçus par jour.

Il n’existe aucun frais pour le service de profil hello. Votre application web doit être hébergée dans au moins hello niveau de base des Services d’application.

## <a name="viewing-profiler-data"></a>Affichage des données du profileur

Ouvrez le panneau de performances hello et faites défiler la liste des opérations toohello.




![Colonne Exemples du panneau Performances d’Application Insights][performance-blade-examples]

les colonnes dans la table de hello Hello sont :

* **Nombre de** -hello nombre de ces requêtes dans la plage de temps hello du Panneau de hello.
* **Valeur médiane** -hello classique temps votre application toorespond tooa demande. La moitié de toutes les réponses étaient plus rapides que cela.
* **95e centile** : 95 % des réponses étaient plus rapides que cela. Si ce chiffre est très différent de la valeur médiane de hello, il peut y avoir un problème intermittent avec votre application. (Cette différence peut aussi s’expliquer par une fonctionnalité de conception, telle que la mise en cache.)
* **Exemples** -une icône indique ce profileur hello a capturé les traces de pile pour cette opération.

Cliquez sur Explorateur de la trace hello exemples icône tooopen hello. Hello l’Explorateur affiche plusieurs exemples qui hello du profileur a capturé, classés par temps de réponse.

Sélectionnez un tooshow exemple une répartition au niveau du code de temps passé à la demande de hello en cours d’exécution.

![Explorateur de trace d’Application Insights][trace-explorer]

**Afficher le chemin réactif** s’ouvre hello majeurs nœud terminal ou fermez au moins un problème. Dans la plupart des cas, ce nœud sera tooa adjacents goulot d’étranglement.



* **Étiquette**: nom hello de fonction hello ou un événement. arborescence de Hello affiche une combinaison de code et les événements qui s’est produite (par exemple, les événements SQL et http). les événements supérieur Hello représente hello globale durée de la demande.
* **Écoulé**: intervalle de temps hello entre hello opération début de hello et à la fin de hello.
* **Lorsque**: montre lorsque événement de la fonction hello était en cours d’exécution dans les fonctions de tooother de relation.

## <a name="how-tooread-performance-data"></a>Comment les données de performances tooread

Générateur de profils Microsoft service utilise une combinaison d’échantillonnage des performances de hello tooanalyze (méthode) et l’instrumentation de votre application.
Lors de la collection détaillée est en cours d’exécution, profileur service hello pointeur d’instruction de chaque UC de l’ordinateur hello dans toutes les millisecondes.
Chaque exemple capture la pile des appels complète hello du thread hello actuellement l’exécution, en donnant des informations utiles et détaillées sur les éléments que thread en cours d’exécution sur les deux serveurs haute et basse des niveaux d’abstraction. Profileur de service collecte également les autres événements tels que les événements de changement de contexte, des événements de la bibliothèque parallèle de tâches et de corrélation de pool de threads événements tootrack activité et causalité.

pile des appels Hello indiquée dans l’affichage de la chronologie hello est résultat hello Hello au-dessus d’échantillonnage et l’instrumentation. Étant donné que chaque exemple capture la pile des appels complète hello du thread de hello, elle inclut du code à partir de hello .NET framework, ainsi que les autres infrastructures que vous faites référence.

### <a id="jitnewobj"></a>Allocation d’objets (`clr!JIT\_New or clr!JIT\_Newarr1`)
Les fonctions d’assistance `clr!JIT\_New and clr!JIT\_Newarr1` intégrées au framework .NET allouent la mémoire à partir du segment de mémoire géré. `clr!JIT\_New` est appelé lorsqu’un objet est alloué. `clr!JIT\_Newarr1` est appelé lorsqu’un tableau d’objets est alloué. Ces deux fonctions sont généralement très rapides et s’exécutent en relativement peu de temps. Si vous voyez `clr!JIT\_New` ou `clr!JIT\_Newarr1` prendre un certain temps dans votre scénario, il s’agit d’une indication que le code de hello peut-être être allocation d’objets et consomme beaucoup de mémoire.

### <a id="theprestub"></a>Code de chargement (`clr!ThePreStub`)
`clr!ThePreStub`est une fonction d’assistance à l’intérieur de .NET framework qui prépare tooexecute de code hello pour hello la première fois. Elle implique en général au moins une compilation JIT (juste à temps). Pour chaque méthode c#, `clr!ThePreStub` doit être appelé au maximum une fois pendant la durée de vie hello d’un processus.

Si vous voyez `clr!ThePreStub` prend beaucoup de temps pour une demande, il indique cette demande est hello premier celui qui exécute cette méthode et l’heure de hello pour tooload de runtime .NET framework que la méthode est importante. Vous pouvez envisager un processus de mise en route qui s’exécute de la partie du code de hello avant que vos utilisateurs y accéder, ou envisagez d’exécuter NGen sur vos assemblys.

### <a id="lockcontention"></a>Contention de verrouillage (`clr!JITutil\_MonContention` ou `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`ou `clr!JITutil\_MonEnterWorker` indiquer le thread en cours de hello est en attente pour un toobe verrou libéré. Cela se produit généralement lors de l’exécution d’une instruction lock C#, lors de l’appel de méthode Monitor.Enter, ou encore lors de l’appel d’une méthode avec l’attribut MethodImplOptions.Synchronized. Contention de verrouillage se produit généralement lorsque le thread A acquiert un verrou, et le thread B tente d’hello tooacquire même verrouiller avant que le thread A le libère.

### <a id="ngencold"></a>Code de chargement (`[COLD]`)
Si le nom de la méthode hello contient `[COLD]`, tel que `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, cela signifie que hello .NET framework runtime exécute le code qui n’est pas optimisé par <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">l’optimisation guidée par profil</a> pour hello première fois. Pour chaque méthode, il doit s’afficher au maximum une fois pendant la durée de vie hello de hello.

Si le chargement de code prend beaucoup de temps pour une demande, il indique que cette demande est hello premier tooexecute un hello non optimisée partie de la méthode hello. Vous pouvez envisager un processus qui exécute cette partie du code de hello avant que vos utilisateurs y accéder de préchauffage.

### <a id="httpclientsend"></a>Envoyer une requête HTTP
Les méthodes telles que `HttpClient.Send` indiquent les code hello attend un toocomplete de demande HTTP.

### <a id="sqlcommand"></a>Opération de base de données
Méthode telle que SqlCommand.Execute indique le code de hello est en attente d’un toocomplete d’opération de base de données.

### <a id="await"></a>En attente (`AWAIT\_TIME`)
`AWAIT\_TIME`Indique le code de hello est en attente d’une autre tâche toocomplete. Cela se produit généralement avec l’instruction C# « await ». Lorsque le code de hello ne c# 'await', se déroule hello thread et retourne le contrôle toohello-pool de threads et il n’existe aucun thread est bloqué en attente de toofinish de 'await' hello. Toutefois, logiquement hello de thread qu’avez-vous hello await est « bloqué » en attente de hello opération toocomplete. La `AWAIT\_TIME` indique le temps de hello bloqué en attente de toocomplete de tâche hello.

### <a id="block"></a>Temps de blocage
`BLOCKED_TIME`Indique le code de hello est en attente d’un autre toobe de ressources disponible, comme en attente pour un objet de synchronisation, en attente pour un toobe thread disponible, ou en attente pour un toofinish de demande.

### <a id="cpu"></a>Temps processeur
Hello du processeur est occupé à exécuter des instructions de hello.

### <a id="disk"></a>Temps du disque
application Hello effectue les opérations de disque.

### <a id="network"></a>Temps réseau
application Hello effectue les opérations de réseau.

### <a id="when"></a>Colonne « When » (Quand)
Il s’agit d’une visualisation de la manière dont les échantillons INCLUSIFS hello collectées pour un nœud peuvent varier au fil du temps. Hello total plage de demande de hello est divisée de 32 plages de temps et les échantillons inclusifs les hello pour ce nœud sont accumulent dans les compartiments de 32. Chaque compartiment est ensuite représenté par une barre dont la hauteur reflète une valeur à l’échelle. Pour les nœuds marquées `CPU_TIME` ou `BLOCKED_TIME`, ou s’il existe une relation évidente d’utilisation d’une ressource (UC, disque, de thread), hello barre représente consommant une de ces ressources pour la période hello de compartiment. Pour ces mesures, vous pouvez dépasser le seuil de 100 % en consommant plusieurs ressources. Par exemple, si vous utilisez en moyenne deux processeurs sur un intervalle donné, vous obtenez 200 %.


## <a id="troubleshooting"></a>Résolution des problèmes

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Comment savoir si le profileur d’Application Insights est en cours d’exécution ?

Générateur de profils Hello s’exécute comme une tâche web continue dans l’application Web. Vous pouvez ouvrir des ressources d’application Web hello dans https://portal.azure.com et vérifier l’état « ApplicationInsightsProfiler » dans le panneau des tâches Web hello. Si elle n’est pas en cours d’exécution, ouvrez **journaux** toofind plus d’informations.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>Je ne trouve pas les exemples de pile même si le Générateur de profils hello est en cours d’exécution ?

Vous pouvez vérifier plusieurs points.

1. Assurez-vous que votre plan Web App Service est au moins au niveau tarifaire De base.
2. Assurez-vous que le SDK Application Insights 2.2 Bêta ou version supérieure est activé sur votre application web.
3. Assurez-vous que votre application Web a le paramètre hello APPINSIGHTS_INSTRUMENTATIONKEY hello utilisé de la même clé d’instrumentation par Application Insights SDK.
4. Assurez-vous que votre application web s’exécute sur .Net Framework 4.6.
5. S’il est une application ASP.NET Core, également vérifier [hello les dépendances requises](#aspnetcore).

Après le démarrage du Générateur de profils hello, il existe une période de préchauffage court lorsque le Générateur de profils hello activement pour collecter les traces de performances plusieurs. Après cela, Générateur de profils hello collecte des traces de performances pendant deux minutes dans toutes les heures.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>J’utilisais avant l’agent Azure Service Profiler. Quelles tooit s’est produit ?  

Lorsque vous activez le profileur d’Application Insights, l’agent Azure Service Profiler est désactivé.

### <a id="double-counting"></a>Double comptage dans des threads parallèles

Dans certains hello cas métrique de temps total dans la visionneuse de pile hello est supérieure à la durée réelle de hello de demande de hello.

Cela peut se produire lorsque deux threads au moins sont associés à une requête et qu’ils s’exécutent en parallèle. temps total de threads de Hello est alors plus de temps écoulé de hello. Dans de nombreux cas, un thread peut être en attente sur hello autres toocomplete. Hello visionneuse tentatives toodetect cela et omettre les attente inintéressants hello, mais pêche par excès côté hello de l’affichage trop plutôt que l’omission de ce qui peut être informations critiques.  

Lorsque vous voyez des threads parallèles dans vos traces, vous devez toodetermine threads en attente afin de déterminer le chemin d’accès critique de hello pour demande de hello. Dans la plupart des cas, le thread hello rapidement passe en état d’attente en attente simplement sur hello autres threads. Se concentrer sur d’autres hello et ignorer les temps hello dans les threads en attente hello.

### <a id="issue-loading-trace-in-viewer"></a>Aucune donnée de profilage

1. Si les données de salutation que vous essayez tooview est antérieure à deux semaines, essayez de limiter votre filtre de temps, puis réessayez.

2. Vérifiez que l’accès toohttps://gateway.azureserviceprofiler.net n’ont pas bloqué par un pare-feu ou proxy.

3. Vérifiez que hello Application Insights, vous utilisez dans votre application clé d’instrumentation est même hello en tant que ressource Application Insights vous avez activé le profilage à l’aide de hello. clé de Hello est généralement dans ApplicationInsights.config, mais il peut également être trouvé dans le fichier web.config ou app.config.

### <a name="error-report-in-hello-profiling-viewer"></a>Rapport d’erreurs de hello visionneuse de profilage

Un ticket de support à partir du portail de hello du fichier. Veuillez inclure hello les ID de corrélation du message d’erreur hello.

## <a name="manual-installation"></a>Installation manuelle

Lorsque vous configurez le Générateur de profils hello, hello suivantes sont mises à jour les paramètres de l’application toohello Web. Vous pouvez les effectuer manuellement par vous-même si votre environnement le requiert, par exemple, si votre application s’exécute dans l’environnement Azure App Service (ASE) :

1. Dans le panneau de contrôle web application hello, ouvrez les paramètres.
2. Définissez « .net Framework version « toov4.6.
3. Définissez tooOn « Always On ».
4. Ajouter le paramètre d’application «__APPINSIGHTS_INSTRUMENTATIONKEY__» et le jeu hello valeur toohello même clé d’instrumentation utilisé par hello SDK.
5. Ouvrez Outils avancés.
6. Cliquez sur « Go » tooopen hello Kudu site Web.
7. Dans le site Web de Kudu hello, sélectionnez « Extensions de Site ».
8. Installez « __Application Insights__ »à partir de la galerie.
9. Redémarrage de l’application web de hello.

## <a id="aspnetcore"></a>Prise en charge d’ASP.NET Core

Application ASP.NET Core doit tooinstall 2.1.0-beta6 de package Nuget de Microsoft.ApplicationInsights.AspNetCore ou supérieur toowork avec hello du Générateur de profils. Nous n’est plus en charge les versions inférieures hello après 6/27/2017.

## <a name="next-steps"></a>Étapes suivantes

* [Utilisation d’Application Insights dans Visual Studio](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
