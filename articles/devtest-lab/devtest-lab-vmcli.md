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
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a>Créer et gérer des machines virtuelles avec DevTest Labs, à l’aide de hello CLI d’Azure
Ce guide de démarrage rapide vous assistera dans la création, le démarrage, la connexion, la mise à jour et le nettoyage d’un ordinateur de développement dans votre laboratoire. 

Avant de commencer :

* Si aucun laboratoire n’a été créé, la procédure à suivre se trouve [ici](devtest-lab-create-lab.md).

* [Installer CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). toostart, toocreate de connexion exécution az une connexion avec Azure. 

## <a name="create-and-verify-hello-virtual-machine"></a>Créer et vérifier l’ordinateur virtuel hello 
Créez une machine virtuelle à partir d’une image de la place du marché avec authentification SSH.
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> Placez hello **groupe de ressources de laboratoire** nom Bonjour--le paramètre de groupe de ressources.
>

Si vous souhaitez toocreate une machine virtuelle à l’aide d’une formule, utilisez hello--paramètre formule dans [créer des ordinateurs virtuels de lab az](https://docs.microsoft.com/cli/azure/lab/vm#create).


Vérifiez que hello machine virtuelle est disponible.
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

## <a name="start-and-connect-toohello-virtual-machine"></a>Démarrer et connecter l’ordinateur virtuel de toohello
Démarrez une machine virtuelle.
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> Placez hello **groupe de ressources de laboratoire** nom Bonjour--le paramètre de groupe de ressources.
>

Se connecter tooa machine virtuelle : [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) ou [Bureau à distance](../virtual-machines/windows/connect-logon.md).
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a>Mettre à jour de la machine virtuelle de hello
Appliquer les artefacts tooa machine virtuelle.
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

Liste des artefacts disponibles dans le laboratoire de hello.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a>Arrêter et supprimer un ordinateur virtuel de hello    
Arrêtez une machine virtuelle.
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

Supprimez une machine virtuelle.
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]