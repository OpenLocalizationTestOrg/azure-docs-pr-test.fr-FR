---
title: "aaaBackup et la restauration de machines virtuelles à l’aide d’Azure Backup chiffré"
description: "Cet article traite de la sauvegarde de hello et expérience de restauration pour les machines virtuelles chiffré à l’aide du chiffrement de disque Azure."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 8387f186-7d7b-400a-8fc3-88a85403ea63
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/27/2017
ms.author: pajosh;markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c19ef6f58e3259949535dab32a55aaf7a8c658fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-encrypted-virtual-machines-with-azure-backup"></a>Mode tooback configuration et restauration de chiffrement de machines virtuelles dans Azure Backup
Cet article traite d’étapes toobackup et la restauration de machines virtuelles à l’aide d’Azure Backup. Il fournit également des détails sur les scénarios pris en charge, les composants requis et les étapes de dépannage en cas d’erreur.

## <a name="supported-scenarios"></a>Scénarios pris en charge
> [!NOTE]
> * La sauvegarde et la restauration de machines virtuelles chiffrées sont prises en charge uniquement pour les machines virtuelles déployées dans Resource Manager. Ces opérations ne sont pas prises en charge par les machines virtuelles classiques. <br>
> * Il est pris en charge pour Windows et Linux des machines virtuelles à l’aide du chiffrement de disque Azure, qui utilise une fonctionnalité standard BitLocker hello industrie de Windows et fonctionnalité Crypt-DM de chiffrement de tooprovide Linux de disques. <br>
> * Elles sont prises en charge uniquement pour les machines virtuelles chiffrées en même temps à l’aide de la clé de chiffrement BitLocker (BEK, BitLocker Encryption Key) et de la clé KEK (Key Encryption Key, clé de chiffrement de clé). Elles ne sont pas prises en charge pour les machines virtuelles chiffrées à l’aide de la clé de chiffrement BitLocker uniquement. <br>
>
>

