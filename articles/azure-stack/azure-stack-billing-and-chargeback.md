---
title: "aaaCustomer de facturation et de rétrofacturation dans Azure pile | Documents Microsoft"
description: "Découvrez comment tooretrieve l’utilisation des informations sur les ressources Azure pile."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: a9afc7b6-43da-437b-a853-aab73ff14113
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2016
ms.author: alfredop
ms.openlocfilehash: d92caac2874e5364870b29a38515b579ab059991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-and-billing-in-azure-stack"></a><span data-ttu-id="ebac0-103">Utilisation et facturation dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ebac0-103">Usage and billing in Azure Stack</span></span>

<span data-ttu-id="ebac0-104">L’utilisation de représente la quantité hello des ressources consommées par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ebac0-104">Usage represents hello quantity of resources consumed by a user.</span></span> <span data-ttu-id="ebac0-105">Pile Azure recueille des informations d’utilisation pour chaque utilisateur et les utilise toobill les.</span><span class="sxs-lookup"><span data-stu-id="ebac0-105">Azure Stack collects usage information for each user and uses it toobill them.</span></span> <span data-ttu-id="ebac0-106">Cet article décrit la façon dont les utilisateurs de la pile de Azure sont facturées pour l’utilisation des ressources, et l’accès à des informations de facturation hello pour analytique, rétrofacturation, etc..</span><span class="sxs-lookup"><span data-stu-id="ebac0-106">This article describes how Azure Stack users are billed for resource usage, and how hello billing information is accessed for analytics, chargeback, etc.</span></span>

<span data-ttu-id="ebac0-107">Pile Azure contient hello infrastructure toocollect et les données d’utilisation d’agrégation de toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="ebac0-107">Azure Stack contains hello infrastructure toocollect and aggregate usage data for all resources.</span></span> <span data-ttu-id="ebac0-108">Vous pouvez accéder à ces données et système de facturation tooa l’exporter à l’aide d’un adaptateur de facturation ou exportez-le tooa un outil décisionnel comme Microsoft Power BI.</span><span class="sxs-lookup"><span data-stu-id="ebac0-108">You can access this data and export it tooa billing system by using a billing adapter, or export it tooa business intelligence tool like Microsoft Power BI.</span></span> <span data-ttu-id="ebac0-109">Après l’exportation, ces informations de facturation sont utilisées pour l’analytique ou transférés tooa rétrofacturation système.</span><span class="sxs-lookup"><span data-stu-id="ebac0-109">After exporting, this billing information is used for analytics or transferred tooa chargeback system.</span></span>

![Modèle conceptuel d’un adaptateur de facturation connexion Azure pile tooa application de facturation](media/azure-stack-billing-and-chargeback/image1.png)

## <a name="what-usage-information-can-i-find-and-how"></a><span data-ttu-id="ebac0-111">Quelles informations d’utilisation puis-je trouver et comment ?</span><span class="sxs-lookup"><span data-stu-id="ebac0-111">What usage information can I find, and how?</span></span>

