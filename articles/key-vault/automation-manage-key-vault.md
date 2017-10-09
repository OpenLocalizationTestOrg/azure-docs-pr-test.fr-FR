---
title: "aaaManage Azure Key Vault à l’aide d’Azure Automation | Documents Microsoft"
description: "Découvrez comment hello service Azure Automation peut être utilisé toomanage Azure Key Vault."
services: Key-Vault, automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 4e780762-19b6-4ca6-b894-ebb44c538f35
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: magoedte;csand
ms.openlocfilehash: 7f46ecc1206a96e8aeb1d086285461cb5b205472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-key-vault-using-azure-automation"></a><span data-ttu-id="b1e27-103">Gestion d'Azure Key Vault avec Azure Automation</span><span class="sxs-lookup"><span data-stu-id="b1e27-103">Managing Azure Key Vault using Azure Automation</span></span>
<span data-ttu-id="b1e27-104">Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisés de vos clés et les clés secrètes dans le coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="b1e27-104">This guide will introduce you toohello Azure Automation service and how it can be used toosimplify management of your keys and secrets in Azure Key Vault.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="b1e27-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="b1e27-105">What is Azure Automation?</span></span>
<span data-ttu-id="b1e27-106">[Azure Automation](../automation/automation-intro.md) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus et la configuration de l’état souhaité.</span><span class="sxs-lookup"><span data-stu-id="b1e27-106">[Azure Automation](../automation/automation-intro.md) is an Azure service for simplifying cloud management through process automation and desired state configuration.</span></span> <span data-ttu-id="b1e27-107">Les tâches manuelles, répétées, longue et sujettes aux erreurs à l’aide d’Azure Automation, peuvent être automatisée tooincrease fiabilité, l’efficacité et toovalue de temps pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b1e27-107">Using Azure Automation, manual, repeated, long-running, and error-prone tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="b1e27-108">Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="b1e27-108">Azure Automation provides a highly-reliable, highly-available workflow execution engine that scales toomeet your needs.</span></span> <span data-ttu-id="b1e27-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="b1e27-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="b1e27-110">Réduire la surcharge opérationnelle et de libérer de l’informatique et toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécuté automatiquement par Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b1e27-110">Reduce operational overhead and free up IT and DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-key-vault"></a><span data-ttu-id="b1e27-111">Comment Azure Automation peut-il aider à gérer Azure Key Vault ?</span><span class="sxs-lookup"><span data-stu-id="b1e27-111">How can Azure Automation help manage Azure Key Vault?</span></span>
<span data-ttu-id="b1e27-112">Le coffre de clés peuvent être géré dans Azure Automation à l’aide de hello [applets de commande de coffre de clés Azure Resource Manager](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) et [applets de commande de coffre de clés Azure Classic](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1e27-112">Key Vault can be managed in Azure Automation by using hello [AzureRM Key Vault cmdlets](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) and [Azure Classic Key Vault cmdlets](https://msdn.microsoft.com/library/azure/dn868052.aspx).</span></span> <span data-ttu-id="b1e27-113">Hello module Azure pour gérer le coffre de clés classique est disponible automatiquement dans Azure Automation, et vous pouvez importer hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) dans Azure Automation, afin que vous pouvez effectuer un grand nombre de gestion de votre coffre de clés tâches au sein du service de hello.</span><span class="sxs-lookup"><span data-stu-id="b1e27-113">hello Azure module for managing classic Key Vault is available automatically in Azure Automation, and you can import hello [AzureRM-KeyVault module](https://www.powershellgallery.com/packages/AzureRM.KeyVault/1.1.4) into Azure Automation, so that you can perform many of your Key Vault management tasks within hello service.</span></span> <span data-ttu-id="b1e27-114">Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.</span><span class="sxs-lookup"><span data-stu-id="b1e27-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="b1e27-115">Avec les applets de commande Azure Key Vault hello, vous pouvez effectuer ces tâches, entre autres :</span><span class="sxs-lookup"><span data-stu-id="b1e27-115">With hello Azure Key Vault cmdlets you can perform these tasks among others:</span></span> 

* <span data-ttu-id="b1e27-116">Création et configuration d’un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="b1e27-116">Create and configure a key vault</span></span>
* <span data-ttu-id="b1e27-117">Création ou importation d’une clé</span><span class="sxs-lookup"><span data-stu-id="b1e27-117">Create or import a key</span></span>
* <span data-ttu-id="b1e27-118">Création ou mise à jour d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="b1e27-118">Create or update a secret</span></span>
* <span data-ttu-id="b1e27-119">Mise à jour des attributs d’une clé</span><span class="sxs-lookup"><span data-stu-id="b1e27-119">Update attributes of a key</span></span>
* <span data-ttu-id="b1e27-120">Obtention d’une clé ou d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="b1e27-120">Get a key or secret</span></span>
* <span data-ttu-id="b1e27-121">Suppression d’une clé ou d’une clé secrète</span><span class="sxs-lookup"><span data-stu-id="b1e27-121">Delete a key or secret</span></span>

<span data-ttu-id="b1e27-122">Voici quelques exemples d’utilisation de PowerShell toomanage le coffre de clés :</span><span class="sxs-lookup"><span data-stu-id="b1e27-122">Here are some examples of using PowerShell toomanage Key Vault:</span></span>  

* [<span data-ttu-id="b1e27-123">Azure Key Vault – Étape par étape</span><span class="sxs-lookup"><span data-stu-id="b1e27-123">Azure Key Vault - Step by Step</span></span>](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step)
* [<span data-ttu-id="b1e27-124">Setting Up and Configuring an Azure Key Vault (Installation et configuration d’Azure Key Vault)</span><span class="sxs-lookup"><span data-stu-id="b1e27-124">Setting Up and Configuring an Azure Key Vault</span></span>](https://www.simple-talk.com/cloud/platform-as-a-service/setting-up-and-configuring-an-azure-key-vault)

## <a name="next-steps"></a><span data-ttu-id="b1e27-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1e27-125">Next steps</span></span>
<span data-ttu-id="b1e27-126">Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage coffre de clés Azure, suivez ces liens de toolearn plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="b1e27-126">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Key Vault, follow these links toolearn more about Azure Automation.</span></span>

* <span data-ttu-id="b1e27-127">Consultez hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="b1e27-127">See hello Azure Automation [Getting Started Tutorial](../automation/automation-first-runbook-graphical.md).</span></span>
* <span data-ttu-id="b1e27-128">Consultez hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span><span class="sxs-lookup"><span data-stu-id="b1e27-128">See hello [Azure Key Vault PowerShell scripts](https://gallery.technet.microsoft.com/scriptcenter/site/search?query=azure%20key%20vault&f%5B0%5D.Value=azure%20key%20vault&f%5B0%5D.Type=SearchText&ac=5).</span></span>

