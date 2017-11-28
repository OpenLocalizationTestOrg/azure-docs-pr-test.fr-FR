---
title: "aaaManage DNS enregistrer des jeux et les enregistrements avec le système DNS Azure | Documents Microsoft"
description: "DNS Azure fournit un enregistrement DNS toomanage hello fonctionnalité définit et enregistre lors de l’hébergement de votre domaine."
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
ms.openlocfilehash: 2e62d017341589eaf8d1f8df2fe5db4b973381d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-record-sets-by-using-hello-azure-portal"></a><span data-ttu-id="29117-103">Gérer les enregistrements DNS et les jeux d’enregistrements à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="29117-103">Manage DNS records and record sets by using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="29117-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="29117-104">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="29117-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="29117-105">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="29117-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="29117-106">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="29117-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29117-107">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="29117-108">Cet article vous explique comment toomanage jeux d’enregistrements et les enregistrements pour votre zone DNS à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="29117-108">This article shows you how toomanage record sets and records for your DNS zone by using hello Azure portal.</span></span>

<span data-ttu-id="29117-109">Il est important toounderstand hello différence jeux d’enregistrements DNS et des enregistrements DNS.</span><span class="sxs-lookup"><span data-stu-id="29117-109">It's important toounderstand hello difference between DNS record sets and individual DNS records.</span></span> <span data-ttu-id="29117-110">Un jeu d’enregistrements est une collection d’enregistrements dans une zone possédant hello même nom et sont hello même type.</span><span class="sxs-lookup"><span data-stu-id="29117-110">A record set is a collection of records in a zone that have hello same name and are hello same type.</span></span> <span data-ttu-id="29117-111">Pour plus d’informations, consultez [jeux d’enregistrements DNS de créer et d’enregistrements à l’aide de portail Azure hello](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="29117-111">For more information, see [Create DNS record sets and records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="create-a-new-record-set-and-record"></a><span data-ttu-id="29117-112">Création d’un jeu d’enregistrements et d’un enregistrement</span><span class="sxs-lookup"><span data-stu-id="29117-112">Create a new record set and record</span></span>

<span data-ttu-id="29117-113">toocreate un ensemble d’enregistrements d’hello portail Azure, consultez [les enregistrements DNS de créer à l’aide de hello Azure portal](dns-getstarted-create-recordset-portal.md).</span><span class="sxs-lookup"><span data-stu-id="29117-113">toocreate a record set in hello Azure portal, see [Create DNS records by using hello Azure portal](dns-getstarted-create-recordset-portal.md).</span></span>

## <a name="view-a-record-set"></a><span data-ttu-id="29117-114">Affichage d’un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="29117-114">View a record set</span></span>

1. <span data-ttu-id="29117-115">Bonjour portail Azure, accédez à toohello **zone DNS** panneau.</span><span class="sxs-lookup"><span data-stu-id="29117-115">In hello Azure portal, go toohello **DNS zone** blade.</span></span>
2. <span data-ttu-id="29117-116">Recherchez le jeu d’enregistrements hello et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="29117-116">Search for hello record set and select it.</span></span> <span data-ttu-id="29117-117">Propriétés du jeu d’enregistrements hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="29117-117">This opens hello record set properties.</span></span>

    ![Recherche d’un jeu d’enregistrements](./media/dns-operations-recordsets-portal/searchset500.png)

## <a name="add-a-new-record-tooa-record-set"></a><span data-ttu-id="29117-119">Ajouter un nouveau jeu d’enregistrements tooa enregistrement</span><span class="sxs-lookup"><span data-stu-id="29117-119">Add a new record tooa record set</span></span>

<span data-ttu-id="29117-120">Vous pouvez ajouter jusqu'à tooany jeu d’enregistrements too20 enregistrements.</span><span class="sxs-lookup"><span data-stu-id="29117-120">You can add up too20 records tooany record set.</span></span> <span data-ttu-id="29117-121">Un jeu d’enregistrements ne peut pas contenir deux enregistrements identiques.</span><span class="sxs-lookup"><span data-stu-id="29117-121">A record set cannot contain two identical records.</span></span> <span data-ttu-id="29117-122">Jeux d’enregistrements vides (avec zéro enregistrements) peut être créés, mais n’apparaître pas sur les serveurs DNS de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="29117-122">Empty record sets (with zero records) can be created, but do not appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="29117-123">Les jeux d’enregistrements du type CNAME peuvent contenir un enregistrement au maximum.</span><span class="sxs-lookup"><span data-stu-id="29117-123">Record sets of type CNAME can contain one record at most.</span></span>

