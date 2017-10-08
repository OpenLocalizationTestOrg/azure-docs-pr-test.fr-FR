---
title: "Sauvegarde Azure : Restaurer des machines virtuelles à l’aide de hello portail Azure | Documents Microsoft"
description: "Restaurer une machine virtuelle Azure à partir d’un point de récupération à l’aide du portail Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "Restaurez la sauvegarde ; Comment toorestore ; point de récupération ;"
ms.assetid: 372b87c6-3544-4dc5-bbc9-c742ca502159
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: f4f75d1da73c7760d2952afe80ff94918a08351c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-toorestore-virtual-machines"></a>Utilisez des ordinateurs virtuels de toorestore portail Azure
> [!div class="op_single_selector"]
> * [Restaurer des machines virtuelles dans le portail classique](backup-azure-restore-vms.md)
> * [Restaurer des machines virtuelles dans le portail Azure](backup-azure-arm-restore-vms.md)
>
>

Protégez vos données en prenant des instantanés de vos données à des intervalles définis. Ces instantanés sont considérés comme des points de récupération stockés dans des coffres Recovery Services. Si, ou lorsqu’il est nécessaire toorepair ou reconstruction d’un ordinateur virtuel, vous pouvez restaurer hello machine virtuelle à partir des hello enregistré des points de récupération. Lorsque vous restaurez un point de récupération, vous pouvez créer une machine virtuelle qui est une représentation sous forme de point-à-temps de votre machine virtuelle sauvegardée, ou restaurer des disques et utiliser le modèle hello fourni en même temps toocustomize hello restauré l’ordinateur virtuel ou effectuer une récupération de fichiers individuels. Cet article explique comment toorestore un tooa VM nouvelle machine virtuelle ou les disques de restaurer toutes les sauvegardé. Pour la récupération de fichiers individuels, consultez trop[récupérer des fichiers de sauvegarde de la machine virtuelle Azure](backup-azure-restore-files-from-vm.md)

![3-ways-restore-from-vm-backup](./media/backup-azure-arm-restore-vms/azure-vm-backup-restore.png)

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Cet article fournit des informations de hello et des procédures pour la restauration d’ordinateurs virtuels déployés à l’aide du modèle de gestionnaire de ressources hello.
>
>

La restauration d’une machine virtuelle ou de tous les disques à partir de la sauvegarde de machine virtuelle implique deux étapes :

1. Sélectionner un point pour la restauration
2. En sélectionnant hello restaurer type - créer une machine virtuelle ou restaurer des disques et spécifiez les paramètres requis. 

