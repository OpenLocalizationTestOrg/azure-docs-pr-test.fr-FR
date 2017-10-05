---
title: "Créer un plan dans Azure Stack | Microsoft Docs"
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
ms.openlocfilehash: ff34bcd6ba485806baf7963e11393633dd893fa7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="984ee-103">Créer un plan dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="984ee-103">Create a plan in Azure Stack</span></span>
<span data-ttu-id="984ee-104">Les [plans](azure-stack-key-features.md) regroupent un ou plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="984ee-104">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="984ee-105">En tant que fournisseur, vous pouvez créer des plans à proposer à vos locataires.</span><span class="sxs-lookup"><span data-stu-id="984ee-105">As a provider, you can create plans to offer to your tenants.</span></span> <span data-ttu-id="984ee-106">En retour, les clients s’abonnent à vos offres pour utiliser les plans et les services inclus.</span><span class="sxs-lookup"><span data-stu-id="984ee-106">In turn, your tenants subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="984ee-107">Cet exemple montre comment créer un plan comprenant les fournisseurs de ressources de stockage, réseau et de calcul.</span><span class="sxs-lookup"><span data-stu-id="984ee-107">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span></span> <span data-ttu-id="984ee-108">Ce plan donne aux abonnés la possibilité d’approvisionner des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="984ee-108">This plan gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="984ee-109">Connectez-vous au portail d’administration Azure Stack (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="984ee-109">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span> <span data-ttu-id="984ee-110">Entrez les informations d’identification du compte que vous avez créé à l’étape 5 de la section [Exécuter le script PowerShell](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="984ee-110">Enter the credentials for the account that you created during step 5 of the [Run the PowerShell script](azure-stack-run-powershell-script.md) section.</span></span>

2. <span data-ttu-id="984ee-111">Pour créer un plan et une offre auxquels les clients peuvent s’abonner, cliquez sur **Nouveau** > **Plans + offres clients** > **Plan**.</span><span class="sxs-lookup"><span data-stu-id="984ee-111">To create a plan and offer that tenants can subscribe to, click **New** > **Tenant Offers + Plans** > **Plan**.</span></span>

   ![](media/azure-stack-create-plan/image01.png)
3. <span data-ttu-id="984ee-112">Sur le panneau **Nouveau plan**, renseignez le **Nom d’affichage** et le **Nom de la ressource**.</span><span class="sxs-lookup"><span data-stu-id="984ee-112">In the **New Plan** blade, fill in **Display Name** and **Resource Name**.</span></span> <span data-ttu-id="984ee-113">Le nom d’affichage correspond au nom convivial du plan, que les clients voient.</span><span class="sxs-lookup"><span data-stu-id="984ee-113">The Display Name is the plan's friendly name that tenants see.</span></span> <span data-ttu-id="984ee-114">Seul l’administrateur peut voir le nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="984ee-114">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="984ee-115">Il s’agit du nom que les administrateurs utilisent pour gérer le plan en tant que ressource Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="984ee-115">It's the name that admins use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![](media/azure-stack-create-plan/image02.png)
4. <span data-ttu-id="984ee-116">Créez un **Groupe de ressources** ou sélectionnez-en un qui servira de conteneur pour le plan.</span><span class="sxs-lookup"><span data-stu-id="984ee-116">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span></span>

   ![](media/azure-stack-create-plan/image02a.png)
5. <span data-ttu-id="984ee-117">Cliquez sur **Services**, sélectionnez **Microsoft.Compute**, **Microsoft.Network** et **Microsoft.Storage**, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="984ee-117">Click **Services**, select **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**, and then click **Select**.</span></span>

   ![](media/azure-stack-create-plan/image03.png)
6. <span data-ttu-id="984ee-118">Cliquez sur **Quotas** et sur **Microsoft.Storage (local)**, puis sélectionnez le quota par défaut ou cliquez sur **Créer un quota** pour personnaliser le quota.</span><span class="sxs-lookup"><span data-stu-id="984ee-118">Click **Quotas**, click **Microsoft.Storage (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

   ![](media/azure-stack-create-plan/image04.png)
7. <span data-ttu-id="984ee-119">Si vous créez un quota, entrez un nom pour le quota > définissez ses valeurs > cliquez sur **OK** > cliquez sur le nom du nouveau quota.</span><span class="sxs-lookup"><span data-stu-id="984ee-119">If you're creating a new quota, enter a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

   ![](media/azure-stack-create-plan/image06.png)
8. <span data-ttu-id="984ee-120">Cliquez sur **Microsoft.Network (local)**, puis sélectionnez le quota par défaut ou cliquez sur **Créer un quota** pour le personnaliser.</span><span class="sxs-lookup"><span data-stu-id="984ee-120">Click **Microsoft.Network (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image07.png)
9. <span data-ttu-id="984ee-121">Si vous créez un quota, tapez un nom pour le quota > définissez ses valeurs > cliquez sur **OK** > cliquez sur le nom du nouveau quota.</span><span class="sxs-lookup"><span data-stu-id="984ee-121">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image08.png)
10. <span data-ttu-id="984ee-122">Cliquez sur **Microsoft.Compute (local)**, puis sélectionnez le quota par défaut ou cliquez sur **Créer un quota** pour le personnaliser.</span><span class="sxs-lookup"><span data-stu-id="984ee-122">Click **Microsoft.Compute (local)**, and then either select the default quota or click **Create new quota** to customize the quota.</span></span>

    ![](media/azure-stack-create-plan/image09.png)
11. <span data-ttu-id="984ee-123">Si vous créez un quota, tapez un nom pour le quota > définissez ses valeurs > cliquez sur **OK** > cliquez sur le nom du nouveau quota.</span><span class="sxs-lookup"><span data-stu-id="984ee-123">If you're creating a new quota, type a name for the quota > set the quota values > click **OK** > click the name of the new quota.</span></span>

    ![](media/azure-stack-create-plan/image10.png)
12. <span data-ttu-id="984ee-124">Sur le panneau **Quotas**, cliquez sur **OK**, puis, sur le panneau **Nouveau plan**, cliquez sur **Créer** pour créer le plan.</span><span class="sxs-lookup"><span data-stu-id="984ee-124">In the **Quotas** blade, click **OK**, and then in the **New Plan** blade, click **Create** to create the plan.</span></span>

    ![](media/azure-stack-create-plan/image11.png)
13. <span data-ttu-id="984ee-125">Pour voir votre nouveau plan, cliquez sur **Toutes les ressources**, puis recherchez-le et cliquez sur son nom.</span><span class="sxs-lookup"><span data-stu-id="984ee-125">To see your new plan, click **All resources**, then search for the plan and click its name.</span></span>

    ![](media/azure-stack-create-plan/image12.png)

### <a name="next-steps"></a><span data-ttu-id="984ee-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="984ee-126">Next steps</span></span>
[<span data-ttu-id="984ee-127">Créer une offre</span><span class="sxs-lookup"><span data-stu-id="984ee-127">Create an offer</span></span>](azure-stack-create-offer.md)
