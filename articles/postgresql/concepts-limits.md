---
title: "Limitations dans une base de données Azure pour PostgreSQL | Microsoft Docs"
description: "Décrit les limitations des bases de données Azure pour PostgreSQL."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.topic: article
ms.date: 06/01/2017
ms.openlocfilehash: 38988fc5c0dc05331ea078534cd1a05e9eca2493
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-in-azure-database-for-postgresql"></a><span data-ttu-id="4ec65-103">Limitations des bases de données Azure pour PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4ec65-103">Limitations in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="4ec65-104">Le service de base de données Azure pour PostgreSQL est en préversion publique.</span><span class="sxs-lookup"><span data-stu-id="4ec65-104">The Azure Database for PostgreSQL service is in public preview.</span></span> <span data-ttu-id="4ec65-105">Les sections suivantes décrivent les limites fonctionnelles et les limites de capacités du service de base de données.</span><span class="sxs-lookup"><span data-stu-id="4ec65-105">The following sections describe capacity and functional limits in the database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="4ec65-106">Maximums de niveau de service</span><span class="sxs-lookup"><span data-stu-id="4ec65-106">Service Tier Maximums</span></span>
<span data-ttu-id="4ec65-107">La base de données Azure pour PostgreSQL a plusieurs niveaux de service que vous pouvez choisir pour créer un serveur.</span><span class="sxs-lookup"><span data-stu-id="4ec65-107">Azure Database for PostgreSQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="4ec65-108">Pour plus d’informations, consultez la page [Comprendre les éléments disponibles dans chaque niveau de service](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="4ec65-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="4ec65-109">Chaque niveau de service comporte un nombre maximal de connexions, d’unités de calcul et de stockage dans la préversion du service :</span><span class="sxs-lookup"><span data-stu-id="4ec65-109">There is a maximum number of connections, compute units, and storage in each service tier during the service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="4ec65-110">**Nombre maximal de connexions**</span><span class="sxs-lookup"><span data-stu-id="4ec65-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="4ec65-111">50 unités de calcul de base</span><span class="sxs-lookup"><span data-stu-id="4ec65-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="4ec65-112">50 connexions</span><span class="sxs-lookup"><span data-stu-id="4ec65-112">50 connections</span></span>    |
| <span data-ttu-id="4ec65-113">100 unités de calcul de base</span><span class="sxs-lookup"><span data-stu-id="4ec65-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="4ec65-114">100 connexions</span><span class="sxs-lookup"><span data-stu-id="4ec65-114">100 connections</span></span>   |
| <span data-ttu-id="4ec65-115">100 unités de calcul standard</span><span class="sxs-lookup"><span data-stu-id="4ec65-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="4ec65-116">200 connexions</span><span class="sxs-lookup"><span data-stu-id="4ec65-116">200 connections</span></span>   |
| <span data-ttu-id="4ec65-117">200 unités de calcul standard</span><span class="sxs-lookup"><span data-stu-id="4ec65-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="4ec65-118">300 connexions</span><span class="sxs-lookup"><span data-stu-id="4ec65-118">300 connections</span></span>   |
| <span data-ttu-id="4ec65-119">400 unités de calcul standard</span><span class="sxs-lookup"><span data-stu-id="4ec65-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="4ec65-120">400 connexions</span><span class="sxs-lookup"><span data-stu-id="4ec65-120">400 connections</span></span>   |
| <span data-ttu-id="4ec65-121">800 unités de calcul standard</span><span class="sxs-lookup"><span data-stu-id="4ec65-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="4ec65-122">500 connexions</span><span class="sxs-lookup"><span data-stu-id="4ec65-122">500 connections</span></span>   |
| <span data-ttu-id="4ec65-123">**Nombre maximal d’unités de calcul**</span><span class="sxs-lookup"><span data-stu-id="4ec65-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="4ec65-124">Niveau de service De base</span><span class="sxs-lookup"><span data-stu-id="4ec65-124">Basic service tier</span></span>         | <span data-ttu-id="4ec65-125">100 unités de calcul</span><span class="sxs-lookup"><span data-stu-id="4ec65-125">100 Compute Units</span></span> |
| <span data-ttu-id="4ec65-126">Niveau de service Standard</span><span class="sxs-lookup"><span data-stu-id="4ec65-126">Standard service tier</span></span>      | <span data-ttu-id="4ec65-127">800 unités de calcul</span><span class="sxs-lookup"><span data-stu-id="4ec65-127">800 Compute Units</span></span> |
| <span data-ttu-id="4ec65-128">**Volume maximal de stockage**</span><span class="sxs-lookup"><span data-stu-id="4ec65-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="4ec65-129">Niveau de service De base</span><span class="sxs-lookup"><span data-stu-id="4ec65-129">Basic service tier</span></span>         | <span data-ttu-id="4ec65-130">1 To</span><span class="sxs-lookup"><span data-stu-id="4ec65-130">1 TB</span></span>              |
| <span data-ttu-id="4ec65-131">Niveau de service Standard</span><span class="sxs-lookup"><span data-stu-id="4ec65-131">Standard service tier</span></span>      | <span data-ttu-id="4ec65-132">1 To</span><span class="sxs-lookup"><span data-stu-id="4ec65-132">1 TB</span></span>              |

<span data-ttu-id="4ec65-133">Au-delà du nombre maximal de connexions, vous risquez de recevoir l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="4ec65-133">When too many connections are reached, you may receive the following error:</span></span>
> <span data-ttu-id="4ec65-134">FATAL:  sorry, too many clients already</span><span class="sxs-lookup"><span data-stu-id="4ec65-134">FATAL:  sorry, too many clients already</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="4ec65-135">Limitations fonctionnelles de la préversion</span><span class="sxs-lookup"><span data-stu-id="4ec65-135">Preview functional limitations</span></span>
### <a name="scale-operations"></a><span data-ttu-id="4ec65-136">Opérations de mise à l’échelle</span><span class="sxs-lookup"><span data-stu-id="4ec65-136">Scale operations</span></span>
1.  <span data-ttu-id="4ec65-137">La mise à l’échelle dynamique de serveurs sur différents niveaux de service n’est pas prise en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="4ec65-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="4ec65-138">Autrement dit, il n’est pas possible de basculer entre les niveaux de service De base et Standard.</span><span class="sxs-lookup"><span data-stu-id="4ec65-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="4ec65-139">L’augmentation dynamique de la demande de stockage sur un serveur créé au préalable n’est pas prise en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="4ec65-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="4ec65-140">La diminution de la taille de stockage du serveur n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="4ec65-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="4ec65-141">Mises à niveau de la version du serveur</span><span class="sxs-lookup"><span data-stu-id="4ec65-141">Server version upgrades</span></span>
- <span data-ttu-id="4ec65-142">La migration automatique entre les versions principales du moteur de base de données n’est pas prise en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="4ec65-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="4ec65-143">Gestion des abonnements</span><span class="sxs-lookup"><span data-stu-id="4ec65-143">Subscription management</span></span>
- <span data-ttu-id="4ec65-144">Le déplacement dynamique de serveurs créés au préalable entre les groupes de ressources et d’abonnements n’est pas pris en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="4ec65-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="4ec65-145">Restauration dans le temps</span><span class="sxs-lookup"><span data-stu-id="4ec65-145">Point-in-time-restore</span></span>
1.  <span data-ttu-id="4ec65-146">La restauration à un autre niveau de service et/ou à une autre taille d’unités de calcul et de stockage n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="4ec65-146">Restoring to different service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="4ec65-147">La restauration d’un serveur supprimé n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="4ec65-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ec65-148">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ec65-148">Next steps</span></span>
- <span data-ttu-id="4ec65-149">Comprendre [les éléments disponibles dans chaque niveau tarifaire](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="4ec65-149">Understand [What’s available in each pricing tier](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="4ec65-150">Comprendre [les versions prises en charge de la base de données PostgreSQL](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="4ec65-150">Understand [Supported PostgreSQL Database Versions](concepts-supported-versions.md)</span></span>
- <span data-ttu-id="4ec65-151">Consulter le [guide pratique : sauvegarder et restaurer un serveur dans une base de données Azure pour PostgreSQL à l’aide du Portail Azure](howto-restore-server-portal.md)</span><span class="sxs-lookup"><span data-stu-id="4ec65-151">Review [How To Back up and Restore a server in Azure Database for PostgreSQL using the Azure portal](howto-restore-server-portal.md)</span></span>
