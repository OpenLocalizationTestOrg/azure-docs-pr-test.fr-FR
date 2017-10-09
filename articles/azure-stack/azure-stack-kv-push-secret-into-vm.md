---
title: "aaaDeploy une machine virtuelle avec un certificat stocké en toute sécurité sur la pile de Azure | Documents Microsoft"
description: "Découvrez comment toodeploy une machine virtuelle et envoyé un certificat sur celui-ci à l’aide d’une clé de coffre dans la pile de Azure"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 46590eb1-1746-4ecf-a9e5-41609fde8e89
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/03/2017
ms.author: sngun
ms.openlocfilehash: b5fa0a502ba582e10ff59b8af0568bf134d3d189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a><span data-ttu-id="552c3-103">Créer une machine virtuelle et inclure un certificat récupéré à partir d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="552c3-103">Create a virtual machine and include certificate retrieved from a key vault</span></span>

<span data-ttu-id="552c3-104">Cet article vous aide à toocreate une machine virtuelle dans la pile d’Azure et les certificats de push sur lui.</span><span class="sxs-lookup"><span data-stu-id="552c3-104">This article helps you toocreate a virtual machine in Azure Stack and push certificates onto it.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="552c3-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="552c3-105">Prerequisites</span></span>

* <span data-ttu-id="552c3-106">Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés Azure hello.</span><span class="sxs-lookup"><span data-stu-id="552c3-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Azure Key Vault service.</span></span>  
* <span data-ttu-id="552c3-107">Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="552c3-107">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="552c3-108">Installer PowerShell pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="552c3-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="552c3-109">Configurer l’environnement de l’utilisateur hello pile d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="552c3-109">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="552c3-110">Un coffre de clés dans la pile de Azure est utilisé toostore certificats.</span><span class="sxs-lookup"><span data-stu-id="552c3-110">A key vault in Azure Stack is used toostore certificates.</span></span> <span data-ttu-id="552c3-111">Les certificats sont utiles dans de nombreux scénarios différents.</span><span class="sxs-lookup"><span data-stu-id="552c3-111">Certificates are helpful in many different scenarios.</span></span> <span data-ttu-id="552c3-112">Prenons l’exemple d’un scénario selon lequel une machine virtuelle dans Azure Stack exécute une application qui a besoin d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="552c3-112">For example, consider a scenario where you have a virtual machine in Azure Stack that is running an application that needs a certificate.</span></span> <span data-ttu-id="552c3-113">Ce certificat peut être utilisé pour le chiffrement, pour l’authentification tooActive Active ou SSL sur un site Web.</span><span class="sxs-lookup"><span data-stu-id="552c3-113">This certificate can be used for encrypting, for authenticating tooActive Directory, or for SSL on a website.</span></span> <span data-ttu-id="552c3-114">Des certificats hello dans un coffre de clés vous permet de vous assurer qu’il est sécurisé.</span><span class="sxs-lookup"><span data-stu-id="552c3-114">Having hello certificate in a key vault helps make sure that it's secure.</span></span>

<span data-ttu-id="552c3-115">Dans cet article, nous vous guident hello étapes toopush requis un certificat sur un ordinateur virtuel de Windows dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="552c3-115">In this article, we walk you through hello steps required toopush a certificate onto a Windows virtual machine in Azure Stack.</span></span> <span data-ttu-id="552c3-116">Vous pouvez utiliser ces étapes hello Kit de développement Azure pile ou à partir d’un client externe Windows si vous êtes connecté via VPN.</span><span class="sxs-lookup"><span data-stu-id="552c3-116">You can use these steps either from hello Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="552c3-117">hello processus requis toopush un certificat sur l’ordinateur virtuel de hello décrire les Hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="552c3-117">hello following steps describe hello process required toopush a certificate onto hello virtual machine:</span></span>

1. <span data-ttu-id="552c3-118">Créer un secret Key Vault.</span><span class="sxs-lookup"><span data-stu-id="552c3-118">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="552c3-119">Fichier de mise à jour hello azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="552c3-119">Update hello azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="552c3-120">Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="552c3-120">Deploy hello template</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="552c3-121">Créer un secret Key Vault</span><span class="sxs-lookup"><span data-stu-id="552c3-121">Create a Key Vault secret</span></span>

