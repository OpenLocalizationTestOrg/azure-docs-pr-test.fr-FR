---
title: "Continuité des activités et récupération d’urgence (BCDR) : régions jumelées d’Azure | Microsoft Docs"
description: "En savoir plus sur Azure régional tooensure de jumelage, que les applications sont résilientes lors de pannes de centre de données."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: c2d0a21c-2564-4d42-991a-bc31723f61a4
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 68a3a33a8e768c72fa296d42c9ab97049232d169
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="business-continuity-and-disaster-recovery-bcdr-azure-paired-regions"></a>Continuité des activités et récupération d’urgence (BCDR) : régions jumelées d’Azure

## <a name="what-are-paired-regions"></a>Régions jumelées : définition

Azure fonctionne dans différents emplacements géographiques monde hello. Un emplacement géographique Azure est une zone de hello world qui contient au moins une région Azure. Une région Azure est une zone géographique contenant un ou plusieurs centres de données.

Chaque région Azure est associée à une autre région de hello même geography, créant ainsi une paire régionale. exception de Hello est sud du Brésil, qui est associé à une région à l’extérieur de son geography.

![AzureGeography](./media/best-practices-availability-paired-regions/GeoRegionDataCenter.png)

Figure 1 – Diagramme de paire régionale Azure

| Geography | Régions jumelées |  |
|:--- |:--- |:--- |
| Asie |Est de l'Asie |Asie du Sud-Est |
| Australie |Est de l’Australie |Sud-est de l’Australie |
| Canada |Centre du Canada |Est du Canada |
| Chine |Chine du Nord |Chine orientale|
| Inde |Inde centrale |Inde du Sud |
| Japon |Est du Japon |Ouest du Japon |
| Corée du Sud |Centre de la Corée |Corée du Sud |
| Amérique du Nord |États-Unis - partie centrale septentrionale |Centre-Sud des États-Unis |
| Amérique du Nord |Est des États-Unis |Ouest des États-Unis |
| Amérique du Nord |Est des États-Unis 2 |Centre des États-Unis |
| Amérique du Nord |Ouest des États-Unis 2 |Ouest-Centre des États-Unis |
| Europe |Europe du Nord |Europe de l’Ouest |
| Japon |Est du Japon |Ouest du Japon |
| Brésil |Sud du Brésil (1) |États-Unis - partie centrale méridionale |
| Gouvernement américain |Gouvernement américain - Iowa |Gouvernement américain - Virginie |
| Gouvernement américain |Gouvernement américain - Virginie |Gouvernement des États-Unis – Texas |
| Gouvernement américain |Gouvernement des États-Unis – Texas |Gouvernement des États-Unis – Arizona |
| Gouvernement américain |Gouvernement des États-Unis – Arizona |Gouvernement des États-Unis – Texas |
| Royaume-Uni |Ouest du Royaume-Uni |Sud du Royaume-Uni |
| Allemagne |Centre de l’Allemagne |Nord-Est de l’Allemagne |

Tableau 1 - Mise en correspondance des paires régionales Azure

> (1) La région Sud du Brésil est unique, car elle est jumelée avec une région située en dehors de sa propre zone géographique. La région secondaire de la région Sud du Brésil est Sud-Centre des États-Unis mais la région secondaire de la région Sud-Centre des États-Unis n’est pas Sud du Brésil.


Nous vous recommandons de répliquer les charges de travail entre toobenefit paires régionaux à partir de stratégies d’isolation et la disponibilité de Azure. Par exemple, les mises à jour système Azure planifié sont déployés séquentiellement (pas à hello simultanément) entre les régions associées. Cela signifie que même dans hello rares cas d’une mise à jour est défectueux, les deux régions ne sont pas affectées simultanément. En outre, dans le cas improbable hello d’une panne de large, récupération d’au moins une région en dehors de chaque paire est prioritaire.

## <a name="an-example-of-paired-regions"></a>Exemple de régions jumelées
Figure 2 ci-dessous illustre une application hypothétique qui utilise la paire de régionaux hello pour la récupération d’urgence. nombres de Hello vert mettre en surbrillance les activités entre régions hello trois services Azure (Azure de calcul, stockage et la base de données) et comment ils sont configurés tooreplicate entre les régions. avantages uniques de Hello de déploiement dans les régions associées sont mises en surbrillance par des nombres hello orange.

