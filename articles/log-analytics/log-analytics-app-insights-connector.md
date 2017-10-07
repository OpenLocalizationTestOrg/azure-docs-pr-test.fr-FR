---
title: "aaaView les données d’application Azure Application Insights | Documents Microsoft"
description: "Vous pouvez utiliser la solution Application Insights Connector hello toodiagnose les problèmes de performances et comprendre ce que les utilisateurs à faire avec votre application quand analysés avec Application Insights."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Solution Application Insights Connector (préversion) dans Operations Management Suite (OMS)

![Symbole Application Insights](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

Hello solution du connecteur d’Applications Insights vous permet de diagnostiquer les problèmes de performances et de comprendre ce que les utilisateurs faire avec votre application quand il est analysé avec [Application Insights](../application-insights/app-insights-overview.md). Vues de hello même télémétrie d’application que les développeurs voir dans Application Insights sont disponibles dans OMS. Toutefois, lorsque vous intégrez vos applications Application Insights à OMS, la visibilité de vos applications augmente lorsque les données de fonctionnement et d’application se trouvent au même emplacement. Avoir hello même vues vous aide à toocollaborate avec vos développeurs d’application. les vues communes Hello peuvent aider à réduire hello temps toodetect et résoudre les problèmes application et plate-forme.

Lorsque vous utilisez la solution de hello, vous pouvez :

- Consulter toutes vos applications Application Insights en un lieu unique, même si elles se trouvent dans différents abonnements Azure
- Mettre en corrélation les données d’infrastructure et les données d’application
- Visualiser les données d’application avec des perspectives dans la recherche dans les journaux
- Tableau croisé dynamique à partir de journal Analytique données tooyour Application Insights application Bonjour OMS et les portails Azure

## <a name="connected-sources"></a>Sources connectées

Contrairement à la plupart des autres solutions d’Analytique de journal, les données n’est pas collectées pour hello Application Insights Connector par les agents. Toutes les données utilisées par la solution de hello proviennent directement d’Azure.

| Source connectée | Pris en charge | Description |
| --- | --- | --- |
| [Agents Windows](log-analytics-windows-agents.md) | Non | solution de Hello ne collecte pas les informations des agents de Windows. |
| [Agents Linux](log-analytics-linux-agents.md) | Non | solution de Hello ne collecte pas les informations des agents de Linux. |
| [Groupe d’administration SCOM](log-analytics-om-agents.md) | Non | solution de Hello ne collecte pas les informations des agents dans un groupe d’administration SCOM connecté. |
| [Compte Azure Storage](log-analytics-azure-storage.md) | Non | solution de Hello ne contient pas les informations de collection à partir du stockage Azure. |

## <a name="prerequisites"></a>Composants requis

- tooaccess les informations Application Insights Connector, vous devez disposer un abonnement Azure
- Vous devez disposer d’au moins une ressource Application Insights configurée.
- Vous devez être propriétaire de hello ou un collaborateur de hello ressource Application Insights.

## <a name="configuration"></a>Configuration

1. Activer la solution Azure Web Apps Analytique hello hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) ou à l’aide de hello est décrite dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
2. Dans le portail OMS : hello, cliquez sur **paramètres** &gt; **données** &gt; **Application Insights**.
3. Sous **Sélectionner un abonnement**, sélectionnez un abonnement qui contient des ressources Application Insights, puis sous **Nom de l’application**, sélectionnez une ou plusieurs applications.
4. Cliquez sur **Enregistrer**.

Dans environ 30 minutes, les données deviennent disponibles et hello Application Insights vignette est mise à jour avec les données, comme hello suivant image :

![Vignette Application Insights](./media/log-analytics-app-insights-connector/app-insights-tile.png)

Autres tookeep points à l’esprit :

