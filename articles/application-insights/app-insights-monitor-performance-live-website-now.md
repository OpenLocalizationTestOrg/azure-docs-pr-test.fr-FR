---
title: aaaMonitor un dynamique ASP.NET web application avec Azure Application Insights | Documents Microsoft
description: "Analysez les performances d'un site web sans le redéployer. Fonctionne avec les applications web ASP.NET hébergées localement, dans des machines virtuelles ou sur Azure."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Instrumenter des applications web lors de l’exécution avec Application Insights


Vous pouvez instrumenter une application web dynamique avec Azure Application Insights, sans avoir toomodify ou redéployer votre code. Si vos applications sont hébergées sur un serveur IIS local, installez Status Monitor. S’ils sont des applications web Azure ou que vous exécutent dans une machine virtuelle Azure, vous pouvez basculer sur la surveillance de l’Application Insights à partir du Panneau de configuration Azure hello. (Des articles distincts sont également consacrés à l’instrumentation des [applications web J2EE actives](app-insights-java-live.md) et [d’Azure Cloud Services](app-insights-cloudservices.md).) Cette opération nécessite un abonnement [Microsoft Azure](http://azure.com) .

![Exemples de graphiques](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

Vous avez le choix entre trois itinéraires tooapply Application Insights tooyour .NET web applications :

* **Heure de création :** [hello d’ajouter Application Insights SDK] [ greenbrown] code d’application web tooyour.
* **Durée d’exécution :** instrumenter votre application web sur le serveur de hello, comme décrit ci-dessous, sans régénérer et redéployer les code hello.
* **Les deux :** générer hello SDK dans votre code d’application web et s’appliquent également des extensions d’exécution hello. Obtenir hello meilleur des deux options.

Voici un résumé de ce que vous apporte chaque méthode :

|  | En cours de création | En cours d’exécution |
| --- | --- | --- |
| Requêtes et exceptions |Oui |Oui |
| [Exceptions plus détaillées](app-insights-asp-net-exceptions.md) | |Oui |
| [Diagnostics de dépendance](app-insights-asp-net-dependencies.md) |Sur .NET 4.6 +, mais moins détaillé |Oui, tous les détails : codes de résultat, texte de commande SQL, verbe HTTP|
| [Compteurs de performances système](app-insights-performance-counters.md) |Oui |Oui |
| [API pour la télémétrie personnalisée][api] |Oui |Non |
| [Intégration des journaux de suivi](app-insights-asp-net-trace-logs.md) |Oui |Non |
| [Mode Page et données utilisateur](app-insights-javascript.md) |Oui |Non |
| Besoin de code toorebuild |Oui | Non |


## <a name="monitor-a-live-azure-web-app"></a>Surveiller une application web Azure active

Si votre application s’exécute en tant que Azure d’un service web, voici comment tooswitch sur la surveillance :

* Sélectionnez l’Application Insights sur le panneau de configuration l’application hello dans Azure.

    ![Configurer Application Insights pour une application web Azure](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Lors de la page de résumé Application Insights hello s’ouvre, cliquez sur le lien de hello en hello bas tooopen hello complète ressource Application Insights.

    ![Parcourez tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Surveillance des applications de machine virtuelle et cloud](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Activation de la surveillance côté client dans Azure

Si vous avez activé Application Insights dans Azure, vous pouvez ajouter la consultation de page et la télémétrie de l’utilisateur.

1. Cliquez sur Paramètres > Paramètres de l’application.
2.  Sous Paramètres de l’application, ajoutez une nouvelle paire clé/valeur : 
   
    Clé :`APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Valeur: `true`
3. **Enregistrer** hello paramètres et **redémarrer** votre application.

Hello SDK de JavaScript Application Insights est désormais injecté dans chaque page web.

## <a name="monitor-a-live-iis-web-app"></a>Surveiller une application web IIS active

Si votre application est hébergée sur un serveur IIS, activez Application Insights à l’aide de Status Monitor.

1. Sur votre serveur web IIS, connectez-vous avec vos informations d’identification d’administrateur.
2. Si l’Application Insights Status Monitor n’est pas déjà installé, téléchargez et exécutez hello [programme d’installation du moniteur d’état](http://go.microsoft.com/fwlink/?LinkId=506648) (ou exécutez [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) et recherchez Application Insights état qu’il contient Moniteur).
3. Dans le moniteur d’état, sélectionnez application hello installé ou site Web que vous souhaitez toomonitor. Connectez-vous avec vos informations d’identification Azure.

    Configurez la ressource hello où vous intéresse toosee hello portail Application Insights de hello. (Normalement, il est meilleure toocreate une nouvelle ressource. Sélectionnez une ressource existante si vous avez déjà configuré des [tests web][availability] ou une [Surveillance du client][client] pour cette application.) 

    ![Choisissez une application et une ressource.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. Redémarrez IIS.

    ![Cliquez sur Redémarrer haut hello de boîte de dialogue hello.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    Votre service web sera interrompu pendant une courte période.

## <a name="customize-monitoring-options"></a>Personnaliser les options de surveillance

L’activation d’Application Insights ajoute des DLL et ApplicationInsights.config tooyour l’application web. Vous pouvez [modifier le fichier .config de hello](app-insights-configuration-with-applicationinsights-config.md) toochange certaines des options de hello.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>Lorsque vous republiez votre application, réactivez Application Insights

Avant de vous republiez votre application, pensez à [Ajout de code d’Application Insights toohello dans Visual Studio][greenbrown]. Vous obtenez la télémétrie plus détaillée et une télémétrie personnalisée hello capacité toowrite.

Si vous souhaitez que toore-publier sans ajouter Application Insights toohello code, n’oubliez pas que les processus de déploiement hello peuvent supprimer les DLL hello et ApplicationInsights.config de hello publié le site web. Par conséquent :

1. Si vous avez modifié le fichier ApplicationInsights.config, copiez-le avant de republier votre application.
2. Republiez votre application.
3. Réactivez la surveillance d’Application Insights. (Utilisez la méthode appropriée de hello : hello Azure web app le panneau de configuration ou de hello Status Monitor sur un ordinateur hôte IIS.)
4. Rétablir les modifications que vous avez effectué sur le fichier .config de hello.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Résolution des problèmes de configuration d’exécution d’Application Insights

### <a name="cant-connect-no-telemetry"></a>Vous n’arrivez pas à vous connecter ? Vous n’obtenez aucune donnée de télémétrie ?

* Ouvrez [hello ports sortants nécessaires](app-insights-ip-addresses.md#outgoing-ports) dans toowork de moniteur d’état de votre serveur pare-feu tooallow.

* Ouvrez Status Monitor et sélectionnez votre application dans le volet gauche. Vérifiez la présence des messages de diagnostic pour cette application Bonjour section « Configuration de notifications » :

  ![Demande de toosee panneau hello ouvrir performances, temps de réponse, dépendances et autres données](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* Sur le serveur de hello, si vous voyez un message sur « Autorisations insuffisantes », essayez suivant de hello :
  * Dans le Gestionnaire des services Internet, sélectionnez le pool d’applications, ouvrez **paramètres avancés**et sous **modèle de processus** Notez l’identité de hello.
  * Dans le panneau de configuration ordinateur gestion, ajoutez cet identité toohello groupe.
* Si des services MMA/SCOM (Systems Center Operations Manager) sont installés sur votre serveur, certaines versions peuvent entrer en conflit. Désinstallez SCOM et le moniteur d’état et réinstallez les versions les plus récentes hello.
* Consultez la rubrique [Résolution des problèmes][qna].

## <a name="system-requirements"></a>Configuration requise
Prise en charge du système d’exploitation pour Application Insights Status Monitor sur le serveur :

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

avec le dernier Service Pack et .NET Framework 4.5

Côté client de hello : Windows 7, 8, 8.1 et 10, à l’aide de .NET Framework 4.5

Prise en charge d’IIS : IIS 7, 7.5, 8, 8.5 (IIS requis)

## <a name="automation-with-powershell"></a>Automation avec PowerShell
Vous pouvez démarrer et arrêter la surveillance à l’aide de PowerShell sur votre serveur IIS.

Module d’Application Insights hello d’abord importer :

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Identifiez les applications qui sont surveillées :

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`Nom hello (facultatif) d’une application web.
* Affiche hello état d’analyse pour chaque application web (ou hello nommé app) Application Insights dans ce serveur IIS.
* Retourne `ApplicationInsightsApplication` pour chaque application :

  * `SdkState==EnabledAfterDeployment`: Application en cours d’analyse et a été instrumentée en cours d’exécution, soit par l’outil d’analyse de l’état de hello, soit en `Start-ApplicationInsightsMonitoring`.
  * `SdkState==Disabled`: application hello n’est pas instrumentée pour Application Insights. Il a été instrumenté jamais, ou analyse de l’exécution a été désactivée avec l’outil d’analyse d’état hello ou `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: application hello a été instrumentée en ajoutant le code source de hello SDK toohello. Son Kit de développement logiciel (SDK) ne peut pas être mis à jour ou arrêté.
  * `SdkVersion`Affiche la version de hello en cours d’utilisation pour l’analyse de cette application.
  * `LatestAvailableSdkVersion`Affiche la version hello actuellement disponible dans la galerie NuGet de hello. version de toothis application tooupgrade hello, utilisez `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`nom Hello de l’application hello dans IIS
* `-InstrumentationKey`Bonjour ikey Hello ressource Application Insights où vous souhaitez hello toobe de résultats affiché.
* Cette applet de commande affecte uniquement les applications qui ne sont pas déjà instrumentées, c’est-à-dire SdkState==NotInstrumented.

    applet de commande Hello n’affecte pas une application qui est déjà instrumentée. Il ne pas important que l’application hello a été instrumentée au moment de la génération en ajoutant le code de toohello hello SDK, ou au moment de l’exécution par l’utilisation précédente de cette applet de commande.

    application de hello tooinstrument Hello SDK version utilisée est version hello qui a été la plus récemment téléchargé toothis server.

    version la plus récente toodownload hello, utilisez ApplicationInsightsVersion de mise à jour.
* Retourne `ApplicationInsightsApplication` en cas de réussite. En cas d’échec, il connecte à un toostderr de trace.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`nom Hello d’une application dans IIS
* `-All` Arrête la surveillance de toutes les applications de ce serveur IIS pour lequel `SdkState==EnabledAfterDeployment`
* Arrête l’analyse hello applications spécifiées et supprime l’instrumentation. Il fonctionne uniquement pour les applications qui ont été instrumentées au moment de l’exécution à l’aide hello outil de surveillance de l’état ou ApplicationInsightsApplication de début. (`SdkState==EnabledAfterDeployment`)
* Renvoie ApplicationInsightsApplication.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: nom hello d’une application web dans IIS.
* `-InstrumentationKey` (Facultatif.) Utilisez que cette toochange hello ressource toowhich hello de télémétrie application est envoyé.
* Cette applet de commande :
  * Hello mises à niveau nommé toohello version de l’application Hello SDK toothis machine téléchargée le plus récemment. (Ne fonctionne que si `SdkState==EnabledAfterDeployment`)
  * Si vous fournissez une clé d’instrumentation, hello nommé app est reconfiguré toosend télémétrie toohello ressource avec cette clé. (Fonctionne si `SdkState != Disabled`)

`Update-ApplicationInsightsVersion`

* Télécharge hello dernière Application Insights toohello serveur SDK.

## <a name="questions"></a>Questions sur Status Monitor

### <a name="what-is-status-monitor"></a>Qu’est-ce que Status Monitor ?

Il s’agit d’une application de bureau que vous installez sur votre serveur web IIS. Il vous permet d’instrumenter et de configurer des applications web. 

### <a name="when-do-i-use-status-monitor"></a>Quand dois-je utiliser Status Monitor ?

* tooinstrument un web application qui s’exécute sur votre serveur IIS - même si elle est déjà en cours d’exécution.
* tooenable de télémétrie supplémentaires pour les applications web qui ont été [intègrent hello Application Insights SDK](app-insights-asp-net.md) au moment de la compilation. 

### <a name="can-i-close-it-after-it-runs"></a>Puis-je le fermer il après son exécution ?

Oui. Une fois qu’il a instrumenté hello des sites Web que vous sélectionnez, vous pouvez le fermer.

Il ne collecte pas la télémétrie par lui-même. Simplement, il configure les applications web hello et définit certaines autorisations.

### <a name="what-does-status-monitor-do"></a>Que fait Status Monitor ?

Lorsque vous sélectionnez une application web pour le moniteur d’état tooinstrument :

* Télécharge et place des assemblys d’Application Insights hello et le fichier .config dans le dossier des fichiers binaires de l’application hello web.
* Modifie `web.config` module de suivi Application Insights HTTP tooadd hello.
* Active les appels de dépendance toocollect de profilage du CLR.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>Dois-je toorun moniteur d’état chaque fois que l’application hello mise à jour ?

Cela n’est pas nécessaire si vous la redéployez de façon incrémentielle. 

Si vous sélectionnez l’option « Supprimer les fichiers existants » de hello Bonjour processus de publication, vous devez exécuter de toore Status Monitor tooconfigure Application Insights.

### <a name="what-telemetry-is-collected"></a>Quel type de télémétrie est collecté ?

Pour les applications que vous instrumentez uniquement au moment de l’exécution à l’aide de Status Monitor :

* Des requêtes HTTP
* Appels toodependencies
* Exceptions
* Compteurs de performances

Pour les applications déjà instrumentées au moment de la compilation :

 * Des compteurs de processus.
 * Des appels de dépendances (.NET 4.5) ; des valeurs de retour dans des appels de dépendances (.NET 4.6).
 * Des valeurs d’arborescence des appels de procédure d’exception.

[En savoir plus](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>Étapes suivantes

Affichez vos données de télémétrie :

* [Explorer les métriques](app-insights-metrics-explorer.md) toomonitor performances et utilisation
* [Rechercher des événements et journaux] [ diagnostic] toodiagnose problèmes
* [Utilisez la fonctionnalité Analytics](app-insights-analytics.md) pour des requêtes plus élaborées
* [Créez des tableaux de bord](app-insights-dashboards.md)

Ajoutez des données de télémétrie :

* [Créer des tests web] [ availability] toomake que votre site reste active.
* [Ajouter des données de télémétrie de client web] [ usage] toosee des exceptions à partir de code de page web et toolet vous insérez trace des appels.
* [Ajouter le code d’Application Insights SDK tooyour] [ greenbrown] afin que vous pouvez insérer la trace et enregistrer les appels

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