![Vue d’ensemble des avantages des région jumelées](./media/best-practices-availability-paired-regions/PairedRegionsOverview2.png)

Figure 2 – Paire régionale Azure hypothétique

## <a name="cross-region-activities"></a>Activités entre régions
En tant que tooin visé figure 2.

![PaaS](./media/best-practices-availability-paired-regions/1Green.png) **de calcul Azure (PaaS)** – vous devez configurer les ressources de calcul supplémentaires à l’avance tooensure ressources sont disponibles dans une autre région lors d’un incident. Pour plus d’informations, consultez le [Guide technique de la résilience Azure](resiliency/resiliency-technical-guidance.md).

![Storage](./media/best-practices-availability-paired-regions/2Green.png)**Azure Storage** - Le stockage géo-redondant (GRS, Geo-Redundant Storage) est configuré par défaut quand vous créez un compte de stockage Azure. Avec GRS, vos données sont répliquées automatiquement trois fois au sein de la région principale de hello et trois fois dans la région associée de hello. Pour plus d'informations, consultez [Options de redondance du stockage Azure](storage/common/storage-redundancy.md).

![SQL Azure](./media/best-practices-availability-paired-regions/3Green.png) **bases de données SQL Azure** – avec Azure SQL géo-réplication Standard, vous pouvez configurer la réplication asynchrone de la région associée tooa de transactions. Avec la géo-réplication premium, vous pouvez configurer région tooany de réplication dans Bonjour ; Toutefois, nous vous recommandons de que déployer ces ressources dans une région associée pour la plupart des scénarios de récupération d’urgence. Pour plus d’informations, consultez la rubrique concernant la [géoréplication dans la base de données SQL Azure](sql-database/sql-database-geo-replication-overview.md).

![Resource Manager](./media/best-practices-availability-paired-regions/4Green.png)**Azure Resource Manager** - Resource Manager offre par nature une isolation logique des composants de gestion de service entre les régions. Cela signifie que les erreurs logiques dans une région sont moins susceptibles de tooimpact un autre.

## <a name="benefits-of-paired-regions"></a>Avantages des régions jumelées
En tant que tooin visé figure 2.  

![Isolation](./media/best-practices-availability-paired-regions/5Orange.png)
**Isolation physique** – Quand cela est possible, Azure préfère une séparation de 483 kilomètres (300 miles) au moins entre les centres de données d’une paire régionale, même si ce n’est pas pratique, voire impossible dans toutes les régions géographiques. Séparation du centre de données physique réduit la probabilité de hello de catastrophes naturelles, troubles civils, pannes de courant ou les pannes de réseau physique qui affectent les deux régions à la fois. L’isolation est contraintes toohello sujet geography hello (taille de la géographie, disponibilité de l’infrastructure réseau et l’alimentation, réglementations, etc.).  

![Réplication](./media/best-practices-availability-paired-regions/6Orange.png)
**réplication fournie par la plateforme** -certains services tels que le stockage géo-redondant fournissent la région associée toohello de réplication automatique.

![Récupération](./media/best-practices-availability-paired-regions/7Orange.png)
**commande de récupération de la région** : événement hello d’une panne de large, la récupération d’une région est prioritée hors de chaque paire. Les applications qui sont déployées sur les régions associées sont garanties toohave une des régions de hello récupérée avec une priorité. Si une application est déployée sur des régions qui ne sont pas combinées, récupération peut être retardée – Bonjour pire des régions choisi hello cas peut être hello toobe deux derniers récupérée.

![Les mises à jour](./media/best-practices-availability-paired-regions/8Orange.png)
**mises à jour séquentielles** – planifié système mise à jour est transférées toopaired régions séquentiellement (pas à hello simultanément) toominimize effet hello des bogues et des erreurs logiques dans rarement hello, temps d’arrêt une mise à jour incorrecte.

![Données](./media/best-practices-availability-paired-regions/9Orange.png)
**délégation de données** – une région trouve dans hello même geography en tant que sa paire (à l’exception de hello du sud du Brésil) ordre toomeet délégation besoins à des fins de taxes et de la loi mise en œuvre juridiction.
