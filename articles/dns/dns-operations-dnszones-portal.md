---
title: aaaManage DNS zones DNS de Azure - portail Azure | Documents Microsoft
description: "Vous pouvez gérer des zones DNS à l’aide de hello portail Azure. Cet article décrit comment tooupdate, supprimer et créer des zones DNS sur le système DNS Azure"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: gwallace
ms.openlocfilehash: 0d8ce302bb7126dfe8077a6f3e33418e16fcea64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-in-hello-azure-portal"></a><span data-ttu-id="84c91-104">Comment les Zones DNS toomanage hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="84c91-104">How toomanage DNS Zones in hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="84c91-105">Portail</span><span class="sxs-lookup"><span data-stu-id="84c91-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="84c91-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84c91-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="84c91-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="84c91-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="84c91-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="84c91-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="84c91-109">Cet article explique comment toomanage votre DNS zones à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="84c91-109">This article shows you how toomanage your DNS zones by using hello Azure portal.</span></span> <span data-ttu-id="84c91-110">Vous pouvez également gérer vos zones DNS à l’aide de hello inter-plateformes [CLI d’Azure](dns-operations-dnszones-cli.md) ou hello Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="84c91-110">You can also manage your DNS zones using hello cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or hello Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="84c91-111">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="84c91-111">Create a DNS zone</span></span>

1. <span data-ttu-id="84c91-112">Se connecter toohello portail Azure</span><span class="sxs-lookup"><span data-stu-id="84c91-112">Sign in toohello Azure portal</span></span>
2. <span data-ttu-id="84c91-113">Dans le menu du Hub hello, cliquez sur, puis cliquez sur **Nouveau > mise en réseau >** puis cliquez sur **zone DNS** Panneau de zone DNS de créer tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="84c91-113">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![Zone DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="84c91-115">Sur hello **zone DNS de créer** panneau hello valeurs suivantes, puis entrez **créer**:</span><span class="sxs-lookup"><span data-stu-id="84c91-115">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>


   | <span data-ttu-id="84c91-116">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="84c91-116">**Setting**</span></span> | <span data-ttu-id="84c91-117">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="84c91-117">**Value**</span></span> | <span data-ttu-id="84c91-118">**Détails**</span><span class="sxs-lookup"><span data-stu-id="84c91-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="84c91-119">**Name**</span><span class="sxs-lookup"><span data-stu-id="84c91-119">**Name**</span></span>|<span data-ttu-id="84c91-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="84c91-120">contoso.com</span></span>|<span data-ttu-id="84c91-121">nom Hello de zone DNS de hello</span><span class="sxs-lookup"><span data-stu-id="84c91-121">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="84c91-122">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="84c91-122">**Subscription**</span></span>|<span data-ttu-id="84c91-123">[Votre abonnement]</span><span class="sxs-lookup"><span data-stu-id="84c91-123">[Your subscription]</span></span>|<span data-ttu-id="84c91-124">Sélectionnez une zone DNS d’abonnement toocreate hello dans.</span><span class="sxs-lookup"><span data-stu-id="84c91-124">Select a subscription toocreate hello DNS zone in.</span></span>|
   |<span data-ttu-id="84c91-125">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="84c91-125">**Resource group**</span></span>|<span data-ttu-id="84c91-126">**Créer :** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="84c91-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="84c91-127">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="84c91-127">Create a resource group.</span></span> <span data-ttu-id="84c91-128">nom de groupe de ressources Hello doit être unique au sein de l’abonnement hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="84c91-128">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="84c91-129">toolearn plus d’informations sur les groupes de ressources, lire hello [le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) l’article de vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="84c91-129">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="84c91-130">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="84c91-130">**Location**</span></span>|<span data-ttu-id="84c91-131">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="84c91-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="84c91-132">groupe de ressources Hello fait référence emplacement toohello hello du groupe de ressources et n’a aucun impact sur la zone DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="84c91-132">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="84c91-133">emplacement des zones DNS Hello est toujours « globaux » et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="84c91-133">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="84c91-134">Création de la liste des zones DNS</span><span class="sxs-lookup"><span data-stu-id="84c91-134">List DNS zones</span></span>

<span data-ttu-id="84c91-135">Dans l’hello portail Azure, accédez trop**davantage de services** > **réseau** > **zones DNS**.</span><span class="sxs-lookup"><span data-stu-id="84c91-135">In hello Azure portal, navigate too**More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="84c91-136">Chaque zone DNS est indépendante. Les informations telles que le nombre de jeux d’enregistrements et les serveurs de noms peuvent être consultés depuis cet aperçu.</span><span class="sxs-lookup"><span data-stu-id="84c91-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="84c91-137">colonne de Hello **serveurs de noms** n’est pas dans la vue par défaut de hello, tooadd il clic **colonnes**, sélectionnez **serveurs de noms** et cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="84c91-137">hello column **NAME SERVERS** is not in hello default view, tooadd it click **Columns**, select **Name servers** and click **Done**.</span></span>

![liste des zones DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="84c91-139">Suppression d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="84c91-139">Delete a DNS zone</span></span>

<span data-ttu-id="84c91-140">Accédez de zone DNS de tooa dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="84c91-140">Navigate tooa DNS zone in hello portal.</span></span> <span data-ttu-id="84c91-141">Sur hello **zone DNS** panneau, cliquez sur **supprimer la zone**.</span><span class="sxs-lookup"><span data-stu-id="84c91-141">On hello **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="84c91-142">Vous êtes invité à tooconfirm vous sont désireux de zone DNS de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="84c91-142">You are prompted tooconfirm you are wanting toodelete hello DNS zone.</span></span> <span data-ttu-id="84c91-143">Suppression d’une zone DNS supprime également tous les enregistrements de hello qui figurent dans la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="84c91-143">Deleting a DNS zone also deletes all hello records that are contained in hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84c91-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="84c91-144">Next steps</span></span>

<span data-ttu-id="84c91-145">Découvrez comment toowork avec votre Zone DNS et les enregistrements en vous rendant sur [prise en main Azure DNS à l’aide de hello Azure portal](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="84c91-145">Learn how toowork with your DNS Zone and records by visiting [Get started with Azure DNS using hello Azure portal](dns-getstarted-portal.md).</span></span>
