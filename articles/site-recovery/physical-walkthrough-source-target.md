---
title: "aaaSet hello source et un cible pour tooAzure de réplication de serveur physique avec Azure Site Recovery | Documents Microsoft"
description: "Résume les tooset d’étapes hello les paramètres source et cible pour la réplication de stockage tooAzure de serveurs physiques avec hello service Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>Étape 7 : Configurer la source de hello et cible pour tooAzure de réplication de serveur physique

Cet article décrit comment tooconfigure les paramètres de source et cible lors de la réplication locale tooAzure des serveurs physiques, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Configurer le serveur de configuration hello, enregistrez-le dans le coffre hello et découvrir les ordinateurs.

1. Cliquez sur **Site Recovery** > **Étape 1 : Préparer l’infrastructure** > **Source**.
2. Si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration**.
3. Dans **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.
4. Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.
5. Télécharger la clé d’inscription du coffre hello. Vous en aurez besoin lors de l’exécution du programme d’installation unifiée. clé de Hello est valide pendant cinq jours après que l’avoir généré.

   ![Configurer la source](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Inscrire le serveur de configuration hello dans le coffre de hello

Suit hello avant de démarrer, puis exécuter le programme d’installation unifiée serveur de configuration tooinstall hello, serveur de processus hello et serveur cible maître de hello. Hello vidéo décrit comment configurer des composants hello pour la réplication tooAzure VMware VM. Toutefois, hello même processus n’est valide pour la réplication tooAzure serveur physique.

- Sur le serveur de configuration hello machine virtuelle, assurez-vous que l’horloge système hello est synchronisée avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Elles doivent correspondre. S’il y a 15 minutes d’avance ou de retard, le programme d’installation peut échouer.
- Exécutez le programme d’installation en tant qu’administrateur Local sur l’ordinateur de serveur de configuration hello.
- Vérifiez que TLS 1.0 est activé sur la machine virtuelle de hello.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> serveur de configuration Hello peut également être installé [à partir de la ligne de commande hello](http://aka.ms/installconfigsrv).




## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello

Avant de configurer l’environnement cible de hello, assurez-vous que vous avez un compte de stockage Azure et le réseau virtuel configuré.

1. Cliquez sur **Prepare infrastructure** > **cible**, et sélectionnez hello abonnement Azure que vous souhaitez toouse.
2. Spécifiez si votre modèle de déploiement cible est basé sur Resource Manager ou est de type classique.
3. Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.

   ![Cible](./media/physical-walkthrough-source-target/gs-target.png)

4. Si vous n’avez pas créé un compte de stockage ou un réseau, cliquez sur **+ compte de stockage** ou **+ réseau**, toocreate un gestionnaire de ressources du réseau ou le compte en ligne.

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 8 : définir une stratégie de réplication](physical-walkthrough-replication.md)
