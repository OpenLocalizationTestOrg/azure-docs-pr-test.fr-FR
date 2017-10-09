---
title: "aaaWhat est un gestionnaire d’instantanés StorSimple ? | Microsoft Docs"
description: "Décrit les hello Gestionnaire d’instantanés StorSimple, son architecture et ses fonctionnalités."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6094c31e-e2d9-4592-8a15-76bdcf60a754
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: v-sharos
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79ce7b7e1970ac862038af2a0e67065b6fb6eda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toostorsimple-snapshot-manager"></a>Un gestionnaire d’instantanés de tooStorSimple introduction

## <a name="overview"></a>Vue d'ensemble
Gestionnaire d’instantanés StorSimple est un composant logiciel enfichable Microsoft Management Console (MMC) qui simplifie la protection des données et la gestion des sauvegardes dans l’environnement Microsoft Azure StorSimple. Avec Gestionnaire d’instantanés StorSimple, vous pouvez gérer les données de Microsoft Azure StorSimple dans le centre de données hello et dans le cloud de hello comme une solution de stockage intégrée unique, par conséquent, ce qui simplifie le processus de sauvegarde et de réduire les coûts.

Cette vue d’ensemble présente hello Gestionnaire d’instantanés StorSimple, décrit ses fonctionnalités et explique son rôle dans Microsoft Azure StorSimple. 

Pour une vue d’ensemble de tout système de Microsoft Azure StorSimple hello, y compris l’appareil StorSimple hello, le service StorSimple Manager, le Gestionnaire d’instantanés StorSimple et de l’adaptateur StorSimple pour SharePoint, consultez [série StorSimple 8000 : un cloud hybride solution de stockage](storsimple-overview.md). 

> [!NOTE]
> * Vous ne pouvez pas utiliser le Gestionnaire d’instantanés StorSimple toomanage Microsoft Azure StorSimple tableaux virtuels (également appelé StorSimple local périphériques virtuels).
> * Si vous envisagez tooinstall 2 de mise à jour StorSimple sur votre appareil StorSimple, que toodownload hello version la plus récente du Gestionnaire d’instantanés StorSimple et l’installer **avant d’installer StorSimple mise à jour 2**. version la plus récente de StorSimple Snapshot Manager Hello est à compatibilité descendante et fonctionne avec les versions de Microsoft Azure StorSimple. Si vous utilisez une version précédente de hello du Gestionnaire d’instantanés StorSimple, vous devez tooupdate informatique (il est inutile version précédente de hello toouninstall avant d’installer de la nouvelle version de hello).
> 
> 

## <a name="storsimple-snapshot-manager-purpose-and-architecture"></a>Architecture et objectif du gestionnaire d’instantanés StorSimple
Gestionnaire d’instantanés StorSimple fournit une console de gestion centrale que vous pouvez utiliser toocreate cohérent, point-à-temps les copies de sauvegarde locaux et cloud données. Par exemple, vous pouvez utiliser la console hello pour :

* Configurer, sauvegarder et supprimer des volumes.
* Configurer le volume tooensure de groupes les données sauvegardées est cohérente avec les applications.
* Gérer les stratégies de sauvegarde afin que les données soient sauvegardées selon un calendrier prédéterminé.
* Créez local et des instantanés, qui peuvent être stockés dans le cloud de hello et utilisés pour la récupération d’urgence de cloud computing.

Hello Gestionnaire d’instantanés StorSimple extrait la liste hello des applications inscrites avec le fournisseur VSS de hello sur l’ordinateur hôte de hello. Ensuite, toocreate des sauvegardes cohérentes avec les applications, il vérifie les volumes hello utilisés par une application suggère tooconfigure de groupes de volumes. Gestionnaire d’instantanés StorSimple utilise ces volume groupes toogenerate copies de sauvegarde sont cohérentes avec les applications. (La cohérence des applications existe lorsque tous les fichiers associés et les bases de données sont synchronisés et représentent hello véritable état de l’application hello à un moment précis dans le temps.) 