## <a name="prerequisites"></a>Prérequis
1. Les machines virtuelles ont été chiffrées à l’aide d’[Azure Disk Encryption](../security/azure-security-disk-encryption.md). Elles doivent être chiffrées en même temps à l’aide de la clé de chiffrement BitLocker et de la clé KEK (Key Encryption Key, clé de chiffrement de clé).
2. Coffre Recovery services a été créé et définie à l’aide de la réplication du stockage étapes mentionnées dans l’article de hello [préparer votre environnement pour la sauvegarde](backup-azure-arm-vms-prepare.md).
3. Azure Backup a été donné [coffre de clés autorisations tooaccess](#provide-permissions-to-azure-backup) contenant des clés, secrets pour chiffré des machines virtuelles.

## <a name="backup-encrypted-vm"></a>Sauvegarde de machines virtuelles chiffrées
Utiliser hello suivant l’objectif de sauvegarde tooset étapes, définir une stratégie, configurez les éléments et le déclenchement de la sauvegarde.

### <a name="configure-backup"></a>Configurer une sauvegarde
1. Si vous avez déjà ouvert un coffre Recovery Services, passez toonext étape. Si vous n’avez pas d’un coffre Recovery Services est ouvert, mais sont Bonjour portail Azure, dans le menu du Hub hello, cliquez sur **Parcourir**.

   * Dans la liste de hello des ressources, tapez **Recovery Services**.
   * Comme vous commencez à taper, hello filtres de la liste en fonction de votre entrée. Lorsque vous voyez **Coffres Recovery Services**, cliquez dessus.

      ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     liste Hello des archivages de Recovery Services s’affiche. À partir de la liste de hello des archivages de Recovery Services, sélectionnez un coffre.

     tableau de bord Hello coffre-fort sélectionné s’ouvre.
2. À partir de la liste hello des éléments qui s’affiche sous le coffre, cliquez sur **sauvegarde** Panneau de sauvegarde tooopen hello.

      ![Ouvrir le panneau Sauvegarde](./media/backup-azure-vms-encryption/select-backup.png)
3. Dans le panneau de sauvegarde hello, cliquez sur **objectif de sauvegarde** panneau d’objectif de sauvegarde tooopen hello.

      ![Ouvrir le panneau Scénario](./media/backup-azure-vms-encryption/select-backup-goal-one.png)
4. Sur le panneau d’objectif de sauvegarde hello, définissez **sur lequel s’exécute votre charge de travail** tooAzure et **comment vous souhaitez toobackup** tooVirtual de l’ordinateur, puis cliquez sur **OK**.

   panneau d’objectif de sauvegarde Hello se ferme et panneau hello de la stratégie de sauvegarde s’ouvre.

   ![Ouvrir le panneau Scénario](./media/backup-azure-vms-encryption/select-backup-goal-two.png)
5. Dans Panneau de stratégie de sauvegarde hello, sélectionnez Stratégie de sauvegarde hello tooapply toohello coffre et cliquez sur **OK**.

      ![Sélectionner la stratégie de sauvegarde](./media/backup-azure-vms-encryption/setting-rs-backup-policy-new.png)

    Détails de Hello de stratégie par défaut de hello sont répertoriées dans les détails de hello. Si vous souhaitez toocreate une stratégie, sélectionnez **créer un nouveau** à partir du menu déroulant de hello. Une fois que vous cliquez sur **OK**, stratégie de sauvegarde hello est associé au coffre de hello.

    Ensuite, choisissez tooassociate de machines virtuelles hello avec le coffre de hello.
6. Choisissez hello chiffré des machines virtuelles tooassociate avec hello spécifié de stratégie et cliquez sur **OK**.

      ![Sélectionner des machines virtuelles chiffrées](./media/backup-azure-vms-encryption/selected-encrypted-vms.png)
7. Cette page affiche un message sur le coffre de clés sélectionnés de machines virtuelles de toohello associé chiffré. Service de sauvegarde nécessite des clés de toohello d’accès en lecture seule et les secrets dans le coffre de clés hello. Il utilise ces clés de toobackup autorisations et secret, ainsi que de hello associés des machines virtuelles. **Vous devez donner le coffre de clés autorisations toobackup service tooaccess pour les sauvegardes toowork**. Vous pouvez fournir ces autorisations à l’aide de [étapes indiquées dans la section ci-dessous sur hello](#provide-permissions-to-azure-backup).

      ![Message Machines virtuelles chiffrées](./media/backup-azure-vms-encryption/encrypted-vm-warning-message.png)

      Maintenant que vous avez défini tous les paramètres pour l’archivage hello, dans le panneau de sauvegarde hello, cliquez sur Activer la sauvegarde en bas hello de page de hello. Activer la sauvegarde déploie le coffre de toohello stratégie hello et les machines virtuelles de hello.
8. Hello prochaine phase de préparation est l’installation hello Agent de machine virtuelle ou rendre hello que l’Agent de machine virtuelle est installé. toodo hello même, procédez comme hello mentionné dans l’article de hello [préparer votre environnement pour la sauvegarde](backup-azure-arm-vms-prepare.md).

### <a name="triggering-backup-job"></a>Déclenchement d’un travail de sauvegarde
Utilisez les étapes hello mentionnés dans l’article de hello [coffre des services de sauvegarde Azure VMs toorecovery](backup-azure-arm-vms.md) tootrigger du travail de sauvegarde.

### <a name="continue-backups-of-already-backed-up-vms-with-encryption-enabled"></a>Continuer les sauvegardes des machines virtuelles déjà sauvegardées avec le chiffrement activé  
Si vous avez des machines virtuelles déjà en cours de sauvegarde dans le coffre recovery services et avez été activées pour le chiffrement à un moment ultérieur, vous devez donner le coffre de clés autorisations toobackup service tooaccess pour toocontinue de sauvegardes. Vous pouvez fournir ces autorisations à l’aide de [les étapes dans la section ci-dessous sur hello](#provide-permissions-to-azure-backup) ou à l’aide de PowerShell étapes mentionnées dans **Enable Backup** section de [documentation PowerShell](backup-azure-vms-automation.md). 

## <a name="provide-permissions-tooazure-backup"></a>Fournir des autorisations tooAzure sauvegarde
Utilisez hello suivant les étapes tooprovide autorisations pertinentes tooAzure sauvegarde tooaccess coffre de clés et effectuer la sauvegarde d’ordinateurs virtuels chiffrées :
1. Sélectionnez **Plus de services** et recherchez **Coffres de clés**.

    ![Rechercher le coffre de clés](./media/backup-azure-vms-encryption/search-key-vault.png)
    
2. À partir de la liste de hello des coffres de clé, sélectionnez coffre de clés hello associé chiffrée machine virtuelle, qui doit toobe sauvegardé.

     ![Sélectionner le coffre de clés](./media/backup-azure-vms-encryption/select-key-vault.png)
     
3. Cliquez sur **Stratégies d’accès**, puis sur **Ajouter nouveau**.

    ![Ajouter une stratégie d’accès](./media/backup-azure-vms-encryption/select-key-vault-access-policy.png)
    
4. Cliquez sur **sélectionnez principal** et type **Service de gestion de sauvegarde** dans la barre de recherche hello. 

    ![Rechercher le service de sauvegarde](./media/backup-azure-vms-encryption/search-backup-service.png)
    
5. Sélectionnez **Service de gestion de sauvegarde** et cliquez sur le bouton Sélectionner.

    ![Sélectionner le service de sauvegarde](./media/backup-azure-vms-encryption/select-backup-service.png)
    
6. Sélectionnez **Sauvegarde Azure** dans la liste déroulante Configurer à partir du modèle. Il renseigne les autorisations hello requis dans les autorisations de clé et les autorisations secrètes liste déroulante. 

    ![Sélectionner Sauvegarde Azure](./media/backup-azure-vms-encryption/select-backup-template.png)
    
7. Cliquez sur **OK**. Notez que le Service de gestion de sauvegarde est ajouté au panneau Stratégies d’accès. 

    ![Stratégie d’accès au service de sauvegarde](./media/backup-azure-vms-encryption/backup-service-access-policy.png)
    
8. Cliquez sur **Enregistrer**. Cela donnera hello requis autorisations tooAzure sauvegarde.

    ![Stratégie d’accès au service de sauvegarde](./media/backup-azure-vms-encryption/save-access-policy.png)

Une fois les autorisations fournies, vous pouvez activer la sauvegarde pour les machines virtuelles chiffrées.

## <a name="restore-encrypted-vm"></a>Restaurer une machine virtuelle chiffrée
toorestore chiffré machine virtuelle, d’utiliser d’abord restaurer des disques section mentionnée dans les étapes **restaurer les disques sauvegardés** dans [restaurer la configuration en choisissant la machine virtuelle](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Après cela, vous pouvez utiliser une des options suivantes de hello :
* Utilisez les étapes de PowerShell hello mentionnés dans [créer une machine virtuelle à partir de disques restaurés](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate complète des ordinateurs virtuels à partir de disques restaurés.
* OR, [utiliser le modèle généré dans le cadre de la restauration des disques](backup-azure-arm-restore-vms.md#use-templates-to-customize-restore-vm) toocreate machines virtuelles à partir de disques restaurés. Les modèles peuvent uniquement être utilisés pour les points de restauration créés après le 26 avril 2017.

## <a name="troubleshooting-errors"></a>Résolution des erreurs
| Opération | Détails de l’erreur | Résolution : |
| --- | --- | --- |
| Sauvegarde |La validation a échoué, car la machine virtuelle est chiffrée avec une clé BEK uniquement. Les sauvegardes peuvent être activées uniquement pour les machines virtuelles chiffrées aussi bien avec des clés BEK qu’avec des clés KEK. |La machine virtuelle doit être chiffrée simultanément à l’aide de clés BEK et KEK. Tout d’abord hello VM de déchiffrer et chiffrer à l’aide de BEK et KEK. Activez la sauvegarde une fois que la machine virtuelle est chiffrée à l’aide de BEK et KEK. En savoir plus sur la façon dont vous pouvez [déchiffrer et chiffrer hello machine virtuelle](../security/azure-security-disk-encryption.md)  |
| Restauration |Vous ne pouvez pas restaurer cette machine virtuelle chiffrée, car le coffre de clés associé à cette machine virtuelle n’existe pas. |Pour créer un coffre de clés, voir [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md). Consultez l’article de hello [restaurer le secret à l’aide d’Azure Backup et la clé de coffre de clés](backup-azure-restore-key-secret.md) toorestore clé et secret s’ils sont absent. |
| Restauration |Vous ne pouvez pas restaurer cette machine virtuelle chiffrée, car la clé et la clé secrète associées n’existent pas. |Consultez l’article de hello [restaurer le secret à l’aide d’Azure Backup et la clé de coffre de clés](backup-azure-restore-key-secret.md) toorestore clé et secret s’ils sont absent. |
| Restauration |Service de sauvegarde n’a pas de ressources de tooaccess d’autorisation dans votre abonnement. |Comme indiqué ci-dessus, commencez par restaurer les disques en suivant les étapes mentionnées dans la section **Restaurer les disques sauvegardés** dans [Choix de la configuration de restauration de la machine virtuelle](backup-azure-arm-restore-vms.md#choosing-a-vm-restore-configuration). Une fois, celui-ci PowerShell trop[créer une machine virtuelle à partir de disques restaurés](backup-azure-vms-automation.md#create-a-vm-from-restored-disks). |
|Sauvegarde | Le Service Azure Backup n’a pas suffisamment autorisations tooKey coffre pour sauvegarde de chiffré les Machines virtuelles | La machine virtuelle doit être chiffrée à l’aide de la clé de chiffrement BitLocker et de la clé KEK (Key Encryption Key, clé de chiffrement de clé). Après l’application de ce chiffrement, la sauvegarde doit être activée.  Service de sauvegarde doit être fourni ces autorisations à l’aide de [étapes indiquées dans la section hello ci-dessus](#provide-permissions-to-azure-backup) ou à l’aide des étapes PowerShell mentionnées dans hello **activer la protection** section Hello PowerShell documentation à l’adresse [tooback d’applets de commande AzureRM.RecoveryServices.Backup d’utilisation des machines virtuelles](backup-azure-vms-automation.md#back-up-azure-vms). |  
