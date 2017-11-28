---
title: "aaaDeploy une machine virtuelle avec un mot de passe stockée en toute sécurité sur la pile de Azure | Documents Microsoft"
description: "Découvrez comment toodeploy une machine virtuelle à l’aide d’un mot de passe stockés dans la pile d’Azure Key Vault"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 23322a49-fb7e-4dc2-8d0e-43de8cd41f80
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/08/2017
ms.author: sngun
ms.openlocfilehash: 368addc1dfc5b7adadd2151fbd6d354f7892eea5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-by-retrieving-hello-password-stored-in-a-key-vault"></a><span data-ttu-id="a4274-103">Créer un ordinateur virtuel par la récupération de mot de passe hello stocké dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="a4274-103">Create a virtual machine by retrieving hello password stored in a Key Vault</span></span>

<span data-ttu-id="a4274-104">Lorsque vous avez besoin d’une valeur sûre comme un mot de passe de toopass durant le déploiement, vous pouvez stocker cette valeur en tant que secret dans un coffre de clés Azure pile et référencez-la dans les modèles Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="a4274-104">When you need toopass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in hello Azure Resource Manager templates.</span></span> <span data-ttu-id="a4274-105">Vous n’avez pas besoin de toomanually Entrez code secret hello chaque fois que vous déployez des ressources de hello, vous pouvez également spécifier les utilisateurs ou les principaux du service accès hello secret.</span><span class="sxs-lookup"><span data-stu-id="a4274-105">You do not need toomanually enter hello secret each time you deploy hello resources, you can also specify which users or service principals can access hello secret.</span></span> 

<span data-ttu-id="a4274-106">Dans cet article, nous vous guident toodeploy requis de hello suit une machine virtuelle de Windows dans la pile de Azure par la récupération de mot de passe hello est stocké dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="a4274-106">In this article, we walk you through hello steps required toodeploy a Windows virtual machine in Azure Stack by retrieving hello password that is stored in a Key Vault.</span></span> <span data-ttu-id="a4274-107">Par conséquent, un mot de passe hello n’est jamais placée en texte brut dans le fichier de paramètres de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="a4274-107">Therefore hello password is never put in plain text in hello template parameter file.</span></span> <span data-ttu-id="a4274-108">Vous pouvez utiliser ces étapes hello Kit de développement Azure pile ou d’un client externe si vous êtes connecté via VPN.</span><span class="sxs-lookup"><span data-stu-id="a4274-108">You can use these steps either from hello Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4274-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a4274-109">Prerequisites</span></span>

* <span data-ttu-id="a4274-110">Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a4274-110">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Azure Key Vault service.</span></span>  
* <span data-ttu-id="a4274-111">Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="a4274-111">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="a4274-112">Installer PowerShell pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="a4274-112">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="a4274-113">Configurer hello pile d’Azure PowerShell environnement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a4274-113">Configure hello Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="a4274-114">Hello étapes suivantes décrivent hello processus requis toocreate un ordinateur virtuel par la récupération de mot de passe hello stocké dans un coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="a4274-114">hello following steps describe hello process required toocreate a virtual machine by retrieving hello password stored in a Key Vault:</span></span>

1. <span data-ttu-id="a4274-115">Créer un secret Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a4274-115">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="a4274-116">Fichier de mise à jour hello azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="a4274-116">Update hello azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="a4274-117">Déployer le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="a4274-117">Deploy hello template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="a4274-118">Créer un secret Key Vault</span><span class="sxs-lookup"><span data-stu-id="a4274-118">Create a Key Vault secret</span></span>

<span data-ttu-id="a4274-119">Hello script suivant crée un coffre de clés et stocke un mot de passe dans le coffre de clés hello en tant que secret.</span><span class="sxs-lookup"><span data-stu-id="a4274-119">hello following script creates a key vault, and stores a password in hello key vault as a secret.</span></span> <span data-ttu-id="a4274-120">Hello d’utilisation `-EnabledForDeployment` paramètre quand vous créez un coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="a4274-120">Use hello `-EnabledForDeployment` parameter when you're creating hello key vault.</span></span> <span data-ttu-id="a4274-121">Ce paramètre permet de s’assurer de que ce coffre de clés hello peut être référencé à partir de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a4274-121">This parameter makes sure that hello key vault can be referenced from Azure Resource Manager templates.</span></span>

```powershell

$vaultName = "contosovault"
$resourceGroup = "contosovaultrg"
$location = "local"
$secretName = "MySecret"

New-AzureRmResourceGroup `
  -Name $resourceGroup `
  -Location $location

New-AzureRmKeyVault `
  -VaultName $vaultName `
  -ResourceGroupName $resourceGroup `
  -Location $location
  -EnabledForTemplateDeployment

$secretValue = ConvertTo-SecureString -String '<Password for your virtual machine>' -AsPlainText -Force

