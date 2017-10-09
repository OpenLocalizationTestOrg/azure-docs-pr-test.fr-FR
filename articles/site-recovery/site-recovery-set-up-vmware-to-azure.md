---
title: "Configurer l’environnement source hello (tooAzure VMware) | Documents Microsoft"
description: "Cet article décrit comment tooset de votre toostart d’environnement local Réplication VMware virtual machines tooAzure."
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Configurer l’environnement source hello (tooAzure VMware)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure physique](./site-recovery-set-up-physical-to-azure.md)

Cet article décrit comment tooset de votre toostart d’environnement local réplication virtual machines en cours d’exécution sur VMware tooAzure.

## <a name="prerequisites"></a>Composants requis

article de Hello part du principe que vous avez déjà créé :
- Un coffre Recovery Services Bonjour [portail Azure](http://portal.azure.com "portail Azure").
- Un compte dédié dans votre serveur VMware vCenter qui peut être utilisé pour la [découverte automatique](./site-recovery-vmware-to-azure.md).
- Un ordinateur virtuel sur le serveur de configuration tooinstall hello.

## <a name="configuration-server-minimum-requirements"></a>Configuration minimale requise du serveur
logiciel de serveur de configuration Hello doit être déployé sur un ordinateur virtuel de VMware hautement disponible. Hello tableau suivant répertorie la configuration matérielle minimale hello, de logiciels et de configuration réseau requise pour un serveur de configuration.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Serveurs proxy de basée sur HTTPS ne sont pas pris en charge par le serveur de configuration hello.

## <a name="choose-your-protection-goals"></a>Sélectionner vos objectifs en matière de protection

1. Bonjour portail Azure, accédez à toohello **Services de récupération** Panneau de coffre et sélectionnez votre archivage.
2. Sur le menu de ressource hello de coffre de hello, accédez trop**mise en route** > **Site Recovery** > **étape 1 : préparer l’Infrastructure**  >  **Objectif de protection**.

    ![Sélectionner des objectifs](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. Dans **objectif de Protection**, sélectionnez **tooAzure**, puis choisissez **Oui, avec l’hyperviseur VMware vSphere**. Cliquez ensuite sur **OK**.

    ![Sélectionner des objectifs](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello
Configuration de l’environnement source hello implique deux activités principales :

- Installer et inscrire un serveur de configuration avec Site Recovery.
- Découvrir vos machines virtuelles de local en vous connectant le Site Recovery tooyour local VMware vCenter ou vSphere EXSi hôtes.

### <a name="step-1-install-and-register-a-configuration-server"></a>Étape 1 : Installer et inscrire un serveur de configuration

1. Cliquez sur **Étape 1 : Préparer l’infrastructure** > **Source**. Dans **Prepare source**, si vous n’avez pas un serveur de configuration, cliquez sur **+ serveur de Configuration** tooadd une.

    ![Configurer la source](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. Sur hello **ajouter un serveur** panneau, vérifiez que **serveur de Configuration** s’affiche dans **type de serveur**.
4. Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.
5. Télécharger la clé d’inscription du coffre hello. Vous devez la clé d’inscription de hello lorsque vous exécutez le programme d’installation unifiée. clé de Hello est valide pendant cinq jours après que l’avoir généré.

    ![Configurer la source](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. Sur la machine hello vous utilisez en tant que serveur de configuration hello, exécutez **installation unifiée d’Azure Site Recovery** serveur de configuration tooinstall hello, serveur de processus hello et maître de hello de serveur ciblent.

#### <a name="run-azure-site-recovery-unified-setup"></a>Exécuter le programme d’installation unifiée Azure Site Recovery

> [!TIP]
> L’inscription du serveur de configuration échoue si le temps hello sur l’horloge système de votre ordinateur diffère de l’heure locale de plus de cinq minutes. Synchroniser l’horloge de votre système avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) avant de commencer l’installation de hello.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> serveur de configuration Hello peut être installé via la ligne de commande. Pour plus d’informations, consultez [installation à l’aide des outils de ligne de commande de server configuration hello](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Ajouter compte de VMware hello pour la découverte automatique

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>Étape 2 : Ajouter un serveur vCenter
tooallow Azure Site Recovery toodiscover machines virtuelles en cours d’exécution dans votre environnement local, vous devez tooconnect votre serveur VMware vCenter ou les ordinateurs hôtes ESXi vSphere avec Site Recovery.

Sélectionnez **+ vCenter** toostart connecter un serveur VMware vCenter ou un hôte VMware vSphere ESXi.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Problèmes courants
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Étapes suivantes
[Configurez votre environnement cible](./site-recovery-prepare-target-vmware-to-azure.md) dans Azure.
