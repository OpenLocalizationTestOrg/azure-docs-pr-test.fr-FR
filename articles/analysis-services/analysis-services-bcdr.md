---
title: "Haute disponibilité Azure Analysis Services | Microsoft Docs"
description: "Garantissez la haute disponibilité Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 84b4c59bac1feeb8611b3a8d783d093ba073e532
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="81331-103">Haute disponibilité Analysis Services</span><span class="sxs-lookup"><span data-stu-id="81331-103">Analysis Services high availability</span></span>
<span data-ttu-id="81331-104">Cet article décrit la garantie d’une haute disponibilité pour les serveurs Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="81331-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="81331-105">Garantissez une haute disponibilité au cours d’une interruption de service</span><span class="sxs-lookup"><span data-stu-id="81331-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="81331-106">Bien que le fait soit rare, un centre de données Azure peut subir une panne.</span><span class="sxs-lookup"><span data-stu-id="81331-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="81331-107">En cas de panne, il entraîne une interruption de service qui peut durer de quelques minutes à plusieurs heures.</span><span class="sxs-lookup"><span data-stu-id="81331-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="81331-108">La haute disponibilité est souvent obtenue grâce à la redondance des serveurs.</span><span class="sxs-lookup"><span data-stu-id="81331-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="81331-109">Avec Azure Analysis Services, vous pouvez obtenir une redondance en créant des serveurs secondaires supplémentaires dans une ou plusieurs régions.</span><span class="sxs-lookup"><span data-stu-id="81331-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="81331-110">Lorsque vous créez des serveurs redondants pour garantir la synchronisation des données et des métadonnées sur ces serveurs avec le serveur d’une région hors connexion, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="81331-110">When creating redundant servers, to assure the data and metadata on those servers is in-sync with the server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="81331-111">Déployer des modèles sur des serveurs redondants dans d’autres régions.</span><span class="sxs-lookup"><span data-stu-id="81331-111">Deploy models to redundant servers in other regions.</span></span> <span data-ttu-id="81331-112">Cette méthode requiert le traitement des données sur votre serveur principal et sur les serveurs redondants en parallèle, garantissant ainsi la synchronisation de tous les serveurs.</span><span class="sxs-lookup"><span data-stu-id="81331-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="81331-113">Sauvegardez les bases de données à partir de votre serveur principal et restaurez-les sur des serveurs redondants.</span><span class="sxs-lookup"><span data-stu-id="81331-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="81331-114">Par exemple, vous pouvez automatiser les sauvegardes nocturnes vers le stockage Azure et procéder à la restauration vers d’autres serveurs redondants dans d’autres régions.</span><span class="sxs-lookup"><span data-stu-id="81331-114">For example, you can automate nightly backups to Azure storage, and restore to other redundant servers in other regions.</span></span> 

<span data-ttu-id="81331-115">Dans les deux cas, si votre serveur principal subit une panne, vous devez modifier les chaînes de connexion des clients de rapport afin de vous connecter au serveur dans un autre centre de données régional.</span><span class="sxs-lookup"><span data-stu-id="81331-115">In either case, if your primary server experiences an outage, you must change the connection strings in reporting clients to connect to the server in a different regional datacenter.</span></span> <span data-ttu-id="81331-116">Cette modification doit être envisagée en dernier recours et uniquement en cas de panne très grave du centre de données régional.</span><span class="sxs-lookup"><span data-stu-id="81331-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="81331-117">Il est plus probable qu’une panne du centre de données hébergeant votre serveur principal réapparaisse en ligne avant que vous ne puissiez mettre à jour les connexions sur tous les clients.</span><span class="sxs-lookup"><span data-stu-id="81331-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="81331-118">Informations connexes</span><span class="sxs-lookup"><span data-stu-id="81331-118">Related information</span></span>
<span data-ttu-id="81331-119">[Sauvegarde et restauration](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="81331-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="81331-120">Gérer Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="81331-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

