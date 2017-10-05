---
title: Surveiller des machines virtuelles Linux dans Azure | Microsoft Docs
description: "Découvrez comment surveiller les diagnostics de démarrage et les métriques de performances sur une machine virtuelle Linux dans Azure"
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
ms.openlocfilehash: 3fe8390e88e609b57a462e066f972346f8e8730e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-monitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="c274e-103">Guide pratique pour surveiller une machine virtuelle Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="c274e-103">How to monitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="c274e-104">Pour vérifier que vos machines virtuelles dans Azure fonctionnent correctement, vous pouvez consulter les diagnostics de démarrage et les métriques de performances.</span><span class="sxs-lookup"><span data-stu-id="c274e-104">To ensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="c274e-105">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c274e-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c274e-106">Activer les diagnostics de démarrage sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c274e-106">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="c274e-107">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="c274e-107">View boot diagnostics</span></span>
> * <span data-ttu-id="c274e-108">Afficher les métriques de l’hôte</span><span class="sxs-lookup"><span data-stu-id="c274e-108">View host metrics</span></span>
> * <span data-ttu-id="c274e-109">Activer l’extension Diagnostics sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c274e-109">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="c274e-110">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c274e-110">View VM metrics</span></span>
> * <span data-ttu-id="c274e-111">Créer des alertes en fonction des métriques des diagnostics</span><span class="sxs-lookup"><span data-stu-id="c274e-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="c274e-112">Configurer la surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="c274e-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c274e-113">Si vous choisissez d’installer et d’utiliser l’interface CLI localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c274e-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c274e-114">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="c274e-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="c274e-115">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c274e-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="c274e-116">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c274e-116">Create VM</span></span>

