---
title: "modèles d’aaaDeploy avec Visual Studio, dans la pile de Azure | Documents Microsoft"
description: "Découvrez comment les modèles toodeploy avec Visual Studio, dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: aea917b585a30ef4fbe7263db66f0659b56b21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a><span data-ttu-id="85856-103">Déploiement de modèles dans Azure Stack à l’aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="85856-103">Deploy templates in Azure Stack using Visual Studio</span></span>

<span data-ttu-id="85856-104">Utilisez le kit de développement Visual Studio toodeploy Azure Resource Manager modèles toohello pile d’Azure.</span><span class="sxs-lookup"><span data-stu-id="85856-104">Use Visual Studio toodeploy Azure Resource Manager templates toohello Azure Stack development kit.</span></span>

1. <span data-ttu-id="85856-105">[Installer et connecter](azure-stack-install-visual-studio.md) tooAzure pile avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85856-105">[Install and connect](azure-stack-install-visual-studio.md) tooAzure Stack with Visual Studio.</span></span>
2. <span data-ttu-id="85856-106">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="85856-106">Open Visual Studio.</span></span>
3. <span data-ttu-id="85856-107">Cliquez sur **fichier**, cliquez sur **nouveau**et Bonjour **nouveau projet** boîte dialogue, cliquez sur **groupe de ressources Azure**.</span><span class="sxs-lookup"><span data-stu-id="85856-107">Click **File**, click **New**, and in hello **New Project** dialog box click **Azure Resource Group**.</span></span>
4. <span data-ttu-id="85856-108">Entrez un **nom** pour hello nouveau projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="85856-108">Enter a **Name** for hello new project, and then click **OK**.</span></span>
5. <span data-ttu-id="85856-109">Bonjour **sélectionner un modèle Azure** boîte de dialogue, modification hello *afficher les modèles de cet emplacement* déroulante trop**démarrage rapide de pile Azure**</span><span class="sxs-lookup"><span data-stu-id="85856-109">In hello **Select Azure Template** dialog box, change hello *Show templates from this location* drop-down too**Azure Stack Quickstart**</span></span>
6. <span data-ttu-id="85856-110">Cliquez sur **101-create-storage-account**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="85856-110">Click **101-create-storage-account**, and then click **OK**.</span></span>  
7. <span data-ttu-id="85856-111">Dans le nouveau projet, vous pouvez voir une liste des modèles de hello disponibles en développant hello **modèles** nœud Bonjour **l’Explorateur de solutions** volet.</span><span class="sxs-lookup"><span data-stu-id="85856-111">In your new project, you can see a list of hello templates available by expanding hello **Templates** node in hello **Solution Explorer** pane.</span></span>
8. <span data-ttu-id="85856-112">Bonjour **l’Explorateur de solutions** volet, avec le bouton hello nom de votre projet, cliquez sur **déployer**, puis cliquez sur **nouveau déploiement**.</span><span class="sxs-lookup"><span data-stu-id="85856-112">In hello **Solution Explorer** pane, right-click hello name of your project, click **Deploy**, then click **New Deployment**.</span></span>
9. <span data-ttu-id="85856-113">Bonjour **déployer tooResource groupe** la boîte de dialogue hello **abonnement** liste déroulante, sélectionnez votre abonnement Microsoft Azure pile.</span><span class="sxs-lookup"><span data-stu-id="85856-113">In hello **Deploy tooResource Group** dialog box, in hello **Subscription** drop-down, select your Microsoft Azure Stack subscription.</span></span>
10. <span data-ttu-id="85856-114">Bonjour **groupe de ressources** liste, choisissez un groupe de ressources existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="85856-114">In hello **Resource Group** list, choose an existing resource group or create a new one.</span></span>
11. <span data-ttu-id="85856-115">Bonjour **emplacement du groupe de ressources** liste, choisissez un emplacement, puis cliquez sur **déployer**.</span><span class="sxs-lookup"><span data-stu-id="85856-115">In hello **Resource group location** list, choose a location, and then click **Deploy**.</span></span>
12. <span data-ttu-id="85856-116">Bonjour **modifier les paramètres** boîte de dialogue, entrez des valeurs pour les paramètres hello (qui varient selon le modèle), puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="85856-116">In hello **Edit Parameters** dialog box, enter values for hello parameters (which vary by template), and then click **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85856-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="85856-117">Next steps</span></span>
[<span data-ttu-id="85856-118">Déployer des modèles de ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="85856-118">Deploy templates with hello command line</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="85856-119">Développer des modèles pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="85856-119">Develop templates for Azure Stack</span></span>](azure-stack-develop-templates.md)

