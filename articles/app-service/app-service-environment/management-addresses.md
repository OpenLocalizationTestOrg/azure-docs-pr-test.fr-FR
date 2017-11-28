---
title: Adresses de gestion Azure App Service Environment
description: "Répertorie les adresses de gestion utilisées pour la commande d’un environnement App Service"
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
ms.openlocfilehash: e97a084772fd16252d925b62498d2e696629a25d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="b7767-103">Adresses de gestion App Service Environment</span><span class="sxs-lookup"><span data-stu-id="b7767-103">App Service Environment management addresses</span></span>

<span data-ttu-id="b7767-104">L’environnement App Service Environment (ASE) est un déploiement du service Azure App Service dans un sous-réseau de votre réseau virtuel Azure.</span><span class="sxs-lookup"><span data-stu-id="b7767-104">The App Service Environment(ASE) is a deployment of the Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="b7767-105">L’ASE doit être accessible à partir du service Azure App Service pour pouvoir être géré.</span><span class="sxs-lookup"><span data-stu-id="b7767-105">The ASE must be accessible from the Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="b7767-106">Ce trafic de gestion ASE parcourt le réseau géré par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b7767-106">This ASE management traffic traverses the user controlled network.</span></span>  <span data-ttu-id="b7767-107">Il provient des serveurs d’administration Azure App Service et arrive à l’adresse IP virtuelle publique associée à l’ASE.</span><span class="sxs-lookup"><span data-stu-id="b7767-107">It comes from Azure App Service management servers to the public VIP that is associated with the ASE.</span></span>  <span data-ttu-id="b7767-108">Pour plus d’informations sur les dépendances de mise en réseau d’un ASE, consultez la page [Considérations relatives à la mise en réseau pour un environnement App Service Environment][networking].</span><span class="sxs-lookup"><span data-stu-id="b7767-108">For details on the ASE networking dependencies read [Networking considerations and the App Service Environment][networking].</span></span>  <span data-ttu-id="b7767-109">Pour des informations générales sur l’ASE, vous pouvez commencer par consulter la page [Présentation de l’environnement App Service Environment][intro].</span><span class="sxs-lookup"><span data-stu-id="b7767-109">For general information on the ASE you can start with [Introduction to the App Service Environment][intro].</span></span>

<span data-ttu-id="b7767-110">Ce document répertorie les adresses IP sources pour le trafic de gestion vers l’ASE.</span><span class="sxs-lookup"><span data-stu-id="b7767-110">This document lists the source IPs for management traffic to the ASE.</span></span> <span data-ttu-id="b7767-111">Vous pouvez utiliser ces adresses afin de créer des groupes de sécurité réseau pour verrouiller le trafic entrant ou les utiliser dans les tables de routage en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="b7767-111">You can use these addresses to create Network Security Groups to lock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="b7767-112">Voici ce dont vous aurez besoin pour utiliser ces informations :</span><span class="sxs-lookup"><span data-stu-id="b7767-112">To use this information you need to use:</span></span>

* <span data-ttu-id="b7767-113">les adresses IP répertoriées pour toutes les régions ;</span><span class="sxs-lookup"><span data-stu-id="b7767-113">the IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="b7767-114">les adresses IP qui correspondent à la région dans laquelle votre ASE est déployé.</span><span class="sxs-lookup"><span data-stu-id="b7767-114">the IP addresses that match to the region that your ASE is deployed into.</span></span>

<span data-ttu-id="b7767-115">Le trafic de gestion entrant arrive de ces adresses IP sur les ports 454 et 455.</span><span class="sxs-lookup"><span data-stu-id="b7767-115">The incoming management traffic comes in from these IP addresses to ports 454 and 455.</span></span>

| <span data-ttu-id="b7767-116">Région</span><span class="sxs-lookup"><span data-stu-id="b7767-116">Region</span></span> | <span data-ttu-id="b7767-117">Adresses</span><span class="sxs-lookup"><span data-stu-id="b7767-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="b7767-118">Toutes les régions</span><span class="sxs-lookup"><span data-stu-id="b7767-118">All regions</span></span> | <span data-ttu-id="b7767-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="b7767-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="b7767-120">Centre Sud et Centre Nord des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b7767-120">South Central US & North Central US</span></span> | <span data-ttu-id="b7767-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="b7767-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="b7767-122">Sud-Est de l’Australie et Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="b7767-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="b7767-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="b7767-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="b7767-124">Ouest des États-Unis et Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b7767-124">US West & US East</span></span> | <span data-ttu-id="b7767-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="b7767-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="b7767-126">Europe de l’Ouest et Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="b7767-126">West Europe & North Europe</span></span> | <span data-ttu-id="b7767-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="b7767-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="b7767-128">Centre Ouest des États-Unis et Ouest des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="b7767-128">West Central US & West US 2</span></span> | <span data-ttu-id="b7767-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="b7767-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="b7767-130">Centre des États-Unis et Est des États-Unis 2</span><span class="sxs-lookup"><span data-stu-id="b7767-130">Central US & East US 2</span></span> | <span data-ttu-id="b7767-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="b7767-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="b7767-132">Asie orientale et Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="b7767-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="b7767-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="b7767-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="b7767-134">Est du Japon et Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="b7767-134">Japan East & Japan West</span></span> | <span data-ttu-id="b7767-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="b7767-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="b7767-136">Centre du Canada et Est du Canada</span><span class="sxs-lookup"><span data-stu-id="b7767-136">Canada Central & Canada East</span></span> | <span data-ttu-id="b7767-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="b7767-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="b7767-138">Ouest du Royaume-Uni et Sud du Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="b7767-138">UK West & UK South</span></span> | <span data-ttu-id="b7767-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="b7767-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="b7767-140">Corée du Sud et Centre de la Corée</span><span class="sxs-lookup"><span data-stu-id="b7767-140">Korea South & Korea Central</span></span> | <span data-ttu-id="b7767-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="b7767-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="b7767-142">Sud du Brésil et Centre Sud des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b7767-142">Brazil South & South Central US</span></span>| <span data-ttu-id="b7767-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="b7767-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="b7767-144">Inde centrale et Inde du Sud</span><span class="sxs-lookup"><span data-stu-id="b7767-144">Central India & South India</span></span> | <span data-ttu-id="b7767-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="b7767-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="b7767-146">Inde-Ouest et Inde-Sud</span><span class="sxs-lookup"><span data-stu-id="b7767-146">West India & South India</span></span> | <span data-ttu-id="b7767-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="b7767-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
