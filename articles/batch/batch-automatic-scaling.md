---
title: "mise à l’échelle aaaAutomatically nœuds de calcul dans un pool de traitement par lots Azure | Documents Microsoft"
description: "Activer l’échelle automatique sur un toodynamically de pool de cloud d’ajuster le nombre de hello de nœuds de calcul dans le pool de hello."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: c624cdfc-c5f2-4d13-a7d7-ae080833b779
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: multiple
ms.date: 06/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6d1e0c5d8e0e56e15a4d3588150f2466a689f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-automatic-scaling-formula-for-scaling-compute-nodes-in-a-batch-pool"></a>Mettre automatiquement à l’échelle les nœuds de calcul dans un pool Azure Batch

Azure Batch peut automatiquement mettre à l’échelle des pools en fonction de paramètres que vous définissez. Mise à l’échelle automatique, lot ajoute dynamiquement le pool tooa de nœuds en tant que tâche l’augmentation des demandes et supprime les nœuds de calcul car ils diminuent. Vous pouvez enregistrer le temps et argent en réglant automatiquement le nombre de hello de nœuds de calcul utilisées par votre application de traitement par lots. 

Pour activer la mise à l’échelle automatique sur un pool de nœuds de calcul, associez-lui une *formule de mise à l’échelle* définie par vos soins. Hello service Batch utilise nombre de hello toodetermine formule hello mise à l’échelle de nœuds de calcul qui sont nécessaire tooexecute votre charge de travail. Les nœuds de calcul peuvent être des nœuds dédiés ou des [nœuds de faible priorité](batch-low-pri-vms.md). Lot répond tooservice les données de métriques sont collectées à intervalles réguliers. À l’aide de ces données de métriques, lot ajuste nombre hello de nœuds de calcul dans le pool hello en fonction de votre formule et selon un intervalle configuré.

Vous pouvez activer la mise à l’échelle automatique lors de la création d’un pool ou dans un pool existant. Vous pouvez également modifier une formule existante dans un pool dont la mise à l’échelle automatique est configurée. Traitement par lots vous permet de tooevaluate vos formules avant de les assigner toopools et toomonitor état hello de mise à l’échelle automatique s’exécute.

Cet article traite de hello diverses entités qui composent votre mise à l’échelle des formules, y compris les variables, les opérateurs, les opérations et les fonctions. Nous expliquons comment tooobtain différentes métriques de ressource et de tâche dans un lot de calcul. Vous pouvez utiliser ces tooadjust mesures nombre de nœuds de votre pool en fonction de l’état de tâche et l’utilisation des ressources. Ensuite, nous décrire comment tooconstruct une formule et automatique de mise à l’échelle sur un pool à l’aide d’activer hello REST de traitement par lots et les API .NET. Et nous terminerons par quelques exemples de formule.

