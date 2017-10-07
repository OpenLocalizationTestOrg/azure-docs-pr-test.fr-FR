---
title: "aaaOnline sauvegarde et restauration avec la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment tooperform automatique de sauvegarde et de restauration sur une base de données de la base de données Azure Cosmos."
keywords: sauvegarde et restauration, sauvegarde en ligne
services: cosmos-db
documentationcenter: 
author: RahulPrasad16
manager: jhubbard
editor: monicar
ms.assetid: 98eade4a-7ef4-4667-b167-6603ecd80b79
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/11/2017
ms.author: raprasa
ms.openlocfilehash: a0b464c95681dfc7b5462b02bf04c2c43d6bc16f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Sauvegarde et restauration en ligne automatiques avec Azure Cosmos DB
Azure Cosmos DB sauvegarde automatiquement toutes vos données à intervalles réguliers. les sauvegardes automatiques Hello sont effectuées sans affecter les performances de hello ou la disponibilité de vos opérations de base de données. Toutes vos sauvegardes sont stockées séparément dans un autre service de stockage, et ces sauvegardes sont répliquées globalement pour garantir la résilience contre les sinistres régionaux. les sauvegardes automatiques Hello sont conçues pour les scénarios lorsque vous supprimez accidentellement le conteneur de votre base de données Comos et version ultérieure requièrent la récupération des données ou une solution de récupération d’urgence.  

Cet article commence par un bref récapitulatif de la redondance des données hello et la disponibilité de base de données Cosmos et puis présente les sauvegardes. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Récapitulatif de la haute disponibilité avec Cosmos DB
COSMOS DB est conçue toobe [distribués internationalement](distribute-data-globally.md) : elle vous permet de tooscale débit dans plusieurs régions Azure, ainsi que la stratégie de basculement et son API multihébergement transparent. En tant qu’une offre de système de base de données [disponibilité de 99,99 % SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db), toutes les écritures hello dans Cosmos DB sont des disques toolocal durablement validée par un quorum de réplicas au sein d’un centre de données local avant d’accuser réception toohello client. Notez que hello haute disponibilité de base de données Cosmos s’appuie sur le stockage local et ne dépend pas de toutes les technologies de stockage externe. En outre, si votre compte de base de données est associé à plusieurs régions Azure, vos écritures sont également répliquées entre les autres régions. tooscale vos données de débit et l’accès à faible latence, vous pouvez avoir plusieurs lire régions associées à votre compte de base de données que vous le souhaitez. Dans chaque région de lecture, les données de salutation (répliquée) sont rendue persistante durablement sur un jeu de réplicas.  

Comme illustré dans hello suivant schéma, un seul conteneur de base de données Cosmos est [partitionnées horizontalement](partition-data.md). Une « partition » est indiquée par un cercle Bonjour suivant schéma, et chaque partition devient hautement disponible via un jeu de réplicas. Il s’agit de distribution local hello au sein d’une seule région Azure (signalée par l’axe des X hello). En outre, chaque partition (avec son jeu de réplica correspondant) est ensuite globalement distribuée dans plusieurs régions associées à votre compte de base de données (par exemple, dans cette illustration hello trois régions : États-Unis, ouest des États-Unis et en Inde centrale). Hello « plage de partition » est distribués internationalement entité comprenant plusieurs copies de vos données dans chaque région (signalée par l’axe des Y de hello). Vous pouvez affecter de priorité de régions toohello associées à votre compte de base de données et base de données Cosmos va en toute transparence basculement toohello la zone suivante en cas d’incident. Vous pouvez aussi simuler de basculement tootest hello bout en bout pour la disponibilité de votre application.  

Hello image suivante illustre la grande redondance avec Cosmos DB hello.

![Degré élevé de redondance avec Cosmos DB](./media/online-backup-and-restore/redundancy.png)

