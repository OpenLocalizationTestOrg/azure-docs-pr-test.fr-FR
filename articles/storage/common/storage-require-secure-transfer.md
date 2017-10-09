---
title: "aaaRequire un transfert sécurisé dans le stockage Azure | Documents Microsoft"
description: "En savoir plus sur la fonctionnalité de « Requièrent un transfert sécurisé » hello pour le stockage Azure et comment tooenable il."
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
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="98746-103">Exiger un transfert sécurisé</span><span class="sxs-lookup"><span data-stu-id="98746-103">Require secure transfer</span></span>

<span data-ttu-id="98746-104">option de Hello » un transfert sécurisé requis » améliore la sécurité de hello de votre compte de stockage en autorisant uniquement les demandes de compte de stockage toohello à partir des connexions sécurisées.</span><span class="sxs-lookup"><span data-stu-id="98746-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="98746-105">Par exemple, lors de l’appel tooaccess de l’API REST de votre compte de stockage, vous devez vous connecter à l’aide de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="98746-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="98746-106">Toutes les requêtes utilisant HTTP sont rejetées lorsque l’option Transfert sécurisé requis est activée.</span><span class="sxs-lookup"><span data-stu-id="98746-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="98746-107">Lorsque vous utilisez le service de fichiers Azure hello, toute connexion sans chiffrement échoue lorsque « Sécuriser le transfert requis » est activée.</span><span class="sxs-lookup"><span data-stu-id="98746-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="98746-108">Cela inclut des scénarios à l’aide de SMB 2.1, SMB 3.0 sans chiffrement et certaines versions de hello client Linux SMB.</span><span class="sxs-lookup"><span data-stu-id="98746-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="98746-109">Par défaut, l’option de hello » un transfert sécurisé requis » est désactivée.</span><span class="sxs-lookup"><span data-stu-id="98746-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="98746-110">Étant donné que le stockage Azure ne prend pas en charge HTTPS pour les noms de domaine personnalisés, cette option n’est pas appliquée lorsque vous utilisez un nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="98746-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="98746-111">Activer « Transfert sécurisé requis » Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="98746-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="98746-112">Vous pouvez activer hello » un transfert sécurisé requis » à la fois paramètre lorsque vous créez un compte de stockage dans hello [portail Azure](https://portal.azure.com)et pour les comptes de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="98746-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="98746-113">Exiger un transfert sécurisé lorsque vous créez un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="98746-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="98746-114">Ouvrez hello **créer le compte de stockage** panneau Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="98746-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="98746-115">Sous **Transfert sécurisé requis**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="98746-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![capture d’écran](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="98746-117">Exiger un transfert sécurisé pour un compte de stockage existant</span><span class="sxs-lookup"><span data-stu-id="98746-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="98746-118">Sélectionnez un compte de stockage existant dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="98746-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="98746-119">Sélectionnez **Configuration** sous **paramètres** dans le panneau de menu de compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="98746-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="98746-120">Sous **Transfert sécurisé requis**, sélectionnez **Activé**.</span><span class="sxs-lookup"><span data-stu-id="98746-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![capture d’écran](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="98746-122">Activer le paramètre « Transfert sécurisé requis » par programmation</span><span class="sxs-lookup"><span data-stu-id="98746-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="98746-123">nom du paramètre Hello est _supportsHttpsTrafficOnly_ dans les propriétés de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="98746-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="98746-124">Vous pouvez activer « Transfert sécurisé requis » avec l’API REST, des outils ou des bibliothèques :</span><span class="sxs-lookup"><span data-stu-id="98746-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="98746-125">**API REST** (Version : 2016-12-01) : [package de version](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="98746-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="98746-126">**PowerShell** (Version : 4.1.0) : [package de version](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="98746-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="98746-127">**CLI** (Version : 2.0.11) : [package de version](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="98746-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="98746-128">**NodeJS** (Version : 1.1.0) : [package de version](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="98746-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="98746-129">**SDK .NET** (Version : 6.3.0) : [package de version](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="98746-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="98746-130">**SDK Python** (Version : 1.1.0) : [package de version](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="98746-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="98746-131">**SDK Ruby** (Version : 0.11.0) : [package de version](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="98746-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="98746-132">Activer le paramètre « Transfert sécurisé requis » avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="98746-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="98746-133">toosimplify test avec l’API REST, vous pouvez utiliser [ArmClient](https://github.com/projectkudu/ARMClient) toocall à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="98746-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="98746-134">Vous pouvez utiliser sous le paramètre de hello toocheck de ligne de commande avec hello API REST :</span><span class="sxs-lookup"><span data-stu-id="98746-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="98746-135">Dans la réponse de hello, vous pouvez trouver _supportsHttpsTrafficOnly_ paramètre.</span><span class="sxs-lookup"><span data-stu-id="98746-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="98746-136">Exemple :</span><span class="sxs-lookup"><span data-stu-id="98746-136">Sample:</span></span>

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

<span data-ttu-id="98746-137">Vous pouvez utiliser sous le paramètre de hello tooenable de ligne de commande avec hello API REST :</span><span class="sxs-lookup"><span data-stu-id="98746-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="98746-138">Exemple de code Input.json :</span><span class="sxs-lookup"><span data-stu-id="98746-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="98746-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="98746-139">Next steps</span></span>
<span data-ttu-id="98746-140">Le stockage Azure fournit un ensemble complet des fonctionnalités de sécurité, qui ensemble permettent aux développeurs de toobuild des applications sécurisées.</span><span class="sxs-lookup"><span data-stu-id="98746-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="98746-141">Pour plus d’informations, visitez hello [Guide de sécurité de stockage](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="98746-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