- Vous pouvez lier uniquement l’espace de travail OMS Application Insights applications tooone.
- Vous ne pouvez lier [ressources Standard ou Premium Application Insights](https://azure.microsoft.com/pricing/details/application-insights) tooOMS Analytique de journal. Toutefois, vous pouvez utiliser niveau gratuit de hello d’Analytique de journal.

## <a name="management-packs"></a>Packs d’administration

Cette solution n’installe aucun pack d’administration dans les groupes d’administration connectés.

## <a name="use-hello-solution"></a>Utilisez la solution hello

Hello sections suivantes décrivent comment vous pouvez utiliser des panneaux hello illustré tooview de tableau de bord Application Insights hello et interagir avec les données à partir de vos applications.

### <a name="view-application-insights-connector-information"></a>Consulter les informations Application Insights Connector

Cliquez sur hello **Application Insights** vignette tooopen hello **Application Insights** hello toosee de tableau de bord suivant lames.

![Tableau de bord Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Tableau de bord Application Insights](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

tableau de bord Hello inclut les panneaux hello indiqués dans la table de hello. Chaque panneau répertorie les articles too10 mise en correspondance que les critères du panneau pour hello spécifié plage étendue et d’heure. Vous pouvez exécuter une recherche de journal qui retourne tous les enregistrements lorsque vous cliquez sur **afficher tous les** bas hello du Panneau de hello ou lorsque vous cliquez sur en-tête de panneau hello.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **Colonne** | **Description** |
| --- | --- |
| Applications - Nombre d’applications | Affiche le nombre hello d’applications dans les ressources d’Application. Également, application de listes de noms et pour chacune, hello le nombre d’enregistrements de l’application. Cliquez sur toorun de nombre hello pour une recherche de journal<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  Cliquez sur une toorun de nom d’application pour l’application hello qui affiche des enregistrements d’applications par hôte, les enregistrements par type de données de télémétrie et toutes les données par type (hello selon la veille), une recherche de journal. |
| Volume de données – Hôtes envoyant des données | Affiche le nombre hello d’hôtes d’ordinateur qui envoient des données. Répertorie également les ordinateurs hôtes et le nombre d’enregistrements pour chaque hôte. Cliquez sur toorun de nombre hello pour une recherche de journal<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> Cliquez sur un toorun de nom d’ordinateur une recherche de journal pour l’hôte hello qui affiche des enregistrements d’applications par hôte, les enregistrements par type de données de télémétrie et toutes les données par type (hello selon la veille). |
| Disponibilité – Résultats du test web | Affiche un graphique en anneau pour les résultats du test web, spécifiant si le test a réussi ou échoué. Cliquez sur hello graphique toorun une recherche de journal pour<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> Résultats indiquent le nombre de hello de passes et les échecs de tous les tests. Il affiche toutes les applications Web avec le trafic de la dernière minute de hello. Cliquez sur une tooview de nom d’application à une recherche de journal présentant les détails des tests web ayant échoué. |
| Requêtes de serveur – Requêtes par heure | Affiche un graphique en courbes de hello des demandes de serveur par heure pour différentes applications. Placez le curseur sur une ligne dans les applications hello graphique toosee hello 3 premiers à recevoir des demandes pour un point dans le temps. Montre également une liste d’applications hello reçoit des demandes et nombre hello de demandes pour la période de hello sélectionné. <br><br>Cliquez sur hello graphique toorun une recherche de journal pour <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> qui affiche un graphique en courbes plus détaillé de hello les requêtes de serveur par heure pour différentes applications. <br><br> Cliquez sur une application hello liste toorun une recherche de journal pour <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> qui affiche une liste des demandes, des graphiques pour les demandes sur la durée de temps et de la demande et une liste de demande de codes de réponse.   |
| Échecs – Requêtes ayant échoué par heure | Affiche un graphique en courbes des requêtes d’application ayant échoué par heure. Pointez sur hello graphique toosee hello 3 applications les plus importantes avec des demandes ayant échoué pour un point dans le temps. Montre également une liste d’applications avec un nombre de hello de demandes ayant échoué pour chacun. Cliquez sur hello graphique toorun une recherche de journal pour <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> qui affiche un graphique en courbes plu de demandes d’application qui a échoué. <br><br>Cliquez sur un élément dans hello liste toorun une recherche de journal pour <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> que montre demandes ayant échoué, les graphiques de demandes ayant échoué sur la durée de temps et de la demande et une liste des codes de réponse des demandes ayant échoué. |
| Exceptions – Exceptions par heure | Affiche un graphique en courbes des exceptions par heure. Pointez sur hello graphique toosee hello 3 applications les plus importantes avec des exceptions pour un point dans le temps. Montre également une liste d’applications avec numéro hello d’exceptions pour chacun. Cliquez sur hello graphique toorun une recherche de journal pour <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> qui affiche un graphique de lien plus détaillé des exceptions. <br><br>Cliquez sur un élément dans hello liste toorun une recherche de journal pour <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> qui affiche la liste des exceptions, des graphiques pour les exceptions par le biais des demandes ayant échouées et de temps et une liste des types d’exception.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>Afficher la perspective d’Application Insights hello avec la recherche de journal

Lorsque vous cliquez sur n’importe quel élément dans le tableau de bord hello, vous voyez une perspective d’Application Insights indiquée dans la recherche. perspective de Hello fournit une visualisation étendue, selon le type de données de télémétrie de hello sélectionné. Le contenu visualisé change donc en fonction du type de données de télémétrie.

Lorsque vous cliquez sur n’importe où dans le panneau des Applications hello, vous voyez par défaut de hello **Applications** perspective.

![Perspective Applications d’Application Insights](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

perspective de Hello montre une vue d’ensemble de l’application hello que vous avez sélectionné.

Hello **disponibilité** panneau affiche une perspective différente où vous pouvez consulter les résultats des tests web et des demandes ayant échoué connexes.

![Perspective Disponibilité d’Application Insights](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

Lorsque vous cliquez sur n’importe où dans hello **les demandes de serveur** ou **échecs** panneaux, perspective hello composants modifier toogive vous une visualisation qui liées toorequests.

![Panneau Échecs d’Application Insights](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

Lorsque vous cliquez sur n’importe où dans hello **Exceptions** panneau, vous voyez une visualisation personnalisé tooexceptions.

![Panneau Exceptions d’Application Insights](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

Indépendamment de si vous cliquez sur un élément hello **Application Insights Connector** tableau de bord, dans hello **recherche** page proprement dit, toute requête retournant des données d’Application Insights montrent hello Perspective d’application Insights. Par exemple, si vous affichez les données d’Application Insights, un **&#42;** requête montre également l’onglet de perspective hello comme hello suivant image :

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

Composants du point de vue sont mises à jour en fonction de la requête de recherche hello. Cela signifie que vous pouvez filtrer les résultats de hello à l’aide de n’importe quel champ de recherche donne hello de capacité toosee hello des données à partir de :

- Toutes vos applications
- Une seule application sélectionnée
- Un groupe d’applications

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>Application tooan Bonjour Azure portal de tableau croisé dynamique

Panneaux de connecteur Insights d’application est conçu tooenable toohello de toopivot vous sélectionné Application Insights application *lorsque vous utilisez le portail OMS est hello*. Vous pouvez utiliser la solution de hello comme plate-forme analyse de haut niveau qui vous permet de résoudre les problèmes d’une application. Lorsque vous voyez un problème potentiel dans aucun de vos applications connectées, vous pouvez soit explorez dans les recherches OMS, ou vous pouvez directement toohello Application Insights application pivot.

toopivot, cliquez sur le bouton de sélection hello (**...** ) qui s’affiche à la fin hello de chaque ligne, puis sélectionnez **ouvert dans Application Insights**.

>[!NOTE]
>**Ouvrir dans Application Insights** n’est pas disponible dans hello portail Azure.

![Ouvrir dans Application Insights](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>Données corrigées par l’exemple

Application Insights fournit  *[d’échantillonnage de correction](../application-insights/app-insights-sampling.md)*  toohelp réduire le trafic de télémétrie. Lorsque vous activez l’échantillonnage sur votre application Application Insights, vous obtenez un nombre limité d’entrées stockées à la fois dans Application Insights et dans OMS. Alors que la cohérence des données est préservée dans hello **Application Insights Connector** page et des perspectives, vous devez corriger manuellement les données échantillonnées pour vos requêtes personnalisées.

Voici un exemple de correction par échantillonnage dans une requête de recherche dans les journaux :

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

Hello **échantillonnées un nombre** champ est présent dans toutes les entrées et montre hello le nombre de points de données hello entrée représente. Si vous activez l’échantillonnage pour votre application Application Insights, la valeur du champ **Sampled Count** (Nombre d’éléments échantillonnés) est supérieure à 1. toocount hello nombre d’écritures générés par votre application, hello de somme **échantillonnées un nombre** champs.

Échantillonnage affecte uniquement hello nombre total d’entrées générés par votre application. Vous n’avez pas besoin d’échantillonnage de toocorrect pour les champs de mesure tels que **RequestDuration** ou **AvailabilityDuration** , car ces champs affichent moyenne hello pour les entrées représentées.

## <a name="input-data"></a>Données d’entrée

solution de Hello reçoit hello suivant des types de données de télémétrie à partir de vos applications Application Insights connectées :

- Disponibilité
- Exceptions
- Requests
- Vues de page – pour votre espace de travail de tooreceive des consultations de page, vous devez configurer votre toocollect applications ces informations. Pour plus d’informations, voir [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views).
- Des événements personnalisés pour votre espace de travail tooreceive des événements personnalisés, vous devez configurer ces informations à votre toocollect d’applications. Pour plus d’informations, voir [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent).

OMS reçoit les données en provenance d’Application Insights dès qu’elles sont disponibles.

## <a name="output-data"></a>Données de sortie

Un enregistrement associé au *type* *ApplicationInsights* est créé pour chaque type de données d’entrée. ApplicationInsights enregistrements ont les propriétés affichées dans les sections suivantes de hello :

### <a name="generic-fields"></a>Champs génériques

| Propriété | Description |
| --- | --- |
| Type | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Heure d’enregistrement de hello |
| ApplicationId | Clé d’instrumentation de l’application d’Application Insights hello |
| ApplicationName | Nom de l’application d’Application Insights hello |
| RoleInstance | ID de l’hôte du serveur |
| DeviceType | Appareil client |
| ScreenResolution |   |
| Continent | Continent où hello émane |
| Pays | Pays où hello émane |
| Province | Province, l’état ou les paramètres régionaux où hello demande d’origine |
| City | Ville ou ville d’origine de la demande de hello |
| isSynthetic | Indique si la demande de hello a été créé par un utilisateur ou par une méthode automatisée. True = générée par l’utilisateur, ou false = méthode automatisée |
| SamplingRate | Pourcentage de télémétrie généré par hello SDK qui est envoyé à tooportal. Plage 0.0-100.0. |
| SampledCount | 100/(SamplingRate). Par exemple, 4 =&gt; 25 % |
| IsAuthenticated | True ou false |
| OperationID | Éléments qui ont le même ID d’opération sont affichés en tant qu’éléments associés dans le portail de hello de hello. ID de demande généralement hello |
| ParentOperationID | ID d’opération de parent hello |
| Nom d'opération |   |
| SessionId | GUID toouniquely identifier la session hello où la demande de hello a été créé |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>Champs spécifiques à la disponibilité

| Propriété | Description |
| --- | --- |
| TelemetryType | Availability |
| AvailabilityTestName | Nom du test web de hello |
| AvailabilityRunLocation | Source géographique de la requête http |
| AvailabilityResult | Indique le résultat de réussite hello du test web de hello |
| AvailabilityMessage | message de type Hello attaché test web de toohello |
| AvailabilityCount | 100/(Sampling Rate). Par exemple, 4 =&gt; 25 % |
| DataSizeMetricValue | 1.0 ou 0.0 |
| DataSizeMetricCount | 100/(Sampling Rate). Par exemple, 4 =&gt; 25 % |
| AvailabilityDuration | Durée, en millisecondes, de la durée du test web hello |
| AvailabilityDurationCount | 100/(Sampling Rate). Par exemple, 4 =&gt; 25 % |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | GUID unique pour le test web de hello |
| AvailabilityTimestamp | Horodatage précis de test de disponibilité hello |
| AvailabilityDurationMin | Pour les enregistrements échantillonnées, ce champ affiche la durée du test hello web minimale (en millisecondes) pour les points de données hello représenté |
| AvailabilityDurationMax | Pour les enregistrements échantillonnées, ce champ affiche la durée du test hello web maximal (en millisecondes) pour les points de données hello représenté |
| AvailabilityDurationStdDev | Pour les enregistrements échantillonnées, ce champ affiche écart hello entre toutes les durées de test web (en millisecondes) pour les points de données hello représenté |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>Champs spécifiques à l’exception

| Type | ApplicationInsights |
| --- | --- |
| TelemetryType | Exception |
| ExceptionType | Type d’exception de hello |
| ExceptionMethod | méthode Hello qui crée l’exception de hello |
| ExceptionAssembly | Assembly inclut les framework hello et la version, ainsi que le jeton de clé publique hello |
| ExceptionGroup | Type d’exception de hello |
| ExceptionHandledAt | Indique le niveau de hello géré hello exception |
| ExceptionCount | 100/(Sampling Rate). Par exemple, 4 =&gt; 25 % |
| ExceptionMessage | Message d’exception de hello |
| ExceptionStack | Complet de la pile d’exception de hello |
| ExceptionHasStack | True, si l’exception possède une pile |



### <a name="request-specific-fields"></a>Champs spécifiques à la requête

| Propriété | Description |
| --- | --- |
| Type | ApplicationInsights |
| TelemetryType | Demande |
| ResponseCode | Tooclient d’envoi de réponse HTTP |
| RequestSuccess | Indique la réussite ou l’échec. True ou false. |
| RequestID | Identifier les ID toouniquely hello de demande |
| RequestName | GET/POST + base d’URL |
| RequestDuration | Durée, en secondes, de la durée de la demande hello |
| URL | URL de demande hello sans hôte |
| Host | Hôte du serveur web |
| URLBase | URL complète de la demande de hello |
| ApplicationProtocol | Type de protocole utilisé par l’application hello |
| RequestCount | 100/(Sampling Rate). Par exemple, 4 =&gt; 25 % |
| RequestDurationCount | 100/(Sampling Rate). Par exemple, 4 =&gt; 25 % |
| RequestDurationMin | Pour les enregistrements échantillonnées, ce champ affiche hello minimale durée (en millisecondes) pour les points de données hello représenté. |
| RequestDurationMax | Pour les enregistrements échantillonnées, ce champ affiche hello maximale durée (en millisecondes) pour les points de données hello représenté |
| RequestDurationStdDev | Pour les enregistrements échantillonnées, ce champ affiche écart hello entre toutes les durées de demande (en millisecondes) pour les points de données hello représenté |

## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux

Cette solution n’a pas d’un ensemble d’exemples les recherches de journal affichées dans le tableau de bord hello. Toutefois, les requêtes de recherche de journal exemple avec les descriptions sont affichés dans hello [les informations de vue Application Insights Connector](#view-application-insights-connector-information) section.

## <a name="next-steps"></a>Étapes suivantes

- Utilisez [recherche de journal](log-analytics-log-searches.md) tooview des informations détaillées sur vos applications Application Insights.
