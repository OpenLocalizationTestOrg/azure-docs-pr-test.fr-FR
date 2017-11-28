---
title: aaaTroubleshoot Azure RBAC. | Documents Microsoft
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
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a><span data-ttu-id="40da6-103">Résolution des problèmes de contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="40da6-103">Role-Based Access Control troubleshooting</span></span>

<span data-ttu-id="40da6-104">Cet article de document répond aux questions courantes sur les droits d’accès spécifiques hello qui sont accordées aux rôles, afin que vous sachiez quels tooexpect lorsque vous utilisez hello rôles Bonjour portail Azure et peut résoudre les problèmes d’accès.</span><span class="sxs-lookup"><span data-stu-id="40da6-104">This document article answers common questions about hello specific access rights that are granted with roles, so that you know what tooexpect when using hello roles in hello Azure portal and can troubleshoot access problems.</span></span> <span data-ttu-id="40da6-105">Ces trois rôles couvrent tous les types de ressources :</span><span class="sxs-lookup"><span data-stu-id="40da6-105">These three roles cover all resource types:</span></span>

* <span data-ttu-id="40da6-106">Propriétaire</span><span class="sxs-lookup"><span data-stu-id="40da6-106">Owner</span></span>  
* <span data-ttu-id="40da6-107">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="40da6-107">Contributor</span></span>  
* <span data-ttu-id="40da6-108">Lecteur</span><span class="sxs-lookup"><span data-stu-id="40da6-108">Reader</span></span>  

<span data-ttu-id="40da6-109">Propriétaires et contributeurs ont toohello gestion de l’accès complet à rencontrer, mais un collaborateur ne peut pas donner accès tooother utilisateurs ou groupes.</span><span class="sxs-lookup"><span data-stu-id="40da6-109">Owners and contributors both have full access toohello management experience, but a contributor can’t give access tooother users or groups.</span></span> <span data-ttu-id="40da6-110">Choses un peu plus intéressantes avec le rôle de lecteur hello, qui est où nous allons passer du temps.</span><span class="sxs-lookup"><span data-stu-id="40da6-110">Things get a little more interesting with hello reader role, so that’s where we'll spend some time.</span></span> <span data-ttu-id="40da6-111">Consultez hello [article de get-started Role-Based Access Control](role-based-access-control-configure.md) pour plus d’informations sur comment accéder à toogrant.</span><span class="sxs-lookup"><span data-stu-id="40da6-111">See hello [Role-Based Access Control get-started article](role-based-access-control-configure.md) for details on how toogrant access.</span></span>

## <a name="app-service-workloads"></a><span data-ttu-id="40da6-112">Charges de travail App Service</span><span class="sxs-lookup"><span data-stu-id="40da6-112">App service workloads</span></span>
### <a name="write-access-capabilities"></a><span data-ttu-id="40da6-113">Fonctionnalités d’accès en écriture</span><span class="sxs-lookup"><span data-stu-id="40da6-113">Write access capabilities</span></span>
<span data-ttu-id="40da6-114">Si vous accordez une accès en lecture seule utilisateur tooa. application web unique, certaines fonctionnalités sont désactivées, que vous ne pouvez pas attendre.</span><span class="sxs-lookup"><span data-stu-id="40da6-114">If you grant a user read-only access tooa single web app, some features are disabled that you might not expect.</span></span> <span data-ttu-id="40da6-115">Hello suivant les fonctionnalités de gestion requièrent **écrire** accéder à l’application web tooa (Contributeur ou propriétaire) et ne sont pas disponibles pour tous les scénarios en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="40da6-115">hello following management capabilities require **write** access tooa web app (either Contributor or Owner), and aren’t available in any read-only scenario.</span></span>

