---
title: "Sécuriser IIS à l’aide de certificats SSL dans Azure | Microsoft Docs"
description: "Découvrez comment sécuriser le serveur web IIS à l’aide de certificats SSL sur une machine virtuelle Windows dans Azure"
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
ms.openlocfilehash: 6567853e9ef3cad63595dc0afe7a793bdc5d972c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="bcd5a-103">Sécuriser le serveur web IIS à l’aide de certificats SSL sur une machine virtuelle Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="bcd5a-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="bcd5a-104">Pour sécuriser les serveurs web, vous pouvez utiliser un certificat SSL (Secure Sockets Layer) et chiffrer ainsi le trafic web.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="bcd5a-105">Ces certificats SSL peuvent être stockés dans Azure Key Vault et autoriser les déploiements sécurisés de certificats sur les machines virtuelles Windows dans Azure.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Windows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="bcd5a-106">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bcd5a-107">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bcd5a-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="bcd5a-108">Générer ou télécharger un certificat dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="bcd5a-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="bcd5a-109">Créer une machine virtuelle et installer le serveur web IIS</span><span class="sxs-lookup"><span data-stu-id="bcd5a-109">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="bcd5a-110">Injecter le certificat dans la machine virtuelle et configurer IIS à l’aide d’une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="bcd5a-110">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="bcd5a-111">Ce didacticiel requiert le module Azure PowerShell version 3.6 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="bcd5a-112">Exécutez ` Get-Module -ListAvailable AzureRM` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="bcd5a-113">Si vous devez effectuer une mise à niveau, consultez [Installer le module Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="bcd5a-114">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bcd5a-114">Overview</span></span>
<span data-ttu-id="bcd5a-115">Azure Key Vault protège les clés de chiffrement et les secrets, tels que les certificats ou les mots de passe.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="bcd5a-116">Key Vault rationalise le processus de gestion de certificats et vous permet de garder le contrôle sur les clés d’accès à ces certificats.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="bcd5a-117">Vous pouvez créer un certificat auto-signé à l’intérieur de Key Vault ou charger un certificat approuvé existant que vous avez déjà.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="bcd5a-118">Au lieu d’utiliser une image de machine virtuelle personnalisée qui inclut des certificats intégrés, vous injectez des certificats dans une machine virtuelle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="bcd5a-119">Ce processus garantit que les certificats les plus récents sont installés sur un serveur web pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="bcd5a-120">Si vous renouvelez ou remplacez un certificat, vous n’êtes pas non plus obligé de créer une image de machine virtuelle personnalisée.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="bcd5a-121">Les certificats les plus récents sont automatiquement injectés à la création des machines virtuelles supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="bcd5a-122">Pendant tout le processus, les certificats ne quittent jamais la plateforme Azure, ni ne sont exposés dans un script, un historique de ligne de commande ou un modèle.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="bcd5a-123">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bcd5a-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="bcd5a-124">Avant de créer un coffre de clés et des certificats, créez un groupe de ressources avec [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="bcd5a-125">L’exemple suivant crée un groupe de ressources nommé *myResourceGroupSecureWeb* à l’emplacement *East US* :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="bcd5a-126">Ensuite, créez un coffre de clés avec [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="bcd5a-127">Chaque Key Vault requiert un nom unique en minuscules.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="bcd5a-128">Remplacez `<mykeyvault>` dans l’exemple suivant par le nom unique de votre propre Key Vault :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-128">Replace `<mykeyvault>` in the following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="bcd5a-129">Générer un certificat et le stocker dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="bcd5a-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="bcd5a-130">Dans un environnement de production, vous devez importer un certificat valide, signé par un fournisseur approuvé, à l’aide de la commande [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="bcd5a-131">Pour ce didacticiel, l’exemple suivant vous montre comment générer un certificat auto-signé avec la commande [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) qui utilise la stratégie de certificat par défaut à partir de [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses the default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

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


## <a name="create-a-virtual-machine"></a><span data-ttu-id="bcd5a-132">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="bcd5a-132">Create a virtual machine</span></span>
<span data-ttu-id="bcd5a-133">Définissez un nom d’utilisateur administrateur et un mot de passe pour la machine virtuelle avec [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-133">Set an administrator username and password for the VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="bcd5a-134">Vous pouvez maintenant créer la machine virtuelle avec [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-134">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="bcd5a-135">L’exemple suivant crée les composants de réseau virtuel requis, la configuration du système d’exploitation, puis une machine virtuelle nommée *myVM* :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-135">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

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

# Use the Custom Script Extension to install IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="bcd5a-136">Il faut quelques minutes pour que la machine virtuelle soit créée.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-136">It takes a few minutes for the VM to be created.</span></span> <span data-ttu-id="bcd5a-137">La dernière étape utilise l’extension de script personnalisé Azure pour installer le serveur web IIS avec [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-137">The last step uses the Azure Custom Script Extension to install the IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-to-vm-from-key-vault"></a><span data-ttu-id="bcd5a-138">Ajouter un certificat à la machine virtuelle à partir de Key Vault</span><span class="sxs-lookup"><span data-stu-id="bcd5a-138">Add a certificate to VM from Key Vault</span></span>
<span data-ttu-id="bcd5a-139">Pour ajouter le certificat à partir de Key Vault sur une machine virtuelle, obtenez l’ID du certificat avec [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-139">To add the certificate from Key Vault to a VM, obtain the ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="bcd5a-140">Ajoutez le certificat à la machine virtuelle avec [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret) :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-140">Add the certificate to the VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-to-use-the-certificate"></a><span data-ttu-id="bcd5a-141">Configurer IIS pour utiliser le certificat</span><span class="sxs-lookup"><span data-stu-id="bcd5a-141">Configure IIS to use the certificate</span></span>
<span data-ttu-id="bcd5a-142">Utilisez de nouveau l’extension de script personnalisé à l’aide de [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) pour mettre à jour la configuration d’IIS.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-142">Use the Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to update the IIS configuration.</span></span> <span data-ttu-id="bcd5a-143">Cette mise à jour applique le certificat injecté à partir de Key Vault dans IIS et configure la liaison web :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-143">This update applies the certificate injected from Key Vault to IIS and configures the web binding:</span></span>

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


### <a name="test-the-secure-web-app"></a><span data-ttu-id="bcd5a-144">Tester l’application web sécurisée</span><span class="sxs-lookup"><span data-stu-id="bcd5a-144">Test the secure web app</span></span>
<span data-ttu-id="bcd5a-145">Obtenez l’adresse IP publique de votre machine virtuelle avec [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="bcd5a-145">Obtain the public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="bcd5a-146">L’exemple suivant obtient l’adresse IP de `myPublicIP` créée précédemment :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-146">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="bcd5a-147">Vous pouvez maintenant ouvrir un navigateur web et entrer `https://<myPublicIP>` dans la barre d’adresse.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-147">Now you can open a web browser and enter `https://<myPublicIP>` in the address bar.</span></span> <span data-ttu-id="bcd5a-148">Pour accepter l’avertissement de sécurité si vous avez utilisé un certificat auto-signé, sélectionnez **Détails**, puis **Atteindre la page web** :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-148">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**:</span></span>

![Accepter l’avertissement de sécurité du navigateur web](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="bcd5a-150">Votre site IIS sécurisé apparaît maintenant comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-150">Your secured IIS website is then displayed as in the following example:</span></span>

![Afficher le site IIS sécurisé en cours d’exécution](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="bcd5a-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcd5a-152">Next steps</span></span>

<span data-ttu-id="bcd5a-153">Dans ce didacticiel, vous avez sécurisé un serveur web IIS à l’aide d’un certificat SSL stocké dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="bcd5a-154">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bcd5a-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bcd5a-155">Créer un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="bcd5a-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="bcd5a-156">Générer ou télécharger un certificat dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="bcd5a-156">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="bcd5a-157">Créer une machine virtuelle et installer le serveur web IIS</span><span class="sxs-lookup"><span data-stu-id="bcd5a-157">Create a VM and install the IIS web server</span></span>
> * <span data-ttu-id="bcd5a-158">Injecter le certificat dans la machine virtuelle et configurer IIS à l’aide d’une liaison SSL</span><span class="sxs-lookup"><span data-stu-id="bcd5a-158">Inject the certificate into the VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="bcd5a-159">Suivez ce lien pour consulter des exemples de scripts de machine virtuelle prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="bcd5a-159">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bcd5a-160">Exemples de scripts de machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="bcd5a-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)