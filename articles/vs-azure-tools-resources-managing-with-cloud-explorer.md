---
title: Gestion des ressources Azure avec Cloud Explorer | Microsoft Docs
description: "Découvrez comment utiliser Cloud Explorer pour rechercher et gérer des ressources Azure dans Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 6e6d8d559f0251b71bfa6d529ead82a246cb3235
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="3de2c-103">Gérer les ressources associées à vos comptes Azure dans Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="3de2c-103">Manage the resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="3de2c-104">Cloud Explorer vous permet de visualiser vos groupes de ressources et vos ressources Azure, d’inspecter leurs propriétés et d’exécuter des actions de diagnostic de développeur essentielles à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3de2c-104">Cloud Explorer enables you to view your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="3de2c-105">Tout comme le [Portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer repose sur la pile Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3de2c-105">Like the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on the Azure Resource Manager stack.</span></span> <span data-ttu-id="3de2c-106">Par conséquent, Cloud Explorer comprend des ressources, telles que les groupes de ressources Azure, et des services Azure, notamment Logic Apps et API Apps, et prend en charge le [contrôle d’accès en fonction du rôle](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="3de2c-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3de2c-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3de2c-107">Prerequisites</span></span>
- <span data-ttu-id="3de2c-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) avec la **charge de travail Azure** sélectionnée, ou une version antérieure de Visual Studio avec le [Kit de développement logiciel (SDK) Microsoft Azure pour .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="3de2c-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the **Azure workload** selected, or an earlier version of Visual Studio with the [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="3de2c-109">Compte Microsoft Azure : si vous ne possédez pas de compte, vous pouvez [vous inscrire à un essai gratuit](http://go.microsoft.com/fwlink/?LinkId=623901) ou [activer les avantages de votre abonnement Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="3de2c-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="3de2c-110">Pour afficher Cloud Explorer, sélectionnez **Afficher** > **Cloud Explorer** sur la barre de menus.</span><span class="sxs-lookup"><span data-stu-id="3de2c-110">To view Cloud Explorer, select **View** > **Cloud Explorer** on the menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-to-cloud-explorer"></a><span data-ttu-id="3de2c-111">Ajouter un compte Azure à Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="3de2c-111">Add an Azure account to Cloud Explorer</span></span>
<span data-ttu-id="3de2c-112">Pour afficher les ressources associées à un compte Azure, vous devez commencer par ajouter le compte à Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="3de2c-112">To view the resources associated with an Azure account, you must first add the account to Cloud Explorer.</span></span> 

1. <span data-ttu-id="3de2c-113">Dans **Cloud Explorer**, sélectionnez **Paramètres de compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="3de2c-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="3de2c-115">Sélectionnez **Ajouter un nouveau compte**.</span><span class="sxs-lookup"><span data-stu-id="3de2c-115">Select **Add new account**.</span></span> 

    ![Lien Ajouter un compte Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="3de2c-117">Connectez-vous au compte Azure dont vous souhaitez parcourir les ressources.</span><span class="sxs-lookup"><span data-stu-id="3de2c-117">Log in to the Azure account whose resources you want to browse.</span></span> 

1. <span data-ttu-id="3de2c-118">Une fois que vous êtes connecté à un compte Azure, les abonnements associés à ce compte s’affichent.</span><span class="sxs-lookup"><span data-stu-id="3de2c-118">Once logged in to an Azure account, the subscriptions associated with that account display.</span></span> <span data-ttu-id="3de2c-119">Cochez les cases des abonnements de compte que vous souhaitez parcourir, puis sélectionnez **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="3de2c-119">Select the check boxes for the account subscriptions you want to browse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer : sélectionnez les abonnements Azure à afficher](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="3de2c-121">Une fois que vous avez sélectionné les abonnements dont vous souhaitez parcourir les ressources, les abonnements et les ressources s’affichent dans Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="3de2c-121">After selecting the subscriptions whose resources you want to browse, those subscriptions and resources display in the Cloud Explorer.</span></span>

    ![Listing des ressources Cloud Explorer pour un compte Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="3de2c-123">Supprimer un compte Azure de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="3de2c-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="3de2c-124">Dans **Cloud Explorer**, sélectionnez **Paramètres de compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="3de2c-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="3de2c-126">En regard du compte à supprimer, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="3de2c-126">Next to the account you want to remove, select **Remove**.</span></span>

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="3de2c-128">Afficher les types ou les groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="3de2c-128">View resource types or resource groups</span></span>
<span data-ttu-id="3de2c-129">Pour afficher vos ressources Azure, vous pouvez choisir l’affichage **Types de ressources** ou **Groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="3de2c-129">To view your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="3de2c-130">Dans **Cloud Explorer**, sélectionnez la liste déroulante d’affichage des ressources.</span><span class="sxs-lookup"><span data-stu-id="3de2c-130">In **Cloud Explorer**, select the resource view dropdown.</span></span>

    ![Liste déroulante Cloud Explorer pour sélectionner l’affichage des ressources souhaité](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="3de2c-132">Dans le menu contextuel, sélectionnez l’affichage souhaité :</span><span class="sxs-lookup"><span data-stu-id="3de2c-132">From the context menu, select the desired view:</span></span> 

    - <span data-ttu-id="3de2c-133">Affichage **Types de ressources** : l’affichage courant utilisé sur le [Portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) affiche vos ressources Azure classées par type, par exemple applications web, comptes de stockage et machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="3de2c-133">**Resource Types** view - The common view used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="3de2c-134">Affichage **Groupes de ressources** : organise les ressources Azure en fonction du groupe de ressources Azure auquel elles sont associées.</span><span class="sxs-lookup"><span data-stu-id="3de2c-134">**Resource Groups** view - Categorizes Azure resources by the Azure resource group with which they're associated.</span></span> <span data-ttu-id="3de2c-135">Un groupe de ressources est un regroupement de ressources Azure, généralement utilisé par une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="3de2c-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="3de2c-136">Pour en savoir plus sur les groupes de ressources Azure, consultez [Présentation d’Azure Resource Manager](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3de2c-136">To learn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="3de2c-137">L’image suivante compare les deux affichages de ressources :</span><span class="sxs-lookup"><span data-stu-id="3de2c-137">The following image shows a comparison of the two resource views:</span></span>

    ![Comparaison des affichages des ressources Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="3de2c-139">Afficher et parcourir les ressources dans Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="3de2c-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="3de2c-140">Pour accéder à une ressource Azure et afficher ses informations dans Cloud Explorer, développez le type de l’élément ou le groupe de ressources associé, puis sélectionnez la ressource.</span><span class="sxs-lookup"><span data-stu-id="3de2c-140">To navigate to an Azure resource and view its information in Cloud Explorer, expand the item's type or associated resource group and then select the resource.</span></span> <span data-ttu-id="3de2c-141">Lorsque vous sélectionnez une ressource, les informations apparaissent dans les deux onglets, **Actions** et **Propriétés**, en bas de Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="3de2c-141">When you select a resource, information appears in the two tabs - **Actions** and **Properties** - at the bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="3de2c-142">Onglet **Actions** : liste les actions possibles dans Cloud Explorer pour la ressource sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="3de2c-142">**Actions** tab - Lists the actions you can take in Cloud Explorer for the selected resource.</span></span> <span data-ttu-id="3de2c-143">Vous pouvez également voir ces options en cliquant avec le bouton droit sur la ressource pour afficher son menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="3de2c-143">You can also view these options by right-clicking the resource to view its context menu.</span></span>

- <span data-ttu-id="3de2c-144">Onglet **Propriétés** : affiche les propriétés de la ressource, notamment son type, ses paramètres régionaux et le groupe de ressources auquel elle est associée.</span><span class="sxs-lookup"><span data-stu-id="3de2c-144">**Properties** tab - Shows the properties of the resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="3de2c-145">L’image suivante montre un exemple de comparaison de ce qui apparaît sur chaque onglet pour un service App Service :</span><span class="sxs-lookup"><span data-stu-id="3de2c-145">The following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="3de2c-146">Chaque ressource dispose de l'action **Ouvrir dans le portail**.</span><span class="sxs-lookup"><span data-stu-id="3de2c-146">Every resource has the action **Open in portal**.</span></span> <span data-ttu-id="3de2c-147">Lorsque vous sélectionnez cette action, Cloud Explorer affiche la ressource sélectionnée dans le [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="3de2c-147">When you choose this action, Cloud Explorer displays the selected resource in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="3de2c-148">La fonctionnalité **Ouvrir dans le portail** est particulièrement pratique pour parcourir des ressources profondément imbriquées.</span><span class="sxs-lookup"><span data-stu-id="3de2c-148">The **Open in portal** feature is handy for navigating to deeply nested resources.</span></span>

<span data-ttu-id="3de2c-149">Des actions et des valeurs de propriétés supplémentaires peuvent également s’afficher en fonction de la ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="3de2c-149">Additional actions and property values may also appear based on the Azure resource.</span></span> <span data-ttu-id="3de2c-150">Par exemple, les applications web et les applications logiques ont également les actions **Ouvrir dans un navigateur** et **Attacher le débogueur** en plus de l’action **Ouvrir dans le portail**.</span><span class="sxs-lookup"><span data-stu-id="3de2c-150">For example, web apps and logic apps also have the actions **Open in browser** and **Attach debugger** in addition to **Open in portal**.</span></span> <span data-ttu-id="3de2c-151">Les actions d’ouverture des éditeurs apparaissent lorsque vous sélectionnez un objet Blob, File d'attente ou Table de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3de2c-151">Actions to open editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="3de2c-152">Les applications Azure ont des propriétés **URL** et **État**, tandis que les ressources de stockage ont des propriétés clé et chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="3de2c-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="3de2c-153">Trouver des ressources dans Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="3de2c-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="3de2c-154">Pour trouver des ressources portant un nom spécifique dans les abonnements de votre compte Azure, entrez le nom dans la zone **Recherche** de Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="3de2c-154">To locate resources with a specific name in your Azure account subscriptions, enter the name in the **Search** box in Cloud Explorer.</span></span>

![Trouver des ressources dans Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="3de2c-156">Lorsque vous entrez des caractères dans la zone **Recherche**, seules les ressources qui correspondent à ces caractères apparaissent dans l’arborescence de ressources.</span><span class="sxs-lookup"><span data-stu-id="3de2c-156">As you enter characters in the **Search** box, only resources that match those characters appear in the resource tree.</span></span>
