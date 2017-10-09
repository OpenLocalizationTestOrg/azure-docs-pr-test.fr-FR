---
title: aaaCreate une machine virtuelle de Windows avec PowerShell | Documents Microsoft
description: "Créer des machines virtuelles Windows Azure PowerShell et le modèle de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>Créer une machine virtuelle Windows avec PowerShell et hello modèle de déploiement classique
> [!div class="op_single_selector"]
> * [Portail Azure - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Ces étapes montrent le fonctionnement des commandes toocustomize un ensemble d’Azure PowerShell qui créer et préconfigurer une machine virtuelle Azure Windows à l’aide d’une approche de bloc de construction. Vous pouvez utiliser ce processus tooquickly créer un jeu de commandes pour un nouvel ordinateur virtuel basé sur Windows et développez un déploiement existant ou toocreate plusieurs commandes qui définit rapidement créer un environnement de pro informatique ou de développement et de test personnalisé.

Ces étapes utilisent une méthode de cases à remplir pour créer des jeux de commandes Azure PowerShell. Cette approche peut être utile si vous êtes tooPowerShell nouveau ou vous souhaitiez tooknow le toospecify de valeurs pour la configuration réussie. Les utilisateurs expérimentés PowerShell peuvent prendre les commandes hello et remplacer leurs propres valeurs pour les variables de hello (lignes hello commençant par « $»).

Si vous n’avez pas déjà fait, suivez les instructions de hello de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell sur votre ordinateur local. Puis ouvrez une invite de commandes Windows PowerShell.

## <a name="step-1-add-your-account"></a>Étape 1 : Ajouter votre compte
1. À l’invite de commandes PowerShell hello, tapez **Add-AzureAccount** et cliquez sur **entrée**. 
2. Tapez hello adresse de messagerie associée à votre abonnement Azure et cliquez sur **continuer**. 
3. Tapez hello de mot de passe pour votre compte. 
4. Cliquez sur **Se connecter**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Étape 2 : Configurer votre abonnement et votre compte de stockage
Définissez votre abonnement Azure et le compte de stockage en exécutant ces commandes à l’invite de commandes Windows PowerShell hello. Tous les éléments entre guillemets hello, notamment hello < et >, remplacez les noms corrects hello.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Vous pouvez obtenir les nom d’abonnement approprié hello de hello propriété SubscriptionName de sortie hello Hello **Get-AzureSubscription** commande. Vous pouvez obtenir nom de compte de stockage correct hello de hello propriété Label du résultat hello de hello **Get-AzureStorageAccount** commande une fois que vous exécutez hello **Select-AzureSubscription** commande.

## <a name="step-3-determine-hello-imagefamily"></a>Étape 3 : Déterminer hello ImageFamily
Ensuite, vous devez toodetermine hello ImageFamily ou la valeur de l’étiquette pour hello image spécifique toohello correspondante machine virtuelle Azure, vous souhaitez toocreate. Vous pouvez obtenir la liste de hello de valeurs ImageFamily disponibles avec cette commande.

    Get-AzureVMImage | select ImageFamily -Unique

Voici des exemples de valeurs ImageFamily pour les ordinateurs basés sur Windows :

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1
* Windows Server 2016 Technical Preview 4
* SQL Server 2012 SP1 Enterprise sur Windows Server 2012

Si vous trouvez image hello que vous cherchez, ouvrez une nouvelle instance de l’éditeur de texte hello de votre choix ou de hello PowerShell Integrated Scripting Environment (ISE). Copiez suivant de hello en fichier texte hello ou hello PowerShell ISE, en remplaçant la valeur de ImageFamily hello.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

Dans certains cas, le nom d’image de hello est Bonjour propriété Label au lieu de hello ImageFamily valeur. Si vous ne trouvez pas image hello que vous cherchez à l’aide de la propriété ImageFamily hello, la liste des images de hello par leur propriété étiquette avec cette commande.

    Get-AzureVMImage | select Label -Unique

Si vous trouvez d’image de droite hello avec cette commande, ouvrez une nouvelle instance de l’éditeur de texte hello de votre choix ou de hello PowerShell ISE. Copiez suivant de hello en fichier texte hello ou hello PowerShell ISE, en remplaçant la valeur de l’étiquette hello.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>Étape 4 : générer votre jeu de commandes
Créer reste hello de votre commande en copiant l’ensemble approprié de hello de blocs ci-dessous dans votre nouveau fichier texte ou hello ISE renseigner les valeurs des variables hello et suppression hello < et >. Consultez hello deux [exemples](#examples) à fin hello de cet article pour avoir une idée du résultat final de hello.

Pour commencer, choisissez l'un des deux blocs de commandes suivants (obligatoire).

Option 1 : spécifiez un nom et une taille de machine virtuelle.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Option 2 : spécifiez un nom, une taille et un nom de groupe à haute disponibilité.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

Pour les valeurs de InstanceSize hello pour D, DS ou machines virtuelles de série G, consultez [Machine virtuelle et les tailles de Service Cloud pour Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

> [!NOTE]
> Si vous avez un contrat d’entreprise avec Software Assurance et que vous envisagez d’avantage tootake Hello Windows Server [hybride utilisez avantage](https://azure.microsoft.com/pricing/hybrid-use-benefit/), ajouter le **- LicenseType** paramètre toohello  **Nouveau-AzureVMConfig** applet de commande, en passant la valeur de hello **Windows_Server** hello classique pour les cas d’usage.  Vérifiez que vous utilisez une image que vous avez téléchargé ; Vous ne pouvez pas utiliser une image standard à partir de la galerie de hello avec hello avantage d’utiliser hybride.
> 
> 

Si vous le souhaitez, pour un ordinateur Windows autonome, vous devez spécifier un mot de passe et le compte d’administrateur local hello.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

Choisissez un mot de passe fort. toocheck sa force, consultez [vérificateur de mot de passe : à l’aide de mots de passe forts](https://www.microsoft.com/security/pc-security/password-checker.aspx).

Si vous le souhaitez, tooadd hello Windows ordinateur tooan domaine Active Directory existant, spécifiez le compte d’administrateur local hello et de mot de passe, de domaine hello et de nom de hello et de mot de passe d’un compte de domaine.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Pour d’autres options de configuration préalable pour les ordinateurs virtuels basés sur Windows, consultez la syntaxe hello pour hello **Windows** et **WindowsDomain** paramètre définit [ Ajouter-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).

Assignez éventuellement une machine virtuelle hello une adresse IP spécifique, appelée une adresse DIP statique.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

Vous pouvez vérifier la disponibilité d'une adresse IP particulière à l'aide de la commande suivante :

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

Assignez éventuellement sous-réseau spécifique du tooa hello machine virtuelle dans un réseau virtuel Azure.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

Si vous le souhaitez, ajoutez un ordinateur virtuel de données unique disque toohello.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Pour un contrôleur de domaine Active Directory, définissez $hcaching trop « None ».

Si vous le souhaitez, ajoutez hello tooan existant équilibrée ensemble de machines virtuelles pour le trafic externe.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

Enfin, choisissez un de ces blocs de commande requis pour la création d’ordinateur virtuel de hello.

Option 1 : Créer une machine virtuelle de hello dans un service cloud existant.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

nom court de Hello du service de cloud hello est nom hello qui apparaît dans la liste hello de Services de cloud computing dans hello portail Azure ou dans liste hello des groupes de ressources hello portail Azure.

Option 2 : Créer hello virtuels dans un service cloud existant et le réseau virtuel.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>Étape 5 : exécuter votre jeu de commandes
Passez en revue le jeu de commandes Azure PowerShell hello créé dans votre éditeur de texte ou hello PowerShell ISE composé de plusieurs blocs de commandes à partir de l’étape 4. Assurez-vous que vous avez spécifié toutes les variables hello nécessité et ont les valeurs correctes hello. Assurez-vous également que vous avez supprimé tous les hello < et > caractères.

Si vous utilisez un éditeur de texte, copie hello commande définir toohello Presse-papiers et puis cliquez sur votre invite de commandes Windows PowerShell ouverte. Cela émettre un jeu de commandes hello comme une série de commandes PowerShell et créez votre machine virtuelle Azure. Vous pouvez également exécuter commande hello Bonjour PowerShell ISE.

Si vous comptez créer cette machine virtuelle de nouveau ou une autre similaire, vous pouvez :

* Enregistrez ce jeu de commandes en tant que fichier de script PowerShell (*.ps1).
* Enregistrer cette commande défini comme un runbook Azure Automation Bonjour **comptes Automation** section Hello portail Azure.

## <a id="examples"></a>Exemples
Voici deux exemples d’étapes de hello ci-dessus toobuild des ensembles de commandes Azure PowerShell qui créent des machines virtuelles basées sur Windows.

### <a name="example-1"></a>Exemple 1
J’ai besoin d’un PowerShell toocreate hello machine virtuelle initiale pour un contrôleur de domaine Active Directory de commande de définir :

* Utilise l’image de Windows Server 2012 R2 Datacenter hello.
* A le nom hello AZDC1.
* est un ordinateur autonome
* comporte un disque de données supplémentaire de 20 Go
* A hello d’adresse IP statique 192.168.244.4.
* Est dans un sous-réseau de principal de hello du réseau virtuel de AZDatacenter hello.
* Est en hello TailspinToys-Azure cloud service.

Voici toocreate Azure PowerShell correspondante du jeu de commande hello cet ordinateur virtuel, des lignes vides entre chaque bloc pour une meilleure lisibilité.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>Exemple 2
J’ai besoin d’un PowerShell commande définir toocreate un ordinateur virtuel pour un serveur de métier qui :

* Utilise l’image de Windows Server 2012 R2 Datacenter hello.
* A le nom hello LOB1.
* Est un membre du domaine corp.contoso.com de hello.
* comporte un disque de données supplémentaire de 200 Go
* Est dans le sous-réseau du serveur frontal hello du réseau virtuel de AZDatacenter hello.
* Est en hello TailspinToys-Azure cloud service.

Voici toocreate Azure PowerShell correspondante du jeu de commande hello cet ordinateur virtuel.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>Étapes suivantes
Si vous avez besoin d’un disque de système d’exploitation qui est supérieur à 127 Go, vous pouvez [développez hello du système d’exploitation disque](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

