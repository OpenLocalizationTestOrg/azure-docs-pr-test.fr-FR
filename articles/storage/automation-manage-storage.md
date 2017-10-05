---
title: "Gestion d'Azure Storage à l'aide d'Azure Automation"
description: "Découvrez comment le service Azure Automation peut être utilisé pour gérer Azure Storage à grande échelle."
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
ms.openlocfilehash: fbf1cd9e73615f8d991f348cb705aa9df8b55b4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-storage-using-azure-automation"></a><span data-ttu-id="748cb-103">Gestion d'Azure Storage à l'aide d'Azure Automation</span><span class="sxs-lookup"><span data-stu-id="748cb-103">Managing Azure Storage using Azure Automation</span></span>
<span data-ttu-id="748cb-104">Ce guide vous présente le service Azure Automation et la manière de l'utiliser pour gérer plus simplement vos objets blob, vos tables et vos files d'attente Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="748cb-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure Storage blobs, tables, and queues.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="748cb-105">Qu'est-ce qu'Azure Automation ?</span><span class="sxs-lookup"><span data-stu-id="748cb-105">What is Azure Automation?</span></span>
<span data-ttu-id="748cb-106">[Azure Automation](https://azure.microsoft.com/services/automation/) est un service Azure destiné à simplifier la gestion du cloud via l'automatisation des processus.</span><span class="sxs-lookup"><span data-stu-id="748cb-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="748cb-107">Azure Automation permet d'automatiser les tâches fastidieuses, manuelles, propices aux erreurs et répétitives, afin d'augmenter la fiabilité, l'efficacité et réduire le retour sur investissement pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="748cb-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability and efficiency, and reduce time to value for your organization.</span></span>

<span data-ttu-id="748cb-108">Azure Automation fournit un moteur d'exécution de workflow hautement fiable et hautement disponible, qui s'adapte à vos besoins au fur et à mesure que votre entreprise se développe.</span><span class="sxs-lookup"><span data-stu-id="748cb-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="748cb-109">Dans Azure Automation, les processus peuvent être lancés manuellement, par des systèmes tiers ou à des intervalles planifiés, afin que les tâches interviennent exactement au moment opportun.</span><span class="sxs-lookup"><span data-stu-id="748cb-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="748cb-110">Réduisez les coûts opérationnels et dégagez du temps pour votre personnel informatique/DevOps afin de lui permettre de se concentrer sur des tâches générant une valeur ajoutée pour l'entreprise, en configurant Azure Automation pour exécuter automatiquement vos tâches de gestion de cloud.</span><span class="sxs-lookup"><span data-stu-id="748cb-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-storage"></a><span data-ttu-id="748cb-111">Comment Azure Automation peut-il aider à gérer Azure Storage ?</span><span class="sxs-lookup"><span data-stu-id="748cb-111">How can Azure Automation help manage Azure Storage?</span></span>
<span data-ttu-id="748cb-112">Azure Storage peut être géré dans Azure Automation à l’aide des applets de commande PowerShell disponibles dans [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span><span class="sxs-lookup"><span data-stu-id="748cb-112">Azure Storage can be managed in Azure Automation by using the PowerShell cmdlets that are available in [Azure PowerShell](https://msdn.microsoft.com/library/azure/jj156055.aspx).</span></span> <span data-ttu-id="748cb-113">Azure Automation dispose dès le départ de ces applets de commande PowerShell pour Storage, de sorte que vous pouvez effectuer toutes vos tâches de gestion d'objets blob, de tables et de files d'attente au sein du service.</span><span class="sxs-lookup"><span data-stu-id="748cb-113">Azure Automation has these Storage PowerShell cmdlets available out of the box, so that you can perform all of your blob, table, and queue management tasks within the service.</span></span> <span data-ttu-id="748cb-114">Dans Azure Automation, vous pouvez également associer ces applets de commande à des applets de commande d'autres services Azure, afin d'automatiser des tâches complexes entre des services Azure et des systèmes tiers.</span><span class="sxs-lookup"><span data-stu-id="748cb-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="748cb-115">La [galerie de Runbooks d’Azure Automation](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contient de nombreux Runbooks d’équipe produit et de communauté pour commencer à automatiser la gestion d’Azure Storage, d’autres services Azure et de systèmes tiers.</span><span class="sxs-lookup"><span data-stu-id="748cb-115">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure Storage, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="748cb-116">La galerie de Runbooks inclut :</span><span class="sxs-lookup"><span data-stu-id="748cb-116">Gallery runbooks include:</span></span>

* [<span data-ttu-id="748cb-117">Supprimer des objets blob de stockage Azure avec une certaine ancienneté à l’aide du service Automation</span><span class="sxs-lookup"><span data-stu-id="748cb-117">Remove Azure Storage Blobs that are Certain Days Old Using Automation Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Remove-Storage-Blobs-that-aae4b761)
* [<span data-ttu-id="748cb-118">Télécharger un objet blob à partir d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="748cb-118">Download a Blob from Azure Storage</span></span>](https://gallery.technet.microsoft.com/scriptcenter/a-Blob-from-Azure-Storage-6bc13745)
* [<span data-ttu-id="748cb-119">Sauvegarder tous les disques d’une machine virtuelle Azure unique ou toutes les machines virtuelles d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="748cb-119">Backup all disks for a single Azure VM or for all VMs in a Cloud Service</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Backup-all-disks-for-a-ede940d5)

## <a name="next-steps"></a><span data-ttu-id="748cb-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="748cb-120">Next Steps</span></span>
<span data-ttu-id="748cb-121">Maintenant que vous avez appris les bases d'Azure Automation et la manière de l'utiliser pour gérer les objets blobs, les tables et les files d'attente Azure Storage, cliquez sur ces liens pour en savoir plus sur Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="748cb-121">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure Storage blobs, tables, and queues, follow these links to learn more about Azure Automation.</span></span>

<span data-ttu-id="748cb-122">Consultez le didacticiel Azure Automation [Création ou importation d’un runbook dans Azure Automation](../automation/automation-creating-importing-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="748cb-122">See the Azure Automation tutorial [Creating or importing a runbook in Azure Automation](../automation/automation-creating-importing-runbook.md).</span></span>

