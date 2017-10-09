---
title: "aaaSQL exercices de récupération d’urgence de base de données | Documents Microsoft"
description: "Découvrez les conseils et meilleures pratiques pour l’utilisation de conserver toohelp de base de données SQL Azure tooperform d’urgence récupération extrait vers votre mission critiques applications résilientes toofailures et les pannes."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: b44a269c-fe2a-404f-b013-290030860bd1
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/31/2016
ms.author: sashan
ms.openlocfilehash: bf17857a19fdebddf0d4f55e4db3a1b33efb4e8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-disaster-recovery-drill"></a>Exécution d'un exercice de récupération d'urgence
Nous recommandons de valider régulièrement la préparation des applications à la récupération. Ce basculement implique un comportement de l’application hello vérification et les implications de l’interruption hello et/ou de perte de données est une bonne pratique d’ingénierie. Il s'agit également d'une exigence figurant dans la plupart des normes industrielles dans le cadre d'une certification de la continuité des activités.

L'exécution d'un exercice de récupération d'urgence comprend :

* la simulation d'une défaillance des couches de données
* la récupération
* la validation de l'intégrité des applications après la récupération

Selon la manière dont vous [conçu votre application pour la continuité d’activité](sql-database-business-continuity.md), extraction de hello tooexecute hello du flux de travail peut varier. Ci-dessous, nous décrivons hello meilleures pratiques effectuer un exercice de récupération d’urgence dans un contexte hello de base de données SQL Azure.

## <a name="geo-restore"></a>Géo-restauration
tooprevent hello perdre des données lors de l’exécution d’un exercice de récupération d’urgence, nous vous recommandons drill hello à l’aide d’un environnement de test en créant une copie de l’environnement de production hello et de l’utiliser le flux de travail de l’application tooverify hello basculement.

#### <a name="outage-simulation"></a>Simulation d'une défaillance
toosimulate hello panne, vous pouvez supprimer ou renommer la base de données source hello. Cela entraîne des échecs de connexion de l’application.

#### <a name="recovery"></a>Récupérer
* Effectuer hello géo-restauration de base de données hello dans un autre serveur comme décrit [ici](sql-database-disaster-recovery.md).
* Modification hello application configuration tooconnect toohello récupérée de base de données et suivez hello [configurer une base de données après récupération](sql-database-disaster-recovery.md) guide de récupération de hello toocomplete.

#### <a name="validation"></a>Validation
* Extraction de hello complète en vérifiant la récupération de valider l’intégrité application hello (y compris les chaînes de connexion, de connexions, de test des fonctionnalités de base ou de l’autre partie de validations de procédures d’approbations d’application standard).

## <a name="geo-replication"></a>Géoréplication
Pour une base de données qui est protégé à l’aide d’extraction de hello géo-réplication exercice implique la base de données secondaire de basculement planifié toohello. Hello basculement planifié garantit que hello principal et les bases de données secondaires hello restent synchronisés lorsque le basculement des rôles de hello. Contrairement aux hello basculement non planifié, cette opération n’entraîne pas de perte de données, afin de l’extraction de hello peut être effectuée dans l’environnement de production hello.

#### <a name="outage-simulation"></a>Simulation d'une défaillance
panne de hello toosimulate, vous pouvez désactiver hello web application ou un ordinateur virtuel connecté toohello base de données. Cela entraîne des défaillances de connectivité hello pour les clients web hello.

#### <a name="recovery"></a>Récupérer
* Vérifiez que configuration de l’application hello dans hello DR région points toohello ancien secondaire qui devient hello entièrement accessible nouveau réplica principal.
* Effectuer [le basculement planifié](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) un nouveau principal de base de données secondaire de hello toomake
* Suivez hello [configurer une base de données après récupération](sql-database-disaster-recovery.md) guide de récupération de hello toocomplete.

#### <a name="validation"></a>Validation
* Extraction de hello complète en vérifiant la récupération de valider l’intégrité application hello (y compris les chaînes de connexion, de connexions, de test des fonctionnalités de base ou de l’autre partie de validations de procédures d’approbations d’application standard).

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur les scénarios de continuité d’activité d’entreprise, consultez [des scénarios de continuité des activités](sql-database-business-continuity.md)
* toolearn sur les sauvegardes de base de données SQL Azure automatisée, consultez [sauvegardes automatisées de base de données SQL](sql-database-automated-backups.md)
* toolearn sur l’utilisation des sauvegardes automatisées pour la récupération, consultez [restaurer une base de données à partir de sauvegardes de hello initiées par le service](sql-database-recovery-using-backups.md)
* toolearn sur les options de récupération plus rapides, consultez [géo-réplication active](sql-database-geo-replication-overview.md)  
