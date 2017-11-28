---
title: "échelle de machines virtuelles aaaMake jeux disponible dans la pile de Azure"
description: "Découvrez comment un administrateur de cloud peut ajouter toohello de mise à l’échelle de machine virtuelle Azure Marketplace de pile"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 14365d62ac2f2bc453c25ce4769464eb30180ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a><span data-ttu-id="59dde-103">Mettre les groupes de machines virtuelles identiques à disposition dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="59dde-103">Make virtual machine scale sets available in Azure Stack</span></span>
<span data-ttu-id="59dde-104">Les groupes de machines virtuelles identiques constituent une ressource de calcul Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="59dde-104">Virtual machine scale sets are an Azure Stack compute resource.</span></span> <span data-ttu-id="59dde-105">Vous pouvez les utiliser toodeploy et gérer un ensemble de machines virtuelles identiques.</span><span class="sxs-lookup"><span data-stu-id="59dde-105">You can use them toodeploy and manage a set of identical virtual machines.</span></span> <span data-ttu-id="59dde-106">Avec tous les ordinateurs virtuels configurés hello identiques, identiques ne nécessitent pas configuration anticipée des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="59dde-106">With all virtual machines configured hello same, scale sets don’t require pre-provisioning of virtual machines.</span></span> <span data-ttu-id="59dde-107">Il est plus facile toobuild à grande échelle des services qui ciblent des charges de travail big compute et données volumineuses.</span><span class="sxs-lookup"><span data-stu-id="59dde-107">It's easier toobuild large-scale services that target big compute, big data, and containerized workloads.</span></span>

<span data-ttu-id="59dde-108">Cette rubrique vous guide tout au long de l’échelle hello processus toomake jeux disponibles Bonjour Azure Marketplace de pile.</span><span class="sxs-lookup"><span data-stu-id="59dde-108">This topic guides you through hello process toomake scale sets available in hello Azure Stack Marketplace.</span></span> <span data-ttu-id="59dde-109">Après avoir terminé cette procédure, vos utilisateurs peuvent ajouter, échelle de machines virtuelles définit tootheir abonnements.</span><span class="sxs-lookup"><span data-stu-id="59dde-109">After you complete this procedure, your users can add virtual machine scale sets tootheir subscriptions.</span></span>

