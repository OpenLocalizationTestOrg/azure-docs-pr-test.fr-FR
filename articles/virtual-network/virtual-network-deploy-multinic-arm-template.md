---
title: "aaaCreate une machine virtuelle avec plusieurs cartes réseau - modèle Azure Resource Manager | Documents Microsoft"
description: "Créez une machine virtuelle avec plusieurs cartes réseau à l’aide d’un modèle Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a><span data-ttu-id="f3503-103">Créer une machine virtuelle avec plusieurs cartes réseau à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="f3503-103">Create a VM with multiple NICs using a template</span></span>
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f3503-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f3503-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="f3503-105">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f3503-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="f3503-106">étapes suivantes Hello utilisent un groupe de ressources nommé *IaaSStory* pour les serveurs WEB hello et un groupe de ressources nommé *IaaSStory-principal* pour les serveurs de base de données de hello.</span><span class="sxs-lookup"><span data-stu-id="f3503-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3503-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f3503-107">Prerequisites</span></span>
<span data-ttu-id="f3503-108">Avant de pouvoir créer hello des serveurs de base de données, vous devez toocreate hello *IaaSStory* groupe de ressources avec toutes les ressources nécessaires hello pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="f3503-108">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="f3503-109">fin de ces ressources, toocreate hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3503-109">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="f3503-110">Accédez trop[page de modèle hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="f3503-110">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="f3503-111">Dans la page de modèle hello, toohello à droite de **groupe de ressources Parent**, cliquez sur **déployer tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="f3503-111">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="f3503-112">Si nécessaire, modifiez les valeurs de paramètre hello, puis suivez les étapes de hello hello Azure en version préliminaire toodeploy portail hello groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f3503-112">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3503-113">Assurez-vous que vos noms de compte de stockage sont uniques.</span><span class="sxs-lookup"><span data-stu-id="f3503-113">Make sure your storage account names are unique.</span></span> <span data-ttu-id="f3503-114">Vous ne pouvez pas avoir des noms de compte de stockage en double dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f3503-114">You cannot have duplicate storage account names in Azure.</span></span>
> 

## <a name="understand-hello-deployment-template"></a><span data-ttu-id="f3503-115">Comprendre le modèle de déploiement hello</span><span class="sxs-lookup"><span data-stu-id="f3503-115">Understand hello deployment template</span></span>
<span data-ttu-id="f3503-116">Avant de déployer les modèles hello fournis dans cette documentation, assurez-vous que vous comprenez ce qu’il fait.</span><span class="sxs-lookup"><span data-stu-id="f3503-116">Before you deploy hello template provided with this documentation, make sure you understand what it does.</span></span> <span data-ttu-id="f3503-117">Hello suit fournit une bonne vue d’ensemble du modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="f3503-117">hello following steps provide a good overview of hello template:</span></span>

