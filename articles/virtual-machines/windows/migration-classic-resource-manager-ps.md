---
title: aaaMigrate tooResource Manager avec PowerShell | Documents Microsoft
description: "Cet article assiste hello plateforme prise en charge la migration de ressources IaaS telles que les machines virtuelles (VM), les réseaux virtuels (réseaux virtuels) et les comptes de stockage à partir de tooAzure classique Resource Manager (ARM) à l’aide de commandes Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Migrer les ressources de IaaS de classique tooAzure Gestionnaire de ressources à l’aide d’Azure PowerShell
Ces étapes vous montrent comment toouse Azure PowerShell commandes toomigrate infrastructure en tant qu’une ressource de service (IaaS) à partir du modèle de déploiement du modèle toohello Azure Resource Manager hello déploiement classique.

Si vous le souhaitez, vous pouvez également migrer des ressources à l’aide de hello [Azure Interface de ligne de commande (CLI d’Azure)](../linux/migration-classic-resource-manager-cli.md).

* Pour plus d’informations sur les scénarios de migration pris en charge, consultez [plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-overview.md).
* Pour obtenir des instructions détaillées et une procédure pas à pas la migration, consultez [techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](migration-classic-resource-manager-deep-dive.md).
* [Passer en revue les erreurs courantes de migration](migration-classic-resource-manager-errors.md)

<br>
Voici un ordre de hello tooidentify organigramme dans lequel les étapes doivent toobe exécutée pendant un processus de migration