* <span data-ttu-id="40da6-116">Commandes (comme start, stop, etc.)</span><span class="sxs-lookup"><span data-stu-id="40da6-116">Commands (like start, stop, etc.)</span></span>
* <span data-ttu-id="40da6-117">Modification de paramètres tels que la configuration générale, les paramètres de mise à l’échelle, les paramètres de sauvegarde et les paramètres d’analyse</span><span class="sxs-lookup"><span data-stu-id="40da6-117">Changing settings like general configuration, scale settings, backup settings, and monitoring settings</span></span>
* <span data-ttu-id="40da6-118">Accès aux informations d’identification de publication et autres informations secrètes, telles que les paramètres d’application et les chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="40da6-118">Accessing publishing credentials and other secrets like app settings and connection strings</span></span>
* <span data-ttu-id="40da6-119">Diffusion de journaux</span><span class="sxs-lookup"><span data-stu-id="40da6-119">Streaming logs</span></span>
* <span data-ttu-id="40da6-120">Configuration des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="40da6-120">Diagnostic logs configuration</span></span>
* <span data-ttu-id="40da6-121">Console (invite de commandes)</span><span class="sxs-lookup"><span data-stu-id="40da6-121">Console (command prompt)</span></span>
* <span data-ttu-id="40da6-122">Déploiements actifs et récents (pour le déploiement continu Git local)</span><span class="sxs-lookup"><span data-stu-id="40da6-122">Active and recent deployments (for local git continuous deployment)</span></span>
* <span data-ttu-id="40da6-123">Estimation de dépense</span><span class="sxs-lookup"><span data-stu-id="40da6-123">Estimated spend</span></span>
* <span data-ttu-id="40da6-124">Tests web</span><span class="sxs-lookup"><span data-stu-id="40da6-124">Web tests</span></span>
* <span data-ttu-id="40da6-125">Réseau virtuel (uniquement visible tooa lecteur si un réseau virtuel a déjà été configuré par un utilisateur avec accès en écriture).</span><span class="sxs-lookup"><span data-stu-id="40da6-125">Virtual network (only visible tooa reader if a virtual network has previously been configured by a user with write access).</span></span>

<span data-ttu-id="40da6-126">Si vous ne peut pas accéder à un de ces vignettes, vous devez tooask votre administrateur pour l’application web de collaborateur accès toohello.</span><span class="sxs-lookup"><span data-stu-id="40da6-126">If you can't access any of these tiles, you need tooask your administrator for Contributor access toohello web app.</span></span>

### <a name="dealing-with-related-resources"></a><span data-ttu-id="40da6-127">Gestion des ressources connexes</span><span class="sxs-lookup"><span data-stu-id="40da6-127">Dealing with related resources</span></span>
<span data-ttu-id="40da6-128">Les applications Web sont compliquées par présence hello de quelques différentes ressources qui interaction.</span><span class="sxs-lookup"><span data-stu-id="40da6-128">Web apps are complicated by hello presence of a few different resources that interplay.</span></span> <span data-ttu-id="40da6-129">Voici un groupe de ressources classique avec deux sites web :</span><span class="sxs-lookup"><span data-stu-id="40da6-129">Here is a typical resource group with a couple websites:</span></span>

