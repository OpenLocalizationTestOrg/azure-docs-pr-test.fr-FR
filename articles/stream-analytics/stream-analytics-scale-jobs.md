---
title: "débit de tooincrease travaux aaaScale flux Analytique | Documents Microsoft"
description: "Découvrez comment tooscale les travaux de flux de données Analytique par la configuration de partitions d’entrée, le paramétrage de la définition de requête hello et définition de la tâche unités de diffusion en continu."
keywords: "diffusion en continu de données, traitement de données de diffusion en continu, régler l’analyse"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a>Débit en échelle Analytique de flux de données Azure travaux tooincrease flux le traitement des données
Cet article vous explique comment tootune un Analytique de flux de requête tooincrease le débit pour les travaux de l’Analytique de diffusion en continu. Vous apprendrez comment tooscale Analytique de flux de travaux en configurant les partitions d’entrée, définition de la requête analytique de hello paramétrage et du calcul et la définition de la tâche *unités de diffusion en continu* (SUs). 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a>Quelles sont les parties hello d’une tâche de flux de données Analytique ?
La définition d’une tâche Stream Analytics se compose d’entrées, d’une requête et d’une sortie. Les entrées sont où le travail de hello lit les flux de données de hello à partir de. flux d’entrée des données hello tootransform utilisé est Hello requête et sortie de la hello est où le travail de hello envoie les résultats de la tâche hello pour.  

Un travail nécessite au moins une source d’entrée pour la diffusion de données en continu. Hello source d’entrée de flux de données peut être stockée dans un concentrateur d’événements Azure ou dans le stockage d’objets blob Azure. Pour plus d’informations, consultez [tooAzure de présentation des flux de données Analytique](stream-analytics-introduction.md) et [prise en main Azure flux Analytique](stream-analytics-real-time-fraud-detection.md).

## <a name="partitions-in-event-hubs-and-azure-storage"></a>Partitions dans les concentrateurs d’événements et le stockage Azure
Mise à l’échelle d’une tâche de flux de données Analytique bénéficie de partitions Bonjour d’entrée ou sortie. Le partitionnement vous permet de répartir les données en sous-ensembles basés sur une clé de partition. Un processus qui consomme des données hello (par exemple, une tâche Analytique de diffusion en continu) peut consommer et écrire des différentes partitions en parallèle, ce qui augmente le débit. Lorsque vous utilisez Stream Analytics, vous pouvez tirer parti du partitionnement dans les concentrateurs d’événements et dans le stockage d’objets blob. 

Pour plus d’informations sur les partitions, consultez hello suivant des articles :

