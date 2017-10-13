---
title: "Déployer une machine virtuelle avec un mot de passe stocké de façon sécurisée sur Azure Stack | Microsoft Docs"
description: "Découvrez comment déployer une machine virtuelle en utilisant un mot de passe stocké dans Azure Stack Key Vault"
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
ms.openlocfilehash: 3292a2dfefc17e5034c66122a3eab24d6c03e694
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="create-a-virtual-machine-by-retrieving-the-password-stored-in-a-key-vault"></a><span data-ttu-id="d319f-103">Créer une machine virtuelle en récupérant le mot de passe stocké dans un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="d319f-103">Create a virtual machine by retrieving the password stored in a Key Vault</span></span>

<span data-ttu-id="d319f-104">Quand vous devez passer une valeur sécurisée lors d’un déploiement, comme un mot de passe, vous pouvez stocker cette valeur en tant que secret dans un coffre de clés Azure Stack et la référencer dans les modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d319f-104">When you need to pass a secure value such as a password during deployment, you can store that value as a secret in an Azure Stack key vault and reference it in the Azure Resource Manager templates.</span></span> <span data-ttu-id="d319f-105">Ainsi, vous ne devez pas entrer manuellement le secret chaque fois que vous déployez les ressources ; vous pouvez aussi spécifier quels utilisateurs ou principaux du service peuvent accéder au secret.</span><span class="sxs-lookup"><span data-stu-id="d319f-105">You do not need to manually enter the secret each time you deploy the resources, you can also specify which users or service principals can access the secret.</span></span> 

<span data-ttu-id="d319f-106">Dans cet article, nous vous guidons à travers les étapes nécessaires pour déployer une machine virtuelle Windows dans Azure Stack en récupérant le mot de passe qui est stocké dans un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d319f-106">In this article, we walk you through the steps required to deploy a Windows virtual machine in Azure Stack by retrieving the password that is stored in a Key Vault.</span></span> <span data-ttu-id="d319f-107">Ainsi, le mot de passe n’est jamais placé en texte brut dans le fichier des paramètres du modèle.</span><span class="sxs-lookup"><span data-stu-id="d319f-107">Therefore the password is never put in plain text in the template parameter file.</span></span> <span data-ttu-id="d319f-108">Vous pouvez utiliser les étapes à partir du Kit de développement Azure Stack, ou à partir d’un client externe si vous êtes connecté via un VPN.</span><span class="sxs-lookup"><span data-stu-id="d319f-108">You can use these steps either from the Azure Stack Development Kit, or from an external client if you are connected through VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d319f-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d319f-109">Prerequisites</span></span>
 
