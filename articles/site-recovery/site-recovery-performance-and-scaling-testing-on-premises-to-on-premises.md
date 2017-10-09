---
title: "résultats aaaTest pour la réplication Hyper-V entre les sites avec Azure Site Recovery | Documents Microsoft"
description: "Cet article fournit des informations sur les tests de performances pour la réplication locale tooon locaux des ordinateurs virtuels Hyper-V à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>Résultats des tests pour la réplication de Hyper-V sur site local tooon avec Site Recovery

Vous pouvez utiliser Microsoft Azure Site Recovery tooorchestrate et gérer la réplication de machines virtuelles et des serveurs physiques tooAzure ou tooa de centre de données secondaire. Cet article fournit des résultats de tests de performances que nous l’avons fait lors de la réplication entre deux des ordinateurs virtuels Hyper-V sur site centres de données hello.

## <a name="test-goals"></a>Objectifs des tests

objectif Hello de test a été tooexamine fonctionnement d’Azure Site Recovery lors de la réplication de l’état stable. Ce type de réplication se produit une fois que les machines virtuelles ont terminé la réplication initiale des données et effectuent une synchronisation du delta des changements. Il est important toomeasure les performances à l’aide de l’état stable, car il s’agit d’état hello dans lequel la plupart des ordinateurs virtuels restent, sauf si les arrêts inattendus se produisent.

déploiement de test Hello est composé de deux sites locaux avec un serveur VMM dans chaque site. Ce déploiement de test est typique d’un déploiement de siège social/agence, dont le siège agissant en tant que site principal de hello et filiale salutation en tant que site de base de données secondaire ou de récupération hello.

## <a name="what-we-did"></a>Nos actions

Voici ce que nous dans les tests hello correspondait :

1. Création des machines virtuelles à l’aide de modèles VMM.
2. Démarrage des machines virtuelles et capture des mesures de performances de référence sur une période de 12 heures.
3. Création de clouds sur les serveurs VMM principal et de récupération.
4. Configuration de la protection du cloud dans Microsoft Azure Site Recovery, notamment du mappage des clouds source et de récupération.
5. Activer la protection des machines virtuelles et les autoriser toocomplete la réplication initiale.
6. Vérification de la stabilisation du système, après une période d’attente de quelques heures.
7. Capture des mesures de performances sur une période de 12 heures, qui garantit que l’ensemble des machines virtuelles présentent l’état de réplication attendu pendant cette période.
8. Delta de hello mesure entre les mesures de performance de ligne de base hello et les métriques de performances de réplication hello.


## <a name="primary-server-performance"></a>Performances du serveur principal

* Hyper-V Replica asynchrone effectue le suivi de fichier journal tooa des modifications avec une surcharge de stockage minimale sur le serveur principal de hello.
* Réplica Hyper-V utilise autonome mémoire cache toominimize IOPS surcharge pour le suivi. Il stocke toohello écritures VHDX en mémoire et les vidages dans le fichier journal de hello avant hello de temps que le journal hello est envoyé toohello le site de récupération. Un vidage disque se produit également si hello écritures atteignent une limite prédéfinie.
* graphique de Hello ci-dessous affiche la surcharge d’e/s de l’état stable hello pour la réplication. Nous pouvons voir que hello tooreplication échéance surcharge d’e/s est d’environ 5 % qui est relativement faible.

