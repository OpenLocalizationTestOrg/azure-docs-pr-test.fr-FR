---
title: "à l’aide de Caches de Redis aaaManaging hello Explorateur Azure pour Eclipse | Documents Microsoft"
description: "Découvrez comment toomanage votre redis Azure met en cache à l’aide de hello Explorateur Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/14/2017
ms.author: robmcm
ms.openlocfilehash: aa0c38862bda7919a3fc6c53c2fdaf555dd64bff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-redis-caches-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="5ae06-103">Gestion des Caches Redis à l’aide de hello Explorateur Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="5ae06-103">Managing Redis Caches using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="5ae06-104">Hello Explorateur Azure, qui fait partie de hello boîte à outils Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour la gestion de redis caches leur compte Azure, à l’intérieur de hello IDE Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5ae06-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing redis caches in their Azure account from inside hello Eclipse IDE.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-redis-cache-by-using-eclipse"></a><span data-ttu-id="5ae06-105">Créer un cache Redis à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="5ae06-105">Create a Redis Cache by using Eclipse</span></span>

<span data-ttu-id="5ae06-106">Hello suit vous guide tout hello étapes toocreate un cache redis à l’aide de hello Explorateur Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae06-106">hello following steps walk you through hello steps toocreate a redis cache using hello Azure Explorer.</span></span>

1. <span data-ttu-id="5ae06-107">Se connecter tooyour compte Azure à l’aide des étapes de hello Bonjour [signe dans des Instructions pour hello boîte à outils Azure pour Eclipse] l’article.</span><span class="sxs-lookup"><span data-stu-id="5ae06-107">Sign in tooyour Azure account using hello steps in hello [Sign In Instructions for hello Azure Toolkit for Eclipse] article.</span></span>

1. <span data-ttu-id="5ae06-108">Bonjour **Explorateur Azure** fenêtre de l’outil, développez hello **Azure** nœud, avec le bouton droit **les Caches Redis**, puis cliquez sur **créer un Cache Redis**.</span><span class="sxs-lookup"><span data-stu-id="5ae06-108">In hello **Azure Explorer** tool window, expand hello **Azure** node, right-click **Redis Caches**, and then click **Create Redis Cache**.</span></span>

   ![Créer un Menu pour le Cache Redis][CR01]

1. <span data-ttu-id="5ae06-110">Hello lorsque **nouveau Cache Redis** boîte de dialogue s’affiche, spécifiez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="5ae06-110">When hello **New Redis Cache** dialog box appears, specify hello following options:</span></span>

   ![Créer une nouvelle boîte de dialogue pour le Cache Redis][CR02]

   <span data-ttu-id="5ae06-112">a.</span><span class="sxs-lookup"><span data-stu-id="5ae06-112">a.</span></span> <span data-ttu-id="5ae06-113">**Nom DNS**: Spécifie le sous-domaine DNS hello cache redis nouveau hello, qui est ajouté en préfixe trop «. redis.cache.windows .net », par exemple : *wingtiptoys.redis.cache.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="5ae06-113">**DNS Name**: Specifies hello DNS subdomain for hello new redis cache, which is prepended too".redis.cache.windows.net"; for example: *wingtiptoys.redis.cache.windows.net*.</span></span>

   <span data-ttu-id="5ae06-114">b.</span><span class="sxs-lookup"><span data-stu-id="5ae06-114">b.</span></span> <span data-ttu-id="5ae06-115">**Abonnement**: Spécifie hello abonnement Azure toouse souhaité pour le cache redis nouveau hello.</span><span class="sxs-lookup"><span data-stu-id="5ae06-115">**Subscription**: Specifies hello Azure subscription you want toouse for hello new redis cache.</span></span>

   <span data-ttu-id="5ae06-116">c.</span><span class="sxs-lookup"><span data-stu-id="5ae06-116">c.</span></span> <span data-ttu-id="5ae06-117">**Groupe de ressources**: Spécifie le groupe de ressources hello pour votre cache redis ; vous devez toochoose une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="5ae06-117">**Resource Group**: Specifies hello resource group for your redis cache; you need toochoose one of hello following options:</span></span>
      * <span data-ttu-id="5ae06-118">**Créer nouveau**: Spécifie que vous souhaitez toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5ae06-118">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="5ae06-119">**Utiliser existant** : spécifie que vous allez choisir à partir d’une liste de groupes de ressources associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae06-119">**Use Existing**: Specifies that you will choose from a list of resource groups associated with your Azure account.</span></span>

   <span data-ttu-id="5ae06-120">d.</span><span class="sxs-lookup"><span data-stu-id="5ae06-120">d.</span></span> <span data-ttu-id="5ae06-121">**Emplacement**: Spécifie l’emplacement de hello où votre cache redis est créé ; par exemple, *ouest des États-Unis*.</span><span class="sxs-lookup"><span data-stu-id="5ae06-121">**Location**: Specifies hello location where your redis cache is created; for example, *West US*.</span></span>

   <span data-ttu-id="5ae06-122">e.</span><span class="sxs-lookup"><span data-stu-id="5ae06-122">e.</span></span> <span data-ttu-id="5ae06-123">**Niveau de tarification**: Spécifie le niveau tarifaire votre cache redis utilise ; ce paramètre détermine le nombre de hello de connexions clientes.</span><span class="sxs-lookup"><span data-stu-id="5ae06-123">**Pricing Tier**: Specifies which pricing tier your redis cache uses; this setting determines hello number of client connections.</span></span> <span data-ttu-id="5ae06-124">(Pour plus d’informations, consultez [Tarification du Cache Redis].)</span><span class="sxs-lookup"><span data-stu-id="5ae06-124">(For more information, see [Redis Cache Pricing].)</span></span>

   <span data-ttu-id="5ae06-125">f.</span><span class="sxs-lookup"><span data-stu-id="5ae06-125">f.</span></span> <span data-ttu-id="5ae06-126">**Port non-SSL** : spécifie si le cache Redis autorise les connexions non-SSL ; par défaut, seules les connexions SSL sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="5ae06-126">**Non-SSL port**: Specifies whether your redis cache allows non-SSL connections; by default, only SSL connections are allowed.</span></span>

