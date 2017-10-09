---
title: "modèle de gestionnaire de ressources Azure aaaExport | Documents Microsoft"
description: "Utilisez Gestion de ressources Azure tooexport un modèle à partir d’un groupe de ressources existant."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="f6a8a-103">Exporter un modèle Azure Resource Manager à partir de ressources existantes</span><span class="sxs-lookup"><span data-stu-id="f6a8a-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="f6a8a-104">Dans cet article, vous apprendrez comment tooexport un modèle de gestionnaire de ressources à partir de ressources existants dans votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="f6a8a-105">Vous pouvez utiliser ce toogain modèle généré une meilleure compréhension de la syntaxe de modèle.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="f6a8a-106">Il existe deux façons tooexport un modèle :</span><span class="sxs-lookup"><span data-stu-id="f6a8a-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="f6a8a-107">Vous pouvez exporter hello **modèle réel utilisé pour le déploiement**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="f6a8a-108">modèle exporté du Hello inclut toutes les variables et les paramètres de hello exactement comme ils apparaissent dans le modèle d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="f6a8a-109">Cette approche est utile lorsque vous avez déployé des ressources via le portail de hello et souhaitez toosee hello modèle toocreate ces ressources.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="f6a8a-110">Ce modèle est facilement utilisable.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-110">This template is readily usable.</span></span> 
* <span data-ttu-id="f6a8a-111">Vous pouvez exporter un **généré le modèle qui représente l’état actuel de hello hello du groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="f6a8a-112">modèle exporté du Hello n’est pas basé sur un modèle que vous avez utilisé pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="f6a8a-113">Au lieu de cela, il crée un modèle qui est un instantané hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="f6a8a-114">modèle exporté du Hello possède de nombreuses valeurs codées en dur et probablement pas autant de paramètres que vous définissez généralement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="f6a8a-115">Cette approche est utile lorsque vous avez modifié le groupe de ressources hello après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="f6a8a-116">Ce modèle doit généralement être modifié avant d’être utilisable.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="f6a8a-117">Cette rubrique montre les deux approches via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="f6a8a-118">Déployer des ressources</span><span class="sxs-lookup"><span data-stu-id="f6a8a-118">Deploy resources</span></span>
<span data-ttu-id="f6a8a-119">Commençons par tooAzure de ressources que vous pouvez utiliser pour l’exportation en tant que modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="f6a8a-120">Si vous avez déjà un groupe de ressources dans votre abonnement que vous souhaitez tooexport tooa modèle, vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="f6a8a-121">reste Hello de cet article suppose que vous avez déployé l’application hello web et les solutions de base de données SQL présentées dans cette section.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="f6a8a-122">Si vous utilisez une autre solution, votre expérience peut être un peu différente, mais les étapes hello tooexport un modèle sont hello même.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="f6a8a-123">Bonjour [portail Azure](https://portal.azure.com), sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![sélectionner nouveau](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="f6a8a-125">Recherchez **web application + SQL** et sélectionnez-le dans les options disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![recherche application web et SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="f6a8a-127">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-127">Select **Create**.</span></span>

      ![sélectionner créer](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="f6a8a-129">Indiquez les valeurs de hello requis pour hello web app et de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="f6a8a-130">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-130">Select **Create**.</span></span>

      ![fournir une valeur web et SQL](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="f6a8a-132">déploiement de Hello peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-132">hello deployment may take a minute.</span></span> <span data-ttu-id="f6a8a-133">Après déploiement de hello, votre abonnement contient des solutions de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="f6a8a-134">Voir un modèle à partir de l’historique de déploiement</span><span class="sxs-lookup"><span data-stu-id="f6a8a-134">View template from deployment history</span></span>
1. <span data-ttu-id="f6a8a-135">Accédez à panneau de groupe de ressources toohello pour votre nouveau groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="f6a8a-136">Notez que ce panneau hello affiche le résultat de hello du dernier déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="f6a8a-137">Sélectionnez ce lien.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-137">Select this link.</span></span>
   
      ![panneau du groupe de ressources](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="f6a8a-139">Vous voyez un historique des déploiements pour le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="f6a8a-140">Dans ce cas, les lames hello répertorie probablement un seul déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="f6a8a-141">Sélectionnez ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-141">Select this deployment.</span></span>
   
     ![dernier déploiement](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="f6a8a-143">Panneau de Hello affiche un résumé du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="f6a8a-144">Hello résumé inclut les valeurs hello que vous avez fourni pour les paramètres état hello du déploiement de hello et ses opérations.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="f6a8a-145">modèle hello toosee que vous avez utilisé pour le déploiement de hello, sélectionnez **modèle d’affichage de**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![afficher le résumé du déploiement](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="f6a8a-147">Le Gestionnaire de ressources récupère hello suivant sept fichiers pour vous :</span><span class="sxs-lookup"><span data-stu-id="f6a8a-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="f6a8a-148">**Modèle** -modèle hello qui définit l’infrastructure hello pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="f6a8a-149">Lorsque vous avez créé le compte de stockage hello via le portail de hello, Gestionnaire de ressources utilisé un toodeploy modèle il et enregistré ce modèle pour référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="f6a8a-150">**Paramètres** -un fichier de paramètres que vous pouvez utiliser toopass dans les valeurs durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="f6a8a-151">Il contient des valeurs hello que vous avez fourni pendant le déploiement de première hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="f6a8a-152">Vous pouvez modifier ces valeurs lorsque vous redéployez le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="f6a8a-153">**CLI** -fichier de script Azure une interface de ligne de commande (CLI) que vous pouvez utiliser le modèle de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="f6a8a-154">**CLI 2.0** -fichier de script Azure une interface de ligne de commande (CLI) que vous pouvez utiliser le modèle de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="f6a8a-155">**PowerShell** -fichier de script d’un Azure PowerShell que vous pouvez utiliser le modèle de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="f6a8a-156">**.NET** -classe A .NET que vous pouvez utiliser le modèle de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="f6a8a-157">**Ruby** -classe A Ruby que vous pouvez utiliser le modèle de hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="f6a8a-158">fichiers de Hello sont disponibles via des liens entre les lames hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="f6a8a-159">Par défaut, panneau de hello affiche le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-159">By default, hello blade displays hello template.</span></span>
      
       ![Afficher le modèle](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="f6a8a-161">Ce modèle est le modèle réel de hello utilisé toocreate votre application web et la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="f6a8a-162">Notez qu’il contient des paramètres qui vous permettent de tooprovide des valeurs différentes au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="f6a8a-163">toolearn en savoir plus sur la structure de hello d’un modèle, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f6a8a-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="f6a8a-164">Exporter le modèle de hello du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f6a8a-164">Export hello template from resource group</span></span>
<span data-ttu-id="f6a8a-165">Si vous avez manuellement modifié vos ressources ou l’ajout de ressources dans plusieurs déploiements, la récupération d’un modèle à partir de l’historique de déploiement hello ne reflète pas état actuel de hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="f6a8a-166">Cette section vous montre comment tooexport un modèle qui reflète hello état actuel du groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="f6a8a-167">Vous ne pouvez pas exporter un modèle pour un groupe de ressources qui contient plus de 200 ressources.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="f6a8a-168">modèle de hello tooview pour un groupe de ressources, sélectionnez **script d’automatisation**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![exporter un groupe de ressources](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="f6a8a-170">Le Gestionnaire de ressources prend la valeur hello ressources hello groupe de ressources et génère un modèle pour ces ressources.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="f6a8a-171">Pas tous les types de ressources prend en charge la fonction de modèle d’exportation hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="f6a8a-172">Vous pouvez voir un message d’erreur indiquant qu’il existe un problème avec l’exportation de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="f6a8a-173">Vous apprendrez comment toohandle ces problèmes dans hello [correctif exportation problèmes](#fix-export-issues) section.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="f6a8a-174">Vous consultez à nouveau hello six fichiers que vous pouvez utiliser la solution de hello tooredeploy.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="f6a8a-175">Toutefois, ce modèle de temps de hello est légèrement différent.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="f6a8a-176">Notez que le modèle hello généré contient moins de paramètres que le modèle hello dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="f6a8a-177">En outre, nombre de valeurs hello (par exemple, l’emplacement et les valeurs de SKU) sont codés en dur dans ce modèle, plutôt que d’accepter une valeur de paramètre.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="f6a8a-178">Avant de réutiliser ce modèle, vous pourriez tooedit hello modèle toomake améliore l’utilisation des paramètres.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="f6a8a-179">Vous disposez de deux options pour continuer toowork avec ce modèle.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="f6a8a-180">Vous pouvez télécharger le modèle de hello et travailler dessus localement avec un éditeur JSON.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="f6a8a-181">Ou bien, vous pouvez enregistrer la bibliothèque de modèles de tooyour hello et travailler dessus via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="f6a8a-182">Si vous savez à l’aide d’un éditeur JSON comme [VS Code](https://code.visualstudio.com/) ou [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), vous pouvez télécharger le modèle hello localement et à l’aide de cet éditeur.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="f6a8a-183">toowork localement, sélectionnez **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-183">toowork locally, select **Download**.</span></span>
   
      ![télécharger un modèle](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="f6a8a-185">Si vous n’êtes pas configuré avec un éditeur JSON, vous préférerez peut-être modifier le modèle hello via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="f6a8a-186">reste Hello de cette rubrique suppose que vous avez enregistré la bibliothèque de modèles de tooyour hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="f6a8a-187">Toutefois, vous vous hello même toohello modèle modifications de la syntaxe si en local avec un éditeur JSON ou via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="f6a8a-188">toowork via le portail de hello, sélectionnez **ajouter toolibrary**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![Ajouter toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="f6a8a-190">Lorsque vous ajoutez une bibliothèque de toohello de modèles, donner au modèle de hello un nom et une description.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="f6a8a-191">Sélectionnez ensuite **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-191">Then, select **Save**.</span></span>
   
     ![définir les valeurs du modèle](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="f6a8a-193">tooview un modèle enregistré dans votre bibliothèque, sélectionnez **davantage de services**, type **modèles** toofilter des résultats, sélectionnez **modèles**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![trouver des modèles](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="f6a8a-195">Sélectionnez modèle hello portant hello, que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-195">Select hello template with hello name you saved.</span></span>
   
      ![sélectionner un modèle](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="f6a8a-197">Personnaliser le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="f6a8a-197">Customize hello template</span></span>
<span data-ttu-id="f6a8a-198">fonctionnement du modèle Hello exportée précis que si vous souhaitez toocreate hello même web app et la base de données SQL pour chaque déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="f6a8a-199">Toutefois, Resource Manager propose des options permettant de déployer des modèles avec une plus grande flexibilité.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="f6a8a-200">Cet article explique les paramètres tooadd pour hello base de mot de passe et le nom d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="f6a8a-201">Vous pouvez utiliser cette même tooadd d’approche davantage de flexibilité pour les autres valeurs dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="f6a8a-202">modèle de toocustomize hello, sélectionnez **modifier**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![afficher le modèle](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="f6a8a-204">Sélectionnez le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-204">Select hello template.</span></span>
   
     ![modifier un modèle](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="f6a8a-206">les valeurs hello toobe toopass en mesure que vous pouvez toospecify pendant le déploiement, ajoutent hello suivant deux paramètres toohello **paramètres** section dans le modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="f6a8a-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="f6a8a-207">toouse nouveaux paramètres hello, remplacez la définition de serveur SQL hello Bonjour **ressources** section.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="f6a8a-208">Notez que **administratorLogin** et **administratorLoginPassword** utilisent maintenant des valeurs de paramètre.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="f6a8a-209">Sélectionnez **OK** lorsque vous avez terminé la modification de modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="f6a8a-210">Sélectionnez **enregistrer** modèle toohello de modifications de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![enregistrer un modèle](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="f6a8a-212">modèle de tooredeploy hello mis à jour, sélectionnez **déployer**.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![déployer un modèle](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="f6a8a-214">Fournir des valeurs de paramètre et sélectionnez une ressource toodeploy hello regrouper à.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="f6a8a-215">Résoudre les problèmes d’exportation</span><span class="sxs-lookup"><span data-stu-id="f6a8a-215">Fix export issues</span></span>
<span data-ttu-id="f6a8a-216">Pas tous les types de ressources prend en charge la fonction de modèle d’exportation hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="f6a8a-217">tooresolve ce problème, ajoutez les ressources manquantes hello dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="f6a8a-218">message d’erreur Hello inclut les types de ressources hello qui ne peuvent pas être exportées.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="f6a8a-219">Recherchez le type de ressource dans [Référence de modèle](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="f6a8a-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="f6a8a-220">Par exemple, toomanually ajouter une passerelle de réseau virtuel, consultez [référence de modèle Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="f6a8a-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="f6a8a-221">Vous rencontrerez des problèmes d’exportation uniquement lors de l’exportation à partir d’un groupe de ressources et non à partir de votre historique de déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="f6a8a-222">Si votre dernier déploiement représente avec précision l’état actuel de hello hello du groupe de ressources, vous devez exporter le modèle de hello à partir de l’historique de déploiement hello plutôt qu’à partir du groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="f6a8a-223">Exporter à partir d’un groupe de ressources lorsque vous avez apporté des modifications toohello ressource groupe qui ne sont pas définis dans un modèle unique.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f6a8a-224">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6a8a-224">Next steps</span></span>
<span data-ttu-id="f6a8a-225">Vous avez appris comment tooexport un modèle à partir des ressources que vous avez créé dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f6a8a-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="f6a8a-226">Vous pouvez déployer un modèle avec [PowerShell](resource-group-template-deploy.md), [l’interface de ligne de commande Azure](resource-group-template-deploy-cli.md) ou [l’API REST](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="f6a8a-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="f6a8a-227">toosee tooexport un modèle via PowerShell, voir [à l’aide de Azure PowerShell avec Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f6a8a-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="f6a8a-228">toosee tooexport un modèle via l’interface CLI d’Azure, voir [hello d’utilisation CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f6a8a-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

