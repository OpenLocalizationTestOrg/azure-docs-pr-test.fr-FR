---
title: "volume de la tarification et les données aaaManage pour Azure Application Insights | Documents Microsoft"
description: "Gérer les volumes de données de télémétrie et surveiller les coûts dans Application Insights."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: ebd0d843-4780-4ff3-bc68-932aa44185f6
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: bwren
ms.openlocfilehash: 4621c989cd467735aefc48ec9547fcbe1b1ae41b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-pricing-and-data-volume-in-application-insights"></a>Gérer la tarification et le volume de données dans Application Insights


La tarification pour [Azure Application Insights][start] est basée sur le volume de données par application. Faible utilisation pendant le développement ou pour une petite application est probablement toobe libre, car il existe une indemnité mensuelle de 1 Go de données de télémétrie.

Chaque ressource Application Insights est facturé comme un service distinct et qui contribue facture toohello tooAzure de votre abonnement.

Il existe deux plans de tarification. plan de Hello par défaut est nommé Basic. Vous pouvez opter pour le plan d’entreprise hello, qui a une charge quotidienne, mais permet à certaines fonctionnalités supplémentaires telles que [exportation continue](app-insights-export-telemetry.md).

Si vous avez des questions sur le fonctionne de la tarification pour Application Insights, vous pouvez toopost libre une question dans nos [forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=ApplicationInsights). 

## <a name="hello-price-plans"></a>prix des plans Hello

Consultez hello [Application Insights, page de tarification] [ pricing] de prix actuelles dans votre devise.

### <a name="basic-plan"></a>Plan De base

plan de base Hello est par défaut de hello lorsqu’une nouvelle ressource Application Insights est créée et est suffisante pour la plupart des clients.

* Dans le plan de base hello, vous êtes facturé par volume de données : nombre d’octets de télémétrie reçus par l’Application Insights. Volume de données est mesuré en taille hello du package de données JSON hello non compressé reçu par Application Insights à partir de votre application.
Pour [des données tabulaires importées dans Analytique](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-import), volume de données hello est mesurée comme hello taille non compressée des fichiers envoyés tooApplication Insights.  
* Votre première 1 Go pour chaque application est gratuite, si vous utilisez simplement d’expérimentation ou de développement, vous êtes peu probable toohave toopay.
* Les données des [Flux de métriques temps réel](app-insights-live-stream.md) ne sont pas comptabilisées dans la tarification.
* [Exportation continue](app-insights-export-telemetry.md) est disponible pour des frais supplémentaires par Go dans le plan de base hello.

### <a name="enterprise-plan"></a>Plan Entreprise

* Dans le plan d’entreprise hello, votre application peut utiliser toutes les fonctionnalités de hello d’Application Insights. L[’exportation continue](app-insights-export-telemetry.md) et 

