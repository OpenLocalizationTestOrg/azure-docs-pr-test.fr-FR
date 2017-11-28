---
title: "aaaManage stockage Azure à l’aide d’Azure Automation"
description: "Découvrez comment hello service Azure Automation peut être utilisé toomanage stockage Azure à l’échelle."
services: storage, automation
documentationcenter: 
author: jodoglevy
manager: eamono
editor: 
ms.assetid: bac41c39-1d95-46aa-a481-ec17bbb21b40
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: eamono
ms.openlocfilehash: 15e34128ffb0ba3315b5260442f628b5978c5197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="941b5-103">Gestion d'Azure Storage à l'aide d'Azure Automation</span><span class="sxs-lookup"><span data-stu-id="941b5-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="941b5-104">Ce guide vous oblige à service d’Azure Automation toohello et comment il peut être gestion toosimplify utilisés de vos objets BLOB Azure Storage, les tables et les files d’attente.</span><span class="sxs-lookup"><span data-stu-id="941b5-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="941b5-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="941b5-105">What is Azure Automation?</span></span>
<span data-ttu-id="941b5-106">[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="941b5-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="941b5-107">À l’aide d’Azure Automation, longues, manuelle, sujette aux erreurs et souvent répété tâches peuvent être automatisés tooincrease fiabilité et l’efficacité et réduire toovalue de temps pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="941b5-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability and efficiency, and reduce time toovalue for your organization.</span></span>

<span data-ttu-id="941b5-108">Azure Automation fournit un moteur d’exécution de flux de travail hautement fiable et à haute disponibilité qui s’adapte toomeet vos besoins que votre organisation se développe.</span><span class="sxs-lookup"><span data-stu-id="941b5-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="941b5-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="941b5-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="941b5-110">Réduire la surcharge opérationnelle et de libérer de l’informatique / toofocus du personnel DevOps sur le travail qui ajoute la valeur de l’entreprise en déplaçant votre toobe de tâches de gestion de cloud exécutés automatiquement par Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="941b5-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="941b5-111">Comment Azure Automation peut-il aider à gérer Azure Storage ?</span><span class="sxs-lookup"><span data-stu-id="941b5-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="941b5-112">Le stockage Azure peut être géré dans Azure Automation à l’aide des applets de commande hello PowerShell qui sont disponibles dans [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="941b5-112">Azure Storage can be managed in Azure Automation by using hello PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="941b5-113">Azure Automation dispose de ces applets de commande PowerShell de stockage disponibles en dehors de la zone de hello, afin que vous pouvez effectuer tous les objets blob, de table et de tâches de gestion de file d’attente dans le service de hello.</span><span class="sxs-lookup"><span data-stu-id="941b5-113">Azure Automation has these Storage PowerShell cmdlets available out of hello box, so that you can perform all of your blob, table, and queue management tasks within hello service.</span></span> <span data-ttu-id="941b5-114">Vous pouvez également de paires de ces applets de commande dans Azure Automation avec les applets de commande hello pour les autres services Azure, les tooautomate des tâches complexes entre des services Azure et les systèmes tiers 3e.</span><span class="sxs-lookup"><span data-stu-id="941b5-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="941b5-115">Hello [galerie de runbooks Azure Automation](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contient une série de produit Communauté et l’équipe runbooks tooget démarré l’automatisation de la gestion du stockage Azure, d’autres services Azure et de 3 systèmes tiers.</span><span class="sxs-lookup"><span data-stu-id="941b5-115">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="941b5-116">La galerie de Runbooks inclut :</span><span class="sxs-lookup"><span data-stu-id="941b5-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="941b5-117">Supprimer des objets blob de stockage Azure avec une certaine ancienneté à l’aide du service Automation</span><span class="sxs-lookup"><span data-stu-id="941b5-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="941b5-118">Télécharger un objet blob à partir d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="941b5-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="941b5-119">Sauvegarder tous les disques d’une machine virtuelle Azure unique ou toutes les machines virtuelles d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="941b5-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="941b5-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="941b5-120">Next Steps</span></span>
<span data-ttu-id="941b5-121">Maintenant que vous avez appris les notions de base de hello d’Azure Automation et comment il peut être utilisé toomanage des objets BLOB de stockage Azure, les tables et les files d’attente, suivez ces liens de toolearn plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="941b5-121">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure Storage blobs, tables, and queues, follow these links toolearn more about Azure Automation.</span></span>

<span data-ttu-id="941b5-122">Consultez le didacticiel d’Azure Automation hello [création ou importation d’un runbook dans Azure Automation](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="941b5-122">See hello Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