Les sauvegardes de gestionnaire d’instantanés StorSimple prennent la forme hello d’instantanés incrémentiels, qui capturent uniquement les modifications hello depuis la dernière sauvegarde de hello. Par conséquent, les sauvegardes nécessitent moins d’espace de stockage et peuvent être créées et restaurées rapidement. Gestionnaire d’instantanés StorSimple utilise hello tooensure de Windows Volume Shadow Copy Service (VSS) que les instantanés capturent des données cohérentes avec les applications. (Pour plus d’informations, accédez toohello Integration avec section de Windows Volume Shadow Copy Service). Avec le Gestionnaire d’instantanés StorSimple, vous pouvez créer des planifications de sauvegarde ou effectuer des sauvegardes immédiates en fonction des besoins. Si vous avez besoin des données toorestore à partir d’une sauvegarde, permet de gestionnaire d’instantanés StorSimple, vous sélectionnez à partir d’un catalogue local ou des instantanés cloud. Azure StorSimple restaure uniquement les données de salutation qui sont nécessaire car il est nécessaire, ce qui évite les retards de disponibilité des données pendant les opérations de restauration).

![Architecture du Gestionnaire d’instantanés StorSimple](./media/storsimple-what-is-snapshot-manager/HCS_SSM_Overview.png)

**Architecture du Gestionnaire d’instantanés StorSimple** 

## <a name="support-for-multiple-volume-types"></a>Prise en charge de plusieurs types de volumes
Vous pouvez utiliser hello tooconfigure de gestionnaire d’instantanés StorSimple et sauvegarder hello les types de volumes suivants : 

* **Volumes de base** : un volume de base est une partition unique sur un disque de base. 
* **Volumes simples** : un volume simple est un volume dynamique qui contient l’espace d’un seul disque dynamique. Un volume simple est constitué d’une seule région sur un disque ou de plusieurs régions liées entre elles sur hello même disque. (Vous pouvez créer des volumes simples uniquement sur des disques dynamiques). Les volumes simples ne sont pas tolérants aux pannes.
* **Volumes dynamiques** : un volume dynamique est un volume créé sur un disque dynamique. Les disques dynamiques utilisent une base de données tootrack d’informations sur les volumes qui figurent sur les disques dynamiques d’un ordinateur. 
* **Volumes dynamiques avec mise en miroir** – volumes dynamiques avec mise en miroir reposent sur l’architecture de hello RAID 1. Avec RAID 1, des données identiques sont écrites sur deux ou plusieurs disques, produisant un ensemble en miroir. Une demande de lecture peut ensuite être traitée par n’importe quel disque contenant hello a demandé des données.
* **Volumes partagés de cluster** – avec des volumes partagés de cluster (CSV), plusieurs nœuds dans un cluster de basculement peuvent simultanément lire ou écrire toohello même disque. Basculement d’un nœud tooanother nœud peut se produire rapidement, sans nécessiter une modification de la propriété du lecteur ou de montage, démontage et suppression d’un volume. 

> [!IMPORTANT]
> Ne mélangez pas les volumes partagés de cluster et non-CSV dans hello même instantané. Le mélange de volumes partagés de cluster et de volumes non partagés de cluster dans un instantané n’est pas pris en charge. 
> 
> 

Vous pouvez utiliser des groupes de volume complet de gestionnaire d’instantanés StorSimple toorestore ou cloner des volumes et restaurer des fichiers individuels.

