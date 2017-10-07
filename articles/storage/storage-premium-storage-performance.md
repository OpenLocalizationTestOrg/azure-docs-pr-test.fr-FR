---
title: 'Azure Premium Storage : conception sous le signe de la haute performance | Microsoft Docs'
description: "Concevoir des applications hautes performances avec Azure Premium Storage. Premium Storage offre une prise en charge très performante et à faible latence des disques pour les charges de travail utilisant beaucoup d'E/S exécutées sur les machines virtuelles Azure."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: e6a409c3-d31a-4704-a93c-0a04fdc95960
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: aungoo
ms.openlocfilehash: 75845eb4707e8e5606153a5e1a7c10b4113ee121
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-premium-storage-design-for-high-performance"></a>Azure Premium Storage : conception sous le signe de la haute performance
## <a name="overview"></a>Vue d'ensemble
Cet article fournit des instructions pour la création d’applications hautes performances avec Azure Premium Storage. Vous pouvez utiliser les instructions hello fournies dans ce document combiné avec des performances tootechnologies d’applicable meilleures de pratiques intégré utilisé par votre application. les instructions hello tooillustrate, nous avons utilisé SQL Server s’exécutant sur un stockage Premium, par exemple dans ce document.

Bien que nous indique les scénarios de performances pour la couche de stockage hello dans cet article, vous devez couche d’application toooptimize hello. Par exemple, si vous hébergez une batterie de serveurs SharePoint sur le stockage Azure Premium, vous pouvez utiliser les exemples de SQL Server hello à partir de ce serveur de base de données de l’article toooptimize hello. En outre, optimiser Web server hello SharePoint la batterie de serveurs et messages hello du serveur tooget Application la plupart des performances.

Cet article vous aidera à répondre à certaines questions courantes relatives à l’optimisation des performances applicatives sur Azure Premium Storage :

* Comment toomeasure les performances de votre application ?  
* Pourquoi n’obtenez-vous pas les hautes performances attendues ?  
* Quels sont les facteurs qui influencent les performances de votre application sur Premium Storage ?  
* Comment ces facteurs influencent-ils les performances de votre application sur Premium Storage ?  
* Comment optimiser les performances d’E/S par seconde, de bande passante et de latence ?  

Ces instructions vous sont spécifiquement fournies pour Premium Storage, car les charges de travail exécutées sur Premium Storage sont extrêmement sensibles aux performances. Nous vous proposons des exemples lorsque cela s’y prête. Vous pouvez également appliquer certaines de ces tooapplications instructions en cours d’exécution sur des machines virtuelles IaaS avec des disques de stockage Standard.

Avant de commencer, si vous êtes tooPremium nouveau stockage, tout d’abord lire hello [stockage Premium : stockage hautes performances pour les charges de travail de Machine virtuelle Azure](storage-premium-storage.md) et [évolutivité du stockage Azure et les objectifs de performances](storage-scalability-targets.md)articles.

## <a name="application-performance-indicators"></a>Indicateurs de performances d’une application
Nous évaluer si une application s’exécute correctement ou non à l’aide de performances telles que les indicateurs de la vitesse à laquelle une application traite une demande de l’utilisateur, la quantité de données est une application de traitement par la demande, le nombre de requêtes est une application de traitement dans un spécifique période de temps, la durée pendant laquelle qu'un utilisateur a toowait tooget une réponse après avoir soumis la demande. termes de techniques Hello pour ces indicateurs de performance sont, e/s, le débit ou la bande passante et la latence.

Dans cette section, nous aborderons les indicateurs de performance hello courantes dans le contexte de hello du stockage Premium. Bonjour, suivant la section, la collecte des exigences de l’Application, vous allez apprendre comment toomeasure ces indicateurs de performance pour votre application. Plus loin dans l’optimisation des performances des applications, vous découvrirez les facteurs de hello affectant ces toooptimize recommandations et les indicateurs de performance les.

## <a name="iops"></a>E/S par seconde
E/s est le nombre de demandes que votre application envoie toohello disques de stockage en une seconde. Une opération d’entrée/sortie peut être accessible en lecture ou écriture, et être séquentielle ou aléatoire. Les applications OLTP comme un site Web de vente au détail en ligne doivent tooprocess immédiatement des demandes de nombreux utilisateurs simultanés. Hello utilisateur sont Insérer et mettre à jour des transactions de bases de données intensif, l’application hello doit traiter rapidement. Les applications OLTP requièrent dont un nombre d’E/S par seconde très élevé. Ces applications gèrent des millions de demandes d’E/S petites et aléatoires. Si vous avez une telle application, vous devez concevoir hello application infrastructure toooptimize IOPS. Bonjour ultérieurement section *optimisation des performances des applications*, les sujets abordés en détail tous les facteurs hello dont vous devez tenir compte tooget e/s élevées.

Lorsque vous attachez une premium stockage disque tooyour à grande échelle machine virtuelle, Azure configure pour vous un garantie nombre d’IOPS conformément aux spécifications de disque hello. Par exemple, un disque P50 configure 7500 E/S par seconde. Chaque taille de machine virtuelle à grande échelle est également associée à une limite spécifique d’E/S par seconde qu’elle peut prendre en charge. Par exemple, une machine virtuelle GS5 Standard a une limite de 80 000 E/S par seconde.

## <a name="throughput"></a>Throughput
Débit ou la bande passante est hello que votre application est l’envoi des données toohello disques de stockage dans un intervalle spécifié. Si votre application effectue des opérations d’entrée/sortie avec des tailles d’unité d’E/S importantes, elle aura besoin d’un débit élevé. Applications d’entrepôt de données ont tendance à tooissue analyse opérations intensives d’accès à la fois des portions de données volumineuses et généralement les opérations en bloc. En d’autres termes, ces applications nécessitent un débit plus élevé. Si vous avez une telle application, vous devez concevoir son toooptimize infrastructure pour le débit. Dans la section suivante de hello, les sujets abordés dans les facteurs de hello détail vous devez paramétrer tooachieve cela.

Lorsque vous attachez une premium stockage disque tooa à grande échelle machine virtuelle, Azure configure débit conformément à la spécification de ce disque. Par exemple, un disque P50 configure un débit de disque de 250 Mo par seconde. Chaque taille de machine virtuelle à grande échelle est également associée à une limite spécifique de débit qu’elle peut prendre en charge. Par exemple, une machine virtuelle GS5 Standard a un débit maximal de 2 000 Mo par seconde. 

Il existe une relation entre un débit et des IOPS comme indiqué dans la formule hello ci-dessous.

![](media/storage-premium-storage-performance/image1.png)

Par conséquent, il est important toodetermine hello débit et des IOPS valeurs optimales que votre application requiert. Lorsque vous essaierez toooptimize une, hello autres obtient également affectée. Dans la section *Optimisation des performances applicatives*, nous aborderons plus en détail la question de l’optimisation des E/S par seconde et du débit.

## <a name="latency"></a>Latency
La latence est hello temps un tooreceive application une demande unique, envoyer des disques de stockage toohello et envoyer hello réponse toohello client. Il s’agit d’une mesure critique des performances d’une application dans Ajout tooIOPS et le débit. Hello latence d’un disque de stockage premium est temps hello prend les informations de hello tooretrieve pour une demande et à communiquer le retour tooyour application. Premium Storage offre de faibles latences. Si vous activez une mise en cache de l’hôte en lecture seule sur des disques de stockage premium, vous pourrez obtenir une latence de lecture bien plus faible. Nous aborderons la mise en cache du disque plus en détail dans la section *Optimisation des performances applicatives*.

Lorsque vous optimisez votre application tooget supérieur IOPS et le débit, cela affectera hello latence de votre application. Après le paramétrage des performances de l’application hello, évaluez toujours hello latence de hello application tooavoid comportement d’une latence élevée inattendue.

## <a name="gather-application-performance-requirements"></a>Collecte des exigences de performances de l’application
Hello première étape de conception d’applications hautes performances en cours d’exécution sur le stockage Azure Premium est, les exigences de performances toounderstand hello de votre application. Après avoir recueilli les exigences de performances, vous pouvez optimiser votre application tooachieve hello plus optimale.

Dans la section précédente de hello, nous avons expliqué hello commun les indicateurs de performance, IOPS, Throughput and Latency. Vous devez identifier laquelle de ces indicateurs de performance sont l’expérience utilisateur tooyour critiques application toodeliver hello souhaité. Par exemple, e/s élevées l'important la plupart des applications tooOLTP le traitement des millions de transactions en une seconde. En revanche, un débit élevé sera plus pertinent pour les applications d’entrepôt de données qui traitent de grandes quantités de données en une seconde. De même, une très faible latence sera cruciale pour les applications en temps réel, telles que les sites web de diffusion en continu de vidéo en direct.

