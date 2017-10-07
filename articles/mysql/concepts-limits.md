---
title: "aaaLimitations dans la base de données Azure pour MySQL | Documents Microsoft"
description: "Décrit les limitations de la préversion des bases de données Azure pour MySQL."
services: mysql
author: jasonh
ms.author: kamathsun
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 9c877c592bf640f62182d8761c9c51363882d706
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-in-azure-database-for-mysql-preview"></a><span data-ttu-id="f3f1b-103">Limitations dans une base de données Azure pour MySQL (préversion)</span><span class="sxs-lookup"><span data-stu-id="f3f1b-103">Limitations in Azure Database for MySQL (Preview)</span></span>
<span data-ttu-id="f3f1b-104">Bonjour Azure de base de données pour le service MySQL est en version préliminaire publique.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-104">hello Azure Database for MySQL service is in public preview.</span></span> <span data-ttu-id="f3f1b-105">Hello sections suivantes décrivent la capacité et des limites fonctionnelles dans le service de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-105">hello following sections describe capacity and functional limits in hello database service.</span></span>

## <a name="service-tier-maximums"></a><span data-ttu-id="f3f1b-106">Maximums de niveau de service</span><span class="sxs-lookup"><span data-stu-id="f3f1b-106">Service Tier Maximums</span></span>
<span data-ttu-id="f3f1b-107">La base de données Azure pour MySQL a plusieurs niveaux de service que vous pouvez choisir pour créer un serveur.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-107">Azure Database for MySQL has multiple service tiers you can choose from when creating a server.</span></span> <span data-ttu-id="f3f1b-108">Pour plus d’informations, consultez la page [Comprendre les éléments disponibles dans chaque niveau de service](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="f3f1b-108">For more information, see [Understand what’s available in each service tier](concepts-service-tiers.md).</span></span>  

<span data-ttu-id="f3f1b-109">Est un nombre maximal de connexions, les unités de calcul et de stockage dans chaque niveau de service préliminaire hello service, comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3f1b-109">There is a maximum number of connections, compute units, and storage in each service tier during hello service preview, as follows:</span></span> 

|                            |                   |
| :------------------------- | :---------------- |
| <span data-ttu-id="f3f1b-110">**Nombre maximal de connexions**</span><span class="sxs-lookup"><span data-stu-id="f3f1b-110">**Max connections**</span></span>        |                   |
| <span data-ttu-id="f3f1b-111">50 unités de calcul de base</span><span class="sxs-lookup"><span data-stu-id="f3f1b-111">Basic 50 Compute Units</span></span>     | <span data-ttu-id="f3f1b-112">50 connexions</span><span class="sxs-lookup"><span data-stu-id="f3f1b-112">50 connections</span></span>    |
| <span data-ttu-id="f3f1b-113">100 unités de calcul de base</span><span class="sxs-lookup"><span data-stu-id="f3f1b-113">Basic 100 Compute Units</span></span>    | <span data-ttu-id="f3f1b-114">100 connexions</span><span class="sxs-lookup"><span data-stu-id="f3f1b-114">100 connections</span></span>   |
| <span data-ttu-id="f3f1b-115">100 unités de calcul standard</span><span class="sxs-lookup"><span data-stu-id="f3f1b-115">Standard 100 Compute Units</span></span> | <span data-ttu-id="f3f1b-116">200 connexions</span><span class="sxs-lookup"><span data-stu-id="f3f1b-116">200 connections</span></span>   |
| <span data-ttu-id="f3f1b-117">200 unités de calcul standard</span><span class="sxs-lookup"><span data-stu-id="f3f1b-117">Standard 200 Compute Units</span></span> | <span data-ttu-id="f3f1b-118">300 connexions</span><span class="sxs-lookup"><span data-stu-id="f3f1b-118">300 connections</span></span>   |
| <span data-ttu-id="f3f1b-119">400 unités de calcul standard</span><span class="sxs-lookup"><span data-stu-id="f3f1b-119">Standard 400 Compute Units</span></span> | <span data-ttu-id="f3f1b-120">400 connexions</span><span class="sxs-lookup"><span data-stu-id="f3f1b-120">400 connections</span></span>   |
| <span data-ttu-id="f3f1b-121">800 unités de calcul standard</span><span class="sxs-lookup"><span data-stu-id="f3f1b-121">Standard 800 Compute Units</span></span> | <span data-ttu-id="f3f1b-122">500 connexions</span><span class="sxs-lookup"><span data-stu-id="f3f1b-122">500 connections</span></span>   |
| <span data-ttu-id="f3f1b-123">**Nombre maximal d’unités de calcul**</span><span class="sxs-lookup"><span data-stu-id="f3f1b-123">**Max Compute Units**</span></span>      |                   |
| <span data-ttu-id="f3f1b-124">Niveau de service De base</span><span class="sxs-lookup"><span data-stu-id="f3f1b-124">Basic service tier</span></span>         | <span data-ttu-id="f3f1b-125">100 unités de calcul</span><span class="sxs-lookup"><span data-stu-id="f3f1b-125">100 Compute Units</span></span> |
| <span data-ttu-id="f3f1b-126">Niveau de service Standard</span><span class="sxs-lookup"><span data-stu-id="f3f1b-126">Standard service tier</span></span>      | <span data-ttu-id="f3f1b-127">800 unités de calcul</span><span class="sxs-lookup"><span data-stu-id="f3f1b-127">800 Compute Units</span></span> |
| <span data-ttu-id="f3f1b-128">**Volume maximal de stockage**</span><span class="sxs-lookup"><span data-stu-id="f3f1b-128">**Max storage**</span></span>            |                   |
| <span data-ttu-id="f3f1b-129">Niveau de service De base</span><span class="sxs-lookup"><span data-stu-id="f3f1b-129">Basic service tier</span></span>         | <span data-ttu-id="f3f1b-130">1 To</span><span class="sxs-lookup"><span data-stu-id="f3f1b-130">1 TB</span></span>              |
| <span data-ttu-id="f3f1b-131">Niveau de service Standard</span><span class="sxs-lookup"><span data-stu-id="f3f1b-131">Standard service tier</span></span>      | <span data-ttu-id="f3f1b-132">1 To</span><span class="sxs-lookup"><span data-stu-id="f3f1b-132">1 TB</span></span>              |