* [Vue d’ensemble des fonctionnalités des concentrateurs d’événements](../event-hubs/event-hubs-features.md#partitions)
* [Partitionnement des données](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a>Unités de diffusion en continu (SU)
Diffusion en continu des ressources de hello représentent des unités (SUs) et calcul d’alimentation qui sont requis dans l’ordre de tooexecute un travail Azure Stream Analytique. SUs fournissent un événement relatif hello toodescribe moyen en fonction de la mesure du processeur, mémoire, la capacité de traitement et lire et écrire des taux. Chaque appel à SU correspond tooroughly débit de 1 Mo par seconde. 

En choisissant SUs combien sont requis pour une tâche particulière dépend de la configuration de partitions hello pour les entrées de hello et de requête hello définis pour le travail de hello. Vous pouvez sélectionner des quotas tooyour SUS d’une tâche. Par défaut, chaque abonnement Azure a un quota de configuration SUs too50 pour tous les travaux d’analytique hello dans une région spécifique. tooincrease SUs pour vos abonnements au-delà de ce quota, contactez [Support technique de Microsoft](http://support.microsoft.com). Valeurs valides pour les unités SU par travail : 1, 3, 6 et au-dessus par incréments de 6.

## <a name="embarrassingly-parallel-jobs"></a>Travaux massivement parallèles
Un *embarrassingly parallel* travail est scénario plus évolutive de hello, nous disposons d’Analytique de flux de données Azure. Il connecte une partition d’instance d’entrée tooone de hello de partition de tooone hello requête de sortie de hello. Ce parallélisme a hello suivant les exigences :

1. Si votre logique de requête dépend hello même clé en cours de traitement par hello même instance de requête, vous devez vous assurer que les événements hello accédez toohello même partition de votre entrée. Pour les concentrateurs d’événements, cela signifie que les données d’événement hello doivent avoir hello **PartitionKey** ensemble de valeurs. Par ailleurs, vous pouvez utiliser des expéditeurs partitionnés. Pour le stockage d’objets blob, cela signifie que les événements de hello sont envoyés toohello même dossier de la partition. Si votre logique de requête ne nécessite pas de hello même clé toobe traité par hello même instance de requête, vous pouvez ignorer cette exigence. Un exemple de cette logique serait une requête simple du type select/project/filter.  

2. Une fois que les données de salutation sont disposées côté hello d’entrée, il se peut que vous devez vous assurer que votre requête est partitionnée. Vous devez toouse **Partition By** dans toutes les étapes de hello. Plusieurs étapes sont autorisés, mais ils doivent être partitionnées par hello même clé. Actuellement, hello clé de partitionnement doit être défini trop**PartitionId** par ordre de hello toobe de travail entièrement parallèle.  

3. Actuellement, seuls les concentrateurs d’événements et le stockage d’objets blob prennent en charge les sorties partitionnées. Pour la sortie de concentrateur d’événements, vous devez configurer toobe clé de partition hello **PartitionId**. Pour la sortie de stockage d’objets blob, vous n’avez toodo quoi que ce soit.  

4. nombre de Hello de partitions d’entrée doit être égal nombre hello de partitions de sortie. Actuellement, la sortie du stockage d’objets blob ne prend pas en charge les partitions, Mais c’est OK, parce qu’elle hérite hello schéma de requête en amont de hello de partitionnement. Voici des exemples de valeurs de partition qui permettent la création d’un travail entièrement parallèle :  

   * 8 partitions d’entrée de concentrateur Event Hub et 8 partitions de sortie de concentrateur Event Hub
   * 8 partitions d’entrée de concentrateur Event Hub et une sortie de stockage d’objets blob  
   * 8 partitions d’entrée de stockage d’objets blob et une sortie de stockage d’objets blob  
   * 8 partitions d’entrée de stockage d’objets blob et 8 partitions de sortie de concentrateur Event Hub  

Hello sections suivantes présentent des exemples de scénarios qui sont excessivement parallèles.

### <a name="simple-query"></a>Requête simple

* Entrée : concentrateur Event Hub avec 8 partitions
* Sortie : concentrateur Event Hub avec 8 partitions

Requête :

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

Cette requête est un filtre simple. Par conséquent, nous n’avez pas besoin tooworry sur le partitionnement d’entrée de hello est envoyée toohello concentrateur d’événements. Notez cette requête hello inclut **Partition par PartitionId**, donc il répond à un besoin #2 précédemment. Pour une sortie hello, nous avons besoin de sortie du hub d’événements tooconfigure hello dans hello travail toohave hello partition jeu de clés trop**PartitionId**. Une dernière vérification est toomake assurer que le nombre hello de partitions d’entrée est nombre égal toohello de partitions de sortie.

### <a name="query-with-a-grouping-key"></a>Requête avec clé de regroupement

* Entrée : concentrateur Event Hub avec 8 partitions
* Sortie : stockage d’objets blob

Requête :

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Cette requête comporte une clé de regroupement. Par conséquent, hello même clé besoins toobe traité par hello même requête d’instance, ce qui signifie que les événements doivent être envoyés toohello concentrateur d’événements de manière partitionnée. Mais quelle clé convient-il d’utiliser ? **PartitionId** est un concept de logique de travail. clé Hello nous intéressent réellement est **TollBoothId**, donc hello **PartitionKey** valeur hello des données d’événement doit être **TollBoothId**. Cela, nous dans les requêtes hello en définissant **Partition By** trop**PartitionId**. Étant donné que la sortie de hello est le stockage d’objets blob, nous n’avez pas besoin tooworry sur la configuration d’une valeur de clé de partition, conformément à la spécification #4.

### <a name="multi-step-query-with-a-grouping-key"></a>Requête à plusieurs étapes avec clé de regroupement
* Entrée : concentrateur Event Hub avec 8 partitions
* Sortie : instance de concentrateur Event Hub avec 8 partitions

Requête :

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Cette requête comporte une clé de regroupement, par conséquent, hello même clé besoins toobe traité par hello même instance de requête. Nous pouvons utiliser hello même stratégie dans l’exemple précédent de hello. Dans ce cas, la requête de hello comprend plusieurs étapes. Chaque étape inclut-elle **Partition By PartitionId** ? Oui, afin de la requête de hello répond à un besoin #3. Pour une sortie hello, nous devons trop clé de partition hello tooset**PartitionId**, comme indiqué précédemment. Nous pouvons également voir qu’il a hello même nombre de partitions en tant qu’entrée de hello.

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a>Exemples de scénarios qui n’impliquent *pas* un parallélisme massif

Dans la section précédente de hello, nous vous avons montré certains scénarios excessivement parallèles. Dans cette section, nous traitent de scénarios qui ne répondent pas aux hello toutes les exigences toobe embarrassingly parallel. 

### <a name="mismatched-partition-count"></a>Nombre de partitions d’entrée et de sortie différent
* Entrée : concentrateur Event Hub avec 8 partitions
* Sortie : concentrateur Event Hub avec 32 partitions

Dans ce cas, il n’importe quelle requête hello est. Si le nombre de partitions d’entrée de hello ne correspond pas à nombre de partitions de sortie hello, topologie de hello n’est pas excessivement parallèle.

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a>Sortie ne correspondant pas à un concentrateur Event Hub ni à un stockage d’objets blob
* Entrée : concentrateur Event Hub avec 8 partitions
* Sortie : Power BI

Pour le moment, la sortie Power BI ne prend pas en charge le partitionnement. Par conséquent, ce scénario n’est pas de type massivement parallèle.

### <a name="multi-step-query-with-different-partition-by-values"></a>Requête à plusieurs étapes avec différentes valeurs Partition By
* Entrée : concentrateur Event Hub avec 8 partitions
* Sortie : concentrateur Event Hub avec 8 partitions

Requête :

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Comme vous pouvez le voir, hello deuxième étape utilise **TollBoothId** en tant que clé de partitionnement de hello. Cette étape est même hello pas en tant que première étape de hello, et elle nécessite par conséquent nous toodo une lecture aléatoire. 

Hello exemples précédents décrivent certains travaux Analytique de flux de données qui sont conformes trop (ou ne) une topologie de ces. Si elles sont conformes, ils ont potentiel hello pour l’échelle maximale. Pour les travaux qui ne correspondent pas à l’un de ces profils, des conseils de mise à l’échelle seront disponibles dans les futures mises à jour. Pour l’instant, utilisez les conseils généraux hello Bonjour les sections suivantes.

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a>Calculer les unités de diffusion en continu maximale hello d’un travail
Nombre total de Hello d’unités de diffusion en continu qui peut être utilisé par une tâche de flux de données Analytique dépend du nombre hello des étapes de requête de hello définie pour les travaux de hello et nombre de hello de partitions pour chaque étape.

### <a name="steps-in-a-query"></a>Étapes dans une requête
Une requête peut avoir une ou plusieurs étapes. Chaque étape est une sous-requête définie par hello **WITH** (mot clé). requête Hello qui se trouve en dehors de hello **WITH** (mot clé) (une requête uniquement) est également comptabilisée comme une étape, par exemple hello **sélectionnez** instruction Bonjour suivant la requête :

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

Cette requête compte deux étapes.

> [!NOTE]
> Cette requête est décrite plus en détail plus loin dans l’article de hello.
>  

### <a name="partition-a-step"></a>Partitionnement d'une étape
Une étape de partitionnement nécessite hello conditions suivantes :

* source d’entrée de Hello doit être partitionné. 
* Hello **sélectionnez** instruction de requête de hello doit lire à partir d’une source d’entrée partitionnée.
* requête Hello au sein de l’étape de hello doit avoir hello **Partition By** (mot clé).

Lorsqu’une requête est partitionnée, les événements d’entrée hello sont des groupes de traité et agrégées dans partition distincte, et les événements de sorties sont générés pour chaque groupe de hello. Si vous souhaitez un agrégat combiné, vous devez créer un deuxième tooaggregate de non partitionné une étape.

### <a name="calculate-hello-max-streaming-units-for-a-job"></a>Calculer max hello unités pour un travail de diffusion en continu
Toutes les étapes non partitionnées ensemble peuvent évoluer toosix unités (SUs) pour une tâche de flux de données Analytique de diffusion en continu. SUs tooadd, une étape doivent être partitionnées. Chaque partition peut comporter six unités SU.

<table border="1">
<tr><th>Interroger</th><th>SUs max pour le travail de hello</th></td>

<tr><td>
<ul>
<li>requête de Hello contient une seule étape.</li>
<li>étape de Hello n’est pas partitionnée.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>flux de données d’entrée Hello est partitionné par 3.</li>
<li>requête de Hello contient une seule étape.</li>
<li>étape de Hello est partitionnée.</li>
</ul>
</td>
<td>18</td></tr>

<tr><td>
<ul>
<li>requête de Hello contient deux étapes.</li>
<li>Aucun des étapes de hello est partitionnée.</li>
</ul>
</td>
<td>6</td></tr>

<tr><td>
<ul>
<li>flux de données d’entrée Hello est partitionné par 3.</li>
<li>requête de Hello contient deux étapes. étape d’entrée de Hello est partitionné et la deuxième étape de hello n’est pas.</li>
<li>Hello <strong>sélectionnez</strong> instruction lit à partir de l’entrée de hello partitionnée.</li>
</ul>
</td>
<td>24 (18 pour les étapes partitionnées + 6 pour les étapes non partitionnées)</td></tr>
</table>

### <a name="examples-of-scaling"></a>Exemples de mise à l’échelle

Hello requête suivante calcule nombre hello de voitures dans une fenêtre de trois minutes traverser une station de péage qui a trois péages. Cette requête peut être augmentée toosix SUs.

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

toouse plus SUs pour hello requête, les deux hello des flux de données d’entrée et les requêtes hello doivent être partitionnées. Étant donné que la partition de flux de données hello a la valeur too3, hello requête modifiée suivante peut être mis à l’échelle too18 SUs :

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

Lorsqu’une requête est partitionnée, les événements d’entrée hello sont traités et agrégées dans des groupes de partition distincte. Événements de sortie sont également générés pour chaque groupe de hello. Le partitionnement peut entraîner des résultats inattendus lorsque hello **GROUP BY** champ n’est pas clé de partition hello dans le flux de données d’entrée hello. Par exemple, hello **TollBoothId** clé de partition hello de champ dans la requête précédente de hello n’est pas **entrée1**. résultat de Hello est que hello données à partir de péage #1 peuvent être réparties dans plusieurs partitions.

Chacun des hello **entrée1** partitions seront traitées séparément par flux de données Analytique. Par conséquent, plusieurs enregistrements de nombre de voitures hello pour hello même péage Bonjour même fenêtre bascule sera créée. Si la clé de partition d’entrée hello ne peut pas être modifié, ce problème peut être résolu en ajoutant une étape d’une partition, comme dans hello l’exemple suivant :

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

Cette requête peut être mis à l’échelle too24 SUs.

> [!NOTE]
> Si vous joignez deux flux de données, assurez-vous que les flux de hello sont partitionnées par clé de partition hello de colonne de hello que vous utilisez des jointures de hello toocreate. Assurez-vous également que vous avez hello même nombre de partitions dans les deux flux de données.
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a>Configurer des unités de diffusion en continu Stream Analytics

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Dans la liste de hello des ressources, recherchez les tâches de flux Analytique hello que vous souhaitez tooscale, puis ouvrez.
3. Bonjour travail panneau, sous **configurer**, cliquez sur **échelle**.

    ![Configuration d’un travail Stream Analytics sur le portail Azure][img.stream.analytics.preview.portal.settings.scale]

4. Utilisez hello curseur tooset hello SUs pour le travail de hello. Notez que vous les paramètres SU toospecific limité.


## <a name="monitor-job-performance"></a>Surveillance des performances du travail
À l’aide de hello portail Azure, vous pouvez suivre le débit d’une tâche hello :

![Surveillance des travaux Azure Stream Analytics][img.stream.analytics.monitor.job]

Calculer le débit de charge de travail hello hello attendu. Si le débit de hello est inférieur au nombre attendu, régler la partition d’entrée de hello, paramétrez hello requête et ajouter SUs tooyour travail.


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a>Visualiser le débit de flux de données Analytique à l’échelle : scénario de framboises Pi hello
toohelp que vous comprenez comment les tâches de flux de données Analytique l’échelle, nous avons effectué une expérience en fonction de l’entrée à partir d’un appareil framboises Pi. Cette expérience nous permettre de voir l’effet hello sur le débit de plusieurs unités de diffusion en continu et partitions.

Dans ce scénario, les appareils hello envoie concentrateur d’événements tooan capteur données (clients). Analytique de diffusion en continu traite les données de hello et envoie une alerte ou les statistiques sous la forme d’un concentrateur d’événements de sortie tooanother. 

client de Hello envoie des données de capteur au format JSON. sortie des données Hello est également au format JSON. les données de salutation ressemble à ceci :

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

Hello suivant la requête est toosend utilisé une alerte lorsqu’une lumière est mises hors tension :

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a>Mesurer le débit

Dans ce contexte, le débit est Montant hello des données d’entrée traitées par les flux de données Analytique une quantité fixe de temps. (Nous mesuré pendant 10 minutes). tooachieve hello meilleur débit de traitement pour hello les données d’entrée, les fichiers de données hello de flux d’entrée et les requêtes hello ont été partitionnées. Nous avons inclus **COUNT()** dans hello requête toomeasure combien d’événements d’entrée ont été traitées. travail de hello que toomake pas simplement attendait toocome des événements d’entrée, chaque partition du concentrateur d’événements d’entrée hello a été préchargée environ 300 Mo de données d’entrée.

Hello tableau suivant montre les résultats hello que nous avons vu lorsque nous avons augmenté nombre hello d’unités de diffusion en continu et du nombre de partition correspondante de hello dans les concentrateurs d’événements.  

<table border="1">
<tr><th>Partitions d'entrée</th><th>Partitions de sortie</th><th>Unités de diffusion en continu</th><th>Débit soutenu
</th></td>

<tr><td>12</td>
<td>12</td>
<td>6</td>
<td>4,06 Mo/s</td>
</tr>

<tr><td>12</td>
<td>12</td>
<td>12</td>
<td>8,06 Mo/s</td>
</tr>

<tr><td>48</td>
<td>48</td>
<td>48</td>
<td>38,32 Mo/s</td>
</tr>

<tr><td>192</td>
<td>192</td>
<td>192</td>
<td>172,67 Mo/s</td>
</tr>

<tr><td>480</td>
<td>480</td>
<td>480</td>
<td>454,27 Mo/s</td>
</tr>

<tr><td>720</td>
<td>720</td>
<td>720</td>
<td>609,69 Mo/s</td>
</tr>
</table>

Et hello graphique suivant montre une visualisation de relation hello entre SUs et le débit.

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a>Obtenir de l’aide
Pour obtenir une assistance, consultez le [forum Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Étapes suivantes
* [Introduction tooAzure Analytique de flux de données](stream-analytics-introduction.md)
* [Prise en main d’Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Références sur le langage des requêtes d'Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Références sur l’API REST de gestion d’Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

