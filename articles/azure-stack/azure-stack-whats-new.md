---
title: aaaWhat de nouveau dans la pile de Azure | Documents Microsoft
description: "Nouveautés de la pile de Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 872b0651-0a92-4d28-b2e6-07d0a4a9a25a
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/13/2017
ms.author: helaw
ms.openlocfilehash: 32b4bd7deebb12a92e4abbdaacdbcebaa5125e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-stack"></a><span data-ttu-id="965f7-103">Nouveautés de la pile de Azure</span><span class="sxs-lookup"><span data-stu-id="965f7-103">What's new in Azure Stack</span></span>
<span data-ttu-id="965f7-104">Cette version fournit de nouvelles fonctionnalités pour les clients et les administrateurs.</span><span class="sxs-lookup"><span data-stu-id="965f7-104">This release provides new features for both tenants and administrators.</span></span>

## <a name="content-services-and-tools"></a><span data-ttu-id="965f7-105">Le contenu, les services et outils</span><span class="sxs-lookup"><span data-stu-id="965f7-105">Content, services, and tools</span></span>
* <span data-ttu-id="965f7-106">[Services de fédération Active Directory (AD FS)](azure-stack-key-features.md#identity) prise en charge fournit des options d’identité pour les scénarios où la connectivité réseau est limitée ou intermittentes.</span><span class="sxs-lookup"><span data-stu-id="965f7-106">[Active Directory Federation Services (AD FS)](azure-stack-key-features.md#identity) support provides identity options for scenarios where network connectivity is limited or intermittent.</span></span>
* <span data-ttu-id="965f7-107">Vous pouvez utiliser avec montée en charge Azure machines virtuelles identiques tooprovide géré et l’échelle dans des charges de travail basé sur une machine virtuelle IaaS.</span><span class="sxs-lookup"><span data-stu-id="965f7-107">You can use Azure Virtual Machine Scale Sets tooprovide managed scale-out and scale-in of IaaS VM-based workloads.</span></span> 
* <span data-ttu-id="965f7-108">Utiliser les tailles de machine virtuelle de série D Azure pour des raisons de performances accrues.</span><span class="sxs-lookup"><span data-stu-id="965f7-108">Use Azure D-Series VM sizes for increased performance and consistency.</span></span>
* <span data-ttu-id="965f7-109">Déployer et créer des modèles dont les disques Temp sont compatibles avec Azure.</span><span class="sxs-lookup"><span data-stu-id="965f7-109">Deploy and create templates with Temp Disks that are consistent with Azure.</span></span>
* <span data-ttu-id="965f7-110">[Marketplace Syndication](azure-stack-download-azure-marketplace-item.md) vous permet de contenu toouse hello Azure Marketplace et rendre disponibles dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="965f7-110">[Marketplace Syndication](azure-stack-download-azure-marketplace-item.md) allows you toouse content from hello Azure Marketplace and make available in Azure Stack.</span></span>

## <a name="infrastructure-and-operations"></a><span data-ttu-id="965f7-111">Infrastructure et les opérations</span><span class="sxs-lookup"><span data-stu-id="965f7-111">Infrastructure and operations</span></span>
* <span data-ttu-id="965f7-112">Isolé administrateur et utilisateur [portails](azure-stack-manage-portals.md) et API offrent une sécurité accrue.</span><span class="sxs-lookup"><span data-stu-id="965f7-112">Isolated administrator and user [portals](azure-stack-manage-portals.md) and APIs provide enhanced security.</span></span>
* <span data-ttu-id="965f7-113">Utilisez les fonctionnalités de gestion des améliorations de l’infrastructure, telles que la génération d’alertes améliorée.</span><span class="sxs-lookup"><span data-stu-id="965f7-113">Use enhanced infrastructure management functionality, such as improved alerting.</span></span>
* <span data-ttu-id="965f7-114">À l’aide de hello [Windows Azure Pack connecteur](azure-stack-manage-windows-azure-pack.md), vous pouvez afficher et gérer des machines virtuelles IaaS qui sont hébergés sur Windows Azure Pack.</span><span class="sxs-lookup"><span data-stu-id="965f7-114">Using hello [Windows Azure Pack Connector](azure-stack-manage-windows-azure-pack.md), you can view and manage IaaS virtual machines that are hosted on Windows Azure Pack.</span></span> <span data-ttu-id="965f7-115">Pour cette version préliminaire, essayez ce scénario uniquement dans les environnements de test (Windows Azure Pack et Azure pile).</span><span class="sxs-lookup"><span data-stu-id="965f7-115">For this preview release, try this scenario only in test environments (both Windows Azure Pack and Azure Stack).</span></span> <span data-ttu-id="965f7-116">Configuration supplémentaire est requise.</span><span class="sxs-lookup"><span data-stu-id="965f7-116">Additional configuration is required.</span></span>
* <span data-ttu-id="965f7-117">Azure prend en charge pile [une architecture mutualisée](azure-stack-enable-multitenancy.md) pour les scénarios où vous devez tooprovide IaaS et PaaS services toousers en dehors de votre domaine Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="965f7-117">Azure Stack now supports [multi-tenancy](azure-stack-enable-multitenancy.md) for scenarios where you need tooprovide IaaS and PaaS services toousers outside of your Azure Active Directory domain.</span></span>  <span data-ttu-id="965f7-118">Par exemple, vous souhaiterez peut-être tooprovide entreprise de partenaire Azure pile services tooa à l’aide de leurs identités.</span><span class="sxs-lookup"><span data-stu-id="965f7-118">For example, you may want tooprovide Azure Stack services tooa partner company using their identities.</span></span> <span data-ttu-id="965f7-119">Vous pouvez configurer des identités de l’autre organisation, hello tootrust de pile d’Azure et permettre aux utilisateurs de ce toosign d’organisation pour les abonnements et consommer des services.</span><span class="sxs-lookup"><span data-stu-id="965f7-119">You can configure Azure Stack tootrust hello other organization's identities, and enable users from that organization toosign up for subscriptions and consume services.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="965f7-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="965f7-120">Next steps</span></span>
* [<span data-ttu-id="965f7-121">Comprendre l’architecture de la preuve de concept de pile Azure</span><span class="sxs-lookup"><span data-stu-id="965f7-121">Understand Azure Stack POC architecture</span></span>](azure-stack-architecture.md)      
* [<span data-ttu-id="965f7-122">Comprendre les conditions préalables au déploiement</span><span class="sxs-lookup"><span data-stu-id="965f7-122">Understand deployment prerequisites</span></span>](azure-stack-deploy.md)
* [<span data-ttu-id="965f7-123">Déployer Azure Stack</span><span class="sxs-lookup"><span data-stu-id="965f7-123">Deploy Azure Stack</span></span>](azure-stack-run-powershell-script.md)