> [!IMPORTANT]
> Lorsque vous créez un compte de traitement par lots, vous pouvez spécifier hello [configuration du compte](batch-api-basics.md#account), qui détermine si les pools sont répartis dans un abonnement au service de traitement par lots (valeur par défaut de hello), ou dans votre abonnement de l’utilisateur. Si vous avez créé votre compte Batch avec la configuration de Service Batch hello par défaut, votre compte est tooa limité le nombre maximal de cœurs qui peut être utilisé pour le traitement. Hello service Batch met à l’échelle des nœuds de calcul uniquement des toothat limite maximale du principal. Pour cette raison, hello service Batch ne peut-être pas atteint le numéro de cible hello de nœuds de calcul spécifié par une formule de mise à l’échelle. Consultez [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md) pour plus d’informations sur l’affichage et d’augmenter les quotas de votre compte.
>
>Si vous avez créé votre compte avec la configuration de l’abonnement de l’utilisateur hello, votre compte de partage dans le quota de cœurs hello pour l’abonnement de hello. Pour en savoir plus, consultez le paragraphe [Limites de machines virtuelles](../azure-subscription-service-limits.md#virtual-machines-limits) de la section [Abonnement Azure et limites, quotas et contraintes de service](../azure-subscription-service-limits.md).
>
>

## <a name="automatic-scaling-formulas"></a>Formules de mise à l’échelle automatique
Une formule de mise à l’échelle automatique est une valeur de chaîne définie par vos soins qui contient une ou plusieurs instructions. formule de mise à l’échelle Hello est affectée du pool tooa [autoScaleFormula] [ rest_autoscaleformula] élément (lot REST) ou [CloudPool.AutoScaleFormula] [ net_cloudpool_autoscaleformula] propriété (lot .NET). Hello service Batch utilise votre numéro de cible toodetermine formule hello de nœuds de calcul dans le pool de hello pour hello prochain intervalle de traitement. chaîne de la formule Hello ne peut pas dépasser 8 Ko, peuvent inclure des instructions too100 qui sont séparées par des points-virgules et peuvent inclure des sauts de ligne et de commentaires.

Les formules de mise à l’échelle automatique reviennent en quelque sorte à utiliser un « langage » de mise à l’échelle Batch. Les instructions formule sont des expressions de forme libre qui peuvent inclure des variables définies par le service (variables définies par le service de traitement par lots hello) et les variables définies par l’utilisateur (les variables que vous définissez). Elles peuvent effectuer différentes opérations sur ces valeurs à l’aide de types, d’opérateurs et de fonctions intégrés. Par exemple, une instruction peut prendre hello suivant du formulaire :

```
$myNewVariable = function($ServiceDefinedVariable, $myCustomVariable);
```

Les formules contiennent généralement plusieurs instructions qui effectuent des opérations sur les valeurs qui sont obtenues dans les instructions précédentes : Par exemple, tout d’abord nous obtenir une valeur pour `variable1`, puis passez-le tooa fonction toopopulate `variable2`:

```
$variable1 = function1($ServiceDefinedVariable);
$variable2 = function2($OtherServiceDefinedVariable, $variable1);
```

Inclure ces instructions dans votre tooarrive formule de mise à l’échelle à un nombre cible de nœuds de calcul. Les nœuds dédiés et les nœuds de faible priorité ont leurs propres paramètres cibles, afin que vous puissiez définir une cible pour chaque type de nœud. Une formule de mise à l’échelle automatique peut inclure une valeur cible pour les nœuds dédiés, une valeur cible pour les nœuds de faible priorité, ou les deux.

nombre de cible Hello de nœuds est supérieure, inférieure, ou même que le nombre actuel de hello de nœuds de ce type dans le pool de hello hello. Le service Batch évalue la formule de mise à l’échelle automatique d’un pool à un intervalle spécifique (reportez-vous aux [intervalles de mise à l’échelle automatique](#automatic-scaling-interval)). Traitement par lots ajuste le nombre cible de hello de chaque type de nœud dans le nombre de toohello pool hello indiquant votre formule de mise à l’échelle au moment de l’évaluation de hello.

### <a name="sample-autoscale-formula"></a>Exemple de formule de mise à l’échelle automatique

Voici un exemple d’une formule de mise à l’échelle peut être ajustée toowork pour la plupart des scénarios. Hello variables `startingNumberOfVMs` et `maxNumberofVMs` Bonjour formule de l’exemple peut être ajustée tooyour besoins. Cette formule met à l’échelle des nœuds dédiés, mais peut être modifiée tooapply également les nœuds de faible priorité tooscale. 

```
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicatedNodes=min(maxNumberofVMs, pendingTaskSamples);
```

Avec cette formule de mise à l’échelle, hello pool est initialement créé avec une seule machine virtuelle. Hello `$PendingTasks` métrique définit le nombre de hello de tâches qui sont en cours d’exécution ou en file d’attente. formule de Hello recherche hello moyenne d’attente de tâches Bonjour 180 dernières secondes et définit hello `$TargetDedicatedNodes` variable en conséquence. formule de Hello garantit que le numéro de cible hello de nœuds dédiés ne dépasse jamais 25 ordinateurs virtuels. Comme les nouvelles tâches sont envoyés, pool de hello croît automatiquement. En tant que tâches se terminent, machines virtuelles deviennent libre un par un et formule d’échelle hello réduit le pool de hello.

## <a name="variables"></a>variables
Vous pouvez utiliser aussi bien des variables **définies par le service** que des variables **définies par l’utilisateur** dans les formules de mise à l’échelle automatique. variables de Hello défini par le service sont générés dans toohello service Batch. Certaines variables définies par le service sont en lecture-écriture, tandis que d’autres sont en lecture seule. Les variables définies par l’utilisateur sont des variables que vous définissez. Dans la formule de l’exemple hello indiqué dans la section précédente de hello, `$TargetDedicatedNodes` et `$PendingTasks` sont des variables définies par le service. Les variables `startingNumberOfVMs` et `maxNumberofVMs` sont des variables définies par l’utilisateur.

> [!NOTE]
> Les variables définies par le service sont toujours précédées d’un signe dollar ($). Pour les variables définies par l’utilisateur, le symbole dollar hello est facultative.
>
>

Hello les tableaux suivants indiquent les deux en lecture-écriture et de variables en lecture seule qui sont définis par hello service Batch.

Vous pouvez obtenir et définir des nombre de hello toomanage de nœuds de calcul de valeurs hello de ces variables défini par le service dans un pool :

| Variables définies par le service en lecture-écriture | Description |
| --- | --- |
| $TargetDedicatedNodes |nœuds pour le pool de hello de calcul du nombre de cible de Hello de dédié. nombre de Hello de nœuds dédiés est spécifié en tant que cible, car un pool ne peut pas atteindre toujours nombre hello souhaité de nœuds. Par exemple, si le nombre de cibles de hello de nœuds dédiés est modifié par une évaluation de mise à l’échelle avant hello pool a atteint cible initiale de hello, puis le pool de hello ne peut pas atteindre cible de hello. <br /><br /> Un pool dans un compte créé avec la configuration du Service de traitement par lots hello ne peut pas atteindre sa cible si la cible de hello dépasse un nœud ou core un quota de comptes Batch. Un pool dans un compte créé avec la configuration de l’abonnement de l’utilisateur hello ne peut pas atteindre sa cible si la cible de hello dépasse le quota de cœur partagé hello pour l’abonnement de hello.|
| $TargetLowPriorityNodes |nœuds pour le pool de hello de calcul du nombre de cible de Hello de faible priorité. nombre de Hello de nœuds de faible priorité est spécifié en tant que cible, car un pool ne peut pas atteindre toujours nombre hello souhaité de nœuds. Par exemple, si le nombre de postes de faible priorité cibles de hello est modifiée par une évaluation de mise à l’échelle avant hello pool a atteint cible initiale de hello, puis le pool de hello ne peut pas atteindre cible de hello. Un pool peut également pas obtenir sa cible si la cible de hello dépasse un quota de comptes Batch nœud ou core. <br /><br /> Pour plus d’informations sur les nœuds de calcul de faible priorité, consultez [Utiliser des machines virtuelles de faible priorité avec Batch (préversion)](batch-low-pri-vms.md). |
| $NodeDeallocationOption |action Hello qui se produit lorsque les nœuds de calcul sont supprimés à partir d’un pool. Les valeurs possibles sont les suivantes :<ul><li>**remettre**--s’arrête immédiatement des tâches et les place en file d’attente de travail hello afin qu’elles soient replanifiées.<li>**Terminer**--s’arrête immédiatement des tâches et les supprime de la file d’attente des travaux hello.<li>**taskcompletion**--attend en cours d’exécution des tâches toofinish et puis supprime le nœud de hello de pool de hello.<li>**retaineddata**--attend que toutes les hello conservés à la tâche données locales sur hello nœud toobe nettoyé avant de supprimer un nœud de hello à partir du pool de hello.</ul> |

Vous pouvez obtenir la valeur hello de ces réglages toomake défini par le service des variables qui sont basées sur les métriques à partir du service de traitement par lots hello :

| Variables définies par le service en lecture seule | Description |
| --- | --- |
| $CPUPercent |pourcentage moyen de Hello d’utilisation du processeur. |
| $WallClockSeconds |nombre de Hello de secondes consommées. |
| $MemoryBytes |Nombre moyen de Hello de mégaoctets consommés. |
| $DiskBytes |Nombre moyen de Hello de gigaoctets utilisés sur les disques locaux hello. |
| $DiskReadBytes |nombre de Hello d’octets lus. |
| $DiskWriteBytes |nombre de Hello d’octets écrits. |
| $DiskReadOps |nombre de Hello d’opérations de lecture sur disque est effectuée. |
| $DiskWriteOps |nombre de Hello disque d’opérations d’écriture effectuées. |
| $NetworkInBytes |nombre de Hello d’octets entrants. |
| $NetworkOutBytes |nombre de Hello d’octets sortants. |
| $SampleNodeCount |nombre de Hello de nœuds de calcul. |
| $ActiveTasks |nombre de Hello de tâches qui sont tooexecute prêt, mais pas l’exécution. nombre de Hello $ActiveTasks inclut toutes les tâches qui se trouvent dans un état actif de hello et dont les dépendances ont été satisfaites. Toutes les tâches qui se trouvent dans un état actif de hello mais dont les dépendances n’ont pas été satisfaites sont exclus du nombre de hello $ActiveTasks.|
| $RunningTasks |nombre de Hello de tâches en cours d’exécution. |
| $PendingTasks |somme de Hello de $ActiveTasks et $RunningTasks. |
| $SucceededTasks |nombre de Hello de tâches qui s’est correctement terminée. |
| $FailedTasks |nombre de Hello de tâches qui ont échoué. |
| $CurrentDedicatedNodes |Nombre actuel de Hello de dédié des nœuds de calcul. |
| $CurrentLowPriorityNodes |Nombre actuel de Hello de faible priorité des nœuds, y compris les nœuds qui ont été devancées de calcul. |
| $PreemptedNodeCount | nombre de Hello de nœuds dans le pool de hello qui se trouvent dans un état devancée. |

> [!TIP]
> Hello variables en lecture seule, défini par le service qui figurent dans le tableau précédent de hello sont *objets* qui fournissent diverses méthodes tooaccess les données associées à chaque. Pour plus d’informations, consultez la section [Obtenir des échantillons de données](#getsampledata) dans la suite de cet article.
>
>

## <a name="types"></a>Types
Ces types sont pris en charge dans une formule :

* double
* doubleVec
* doubleVecList
* string
* timestamp--timestamp est une structure composée contient hello suivant des membres :

  * year
  * mois (1-12)
  * jour (1-31)
  * jour de la semaine (au format hello du numéro de ; par exemple, 1 pour lundi)
  * heure (au format 24 heures, par exemple, 13 signifie 1 PM)
  * minute (00-59)
  * seconde (00-59)
* timeinterval

  * TimeInterval_Zero
  * TimeInterval_100ns
  * TimeInterval_Microsecond
  * TimeInterval_Millisecond
  * TimeInterval_Second
  * TimeInterval_Minute
  * TimeInterval_Hour
  * TimeInterval_Day
  * TimeInterval_Week
  * TimeInterval_Year

## <a name="operations"></a>Opérations
Ces opérations sont autorisées sur les types de hello qui sont répertoriées dans la section précédente de hello.

| Opération | Opérateurs pris en charge | Type de résultat |
| --- | --- | --- |
| double *opérateur* double |+, -, *, / |double |
| double *opérateur* timeinterval |* |timeinterval |
| doubleVec *opérateur* double |+, -, *, / |doubleVec |
| doubleVec *opérateur* doubleVec |+, -, *, / |doubleVec |
| timeinterval *opérateur* double |*, / |timeinterval |
| timeinterval *opérateur* timeinterval |+, - |timeinterval |
| timeinterval *opérateur* timestamp |+ |timestamp |
| timestamp *opérateur* timeinterval |+ |timestamp |
| timestamp *opérateur* timestamp |- |timeinterval |
| *opérateur*double |-, ! |double |
| *opérateur*timeinterval |- |timeinterval |
| double *opérateur* double |<, <=, ==, >=, >, != |double |
| string *opérateur* string |<, <=, ==, >=, >, != |double |
| timestamp *opérateur* timestamp |<, <=, ==, >=, >, != |double |
| timeinterval *opérateur* timeinterval |<, <=, ==, >=, >, != |double |
| double *opérateur* double |&&, &#124;&#124; |double |

Quand vous testez un double avec un opérateur ternaire (`double ? statement1 : statement2`), la valeur différente de zéro est **true** et zéro est **false**.

## <a name="functions"></a>Fonctions
Ces paramètres prédéfinis **fonctions** sont disponibles pour vous toouse dans la définition d’une formule de mise à l’échelle automatique.

| Fonction | Type de retour | Description |
| --- | --- | --- |
| avg(doubleVecList) |double |Retourne hello valeur moyenne de toutes les valeurs dans doubleVecList de hello. |
| len(doubleVecList) |double |Retourne hello longueur du vecteur de hello est créé à partir de doubleVecList de hello. |
| lg(double) |double |Retourne hello logarithme base 2 de hello double. |
| lg(doubleVecList) |doubleVec |Retourne hello component-wise logarithme base 2 de hello doubleVecList. Un vec (double) doit être explicitement transmis pour le paramètre hello. Sinon, la version double LG (double) de hello est supposée. |
| ln(double) |double |Retourne hello logarithme naturel de hello en double. |
| ln(doubleVecList) |doubleVec |Retourne hello component-wise logarithme base 2 de hello doubleVecList. Un vec (double) doit être explicitement transmis pour le paramètre hello. Sinon, la version double LG (double) de hello est supposée. |
| log(double) |double |Retourne hello base 10 de hello double. |
| log(doubleVecList) |doubleVec |Retourne hello component-wise base 10 de hello doubleVecList. Un vec (double) doit être explicitement transmis pour le paramètre de type double unique hello. Sinon, la version de log(double) double hello est supposée. |
| max(doubleVecList) |double |Retourne hello valeur maximale dans doubleVecList de hello. |
| min(doubleVecList) |double |Retourne hello valeur minimale dans doubleVecList de hello. |
| norm(doubleVecList) |double |Retourne hello norme deux du vecteur de hello est créé à partir de doubleVecList de hello. |
| percentile(doubleVec v, double p) |double |Retourne hello élément percentile du vecteur de hello v. |
| rand() |double |Retourne une valeur aléatoire comprise entre 0,0 et 1,0. |
| range(doubleVecList) |double |Retourne la différence hello hello valeurs minimale et maximales dans doubleVecList de hello. |
| std(doubleVecList) |double |Retourne hello exemple d’écart des valeurs hello hello doubleVecList. |
| stop() | |Arrête l’évaluation d’expression d’échelle hello. |
| sum(doubleVecList) |double |Retourne hello somme de tous les composants hello de hello doubleVecList. |
| time(string dateTime="") |timestamp |Retourne les hello horodatage de hello heure actuelle, si aucun paramètre est passés ou hello horodatage de la chaîne de date/heure hello s’il est passé. Les formats dateTime pris en charge sont W3C-DTF et RFC 1123. |
| val(doubleVec v, double i) |double |Retourne la valeur hello d’élément hello qui est à l’emplacement i dans le vecteur v, avec un index de départ de zéro. |

Certaines fonctions hello qui sont décrites dans le tableau précédent de hello peuvent accepter une liste en tant qu’argument. liste séparée par des virgules de Hello est n’importe quelle combinaison de *double* et *doubleVec*. Par exemple :

`doubleVecList := ( (double | doubleVec)+(, (double | doubleVec) )* )?`

Hello *doubleVecList* valeur est convertie tooa unique *doubleVec* avant d’évaluation. Par exemple, si `v = [1,2,3]`, puis en appelant `avg(v)` est équivalent toocalling `avg(1,2,3)`. Appel de `avg(v, 7)` est équivalent toocalling `avg(1,2,3,7)`.

## <a name="getsampledata"></a>Obtenir des échantillons de données
Formules de mise à l’échelle agissent sur les données de métrique (exemples) qui sont fournies par hello service Batch. Une formule augmente ou diminue la taille du pool en fonction des valeurs hello qu’il obtient de service de hello. Hello service défini les variables qui ont été décrites précédemment sont des objets qui fournissent diverses méthodes données tooaccess qui sont associées à cet objet. Par exemple, hello expression suivante montre un Bonjour de tooget demande cinq dernières minutes d’utilisation du processeur :

```
$CPUPercent.GetSample(TimeInterval_Minute * 5)
```

| Méthode | Description |
| --- | --- |
| GetSample() |Hello `GetSample()` méthode retourne un vecteur d’exemples de données.<br/><br/>Un échantillon correspond à 30 secondes de données de métrique. En d’autres termes, des échantillons sont obtenus toutes les 30 secondes, Mais comme indiqué ci-dessous, il existe un décalage entre quand un échantillon est collecté et lorsqu’il est disponible tooa formule. Par conséquent, tous les échantillons pour une période donnée ne sont pas forcément disponibles pour évaluation par une formule.<ul><li>`doubleVec GetSample(double count)`<br/>Spécifie le nombre hello de tooobtain exemples à partir d’échantillons les plus récents hello qui ont été collectés.<br/><br/>`GetSample(1)`Retourne la dernière hello, exemple disponible. Pour les métriques tels que `$CPUPercent`, toutefois, cela pas doit être utilisé, car il est impossible tooknow *lorsque* hello échantillon a été collecté. Il peut s’agir d’un événement récent ou plus ancien en raison de problèmes système. Il est préférable, dans ce cas de toouse un intervalle de temps, comme indiqué ci-dessous.<li>`doubleVec GetSample((timestamp or timeinterval) startTime [, double samplePercent])`<br/>Spécifie le délai d’exécution de la collecte des exemples de données. Si vous le souhaitez, il spécifie également pourcentage d’échantillons qui doivent être disponibles dans hello hello demandé laps de temps.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10)`Renvoie 20 échantillons si tous les échantillons pour hello les 10 dernières minutes sont présentes dans l’historique de CPUPercent hello. Toutefois, si hello dernière minute de l’historique n’était pas disponible, exemples uniquement 18 sont retournées. Dans ce cas :<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 95)`échoue, car seuls 90 pour cent d’échantillons de hello sont disponibles.<br/><br/>`$CPUPercent.GetSample(TimeInterval_Minute * 10, 80)` aboutirait.<li>`doubleVec GetSample((timestamp or timeinterval) startTime, (timestamp or timeinterval) endTime [, double samplePercent])`<br/>Spécifie le délai d’exécution de la collecte des données avec une heure de début et une heure de fin.<br/><br/>Comme indiqué ci-dessus, il existe un décalage entre quand un échantillon est collecté et lorsqu’il est disponible tooa formule. Envisagez ce délai lorsque vous utilisez hello `GetSample` (méthode). Consultez `GetSamplePercent` ci-dessous. |
| GetSamplePeriod() |Retourne la période hello d’échantillons qui ont été effectuées dans un jeu de données exemple historiques. |
| Count() |Retourne hello nombre total d’échantillons dans l’historique de la métrique de hello. |
| HistoryBeginTime() |Retourne hello horodatage de hello plus ancien disponible échantillon de données de mesure de hello. |
| GetSamplePercent() |Retourne hello pourcentage des exemples qui sont disponibles pour un intervalle de temps donné. Par exemple :<br/><br/>`doubleVec GetSamplePercent( (timestamp or timeinterval) startTime [, (timestamp or timeinterval) endTime] )`<br/><br/>Étant donné que hello `GetSample` méthode échoue si le pourcentage d’échantillons retourné hello est inférieur à hello `samplePercent` spécifié, vous pouvez utiliser hello `GetSamplePercent` méthode toocheck première. Ensuite, vous pouvez effectuer une autre action si exemples insuffisantes sont présentes, sans arrêter l’évaluation de mise à l’échelle automatique hello. |

### <a name="samples-sample-percentage-and-hello-getsample-method"></a>Exemples et pourcentage de l’exemple hello *GetSample()* (méthode)
fonctionnement de base Hello d’une formule de mise à l’échelle est données métriques tooobtain tâches et les ressources et ajustez ensuite la taille du pool basé sur ces données. Par conséquent, il est important toohave conscience de l’interagissent entre les formules de mise à l’échelle avec les données de métriques (exemples).

**Exemples**

Hello service Batch régulièrement tire les exemples de tâches et les ressources des métriques et les formules de mise à l’échelle tooyour disponibles. Ces exemples sont enregistrées toutes les 30 secondes par hello service Batch. Toutefois, il y a généralement un délai entre lorsque ces exemples ont été enregistrés et lorsqu’elles sont rendues disponibles trop (et peuvent être lu par) vos formules de mise à l’échelle. En outre, en raison de facteurs tels que le réseau ou d’autres problèmes d’infrastructure toovarious échantillons ne soient pas enregistrées pour un intervalle donné.

**Pourcentage d’échantillonnage**

Lorsque `samplePercent` est passé toohello `GetSample()` méthode ou hello `GetSamplePercent()` méthode est appelée, _%_ fait référence tooa comparer le nombre possible de hello total d’exemples qui sont enregistrées par hello service Batch et nombre de Hello d’exemples qui sont la formule de mise à l’échelle tooyour disponibles.

Prenons l’exemple d’un intervalle de 10 minutes. Étant donné que les exemples sont enregistrées toutes les 30 secondes dans un intervalle de temps de 10 minutes, hello maximale nombre total d’exemples qui sont enregistrés par le traitement par lots serait 20 échantillons (2 par minute). Toutefois, en raison de la latence inhérente de toohello Hello reporting mécanisme et autres problèmes dans Azure, il peut être uniquement 15 échantillons sont la formule de mise à l’échelle tooyour disponibles pour la lecture. Par conséquent, par exemple, pendant cette période de 10 minutes, qu’à 75 % du nombre total de hello d’échantillons enregistré peut être tooyour disponibles formule.

**Méthode GetSample() et plages d’échantillons**

Vos formules de mise à l’échelle sont augmente de toobe continu et la réduction de vos pools &mdash; Ajout de nœuds ou la suppression de nœuds. Étant donné que les nœuds de coûtent pour vous, vous souhaitez tooensure vos formules utilisent une méthode intelligente d’analyse est basée sur des données suffisantes. Par conséquent, nous vous recommandons d’utiliser une analyse des types de tendance dans vos formules. Ce type augmente ou réduit vos pools en fonction d’une plage d’échantillons collectés.

toodo donc utiliser `GetSample(interval look-back start, interval look-back end)` tooreturn un vecteur d’échantillons :

```
$runningTasksSample = $RunningTasks.GetSample(1 * TimeInterval_Minute, 6 * TimeInterval_Minute);
```

Hello au-dessus de la ligne est évaluée par lot, il renvoie une plage d’échantillons comme un vecteur de valeurs. Par exemple :

```
$runningTasksSample=[1,1,1,1,1,1,1,1,1,1];
```

Une fois que vous avez collecté vecteur hello d’échantillons, vous pouvez ensuite utiliser des fonctions telles que `min()`, `max()`, et `avg()` tooderive des valeurs significatives à partir de hello collectées plage.

Pour renforcer la sécurité, vous pouvez forcer une toofail d’évaluation de formule si inférieur à un certain pourcentage de l’exemple est disponible pour une période donnée. Lorsque vous forcez une toofail d’évaluation de formule, vous indiquez à toocease lot davantage l’évaluation de la formule de hello si hello spécifié pourcentage d’échantillons n’est pas disponible. Dans ce cas, aucune modification n’est apportée toohello taille du pool. toospecify un pourcentage obligatoire d’échantillons pour hello évaluation toosucceed, spécifiez-le comme hello troisième paramètre trop`GetSample()`. Dans l’exemple ci-dessous, une exigence de 75 pour cent d’échantillons est spécifiée :

```
$runningTasksSample = $RunningTasks.GetSample(60 * TimeInterval_Second, 120 * TimeInterval_Second, 75);
```

Car il peut y avoir un délai dans la disponibilité d’exemple, il est important de tooalways spécifier une plage de temps avec une heure de début de l’aspect différée est antérieure à une minute. Il prend environ une minute pour toopropagate exemples via le système de hello, par conséquent, des exemples dans la plage de hello `(0 * TimeInterval_Second, 60 * TimeInterval_Second)` ne peuvent pas être disponibles. Là encore, vous pouvez utiliser le paramètre de pourcentage hello de `GetSample()` tooforce une exigence de pourcentage exemple spécifique.

> [!IMPORTANT]
> Nous vous **conseillons fortement** **d’éviter de vous appuyer *uniquement* sur `GetSample(1)` dans vos formules de mise à l’échelle automatique**, C’est parce que `GetSample(1)` essentiellement indique que le service de traitement par lots toohello, « Donnent me hello dernier échantillon avoir, quel que soit le temps écoulé de récupérer. » Dans la mesure où il est uniquement un échantillon unique, et il peut être un exemple plus anciens, peut-être pas représentatif d’image hello des tâches récentes ou l’état de la ressource. Si vous utilisez `GetSample(1)`, assurez-vous qu’il fait partie d’une instruction supérieure et pas hello seul point de données qui dépend de votre formule.
>
>

## <a name="metrics"></a>Mesures
Vous pouvez utiliser à la fois les mesures de ressources et de tâches quand vous définissez une formule. Vous ajustez le nombre de cible de hello de nœuds dédiés dans le pool hello en fonction des données de métriques hello vous procurer et d’évaluez. Consultez hello [Variables](#variables) section ci-dessus pour plus d’informations sur chaque métrique.

<table>
  <tr>
    <th>Mesure</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><b>Ressource</b></td>
    <td><p>Métriques de ressources sont basés sur hello UC, la bande passante hello, utilisation de la mémoire hello de nœuds de calcul et hello du nombre de nœuds.</p>
        <p> Ces variables définies par le service sont utiles pour effectuer des ajustements en fonction du nombre de nœuds :</p>
    <p><ul>
            <li>$TargetDedicatedNodes</li>
            <li>$TargetLowPriorityNodes</li>
            <li>$CurrentDedicatedNodes</li>
            <li>$CurrentLowPriorityNodes</li>
            <li>$preemptedNodeCount</li>
            <li>$SampleNodeCount</li>
    </ul></p>
    <p>Ces variables définies par le service sont utilisées pour effectuer des ajustements en fonction de l’utilisation des ressources du nœud :</p>
    <p><ul>
      <li>$CPUPercent</li>
      <li>$WallClockSeconds</li>
      <li>$MemoryBytes</li>
      <li>$DiskBytes</li>
      <li>$DiskReadBytes</li>
      <li>$DiskWriteBytes</li>
      <li>$DiskReadOps</li>
      <li>$DiskWriteOps</li>
      <li>$NetworkInBytes</li>
      <li>$NetworkOutBytes</li></ul></p>
  </tr>
  <tr>
    <td><b>Tâche</b></td>
    <td><p>Métriques de tâche sont basés sur l’état de hello de tâches, comme actif, en attente et s’est terminées. Hello défini par le service variables suivantes sont utiles pour effectuer les modifications de taille de pool basées sur les mesures de tâche :</p>
    <p><ul>
      <li>$ActiveTasks</li>
      <li>$RunningTasks</li>
      <li>$PendingTasks</li>
      <li>$SucceededTasks</li>
            <li>$FailedTasks</li></ul></p>
        </td>
  </tr>
</table>

## <a name="write-an-autoscale-formula"></a>Écrire une formule de mise à l’échelle automatique
Vous générez une formule de mise à l’échelle par formation d’instructions qui utilisent hello au-dessus de composants, puis combinez ces instructions dans une formule complète. Dans cette section, nous allons créer un exemple de formule capable de prendre des décisions concrètes en matière de mise à l’échelle automatique.

Tout d’abord, nous allons définir les exigences de hello pour notre nouvelle formule de mise à l’échelle. formule de Hello doit :

1. Augmenter le nombre de cibles de hello dédié de nœuds de calcul dans un pool si l’utilisation du processeur est élevée.
2. Réduire le nombre de cibles de hello dédié de nœuds de calcul dans un pool lors de l’utilisation du processeur est faible.
3. Toujours limiter nombre maximal de hello de nœuds dédié too400.

nombre de hello tooincrease de nœuds lors de l’utilisation élevée du processeur, définir l’instruction hello qui remplit une variable définie par l’utilisateur (`$totalDedicatedNodes`) avec une valeur qui est de 110 % de hello cible nombre actuel de nœuds dédiés, mais uniquement si hello minimale utilisation moyenne du processeur au cours de hello les 10 dernières minutes était supérieure à 70 %. Sinon, utilisez hello valeur pour le nombre actuel de hello de nœuds dédiés.

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
```

trop*diminuer* hello du nombre de nœuds dédiés lors de l’utilisation du processeur basse, hello l’instruction suivante dans notre hello de jeux de formules même `$totalDedicatedNodes` % too90 variable de hello cible nombre actuel de nœuds dédiés si hello utilisation moyenne du processeur Bonjour dernières minutes 60 a été sous 20 pour cent. Sinon, utilisez la valeur actuelle de hello de `$totalDedicatedNodes` que nous avons rempli dans l’instruction hello ci-dessus.

```
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
```

Maintenant limite hello cible le nombre maximum de tooa de nœuds de calcul dédié de 400 :

```
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

Voici la formule complète de hello :

```
$totalDedicatedNodes =
    (min($CPUPercent.GetSample(TimeInterval_Minute * 10)) > 0.7) ?
    ($CurrentDedicatedNodes * 1.1) : $CurrentDedicatedNodes;
$totalDedicatedNodes =
    (avg($CPUPercent.GetSample(TimeInterval_Minute * 60)) < 0.2) ?
    ($CurrentDedicatedNodes * 0.9) : $totalDedicatedNodes;
$TargetDedicatedNodes = min(400, $totalDedicatedNodes)
```

## <a name="create-an-autoscale-enabled-pool-with-net"></a>Créer un pool avec mise à l’échelle automatique dans .NET

toocreate un pool avec l’échelle automatique activée dans .NET, procédez comme suit :

1. Créer le pool hello avec [BatchClient.PoolOperations.CreatePool](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.createpool).
2. Ensemble hello [CloudPool.AutoScaleEnabled](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleenabled) propriété trop`true`.
3. Ensemble hello [CloudPool.AutoScaleFormula](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula) propriété avec la formule de mise à l’échelle.
4. (Facultatif) Ensemble hello [CloudPool.AutoScaleEvaluationInterval](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval) propriété (valeur par défaut est 15 minutes).
5. Valider le pool hello avec [CloudPool.Commit](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commit) ou [CommitAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.commitasync).

Hello extrait de code suivant crée un pool de mise à l’échelle dans .NET. Hello formule de mise à l’échelle du pool définit nombre cible de hello de too5 nœuds dédié lundi et 1 sur tous les jours de semaine de hello. Hello [intervalle de mise à l’échelle automatique](#automatic-scaling-interval) est définie too30 minutes. Dans ce et hello autres extraits de code c# dans cet article, `myBatchClient` est une instance initialisée correctement de hello [BatchClient] [ net_batchclient] classe.

```csharp
CloudPool pool = myBatchClient.PoolOperations.CreatePool(
                    poolId: "mypool",
                    virtualMachineSize: "small", // single-core, 1.75 GB memory, 225 GB disk
                    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));    
pool.AutoScaleEnabled = true;
pool.AutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";
pool.AutoScaleEvaluationInterval = TimeSpan.FromMinutes(30);
await pool.CommitAsync();
```

> [!IMPORTANT]
> Lorsque vous créez un pool de mise à l’échelle, ne spécifiez pas hello _targetDedicatedComputeNodes_ paramètre ou hello _targetLowPriorityComputeNodes_ paramètre sur hello appeler trop **CreatePool**. Au lieu de cela, spécifiez hello **AutoScaleEnabled** et **AutoScaleFormula** propriétés sur le pool de hello. valeurs Hello pour ces propriétés déterminent le nombre de cible de hello de chaque type de nœud. En outre, toomanually redimensionner un pool de mise à l’échelle (par exemple, avec [BatchClient.PoolOperations.ResizePoolAsync][net_poolops_resizepoolasync]), d’abord **désactiver** mise à l’échelle automatique sur Hello pool, puis redimensionnez-le.
>
>

En outre tooBatch .NET, vous pouvez utiliser une des hello autres [kits de développement logiciel lot](batch-apis-tools.md#azure-accounts-for-batch-development), [lot reste](https://docs.microsoft.com/rest/api/batchservice/), [applets de commande PowerShell de lot](batch-powershell-cmdlets-get-started.md)et hello [lot CLI](batch-cli-get-started.md)tooconfigure échelle.


### <a name="automatic-scaling-interval"></a>Intervalle de mise à l’échelle automatique
Par défaut, hello service Batch ajuste la taille d’un pool en fonction de tooits formule de mise à l’échelle toutes les 15 minutes. Cet intervalle est configurable à l’aide de hello pool propriétés suivantes :

* [CloudPool.AutoScaleEvaluationInterval][net_cloudpool_autoscaleevalinterval] (Batch .NET)
* [autoScaleEvaluationInterval][rest_autoscaleinterval] (API REST)

intervalle minimal de Hello est de cinq minutes et hello maximale est 168 heures. Si un intervalle en dehors de cette plage est spécifié, hello service Batch retourne une erreur demande incorrecte (400).

> [!NOTE]
> Échelle n’est pas actuellement prévue toorespond toochanges en moins d’une minute, mais au lieu de cela est prévu taille de hello tooadjust de votre pool progressivement lorsque vous exécutez une charge de travail.
>
>

## <a name="enable-autoscaling-on-an-existing-pool"></a>Activer la mise à l’échelle automatique sur un pool existant

Chaque lot fournit une échelle tooenable de façon automatique. Par exemple :

* [BatchClient.PoolOperations.EnableAutoScaleAsync][net_enableautoscaleasync] (Batch .NET)
* [Activer la mise à l’échelle automatique sur un pool][rest_enableautoscale] (API REST)

Lorsque vous activez l’échelle sur un pool existant, gardez Bonjour l’esprit les points suivants :

* Si la mise à l’échelle automatique est actuellement désactivée sur le pool de hello lorsque vous émettez hello demande tooenable échelle, vous devez spécifier une formule de mise à l’échelle valide lors de l’exécution de la demande de hello. Vous pouvez éventuellement spécifier un intervalle d’évaluation de mise à l’échelle automatique. Si vous ne spécifiez pas un intervalle, la valeur par défaut de hello de 15 minutes est utilisé.
* Si l’échelle automatique est actuellement activée sur hello pool, vous pouvez spécifier une formule de mise à l’échelle, un intervalle d’évaluation ou les deux. Vous devez spécifier au moins l’une de ces propriétés.

  * Si vous spécifiez un nouvel intervalle d’évaluation de mise à l’échelle, puis le calendrier d’évaluation existant de hello est arrêté et une planification est démarrée. du Hello nouvelle planification démarrage hello time est à quels hello demande tooenable échelle a été émis.
  * Si vous omettez soit intervalle de formule ou d’évaluation de la mise à l’échelle hello, hello service Batch continue la valeur actuelle de hello toouse de ce paramètre.

> [!NOTE]
> Si vous avez spécifié des valeurs pour hello *targetDedicatedComputeNodes* ou *targetLowPriorityComputeNodes* paramètres Hello **CreatePool** lorsque vous avez créé hello (méthode) pool dans .NET, ou pour les paramètres de comparables hello dans une autre langue, alors ces valeurs sont ignorées lorsque hello automatique de mise à l’échelle de formule est évaluée.
>
>

Cet extrait de code c# utilise hello [Batch .NET] [ net_api] échelle tooenable de bibliothèque sur un pool existant :

```csharp
// Define hello autoscaling formula. This formula sets hello target number of nodes
// too5 on Mondays, and 1 on every other day of hello week
string myAutoScaleFormula = "$TargetDedicatedNodes = (time().weekday == 1 ? 5:1);";

// Set hello autoscale formula on hello existing pool
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myAutoScaleFormula);
```

### <a name="update-an-autoscale-formula"></a>Mettre à jour une formule de mise à l’échelle automatique

formule de hello tooupdate sur un activée à la mise à l’échelle pool existant, appel hello opération tooenable échelle à nouveau avec la nouvelle formule de hello. Par exemple, si l’échelle automatique est déjà activé sur `myexistingpool` lorsque hello suivant le code .NET est exécuté, sa formule de mise à l’échelle est remplacé par contenu hello de `myNewFormula`.

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleFormula: myNewFormula);
```

### <a name="update-hello-autoscale-interval"></a>Intervalle de mise à l’échelle hello mise à jour

intervalle d’évaluation mise à l’échelle tooupdate hello d’un activée à la mise à l’échelle pool existant, appel hello opération tooenable échelle à nouveau avec le nouvel intervalle de hello. Par exemple, tooset hello mise à l’échelle d’évaluation intervalle too60 minutes pour un pool est déjà activé mise à l’échelle dans .NET :

```csharp
await myBatchClient.PoolOperations.EnableAutoScaleAsync(
    "myexistingpool",
    autoscaleEvaluationInterval: TimeSpan.FromMinutes(60));
```

## <a name="evaluate-an-autoscale-formula"></a>Évaluer une formule de mise à l’échelle automatique

Vous pouvez évaluer une formule avant de l’appliquer tooa pool. De cette façon, vous pouvez tester les toosee formule hello comment ses instructions évaluent avant de passer de la formule de hello en production.

tooevaluate une formule de mise à l’échelle, vous devez d’abord activer l’échelle sur pool hello avec une formule valide. tootest une formule sur un pool qui ne dispose pas encore échelle automatique est activée, une ligne hello utiliser une formule `$TargetDedicatedNodes = 0` lorsque vous activez pour la première échelle. Ensuite, utilisez une des hello suivant tooevaluate hello formule tootest :

* [BatchClient.PoolOperations.EvaluateAutoScale](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscale) ou [EvaluateAutoScaleAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.evaluateautoscaleasync)

    Ces méthodes de traitement par lots .NET requièrent des ID de hello d’un pool existant et une chaîne contenant tooevaluate formule de mise à l’échelle hello.

* [Évaluer une formule de mise à l’échelle automatique](https://docs.microsoft.com/rest/api/batchservice/evaluate-an-automatic-scaling-formula)

    Dans cette demande d’API REST, spécifiez l’ID du pool hello Bonjour URI et hello formule de mise à l’échelle Bonjour *autoScaleFormula* élément hello du corps de demande. réponse Hello d’opération de hello contient toutes les informations d’erreur qui peuvent être associées toohello formule.

Dans cet extrait de code [Batch .NET][net_api], nous évaluons une formule de mise à l’échelle automatique. Si le pool de hello n’a pas l’échelle automatique activée, nous activez-la tout d’abord.

```csharp
// First obtain a reference tooan existing pool
CloudPool pool = await batchClient.PoolOperations.GetPoolAsync("myExistingPool");

// If autoscaling isn't already enabled on hello pool, enable it.
// You can't evaluate an autoscale formula on non-autoscale-enabled pool.
if (pool.AutoScaleEnabled == false)
{
    // We need a valid autoscale formula tooenable autoscaling on the
    // pool. This formula is valid, but won't resize hello pool:
    await pool.EnableAutoScaleAsync(
        autoscaleFormula: "$TargetDedicatedNodes = {pool.CurrentDedicatedNodes};",
        autoscaleEvaluationInterval: TimeSpan.FromMinutes(5));

    // Batch limits EnableAutoScaleAsync calls tooonce every 30 seconds.
    // Because we want tooapply our new autoscale formula below if it
    // evaluates successfully, and we *just* enabled autoscaling on
    // this pool, we pause here tooensure we pass that threshold.
    Thread.Sleep(TimeSpan.FromSeconds(31));

    // Refresh hello properties of hello pool so that we've got the
    // latest value for AutoScaleEnabled
    await pool.RefreshAsync();
}

// We must ensure that autoscaling is enabled on hello pool prior to
// evaluating a formula
if (pool.AutoScaleEnabled == true)
{
    // hello formula tooevaluate - adjusts target number of nodes based on
    // day of week and time of day
    string myFormula = @"
        $curTime = time();
        $workHours = $curTime.hour >= 8 && $curTime.hour < 18;
        $isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
        $isWorkingWeekdayHour = $workHours && $isWeekday;
        $TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
    ";

    // Perform hello autoscale formula evaluation. Note that this code does not
    // actually apply hello formula toohello pool.
    AutoScaleRun eval =
        await batchClient.PoolOperations.EvaluateAutoScaleAsync(pool.Id, myFormula);

    if (eval.Error == null)
    {
        // Evaluation success - print hello results of hello AutoScaleRun.
        // This will display hello values of each variable as evaluated by the
        // autoscale formula.
        Console.WriteLine("AutoScaleRun.Results: " +
            eval.Results.Replace("$", "\n    $"));

        // Apply hello formula toohello pool since it evaluated successfully
        await batchClient.PoolOperations.EnableAutoScaleAsync(pool.Id, myFormula);
    }
    else
    {
        // Evaluation failed, output hello message associated with hello error
        Console.WriteLine("AutoScaleRun.Error.Message: " +
            eval.Error.Message);
    }
}
```

Évaluation réussie de formule hello indiqué dans cet extrait de code produit des résultats similaires à :

```
AutoScaleRun.Results:
    $TargetDedicatedNodes=10;
    $NodeDeallocationOption=requeue;
    $curTime=2016-10-13T19:18:47.805Z;
    $isWeekday=1;
    $isWorkingWeekdayHour=0;
    $workHours=0
```

## <a name="get-information-about-autoscale-runs"></a>Obtenir des informations sur les exécutions de mise à l’échelle automatique

tooensure l’exécution de votre formule comme prévu, nous vous recommandons de vérifier régulièrement les résultats hello des exécutions d’échelle hello qui effectue le traitement par lots dans votre pool. toodo, get (ou Actualiser) un toohello de référence du pool, puis examinez les propriétés hello de mise à l’échelle de sa dernière exécution.

Dans .NET de lot, hello [CloudPool.AutoScaleRun](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscalerun) propriété possède plusieurs propriétés qui fournissent des informations sur hello dernière l’échelle automatique exécuter effectuées sur le pool de hello :

* [AutoScaleRun.Timestamp](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.timestamp)
* [AutoScaleRun.Results](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.results)
* [AutoScaleRun.Error](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.autoscalerun.error)

Bonjour API REST, hello [obtenir des informations sur un pool](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool) demande retourne des informations sur le pool de hello, qui inclut hello dernière l’échelle automatique, exécutez informations Bonjour [autoScaleRun](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-pool#bk_autrun) propriété.

Hello extrait de code c# suivant utilise hello Batch .NET bibliothèque tooprint plus d’informations sur l’échelle automatique dernière hello s’exécutent sur le pool _monpool_:

```csharp
await Cloud pool = myBatchClient.PoolOperations.GetPoolAsync("myPool");
Console.WriteLine("Last execution: " + pool.AutoScaleRun.Timestamp);
Console.WriteLine("Result:" + pool.AutoScaleRun.Results.Replace("$", "\n  $"));
Console.WriteLine("Error: " + pool.AutoScaleRun.Error);
```

Résultat de l’exemple Hello précédant l’extrait de code :

```
Last execution: 10/14/2016 18:36:43
Result:
  $TargetDedicatedNodes=10;
  $NodeDeallocationOption=requeue;
  $curTime=2016-10-14T18:36:43.282Z;
  $isWeekday=1;
  $isWorkingWeekdayHour=0;
  $workHours=0
Error:
```

## <a name="example-autoscale-formulas"></a>Exemples de formules de mise à l’échelle automatique
Examinons quelques formules qui montrent différentes manières tooadjust hello quantité des ressources de calcul dans un pool.

### <a name="example-1-time-based-adjustment"></a>Exemple 1 : ajustement en fonction du temps
Supposons que vous souhaitez que la taille du pool hello tooadjust en fonction de la journée hello de la semaine de hello et d’une heure. Cet exemple montre comment les tooincrease ou diminuer nombre de hello de nœuds Bonjour pool en conséquence.

formule de Hello obtient d’abord hello heure actuelle. S’il s’agit d’un jour de la semaine (1-5) et les heures de travail (too6 de 8 h 00 PM), taille de pool hello cible a la valeur too20 nœuds. Sinon, il a la valeur too10 nœuds.

```
$curTime = time();
$workHours = $curTime.hour >= 8 && $curTime.hour < 18;
$isWeekday = $curTime.weekday >= 1 && $curTime.weekday <= 5;
$isWorkingWeekdayHour = $workHours && $isWeekday;
$TargetDedicatedNodes = $isWorkingWeekdayHour ? 20:10;
```

### <a name="example-2-task-based-adjustment"></a>Exemple 2 : ajustement en fonction de la tâche
Dans cet exemple, la taille du pool hello est ajustée en fonction nombre hello de tâches dans la file d’attente hello. Les commentaires et les sauts de ligne sont acceptés dans les chaînes de formule.

```csharp
// Get pending tasks for hello past 15 minutes.
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
// If we have fewer than 70 percent data points, we use hello last sample point,
// otherwise we use hello maximum of last sample point and hello history average.
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1), avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// If number of pending tasks is not 0, set targetVM toopending tasks, otherwise
// half of current dedicated.
$targetVMs = $tasks > 0? $tasks:max(0, $TargetDedicatedNodes/2);
// hello pool size is capped at 20, if target VM value is more than that, set it
// too20. This value should be adjusted according tooyour use case.
$TargetDedicatedNodes = max(0, min($targetVMs, 20));
// Set node deallocation mode - keep nodes active only until tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-3-accounting-for-parallel-tasks"></a>Exemple 3 : comptabilisation des tâches parallèles
Cet exemple modifie la taille de pool de hello en fonction du nombre de hello de tâches. Cette formule prend également en hello de compte [MaxTasksPerComputeNode] [ net_maxtasks] valeur a été définie pour le pool de hello. Cette approche est particulièrement utile dans les situations où [l’exécution parallèle de tâches](batch-parallel-node-tasks.md) a été activée sur votre pool.

```csharp
// Determine whether 70 percent of hello samples have been recorded in hello past
// 15 minutes; if not, use last sample
$samples = $ActiveTasks.GetSamplePercent(TimeInterval_Minute * 15);
$tasks = $samples < 70 ? max(0,$ActiveTasks.GetSample(1)) : max( $ActiveTasks.GetSample(1),avg($ActiveTasks.GetSample(TimeInterval_Minute * 15)));
// Set hello number of nodes tooadd tooone-fourth hello number of active tasks (the
// MaxTasksPerComputeNode property on this pool is set too4, adjust this number
// for your use case)
$cores = $TargetDedicatedNodes * 4;
$extraVMs = (($tasks - $cores) + 3) / 4;
$targetVMs = ($TargetDedicatedNodes + $extraVMs);
// Attempt toogrow hello number of compute nodes toomatch hello number of active
// tasks, with a maximum of 3
$TargetDedicatedNodes = max(0,min($targetVMs,3));
// Keep hello nodes active until hello tasks finish
$NodeDeallocationOption = taskcompletion;
```

### <a name="example-4-setting-an-initial-pool-size"></a>Exemple 4 : définition d’une taille de pool initiale
Cet exemple montre d’extrait de code dans une formule de mise à l’échelle qui définit le code c# hello tooa de taille de pool spécifié le nombre de nœuds pour une période initiale. Puis il ajuste la taille du pool hello en fonction du nombre de hello en cours d’exécution et les tâches actives après hello initiale laps de temps écoulé.

formule Hello Bonjour suivant extrait de code :

* Définit le pool initial de hello nœuds toofour de taille.
* N’ajuste pas taille du pool hello dans hello 10 premières minutes de cycle de vie du pool hello.
* Après 10 minutes, obtient la valeur max hello hello active et du numéro de l’exécution tâches au sein de hello dernières de 60 minutes.
  * Si les deux valeurs sont 0 (ce qui indique qu’aucune tâche n’étaient en cours d’exécution ou active Bonjour 60 dernières minutes), taille du pool hello a la valeur too0.
  * Si l’une des valeurs est supérieure à zéro, aucune modification n’est apportée.

```csharp
string now = DateTime.UtcNow.ToString("r");
string formula = string.Format(@"
    $TargetDedicatedNodes = {1};
    lifespan         = time() - time(""{0}"");
    span             = TimeInterval_Minute * 60;
    startup          = TimeInterval_Minute * 10;
    ratio            = 50;

    $TargetDedicatedNodes = (lifespan > startup ? (max($RunningTasks.GetSample(span, ratio), $ActiveTasks.GetSample(span, ratio)) == 0 ? 0 : $TargetDedicatedNodes) : {1});
    ", now, 4);
```

## <a name="next-steps"></a>Étapes suivantes
* [Optimiser l’utilisation des ressources calcul Azure Batch avec les tâches simultanées nœud](batch-parallel-node-tasks.md) contient des détails sur la façon dont vous pouvez exécuter plusieurs tâches simultanément sur les nœuds de calcul hello dans votre pool. En outre tooautoscaling, cette fonctionnalité peut aider à durée du travail toolower pour certaines charges de travail, vous épargner.
* Pour une autre amélioration de l’efficacité, assurez-vous que votre application, des requêtes par lots hello service Batch Bonjour la plupart de façon optimale. Consultez [interroger le service de traitement par lots Azure hello efficacement](batch-efficient-list-queries.md) toolearn comment toolimit hello la quantité de données qui transitent par câble de hello lorsque vous interrogez l’état hello de milliers de calcul nœuds ou des tâches.

[net_api]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch
[net_batchclient]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.batchclient
[net_cloudpool_autoscaleformula]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleformula
[net_cloudpool_autoscaleevalinterval]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.autoscaleevaluationinterval
[net_enableautoscaleasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.enableautoscaleasync
[net_maxtasks]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool.maxtaskspercomputenode
[net_poolops_resizepoolasync]: https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.pooloperations.resizepoolasync

[rest_api]: https://docs.microsoft.com/rest/api/batchservice/
[rest_autoscaleformula]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_autoscaleinterval]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
[rest_enableautoscale]: https://docs.microsoft.com/rest/api/batchservice/enable-automatic-scaling-on-a-pool
