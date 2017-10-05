---
title: "Résoudre les problèmes d’Azure RBAC | Microsoft Docs"
description: "Obtenez de l’aide en cas de problèmes ou de questions concernant les ressources de contrôle d’accès en fonction du rôle."
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 407c030ea159915d4d7ac21760a3d17ec2204372
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="03293-103">Résolution des problèmes de contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="03293-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="03293-104">Cet article répond aux questions courantes sur les droits d’accès spécifiques qui sont accordés aux rôles, afin que vous sachiez à quoi vous attendre lorsque vous utilisez les rôles sur le Portail Azure et que vous puissiez résoudre les problèmes d’accès.</span><span class="sxs-lookup"><span data-stu-id="03293-104">This document article answers common questions about the specific access rights that are granted with roles, so that you know what to expect when using the roles in the Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="03293-105">Ces trois rôles couvrent tous les types de ressources :</span><span class="sxs-lookup"><span data-stu-id="03293-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="03293-106">Propriétaire</span><span class="sxs-lookup"><span data-stu-id="03293-106">Owner</span></span>  
* <span data-ttu-id="03293-107">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="03293-107">Contributor</span></span>  
* <span data-ttu-id="03293-108">Lecteur</span><span class="sxs-lookup"><span data-stu-id="03293-108">Reader</span></span>  