<span data-ttu-id="ebac0-112">Les fournisseurs de ressources Azure Stack, comme Calcul, Stockage et Réseau, génèrent des données d’utilisation toutes les heures pour chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="ebac0-112">Azure Stack Resource providers, such as Compute, Storage, and Network, generate usage data at hourly intervals for each subscription.</span></span> <span data-ttu-id="ebac0-113">les données d’utilisation Hello contient plus d’informations sur la ressource hello utilisé comme nom de la ressource, de la quantité de nom, ID de la jauge, compteur utilisé toolearn etc. sur les ressources de code hello mètres, consultez toohello [API Forum aux questions sur l’utilisation de](azure-stack-usage-related-faq.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="ebac0-113">hello usage data contains information about hello resource used such as resource name, meter name, meter ID, quantity used etc. toolearn about hello meters ID resources, refer toohello [usage API FAQ](azure-stack-usage-related-faq.md) article.</span></span> 

<span data-ttu-id="ebac0-114">Une fois les données d’utilisation hello ont été collectées, il est [signalé tooAzure](azure-stack-usage-reporting.md) toogenerate une facture, ce qui peut être affichée via hello portail de facturation Azure.</span><span class="sxs-lookup"><span data-stu-id="ebac0-114">After hello usage data has been collected, it is [reported tooAzure](azure-stack-usage-reporting.md) toogenerate a bill, which can be viewed through hello Azure billing portal.</span></span> <span data-ttu-id="ebac0-115">Hello portail de facturation Azure les données d’utilisation de hello uniquement pour les ressources facturables hello.</span><span class="sxs-lookup"><span data-stu-id="ebac0-115">hello Azure billing portal shows hello usage data only for hello chargeable resources.</span></span> <span data-ttu-id="ebac0-116">En outre ressources facturables toohello, Azure pile capture les données d’utilisation pour un ensemble plus large de ressources, auquel vous pouvez accéder dans votre environnement Azure pile via l’API REST ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ebac0-116">In addition toohello chargeable resources, Azure Stack captures usage data for a broader set of resources, which you can access in your Azure Stack environment through REST APIs or PowerShell.</span></span> <span data-ttu-id="ebac0-117">Azure pile cloud les administrateurs peuvent récupérer les données d’utilisation hello pour tous les abonnements de l’utilisateur qu’un utilisateur peut obtenir uniquement les détails d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="ebac0-117">Azure Stack cloud administrators can retrieve hello usage data for all user subscriptions whereas a user can get only their usage details.</span></span>

## <a name="retrieve-usage-information"></a><span data-ttu-id="ebac0-118">Récupérer les informations sur l’utilisation</span><span class="sxs-lookup"><span data-stu-id="ebac0-118">Retrieve usage information</span></span>

<span data-ttu-id="ebac0-119">données d’utilisation toogenerate hello, vous devez disposer de ressources qui sont en cours d’exécution et activement à l’aide de système de hello.</span><span class="sxs-lookup"><span data-stu-id="ebac0-119">toogenerate hello usage data, you should have resources that are running and actively using hello system.</span></span> <span data-ttu-id="ebac0-120">Si vous ne savez pas si vous avez toutes les ressources en cours d’exécution dans Azure Marketplace de pile, déployez un ordinateur virtuel (VM) et de Vérifiez hello VM analyse toomake panneau que qu’il est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ebac0-120">If you’re not sure whether you have any resources running in Azure Stack Marketplace, deploy a virtual machine (VM), and verify hello VM monitoring blade toomake sure it’s running.</span></span> <span data-ttu-id="ebac0-121">Utilisez hello PowerShell applets de commande tooview hello l’utilisation des données suivantes :</span><span class="sxs-lookup"><span data-stu-id="ebac0-121">Use hello following PowerShell cmdlets tooview hello usage data:</span></span>

1. [<span data-ttu-id="ebac0-122">Installer PowerShell pour Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="ebac0-122">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)
2. * <span data-ttu-id="ebac0-123">[Configurer l’utilisateur hello Azure pile](azure-stack-powershell-configure-user.md) ou hello [l’opérateur Azure pile](azure-stack-powershell-configure-admin.md) environnement PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebac0-123">[Configure hello Azure Stack user's](azure-stack-powershell-configure-user.md) or hello [Azure Stack operator's](azure-stack-powershell-configure-admin.md) PowerShell environment</span></span> 
3. <span data-ttu-id="ebac0-124">données d’utilisation tooretrieve hello, utilisez hello [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) applet de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="ebac0-124">tooretrieve hello usage data, use hello [Get-UsageAggregates](/powershell/module/azurerm.usageaggregates/get-usageaggregates) PowerShell cmdlet:</span></span>
   ```PowerShell
   Get-UsageAggregates -ReportedStartTime "<Start time for usage reporting>" -ReportedEndTime "<end time for usage reporting>" -AggregationGranularity <Hourly or Daily>
   ```

   <span data-ttu-id="ebac0-125">Si les données d’utilisation ne seront disponibles, elle est retournée dans comme indiqué dans hello suivant capture d’écran :</span><span class="sxs-lookup"><span data-stu-id="ebac0-125">If usage data is available, it’s returned in as shown in hello following screenshot:</span></span> 
   
   ![Agrégats d’utilisation](media/azure-stack-billing-and-chargeback/image2.png)
   
   <span data-ttu-id="ebac0-127">PowerShell retourne 1 000 lignes d’utilisation par appel.</span><span class="sxs-lookup"><span data-stu-id="ebac0-127">PowerShell returns 1,000 lines of usage per call.</span></span> <span data-ttu-id="ebac0-128">Vous pouvez utiliser hello continuation paramètre tooretrieve plus de 1 000 lignes</span><span class="sxs-lookup"><span data-stu-id="ebac0-128">You can use hello continuation parameter tooretrieve more than 1,000 lines</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebac0-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebac0-129">Next steps</span></span>

[<span data-ttu-id="ebac0-130">TooAzure de pile Azure l’utilisation des données de rapport</span><span class="sxs-lookup"><span data-stu-id="ebac0-130">Report Azure Stack usage data tooAzure</span></span>](azure-stack-usage-reporting.md)

[<span data-ttu-id="ebac0-131">API Utilisation des ressources de fournisseur</span><span class="sxs-lookup"><span data-stu-id="ebac0-131">Provider Resource Usage API</span></span>](azure-stack-provider-resource-api.md)

[<span data-ttu-id="ebac0-132">API Utilisation des ressources de client</span><span class="sxs-lookup"><span data-stu-id="ebac0-132">Tenant Resource Usage API</span></span>](azure-stack-tenant-resource-usage-api.md)

[<span data-ttu-id="ebac0-133">Questions fréquentes (FAQ) relatives à l’utilisation</span><span class="sxs-lookup"><span data-stu-id="ebac0-133">Usage-related FAQ</span></span>](azure-stack-usage-related-faq.md)

