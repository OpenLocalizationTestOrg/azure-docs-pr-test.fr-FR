---
title: "Ressources, rôles et contrôle d’accès dans Azure Application Insights | Microsoft Docs"
description: "Propriétaires, collaborateurs et lecteurs des perspectives de votre organisation."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: c979a8bfbeecacc7c0bbc112e02a4b68e874c219
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="505e0-103">Contrôle d’accès, rôles et ressources dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="505e0-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="505e0-104">Vous pouvez contrôler qui a lu et mis à jour l’accès à vos données dans Azure [Application Insights][start], à l’aide du [Contrôle d’accès basé sur les rôles dans Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="505e0-104">You can control who has read and update access to your data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="505e0-105">Accordez l’accès aux utilisateurs dans le **groupe de ressources ou l’abonnement** auquel appartient votre ressource d’application et non dans la ressource elle-même.</span><span class="sxs-lookup"><span data-stu-id="505e0-105">Assign access to users in the **resource group or subscription** to which your application resource belongs - not in the resource itself.</span></span> <span data-ttu-id="505e0-106">Affectez le rôle de **collaborateur de composants Application Insights** .</span><span class="sxs-lookup"><span data-stu-id="505e0-106">Assign the **Application Insights component contributor** role.</span></span> <span data-ttu-id="505e0-107">Cela garantit un contrôle d’accès uniforme aux tests et aux alertes Web, ainsi qu’aux ressources de votre application.</span><span class="sxs-lookup"><span data-stu-id="505e0-107">This ensures uniform control of access to web tests and alerts along with your application resource.</span></span> <span data-ttu-id="505e0-108">[En savoir plus](#access).</span><span class="sxs-lookup"><span data-stu-id="505e0-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="505e0-109">Ressources, groupes et abonnements</span><span class="sxs-lookup"><span data-stu-id="505e0-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="505e0-110">Quelques définitions pour commencer :</span><span class="sxs-lookup"><span data-stu-id="505e0-110">First, some definitions:</span></span>