![Résultats principaux](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Réplica Hyper-V utilise la mémoire sur les performances du disque toooptimize hello serveur principal. Comme indiqué dans hello suivant graphique, mémoire surcharge sur tous les serveurs dans le cluster principal de hello est marginale. Hello surcharge de mémoire indiquée est le pourcentage de hello de mémoire utilisée par la réplication par rapport de mémoire toohello total installé sur le serveur d’Hyper-V hello.

![Résultats principaux](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

Par ailleurs, le Réplica Hyper-V présente une surcharge minimale pour les processeurs. Comme indiqué dans le graphique de hello, la surcharge de réplication est hello de 2 à 3 %.

![Résultats principaux](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>Performances du serveur secondaire (récupération)

Réplica Hyper-V utilise une petite quantité de mémoire hello récupération serveur toooptimize hello nombre d’opérations de stockage. graphique de Hello résume l’utilisation de la mémoire sur le serveur de récupération hello hello. Hello surcharge de mémoire indiquée est le pourcentage de hello de mémoire utilisée par la réplication par rapport de mémoire toohello total installé sur le serveur d’Hyper-V hello.

![Résultats secondaires](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

quantité Hello d’opérations d’e/s sur le site de récupération hello est une fonction du nombre de hello d’opérations d’écriture sur le site principal de hello. Nous allons examiner les opérations d’e/s total hello sur le site de récupération de hello au nombre total d’opérations d’e/s hello et les opérations d’écriture sur le site principal de hello. affichent les graphiques de Hello total hello qu'e/s sur le site de récupération hello est

* Environ 1,5 fois hello d’écriture e/s sur hello principal.
* Environ 37 % des hello total e/s sur le site principal de hello.

![Résultats secondaires](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![Résultats secondaires](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>Effet sur l’utilisation du réseau

Une moyenne de 275 Mo par seconde de la bande passante du réseau a été utilisée entre hello principal et les nœuds de récupération (avec la compression activée) sur une bande passante existante de 5 Go par seconde.

![Résultats : utilisation du réseau](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>Effet sur le niveau de performance des machines virtuelles

Une considération importante est l’impact hello de la réplication sur les charges de production en cours d’exécution sur des machines virtuelles de hello. Si le site principal de hello est correctement approvisionné pour la réplication, il ne doivent pas être tout impact sur les charges de travail hello. Mécanisme de suivi de léger du réplica Hyper-V permet de s’assurer que les charges de travail en cours d’exécution sur des machines virtuelles hello ne soient pas affectés pendant la réplication de l’état stable. Ceci est illustré dans hello suivant des graphiques.

Ce graphe affiche le nombre d’E/S par seconde produites par les machines virtuelles exécutant diverses charges de travail, avant et après l’activation de la réplication. Vous pouvez observer qu’il n’existe aucune différence entre deux de hello.

![Résultats relatifs à l’effet du Réplica](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

Hello graphique suivant illustre le débit hello de machines virtuelles exécutant différentes charges de travail avant et après l’activation de la réplication. Comme vous pouvez le voir, l’impact de la réplication est négligeable.

![Résultats : effets du Réplica](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>Conclusion

résultats de Hello montrent clairement que Azure Site Recovery, couplé avec le réplica Hyper-V, met à l’échelle avec une surcharge minimale pour un grand cluster.  Microsoft Azure Site Recovery offre des fonctions simples de déploiement, de réplication, de gestion et de surveillance. Réplica Hyper-V fournit une infrastructure de nécessaires hello pour la mise à l’échelle de réussite de la réplication. Pour planifier un déploiement optimal nous vous suggérons de télécharger hello [Hyper-V Replica Capacity Planner](https://www.microsoft.com/download/details.aspx?id=39057).

## <a name="test-environment-details"></a>Détails de l’environnement de test

### <a name="primary-site"></a>Site principal

* site principal de Hello a un cluster contenant cinq serveurs Hyper-V exécutant 470 machines virtuelles.
* machines virtuelles de Hello exécuter différentes charges de travail, et leur protection Azure Site Recovery est activée.
* Stockage de nœud de cluster hello est fourni par un réseau SAN iSCSI. Modèle : Hitachi HUS130.
* Chaque serveur du cluster inclut quatre cartes d’interface réseau d’1 Gbit/s chacune.
* Deux cartes réseau de hello sont réseau privé d’iSCSI connecté tooan et deux sont connectés tooan réseau d’entreprise externe. Un des réseaux externes de hello est réservé pour les communications de cluster uniquement.

![Principales conditions matérielles requises](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| Serveur | RAM | Modèle | Processeur | Nombre de processeurs | Carte d’interface réseau | Logiciel |
| --- | --- | --- | --- | --- | --- | --- |
| Serveurs Hyper-V en cluster :  <br />ESTLAB-HOST11<br />ESTLAB-HOST12<br />ESTLAB-HOST13<br />ESTLAB-HOST14<br />ESTLAB-HOST25 |128 - ESTLAB-HOST25 : 256 |Dell™ PowerEdge™ R820 |Processeur Intel(R) Xeon(R) E5-4620 0 à 2,20 GHz |4 |1 Gbit/s x 4 |Windows Server Datacenter 2012 R2 (x 64) + rôle Hyper-V |
| Serveur VMM |2 | | |2 |1 Gbit/s |Windows Server Database 2012 R2 (x 64) + rôle VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>Site secondaire (récupération)

* site secondaire de Hello a un cluster de basculement à six nœuds.
* Stockage de nœud de cluster hello est fourni par un réseau SAN iSCSI. Modèle : Hitachi HUS130.

![Principales spécifications matérielles](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| Serveur | RAM | Modèle | Processeur | Nombre de processeurs | Carte d’interface réseau | Logiciel |
| --- | --- | --- | --- | --- | --- | --- |
| Serveurs Hyper-V en cluster :  <br />ESTLAB-HOST07<br />ESTLAB-HOST08<br />ESTLAB-HOST09<br />ESTLAB-HOST10 |96 |Dell™ PowerEdge™ R720 |Processeur Intel(R) Xeon(R) E5-2630 0 à 2,30 GHz |2 |1 Gbit/s x 4 |Windows Server Datacenter 2012 R2 (x 64) + rôle Hyper-V |
| ESTLAB-HOST17 |128 |Dell™ PowerEdge™ R820 |Processeur Intel(R) Xeon(R) E5-4620 0 à 2,20 GHz |4 | |Windows Server Datacenter 2012 R2 (x 64) + rôle Hyper-V |
| ESTLAB-HOST24 |256 |Dell™ PowerEdge™ R820 |Processeur Intel(R) Xeon(R) E5-4620 0 à 2,20 GHz |2 | |Windows Server Datacenter 2012 R2 (x 64) + rôle Hyper-V |
| Serveur VMM |2 | | |2 |1 Gbit/s |Windows Server Database 2012 R2 (x 64) + rôle VMM 2012 R2 |

### <a name="server-workloads"></a>Charges de travail du serveur

* À des fins de test, nous avons choisi les charges de travail souvent utilisées dans les scénarios de clients d’entreprise.
* Nous utilisons [IOMeter](http://www.iometer.org) aux caractéristiques de charge de travail hello résumées dans le tableau hello pour la simulation.
* Tous les profils IOMeter sont définis toowrite octets aléatoires toosimulate écriture pessimistes des modèles pour les charges de travail.

| Charge de travail | Taille des E/S (Ko) | Pourcentage d’accès | Pourcentage de lectures | E/S en attente | Modèle d’E/S |
| --- | --- | --- | --- | --- | --- |
| Serveur de fichiers |48163264 |60 %20 %5 %5 %10 % |80 %80 %80 %80 %80 % |88888 |100 % aléatoires |
| SQL Server (volume 1) SQL Server (volume 2) |864 |100 %100 % |70 %0 % |88 |100 % aléatoires100 % séquentielles |
| Microsoft Exchange |32 |100 % |67 % |8 |100 % aléatoires |
| Station de travail/VDI |464 |66 %34 % |70 %95 % |11 |100 % aléatoires |
| Serveur de fichiers web |4864 |33 %34 %33 % |95 %95 %95 % |888 |75 % aléatoires |

### <a name="vm-configuration"></a>Configuration des machines virtuelles

* 470 machines virtuelles sur le cluster principal de hello.
* Toutes les machines virtuelles avec un disque VHDX.
* Machines virtuelles exécutant des charges de travail résumées dans le tableau de hello. Elles ont toutes été créées avec des modèles VMM.

| Charge de travail | Nombre de machines virtuelles | Mémoire RAM minimale (en Go) | Mémoire RAM maximale (en Go) | Taille du disque logique par machine virtuelle (en Go) | Nombre maximal d’E/S par seconde |
| --- | --- | --- | --- | --- | --- |
| SQL Server |51 |1 |4 |167 |10 |
| Microsoft Exchange Server |71 |1 |4 |552 |10 |
| Serveur de fichiers |50 |1 |2 |552 |22 |
| VDI |149 |0,5 |1 |80 |6 |
| Serveur web |149 |0,5 |1 |80 |6 |
| TOTAL |470 | | |96,83 To |4 108 |

### <a name="site-recovery-settings"></a>Paramètres de Site Recovery

* Azure Site Recovery a été configuré pour la protection de local tooon local
* serveur VMM de Hello possède quatre clouds configurés, contenant des serveurs de cluster Hyper-V hello et leurs ordinateurs virtuels.

| Cloud VMM principal | Machines virtuelles protégées dans le cloud de hello | Fréquence de réplication | Points de récupération supplémentaires |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 minutes |Aucun |
| PrimaryCloudRpo30s |47 |30 secondes |Aucun |
| PrimaryCloudRpo30sArp1 |47 |30 secondes |1 |
| PrimaryCloudRpo5m |235 |5 minutes |Aucun |

### <a name="performance-metrics"></a>Mesures de performances

tableau de Hello récapitule les métriques de performances hello et des compteurs qui ont été mesurés dans le déploiement de hello.

| Mesure | Compteur |
| --- | --- |
| UC |\Processor(_Total)\% temps processeur |
| Mémoire disponible |\Memory\Available MBytes |
| E/S par seconde |\PhysicalDisk(_Total)\Disk Transfers/sec |
| Nombre d’opérations d’E/S par seconde en lecture de la VM |\Hyper-V Virtual Storage Device(<VHD>)\Read Operations/Sec |
| Nombre d’opérations d’E/S par seconde en écriture de la VM |\Hyper-V Virtual Storage Device(<VHD>)\Write Operations/S |
| Débit de lecture des VM |\Hyper-V Virtual Storage Device(<VHD>)\Read Bytes/sec |
| Débit d’écriture des VM |\Hyper-V Virtual Storage Device(<VHD>)\Write Bytes/sec |

## <a name="next-steps"></a>Étapes suivantes

[Configuration de la réplication entre deux sites VMM locaux](site-recovery-vmm-to-vmm.md)
