---
title: "modèle de hello aaaDownload pour une machine virtuelle Azure | Documents Microsoft"
description: "Télécharger hello templatefor un toohelp de machine virtuelle avec l’automatisation des déploiements dans le modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="528ef-103">Téléchargez le modèle de hello pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="528ef-103">Download hello template for a VM</span></span>
<span data-ttu-id="528ef-104">Lorsque vous créez une machine virtuelle dans Azure à l’aide du portail de hello ou de PowerShell, un gestionnaire de ressources du modèle est automatiquement créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="528ef-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="528ef-105">Vous pouvez utiliser cette copie de tooquickly un déploiement de modèle.</span><span class="sxs-lookup"><span data-stu-id="528ef-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="528ef-106">modèle de Hello contient des informations sur toutes les ressources hello dans un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="528ef-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="528ef-107">Pour un ordinateur virtuel, cela signifie que le modèle de hello contient tout ce qui est créé pour prendre en charge hello VM dans ce groupe de ressources, y compris des ressources de mise en réseau hello.</span><span class="sxs-lookup"><span data-stu-id="528ef-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="528ef-108">Téléchargez le modèle de hello à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="528ef-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="528ef-109">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="528ef-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="528ef-110">Menu d’un hello concentrateur, sélectionnez **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="528ef-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="528ef-111">Sélectionnez hello virtuels à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="528ef-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="528ef-112">Sélectionnez **Script Automation**.</span><span class="sxs-lookup"><span data-stu-id="528ef-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="528ef-113">Sélectionnez **télécharger** et enregistrez l’ordinateur local du tooyour fichier .zip hello.</span><span class="sxs-lookup"><span data-stu-id="528ef-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="528ef-114">Ouvrez le fichier .zip de hello et extraire le dossier de tooa fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="528ef-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="528ef-115">fichier .zip de Hello contient :</span><span class="sxs-lookup"><span data-stu-id="528ef-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="528ef-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="528ef-116">deploy.ps1</span></span>
   * <span data-ttu-id="528ef-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="528ef-117">deploy.sh</span></span> 
   * <span data-ttu-id="528ef-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="528ef-118">deployer.rb</span></span>
   * <span data-ttu-id="528ef-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="528ef-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="528ef-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="528ef-120">parameters.json</span></span>
   * <span data-ttu-id="528ef-121">template.json</span><span class="sxs-lookup"><span data-stu-id="528ef-121">template.json</span></span>

<span data-ttu-id="528ef-122">fichier de template.json Hello est le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="528ef-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="528ef-123">Téléchargez le modèle de hello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="528ef-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="528ef-124">Vous pouvez également télécharger le fichier de modèle .json hello à l’aide de hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="528ef-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="528ef-125">Vous pouvez utiliser hello `-path` paramètre tooprovide hello nom de fichier et chemin d’accès de fichier .json de hello.</span><span class="sxs-lookup"><span data-stu-id="528ef-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="528ef-126">Cet exemple montre comment le modèle de hello de toodownload pour le groupe de ressources hello nommé **myResourceGroup** toohello **C:\users\public\downloads** dossier sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="528ef-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="528ef-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="528ef-127">Next steps</span></span>
<span data-ttu-id="528ef-128">toolearn plus sur le déploiement de ressources à l’aide de modèles, consultez [procédure pas à pas de gestionnaire de ressources du modèle](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="528ef-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

