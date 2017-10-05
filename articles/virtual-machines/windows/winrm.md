---
title: "Configurer l’accès WinRM pour une machine virtuelle Azure | Microsoft Docs"
description: "Configurez l’accès WinRM à utiliser avec une machine virtuelle Azure créée à l’aide du modèle de déploiement Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 2d6533462400bc1d93d0d3b0227769784e2658a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="57a2d-103">Configuration de l’accès WinRM pour les machines virtuelles dans Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57a2d-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="57a2d-104">WinRM dans Azure Service Management par rapport à Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57a2d-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="57a2d-105">Pour obtenir une vue d’ensemble d’Azure Resource Manager, consultez cet [article](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="57a2d-105">For an overview of the Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="57a2d-106">Pour connaître les différences entre Azure Service Management et Azure Resource Manager, consultez cet [article](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="57a2d-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="57a2d-107">La principale différence dans la configuration de WinRM dans les deux piles réside dans la manière dont le certificat est installé sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57a2d-107">The key difference in setting up WinRM configuration between the two stacks is how the certificate gets installed on the VM.</span></span> <span data-ttu-id="57a2d-108">Dans la pile Azure Resource Manager, les certificats sont modélisés en tant que ressources gérées par le fournisseur de ressources Key Vault.</span><span class="sxs-lookup"><span data-stu-id="57a2d-108">In the Azure Resource Manager stack, the certificates are modeled as resources managed by the Key Vault Resource Provider.</span></span> <span data-ttu-id="57a2d-109">Par conséquent, l’utilisateur doit fournir leur propre certificat et le charger vers un coffre de clés avant de l’utiliser dans une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57a2d-109">Therefore, the user needs to provide their own certificate and upload it to a Key Vault before using it in a VM.</span></span>

