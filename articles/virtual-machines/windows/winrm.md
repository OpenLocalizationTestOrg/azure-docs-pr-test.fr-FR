---
title: "aaaSet d’accès WinRM pour une machine virtuelle Azure | Documents Microsoft"
description: "Configurer l’accès de WinRM pour une utilisation avec une machine virtuelle Azure créée dans le modèle de déploiement du Gestionnaire de ressources hello."
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
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="e45a5-103">Configuration de l’accès WinRM pour les machines virtuelles dans Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e45a5-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="e45a5-104">WinRM dans Azure Service Management par rapport à Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e45a5-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="e45a5-105">Pour une vue d’ensemble de hello Azure Resource Manager, consultez ce [article](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="e45a5-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="e45a5-106">Pour connaître les différences entre Azure Service Management et Azure Resource Manager, consultez cet [article](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="e45a5-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="e45a5-107">Hello principale différence dans la définition de la configuration de WinRM entre deux piles de hello est ainsi les certificats hello obtient installées sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e45a5-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="e45a5-108">Dans la pile du Gestionnaire de ressources Azure hello, certificats de hello sont modélisées comme des ressources gérées par hello fournisseur de ressources de coffre de clé.</span><span class="sxs-lookup"><span data-stu-id="e45a5-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="e45a5-109">Par conséquent, utilisateur de hello doit tooprovide leur propre certificat et téléchargez-le tooa le coffre de clés avant son utilisation dans une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e45a5-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="e45a5-110">Voici les étapes hello tooset tootake d’un ordinateur virtuel avec connectivité de WinRM</span><span class="sxs-lookup"><span data-stu-id="e45a5-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="e45a5-111">Créer un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e45a5-111">Create a Key Vault</span></span>
2. <span data-ttu-id="e45a5-112">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="e45a5-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="e45a5-113">Télécharger votre coffre de tooKey un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="e45a5-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="e45a5-114">Obtenir l’URL de hello pour votre certificat auto-signé dans le coffre de clés de hello</span><span class="sxs-lookup"><span data-stu-id="e45a5-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="e45a5-115">Référencer les URL de vos certificats auto-signés lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e45a5-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="e45a5-116">Étape 1 : créer un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e45a5-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="e45a5-117">Vous pouvez utiliser hello ci-dessous commande toocreate hello coffre de clés</span><span class="sxs-lookup"><span data-stu-id="e45a5-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="e45a5-118">Étape 2 : créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="e45a5-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="e45a5-119">Vous pouvez créer un certificat auto-signé à l’aide de ce script PowerShell</span><span class="sxs-lookup"><span data-stu-id="e45a5-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="e45a5-120">Étape 3 : Téléchargez votre coffre de clés de toohello un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="e45a5-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="e45a5-121">Avant de télécharger hello certificat toohello le coffre de clés créé à l’étape 1, doit tooconverted dans un Bonjour format Microsoft.Compute comprendre de fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="e45a5-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="e45a5-122">Hello PowerShell script ci-dessous permettra de que vous faire</span><span class="sxs-lookup"><span data-stu-id="e45a5-122">hello below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path toohello .pfx file>"
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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="e45a5-123">Étape 4 : Obtenir l’URL de hello pour votre certificat auto-signé dans le coffre de clés de hello</span><span class="sxs-lookup"><span data-stu-id="e45a5-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="e45a5-124">fournisseur de ressources Microsoft.Compute Hello a besoin d’un secret de toohello URL à l’intérieur de hello coffre de clés lors de la configuration de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="e45a5-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="e45a5-125">Cela permet la clé secrète fournisseur toodownload hello hello Microsoft.Compute ressource et que vous créez des certificat équivalent de hello sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e45a5-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="e45a5-126">URL de Hello du secret de hello doit tooinclude hello version.</span><span class="sxs-lookup"><span data-stu-id="e45a5-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="e45a5-127">Un exemple d’URL se présente comme suit https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="e45a5-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="e45a5-128">Modèles</span><span class="sxs-lookup"><span data-stu-id="e45a5-128">Templates</span></span>
<span data-ttu-id="e45a5-129">Vous pouvez obtenir l’URL de toohello de lien de hello dans le modèle hello à l’aide de hello code ci-dessous</span><span class="sxs-lookup"><span data-stu-id="e45a5-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="e45a5-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e45a5-130">PowerShell</span></span>
<span data-ttu-id="e45a5-131">Vous pouvez obtenir cette URL à l’aide de hello ci-dessous la commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="e45a5-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="e45a5-132">Étape 5 : référencer les URL de vos certificats auto-signés lors de la création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e45a5-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="e45a5-133">Modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e45a5-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="e45a5-134">Lors de la création d’une machine virtuelle via des modèles, le certificat de hello est référencée dans les sections de secrets hello et hello winRM comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e45a5-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
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
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="e45a5-135">Un exemple de modèle pour hello ci-dessus trouverez ici [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="e45a5-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="e45a5-136">Pour obtenir le code source pour ce modèle, consultez [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="e45a5-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="e45a5-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e45a5-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="e45a5-138">Étape 6 : Connexion toohello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e45a5-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="e45a5-139">Avant de pouvoir connecter toohello machine virtuelle, vous devez toomake que votre ordinateur est configuré pour l’administration à distance via WinRM.</span><span class="sxs-lookup"><span data-stu-id="e45a5-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="e45a5-140">Démarrer PowerShell en tant qu’administrateur et exécutez hello ci-dessous toomake de commande que vous êtes prêt.</span><span class="sxs-lookup"><span data-stu-id="e45a5-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="e45a5-141">Vous devrez peut-être toomake que hello service WinRM est en cours d’exécution si hello ci-dessus ne fonctionne pas.</span><span class="sxs-lookup"><span data-stu-id="e45a5-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="e45a5-142">Vous pouvez le faire à l’aide de `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="e45a5-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="e45a5-143">Une fois que le programme d’installation hello est terminé, vous pouvez vous connecter à toohello machine virtuelle à l’aide de hello commande ci-dessous</span><span class="sxs-lookup"><span data-stu-id="e45a5-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