<span data-ttu-id="c274e-117">Pour voir les diagnostics et les métriques en action, vous avez besoin d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c274e-117">To see diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="c274e-118">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c274e-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c274e-119">L’exemple suivant crée un groupe de ressources nommé *myResourceGroupMonitor* à l’emplacement *eastus*.</span><span class="sxs-lookup"><span data-stu-id="c274e-119">The following example creates a resource group named *myResourceGroupMonitor* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="c274e-120">Créez maintenant une machine virtuelle avec la commande [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="c274e-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="c274e-121">L’exemple suivant crée une machine virtuelle nommée *myVM* :</span><span class="sxs-lookup"><span data-stu-id="c274e-121">The following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="c274e-122">Activer les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="c274e-122">Enable boot diagnostics</span></span>

<span data-ttu-id="c274e-123">Au démarrage des machines virtuelles Linux, l’extension Diagnostics de démarrage capture la sortie du démarrage et la stocke dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="c274e-123">As Linux VMs boot, the boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="c274e-124">Ces données peuvent être utilisées pour résoudre les problèmes de démarrage des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="c274e-124">This data can be used to troubleshoot VM boot issues.</span></span> <span data-ttu-id="c274e-125">Les diagnostics de démarrage ne sont pas activés automatiquement quand vous créez une machine virtuelle Linux à l’aide d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c274e-125">Boot diagnostics are not automatically enabled when you create a Linux VM using the Azure CLI.</span></span>

<span data-ttu-id="c274e-126">Avant d’activer les diagnostics de démarrage, vous devez créer un compte de stockage pour stocker les journaux de démarrage.</span><span class="sxs-lookup"><span data-stu-id="c274e-126">Before enabling boot diagnostics, a storage account needs to be created for storing boot logs.</span></span> <span data-ttu-id="c274e-127">Les comptes de stockage doivent avoir un nom global unique, comprenant entre 3 et 24 caractères, et contenant seulement des chiffres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="c274e-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="c274e-128">Créez un compte de stockage avec la commande [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="c274e-128">Create a storage account with the [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="c274e-129">Dans cet exemple, une chaîne aléatoire est utilisée pour créer un nom de compte de stockage unique.</span><span class="sxs-lookup"><span data-stu-id="c274e-129">In this example, a random string is used to create a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="c274e-130">Lors de l’activation des diagnostics de démarrage, l’URI vers le conteneur de stockage d’objets blob est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="c274e-130">When enabling boot diagnostics, the URI to the blob storage container is needed.</span></span> <span data-ttu-id="c274e-131">La commande suivante interroge le compte de stockage et retourne cet URI.</span><span class="sxs-lookup"><span data-stu-id="c274e-131">The following command queries the storage account to return this URI.</span></span> <span data-ttu-id="c274e-132">La valeur de l’URI est stockée dans une variable nommée *bloburi*, qui est utilisé à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="c274e-132">The URI value is stored in a variable names *bloburi*, which is used in the next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="c274e-133">Activez maintenant les diagnostics de démarrage avec la commande [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="c274e-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="c274e-134">La valeur de `--storage` est l’URI de l’objet blob collecté à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="c274e-134">The `--storage` value is the blob URI collected in the previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="c274e-135">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="c274e-135">View boot diagnostics</span></span>

<span data-ttu-id="c274e-136">Quand les diagnostics de démarrage sont activés, chaque fois que vous arrêtez et que vous démarrez la machine virtuelle, des informations sur le processus de démarrage sont écrites dans un fichier journal.</span><span class="sxs-lookup"><span data-stu-id="c274e-136">When boot diagnostics are enabled, each time you stop and start the VM, information about the boot process is written to a log file.</span></span> <span data-ttu-id="c274e-137">Pour cet exemple, désallouez d’abord la machine virtuelle avec la commande [az vm deallocate](/cli/azure/vm#deallocate) comme suit :</span><span class="sxs-lookup"><span data-stu-id="c274e-137">For this example, first deallocate the VM with the [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="c274e-138">Démarrez maintenant la machine virtuelle avec la commande [az vm start]( /cli/azure/vm#stop) comme suit :</span><span class="sxs-lookup"><span data-stu-id="c274e-138">Now start the VM with the [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="c274e-139">Vous pouvez obtenir les données des diagnostics de démarrage pour *myVM* avec la commande [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) comme suit :</span><span class="sxs-lookup"><span data-stu-id="c274e-139">You can get the boot diagnostic data for *myVM* with the [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="c274e-140">Afficher les métriques de l’hôte</span><span class="sxs-lookup"><span data-stu-id="c274e-140">View host metrics</span></span>

<span data-ttu-id="c274e-141">Une machine virtuelle Linux a un hôte dédié dans Azure qui interagit avec elle.</span><span class="sxs-lookup"><span data-stu-id="c274e-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="c274e-142">Les métriques sont automatiquement collectées pour l’hôte et peuvent être visualisées dans le portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="c274e-142">Metrics are automatically collected for the host and can be viewed in the Azure portal as follows:</span></span>

1. <span data-ttu-id="c274e-143">Dans le portail Azure, cliquez sur **Groupes de ressources**, sélectionnez **myResourceGroupMonitor** puis sélectionnez **myVM** dans la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="c274e-143">In the Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="c274e-144">Pour voir comment la machine virtuelle hôte fonctionne, cliquez sur **Métriques** dans le panneau de la machine virtuelle, puis sélectionnez une des métriques de *[hôte]* sous **Métriques disponibles**.</span><span class="sxs-lookup"><span data-stu-id="c274e-144">To see how the host VM is performing, click **Metrics** on the VM blade, then select any of the *[Host]* metrics under **Available metrics**.</span></span>

    ![Afficher les métriques de l’hôte](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="c274e-146">Installer l’extension Diagnostics</span><span class="sxs-lookup"><span data-stu-id="c274e-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c274e-147">Ce document décrit la version 2.3 de l’extension de diagnostic Linux, qui est déconseillée.</span><span class="sxs-lookup"><span data-stu-id="c274e-147">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="c274e-148">La version 2.3 sera prise en charge jusqu’au 30 juin 2018.</span><span class="sxs-lookup"><span data-stu-id="c274e-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="c274e-149">La version 3.0 de l’extension de diagnostic Linux peut être activée à la place.</span><span class="sxs-lookup"><span data-stu-id="c274e-149">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="c274e-150">Pour plus d’informations, consultez [la documentation](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="c274e-150">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="c274e-151">Les métriques de base de l’hôte sont disponibles, mais pour voir des métriques plus précises et spécifiques à la machine virtuelle, vous devez installer l’extension Diagnostics Azure sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c274e-151">The basic host metrics are available, but to see more granular and VM-specific metrics, you to need to install the Azure diagnostics extension on the VM.</span></span> <span data-ttu-id="c274e-152">L’extension Diagnostics Azure permet de récupérer des données supplémentaires de surveillance et de diagnostic auprès de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c274e-152">The Azure diagnostics extension allows additional monitoring and diagnostics data to be retrieved from the VM.</span></span> <span data-ttu-id="c274e-153">Vous pouvez voir ces métriques de performances et créer des alertes basées sur le fonctionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c274e-153">You can view these performance metrics and create alerts based on how the VM performs.</span></span> <span data-ttu-id="c274e-154">L’extension Diagnostics est installée via le portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="c274e-154">The diagnostic extension is installed through the Azure portal as follows:</span></span>

1. <span data-ttu-id="c274e-155">Dans le portail Azure, cliquez sur **Groupes de ressources**, sélectionnez **myResourceGroup** puis sélectionnez **myVM** dans la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="c274e-155">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="c274e-156">Cliquez sur **Paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="c274e-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="c274e-157">La liste montre que les *Diagnostics de démarrage* sont déjà activés depuis la section précédente.</span><span class="sxs-lookup"><span data-stu-id="c274e-157">The list shows that *Boot diagnostics* are already enabled from the previous section.</span></span> <span data-ttu-id="c274e-158">Cliquez sur la case à cocher *Métriques de base*.</span><span class="sxs-lookup"><span data-stu-id="c274e-158">Click the check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="c274e-159">Dans la section *Compte de stockage*, recherchez et sélectionnez le compte *mydiagdata[1234]* créé dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="c274e-159">In the *Storage account* section, browse to and select the *mydiagdata[1234]* account created in the previous section.</span></span>
1. <span data-ttu-id="c274e-160">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="c274e-160">Click the **Save** button.</span></span>

    ![Afficher les métriques de diagnostic](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="c274e-162">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c274e-162">View VM metrics</span></span>

<span data-ttu-id="c274e-163">Vous pouvez afficher les métriques de la machine virtuelle de la même façon que vous avez affiché le mesures de la machine virtuelle hôte :</span><span class="sxs-lookup"><span data-stu-id="c274e-163">You can view the VM metrics in the same way that you viewed the host VM metrics:</span></span>

1. <span data-ttu-id="c274e-164">Dans le portail Azure, cliquez sur **Groupes de ressources**, sélectionnez **myResourceGroup** puis sélectionnez **myVM** dans la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="c274e-164">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
1. <span data-ttu-id="c274e-165">Pour voir comment la machine virtuelle fonctionne, cliquez sur **Métriques** dans le panneau de la machine virtuelle puis sélectionnez une des métriques de diagnostic sous **Métriques disponibles**.</span><span class="sxs-lookup"><span data-stu-id="c274e-165">To see how the VM is performing, click **Metrics** on the VM blade, and then select any of the diagnostics metrics under **Available metrics**.</span></span>

    ![Afficher les métriques de la machine virtuelle](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="c274e-167">Créez des alertes</span><span class="sxs-lookup"><span data-stu-id="c274e-167">Create alerts</span></span>

<span data-ttu-id="c274e-168">Vous pouvez créer des alertes en fonction de métriques de performances spécifiques.</span><span class="sxs-lookup"><span data-stu-id="c274e-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="c274e-169">Les alertes peuvent être utilisées par exemple pour notifier que l’utilisation moyenne de l’UC dépasse un certain seuil ou que l’espace disque disponible est inférieur à une certaine quantité.</span><span class="sxs-lookup"><span data-stu-id="c274e-169">Alerts can be used to notify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="c274e-170">Les alertes sont affichées dans le portail Azure ou peuvent être envoyées par e-mail.</span><span class="sxs-lookup"><span data-stu-id="c274e-170">Alerts are displayed in the Azure portal or can be sent via email.</span></span> <span data-ttu-id="c274e-171">Vous pouvez également déclencher des runbooks Azure Automation ou Azure Logic Apps en réponse aux alertes générées.</span><span class="sxs-lookup"><span data-stu-id="c274e-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response to alerts being generated.</span></span>

<span data-ttu-id="c274e-172">L’exemple suivant crée une alerte pour l’utilisation moyenne de l’UC.</span><span class="sxs-lookup"><span data-stu-id="c274e-172">The following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="c274e-173">Dans le portail Azure, cliquez sur **Groupes de ressources**, sélectionnez **myResourceGroup** puis sélectionnez **myVM** dans la liste des ressources.</span><span class="sxs-lookup"><span data-stu-id="c274e-173">In the Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in the resource list.</span></span>
2. <span data-ttu-id="c274e-174">Cliquez sur **Règles d’alerte** dans le panneau de la machine virtuelle puis cliquez sur **Ajouter une alerte Métrique** dans la partie supérieure du panneau des alertes.</span><span class="sxs-lookup"><span data-stu-id="c274e-174">Click **Alert rules** on the VM blade, then click **Add metric alert** across the top of the alerts blade.</span></span>
4. <span data-ttu-id="c274e-175">Spécifiez un **Nom** pour votre alerte, comme *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="c274e-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="c274e-176">Pour déclencher une alerte quand le pourcentage d’UC dépasse 1,0 pendant cinq minutes, laissez toutes les autres valeurs par défaut sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="c274e-176">To trigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all the other defaults selected.</span></span>
6. <span data-ttu-id="c274e-177">Si vous le souhaitez, cochez la case *Envoyer un e-mail aux propriétaires, aux contributeurs et aux lecteurs* pour envoyer la notification par e-mail.</span><span class="sxs-lookup"><span data-stu-id="c274e-177">Optionally, check the box for *Email owners, contributors, and readers* to send email notification.</span></span> <span data-ttu-id="c274e-178">L’action par défaut est de présenter une notification dans le portail.</span><span class="sxs-lookup"><span data-stu-id="c274e-178">The default action is to present a notification in the portal.</span></span>
7. <span data-ttu-id="c274e-179">Cliquez sur le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="c274e-179">Click the **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="c274e-180">Surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="c274e-180">Advanced monitoring</span></span> 

<span data-ttu-id="c274e-181">Vous pouvez faire une surveillance plus avancée de votre machine virtuelle en utilisant [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="c274e-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="c274e-182">Si vous ne l’avez pas déjà fait, vous pouvez vous inscrire pour une [version d’évaluation gratuite](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) d’Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="c274e-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="c274e-183">Quand vous avez accès au portail OMS, vous pouvez trouver la clé de l’espace de travail et l’identificateur de l’espace de travail dans le panneau Paramètres.</span><span class="sxs-lookup"><span data-stu-id="c274e-183">When you have access to the OMS portal, you can find the workspace key and workspace identifier on the Settings blade.</span></span> <span data-ttu-id="c274e-184">Remplacez <workspace-key> et <workspace-id> par les valeurs correspondant à votre espace de travail OMS et utilisez ensuite **az vm extension set** pour ajouter l’extension OMS à la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="c274e-184">Replace <workspace-key> and <workspace-id> with the values for from your OMS workspace and then you can use **az vm extension set** to add the OMS extension to the VM:</span></span>

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

<span data-ttu-id="c274e-185">Dans le panneau Recherche dans les journaux du portail OMS, vous devez normalement voir *myVM*, comme illustré dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="c274e-185">On the Log Search blade of the OMS portal, you should see *myVM* such as what is shown in the following picture:</span></span>

![Panneau OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="c274e-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c274e-187">Next steps</span></span>

<span data-ttu-id="c274e-188">Dans ce didacticiel, vous avez configuré et examiné des machines virtuelles avec Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="c274e-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="c274e-189">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c274e-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c274e-190">Activer les diagnostics de démarrage sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c274e-190">Enable boot diagnostics on the VM</span></span>
> * <span data-ttu-id="c274e-191">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="c274e-191">View boot diagnostics</span></span>
> * <span data-ttu-id="c274e-192">Afficher les métriques de l’hôte</span><span class="sxs-lookup"><span data-stu-id="c274e-192">View host metrics</span></span>
> * <span data-ttu-id="c274e-193">Activer l’extension Diagnostics sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c274e-193">Enable diagnostics extension on the VM</span></span>
> * <span data-ttu-id="c274e-194">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c274e-194">View VM metrics</span></span>
> * <span data-ttu-id="c274e-195">Créer des alertes en fonction des métriques des diagnostics</span><span class="sxs-lookup"><span data-stu-id="c274e-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="c274e-196">Configurer la surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="c274e-196">Set up advanced monitoring</span></span>

<span data-ttu-id="c274e-197">Passez au didacticiel suivant pour découvrir plus d’informations sur Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="c274e-197">Advance to the next tutorial to learn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c274e-198">Gérer la sécurité des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="c274e-198">Manage VM security</span></span>](./tutorial-azure-security.md)