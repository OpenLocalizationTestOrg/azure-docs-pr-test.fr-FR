---
title: "Gérer des jeux d’enregistrements DNS et des enregistrements avec Azure DNS | Microsoft Docs"
description: "Azure DNS permet de gérer les jeux d’enregistrements DNS et les enregistrements lors de l’hébergement de votre domaine."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ed44a1-7bfe-454f-964e-922ad978264a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 001b80ccba43beab44f6a598f820df65a85a345f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-the-azure-portal"></a><span data-ttu-id="6639c-103">Gestion d’enregistrements et de jeux d’enregistrements DNS à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="6639c-103">Manage DNS records and record sets by using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="6639c-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="6639c-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="6639c-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6639c-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="6639c-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6639c-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="6639c-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6639c-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="6639c-108">Cet article explique comment gérer les jeux d’enregistrements et les enregistrements pour votre zone DNS À l’aide du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6639c-108">This article shows you how to manage record sets and records for your DNS zone by using the Azure portal.</span></span>

<span data-ttu-id="6639c-109">Il est important de comprendre la différence entre les jeux d’enregistrements DNS et les enregistrements DNS individuels.</span><span class="sxs-lookup"><span data-stu-id="6639c-109">It's important to understand the difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="6639c-110">Un jeu d’enregistrements est une collection d’enregistrements dans une zone ayant le même nom et le même type.</span><span class="sxs-lookup"><span data-stu-id="6639c-110">A record set is a collection of records in a zone that have the same name and are the same type.</span></span> <span data-ttu-id="6639c-111">Pour plus d’informations, consultez [Création de jeux d’enregistrements et d’enregistrements DNS à l’aide du portail Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6639c-111">For more information, see [Create DNS record sets and records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="6639c-112">Création d’un jeu d’enregistrements et d’un enregistrement</span><span class="sxs-lookup"><span data-stu-id="6639c-112">Create a new record set and record</span></span>

