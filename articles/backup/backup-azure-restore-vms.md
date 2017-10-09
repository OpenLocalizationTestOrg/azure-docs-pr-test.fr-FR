---
title: "aaaRestore un ordinateurs virtuels à partir de la sauvegarde | Documents Microsoft"
description: "Découvrez comment toorestore une machine virtuelle Azure à partir de la récupération d’un point"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "Restaurez la sauvegarde ; Comment toorestore ; point de récupération ;"
ms.assetid: fed877b3-b496-49fb-99e4-653be7c23e3a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: trinadhk; jimpark;
ms.openlocfilehash: 44c25f3248784accd1c2beaabb2c9a4dca3232d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-virtual-machines-in-azure"></a>Restauration de machines virtuelles dans Azure
> [!div class="op_single_selector"]
> * [Restaurer des machines virtuelles dans le portail Azure](backup-azure-arm-restore-vms.md)
> * [Restaurer des machines virtuelles dans le portail classique](backup-azure-restore-vms.md)
>
>

Restaurer un tooa de machine virtuelle nouvelle machine virtuelle à partir de sauvegardes hello stockées dans un coffre Azure Backup avec hello suivant les étapes.

> [!IMPORTANT]
> Vous pouvez maintenant mettre à niveau vos archivages de sauvegarde coffres tooRecovery Services. Pour plus d’informations, voir l’article hello [mise à niveau d’un tooa de coffre de sauvegarde de coffre Recovery Services](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft vous encourage tooupgrade coffres des Services tooRecovery les coffres de votre sauvegarde.<br/> **Le 15 octobre 2017**, vous ne pourra plus être coffres de sauvegarde toocreate toouse en mesure de PowerShell. <br/> **À compter du 1er novembre 2017** :
>- Les coffres de sauvegarde restants seront les coffres des Services de tooRecovery automatiquement mis à niveau.
>- Vous ne pourra plus être en mesure de tooaccess vos données de sauvegarde dans le portail classique de hello. Au lieu de cela, utilisez hello tooaccess portail Azure vos données de sauvegarde dans les coffres des Services de récupération.
>

## <a name="restore-workflow"></a>Flux de travail de restauration
### <a name="step-1-choose-an-item-toorestore"></a>Étape 1 : Choisissez un élément de toorestore
1. Accédez toohello **éléments protégés** onglet et sélectionnez hello machine virtuelle toorestore tooa nouvelle machine virtuelle.

    ![Éléments protégés](./media/backup-azure-restore-vms/protected-items.png)

    Hello **Point de récupération** colonne Bonjour **éléments protégés** page indiquera hello de nombre de points de récupération pour un ordinateur virtuel. Hello **Point de récupération plus récent** colonne indique hello de temps de sauvegarde la plus récente hello à partir de laquelle un ordinateur virtuel peut être restauré.
2. Cliquez sur **restaurer** tooopen hello **restaurer un élément** Assistant.

    ![Restaurer un élément](./media/backup-azure-restore-vms/restore-item.png)

### <a name="step-2-pick-a-recovery-point"></a>Étape 2 : Choix d’un point de récupération
1. Bonjour **sélectionner un point de récupération** écran, vous pouvez restaurer à partir du point de récupération les plus récents hello, ou à partir d’un point antérieur dans le temps. Bonjour option sélectionnée lors de l’Assistant s’ouvre par défaut est *Point de récupération plus récent*.

    ![Sélectionner un point de récupération](./media/backup-azure-restore-vms/select-recovery-point.png)
2. toopick un point antérieur dans le temps, choisissez hello **sélectionner une Date de** option dans la liste déroulante de hello et sélectionnez une date dans le contrôle de calendrier hello en cliquant sur hello **icône de calendrier**. Dans le contrôle hello, toutes les dates qui ont des points de récupération sont remplis avec un niveau de gris clair et peuvent être sélectionnés par l’utilisateur de hello.

    ![Sélectionner une date](./media/backup-azure-restore-vms/select-date.png)

    Une fois que vous cliquez sur une date dans le contrôle de calendrier hello, les points de récupération de hello disponibles sur la date apparaît dans le tableau de points de récupération ci-dessous. Hello **temps** colonne indique le temps hello à quels hello instantané a été pris. Hello **Type** colonne affiche hello [cohérence](https://azure.microsoft.com/documentation/articles/backup-azure-vms/#consistency-of-recovery-points) hello point de récupération. en-tête de table Hello montre le nombre hello de points de récupération disponibles ce jour-là entre parenthèses.

    ![Points de récupération](./media/backup-azure-restore-vms/recovery-points.png)
3. Sélectionnez le point de récupération hello de hello **Points de récupération** de table et cliquez sur hello écran suivant de flèche toogo toohello suivant.

### <a name="step-3-specify-a-destination-location"></a>Étape 3 : Spécification d’un emplacement de destination
1. Bonjour **sélectionner Restaurer instance** écran de spécifier les détails d’où toorestore hello machine virtuelle.

   * Spécifiez le nom d’ordinateur virtuel hello : dans un service cloud donné, le nom d’ordinateur virtuel hello doit être unique. Nous ne prenons pas en charge l’écrasement d’une machine virtuelle existante.
   * Sélectionnez un service cloud pour hello machine virtuelle : ce champ est obligatoire pour la création d’une machine virtuelle. Vous pouvez choisir tooeither utilisez un service cloud existant ou créer un nouveau service cloud.

        Quel que soit le nom du service cloud choisi, il doit être globalement unique. En général, nom du service cloud hello est associée à une URL publique sous forme hello [cloudservice]. cloudapp.net. Azure vous autorisera pas toocreate un nouveau service cloud si hello nom a déjà été utilisé. Si vous choisissez toocreate un nouveau service cloud, il sera indiqué hello même nom en tant que machine virtuelle de hello : dans quels cas hello VM nom choisi doit être assez uniques toobe appliqué toohello associé cloud service.

        Nous afficher uniquement les services de cloud computing et des réseaux virtuels qui ne sont pas associés à tous les groupes d’affinités Bonjour restaurer les détails de l’instance. [En savoir plus](../virtual-network/virtual-networks-migrate-to-regional-vnet.md)
2. Sélectionnez un compte de stockage pour hello machine virtuelle : ce champ est obligatoire pour la création de hello machine virtuelle. Vous pouvez sélectionner à partir des comptes de stockage existants Bonjour même région que le coffre de sauvegarde Azure hello. Nous ne prenons pas en charge les comptes de stockage redondants dans une zone ou de type Premium.

    S’il n’y a aucun compte de stockage avec une configuration prise en charge, créez un compte de stockage configuration prise en charge toostarting préalable d’opération de restauration.

    ![Sélectionner un réseau virtuel](./media/backup-azure-restore-vms/restore-sa.png)
3. Sélectionnez un réseau virtuel : hello réseau () pour la machine virtuelle de hello doit être sélectionné au moment de la création de hello hello machine virtuelle. Hello restaurer l’interface utilisateur affiche tous les réseaux virtuels de hello dans cet abonnement qui peut être utilisé. Il n’est pas obligatoire tooselect un réseau virtuel pour hello restauré l’ordinateur virtuel, vous serez en mesure de tooconnect toohello restauré virtuels sur hello internet même si hello réseau virtuel n’est pas appliqué.

    Si hello cloud service sélectionné est associé à un réseau virtuel, vous ne pouvez pas modifier le réseau virtuel de hello.

    ![Sélectionner un réseau virtuel](./media/backup-azure-restore-vms/restore-cs-vnet.png)
4. Sélectionnez un sous-réseau : au cas où hello réseau virtuel a des sous-réseaux, premier sous-réseau de hello sera sélectionné par défaut. Choisissez le sous-réseau hello de votre choix à partir des options de liste déroulante hello. Pour plus d’informations de sous-réseau, accédez à extension tooNetworks Bonjour [page d’accueil du portail](https://manage.windowsazure.com/), accédez trop**réseaux virtuels** et réseau virtuel de select hello et vers le bas dans les détails du sous-réseau toosee configurer.

    ![Sélectionner un sous-réseau](./media/backup-azure-restore-vms/select-subnet.png)
5. Cliquez sur hello **Submit** icône hello Assistant toosubmit hello détails et créer un travail de restauration.

## <a name="track-hello-restore-operation"></a>Suivre l’opération de restauration hello
Une fois que vous avez entrée toutes les informations de hello dans l’Assistant de restauration hello et soumis toocreate une opération de restauration de travail tootrack hello va essayer de sauvegarde Azure.

![Création d’un travail de restauration](./media/backup-azure-restore-vms/create-restore-job.png)

Si la création du travail hello est réussie, vous verrez une notification toast indiquant que le travail hello est créé. Vous pouvez obtenir plus de détails en cliquant sur hello **afficher le travail** bouton qui vous conduira trop**travaux** onglet.

![Travail de restauration créé](./media/backup-azure-restore-vms/restore-job-created.png)

Une fois l’opération de restauration hello est terminée, elle sera marquée comme étant terminée en **travaux** onglet.

![Travail de restauration terminé](./media/backup-azure-restore-vms/restore-job-complete.png)

Une fois la restauration hello machine virtuelle, vous devrez peut-être installer toore extensions de hello existants sur hello machine virtuelle d’origine et [modifier les points de terminaison hello](../virtual-machines/windows/classic/setup-endpoints.md) pour l’ordinateur virtuel de hello Bonjour portail Azure.

## <a name="post-restore-steps"></a>Étapes post-restauration
Si vous utilisez une distribution Linux basée sur cloud-init telle qu’Ubuntu, le mot de passe sera bloqué après la restauration pour des raisons de sécurité. Veuillez utiliser l’extension VMAccess sur hello restauré VM trop[le mot de passe réinitialisé hello](../virtual-machines/linux/classic/reset-access.md). Nous vous recommandons d’utiliser des clés SSH sur ces tooavoid distributions la réinitialisation de mot de passe après restauration.

## <a name="backup-for-restored-vms"></a>Sauvegarde de machines virtuelles restaurées
Si vous avez restauré le service de cloud toosame machine virtuelle avec le même nom sauvegardé à l’origine de machine virtuelle de hello, sauvegarde va se poursuivre sur hello restauration post de machine virtuelle. Si vous avez restauré la machine virtuelle tooa autre service cloud ou spécifiez un autre nom pour la machine virtuelle restaurée, il sera traité comme un nouvel ordinateur virtuel, et vous devez toosetup sauvegarde pour la machine virtuelle restaurée.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Restauration d’une machine virtuelle en cas de défaillance du centre de données Azure
Azure Backup permet la restauration sauvegardés de centre de données associés de machines virtuelles toohello en cas de machines virtuelles s’exécutent après sinistre des expériences alors que vous avez configuré toobe de coffre de sauvegarde géo-redondant du centre de données principal de hello. Au cours de ces scénarios, vous devez tooselect un compte de stockage qui n’est présent dans le centre de données associés, et le reste du processus de restauration hello reste la même. Azure Backup utilise le service de calcul de la machine virtuelle de géo-réplication appariés toocreate hello restaurée. En savoir plus sur la [résilience des centres de données Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Restauration de machines virtuelles d’un contrôleur de domaine
Azure Backup prend en charge la sauvegarde de machines virtuelles d’un contrôleur de domaine. Toutefois, être vigilant lors des processus de restauration hello. processus de restauration correcte Hello dépend de la structure de hello du domaine de hello. Dans le cas le plus simple hello, vous avez un seul contrôleur de domaine dans un domaine unique. Plus communément pour les charges de production, vous disposez d’un domaine unique avec plusieurs contrôleurs de domaine, dont certains sont peut-être locaux. Enfin, vous disposez peut-être d’une forêt avec plusieurs domaines.

À partir d’une salutation de perspective Active Directory Azure VM revient à n’importe quel autre ordinateur virtuel sur un hyperviseur pris en charge modern. Hello principale différence avec les hyperviseurs local est qu’aucune console des ordinateurs virtuels n’est disponible dans Azure. Une console est nécessaire pour certains scénarios tels que la récupération à l’aide d’une sauvegarde de type Récupération complète (BMR, Bare Metal Recovery). Toutefois, la restauration VM hello coffre de sauvegarde est un remplacement complet pour la récupération complète. Le mode DSRM (Active Directory Restore Mode) étant également disponible, tous les scénarios de récupération Active Directory sont viables. Pour plus d’informations, voir les [considérations en matière de sauvegarde et de restauration pour les contrôleurs de domaine virtualisés](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) et la [planification de la récupération de forêt Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Contrôleur de domaine unique dans un seul domaine
Hello machine virtuelle peut être restaurée (comme tout autre ordinateur virtuel) à partir de hello Azure portal ou à l’aide de PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Contrôleurs de domaine multiples dans un seul domaine
Lorsque d’autres contrôleurs de domaine de hello même domaine peut être atteint via hello réseau, hello contrôleur de domaine peut être restauré à n’importe quel ordinateur virtuel. Si elle est hello du dernier contrôleur de domaine restant dans le domaine de hello, ou une récupération dans un réseau isolé est effectuée, une procédure de récupération de forêt doit être suivie.

### <a name="multiple-domains-in-one-forest"></a>Domaines multiples dans une seule forêt
Lorsque d’autres contrôleurs de domaine de hello même domaine peut être atteint via hello réseau, hello contrôleur de domaine peut être restauré à n’importe quel ordinateur virtuel. Toutefois, dans tous les autres cas, une récupération de forêt est recommandée.

<!--- WK: this following original supportability statement is incorrect, taking it out.
hello challenge arises because DSRM mode is not present in Azure. So toorestore such a VM, you cannot use hello Azure portal. hello only supported restore mechanism is disk-based restore using PowerShell.

> [!WARNING]
> For Domain Controller VMs in a multi-DC environment, do not use hello Azure portal for restore! Only PowerShell based restore is supported
>
>

Read more about hello [USN rollback problem](https://technet.microsoft.com/library/dd363553) and hello strategies suggested toofix it.
--->

## <a name="restoring-vms-with-special-network-configurations"></a>Restauration de machines virtuelles avec des configurations de réseau spéciales
Azure Backup prend en charge la sauvegarde pour les configurations de réseau spéciales de machines virtuelles.

* Machines virtuelles sous un équilibreur de charge (interne et externe)
* Machines virtuelles avec plusieurs adresses IP réservées
* Machines virtuelles avec plusieurs cartes d'interface réseau

Les considérations suivantes doivent être prises en compte lors de la restauration de ces configurations.

> [!TIP]
> Utilisez basé sur PowerShell restauration flux toorecreate hello spéciaux configuration du réseau de machines virtuelles après restauration.
>
>

### <a name="restoring-from-hello-ui"></a>La restauration à partir de l’interface utilisateur de hello :
Lors de la restauration à partir de l'interface utilisateur, **choisissez toujours un service cloud**. Notez qu’étant donné que le portail n’accepte qu’obligatoire paramètres pendant le flux de restauration, de machines virtuelles restaurées à l’aide de l’interface utilisateur perdrez dont ils disposent de la configuration du réseau spéciales hello. En d'autres termes, les machines virtuelles restaurées seront normales sans configuration d'un équilibreur de charge ou de plusieurs cartes réseau ou plusieurs adresses IP réservées.

### <a name="restoring-from-powershell"></a>Restauration de PowerShell :
PowerShell a hello capacité toojust restaurer des disques de machine virtuelle hello à partir de la sauvegarde et de créer un ordinateur virtuel hello. Cela est utile lors de la restauration de machines virtuelles qui nécessitent les configurations de réseau spéciales mentionnées ci-dessus.

Dans l’ordre toofully recréer post de machine virtuelle hello restauration des disques, procédez comme suit :

1. Restaurer des disques hello de coffre de sauvegarde à l’aide [PowerShell de sauvegarde Azure](backup-azure-vms-classic-automation.md#restore-an-azure-vm)
2. Création de la configuration de machine virtuelle hello requise pour l’équilibrage de charge / plusieurs cartes réseau/plusieurs réservée IP à l’aide de hello applets de commande PowerShell et l’utiliser toocreate hello machine virtuelle de la configuration souhaitée.

   * Créer une machine virtuelle dans le service cloud avec un [équilibreur de charge interne ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Créer des ordinateurs virtuels tooconnect trop[Internet exposés à équilibrage de charge](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Créer une machine virtuelle avec [plusieurs cartes d’interface réseau](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Créer des machines virtuelles avec [plusieurs adresses IP réservées](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Étapes suivantes
* [Résolution des erreurs](backup-azure-vms-troubleshoot.md#restore)
* [Gestion des machines virtuelles](backup-azure-manage-vms.md)