<span data-ttu-id="552c3-122">Hello script suivant crée un certificat au format .pfx de hello, crée un coffre de clés et stocke le certificat de hello dans le coffre de clés hello en tant que secret.</span><span class="sxs-lookup"><span data-stu-id="552c3-122">hello following script creates a certificate in hello .pfx format, creates a key vault, and stores hello certificate in hello key vault as a secret.</span></span> <span data-ttu-id="552c3-123">Vous devez utiliser hello `-EnabledForDeployment` paramètre quand vous créez un coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="552c3-123">You must use hello `-EnabledForDeployment` parameter when you're creating hello key vault.</span></span> <span data-ttu-id="552c3-124">Ce paramètre permet de s’assurer de que ce coffre de clés hello peut être référencé à partir de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="552c3-124">This parameter makes sure that hello key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in hello .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used tooexport hello certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in hello previous step>" `
  -FilePath "<Fully qualified path where hello exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload hello certificate into hello key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where hello exported certificate can be stored>"
$certPassword = "<Password used tooexport hello certificate>"

$fileContentBytes = get-content $fileName `
  -Encoding Byte

$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
$jsonObject = @"
{
"data": "$filecontentencoded",
"dataType" :"pfx",
"password": "$certPassword"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location `
  -sku standard `
  -EnabledForDeployment

$secret = ConvertTo-SecureString `
  -String $jsonEncoded `
  -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
   -SecretValue $secret

```