1. <span data-ttu-id="f3503-118">Accédez trop[page de modèle hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="f3503-118">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="f3503-119">Cliquez sur **azuredeploy.json** fichier de modèle tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="f3503-119">Click **azuredeploy.json** tooopen hello template file.</span></span>
3. <span data-ttu-id="f3503-120">Hello d’avis *osType* paramètre répertoriée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-120">Notice hello *osType* parameter listed below.</span></span> <span data-ttu-id="f3503-121">Ce paramètre est utilisé tooselect le toouse d’image de machine virtuelle pour le serveur de base de données hello, ainsi que plusieurs systèmes d’exploitation les paramètres associés.</span><span class="sxs-lookup"><span data-stu-id="f3503-121">This parameter is used tooselect what VM image toouse for hello database server, along with multiple operating system related settings.</span></span>

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. <span data-ttu-id="f3503-122">Faites défiler la liste des variables toohello et vérifiez la définition de hello pour hello **dbVMSetting** variables, répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-122">Scroll down toohello list of variables, and check hello definition for hello **dbVMSetting** variables, listed below.</span></span> <span data-ttu-id="f3503-123">Il reçoit l’un des éléments de tableau hello contenues dans hello **dbVMSettings** variable.</span><span class="sxs-lookup"><span data-stu-id="f3503-123">It receives one of hello array elements contained in hello **dbVMSettings** variable.</span></span> <span data-ttu-id="f3503-124">Si vous êtes familiarisé avec la terminologie de développement logiciel, vous pouvez afficher hello **dbVMSettings** variable comme une table de hachage ou un dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="f3503-124">If you are familiar with software development terminology, you can view hello **dbVMSettings** variable as a hash table, or a dictionary.</span></span>

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. <span data-ttu-id="f3503-125">Supposons que vous décidez de toodeploy les machines virtuelles Windows en cours d’exécution SQL dans hello back-end.</span><span class="sxs-lookup"><span data-stu-id="f3503-125">Suppose you decide toodeploy Windows VMs running SQL in hello back-end.</span></span> <span data-ttu-id="f3503-126">Puis hello valeur pour **osType** serait *Windows*et hello **dbVMSetting** variable contient l’élément hello répertoriée ci-dessous, qui représente la première valeur de hello Bonjour **dbVMSettings** variable.</span><span class="sxs-lookup"><span data-stu-id="f3503-126">Then hello value for **osType** would be *Windows*, and hello **dbVMSetting** variable would contain hello element listed below, which represents hello first value in hello **dbVMSettings** variable.</span></span>

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. <span data-ttu-id="f3503-127">Hello d’avis **vmSize** contient la valeur de hello *Standard_DS3*.</span><span class="sxs-lookup"><span data-stu-id="f3503-127">Notice hello **vmSize** contains hello value *Standard_DS3*.</span></span> <span data-ttu-id="f3503-128">Utilisez hello de plusieurs cartes réseau autorisent uniquement certaines tailles de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3503-128">Only certain VM sizes allow for hello use of multiple NICs.</span></span> <span data-ttu-id="f3503-129">Vous pouvez vérifier les tailles de machine virtuelle prend en charge plusieurs cartes réseau en lisant hello [tailles de machine virtuelle Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [tailles de Linux VM](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span><span class="sxs-lookup"><span data-stu-id="f3503-129">You can verify which VM sizes support multiple NICs by reading hello [Windows VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux VM sizes](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.</span></span>

7. <span data-ttu-id="f3503-130">Faites défiler la liste trop**ressources** et avis hello premier élément.</span><span class="sxs-lookup"><span data-stu-id="f3503-130">Scroll down too**resources** and notice hello first element.</span></span> <span data-ttu-id="f3503-131">Il décrit un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="f3503-131">It describes a storage account.</span></span> <span data-ttu-id="f3503-132">Ce compte de stockage sera utilisés par chaque ordinateur virtuel de la base de données des disques de données utilisé toomaintain hello.</span><span class="sxs-lookup"><span data-stu-id="f3503-132">This storage account will be used toomaintain hello data disks used by each database VM.</span></span> <span data-ttu-id="f3503-133">Dans ce scénario, chaque machine virtuelle de base de données possède un disque de système d’exploitation stocké dans le stockage standard et deux disques de données stockés dans le stockage SSD (Premium).</span><span class="sxs-lookup"><span data-stu-id="f3503-133">In this scenario, each database VM has an OS disk stored in regular storage, and two data disks stored in SSD (premium) storage.</span></span>

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. <span data-ttu-id="f3503-134">Faites défiler toohello de ressource suivant, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-134">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="f3503-135">Cette ressource représente hello que carte réseau utilisée pour l’accès de base de données dans chaque base de données de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3503-135">This resource represents hello NIC used for database access in each database VM.</span></span> <span data-ttu-id="f3503-136">Utilisation de hello avis de hello **copie** fonction de cette ressource.</span><span class="sxs-lookup"><span data-stu-id="f3503-136">Notice hello use of hello **copy** function in this resource.</span></span> <span data-ttu-id="f3503-137">Hello modèle vous permet de toodeploy comme de nombreux ordinateurs virtuels que vous le souhaitez, en fonction de hello **dbCount** paramètre.</span><span class="sxs-lookup"><span data-stu-id="f3503-137">hello template allows you toodeploy as many VMs as you want, based on hello **dbCount** parameter.</span></span> <span data-ttu-id="f3503-138">Par conséquent, vous devez toocreate hello du même montant de cartes réseau pour l’accès de base de données, un pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3503-138">Therefore you need toocreate hello same amount of NICs for database access, one for each VM.</span></span>

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. <span data-ttu-id="f3503-139">Faites défiler toohello de ressource suivant, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-139">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="f3503-140">Cette ressource représente hello que carte réseau utilisée pour la gestion de chaque machine virtuelle de la base de données.</span><span class="sxs-lookup"><span data-stu-id="f3503-140">This resource represents hello NIC used for management in each database VM.</span></span> <span data-ttu-id="f3503-141">Une fois encore, vous devez avoir une carte réseau pour chaque machine virtuelle de base de données.</span><span class="sxs-lookup"><span data-stu-id="f3503-141">Once again, you need one of these NICs for each database VM.</span></span> <span data-ttu-id="f3503-142">Hello d’avis **sécurité réseau** élément, liaison d’un groupe de sécurité réseau qui permet l’accès tooRDP/SSH toothis carte réseau uniquement.</span><span class="sxs-lookup"><span data-stu-id="f3503-142">Notice hello **networkSecurityGroup** element, linking an NSG that allows access tooRDP/SSH toothis NIC only.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. <span data-ttu-id="f3503-143">Faites défiler toohello de ressource suivant, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-143">Scroll down toohello next resource, as listed below.</span></span> <span data-ttu-id="f3503-144">Cette ressource représente un toobe de jeu de disponibilité partagé par tous les ordinateurs virtuels de base de données.</span><span class="sxs-lookup"><span data-stu-id="f3503-144">This resource represents an availability set toobe shared by all database VMs.</span></span> <span data-ttu-id="f3503-145">De cette façon, vous assurer qu’il y aura toujours une machine virtuelle Bonjour configuré pour s’exécuter lors de la maintenance.</span><span class="sxs-lookup"><span data-stu-id="f3503-145">That way, you guarantee that there will always be one VM in hello set running during maintenance.</span></span>

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. <span data-ttu-id="f3503-146">Faites défiler les ressources suivant toohello.</span><span class="sxs-lookup"><span data-stu-id="f3503-146">Scroll down toohello next resource.</span></span> <span data-ttu-id="f3503-147">Cette ressource représente la base de données de hello machines virtuelles, comme dans hello tout d’abord quelques lignes répertoriées ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-147">This resource represents hello database VMs, as seen in hello first few lines listed below.</span></span> <span data-ttu-id="f3503-148">Utilisation de hello avis de hello **copie** fonctionne à nouveau, de s’assurer que plusieurs ordinateurs virtuels sont créés en fonction hello **dbCount** paramètre.</span><span class="sxs-lookup"><span data-stu-id="f3503-148">Notice hello use of hello **copy** function again, ensuring that multiple VMs are created based on hello **dbCount** parameter.</span></span> <span data-ttu-id="f3503-149">Notez également hello **dependsOn** collection.</span><span class="sxs-lookup"><span data-stu-id="f3503-149">Also notice hello **dependsOn** collection.</span></span> <span data-ttu-id="f3503-150">Il répertorie les deux cartes réseau qui est nécessaire toobe créé avant hello qu'ordinateur virtuel est déployé, ainsi que le groupe à haute disponibilité hello et compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="f3503-150">It lists two NICs being necessary toobe created before hello VM is deployed, along with hello availability set, and hello storage account.</span></span>

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. <span data-ttu-id="f3503-151">Faites défiler toohello de ressource de machine virtuelle hello **VM** élément, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-151">Scroll down in hello VM resource toohello **networkProfile** element, as listed below.</span></span> <span data-ttu-id="f3503-152">Notez que deux cartes réseau sont référencées pour chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3503-152">Notice that there are two NICs being reference for each VM.</span></span> <span data-ttu-id="f3503-153">Lorsque vous créez plusieurs cartes réseau pour un ordinateur virtuel, vous devez définir hello **principal** propriété de l’une des cartes réseau de hello trop*true*, et hello reste trop*false*.</span><span class="sxs-lookup"><span data-stu-id="f3503-153">When you create multiple NICs for a VM, you must set hello **primary** property of one of hello NICs too*true*, and hello rest too*false*.</span></span>

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a><span data-ttu-id="f3503-154">Déployer le modèle de hello ARM à l’aide de cliquez sur toodeploy</span><span class="sxs-lookup"><span data-stu-id="f3503-154">Deploy hello ARM template by using click toodeploy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f3503-155">Assurez-vous que vous suivez hello [préalables](#Pre-requisites) étapes avant de suivre les instructions hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-155">Make sure you follow hello [pre-requisites](#Pre-requisites) steps before following hello instructions below.</span></span>
> 

<span data-ttu-id="f3503-156">Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="f3503-156">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="f3503-157">toodeploy ce modèle à l’aide de cliquez toodeploy, suivez [ce lien](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello à droite de **groupe de ressources du serveur principal (consultez la documentation)** cliquez sur **déployer tooAzure**, remplacer Hello des valeurs de paramètre par défaut si nécessaire et suivez les instructions de hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f3503-157">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello right of **Backend resource group (see documentation)** click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

<span data-ttu-id="f3503-158">Hello figure ci-dessous contenu hello du nouveau groupe de ressources hello, après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f3503-158">hello figure below shows hello contents of hello new resource group, after deployment.</span></span>

![Groupe de ressources du back end](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="f3503-160">Déployer le modèle de hello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f3503-160">Deploy hello template by using PowerShell</span></span>
<span data-ttu-id="f3503-161">modèle de hello toodeploy vous avez téléchargé à l’aide de PowerShell, installer et configurer des PowerShell en effectuant les étapes hello Bonjour [installer et configurer PowerShell](/powershell/azure/overview) de l’article, puis terminez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3503-161">toodeploy hello template you downloaded by using PowerShell, install and configure PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article and then complete hello following steps:</span></span>

<span data-ttu-id="f3503-162">Exécutez hello  **`New-AzureRmResourceGroup`**  toocreate d’applet de commande un groupe de ressources à l’aide de hello modèle.</span><span class="sxs-lookup"><span data-stu-id="f3503-162">Run hello **`New-AzureRmResourceGroup`** cmdlet toocreate a resource group using hello template.</span></span>

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

<span data-ttu-id="f3503-163">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f3503-163">Expected output:</span></span>

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="f3503-164">Déployer le modèle de hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="f3503-164">Deploy hello template by using hello Azure CLI</span></span>
<span data-ttu-id="f3503-165">modèle de hello toodeploy à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-165">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="f3503-166">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f3503-166">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f3503-167">Exécutez hello  **`azure config mode`**  mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f3503-167">Run hello **`azure config mode`** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="f3503-168">Hello attendu sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="f3503-168">hello expected output follows:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="f3503-169">Ouvrez hello [fichier de paramètres](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), sélectionnez son contenu et enregistrez-le tooa fichier sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f3503-169">Open hello [parameter file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="f3503-170">Pour cet exemple, nous avons enregistré des fichiers de paramètres hello trop*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="f3503-170">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="f3503-171">Exécutez hello  **`azure group deployment create`**  applet de commande toodeploy hello nouveau réseau virtuel à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés.</span><span class="sxs-lookup"><span data-stu-id="f3503-171">Run hello **`azure group deployment create`** cmdlet toodeploy hello new VNet by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="f3503-172">liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.</span><span class="sxs-lookup"><span data-stu-id="f3503-172">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    <span data-ttu-id="f3503-173">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f3503-173">Expected output:</span></span>
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