## <a name="select-restore-point-for-restore"></a>Sélectionner un point pour la restauration
1. Connectez-vous à toohello [portail Azure](http://portal.azure.com/)
2. Dans hello menu Azure, cliquez sur **Parcourir** et, dans la liste de hello des services, tapez **Recovery Services**. liste Hello des services ajuste toowhat que vous tapez. Lorsque vous voyez **Coffres Recovery Services**, cliquez dessus.

    ![Ouvrir le coffre Recovery Services](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    liste Hello de coffres dans l’abonnement de hello s’affiche.

    ![Liste des coffres Recovery Services](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
3. À partir de la liste de hello, le coffre hello sélectionnez associé hello machine virtuelle que vous souhaitez toorestore. Lorsque vous cliquez sur le coffre de hello, son tableau de bord s’ouvre.

    ![Liste des coffres Recovery Services](./media/backup-azure-arm-restore-vms/select-vault-open-vault-blade.png)
4. Maintenant que vous êtes dans le tableau de bord coffre hello. Sur hello **des éléments de sauvegarde** vignette, cliquez sur **des Machines virtuelles Azure** toodisplay hello machines virtuelles associées avec le coffre de hello.

    ![tableau de bord du coffre](./media/backup-azure-arm-restore-vms/vault-dashboard.png)

    Hello **des éléments de sauvegarde** panneau s’ouvre et affiche la liste de hello des machines virtuelles.

    ![liste des machines virtuelles du coffre](./media/backup-azure-arm-restore-vms/list-of-vms-in-vault.png)
5. Dans la liste hello, sélectionnez un tableau de bord de machine virtuelle tooopen hello. le tableau de bord Hello VM ouvre toohello zone d’analyse, qui contient la vignette de points de restauration hello.

    ![liste des machines virtuelles du coffre](./media/backup-azure-arm-restore-vms/vm-blade.png)
6. Menu de tableau de bord de machine virtuelle hello, cliquez sur **restaurer**

    ![liste des machines virtuelles du coffre](./media/backup-azure-arm-restore-vms/vm-blade-menu-restore.png)

    Panneau de restauration Hello s’ouvre.

    ![panneau de restauration](./media/backup-azure-arm-restore-vms/restore-blade.png)
7. Sur hello **restaurer** panneau, cliquez sur **point de restauration** tooopen hello **sélectionner restaurer le point** panneau.

    ![panneau de restauration](./media/backup-azure-arm-restore-vms/recovery-point-selector.png)

    Par défaut, boîte de dialogue hello affiche tous les points de restauration à partir de hello 30 derniers jours. Hello d’utilisation **filtre** affiche des points de restauration de plage de temps tooalter hello Hello. Par défaut, les points de restauration de toute cohérence sont affichés. Modifier **restaurer tous les points** filtrer tooselect une cohérence spécifique de points de restauration. Pour plus d’informations sur chaque type de point de restauration, consultez explication hello de [la cohérence des données](backup-azure-vms-introduction.md#data-consistency).  

   * **Cohérence du point de restauration** : dans cette liste, choisissez :
     * points de restauration cohérents d’incident ;
     * points de restauration cohérents d’application ;
     * points de restauration cohérents de système de fichiers ;
     * tous les points de restauration.  
8. Choisissez un point de restauration et cliquez sur **OK**.

    ![sélectionner un point de restauration](./media/backup-azure-arm-restore-vms/select-recovery-point.png)

    Hello **restaurer** panneau montre hello point de restauration est définie.

    ![le point de restauration est défini](./media/backup-azure-arm-restore-vms/recovery-point-set.png)
9. Sur hello **restaurer** panneau, **restaurer la configuration** s’ouvre automatiquement une fois le point de restauration est défini.

## <a name="choosing-a-vm-restore-configuration"></a>Choisir une configuration de restauration de machine virtuelle
Maintenant que vous avez sélectionné le point de restauration hello, choisissez une configuration pour votre machine virtuelle de la restauration. Vos choix de configuration hello restaurer la machine virtuelle sont toouse : portail Azure ou PowerShell.

1. Si vous n’êtes pas déjà, accédez à toohello **restaurer** panneau. Garantir une [point de restauration a été sélectionné](#select-restore-point-for-restore), puis cliquez sur **restaurer la configuration** tooopen hello **configuration de la récupération** panneau.

    ![l’assistant de configuration de récupération est défini](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard-recovery-type.png)
2. Sur hello **restaurer la configuration** panneau, vous avez deux possibilités :
   * Restaurer la totalité de la machine virtuelle
   * Restaurer des disques sauvegardés

Le Portail fournit une option Création rapide pour la machine virtuelle restaurée. Si vous voulez que la configuration de machine virtuelle de hello toocustomize ou noms de ressources hello créés dans le cadre de créer un nouveau choix de la machine virtuelle, utilisez PowerShell ou portail toorestore sauvegardé disques et l’utilisation de PowerShell commandes tooattach les toochoice de modèle de configuration ou l’utilisation d’ordinateur virtuel qui est fourni avec la restauration hello toocustomize de disques restaurés machine virtuelle. Consultez [restauration d’une machine virtuelle avec les configurations réseau spéciales](#restoring-vms-with-special-network-configurations) pour plus d’informations sur la façon de toorestore machine virtuelle qui possède plusieurs cartes réseau ou sous l’équilibrage de charge. Si votre machine virtuelle Windows utilise [HUB licences](../virtual-machines/windows/hybrid-use-benefit-licensing.md), vous devez toorestore disques et utiliser PowerShell/modèle comme indiqué ci-dessous toocreate hello VM et assurez-vous que vous spécifiez LicenseType en tant que « Windows_Server » lors de la création de machine virtuelle tooavail HUB avantages de la machine virtuelle restaurée. 
 
## <a name="create-a-new-vm-from-restore-point"></a>Créer une machine virtuelle à partir du point de restauration
Si vous n’avez pas encore fait, [sélectionner un point de restauration](#restoring-vms-with-special-network-configurations) avant de continuer toocreating une nouvelle machine virtuelle à partir de la restauration de point. Une fois que le point de restauration est sélectionné, sur hello **restaurer la configuration** panneau, entrez ou sélectionnez des valeurs pour chacun des hello champs qui suivent :

* **Type de restauration** : créer une machine virtuelle.
* **Nom de machine virtuelle** -fournissez un nom pour hello machine virtuelle. nom de Hello doit être le groupe de ressources unique toohello (pour un ordinateur virtuel déployé de gestionnaire de ressources) ou un service cloud (pour une machine virtuelle classique). Vous ne pouvez pas remplacer hello virtual machine s’il existe déjà dans l’abonnement de hello.
* **Groupe de ressources** : sélectionnez un groupe de ressources existant ou créez-en un. Si vous restaurez un ordinateur virtuel classique, utilisez ce nom de hello toospecify champ d’un nouveau service cloud. Si vous créez un nouvelle ressource groupe/service cloud, nom de hello doit être globalement unique. En général, nom du service cloud hello est associé à une URL publique - par exemple : [cloudservice]. cloudapp.net. Si vous essayez de toouse un nom pour le service/cloud du groupe de ressources de cloud de hello a déjà été utilisé, Azure affecte hello ressource groupe/service cloud hello même nom comme hello de machine virtuelle. Azure affiche les groupes de ressources/services cloud et les machines virtuelles qui ne sont associées à aucun groupe d’affinités. Pour plus d’informations, consultez [comment toomigrate à partir de groupes d’affinités tooa réseau virtuel régional (VNet)](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).
* **Réseau virtuel** : sélectionnez hello réseau () lors de la création hello machine virtuelle. champ de Hello fournit tous les réseaux virtuels associés à hello abonnement. Groupe de ressources de hello machine virtuelle s’affiche entre parenthèses.
* **Sous-réseau** -si hello réseau virtuel a des sous-réseaux, le premier sous-réseau de hello est sélectionnée par défaut. S’il existe des sous-réseaux supplémentaires, sélectionnez hello sous-réseau souhaité.
* **Compte de stockage** -ce menu répertorie les comptes de stockage hello Bonjour même emplacement que hello de coffre Recovery Services. Les comptes de stockage redondant dans une zone ne sont pas pris en charge. Si aucun compte de stockage avec les Services de récupération hello même emplacement que hello coffre, vous devez en créer un avant de commencer l’opération de restauration hello. type de réplication du compte de stockage Hello est indiqué entre parenthèses.

![l’assistant de configuration de restauration est défini](./media/backup-azure-arm-restore-vms/recovery-configuration-wizard.png)

> [!NOTE]
> 1. Si vous restaurez une machine virtuelle déployée à l'aide de Resource Manager, vous devez identifier un réseau virtuel (VNET). Un réseau virtuel (VNET) est facultatif pour une machine virtuelle classique.
> 2. Si vous restaurez des machines virtuelles avec des disques gérés, vérifiez que le chiffrement du service de stockage (SSE) n’est pas activé sur le compte de stockage sélectionné au cours de la durée de vie de celui-ci.
> 3. Selon le type de stockage de hello du compte de stockage sélectionné (premium ou standard), tous les disques restaurés sera disques standards ou premium. Actuellement, le mode mixte de disques n’est pas pris en charge lors de la restauration.  
>
>

Sur hello **restaurer la configuration** panneau, cliquez sur **OK** toofinalize hello restauration de la configuration. Sur hello **restaurer** panneau, cliquez sur **restaurer** opération de restauration tootrigger hello.

## <a name="restore-backed-up-disks"></a>Restaurer des disques sauvegardés
Si vous souhaitez que la machine virtuelle de hello toocustomize vous souhaitez toocreate de sauvegardés que celles présentes dans le panneau de configuration de restauration, sélectionnez les disques **restaurer des disques** valeur **restaurer le Type**. Ce choix exige un compte de stockage sur lequel copier les disques à partir des sauvegardes. Lorsque vous choisissez un compte de stockage, sélectionnez un compte que les partages hello même emplacement que le coffre de Services de récupération hello. Les comptes de stockage redondant dans une zone ne sont pas pris en charge. Si aucun compte de stockage avec les Services de récupération hello même emplacement que hello coffre, vous devez en créer un avant de commencer l’opération de restauration hello. type de réplication du compte de stockage Hello est indiqué entre parenthèses.

Une fois l’opération de restauration terminée, vous pouvez :
* [Hello de toocustomize modèle utilisez restauré la machine virtuelle](#use-templates-to-customize-restore-vm)
* [Hello d’utilisation restauré l’ordinateur virtuel existant de disques tooattach tooan](../virtual-machines/windows/attach-managed-disk-portal.md)
* [Créer une machine virtuelle à l’aide de PowerShell à partir de disques restaurés](./backup-azure-vms-automation.md#restore-an-azure-vm)

Sur hello **restaurer la configuration** panneau, cliquez sur **OK** toofinalize hello restauration de la configuration. Sur hello **restaurer** panneau, cliquez sur **restaurer** opération de restauration tootrigger hello.

![Configuration de la récupération terminée](./media/backup-azure-arm-restore-vms/trigger-restore-operation.png)

## <a name="track-hello-restore-operation"></a>Suivre l’opération de restauration hello
Une fois que vous déclenchez l’opération de restauration hello, hello service de sauvegarde crée une tâche pour suivre l’opération de restauration hello. Hello service de sauvegarde crée également et affiche temporairement la notification de hello dans la zone de notification du portail. Si vous ne voyez pas de notification de hello, vous pouvez toujours cliquer sur hello Notifications icône tooview vos notifications.

![Restauration déclenchée](./media/backup-azure-arm-restore-vms/restore-notification.png)

tooview hello opération pendant son traitement ou tooview lorsqu’elle est terminée, ouvrez la liste des tâches de sauvegarde hello.

1. Dans hello menu Azure, cliquez sur **Parcourir** et, dans la liste de hello des services, tapez **Recovery Services**. liste Hello des services ajuste toowhat que vous tapez. Lorsque vous voyez **Coffres Recovery Services**, cliquez dessus.

    ![Ouvrir le coffre Recovery Services](./media/backup-azure-arm-restore-vms/open-recovery-services-vault.png)

    liste Hello de coffres dans l’abonnement de hello s’affiche.

    ![Liste des coffres Recovery Services](./media/backup-azure-arm-restore-vms/list-of-rs-vaults.png)
2. À partir de la liste de hello, le coffre hello sélectionnez associé hello machine virtuelle que vous avez restauré. Lorsque vous cliquez sur le coffre de hello, son tableau de bord s’ouvre.
3. Dans le tableau de bord du coffre de hello sur hello **des tâches de sauvegarde** vignette, cliquez sur **des Machines virtuelles Azure** travaux de hello toodisplay associée hello coffre.

    ![tableau de bord du coffre](./media/backup-azure-arm-restore-vms/vault-dashboard-jobs.png)

    Hello **des tâches de sauvegarde** panneau s’ouvre et affiche la liste de hello des tâches.

    ![liste des machines virtuelles du coffre](./media/backup-azure-arm-restore-vms/restore-job-in-progress.png)
    
## <a name="use-templates-toocustomize-restore-vm"></a>Utiliser des modèles toocustomize restauration vm
Une fois [disques est terminée](#Track-the-restore-operation), vous pouvez utiliser le modèle hello qui est généré dans le cadre de l’opération de restauration toocreate un nouvel ordinateur virtuel avec une configuration différente de noms de configuration ou toocustomize sauvegarde des ressources créées lorsque vous créez une machine virtuelle à partir du point de restauration. 

> [!NOTE]
> Les modèles seront ajoutés dans le cadre de la restauration des disques pour les points de récupération effectuée après le 1er mars 2017. Ils sont applicables aux machines virtuelles non chiffrées et aux machines virtuelles avec disque non géré. La prise en charge des machines virtuelles chiffrées et des machines virtuelles avec disque géré est prévue dans une prochaine version. 
>
>

modèle de hello tooget généré dans le cadre de l’option de restauration des disques,

1. Accédez à détails de la tâche toorestore correspondant toohello travail. 
2. Dans l’écran de détails de travail de restauration de hello, cliquez sur *déployer le modèle* tooinitiate déploiement d’un modèle de bouton. 

     ![Détail du travail de restauration](./media/backup-azure-arm-restore-vms/restore-job-drill-down.png)
   
Dans le panneau de modèle hello déployer pour un déploiement personnalisé, utilisez un déploiement de modèle trop[modifier et déployer le modèle de hello](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template) ou ajouter d’autres personnalisations par [création d’un modèle](../azure-resource-manager/resource-group-authoring-templates.md) avant de déployer. 

   ![chargement du déploiement de modèle](./media/backup-azure-arm-restore-vms/loading-template.png)
   
Après avoir entré les valeurs hello requis, accepter hello *termes et Conditions* , puis cliquez sur **bon**.

   ![envoi du déploiement de modèle](./media/backup-azure-arm-restore-vms/submitting-template.png)

## <a name="post-restore-steps"></a>Étapes post-restauration
* Si vous utilisez une distribution Linux basée sur cloud-init telle qu’Ubuntu, le mot de passe est bloqué après la restauration pour des raisons de sécurité. Veuillez utiliser l’extension VMAccess sur hello restauré VM trop[le mot de passe réinitialisé hello](../virtual-machines/linux/classic/reset-access.md). Nous vous recommandons d’utiliser des clés SSH sur ces tooavoid distributions la réinitialisation de mot de passe après restauration.
* Extensions présentes au cours de la configuration de sauvegarde hello seront installées, mais elles ne sont pas être activées. En cas de problème, réinstallez les extensions. 
* Si sauvegardé hello IP statique, la restauration de la publication est l’ordinateur virtuel, machine virtuelle restaurée aura un conflit de tooavoid IP dynamique lors de la création de restauration machine virtuelle. En savoir plus sur la façon dont vous pouvez [ajouter un toorestored IP statique machine virtuelle](../virtual-network/virtual-networks-reserved-private-ip.md#how-to-add-a-static-internal-ip-to-an-existing-vm)
* La machine virtuelle restaurée n’aura pas de valeur de disponibilité définie. Nous recommandons d’utiliser l’option de restauration des disques et [d’ajouter un groupe à haute disponibilité](../virtual-machines/windows/tutorial-availability-sets.md) lors de la création d’une machine virtuelle depuis PowerShell ou de modèles à l’aide de disques restaurés. 


## <a name="backup-for-restored-vms"></a>Sauvegarde de machines virtuelles restaurées
Si vous avez restauré la machine virtuelle toosame groupe de ressources avec le même nom sauvegardé à l’origine de machine virtuelle de hello, sauvegarde continue sur hello restauration post de machine virtuelle. Si vous avez restauré le groupe de ressources différent de machine virtuelle tooa ou spécifiez un autre nom pour la machine virtuelle restaurée, il est considéré comme un nouvel ordinateur virtuel, et vous devez toosetup sauvegarde pour la machine virtuelle restaurée.

## <a name="restoring-a-vm-during-azure-datacenter-disaster"></a>Restauration d’une machine virtuelle en cas de défaillance du centre de données Azure
Azure Backup permet la restauration sauvegardés de centre de données associés de machines virtuelles toohello en cas de machines virtuelles s’exécutent après sinistre des expériences alors que vous avez configuré toobe de coffre de sauvegarde géo-redondant du centre de données principal de hello. Au cours de ces scénarios, vous devez tooselect un compte de stockage, ce qui n’est présent dans le centre de données associés, et le reste du processus de restauration hello reste la même. Azure Backup utilise le service de calcul de la machine virtuelle de géo-réplication appariés toocreate hello restaurée. En savoir plus sur la [résilience des centres de données Azure](../resiliency/resiliency-technical-guidance-recovery-loss-azure-region.md)

## <a name="restoring-domain-controller-vms"></a>Restauration de machines virtuelles d’un contrôleur de domaine
Azure Backup prend en charge la sauvegarde de machines virtuelles d’un contrôleur de domaine. Toutefois, être vigilant lors des processus de restauration hello. processus de restauration correcte Hello dépend de la structure de hello du domaine de hello. Dans le cas le plus simple hello, vous avez un seul contrôleur de domaine dans un domaine unique. Plus communément pour les charges de production, vous disposez d’un domaine unique avec plusieurs contrôleurs de domaine, dont certains sont peut-être locaux. Enfin, vous disposez peut-être d’une forêt avec plusieurs domaines. 

À partir d’une salutation de perspective Active Directory Azure VM revient à n’importe quel autre ordinateur virtuel sur un hyperviseur pris en charge modern. Hello principale différence avec les hyperviseurs local est qu’aucune console des ordinateurs virtuels n’est disponible dans Azure. Une console est nécessaire pour certains scénarios tels que la récupération à l’aide d’une sauvegarde de type Récupération complète (BMR, Bare Metal Recovery). Toutefois, la restauration VM hello coffre de sauvegarde est un remplacement complet pour la récupération complète. Le mode DSRM (Active Directory Restore Mode) étant également disponible, tous les scénarios de récupération Active Directory sont viables. Pour plus d’informations, voir les [considérations en matière de sauvegarde et de restauration pour les contrôleurs de domaine virtualisés](https://technet.microsoft.com/en-us/library/virtual_active_directory_domain_controller_virtualization_hyperv(v=ws.10).aspx#backup_and_restore_considerations_for_virtualized_domain_controllers) et la [planification de la récupération de forêt Active Directory](https://technet.microsoft.com/en-us/library/planning-active-directory-forest-recovery(v=ws.10).aspx).

### <a name="single-dc-in-a-single-domain"></a>Contrôleur de domaine unique dans un seul domaine
Hello machine virtuelle peut être restaurée (comme tout autre ordinateur virtuel) à partir de hello Azure portal ou à l’aide de PowerShell.

### <a name="multiple-dcs-in-a-single-domain"></a>Contrôleurs de domaine multiples dans un seul domaine
Lorsque d’autres contrôleurs de domaine de hello même domaine peut être atteint via hello réseau, hello contrôleur de domaine peut être restauré à n’importe quel ordinateur virtuel. Si elle est hello du dernier contrôleur de domaine restant dans le domaine de hello, ou une récupération dans un réseau isolé est effectuée, une procédure de récupération de forêt doit être suivie.

### <a name="multiple-domains-in-one-forest"></a>Domaines multiples dans une seule forêt
Lorsque d’autres contrôleurs de domaine de hello même domaine peut être atteint via hello réseau, hello contrôleur de domaine peut être restauré à n’importe quel ordinateur virtuel. Toutefois, dans tous les autres cas, une récupération de forêt est recommandée.

## <a name="restoring-vms-with-special-network-configurations"></a>Restauration de machines virtuelles avec des configurations de réseau spéciales
Il est possible tooback des et restauration machines virtuelles avec hello suivant les configurations réseau spéciales. Toutefois, ces configurations requièrent une attention particulière tout en parcourant le processus de restauration hello.

* Machines virtuelles sous un équilibreur de charge (interne et externe)
* Machines virtuelles avec plusieurs adresses IP réservées
* Machines virtuelles avec plusieurs cartes d'interface réseau

> [!IMPORTANT]
> Lorsque vous créez la configuration de réseau spéciales hello pour les machines virtuelles, vous devez utiliser des machines virtuelles toocreate de PowerShell à partir de disques hello restaurées.
>
>

Recréez toofully hello les ordinateurs virtuels après la restauration toodisk, procédez comme suit :

1. Restaurer des disques de hello à partir d’un coffre de services de récupération à l’aide [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
2. Créer la configuration d’ordinateur virtuel hello requise pour l’équilibrage de charge / plusieurs cartes réseau/plusieurs réservée IP à l’aide de hello applets de commande PowerShell et l’utiliser toocreate hello machine virtuelle de la configuration souhaitée.

   * Créer une machine virtuelle dans le service cloud avec un [équilibreur de charge interne ](https://azure.microsoft.com/documentation/articles/load-balancer-internal-getstarted/)
   * Créer des ordinateurs virtuels tooconnect trop[Internet exposés à équilibrage de charge](https://azure.microsoft.com/en-us/documentation/articles/load-balancer-internet-getstarted/)
   * Créer une machine virtuelle avec [plusieurs cartes d’interface réseau](https://azure.microsoft.com/documentation/articles/virtual-networks-multiple-nics/)
   * Créer des machines virtuelles avec [plusieurs adresses IP réservées](https://azure.microsoft.com/documentation/articles/virtual-networks-reserved-public-ip/)

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous pouvez restaurer vos machines virtuelles, consultez hello résolution des problèmes d’article pour plus d’informations sur les erreurs courantes liées aux machines virtuelles. Vérifiez également l’article de hello sur la gestion des tâches avec vos machines virtuelles.

* [Résolution des erreurs](backup-azure-vms-troubleshoot.md#restore)
* [Gestion des machines virtuelles](backup-azure-manage-vms.md)
