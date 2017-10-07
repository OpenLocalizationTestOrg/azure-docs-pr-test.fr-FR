---
title: aaaCreate un plan dans la pile de Azure | Documents Microsoft
description: "En tant qu’administrateur cloud, créez un plan permettant aux abonnés d’approvisionner des machines virtuelles."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: erikje
ms.openlocfilehash: 3665bae5d212002da43316e62ce73686b4c66eea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="1bb5c-103">Créer un plan dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="1bb5c-103">Create a plan in Azure Stack</span></span>
<span data-ttu-id="1bb5c-104">Les [plans](azure-stack-key-features.md) regroupent un ou plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-104">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="1bb5c-105">En tant que fournisseur, vous pouvez créer des plans toooffer tooyour locataires.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-105">As a provider, you can create plans toooffer tooyour tenants.</span></span> <span data-ttu-id="1bb5c-106">À son tour, vos clients de s’abonner tooyour offres toouse hello plans et services qu’ils comprennent.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-106">In turn, your tenants subscribe tooyour offers toouse hello plans and services they include.</span></span> <span data-ttu-id="1bb5c-107">Cet exemple vous montre comment toocreate un plan qui inclut hello des fournisseurs de ressources de calcul, réseau et de stockage.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-107">This example shows you how toocreate a plan that includes hello compute, network, and storage resource providers.</span></span> <span data-ttu-id="1bb5c-108">Ce plan offre abonnés hello capacité tooprovision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-108">This plan gives subscribers hello ability tooprovision virtual machines.</span></span>

1. <span data-ttu-id="1bb5c-109">Se connecter toohello portail d’administration Azure pile (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="1bb5c-109">Sign in toohello Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="1bb5c-110">Entrez des informations d’identification de hello compte hello que vous avez créé à l’étape 5 de hello [exécuter le script PowerShell de hello](azure-stack-run-powershell-script.md) section.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-110">Enter hello credentials for hello account that you created during step 5 of hello [Run hello PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="1bb5c-111">toocreate un plan et offre que les clients peuvent s’abonner, cliquez sur **nouveau** > **client offre + Plans** > **Plan**.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-111">toocreate a plan and offer that tenants can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="1bb5c-112">Bonjour **nouveau Plan** panneau, renseignez **nom d’affichage** et **nom de la ressource**.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-112">In hello **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="1bb5c-113">Hello nom complet est le nom convivial du plan hello clients plus.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-113">hello Display Name is hello plan's friendly name that tenants see.</span></span> <span data-ttu-id="1bb5c-114">Seul l’administrateur hello peut voir hello nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-114">Only hello admin can see hello Resource Name.</span></span> <span data-ttu-id="1bb5c-115">Son nom hello qu’administrateurs utiliser toowork hello plan comme une ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-115">It's hello name that admins use toowork with hello plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="1bb5c-116">Créer un nouveau **groupe de ressources**, ou sélectionnez-en un existant, comme un conteneur pour un plan de hello.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-116">Create a new **Resource Group**, or select an existing one, as a container for hello plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="1bb5c-117">Cliquez sur **Services**, sélectionnez **Microsoft.Compute**, **Microsoft.Network** et **Microsoft.Storage**, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-117">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="1bb5c-118">Cliquez sur **Quotas**, cliquez sur **Microsoft.Storage (local)**et puis soit hello sélection par défaut de quota ou cliquez sur **créer nouveau quota** quota de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-118">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="1bb5c-119">Si vous créez un nouveau quota, entrez un nom pour le quota de hello > définir des valeurs de quota hello > cliquez sur **OK** > cliquez sur le nom hello du quota de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-119">If you're creating a new quota, enter a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="1bb5c-120">Cliquez sur **Microsoft.Network (local)**et puis soit hello sélection par défaut de quota ou cliquez sur **créer nouveau quota** quota de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-120">Click **Microsoft.Network (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="1bb5c-121">Si vous créez un nouveau quota, tapez un nom pour le quota de hello > définir des valeurs de quota hello > cliquez sur **OK** > cliquez sur le nom hello du quota de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-121">If you're creating a new quota, type a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="1bb5c-122">Cliquez sur **Microsoft.Compute (local)**et puis soit hello sélection par défaut de quota ou cliquez sur **créer nouveau quota** quota de hello toocustomize.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-122">Click **Microsoft.Compute (local)**, and then either select hello default quota or click **Create new quota** toocustomize hello quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="1bb5c-123">Si vous créez un nouveau quota, tapez un nom pour le quota de hello > définir des valeurs de quota hello > cliquez sur **OK** > cliquez sur le nom hello du quota de nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-123">If you're creating a new quota, type a name for hello quota > set hello quota values > click **OK** > click hello name of hello new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="1bb5c-124">Bonjour **Quotas** panneau, cliquez sur **OK**, puis dans hello **nouveau Plan** panneau, cliquez sur **créer** plan de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-124">In hello **Quotas** blade, click **OK**, and then in hello **New Plan** blade, click **Create** toocreate hello plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="1bb5c-125">toosee votre nouveau plan, cliquez sur **toutes les ressources**, puis recherchez le plan de hello et cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="1bb5c-125">toosee your new plan, click **All resources**, then search for hello plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="1bb5c-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1bb5c-126">Next steps</span></span>
[<span data-ttu-id="1bb5c-127">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="1bb5c-127">Create an offer</span></span>](azure-stack-create-offer.md)