1. <span data-ttu-id="29117-124">Sur hello **propriétés du jeu d’enregistrements** panneau pour votre zone DNS, cliquez sur l’enregistrement hello défini que vous souhaitez tooadd un enregistrement.</span><span class="sxs-lookup"><span data-stu-id="29117-124">On hello **Record set properties** blade for your DNS zone, click hello record set that you want tooadd a record to.</span></span>

    ![Sélection d’un jeu d'enregistrements](./media/dns-operations-recordsets-portal/selectset500.png)

2. <span data-ttu-id="29117-126">Spécifiez les propriétés de jeu d’enregistrements de hello en renseignant les champs hello.</span><span class="sxs-lookup"><span data-stu-id="29117-126">Specify hello record set properties by filling in hello fields.</span></span>

    ![Ajouter un enregistrement](./media/dns-operations-recordsets-portal/addrecord500.png)

3. <span data-ttu-id="29117-128">Cliquez sur **enregistrer** à hello haut de hello panneau toosave vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="29117-128">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="29117-129">Puis fermez le panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="29117-129">Then close hello blade.</span></span>
4. <span data-ttu-id="29117-130">Dans l’angle de hello, vous verrez que l’enregistrement de hello enregistre.</span><span class="sxs-lookup"><span data-stu-id="29117-130">In hello corner, you will see that hello record is saving.</span></span>

    ![Enregistrement d’un jeu d'enregistrements](./media/dns-operations-recordsets-portal/saving150.png)

<span data-ttu-id="29117-132">Une fois l’enregistrement de hello a été enregistré, hello valeurs hello **zone DNS** panneau reflète le nouvel enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="29117-132">After hello record has been saved, hello values on hello **DNS zone** blade will reflect hello new record.</span></span>

## <a name="update-a-record"></a><span data-ttu-id="29117-133">Mise à jour d’un enregistrement</span><span class="sxs-lookup"><span data-stu-id="29117-133">Update a record</span></span>

<span data-ttu-id="29117-134">Lorsque vous mettez à jour un enregistrement dans un jeu d’enregistrements existant, vous pouvez mettre à jour des champs de hello dépendent de type hello d’enregistrement avec lequel vous travaillez.</span><span class="sxs-lookup"><span data-stu-id="29117-134">When you update a record in an existing record set, hello fields you can update depend on hello type of record you're working with.</span></span>

1. <span data-ttu-id="29117-135">Sur hello **propriétés du jeu d’enregistrements** panneau pour votre jeu d’enregistrements, recherchez les enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="29117-135">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="29117-136">Modifier un enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="29117-136">Modify hello record.</span></span> <span data-ttu-id="29117-137">Lorsque vous modifiez un enregistrement, vous pouvez modifier les paramètres disponibles de hello pour l’enregistrement de hello.</span><span class="sxs-lookup"><span data-stu-id="29117-137">When you modify a record, you can change hello available settings for hello record.</span></span> <span data-ttu-id="29117-138">Dans l’exemple suivant de hello, hello **adresse IP** champ est sélectionné et l’adresse IP de hello est en cours de hello d’en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="29117-138">In hello following example, hello **IP address** field is selected, and hello IP address is in hello process of being modified.</span></span>

    ![Modification d’un enregistrement](./media/dns-operations-recordsets-portal/modifyrecord500.png)

3. <span data-ttu-id="29117-140">Cliquez sur **enregistrer** à hello haut de hello panneau toosave vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="29117-140">Click **Save** at hello top of hello blade toosave your settings.</span></span> <span data-ttu-id="29117-141">Dans le coin supérieur droit hello, vous verrez notification hello hello enregistrement a été enregistré.</span><span class="sxs-lookup"><span data-stu-id="29117-141">In hello upper right corner, you'll see hello notification that hello record has been saved.</span></span>

    ![Ajout d’un jeu d’enregistrements](./media/dns-operations-recordsets-portal/saved150.png)

<span data-ttu-id="29117-143">Une fois l’enregistrement de hello a été enregistré, les valeurs de hello pour l’enregistrement de hello définies sur hello **zone DNS** panneau reflètent les enregistrement hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="29117-143">After hello record has been saved, hello values for hello record set on hello **DNS zone** blade will reflect hello updated record.</span></span>

## <a name="remove-a-record-from-a-record-set"></a><span data-ttu-id="29117-144">Suppression d’un enregistrement d’un jeu d’enregistrements</span><span class="sxs-lookup"><span data-stu-id="29117-144">Remove a record from a record set</span></span>

<span data-ttu-id="29117-145">Vous pouvez utiliser des enregistrements de tooremove portail Azure hello à partir d’un jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="29117-145">You can use hello Azure portal tooremove records from a record set.</span></span> <span data-ttu-id="29117-146">Notez que la suppression du dernier enregistrement de hello à partir d’un jeu d’enregistrements ne supprime pas jeu d’enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="29117-146">Note that removing hello last record from a record set does not delete hello record set.</span></span>

1. <span data-ttu-id="29117-147">Sur hello **propriétés du jeu d’enregistrements** panneau pour votre jeu d’enregistrements, recherchez les enregistrements hello.</span><span class="sxs-lookup"><span data-stu-id="29117-147">On hello **Record set properties** blade for your record set, search for hello record.</span></span>
2. <span data-ttu-id="29117-148">Cliquez sur hello d’enregistrement tooremove.</span><span class="sxs-lookup"><span data-stu-id="29117-148">Click hello record that you want tooremove.</span></span> <span data-ttu-id="29117-149">Puis sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="29117-149">Then select **Remove**.</span></span>

    ![Suppression d’un enregistrement](./media/dns-operations-recordsets-portal/removerecord500.png)

3. <span data-ttu-id="29117-151">Cliquez sur **enregistrer** à hello haut de hello panneau toosave vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="29117-151">Click **Save** at hello top of hello blade toosave your settings.</span></span>
4. <span data-ttu-id="29117-152">Une fois l’enregistrement de hello a été supprimé, de valeurs pour l’enregistrement de hello hello hello **zone DNS** panneau reflète la suppression de hello.</span><span class="sxs-lookup"><span data-stu-id="29117-152">After hello record has been removed, hello values for hello record on hello **DNS zone** blade will reflect hello removal.</span></span>

## <span data-ttu-id="29117-153"><a name="delete"></a>Suppression d’un jeu d'enregistrements</span><span class="sxs-lookup"><span data-stu-id="29117-153"><a name="delete"></a>Delete a record set</span></span>

1. <span data-ttu-id="29117-154">Sur hello **propriétés du jeu d’enregistrements** panneau pour votre jeu d’enregistrements, cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="29117-154">On hello **Record set properties** blade for your record set, click **Delete**.</span></span>

    ![Supprimer un jeu d’enregistrements](./media/dns-operations-recordsets-portal/deleterecordset500.png)

2. <span data-ttu-id="29117-156">Un message apparaît vous demandant si vous souhaitez que le jeu d’enregistrements toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="29117-156">A message appears asking if you want toodelete hello record set.</span></span>
3. <span data-ttu-id="29117-157">Vérifiez que hello nom correspondances hello enregistrement que vous souhaitez toodelete, puis cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="29117-157">Verify that hello name matches hello record set that you want toodelete, and then click **Yes**.</span></span>
4. <span data-ttu-id="29117-158">Sur hello **zone DNS** panneau, vérifiez que le jeu d’enregistrements hello n’est plus visible.</span><span class="sxs-lookup"><span data-stu-id="29117-158">On hello **DNS zone** blade, verify that hello record set is no longer visible.</span></span>

## <a name="work-with-ns-and-soa-records"></a><span data-ttu-id="29117-159">Utilisation d’enregistrements NS et SOA</span><span class="sxs-lookup"><span data-stu-id="29117-159">Work with NS and SOA records</span></span>

<span data-ttu-id="29117-160">Les enregistrements NS et SOA qui sont créés automatiquement sont gérés différemment des autres types d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="29117-160">NS and SOA records that are automatically created are managed differently from other record types.</span></span>

### <a name="modify-soa-records"></a><span data-ttu-id="29117-161">Modification d'enregistrements SOA</span><span class="sxs-lookup"><span data-stu-id="29117-161">Modify SOA records</span></span>

<span data-ttu-id="29117-162">Impossible d’ajouter ou supprimer des enregistrements de hello créé automatiquement SOA jeu d’enregistrements au sommet de zone hello (nom = « @ »).</span><span class="sxs-lookup"><span data-stu-id="29117-162">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (name = "@").</span></span> <span data-ttu-id="29117-163">Toutefois, vous pouvez modifier les paramètres de hello dans hello enregistrement SOA (à l’exception de « hôte ») et enregistrement de hello définie la durée de vie.</span><span class="sxs-lookup"><span data-stu-id="29117-163">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

### <a name="modify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="29117-164">Modifier les enregistrements NS au sommet de zone hello</span><span class="sxs-lookup"><span data-stu-id="29117-164">Modify NS records at hello zone apex</span></span>

<span data-ttu-id="29117-165">jeu au sommet de zone hello d’enregistrements NS Hello sont automatiquement créé avec chaque zone DNS.</span><span class="sxs-lookup"><span data-stu-id="29117-165">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="29117-166">Il contient les noms de hello de zone de hello Azure DNS nom serveurs toohello attribué.</span><span class="sxs-lookup"><span data-stu-id="29117-166">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="29117-167">Vous pouvez ajouter des noms supplémentaires serveurs toothis NS jeu d’enregistrements, toosupport domaines l’hébergement avec le fournisseur DNS.</span><span class="sxs-lookup"><span data-stu-id="29117-167">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="29117-168">Vous pouvez également modifier la durée de vie de hello et les métadonnées pour ce jeu d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="29117-168">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="29117-169">Toutefois, vous ne peut pas supprimer ou modifier les serveurs de noms DNS Azure hello préremplies.</span><span class="sxs-lookup"><span data-stu-id="29117-169">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="29117-170">Notez que cela s’applique uniquement toohello NS jeu d’enregistrements au sommet de zone hello.</span><span class="sxs-lookup"><span data-stu-id="29117-170">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="29117-171">Autres jeux d’enregistrements NS dans votre zone (comme les zones enfant toodelegate utilisé) peut être modifié sans contrainte.</span><span class="sxs-lookup"><span data-stu-id="29117-171">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

### <a name="delete-soa-or-ns-record-sets"></a><span data-ttu-id="29117-172">Suppression de jeux d’enregistrements SOA ou NS</span><span class="sxs-lookup"><span data-stu-id="29117-172">Delete SOA or NS record sets</span></span>

<span data-ttu-id="29117-173">Vous ne pouvez pas supprimer hello SOA et NS jeux d’enregistrements au sommet de zone hello (nom = « @ ») qui sont créés automatiquement lors de la zone de hello est créée.</span><span class="sxs-lookup"><span data-stu-id="29117-173">You cannot delete hello SOA and NS record sets at hello zone apex (name = "@") that are created automatically when hello zone is created.</span></span> <span data-ttu-id="29117-174">Elles sont supprimées automatiquement lorsque vous supprimez la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="29117-174">They are deleted automatically when you delete hello zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29117-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29117-175">Next steps</span></span>

* <span data-ttu-id="29117-176">Pour plus d’informations sur le système DNS Azure, consultez hello [vue d’ensemble de DNS Azure](dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29117-176">For more information about Azure DNS, see hello [Azure DNS overview](dns-overview.md).</span></span>
* <span data-ttu-id="29117-177">Pour plus d’informations sur l’automatisation de DNS, consultez [zones DNS de création et jeux d’enregistrements à l’aide de .NET SDK hello](dns-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="29117-177">For more information about automating DNS, see [Creating DNS zones and record sets using hello .NET SDK](dns-sdk.md).</span></span>
* <span data-ttu-id="29117-178">Pour plus d’informations sur les enregistrements DNS inversés, consultez l’article [Vue d’ensemble des DNS inversés et assistance dans Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29117-178">For more information about reverse DNS records, see [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>
