---
title: aaaCapacity et solution de performances dans Azure journal Analytique | Documents Microsoft
description: "Hello d’utiliser la capacité et de la solution de performances dans toohelp Analytique de journal vous comprenez hello la capacité de vos serveurs Hyper-V."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Planifier la capacité d’ordinateur virtuel Hyper-V avec hello capacité et de la solution de performances (version préliminaire)

![Symbole de Capacity and Performance](./media/log-analytics-capacity/capacity-solution.png)

Vous pouvez utiliser la capacité de hello et solution de performances dans toohelp Analytique de journal vous comprenez hello la capacité de vos serveurs Hyper-V. solution de Hello fournit les insights dans votre environnement Hyper-V en vous montrant hello utilisation globale (processeur, mémoire et disque) des hôtes de hello et hello des machines virtuelles en cours d’exécution sur ces ordinateurs hôtes Hyper-V. Mesures sont collectées pour l’UC, la mémoire et les disques sur tous les hôtes et les machines virtuelles de hello s’exécutant sur ceux-ci.

solution de Hello :

-   Indique les hôtes dont les utilisations de processeur et de mémoire sont la plus élevée et la plus faible
-   Indique les machines virtuelles dont les utilisations de processeur et de mémoire sont la plus élevée et la plus faible
-   Indique les machines virtuelles avec le nombre d’E/S par seconde et l’utilisation de débit les plus élevés et les plus faibles
-   Indique quelles machines virtuelles sont exécutées sur tels hôtes
-   Montre hello disques supérieur avec un débit élevé, e/s, et les volumes partagés de latence en cluster
- Vous permet de toocustomize et des filtrer en fonction des groupes

> [!NOTE]
> version précédente de Hello de hello capacité et des solutions de performances appelée gestion de la capacité requise de System Center Operations Manager et System Center Virtual Machine Manager. Cette solution mise à jour ne comporte plus ces dépendances.


## <a name="connected-sources"></a>Sources connectées

Hello tableau suivant décrit les sources de hello connecté sont pris en charge par cette solution.

| Source connectée | Support | Description |
|---|---|---|
| [Agents Windows](log-analytics-windows-agents.md) | Oui | solution de Hello collecte des informations de données de capacité et de performances à partir des agents Windows. |
| [Agents Linux](log-analytics-linux-agents.md) | Non    | solution de Hello ne collecte pas les informations de capacité et de performances de données à partir des agents Linux directes.|
| [Groupe d’administration SCOM](log-analytics-om-agents.md) | Oui |solution de Hello collecte les données de capacité et de performances à partir des agents dans un groupe d’administration SCOM connecté. Une connexion directe à partir de hello SCOM agent tooOMS n’est pas nécessaire. Données sont transférées depuis le référentiel OMS toohello hello gestion groupe.|
| [Compte Azure Storage](log-analytics-azure-storage.md) | Non | Le stockage Azure n’inclut pas de données de performances ni de capacité.|

## <a name="prerequisites"></a>Composants requis

- Des agents Windows ou Operations Manager doivent être installés sur Windows Server 2012 ou des hôtes Hyper-V supérieurs, mais pas sur des machines virtuelles.


## <a name="configuration"></a>Configuration

Effectuer hello suivant l’étape tooadd hello capacité et performances solution tooyour espace de travail.

- Ajouter hello capacité et performances solution tooyour espace de travail OMS à l’aide du processus de hello décrites dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Packs d’administration

Si votre groupe d’administration SCOM est l’espace de travail OMS tooyour connecté, hello suivant des packs d’administration sera installé dans SCOM lorsque vous ajoutez cette solution. Ces packs d’administration ne nécessitent aucune opération de configuration ou de maintenance.

- Microsoft.IntelligencePacks.CapacityPerformance

événement de 1201 Hello ressemble à :


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Lorsque la mise à jour de hello solution de capacité et de performances, numéro de version hello change.