<span data-ttu-id="6639c-113">Pour créer un jeu d’enregistrements dans le portail Azure, consultez [Création d’enregistrements DNS à l’aide du portail Azure](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6639c-113">To create a record set in the Azure portal, see [Create DNS records by using the Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="6639c-114">Affichage d’un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="6639c-114">View a record set</span></span>

1. <span data-ttu-id="6639c-115">Dans le portail Azure, accédez au panneau **zone DNS** .</span><span class="sxs-lookup"><span data-stu-id="6639c-115">In the Azure portal, go to the **DNS zone** blade.</span></span>
2. <span data-ttu-id="6639c-116">Recherchez le jeu d’enregistrements et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="6639c-116">Search for the record set and select it.</span></span> <span data-ttu-id="6639c-117">Les propriétés du jeu d’enregistrements s’affichent.</span><span class="sxs-lookup"><span data-stu-id="6639c-117">This opens the record set properties.</span></span>

    ![Recherche d’un jeu d’enregistrements](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-to-a-record-set"></a><span data-ttu-id="6639c-119">Ajouter un nouvel enregistrement à un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="6639c-119">Add a new record to a record set</span></span>

<span data-ttu-id="6639c-120">Vous pouvez ajouter jusqu'à 20 enregistrements à n'importe quel jeu d'enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6639c-120">You can add up to 20 records to any record set.</span></span> <span data-ttu-id="6639c-121">Un jeu d’enregistrements ne peut pas contenir deux enregistrements identiques.</span><span class="sxs-lookup"><span data-stu-id="6639c-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="6639c-122">Des jeux d'enregistrements vides (avec zéro enregistrement) peuvent être créés, mais ils n'apparaîtront pas sur les serveurs de noms Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="6639c-122">Empty record sets (with zero records) can be created, but do not appear on the Azure DNS name servers.</span></span> <span data-ttu-id="6639c-123">Les jeux d’enregistrements du type CNAME peuvent contenir un enregistrement au maximum.</span><span class="sxs-lookup"><span data-stu-id="6639c-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="6639c-124">Dans le panneau des **propriétés du jeu d’enregistrements** de votre zone DNS, cliquez sur le jeu d’enregistrements auquel vous souhaitez ajouter un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="6639c-124">On the **Record set properties** blade for your DNS zone, click the record set that you want to add a record to.</span></span>

    ![Sélection d’un jeu d'enregistrements](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="6639c-126">Spécifiez les propriétés du jeu d’enregistrements en remplissant les champs.</span><span class="sxs-lookup"><span data-stu-id="6639c-126">Specify the record set properties by filling in the fields.</span></span>

    ![Ajouter un enregistrement](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="6639c-128">Cliquez sur **Enregistrer** en haut du panneau pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="6639c-128">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="6639c-129">Puis fermez le panneau.</span><span class="sxs-lookup"><span data-stu-id="6639c-129">Then close the blade.</span></span>
4. <span data-ttu-id="6639c-130">Dans l’angle, vous verrez que l’enregistrement est en cours de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6639c-130">In the corner, you will see that the record is saving.</span></span>

    ![Enregistrement d’un jeu d'enregistrements](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="6639c-132">Une fois que l’enregistrement a été sauvegardé, les valeurs du panneau **Zone DNS** reflètent le nouvel enregistrement.</span><span class="sxs-lookup"><span data-stu-id="6639c-132">After the record has been saved, the values on the **DNS zone** blade will reflect the new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="6639c-133">Mise à jour d’un enregistrement</span><span class="sxs-lookup"><span data-stu-id="6639c-133">Update a record</span></span>

<span data-ttu-id="6639c-134">Lors de la mise à jour d’un enregistrement dans un jeu d’enregistrements existant, les champs pouvant être mis à jour varient selon le type d’enregistrement que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="6639c-134">When you update a record in an existing record set, the fields you can update depend on the type of record you're working with.</span></span>

1. <span data-ttu-id="6639c-135">Dans le panneau **Propriétés du jeu d’enregistrements** de votre jeu d’enregistrements, recherchez l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="6639c-135">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="6639c-136">Modifiez l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="6639c-136">Modify the record.</span></span> <span data-ttu-id="6639c-137">Lorsque vous modifiez un enregistrement, vous pouvez modifier les paramètres disponibles pour l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="6639c-137">When you modify a record, you can change the available settings for the record.</span></span> <span data-ttu-id="6639c-138">Dans l’exemple suivant, le champ **Adresse IP** est sélectionné et l’adresse IP est en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="6639c-138">In the following example, the **IP address** field is selected, and the IP address is in the process of being modified.</span></span>

    ![Modification d’un enregistrement](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="6639c-140">Cliquez sur **Enregistrer** en haut du panneau pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="6639c-140">Click **Save** at the top of the blade to save your settings.</span></span> <span data-ttu-id="6639c-141">Une notification s’affiche dans le coin supérieur droit indiquant que l’enregistrement a été sauvegardé.</span><span class="sxs-lookup"><span data-stu-id="6639c-141">In the upper right corner, you'll see the notification that the record has been saved.</span></span>

    ![Ajout d’un jeu d’enregistrements](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="6639c-143">Une fois que l’enregistrement a été sauvegardé, les valeurs du jeu d’enregistrements dans le panneau **Zone DNS** reflètent l’enregistrement mis à jour.</span><span class="sxs-lookup"><span data-stu-id="6639c-143">After the record has been saved, the values for the record set on the **DNS zone** blade will reflect the updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="6639c-144">Suppression d’un enregistrement d’un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="6639c-144">Remove a record from a record set</span></span>

<span data-ttu-id="6639c-145">Vous pouvez utiliser le portail Azure pour supprimer des enregistrements d’un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6639c-145">You can use the Azure portal to remove records from a record set.</span></span> <span data-ttu-id="6639c-146">Notez que la suppression du dernier enregistrement d’un jeu d’enregistrements ne supprime pas le jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6639c-146">Note that removing the last record from a record set does not delete the record set.</span></span>

1. <span data-ttu-id="6639c-147">Dans le panneau **Propriétés du jeu d’enregistrements** de votre jeu d’enregistrements, recherchez l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="6639c-147">On the **Record set properties** blade for your record set, search for the record.</span></span>
2. <span data-ttu-id="6639c-148">Cliquez sur l’enregistrement que vous souhaitez supprimer.</span><span class="sxs-lookup"><span data-stu-id="6639c-148">Click the record that you want to remove.</span></span> <span data-ttu-id="6639c-149">Puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6639c-149">Then select **Remove**.</span></span>

    ![Suppression d’un enregistrement](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="6639c-151">Cliquez sur **Enregistrer** en haut du panneau pour enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="6639c-151">Click **Save** at the top of the blade to save your settings.</span></span>
4. <span data-ttu-id="6639c-152">Une fois que l’enregistrement a été supprimé, les valeurs du jeu d’enregistrements dans le panneau **Zone DNS** reflètent la suppression de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="6639c-152">After the record has been removed, the values for the record on the **DNS zone** blade will reflect the removal.</span></span>

## <span data-ttu-id="6639c-153"><a name="delete"></a>Suppression d’un jeu d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="6639c-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="6639c-154">Dans le panneau **Propriétés du jeu d’enregistrements** de votre jeu d’enregistrements, cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="6639c-154">On the **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Supprimer un jeu d’enregistrements](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="6639c-156">Un message s’affiche vous demandant si vous souhaitez supprimer le jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6639c-156">A message appears asking if you want to delete the record set.</span></span>
3. <span data-ttu-id="6639c-157">Vérifiez que le nom correspond au jeu d’enregistrements que vous souhaitez supprimer, puis cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="6639c-157">Verify that the name matches the record set that you want to delete, and then click **Yes**.</span></span>
4. <span data-ttu-id="6639c-158">Dans le panneau de **Zone DNS** , vous pouvez vérifier que le jeu d’enregistrements n’est plus visible.</span><span class="sxs-lookup"><span data-stu-id="6639c-158">On the **DNS zone** blade, verify that the record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="6639c-159">Utilisation d’enregistrements NS et SOA</span><span class="sxs-lookup"><span data-stu-id="6639c-159">Work with NS and SOA records</span></span>

<span data-ttu-id="6639c-160">Les enregistrements NS et SOA qui sont créés automatiquement sont gérés différemment des autres types d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6639c-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="6639c-161">Modification d'enregistrements SOA</span><span class="sxs-lookup"><span data-stu-id="6639c-161">Modify SOA records</span></span>

<span data-ttu-id="6639c-162">Vous ne pouvez pas ajouter ou supprimer d’enregistrements dans le jeu d’enregistrements SOA créé automatiquement à l’extrémité de la zone (nom = « @ »).</span><span class="sxs-lookup"><span data-stu-id="6639c-162">You cannot add or remove records from the automatically created SOA record set at the zone apex (name = "@").</span></span> <span data-ttu-id="6639c-163">Vous pouvez cependant modifier les paramètres dans l’enregistrement SOA (à l’exception de « l’hôte ») et pendant la durée de vie du jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6639c-163">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

### <a name="modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="6639c-164">Modification d’enregistrements NS à l’extrémité de la zone</span><span class="sxs-lookup"><span data-stu-id="6639c-164">Modify NS records at the zone apex</span></span>

<span data-ttu-id="6639c-165">Le jeu d’enregistrements NS à l’apex de la zone est créé automatiquement avec chaque zone DNS.</span><span class="sxs-lookup"><span data-stu-id="6639c-165">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="6639c-166">Il contient les noms des serveurs de noms Azure DNS attribués à la zone.</span><span class="sxs-lookup"><span data-stu-id="6639c-166">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="6639c-167">Vous pouvez ajouter des serveurs de noms supplémentaires à ce jeu d’enregistrements NS, pour prendre en charge le co-hébergement de domaines avec plusieurs fournisseurs DNS.</span><span class="sxs-lookup"><span data-stu-id="6639c-167">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="6639c-168">Vous pouvez également modifier la durée de vie et les métadonnées pour ce jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="6639c-168">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="6639c-169">Toutefois, vous ne pouvez pas supprimer ni modifier les serveurs de noms Azure DNS préremplis.</span><span class="sxs-lookup"><span data-stu-id="6639c-169">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="6639c-170">Notez que cela s’applique uniquement au jeu d’enregistrements NS défini à l’apex de la zone.</span><span class="sxs-lookup"><span data-stu-id="6639c-170">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="6639c-171">Les autres jeux d’enregistrements NS dans votre zone (tels que ceux utilisés pour déléguer des zones enfants) peuvent être modifiés sans contrainte.</span><span class="sxs-lookup"><span data-stu-id="6639c-171">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="6639c-172">Suppression de jeux d’enregistrements SOA ou NS</span><span class="sxs-lookup"><span data-stu-id="6639c-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="6639c-173">Vous ne pouvez pas supprimer les jeux d’enregistrements SOA et NS à l’extrémité de la zone (nom = « @ ») qui sont créés automatiquement quand la zone est créée.</span><span class="sxs-lookup"><span data-stu-id="6639c-173">You cannot delete the SOA and NS record sets at the zone apex (name = "@") that are created automatically when the zone is created.</span></span> <span data-ttu-id="6639c-174">Ils sont automatiquement supprimés lorsque vous supprimez la zone.</span><span class="sxs-lookup"><span data-stu-id="6639c-174">They are deleted automatically when you delete the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6639c-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6639c-175">Next steps</span></span>

* <span data-ttu-id="6639c-176">Pour plus d’informations sur Azure DNS, consultez la [Vue d’ensemble d’Azure DNS](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6639c-176">For more information about Azure DNS, see the [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="6639c-177">Pour plus d’informations sur l’automatisation de DNS, consultez la rubrique [Création des zones DNS et de jeux d’enregistrements à l’aide du Kit de développement logiciel (SDK) .NET](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="6639c-177">For more information about automating DNS, see [Creating DNS zones and record sets using the .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="6639c-178">Pour plus d’informations sur les enregistrements DNS inversés, consultez l’article [Vue d’ensemble des DNS inversés et assistance dans Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6639c-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