* <span data-ttu-id="505e0-111">**Ressource** : une instance d’un service Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="505e0-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="505e0-112">Votre ressource Application Insights collecte, analyse et affiche les données de télémétrie envoyées par votre application.</span><span class="sxs-lookup"><span data-stu-id="505e0-112">Your Application Insights resource collects, analyzes and displays the telemetry data sent from your application.</span></span>  <span data-ttu-id="505e0-113">Les autres types de ressources Azure incluent des applications Web, des bases de données et des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="505e0-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="505e0-114">Pour voir vos ressources, ouvrez le [portail Azure][portal], connectez-vous, puis cliquez sur Toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="505e0-114">To see your resources, open the [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="505e0-115">Pour trouver une ressource, tapez une partie de son nom dans le champ filtre.</span><span class="sxs-lookup"><span data-stu-id="505e0-115">To find a resource, type part of its name in the filter field.</span></span>
  
    ![Liste des ressources Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="505e0-117">[**Groupe de ressources**][group] : chaque ressource appartient à un groupe.</span><span class="sxs-lookup"><span data-stu-id="505e0-117">[**Resource group**][group] - Every resource belongs to one group.</span></span> <span data-ttu-id="505e0-118">Un groupe est un moyen pratique de gérer les ressources apparentées, en particulier pour le contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="505e0-118">A group is a convenient way to manage related resources, particularly for access control.</span></span> <span data-ttu-id="505e0-119">Par exemple, vous pouvez placer dans un groupe de ressources une application Web, une ressource Application Insights pour surveiller l’application et une ressource de stockage pour conserver les données exportées.</span><span class="sxs-lookup"><span data-stu-id="505e0-119">For example, into one resource group you could put a Web App, an Application Insights resource to monitor the app, and a Storage resource to keep exported data.</span></span>

    ![Cliquez sur Parcourir, Groupes de ressources, puis choisissez un groupe](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="505e0-121">[**Abonnement**](https://manage.windowsazure.com) : pour utiliser Application Insights ou d’autres ressources Azure, vous vous connectez à un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="505e0-121">[**Subscription**](https://manage.windowsazure.com) - To use Application Insights or other Azure resources, you sign in to an Azure subscription.</span></span> <span data-ttu-id="505e0-122">Chaque groupe de ressources appartient à un abonnement Azure, où vous choisissez votre package de prix et, s’il s’agit d’un abonnement d’organisation, sélectionnez les membres et leurs autorisations d’accès.</span><span class="sxs-lookup"><span data-stu-id="505e0-122">Every resource group belongs to one Azure subscription, where you choose your price package and, if it's an organization subscription, choose the members and their access permissions.</span></span>
* <span data-ttu-id="505e0-123">[**Compte Microsoft**][account] : le nom d’utilisateur et le mot de passe que vous utilisez pour vous connecter aux abonnements Microsoft Azure, XBox Live, Outlook.com et autres services Microsoft.</span><span class="sxs-lookup"><span data-stu-id="505e0-123">[**Microsoft account**][account] - The username and password that you use to sign in to Microsoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="505e0-124"><a name="access"></a> Contrôle de l’accès dans le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="505e0-124"><a name="access"></a> Control access in the resource group</span></span>
<span data-ttu-id="505e0-125">Il est important de comprendre qu’en plus de la ressource que vous avez créée pour votre application, il existe également des ressources distinctes masquées pour les alertes et les tests Web.</span><span class="sxs-lookup"><span data-stu-id="505e0-125">It's important to understand that in addition to the resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="505e0-126">Elles sont associées au même [groupe de ressources](#resource-group) que votre application.</span><span class="sxs-lookup"><span data-stu-id="505e0-126">They are attached to the same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="505e0-127">Vous pouvez également placer d’autres services Azure ici, comme des sites Web ou du stockage.</span><span class="sxs-lookup"><span data-stu-id="505e0-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Ressources dans Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="505e0-129">Pour contrôler l’accès à ces ressources, il est donc recommandé de :</span><span class="sxs-lookup"><span data-stu-id="505e0-129">To control access to these resources it's therefore recommended to:</span></span>

* <span data-ttu-id="505e0-130">contrôler l’accès au niveau du **groupe de ressources ou de l’abonnement** .</span><span class="sxs-lookup"><span data-stu-id="505e0-130">Control access at the **resource group or subscription** level.</span></span>
* <span data-ttu-id="505e0-131">affecter le rôle de **collaborateur de composants Application Insights** .</span><span class="sxs-lookup"><span data-stu-id="505e0-131">Assign the **Application Insights Component contributor** role to users.</span></span> <span data-ttu-id="505e0-132">Cela leur permet de modifier les tests Web, les alertes et les ressources d’Application Insights, sans donner accès aux autres services dans le groupe.</span><span class="sxs-lookup"><span data-stu-id="505e0-132">This allows them to edit web tests, alerts, and Application Insights resources, without providing access to any other services in the group.</span></span>

## <a name="to-provide-access-to-another-user"></a><span data-ttu-id="505e0-133">Pour fournir l’accès à un autre utilisateur</span><span class="sxs-lookup"><span data-stu-id="505e0-133">To provide access to another user</span></span>
<span data-ttu-id="505e0-134">Vous devez disposer des droits du propriétaire de l’abonnement ou du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="505e0-134">You must have Owner rights to the subscription or the resource group.</span></span>

<span data-ttu-id="505e0-135">L’utilisateur doit avoir un [compte Microsoft][account] ou disposer d’un accès à son [compte professionnel Microsoft](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="505e0-135">The user must have a [Microsoft Account][account], or access to their [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="505e0-136">Vous pouvez fournir l’accès aux personnes et aux groupes d’utilisateurs définis dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="505e0-136">You can provide access to individuals, and also to user groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-to-the-resource-group"></a><span data-ttu-id="505e0-137">Accédez au groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="505e0-137">Navigate to the resource group</span></span>
<span data-ttu-id="505e0-138">Ajoutez l’utilisateur à cet endroit.</span><span class="sxs-lookup"><span data-stu-id="505e0-138">Add the user there.</span></span>

![Dans le panneau de ressources de votre application, ouvrez Essentials, puis le groupe de ressources et sélectionnez Paramètres/Utilisateurs.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="505e0-141">Vous pouvez également monter d’un niveau supplémentaire et ajouter l’utilisateur à l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="505e0-141">Or you could go up another level and add the user to the Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="505e0-142">Sélectionnez un rôle</span><span class="sxs-lookup"><span data-stu-id="505e0-142">Select a role</span></span>
![Sélectionnez un rôle pour le nouvel utilisateur](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="505e0-144">Rôle</span><span class="sxs-lookup"><span data-stu-id="505e0-144">Role</span></span> | <span data-ttu-id="505e0-145">Dans le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="505e0-145">In the resource group</span></span> |
| --- | --- |
| <span data-ttu-id="505e0-146">Propriétaire</span><span class="sxs-lookup"><span data-stu-id="505e0-146">Owner</span></span> |<span data-ttu-id="505e0-147">Peut tout modifier, y compris l’accès utilisateur</span><span class="sxs-lookup"><span data-stu-id="505e0-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="505e0-148">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="505e0-148">Contributor</span></span> |<span data-ttu-id="505e0-149">Peut tout modifier, y compris l’ensemble des ressources</span><span class="sxs-lookup"><span data-stu-id="505e0-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="505e0-150">collaborateur de composants Application Insights</span><span class="sxs-lookup"><span data-stu-id="505e0-150">Application Insights Component contributor</span></span> |<span data-ttu-id="505e0-151">Peut modifier les ressources, les tests Web et les alertes Application Insights</span><span class="sxs-lookup"><span data-stu-id="505e0-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="505e0-152">Lecteur</span><span class="sxs-lookup"><span data-stu-id="505e0-152">Reader</span></span> |<span data-ttu-id="505e0-153">Peut afficher les éléments, mais ne peut rien modifier</span><span class="sxs-lookup"><span data-stu-id="505e0-153">Can view but not change anything</span></span> |

<span data-ttu-id="505e0-154">Une « modification » inclut la création, la suppression et la mise à jour des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="505e0-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="505e0-155">Ressources</span><span class="sxs-lookup"><span data-stu-id="505e0-155">Resources</span></span>
* <span data-ttu-id="505e0-156">Tests web</span><span class="sxs-lookup"><span data-stu-id="505e0-156">Web tests</span></span>
* <span data-ttu-id="505e0-157">Alertes</span><span class="sxs-lookup"><span data-stu-id="505e0-157">Alerts</span></span>
* <span data-ttu-id="505e0-158">Exportation continue</span><span class="sxs-lookup"><span data-stu-id="505e0-158">Continuous export</span></span>

#### <a name="select-the-user"></a><span data-ttu-id="505e0-159">Sélectionnez l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="505e0-159">Select the user</span></span>

<span data-ttu-id="505e0-160">Si l’utilisateur n’est pas dans le répertoire, vous pouvez inviter toute personne disposant d’un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="505e0-160">If the user you want isn't in the directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="505e0-161">(Si elle utilise des services comme Outlook.com, OneDrive, Windows Phone ou XBox Live, elle dispose d’un compte Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="505e0-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="505e0-162">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="505e0-162">Related content</span></span>

* [<span data-ttu-id="505e0-163">Contrôle d’accès en fonction du rôle dans Azure</span><span class="sxs-lookup"><span data-stu-id="505e0-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
