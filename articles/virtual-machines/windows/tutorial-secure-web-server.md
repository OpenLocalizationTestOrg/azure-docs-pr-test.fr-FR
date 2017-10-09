---
title: aaaSecure IIS avec SSL des certificats dans Azure | Documents Microsoft
description: "Découvrez comment toosecure hello IIS web server avec les certificats SSL sur un ordinateur virtuel Windows Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="bfc7f-103">Sécuriser le serveur web IIS à l’aide de certificats SSL sur une machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="bfc7f-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="bfc7f-104">les serveurs web toosecure, un certificat ultérieurement SSL (Secure Sockets) peut être utilisé tooencrypt le trafic web.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="bfc7f-105">Ces certificats SSL peuvent être stockées dans le coffre de clés Azure et autoriser des déploiements sécurisés de certificats tooWindows virtual machines virtuelles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="bfc7f-106">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bfc7f-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bfc7f-107">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bfc7f-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="bfc7f-108">Générer ou télécharger un certificat de toohello le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="bfc7f-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="bfc7f-109">Créer une machine virtuelle et installer le serveur web hello IIS</span><span class="sxs-lookup"><span data-stu-id="bfc7f-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="bfc7f-110">Injecter du certificat de hello dans hello machine virtuelle et configurer IIS avec une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="bfc7f-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="bfc7f-111">Ce didacticiel nécessite hello Azure PowerShell version 3.6 ou version ultérieure du module.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="bfc7f-112">Exécutez ` Get-Module -ListAvailable AzureRM` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="bfc7f-113">Si vous avez besoin de tooupgrade, consultez [installez Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="bfc7f-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bfc7f-114">Overview</span></span>
<span data-ttu-id="bfc7f-115">Azure Key Vault protège les clés de chiffrement et les secrets, tels que les certificats ou les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="bfc7f-116">Coffre de clés permet de rationaliser le processus de gestion des certificats hello et vous permet de contrôler toomaintain clés qui accèdent à ces certificats.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="bfc7f-117">Vous pouvez créer un certificat auto-signé à l’intérieur de Key Vault ou charger un certificat approuvé existant que vous avez déjà.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="bfc7f-118">Au lieu d’utiliser une image de machine virtuelle personnalisée qui inclut des certificats intégrés, vous injectez des certificats dans une machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="bfc7f-119">Ce processus garantit que les certificats hello plus récentes sont installés sur un serveur web pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="bfc7f-120">Si vous renouvelez ou remplacez un certificat, vous ne pouvez toocreate une nouvelle image de machine virtuelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="bfc7f-121">certificats de dernière Hello sont automatiquement injectés que vous créez des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="bfc7f-122">Au cours de l’ensemble du processus hello, certificats hello jamais laisser hello plateforme Azure ou sont exposées dans un script, un historique de ligne de commande ou un modèle.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="bfc7f-123">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bfc7f-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="bfc7f-124">Avant de créer un coffre de clés et des certificats, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="bfc7f-125">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupSecureWeb* Bonjour *États-Unis* emplacement :</span><span class="sxs-lookup"><span data-stu-id="bfc7f-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="bfc7f-126">Ensuite, créez un coffre de clés avec [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="bfc7f-127">Chaque Key Vault requiert un nom unique en minuscules.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="bfc7f-128">Remplacez `<mykeyvault>` Bonjour votre propre nom de coffre de clés unique de l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bfc7f-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="bfc7f-129">Générer un certificat et le stocker dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="bfc7f-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="bfc7f-130">Dans un environnement de production, vous devez importer un certificat valide, signé par un fournisseur approuvé, à l’aide de la commande [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="bfc7f-131">Pour ce didacticiel, hello suivant montre comment vous pouvez générer un certificat auto-signé avec [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) qu’utilise hello stratégie de certificat par défaut de [ Nouveau-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a><span data-ttu-id="bfc7f-132">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bfc7f-132">Create a virtual machine</span></span>
<span data-ttu-id="bfc7f-133">Ensemble d’un nom d’utilisateur administrateur et le mot de passe de machine virtuelle avec hello [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="bfc7f-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="bfc7f-134">Vous pouvez désormais créer de machine virtuelle avec hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="bfc7f-135">Hello exemple suivant crée les composants de réseau virtuel hello requis, configuration de hello du système d’exploitation et crée ensuite un ordinateur virtuel nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="bfc7f-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="bfc7f-136">Il prend quelques minutes pour hello toobe de machine virtuelle créée.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="bfc7f-137">dernière étape Hello utilise hello Extension de Script personnalisé Azure tooinstall hello le serveur web IIS avec [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="bfc7f-138">Ajouter un tooVM de certificat à partir du coffre de clés</span><span class="sxs-lookup"><span data-stu-id="bfc7f-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="bfc7f-139">certificat de hello tooadd à partir du coffre de clés tooa machine virtuelle, obtenir les ID de hello de votre certificat avec [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="bfc7f-140">Ajouter hello certificat toohello machine virtuelle avec [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="bfc7f-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="bfc7f-141">Configurer le certificat IIS toouse hello</span><span class="sxs-lookup"><span data-stu-id="bfc7f-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="bfc7f-142">Utilisez hello Extension de Script personnalisé à l’aide de [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) configuration d’IIS tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="bfc7f-143">Cette mise à jour s’applique certificat hello injecté dans le coffre de clés tooIIS et configure la liaison de hello web :</span><span class="sxs-lookup"><span data-stu-id="bfc7f-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="bfc7f-144">Application de test hello web sécurisé</span><span class="sxs-lookup"><span data-stu-id="bfc7f-144">Test hello secure web app</span></span>
<span data-ttu-id="bfc7f-145">Obtenir hello une adresse IP publique de votre machine virtuelle avec [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="bfc7f-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="bfc7f-146">exemple Hello obtient adresse IP hello `myPublicIP` créé précédemment :</span><span class="sxs-lookup"><span data-stu-id="bfc7f-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="bfc7f-147">Vous pouvez désormais ouvrir un navigateur web et entrez `https://<myPublicIP>` dans la barre d’adresses hello.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="bfc7f-148">Avertissement de sécurité hello tooaccept si vous avez utilisé un certificat auto-signé, sélectionnez **détails** , puis **aller sur la page Web de toohello**:</span><span class="sxs-lookup"><span data-stu-id="bfc7f-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Accepter l’avertissement de sécurité du navigateur web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="bfc7f-150">Votre site Web IIS sécurisé est ensuite affichée comme hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bfc7f-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Afficher le site IIS sécurisé en cours d’exécution](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="bfc7f-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bfc7f-152">Next steps</span></span>

<span data-ttu-id="bfc7f-153">Dans ce didacticiel, vous avez sécurisé un serveur web IIS à l’aide d’un certificat SSL stocké dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="bfc7f-154">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bfc7f-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bfc7f-155">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bfc7f-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="bfc7f-156">Générer ou télécharger un certificat de toohello le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="bfc7f-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="bfc7f-157">Créer une machine virtuelle et installer le serveur web hello IIS</span><span class="sxs-lookup"><span data-stu-id="bfc7f-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="bfc7f-158">Injecter du certificat de hello dans hello machine virtuelle et configurer IIS avec une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="bfc7f-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="bfc7f-159">Suivez cette toosee lien intégrées dans les exemples de scripts de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="bfc7f-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfc7f-160">Exemples de scripts de machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="bfc7f-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)