<span data-ttu-id="552c3-125">Lorsque vous exécutez le script précédent de hello, sortie de hello inclut le secret hello URI.</span><span class="sxs-lookup"><span data-stu-id="552c3-125">When you run hello previous script, hello output includes hello secret URI.</span></span> <span data-ttu-id="552c3-126">Notez cet URI.</span><span class="sxs-lookup"><span data-stu-id="552c3-126">Make a note of this URI.</span></span> <span data-ttu-id="552c3-127">Vous avez tooreference dans hello [Push certificat tooWindows modèle Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span><span class="sxs-lookup"><span data-stu-id="552c3-127">You have tooreference it in hello [Push certificate tooWindows Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span></span> <span data-ttu-id="552c3-128">Télécharger hello [modèle de machine virtuelle push certificat windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) dossier sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="552c3-128">Download hello [vm-push-certificate-windows template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) folder onto your development computer.</span></span> <span data-ttu-id="552c3-129">Ce dossier contient hello `azuredeploy.json` et `azuredeploy.parameters.json` fichiers dont vous aurez besoin dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="552c3-129">This folder contains hello `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in hello next steps.</span></span>

<span data-ttu-id="552c3-130">Modifier hello `azuredeploy.parameters.json` fichier selon des valeurs d’environnement tooyour.</span><span class="sxs-lookup"><span data-stu-id="552c3-130">Modify hello `azuredeploy.parameters.json` file according tooyour environment values.</span></span> <span data-ttu-id="552c3-131">paramètres de Hello un intérêt particulier sont le nom de coffre hello, groupe de ressources de coffre hello et le secret de hello URI (tel que généré par le script précédent de hello).</span><span class="sxs-lookup"><span data-stu-id="552c3-131">hello parameters of special interest are hello vault name, hello vault resource group, and hello secret URI (as generated by hello previous script).</span></span> <span data-ttu-id="552c3-132">Hello, le fichier suivant est un exemple d’un fichier de paramètres :</span><span class="sxs-lookup"><span data-stu-id="552c3-132">hello following file is an example of a parameter file:</span></span>

## <a name="update-hello-azuredeployparametersjson-file"></a><span data-ttu-id="552c3-133">Fichier de mise à jour hello azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="552c3-133">Update hello azuredeploy.parameters.json file</span></span>

<span data-ttu-id="552c3-134">Mettre à jour fichier azuredeploy.parameters.json de hello hello coffre, URI secret, VmName et autres valeurs en fonction de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="552c3-134">Update hello azuredeploy.parameters.json file with hello vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="552c3-135">Hello fichier JSON suivant illustre un exemple de fichier de paramètres de modèle hello :</span><span class="sxs-lookup"><span data-stu-id="552c3-135">hello following JSON file shows an example of hello template parameters file:</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "newStorageAccountName": {
      "value": "kvstorage01"
    },
    "vmName": {
      "value": "VM1"
    },
    "vmSize": {
      "value": "Standard_D1_v2"
    },
    "adminUserName": {
      "value": "demouser"
    },
    "adminPassword": {
      "value": "demouser@123"
    },
    "vaultName": {
      "value": "contosovault"
    },
    "vaultResourceGroup": {
      "value": "contosovaultrg"
    },
    "secretUrlWithVersion": {
      "value": "https://testkv001.vault.local.azurestack.external/secrets/testcert002/82afeeb84f4442329ce06593502e7840"
    }
  }
}
```

## <a name="deploy-hello-template"></a><span data-ttu-id="552c3-136">Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="552c3-136">Deploy hello template</span></span>

<span data-ttu-id="552c3-137">Maintenant déployer le modèle de hello en utilisant hello PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="552c3-137">Now deploy hello template by using hello following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template toocreate a VM and push hello secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```

<span data-ttu-id="552c3-138">Lorsque le modèle de hello est déployée avec succès, il en résulte hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="552c3-138">When hello template is deployed successfully, it results in hello following output:</span></span>

![Sortie du déploiement](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="552c3-140">Lorsque cet ordinateur virtuel est déployé, la pile de Azure exécute un push de certificat hello sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="552c3-140">When this virtual machine is deployed, Azure Stack pushes hello certificate onto hello virtual machine.</span></span> <span data-ttu-id="552c3-141">Dans Windows, les certificats hello sont ajouté toohello LocalMachine emplacement de certificat, avec le certificat de hello stocker cet utilisateur hello fourni.</span><span class="sxs-lookup"><span data-stu-id="552c3-141">In Windows, hello certificate is added toohello LocalMachine certificate location, with hello certificate store that hello user provided.</span></span> <span data-ttu-id="552c3-142">Sous Linux, certificat de hello est placé sous le répertoire de /var/lib/waagent hello, avec le nom de fichier hello &lt;UppercaseThumbprint&gt;.crt hello X509 fichier de certificat et &lt;UppercaseThumbprint&gt;.prv pour hello clé privée.</span><span class="sxs-lookup"><span data-stu-id="552c3-142">In Linux, hello certificate is placed under hello /var/lib/waagent directory, with hello file name &lt;UppercaseThumbprint&gt;.crt for hello X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for hello private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="552c3-143">Mettre hors service des certificats</span><span class="sxs-lookup"><span data-stu-id="552c3-143">Retire certificates</span></span>

<span data-ttu-id="552c3-144">Bonjour précédant la section, nous vous a montré comment toopush un nouveau certificat sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="552c3-144">In hello preceding section, we showed you how toopush a new certificate onto a virtual machine.</span></span> <span data-ttu-id="552c3-145">Votre ancien certificat est toujours sur l’ordinateur virtuel de hello, et il ne peut pas être supprimé.</span><span class="sxs-lookup"><span data-stu-id="552c3-145">Your old certificate is still on hello virtual machine, and it can't be removed.</span></span> <span data-ttu-id="552c3-146">Toutefois, vous pouvez désactiver hello ancienne version de code secret hello à l’aide de hello `Set-AzureKeyVaultSecretAttribute` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="552c3-146">However, you can disable hello older version of hello secret by using hello `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span> <span data-ttu-id="552c3-147">Hello Voici un exemple d’utilisation de cette applet de commande.</span><span class="sxs-lookup"><span data-stu-id="552c3-147">hello following is an example usage of this cmdlet.</span></span> <span data-ttu-id="552c3-148">Créer un nom du coffre que tooreplace hello, nom secret et selon l’environnement de tooyour les valeurs de version :</span><span class="sxs-lookup"><span data-stu-id="552c3-148">Make sure tooreplace hello vault name, secret name, and version values according tooyour environment:</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="552c3-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="552c3-149">Next steps</span></span>

* [<span data-ttu-id="552c3-150">Déployer une machine virtuelle avec un mot de passe Key Vault</span><span class="sxs-lookup"><span data-stu-id="552c3-150">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="552c3-151">Autoriser un tooaccess application coffre de clés</span><span class="sxs-lookup"><span data-stu-id="552c3-151">Allow an application tooaccess Key Vault</span></span>](azure-stack-kv-sample-app.md)


