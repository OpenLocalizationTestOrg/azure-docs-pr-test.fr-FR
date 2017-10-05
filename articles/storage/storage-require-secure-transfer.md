---
title: "Exiger un transfert sécurisé dans le stockage Azure | Microsoft Docs"
description: "Découvrez la fonctionnalité Transfert sécurisé requis pour le stockage Azure et apprenez à l’activer."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="a91ff-103">Exiger un transfert sécurisé</span><span class="sxs-lookup"><span data-stu-id="a91ff-103">Require secure transfer</span></span>

<span data-ttu-id="a91ff-104">L’option Transfert sécurisé requis améliore la sécurité de votre compte de stockage en autorisant uniquement les requêtes pour le compte de stockage à partir de connexions sécurisées.</span><span class="sxs-lookup"><span data-stu-id="a91ff-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="a91ff-105">Par exemple, lors de l’appel d’API REST pour l’accès à votre compte de stockage, vous devez vous connecter à l’aide de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a91ff-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="a91ff-106">Toutes les requêtes utilisant HTTP sont rejetées lorsque l’option Transfert sécurisé requis est activée.</span><span class="sxs-lookup"><span data-stu-id="a91ff-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="a91ff-107">Lorsque vous utilisez le service Azure Files, toute connexion sans chiffrement échoue si l’option Transfert sécurisé requis est activée.</span><span class="sxs-lookup"><span data-stu-id="a91ff-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="a91ff-108">Cela inclut des scénarios utilisant SMB 2.1, SMB 3.0 sans chiffrement, et certaines versions du client SMB Linux.</span><span class="sxs-lookup"><span data-stu-id="a91ff-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="a91ff-109">Par défaut, l’option Transfert sécurisé requis est désactivée.</span><span class="sxs-lookup"><span data-stu-id="a91ff-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="a91ff-110">Étant donné que le stockage Azure ne prend pas en charge HTTPS pour les noms de domaine personnalisés, cette option n’est pas appliquée lorsque vous utilisez un nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="a91ff-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="a91ff-111">Activer l’option Transfert sécurisé requis dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="a91ff-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="a91ff-112">Vous pouvez activer le paramètre Transfert sécurisé requis à la fois lorsque vous créez un compte de stockage dans le [portail Azure](https://portal.azure.com) et pour les comptes de stockage existants.</span><span class="sxs-lookup"><span data-stu-id="a91ff-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="a91ff-113">Exiger un transfert sécurisé lorsque vous créez un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="a91ff-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="a91ff-114">Ouvrez le panneau **Créer un compte de stockage** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a91ff-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="a91ff-115">Sous **Transfert sécurisé requis**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="a91ff-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![capture d’écran](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="a91ff-117">Exiger un transfert sécurisé pour un compte de stockage existant</span><span class="sxs-lookup"><span data-stu-id="a91ff-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="a91ff-118">Sélectionnez un compte de stockage existant dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a91ff-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="a91ff-119">Sélectionnez **Configuration** sous **PARAMÈTRES** dans le panneau de menu du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a91ff-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="a91ff-120">Sous **Transfert sécurisé requis**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="a91ff-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![capture d’écran](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="a91ff-122">Activer le paramètre « Transfert sécurisé requis » par programmation</span><span class="sxs-lookup"><span data-stu-id="a91ff-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="a91ff-123">Le nom du paramètre est _supportsHttpsTrafficOnly_ dans les propriétés du compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="a91ff-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="a91ff-124">Vous pouvez activer « Transfert sécurisé requis » avec l’API REST, des outils ou des bibliothèques :</span><span class="sxs-lookup"><span data-stu-id="a91ff-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="a91ff-125">**API REST** (Version : 2016-12-01) : [package de version](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="a91ff-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="a91ff-126">**PowerShell** (Version : 4.1.0) : [package de version](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="a91ff-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="a91ff-127">**CLI** (Version : 2.0.11) : [package de version](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="a91ff-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="a91ff-128">**NodeJS** (Version : 1.1.0) : [package de version](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="a91ff-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="a91ff-129">**SDK .NET** (Version : 6.3.0) : [package de version](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="a91ff-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="a91ff-130">**SDK Python** (Version : 1.1.0) : [package de version](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="a91ff-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="a91ff-131">**SDK Ruby** (Version : 0.11.0) : [package de version](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="a91ff-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="a91ff-132">Activer le paramètre « Transfert sécurisé requis » avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="a91ff-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="a91ff-133">Pour simplifier les tests avec l’API REST, vous pouvez utiliser [ArmClient](https://github.com/projectkudu/ARMClient) pour appeler à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="a91ff-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="a91ff-134">Vous pouvez utiliser la ligne de commande ci-dessous pour vérifier le paramètre avec l’API REST :</span><span class="sxs-lookup"><span data-stu-id="a91ff-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="a91ff-135">Dans la réponse figure le paramètre _supportsHttpsTrafficOnly_.</span><span class="sxs-lookup"><span data-stu-id="a91ff-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="a91ff-136">Exemple :</span><span class="sxs-lookup"><span data-stu-id="a91ff-136">Sample:</span></span>

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

<span data-ttu-id="a91ff-137">Vous pouvez utiliser la ligne de commande ci-dessous pour activer le paramètre avec l’API REST :</span><span class="sxs-lookup"><span data-stu-id="a91ff-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="a91ff-138">Exemple de code Input.json :</span><span class="sxs-lookup"><span data-stu-id="a91ff-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="a91ff-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a91ff-139">Next steps</span></span>
<span data-ttu-id="a91ff-140">Stockage Azure propose un ensemble complet de fonctionnalités de sécurité qui, une fois réunies, permettent aux développeurs de créer des applications sécurisées.</span><span class="sxs-lookup"><span data-stu-id="a91ff-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="a91ff-141">Pour plus d’informations, consultez notre [guide de sécurité sur Stockage](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="a91ff-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