<span data-ttu-id="57a2d-110">Voici les étapes à suivre pour configurer une machine virtuelle avec une connectivité WinRM</span><span class="sxs-lookup"><span data-stu-id="57a2d-110">Here are the steps you need to take to set up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="57a2d-111">Créer un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="57a2d-111">Create a Key Vault</span></span>
2. <span data-ttu-id="57a2d-112">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="57a2d-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="57a2d-113">Charger votre certificat auto-signé dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="57a2d-113">Upload your self-signed certificate to Key Vault</span></span>
4. <span data-ttu-id="57a2d-114">Obtenir l’URL de votre certificat auto-signé dans le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="57a2d-114">Get the URL for your self-signed certificate in the Key Vault</span></span>
5. <span data-ttu-id="57a2d-115">Référencer les URL de vos certificats auto-signés lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="57a2d-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="57a2d-116">Étape 1 : créer un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="57a2d-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="57a2d-117">Vous pouvez utiliser la commande ci-dessous pour créer le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="57a2d-117">You can use the below command to create the Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="57a2d-118">Étape 2 : créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="57a2d-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="57a2d-119">Vous pouvez créer un certificat auto-signé à l’aide de ce script PowerShell</span><span class="sxs-lookup"><span data-stu-id="57a2d-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-to-the-key-vault"></a><span data-ttu-id="57a2d-120">Étape 3 : charger votre certificat auto-signé dans Key Vault</span><span class="sxs-lookup"><span data-stu-id="57a2d-120">Step 3: Upload your self-signed certificate to the Key Vault</span></span>
<span data-ttu-id="57a2d-121">Avant de charger le certificat dans le coffre de clés créé à l’étape 1, vous devez le convertir dans un format que le fournisseur de ressources Microsoft.Compute comprend.</span><span class="sxs-lookup"><span data-stu-id="57a2d-121">Before uploading the certificate to the Key Vault created in step 1, it needs to converted into a format the Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="57a2d-122">Le script PowerShell ci-dessous vous permettra de le faire</span><span class="sxs-lookup"><span data-stu-id="57a2d-122">The below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path to the .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-the-url-for-your-self-signed-certificate-in-the-key-vault"></a><span data-ttu-id="57a2d-123">Étape 4 : obtenir l’URL de votre certificat auto-signé dans le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="57a2d-123">Step 4: Get the URL for your self-signed certificate in the Key Vault</span></span>
<span data-ttu-id="57a2d-124">Le fournisseur de ressources Microsoft.Compute a besoin de l’URL de la clé secrète dans le coffre de clés lors de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57a2d-124">The Microsoft.Compute resource provider needs a URL to the secret inside the Key Vault while provisioning the VM.</span></span> <span data-ttu-id="57a2d-125">Ainsi, le fournisseur de ressources Microsoft.Compute peut télécharger la clé secrète et créer le certificat équivalent sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57a2d-125">This enables the Microsoft.Compute resource provider to download the secret and create the equivalent certificate on the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="57a2d-126">L’URL de la clé secrète doit également inclure la version.</span><span class="sxs-lookup"><span data-stu-id="57a2d-126">The URL of the secret needs to include the version as well.</span></span> <span data-ttu-id="57a2d-127">Un exemple d’URL se présente comme suit https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="57a2d-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="57a2d-128">Modèles</span><span class="sxs-lookup"><span data-stu-id="57a2d-128">Templates</span></span>
<span data-ttu-id="57a2d-129">Vous pouvez obtenir le lien vers l’URL dans le modèle à l’aide du code ci-dessous</span><span class="sxs-lookup"><span data-stu-id="57a2d-129">You can get the link to the URL in the template using the below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="57a2d-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="57a2d-130">PowerShell</span></span>
<span data-ttu-id="57a2d-131">Vous pouvez obtenir cette URL à l’aide de la commande PowerShell ci-dessous</span><span class="sxs-lookup"><span data-stu-id="57a2d-131">You can get this URL using the below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="57a2d-132">Étape 5 : référencer les URL de vos certificats auto-signés lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="57a2d-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="57a2d-133">Modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="57a2d-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="57a2d-134">Lorsque vous créez une machine virtuelle par le biais de modèles, le certificat est référencé dans la section des clés secrètes et la section winRM comme suit :</span><span class="sxs-lookup"><span data-stu-id="57a2d-134">While creating a VM through templates, the certificate gets referenced in the secrets section and the winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="57a2d-135">Vous trouverez un exemple de modèle pour machine virtuelle dans [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="57a2d-135">A sample template for the above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="57a2d-136">Pour obtenir le code source pour ce modèle, consultez [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="57a2d-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="57a2d-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="57a2d-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-to-the-vm"></a><span data-ttu-id="57a2d-138">Étape 6 : se connecter à la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="57a2d-138">Step 6: Connecting to the VM</span></span>
<span data-ttu-id="57a2d-139">Avant de vous connecter à la machine virtuelle, vous devrez vous assurer que votre machine est configurée pour la gestion à distance WinRM.</span><span class="sxs-lookup"><span data-stu-id="57a2d-139">Before you can connect to the VM you'll need to make sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="57a2d-140">Démarrez PowerShell en tant qu’administrateur et exécutez la commande ci-dessous pour vérifier que l’installation est terminée.</span><span class="sxs-lookup"><span data-stu-id="57a2d-140">Start PowerShell as an administrator and execute the below command to make sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="57a2d-141">Vous devrez peut-être vous assurer que le service WinRM est en cours d’exécution si la commande ci-dessus ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="57a2d-141">You might need to make sure the WinRM service is running if the above does not work.</span></span> <span data-ttu-id="57a2d-142">Vous pouvez le faire à l’aide de `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="57a2d-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="57a2d-143">Une fois l’installation terminée, vous pouvez vous connecter à la machine virtuelle à l’aide de la commande ci-dessous</span><span class="sxs-lookup"><span data-stu-id="57a2d-143">Once the setup is done, you can connect to the VM using the below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
