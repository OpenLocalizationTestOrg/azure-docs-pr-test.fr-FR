---
title: "performances de l’application web aaaSlow dans le Service d’applications | Documents Microsoft"
description: "Cet article vous aide à résoudre les problèmes de baisse de performances d’une application web dans Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: performances d'application web, application lente
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>Résoudre les problèmes de baisse de performances d’une application web dans Azure App Service
Cet article vous aide à résoudre les problèmes de baisse de performances d’une application web dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello MSDN Azure et hello forums de débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de Support technique Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Get Support**.

## <a name="symptom"></a>Symptôme
Lorsque vous accédez à l’application web hello, hello pages charge lentement et parfois délai d’attente.

## <a name="cause"></a>Cause :
Ce problème est souvent dû à des problèmes au niveau de l’application, tels que :

* requêtes réseau chronophages ;
* interrogations inefficaces du code ou de la base de données de l’application ;
* un taux d’utilisation élevé de la mémoire/UC par l’application ;
* panne en raison de l’exception de tooan d’application

## <a name="troubleshooting-steps"></a>Étapes de dépannage
Le dépannage peut être divisé en trois tâches distinctes, dans un ordre séquentiel :

1. [Observer et contrôler le comportement de l’application](#observe)
2. [Collecter les données](#collect)
3. [Limiter le problème de hello](#mitigate)

[App Service Web Apps](/services/app-service/web/) vous offre différentes options à chaque étape.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Observer et contrôler le comportement de l'application
#### <a name="track-service-health"></a>Suivi de l’état du service
Microsoft Azure publie chaque interruption du service et chaque dégradation des performances. Vous pouvez suivre la santé hello du service de hello sur hello [portail Azure](https://portal.azure.com/). Pour plus d’informations, consultez la rubrique [Suivi de l’état du service](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Contrôle de votre application web
Cette option permet de vous toofind out si votre application rencontre des problèmes. Dans le panneau de votre application web, cliquez sur hello **demandes et les erreurs** vignette. Hello **métrique** panneau vous montre toutes les métriques hello que vous pouvez ajouter.

Parmi les métriques hello que vous pouvez vouloir toomonitor pour votre application web

* Plage de travail moyenne de la mémoire
* Temps de réponse moyen
* Temps processeur
* Plage de travail de la mémoire
* Requêtes

![surveiller les performances d’une application web](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

Pour plus d'informations, consultez les pages suivantes :

* [Surveiller les applications web dans Microsoft Azure App Service](web-sites-monitor.md)
* [Réception de notifications d'alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>Surveillance de l'état d'un point de terminaison Web
Si vous exécutez votre application web Bonjour **Standard** niveau tarifaire, applications Web vous permet d’analyser deux points de terminaison de trois emplacements géographiques.

Elle paramètre des tests Web à partir de différents emplacements où sont évalués les temps de réponse et de disponibilité des URL. test de Hello effectue une opération HTTP GET sur le temps de réponse hello web URL toodetermine hello et temps d’activité à partir de chaque emplacement. Chaque emplacement configuré exécute un test toutes les cinq minutes.

La disponibilité est contrôlée à l'aide des codes réponse HTTP et le temps de réponse est mesuré en millisecondes. Un test de surveillance échoue si hello code de réponse HTTP est supérieur ou égal too400 ou si les réponse hello prend plus de 30 secondes. Un point de terminaison est considéré comme étant disponible si ses tests de surveillance aboutissent tous hello indiqué des emplacements.

tooset il, consultez [surveiller les applications dans Azure App Service](web-sites-monitor.md).

Consultez également [Assurer la gestion des sites Web Azure et la surveillance des points de terminaison, avec Stefan Schackow](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) pour obtenir une vidéo décrivant la surveillance d’un point de terminaison.

#### <a name="application-performance-monitoring-using-extensions"></a>Analyse des performances des applications à l’aide d’Extensions
Vous pouvez également surveiller les performances de votre application grâce aux *extensions de site*.

Chaque application Service web d’application fournit un point de terminaison de gestion extensible qui vous permet de toouse un ensemble puissant d’outils déployés en tant qu’extensions de site. Les extensions incluent : 

- Des éditeurs de code source, tels que [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx). 
- Outils de gestion des ressources connectées comme une base de données MySQL connecté tooa l’application web.

[Azure Application Insights](/services/application-insights/) et [New Relic](/marketplace/partners/newrelic/newrelic/) sont deux des extensions de site disponibles d’analyse des performances hello. toouse New Relic, vous installez un agent lors de l’exécution. toouse Azure Application Insights, vous régénérez votre code avec un kit de développement, et vous pouvez également installer une extension qui fournit l’accès aux données de tooadditional. Hello SDK vous permet d’écrire des performances de votre application et l’utilisation de code toomonitor hello plus en détail.

toouse Application Insights, consultez [analyser les performances dans les applications web](../application-insights/app-insights-web-monitor-performance.md).

toouse New Relic, consultez [nouvelle gestion des performances Application Relic sur Azure](../store-new-relic-cloud-services-dotnet-application-performance-management.md).

<a name="collect" />

### <a name="2-collect-data"></a>2. Collecter les données
environnement d’applications Web Hello fournit des fonctionnalités de diagnostic enregistrées les informations de serveur web de hello et application web de hello. informations de Hello sont divisées en diagnostic du serveur web et application diagnostics.

#### <a name="enable-web-server-diagnostics"></a>Activer les diagnostics de serveur web
Vous pouvez activer ou désactiver hello suivant les types de journaux :

* **Messages d’erreur détaillés** : informations d’erreur détaillées pour les codes d’état HTTP qui indiquent un échec (code d’état 400 ou supérieur). Il peut contenir des informations qui peuvent aider à déterminer pourquoi les serveur hello a renvoyé un code d’erreur hello.
* **Échec de l’outil suivi des demandes** -des informations détaillées sur les demandes ayant échoué, y compris une trace de hello IIS composants utilisés tooprocess hello demande et de durée hello dans chaque composant. Cela peut être utile si vous essayez de performances de l’application web tooimprove ou isolez ce qui provoque une erreur HTTP spécifique.
* **Journalisation du serveur Web** -informations sur les transactions HTTP en utilisant le format de fichier journal étendu hello W3C. Cela est utile lors de la détermination des métriques d’application web global, telles que nombre hello de demandes traitées ou le nombre de requêtes qui proviennent d’une adresse IP spécifique.

#### <a name="enable-application-diagnostics"></a>Activer les diagnostics d’application
Il existe plusieurs options toocollect application performance des données à partir d’applications Web, de profiler votre application dynamique à partir de Visual Studio ou de modifier votre toolog de code d’application plus d’informations et suivis. Vous pouvez choisir les options de hello sur le niveau d’accès toohello application et que vous observé à partir des outils d’analyse de hello.

##### <a name="use-application-insights-profiler"></a>Utiliser Application Insights Profiler
Vous pouvez activer toostart d’Application Insights Profiler hello capturer une trace de performances détaillés. Vous pouvez accéder à des traces capturées des toofive jours lorsque vous avez besoin des problèmes de tooinvestigate s’est produites dans hello passée. Vous pouvez choisir cette option tant que vous disposez de ressource Application Insights de l’application web accès toohello sur le portail Azure.

Application Insights Profiler fournit des statistiques sur les temps de réponse pour chaque appel web et les traces qui indique la ligne de code qui a provoqué hello réponses lentes. Parfois hello application de Service de l’application est lente, car du code n’est pas écrite dans un performant moyen. Il peut s’agir par exemple d’un code séquentiel exécuté en parallèle et de conflits indésirables de verrouillage de base de données. Suppression de ces goulots d’étranglement dans le code hello augmente les performances de l’application hello, mais ils sont toodetect dur sans configurer les journaux et traces élaborées. les traces de Hello collectées par le profileur d’Application Insights permet d’identifier les lignes de hello de code qui ralentit application hello et relever ce défi pour les applications de Service d’applications.

 Pour plus d’informations, consultez [Profilage des applications web dynamiques Azure avec Application Insights](../application-insights/app-insights-profiler.md).

##### <a name="use-remote-profiling"></a>Utiliser le profilage distant
Dans Azure Service App, Web Apps, API Apps et WebJobs peuvent être profilés à distance. Choisissez cette option si vous avez accès toohello-ressource d’application web et vous savez comment tooreproduce hello problème, ou si vous connaissez hello exacte durée intervalle hello performances problème se produit.

Profilage à distance est utile si hello l’utilisation du processeur du processus de hello est élevé et votre processus s’exécute plus lentement que prévu ou latence hello de requêtes HTTP est supérieur à la normale, vous pouvez à distance à profiler vos processus et obtenir hello du processeur d’échantillonnage appel piles tooanalyze Hello d’activité de processus et à chaud chemins de code.

Pour plus d’informations, consultez [Prise en charge d’analyse de profil distant dans Azure App Service](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).

##### <a name="set-up-diagnostic-traces-manually"></a>Configurer manuellement des traces de diagnostic
Si vous avez le code source d’applications web accès toohello, Application diagnostics vous permet de toocapture les informations produites par une application web. Applications ASP.NET peuvent utiliser hello `System.Diagnostics.Trace` classe toolog informations toohello application diagnostics se connecter. Toutefois, vous devez toochange hello code et redéployer votre application. Cette méthode est recommandée si votre application s’exécute sur un environnement de test.

Pour obtenir des instructions détaillées sur la façon de voir de votre application pour la journalisation, tooconfigure [activer la journalisation des diagnostics pour les applications web dans Azure App Service](web-sites-enable-diagnostic-log.md).

#### <a name="use-hello-azure-app-service-support-portal"></a>Utiliser le portail de support du Service d’applications Azure hello
Web Apps fournit hello capacité tootroubleshoot problèmes connexes tooyour web application en examinant HTTP journaux, les journaux des événements, les vidages de processus et bien plus encore. Vous pouvez accéder à toutes ces informations à l’aide de notre portail de support à l’adresse **http://&lt;your app name>.scm.azurewebsites.net/Support**

portail de support du Service d’applications Azure Hello offre trois onglets distincts toosupport hello trois étapes d’un scénario de dépannage courantes :

1. Observer le comportement actuel
2. Analyser à la collecte des informations de diagnostic et en cours d’exécution hello analyseurs intégrés
3. Résoudre

Si le problème de hello se produit dès maintenant, cliquez sur **analyser** > **Diagnostics** > **diagnostiquer maintenant** toocreate une session de diagnostic pour vous, qui collecte des journaux HTTP, Observateur d’événements, les vidages de mémoire, les journaux d’erreurs PHP et rapports de processus PHP.

Une fois la collecte des données de hello, portail de support hello exécute une analyse sur les données de salutation et vous fournit un rapport HTML.

Dans le cas des données toodownload hello, par défaut, il est stocké dans le dossier de D:\home\data\DaaS hello.

Pour plus d’informations sur le portail de support du Service d’applications Azure hello, consultez [tooSupport de nouvelles mises à jour Extension de Site des sites Web Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Utilisez hello Kudu la Console de débogage
Web Apps est fourni avec une console de débogage que vous pouvez utiliser pour le débogage, l’exploration, le téléchargement de fichiers, ainsi que les points de terminaison JSON pour obtenir des informations relatives à votre environnement. Cette console est appelée hello *Kudu Console* ou hello *tableau de bord SCM* pour votre application web.

Vous pouvez accéder à ce tableau de bord en accédant le lien toohello **https://&lt;votre nom de l’application >.scm.azurewebsites.net/**.

Certains des éléments de hello Kudu offre sont :

* paramètres d’environnement pour votre application ;
* flux de journal ;
* vidage de diagnostic ;
* console de débogage dans laquelle vous pouvez exécuter les applets de commande Powershell et les commandes DOS de base.

Une autre fonctionnalité utile de Kudu est que, dans le cas où votre application lève des exceptions de première chance, vous pouvez utiliser Kudu et images hello SysInternals outil Procdump toocreate mémoire. Ces images mémoire sont des instantanés des processus de hello et peuvent vous aider à résoudre les problèmes plus complexes avec votre application web.

Pour plus d’informations sur les fonctionnalités disponibles dans Kudu, consultez [Outils Team Services de Sites Web Azure que vous devez connaître](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Limiter le problème de hello
#### <a name="scale-hello-web-app"></a>Échelle hello web app
Dans Azure App Service, pour améliorer les performances et le débit, vous pouvez ajuster échelle hello à partir duquel vous exécutez votre application. Mise à l’échelle d’une application web implique deux actions connexes : la modification de votre tooa de plan App Service supérieur tarification et configurer certains paramètres après avoir basculé toohello niveau de tarification supérieur.

Pour plus d'informations sur la mise à l'échelle, consultez [Mise à l'échelle d'une application web dans Microsoft Azure App Service](web-sites-scale.md).

En outre, vous pouvez choisir toorun votre application sur plusieurs instances. La montée en charge vous offre plus de capacité de traitement, mais également un certain niveau de tolérance aux pannes. Si le processus de hello tombe en panne sur une instance, hello autres continuent tooserve demandes.

Vous pouvez définir hello mise à l’échelle toobe manuel ou automatique.

#### <a name="use-autoheal"></a>Utilisation de la correction automatique (AutoHeal)
AutoHeal recycle le processus de travail hello pour votre application en fonction des paramètres que vous choisissez (par exemple, les modifications de configuration, les demandes, les limites de mémoire ou une durée de hello nécessaire tooexecute une demande). La plupart du temps de hello, recycler le processus de hello est hello toorecover de façon plus rapide d’un problème. Bien que vous pouvez toujours redémarrer hello web de l’application directement dans hello portail Azure, AutoHeal fait automatiquement pour vous. Vous devez toodo est ajoutent des déclencheurs dans le fichier web.config racine de hello pour votre application web. Ces paramètres fonctionnerait Bonjour même façon, même si votre application n’est pas une application .net.

Pour plus d'informations, consultez [Correction automatique de Sites Web Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Redémarrage de l’application web de hello
Le redémarrage est souvent hello toorecover de façon la plus simple des problèmes à usage unique. Sur hello [portail Azure](https://portal.azure.com/), dans Panneau de votre application web, vous avez hello options toostop ou redémarrer votre application.

 ![Redémarrez les problèmes de performances web application toosolve](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

Vous pouvez également gérer votre application web à l’aide d’Azure PowerShell. Pour plus d'informations, consultez [Utilisation d'Azure PowerShell avec le Gestionnaire de ressources Azure](../powershell-azure-resource-manager.md).