* <span data-ttu-id="d319f-110">Les utilisateurs doivent s’abonner à une offre qui inclut le service Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d319f-110">You must must subscribe to an offer that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="d319f-111">Installer PowerShell pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d319f-111">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* [<span data-ttu-id="d319f-112">Configurez l’environnement PowerShell de l’utilisateur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="d319f-112">Configure the Azure Stack user's PowerShell environment.</span></span>](azure-stack-powershell-configure-user.md)

<span data-ttu-id="d319f-113">Les étapes suivantes décrivent le processus nécessaire pour créer une machine virtuelle en récupérant le mot de passe stocké dans un coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="d319f-113">The following steps describe the process required to create a virtual machine by retrieving the password stored in a Key Vault:</span></span>

1. <span data-ttu-id="d319f-114">Créez un secret de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d319f-114">Create a Key Vault secret.</span></span>
2. <span data-ttu-id="d319f-115">Mettre à jour le fichier azuredeploy.parameters.json.</span><span class="sxs-lookup"><span data-stu-id="d319f-115">Update the azuredeploy.parameters.json file.</span></span>
3. <span data-ttu-id="d319f-116">Déployez le modèle.</span><span class="sxs-lookup"><span data-stu-id="d319f-116">Deploy the template.</span></span>

## <a name="create-a-key-vault-secret"></a><span data-ttu-id="d319f-117">Créer un secret Key Vault</span><span class="sxs-lookup"><span data-stu-id="d319f-117">Create a Key Vault secret</span></span>

<span data-ttu-id="d319f-118">Le script suivant crée un coffre de clés et stocke un mot de passe dans le coffre de clés en tant que secret.</span><span class="sxs-lookup"><span data-stu-id="d319f-118">The following script creates a key vault, and stores a password in the key vault as a secret.</span></span> <span data-ttu-id="d319f-119">Utilisez le paramètre `-EnabledForDeployment` quand vous créez le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="d319f-119">Use the `-EnabledForDeployment` parameter when you're creating the key vault.</span></span> <span data-ttu-id="d319f-120">Ce paramètre garantit que le coffre de clés peut être référencé à partir des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d319f-120">This parameter makes sure that the key vault can be referenced from Azure Resource Manager templates.</span></span>

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

<span data-ttu-id="d319f-121">À l’exécution du script précédent, la sortie inclut l’URI du secret.</span><span class="sxs-lookup"><span data-stu-id="d319f-121">When you run the previous script, the output includes the secret URI.</span></span> <span data-ttu-id="d319f-122">Notez cet URI.</span><span class="sxs-lookup"><span data-stu-id="d319f-122">Make a note of this URI.</span></span> <span data-ttu-id="d319f-123">Vous devez le référencer dans le modèle utilisé dans [Déployer une machine virtuelle Windows avec un mot de passe dans un coffre de clés](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv).</span><span class="sxs-lookup"><span data-stu-id="d319f-123">You have to reference it in the [Deploy Windows virtual machine with password in key vault template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv).</span></span> <span data-ttu-id="d319f-124">Téléchargez le dossier [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) sur votre ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="d319f-124">Download the [101-vm-secure-password](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-vm-windows-create-passwordfromkv) folder onto your development computer.</span></span> <span data-ttu-id="d319f-125">Ce dossier contient les fichiers `azuredeploy.json` et `azuredeploy.parameters.json` dont vous avez besoin dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="d319f-125">This folder contains the `azuredeploy.json` and `azuredeploy.parameters.json` files, which you will need in the next steps.</span></span>

<span data-ttu-id="d319f-126">Modifiez le fichier `azuredeploy.parameters.json` en fonction des valeurs de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="d319f-126">Modify the `azuredeploy.parameters.json` file according to your environment values.</span></span> <span data-ttu-id="d319f-127">Les paramètres les plus intéressants sont le nom du coffre, le groupe de ressources du coffre et l’URI du secret (généré par le script précédent).</span><span class="sxs-lookup"><span data-stu-id="d319f-127">The parameters of special interest are the vault name, the vault resource group, and the secret URI (as generated by the previous script).</span></span> <span data-ttu-id="d319f-128">Le fichier suivant est un exemple de fichier de paramètres :</span><span class="sxs-lookup"><span data-stu-id="d319f-128">The following file is an example of a parameter file:</span></span>

## <a name="update-the-azuredeployparametersjson-file"></a><span data-ttu-id="d319f-129">Mettre à jour le fichier azuredeploy.parameters.json</span><span class="sxs-lookup"><span data-stu-id="d319f-129">Update the azuredeploy.parameters.json file</span></span>

<span data-ttu-id="d319f-130">Mettez à jour le fichier azuredeploy.parameters.json avec les valeurs de la machine virtuelle KeyVaultURI, secretName, adminUsername correspondant à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="d319f-130">Update the azuredeploy.parameters.json file with the KeyVault URI, secretName, adminUsername of the virtual machine values as per your environment.</span></span> <span data-ttu-id="d319f-131">Le fichier JSON suivant est un exemple de fichier de paramètres du modèle :</span><span class="sxs-lookup"><span data-stu-id="d319f-131">The following JSON file shows an example of the template parameters file:</span></span> 

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

## <a name="template-deployment"></a><span data-ttu-id="d319f-132">Déploiement de modèle</span><span class="sxs-lookup"><span data-stu-id="d319f-132">Template deployment</span></span>

<span data-ttu-id="d319f-133">Déployez maintenant le modèle avec le script PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="d319f-133">Now deploy the template by using the following PowerShell script:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
  -Name KVPwdDeployment `
  -ResourceGroupName $resourceGroup `
  -TemplateFile "<Fully qualified path to the azuredeploy.json file>" `
  -TemplateParameterFile "<Fully qualified path to the azuredeploy.parameters.json file>"
```
<span data-ttu-id="d319f-134">Une fois le modèle déployé, la sortie suivante est générée :</span><span class="sxs-lookup"><span data-stu-id="d319f-134">When the template is deployed successfully, it results in the following output:</span></span>

![Sortie du déploiement](media/azure-stack-kv-deploy-vm-with-secret/deployment-output.png)


## <a name="next-steps"></a><span data-ttu-id="d319f-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d319f-136">Next steps</span></span>
[<span data-ttu-id="d319f-137">Déployer un exemple d’application avec Key Vault</span><span class="sxs-lookup"><span data-stu-id="d319f-137">Deploy a sample app with Key Vault</span></span>](azure-stack-kv-sample-app.md)

[<span data-ttu-id="d319f-138">Déployer une machine virtuelle avec un certificat Key Vault</span><span class="sxs-lookup"><span data-stu-id="d319f-138">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