<span data-ttu-id="59dde-110">Les groupes de machines virtuelles identiques sur Azure Stack suivent le même principe que sur Azure.</span><span class="sxs-lookup"><span data-stu-id="59dde-110">Virtual machine scale sets on Azure Stack are like virtual machine scale sets on Azure.</span></span> <span data-ttu-id="59dde-111">Pour plus d’informations, consultez hello suivant vidéos :</span><span class="sxs-lookup"><span data-stu-id="59dde-111">For more information, see hello following videos:</span></span>
* [<span data-ttu-id="59dde-112">Mark Russinovich parle des groupes identiques Azure</span><span class="sxs-lookup"><span data-stu-id="59dde-112">Mark Russinovich talks Azure scale sets</span></span>](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [<span data-ttu-id="59dde-113">Jeux de mise à l’échelle de machine virtuelle, avec Guy Bowerman</span><span class="sxs-lookup"><span data-stu-id="59dde-113">Virtual Machine Scale Sets with Guy Bowerman</span></span>](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

<span data-ttu-id="59dde-114">Sur Azure Stack, les groupes de machines virtuelles identiques ne sont pas compatibles avec la mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="59dde-114">On Azure Stack, Virtual Machine Scale Sets do not support auto-scale.</span></span> <span data-ttu-id="59dde-115">Vous pouvez ajouter plusieurs instances tooa mise à l’échelle définie à l’aide du portail de pile de Azure hello, des modèles de gestionnaire de ressources ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59dde-115">You can add more instances tooa scale set using hello Azure Stack portal, Resource Manager templates, or PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59dde-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="59dde-116">Prerequisites</span></span>
* <span data-ttu-id="59dde-117">**PowerShell et outils**</span><span class="sxs-lookup"><span data-stu-id="59dde-117">**Powershell and tools**</span></span>

   <span data-ttu-id="59dde-118">Installer et PowerShell configuré pour la pile d’Azure et les outils de pile de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="59dde-118">Install and configured PowerShell for Azure Stack and hello Azure Stack tools.</span></span> <span data-ttu-id="59dde-119">Consultez la page [Devenir opérationnel avec PowerShell dans Azure Stack](azure-stack-powershell-configure-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="59dde-119">See [Get up and running with PowerShell in Azure Stack](azure-stack-powershell-configure-quickstart.md).</span></span>

   <span data-ttu-id="59dde-120">Après avoir installé les outils de pile de Azure hello, assurez-vous d’importer hello suivant le module PowerShell (toohello relative du chemin d’accès. dossier \ComputeAdmin dans le dossier de hello AzureStack-outils-master) :</span><span class="sxs-lookup"><span data-stu-id="59dde-120">After you install hello Azure Stack tools, make sure you import hello following PowerShell module (path relative toohello .\ComputeAdmin folder in hello AzureStack-Tools-master folder):</span></span>

        Import-Module .\AzureStack.ComputeAdmin.psm1

* <span data-ttu-id="59dde-121">**Image du système d’exploitation**</span><span class="sxs-lookup"><span data-stu-id="59dde-121">**Operating system image**</span></span>

   <span data-ttu-id="59dde-122">Si vous n’avez pas ajouté une tooyour d’image de système d’exploitation Azure Marketplace de pile, consultez [marketplace de la pile de Azure ajouter hello Windows Server 2016 VM image toohello](azure-stack-add-default-image.md).</span><span class="sxs-lookup"><span data-stu-id="59dde-122">If you haven’t added an operating system image tooyour Azure Stack Marketplace, see [Add hello Windows Server 2016 VM image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>

   <span data-ttu-id="59dde-123">Pour la prise en charge de Linux, téléchargez Ubuntu Server 16.04 et l’ajouter à l’aide de ```Add-AzsVMImage``` avec les paramètres suivants de hello : ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span><span class="sxs-lookup"><span data-stu-id="59dde-123">For Linux support, download Ubuntu Server 16.04 and add it using ```Add-AzsVMImage``` with hello following parameters: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span></span>

## <a name="add-hello-virtual-machine-scale-set"></a><span data-ttu-id="59dde-124">Ajouter l’ensemble d’échelle de machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="59dde-124">Add hello virtual machine scale set</span></span>

<span data-ttu-id="59dde-125">Modifier hello PowerShell suivantes pour votre environnement de script et exécutez-le tooadd un tooyour de jeu de mise à l’échelle machine virtuelle Azure Marketplace de pile.</span><span class="sxs-lookup"><span data-stu-id="59dde-125">Edit hello following PowerShell script for your environment and then run it tooadd a virtual machine scale set tooyour Azure Stack Marketplace.</span></span> 

<span data-ttu-id="59dde-126">``$User``est un compte de hello que vous utilisez le portail d’administration tooconnect hello.</span><span class="sxs-lookup"><span data-stu-id="59dde-126">``$User`` is hello account you use tooconnect hello administrator portal.</span></span> <span data-ttu-id="59dde-127">Par exemple, serviceadmin@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="59dde-127">For example, serviceadmin@contoso.onmicrosoft.com.</span></span>

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a><span data-ttu-id="59dde-128">Supprimer un groupe de machines virtuelles identiques</span><span class="sxs-lookup"><span data-stu-id="59dde-128">Remove a virtual machine scale set</span></span>

<span data-ttu-id="59dde-129">tooremove un élément de galerie de machine virtuelle mise à l’échelle ensemble, exécutez hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="59dde-129">tooremove a virtual machine scale set gallery item, run hello following PowerShell command:</span></span>

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> <span data-ttu-id="59dde-130">élément de la galerie Hello ne peut pas être supprimée immédiatement.</span><span class="sxs-lookup"><span data-stu-id="59dde-130">hello gallery item may not be removed immediately.</span></span> <span data-ttu-id="59dde-131">Vous devrez peut-être portal de hello toorefresh plusieurs fois avant qu’il soit supprimé hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="59dde-131">You may need toorefresh hello portal several times before it is removed from hello Marketplace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="59dde-132">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="59dde-132">Next steps</span></span>
[<span data-ttu-id="59dde-133">Forum aux questions sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="59dde-133">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