Pour plus d’informations sur la façon dont les packs d’administration de solution sont mises à jour, consultez [connecter Operations Manager tooLog Analytique](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>À l’aide de la solution de hello

Lorsque vous ajoutez hello capacité et performances solution tooyour espace de travail, hello capacité et performances est ajouté toohello tableau de bord de présentation. Cette vignette affiche le nombre de nombre de hello d’actives hôtes Hyper-V et de nombre de hello d’ordinateurs virtuels actifs qui ont été analysés pour hello période sélectionnée.

![Vignette Capacité et performances](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Vérifier l’utilisation

Cliquez sur hello capacité et performances vignette tooopen hello capacité et performances tableau de bord. tableau de bord Hello inclut des colonnes de hello Bonjour tableau suivant. Chaque colonne répertorie les articles tooten mise en correspondance que les critères de la colonne pour hello spécifié plage étendue et d’heure. Vous pouvez exécuter une recherche de journal qui retourne tous les enregistrements en cliquant sur **afficher tous les** bas hello de colonne de hello ou en cliquant sur en-tête de colonne hello.

- **Hôtes**
    - **Hôte de l’utilisation du processeur** indique une tendance graphique d’utilisation de hello du processeur des ordinateurs hôtes et une liste des ordinateurs hôtes, en fonction de hello période sélectionnée. Pointez sur les détails de tooview graphique la ligne hello pour un point spécifique dans le temps. Cliquez sur hello graphique tooview plus de détails dans la recherche de journal. Cliquez sur les recherches de journal hôte nom tooopen et afficher les détails des compteurs UC pour les ordinateurs virtuels hébergés.
    - **Héberger l’utilisation de la mémoire** indique une tendance graphique d’utilisation de la mémoire des ordinateurs hôtes hello et une liste des ordinateurs hôtes, en fonction de hello période sélectionnée. Pointez sur les détails de tooview graphique la ligne hello pour un point spécifique dans le temps. Cliquez sur hello graphique tooview plus de détails dans la recherche de journal. Cliquez sur n’importe quel hôte nom tooopen journal recherche et affichage compteur détails de la mémoire pour les ordinateurs virtuels hébergés.
- **Machines virtuelles**
    - **Utilisation du processeur de machine virtuelle** indique une tendance graphique d’utilisation de hello du processeur des ordinateurs virtuels et une liste d’ordinateurs virtuels, en fonction de hello période sélectionnée. Survolez hello graphique tooview détails d’un point spécifique dans le temps pour hello premiers 3 machines virtuelles. Cliquez sur hello graphique tooview plus de détails dans la recherche de journal. Cliquez sur n’importe quel recherche de journal de machine virtuelle nom tooopen et afficher les détails des compteurs UC agrégées pour hello machine virtuelle.
    - **Utilisation de la mémoire virtuelle** indique une tendance graphique d’utilisation de la mémoire hello d’ordinateurs virtuels et une liste d’ordinateurs virtuels, en fonction de hello période sélectionnée. Survolez hello graphique tooview détails d’un point spécifique dans le temps pour hello premiers 3 machines virtuelles. Cliquez sur hello graphique tooview plus de détails dans la recherche de journal. Cliquez sur n’importe quel recherche de journal de machine virtuelle nom tooopen et afficher les détails des compteurs mémoire agrégées pour hello machine virtuelle.
    - **E/s de disque totale VM** indique une tendance graphique de hello total e/s de disque pour les ordinateurs virtuels et une liste d’ordinateurs virtuels avec hello IOPS pour chacun, en fonction de hello période sélectionnée. Survolez hello graphique tooview détails d’un point spécifique dans le temps pour hello premiers 3 machines virtuelles. Cliquez sur hello graphique tooview plus de détails dans la recherche de journal. Cliquez sur n’importe quel recherche de journal de tooopen de nom de machine virtuelle et une vue agrégée de disque IOPS compteur détails pour hello machine virtuelle.
    - **Débit Total du disque VM** indique une tendance graphique de hello débit total du disque pour les machines virtuelles et une liste d’ordinateurs virtuels avec hello débit total du disque pour chaque, hello selon sélectionnés laps de temps. Survolez hello graphique tooview détails d’un point spécifique dans le temps pour hello premiers 3 machines virtuelles. Cliquez sur hello graphique tooview plus de détails dans la recherche de journal. Cliquez sur n’importe quel recherche de journal de machine virtuelle nom tooopen et afficher les détails des compteurs disque total agrégé débit pour hello machine virtuelle.
- **Volumes en cluster partagés**
    - **Nombre total de débit** affiche la somme hello des deux lectures et écritures sur les volumes partagés de cluster.
    - **Nombre total d’e/s** somme de hello montre des opérations d’entrée/sortie par seconde sur les volumes partagés de cluster.
    - **Latence totale** montre la latence totale de hello sur des volumes partagés de cluster.
- **Héberger densité** vignette de supérieur de hello affiche le nombre total de hello de solution de toohello disponible des ordinateurs hôtes et des machines virtuelles. Cliquez sur hello Vignette supérieure tooview des détails supplémentaires dans recherche de journal. Répertorie également tous les hôtes et nombre de hello d’ordinateurs virtuels qui sont hébergés. Cliquez sur un hôte de toodrill les résultats de la machine virtuelle hello dans une recherche de journal.


![panneau Hôtes du tableau de bord](./media/log-analytics-capacity/dashboard-hosts.png)

![panneau Machines virtuelles du tableau de bord](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Évaluer les performances

Environnements de production diffèrent considérablement des tooanother d’une organisation. En outre, les charges de travail de capacité et de performance peuvent dépendre du mode d’exécution de vos machines virtuelles et de ce que vous considérez normal. Toohelp procédures spécifiques mesurer les performances s’appliquera probablement pas tooyour environnement. Par conséquent, plus généralisé des instructions est mieux adapté toohelp. Microsoft publie une variété d’instructions articles toohelp mesurer les performances.

toosummarize, solution de hello collecte des données de capacité et de performances à partir de diverses sources, y compris les compteurs de performance. Utiliser ces données de capacité et de performances présentés dans les surfaces différents dans les solutions hello et comparer votre toothose de résultats à hello [mesure les performances sur Hyper-V](https://msdn.microsoft.com/library/cc768535.aspx) l’article. Bien que l’article de hello a été publiée quelques temps auparavant, les instructions, des considérations et des métriques de hello sont toujours valides. article de Hello contient des ressources utiles tooother de liens.


## <a name="sample-log-searches"></a>Exemples de recherches dans les journaux

Hello tableau suivant fournit des exemples des recherches de journaux pour les données de capacité et de performances collectées et calculée par cette solution.

| Interroger | Description |
|---|---|
| Toutes les configurations mémoire d’hôte | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Toutes les configurations mémoire de machine virtuelle | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Répartition de toutes les E/S par seconde des disques entre toutes les machines virtuelles | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Répartition du débit total des disques entre toutes les machines virtuelles | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Répartition de toutes les E/S par seconde entre tous les volumes partagés de cluster | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Répartition du débit total entre tous les volumes partagés de cluster | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Répartition de la latence totale entre tous les volumes partagés de cluster | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivant.

> | Interroger | Description |
|:--- |:--- |
| Toutes les configurations mémoire d’hôte | Perf &#124; où ObjectName == « Capacité et performances » et CounterName == « Mo de mémoire attribuée Mo à l’hôte » &#124; résumer Mo = avg(CounterValue) par InstanceName |
| Toutes les configurations mémoire de machine virtuelle | Perf &#124; où ObjectName == « Capacité et performance » et CounterName == « Mo de mémoire attribuée à la machine virtuelle » &#124; résumer Mo = avg(CounterValue) par InstanceName |
| Répartition de toutes les E/S par seconde des disques entre toutes les machines virtuelles | Perf &#124; où ObjectName == « Capacité et performance » et (CounterName == « Lectures/s de disque dur virtuel » ou CounterName == « Écritures/s de disque dur virtuel ») &#124; résumer AggregatedValue = avg(CounterValue) par emplacement (TimeGenerated, 1 h), CounterName, InstanceName |
| Répartition du débit total des disques entre toutes les machines virtuelles | Perf &#124; où ObjectName == « Capacité et performance » et (CounterName == « Lecture Mo/s de disque dur virtuel » ou CounterName == « Écriture Mo/s de disque dur virtuel ») &#124; résumer AggregatedValue = avg(CounterValue) par emplacement (TimeGenerated, 1 h), CounterName, InstanceName |
| Répartition de toutes les E/S par seconde entre tous les volumes partagés de cluster | Perf &#124; où ObjectName == « Capacité et performance » et (CounterName == « Lectures/s de volume partagé de cluster » ou CounterName == « Écritures/s de volume partagé de cluster ») &#124; résumer AggregatedValue = avg(CounterValue) par emplacement (TimeGenerated, 1 h), CounterName, InstanceName |
| Répartition du débit total entre tous les volumes partagés de cluster | Perf &#124; où ObjectName == « Capacité et performance » et (CounterName == « Lectures/s de volume partagé de cluster » ou CounterName == « Écritures/s de volume partagé de cluster ») &#124; résumer AggregatedValue = avg(CounterValue) par emplacement (TimeGenerated, 1 h), CounterName, InstanceName |
| Répartition de la latence totale entre tous les volumes partagés de cluster | Perf &#124; où ObjectName == « Capacité et performance » et (CounterName == « Latence de lectures/s de volume partagé de cluster » ou CounterName == « Latence d’écritures/s de volume partagé de cluster ») &#124; résumer AggregatedValue = avg(CounterValue) par emplacement (TimeGenerated, 1 h), CounterName, InstanceName |


## <a name="next-steps"></a>Étapes suivantes
* Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillées des données de performances et de capacité.
