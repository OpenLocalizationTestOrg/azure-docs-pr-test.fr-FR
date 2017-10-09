---
title: "les instructions de réglage des performances de données Lake Store Storm aaaAzure | Documents Microsoft"
description: "Recommandations en matière d’optimisation des performances d’Azure Data Lake Store Storm"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 5412fd46cf2373f5877030913df4fe1fc6f5473a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-storm-on-hdinsight-and-azure-data-lake-store"></a>Recommandations en matière d’optimisation des performances pour Storm sur HDInsight et Azure Data Lake Store

Comprendre les facteurs hello à prendre en compte lorsque vous paramétrez performances hello d’une topologie de Azure Storm. Par exemple, il s’agit de caractéristiques de hello toounderstand important de travail hello par becs verseurs de hello et boulons hello (si travail de hello est d’e/s ou mémoire). Cet article aborde diverses recommandations d’optimisation des performances, y compris la résolution des problèmes courants.

## <a name="prerequisites"></a>Composants requis

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Un compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de voir d’un seul, toocreate [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md).
* **Un cluster Azure HDInsight** avec accès tooa compte Data Lake Store. Voir [Créer un cluster HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Assurez-vous que vous activez Bureau à distance de cluster de hello.
* **Exécution d’un cluster Storm sur Data Lake Store**. Pour plus d’informations, consultez [Présentation d’Apache Storm sur HDInsight : analyse en temps réel pour Hadoop](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-overview).
* **Recommandations en matière d’optimisation des performances sur Data Lake Store**.  Pour les concepts généraux sur les performances, consultez [Recommandations en matière d’optimisation des performances pour Azure Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance).  

## <a name="tune-hello-parallelism-of-hello-topology"></a>Paramétrer le parallélisme hello de topologie de hello

Vous pouvez être tooimprove en mesure des performances par l’accès simultané de hello croissante de tooand d’e/s de hello depuis Data Lake Store. Une topologie Storm possède un ensemble de configurations qui déterminent le parallélisme de hello :
* Nombre de processus de travail (travailleurs de hello sont équitablement distribuées entre hello machines virtuelles).
* Nombre d’instances d’exécuteur de Spout.
* Nombre d’instances d’exécuteur de Bolt.
* Nombre de tâches de Spout.
* Nombre de tâches de Bolt.

Par exemple, sur un cluster avec 4 machines virtuelles et 4 processus de travail, les exécuteurs de bec 32 et 32 bec de tâches et les exécuteurs éclair 256 et tâches d’éclair 512, tenez compte des éléments suivants de hello :

Chaque superviseur, qui est un nœud Worker, a un seul processus Worker de machine virtuelle Java. Ce processus de machine virtuelle Java gère 4 threads de Spout et 64 threads de Bolt. Au sein de chaque thread, les tâches sont exécutées séquentiellement. Chaque thread bec a 1 tâche hello précédant la configuration, et chaque thread éclair a 2 tâches.

Dans Storm, voici hello divers composants impliqués, et comment ils affectent niveau hello de parallélisme, que vous devez :
* nœud principal de Hello (appelée Nimbus dans Storm) est utilisé toosubmit et gérer des tâches. Ces nœuds n’ont aucun impact sur le degré de hello de parallélisme.
* nœuds superviseur Hello. Dans HDInsight, il s’agit de nœud de travail tooa machine virtuelle Azure.
* tâches de travail Hello sont des processus Storm en cours d’exécution dans des machines virtuelles de hello. Chaque tâche de travail correspond l’instance de machine virtuelle Java tooa. Storm distribue le nombre de hello de processus de travail vous spécifiez des nœuds de travail toohello d’une façon aussi équilibrée que possible.
* Instances d’exécuteur de Spout et de Bolt. Chaque instance d’exécuteur correspond thread tooa qui s’exécutent dans le processus de travail hello (JVM).
* Tâches de Storm. Il s’agit des tâches logiques exécutées par chacun de ces threads. Cela ne modifie pas le niveau de hello de parallélisme, vous devez évaluer si vous avez besoin de plusieurs tâches par l’exécuteur ou non.

### <a name="get-hello-best-performance-from-data-lake-store"></a>Obtenir des performances optimales hello Data Lake Store

Lorsque vous utilisez Data Lake Store, vous obtenez des performances optimales hello si vous hello suivant :
* Fusionnez vos petits éléments dans des tailles supérieures (idéalement 4 Mo).
* Effectuez autant de requêtes simultanées que vous le pouvez. Étant donné que chaque thread éclair effectue un blocage de lectures, vous souhaitez toohave quelque part dans la plage de hello de threads de 8 à 12 par cœur. Cela permet de conserver hello hello de carte réseau et d’utilisation de processeur correctement. Une machine virtuelle plus grande permet d’avoir plus de demandes simultanées.  

### <a name="example-topology"></a>Exemple de topologie

Supposons que vous disposez d’un cluster de 8 nœuds Worker avec une machine virtuelle Azure D13v2. Cet ordinateur virtuel a 8 cœurs, donc entre hello 8 nœuds de travail, vous avez 64 cœurs total.

Supposons que nous utilisons 8 threads bolt par cœur. Avec 64 cœurs, nous voulons 512 instances (c’est-à-dire les threads) d’exécuteur de Bolt au total. Dans ce cas, supposons que nous commencer par une machine virtuelle Java par machine virtuelle et principalement utiliser hello thread l’accès concurrentiel au sein de la concurrence de tooachieve hello JVM. Cela signifie que nous avons besoins de 8 tâches worker (une par machine virtuelle Azure) et 512 exécuteurs bolt. Avec cette configuration, Storm tente de traitements de hello toodistribute uniformément entre les nœuds de travail (également connu sous les nœuds de superviseur), en donnant à chaque nœud de travail 1 machine virtuelle Java. Maintenant dans, par exemple hello Storm tente des exécuteurs de hello toodistribute uniformément entre les superviseurs, donnant chaque responsable (autrement dit, JVM) 8 threads chacun.

## <a name="tune-additional-parameters"></a>Ajuster les paramètres supplémentaires
Une fois que vous avez la topologie de base hello, vous pouvez envisager si vous souhaitez que tootweak un des paramètres de hello :
* **Number of JVMs per worker node (Nombre de machines virtuelles Java par nœud Worker).** Si vous avez une structure de données de grande taille (par exemple, une table de recherche) que vous hébergez dans la mémoire, chaque machine virtuelle Java requiert une copie distincte. Vous pouvez également utiliser structure de données hello entre le nombre de threads si vous avez moins de JVM. Pour d’e/s d’éclair hello, nombre hello de JVM ne fait pas de différence en tant que nombre de hello de threads ajouté entre ces JVM. Par souci de simplicité, il s’agit d’un toohave conseillé une machine virtuelle Java par travail. Selon ce que fait votre éclair ou l’application de traitement vous nécessite, cependant, vous devrez peut-être toochange ce nombre.
* **Number of spout executors (Nombre d’exécuteurs de Spout).** Comme hello exemple précédent utilise boulons pour l’écriture de tooData Lake Store, nombre hello de becs verseurs n’est pas performances d’éclair toohello directement pertinents. Toutefois, selon la quantité de hello de traitement ou d’e/s se produit dans bec de hello, il est judicieux tootune hello becs verseurs amovibles pour de meilleures performances. Assurez-vous que vous avez suffisamment boulons de hello becs verseurs toobe tookeep en mesure de disponibilité. taux de sortie Hello de becs verseurs de hello doivent correspondre au débit hello de hello boulons. dépend de la configuration réelle de Hello sur bec de hello.
* **Nombre de tâches.** Chaque Bolt s’exécute en tant que thread unique. Les tâches supplémentaires par Bolt n’apportent pas d’accès concurrentiel supplémentaire. Hello qu’ils sont utiles étant uniquement si votre processus d’accusé de réception hello tuple est une proportion élevée de temps d’exécution éclair. Il s’agit d’un toogroup conseillé de tuples dans un plus grand ajouter avant d’envoyer un accusé de réception à partir d’éclair de hello. Par conséquent, dans la plupart des cas, plusieurs tâches ne fournissent pas d’avantage supplémentaire.
* **Local or shuffle grouping (Groupage local ou aléatoire).** Lorsque ce paramètre est activé, les tuples sont envoyés toobolts dans hello même processus de travail. Cela réduit les communications entre processus et les appels réseau. Cela est recommandé pour la plupart des topologies.

Ce scénario de base est un bon point de départ. Test avec votre propre hello tootweak de données précédents paramètres tooachieve optimiser les performances.

## <a name="tune-hello-spout"></a>Régler hello bec

Vous pouvez modifier hello suivant paramètres tootune hello bec.

- **Délai d’expiration de tuple : topology.message.timeout.secs**. Ce paramètre détermine la durée hello toocomplete qu’un message emprunte et recevoir l’accusé de réception, avant d’être considérée a échoué.

- **Mémoire maximale par le processus worker : worker.childopts**. Ce paramètre vous permet de spécifier les paramètres de ligne de commande supplémentaires toohello Java travailleurs. Hello couramment utilisé paramètre ici est XmX, qui détermine le segment de mémoire hello mémoire maximale allouée tooa la machine virtuelle Java.

- **Nombre max. de spouts en attente : topology.max.spout.pending**. Ce paramètre détermine le nombre de hello de tuples qui peut être en vol (pas encore d’accusé de réception de tous les nœuds dans une topologie de hello) par bec thread à tout moment.

 Un calcul correct de toodo est la taille de hello de tooestimate de chacun de vos tuples. Ensuite, calculez la quantité de mémoire par thread spout. Hello mémoire totale allouée thread tooa, divisé par cette valeur, doit vous donner la limite supérieure de hello pour bec max de hello en attente de paramètre.

## <a name="tune-hello-bolt"></a>Régler hello éclair
Lorsque vous écrivez tooData Lake Store, définir une stratégie de synchronisation de taille (tampon côté client de hello) too4 Mo. Un vidage ou hsync() est ensuite effectuée uniquement lorsque la taille de mémoire tampon hello est hello à cette valeur. pilote de Data Lake Store Hello sur le travail de hello VM effectue automatiquement cette mise en mémoire tampon, sauf si vous effectuez explicitement un hsync().

éclair de données Lake Store Storm Hello par défaut a un paramètre de stratégie de la synchronisation de taille (fileBufferSize) peut être utilisé tootune ce paramètre.

Dans les topologies d’e/S intensives, il s’agit d’une bonne idée toohave chaque thread éclair écrire les fichiers propres tooits et tooset une stratégie de rotation des fichiers (fileRotationSize). Lorsque hello atteint une certaine taille, les flux hello sont vidé automatiquement et un nouveau fichier est écrit dans. Hello, taille de fichier pour la rotation recommandée est de 1 Go.

### <a name="handle-tuple-data"></a>Gérer les données de tuple

Dans Storm, un bec conserve sur tooa tuple jusqu'à ce qu’elle est acceptée explicitement par un éclair de hello. Si un tuple a été lu par un éclair de hello mais n’a pas encore été accepté, bec de hello ne peut pas avoir rendue persistante dans le back-end Data Lake Store. Après qu’un tuple est accepté, bec de hello peut être garanti la persistance par éclair de hello et source de données hello supprimez-les de quelque source qu’il lit à partir de.  

Pour obtenir des performances optimales sur Data Lake Store, ont éclair de hello 4 Mo de données de tuple de la mémoire tampon. Puis, écrivez toohello Data Lake Store précédent fin sous la forme d’une écriture de 4 Mo. Après les données de salutation a été correctement écrite toohello magasin (en appelant hflush()), éclair de hello peut accuser réception hello données toohello arrière bec. Il s’agit quel exemple hello boulon fournie n’ici. Il est également acceptable toohold un plus grand nombre de tuples avant hello hflush() appel est effectué et hello tuples d’accusé de réception. Toutefois, cela augmente le nombre de hello de tuples en vol que bec de hello doit toohold, et par conséquent, augmente hello la quantité de mémoire requise par la machine virtuelle Java.

> [!NOTE]
Applications peuvent avoir un tuples de tooacknowledge exigence plus fréquemment (à des tailles de données inférieure à 4 Mo) pour d’autres raisons de performances non. Toutefois, sont susceptibles d’affecter hello d’e/s de débit toohello stockage back-end. Évaluez ce compromis par rapport aux performances d’e/s d’éclair hello.

Si la vitesse d’entrée de tuples hello n’est pas élevé, afin de la mémoire tampon de 4 Mo hello prend un toofill beaucoup de temps, envisagez d’atténuation en :
* Réduisant le nombre de hello de boulons, il existe donc moins toofill de mémoires tampons.
* Ayant une stratégie basée sur le nombre ou heure, où une hflush() est déclenchée toutes les x vidages ou chaque millisecondes de y, et les tuples hello accumulés jusqu'à présent sont précédent.

Notez que le débit de hello dans ce cas est inférieure, mais avec un taux d’événements lent, débit maximal n’est pas hello plus grand objectif quand même. Ces solutions d’atténuation vous aider à réduire le temps total hello nécessaire pour un tooflow tuple via toohello store. Cela peut avoir une importance si vous souhaitez un pipeline en temps réel, même avec un taux d’événements faible. Notez également que si votre taux de tuple est faible, vous devez ajuster paramètre topology.message.timeout_secs hello pour les tuples hello n’expirent pas pendant qu’ils reçoivent en mémoire tampon ou traité.

## <a name="monitor-your-topology-in-storm"></a>Surveiller votre topologie dans Storm  
Pendant l’exécution de votre topologie, vous pouvez le surveiller dans l’interface utilisateur hello Storm. Voici toolook des principaux paramètres hello à :

* **Total process execution latency (Latence totale de l’exécution du processus).** Il s’agit de hello durée moyenne un tuple toobe émis par bec de hello, traité par un éclair de hello et d’accusé de réception.

* **Total bolt process latency (Latence totale du processus Bolt).** Il s’agit de temps moyen de hello passé par le tuple de hello à éclair de hello jusqu'à ce qu’il reçoit un accusé de réception.

* **Total bolt execute latency (Latence totale d’exécution de Bolt).** Il s’agit hello moyenne temps passé par un éclair hello Bonjour exécuter la méthode.

* **Nombre d’échecs.** Cela fait référence nombre toohello de tuples ayant échoué toobe complètement traité avant leur expiration du délai.

* **Capacité.** Il s’agit d’une mesure du niveau d’activité de votre système. Si ce nombre a la valeur 1, vos bolts fonctionnent aussi rapidement que possible. S’il est inférieur à 1, augmentez le parallélisme de hello. S’il est supérieur à 1, réduire le parallélisme de hello.

## <a name="troubleshoot-common-problems"></a>Résoudre les problèmes courants
Voici quelques scénarios courants de résolution des problèmes.
* **Grand nombre de tuples expirés.** Examinez chaque nœud hello topologie toodetermine où le goulot d’étranglement hello est. Hello plus souvent du est que hello boulons ne sont pas en mesure de tookeep haut avec becs verseurs de hello. Cela conduit tootuples objets mémoires tampons internes de hello lors toobe en attente traités. Envisagez d’augmenter la valeur de délai d’attente hello ou de diminution bec max de hello en attente.

* **Latence totale d’exécution de processus élevée, mais latence de traitement des Bolts faible.** Dans ce cas, il est possible que les tuples hello ne sont pas reçus suffisamment rapide. Vérifiez qu’il existe un nombre suffisant de validateurs. Une autre possibilité est qu’ils attendent dans la file d’attente hello trop longtemps avant hello boulons démarrer leur traitement. Diminuer bec max de hello en attente.

* **Latence d’exécution des Bolts élevée.** Cela signifie que méthode execute() hello votre éclair prend trop de temps. Optimiser le code hello, ou examiner les tailles d’écriture et comportement de vidage.

### <a name="data-lake-store-throttling"></a>Limitation Data Lake Store
Si vous avez atteint les limites de la bande passante fournie par Data Lake Store hello, vous pouvez rencontrer des échecs de la tâche. Consultez les journaux des tâches pour les erreurs de limitation. Vous pouvez réduire le parallélisme de hello en augmentant la taille du conteneur.    

toocheck si vous l’obtention de sont limités, activer le débogage hello journalisation côté client de hello :

1. Dans **Ambari** > **Storm** > **Config** > **avancé storm-travail-log4j**, modifier  **&lt;racine niveau = « info »&gt;**  trop**&lt;racine niveau = « debug »&gt;**. Redémarrez tous les nœuds/service hello pour effet de tootake configuration hello.
2. Moniteur hello Storm topologie ouvre une session sur les nœuds de travail (sous /var/log/storm/worker-artifacts /&lt;TopologyName&gt;/&lt;port&gt;/worker.log) pour les exceptions de limitation Data Lake Store.

## <a name="next-steps"></a>Étapes suivantes
Pour optimiser davantage les performances, consultez [ce blog](https://blogs.msdn.microsoft.com/shanyu/2015/05/14/performance-tuning-for-hdinsight-storm-and-microsoft-azure-eventhubs/).

Pour un toorun exemple supplémentaire, consultez [sur GitHub](https://github.com/hdinsight/storm-performance-automation).
