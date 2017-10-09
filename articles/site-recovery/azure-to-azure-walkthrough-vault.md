---
title: "aaaSet d’un coffre pour Azure VM repliction entre les régions avec Azure Site Recovery | Documents Microsoft"
description: "Résume les étapes hello nécessaire tooset d’un coffre pour la réplication Azure entre les régions Azure à l’aide d’Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: 40472189-3d80-4963-b175-8bddcbc2f61f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: 9959c59c7ea57114763f13bf060404ddd267ba80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-a-vault-for-azure-tooazure-replication"></a>Étape 4 : Configurer un coffre pour la réplication tooAzure Azure

Après avoir [planification de réseaux](azure-to-azure-walkthrough-network.md), utilisez cette tooset article d’un coffre, pour les machines virtuelles (VM) Azure réplication tooanother région Azure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

- Lorsque vous avez terminé l’article de hello, vous devez disposer d’un coffre Recovery Services configuré.
- Valider les commentaires en bas de hello de cet article, ou poser des questions dans hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



>[!NOTE]
>
> La réplication de machines virtuelles Azure est actuellement disponible en préversion.




## <a name="create-a-vault"></a>création d'un coffre

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Nous vous recommandons de créer le coffre Recovery Services hello dans hello emplacement où votre tooreplicate de machines virtuelles. Par exemple, si votre emplacement cible est hello central US, créer dans le coffre hello **du centre des États-Unis**.


## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 5 : activer la réplication](azure-to-azure-walkthrough-enable-replication.md)