Set-AzureKeyVaultSecret `
  -VaultName $vaultName `
  -Name $secretName `
  -SecretValue $secretValue

```

<span data-ttu-id="a4274-122">Lorsque vous exécutez le script précédent de hello, sortie de hello inclut le secret hello URI.</span><span class="sxs-lookup"><span data-stu-id="a4274-122">When you run hello previous script, hello output includes hello secret URI.</span></span> <span data-ttu-id="a4274-123">Notez cet URI.</span><span class="sxs-lookup"><span data-stu-id="a4274-123">Make a note of this URI.</span></span> <span data-ttu-id="a4274-124">Vous avez tooreference dans hello [machine virtuelle Windows de déployer avec mot de passe dans le modèle de coffre de clés](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span><span class="sxs-lookup"><span data-stu-id="a4274-124">You have tooreference it in hello [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password).</span></span> <span data-ttu-id="a4274-125">Télécharger hello [101-vm--mot de passe sécurisé](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) dossier sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="a4274-125">Download hello [101-vm-secure-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-secure-password) folder onto your development computer.</span></span> <span data-ttu-id="a4274-126">Ce dossier contient hello `azuredeploy.json` et `azuredeploy.parameters.json` fichiers dont vous aurez besoin dans les étapes suivantes hello.</span><span class="sxs-lookup"><span data-stu-id="a4274-126">This folder contains hello `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in hello next steps.</span></span>

<span data-ttu-id="a4274-127">Modifier hello `azuredeploy.parameters.json` fichier selon des valeurs d’environnement tooyour.</span><span class="sxs-lookup"><span data-stu-id="a4274-127">Modify hello `azuredeploy.parameters.json` file according tooyour environment values.</span></span> <span data-ttu-id="a4274-128">paramètres de Hello un intérêt particulier sont le nom de coffre hello, groupe de ressources de coffre hello et le secret de hello URI (tel que généré par le script précédent de hello).</span><span class="sxs-lookup"><span data-stu-id="a4274-128">hello parameters of special interest are hello vault name, hello vault resource group, and hello secret URI (as generated by hello previous script).</span></span> <span data-ttu-id="a4274-129">Hello, le fichier suivant est un exemple d’un fichier de paramètres :</span><span class="sxs-lookup"><span data-stu-id="a4274-129">hello following file is an example of a parameter file:</span></span>

## <a name="update-hello-azuredeployparametersjson-file"></a><span data-ttu-id="a4274-130">Fichier de mise à jour hello azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="a4274-130">Update hello azuredeploy.parameters.json file</span></span>

<span data-ttu-id="a4274-131">Mettre à jour les fichiers de azuredeploy.parameters.json hello avec hello KeyVault URI, secretName, adminUsername de valeurs de machine virtuelle hello conformément à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a4274-131">Update hello azuredeploy.parameters.json file with hello KeyVault URI, secretName, adminUsername of hello virtual machine values as per your environment.</span></span> <span data-ttu-id="a4274-132">Hello fichier JSON suivant illustre un exemple de fichier de paramètres de modèle hello :</span><span class="sxs-lookup"><span data-stu-id="a4274-132">hello following JSON file shows an example of hello template parameters file:</span></span> 

```json
{
    "$schema":  "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion":  "1.0.0.0",
    "parameters":  {
       "adminUsername":  {
         "value":  "demouser"
          },
         "adminPassword":  {
           "reference":  {
              "keyVault":  {
                "id":  "/subscriptions/xxxxxx/resourceGroups/RgKvPwd/providers/Microsoft.KeyVault/vaults/KvPwd"
                },
              "secretName":  "MySecret"
           }
         },
       "dnsLabelPrefix":  {
          "value":  "mydns123456"
        },
        "windowsOSVersion":  {
          "value":  "2016-Datacenter"
        }
    }
}

```

## <a name="template-deployment"></a><span data-ttu-id="a4274-133">Déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="a4274-133">Template deployment</span></span>

<span data-ttu-id="a4274-134">Maintenant déployer le modèle de hello en utilisant hello PowerShell script suivant :</span><span class="sxs-lookup"><span data-stu-id="a4274-134">Now deploy hello template by using hello following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path toohello azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path toohello azuredeploy.parameters.json file>"
```
<span data-ttu-id="a4274-135">Lorsque le modèle de hello est déployée avec succès, il en résulte hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="a4274-135">When hello template is deployed successfully, it results in hello following output:</span></span>

![Sortie du déploiement](media\azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="a4274-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4274-137">Next steps</span></span>
[<span data-ttu-id="a4274-138">Déployer un exemple d’application avec Key Vault</span><span class="sxs-lookup"><span data-stu-id="a4274-138">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="a4274-139">Déployer une machine virtuelle avec un certificat Key Vault</span><span class="sxs-lookup"><span data-stu-id="a4274-139">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

