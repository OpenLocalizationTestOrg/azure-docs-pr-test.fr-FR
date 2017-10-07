---
title: "aaaManage stockage Azure à l’aide d’Azure Automation"
description: "Découvrez comment hello service Azure Automation peut être utilisé toomanage stockage Azure à l’échelle."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 5edfba1a9ce1f9c81b5bd0889de19099f3d86fc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a>Gestion d'Azure Storage à l'aide d'Azure Automation
Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisés de vos objets BLOB Azure Storage, les tables et les files d’attente.

## <a name="what-is-azure-automation"></a>Qu'est-ce qu'Azure Automation ?
[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus. À l’aide d’Azure Automation, longues, manuelle, sujette aux erreurs et souvent répété tâches peuvent être automatisés tooincrease fiabilité et l’efficacité et réduire toovalue de temps pour votre organisation.

Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet vos besoins que votre organisation se développe. Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.

Réduire la surcharge opérationnelle et de libérer de l’informatique / toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécutés automatiquement par Azure Automation.

## <a name="how-can-azure-automation-help-manage-azure-storage"></a>Comment Azure Automation peut-il aider à gérer Azure Storage ?
Le stockage Azure peut être géré dans Azure Automation à l’aide des applets de commande hello PowerShell qui sont disponibles dans [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx). Azure Automation dispose de ces applets de commande PowerShell de stockage disponibles en dehors de la zone de hello, afin que vous pouvez effectuer tous les objets blob, de table et de tâches de gestion de file d’attente dans le service de hello. Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.

Hello [galerie de runbooks Azure Automation](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contient une série de produit Communauté et l’équipe runbooks tooget démarré l’automatisation de la gestion du stockage Azure, d’autres services Azure et de 3 systèmes tiers. La galerie de Runbooks inclut :

* [Supprimer des objets blob de stockage Azure avec une certaine ancienneté à l’aide du service Automation](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [Télécharger un objet blob à partir d’Azure Storage](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [Sauvegarder tous les disques d’une machine virtuelle Azure unique ou toutes les machines virtuelles d’un service cloud](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage des objets BLOB de stockage Azure, les tables et les files d’attente, suivez ces liens de toolearn plus sur Azure Automation.

Consultez le didacticiel d’Azure Automation hello [création ou importation d’un runbook dans Azure Automation](../../automation/automation-creating-importing-runbook.md).

