---
title: aaaHow toouse le stockage Azure pour la sauvegarde et restauration SQL Server | Documents Microsoft
description: "Découvrez comment tooback de SQL Server tooAzure stockage. Explique les avantages de hello de la sauvegarde des bases de données SQL tooAzure stockage."
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>Utilisation du stockage Azure pour la sauvegarde et la restauration de SQL Server
## <a name="overview"></a>Vue d'ensemble
À partir de SQL Server 2012 SP1 CU2, vous pouvez maintenant écrire des sauvegardes SQL Server directement toohello service de stockage d’objets Blob Azure. Vous pouvez utiliser cette tooback la fonctionnalité de restauration tooand à partir du service d’objets Blob Azure hello avec une base de données SQL Server sur site ou d’une base de données SQL Server dans une machine virtuelle Azure. Sauvegarde toocloud offre les avantages de la disponibilité, un stockage hors site géorépliqué et la facilité de migration des données tooand du cloud de hello. Vous pouvez émettre des instructions BACKUP ou RESTORE en utilisant Transact-SQL ou SMO.

SQL Server 2016 introduit de nouvelles fonctionnalités ; Vous pouvez utiliser [sauvegarde d’instantanés de fichiers](http://msdn.microsoft.com/library/mt169363.aspx) tooperform des sauvegardes quasi instantanées et des restaurations extrêmement rapides.

Cette rubrique explique pourquoi vous pouvez choisir toouse le stockage Azure pour les sauvegardes SQL et décrit ensuite les composants hello impliqués. Vous pouvez utiliser les ressources hello fournis à fin hello des procédures pas à pas de hello article tooaccess et toostart des informations supplémentaires à l’aide de ce service avec vos sauvegardes SQL Server.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>Avantages de l’utilisation hello Service d’objets Blob Azure pour les sauvegardes SQL Server
La sauvegarde de SQL Server pose diverses difficultés. Ces défis incluent la gestion de stockage, les risques de défaillance du stockage, l’accès de stockage sur le site de toooff et la configuration matérielle. La plupart de ces défis sont adressées à l’aide du service de magasin d’objets Blob Azure hello pour les sauvegardes de SQL Server. Tenez compte des hello avantages suivants :

* **Facilité d’utilisation**: stockage de vos sauvegardes dans des objets BLOB Azure peut être une option hors site pratique, flexible et facile tooaccess. Création d’un stockage hors site pour vos sauvegardes SQL Server peuvent être aussi simples que la modification de vos scripts/tâches toouse hello **sauvegarde tooURL** syntaxe. Stockage hors site généralement doit être suffisamment éloigné de tooprevent d’emplacement de base de données de production hello un sinistre peut avoir un impact sur les hello hors site et les emplacements de base de données de production. En choisissant trop[géo-répliquer des objets BLOB de votre Azure](../../../storage/common/storage-redundancy.md), vous disposez d’une couche supplémentaire de protection en cas de hello d’un sinistre affecterait l’ensemble de la région hello.
* **Archive de sauvegarde**: hello service de stockage d’objets Blob Azure offre une bande toohello autre souvent utilisé mieux les sauvegardes tooarchive option. Stockage sur bande peut nécessiter le transport physique tooan supports hors site, ainsi que les mesures tooprotect hello. Le stockage de vos sauvegardes dans le service BLOB Azure offre une option d’archivage instantané, hautement disponible et durable.
* **Matériel géré**: il n’y a aucun frais de gestion du matériel avec les services Azure. Services Azure gérer le matériel de hello et fournissent la géo-réplication pour la redondance et la protection contre les défaillances matérielles.
* **Stockage illimité**: en activant un BLOB tooAzure sauvegarde directe, vous avez accès toovirtually stockage illimité. Ou bien, sauvegarde de disque de machine virtuelle Azure tooan y a des limites en fonction de la taille de l’ordinateur. Il existe un toohello limiter le nombre de disques, vous pouvez attacher tooan machine virtuelle Azure pour les sauvegardes. Cette limite est de 16 disques pour une instance très volumineuse et un nombre inférieur pour les instances plus petites.
* **Disponibilité de sauvegarde**: sauvegardes stockées dans des objets BLOB Azure sont accessibles à partir de n’importe quel endroit et à tout moment et peuvent être facilement accessible pour les restaurations tooeither un local SQL Server ou un autre serveur SQL en cours d’exécution dans une Machine virtuelle Azure, sans besoin de hello Pour attacher/détacher la base de données ou de télécharger et attacher hello disque dur virtuel.
* **Coût**: payez uniquement pour le service hello est utilisé. Peut être économique comme option d'archivage hors site et de sauvegarde. Consultez hello [calculatrice de prix Azure](http://go.microsoft.com/fwlink/?LinkId=277060 "calculatrice de tarification")et hello [l’article de la tarification Azure](http://go.microsoft.com/fwlink/?LinkId=277059 "tarification article") pour plus d’informations plus d’informations.
* **Instantanés de stockage**: lorsque les fichiers de base de données sont stockés dans un objet blob Azure et à l’aide de SQL Server 2016, vous pouvez utiliser [sauvegarde d’instantanés de fichiers](http://msdn.microsoft.com/library/mt169363.aspx) tooperform des sauvegardes quasi instantanées et des restaurations extrêmement rapides.

Pour plus d'informations, consultez la page [Sauvegarde et restauration SQL Server avec le service de stockage d'objets blob Azure](http://go.microsoft.com/fwlink/?LinkId=271617).

Hello, les deux sections suivantes présentent le service de stockage d’objets Blob Azure hello, y compris les composants de SQL Server hello requis. Il s’agit de composants de hello toounderstand important et leur interaction toosuccessfully utiliser la sauvegarde et restauration à partir du service de stockage d’objets Blob Azure hello.

## <a name="azure-blob-storage-service-components"></a>Composants du service BLOB Azure
les composants Azure suivants Hello sont utilisées lorsque vous sauvegardez toohello service de stockage d’objets Blob Azure.

| Composant | Description |
| --- | --- |
| **Compte de stockage** |compte de stockage Hello est hello point de départ pour tous les services de stockage. tooaccess un service de stockage d’objets Blob Azure, d’abord créer un compte de stockage Azure. Pour plus d’informations sur le service de stockage d’objets Blob Azure, consultez [comment toouse hello Service de stockage d’objets Blob Azure](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **Conteneur** |Un conteneur fournit un regroupement contenant un nombre illimité d’objets blob. toowrite un tooan de sauvegarde de SQL Server service Blob Azure, vous devez disposer au moins conteneur racine de hello créé. |
| **Objet blob** |fichier de n'importe quel type et de n'importe quelle taille. Les objets BLOB sont adressables en utilisant hello suivant le format d’URL : **https://[storage account].blob.core.windows.net/[container]/[blob]**. Pour plus d’informations sur les blobs, consultez [Présentation des objets blob de blocs et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>Composants SQL Server
les composants de SQL Server suivants Hello sont utilisées lorsque vous sauvegardez toohello service de stockage d’objets Blob Azure.

| Composant | Description |
| --- | --- |
| **URL** |Une URL spécifie un fichier de sauvegarde unique tooa identificateur de ressource uniforme (URI). URL de Hello est utilisé tooprovide hello emplacement et nom du fichier de sauvegarde de SQL Server hello. Hello URL doit pointer objet blob tooan réel et pas simplement un conteneur. Si l’objet blob de hello n’existe pas, il est créé. Si un objet blob existant est spécifié, la sauvegarde échoue, sauf si hello > option WITH FORMAT est spécifiée. Hello Voici un exemple d’URL hello vous devez spécifier dans la commande de sauvegarde de hello : **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**. HTTPS n’est pas requis, mais recommandé. |
| **Informations d'identification** |informations Hello tooconnect requis et authentifient tooAzure service de stockage d’objets Blob sont stockées en tant qu’informations d’identification.  Dans l’ordre pour SQL Server toowrite sauvegardes tooan objets Blob Azure ou une restauration à partir de celui-ci, informations d’identification SQL Server doivent être créée. Pour plus d’informations, consultez [Informations d’identification SQL Server](https://msdn.microsoft.com/library/ms189522.aspx). |

> [!NOTE]
> Si vous choisissez toocopy et téléchargez un fichier de sauvegarde de toohello service de stockage d’objets Blob Azure, vous devez utiliser un type d’objet blob de page comme option de stockage si vous envisagez de toouse ce fichier pour les opérations de restauration. La commande RESTORE depuis un type d’objet blob de blocs échouera avec une erreur.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
1. Création d’un compte Azure si vous n’en avez pas encore. Si vous évaluez Azure, envisagez de hello [version d’évaluation gratuite](https://azure.microsoft.com/free/).
2. Puis vous accédez via un des hello suivant des didacticiels qui vous guident dans la création d’un compte de stockage et d’effectuer une restauration.
   
   * **SQL Server 2014**: [didacticiel : SQL Server 2014 sauvegarde et restauration tooMicrosoft Azure Blob Storage Service](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx).
   * **SQL Server 2016**: [didacticiel : à l’aide du service de stockage d’objets Blob Microsoft Azure hello avec les bases de données SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx)
3. Passez en revue la documentation supplémentaire commençant par [Sauvegarde et restauration SQL Server avec le service de stockage d’objets blob Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

Si vous rencontrez des problèmes, consultez la rubrique de hello [sauvegarde SQL Server tooURL meilleures pratiques et dépannage](https://msdn.microsoft.com/library/jj919149.aspx).

Pour les autres options de sauvegarde et de restauration de SQL Server, voir [Sauvegarde et restauration de SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

