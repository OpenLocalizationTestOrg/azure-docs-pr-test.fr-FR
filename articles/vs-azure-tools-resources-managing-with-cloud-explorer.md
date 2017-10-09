---
title: aaaManaging Azure ressources de Cloud Explorer | Documents Microsoft
description: "Découvrez comment toouse Cloud Explorer toobrowse et gérer des ressources Azure dans Visual Studio."
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
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a><span data-ttu-id="7d6b7-103">Gérer les ressources hello associés à vos comptes Azure dans Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="7d6b7-103">Manage hello resources associated with your Azure accounts in Visual Studio Cloud Explorer</span></span>
<span data-ttu-id="7d6b7-104">Cloud Explorer Active vous tooview vos ressources Azure et les groupes de ressources, examiner leurs propriétés et effectuer des actions de diagnostics essentiels de développeur à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-104">Cloud Explorer enables you tooview your Azure resources and resource groups, inspect their properties, and perform key developer diagnostics actions from within Visual Studio.</span></span> 

<span data-ttu-id="7d6b7-105">Comme hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer repose sur la pile du Gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-105">Like hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer is built on hello Azure Resource Manager stack.</span></span> <span data-ttu-id="7d6b7-106">Par conséquent, Cloud Explorer comprend des ressources, telles que les groupes de ressources Azure, et des services Azure, notamment Logic Apps et API Apps, et prend en charge le [contrôle d’accès en fonction du rôle](active-directory/role-based-access-control-configure.md) (RBAC).</span><span class="sxs-lookup"><span data-stu-id="7d6b7-106">Therefore, Cloud Explorer understands resources such as Azure resource groups and Azure services such as Logic apps and API apps, and it supports [role-based access control](active-directory/role-based-access-control-configure.md) (RBAC).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7d6b7-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7d6b7-107">Prerequisites</span></span>
- <span data-ttu-id="7d6b7-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) avec hello **la charge de travail Azure** sélectionné, ou une version antérieure de Visual Studio avec hello [Microsoft Azure SDK pour .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span><span class="sxs-lookup"><span data-stu-id="7d6b7-108">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello **Azure workload** selected, or an earlier version of Visual Studio with hello [Microsoft Azure SDK for .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).</span></span>
- <span data-ttu-id="7d6b7-109">Compte Microsoft Azure : si vous ne possédez pas de compte, vous pouvez [vous inscrire à un essai gratuit](http://go.microsoft.com/fwlink/?LinkId=623901) ou [activer les avantages de votre abonnement Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).</span><span class="sxs-lookup"><span data-stu-id="7d6b7-109">Microsoft Azure account - If you don't have an account, you can [sign up for a free trial](http://go.microsoft.com/fwlink/?LinkId=623901) or [activate your Visual Studio subscriber benefits](http://go.microsoft.com/fwlink/?LinkId=623901).</span></span>

> [!NOTE]
> <span data-ttu-id="7d6b7-110">tooview Cloud Explorer, sélectionnez **vue** > **Cloud Explorer** sur la barre de menus hello.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-110">tooview Cloud Explorer, select **View** > **Cloud Explorer** on hello menu bar.</span></span>   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a><span data-ttu-id="7d6b7-111">Ajouter un compte Azure de tooCloud Explorer</span><span class="sxs-lookup"><span data-stu-id="7d6b7-111">Add an Azure account tooCloud Explorer</span></span>
<span data-ttu-id="7d6b7-112">ressources de hello tooview associés à un compte Azure, vous devez d’abord ajouter hello compte tooCloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-112">tooview hello resources associated with an Azure account, you must first add hello account tooCloud Explorer.</span></span> 

1. <span data-ttu-id="7d6b7-113">Dans **Cloud Explorer**, sélectionnez **Paramètres de compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-113">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="7d6b7-115">Sélectionnez **Ajouter un nouveau compte**.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-115">Select **Add new account**.</span></span> 

    ![Lien Ajouter un compte Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. <span data-ttu-id="7d6b7-117">Connectez-vous à toohello dont vous souhaitez que les ressources de compte Azure toobrowse.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-117">Log in toohello Azure account whose resources you want toobrowse.</span></span> 

1. <span data-ttu-id="7d6b7-118">Une fois connecté tooan compte Azure, affichent les abonnements hello associés à ce compte.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-118">Once logged in tooan Azure account, hello subscriptions associated with that account display.</span></span> <span data-ttu-id="7d6b7-119">Sélectionnez hello cases à cocher pour les abonnements de compte hello vous souhaitez toobrowse, puis sélectionnez **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-119">Select hello check boxes for hello account subscriptions you want toobrowse and then select **Apply**.</span></span> 
 
    ![Cloud Explorer : sélectionnez toodisplay des abonnements Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. <span data-ttu-id="7d6b7-121">Après avoir sélectionné les abonnements dont vous souhaitez que les ressources hello toobrowse, ces abonnements et des ressources affichent Bonjour Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-121">After selecting hello subscriptions whose resources you want toobrowse, those subscriptions and resources display in hello Cloud Explorer.</span></span>

    ![Listing des ressources Cloud Explorer pour un compte Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a><span data-ttu-id="7d6b7-123">Supprimer un compte Azure de Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="7d6b7-123">Remove an Azure account from Cloud Explorer</span></span> 

1. <span data-ttu-id="7d6b7-124">Dans **Cloud Explorer**, sélectionnez **Paramètres de compte Azure**.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-124">In **Cloud Explorer**, select **Azure account settings**.</span></span>

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. <span data-ttu-id="7d6b7-126">Suivant toohello compte tooremove, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-126">Next toohello account you want tooremove, select **Remove**.</span></span>

    ![Icône des paramètres de compte Azure Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a><span data-ttu-id="7d6b7-128">Afficher les types ou les groupes de ressources</span><span class="sxs-lookup"><span data-stu-id="7d6b7-128">View resource types or resource groups</span></span>
<span data-ttu-id="7d6b7-129">tooview vos ressources Azure, vous pouvez choisir le **Types de ressources** ou **groupes de ressources** vue.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-129">tooview your Azure resources, you can choose either **Resource Types** or **Resource Groups** view.</span></span>

1. <span data-ttu-id="7d6b7-130">Dans **Cloud Explorer**, sélectionnez hello liste déroulante Affichage de ressources.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-130">In **Cloud Explorer**, select hello resource view dropdown.</span></span>

    ![Affichage de ressources de l’Explorateur déroulante liste tooselect hello souhaité de cloud computing](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. <span data-ttu-id="7d6b7-132">À partir du menu contextuel de hello, sélectionnez hello affichage de votre choix :</span><span class="sxs-lookup"><span data-stu-id="7d6b7-132">From hello context menu, select hello desired view:</span></span> 

    - <span data-ttu-id="7d6b7-133">**Types de ressources** affichage - hello commun utilisé sur hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), affiche vos ressources Azure classés par leur type, telles que les applications web, les comptes de stockage et les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-133">**Resource Types** view - hello common view used on hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), shows your Azure resources categorized by their type, such as web apps, storage accounts, and virtual machines.</span></span> 
    - <span data-ttu-id="7d6b7-134">**Groupes de ressources** afficher - ressources Azure de classe par groupe de ressources Azure hello auquel ils sont associés.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-134">**Resource Groups** view - Categorizes Azure resources by hello Azure resource group with which they're associated.</span></span> <span data-ttu-id="7d6b7-135">Un groupe de ressources est un regroupement de ressources Azure, généralement utilisé par une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-135">A resource group is a bundle of Azure resources, typically used by a specific application.</span></span> <span data-ttu-id="7d6b7-136">toolearn savoir plus sur les groupes de ressources Azure, consultez [vue d’ensemble du Gestionnaire de ressources Azure](./azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7d6b7-136">toolearn more about Azure resource groups, see [Azure Resource Manager Overview](./azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="7d6b7-137">Hello image suivante présente une comparaison des hello deux affichages de ressources :</span><span class="sxs-lookup"><span data-stu-id="7d6b7-137">hello following image shows a comparison of hello two resource views:</span></span>

    ![Comparaison des affichages des ressources Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a><span data-ttu-id="7d6b7-139">Afficher et parcourir les ressources dans Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="7d6b7-139">View and navigate resources in Cloud Explorer</span></span>
<span data-ttu-id="7d6b7-140">toonavigate tooan ressource Azure et afficher les informations dans le Cloud Explorer, développez l’élément hello type ou groupe de ressources et puis sélectionnez les ressources hello.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-140">toonavigate tooan Azure resource and view its information in Cloud Explorer, expand hello item's type or associated resource group and then select hello resource.</span></span> <span data-ttu-id="7d6b7-141">Lorsque vous sélectionnez une ressource, les informations s’affichent dans les onglets de hello deux - **Actions** et **propriétés** - bas hello Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-141">When you select a resource, information appears in hello two tabs - **Actions** and **Properties** - at hello bottom of Cloud Explorer.</span></span> 

- <span data-ttu-id="7d6b7-142">**Actions** onglet - listes hello actions possibles dans Cloud Explorer pour la ressource de hello sélectionné.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-142">**Actions** tab - Lists hello actions you can take in Cloud Explorer for hello selected resource.</span></span> <span data-ttu-id="7d6b7-143">Vous pouvez également afficher ces options en cliquant sur hello ressource tooview son menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-143">You can also view these options by right-clicking hello resource tooview its context menu.</span></span>

- <span data-ttu-id="7d6b7-144">**Propriétés** onglet - affiche les propriétés hello de ressource hello, telles que son groupe de type, de paramètres régionaux et de ressources auquel il est associé.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-144">**Properties** tab - Shows hello properties of hello resource, such as its type, locale, and resource group with which it is associated.</span></span>

<span data-ttu-id="7d6b7-145">Hello image suivante montre une comparaison de l’exemple de ce que vous voyez sur chaque onglet pour un Service d’application :</span><span class="sxs-lookup"><span data-stu-id="7d6b7-145">hello following image shows an example comparison of what you see on each tab for an App Service:</span></span>

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

<span data-ttu-id="7d6b7-146">Chaque ressource a d’action hello **ouvrir dans le portail**.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-146">Every resource has hello action **Open in portal**.</span></span> <span data-ttu-id="7d6b7-147">Lorsque vous sélectionnez cette action, Cloud Explorer affiche les ressources hello sélectionné Bonjour [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="7d6b7-147">When you choose this action, Cloud Explorer displays hello selected resource in hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="7d6b7-148">Hello **ouvrir dans le portail** fonctionnalité est pratique pour parcourir les ressources de toodeeply imbriquée.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-148">hello **Open in portal** feature is handy for navigating toodeeply nested resources.</span></span>

<span data-ttu-id="7d6b7-149">Actions supplémentaires et des valeurs de propriété peuvent également apparaître en fonction de hello ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-149">Additional actions and property values may also appear based on hello Azure resource.</span></span> <span data-ttu-id="7d6b7-150">Par exemple, les applications web et logique ont également les actions hello **ouvrir dans le navigateur** et **attacher le débogueur** en outre trop**ouvrir dans le portail**.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-150">For example, web apps and logic apps also have hello actions **Open in browser** and **Attach debugger** in addition too**Open in portal**.</span></span> <span data-ttu-id="7d6b7-151">Éditeurs de tooopen actions s’affichent lorsque vous choisissez un objet blob de compte de stockage, une file d’attente ou une table.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-151">Actions tooopen editors appear when you choose a storage account blob, queue, or table.</span></span> <span data-ttu-id="7d6b7-152">Les applications Azure ont des propriétés **URL** et **État**, tandis que les ressources de stockage ont des propriétés clé et chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-152">Azure apps have **URL** and **Status** properties, while storage resources have key and connection string properties.</span></span>

## <a name="find-resources-in-cloud-explorer"></a><span data-ttu-id="7d6b7-153">Trouver des ressources dans Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="7d6b7-153">Find resources in Cloud Explorer</span></span>
<span data-ttu-id="7d6b7-154">ressources toolocate avec un nom spécifique dans vos abonnements de compte Azure, entrez les nom hello Bonjour **recherche** zone dans l’Explorateur de Cloud.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-154">toolocate resources with a specific name in your Azure account subscriptions, enter hello name in hello **Search** box in Cloud Explorer.</span></span>

![Trouver des ressources dans Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

<span data-ttu-id="7d6b7-156">Lorsque vous entrez des caractères dans hello **recherche** zone, uniquement les ressources qui correspondent à ces caractères s’affichent dans l’arborescence des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="7d6b7-156">As you enter characters in hello **Search** box, only resources that match those characters appear in hello resource tree.</span></span>