[Connecteur d’Analytique de journal](https://go.microsoft.com/fwlink/?LinkId=833039&amp;clcid=0x409) sont disponibles sans les frais supplémentaires dans le plan d’entreprise hello.
* Vous payez par nœud qui envoie des données de télémétrie pour toutes les applications dans le plan d’entreprise hello. 
 * Un *nœud* correspond à une machine serveur virtuelle ou physique ou à une instance de rôle Platform-as-a-Service qui héberge votre application.
 * Les ordinateurs de développement, les navigateurs clients et les appareils mobiles ne sont pas comptés comme nœuds.
 * Si votre application comporte plusieurs composants qui envoient des données de télémétrie, comme un service web et un Worker back-end, ces composants sont comptés séparément.
 * Les données [Flux de métriques en temps réel](app-insights-live-stream.md) ne sont pas comptabilisées dans la tarification.* Dans un abonnement, vos frais sont calculés par nœud et non par application. Si vous disposez de cinq nœuds envoi des données de télémétrie pour applications 12, puis hello facture est de cinq nœuds.
* Bien que les frais indiqués soient par mois, vous êtes facturé uniquement pour toutes les heures dans lesquelles un nœud envoie des données de télémétrie à partir d’une application. Bonjour tarif horaire est hello entre guillemets frais mensuels / 744 (hello le nombre d’heures dans un mois de 31 jours).
* Une allocation de volume de données de 200 Mo par jour est accordée pour chaque nœud détecté (avec une granularité par heure). L’allocation des données inutilisées n'est pas reportée à partir d’un jour toohello ensuite.
 * Si vous choisissez hello option tarification d’entreprise, chaque abonnement Obtient une indemnité de données en fonction du nombre de hello de nœuds d’envoi de données de télémétrie toohello ressource Application Insights dans cet abonnement. Par conséquent, si vous avez des 5 nœuds envoi de données toute la journée, vous aurez une allocation mis en pool des ressources d’Application Insights 1 Go appliqué tooall hello dans cet abonnement. Peu importe si certains nœuds sont envoie que plus de données que les autres nœuds hello inclus des données sont partagés entre tous les nœuds. Si un jour donné, ressources d’Application Insights hello recevoir davantage de données est inclus dans l’allocation des données quotidiennes hello pour cet abonnement, hello par Go dépassement des frais s’appliquent. 
 * allocation de données quotidienne Hello est calculée en tant que nombre de hello d’heures dans hello jour (UTC) que chaque nœud envoie des données de télémétrie divisée par 24 heures 200 Mo. Ainsi, si vous disposez de 4 nœuds envoi télémétrie pendant 15 Hello jour de hello de 24 heures, hello inclus données pour ce jour serait ((4 x 15) / 24) x 200 Mo = 500 Mo. Prix hello 2.30 USD par Go pour le dépassement de données, les frais de hello pour s’EUR 1,15 si les nœuds hello envoient 1 Go de données dans la journée.
 * Notez qu’indemnité du plan d’entreprise hello n’est pas partagée avec les applications pour lesquelles vous avez choisi d’option de base hello et indemnités inutilisée ne sont pas reportée d’un jour. 
* Voici quelques exemples de détermination du nombre de nœuds distincts :
| Scénario                               | Nombre total de nœuds quotidien |
|:---------------------------------------|:----------------:|
| 1 application utilise 3 instances d'Azure App Service et 1 serveur virtuel | 4 |
| 3 applications en cours d’exécution sur 2 machines virtuelles et les ressources d’Application Insights hello pour ces applications sont dans hello même abonnement et dans hello entreprise planifier | 2 | 
| dont les ressources Insights d’Applications se trouvent dans les 4 applications hello même abonnement. Chaque application exécute 2 instances pendant 16 heures creuses et 4 instances pendant 8 heures de pointe. | 13.33 | 
| Services cloud avec 1 rôle de travail et 1 rôle web, chacune exécutant 2 instances | 4 | 
| Cluster de 5 nœuds Service Fabric exécutant 50 micro-services, chaque micro-service exécutant 3 instances | 5|

* comportement de comptage de nœud précis Hello varie sur lequel utilise le Kit de développement logiciel Application Insights votre application. 
  * Dans les versions du Kit de développement logiciel 2.2 et, à la fois hello Application Insights [kit](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) ou [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) sera chaque hôte d’application en tant que nœud de rapports, par exemple hello nom d’ordinateur pour le serveur physique et les hôtes d’ordinateur virtuel ou hello nom de l’instance dans les cas de hello de services de cloud computing.  Hello la seule exception est applications uniquement à l’aide de [.NET Core](https://dotnet.github.io/) et hello Application Insights Core SDK, dans lequel cas qu’un seul nœud sera signalé pour tous les ordinateurs hôtes, car le nom d’hôte hello n’est pas disponible. 
  * Pour les versions antérieures du Kit de développement logiciel de hello, hello [Web SDK](https://www.nuget.org/packages/Microsoft.ApplicationInsights.Web/) se comporteront comme hello versions plus récentes de kit de développement logiciel, toutefois hello [kit](https://www.nuget.org/packages/Microsoft.ApplicationInsights/) signale qu’un seul nœud, quelle que soit le nombre de hello d’hôtes d’application réelle. 
  * Notez que si votre application utilise la valeur personnalisé tooa du roleInstance tooset hello SDK, par défaut cette même valeur sera utilisé le nombre de hello toodetermine de nœuds. 
  * Si vous utilisez une nouvelle version du Kit de développement logiciel avec une application qui est exécutée à partir d’appareils mobiles ou des ordinateurs clients, il est possible que nombre hello de nœuds peut retourner un nombre qui est très volumineux (hello grand nombre d’ordinateurs clients ou des périphériques mobiles). 

### <a name="multi-step-web-tests"></a>Tests web à plusieurs étapes

Des frais supplémentaires sont facturés pour les [tests web à plusieurs étapes](app-insights-monitor-web-app-availability.md#multi-step-web-tests). Il s’agit de tests tooweb qui effectuent une séquence d’actions. 

Aucun frais supplémentaire n'est facturé pour les tests Ping sur une seule page. Les données de télémétrie des tests Ping et des tests à plusieurs étapes sont facturées, ainsi que d’autres données de télémétrie de votre application.
 
## <a name="operations-management-suite-subscription-entitlement"></a>Droit d’abonnement à Operations Management Suite

En tant que [a récemment annoncé](https://blogs.technet.microsoft.com/msoms/2017/05/19/azure-application-insights-enterprise-as-part-of-operations-management-suite-subscription/), les clients qui achètent Microsoft Operations Management Suite E1 et E2 sont en mesure de tooget Application Insights entreprise comme un composant supplémentaire sans coût supplémentaire. Plus précisément, chaque unité de Operations Management Suite E1 et E2 inclut un nœud de too1 droit du plan d’entreprise hello d’Application Insights. Comme indiqué ci-dessus, chaque nœud de l’Application Insights inclut Mo too200 de données ingérées par jour (distinct à partir de la réception de données Analytique de journal), avec conservation des données de 90 jours sans coût supplémentaire. 

> [!NOTE]
> tooensure que vous obtenez ce droit, vous devez avoir vos ressources d’Application Insights dans hello entreprise plan de tarification. Ce droit s’applique uniquement en tant que nœuds, les ressources Application Insights dans le plan de base hello ne seront pas en bénéficier. Notez que ce droit ne sera pas visible sur hello estimé des coûts affichés sur les fonctions hello + tarification panneau. 
>
 
## <a name="review-pricing-plans-and-estimate-costs"></a>Passer en revue les plans de tarification et estimer les coûts

Applicaition Insights rend hello toounderstand facile tarifications disponibles et le coûts sont probablement de hello reposer sur des modèles d’utilisation récente. Commencez par ouvrir de hello **fonctionnalités + tarification** panneau Bonjour ressource Application Insights Bonjour portail Azure :

![Choisissez Tarification.](./media/app-insights-pricing/01-pricing.png)

**a.** Passez en revue votre volume de données pour le mois de hello. Cela inclut toutes les données de salutation reçu et conservées (après n’importe quel [échantillonnage](app-insights-sampling.md) à partir de votre serveur et les applications clientes et des tests de disponibilité.

**b.** Les [tests web multiétapes](app-insights-monitor-web-app-availability.md#multi-step-web-tests) font l’objet d’une facturation distincte. (Cela n’inclut pas les tests de disponibilité simple, qui sont inclus dans les frais de volume de données hello).

**c.** Activer le plan d’entreprise hello.

**d.** Parcourez le volume de données toodata gestion options tooview pourquoi le mois dernier, définir une limite quotidienne ou valeur d’échantillonnage d’ingestion.

Des frais application Insights sont ajoutés tooyour facture Azure. Vous pouvez voir les détails de votre Azure facturer sur hello section facturation Hello portail Azure ou Bonjour [Azure Billing Portal](https://account.windowsazure.com/Subscriptions). 

![Dans le menu latéral de hello, choisissez facturation.](./media/app-insights-pricing/02-billing.png)

## <a name="data-rate"></a>Débit de données
Il existe trois façons les Bonjour vous envoyer des données de volume est limité :

* **Échantillonnage :** ce mécanisme peut servir hello réduire de télémétrie envoyé à partir de vos applications serveur et client, avec des métriques de distorsion minimale. Il s’agit de hello principal outil quantité de hello tootune de données. Découvrez plus en détail les [fonctionnalités d’échantillonnage](app-insights-sampling.md). 
* **Limite quotidienne :** quand la création d’une ressource Application Insights à partir de hello portail Azure cela a too500 Go/jour. Hello par défaut lors de la création d’une ressource Application Insights à partir de Visual Studio, est petit (seul 32,3 Mo/jour), qui est destinée uniquement toofaciliate de test. Dans ce cas, il est prévu que l’utilisateur hello déclenchera la limite quotidienne de hello avant de déployer l’application hello en production. capacité maximale de Hello est de 500 Go/jour, sauf si vous avez demandé un maximum supérieure pour une application de trafic élevé. Soyez prudent lorsque vous définissez la limite quotidienne de hello, comme votre intention doit être **jamais toohit hello limite quotidienne**, car vous allez ensuite de perdre des données pour reste hello du jour de hello et être toomonitor Impossible de votre application. toochange il, utilisez hello quotidienne volume cap panneau, lié à partir du Panneau de gestion des volumes de données hello (voir ci-dessous). Notez que certains types d’abonnement disposent d’un crédit qui ne peut pas être utilisé pour Application Insights. Si les abonnement hello de dépense limiter, hello quotidiennement panneau d’extrémité de fin n’a instructions comment tooremove elle et activer hello quotidienne toobe cap déclenché au-delà 32,3 Mo par jour.  
* **La limitation :** cette limite hello données taux too32 k les événements par seconde, moyenne calculée sur 1 minute. 


*Que se passe-t-il si mon application dépasse le taux de limitation de hello ?*

* volume Hello de données qui envoie de votre application est évaluée chaque minute. Si elle dépasse le taux par seconde de hello moyenne par minute de hello, serveur de hello refuse des demandes. Hello SDK met en mémoire tampon des données de hello et tente ensuite de tooresend, en répartissant un brusque sur plusieurs minutes. Si votre application envoie régulièrement des données au niveau au-dessus hello taux de limitation, certaines données sont supprimées. (hello ASP.NET, Java et kits de développement logiciel JavaScript essaient tooresend de cette manière ; autres kits de développement logiciel peuvent simplement les données de liste limitée). En cas de limitation, vous en êtes informé par un avertissement.

*Comment déterminer la quantité de données envoyées par mon application ?*

* Ouvrez hello **gestion des volumes de données** graphique du volume données quotidiennes panneau toosee hello. 
* Ou dans Metrics Explorer, ajoutez un nouveau graphique et sélectionnez la mesure **Volume du point de données** . Basculez sur le regroupement et regroupez par **Type de données**.

## <a name="tooreduce-your-data-rate"></a>tooreduce votre taux de données
Voici quelques opérations que vous pouvez effectuer tooreduce votre volume de données :

* Utilisez l’ [échantillonnage](app-insights-sampling.md). Cette technologie réduit débit sans inclinaison vos métriques et sans interruption de toonavigate de capacité hello entre les éléments associés dans la recherche. Dans les applications serveurs, elle s’applique automatiquement.
* [Limiter le nombre de hello des appels Ajax qui peuvent être signalées](app-insights-javascript.md#detailed-configuration) dans chaque affichage de page ou le commutateur hors tension Ajax reporting.
* Désactivez les modules de collecte dont vous n'avez pas besoin en [modifiant ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Par exemple, vous pouvez décider que les compteurs de performances ou les données de dépendance ne sont pas essentiels.
* Fractionner vos clés d’instrumentation tooseparate télémétrie. 
* Procédez à la pré-agrégation des métriques. Si vous avez placé les appels tooTrackMetric dans votre application, vous pouvez réduire le trafic à l’aide de la surcharge qui accepte le calcul de la moyenne de hello et l’écart type d’un lot de mesures hello. Une autre possibilité consiste à utiliser un [package de pré-agrégation](https://www.myget.org/gallery/applicationinsights-sdk-labs).

## <a name="managing-hello-maximum-daily-data-volume"></a>La gestion du volume de données quotidienne maximale hello

Vous pouvez utiliser hello quotidienne volume cap toolimit hello données collectées, mais si embout de hello est remplie, il entraîne une perte de toutes les telemetery envoyés à partir de votre application pour le reste de hello du jour de hello. Il s’agit de **déconseillé** toohave votre limite quotidienne hello application toohit depuis que vous avez sont tootrack impossible la santé hello et les performances de votre application après qu’il est atteint. 

Au lieu de cela, utilisez [échantillonnage](app-insights-sampling.md) tootune hello volume toohello niveau de données vous comme et utiliser la limite quotidienne de hello uniquement en tant que « dernier recours » dans le cas où votre application commence à envoyer de façon inattendue beaucoup plus grand nombre de telemetery. 

toochange la limite quotidienne de hello, Bonjour section de configuration de votre ressource Insihgts de l’Application, cliquez sur **gestion des volumes de données** puis **limite quotidienne**.

![Ajustement de limite de volume de données de télémétrie quotidienne hello](./media/app-insights-pricing/daily-cap.png) 

## <a name="sampling"></a>échantillonnage
[Échantillonnage](app-insights-sampling.md) est une méthode de réduction du taux de hello auquel télémétrie est envoyée au tooyour application, tandis qu’en conservant hello capacité toofind les événements liés au cours des recherches de diagnostic, et conserve toujours événement correcte compte. 

L’échantillonnage est un moyen efficace tooreduce frais et rester au sein de votre quota mensuel. Hello algorithme d’échantillonnage conserve les éléments de télémétrie, afin que, par exemple, lorsque vous utilisez la recherche, vous pouvez rechercher les demande hello liées exception particulière de tooa. algorithme de Hello conserve également le nombre correct, afin que vous voyez hello des valeurs correctes dans l’Explorateur de métrique pour le taux de demandes, les taux d’exception et les autres compteurs.

Il existe plusieurs formes d’échantillonnage.

* [Échantillonnage Adaptive](app-insights-sampling.md) est par défaut de hello pour hello Kit de développement ASP.NET, qui ajuste automatiquement le volume toohello de télémétrie envoie de votre application. Il s’exécute automatiquement dans hello SDK dans votre application web, afin que le trafic de télémétrie hello sur le réseau de hello est réduit. 
* *Échantillonnage de l’ingestion* est une alternative qui fonctionne au niveau du point de hello où télémétrie à partir de votre application entre le service d’Application Insights hello. Il n’affecte pas volume hello de télémétrie envoyé à partir de votre application, mais elle réduit le volume hello conservée par le service de hello. Vous pouvez l’utiliser quota de hello tooreduce utilisé par les données de télémétrie à partir de navigateurs et d’autres kits de développement logiciel.

réception tooset d’échantillonnage, définir le contrôle dans le panneau de tarification hello hello :

![Hello Quota et de tarification panneau, cliquez sur la vignette d’exemples hello et sélectionnez une fraction de l’échantillonnage.](./media/app-insights-pricing/04.png)

> [!WARNING]
> panneau d’échantillonnage des données Hello contrôle uniquement la valeur hello d’échantillonnage de l’ingestion. Il ne reflète le taux d’échantillonnage hello appliquée par hello Application Insights SDK dans votre application. Si les données de télémétrie entrants hello a déjà été échantillonnées à hello SDK, l’échantillonnage de réception n’est pas appliqué.
> 

hello toodiscover réel d’échantillonnage taux, quel que soit l’où il a été appliqué, utilisez un [les requête Analytique](app-insights-analytics.md) comme celui-ci :

    requests | where timestamp > ago(1d)
    | summarize 100/avg(itemCount) by bin(timestamp, 1h) 
    | render areachart 

Chaque enregistrement, conservé `itemCount` indique nombre hello d’origine enregistrements qu’elle représente, too1 égal + nombre de hello d’anciens enregistrements rejetés. 


## <a name="automation"></a>Automatisation

Vous pouvez écrire un plan de prix script tooset hello, à l’aide de la gestion des ressources Azure. [Découvrez comment](app-insights-powershell.md#price).

## <a name="limits-summary"></a>Synthèse des limites
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

## <a name="next-steps"></a>Étapes suivantes

* [Échantillonnage](app-insights-sampling.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[start]: app-insights-overview.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/

