---
title: adresses de gestion aaaAzure environnement App Service
description: "Listes des adresses de gestion hello utilisé toocommand un environnement App Service"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="3c56c-103">Adresses de gestion App Service Environment</span><span class="sxs-lookup"><span data-stu-id="3c56c-103">App Service Environment management addresses</span></span>

<span data-ttu-id="3c56c-104">Hello Environment(ASE) de Service d’application est un déploiement de hello du Service d’applications Azure dans un sous-réseau dans votre réseau virtuel de Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="3c56c-104">hello App Service Environment(ASE) is a deployment of hello Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="3c56c-105">Hello ASE doit être accessible à partir de hello Azure App Service afin qu’il puisse être géré.</span><span class="sxs-lookup"><span data-stu-id="3c56c-105">hello ASE must be accessible from hello Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="3c56c-106">Ce trafic de gestion ASE parcourt le réseau géré par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="3c56c-106">This ASE management traffic traverses hello user controlled network.</span></span>  <span data-ttu-id="3c56c-107">Il provient du Service d’applications Azure Gestion serveurs toohello adresse VIP publique qui est associé à hello ASE.</span><span class="sxs-lookup"><span data-stu-id="3c56c-107">It comes from Azure App Service management servers toohello public VIP that is associated with hello ASE.</span></span>  <span data-ttu-id="3c56c-108">Pour plus d’informations sur hello ASE mise en réseau de dépendances lire [hello environnement App Service et les considérations relatives à la mise en réseau][networking].</span><span class="sxs-lookup"><span data-stu-id="3c56c-108">For details on hello ASE networking dependencies read [Networking considerations and hello App Service Environment][networking].</span></span>  <span data-ttu-id="3c56c-109">Pour des informations générales sur hello ASE, vous pouvez démarrer avec [Introduction toohello environnement App Service][intro].</span><span class="sxs-lookup"><span data-stu-id="3c56c-109">For general information on hello ASE you can start with [Introduction toohello App Service Environment][intro].</span></span>

<span data-ttu-id="3c56c-110">Ce document répertorie les adresses IP de source de hello pour le trafic de gestion toohello ASE.</span><span class="sxs-lookup"><span data-stu-id="3c56c-110">This document lists hello source IPs for management traffic toohello ASE.</span></span> <span data-ttu-id="3c56c-111">Vous pouvez utiliser ces toolock de groupes de sécurité réseau toocreate adresses vers le bas le trafic entrant ou les utiliser dans les Tables d’itinéraires en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="3c56c-111">You can use these addresses toocreate Network Security Groups toolock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="3c56c-112">toouse ces informations, vous devez toouse :</span><span class="sxs-lookup"><span data-stu-id="3c56c-112">toouse this information you need toouse:</span></span>

* <span data-ttu-id="3c56c-113">adresses IP Hello répertoriés pour toutes les régions</span><span class="sxs-lookup"><span data-stu-id="3c56c-113">hello IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="3c56c-114">cette région toohello de correspondance que votre ASE est déployé dans des adresses IP de Hello.</span><span class="sxs-lookup"><span data-stu-id="3c56c-114">hello IP addresses that match toohello region that your ASE is deployed into.</span></span>

<span data-ttu-id="3c56c-115">le trafic de gestion entrants Hello proviennent ces adresses IP tooports 454 et 455.</span><span class="sxs-lookup"><span data-stu-id="3c56c-115">hello incoming management traffic comes in from these IP addresses tooports 454 and 455.</span></span>

| <span data-ttu-id="3c56c-116">Région</span><span class="sxs-lookup"><span data-stu-id="3c56c-116">Region</span></span> | <span data-ttu-id="3c56c-117">Adresses</span><span class="sxs-lookup"><span data-stu-id="3c56c-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="3c56c-118">Toutes les régions</span><span class="sxs-lookup"><span data-stu-id="3c56c-118">All regions</span></span> | <span data-ttu-id="3c56c-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="3c56c-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="3c56c-120">Centre Sud et Centre Nord des États-Unis</span><span class="sxs-lookup"><span data-stu-id="3c56c-120">South Central US & North Central US</span></span> | <span data-ttu-id="3c56c-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="3c56c-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="3c56c-122">Sud-Est de l’Australie et Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="3c56c-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="3c56c-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="3c56c-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="3c56c-124">Ouest des États-Unis et Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="3c56c-124">US West & US East</span></span> | <span data-ttu-id="3c56c-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="3c56c-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="3c56c-126">Europe de l’Ouest et Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="3c56c-126">West Europe & North Europe</span></span> | <span data-ttu-id="3c56c-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="3c56c-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="3c56c-128">Centre Ouest des États-Unis et Ouest des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="3c56c-128">West Central US & West US 2</span></span> | <span data-ttu-id="3c56c-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="3c56c-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="3c56c-130">Centre des États-Unis et Est des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="3c56c-130">Central US & East US 2</span></span> | <span data-ttu-id="3c56c-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="3c56c-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="3c56c-132">Asie orientale et Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="3c56c-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="3c56c-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="3c56c-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="3c56c-134">Est du Japon et Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="3c56c-134">Japan East & Japan West</span></span> | <span data-ttu-id="3c56c-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="3c56c-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="3c56c-136">Centre du Canada et Est du Canada</span><span class="sxs-lookup"><span data-stu-id="3c56c-136">Canada Central & Canada East</span></span> | <span data-ttu-id="3c56c-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="3c56c-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="3c56c-138">Ouest du Royaume-Uni et Sud du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="3c56c-138">UK West & UK South</span></span> | <span data-ttu-id="3c56c-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="3c56c-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="3c56c-140">Corée du Sud et Centre de la Corée</span><span class="sxs-lookup"><span data-stu-id="3c56c-140">Korea South & Korea Central</span></span> | <span data-ttu-id="3c56c-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="3c56c-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="3c56c-142">Sud du Brésil et Centre Sud des États-Unis</span><span class="sxs-lookup"><span data-stu-id="3c56c-142">Brazil South & South Central US</span></span>| <span data-ttu-id="3c56c-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="3c56c-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="3c56c-144">Inde centrale et Inde du Sud</span><span class="sxs-lookup"><span data-stu-id="3c56c-144">Central India & South India</span></span> | <span data-ttu-id="3c56c-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="3c56c-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="3c56c-146">Inde-Ouest et Inde-Sud</span><span class="sxs-lookup"><span data-stu-id="3c56c-146">West India & South India</span></span> | <span data-ttu-id="3c56c-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="3c56c-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