Ensuite, mesurer les exigences de performances maximales hello de votre application tout au long de sa durée de vie. Utiliser la liste de vérification hello exemple ci-dessous comme un point de départ. Exigences de performances maximales hello enregistrement normale, les périodes de charge de travail des heures de pointe et les heures creuses. En identifiant les conditions requises pour tous les niveaux de charges de travail, vous serez en mesure de toodetermine hello des spécifications de performances globales de votre application. Par exemple, hello normal la charge de travail d’un site Web de commerce électronique sera transactions hello fait lors de la plupart des jours dans une année. une charge importante Hello du site Web de hello sera transactions hello fait pendant les vacances ou des événements de vente spéciale. une charge importante Hello est généralement expérimentée pendant une période limitée, mais peut nécessiter votre tooscale application deux ou plusieurs fois à son fonctionnement normal. Découvrez le centile de 50 hello, 90 centile et des exigences en termes de pourcentage 99. Cela permet de filtrer les valeurs hors norme dans les exigences de performances hello et vous pouvez vous concentrer vos efforts sur l’optimisation pour les valeurs hello.

**Liste de contrôle pour les exigences de performances de l’application**

| **Exigences de performances** | **50e percentile** | **90e percentile** | **99e percentile** |
| --- | --- | --- | --- |
| Bande passante Transactions par seconde | | | |
| % d’opérations de lecture | | | |
| % d’opérations d’écriture | | | |
| % d’opérations aléatoires | | | |
| % d’opérations séquentielles | | | |
| Taille de la demande d’E/S | | | |
| Débit moyen | | | |
| Bande passante Débit | | | |
| min. Latence | | | |
| Latence moyenne | | | |
| Bande passante UC | | | |
| Utilisation moyenne de l’UC | | | |
| Bande passante Mémoire | | | |
| Utilisation moyenne de la mémoire | | | |
| Profondeur de file d’attente | | | |

> [!NOTE]
> vous devez anticiper la mise à l’échelle de ces nombres en fonction de la croissance prévue de votre application. Il est un tooplan recommandé pour la croissance avance, car il peut être plus difficile infrastructure de hello toochange d’amélioration des performances plus tard.
>
>

Si vous possédez une application existante et que vous souhaitez toomove tooPremium stockage, tout d’abord créer de liste de vérification hello ci-dessus pour l’application existante hello. Ensuite, générez un prototype de votre application sur la conception et stockage Premium application hello selon les indications décrites dans *optimisation des performances des applications* dans une section ultérieure de ce document. Hello suivant décrit les outils hello vous pouvez utiliser des mesures de performances toogather hello.

