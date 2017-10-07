---
title: "aaaAzure limites de Quota de données Lake Analytique | Documents Microsoft"
description: "Découvrez comment tooadjust et l’augmentation de quota limite dans les comptes Azure données Lake Analytique (ADLA)."
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
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a><span data-ttu-id="8d6fa-104">Limites de quota pour Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8d6fa-104">Azure Data Lake Analytics Quota Limits</span></span>

<span data-ttu-id="8d6fa-105">Découvrez comment tooadjust et l’augmentation de quota limite dans les comptes Azure données Lake Analytique (ADLA).</span><span class="sxs-lookup"><span data-stu-id="8d6fa-105">Learn how tooadjust and increase quota limits in Azure Data Lake Analytics (ADLA) accounts.</span></span> <span data-ttu-id="8d6fa-106">Il vous sera plus simple d’appréhender le comportement de vos tâches U-SQL si vous connaissez ces limites.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-106">Knowing these limits may help you understand your U-SQL job behavior.</span></span> <span data-ttu-id="8d6fa-107">Toutes les limites de quota sont paramétrés, vous pouvez augmenter les limites maximales hello par approcher toous.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-107">All quota limits are soft, so you can increase hello maximum limits by reaching out toous.</span></span>

## <a name="azure-subscriptions-limits"></a><span data-ttu-id="8d6fa-108">Limites des abonnements Azure</span><span class="sxs-lookup"><span data-stu-id="8d6fa-108">Azure subscriptions limits</span></span>

<span data-ttu-id="8d6fa-109">**Nombre maximal de comptes ADLA par abonnement :** 5.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-109">**Maximum number of ADLA accounts per subscription:**  5</span></span>

 <span data-ttu-id="8d6fa-110">Ceci est hello le nombre maximal de comptes ADLA que vous pouvez créer par abonnement.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-110">This is hello maximum number of ADLA accounts you can create per subscription.</span></span> <span data-ttu-id="8d6fa-111">Si vous essayez de compte ADLA toocreate un sixième, vous obtiendrez une erreur « Vous avez atteint nombre maximal de hello des comptes Analytique lac de données autorisés (5) dans la zone sous le nom de l’abonnement ».</span><span class="sxs-lookup"><span data-stu-id="8d6fa-111">If you try toocreate a sixth ADLA account, you will get an error "You have reached hello maximum number of Data Lake Analytics accounts allowed (5) in region under subscription name".</span></span> <span data-ttu-id="8d6fa-112">Dans ce cas, supprimez tous les comptes ADLA inutilisés ou atteindre toous par [ouvrant un ticket de support](#increase-maximum-quota-limits).</span><span class="sxs-lookup"><span data-stu-id="8d6fa-112">In this case, either delete any unused ADLA accounts, or reach out toous by [opening a support ticket](#increase-maximum-quota-limits).</span></span>

## <a name="adla-account-limits"></a><span data-ttu-id="8d6fa-113">Limites des comptes ADLA</span><span class="sxs-lookup"><span data-stu-id="8d6fa-113">ADLA account limits</span></span>

<span data-ttu-id="8d6fa-114">**Nombre maximal d’unités Analytics par compte :**  250</span><span class="sxs-lookup"><span data-stu-id="8d6fa-114">**Maximum number of Analytics Units (AUs) per account:** 250</span></span>

<span data-ttu-id="8d6fa-115">Il s’agit de nombre maximal de hello de AUs pouvant s’exécuter simultanément dans votre compte.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-115">This is hello maximum number of AUs that can run concurrently in your account.</span></span> <span data-ttu-id="8d6fa-116">Si le nombre total d’unités Analytics exécutées dans l’ensemble des tâches dépasse cette limite, les tâches les plus récentes sont automatiquement placées dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-116">If your total running AUs across all jobs exceeds this limit, newer jobs are queued automatically.</span></span> <span data-ttu-id="8d6fa-117">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="8d6fa-117">For example:</span></span>

