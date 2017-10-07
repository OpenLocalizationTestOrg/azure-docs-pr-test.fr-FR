---
title: aaaCreate une Machine virtuelle de SQL Server dans Azure PowerShell (classiques) | Documents Microsoft
description: "Fournit une procédure et des scripts PowerShell pour la création d’une machine virtuelle Azure à l’aide des images de la galerie de machines virtuelles SQL Server. Cette rubrique utilise le mode de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Approvisionner une machine virtuelle SQL Server à l’aide d’Azure PowerShell (Classic)

Cet article explique comment un ordinateur virtuel de SQL Server dans Azure à l’aide de toocreate hello applets de commande PowerShell.

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

Version de gestionnaire de ressources hello de cette rubrique, consultez [configurer un ordinateur virtuel de SQL Server à l’aide du Gestionnaire de ressources Azure PowerShell](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>Installation et configuration de PowerShell :
1. Si vous n'avez pas de compte Azure, visitez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
2. [Téléchargez et installez les commandes Azure PowerShell dernière hello](/powershell/azure/overview).
3. Démarrez Windows PowerShell et le connecter tooyour abonnement Azure avec hello **Add-AzureAccount** commande.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Déterminer votre région Azure cible

Votre machine virtuelle SQL Server est hébergée dans un service cloud qui se trouve dans une région Azure spécifique. Hello suit aider à vous toodetermine votre région, le compte de stockage et le service cloud qui sera utilisé pour le reste de hello du didacticiel de hello.

1. Déterminer le centre de données hello que vous souhaitez toouse toohost votre machine virtuelle SQL Server. Hello PowerShell commande suivante affiche une liste de noms de région disponible.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Une fois que vous avez identifié l’emplacement par défaut, définissez une variable nommée **$dcLocation** toothat région. Par exemple, hello jeux hello région trop de commande suivante « États-Unis » :

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Configuration de votre compte d'abonnement et de stockage

1. Déterminer hello abonnement Azure, vous allez utiliser pour la machine virtuelle hello.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Affecter votre toohello d’abonnement Azure cible **$subscr** variable. Définissez cet abonnement comme votre abonnement Azure actuel.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Recherchez ensuite des comptes de stockage. Hello script suivant affiche tous les comptes de stockage qui existent dans votre région choisie :

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Si vous avez besoin d’un compte de stockage, d’abord créer un nom de compte de stockage de toutes les minuscules avec la commande hello New-AzureStorageAccount comme hello l’exemple suivant :`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Affecter hello cible stockage compte nom toohello **$staccount**. Utilisez ensuite **Set-AzureSubscription** tooset hello abonnement et compte de stockage actif.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Sélectionner une image de machine virtuelle SQL Server

1. Découvrez la liste hello des images de machines virtuelles SQL Server disponibles à partir de la galerie de hello. Ces images ont toutes la propriété **ImageFamily** qui commence par « SQL ». suivant de Hello de requête affiche hello image famille disponible tooyou que SQL Server est préinstallé.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Lorsque vous trouvez la famille d’image de machine virtuelle hello, cette famille peuvent avoir plusieurs images publiées. Toofind hello plus récente publiée image nom de machine virtuelle pour votre famille de l’image sélectionnée de script suivant de hello utilisez (telles que **SQL Server 2016 RTM Enterprise sur Windows Server 2012 R2**) :

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Créer la machine virtuelle de hello

Enfin, créer hello machine virtuelle avec PowerShell :

1. Créer un cloud service toohost hello nouvelle machine virtuelle. Notez qu’il est également possible de toouse un service cloud existant à la place. Créer une nouvelle variable **$svcname** avec le nom court de hello du service de cloud hello.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Spécifiez le nom d’ordinateur virtuel hello et une taille. Pour plus d’informations sur les tailles de machines virtuelles, voir [Tailles de machines virtuelles pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Spécifiez le mot de passe et le compte d’administrateur local hello.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Exécutez hello suivant la machine virtuelle de script toocreate hello.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Pour une explication supplémentaire et les options de configuration, consultez hello **créer votre jeu de commandes** section [toocreate d’utiliser Azure PowerShell et préconfigurer des Machines virtuelles basées sur Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Exemple de script PowerShell

Hello script suivant fournit un exemple de script complet qui crée un **SQL Server 2016 RTM Enterprise sur Windows Server 2012 R2** machine virtuelle. Si vous utilisez ce script, vous devez personnaliser les variables initiale hello en suivant les étapes précédentes hello dans cette rubrique.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Connexion avec le Bureau à distance

1. Créer des fichiers RDP hello dans toolaunch de dossier de document de l’utilisateur actuel hello ces toocomplete le programme d’installation les machines virtuelles :

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. Dans le répertoire documents de hello, lancez le fichier RDP de hello. Se connecter avec un nom d’utilisateur administrateur hello et le mot de passe fourni précédemment (par exemple, si votre nom d’utilisateur a été VMAdmin, spécifiez « \VMAdmin » en tant qu’utilisateur de hello et fournir le mot de passe hello).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Configuration terminée hello Hello ordinateur SQL Server pour l’accès à distance

Une fois connecté sur l’ordinateur toohello avec le Bureau à distance, configurer SQL Server en fonction des instructions hello dans [étapes requises pour configurer la connectivité de SQL Server dans une machine virtuelle Azure](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Étapes suivantes

Vous trouverez des instructions supplémentaires pour la configuration des machines virtuelles avec PowerShell Bonjour [documentation de machines virtuelles](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Dans de nombreux cas, étape suivante de hello est toomigrate toothis de vos bases de données nouvelle machine virtuelle de serveur SQL. Pour obtenir des conseils de migration de base de données, consultez [migrer une base de données de tooSQL Server sur une machine virtuelle Azure](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Si vous êtes également intéressé par l’utilisation de hello toocreate portail Azure Machines virtuelles SQL, consultez [approvisionnement d’une Machine virtuelle de SQL Server sur Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Notez ce didacticiel hello que vous via le portail de hello crée des machines virtuelles à l’aide de parcours hello recommandée modèle du Gestionnaire de ressources, plutôt que classique hello utilisé dans cette rubrique de PowerShell.

En outre des ressources toothese, nous vous recommandons de consulter [autres rubriques liées toorunning SQL Server dans Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).
