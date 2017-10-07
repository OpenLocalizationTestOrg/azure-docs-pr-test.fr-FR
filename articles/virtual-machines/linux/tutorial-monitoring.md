---
title: machines virtuelles Azure aaaMonitor Linux | Documents Microsoft
description: "Découvrez comment toomonitor démarrer les diagnostics et les mesures de performances sur un ordinateur virtuel de Linux dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>Comment toomonitor une machine virtuelle de Linux dans Azure

tooensure que vos machines virtuelles (VM) dans Azure s’exécutent correctement, vous pouvez consulter les métriques de performances et diagnostics de démarrage. Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Activer les diagnostics de démarrage sur hello machine virtuelle
> * Afficher les diagnostics de démarrage
> * Afficher les métriques de l’hôte
> * Activer l’extension diagnostics sur hello machine virtuelle
> * Afficher les métriques de la machine virtuelle
> * Créer des alertes en fonction des métriques des diagnostics
> * Configurer la surveillance avancée


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-vm"></a>Créer une machine virtuelle

toosee diagnostics et les mesures d’action, vous avez besoin d’une machine virtuelle. Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create). Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupMonitor* Bonjour *eastus* emplacement.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

Créez maintenant une machine virtuelle avec la commande [az vm create](https://docs.microsoft.com/cli/azure/vm#create). Hello exemple suivant crée un ordinateur virtuel nommé *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>Activer les diagnostics de démarrage

Comme les machines virtuelles Linux de démarrage, extension de Diagnostics de démarrage hello capture la sortie de démarrage et la stocke dans le stockage Azure. Ces données peuvent être des problèmes de démarrage de machine virtuelle tootroubleshoot utilisé. Diagnostics de démarrage ne sont pas automatiquement activés lorsque vous créez un VM Linux à l’aide de hello CLI d’Azure.

Avant d’activer les diagnostics de démarrage, un compte de stockage doit toobe créé pour stocker les journaux de démarrage. Les comptes de stockage doivent avoir un nom global unique, comprenant entre 3 et 24 caractères, et contenant seulement des chiffres et des lettres minuscules. Créer un compte de stockage avec hello [créer de compte de stockage az](/cli/azure/storage/account#create) commande. Dans cet exemple, une chaîne aléatoire est toocreate utilisé un nom de compte de stockage unique. 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

Lorsque vous activez les diagnostics de démarrage, le conteneur de stockage d’objets blob toohello hello URI est nécessaire. Hello requêtes suivantes de la commande hello tooreturn de compte de stockage cet URI. Hello, valeur de l’URI est stockée dans un nom de variable *bloburi*, qui est utilisé dans l’étape suivante de hello.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

Activez maintenant les diagnostics de démarrage avec la commande [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable). Hello `--storage` valeur est blob hello URI collecté à l’étape précédente de hello.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>Afficher les diagnostics de démarrage

Lorsque les diagnostics de démarrage sont activées, chaque fois que vous arrêtez et démarrez hello machine virtuelle, plus d’informations sur le processus de démarrage hello est écrit tooa du journal. Pour cet exemple, d’abord libérer hello VM par hello [az vm désallouer](/cli/azure/vm#deallocate) commande comme suit :

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

Commencer maintenant hello VM hello [début de machine virtuelle az]( /cli/azure/vm#stop) commande comme suit :

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

Vous pouvez obtenir des données de diagnostic de démarrage hello pour *myVM* avec hello [az vm diagnostics de démarrage get-démarrage-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) commande comme suit :

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>Afficher les métriques de l’hôte

Une machine virtuelle Linux a un hôte dédié dans Azure qui interagit avec elle. Métriques sont automatiquement collectées pour l’hôte de hello et peuvent être affichés dans hello portail Azure comme suit :

1. Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroupMonitor**, puis sélectionnez **myVM** dans la liste des ressources hello.
1. toosee l’exécution de la machine virtuelle d’hôte hello, cliquez sur **métriques** sur le panneau de la machine virtuelle hello, puis sélectionnez une des hello *[hôte]* métriques sous **métriques disponibles**.

    ![Afficher les métriques de l’hôte](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>Installer l’extension Diagnostics

> [!IMPORTANT]
> Ce document décrit la version 2.3 de hello Extension Diagnostics Linux, ce qui a été déconseillée. La version 2.3 sera prise en charge jusqu’au 30 juin 2018.
>
> La version 3.0 de hello Extension Diagnostics Linux peut être activée à la place. Pour plus d’informations, consultez [hello documentation](./diagnostic-extension.md).

métriques de base hôte Hello sont disponibles, mais toosee plus précis et des mesures spécifiques à la machine virtuelle, vous tooneed tooinstall hello extension Azure diagnostics sur hello machine virtuelle. Hello extension Azure diagnostics permet une analyse supplémentaire et diagnostics toobe de données récupérées à partir de la machine virtuelle de hello. Vous pouvez afficher ces métriques de performances et créer des alertes basées sur le fonctionnement de hello machine virtuelle. extension de diagnostic Hello est installée via hello portail Azure comme suit :

1. Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.
1. Cliquez sur **Paramètres de diagnostic**. liste de Hello montre que *diagnostics de démarrage* sont déjà activés à partir de la section précédente de hello. Cliquez sur la case à cocher pour hello *les audits de base*.
1. Bonjour *compte de stockage* section, parcourir les hello sélectionnez tooand *mydiagdata [1234]* compte créé dans la section précédente de hello.
1. Cliquez sur hello **enregistrer** bouton.

    ![Afficher les métriques de diagnostic](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>Afficher les métriques de la machine virtuelle

Vous pouvez afficher les métriques de machine virtuelle hello Bonjour même façon que vous avez affiché les métriques de machine virtuelle hôte hello :

1. Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.
1. toosee effectue hello machine virtuelle, cliquez sur **métriques** sur hello Panneau de machine virtuelle, puis sélectionnez une des métriques de diagnostic hello sous **métriques disponibles**.

    ![Afficher les métriques de la machine virtuelle](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>Créez des alertes

Vous pouvez créer des alertes en fonction de métriques de performances spécifiques. Les alertes peuvent être utilisé toonotify vous lors de l’utilisation moyenne du processeur dépasse un seuil ou une espace disque disponible devient inférieur à un certain montant, par exemple. Les alertes sont affichent dans hello portail Azure ou peuvent être envoyés par courrier électronique. Vous pouvez également déclencher des runbooks Azure Automation ou Azure Logic Apps dans tooalerts de réponse en cours de génération.

Hello exemple suivant crée une alerte pour l’utilisation moyenne du processeur.

1. Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.
2. Cliquez sur **règles d’alerte** sur le panneau de la machine virtuelle hello, puis cliquez sur **ajouter une alerte métrique** haut hello du panneau des alertes hello.
4. Spécifiez un **Nom** pour votre alerte, comme *myAlertRule*
5. tootrigger une alerte lorsque le pourcentage de l’UC dépasse 1.0 pendant cinq minutes, laissez hello toutes les autres valeurs par défaut sélectionnées.
6. Si vous le souhaitez, case hello pour *propriétaires, collaborateurs et les lecteurs de messagerie* toosend la notification par e-mail. action par défaut de Hello est toopresent une notification dans le portail de hello.
7. Cliquez sur hello **OK** bouton.


## <a name="advanced-monitoring"></a>Surveillance avancée 

Vous pouvez faire une surveillance plus avancée de votre machine virtuelle en utilisant [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Si vous ne l’avez pas déjà fait, vous pouvez vous inscrire pour une [version d’évaluation gratuite](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) d’Operations Management Suite.

Lorsque vous avez accès toohello OMS portail, vous pouvez trouver l’identificateur de clé et l’espace de travail du espace de travail hello sur le panneau des paramètres hello. Remplacez < espace de travail-key > et < id espace de travail > avec des valeurs hello pour à partir de votre OMS espace de travail et que vous pouvez utiliser **az vm extension ensemble** tooadd hello OMS extension toohello machine virtuelle :

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

Dans le panneau de recherche de journal hello du portail OMS de hello, vous devez voir *myVM* tels que ce qui est affiché dans hello illustration suivante :

![Panneau OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez configuré et examiné des machines virtuelles avec Azure Security Center. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Activer les diagnostics de démarrage sur hello machine virtuelle
> * Afficher les diagnostics de démarrage
> * Afficher les métriques de l’hôte
> * Activer l’extension diagnostics sur hello machine virtuelle
> * Afficher les métriques de la machine virtuelle
> * Créer des alertes en fonction des métriques des diagnostics
> * Configurer la surveillance avancée

Avance toohello toolearn de didacticiel suivant sur le centre de sécurité Azure.

> [!div class="nextstepaction"]
> [Gérer la sécurité des machines virtuelles](./tutorial-azure-security.md)