* <span data-ttu-id="8d6fa-118">Si vous avez un seul travail en cours d’exécution avec 250 AUs, lorsque vous soumettez une seconde tâche attend dans la file d’attente des travaux hello hello première tâche se termine.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-118">If you have only one job running with 250 AUs, when you submit a second job it will wait in hello job queue until hello first job completes.</span></span>
* <span data-ttu-id="8d6fa-119">Si vous avez déjà cinq tâches en cours d’exécution et que chacune utilise 50 AUs, lorsque vous soumettez une tâche sixième dont a besoin de 20 AUs qu’elle attend dans la file d’attente des travaux hello sont 20 AUs disponibles.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-119">If you already have five jobs running and each is using 50 AUs, when you submit a sixth job that needs 20 AUs it waits in hello job queue until there are 20 AUs available.</span></span>

<span data-ttu-id="8d6fa-120">**Nombre maximal de tâches U-SQL simultanées par compte :** 20</span><span class="sxs-lookup"><span data-stu-id="8d6fa-120">**Maximum number of concurrent U-SQL jobs per account:** 20</span></span>

<span data-ttu-id="8d6fa-121">Ceci est hello le nombre maximal de tâches pouvant s’exécuter simultanément dans votre compte.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-121">This is hello maximum number of jobs that can run concurrently in your account.</span></span> <span data-ttu-id="8d6fa-122">Au-dessus de cette valeur, les tâches les plus récentes sont automatiquement placées dans la file d’attente.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-122">Above this value, newer jobs are queued automatically.</span></span>

## <a name="adjust-adla-quota-limits-per-account"></a><span data-ttu-id="8d6fa-123">Ajuster les limites de quota ADLA par compte</span><span class="sxs-lookup"><span data-stu-id="8d6fa-123">Adjust ADLA quota limits per account</span></span>

1. <span data-ttu-id="8d6fa-124">Ouverture de session toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8d6fa-124">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8d6fa-125">Choisissez un compte ADLA existant.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-125">Choose an existing ADLA account.</span></span>
3. <span data-ttu-id="8d6fa-126">Cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-126">Click **Properties**.</span></span>
4. <span data-ttu-id="8d6fa-127">Ajuster **parallélisme** et **travaux simultanés** toosuit vos besoins.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-127">Adjust **Parallelism** and **Concurrent Jobs** toosuit your needs.</span></span>

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a><span data-ttu-id="8d6fa-129">Augmenter les limites de quota maximales</span><span class="sxs-lookup"><span data-stu-id="8d6fa-129">Increase maximum quota limits</span></span>

1. <span data-ttu-id="8d6fa-130">Ouvrez une demande de support dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-130">Open a support request in Azure Portal.</span></span>

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. <span data-ttu-id="8d6fa-133">Sélectionnez le type de problème hello **Quota**.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-133">Select hello issue type **Quota**.</span></span>
3. <span data-ttu-id="8d6fa-134">Sélectionnez votre **Abonnement** (vérifiez qu’il ne s’agit pas d’une version d’essai).</span><span class="sxs-lookup"><span data-stu-id="8d6fa-134">Select your **Subscription** (make sure it is not a "trial" subscription).</span></span>
4. <span data-ttu-id="8d6fa-135">Sélectionnez le type de quota **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-135">Select quota type **Data Lake Analytics**.</span></span>

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. <span data-ttu-id="8d6fa-137">Dans le panneau de problème hello, expliquez votre limite de l’augmentation demandée avec **détails** de pourquoi vous devez cette capacité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-137">In hello problem blade, explain your requested increase limit with **Details** of why you need this extra capacity.</span></span>

    ![Volet du portail Azure Data Lake Analytics](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. <span data-ttu-id="8d6fa-139">Vérifiez vos informations de contact et créer une demande de prise en charge hello.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-139">Verify your contact information and create hello support request.</span></span>

<span data-ttu-id="8d6fa-140">Microsoft vérifie votre demande et tente de tooaccommodate dès que possible les besoins de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="8d6fa-140">Microsoft reviews your request and tries tooaccommodate your business needs as soon as possible.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d6fa-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d6fa-141">Next steps</span></span>

* [<span data-ttu-id="8d6fa-142">Vue d'ensemble de Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="8d6fa-142">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="8d6fa-143">Gestion d'Azure Data Lake Analytics à l'aide d'Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d6fa-143">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="8d6fa-144">Surveiller et résoudre les problèmes des tâches Azure Data Lake Analytics à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="8d6fa-144">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
