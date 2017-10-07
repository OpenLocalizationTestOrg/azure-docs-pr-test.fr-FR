---
title: aaaAzure Application Insights FAQ | Documents Microsoft
description: "Questions fréquentes sur Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0e3b103c-6e2a-4634-9e8c-8b85cf5e9c84
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: e27ee9b7d040a04828a9892865a6681b83f94326
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-frequently-asked-questions"></a>Application Insights : questions fréquentes

## <a name="configuration-problems"></a>Problèmes de configuration
*J’ai des difficultés à configurer :*

* [Application .NET](app-insights-asp-net-troubleshoot-no-data.md)
* [Analyse d’une application déjà en cours d’exécution](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights)
* [Diagnostics Azure](app-insights-azure-diagnostics.md)
* [Applications web Java](app-insights-java-troubleshoot.md)

*Je ne reçois aucune donnée de mon serveur*

* [Définir les exceptions de pare-feu](app-insights-ip-addresses.md)
* [Configurer un serveur ASP.NET](app-insights-monitor-performance-live-website-now.md)
* [Configurer un serveur Java](app-insights-java-agent.md)

## <a name="can-i-use-application-insights-with-"></a>Puis-je utiliser Application Insights avec... ?

* [Applications web sur un serveur IIS - en local ou sur une machine virtuelle](app-insights-asp-net.md)
* [Applications web Java](app-insights-java-get-started.md)
* [Applications Node.js](app-insights-nodejs.md)
* [Applications web sur Azure](app-insights-azure-web-apps.md)
* [Services cloud sur Azure](app-insights-cloudservices.md)
* [Serveurs d’applications exécutés dans Docker](app-insights-docker.md)
* [Applications web d’une seule page](app-insights-javascript.md)
* [Sharepoint](app-insights-sharepoint.md)
* [Applications de bureau Windows](app-insights-windows-desktop.md)
* [autres plateformes](app-insights-platforms.md)

## <a name="is-it-free"></a>Est-ce gratuit ?

Oui, pour une utilisation expérimentale. Bonjour base plan de tarification, votre application peut envoyer une certain l’allocation des données de chaque mois sans frais. l’allocation de libre Hello est suffisamment grande toocover développement et publication d’une application pour un petit nombre d’utilisateurs. Vous pouvez définir une extrémité de fin tooprevent plus d’une quantité de données spécifiée à partir d’en cours de traitement.

Volumes de grande capacité de télémétrie sont facturées à hello go. Nous fournissons des conseils sur la façon de trop[limiter vos frais](app-insights-pricing.md).

plan d’entreprise Hello implique un coût pour chaque jour de chaque nœud de serveur web envoie des données de télémétrie. Il est approprié si vous souhaitez que toouse de l’exportation continue à grande échelle.