<span data-ttu-id="f3f1b-133">Lorsque de trop nombreuses connexions sont atteints, hello l’erreur suivante peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="f3f1b-133">When too many connections are reached, you may receive hello following error:</span></span>
> <span data-ttu-id="f3f1b-134">ERROR 1040 (08004): Too many connections</span><span class="sxs-lookup"><span data-stu-id="f3f1b-134">ERROR 1040 (08004): Too many connections</span></span>

## <a name="preview-functional-limitations"></a><span data-ttu-id="f3f1b-135">Limitations fonctionnelles de la préversion :</span><span class="sxs-lookup"><span data-stu-id="f3f1b-135">Preview functional limitations:</span></span>
### <a name="scale-operations"></a><span data-ttu-id="f3f1b-136">Opérations de mise à l’échelle :</span><span class="sxs-lookup"><span data-stu-id="f3f1b-136">Scale operations:</span></span>
1.  <span data-ttu-id="f3f1b-137">La mise à l’échelle dynamique de serveurs sur différents niveaux de service n’est pas prise en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-137">Dynamic scaling of servers across service tiers is currently not supported.</span></span> <span data-ttu-id="f3f1b-138">Autrement dit, il n’est pas possible de basculer entre les niveaux de service De base et Standard.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-138">That is, switching between Basic and Standard service tiers.</span></span>
2.  <span data-ttu-id="f3f1b-139">L’augmentation dynamique de la demande de stockage sur un serveur créé au préalable n’est pas prise en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-139">Dynamic on-demand increase of storage on pre-created server is currently not supported.</span></span>
3.  <span data-ttu-id="f3f1b-140">La diminution de la taille de stockage du serveur n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-140">Decreasing server storage size is not supported.</span></span>

### <a name="server-version-upgrades"></a><span data-ttu-id="f3f1b-141">Mise à niveau de la version du serveur :</span><span class="sxs-lookup"><span data-stu-id="f3f1b-141">Server version upgrades:</span></span>
- <span data-ttu-id="f3f1b-142">La migration automatique entre les versions principales du moteur de base de données n’est pas prise en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-142">Automated migration between major database engine versions is currently not supported.</span></span>

### <a name="subscription-management"></a><span data-ttu-id="f3f1b-143">Gestion des abonnements :</span><span class="sxs-lookup"><span data-stu-id="f3f1b-143">Subscription management:</span></span>
- <span data-ttu-id="f3f1b-144">Le déplacement dynamique de serveurs créés au préalable entre les groupes de ressources et d’abonnements n’est pas pris en charge pour le moment.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-144">Dynamically moving pre-created servers across subscription and resource group is currently not supported.</span></span>

### <a name="point-in-time-restore"></a><span data-ttu-id="f3f1b-145">Limite de restauration dans le temps :</span><span class="sxs-lookup"><span data-stu-id="f3f1b-145">Point-in-time-restore:</span></span>
1.  <span data-ttu-id="f3f1b-146">La restauration de niveau de service toodifferent et/ou la taille des unités de calcul et de stockage n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-146">Restoring toodifferent service tier and/or Compute Units and Storage size is not allowed.</span></span>
2.  <span data-ttu-id="f3f1b-147">La restauration d’un serveur supprimé n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="f3f1b-147">Restoring a dropped server is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3f1b-148">Étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3f1b-148">Next Steps:</span></span>
<span data-ttu-id="f3f1b-149">[Éléments disponibles dans chaque niveau de service](concepts-service-tiers.md)
[Versions de bases de données MySQL prises en charge](concepts-supported-versions.md)</span><span class="sxs-lookup"><span data-stu-id="f3f1b-149">[What’s available in each service tier](concepts-service-tiers.md)
[Supported MySQL Database Versions](concepts-supported-versions.md)</span></span>
