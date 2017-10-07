---
title: " Gérer un serveur de processus en cours d’exécution dans Azure (Resource Manager) | Microsoft Docs"
description: "Cet article décrit comment tooset d’une restauration automatique processus serveur (Resource Manager) dans Azure."
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Gérer un serveur de processus en cours d’exécution dans Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Gestionnaire de ressources](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Classic ](./site-recovery-vmware-setup-azure-ps-classic.md)

Lors de la restauration automatique, il est recommandé de serveur de processus toodeploy dans Azure s’il existe une latence élevée entre hello réseau virtuel Azure et votre réseau local. Cet article décrit comment vous pouvez définir, configurer et gérer des serveurs de traitement hello s’exécutant dans Azure.

> [!NOTE]
> Cet article est utilisé si vous avez utilisé des toobe **le Gestionnaire de ressources** en tant que modèle de déploiement hello pour les ordinateurs virtuels de hello pendant le basculement. Si vous avez utilisé **classique** en tant que modèle de déploiement hello, suivez les étapes de hello dans [comment tooset & Mettre à configurer un serveur de processus de restauration automatique (classique)](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>Composants requis

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Déployer un serveur de processus dans Azure
1. Bonjour coffre > **Infrastructure Site Recovery** (sous le titre de « Gérer » hello) > **serveurs de Configuration** (titre « Pour VMware et les Machines physiques »), sélectionnez le serveur de configuration hello.
2. Dans la page de détails de Configuration serveur hello qui s’ouvre, cliquez sur « + serveur de traitement »

  ![Galerie Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  Sur hello **ajouter un serveur de processus** page, sélectionnez hello valeurs suivantes

  ![Élément de la galerie Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**Nom du champ**|**Valeur**|
|-|-|
|Choisissez où vous souhaitez toodeploy votre serveur de processus|Sélectionnez la valeur de hello **déployer un serveur de processus de restauration dans Azure** |
|Abonnement|Sélectionnez hello abonnement Azure où vous hello machines virtuelles ayant basculé|
|Groupe de ressources|Vous pouvez créer un groupe de ressources de toodeploy ce serveur de processus ou choisissez un serveur de processus toodeploy hello dans un groupe de ressources existant|
|Lieu|Sélectionnez le centre de données Azure hello dans laquelle les ordinateurs virtuels hello où basculé dans|
|Réseau Azure|Sélectionnez hello Network(VNet) virtuel Azure qui hello des machines virtuelles où basculé dans. Si vous avez basculé des machines virtuelles dans plusieurs réseaux virtuels Azure, vous devez déployer un serveur de processus pour chaque réseau virtuel|

4. Renseignez hello autres propriétés hello pour serveur de processus hello

  ![Récapitulatif Ajouter un serveur de processus](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**Nom du champ**|**Valeur**|
|-|-|
|Nom du serveur|Nom d’affichage et nom d’hôte de la machine virtuelle de votre serveur processus|
| User Name|Nom d’utilisateur qui devient un administrateur sur cette machine virtuelle|
|Compte de stockage|Nom de compte de stockage où est placé les du disque virtuel hello machine virtuelle de hello|
|Sous-réseau|sous-réseau Hello de machine virtuelle de hello réseau virtuel Azure toowhich hello est connecté.|
| Adresse IP|Adresse IP que vous aimeriez hello processus serveur tooassume une fois qu’il démarre|
5. Cliquez sur toostart de bouton OK hello déploiement d’ordinateur virtuel de hello processus serveur.

> [!NOTE]
> toouse en mesure de toobe ce serveur de processus pour la restauration automatique, vous devez tooregister avec le serveur de configuration local hello.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>L’inscription hello processus serveur (en cours d’exécution dans Azure) tooa Configuration serveur (local)

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>La mise à niveau hello processus toolatest version du serveur.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Annuler l’inscription du serveur de processus hello (en cours d’exécution dans Azure) à partir d’un serveur de Configuration (en cours d’exécution locale)

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