[Hello en lecture plan de tarification](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="how-much-is-it-costing"></a>Combien cela coûte ?

* Ouvrez hello **fonctionnalités + tarification** page dans une ressource Application Insights. Cette page contient un graphique reflétant l’utilisation récente. Vous pouvez définir une limite de volume de données si vous le souhaitez.
* Ouvrez hello [Panneau de la facturation Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/BillingBlade/Overview) toosee vos factures pour toutes les ressources.

## <a name="q14"></a>Que modifie Application Insights dans mon projet ?
Détails de Hello dépendent de type hello de projet. Pour une application web :

* Ajoute le projet tooyour de ces fichiers :

  * ApplicationInsights.config.
  * ai.js
* Installe ces packages NuGet :

  * *API application Insights* hello - API de base
  * *L’API application Insights pour les Applications Web* -utilisé télémétrie toosend à partir du serveur de hello
  * *L’API application Insights pour les Applications JavaScript* -utilisé télémétrie toosend à partir du client de hello

    les packages Hello incluant ces assemblys :
  * Microsoft.ApplicationInsights
  * Microsoft.ApplicationInsights.Platform
* Insère des éléments dans :

  * Web.config
  * packages.config
* (Nouvelle projets uniquement - si vous [ajouter Application Insights un projet existant tooan][start], vous avez toodo cela manuellement.) Insérer des extraits de code tooinitialize du code hello client et le serveur avec l’ID de ressource Application Insights hello. Par exemple, dans une application MVC, le code est inséré dans la page maître de hello Views/Shared/_Layout.cshtml

## <a name="how-do-i-upgrade-from-older-sdk-versions"></a>Comment mettre à niveau à partir d'anciennes versions du Kit de développement logiciel (SDK) ?
Consultez hello [notes de publication](app-insights-release-notes.md) pour hello Kit de développement logiciel appropriés type tooyour d’application.

## <a name="update"></a>Comment puis-je changer la ressource Azure à laquelle mon projet envoie des données ?
Dans l’Explorateur de solutions, cliquez avec le bouton droit sur `ApplicationInsights.config` , puis sélectionnez **Mettre à jour Application Insights**. Vous pouvez envoyer des ressources de nouveau ou existant la tooan des données hello dans Azure. changement de l’Assistant Mise à jour Hello hello clé d’instrumentation dans ApplicationInsights.config, qui détermine où le serveur hello SDK envoie vos données. Sauf si vous désélectionnez « Tout mettre à jour », il est également modifiée clé hello où il apparaît dans vos pages web.

## <a name="what-is-status-monitor"></a>Qu’est-ce que Status Monitor ?

Une application de bureau que vous pouvez utiliser dans votre toohelp de serveur web IIS configurer Application Insights dans les applications web. Cette application ne collecte pas de données de télémétrie : vous pouvez l’arrêter lorsque vous ne configurez pas une application. 

[En savoir plus](app-insights-monitor-performance-live-website-now.md#questions).

## <a name="what-telemetry-is-collected-by-application-insights"></a>Quelles sont les données de télémétrie recueillies par Application Insights ?

À partir d’applications web serveur :

* Requêtes HTTP
* [Dépendances](app-insights-asp-net-dependencies.md). Les appels à : bases de données SQL ; HTTP appelle tooexternal services ; Azure Cosmos DB, table, stockage d’objets blob et file d’attente. 
* [Exceptions](app-insights-asp-net-exceptions.md) et arborescences des appels de procédure.
* [Les compteurs de performance](app-insights-performance-counters.md) : Si vous utilisez [Status Monitor](app-insights-monitor-performance-live-website-now.md), monitoring(app-insights-azure-web-apps.md) Azure ou hello [writer de collectd Application Insights](app-insights-java-collectd.md).
* [Événements et mesures personnalisés](app-insights-api-custom-events-metrics.md) que vous codez.
* [Journaux de suivi](app-insights-asp-net-trace-logs.md) si vous configurez le collecteur approprié de hello.

À partir des [ pages web client](app-insights-javascript.md) :

* [Nombre de pages consultées](app-insights-web-track-usage.md)
* [Appels AJAX](app-insights-asp-net-dependencies.md). Requêtes transmises à partir d’un script en cours d’exécution.
* Données relatives au chargement de pages
* Nombre de sessions et d’utilisateurs
* [ID des utilisateurs authentifiés](app-insights-api-custom-events-metrics.md#authenticated-users)

À partir d’autres sources, si vous les configurez :

* [Diagnostics Azure](app-insights-azure-diagnostics.md)
* [Conteneurs Docker](app-insights-docker.md)
* [Importation de tables tooAnalytics](app-insights-analytics-import.md)
* [OMS (Log Analytics)](https://azure.microsoft.com/blog/omssolutionforappinsightspublicpreview/)
* [Logstash](app-insights-analytics-import.md)

## <a name="can-i-filter-out-or-modify-some-telemetry"></a>Puis-je filtrer ou modifier des données de télémétrie ?

Oui, dans le serveur hello que vous pouvez écrire :

* Télémétrie processeur toofilter ou ajouter des propriétés des éléments de télémétrie tooselected avant leur envoi à partir de votre application.
* Télémétrie tooadd propriétés tooall les éléments d’initialiseur de télémétrie.

En savoir plus pour [ASP.NET](app-insights-api-filtering-sampling.md) ou [Java](app-insights-java-filter-telemetry.md).

## <a name="how-are-city-country-and-other-geo-location-data-calculated"></a>Comment sont calculées les données relative à la ville, au pays et aux autres emplacements géographiques ?

Nous allons adresse hello IP (IPv4 ou IPv6) d’à l’aide de WebClient hello [GeoLite2](http://dev.maxmind.com/geoip/geoip2/geolite2/).

* Données de télémétrie de navigateur : nous collectons adresse IP hello son.
* Télémétrie Server : module d’Application Insights hello collecte l’adresse IP du client hello. Elle n’est pas collectée si `X-Forwarded-For` est défini.

Vous pouvez configurer hello `ClientIpHeaderTelemetryInitializer` adresse tootake hello à partir d’un autre en-tête. Dans certains systèmes, par exemple, il est déplacé par un proxy, puis chargez d’équilibreur de charge ou CDN trop`X-Originating-IP`. [En savoir plus](http://apmtips.com/blog/2016/07/05/client-ip-address/).

Vous pouvez [utiliser Power BI](app-insights-export-power-bi.md) toodisplay votre télémétrie des requêtes sur une carte.


## <a name="data"></a>La durée pendant laquelle les données sont conservées dans le portail de hello ? Sont-elles sécurisées ?
Voir [Rétention de données et confidentialité][data].

## <a name="might-personally-identifiable-information-pii-be-sent-in-hello-telemetry"></a>Peuvent les informations d’identification personnelle (PII) être envoyées dans la télémétrie de hello ?

Cela est possible si votre code envoie ce type de données. Cela peut également se produire si les variables dans les arborescences des appels de procédure incluent des informations d’identification personnelle. Votre équipe de développement doit mener tooensure d’évaluations de risques dont les informations d’identification personnelle sont traitées correctement. [En savoir plus sur la rétention et la confidentialité des données](app-insights-data-retention-privacy.md).

Hello dernier octet d’adresse web du client hello est toujours la valeur too0 après réception par le portail de hello.

## <a name="my-ikey-is-visible-in-my-web-page-source"></a>Mon iKey est visible dans la source de ma page web. 

* Il s’agit d’une pratique courante dans les solutions de surveillance.
* Il ne peut pas être utilisé toosteal vos données.
* Il peut être utilisé tooskew vos alertes de données ou du déclencheur.
* Aucun client ne nous a jamais signalé ce type de problème.

Vous pouvez :

* Utilisez deux iKeys distincts (ressources Application Insights distinctes) pour les données client et serveur. Ou
* Écrire un proxy qui s’exécute sur votre serveur et avoir WebClient hello à envoyer des données via ce proxy.

## <a name="post"></a>Comment consulter les données POST dans la fonction Recherche de diagnostic ?
Nous n’enregistre pas automatiquement les données de publication, mais vous pouvez utiliser un appel TrackTrace : placer des données de hello dans le paramètre de message hello. Cela a une limite de taille plus de temps que les limites de hello sur les propriétés de chaîne, si vous ne pouvez pas filtrer sur celui-ci.

## <a name="should-i-use-single-or-multiple-application-insights-resources"></a>Dois-je utiliser une ou plusieurs ressources Application Insights ?

Utiliser une ressource unique pour tous les composants de hello ou les rôles dans un système d’entreprise unique. Utilisez des ressources distinctes pour les versions de développement, de test et de publication, et pour les applications indépendantes.

* [Consultez la discussion hello ici](app-insights-separate-resources.md)
* [Exemple : service cloud avec des rôles web et worker](app-insights-cloudservices.md)

## <a name="how-do-i-dynamically-change-hello-instrumentation-key"></a>Comment modifier dynamiquement clé d’instrumentation hello ?

* [Discussion ici](app-insights-separate-resources.md)
* [Exemple : service cloud avec des rôles web et worker](app-insights-cloudservices.md)

## <a name="what-are-hello-user-and-session-counts"></a>Quelles sont les hello utilisateur et la Session de compte ?

* Hello SDK JavaScript définit un cookie de l’utilisateur sur hello client web, les utilisateurs de retour tooidentify et activités de toogroup de cookie de session.
* S’il n’existe aucun script côté client, vous pouvez [définir des cookies sur le serveur de hello](http://apmtips.com/blog/2016/07/09/tracking-users-in-api-apps/).
* Si un utilisateur réel utilise votre site dans différents navigateurs, ou s’il utilise une navigation privée ou encore des ordinateurs différents, il sera comptabilisé plusieurs fois.
* tooidentify un utilisateur connecté sur les ordinateurs et les navigateurs, ajoutez un appel trop[setAuthenticatedUserContect()](app-insights-api-custom-events-metrics.md#authenticated-users).

## <a name="q17"></a> Comment savoir si j'ai activé tout ce qu'il faut pour utiliser Application Insights ?
| Ce qui suit doit s'afficher | Comment tooget il | Utilité |
| --- | --- | --- |
| Graphiques de disponibilité |[Tests web](app-insights-monitor-web-app-availability.md) |Savoir si votre application web est active |
| Performances des applications de serveur (temps de réponse, etc.) |[Ajouter le projet d’Application Insights tooyour](app-insights-asp-net.md) ou [installer AI Status Monitor sur serveur](app-insights-monitor-performance-live-website-now.md) (ou écrire votre propre code trop[suivre les dépendances](app-insights-api-custom-events-metrics.md#trackdependency)) |Détecter les problèmes de performances |
| Télémétrie des dépendances |[Installation d’AI Status Monitor sur le serveur](app-insights-monitor-performance-live-website-now.md) |Diagnostiquer les problèmes relatifs à des bases de données ou à d'autres composants externes |
| Obtention de l'arborescence des appels de procédure à partir des exceptions |[Insertion d’appels TrackException dans votre code](app-insights-asp-net-exceptions.md) (certains d’entre eux sont cependant signalés automatiquement) |Détecter et diagnostiquer les exceptions |
| Recherche des données de suivi des journaux |[Ajout d’un enregistreur de données](app-insights-asp-net-trace-logs.md) |Diagnostiquer les exceptions et problèmes de performances |
| Principes fondamentaux d'utilisation des clients (vues de page, sessions, etc.) |[Initialiseur JavaScript dans les pages web](app-insights-javascript.md) |Analyse de l'utilisation |
| Mesures personnalisées des clients |[Appels de suivi dans les pages web](app-insights-api-custom-events-metrics.md) |Améliorer l'expérience utilisateur |
| Mesures personnalisées des serveurs |[Appels de suivi dans le serveur](app-insights-api-custom-events-metrics.md) |Décisionnel |

## <a name="why-are-hello-counts-in-search-and-metrics-charts-unequal"></a>Pourquoi les hello compte dans les graphiques de recherche et des mesures différentes ?

[Échantillonnage](app-insights-sampling.md) réduit le nombre hello d’éléments de télémétrie (demandes, les événements personnalisés, etc.) qui sont réellement envoyé à partir de votre portail toohello d’application. Dans la recherche, vous voyez nombre hello d’éléments réellement reçu. Dans les graphiques de métriques qui affichent le nombre d’événements, vous voyez nombre hello d’événements d’origine qui s’est produite. 

Chaque élément transmis comporte une propriété `itemCount` qui indique le nombre d’événements d’origine que représente cet élément. tooobserve d’échantillonnage dans l’opération, vous pouvez exécuter cette requête dans Analytique :

```
    requests | summarize original_events = sum(itemCount), transmitted_events = count()
```


## <a name="automation"></a>Automatisation

### <a name="configuring-application-insights"></a>Configuration d'Application Insights

Vous pouvez [écrire des scripts PowerShell](app-insights-powershell.md) à l’aide du moniteur de ressources Azure pour :

* Créer et mettre à jour des ressources Application Insights.
* Définissez hello plan de tarification.
* Obtenir la clé d’instrumentation hello.
* Ajouter une alerte métrique.
* Ajouter un test de disponibilité.

Vous ne peut pas définir un rapport état Metrics Explorer ou configurer une exportation continue.

### <a name="querying-hello-telemetry"></a>Interrogation des données de télémétrie hello

Hello d’utilisation [API REST](https://dev.applicationinsights.io/) toorun [Analytique](app-insights-analytics.md) requêtes.

## <a name="how-can-i-set-an-alert-on-an-event"></a>Comment puis-je définir une alerte sur un événement ?

Les alertes Azure portent uniquement sur les mesures. Créez une mesure personnalisée qui dépasse un seuil de valeur chaque fois que l’événement se produit. Puis définir une alerte sur métrique de hello. Notez que : vous recevrez une notification chaque fois que la métrique de hello dépasse le seuil de hello dans les deux sens ; Vous ne recevez une notification jusqu'à ce que hello premier passage, quel que soit l’indique si la valeur initiale de hello est élevé ou faible ; Il existe toujours une latence de quelques minutes.

## <a name="are-there-data-transfer-charges-between-an-azure-web-app-and-application-insights"></a>Existe-t-il des frais de transfert de données entre une application web Azure et Application Insights ?

* Si votre application web Azure est hébergée dans un centre de données qui comporte un point de terminaison de collecte Application Insights, aucuns frais ne sont appliqués. 
* S’il n’existe aucun point de terminaison de collecte dans votre centre de données hôte, les données de télémétrie de votre application généreront des [frais Azure de trafic sortant](https://azure.microsoft.com/pricing/details/bandwidth/).

Cela ne dépend pas de l’emplacement où est hébergée votre ressource Application Insights. Il dépend simplement de distribution hello de ses points de terminaison.

## <a name="can-i-send-telemetry-toohello-application-insights-portal"></a>Puis-je envoyer portail de télémétrie toohello Application Insights ?

Nous vous recommandons de vous utilisez nos kits de développement logiciel et hello API du Kit de développement logiciel (app-insights-api-custom-events-metrics.md). Il existe des variantes de hello SDK pour différentes [plateformes](app-insights-platforms.md). Ces kits de développement logiciel gèrent la mise en mémoire tampon, la compression, la limitation, les nouvelles tentatives, etc. Toutefois, hello [schéma d’ingestion](https://github.com/Microsoft/ApplicationInsights-dotnet/tree/develop/Schema/PublicSchema) et [protocole de point de terminaison](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/EndpointSpecs/ENDPOINT-PROTOCOL.md) sont publics.

## <a name="can-i-monitor-an-intranet-web-server"></a>Puis-je surveiller un serveur web intranet ?

Il existe deux méthodes :

### <a name="firewall-door"></a>Pare-feu

Autoriser votre web server toosend télémétrie tooour points de terminaison https://dc.services.visualstudio.com:443 et le https://rt.services.visualstudio.com:443. 

### <a name="proxy"></a>Proxy

Acheminer le trafic à partir de votre serveur de passerelle tooa sur votre intranet, en définissant ce paramètre dans ApplicationInsights.config :

```XML
<TelemetryChannel>
    <EndpointAddress>your gateway endpoint</EndpointAddress>
</TelemetryChannel>
```

Votre passerelle doit acheminer toohttps://dc.services.visualstudio.com:443/v2/suivi de trafic hello

## <a name="can-i-run-availability-web-tests-on-an-intranet-server"></a>Puis-je exécuter des tests web de disponibilité sur un serveur intranet ?

Notre [tests web](app-insights-monitor-web-app-availability.md) s’exécutent sur des points de présence sont distribuées monde hello. Il existe deux solutions :

* Porte de pare-feu : autoriser les demandes serveur tooyour [hello long et liste modifiable du site web des agents de test](app-insights-ip-addresses.md).
* Écrire votre propre code toosend des demandes périodiques tooyour serveur à partir de votre intranet. Vous pouvez exécuter des tests web Visual Studio à cet effet. testeur de Hello a pu envoyer les résultats hello Insights tooApplication à l’aide de hello TrackAvailability() API.

## <a name="more-answers"></a>Réponses supplémentaires
* [Forum Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

<!--Link references-->

[data]: app-insights-data-retention-privacy.md
[platforms]: app-insights-platforms.md
[start]: app-insights-overview.md
[windows]: app-insights-windows-get-started.md
