---
title: "aaaCreate et gérer des ordinateurs virtuels dans DevTest Labs avec CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toouse Azure DevTest Labs toocreate et gérer des machines virtuelles avec Azure CLI 2.0"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a><span data-ttu-id="a458a-103">Créer et gérer des machines virtuelles avec DevTest Labs, à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="a458a-103">Create and manage virtual machines with DevTest Labs using hello Azure CLI</span></span>
<span data-ttu-id="a458a-104">Ce guide de démarrage rapide vous assistera dans la création, le démarrage, la connexion, la mise à jour et le nettoyage d’un ordinateur de développement dans votre laboratoire.</span><span class="sxs-lookup"><span data-stu-id="a458a-104">This quick start will guide you through creating, starting, connecting, updating and cleaning up a development machine in your lab.</span></span> 

<span data-ttu-id="a458a-105">Avant de commencer :</span><span class="sxs-lookup"><span data-stu-id="a458a-105">Before you begin:</span></span>

* <span data-ttu-id="a458a-106">Si aucun laboratoire n’a été créé, la procédure à suivre se trouve [ici](devtest-lab-create-lab.md).</span><span class="sxs-lookup"><span data-stu-id="a458a-106">If a lab has not been created, instructions can be found [here](devtest-lab-create-lab.md).</span></span>

* <span data-ttu-id="a458a-107">[Installer CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a458a-107">[Install CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="a458a-108">toostart, toocreate de connexion exécution az une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="a458a-108">toostart, run az login toocreate a connection with Azure.</span></span> 

## <a name="create-and-verify-hello-virtual-machine"></a><span data-ttu-id="a458a-109">Créer et vérifier l’ordinateur virtuel hello</span><span class="sxs-lookup"><span data-stu-id="a458a-109">Create and verify hello virtual machine</span></span> 
<span data-ttu-id="a458a-110">Créez une machine virtuelle à partir d’une image de la place du marché avec authentification SSH.</span><span class="sxs-lookup"><span data-stu-id="a458a-110">Create a VM from a marketplace image with ssh authentication.</span></span>
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> <span data-ttu-id="a458a-111">Placez hello **groupe de ressources de laboratoire** nom Bonjour--le paramètre de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a458a-111">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="a458a-112">Si vous souhaitez toocreate une machine virtuelle à l’aide d’une formule, utilisez hello--paramètre formule dans [créer des ordinateurs virtuels de lab az](https://docs.microsoft.com/cli/azure/lab/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a458a-112">If you want toocreate a VM using a formula, use hello --formula parameter in [az lab vm create](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>


<span data-ttu-id="a458a-113">Vérifiez que hello machine virtuelle est disponible.</span><span class="sxs-lookup"><span data-stu-id="a458a-113">Verify that hello VM is available.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-toohello-virtual-machine"></a><span data-ttu-id="a458a-114">Démarrer et connecter l’ordinateur virtuel de toohello</span><span class="sxs-lookup"><span data-stu-id="a458a-114">Start and connect toohello virtual machine</span></span>
<span data-ttu-id="a458a-115">Démarrez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a458a-115">Start a VM.</span></span>
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> <span data-ttu-id="a458a-116">Placez hello **groupe de ressources de laboratoire** nom Bonjour--le paramètre de groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="a458a-116">Put hello **lab's resource group** name in hello --resource-group parameter.</span></span>
>

<span data-ttu-id="a458a-117">Se connecter tooa machine virtuelle : [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) ou [Bureau à distance](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="a458a-117">Connect tooa VM: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) or [Remote Desktop](../virtual-machines/windows/connect-logon.md).</span></span>
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a><span data-ttu-id="a458a-118">Mettre à jour de la machine virtuelle de hello</span><span class="sxs-lookup"><span data-stu-id="a458a-118">Update hello virtual machine</span></span>
<span data-ttu-id="a458a-119">Appliquer les artefacts tooa machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a458a-119">Apply artifacts tooa VM.</span></span>
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

<span data-ttu-id="a458a-120">Liste des artefacts disponibles dans le laboratoire de hello.</span><span class="sxs-lookup"><span data-stu-id="a458a-120">List artifacts available in hello lab.</span></span>
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a><span data-ttu-id="a458a-121">Arrêter et supprimer un ordinateur virtuel de hello</span><span class="sxs-lookup"><span data-stu-id="a458a-121">Stop and delete hello virtual machine</span></span>    
<span data-ttu-id="a458a-122">Arrêtez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a458a-122">Stop a VM.</span></span>
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

<span data-ttu-id="a458a-123">Supprimez une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a458a-123">Delete a VM.</span></span>
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]