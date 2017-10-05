---
title: "Téléchargement du modèle d’une machine virtuelle Azure | Microsoft Docs"
description: "Téléchargez un modèle de machine virtuelle pour faciliter l’automatisation de déploiements dans le modèle de déploiement Resource Manager"
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
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="93a48-103">Télécharger le modèle d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="93a48-103">Download the template for a VM</span></span>
<span data-ttu-id="93a48-104">Lorsque vous créez une machine virtuelle dans Azure à l’aide du portail ou de PowerShell, un modèle Resource Manager est automatiquement créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="93a48-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="93a48-105">Vous pouvez utiliser ce modèle pour dupliquer rapidement un déploiement.</span><span class="sxs-lookup"><span data-stu-id="93a48-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="93a48-106">Le modèle contient des informations sur toutes les ressources d’un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="93a48-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="93a48-107">Pour une machine virtuelle, cela signifie que le modèle contient tout ce qui est créé pour prendre en charge la machine virtuelle dans ce groupe de ressources, notamment les ressources réseau.</span><span class="sxs-lookup"><span data-stu-id="93a48-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="93a48-108">Télécharger le modèle à l’aide du portail</span><span class="sxs-lookup"><span data-stu-id="93a48-108">Download the template using the portal</span></span>
1. <span data-ttu-id="93a48-109">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="93a48-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="93a48-110">Dans le menu hub, sélectionnez **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="93a48-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="93a48-111">Sélectionnez la machine virtuelle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="93a48-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="93a48-112">Sélectionnez **Script Automation**.</span><span class="sxs-lookup"><span data-stu-id="93a48-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="93a48-113">Sélectionnez **Télécharger** et enregistrez le fichier .zip sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="93a48-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="93a48-114">Ouvrez le fichier .zip et extrayez les fichiers dans un dossier.</span><span class="sxs-lookup"><span data-stu-id="93a48-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="93a48-115">Le fichier .zip contient :</span><span class="sxs-lookup"><span data-stu-id="93a48-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="93a48-116">deploy.ps1</span><span class="sxs-lookup"><span data-stu-id="93a48-116">deploy.ps1</span></span>
   * <span data-ttu-id="93a48-117">deploy.sh</span><span class="sxs-lookup"><span data-stu-id="93a48-117">deploy.sh</span></span> 
   * <span data-ttu-id="93a48-118">deployer.rb</span><span class="sxs-lookup"><span data-stu-id="93a48-118">deployer.rb</span></span>
   * <span data-ttu-id="93a48-119">DeploymentHelper.cs</span><span class="sxs-lookup"><span data-stu-id="93a48-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="93a48-120">parameters.json</span><span class="sxs-lookup"><span data-stu-id="93a48-120">parameters.json</span></span>
   * <span data-ttu-id="93a48-121">template.json</span><span class="sxs-lookup"><span data-stu-id="93a48-121">template.json</span></span>

<span data-ttu-id="93a48-122">Le fichier template.json est le modèle.</span><span class="sxs-lookup"><span data-stu-id="93a48-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="93a48-123">Télécharger le modèle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="93a48-123">Download the template using PowerShell</span></span>
<span data-ttu-id="93a48-124">Vous pouvez également télécharger le fichier de modèle .json à l’aide de l’applet de commande [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx).</span><span class="sxs-lookup"><span data-stu-id="93a48-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="93a48-125">Vous pouvez utiliser le paramètre `-path` afin de fournir le nom et le chemin d’accès du fichier .json.</span><span class="sxs-lookup"><span data-stu-id="93a48-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="93a48-126">Cet exemple montre comment télécharger le modèle pour le groupe de ressources nommé **myResourceGroup** vers le dossier **C:\users\public\downloads** sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="93a48-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="93a48-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93a48-127">Next steps</span></span>
<span data-ttu-id="93a48-128">Pour en savoir plus sur le déploiement des ressources à l’aide de modèles, consultez la page [Procédure pas à pas du modèle Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="93a48-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

