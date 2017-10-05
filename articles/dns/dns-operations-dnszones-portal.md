---
title: "Gérer des zones DNS dans Azure DNS - Portail Azure | Microsoft Docs"
description: "Vous pouvez gérer des zones DNS à l’aide du portail Azure. Cet article décrit comment mettre à jour, supprimer et créer des zones DNS sur Azure DNS."
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
ms.openlocfilehash: 69a509612e6204fc93dd42bf2fe69cb165b5777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="a1409-104">Gérer des zones DNS à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="a1409-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1409-105">Portail</span><span class="sxs-lookup"><span data-stu-id="a1409-105">Portal</span></span>](dns-operations-dnszones-portal.md)
> * [<span data-ttu-id="a1409-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1409-106">PowerShell</span></span>](dns-operations-dnszones.md)
> * [<span data-ttu-id="a1409-107">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a1409-107">Azure CLI 1.0</span></span>](dns-operations-dnszones-cli-nodejs.md)
> * [<span data-ttu-id="a1409-108">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a1409-108">Azure CLI 2.0</span></span>](dns-operations-dnszones-cli.md)

<span data-ttu-id="a1409-109">Cet article vous montre comment gérer vos zones DNS avec le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a1409-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="a1409-110">Vous pouvez également gérer vos zones DNS à l’aide de l’[interface de ligne de commande Azure](dns-operations-dnszones-cli.md) multiplateforme ou d’Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="a1409-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="a1409-111">Création d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="a1409-111">Create a DNS zone</span></span>

1. <span data-ttu-id="a1409-112">Connectez-vous au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a1409-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="a1409-113">Dans le menu Hub, cliquez sur **Nouveau > Mise en réseau >**, puis cliquez sur **Zone DNS** pour ouvrir le panneau Créer une zone DNS.</span><span class="sxs-lookup"><span data-stu-id="a1409-113">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![Zone DNS](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="a1409-115">Dans le panneau **Créer une zone DNS**, entrez les valeurs suivantes, puis cliquez sur **Créer** :</span><span class="sxs-lookup"><span data-stu-id="a1409-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="a1409-116">**Paramètre**</span><span class="sxs-lookup"><span data-stu-id="a1409-116">**Setting**</span></span> | <span data-ttu-id="a1409-117">**Valeur**</span><span class="sxs-lookup"><span data-stu-id="a1409-117">**Value**</span></span> | <span data-ttu-id="a1409-118">**Détails**</span><span class="sxs-lookup"><span data-stu-id="a1409-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="a1409-119">**Name**</span><span class="sxs-lookup"><span data-stu-id="a1409-119">**Name**</span></span>|<span data-ttu-id="a1409-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="a1409-120">contoso.com</span></span>|<span data-ttu-id="a1409-121">Nom de la zone DNS</span><span class="sxs-lookup"><span data-stu-id="a1409-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="a1409-122">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="a1409-122">**Subscription**</span></span>|<span data-ttu-id="a1409-123">[Votre abonnement]</span><span class="sxs-lookup"><span data-stu-id="a1409-123">[Your subscription]</span></span>|<span data-ttu-id="a1409-124">Sélectionnez un abonnement pour y créer la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="a1409-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="a1409-125">**Groupe de ressources**</span><span class="sxs-lookup"><span data-stu-id="a1409-125">**Resource group**</span></span>|<span data-ttu-id="a1409-126">**Créer :** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="a1409-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="a1409-127">Créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a1409-127">Create a resource group.</span></span> <span data-ttu-id="a1409-128">Le nom du groupe de ressources doit être unique au sein de l’abonnement sélectionné.</span><span class="sxs-lookup"><span data-stu-id="a1409-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="a1409-129">Pour plus d’informations sur les groupes de ressources, consultez l’article [Présentation de Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="a1409-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="a1409-130">**Emplacement**</span><span class="sxs-lookup"><span data-stu-id="a1409-130">**Location**</span></span>|<span data-ttu-id="a1409-131">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="a1409-131">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="a1409-132">Le groupe de ressources fait référence à l’emplacement du groupe de ressources et n’a aucun impact sur la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="a1409-132">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="a1409-133">L’emplacement de la zone DNS est toujours « global » et n’est pas affiché.</span><span class="sxs-lookup"><span data-stu-id="a1409-133">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="list-dns-zones"></a><span data-ttu-id="a1409-134">Création de la liste des zones DNS</span><span class="sxs-lookup"><span data-stu-id="a1409-134">List DNS zones</span></span>

<span data-ttu-id="a1409-135">Dans le portail Azure, accédez à **Plus de services** > **Mise en réseau** > **Zones DNS**.</span><span class="sxs-lookup"><span data-stu-id="a1409-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="a1409-136">Chaque zone DNS est indépendante. Les informations telles que le nombre de jeux d’enregistrements et les serveurs de noms peuvent être consultés depuis cet aperçu.</span><span class="sxs-lookup"><span data-stu-id="a1409-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="a1409-137">La colonne **SERVEURS DE NOMS** n’apparaît pas dans l’affichage par défaut. Pour l’ajouter, cliquez sur **Colonnes**, sélectionnez **Serveurs de noms**, puis cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="a1409-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![liste des zones DNS](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="a1409-139">Suppression d’une zone DNS</span><span class="sxs-lookup"><span data-stu-id="a1409-139">Delete a DNS zone</span></span>

<span data-ttu-id="a1409-140">Accédez à une zone DNS dans le portail.</span><span class="sxs-lookup"><span data-stu-id="a1409-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="a1409-141">Sur le panneau **Zone DNS**, cliquez sur **Supprimer la zone**.</span><span class="sxs-lookup"><span data-stu-id="a1409-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="a1409-142">Vous êtes invité à confirmer la suppression de la zone DNS.</span><span class="sxs-lookup"><span data-stu-id="a1409-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="a1409-143">La suppression d’une zone DNS entraîne la suppression de tous les enregistrements présents dans la zone.</span><span class="sxs-lookup"><span data-stu-id="a1409-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1409-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a1409-144">Next steps</span></span>

<span data-ttu-id="a1409-145">Apprenez à travailler avec votre zone DNS et vos enregistrements en vous rendant sur [Prise en main d’Azure DNS à l’aide du portail Azure](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a1409-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>