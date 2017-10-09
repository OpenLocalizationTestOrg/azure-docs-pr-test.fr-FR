---
title: "aaaReplicate machines virtuelles Azure entre les régions Azure | Des documents Microsoft"
description: "Résume hello étapes requises tooreplicate machines virtuelles Azure entre des régions Azure avec le service d’Azure Site Recovery hello Bonjour portail Azure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 6dd36239-4363-4538-bf80-a18e71b8ec67
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: f4ac386f040945131f8a10f02143437f4441e298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Répliquer des machines virtuelles Azure entre des régions avec Azure Site Recovery

>Cet article fournit une vue d’ensemble de tooreplicate requis des étapes de hello machines virtuelles Azure (VM) dans une région Azure tooAzure machines virtuelles dans une autre région. 

>[!NOTE]
>
> La réplication de machines virtuelles Azure est actuellement disponible en préversion.

Ajouter des commentaires et questions bas hello de cet article ou sur hello [forum Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="step-1-review-architecture"></a>Étape 1 : examen de l’architecture

Avant de commencer le déploiement, passez en revue l’architecture du scénario hello et composants hello toodeploy.

Accédez trop[étape 1 : examen de l’architecture de hello](azure-to-azure-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Étape 2 : Vérifier les conditions préalables

Vérifiez que vous avez hello Azure conditions préalables dans des lieux, y compris un abonnement, les réseaux virtuels, les comptes de stockage et les exigences de la machine virtuelle.

Accédez trop[étape 2 : vérifier les conditions préalables et restrictions](azure-to-azure-walkthrough-prerequisites.md)


## <a name="step-3-plan-networking"></a>Étape 3 : Planifier la mise en réseau

Vérifiez que la connectivité sortante est configurée sur des machines virtuelles de Azure vous voulez tooreplicate et que les connexions du site sont configurées.

Accédez trop[étape 4 : planifier la mise en réseau](azure-to-azure-walkthrough-network.md)



## <a name="step-4-create-a-vault"></a>Étape 4 : créer un coffre 

Vous devez tooset d’un tooorchestrate du coffre Recovery Services et gérez la réplication et spécifiez la région de la source hello.

Accédez trop[étape 4 : créer un coffre](azure-to-azure-walkthrough-vault.md)


## <a name="step-5-enable-replication"></a>Étape 5 : activer la réplication


tooenable la réplication, vous configurez les paramètres de l’emplacement cible, définir une stratégie de réplication et sélectionnez hello machines virtuelles d’Azure que vous souhaitez tooreplicate. Après l’activation, la réplication initiale de hello machine virtuelle se produit.

Accédez trop[étape 5 : activer la réplication](azure-to-azure-walkthrough-enable-replication.md)


## <a name="step-6-run-a-test-failover"></a>Étape 6 : exécuter un test de basculement

Une fois la réplication initiale se termine, et la réplication delta est en cours d’exécution, vous pouvez exécuter un toomake de basculement de test que tout fonctionne comme prévu.

Accédez trop[étape 6 : exécuter un test de basculement](azure-to-azure-walkthrough-test-failover.md)