![Capture d’écran qui illustre les étapes de migration hello](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>Étape 1 : planifier la migration
Voici quelques meilleures pratiques que nous recommandons lors de l’évaluation de la migration des ressources IaaS de classique tooResource Manager :

* Lisez hello [pris en charge et non pris en charge des fonctionnalités et configurations](migration-classic-resource-manager-overview.md). Si vous avez des ordinateurs virtuels qui utilisent des configurations non prises en charge et fonctionnalités, nous vous recommandons d’attendre hello configuration ou une fonctionnalité prise en charge toobe a annoncé. Si elle répond à vos besoins, supprimer cette fonctionnalité ou sortir de cette migration tooenable de configuration.
* Si vous avez automatisé scripts aujourd'hui à déployer votre infrastructure et vos applications, essayez de toocreate une configuration de test similaire à l’aide de ces scripts pour la migration. Ou bien, vous pouvez définir des environnements d’exemple à l’aide de hello portail Azure.

> [!IMPORTANT]
> Passerelles d’application ne sont pas actuellement pris en charge pour la migration de classique tooResource Manager. toomigrate un réseau virtuel classique avec une passerelle d’Application, supprimer la passerelle de hello avant l’exécution d’un réseau de Préparer opération toomove hello. Après avoir effectué la migration de hello, reconnectez le passerelle hello dans Azure Resource Manager.
>
>Les passerelles ExpressRoute connexion circuits tooExpressRoute dans un autre abonnement ne peut pas être migrés automatiquement. Dans ce cas, supprimez la passerelle ExpressRoute de hello, migrer un réseau virtuel hello et recréez hello passerelle. Consultez [ExpressRoute de migrer des circuits et associé des réseaux virtuels à partir du modèle de déploiement du Gestionnaire de ressources hello classique toohello](../../expressroute/expressroute-migration-classic-resource-manager.md) pour plus d’informations.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>Étape 2 : Installer la version la plus récente d’Azure PowerShell hello
Il existe deux options principales tooinstall Azure PowerShell : [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) ou [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps). WebPI reçoit des mises à jour mensuelles. PowerShell Gallery reçoit des mises à jour en continu. Cet article est basé sur Azure PowerShell version 2.1.0.

Pour obtenir des instructions d’installation, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>Étape 3 : Vérifiez que vous êtes un administrateur pour l’abonnement de hello dans le portail Azure
tooperform cette migration, vous devez être ajouté en tant que coadministrateur pour l’abonnement hello Bonjour [portail Azure](https://portal.azure.com).

1. L’authentification à hello [portail Azure](https://portal.azure.com).
2. Dans le menu du Hub hello, sélectionnez **abonnement**. Si vous ne le voyez pas, sélectionnez **Autres services**.
3. Trouver l’entrée d’abonnement approprié hello, puis examinez hello **mon rôle** champ. Pour un coadministrateur, valeur de hello doit être _admin. compte_.

Si vous n’êtes pas en mesure de tooadd un coadministrateur, puis contactez un administrateur de service ou un coadministrateur pour tooget d’abonnement hello vous-même ajouté.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>Étape 4 : définition de votre abonnement inscription pour la migration
Commencez par démarrer une invite de commandes PowerShell. Pour la migration, vous devez tooset de votre environnement pour les deux classique et Gestionnaire de ressources.

Compte tooyour pour le modèle de gestionnaire de ressources hello de connexion.

```powershell
    Login-AzureRmAccount
```

Obtenir les abonnements disponibles hello à l’aide de hello de commande suivante :

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

Définissez votre abonnement Azure pour hello la session active. Cet exemple définit hello le nom de l’abonnement par défaut trop**mon abonnement Azure**. Remplacez le nom de l’abonnement exemple hello avec vos propres.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> L’inscription constitue une étape unique, mais vous devez le faire une seule fois avant de tenter la migration. Sans l’enregistrer, vous voyez hello message d’erreur suivant :
>
> *Requête invalide : l’abonnement n’est pas inscrit pour la migration.*
>
>

Enregistrer avec le fournisseur de ressources hello migration à l’aide de hello de commande suivante :

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Attendez cinq minutes pour hello inscription toofinish. Vous pouvez vérifier l’état hello d’approbation de hello à l’aide de hello de commande suivante :

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Assurez-vous que RegistrationState est `Registered` avant de continuer.

Connectez-vous maintenant compte tooyour pour le modèle classique de hello.

```powershell
    Add-AzureAccount
```

Obtenir les abonnements disponibles hello à l’aide de hello de commande suivante :

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

Définissez votre abonnement Azure pour hello la session active. Cet exemple définit abonnement par défaut de hello trop**mon abonnement Azure**. Remplacez le nom de l’abonnement exemple hello avec vos propres.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Étape 5 : Vérifiez que vous disposez assez de cœurs Machine virtuelle de Azure Resource Manager Bonjour région Azure de votre déploiement en cours ou de réseau virtuel
Vous pouvez utiliser hello suivant PowerShell commande toocheck hello nombre actuel de cœurs que dans le Gestionnaire de ressources Azure. toolearn en savoir plus sur les quotas de base, consultez [hello Azure Resource Manager et les limites](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).

Cet exemple vérifie la disponibilité de hello Bonjour **ouest des États-Unis** région. Remplacez le nom de la région exemple hello par les vôtres.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>Étape 6 : Exécuter des commandes toomigrate vos ressources IaaS
> [!NOTE]
> Toutes les opérations de hello décrites ici sont idempotent. Si vous avez un problème autre qu’une fonctionnalité non prise en charge ou une erreur de configuration, nous vous recommandons de relancer hello préparer, abandonner ou valider l’opération. plateforme de Hello tente ensuite action hello à nouveau.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>Étape 6.1 : Option 1 - migrer les machines virtuelles vers un service cloud (pas un réseau virtuel)
Obtenez la liste de services de cloud computing à l’aide de hello commande suivante, puis sur service de cloud hello choix que vous souhaitez toomigrate hello. Si hello machines virtuelles dans le service cloud hello se trouvent dans un réseau virtuel, ou si elles ont des rôles web ou de travail, la commande hello renvoie un message d’erreur.

```powershell
    Get-AzureService | ft Servicename
```

Obtenir le nom du déploiement pour le service cloud hello hello. Dans cet exemple, le nom du service hello est **mon Service**. Remplacez le nom du service exemple hello avec votre propre nom de service.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

Préparer les ordinateurs virtuels de hello dans le service cloud hello pour la migration. Vous avez deux options toochoose, à partir de.

* **Option 1. Migrer hello machines virtuelles tooa créé de plateforme réseau virtuel**

    Tout d’abord, vérifiez si vous pouvez migrer le service de cloud computing hello hello suivant les commandes à l’aide de :

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    Hello commande précédente affiche les avertissements et erreurs qui bloquent la migration. Si la validation est réussie, vous pouvez déplacer sur toohello **préparation** étape :

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **Option 2. Migrer tooan un réseau virtuel existant dans le modèle de déploiement du Gestionnaire de ressources hello**

    Cet exemple définit hello nom groupe de ressources trop**myResourceGroup**, hello trop de nom de réseau virtuel**myVirtualNetwork** et hello nom du sous-réseau trop**mySubNet**. Remplacez les noms de hello dans hello exemple avec des noms de vos propres ressources hello.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    Tout d’abord, vérifiez si vous pouvez migrer hello virtual network utilisant hello de commande suivante :

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    Hello commande précédente affiche les avertissements et erreurs qui bloquent la migration. Si la validation est réussie, vous pouvez poursuivre hello suivant l’étape de préparation :

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Une fois hello opération de préparation réussie avec l’option de hello précédant options, interroger l’état de migration de hello Hello machines virtuelles. Vérifier qu’ils sont Bonjour `Prepared` état.

Cet exemple définit hello nom d’ordinateur virtuel trop**myVM**. Remplacez le nom de l’exemple hello avec votre propre nom d’ordinateur virtuel.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

Vérifiez la configuration de hello pour hello préparé des ressources à l’aide de PowerShell ou hello portail Azure. Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello de commande suivante :

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello de commande suivante :

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>Étape 6.1 : Option 2 - migrer les machines virtuelles vers un réseau virtuel

machines virtuelles de toomigrate dans un réseau virtuel, vous migrez le réseau virtuel de hello. machines virtuelles de Hello faire migrer automatiquement avec un réseau virtuel hello. Réseau virtuel de prélèvement hello que vous souhaitez toomigrate.
> [!NOTE]
> [Migration classique de machine virtuelle unique](migrate-single-classic-to-resource-manager.md) en créant un nouvel ordinateur virtuel de gestionnaire de ressources avec des disques gérés à l’aide de fichiers de (système d’exploitation et données) de disque dur virtuel de la machine virtuelle de hello hello.
<br>

> [!NOTE]
> nom de réseau virtuel Hello peut différer de ce qui est affiché dans hello nouveau portail. nouveau portail Azure Hello affiche nom hello en tant que `[vnet-name]` , mais le nom de réseau virtuel réelle hello est de type `Group [resource-group-name] [vnet-name]`. Avant de migrer, nom de réseau virtuel réelle hello de recherche à l’aide de la commande hello `Get-AzureVnetSite | Select -Property Name` ni l’afficher dans hello ancien portail Azure. 

Cet exemple définit hello nom de réseau virtuel trop**myVnet**. Remplacez le nom de réseau virtuel exemple hello avec vos propres.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> Si les réseaux virtuels hello contient web ou des rôles de travail ou des machines virtuelles avec des configurations non prises en charge, vous obtenez un message d’erreur de validation.
>
>

Tout d’abord, vérifiez si vous pouvez migrer le réseau virtuel de hello à l’aide de hello de commande suivante :

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

Hello commande précédente affiche les avertissements et erreurs qui bloquent la migration. Si la validation est réussie, vous pouvez poursuivre hello suivant l’étape de préparation :

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Vérifiez la configuration de hello pour hello préparé les ordinateurs virtuels à l’aide d’Azure PowerShell ou hello portail Azure. Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello de commande suivante :

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello de commande suivante :

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>Étape 6.2 : migrer un compte de stockage
Une fois que vous avez terminé la migration d’ordinateurs virtuels hello, nous vous recommandons de que migrer les comptes de stockage hello.

Avant de migrer de compte de stockage hello, effectuez précédant les vérifications des conditions préalables :

* **Migrer des machines virtuelles classiques, dont les disques sont stockés dans le compte de stockage hello**

    Précédant la commande retourne les propriétés RoleName et DiskName de tous les disques de machine virtuelle classiques hello hello compte de stockage. RoleName désigne hello hello toowhich de machine virtuelle qu'un disque est attaché. Si précédant la commande retourne les disques, puis vérifiez que toowhich de machines virtuelles ces disques sont attachés sont migrés avant la migration hello compte de stockage.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Supprimer des disques de machine virtuelle classiques détachés stockées dans le compte de stockage hello**

    Trouver détachés classiques disques de machine virtuelle dans le stockage hello compte à l’aide commande suivante :

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    Si la commande ci-dessus renvoie des disques, supprimez-les en utilisant la commande suivante :

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **Supprimer les images de machine virtuelle stockés dans le compte de stockage hello**

    Disque de système d’exploitation stockée dans le compte de stockage hello précédant la commande retourne toutes les images de machine virtuelle hello.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     Disques de données stockées dans le compte de stockage hello précédant la commande retourne toutes les images de machine virtuelle hello.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    Supprimer toutes les images de machine virtuelle hello retournés par au-dessus de commandes à l’aide de la commande précédente :
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

Valider chaque compte de stockage pour la migration à l’aide de hello commande suivante. Dans cet exemple, le nom de compte de stockage hello est **myStorageAccount**. Remplacer le nom de l’exemple hello avec nom hello du compte de stockage.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

Étape suivante est le compte de stockage tooPrepare hello pour la migration

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Vérifiez la configuration de hello pour hello préparé le compte de stockage à l’aide d’Azure PowerShell ou hello portail Azure. Si vous n’êtes pas prêt pour la migration et que vous souhaitez toogo toohello arrière ancien état, utilisez hello de commande suivante :

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

Si la configuration de préparée hello semble correcte, vous pouvez mettre en œuvre et valider les ressources hello à l’aide de hello de commande suivante :

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>Étapes suivantes
* [Vue d’ensemble de la plateforme prise en charge la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Techniques détaillées sur la plateforme prise en charge la migration à partir de tooAzure classique Gestionnaire de ressources](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planification de la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Utiliser les ressources IaaS CLI toomigrate classique tooAzure Gestionnaire de ressources](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Outils de communauté qui contribuent à la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Passer en revue les erreurs courantes de migration](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Hello de révision plus Forum aux questions sur la migration des ressources IaaS de classique tooAzure Gestionnaire de ressources](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
