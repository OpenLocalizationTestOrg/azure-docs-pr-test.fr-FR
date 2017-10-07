---
title: " Gérer un serveur de processus en cours d’exécution dans Azure (Classic) | Microsoft Docs"
description: "Cet article décrit comment tooset d’une restauration automatique du processus Server(Classic) dans Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>Gérer un serveur de processus en cours d’exécution dans Azure (Classic)
> [!div class="op_single_selector"]
> * [Azure Classic ](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Gestionnaire de ressources](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

Lors de la restauration automatique, il est recommandé de toodeploy serveur de traitement dans Azure s’il existe une latence élevée entre hello réseau virtuel Azure et votre réseau local. Cet article décrit comment vous pouvez définir, configurer et gérer des serveurs de traitement hello s’exécutant dans Azure.

> [!NOTE]
> Cet article est toobe utilisé si vous avez utilisé classique en tant que modèle de déploiement hello pour les ordinateurs virtuels de hello pendant le basculement. Si vous avez utilisé le Gestionnaire de ressources comme hello des étapes de déploiement modèle suivent hello dans [comment tooset & Mettre à configurer un serveur de processus de restauration automatique (Resource Manager).](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Composants requis

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Déployer un serveur de processus dans Azure

1. Dans Azure Marketplace, créez un ordinateur virtuel à l’aide de hello **processus serveur V2 de Microsoft Azure Site Recovery** </br>
    ![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. Vérifiez que vous sélectionnez le modèle de déploiement hello en tant que **classique** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. Dans l’Assistant de création de machine virtuelle hello > Paramètres de base, veillez à sélectionner toowhere d’abonnement et l’emplacement hello vous hello machines virtuelles ayant basculé.</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Vérifiez que l’ordinateur virtuel hello est connecté hello de toowhich toohello réseau virtuel Azure a échoué sur l’ordinateur virtuel est connecté.</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Une fois que la machine virtuelle de processus serveur hello est configuré, vous devez toolog dans et l’inscrivez auprès de hello serveur de Configuration.

> [!NOTE]
> toouse en mesure de toobe ce serveur de processus pour la restauration automatique, vous devez tooregister avec le serveur de configuration local hello.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>L’inscription de serveur de processus (en cours d’exécution dans Azure) de hello tooa Configuration serveur (local)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>La mise à niveau de version de toolatest hello serveur de processus.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Hello Désinscription du serveur de processus (en cours d’exécution dans Azure) à partir d’un serveur de Configuration (en cours d’exécution locale)

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
