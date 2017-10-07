---
title: "aaaMigrate machines virtuelles à partir de AWS tooAzure | Documents Microsoft"
description: "Cet article décrit comment toomigrate virtual machines en cours d’exécution dans tooAzure Amazon Web Services (AWS) à l’aide d’Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a>Migrer des ordinateurs virtuels dans tooAzure Amazon Web Services (AWS) avec Azure Site Recovery

Cet article décrit le fonctionnement des instances toomigrate AWS Windows virtuels tooAzure avec hello [Azure Site Recovery](site-recovery-overview.md) service.

La migration est en réalité un basculement à partir de AWS tooAzure. Vous ne pouvez pas la restauration automatique machines tooAWS, et il n’est pas en cours de réplication. Cet article décrit les étapes de hello pour la migration dans hello portail Azure et sont basées sur les instructions hello pour [répliquer un ordinateur physique de tooAzure](site-recovery-vmware-to-azure.md).

Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

## <a name="supported-operating-systems"></a>Systèmes d’exploitation pris en charge

Récupération de site peut être utilisé toomigrate EC2 les instances des hello suivant des systèmes d’exploitation en cours d’exécution :

- Windows (64 bits uniquement)
    - Windows Server 2008 R2 SP1+ (pilotes PV Citrix AWS uniquement. **Les instances qui exécutent des pilotes PV RedHat ne sont pas pris en charge**) Windows Server 2012 Windows Server 2012 R2
- Linux (64 bits uniquement)
    - Red Hat Enterprise Linux 6.7 (instances virtualisées HVM uniquement)

## <a name="prerequisites"></a>Composants requis

Voici ce dont vous avez besoin pour ce déploiement :

* **Serveur de configuration**: un Amazon EC2 exécution des machines virtuelles Windows Server 2012 R2 est déployé comme serveur de configuration hello. Par défaut, hello autres composants Azure Site Recovery (serveur de processus et un serveur cible maître) sont installés lorsque vous déployez le serveur de configuration hello. Cet article décrit les étapes de hello pour la migration dans hello portail Azure et sont basées sur les instructions hello pour [en savoir plus](site-recovery-components.md)

* **Les instances EC2**: hello Amazon EC2 instances de machines virtuelles que vous souhaitez toomigrate.

## <a name="deployment-steps"></a>Étapes du déploiement

1. Créez un coffre Recovery Services.
2. Hello groupe de sécurité de vos instances EC2 doit avoir des règles configurées tooallow communiquer instance EC2 de hello que vous voulez toomigrate et instance hello sur lequel vous comptez toodeploy hello serveur de Configuration.

3. Sur hello même Cloud privé virtuel Amazon en tant que vos instances EC2, déployez un serveur de configuration du système. Consultez hello VMware / physiques tooAzure les conditions préalables requises pour les spécifications de déploiement de serveur de configuration.

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  Une fois que votre serveur de configuration est déployée dans AWS et inscrit avec votre coffre Recovery Services, vous devez voir serveur de configuration hello et serveur de processus sous l’infrastructure de la récupération de Site comme indiqué ci-dessous :

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. Une fois que vous avez déployé le serveur de configuration hello (elle peut prendre too15 minustes pour qu’il tooappear), valider qu’il peut communiquer avec des machines virtuelles de hello que vous souhaitez toomigrate.

6. [Configurer les paramètres de réplication](site-recovery-setup-replication-settings-vmware.md).

7. Activer la réplication : activer la réplication pour hello machines virtuelles que vous souhaitez toomigrate. Vous pouvez détecter les instances de EC2 hello à l’aide d’adresses IP privées hello, que vous pouvez obtenir à partir de la console de EC2 hello.

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. Une fois que les instances de hello EC2 ont été protégés et hello réplication tooAzure est terminée, [exécuter un Test de basculement](site-recovery-test-failover-to-azure.md) toovalidate les performances de votre application dans Azure.

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. Exécuter un basculement à partir de AWS tooAzure pour chaque machine virtuelle. Si vous le souhaitez, vous pouvez créer un plan de récupération et exécuter un basculement, toomigrate plusieurs ordinateurs virtuels à partir de AWS tooAzure. [Découvrez d’autres informations](site-recovery-create-recovery-plans.md) sur les plans de récupération.

10. Pour la migration, vous n’avez pas besoin toocommit un basculement. Au lieu de cela, vous sélectionnez l’option d’effectuer la Migration de hello pour chaque ordinateur, vous souhaitez toomigrate. Hello action d’effectuer la Migration se termine les processus de migration hello, supprime la réplication pour l’ordinateur de hello et arrête la récupération de Site de facturation pour l’ordinateur de hello.

    ![Migrer](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a>Étapes suivantes

- [Préparer les ordinateurs migrés tooenable réplication](site-recovery-azure-to-azure-after-migration.md) région tooanother pour les besoins de récupération d’urgence.
- Commencez à protéger vos charges de travail en [répliquant des machines virtuelles Azure.](site-recovery-azure-to-azure.md)
