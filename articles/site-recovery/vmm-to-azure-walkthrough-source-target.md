---
title: "aaaSet hello source et un cible pour tooAzure de réplication Hyper-V (avec System Center VMM) avec Azure Site Recovery | Documents Microsoft"
description: "Résume les tooset d’étapes hello les paramètres source et cible pour la réplication des ordinateurs virtuels Hyper-V dans VMM clouds tooAzure de stockage avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>Étape 8 : Configurer la source de hello et cible pour tooAzure de réplication Hyper-V (avec VMM)

Après avoir [création d’un coffre](vmm-to-azure-walkthrough-create-vault.md) et en spécifiant ce que vous souhaitez tooreplicate, utilisent cette source de tooconfigure article et cibler des paramètres lors de la réplication des machines virtuelles de Hyper-V sur site dans System Center Virtual Machine Manager (VMM) clouds tooAzure, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

S1. Cliquez sur **Préparer l’infrastructure** > **Source**.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. Dans **Prepare source**, cliquez sur **+ VMM** tooadd un serveur VMM.

    ![Configurer la source](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. Dans **ajouter un serveur**, vérifiez que **serveur System Center VMM** s’affiche dans **type de serveur** et le serveur VMM hello satisfont à hello [conditions préalables et les URL configuration requise](#prerequisites).
4. Téléchargez le fichier d’installation hello fournisseur Azure Site Recovery.
5. Téléchargez la clé d’inscription de hello. Vous en aurez besoin lorsque vous exécuterez le programme d’installation. clé de Hello est valide pendant cinq jours après que l’avoir généré.

    ![Configurer la source](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Installer hello fournisseur sur le serveur VMM de hello

1. Exécutez le fichier de configuration de fournisseur hello sur le serveur VMM de hello.
2. Dans **Microsoft Update**, vous pouvez choisir des mises à jour, pour que celles du fournisseur soient installées conformément à votre stratégie Microsoft Update.
3. Dans **Installation**, acceptez ou modifiez l’emplacement d’installation fournisseur hello par défaut et cliquez sur **installer**.

    ![Emplacement d’installation](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. Lors de l’installation terminée, cliquez sur **inscrire** serveur VMM tooregister hello dans le coffre hello.
5. Bonjour **paramètres du coffre** , cliquez sur **Parcourir** fichier de clé de coffre tooselect hello. Spécifier l’abonnement Azure Site Recovery de hello et de coffre hello.

    ![Enregistrement du serveur](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. Dans **connexion Internet**, spécifiez comment hello fournisseur qui s’exécute sur le serveur VMM de hello se connectera tooSite récupération sur hello internet.

   * Si vous souhaitez hello fournisseur tooconnect directement, sélectionnez **vous connecter directement tooAzure Site Recovery sans proxy**.
   * Si votre proxy existant nécessite une authentification ou si vous souhaitez toouse un proxy personnalisé, sélectionnez **tooAzure Site Recovery à l’aide d’un serveur proxy de connexion**.
   * Si vous utilisez un proxy personnalisé, spécifiez les informations d’identification, le port et adresse de hello.
   * Si vous utilisez un proxy, vous devez avoir déjà hello URL autorisées décrites dans [conditions préalables](#on-premises-prerequisites).
   * Si vous utilisez un proxy personnalisé, un compte RunAs VMM (DRAProxyAccount) est créé automatiquement à l’aide de hello spécifié les informations d’identification de proxy. Configurer le serveur de proxy hello afin que ce compte peut s’authentifier avec succès. paramètres du compte RunAs VMM Hello peuvent être modifiés dans la console VMM hello. Dans **paramètres**, développez **sécurité** > **comptes d’identification**, puis modifiez le mot de passe hello de DRAProxyAccount. Vous devez le service VMM toorestart hello afin que ce paramètre prenne effet.

     ![Internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. Acceptez ou modifiez l’emplacement de hello d’un certificat SSL qui est généré automatiquement pour le chiffrement de données. Ce certificat est utilisé si vous activez le chiffrement des données pour un cloud protégé par Azure dans le portail Azure Site Recovery hello. Conservez ce certificat en sécurité. Lorsque vous exécutez un basculement tooAzure vous en aurez besoin toodecrypt, si le chiffrement des données est activé.
8. Dans **nom du serveur**, spécifiez un serveur VMM à hello tooidentify nom convivial dans le coffre hello. Dans une configuration de cluster, spécifiez le nom de rôle de cluster VMM hello.
9. Activer **synchroniser les métadonnées de cloud**si vous voulez que les métadonnées toosynchronize pour tous les clouds sur le serveur VMM de hello avec le coffre de hello. Cette action ne doit toohappen qu’une seule fois sur chaque serveur. Si vous ne souhaitez pas toosynchronize tous les clouds, vous pouvez laisser ce paramètre désactivé et synchroniser chaque cloud individuellement dans les propriétés du cloud hello dans la console VMM hello. Cliquez sur **inscrire** processus de hello toocomplete.

    ![Enregistrement du serveur](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. L’inscription débute. Une fois l’inscription terminée, le serveur de hello s’affiche dans **Infrastructure Site Recovery** > **serveurs VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Installer l’agent Azure Recovery Services de hello sur les ordinateurs hôtes Hyper-V

1. Une fois que vous avez configuré hello fournisseur, vous devez les fichier d’installation toodownload hello pour hello Azure Recovery Services agent. Exécutez le programme d’installation sur chaque serveur Hyper-V dans hello cloud VMM.

    ![Sites Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. Sous **Vérification de la configuration requise**, cliquez sur **Suivant**. Tous les éléments manquants de la configuration requise sont automatiquement installés.

    ![Prerequisites Recovery Services Agent](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. Dans **les paramètres d’Installation**, acceptez ou modifiez l’emplacement d’installation Bonjour et l’emplacement de cache hello. Vous pouvez configurer le cache de hello sur un lecteur qui dispose d’au moins 5 Go de stockage disponible, mais nous vous recommandons d’un lecteur de cache avec 600 Go ou plus d’espace libre. Cliquez ensuite sur **Installer**.
4. Une fois l’installation terminée, cliquez sur **fermer** toofinish.

    ![Inscrire l’Agent MARS](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>Installer à partir de la ligne de commande
Vous pouvez installer hello Microsoft Azure Recovery Services Agent à partir de la ligne de commande à l’aide de hello commande suivante :

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Configurer internet proxy accès tooSite la récupération à partir d’ordinateurs hôtes Hyper-V

Hello Recovery Services agent en cours d’exécution sur les ordinateurs hôtes Hyper-V doit tooAzure d’accès internet pour la réplication de la machine virtuelle. Si vous accédez à hello internet via un proxy, définissez-le comme suit :

1. Ouvrez le composant logiciel enfichable MMC Microsoft Azure Backup hello sur l’ordinateur hôte Hyper-V de hello. Par défaut, un raccourci pour Microsoft Azure Backup est disponible sur le bureau de hello ou dans C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Dans le composant logiciel enfichable hello, cliquez sur **modifier les propriétés**.
3. Sur hello **Configuration Proxy** onglet, spécifiez les informations du serveur proxy.

    ![Inscrire l’Agent MARS](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. Vérifiez que l’agent hello peut atteindre l’URL de hello décrites dans hello [conditions préalables](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello
Spécifiez toobe de compte de stockage Azure hello utilisée pour la réplication et hello réseau Azure toowhich machines virtuelles Azure se connectera après le basculement.

1. Cliquez sur **Prepare infrastructure** > **cible**, sélectionnez l’abonnement de hello et hello du groupe de ressources où vous souhaitez hello toocreate machines virtuelles ayant basculé. Choisir un modèle de déploiement hello souhaitées toouse dans Azure (classique ou une ressource de gestion) pour hello machines virtuelles ayant basculé.

    ![Storage](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.

    ![Storage](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. Si vous n’avez pas créé un compte de stockage et que vous souhaitez toocreate un à l’aide du Gestionnaire de ressources, cliquez sur **+ compte de stockage** toodo qu’inline.  Sur hello **créer le compte de stockage** panneau spécifier un nom de compte, un type, un abonnement et un emplacement. compte de Hello doit être Bonjour même emplacement que hello de coffre Recovery Services.

   ![Storage](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Si vous voulez toocreate un compte de stockage à l’aide du modèle classique de hello, faire Bonjour portail Azure. [En savoir plus](../storage/common/storage-create-storage-account.md)
   * Si vous utilisez un compte de stockage premium pour les données répliquées, configurez un compte de stockage standard supplémentaire, les journaux de réplication toostore qui capturent des données de site tooon les changements en cours.
5. Si vous n’avez pas créé un réseau Azure et que vous souhaitez toocreate un à l’aide du Gestionnaire de ressources, cliquez sur **+ réseau** toodo qu’inline. Sur hello **créer un réseau virtuel** panneau spécifier un nom de réseau, plage d’adresses, les informations de sous-réseau, abonnement et l’emplacement. réseau de Hello doivent se trouver dans hello même emplacement que hello de coffre Recovery Services.

   ![Réseau](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Si vous voulez toocreate un réseau en utilisant le modèle classique de hello, faire Bonjour portail Azure. [En savoir plus](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).





## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 9 : configurer le mappage réseau](vmm-to-azure-walkthrough-network-mapping.md)
