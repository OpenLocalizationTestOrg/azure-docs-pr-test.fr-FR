---
title: Limites de quota pour Azure Data Lake Analytics | Microsoft Docs
description: "Découvrez comment ajuster et augmenter les limites de quota dans un compte Azure Data Lake Analytics (ADLA)."
services: data-lake-analytics
keywords: Service Analytique Azure Data Lake
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 957f306ea0e80b5830ad64e5ef06c6d122d9eccc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="3f05b-104">Limites de quota pour Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3f05b-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="3f05b-105">Découvrez comment ajuster et augmenter les limites de quota dans un compte Azure Data Lake Analytics (ADLA).</span><span class="sxs-lookup"><span data-stu-id="3f05b-105">Learn how to adjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="3f05b-106">Il vous sera plus simple d’appréhender le comportement de vos tâches U-SQL si vous connaissez ces limites.</span><span class="sxs-lookup"><span data-stu-id="3f05b-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="3f05b-107">Toutes ces limites sont souples. Pour les augmenter, il vous suffit de nous contacter.</span><span class="sxs-lookup"><span data-stu-id="3f05b-107">All quota limits are soft, so you can increase the maximum limits by reaching out to us.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="3f05b-108">Limites des abonnements Azure</span><span class="sxs-lookup"><span data-stu-id="3f05b-108">Azure subscriptions limits</span></span>

<span data-ttu-id="3f05b-109">**Nombre maximal de comptes ADLA par abonnement :** 5.</span><span class="sxs-lookup"><span data-stu-id="3f05b-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="3f05b-110">Il s’agit du nombre maximal de comptes ADLA que vous pouvez créer par abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f05b-110">This is the maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="3f05b-111">Lorsque vous essayez de créer le sixième compte ADLA, le message d’erreur suivant s’affiche : « Vous avez atteint le nombre maximal de comptes Data Lake Analytics autorisés (5) dans (zone) sous l’abonnement (nom). »</span><span class="sxs-lookup"><span data-stu-id="3f05b-111">If you try to create a sixth ADLA account, you will get an error "You have reached the maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="3f05b-112">Dans ce cas, supprimez les comptes ADLA non utilisés ou contactez-nous en [ouvrant un ticket de support](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="3f05b-112">In this case, either delete any unused ADLA accounts, or reach out to us by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="3f05b-113">Limites des comptes ADLA</span><span class="sxs-lookup"><span data-stu-id="3f05b-113">ADLA account limits</span></span>

<span data-ttu-id="3f05b-114">**Nombre maximal d’unités Analytics par compte :**  250</span><span class="sxs-lookup"><span data-stu-id="3f05b-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="3f05b-115">Il s’agit du nombre maximal d’unités Analytics pouvant s’exécuter simultanément dans votre compte.</span><span class="sxs-lookup"><span data-stu-id="3f05b-115">This is the maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="3f05b-116">Si le nombre total d’unités Analytics exécutées dans l’ensemble des tâches dépasse cette limite, les tâches les plus récentes sont automatiquement placées dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="3f05b-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="3f05b-117">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3f05b-117">For example:</span></span>

* <span data-ttu-id="3f05b-118">Si une seule tâche est exécutée avec 250 unités Analytics, lorsque vous envoyez une deuxième tâche, celle-ci est placée dans la file d’attente jusqu’à ce que la première tâche soit terminée.</span><span class="sxs-lookup"><span data-stu-id="3f05b-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in the job queue until the first job completes.</span></span>
* <span data-ttu-id="3f05b-119">Si vous avez déjà cinq tâches en cours d’exécution et que chacune utilise 50 unités Analytics, lorsque vous envoyez une sixième tâche nécessitant 20 unités Analytics, celle-ci est placée dans la file d’attente jusqu’à ce que les 20 unités Analytics soient disponibles.</span><span class="sxs-lookup"><span data-stu-id="3f05b-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in the job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="3f05b-120">**Nombre maximal de tâches U-SQL simultanées par compte :** 20</span><span class="sxs-lookup"><span data-stu-id="3f05b-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="3f05b-121">Il s’agit du nombre maximal de tâches pouvant s’exécuter simultanément dans votre compte.</span><span class="sxs-lookup"><span data-stu-id="3f05b-121">This is the maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="3f05b-122">Au-dessus de cette valeur, les tâches les plus récentes sont automatiquement placées dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="3f05b-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="3f05b-123">Ajuster les limites de quota ADLA par compte</span><span class="sxs-lookup"><span data-stu-id="3f05b-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="3f05b-124">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f05b-124">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3f05b-125">Choisissez un compte ADLA existant.</span><span class="sxs-lookup"><span data-stu-id="3f05b-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="3f05b-126">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="3f05b-126">Click **Properties**.</span></span>
4. <span data-ttu-id="3f05b-127">Ajustez les valeurs **Parallélisme** et **Tâches simultanées** selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="3f05b-127">Adjust **Parallelism** and **Concurrent Jobs** to suit your needs.</span></span>

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="3f05b-129">Augmenter les limites de quota maximales</span><span class="sxs-lookup"><span data-stu-id="3f05b-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="3f05b-130">Ouvrez une demande de support dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3f05b-130">Open a support request in Azure Portal.</span></span>

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="3f05b-133">Sélectionnez **Quota** comme type de problème.</span><span class="sxs-lookup"><span data-stu-id="3f05b-133">Select the issue type **Quota**.</span></span>
3. <span data-ttu-id="3f05b-134">Sélectionnez votre **Abonnement** (vérifiez qu’il ne s’agit pas d’une version d’essai).</span><span class="sxs-lookup"><span data-stu-id="3f05b-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="3f05b-135">Sélectionnez le type de quota **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="3f05b-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="3f05b-137">Dans le panneau Problème, expliquez le motif de votre demande d’augmentation de limite. Indiquez pourquoi vous avez besoin de cette capacité supplémentaire dans la zone **Détails**.</span><span class="sxs-lookup"><span data-stu-id="3f05b-137">In the problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="3f05b-139">Vérifiez vos informations de contact et créez la demande de support.</span><span class="sxs-lookup"><span data-stu-id="3f05b-139">Verify your contact information and create the support request.</span></span>

<span data-ttu-id="3f05b-140">Microsoft examine votre demande et essaie de répondre aux besoins de votre activité dans les plus brefs délais.</span><span class="sxs-lookup"><span data-stu-id="3f05b-140">Microsoft reviews your request and tries to accommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f05b-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f05b-141">Next steps</span></span>

* [<span data-ttu-id="3f05b-142">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3f05b-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="3f05b-143">Gestion d'Azure Data Lake Analytics à l'aide d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f05b-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="3f05b-144">Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="3f05b-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
