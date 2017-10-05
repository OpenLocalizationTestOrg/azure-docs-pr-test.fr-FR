---
title: "Déployer une machine virtuelle avec un certificat stocké de façon sécurisée sur Azure Stack | Microsoft Docs"
description: "Découvrez comment déployer une machine virtuelle et y placer un certificat avec un coffre de clés dans Azure Stack."
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
ms.openlocfilehash: 95008e783b2597895e870ceb3514bffbd4ab1dbf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-virtual-machine-and-include-certificate-retrieved-from-a-key-vault"></a><span data-ttu-id="5180c-103">Créer une machine virtuelle et inclure un certificat récupéré à partir d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="5180c-103">Create a virtual machine and include certificate retrieved from a key vault</span></span>

<span data-ttu-id="5180c-104">Cet article aide à créer une machine virtuelle dans Azure Stack et à y placer des certificats.</span><span class="sxs-lookup"><span data-stu-id="5180c-104">This article helps you to create a virtual machine in Azure Stack and push certificates onto it.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5180c-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5180c-105">Prerequisites</span></span>

* <span data-ttu-id="5180c-106">Les administrateurs cloud d’Azure Stack doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5180c-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Azure Key Vault service.</span></span>  
* <span data-ttu-id="5180c-107">Les utilisateurs doivent [s’abonner à une offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5180c-107">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="5180c-108">[Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="5180c-108">[Install PowerShell for Azure Stack.](azure-stack-powershell-install.md)</span></span>  
* <span data-ttu-id="5180c-109">[Configurez l’environnement PowerShell de l’utilisateur Azure Stack](azure-stack-powershell-configure-user.md).</span><span class="sxs-lookup"><span data-stu-id="5180c-109">[Configure the Azure Stack user's PowerShell environment](azure-stack-powershell-configure-user.md)</span></span>

<span data-ttu-id="5180c-110">Un coffre de clés dans Azure Stack est utilisé pour stocker les certificats.</span><span class="sxs-lookup"><span data-stu-id="5180c-110">A key vault in Azure Stack is used to store certificates.</span></span> <span data-ttu-id="5180c-111">Les certificats sont utiles dans de nombreux scénarios différents.</span><span class="sxs-lookup"><span data-stu-id="5180c-111">Certificates are helpful in many different scenarios.</span></span> <span data-ttu-id="5180c-112">Prenons l’exemple d’un scénario selon lequel une machine virtuelle dans Azure Stack exécute une application qui a besoin d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="5180c-112">For example, consider a scenario where you have a virtual machine in Azure Stack that is running an application that needs a certificate.</span></span> <span data-ttu-id="5180c-113">Ce certificat peut être utilisé pour le chiffrement, l’authentification auprès d’Active Directory ou le protocole SSL sur un site web.</span><span class="sxs-lookup"><span data-stu-id="5180c-113">This certificate can be used for encrypting, for authenticating to Active Directory, or for SSL on a website.</span></span> <span data-ttu-id="5180c-114">Conserver le certificat dans un coffre de clés permet d’assurer sa sécurité.</span><span class="sxs-lookup"><span data-stu-id="5180c-114">Having the certificate in a key vault helps make sure that it's secure.</span></span>

<span data-ttu-id="5180c-115">Dans cet article, nous vous guidons à travers les étapes requises pour placer un certificat sur une machine virtuelle Windows dans Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5180c-115">In this article, we walk you through the steps required to push a certificate onto a Windows virtual machine in Azure Stack.</span></span> <span data-ttu-id="5180c-116">Vous pouvez les suivre à partir du kit de développement Azure Stack ou d’un client externe Windows si vous êtes connecté via un VPN.</span><span class="sxs-lookup"><span data-stu-id="5180c-116">You can use these steps either from the Azure Stack Development Kit, or from a Windows-based external client if you are connected through VPN.</span></span>

<span data-ttu-id="5180c-117">Les étapes suivantes décrivent le processus permettant de placer un certificat sur la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="5180c-117">The following steps describe the process required to push a certificate onto the virtual machine:</span></span>

1. <span data-ttu-id="5180c-118">Créer un secret Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5180c-118">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="5180c-119">Mettre à jour le fichier azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="5180c-119">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="5180c-120">Déployer le modèle</span><span class="sxs-lookup"><span data-stu-id="5180c-120">Deploy the template</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="5180c-121">Créer un secret Key Vault</span><span class="sxs-lookup"><span data-stu-id="5180c-121">Create a Key Vault secret</span></span>

<span data-ttu-id="5180c-122">Le script suivant crée un certificat au format .pfx et un coffre de clés, puis stocke le certificat dans le coffre de clés en tant que secret.</span><span class="sxs-lookup"><span data-stu-id="5180c-122">The following script creates a certificate in the .pfx format, creates a key vault, and stores the certificate in the key vault as a secret.</span></span> <span data-ttu-id="5180c-123">Vous devez utiliser le paramètre `-EnabledForDeployment` pour créer le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="5180c-123">You must use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="5180c-124">Il garantit que le coffre de clés peut être référencé à partir de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5180c-124">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

# Create a certificate in the .pfx format
New-SelfSignedCertificate `
  -certstorelocation cert:\LocalMachine\My `
  -dnsname contoso.microsoft.com

$pwd = ConvertTo-SecureString `
  -String "<Password used to export the certificate>" `
  -Force `
  -AsPlainText

Export-PfxCertificate `
  -cert "cert:\localMachine\my\<Certificate Thumbprint that was created in the previous step>" `
  -FilePath "<Fully qualified path where the exported certificate can be stored>" `
  -Password $pwd

# Create a key vault and upload the certificate into the key vault as a secret
$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "servicecert"
$fileName = "<Fully qualified path where the exported certificate can be stored>"
$certPassword = "<Password used to export the certificate>"

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

<span data-ttu-id="5180c-125">À l’exécution du script précédent, la sortie inclut l’URI du secret.</span><span class="sxs-lookup"><span data-stu-id="5180c-125">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="5180c-126">Notez cet URI.</span><span class="sxs-lookup"><span data-stu-id="5180c-126">Make a note of this URI.</span></span> <span data-ttu-id="5180c-127">Vous devez le référencer dans le [modèle Placer le certificat dans Windows Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span><span class="sxs-lookup"><span data-stu-id="5180c-127">You have to reference it in the [Push certificate to Windows Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows).</span></span> <span data-ttu-id="5180c-128">Téléchargez le dossier [Modèle vm-push-certificate-windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="5180c-128">Download the [vm-push-certificate-windows template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-push-certificate-windows) folder onto your development computer.</span></span> <span data-ttu-id="5180c-129">Ce dossier contient les fichiers `azuredeploy.json` et `azuredeploy.parameters.json` dont vous avez besoin aux étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="5180c-129">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="5180c-130">Modifiez le fichier `azuredeploy.parameters.json` en fonction des valeurs de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="5180c-130">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="5180c-131">Les paramètres les plus intéressants sont le nom du coffre, le groupe de ressources du coffre et l’URI du secret (généré par le script précédent).</span><span class="sxs-lookup"><span data-stu-id="5180c-131">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="5180c-132">Le fichier suivant est un exemple de fichier de paramètres :</span><span class="sxs-lookup"><span data-stu-id="5180c-132">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="5180c-133">Mettre à jour le fichier azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="5180c-133">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="5180c-134">Mettez à jour le fichier azuredeploy.parameters.json avec les valeurs vaultName, URI du secret, VmName et autres en fonction de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="5180c-134">Update the azuredeploy.parameters.json file with the vaultName, secret URI, VmName, and other values as per your environment.</span></span> <span data-ttu-id="5180c-135">Le fichier JSON suivant est un exemple de fichier de paramètres du modèle :</span><span class="sxs-lookup"><span data-stu-id="5180c-135">The following JSON file shows an example of the template parameters file:</span></span> 

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

## <a name="deploy-the-template"></a><span data-ttu-id="5180c-136">Déployer le modèle</span><span class="sxs-lookup"><span data-stu-id="5180c-136">Deploy the template</span></span>

<span data-ttu-id="5180c-137">Déployez maintenant le modèle avec le script PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="5180c-137">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
# Deploy a Resource Manager template to create a VM and push the secret onto it
New-AzureRmResourceGroupDeployment `
  -Name KVDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```

<span data-ttu-id="5180c-138">Une fois le modèle déployé, la sortie suivante est générée :</span><span class="sxs-lookup"><span data-stu-id="5180c-138">When the template is deployed successfully, it results in the following output:</span></span>

![Sortie du déploiement](media\azure-stack-kv-push-secret-into-vm/deployment-output.png)

<span data-ttu-id="5180c-140">Lorsque cette machine virtuelle est déployée, Azure Stack place le certificat sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5180c-140">When this virtual machine is deployed, Azure Stack pushes the certificate onto the virtual machine.</span></span> <span data-ttu-id="5180c-141">Sous Windows, le certificat est ajouté à l’emplacement de certificat LocalMachine, avec le magasin de certificats fourni par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5180c-141">In Windows, the certificate is added to the LocalMachine certificate location, with the certificate store that the user provided.</span></span> <span data-ttu-id="5180c-142">Sous Linux, le certificat est placé dans le répertoire /var/lib/waagent, avec le nom de fichier &lt;UppercaseThumbprint&gt;.crt pour le fichier de certificat X509 et &lt;UppercaseThumbprint&gt;.prv pour la clé privée.</span><span class="sxs-lookup"><span data-stu-id="5180c-142">In Linux, the certificate is placed under the /var/lib/waagent directory, with the file name &lt;UppercaseThumbprint&gt;.crt for the X509 certificate file and &lt;UppercaseThumbprint&gt;.prv for the private key.</span></span>

## <a name="retire-certificates"></a><span data-ttu-id="5180c-143">Mettre hors service des certificats</span><span class="sxs-lookup"><span data-stu-id="5180c-143">Retire certificates</span></span>

<span data-ttu-id="5180c-144">Dans la section précédente, nous vous avons montré comment placer un nouveau certificat sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="5180c-144">In the preceding section, we showed you how to push a new certificate onto a virtual machine.</span></span> <span data-ttu-id="5180c-145">Votre ancien certificat est toujours sur la machine virtuelle ; il ne peut pas être supprimé.</span><span class="sxs-lookup"><span data-stu-id="5180c-145">Your old certificate is still on the virtual machine, and it can't be removed.</span></span> <span data-ttu-id="5180c-146">Toutefois, vous pouvez désactiver l’ancienne version du secret avec la cmdlet `Set-AzureKeyVaultSecretAttribute`.</span><span class="sxs-lookup"><span data-stu-id="5180c-146">However, you can disable the older version of the secret by using the `Set-AzureKeyVaultSecretAttribute` cmdlet.</span></span> <span data-ttu-id="5180c-147">L’exemple suivant montre comment utiliser cette cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5180c-147">The following is an example usage of this cmdlet.</span></span> <span data-ttu-id="5180c-148">Veillez à remplacer les valeurs du nom du coffre, du nom du secret et de la version en fonction de votre environnement :</span><span class="sxs-lookup"><span data-stu-id="5180c-148">Make sure to replace the vault name, secret name, and version values according to your environment:</span></span>

```powershell
Set-AzureKeyVaultSecretAttribute -VaultName contosovault -Name servicecert -Version e3391a126b65414f93f6f9806743a1f7 -Enable 0
```

## <a name="next-steps"></a><span data-ttu-id="5180c-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5180c-149">Next steps</span></span>

* [<span data-ttu-id="5180c-150">Déployer une machine virtuelle avec un mot de passe Key Vault</span><span class="sxs-lookup"><span data-stu-id="5180c-150">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)
* [<span data-ttu-id="5180c-151">Autoriser une application à accéder à Key Vault</span><span class="sxs-lookup"><span data-stu-id="5180c-151">Allow an application to access Key Vault</span></span>](azure-stack-kv-sample-app.md)


