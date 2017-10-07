---
title: "aaaMoving de grandes quantités de données vers/depuis le stockage cloud dans Azure | Documents Microsoft"
description: "Vue d’ensemble de hello différentes méthodes de déplacement tooand de données depuis le stockage Azure."
services: storage
documentationcenter: 
author: JarrettRenshaw
manager: msmets
editor: tysonn
ms.assetid: 5e3947a9-d99b-4108-9d57-3eb67c03e7ba
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: jarrettr
ms.openlocfilehash: 7c8ec9d99cbd48042b8146130c8827f9f25c024d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-tooand-from-azure-storage"></a>Déplacement des données tooand depuis le stockage Azure
Si vous souhaitez toomove local données tooAzure stockage (ou inversement), il existe diverses façons toodo cela. approche Hello qui vous convient le mieux dépend de votre scénario. Cet article fournit un aperçu des différents scénarios et des offres appropriées pour chacun d’eux.

## <a name="building-applications"></a>Création d’applications
Si vous créez une application, le développement par rapport aux API REST de hello ou l’un de nos nombreuses bibliothèques clientes est un tooand de données idéal toomove depuis le stockage Azure.

Azure Storage fournit de riches bibliothèques clientes pour .NET, iOS, Java, Android, la plateforme Windows universelle, Xamarin, C++, Node.JS, PHP, Ruby et Python. les bibliothèques clientes Hello proposent des fonctionnalités avancées telles que des téléchargements parallèles, la journalisation et la logique de nouvelle tentative. Vous pouvez également développer directement sur hello API REST, ce qui peut être appelée par n’importe quel langage qui rend les requêtes HTTP/HTTPS.

Consultez [prise en main Azure Blob Storage](../blobs/storage-dotnet-how-to-use-blobs.md) toolearn plus.

En outre, nous offrons également hello [bibliothèque de déplacement des données de stockage Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) qui est une bibliothèque conçue pour la copie de données tooand hautes performances Azure. Reportez-vous tooour bibliothèque de déplacement des données [documentation](https://github.com/Azure/azure-storage-net-data-movement) toolearn plus. 

## <a name="quickly-viewinginteracting-with-your-data"></a>Affichage/utilisation rapide de vos données
Si vous souhaitez un tooview facilement vos données de stockage Azure tout en ayant tooupload de capacité hello et téléchargez vos données, envisagez d’utiliser un Explorateur de stockage Azure.

Consultez notre liste de [explorateurs de stockage Azure](../storage-explorers.md) toolearn plus.

## <a name="system-administration"></a>Administration système
Si vous devez ou sentez plus à l’aise avec un utilitaire de ligne de commande (par exemple, les administrateurs système), voici quelques options pour vous tooconsider :

### <a name="azcopy"></a>AzCopy
AzCopy est un utilitaire de ligne de commande Windows destiné à hautes performances, copie des données tooand depuis le stockage Azure. Vous pouvez également copier des données au sein d’un compte de stockage ou d’un compte de stockage à l’autre.

Consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md) toolearn plus.

### <a name="azure-powershell"></a>Azure PowerShell
Le module Azure PowerShell fournit des applets de commande pour la gestion des services sur Azure. Il s’agit d’un interpréteur en ligne de commande basé sur les tâches et d’un langage de génération de scripts conçu spécialement pour l’administration de systèmes.

Consultez [à l’aide d’Azure PowerShell avec le stockage Azure](storage-powershell-guide-full.md) toolearn plus.

### <a name="azure-cli"></a>Interface de ligne de commande Azure
L’interface CLI Azure offre un ensemble de commandes multiplateforme open source pour l’utilisation des services Azure. L’interface CLI Azure est disponible sur Windows, OS X et Linux.

Consultez [Using hello CLI d’Azure avec le stockage Azure](../storage-azure-cli.md) toolearn plus.

## <a name="moving-large-amounts-of-data-with-a-slow-network"></a>Déplacement de grandes quantités de données avec un réseau lent
Un des défis majeurs de hello associées au déplacement de grandes quantités de données est le temps de transfert hello. Si vous souhaitez que les données tooget vers/depuis le stockage Azure sans tenir compte des coûts de réseaux ou de l’écriture de code, l’importation/exportation Azure est une solution appropriée.

Consultez [Azure Import/Export](../storage-import-export-service.md) toolearn plus.

## <a name="backing-up-your-data"></a>Sauvegarde de vos données
Si vous devez simplement toobackup votre tooAzure données stockage, Azure Backup est toogo de façon hello. Il s’agit d’une solution puissante pour la sauvegarde des données locales et des machines virtuelles Azure.

Consultez [Azure Backup](../../backup/backup-introduction-to-azure-backup.md) toolearn plus.

## <a name="accessing-your-data-on-premises-and-from-hello-cloud"></a>L’accès à vos données en local et du cloud de hello
Si vous avez besoin d’une solution pour accéder à vos données en local et du cloud de hello, puis vous devez envisager d’utiliser la solution de stockage cloud de Azure hybride, StorSimple. Cette solution se compose d’un appareil physique StorSimple qui stocke intelligemment les données fréquemment utilisées sur des disques SSD, les données occasionnellement utilisées sur des disques durs et les données inactives/de sauvegarde/d’archivage sur Azure Storage.

Consultez [StorSimple](../../storsimple/storsimple-overview.md) toolearn plus.

## <a name="recovering-your-data"></a>Récupération de vos données
Lorsque vous avez des applications et charges de travail local, vous aurez besoin d’une solution qui permet à votre toocontinue d’entreprise en cours d’exécution dans l’événement hello de sinistre. Azure Site Recovery gère la réplication, le basculement et la récupération des machines virtuelles et des serveurs physiques. Les données répliquées sont stockées dans le stockage Azure, ce qui vous besoin de hello tooeliminate pour un centre de données sur site secondaire.

Consultez [Azure Site Recovery](../../site-recovery/site-recovery-overview.md) toolearn plus.
### <a name="moving-data-faq"></a>FAQ sur le déplacement des données :
## <a name="can-i-migrate-vhds-from-one-region-tooanother-without-copying"></a>Puis-je migrer les disques durs virtuels à partir d’une région tooanother sans copier ?
Hello uniquement moyen toocopy disques durs virtuels entre une région donnée toocopy hello entre les comptes de stockage de chaque région. Pour ce faire, vous pouvez utiliser AZCopy. Consulter les données de transfert avec toolearn de l’utilitaire de ligne de commande AzCopy hello plus. Pour les très grandes quantités de données, vous pouvez également utiliser Azure Import/Export. Consultez [Azure Import/Export](https://docs.microsoft.com/en-us/azure/storage/storage-import-export-service) toolearn plus.