Créer une liste de vérification tooyour existant application similaire pour le prototype de hello. À l’aide des outils de Benchmarking, vous pouvez simuler des charges de travail hello et mesurer les performances dans l’application hello prototype. Consultez la section de hello sur [Benchmarking](#benchmarking) toolearn plus. En procédant ainsi, vous pouvez déterminer si Premium Storage peut satisfaire ou dépasser les exigences de performances de votre application. Ensuite, vous pouvez implémenter hello les mêmes instructions pour votre application de production.

### <a name="counters-toomeasure-application-performance-requirements"></a>Compteurs de performances d’application toomeasure requises
Hello meilleures conditions de performances toomeasure moyen de votre application, outils d’analyse des performances toouse hello système d’exploitation du serveur de hello. Vous pouvez utiliser PerfMon pour Windows et iostat pour Linux. Ces outils capturent les compteurs de mesure tooeach correspondante est expliqué dans hello au-dessus de section. Vous devez capturer les valeurs de ces compteurs hello lorsque votre application s’exécute ses normal, les charges de travail de pointe et les heures creuses.

les compteurs PerfMon Hello sont disponibles pour le processeur, mémoire et, chaque disque logique et le disque physique de votre serveur. Lorsque vous utilisez des disques de stockage premium avec une machine virtuelle, sont des compteurs de disque physique hello pour chaque disque de stockage premium, et sont des compteurs de disque logique pour chaque volume créée sur des disques de stockage premium hello. Vous devez capturer les valeurs hello pour les disques hello qui hébergent votre charge de travail d’application. S’il existe un mappage tooone un entre les disques logiques et physiques, vous pouvez faire référence à des compteurs de disque toophysical ; dans le cas contraire, consultez les compteurs de disque logique toohello. Sur Linux, commande iostat de hello génère un rapport d’utilisation du processeur et disque. rapport d’utilisation du disque Hello fournit des statistiques par partition ou le périphérique physique. Si vous avez un serveur de base de données dont les données et les journaux résident sur des disques distincts, récupérez ces données pour les deux disques. Le tableau ci-dessous décrit les compteurs de disques, de processeur et de mémoire :

| Compteur | Description | PerfMon | Iostat |
| --- | --- | --- | --- |
| **Nombre d’E/S par seconde ou de transactions par seconde** |Nombre de demandes d’e/s émises disque de stockage toohello par seconde. |Nb d’opérations de lectures de disque/s  <br> Nb d’opération d’écriture de disque/s |tps  <br> r/s  <br> w/s |
| **Opérations de lecture et d’écriture de disque** |% de lectures et d’écrire des opérations effectuées sur le disque de hello. |% temps de lecture du disque  <br> % temps d’écriture du disque |r/s  <br> w/s |
| **Débit** |Quantité de données lues ou écrites toohello de disque par seconde. |Nb d’octets de lecture de disque/s  <br> Nb d’octets d’écriture de disque/s |kB_read/s <br> kB_wrtn/s |
| **Latence** |Nombre total de temps toocomplete une demande d’e/s de disque. |Temps de lecture moyen du disque/s  <br> Temps d’écriture moyen du disque/s |await  <br> svctm |
| **Taille d’E/S** |taille Hello de demandes d’e/s émet des disques de stockage toohello. |Nb moyen d’octets en lecture du disque  <br> Nb moyen d’octets en écriture du disque |avgrq-sz |
| **Profondeur de file d’attente** |Nombre d’e/s en suspens demandes en attente toobe à lire ou d’écriture de disque de stockage toohello. |Longueur de file d’attente actuelle du disque |avgqu-sz |
| **IOPS Mémoire** |Quantité de mémoire requise toorun application sans heurts |% d’octets dédiés utilisés |Use vmstat |
| **Bande passante UC** |Quantité du processeur requise toorun application sans heurts |% temps processeur |%util |

En savoir plus sur [iostat](http://linuxcommand.org/man_pages/iostat1.html) et [PerfMon](https://msdn.microsoft.com/library/aa645516.aspx).

## <a name="optimizing-application-performance"></a>Optimisation des performances applicatives
Hello principaux facteurs qui influencent les performances d’une application en cours d’exécution sur le stockage Premium sont de Nature de requêtes e/s, taille de machine virtuelle, la taille du disque, nombre de disques, la mise en cache du disque, le Multithreading et profondeur de file d’attente. Vous pouvez contrôler certains de ces facteurs avec les boutons fournis par le système de hello. La plupart des applications, vous obtenez un hello de tooalter option taille d’e/s et la profondeur de file d’attente directement. Par exemple, si vous utilisez SQL Server, vous ne pouvez pas choisir profondeur de file d’attente et de taille hello e/s. SQL Server choisit hello optimale d’e/s taille et la file d’attente profondeur valeurs tooget hello la plupart des performances. Il est important toounderstand les effets de hello des deux types de facteurs sur les performances de votre application, afin que vous pouvez prévoir les besoins en performances toomeet ressources appropriées.

Dans cette section, consultez toohello application aide-mémoire des conditions requises que vous avez créé, tooidentify combien vous devez toooptimize les performances de votre application. Selon que vous serez en mesure de toodetermine qui facteurs à partir de cette section, vous devez tootune. toowitness hello les effets de chaque facteur sur les performances de votre application, exécutez les outils de votre configuration de l’application des tests de performances. Consultez toohello [Benchmarking](#Benchmarking) section à fin hello de cet article pour toorun étapes courantes outils sur Windows et les machines virtuelles Linux des tests de performances.

### <a name="optimizing-iops-throughput-and-latency-at-a-glance"></a>Aperçu de l’optimisation des E/S, du débit et de la latence
Hello tableau ci-dessous résume tous les facteurs de performances hello et hello étapes toooptimize IOPS, débit et la latence. Hello sections suivant ce résumé décrit chaque facteur est beaucoup plus en détail.

| &nbsp; | **D’OPÉRATIONS D’E/S PAR SECONDE** | **Débit** | **Latence** |
| --- | --- | --- | --- |
| **Exemple de scénario** |Application OLTP d’entreprise nécessitant un taux très élevé de transactions par seconde. |Application d’entreposage de données d’entreprise traitant de grandes quantités de données. |Près des applications en temps réel nécessitant des demandes de toouser réponses instantanée, telles que les jeux en ligne. |
| Facteurs de performances | &nbsp; | &nbsp; | &nbsp; |
| **Taille d’E/S** |Une plus petite taille d’E/S génère un nombre d’E/S par seconde plus élevé. |Tooyields de taille d’e/s plus grand débit plus élevé. | &nbsp;|
| **Taille de la machine virtuelle** |Utilisez une taille de machine virtuelle qui offre un nombre d’E/S par seconde supérieur aux besoins de votre application. Voir ici les tailles de machine virtuelle et les limites d’E/S par seconde qui leur sont associées. |Utilisez une taille de machine virtuelle qui offre une limite de débit supérieure aux besoins de votre application. Voir ici les tailles de machine virtuelle et les limites de débit qui leur sont associées. |Utilisez une taille de machine virtuelle qui offre une limite de mise à l’échelle supérieure aux besoins de votre application. Voir ici les tailles de machine virtuelle et les limites qui leur sont associées. |
| **Taille du disque** |Utilisez une taille de disque qui offre un nombre d’E/S par seconde supérieur aux besoins de votre application. Voir ici les tailles de disque et les limites d’E/S par seconde qui leur sont associées. |Utilisez une taille de disque qui offre une limite de débit supérieure aux besoins de votre application. Vous trouverez ici les tailles de disque et les limites de débit qui leur sont associées. |Utilisez une taille de disque qui offre une limite de mise à l’échelle supérieure aux besoins de votre application. Vous trouverez ici les tailles de disque et les limites qui leur sont associées. |
| **Limites de mises à l’échelle des machines virtuelles et des disques** |Limite d’e/s de choisi de taille de machine virtuelle hello doit être supérieure à total IOPS dus à des disques de stockage premium attaché tooit. |Limite de débit de choisi de taille de machine virtuelle hello doit être supérieure à débit total dus à des disques de stockage premium attaché tooit. |Limites d’échelles de choisi de taille de machine virtuelle hello doivent être supérieurs à des limites d’échelle total premium attachés des disques de stockage. |
| **Mise en cache du disque** |Activer le Cache d’en lecture seule sur les disques de stockage premium avec tooget lourde d’opérations de lecture e/s de lecture plus élevée. | &nbsp; |Activer le Cache d’en lecture seule sur les disques de stockage premium avec des latences de lecture des opérations lourdes prêt tooget très faibles. |
| **Entrelacement de disques** |Utiliser plusieurs disques et les distribuer tooget ensemble un niveau d’IOPS supérieure combinée et limite de débit. Notez que hello limite combinée par machine virtuelle doit être supérieur à hello limites combinés des disques attachés premium. | &nbsp; | &nbsp; |
| **Taille de l’entrelacement** |Taille d’entrelacement plus petite pour les petits schémas d’E/S aléatoires associés aux applications OLTP. Utilisez par exemple une taille d’entrelacement de 64 Ko pour les applications OLTP sous SQL Server. |Plus grande taille d’entrelacement pour les grands schémas d’E/S séquentiels associés aux applications d’entrepôt de données. Utilisez par exemple une taille d’entrelacement de 256 Ko pour les applications d’entrepôt de données sous SQL Server. | &nbsp; |
| **Traitement multithread** |Utilisez le multithreading toopush le nombre élevé de demandes tooPremium stockage qui entraîne des toohigher IOPS et le débit. Par exemple, sur SQL Server définir un tooallocate de valeur élevée MAXDOP plusieurs unités centrales tooSQL Server. | &nbsp; | &nbsp; |
| **Profondeur de file d’attente** |Une plus grande profondeur de file d’attente génère un nombre plus élevé d’E/S par seconde. |Une plus grande profondeur de file d’attente génère un débit plus élevé. |Une plus petite profondeur de file d’attente réduit les latences. |

## <a name="nature-of-io-requests"></a>Nature des demandes d’E/S
Une demande d’E/S représente une unité d’opération d’entrée/sortie exécutée par votre application. Identifier la nature hello de demandes d’e/s, aléatoires ou séquentielles, de lecture ou d’écriture, petite ou grande, vous aide à déterminer les besoins de performances hello de votre application. Il est de nature de hello toounderstand très important de demandes d’e/s, toomake hello bonnes décisions lors de la conception de votre infrastructure d’application.

Taille d’e/s est un des hello facteurs les plus importants. Hello taille d’e/s est la taille hello de demande d’opération d’entrée/sortie hello générée par votre application. Hello taille d’e/s a un impact significatif sur les performances en particulier sur hello IOPS et bande passante hello application est en mesure de tooachieve. Hello formule suivante illustre relation hello entre les e/s, taille d’e/s et la bande passante ou de débit.  
    ![](media/storage-premium-storage-performance/image1.png)

Certaines applications vous permettent de tooalter taille de leur e/s, contrairement à certaines applications. Par exemple, SQL Server détermine la taille d’e/s optimales hello lui-même et ne fournit pas les utilisateurs avec n’importe quel toochange boutons il. Sur hello autre part, Oracle fournit un paramètre appelé [DB\_bloquer\_taille](https://docs.oracle.com/cd/B19306_01/server.102/b14211/iodesign.htm#i28815) à l’aide de laquelle vous pouvez configurer hello taille de demande d’e/s de base de données hello.

Si vous utilisez une application qui n’autorise pas de vous toochange hello taille d’e/s, suivez les indications de hello cet indicateur de performance clé qui est l’application la plus appropriée tooyour des performances hello article toooptimize. Par exemple,

* Une application OLTP génère des millions de demandes d’E/S petites et aléatoires. demande de toohandle ces type d’e/s, vous devez concevoir votre tooget d’infrastructure application IOPS plus élevée.  
* Une application d’entrepôt de données génère d’importantes demandes d’E/S séquentielles. toohandle ces type de demandes d’e/s, vous devez concevoir votre tooget d’infrastructure d’application beaucoup de bande passante ou de débit.

Si vous utilisez une application, ce qui vous permet de taille d’e/s toochange hello, utilisez cette règle générale pour hello e/s de taille en outre les instructions de performances tooother,

* Plus petit tooget de taille d’e/s des e/s plus élevée. Par exemple, 8 Ko pour une application OLTP.  
* Tooget de taille d’e/s plus grande bande passante ou de débit plus élevé. Par exemple, 1 024 Ko pour une application d’entrepôt de données.

Voici un exemple sur la façon dont vous pouvez calculer hello IOPS et le débit et la bande passante pour votre application. Supposons une application utilisant un disque P30. Hello IOPS maximal et un disque P30 peut atteindre un débit et bande passante est 5000 IOPS et 200 Mo par seconde respectivement. Si votre application requiert hello que maximales e/s de disque de hello P30 et que vous utilisent une taille d’e/s inférieure à 8 Ko, hello résultant de la bande passante, vous serez en mesure de tooget est désormais 40 Mo par seconde. Toutefois, si votre application requiert hello débit maximale et bande passante à partir du disque de P30 et que vous utilisez une plus grande taille d’e/s à 1 024 Ko, hello IOPS résultant sera inférieur, 200 IOPS. Par conséquent, paramétrez taille d’e/s hello tel qu’il réponde aux deux votre IOPS et le débit et la bande passante nécessaires à une application. Tableau ci-dessous récapitule les tailles d’e/s différentes hello et leurs IOPS et débit correspondants pour un disque P30.

| Spécification de l’application | Taille des E/S | E/S par seconde | Débit/bande passante |
| --- | --- | --- | --- |
| Nb max. d’E/S par seconde |8 Ko |5 000 |40 Mo par seconde |
| Débit max. |1 024 Ko |200 |200 Mo par seconde |
| Débit max + nb élevé d’E/S par seconde |64 Ko |3 200 |200 Mo par seconde |
| Nb max d’E/S par seconde + débit élevé |32 Ko |5 000 |160 Mo par seconde |

tooget IOPS et bande passante supérieure à la valeur maximale de hello d’un disque de stockage premium unique, utiliser plusieurs disques premium réparties ensemble. Par exemple, distribuez tooget de disques deux P30 un IOPS combiné de 10 000 IOPS ou un débit combiné de 400 Mo par seconde. Comme expliqué dans la section suivante de hello, vous devez utiliser une taille de machine virtuelle qui prend en charge les IOPS de disque hello combiné et le débit.

> [!NOTE]
> Lorsque vous augmentez l’e/s ou hello débit autres augmente également, assurez-vous que vous ne cliquez pas sur débit ou les limites d’e/s de la machine virtuelle ou disque de hello lorsque l’une de l’augmentation.
>
>

toowitness hello les effets de la taille d’e/s sur les performances de l’application, vous pouvez exécuter les outils de test sur votre machine virtuelle et les disques. Créer plusieurs séries de tests et utiliser différentes taille d’e/s pour chaque impact de hello toosee d’exécution. Consultez toohello [Benchmarking](#Benchmarking) section à fin hello de cet article pour plus d’informations.

## <a name="high-scale-vm-sizes"></a>Tailles des machines virtuelles à grande échelle
Lorsque vous démarrez la conception d’une application, un des hello première choses toodo est, choisissez un toohost de machine virtuelle de votre application. Premium Storage est fourni avec des tailles de machine virtuelle à grande échelle capables d’exécuter des applications qui requièrent une plus grande puissance de calcul et de hautes performances d’E/S du disque local. Ces machines virtuelles fournissent des processeurs plus rapides, un taux de mémoire-cœur plus élevé et un Solid-State Drive (SSD) pour le disque local de hello. Série DS, DSv2 et GS hello machines virtuelles sont des exemples de grande échelle machines virtuelles prenant en charge le stockage Premium.

Ces machines virtuelles sont disponibles en différentes tailles, avec un nombre différent de cœurs de processeur, de mémoire, de système d’exploitation et de taille du disque temporaire. Chaque taille de machine virtuelle dotée d’un nombre maximal de disques de données que vous pouvez attacher toohello machine virtuelle. Par conséquent, taille de machine virtuelle hello choisi affecte la quantité capacité de traitement, de mémoire et de stockage est disponible pour votre application. Elle affecte également hello calcul et stockage à moindre coût. Par exemple, voici les spécifications de hello hello plus grande taille d’ordinateur virtuel dans une série DS, DSv2 série et une série GS :

| Taille de la machine virtuelle | Cœurs d’unité centrale | Mémoire | Tailles du disque de la machine virtuelle | Bande passante disques de données | Taille du cache | E/S par seconde | Limites d’E/S du cache de bande passante |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_DS14 |16 |112 Go |OS = 1023 Go  <br> SSD local = 224 Go |32 |576 Go |50 000 E/S par seconde  <br> 512 Mo par seconde |4 000 E/S par seconde et 33 Mo par seconde |
| Standard_GS5 |32 |448 Go |OS = 1023 Go  <br> SSD local = 896 Go |64 |4 224 Go |80 000 E/S par seconde  <br> 2 000 Mo par seconde |5 000 E/S par seconde et 50 Mo par seconde |

tooview une liste complète de toutes les tailles de machine virtuelle Azure disponibles, consultez trop[tailles de machine virtuelle Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [tailles de Linux VM](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Choisissez une taille de machine virtuelle qui peut répondre aux et tooyour de mise à l’échelle souhaitée des exigences de performances d’application. En outre, toothis, prendre en compte suivant les points importants à considérer lors du choix de tailles de machine virtuelle.

*Limites de mise à l’échelle*  
Hello limites maximum d’IOPS par machine virtuelle et par disque sont différentes et indépendante des autres. Assurez-vous qu’application hello est en e/s dans les limites de hello machine virtuelle, ainsi que tooit joint des disques premium hello hello. Dans le cas contraire, les performances de l’application seront limitées.

Par exemple, supposons une application exigeant un maximum de 4 000 E/S par seconde. tooachieve cette option, vous configurer un disque P30 sur une machine virtuelle DS1. too5, 000 IOPS peut offrir un disque de P30 Hello. Toutefois, hello DS1 VM est limitée too3, 200 IOPS. Par conséquent, les performances de l’application hello seront contraint par la limite d’ordinateurs virtuels hello à 3 200 niveau d’IOPS et il y aura de dégradation des performances. tooprevent cette situation, choisissez un ordinateur virtuel et taille qui sera à ces deux exigences de l’application satisfait du disque.

*Coût d’exploitation*  
Dans de nombreux cas, il est possible que le coût global d’exploitation lié à l’utilisation de Premium Storage soit inférieur à celui associé à l’utilisation d’un stockage Standard.

Imaginez par exemple une application nécessitant 16 000 E/S par seconde. tooachieve ces performances, vous aurez besoin d’une norme\_D14 IaaS machine virtuelle Azure, qui peut octroyer à un niveau d’IOPS maximale de 16 000 à l’aide de 32 disques de 1 To de stockage standard. Chaque disque de stockage standard de 1 To peut atteindre un maximum de 500 E/S par seconde. Hello estimation de coût de cet ordinateur virtuel par mois sera 1,570 $. coût mensuel de Hello 32 standard des disques de stockage sera 1,638 $. Hello estimation de coût mensuel total sera 3,208 $.

Toutefois, si vous hébergé hello même application sur un stockage Premium, vous aurez besoin une plus petite taille de machine virtuelle et disques de stockage moins premium, ce qui réduit le coût global de hello. Une norme\_DS13 VM peut disposer de hello 16 000 e/s à l’aide de quatre disques P30. Hello DS13 VM a un nombre maximal d’IOPS de 25,600 et chaque disque P30 a un niveau d’IOPS maximal de 5 000. Globalement, cette configuration peut atteindre 5 000 x 4 = 20 000 E/S par seconde. Hello estimation de coût de cet ordinateur virtuel par mois sera 1,003 $. coût mensuel de Hello quatre P30 premium des disques de stockage sera 544.34 $. Hello estimation de coût mensuel total sera 1,544 $.

Tableau ci-dessous résume la répartition des coûts hello de ce scénario pour Standard et Premium Storage.

| &nbsp; | **Standard** | **Premium** |
| --- | --- | --- |
| **Coût de la machine virtuelle par mois** |1 570,58 $ (Standard\_StandardD14) |1 003,66 $ (Standard\_StandardDS13) |
| **Coût des disques par mois** |1 638,40 $ (32 disques de 1 To) |544,34 $ (4 disques P30) |
| **Coût global par mois** |3 208,98 $ |1 544,34 $ |

*Distributions Linux*  

Avec le stockage Azure Premium, vous obtenez hello même niveau de Performance pour les machines virtuelles exécutant Windows et Linux. Nous prenons en charge diverses versions de versions de Linux, et vous pouvez voir la liste complète hello [ici](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Il est important de toonote que les différentes versions sont mieux adaptées pour différents types de charges de travail. Vous verrez des différents niveaux de performances en fonction de distribution hello que votre charge de travail est en cours d’exécution. Tester les versions de Linux hello avec votre application et choisissez hello qui fonctionne le mieux.

Lors de l’exécution de Linux avec un stockage Premium, vérifiez hello plus récentes des mises à jour sur les performances de haute tooensure pilotes requis.

## <a name="premium-storage-disk-sizes"></a>Tailles de disques Premium Storage
Azure Premium Storage offre actuellement sept tailles de disque. Chaque taille de disque a une limite de mise à l’échelle bien spécifique pour le nombre d’E/S par seconde, la bande passante et le stockage. Choisissez la taille de disque de stockage Premium droite hello en fonction des spécifications d’application hello et élevée hello taille de machine virtuelle. tableau Hello ci-dessous montre les tailles de disques sept hello et leurs fonctionnalités. Les tailles de disque P4 et P6 ne sont actuellement prises en charge que par Managed Disks.

| Type de disque Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Taille du disque           | 32 Go | 64 Go | 128 Go| 512 Go            | 1024 Go (1 To)    | 2 048 Go (2 To)    | 4 095 Go (4 To)    | 
| IOPS par disque       | 120   | 240   | 500   | 2 300              | 5 000              | 7500              | 7500              | 
| Débit par disque | 25 Mo par seconde  | 50 Mo par seconde  | 100 Mo par seconde | 150 Mo par seconde | 200 Mo par seconde | 250 Mo par seconde | 250 Mo par seconde | 


Le nombre de disques que vous choisissez dépend de disque de hello taille choisie. Vous pouvez utiliser un seul disque P50 ou toomeet de disques P10 plusieurs de vos besoins de l’application. Prendre en considération ci-dessous lorsque vous élaborez des choix de hello.

*Limites de mise à l’échelle (E/S par seconde et débit)*  
limites de Hello IOPS et le débit de chaque taille de disque Premium est différente et indépendants des limites de mise à l’échelle de machine virtuelle hello. Vérifiez que hello total IOPS et débit à partir de disques de hello sont choisis dans les limites d’échelle de hello taille de machine virtuelle.

Imaginez par exemple que votre application requiert un débit maximum de 250 Mo/s et que vous utilisez une machine virtuelle DS4 avec un seul disque P30. Hello DS4 VM peut abandonner le débit de Mo/s too256. Toutefois, un seul disque P30 a limite de débit de 200 Mo par seconde. Par conséquent, application hello sera contraint à 200 Mo/s en raison de la limite de disque toohello. tooovercome cette limite, configurer plusieurs toohello de disques de données machine virtuelle ou redimensionner des disques tooP40 P50.

> [!NOTE]
> Lectures pris en charge par le cache de hello ne sont pas inclus dans les IOPS de disque hello et le débit, par conséquent, pas l’objet toodisk limites. Le cache possède sa propre limite de débit et d’E/S pour chaque machine virtuelle.
>
> Par exemple, les lectures et écritures sont initialement de 60 Mo/s et 40 Mo/s respectivement. Au fil du temps, le cache de hello préchauffage et sert de plus en plus de hello lectures à partir du cache de hello. Ensuite, vous pouvez obtenir écriture plus élevé de débit à partir du disque de hello.
>
>

*Nombre de disques*  
Déterminer le nombre de hello de disques que vous aurez besoin à l’évaluation des besoins de l’application. Chaque taille de machine virtuelle dotée d’une limite de nombre hello de disques que vous pouvez attacher toohello machine virtuelle. En règle générale, il s’agit de deux fois de hello nombre de cœurs. Vérifiez que hello taille de machine virtuelle que vous choisissez peut prendre en charge hello de disques requis.

N’oubliez pas de disques de stockage Premium hello ont des disques de stockage tooStandard de fonctions par rapport performances supérieurs. Par conséquent, si vous migrez votre application à partir de la machine virtuelle IaaS de Azure à l’aide du stockage Standard tooPremium stockage, vous aurez probablement besoin moins de disques premium tooachieve hello performance identique ou supérieur pour votre application.

## <a name="disk-caching"></a>Mise en cache du disque
Les machines virtuelles à grande échelle qui exploitent Azure Premium Storage ont une technologie de mise en cache à plusieurs niveaux appelée BlobCache. BlobCache utilise une combinaison de hello RAM de l’ordinateur virtuel et le disque SSD local pour la mise en cache. Ce cache est disponible pour les disques persistants de stockage Premium hello et les disques locaux de machine virtuelle de hello. Par défaut, ce paramètre de cache est défini tooRead/écriture pour les disques du système d’exploitation et en lecture seule pour les disques de données hébergées sur le stockage Premium. Avec la mise en cache disque activé sur les disques de stockage Premium hello, élevée hello machines virtuelles permettre atteindre très élevées de performances qui dépassent les performances du disque sous-jacent hello.

> [!WARNING]
> La modification de paramètre de cache hello d’un disque Azure détache et rattache le disque cible de hello. S’il est le disque du système d’exploitation hello, hello machine virtuelle est redémarré. Arrêtez toutes les applications/services qui peuvent être affectées par cette indisponibilité avant de modifier le paramètre de cache du disque hello.
>
>

toolearn en savoir plus sur le fonctionne de BlobCache, consultez toohello à l’intérieur de [stockage Azure Premium](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/) billet de blog.

Il s’agit de cache tooenable important sur l’ensemble approprié de hello de disques. Que vous devez activer la mise en cache du disque sur un disque premium ou pas dépendront de modèle de charge de travail hello ce disque doit gérer. Tableau ci-dessous présente des paramètres de cache pour les disques du système d’exploitation et des données par défaut de hello.

| **Type de disque** | **Paramètre de cache par défaut** |
| --- | --- |
| Disque de système d’exploitation |Lecture/écriture |
| Disque de données |Aucun |

Suivantes sont hello des paramètres de cache de disque recommandé pour les disques de données,

| **Paramètre de mise en cache du disque** | **Recommandation lorsque toouse ce paramètre** |
| --- | --- |
| Aucun |Configurer le cache hôte sur cette option pour les disques en lecture seule et les disques gourmands en écriture. |
| Lecture seule |Configurer le cache hôte en lecture seule pour les disques en lecture seule et les disques en lecture/écriture. |
| Lecture/écriture |Configurer le cache d’hôte comme ReadWrite uniquement si votre application gère correctement l’écriture de mise en cache des disques toopersistent de données si nécessaire. |

*Lecture seule*  
En configurant une mise en cache en lecture seule sur des disques de données Premium Storage, vous pouvez obtenir une faible latence de lecture et obtenir de très hautes performances d’E/S et de débit en lecture pour votre application. Cela est dû à deux raisons :

1. Lectures effectuées à partir du cache, ce qui se trouve sur la mémoire de machine virtuelle hello et disque SSD local, sont beaucoup plus rapides que les lectures sur le disque de données hello, qui se trouve sur hello stockage d’objets blob Azure.  
2. Stockage Premium ne compte pas hello pris en charge les lectures du cache, vers le disque hello IOPS et le débit. Par conséquent, votre application est en mesure de tooachieve supérieur total IOPS et le débit.

*Lecture/écriture*  
Par défaut, les disques du système d’exploitation hello ReadWrite cache sont activé. Nous avons récemment ajouté la prise en charge de la mise en cache en lecture/écriture sur les données des disques. Si vous utilisez la mise en cache de lecture/écriture, vous devez disposer d’un bon moyen toowrite hello de données à partir de disques toopersistent de cache. Par exemple, l’écriture des descripteurs de SQL Server mis en cache les disques de stockage persistant toohello de données sur son propre. À l’aide du cache de lecture/écriture avec une application qui ne gère pas la persistance hello requis données peuvent entraîner une perte de toodata si hello VM tombe en panne.

Par exemple, vous pouvez appliquer ces tooSQL directives serveur en cours d’exécution sur le stockage Premium en procédant comme suit de hello,

1. Configurez le cache en lecture seule sur les disques de stockage Premium qui hébergent des fichiers de données.  
   a.  Hello rapide lit à partir de la durée de requête de SQL Server du cache du inférieure hello étant donné que les pages de données sont extraites beaucoup plus rapidement toodirectly de cache comparé hello à partir de disques de données hello.  
   b.  Le traitement des lectures à partir du cache signifie que les disques de données premium délivrent un débit supplémentaire. SQL Server peut utiliser ce débit supplémentaire pour la récupération d’un plus grand nombre de pages de données et d’autres opérations telles que la sauvegarde/restauration, les charges de traitement par lots et les reconstructions d’index.  
2. Configurer « None » des fichiers journaux hello hébergement des disques de cache sur le stockage premium.  
   a.  Les fichiers journaux ont principalement des opérations d’écriture intensives. Par conséquent, ils ne bénéficient pas hello ReadOnly cache.

## <a name="disk-striping"></a>Entrelacement de disques
Quand une grande échelle de que machine virtuelle est attachée avec plusieurs premium stockage persistant disques, hello peut être réparties ensemble tooaggregate leurs IOPs, la bande passante et la capacité de stockage.

Sous Windows, vous pouvez utiliser des disques des espaces de stockage toostripe ensemble. Vous devez configurer une seule colonne pour chaque disque dans un pool. Dans le cas contraire, hello performances globales du volume agrégé par bandes peuvent être plus faible que prévu, en raison de la distribution de toouneven du trafic sur les disques hello.

Important : Vous utilisez le Gestionnaire de serveur UI, vous pouvez définir le nombre total de hello de colonnes des too8 pour un volume agrégé par bandes. Lors de l’attachement de disques plus de 8, utilisez le volume de hello toocreate PowerShell. À l’aide de PowerShell, vous pouvez définir nombre hello de colonnes nombre égal toohello de disques. Par exemple, s’il existe 16 disques dans un agrégat unique ; Spécifiez des 16 colonnes Bonjour *NumberOfColumns* paramètre Hello *New-VirtualDisk* applet de commande PowerShell.

Sur Linux, utilisez conjointement hello MDADM utilitaire toostripe des disques. Pour obtenir des instructions détaillées sur les disques d’agrégation par bandes sur Linux, consultez trop[configurer de RAID logiciels sur Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

*Taille de l’entrelacement*  
Une configuration importante dans la répartition des disques est la taille de bande hello. taille de bande Hello ou la taille de bloc est hello plus petit segment de données qui application peut adresser sur un volume agrégé par bandes. taille de bande Hello que vous configurez dépend de type hello d’application et de son modèle de demande. Si vous choisissez la taille de la mauvaise répartition hello, il risque de mauvais tooIO, ce qui conduit toodegraded les performances de votre application.

Par exemple, si une demande d’e/s générée par votre application est supérieure à la taille de bande hello disque, le système de stockage hello écrit sur bande des limites d’unité sur plusieurs disques. Lorsqu’il est temps tooaccess ces données, il aura tooseek sur plusieurs bandes unités toocomplete hello demande. effet cumulatif de Hello du comportement de ce type peut entraîner une dégradation des performances de toosubstantial. Sur hello autre part, si hello taille de la demande d’e/s est plus petite que la taille de bande, et si elle est aléatoire par nature, les demandes d’e/s hello peuvent additionner sur hello même disque provoquent un goulet d’étranglement et finalement dégrader les performances d’e/s hello.

En fonction de type hello de charge de travail de que votre application est en cours d’exécution, choisissez une taille de répartition appropriée. Pour les petites demandes d’E/S aléatoires, utilisez une plus petite taille d’entrelacement. Pour de grandes demandes d’E/S séquentielles, utilisez en revanche une plus grande taille d’entrelacement. Découvrez hello stripe taille recommandations pour l’application hello que vous allez exécuter sur un stockage Premium. Pour SQL Server, configurez une taille d’entrelacement de 64 Ko pour les charges de travail OLTP et de 256 Ko pour les charges de travail d’entrepôt de données. Consultez [performances meilleures pratiques pour SQL Server sur des machines virtuelles Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md#disks-guidance) toolearn plus.

> [!NOTE]
> vous pouvez entrelacer au maximum 32 disques de stockage premium sur une machine virtuelle DS et 64 disques de stockage premium sur une machine virtuelle GS.
>
>

## <a name="multi-threading"></a>Multithreading
Azure a conçu toobe de plate-forme de stockage Premium parallèle massif. Par conséquent, une application multithread délivre de bien meilleures performances qu’une application à thread unique. Une application multithread répartit de ses tâches sur plusieurs threads et augmente l’efficacité de son exécution en utilisant hello VM et toohello de ressources de disque maximale.

Par exemple, si votre application s’exécute sur un seul cœur de machine virtuelle à l’aide de deux threads, hello du processeur peut basculer entre l’efficacité de hello deux threads tooachieve. Lorsqu’un thread est en attente sur un toocomplete d’e/s disque, hello du processeur peut basculer toohello autre thread. De cette façon, deux threads peuvent accomplir bien plus qu’un seul thread. Si hello machine virtuelle possède plusieurs cœurs, il diminue plus temps d’exécution étant donné que chaque cœur peut exécuter des tâches en parallèle.

Vous n’êtes peut-être pas en mesure de toochange moyen de hello une application prête à implémente unique thread ou multi-threading. Par exemple, SQL Server est capable de gérer plusieurs processeurs et plusieurs nœuds. Toutefois, SQL Server décide dans quelles conditions elle reposera sur un ou plusieurs threads tooprocess une requête. Il peut exécuter des requêtes et créer des index à l’aide du traitement multithread. Pour une requête qui implique une jointure de tables de grande taille et le tri des données avant de retourner toohello utilisateur, SQL Server utilise probablement plusieurs threads. Toutefois, un utilisateur ne peut pas décider si SQL Server exécutera une requête à l’aide d’un ou plusieurs threads.

Il existe des paramètres de configuration que vous pouvez modifier tooinfluence ce multi-threading ou parallèle du traitement d’une application. Par exemple, en cas de SQL Server, il est configuration de degré de parallélisme maximale hello. Ce paramètre de MAXDOP, vous permet de tooconfigure hello nombre de processeurs que SQL Server peut utiliser lorsque le traitement en parallèle. Vous pouvez configurer MAXDOP pour des requêtes individuelles ou pour des opérations d’index. Cela s’avère utile lorsque vous souhaitez toobalance les ressources de votre système pour une application critique de performances.

Par exemple, supposons que votre application à l’aide de SQL Server exécute une requête de grande taille et une opération d’index sur hello même temps. Supposons que vous souhaitiez hello index opération toobe plus performant par rapport toohello grande requête. Dans ce cas, vous pouvez définir la valeur MAXDOP hello index opération toobe supérieur hello valeur MAXDOP pour la requête de hello. De cette manière, SQL Server a plus grand nombre de processeurs, il peut exploiter pour hello index opération comparée toohello nombre de processeurs, il peut consacrer toohello requête de grande taille. N’oubliez pas, vous ne contrôlez pas le nombre de hello de threads SQL Server utilisera pour chaque opération. Vous pouvez contrôler hello le nombre maximal de processeurs qui est dédié au multithreading.

En savoir plus sur [Degrés de parallélisme](https://technet.microsoft.com/library/ms188611.aspx) dans SQL Server. Découvrez des paramètres qui influencent multithreading dans votre application et leurs performances toooptimize de configurations.

## <a name="queue-depth"></a>Profondeur de file d’attente
Hello profondeur de file d’attente ou de longueur de file d’attente ou la taille de la file d’attente est le nombre hello de demandes d’e/s en attente dans le système de hello. valeur Hello de profondeur de file d’attente détermine le nombre d’e/s d’opérations votre application peut aligner, les disques de stockage hello traitera. Il affecte tous les hello trois applications les indicateurs de performance dont nous avons discuté dans cet article savoir, IOPS, débit et la latence.

La profondeur de file d’attente et le traitement multithread sont étroitement liés. Hello valeur de profondeur de file d’attente indique la quantité multi-threading qui peut être obtenue par application hello. Si hello profondeur de file d’attente est importante, application peut exécuter plusieurs opérations simultanément, en d’autres termes, plus multi-threading. Si hello profondeur de file d’attente est petite, même si l’application est multithread, il n’aura pas suffisamment demandes alignés pour une exécution simultanée.

En règle générale, off hello étagère applications n’autorisent pas vous profondeur de file d’attente toochange hello, car si définie correctement, il fera plus de mal que de bien. Les applications seront valeur hello droite des performances optimales de file d’attente profondeur tooget hello. Toutefois, il est important toounderstand ce concept afin que vous pouvez résoudre les problèmes de performances avec votre application. Vous pouvez également observer les effets de hello de profondeur de file d’attente par les outils de test en cours d’exécution sur votre système.

Certaines applications fournissent des paramètres tooinfluence hello profondeur de file d’attente. Par exemple, paramètre de MAXDOP (degré maximal de parallélisme) hello dans SQL Server est expliqué dans la section précédente. MAXDOP est un moyen de tooinfluence profondeur de file d’attente et multi-threading, bien qu’il ne modifie pas directement les valeur de profondeur de file d’attente de hello de SQL Server.

*Grande profondeur de file d’attente*  
Une profondeur de file d’attente élevé les lignes les plus d’opérations sur le disque de hello. disque de Hello sait demande suivante de hello dans sa file d’attente à l’avance. Par conséquent, disque de hello permettre planifier des opérations d’avance et les traiter dans une séquence optimale. Étant donné que l’application hello envoie plus disque toohello de demandes, disque de hello peut traiter les e/s parallèles plus. Pour finir, application hello sera en mesure de tooachieve e/s plus élevée. Étant donné que l’application est en train de traiter plus de requêtes, hello débit total d’application hello augmente également.

En général, une application peut atteindre un débit maximal avec 8-16 E/S en attente par disque connecté. Si une profondeur de file d’attente, application effectue pas suffisamment toohello du système IOs, et il traitera moins le montant de pendant une période donnée. En d’autres termes, elle atteindra un débit inférieur.

Par exemple, dans SQL Server, hello du paramètre MAXDOP valeur pour une requête trop « 4 » indique à SQL Server qu’il peut utiliser des requêtes de hello tooexecute toofour cœurs. SQL Server détermine quel est meilleure file d’attente profondeur hello et la valeur de nombre de cœurs pour l’exécution de requête hello.

*Profondeur de file d’attente optimale*  
Une valeur de profondeur de file d’attente très élevée présente aussi des inconvénients. Si la valeur de profondeur de file d’attente est trop élevé, application hello essaiera toodrive e/s très élevées. À moins que l’application repose sur des disques persistants associés à un nombre suffisant d’E/S par seconde, cela peut affecter sérieusement les latences d’application. Formule suivante montre la relation de hello entre les e/s, la latence et profondeur de file d’attente.  
    ![](media/storage-premium-storage-performance/image6.png)

Vous ne configurez pas de valeur élevée tooany de profondeur de file d’attente, mais tooan la valeur optimale qui peut fournir suffisamment d’IOPS pour l’application hello sans affecter les temps de latence. Par exemple, si la latence de l’application hello doit toobe 1 milliseconde, hello profondeur de file d’attente requis tooachieve est de 5 000 IOPS, QD = 5000 x 0,001 = 5.

*Profondeur de file d’attente pour le volume entrelacé*  
Pour un volume entrelacé, conservez une profondeur de file d’attente suffisamment élevée de sorte que chaque disque dispose individuellement d’un pic de profondeur de file d’attente. Par exemple, considérez une application qui exécute un push d’une profondeur de file d’attente de 2, et il existe 4 disques de répartition de hello. demandes d’e/s deux Hello passera tootwo disques et restant deux disques sera inactif. Par conséquent, configurer profondeur de file d’attente hello telles que tous les disques hello peuvent être occupés. Formule ci-dessous montre comment toodetermine hello profondeur de file d’attente de volumes agrégés par bandes.  
    ![](media/storage-premium-storage-performance/image7.png)

## <a name="throttling"></a>Limitation
Les dispositions de stockage Premium Azure spécifié nombre d’IOPS et le débit en fonction des tailles de machine virtuelle hello et tailles de disque que vous choisissez. Chaque fois que votre application tente de toodrive e/s ou un débit dépasse ces limites de quel hello machine virtuelle ou un disque peut gérer, il est limité par stockage Premium. Cela se manifeste sous forme de hello de dégradation des performances dans votre application. à savoir une latence plus élevée, un débit réduit ou un nombre inférieur d’E/S par seconde. Sans cette limitation, votre application risquerait de planter en demandant plus que ses ressources ne lui permettent d’effectuer. Par conséquent, des problèmes en raison de performances de tooavoid toothrottling, toujours configurer suffisamment de ressources pour votre application. Prenez en compte ce que nous avons abordée dans les sections de tailles de disque ci-dessus et les tailles de machine virtuelle hello. Tests de performances est hello meilleure manière toofigure out les ressources auxquelles vous devez toohost votre application.

## <a name="benchmarking"></a>Benchmarking
Tests de performances consiste à hello simuler différentes charges de travail sur votre application et de mesurer les performances de l’application hello pour chaque charge de travail. À l’aide des étapes hello décrits dans une section précédente, vous avez rassemblé les exigences de performances d’application hello. En exécutant des tests de performances outils sur des machines virtuelles de hello hébergeant l’application hello, vous pouvez déterminer les niveaux de performance hello que votre application peut atteindre avec stockage Premium. Dans cette section, nous allons vous fournir des exemples d’un benchmarking effectué sur une machine virtuelle DS14 Standard configurée avec des disques Azure Premium Storage.

Nous avons utilisé les outils courants Iometer et FIO, pour Windows et Linux respectivement. Ces outils générer plusieurs threads en simulant une charge de travail et de mesurer les performances système hello en production. À l’aide des outils de hello vous pouvez également configurer des paramètres tels que la profondeur blocs de taille et de la file d’attente, que vous ne pouvez pas normalement modifier pour une application. Cela vous donne davantage de souplesse toodrive hello maximale de performances sur une ordinateur virtuel configuré avec les disques premium pour différents types de charges de travail applicatives à grande échelle. toolearn plus sur chaque outil de test, visitez [Iometer](http://www.iometer.org/) et [FIO](http://freecode.com/projects/fio).

exemples de hello toofollow ci-dessous, créer une machine virtuelle de DS14 Standard et attacher 11 toohello de disques de stockage Premium machine virtuelle. Des disques de hello 11, configurer 10 disques avec l’hôte de la mise en cache en tant que « None » et les distribuer dans un volume appelé NoCacheWrites. Configurer l’hôte de la mise en cache en tant que « ReadOnly » sur le disque restant de hello et créer un volume appelé CacheReads avec ce disque. À l’aide de ce programme d’installation, vous serez en mesure de toosee hello en lecture et écriture performances maximales à partir d’un ordinateur virtuel DS14 Standard. Pour obtenir des instructions détaillées sur la création d’une machine virtuelle DS14 avec disques premium, consultez trop[créer et utiliser un stockage Premium compte pour un disque de données de machine virtuelle](storage-premium-storage.md).

*Mise en route hello du Cache*  
disque Hello avec caching d’hôte ReadOnly sera en mesure de toogive IOPS supérieur à la limite de disque hello. tooget ce maximum les performances de lecture à partir du cache d’hôte hello, tout d’abord vous devez préchauffage cache hello de ce disque. Cela garantit que hello IOs en lecture quel outil de test dirige sur CacheReads volume réellement atteint cache de hello et de disque de hello pas directement. résultat de présences dans le cache Hello dans les e/s supplémentaires à partir du cache d’unique hello activé disque.

> **Important :**  
> Vous devez préchauffage du cache de hello avant d’exécuter des tests de performances, chaque redémarrage de machine virtuelle.
>
>

#### <a name="iometer"></a>Iometer
[Télécharger l’outil de Iometer hello](http://sourceforge.net/projects/iometer/files/iometer-stable/2006-07-27/iometer-2006.07.27.win32.i386-setup.exe/download) sur hello machine virtuelle.

*Fichier de test*  
Iometer utilise un fichier de test qui est stocké sur le volume hello sur lequel vous allez exécuter hello test des tests de performances. Lecteurs de lectures et écritures sur ce test disque hello toomeasure IOPS et le débit. Iometer crée ce fichier de test si vous n’en avez pas fourni. Créer un fichier de test de 200 Go appelé iobw.tst sur des volumes CacheReads et NoCacheWrites hello.

*Spécifications d’accès*  
Hello, spécifications de taille de la demande d’e/s, % en lecture/écriture, % aléatoire/séquentiel configurés à l’aide d’onglet de « Spécifications d’accès » hello dans Iometer. Créer une spécification de l’accès pour chacun des scénarios hello décrits ci-dessous. Créer des spécifications d’accès hello et « Enregistrer » avec un nom similaire – RandomWrites\_8K, RandomReads\_8 Ko. Sélectionnez la spécification correspondante de hello lors de l’exécution du scénario de test de hello.

Vous trouverez ci-dessous un exemple de spécifications d’accès pour un scénario d’E/S en écriture maximales.  
    ![](media/storage-premium-storage-performance/image8.png)

*Spécifications de test du taux maximal d’E/S par seconde*  
toodemonstrate maximale IOPs, utilisez la plus petite taille de la demande. Utilisez une taille de 8 Ko et créez des spécifications pour les lectures et écritures aléatoires.

| Spécification d’accès | Taille de la demande | % aléatoire | % écriture |
| --- | --- | --- | --- |
| RandomWrites\_8K |8 Ko |100 |0 |
| RandomReads\_8K |8 Ko |100 |100 |

*Spécifications de test du débit maximal*  
toodemonstrate débit maximal, utilisent la plus grande taille de demande. Utilisez une taille de requête 64 K et créez des spécifications pour les lectures et écritures aléatoires.

| Spécification d’accès | Taille de la demande | % aléatoire | % écriture |
| --- | --- | --- | --- |
| RandomWrites\_64K |64 Ko |100 |0 |
| RandomReads\_64K |64 Ko |100 |100 |

*Hello Iometer Test en cours d’exécution*  
Effectuez les opérations hello ci-dessous toowarm cache

1. Créez deux spécifications d’accès avec les valeurs indiquées ci-dessous

   | Nom | Taille de la demande | % aléatoire | % écriture |
   | --- | --- | --- | --- |
   | RandomWrites\_1MB |1 Mo |100 |0 |
   | RandomReads\_1MB |1 Mo |100 |100 |
2. Exécutez test de Iometer hello pour l’initialisation du cache disque avec les paramètres suivants. Utilisez trois threads de travail pour le volume cible hello et une profondeur de file d’attente de 128. Définir hello « Exécution » la durée de too2hrs de test hello sur l’onglet de « Tester le programme d’installation » hello.

   | Scénario | Volume cible | Nom | Durée |
   | --- | --- | --- | --- |
   | Initialisation du disque de cache |CacheReads |RandomWrites\_1MB |2 heures |
3. Exécutez test de Iometer hello pour le préchargement dans le disque de cache avec les paramètres suivants. Utilisez trois threads de travail pour le volume cible hello et une profondeur de file d’attente de 128. Définir hello « Exécution » la durée de too2hrs de test hello sur l’onglet de « Tester le programme d’installation » hello.

   | Scénario | Volume cible | Nom | Durée |
   | --- | --- | --- | --- |
   | Préchauffage du disque de cache |CacheReads |RandomReads\_1MB |2 heures |

Une fois le cache disque est préparée, procéder à des scénarios de test hello répertoriées ci-dessous. toorun hello Iometer test, utilisez au moins trois des threads de travail pour **chaque** volume cible. Pour chaque thread de travail, sélectionnez le volume cible hello, définissez une profondeur de file d’attente et sélectionnez une des caractéristiques de test hello enregistré, comme indiqué dans la table hello ci-dessous, le scénario de test correspondant toorun hello. table de Hello montre également les résultats attendus pour e/s et un débit lors de l’exécution de ces tests. Pour tous les scénarios, une petite taille d’E/S de 8 Ko et une profondeur de file d’attente élevée de 128 sont utilisées.

| Scénario de test | Volume cible | Nom | Résultat |
| --- | --- | --- | --- |
| Bande passante E/S par seconde en lecture |CacheReads |RandomWrites\_8K |50 000 E/S par seconde  |
| Bande passante E/S par seconde en écriture |NoCacheWrites |RandomReads\_8K |64 000 E/S par seconde |
| Bande passante Taux d’E/S par seconde combiné |CacheReads |RandomWrites\_8K |100 000 E/S par seconde |
| NoCacheWrites |RandomReads\_8K | &nbsp; | &nbsp; |
| Bande passante Mo/s en lecture |CacheReads |RandomWrites\_64K |524 Mo/s |
| Bande passante Mo/s en écriture |NoCacheWrites |RandomReads\_64K |524 Mo/s |
| Mo/s combiné |CacheReads |RandomWrites\_64K |1 000 Mo/s |
| NoCacheWrites |RandomReads\_64K | &nbsp; | &nbsp; |

Vous trouverez ci-dessous des captures d’écran de hello Iometer les résultats de test pour des scénarios de débit et des IOPS combinés.

*Taux d’E/S maximal combiné en lecture et en écriture*  
![](media/storage-premium-storage-performance/image9.png)

*Débit maximal combiné en lecture et en écriture*  
![](media/storage-premium-storage-performance/image10.png)

### <a name="fio"></a>FIO
FIO est un stockage de toobenchmark outil populaire sur hello les machines virtuelles Linux. Il a des tailles différentes e/s hello flexibilité tooselect, séquentiels ou aléatoires des lectures et écritures. Il génère des threads de travail ou hello tooperform de processus spécifié les opérations d’e/s. Vous pouvez spécifier le type hello d’opérations d’e/s que chaque thread de travail doit effectuer à l’aide de fichiers de travail. Nous avons créé un fichier de travail par le scénario illustré dans les exemples hello ci-dessous. Vous pouvez modifier les spécifications de hello dans ces travaux fichiers toobenchmark différentes charges de travail en cours d’exécution sur le stockage Premium. Dans les exemples hello, nous utilisons une exécution Standard pour machine virtuelle 14 DS **Ubuntu**. Hello d’utiliser le programme d’installation même décrit début hello Hello [section des tests de performances](#Benchmarking) et préchauffage cache hello avant d’exécuter des tests des tests de performances de hello.

Avant de commencer, [téléchargez FIO](https://github.com/axboe/fio) et installez-le sur votre machine virtuelle.

Exécutez hello de commande suivante pour Ubuntu,

```
apt-get install fio
```

Nous allons utiliser quatre threads de travail de commande d’opérations d’écriture et de quatre threads de travail pour la conduite des opérations de lecture sur des disques hello. Hello travailleurs de l’écriture seront être gèrent le trafic sur le volume hello « nocache », ce qui a 10 disques avec le cache défini trop « None ». Hello threads de travail en lecture seront être gérant le trafic sur le volume hello « readcache », qui a 1 disque avec le jeu de cache trop « ReadOnly ».

*Taux d’E/S par seconde maximal en écriture*  
Créer un fichier de travail hello avec tooget de spécifications suivantes maxi. d’écriture. Nommez ce fichier « fiowrite.ini ».

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[writer1]
rw=randwrite
directory=/mnt/nocache
[writer2]
rw=randwrite
directory=/mnt/nocache
[writer3]
rw=randwrite
directory=/mnt/nocache
[writer4]
rw=randwrite
directory=/mnt/nocache
```

Hello de Remarque Suivez les informations essentielles qui respectent les règles de conception hello présentées dans les sections précédentes. Ces spécifications sont essentiel toodrive nombre maximal d’IOPS,  

* Une profondeur de file d’attente élevée de 256.  
* Une petite taille de bloc de 8 Ko.  
* Plusieurs threads effectuant des écritures aléatoires.

Exécutez hello suivant tookick commande off hello FIO vérifier la présence de 30 secondes,  

```
sudo fio --runtime 30 fiowrite.ini
```

Pendant l’exécution de test de hello, vous serez nombre de hello toosee en mesure de remettre des disques de machine virtuelle et Premium de hello e/s d’écriture. Comme indiqué dans l’exemple hello ci-dessous, hello DS14 VM propose sa limite d’e/s de 50 000 IOPS maximale d’écriture.  
    ![](media/storage-premium-storage-performance/image11.png)

*Taux d’E/S par seconde maximal en lecture*  
Créer un fichier de travail hello avec tooget de spécifications suivantes IOPS maximales qu’en lecture. Nommez ce fichier « fioread.ini ».

```
[global]
size=30g
direct=1
iodepth=256
ioengine=libaio
bs=8k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache
```

Hello de Remarque Suivez les informations essentielles qui respectent les règles de conception hello présentées dans les sections précédentes. Ces spécifications sont essentiel toodrive nombre maximal d’IOPS,

* Une profondeur de file d’attente élevée de 256.  
* Une petite taille de bloc de 8 Ko.  
* Plusieurs threads effectuant des écritures aléatoires.

Exécutez hello suivant tookick commande off hello FIO vérifier la présence de 30 secondes,

```
sudo fio --runtime 30 fioread.ini
```

Pendant l’exécution de test de hello, vous serez nombre de hello toosee en mesure de lecture e/s hello VM et remettre des disques Premium. Comme indiqué dans l’exemple hello ci-dessous, hello DS14 VM offre plus de 64 000 e/s de lecture. Il s’agit d’une combinaison de disque de hello et les performances du cache hello.  
    ![](media/storage-premium-storage-performance/image12.png)

*Taux d’E/S par seconde maximal en lecture et en écriture*  
Créer le fichier de travail hello avec suivant tooget spécifications maximale combinées en lecture et écriture des e/s. Nommez ce fichier « fioreadwrite.ini ».

```
[global]
size=30g
direct=1
iodepth=128
ioengine=libaio
bs=4k

[reader1]
rw=randread
directory=/mnt/readcache
[reader2]
rw=randread
directory=/mnt/readcache
[reader3]
rw=randread
directory=/mnt/readcache
[reader4]
rw=randread
directory=/mnt/readcache

[writer1]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer2]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer3]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
[writer4]
rw=randwrite
directory=/mnt/nocache
rate_iops=12500
```

Hello de Remarque Suivez les informations essentielles qui respectent les règles de conception hello présentées dans les sections précédentes. Ces spécifications sont essentiel toodrive nombre maximal d’IOPS,

* Une profondeur de file d’attente élevée de 128.  
* Une petite taille de bloc de 4 Ko.  
* Plusieurs threads effectuant des opérations d’écriture et de lecture aléatoires.

Exécutez hello suivant tookick commande off hello FIO vérifier la présence de 30 secondes,

```
sudo fio --runtime 30 fioreadwrite.ini
```

Pendant l’exécution de test de hello, vous toosee en mesure de hello quantité, combiné en lecture et écriture IOPS hello de machine virtuelle et de livrer des disques Premium. Comme indiqué dans l’exemple hello ci-dessous, hello DS14 VM offre plus de 100 000 lecture combinée et écrire les e/s. Il s’agit d’une combinaison de disque de hello et les performances du cache hello.  
    ![](media/storage-premium-storage-performance/image13.png)

*Débit maximal combiné*  
hello tooget maximale combinées en lecture et écriture de débit, utilisez une plus grande taille de bloc et de la profondeur de file d’attente avec plusieurs threads exécutant des lectures et écritures. Vous pouvez utiliser une taille de bloc de 64 Ko et une profondeur de file d’attente de 128.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur Azure Premium Storage :

* [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md)  

Pour les utilisateurs de SQL Server, consultez les articles relatifs aux meilleures pratiques de performances de SQL Server :

* [Bonnes pratiques relatives aux performances de SQL Server sur les machines virtuelles Azure](../virtual-machines/windows/sql/virtual-machines-windows-sql-performance.md)
* [Azure Premium Storage provides highest performance for SQL Server in Azure VM (en anglais)](http://blogs.technet.com/b/dataplatforminsider/archive/2015/04/23/azure-premium-storage-provides-highest-performance-for-sql-server-in-azure-vm.aspx)
