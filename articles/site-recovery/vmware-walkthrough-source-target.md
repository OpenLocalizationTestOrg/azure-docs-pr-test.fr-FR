---
title: "aaaSet hello source et un cible pour tooAzure de réplication VMware avec Azure Site Recovery | Documents Microsoft"
description: "Résume les tooset d’étapes hello les paramètres source et cible pour la réplication de stockage de tooAzure les ordinateurs virtuels VMware avec Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>Étape 8 : Configurer la source de hello et cible pour VMware réplication tooAzure

Cet article décrit comment tooconfigure les paramètres de source et cible lors de la réplication locale tooAzure d’ordinateurs virtuels VMware, à l’aide de hello [Azure Site Recovery](site-recovery-overview.md) service Bonjour portail Azure.

Ajouter des commentaires et questions bas hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurer l’environnement source hello

Configurer le serveur de configuration hello, enregistrez-le dans le coffre hello et découvrir des ordinateurs virtuels.

1. Cliquez sur **Site Recovery** > **Étape 1 : Préparer l’infrastructure** > **Source**.
2. Si vous n’avez pas de serveur de configuration, cliquez sur **+Serveur de configuration**.
3. Dans **Ajouter un serveur**, vérifiez que **Serveur de configuration** s’affiche dans **Type de serveur**.
4. Télécharger le fichier d’installation le programme d’installation de Site Recovery unifiée hello.
5. Télécharger la clé d’inscription du coffre hello. Vous en aurez besoin lors de l’exécution du programme d’installation unifiée. clé de Hello est valide pendant cinq jours après que l’avoir généré.

   ![Configurer la source](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Inscrire le serveur de configuration hello dans le coffre de hello

Suit hello avant de démarrer, puis exécuter le programme d’installation unifiée serveur de configuration tooinstall hello, serveur de processus hello et serveur cible maître de hello.
    - Visionnez une courte vidéo de présentation :

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - Sur le serveur de configuration hello machine virtuelle, assurez-vous que l’horloge système hello est synchronisée avec un [serveur de temps](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Elles doivent correspondre. S’il y a 15 minutes d’avance ou de retard, le programme d’installation peut échouer.
    - Exécutez le programme d’installation en tant qu’administrateur Local sur le serveur de configuration hello machine virtuelle.
    - Vérifiez que TLS 1.0 est activé sur la machine virtuelle de hello.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> serveur de configuration Hello peut également être installé [à partir de la ligne de commande hello](http://aka.ms/installconfigsrv).



## <a name="connect-toovmware-servers"></a>Connecter les serveurs tooVMware

tooallow Azure Site Recovery toodiscover machines virtuelles en cours d’exécution dans votre environnement local, vous devez tooconnect votre serveur VMware vCenter ou les ordinateurs hôtes ESXi vSphere avec Site Recovery. Notez les points suivants de hello avant de commencer :

- Si vous ajoutez le serveur vCenter hello ou vSphere hôtes tooSite récupération avec un compte sans privilèges d’administrateur sur le serveur de hello, compte de hello a besoin de ces privilèges activés :
    - Centre de données, magasin de données, dossier, hôte, réseau, ressource, machine virtuelle, vSphere Distributed Switch.
    - le serveur vCenter Hello a besoin d’autorisations de vues de stockage.
- Lorsque vous ajoutez des serveurs de VMware tooSite récupération, il peut prendre 15 minutes ou plus pour les tooappear dans le portail de hello.

### <a name="add-hello-account-for-automatic-discovery"></a>Ajoutez le compte hello pour la découverte automatique

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>Configurer une connexion

Se connecter tooservers comme suit :

1. Sélectionnez **+ vCenter** toostart connecter un serveur VMware vCenter ou un hôte VMware vSphere ESXi.
2. Dans **ajouter vCenter**, spécifiez un nom convivial pour le serveur hôte ou vCenter du vSphere hello, puis spécifiez l’adresse IP de hello ou nom de domaine complet du serveur de hello.
3. Conservez les port hello 443, sauf si vos serveurs VMware sont toolisten configurée pour les demandes sur un port différent. Sélectionnez compte hello tooconnect toohello VMware vCenter ou vSphere ESXi Server. Cliquez sur **OK**.
4. Récupération de site connecte tooVMware serveurs à l’aide de hello spécifié de paramètres et détecte les machines virtuelles.

> [!NOTE]
> Si vous ajoutez un serveur ou un ordinateur hôte avec un compte qui ne dispose pas des privilèges d’administrateur sur le serveur vCenter ou un hôte de hello, assurez-vous que le compte de hello a ces privilèges activés : centre de données, magasin de données, dossier, hôte, réseau, ressources, l’ordinateur virtuel, et vSphere Distributed Switch. En outre, hello VMware vCenter server a besoin d’affichages de stockage hello privilège activé.


## <a name="set-up-hello-target-environment"></a>Configuration d’environnement cible de hello

Avant de configurer l’environnement cible de hello, assurez-vous que vous avez un compte de stockage Azure et le réseau virtuel configuré.

1. Cliquez sur **Prepare infrastructure** > **cible**, et sélectionnez hello abonnement Azure que vous souhaitez toouse.
2. Spécifiez si votre modèle de déploiement cible est basé sur Resource Manager ou est de type classique.
3. Site Recovery vérifie que vous disposez d’un ou de plusieurs réseaux et comptes Azure Storage compatibles.

   ![Cible](./media/vmware-walkthrough-source-target/gs-target.png)
4. Si vous n’avez pas créé un compte de stockage ou un réseau, cliquez sur **+ compte de stockage** ou **+ réseau**, toocreate un gestionnaire de ressources du réseau ou le compte en ligne.

## <a name="next-steps"></a>Étapes suivantes

Accédez trop[étape 9 : configurer une stratégie de réplication](vmware-walkthrough-replication.md)