1. <span data-ttu-id="5ae06-127">Une fois que vous avez spécifié tous les paramètres du cache Redis, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ae06-127">When you have specified all your redis cache settings, click **OK**.</span></span>

<span data-ttu-id="5ae06-128">Une fois que votre cache redis a été créé, il s’affichera dans hello Explorateur Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae06-128">After your redis cache has been created, it will be displayed in hello Azure Explorer.</span></span>

   ![Cache Redis dans l’Explorateur Azure][CR03]

> [!NOTE]
>
> <span data-ttu-id="5ae06-130">Pour plus d’informations sur la configuration de votre Azure des paramètres de cache redis, consultez [comment tooconfigure le Cache Redis Azure].</span><span class="sxs-lookup"><span data-stu-id="5ae06-130">For more information about configuring your Azure redis cache settings, see [How tooconfigure Azure Redis Cache].</span></span>
>

## <a name="display-hello-properties-for-your-redis-cache-in-eclipse"></a><span data-ttu-id="5ae06-131">Afficher les propriétés de hello pour votre Cache Redis dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="5ae06-131">Display hello properties for your Redis Cache in Eclipse</span></span>

1. <span data-ttu-id="5ae06-132">Hello Explorateur Azure, avec le bouton droit de votre cache redis et cliquez sur **afficher les propriétés**.</span><span class="sxs-lookup"><span data-stu-id="5ae06-132">In hello Azure Explorer, right-click your redis cache and click **Show properties**.</span></span>

   ![Azure Explorer toodisplay propriétés du menu contextuel pour un cache redis][SP01]

1. <span data-ttu-id="5ae06-134">Hello Explorateur Azure affiche les propriétés de hello pour votre cache redis.</span><span class="sxs-lookup"><span data-stu-id="5ae06-134">hello Azure Explorer displays hello properties for your redis cache.</span></span>

   ![Propriétés du cache Redis][SP02]

## <a name="delete-your-redis-cache-by-using-eclipse"></a><span data-ttu-id="5ae06-136">Supprimer votre cache Redis à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="5ae06-136">Delete your Redis Cache by using Eclipse</span></span>

1. <span data-ttu-id="5ae06-137">Hello Explorateur Azure, avec le bouton droit de votre cache redis et cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="5ae06-137">In hello Azure Explorer, right-click your redis cache and click **Delete**.</span></span>

   ![Azure toodelete menu de contexte Explorer un cache redis][DE01]

1. <span data-ttu-id="5ae06-139">Cliquez sur **OK** lorsque vous y êtes invité toodelete votre cache redis.</span><span class="sxs-lookup"><span data-stu-id="5ae06-139">Click **OK** when prompted toodelete your redis cache.</span></span>

   ![Invite de suppression d’un cache Redis][DE02]

## <a name="next-steps"></a><span data-ttu-id="5ae06-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5ae06-141">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="5ae06-142">Pour plus d’informations sur les caches redis Azure, les paramètres de configuration et la tarification, consultez hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="5ae06-142">For more information about Azure redis caches, configuration settings and pricing, see hello following links:</span></span>

* <span data-ttu-id="5ae06-143">[Cache Redis Azure]</span><span class="sxs-lookup"><span data-stu-id="5ae06-143">[Azure Redis Cache]</span></span>
* <span data-ttu-id="5ae06-144">[Documentation du Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="5ae06-144">[Redis Cache Documentation]</span></span>
* <span data-ttu-id="5ae06-145">[Tarification du Cache Redis]</span><span class="sxs-lookup"><span data-stu-id="5ae06-145">[Redis Cache Pricing]</span></span>
* <span data-ttu-id="5ae06-146">[comment tooconfigure le Cache Redis Azure]</span><span class="sxs-lookup"><span data-stu-id="5ae06-146">[How tooconfigure Azure Redis Cache]</span></span>

<!-- URL List -->

[Tarification du Cache Redis]: https://azure.microsoft.com/pricing/details/cache/
[Cache Redis Azure]: https://azure.microsoft.com/services/cache/
[Documentation du Cache Redis]: ./redis-cache/index.md
[comment tooconfigure le Cache Redis Azure]: ./redis-cache/cache-configure.md
[signe dans des Instructions pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md

<!-- IMG List -->

[CR01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/CR03.png

[SP01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP01.png
[SP02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/SP02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-redis-caches-using-azure-explorer/DE02.png
