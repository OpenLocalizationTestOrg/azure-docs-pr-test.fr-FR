---
title: "aaaResources, rôles et contrôle d’accès dans Azure Application Insights | Documents Microsoft"
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
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a><span data-ttu-id="5e658-103">Contrôle d’accès, rôles et ressources dans Application Insights</span><span class="sxs-lookup"><span data-stu-id="5e658-103">Resources, roles, and access control in Application Insights</span></span>
<span data-ttu-id="5e658-104">Vous pouvez contrôler qui a lu et mettre à jour des données de tooyour d’accès dans Azure [Application Insights][start], à l’aide de [contrôle d’accès basé sur un rôle dans Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="5e658-104">You can control who has read and update access tooyour data in Azure [Application Insights][start], by using [Role-based access control in Microsoft Azure](../active-directory/role-based-access-control-configure.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e658-105">Affecter toousers accès Bonjour **groupe de ressources ou d’un abonnement** toowhich votre ressource application appartienne - pas de ressource hello elle-même.</span><span class="sxs-lookup"><span data-stu-id="5e658-105">Assign access toousers in hello **resource group or subscription** toowhich your application resource belongs - not in hello resource itself.</span></span> <span data-ttu-id="5e658-106">Affecter hello **contributeur de composant Application Insights** rôle.</span><span class="sxs-lookup"><span data-stu-id="5e658-106">Assign hello **Application Insights component contributor** role.</span></span> <span data-ttu-id="5e658-107">Cela garantit uniform contrôle d’accès tooweb tests et des alertes, ainsi que des ressources de votre application.</span><span class="sxs-lookup"><span data-stu-id="5e658-107">This ensures uniform control of access tooweb tests and alerts along with your application resource.</span></span> <span data-ttu-id="5e658-108">[En savoir plus](#access).</span><span class="sxs-lookup"><span data-stu-id="5e658-108">[Learn more](#access).</span></span>
> 
> 

## <a name="resources-groups-and-subscriptions"></a><span data-ttu-id="5e658-109">Ressources, groupes et abonnements</span><span class="sxs-lookup"><span data-stu-id="5e658-109">Resources, groups and subscriptions</span></span>
<span data-ttu-id="5e658-110">Quelques définitions pour commencer :</span><span class="sxs-lookup"><span data-stu-id="5e658-110">First, some definitions:</span></span>

* <span data-ttu-id="5e658-111">**Ressource** : une instance d’un service Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5e658-111">**Resource** - An instance of a Microsoft Azure service.</span></span> <span data-ttu-id="5e658-112">Votre ressource Application Insights collecte, analyse et affiche les données de télémétrie hello envoyées à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="5e658-112">Your Application Insights resource collects, analyzes and displays hello telemetry data sent from your application.</span></span>  <span data-ttu-id="5e658-113">Les autres types de ressources Azure incluent des applications Web, des bases de données et des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="5e658-113">Other types of Azure resources include web apps, databases, and VMs.</span></span>
  
    <span data-ttu-id="5e658-114">Ouvrez de vos ressources, toosee hello [Azure Portal][portal], connectez-vous, puis cliquez sur toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="5e658-114">toosee your resources, open hello [Azure Portal][portal], sign in, and click All Resources.</span></span> <span data-ttu-id="5e658-115">toofind une ressource, tapez une partie de son nom dans le champ de filtre hello.</span><span class="sxs-lookup"><span data-stu-id="5e658-115">toofind a resource, type part of its name in hello filter field.</span></span>
  
    ![Liste des ressources Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* <span data-ttu-id="5e658-117">[**Groupe de ressources** ] [ group] -chaque ressource appartient tooone groupe.</span><span class="sxs-lookup"><span data-stu-id="5e658-117">[**Resource group**][group] - Every resource belongs tooone group.</span></span> <span data-ttu-id="5e658-118">Un groupe est un moyen toomanage liées à des ressources, en particulier pour le contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="5e658-118">A group is a convenient way toomanage related resources, particularly for access control.</span></span> <span data-ttu-id="5e658-119">Par exemple, dans une ressource de groupe, vous pouvez placer une application Web, une application de hello de toomonitor ressource Application Insights et un tookeep de ressource de stockage données exportées.</span><span class="sxs-lookup"><span data-stu-id="5e658-119">For example, into one resource group you could put a Web App, an Application Insights resource toomonitor hello app, and a Storage resource tookeep exported data.</span></span>

    ![Cliquez sur Parcourir, Groupes de ressources, puis choisissez un groupe](./media/app-insights-resources-roles-access-control/11-group.png)

* <span data-ttu-id="5e658-121">[**Abonnement** ](https://manage.windowsazure.com) -toouse Application Insights ou autres ressources Azure, vous vous connectez tooan abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5e658-121">[**Subscription**](https://manage.windowsazure.com) - toouse Application Insights or other Azure resources, you sign in tooan Azure subscription.</span></span> <span data-ttu-id="5e658-122">Chaque groupe de ressources appartient tooone abonnement Azure, où vous choisissez votre package de prix et, s’il s’agit d’un abonnement de l’organisation, choisissez les membres hello et leurs autorisations d’accès.</span><span class="sxs-lookup"><span data-stu-id="5e658-122">Every resource group belongs tooone Azure subscription, where you choose your price package and, if it's an organization subscription, choose hello members and their access permissions.</span></span>
* <span data-ttu-id="5e658-123">[**Compte Microsoft** ] [ account] -hello nom d’utilisateur et mot de passe que vous utilisez toosign dans tooMicrosoft Azure abonnements, XBox Live, Outlook.com et autres services Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5e658-123">[**Microsoft account**][account] - hello username and password that you use toosign in tooMicrosoft Azure subscriptions, XBox Live, Outlook.com, and other Microsoft services.</span></span>

## <span data-ttu-id="5e658-124"><a name="access"></a>Contrôler l’accès dans le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="5e658-124"><a name="access"></a> Control access in hello resource group</span></span>
<span data-ttu-id="5e658-125">Il est important toounderstand que dans la ressource de toohello plus que vous avez créé pour votre application, il existe également de séparer des ressources masqués pour les alertes et les tests web.</span><span class="sxs-lookup"><span data-stu-id="5e658-125">It's important toounderstand that in addition toohello resource you created for your application, there are also separate hidden resources for alerts and web tests.</span></span> <span data-ttu-id="5e658-126">Ils sont attaché toohello même [groupe de ressources](#resource-group) que votre application.</span><span class="sxs-lookup"><span data-stu-id="5e658-126">They are attached toohello same [resource group](#resource-group) as your application.</span></span> <span data-ttu-id="5e658-127">Vous pouvez également placer d’autres services Azure ici, comme des sites Web ou du stockage.</span><span class="sxs-lookup"><span data-stu-id="5e658-127">You might also have put other Azure services in there, such as websites or storage.</span></span>

![Ressources dans Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

<span data-ttu-id="5e658-129">toocontrol accéder aux ressources toothese qu'il est donc recommandé :</span><span class="sxs-lookup"><span data-stu-id="5e658-129">toocontrol access toothese resources it's therefore recommended to:</span></span>

* <span data-ttu-id="5e658-130">Contrôler l’accès au hello **groupe de ressources ou d’un abonnement** niveau.</span><span class="sxs-lookup"><span data-stu-id="5e658-130">Control access at hello **resource group or subscription** level.</span></span>
* <span data-ttu-id="5e658-131">Affecter hello **contributeur de composant d’Application Insights** toousers de rôle.</span><span class="sxs-lookup"><span data-stu-id="5e658-131">Assign hello **Application Insights Component contributor** role toousers.</span></span> <span data-ttu-id="5e658-132">Cela leur permet de tooedit des tests web, les alertes et les ressources Application Insights, sans fournir d’autres services dans le groupe de hello tooany d’accès.</span><span class="sxs-lookup"><span data-stu-id="5e658-132">This allows them tooedit web tests, alerts, and Application Insights resources, without providing access tooany other services in hello group.</span></span>

## <a name="tooprovide-access-tooanother-user"></a><span data-ttu-id="5e658-133">tooprovide tooanother utilisateur</span><span class="sxs-lookup"><span data-stu-id="5e658-133">tooprovide access tooanother user</span></span>
<span data-ttu-id="5e658-134">Vous devez disposer d’abonnement de toohello de droits de propriétaire ou un groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="5e658-134">You must have Owner rights toohello subscription or hello resource group.</span></span>

<span data-ttu-id="5e658-135">Hello utilisateur doit avoir un [Account Microsoft][account], ou accéder aux tootheir [Account Microsoft](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="5e658-135">hello user must have a [Microsoft Account][account], or access tootheir [organizational Microsoft Account](../active-directory/sign-up-organization.md).</span></span> <span data-ttu-id="5e658-136">Vous pouvez fournir tooindividuals d’accès, ainsi que les groupes toouser définis dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5e658-136">You can provide access tooindividuals, and also toouser groups defined in Azure Active Directory.</span></span>

#### <a name="navigate-toohello-resource-group"></a><span data-ttu-id="5e658-137">Parcourir le groupe de ressources toohello</span><span class="sxs-lookup"><span data-stu-id="5e658-137">Navigate toohello resource group</span></span>
<span data-ttu-id="5e658-138">Ajouter un utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="5e658-138">Add hello user there.</span></span>

![Dans le panneau des ressources de votre application, ouvrez Essentials, ouvrez le groupe de ressources hello et sélectionner les utilisateurs/paramètres.](./media/app-insights-resources-roles-access-control/01-add-user.png)

<span data-ttu-id="5e658-141">Ou vous pouvez aller plus loin et ajouter hello utilisateur toohello abonnement.</span><span class="sxs-lookup"><span data-stu-id="5e658-141">Or you could go up another level and add hello user toohello Subscription.</span></span>

#### <a name="select-a-role"></a><span data-ttu-id="5e658-142">Sélectionnez un rôle</span><span class="sxs-lookup"><span data-stu-id="5e658-142">Select a role</span></span>
![Sélectionnez un rôle pour le nouvel utilisateur de hello](./media/app-insights-resources-roles-access-control/03-role.png)

| <span data-ttu-id="5e658-144">Rôle</span><span class="sxs-lookup"><span data-stu-id="5e658-144">Role</span></span> | <span data-ttu-id="5e658-145">Dans le groupe de ressources hello</span><span class="sxs-lookup"><span data-stu-id="5e658-145">In hello resource group</span></span> |
| --- | --- |
| <span data-ttu-id="5e658-146">Propriétaire</span><span class="sxs-lookup"><span data-stu-id="5e658-146">Owner</span></span> |<span data-ttu-id="5e658-147">Peut tout modifier, y compris l’accès utilisateur</span><span class="sxs-lookup"><span data-stu-id="5e658-147">Can change anything, including user access</span></span> |
| <span data-ttu-id="5e658-148">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="5e658-148">Contributor</span></span> |<span data-ttu-id="5e658-149">Peut tout modifier, y compris l’ensemble des ressources</span><span class="sxs-lookup"><span data-stu-id="5e658-149">Can edit anything, including all resources</span></span> |
| <span data-ttu-id="5e658-150">collaborateur de composants Application Insights</span><span class="sxs-lookup"><span data-stu-id="5e658-150">Application Insights Component contributor</span></span> |<span data-ttu-id="5e658-151">Peut modifier les ressources, les tests Web et les alertes Application Insights</span><span class="sxs-lookup"><span data-stu-id="5e658-151">Can edit Application Insights resources, web tests and alerts</span></span> |
| <span data-ttu-id="5e658-152">Lecteur</span><span class="sxs-lookup"><span data-stu-id="5e658-152">Reader</span></span> |<span data-ttu-id="5e658-153">Peut afficher les éléments, mais ne peut rien modifier</span><span class="sxs-lookup"><span data-stu-id="5e658-153">Can view but not change anything</span></span> |

<span data-ttu-id="5e658-154">Une « modification » inclut la création, la suppression et la mise à jour des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5e658-154">'Editing' includes creating, deleting and updating:</span></span>

* <span data-ttu-id="5e658-155">Ressources</span><span class="sxs-lookup"><span data-stu-id="5e658-155">Resources</span></span>
* <span data-ttu-id="5e658-156">Tests web</span><span class="sxs-lookup"><span data-stu-id="5e658-156">Web tests</span></span>
* <span data-ttu-id="5e658-157">Alertes</span><span class="sxs-lookup"><span data-stu-id="5e658-157">Alerts</span></span>
* <span data-ttu-id="5e658-158">Exportation continue</span><span class="sxs-lookup"><span data-stu-id="5e658-158">Continuous export</span></span>

#### <a name="select-hello-user"></a><span data-ttu-id="5e658-159">Sélectionnez hello utilisateur</span><span class="sxs-lookup"><span data-stu-id="5e658-159">Select hello user</span></span>

<span data-ttu-id="5e658-160">Si l’utilisateur hello souhaité n’est pas dans le répertoire de hello, vous pouvez inviter toute personne disposant d’un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5e658-160">If hello user you want isn't in hello directory, you can invite anyone with a Microsoft account.</span></span>
<span data-ttu-id="5e658-161">(Si elle utilise des services comme Outlook.com, OneDrive, Windows Phone ou XBox Live, elle dispose d’un compte Microsoft.)</span><span class="sxs-lookup"><span data-stu-id="5e658-161">(If they use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, they have a Microsoft account.)</span></span>

## <a name="related-content"></a><span data-ttu-id="5e658-162">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="5e658-162">Related content</span></span>

* [<span data-ttu-id="5e658-163">Contrôle d’accès en fonction du rôle dans Azure</span><span class="sxs-lookup"><span data-stu-id="5e658-163">Role based access control in Azure</span></span>](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