![Degré élevé de redondance avec Cosmos DB](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Sauvegardes complètes, automatiques, en ligne
Oups, j’ai supprimé mon conteneur ou ma base de données ! Avec la base de données Cosmos, non seulement vos données, mais les sauvegardes hello de vos données sont également créées les sinistres tooregional hautement résilientes et redondants. Actuellement, ces sauvegardes automatisées sont effectuées environ toutes les quatre heures et les deux sauvegardes les plus récentes sont stockées en permanence. Si les données de salutation sont accidentellement supprimé ou endommagé, veuillez [contactez le support Azure](https://azure.microsoft.com/support/options/) dans les 8 heures. 

sauvegardes de Hello sont effectuées sans affecter les performances de hello ou la disponibilité de vos opérations de base de données. COSMOS DB accepte les sauvegarde hello en arrière-plan de hello sans consommer votre RUs approvisionnés ou affecter les performances de hello et sans affecter la disponibilité de hello de votre base de données. 

Contrairement à vos données sont stockées dans la base de données Cosmos, les sauvegardes automatiques hello sont stockés dans le service de stockage d’objets Blob Azure. téléchargement de faible latence/efficace hello tooguarantee, instantané hello de votre sauvegarde est instance tooan téléchargé de stockage d’objets Blob Azure dans hello même région que hello écriture région actuelle de votre compte de base de données de base de données Cosmos. Pour assurer la résilience contre les sinistres régionaux, chaque instantané de vos données de sauvegarde dans le stockage d’objets Blob Azure à nouveau répliquée à l’aide la région tooanother stockage géo-redondant (GRS). Hello diagramme suivant montre que hello entière Cosmos DB conteneur (avec toutes les trois partitions principales dans l’ouest des États-Unis, dans cet exemple) est sauvegardé dans un compte de stockage d’objets Blob Azure à distance ouest des États-Unis et ensuite GRS répliquées tooEast US. 

Hello image suivante illustre les sauvegardes complètes périodiques de toutes les entités de base de données Cosmos dans le stockage Azure GRS.

![Sauvegardes complètes périodiques de toutes les entités Cosmos DB dans Stockage Azure GRS](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Période de rétention des sauvegardes
Comme décrit ci-dessus, base de données Azure Cosmos prendre des instantanés de vos données toutes les quatre heures et conserve les instantanés de deux derniers hello de chaque partition pendant 30 jours. Conformément à nos obligations réglementaires, les instantanés sont supprimés au bout de 90 jours.

Si vous souhaitez toomaintain vos propres instantanés, vous pouvez utiliser tooJSON l’option d’exportation hello Bonjour Azure Cosmos DB [l’outil de Migration de données](import-data.md#export-to-json-file) tooschedule des sauvegardes supplémentaires. 

## <a name="restoring-a-database-from-an-online-backup"></a>Restauration d’une base de données depuis une sauvegarde en ligne
Si vous supprimez accidentellement votre base de données ou de la collection, vous pouvez [un ticket de support de fichiers](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ou [le support technique Azure](https://azure.microsoft.com/support/options/) toorestore les données de salutation à partir de la dernière sauvegarde d’automatique hello. Si vous devez toorestore votre base de données en raison du problème d’altération des données, consultez [la gestion des données endommagées](#handling-data-corruption) dont vous avez besoin tootake supplémentaire étapes tooprevent hello endommagé données à partir de sauvegardes de hello pénétrer. Pour obtenir un instantané spécifique de votre toobe sauvegarde restaurée, Cosmos DB requiert que les données de salutation n’étaient disponibles pour la durée du cycle de sauvegarde hello pour cet instantané hello.

## <a name="handling-data-corruption"></a>Gestion de l’altération des données
Azure Cosmos DB conserve les sauvegardes de deux derniers hello de chaque partition dans le système de hello. Ce modèle fonctionne très bien quand un conteneur (collection de documents, graphique, table) ou une base de données est accidentellement supprimé, car une des dernières versions de hello peut être restaurée. Toutefois, dans hello cas lorsque lorsque les utilisateurs peuvent présenter un problème d’altération des données, base de données Azure Cosmos peuvent ne pas savoir hello d’altération des données, et il est possible que hello altération peuvent ont été les sauvegardes hello. Dès qu’il est endommagé, vous devez supprimer le conteneur hello endommagé (collection/graphique/table) afin que les sauvegardes sont protégés contre l’écrasement des données corrompues. Depuis la dernière sauvegarde de hello peut être de quatre heures, l’utilisateur de hello peut employer [modifier le flux](change-feed.md) toocapture et magasin hello dernière quatre heures de données avant de supprimer le conteneur de hello.

## <a name="next-steps"></a>Étapes suivantes

reportez-vous à votre base de données dans plusieurs centres de données, tooreplicate [distribuer vos données globalement avec Cosmos DB](distribute-data-globally.md). 

toofile contact prise en charge d’Azure, [soumettent un ticket de hello Azure portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

