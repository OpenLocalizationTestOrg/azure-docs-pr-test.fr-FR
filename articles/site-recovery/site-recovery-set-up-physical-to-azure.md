---
title: "Configurer l’environnement source hello (tooAzure serveurs physiques) | Documents Microsoft"
description: "Cet article décrit comment tooset de votre toostart d’environnement local réplication des serveurs physiques exécutant Windows ou Linux dans Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Configurer l’environnement source hello (serveur physique tooAzure)
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [TooAzure physique](./site-recovery-set-up-physical-to-azure.md)

Cet article décrit comment tooset de votre toostart d’environnement local réplication des serveurs physiques exécutant Windows ou Linux dans Azure.

## <a name="prerequisites"></a>Composants requis

article de Hello suppose que vous avez déjà :
1. Un coffre Recovery Services Bonjour [portail Azure](http://portal.azure.com "portail Azure").
3. Un ordinateur physique sur le serveur de configuration tooinstall hello.

### <a name="configuration-server-minimum-requirements"></a>Configuration minimale requise du serveur
Hello tableau suivant répertorie la configuration matérielle minimale hello, de logiciels et de configuration réseau requise pour un serveur de configuration.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> Serveurs proxy de basée sur HTTPS ne sont pas pris en charge par le serveur de configuration hello.

## <a name="choose-your-protection-goals"></a>Sélectionner vos objectifs en matière de protection

1. Bonjour portail Azure, accédez à toohello **Services de récupération** panneau les coffres et sélectionnez votre archivage.
2. Bonjour **ressource** menu du coffre de hello, cliquez sur **mise en route** > **Site Recovery** > **étape 1 : préparer Infrastructure** > **objectif de Protection**.

    ![Sélectionner des objectifs](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. Dans **objectif de Protection**, sélectionnez **tooAzure** et **non virtualisé,**, puis cliquez sur **OK**.

    ![Sélectionner des objectifs](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

1. Dans **Prepare source**, si vous n’avez pas un serveur de configuration, cliquez sur **+ serveur de Configuration** tooadd une.

  ![Configurer la source](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. Bonjour **ajouter un serveur** panneau, vérifiez que **serveur de Configuration** s’affiche dans **type de serveur**.
4. Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.
5. Télécharger la clé d’inscription du coffre hello. Vous devez la clé d’inscription de hello lorsque vous exécutez le programme d’installation unifiée. clé de Hello est valide pendant cinq jours après que l’avoir généré.

    ![Configurer la source](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. Sur la machine hello vous utilisez en tant que serveur de configuration hello, exécutez **installation unifiée d’Azure Site Recovery** serveur de configuration tooinstall hello, serveur de processus hello et maître de hello de serveur ciblent.

#### <a name="run-azure-site-recovery-unified-setup"></a>Exécuter le programme d’installation unifiée Azure Site Recovery

> [!TIP]
> L’inscription du serveur de configuration échoue si les temps de hello sur l’horloge système de votre ordinateur est plus de cinq minutes sur une heure locale. Synchroniser l’horloge de votre système avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) avant de commencer l’installation de hello.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> serveur de configuration Hello peut être installé via une ligne de commande. Pour plus d’informations, consultez [Installation du serveur de configuration à l’aide des outils en ligne de commande](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Problèmes courants

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Étapes suivantes

L’étape suivante consiste en la [configuration de votre environnement cible](./site-recovery-prepare-target-physical-to-azure.md) dans Azure.