![Groupe de ressources d'application web](./media/role-based-access-control-troubleshooting/website-resource-model.png)

<span data-ttu-id="40da6-131">Par conséquent, si vous accordez l’accès toojust hello web app, une grande partie de la fonctionnalité hello sur Panneau du site Web de hello Bonjour portail Azure est désactivée.</span><span class="sxs-lookup"><span data-stu-id="40da6-131">As a result, if you grant someone access toojust hello web app, much of hello functionality on hello website blade in hello Azure portal is disabled.</span></span>

<span data-ttu-id="40da6-132">Ces éléments nécessitent **écrire** accéder toohello **plan App Service** qui correspond le site Web de tooyour :</span><span class="sxs-lookup"><span data-stu-id="40da6-132">These items require **write** access toohello **App Service plan** that corresponds tooyour website:</span></span>  

* <span data-ttu-id="40da6-133">L’application web affichage hello de tarification (gratuit ou Standard)</span><span class="sxs-lookup"><span data-stu-id="40da6-133">Viewing hello web app’s pricing tier (Free or Standard)</span></span>  
* <span data-ttu-id="40da6-134">Configuration de mise à l'échelle (le nombre d'instances, la taille de la machine virtuelle, les paramètres de mise à l'échelle automatique)</span><span class="sxs-lookup"><span data-stu-id="40da6-134">Scale configuration (number of instances, virtual machine size, autoscale settings)</span></span>  
* <span data-ttu-id="40da6-135">Quotas (stockage, bande passante, UC)</span><span class="sxs-lookup"><span data-stu-id="40da6-135">Quotas (storage, bandwidth, CPU)</span></span>  

<span data-ttu-id="40da6-136">Ces éléments nécessitent **écrire** toohello accès entier **groupe de ressources** qui contient votre site Web :</span><span class="sxs-lookup"><span data-stu-id="40da6-136">These items require **write** access toohello whole **Resource group** that contains your website:</span></span>  

* <span data-ttu-id="40da6-137">Certificats SSL et liaisons (certificats SSL peuvent être partagées entre les sites de hello même groupe de ressources et l’emplacement géographique)</span><span class="sxs-lookup"><span data-stu-id="40da6-137">SSL Certificates and bindings (SSL certificates can be shared between sites in hello same resource group and geo-location)</span></span>  
* <span data-ttu-id="40da6-138">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="40da6-138">Alert rules</span></span>  
* <span data-ttu-id="40da6-139">Paramètres de mise à l'échelle automatique</span><span class="sxs-lookup"><span data-stu-id="40da6-139">Autoscale settings</span></span>  
* <span data-ttu-id="40da6-140">Composants Application Insights</span><span class="sxs-lookup"><span data-stu-id="40da6-140">Application insights components</span></span>  
* <span data-ttu-id="40da6-141">Tests web</span><span class="sxs-lookup"><span data-stu-id="40da6-141">Web tests</span></span>  

## <a name="virtual-machine-workloads"></a><span data-ttu-id="40da6-142">Charges de travail des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="40da6-142">Virtual machine workloads</span></span>
<span data-ttu-id="40da6-143">Beaucoup comme avec les applications web, certaines fonctionnalités dans le panneau de machine virtuelle hello requièrent un accès en écriture toohello virtual machine ou tooother ressources hello groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="40da6-143">Much like with web apps, some features on hello virtual machine blade require write access toohello virtual machine, or tooother resources in hello resource group.</span></span>

<span data-ttu-id="40da6-144">Machines virtuelles sont associées tooDomain noms, les réseaux virtuels, les comptes de stockage et les règles d’alerte.</span><span class="sxs-lookup"><span data-stu-id="40da6-144">Virtual machines are related tooDomain names, virtual networks, storage accounts, and alert rules.</span></span>

<span data-ttu-id="40da6-145">Ces éléments nécessitent **écrire** accéder toohello **machine virtuelle**:</span><span class="sxs-lookup"><span data-stu-id="40da6-145">These items require **write** access toohello **Virtual machine**:</span></span>

* <span data-ttu-id="40da6-146">Points de terminaison</span><span class="sxs-lookup"><span data-stu-id="40da6-146">Endpoints</span></span>  
* <span data-ttu-id="40da6-147">Adresses IP</span><span class="sxs-lookup"><span data-stu-id="40da6-147">IP addresses</span></span>  
* <span data-ttu-id="40da6-148">Disques</span><span class="sxs-lookup"><span data-stu-id="40da6-148">Disks</span></span>  
* <span data-ttu-id="40da6-149">Extensions</span><span class="sxs-lookup"><span data-stu-id="40da6-149">Extensions</span></span>  

<span data-ttu-id="40da6-150">Ces cubes nécessitent **écrire** hello de tooboth accès **machine virtuelle**et hello **groupe de ressources** (ainsi que le nom de domaine hello) qu’il est dans :</span><span class="sxs-lookup"><span data-stu-id="40da6-150">These require **write** access tooboth hello **Virtual machine**, and hello **Resource group** (along with hello Domain name) that it is in:</span></span>  

* <span data-ttu-id="40da6-151">Groupe à haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="40da6-151">Availability set</span></span>  
* <span data-ttu-id="40da6-152">Jeu d'équilibrage de la charge</span><span class="sxs-lookup"><span data-stu-id="40da6-152">Load balanced set</span></span>  
* <span data-ttu-id="40da6-153">Règles d'alerte</span><span class="sxs-lookup"><span data-stu-id="40da6-153">Alert rules</span></span>  

<span data-ttu-id="40da6-154">Si vous ne peut pas accéder à un de ces vignettes, demandez à votre administrateur pour le groupe de ressources de collaborateur accès toohello.</span><span class="sxs-lookup"><span data-stu-id="40da6-154">If you can't access any of these tiles, ask your administrator for Contributor access toohello Resource group.</span></span>

## <a name="see-more"></a><span data-ttu-id="40da6-155">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="40da6-155">See more</span></span>
* <span data-ttu-id="40da6-156">[Contrôle d’accès basé sur rôle](role-based-access-control-configure.md): prise en main RBAC Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="40da6-156">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="40da6-157">[Rôles intégrés](role-based-access-built-in-roles.md): obtenir des informations sur les rôles hello livrés dans RBAC.</span><span class="sxs-lookup"><span data-stu-id="40da6-157">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
* <span data-ttu-id="40da6-158">[Les rôles personnalisés dans Azure RBAC](role-based-access-control-custom-roles.md): Découvrez comment toocreate des rôles personnalisés toofit doit votre accès.</span><span class="sxs-lookup"><span data-stu-id="40da6-158">[Custom roles in Azure RBAC](role-based-access-control-custom-roles.md): Learn how toocreate custom roles toofit your access needs.</span></span>
* <span data-ttu-id="40da6-159">[Créer un rapport d’historique des modifications d’accès](role-based-access-control-access-change-history-report.md): effectuez le suivi des changements d’affection de rôle dans RBAC.</span><span class="sxs-lookup"><span data-stu-id="40da6-159">[Create an access change history report](role-based-access-control-access-change-history-report.md): Keep track of changing role assignments in RBAC.</span></span>