<span data-ttu-id="03293-109">Les propriétaires et collaborateurs disposent tous les deux d’un accès complet à toutes les opérations de gestion, mais un collaborateur ne peut pas accorder d’accès à d’autres utilisateurs ou groupes.</span><span class="sxs-lookup"><span data-stu-id="03293-109">Owners and contributors both have full access to the management experience, but a contributor can’t give access to other users or groups.</span></span> <span data-ttu-id="03293-110">La situation du rôle de lecteur est un peu plus intéressante, et nous allons nous y attarder.</span><span class="sxs-lookup"><span data-stu-id="03293-110">Things get a little more interesting with the reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="03293-111">Consultez l’ [article Prise en main du contrôle d’accès en fonction du rôle](role-based-access-control-configure.md) pour plus d’informations sur la façon d’octroyer l’accès.</span><span class="sxs-lookup"><span data-stu-id="03293-111">See the [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how to grant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="03293-112">Charges de travail App Service</span><span class="sxs-lookup"><span data-stu-id="03293-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="03293-113">Fonctionnalités d’accès en écriture</span><span class="sxs-lookup"><span data-stu-id="03293-113">Write access capabilities</span></span>
<span data-ttu-id="03293-114">Si vous accordez un accès utilisateur en lecture seule à une seule application web, certaines fonctionnalités sont désactivées, ce que vous n’avez peut-être pas prévu.</span><span class="sxs-lookup"><span data-stu-id="03293-114">If you grant a user read-only access to a single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="03293-115">Les fonctionnalités de gestion suivantes exigent un accès en **écriture** à une application web (Collaborateur ou Propriétaire) et ne sont pas disponibles en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="03293-115">The following management capabilities require **write** access to a web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="03293-116">Commandes (comme start, stop, etc.)</span><span class="sxs-lookup"><span data-stu-id="03293-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="03293-117">Modification de paramètres tels que la configuration générale, les paramètres de mise à l’échelle, les paramètres de sauvegarde et les paramètres d’analyse</span><span class="sxs-lookup"><span data-stu-id="03293-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="03293-118">Accès aux informations d’identification de publication et autres informations secrètes, telles que les paramètres d’application et les chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="03293-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="03293-119">Diffusion de journaux</span><span class="sxs-lookup"><span data-stu-id="03293-119">Streaming logs</span></span>
* <span data-ttu-id="03293-120">Configuration des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="03293-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="03293-121">Console (invite de commandes)</span><span class="sxs-lookup"><span data-stu-id="03293-121">Console (command prompt)</span></span>
* <span data-ttu-id="03293-122">Déploiements actifs et récents (pour le déploiement continu Git local)</span><span class="sxs-lookup"><span data-stu-id="03293-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="03293-123">Estimation de dépense</span><span class="sxs-lookup"><span data-stu-id="03293-123">Estimated spend</span></span>
* <span data-ttu-id="03293-124">Tests web</span><span class="sxs-lookup"><span data-stu-id="03293-124">Web tests</span></span>
* <span data-ttu-id="03293-125">Réseau virtuel (accessible à un lecteur uniquement si un réseau virtuel a été précédemment configuré par un utilisateur avec accès en écriture).</span><span class="sxs-lookup"><span data-stu-id="03293-125">Virtual network (only visible to a reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="03293-126">Si vous ne pouvez accéder à aucune de ces vignettes, vous devez obtenir l’accès Collaborateur à l’application web auprès de votre administrateur.</span><span class="sxs-lookup"><span data-stu-id="03293-126">If you can't access any of these tiles, you need to ask your administrator for Contributor access to the web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="03293-127">Gestion des ressources connexes</span><span class="sxs-lookup"><span data-stu-id="03293-127">Dealing with related resources</span></span>
<span data-ttu-id="03293-128">Les applications web sont compliqués par la présence de quelques ressources différentes qui interagissent.</span><span class="sxs-lookup"><span data-stu-id="03293-128">Web apps are complicated by the presence of a few different resources that interplay.</span></span> <span data-ttu-id="03293-129">Voici un groupe de ressources classique avec deux sites web :</span><span class="sxs-lookup"><span data-stu-id="03293-129">Here is a typical resource group with a couple websites:</span></span>

![Groupe de ressources d'application web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="03293-131">En conséquence, si vous accordez à un utilisateur le seul accès à l’application web, la plupart des fonctionnalités du volet Site web dans le portail Azure sont désactivées.</span><span class="sxs-lookup"><span data-stu-id="03293-131">As a result, if you grant someone access to just the web app, much of the functionality on the website blade in the Azure portal is disabled.</span></span>

<span data-ttu-id="03293-132">Les éléments suivants requièrent l’accès **en écriture** au **plan App Service** qui correspond à votre site web :</span><span class="sxs-lookup"><span data-stu-id="03293-132">These items require **write** access to the **App Service plan** that corresponds to your website:</span></span>  

* <span data-ttu-id="03293-133">Affichage du niveau de tarification de l'application web (Gratuit ou Standard)</span><span class="sxs-lookup"><span data-stu-id="03293-133">Viewing the web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="03293-134">Configuration de mise à l'échelle (le nombre d'instances, la taille de la machine virtuelle, les paramètres de mise à l'échelle automatique)</span><span class="sxs-lookup"><span data-stu-id="03293-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="03293-135">Quotas (stockage, bande passante, UC)</span><span class="sxs-lookup"><span data-stu-id="03293-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="03293-136">Les éléments suivants requièrent l’accès **en écriture** à l’ensemble du **Groupe de ressources** qui contient le site web :</span><span class="sxs-lookup"><span data-stu-id="03293-136">These items require **write** access to the whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="03293-137">Certificats et liaisons SSL (les certificats SSL peuvent être partagés entre différents sites dans le même groupe de ressources et emplacement)</span><span class="sxs-lookup"><span data-stu-id="03293-137">SSL Certificates and bindings (SSL certificates can be shared between sites in the same resource group and geo-location)</span></span>  
* <span data-ttu-id="03293-138">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="03293-138">Alert rules</span></span>  
* <span data-ttu-id="03293-139">Paramètres de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="03293-139">Autoscale settings</span></span>  
* <span data-ttu-id="03293-140">Composants Application Insights</span><span class="sxs-lookup"><span data-stu-id="03293-140">Application insights components</span></span>  
* <span data-ttu-id="03293-141">Tests web</span><span class="sxs-lookup"><span data-stu-id="03293-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="03293-142">Charges de travail des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="03293-142">Virtual machine workloads</span></span>
<span data-ttu-id="03293-143">Comme pour les applications web, certaines fonctionnalités du volet de la machine virtuelle exigent un accès en écriture à la machine virtuelle ou à d'autres ressources du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="03293-143">Much like with web apps, some features on the virtual machine blade require write access to the virtual machine, or to other resources in the resource group.</span></span>

<span data-ttu-id="03293-144">Les machines virtuelles sont associées aux noms de domaine, réseaux virtuels, comptes de stockage et règles d'alerte.</span><span class="sxs-lookup"><span data-stu-id="03293-144">Virtual machines are related to Domain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="03293-145">Les éléments suivants requièrent l’accès **en écriture** à la **machine virtuelle** :</span><span class="sxs-lookup"><span data-stu-id="03293-145">These items require **write** access to the **Virtual machine**:</span></span>

* <span data-ttu-id="03293-146">Points de terminaison</span><span class="sxs-lookup"><span data-stu-id="03293-146">Endpoints</span></span>  
* <span data-ttu-id="03293-147">Adresses IP</span><span class="sxs-lookup"><span data-stu-id="03293-147">IP addresses</span></span>  
* <span data-ttu-id="03293-148">Disques</span><span class="sxs-lookup"><span data-stu-id="03293-148">Disks</span></span>  
* <span data-ttu-id="03293-149">Extensions</span><span class="sxs-lookup"><span data-stu-id="03293-149">Extensions</span></span>  

<span data-ttu-id="03293-150">Les éléments suivants requièrent l’accès **en écriture** à la **machine virtuelle**, ainsi qu’au **Groupe de ressources** (avec le nom de domaine) auxquels ils appartiennent :</span><span class="sxs-lookup"><span data-stu-id="03293-150">These require **write** access to both the **Virtual machine**, and the **Resource group** (along with the Domain name) that it is in:</span></span>  

* <span data-ttu-id="03293-151">Groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="03293-151">Availability set</span></span>  
* <span data-ttu-id="03293-152">Jeu d'équilibrage de la charge</span><span class="sxs-lookup"><span data-stu-id="03293-152">Load balanced set</span></span>  
* <span data-ttu-id="03293-153">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="03293-153">Alert rules</span></span>  

<span data-ttu-id="03293-154">Si vous ne pouvez accéder à aucune de ces vignettes, demandez l’accès Collaborateur au groupe de ressources à votre administrateur.</span><span class="sxs-lookup"><span data-stu-id="03293-154">If you can't access any of these tiles, ask your administrator for Contributor access to the Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="03293-155">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="03293-155">See more</span></span>
* <span data-ttu-id="03293-156">[Contrôle d’accès en fonction du rôle Azure](role-based-access-control-configure.md): découvrez le Contrôle d’accès en fonction du rôle Azure dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="03293-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="03293-157">[Rôles intégrés](role-based-access-built-in-roles.md): obtenez des informations sur les rôles qui livrés en standard dans RBAC.</span><span class="sxs-lookup"><span data-stu-id="03293-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>
* <span data-ttu-id="03293-158">[Rôles personnalisés dans le contrôle d’accès en fonction du rôle (RBAC) Azure](role-based-access-control-custom-roles.md): découvrez comment créer des rôles personnalisés selon vos besoins d'accès.</span><span class="sxs-lookup"><span data-stu-id="03293-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how to create custom roles to fit your access needs.</span></span>
* <span data-ttu-id="03293-159">[Créer un rapport d’historique des modifications d’accès](role-based-access-control-access-change-history-report.md): effectuez le suivi des changements d'affection de rôle dans RBAC.</span><span class="sxs-lookup"><span data-stu-id="03293-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

