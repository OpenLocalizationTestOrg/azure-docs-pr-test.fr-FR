---
title: "aaaGet a démarré avec des modèles privés | Documents Microsoft"
description: "Ajouter, gérer et partager vos modèles privés à l’aide de hello portail Azure, hello CLI d’Azure ou PowerShell."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a><span data-ttu-id="12be1-103">Prise en main des modèles privés sur hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="12be1-103">Get started with private Templates on hello Azure Portal</span></span>
<span data-ttu-id="12be1-104">Un [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) modèle est un modèle déclaratif utilisé toodefine votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="12be1-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used toodefine your deployment.</span></span> <span data-ttu-id="12be1-105">Vous pouvez définir des toodeploy de ressources hello pour une solution et spécifier les paramètres et les variables qui vous permettent de valeurs tooinput pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="12be1-105">You can define hello resources toodeploy for a solution, and specify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="12be1-106">Hello modèle se compose de JSON et les expressions que vous pouvez utiliser les valeurs de tooconstruct pour votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="12be1-106">hello template consists of JSON and expressions which you can use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="12be1-107">Vous pouvez utiliser hello nouvelle **modèles** fonctionnalité Bonjour [Azure Portal](https://portal.azure.com) avec hello **Microsoft.Gallery** fournisseur de ressources comme une extension de hello [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable utilisateurs toocreate, gérer et déployer des modèles de privé à partir d’une bibliothèque personnelle.</span><span class="sxs-lookup"><span data-stu-id="12be1-107">You can use hello new **Templates** capability in hello [Azure Portal](https://portal.azure.com) along with hello **Microsoft.Gallery** resource provider as an extension of hello [Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable users toocreate, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="12be1-108">Ce document présente l’ajout, la gestion et le partage privé **modèle** à l’aide de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12be1-108">This document walks you through adding, managing and sharing a private **Template** using hello Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="12be1-109">Assistance</span><span class="sxs-lookup"><span data-stu-id="12be1-109">Guidance</span></span>
<span data-ttu-id="12be1-110">Hello suggestions suivantes vous permettra de tirer pleinement parti des **modèles** lorsque vous travaillez avec vos solutions :</span><span class="sxs-lookup"><span data-stu-id="12be1-110">hello following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="12be1-111">Un **Modèle** est une ressource d’encapsulation qui contient un modèle Resource Manager et des métadonnées supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="12be1-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="12be1-112">Il comporte très comme élément tooan Bonjour Marketplace.</span><span class="sxs-lookup"><span data-stu-id="12be1-112">It behaves very similarly tooan item in hello Marketplace.</span></span> <span data-ttu-id="12be1-113">Hello principale différence est qu’il est un élément privé en tant qu’éléments de Marketplace publics toohello exécutée.</span><span class="sxs-lookup"><span data-stu-id="12be1-113">hello key difference is that it is a private item as opposed toohello public Marketplace items.</span></span>
* <span data-ttu-id="12be1-114">Hello **modèles** bibliothèque fonctionne bien pour les utilisateurs qui ont besoin de toocustomize leurs déploiements.</span><span class="sxs-lookup"><span data-stu-id="12be1-114">hello **Templates** library works well for users who need toocustomize their deployments.</span></span>
* <span data-ttu-id="12be1-115">**Modèles** conviennent aux utilisateurs ayant besoin d’un référentiel simple dans Azure.</span><span class="sxs-lookup"><span data-stu-id="12be1-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="12be1-116">Commencez par un modèle Resource Manager existant.</span><span class="sxs-lookup"><span data-stu-id="12be1-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="12be1-117">Recherchez des modèles dans [github](https://github.com/Azure/azure-quickstart-templates) ou [exportez des modèles](../azure-resource-manager/resource-manager-export-template.md) à partir d’un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="12be1-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="12be1-118">**Modèles** liée toohello utilisateurs en les publie.</span><span class="sxs-lookup"><span data-stu-id="12be1-118">**Templates** are tied toohello user who publishes them.</span></span> <span data-ttu-id="12be1-119">nom du serveur de publication Hello est visible tooeveryone disposant d’un accès en lecture tooit.</span><span class="sxs-lookup"><span data-stu-id="12be1-119">hello publisher name is visible tooeveryone who has read access tooit.</span></span>
* <span data-ttu-id="12be1-120">**Modèles** sont des ressources Azure Resource Manager et ne peuvent être renommés une fois publiés.</span><span class="sxs-lookup"><span data-stu-id="12be1-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="12be1-121">Ajouter une ressource de Modèle</span><span class="sxs-lookup"><span data-stu-id="12be1-121">Add a Template resource</span></span>
<span data-ttu-id="12be1-122">Il existe deux façons toocreate un **modèle** ressource Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12be1-122">There are two ways toocreate a **Template** resource in hello Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="12be1-123">Méthode 1 : Créer une ressource de Modèle à partir d’un groupe de ressources en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="12be1-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="12be1-124">Accédez tooan groupe de ressources existant sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12be1-124">Navigate tooan existing resource group on hello Azure Portal.</span></span> <span data-ttu-id="12be1-125">Sélectionnez **Exporter le modèle** dans **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="12be1-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="12be1-126">Une fois le modèle de gestionnaire de ressources hello est exporté, utilisez hello **enregistrer le modèle** bouton toosave il toohello **modèles** référentiel.</span><span class="sxs-lookup"><span data-stu-id="12be1-126">Once hello Resource Manager template is exported, use hello **Save Template** button toosave it toohello **Templates** repository.</span></span> <span data-ttu-id="12be1-127">Cliquez [ici](../azure-resource-manager/resource-manager-export-template.md)pour obtenir des informations complètes sur l’exportation des modèles.</span><span class="sxs-lookup"><span data-stu-id="12be1-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br /><span data-ttu-id="12be1-128">
   ![Exportation de groupe de ressources](media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="12be1-128">
![Resource group export](media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="12be1-129">Sélectionnez hello **enregistrer tooTemplate** bouton de commande.</span><span class="sxs-lookup"><span data-stu-id="12be1-129">Select hello **Save tooTemplate** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="12be1-130">Entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="12be1-130">Enter hello following information:</span></span>
   
   * <span data-ttu-id="12be1-131">Nom : nom de l’objet de modèle hello (Remarque : il s’agit d’un nom de base Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12be1-131">Name – Name of hello template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="12be1-132">Toutes les restrictions d’affectation de noms s’appliquent et ces derniers ne peuvent être modifiés une fois créés).</span><span class="sxs-lookup"><span data-stu-id="12be1-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="12be1-133">Description : résumé sur le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="12be1-133">Description – Quick summary about hello template.</span></span>
     
     ![Enregistrer un Modèle](media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="12be1-135">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="12be1-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="12be1-136">Hello Panneau de modèle d’exportation affiche des notifications lorsque hello modèle exporté du Gestionnaire de ressources comporte des erreurs, mais vous serez toujours en mesure de toosave cette toohello de modèle de gestionnaire de ressources modèles.</span><span class="sxs-lookup"><span data-stu-id="12be1-136">hello Export template blade shows notifications when hello exported Resource Manager template has errors, but you will still be able toosave this Resource Manager template toohello Templates.</span></span> <span data-ttu-id="12be1-137">Assurez-vous que vous vérifiez et corrigez les problèmes de modèle de n’importe quel gestionnaire de ressources avant redéploiement hello exportée modèle du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="12be1-137">Ensure that you check and fix any Resource Manager template issues before redeploying hello exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="12be1-138">Méthode 2: Ajouter une nouvelle ressource de Modèle à partir du panneau Parcourir</span><span class="sxs-lookup"><span data-stu-id="12be1-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="12be1-139">Vous pouvez également ajouter un nouveau **modèle** à partir de zéro à l’aide de hello + ajouter bouton de commande dans **Parcourir > modèles**.</span><span class="sxs-lookup"><span data-stu-id="12be1-139">You can also add a new **Template** from scratch using hello +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="12be1-140">Vous devez tooprovide un nom, Description et hello modèle du Gestionnaire de ressources JSON.</span><span class="sxs-lookup"><span data-stu-id="12be1-140">You will need tooprovide a Name, Description and hello Resource Manager template JSON.</span></span>

![Ajouter un Modèle](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="12be1-142">Microsoft.Gallery est un fournisseur de ressources Azure basé sur le client.</span><span class="sxs-lookup"><span data-stu-id="12be1-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="12be1-143">Bonjour ressource de modèle est utilisateur toohello liée qui l’a créée.</span><span class="sxs-lookup"><span data-stu-id="12be1-143">hello Template resource is tied toohello user who created it.</span></span> <span data-ttu-id="12be1-144">Il n’est pas liée tooany des abonnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="12be1-144">It is not tied tooany specific subscription.</span></span> <span data-ttu-id="12be1-145">Un abonnement doit toobe choisi uniquement lors du déploiement d’un modèle.</span><span class="sxs-lookup"><span data-stu-id="12be1-145">A subscription needs toobe chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="12be1-146">Afficher les ressources de Modèle</span><span class="sxs-lookup"><span data-stu-id="12be1-146">View Template resources</span></span>
<span data-ttu-id="12be1-147">Tous les **modèles** tooyou disponible peut être consulté à **Parcourir > modèles**.</span><span class="sxs-lookup"><span data-stu-id="12be1-147">All **Templates** available tooyou can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="12be1-148">Cela inclut les **Modèles** que vous avez créés, ainsi que ceux ayant été partagés avec vous avec différents niveaux d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="12be1-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="12be1-149">Plus de détails dans hello [le contrôle d’accès](#access-control-for-a-tenant-resource-provider) section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="12be1-149">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![Afficher le Modèle](media/view-template-portal1.PNG)  <br />

<span data-ttu-id="12be1-151">Vous pouvez afficher les détails de hello d’un **modèle** en cliquant sur un élément dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="12be1-151">You can view hello details of a **Template** by clicking into an item in hello list.</span></span>

![Afficher le Modèle](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="12be1-153">Modifier une ressource de Modèle</span><span class="sxs-lookup"><span data-stu-id="12be1-153">Edit a Template resource</span></span>
<span data-ttu-id="12be1-154">Vous pouvez lancer des flux d’édition hello pour un **modèle** par élément de hello avec le bouton droit sur la liste de navigation hello ou en choisissant le bouton de commande hello modifier.</span><span class="sxs-lookup"><span data-stu-id="12be1-154">You can initiate hello edit flow for a **Template** by right clicking hello item on hello Browse list or by choosing hello Edit command button.</span></span>

![Modifier un Modèle](media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="12be1-156">Vous pouvez modifier la description de hello ou le texte du modèle de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="12be1-156">You can edit hello description or Resource Manager template text.</span></span> <span data-ttu-id="12be1-157">Vous ne pouvez pas modifier le nom de hello puisqu’il s’agit d’un nom de ressource du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="12be1-157">You cannot edit hello name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="12be1-158">Lorsque vous modifiez le modèle de gestionnaire de ressources hello JSON nous validera tooensure qu’il s’agit d’un JSON valide.</span><span class="sxs-lookup"><span data-stu-id="12be1-158">When you edit hello Resource Manager template JSON we will validate tooensure that it is valid JSON.</span></span> <span data-ttu-id="12be1-159">Choisissez **OK** , puis **enregistrer** toosave votre modèle mis à jour.</span><span class="sxs-lookup"><span data-stu-id="12be1-159">Choose **OK** and then **Save** toosave your updated template.</span></span>

![Modifier un Modèle](media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="12be1-161">Une fois hello **modèle** est enregistrée une notification de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="12be1-161">Once hello **Template** is saved you will see a confirmation notification.</span></span>

![Modifier un Modèle](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="12be1-163">Déployer une ressource de modèle</span><span class="sxs-lookup"><span data-stu-id="12be1-163">Deploy a Template resource</span></span>
<span data-ttu-id="12be1-164">Vous pouvez déployer tout **Modèle** pour lequel vous disposez d’autorisations de **lecture**.</span><span class="sxs-lookup"><span data-stu-id="12be1-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="12be1-165">flux de déploiement Hello lance le panneau de déploiement Azure modèle standard hello.</span><span class="sxs-lookup"><span data-stu-id="12be1-165">hello deployment flow launches hello standard Azure Template deployment blade.</span></span> <span data-ttu-id="12be1-166">Renseignez les valeurs hello pour tooproceed de paramètres de modèle de gestionnaire de ressources hello avec le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="12be1-166">Fill out hello values for hello Resource Manager template parameters tooproceed with hello deployment.</span></span>

![Déployer un modèle](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="12be1-168">Partager une ressource de Modèle</span><span class="sxs-lookup"><span data-stu-id="12be1-168">Share a Template resource</span></span>
<span data-ttu-id="12be1-169">Une ressource de **Modèle** peut être partagée avec vos homologues.</span><span class="sxs-lookup"><span data-stu-id="12be1-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="12be1-170">Partage se comporte de la même façon trop[attribution de rôle pour n’importe quelle ressource sur Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="12be1-170">Sharing behaves similarly too[role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="12be1-171">Hello **modèle** propriétaire accorde des autorisations tooother les utilisateurs peuvent interagir avec une ressource de modèle.</span><span class="sxs-lookup"><span data-stu-id="12be1-171">hello **Template** owner provides permissions tooother users who can interact with a Template resource.</span></span> <span data-ttu-id="12be1-172">Hello personne ou le groupe de personnes, vous partagez hello **modèle** avec sera modèle de gestionnaire de ressources en mesure de toosee hello et ses propriétés de la galerie.</span><span class="sxs-lookup"><span data-stu-id="12be1-172">hello person or group of people you share hello **Template** with will be able toosee hello Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-hello-microsoftgallery-resources"></a><span data-ttu-id="12be1-173">Contrôle d’accès pour les ressources Microsoft.Gallery hello</span><span class="sxs-lookup"><span data-stu-id="12be1-173">Access control for hello Microsoft.Gallery resources</span></span>
| <span data-ttu-id="12be1-174">Rôle</span><span class="sxs-lookup"><span data-stu-id="12be1-174">Role</span></span> | <span data-ttu-id="12be1-175">Autorisations</span><span class="sxs-lookup"><span data-stu-id="12be1-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="12be1-176">Propriétaire</span><span class="sxs-lookup"><span data-stu-id="12be1-176">Owner</span></span> |<span data-ttu-id="12be1-177">Permet un contrôle total sur la ressource de modèle hello, y compris le partage</span><span class="sxs-lookup"><span data-stu-id="12be1-177">Allows full control on hello Template resource including Share</span></span> |
| <span data-ttu-id="12be1-178">Lecteur</span><span class="sxs-lookup"><span data-stu-id="12be1-178">Reader</span></span> |<span data-ttu-id="12be1-179">Permet de lire et Execute(Deploy) sur hello ressource de modèle</span><span class="sxs-lookup"><span data-stu-id="12be1-179">Allows Read and Execute(Deploy) on hello Template resource</span></span> |
| <span data-ttu-id="12be1-180">Collaborateur</span><span class="sxs-lookup"><span data-stu-id="12be1-180">Contributor</span></span> |<span data-ttu-id="12be1-181">Accorde l’autorisation de modifier et supprimer sur hello ressource de modèle.</span><span class="sxs-lookup"><span data-stu-id="12be1-181">Allows Edit and Delete permission on hello Template resource.</span></span> <span data-ttu-id="12be1-182">Utilisateur ne peuvent pas partager hello modèle avec d’autres utilisateurs</span><span class="sxs-lookup"><span data-stu-id="12be1-182">User cannot Share hello Template with others</span></span> |

<span data-ttu-id="12be1-183">Sélectionnez **partage** sur l’élément de navigation hello par avec le bouton droit ou sur le panneau d’affichage hello d’un élément spécifique.</span><span class="sxs-lookup"><span data-stu-id="12be1-183">Select **Share** on hello browse item by right clicking or on hello view blade of a specific item.</span></span> <span data-ttu-id="12be1-184">Cette opération lance une expérience de partage.</span><span class="sxs-lookup"><span data-stu-id="12be1-184">This launches a Share experience.</span></span>

![Partager le modèle](media/share-template-portal1a.png)  <br />

 <span data-ttu-id="12be1-186">Vous pouvez maintenant choisir un rôle et une tooa de l’accès des tooprovide l’utilisateur ou un groupe particulier **modèle**.</span><span class="sxs-lookup"><span data-stu-id="12be1-186">You can now choose a role and a user or group tooprovide access tooa particular **Template**.</span></span> <span data-ttu-id="12be1-187">les rôles disponibles Hello sont propriétaire, collaborateur et le lecteur.</span><span class="sxs-lookup"><span data-stu-id="12be1-187">hello available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="12be1-188">Plus de détails dans hello [le contrôle d’accès](#access-control-for-a-tenant-resource-provider) section ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="12be1-188">More details in hello [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Partager le modèle](media/share-template-portal2b.png)  <br />

![Partager le modèle](media/share-template-portal3b.png)  <br />

<span data-ttu-id="12be1-191">Cliquez sur **Sélectionner**, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="12be1-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="12be1-192">Vous pouvez maintenant voir hello utilisateurs ou groupes vous avez ajouté les ressources toohello.</span><span class="sxs-lookup"><span data-stu-id="12be1-192">You can now see hello users or groups you added toohello resource.</span></span>

![Partager le modèle](media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="12be1-194">Un modèle peut être partagé uniquement avec des utilisateurs et groupes Bonjour même locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12be1-194">A Template can only be shared with users and groups in hello same Azure Active Directory tenant.</span></span> <span data-ttu-id="12be1-195">Si vous partagez un modèle avec une adresse de messagerie qui n’est pas dans votre client, une invitation sera envoyée demandant le locataire de hello toojoin hello utilisateur en tant qu’invité.</span><span class="sxs-lookup"><span data-stu-id="12be1-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking hello user toojoin hello tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="12be1-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12be1-196">Next steps</span></span>
* <span data-ttu-id="12be1-197">toolearn sur la création de modèles du Gestionnaire de ressources, consultez [création de modèles](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="12be1-197">toolearn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="12be1-198">les fonctions hello toounderstand que vous pouvez utiliser dans un modèle de gestionnaire de ressources, consultez [fonctions de modèle](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="12be1-198">toounderstand hello functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="12be1-199">Pour obtenir des instructions sur la conception de vos modèles, consultez [Meilleures pratiques relatives à la conception des modèles Azure Resource Manager](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="12be1-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>