* [Volumes et groupes de volumes](#volumes-and-volume-groups) 
* [Types de sauvegarde et stratégies de sauvegarde](#backup-types-and-backup-policies) 

Pour plus d’informations sur les fonctionnalités du Gestionnaire d’instantanés StorSimple et toouse, voir [interface utilisateur de gestionnaire d’instantanés StorSimple](storsimple-use-snapshot-manager.md).

## <a name="volumes-and-volume-groups"></a>Volumes et groupes de volumes
Avec le Gestionnaire d’instantanés StorSimple, vous créez dans un premier temps des volumes, puis configurez en groupes de volumes. 

Gestionnaire d’instantanés StorSimple utilise volume groupes toocreate copies de sauvegarde sont cohérentes avec les applications. La cohérence des applications existe lorsque tous les fichiers associés et les bases de données sont synchronisés et représentent hello véritable état d’une application à un moment précis dans le temps. Groupes de volumes (également appelés *groupes de cohérence*) base hello d’une sauvegarde ou de travail de restauration.

Groupes de volumes ne sont pas hello identique aux conteneurs de volumes. Un conteneur de volume contient un ou plusieurs volumes qui partagent un compte de stockage cloud et d’autres attributs, tels que le chiffrement et la consommation de bande passante. Un conteneur de volume unique peut contenir des volumes de StorSimple too256 alloués dynamiquement. Pour plus d’informations sur les conteneurs de volumes, consultez trop[gérer vos conteneurs de volumes](storsimple-manage-volume-containers.md). Groupes de volumes sont des ensembles de volumes que vous configurez les opérations de sauvegarde toofacilitate. Si vous sélectionnez deux volumes qui appartiennent les conteneurs de volumes toodifferent, placez-les dans un seul groupe de volumes, puis créer une stratégie de sauvegarde pour ce groupe de volumes, chaque volume est sauvegardé dans le conteneur de volumes approprié hello, à l’aide du stockage approprié de hello compte.

> [!NOTE]
> Tous les volumes d’un groupe de volumes doivent provenir d’un fournisseur de services cloud unique.
> 
> 

## <a name="integration-with-windows-volume-shadow-copy-service"></a>Intégration à Windows Volume Shadow Copy Service
Gestionnaire d’instantanés StorSimple utilise hello données cohérentes avec les applications de toocapture Windows Volume Shadow Copy Service (VSS). VSS facilite la cohérence des applications en communiquant avec prenant en charge VSS applications toocoordinate hello la création d’instantanés incrémentiels. Service VSS vérifie que les applications de hello sont temporairement inactives ou inactive, quand les instantanés sont créés. 

implémentation de gestionnaire d’instantanés StorSimple Hello du service VSS fonctionne avec SQL Server et les volumes NTFS génériques. processus de Hello est comme suit : 

1. Un demandeur, qui est généralement une gestion des données et d’une solution de protection (telles que gestionnaire d’instantanés StorSimple) ou d’une application de sauvegarde, appelle le service VSS et lui demande d’informations à partir du logiciel d’enregistreur hello dans l’application cible de hello toogather.
2. Contacts VSS hello enregistreur composant tooretrieve une description des données de hello. enregistreur de Hello retourne la description hello de hello toobe de données sauvegardée. 
3. Le service VSS indique l’application hello tooprepare du writer hello pour la sauvegarde. enregistreur de Hello prépare les données hello pour la sauvegarde en achevant les transactions ouvertes, mise à jour des journaux de transactions et ainsi de suite et indique à VSS.
4. Le service VSS indique l’enregistreur de hello tootemporarily stop hello de données d’application stocke et assurez-vous qu’aucune donnée n’est écrite toohello volume pendant la création de cliché instantané hello. Cette étape garantit la cohérence des données et ne prend pas plus de 60 secondes.
5. Le service VSS indique un cliché instantané hello fournisseur toocreate hello. Les fournisseurs, qui peuvent être logiciel ou matériel basés, gérer les volumes de hello qui sont en cours d’exécution et créer des copies de clichés instantanés de ces derniers à la demande. Hello fournisseur crée le cliché instantané hello et informe le service VSS lorsqu’elle est effectuée.
6. VSS contacts hello enregistreur toonotify hello application e/s peut reprendre et également tooconfirm qu’e/s a été suspendu au cours de l’ombre copient la création. 
7. Si la copie de hello a réussi, le service VSS renvoie hello demandeur de toohello d’emplacement de la copie. 
8. Si les données ont été enregistrées pendant la création de cliché instantané hello, sauvegarde de hello seront incohérent. VSS supprime le cliché instantané hello et informe le demandeur de hello. Hello demandeur peut répéter le processus de sauvegarde hello automatiquement ou notifier hello administrateur tooretry à une date ultérieure.

Consultez hello après l’illustration.

![Processus VSS](./media/storsimple-what-is-snapshot-manager/HCS_SSM_VSS_process.png)

**Processus du service VSS Windows** 

## <a name="backup-types-and-backup-policies"></a>Types de sauvegarde et stratégies de sauvegarde
Avec Gestionnaire d’instantanés StorSimple, vous pouvez sauvegarder les données et stocker localement et dans le cloud de hello. Vous pouvez utiliser tooback de gestionnaire d’instantanés StorSimple les données immédiatement, ou vous pouvez utiliser une stratégie de sauvegarde de toocreate une planification pour effectuer les sauvegardes automatiquement. Stratégies de sauvegarde vous permettent également de toospecify le nombre d’instantanés à conserver. 

### <a name="backup-types"></a>Types de sauvegarde
Vous pouvez utiliser hello Gestionnaire d’instantanés StorSimple toocreate les types de sauvegardes suivants :

* **Instantanés locaux** – instantanés locaux sont des copies des données de volume sont stockées sur l’appareil StorSimple hello point-à-temps. En règle générale, ce type de sauvegarde peut être créé et restauré rapidement. Vous pouvez utiliser un instantané local comme vous utiliseriez une copie de sauvegarde locale.
* **Instantanés cloud** – instantanés Cloud sont des copies des données de volume sont stockées dans le cloud de hello point-à-temps. Un instantané cloud est équivalent instantané tooa répliqué sur un système de stockage hors site, distinct. Les instantanés cloud sont particulièrement utiles dans les scénarios de récupération d’urgence.

### <a name="on-demand-and-scheduled-backups"></a>Sauvegardes à la demande et planifiées
Avec Gestionnaire d’instantanés StorSimple, vous pouvez lancer une toobe à usage unique de sauvegarde créé immédiatement, ou vous pouvez utiliser un tooschedule de stratégie de sauvegarde périodique des opérations de sauvegarde.

Une stratégie de sauvegarde est un ensemble de règles automatisées que vous pouvez utiliser des sauvegardes régulières tooschedule. Une stratégie de sauvegarde vous permet de toodefine hello fréquence et les paramètres de captures instantanées d’un groupe de volumes spécifique. Vous pouvez utiliser des dates de début et d’expiration de toospecify stratégies, des heures, les fréquences et les conditions de rétention pour locaux et les instantanés cloud. Une stratégie est appliquée dès que vous l’avez définie. 

Vous pouvez utiliser le Gestionnaire d’instantanés StorSimple tooconfigure ou reconfigurer les stratégies de sauvegarde chaque fois que nécessaire. 

Vous configurez hello suivant des informations pour chaque stratégie de sauvegarde que vous créez :

* **Nom** : nom unique de hello Hello sélectionné stratégie de sauvegarde.
* **Type** – hello du type de stratégie de sauvegarde, instantané local ou instantané cloud.
* **Groupe de volumes** – hello volume groupe toowhich hello sélectionné stratégie de sauvegarde est affectée.
* **Rétention** – hello du nombre de copies de sauvegarde tooretain. Si vous cochez hello **tous les** boîte, toutes les copies de sauvegarde sont conservées jusqu'à ce que hello le nombre maximal de copies de sauvegarde par volume est atteint, à quel hello point stratégie échoue et génère un message d’erreur. Vous pouvez également spécifier un nombre de sauvegardes des tooretain (entre 1 et 64).
* **Date** – date hello lorsque la stratégie de sauvegarde hello a été créé.

Pour plus d’informations sur la configuration des stratégies de sauvegarde, accédez trop[toocreate de gestionnaire d’instantanés StorSimple utiliser et gérer des stratégies de sauvegarde](storsimple-snapshot-manager-manage-backup-policies.md).

### <a name="backup-job-monitoring-and-management"></a>Analyse et gestion des tâches de sauvegarde
Vous pouvez utiliser hello toomonitor de gestionnaire d’instantanés StorSimple et gérer des travaux de sauvegarde à venir, planifiés et effectués. En outre, le Gestionnaire d’instantanés StorSimple fournit un catalogue de sauvegarde too64 s’est terminée. Vous pouvez utiliser hello catalogue toofind et restaurer des volumes ou des fichiers individuels. 

Pour plus d’informations sur la surveillance des travaux de sauvegarde, accédez trop[tooview de gestionnaire d’instantanés StorSimple utiliser et gérer des travaux de sauvegarde](storsimple-snapshot-manager-manage-backup-jobs.md).

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [à l’aide du Gestionnaire d’instantanés StorSimple tooadminister votre solution StorSimple](storsimple-snapshot-manager-admin.md).
* [Télécharger le Gestionnaire d’instantanés StorSimple](https://www.microsoft.com/download/details.aspx?id=44220).

