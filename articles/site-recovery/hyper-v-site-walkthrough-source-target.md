---
title: "aaaSet hello source et un cible pour tooAzure de réplication Hyper-V (sans System Center VMM) avec Azure Site Recovery | Documents Microsoft"
description: "Résume les tooset d’étapes hello les paramètres source et cible pour la réplication de stockage de tooAzure d’ordinateurs virtuels Hyper-V avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a>Étape 8 : Configurer la source de hello et cible pour tooAzure de réplication Hyper-V

Cet article décrit comment tooconfigure les paramètres de source et cible lors de la réplication locale tooAzure d’ordinateurs virtuels (sans System Center VMM) Hyper-V, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Configurer le site de hello Hyper-V, installer hello fournisseur Azure Site Recovery et hello Azure Recovery Services agent sur les ordinateurs hôtes Hyper-V et inscrire le site de hello dans le coffre hello.

1. Dans **Préparer l’infrastructure**, cliquez sur **Source**. tooadd un nouveau site Hyper-V en tant que conteneur pour vos ordinateurs hôtes Hyper-V ou des clusters, cliquez sur **+ Site Hyper-V**.

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. Dans **site Hyper-V créer**, spécifiez un nom pour le site de hello. Cliquez ensuite sur **OK**. À présent, sélectionnez site hello vous créé, puis cliquez sur **+ Hyper-V Server** tooadd un site toohello du serveur.

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. Dans **Ajouter un serveur** > **Type de serveur**, vérifiez que **Serveur Hyper-V** est affiché.

    - Assurez-vous que server hello Hyper-V que vous souhaitez tooadd est conforme à hello [conditions préalables](#on-premises-prerequisites), et est en mesure de tooaccess hello URL spécifiées.
    - Téléchargez le fichier d’installation hello fournisseur Azure Site Recovery. Vous exécutez cette hello tooinstall de fichier fournisseur et hello agent Recovery Services sur chaque ordinateur hôte Hyper-V.

    ![Configurer la source](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a>Installer hello fournisseur et l’agent

1. Exécutez le fichier de configuration de fournisseur hello sur chaque ordinateur hôte ajouté toohello Hyper-V site. Si vous effectuez l’installation sur un cluster Hyper-V, exécutez le programme d’installation sur chaque nœud du cluster. L’installation et l’inscription de chaque nœud de cluster Hyper-V permettent de s’assurer que les machines virtuelles sont protégées, même si elles migrent entre les nœuds.
2. Dans **Microsoft Update**, vous pouvez choisir des mises à jour, pour que celles du fournisseur soient installées conformément à votre stratégie Microsoft Update.
3. Dans **Installation**, acceptez ou modifiez l’emplacement d’installation fournisseur hello par défaut et cliquez sur **installer**.
4. Dans **paramètres du coffre**, cliquez sur **Parcourir** tooselect hello coffre fichier de clé que vous avez téléchargé. Spécifier l’abonnement Azure Site Recovery de hello, nom du coffre hello, et hello Hyper-V site toowhich hello Hyper-V serveur appartient.

    ![Enregistrement du serveur](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. Dans **paramètres Proxy**, spécifiez comment hello fournisseur en cours d’exécution sur les ordinateurs hôtes Hyper-V connecte tooAzure Site Recovery via hello internet.

    * Si vous souhaitez sélectionner directement que hello fournisseur tooconnect **vous connecter directement tooAzure Site Recovery sans proxy**.
    * Si votre proxy existant nécessite une authentification, ou que vous souhaitez toouse un proxy personnalisé pour la connexion du fournisseur hello, sélectionnez **tooAzure Site Recovery à l’aide d’un serveur proxy de connexion**.
    * Si vous utilisez un proxy :
        - Spécifiez les informations d’identification, le port et adresse de hello
        - Vérifiez que hello URL décrites dans hello [conditions préalables](#prerequisites) sont autorisées via le proxy hello.

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. Une fois l’installation terminée, cliquez sur **inscrire** serveur hello de tooregister dans le coffre hello.

    ![Emplacement d’installation](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. Une fois l’inscription terminée, les métadonnées à partir du serveur de hello Hyper-V sont récupérées par Azure Site Recovery et hello serveur s’affiche dans **Infrastructure Site Recovery** > **hôtes Hyper-V**.


## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello

Spécifiez le compte de stockage Azure hello pour la réplication et hello réseau Azure toowhich machines virtuelles Azure se connectera après le basculement.

1. Cliquez sur **Préparer l’infrastructure** > **Cible**.
2. Sélectionnez l’abonnement de hello et groupe de ressources hello dans lequel vous souhaitez toocreate hello machines virtuelles Azure après le basculement. Choisissez le déploiement hello modèle que vous souhaitez toouse dans Azure (classique ou une ressource de gestion) pour les machines virtuelles de hello.

3. Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.

    - Si vous n’avez pas un compte de stockage, cliquez sur **+ stockage** toocreate un inline compte basé sur le Gestionnaire de ressources. 
    - Si vous n’avez pas un réseau Azure, cliquez sur **+ réseau** toocreate un inline réseau basé sur le Gestionnaire de ressources.






## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 9 : configurer une stratégie de réplication](hyper-v-site-walkthrough-replication.md)
