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
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="6b725-103">Comment toomonitor une machine virtuelle de Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="6b725-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="6b725-104">tooensure que vos machines virtuelles (VM) dans Azure s’exécutent correctement, vous pouvez consulter les métriques de performances et diagnostics de démarrage.</span><span class="sxs-lookup"><span data-stu-id="6b725-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="6b725-105">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b725-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b725-106">Activer les diagnostics de démarrage sur hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6b725-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="6b725-107">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="6b725-107">View boot diagnostics</span></span>
> * <span data-ttu-id="6b725-108">Afficher les métriques de l’hôte</span><span class="sxs-lookup"><span data-stu-id="6b725-108">View host metrics</span></span>
> * <span data-ttu-id="6b725-109">Activer l’extension diagnostics sur hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6b725-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="6b725-110">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6b725-110">View VM metrics</span></span>
> * <span data-ttu-id="6b725-111">Créer des alertes en fonction des métriques des diagnostics</span><span class="sxs-lookup"><span data-stu-id="6b725-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="6b725-112">Configurer la surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="6b725-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6b725-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6b725-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6b725-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="6b725-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6b725-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b725-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="6b725-116">Créer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6b725-116">Create VM</span></span>

<span data-ttu-id="6b725-117">toosee diagnostics et les mesures d’action, vous avez besoin d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6b725-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="6b725-118">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="6b725-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="6b725-119">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroupMonitor* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="6b725-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="6b725-120">Créez maintenant une machine virtuelle avec la commande [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="6b725-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="6b725-121">Hello exemple suivant crée un ordinateur virtuel nommé *myVM*:</span><span class="sxs-lookup"><span data-stu-id="6b725-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="6b725-122">Activer les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="6b725-122">Enable boot diagnostics</span></span>

<span data-ttu-id="6b725-123">Comme les machines virtuelles Linux de démarrage, extension de Diagnostics de démarrage hello capture la sortie de démarrage et la stocke dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="6b725-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="6b725-124">Ces données peuvent être des problèmes de démarrage de machine virtuelle tootroubleshoot utilisé.</span><span class="sxs-lookup"><span data-stu-id="6b725-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="6b725-125">Diagnostics de démarrage ne sont pas automatiquement activés lorsque vous créez un VM Linux à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="6b725-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="6b725-126">Avant d’activer les diagnostics de démarrage, un compte de stockage doit toobe créé pour stocker les journaux de démarrage.</span><span class="sxs-lookup"><span data-stu-id="6b725-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="6b725-127">Les comptes de stockage doivent avoir un nom global unique, comprenant entre 3 et 24 caractères, et contenant seulement des chiffres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="6b725-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="6b725-128">Créer un compte de stockage avec hello [créer de compte de stockage az](/cli/azure/storage/account#create) commande.</span><span class="sxs-lookup"><span data-stu-id="6b725-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="6b725-129">Dans cet exemple, une chaîne aléatoire est toocreate utilisé un nom de compte de stockage unique.</span><span class="sxs-lookup"><span data-stu-id="6b725-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="6b725-130">Lorsque vous activez les diagnostics de démarrage, le conteneur de stockage d’objets blob toohello hello URI est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6b725-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="6b725-131">Hello requêtes suivantes de la commande hello tooreturn de compte de stockage cet URI.</span><span class="sxs-lookup"><span data-stu-id="6b725-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="6b725-132">Hello, valeur de l’URI est stockée dans un nom de variable *bloburi*, qui est utilisé dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="6b725-133">Activez maintenant les diagnostics de démarrage avec la commande [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="6b725-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="6b725-134">Hello `--storage` valeur est blob hello URI collecté à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="6b725-135">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="6b725-135">View boot diagnostics</span></span>

<span data-ttu-id="6b725-136">Lorsque les diagnostics de démarrage sont activées, chaque fois que vous arrêtez et démarrez hello machine virtuelle, plus d’informations sur le processus de démarrage hello est écrit tooa du journal.</span><span class="sxs-lookup"><span data-stu-id="6b725-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="6b725-137">Pour cet exemple, d’abord libérer hello VM par hello [az vm désallouer](/cli/azure/vm#deallocate) commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b725-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="6b725-138">Commencer maintenant hello VM hello [début de machine virtuelle az]( /cli/azure/vm#stop) commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b725-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="6b725-139">Vous pouvez obtenir des données de diagnostic de démarrage hello pour *myVM* avec hello [az vm diagnostics de démarrage get-démarrage-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) commande comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b725-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="6b725-140">Afficher les métriques de l’hôte</span><span class="sxs-lookup"><span data-stu-id="6b725-140">View host metrics</span></span>

<span data-ttu-id="6b725-141">Une machine virtuelle Linux a un hôte dédié dans Azure qui interagit avec elle.</span><span class="sxs-lookup"><span data-stu-id="6b725-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="6b725-142">Métriques sont automatiquement collectées pour l’hôte de hello et peuvent être affichés dans hello portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b725-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="6b725-143">Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroupMonitor**, puis sélectionnez **myVM** dans la liste des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="6b725-144">toosee l’exécution de la machine virtuelle d’hôte hello, cliquez sur **métriques** sur le panneau de la machine virtuelle hello, puis sélectionnez une des hello *[hôte]* métriques sous **métriques disponibles**.</span><span class="sxs-lookup"><span data-stu-id="6b725-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![Afficher les métriques de l’hôte](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="6b725-146">Installer l’extension Diagnostics</span><span class="sxs-lookup"><span data-stu-id="6b725-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6b725-147">Ce document décrit la version 2.3 de hello Extension Diagnostics Linux, ce qui a été déconseillée.</span><span class="sxs-lookup"><span data-stu-id="6b725-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="6b725-148">La version 2.3 sera prise en charge jusqu’au 30 juin 2018.</span><span class="sxs-lookup"><span data-stu-id="6b725-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="6b725-149">La version 3.0 de hello Extension Diagnostics Linux peut être activée à la place.</span><span class="sxs-lookup"><span data-stu-id="6b725-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="6b725-150">Pour plus d’informations, consultez [hello documentation](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="6b725-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="6b725-151">métriques de base hôte Hello sont disponibles, mais toosee plus précis et des mesures spécifiques à la machine virtuelle, vous tooneed tooinstall hello extension Azure diagnostics sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6b725-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="6b725-152">Hello extension Azure diagnostics permet une analyse supplémentaire et diagnostics toobe de données récupérées à partir de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="6b725-153">Vous pouvez afficher ces métriques de performances et créer des alertes basées sur le fonctionnement de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6b725-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="6b725-154">extension de diagnostic Hello est installée via hello portail Azure comme suit :</span><span class="sxs-lookup"><span data-stu-id="6b725-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="6b725-155">Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="6b725-156">Cliquez sur **Paramètres de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="6b725-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="6b725-157">liste de Hello montre que *diagnostics de démarrage* sont déjà activés à partir de la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="6b725-158">Cliquez sur la case à cocher pour hello *les audits de base*.</span><span class="sxs-lookup"><span data-stu-id="6b725-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="6b725-159">Bonjour *compte de stockage* section, parcourir les hello sélectionnez tooand *mydiagdata [1234]* compte créé dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="6b725-160">Cliquez sur hello **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="6b725-160">Click hello **Save** button.</span></span>

    ![Afficher les métriques de diagnostic](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="6b725-162">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6b725-162">View VM metrics</span></span>

<span data-ttu-id="6b725-163">Vous pouvez afficher les métriques de machine virtuelle hello Bonjour même façon que vous avez affiché les métriques de machine virtuelle hôte hello :</span><span class="sxs-lookup"><span data-stu-id="6b725-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="6b725-164">Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="6b725-165">toosee effectue hello machine virtuelle, cliquez sur **métriques** sur hello Panneau de machine virtuelle, puis sélectionnez une des métriques de diagnostic hello sous **métriques disponibles**.</span><span class="sxs-lookup"><span data-stu-id="6b725-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![Afficher les métriques de la machine virtuelle](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="6b725-167">Créez des alertes</span><span class="sxs-lookup"><span data-stu-id="6b725-167">Create alerts</span></span>

<span data-ttu-id="6b725-168">Vous pouvez créer des alertes en fonction de métriques de performances spécifiques.</span><span class="sxs-lookup"><span data-stu-id="6b725-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="6b725-169">Les alertes peuvent être utilisé toonotify vous lors de l’utilisation moyenne du processeur dépasse un seuil ou une espace disque disponible devient inférieur à un certain montant, par exemple.</span><span class="sxs-lookup"><span data-stu-id="6b725-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="6b725-170">Les alertes sont affichent dans hello portail Azure ou peuvent être envoyés par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="6b725-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="6b725-171">Vous pouvez également déclencher des runbooks Azure Automation ou Azure Logic Apps dans tooalerts de réponse en cours de génération.</span><span class="sxs-lookup"><span data-stu-id="6b725-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="6b725-172">Hello exemple suivant crée une alerte pour l’utilisation moyenne du processeur.</span><span class="sxs-lookup"><span data-stu-id="6b725-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="6b725-173">Bonjour portail Azure, cliquez sur **groupes de ressources**, sélectionnez **myResourceGroup**, puis sélectionnez **myVM** dans la liste des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="6b725-174">Cliquez sur **règles d’alerte** sur le panneau de la machine virtuelle hello, puis cliquez sur **ajouter une alerte métrique** haut hello du panneau des alertes hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="6b725-175">Spécifiez un **Nom** pour votre alerte, comme *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="6b725-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="6b725-176">tootrigger une alerte lorsque le pourcentage de l’UC dépasse 1.0 pendant cinq minutes, laissez hello toutes les autres valeurs par défaut sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="6b725-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="6b725-177">Si vous le souhaitez, case hello pour *propriétaires, collaborateurs et les lecteurs de messagerie* toosend la notification par e-mail.</span><span class="sxs-lookup"><span data-stu-id="6b725-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="6b725-178">action par défaut de Hello est toopresent une notification dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="6b725-179">Cliquez sur hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="6b725-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="6b725-180">Surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="6b725-180">Advanced monitoring</span></span> 

<span data-ttu-id="6b725-181">Vous pouvez faire une surveillance plus avancée de votre machine virtuelle en utilisant [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="6b725-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="6b725-182">Si vous ne l’avez pas déjà fait, vous pouvez vous inscrire pour une [version d’évaluation gratuite](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) d’Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="6b725-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="6b725-183">Lorsque vous avez accès toohello OMS portail, vous pouvez trouver l’identificateur de clé et l’espace de travail du espace de travail hello sur le panneau des paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="6b725-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="6b725-184">Remplacez < espace de travail-key > et < id espace de travail > avec des valeurs hello pour à partir de votre OMS espace de travail et que vous pouvez utiliser **az vm extension ensemble** tooadd hello OMS extension toohello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="6b725-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

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

<span data-ttu-id="6b725-185">Dans le panneau de recherche de journal hello du portail OMS de hello, vous devez voir *myVM* tels que ce qui est affiché dans hello illustration suivante :</span><span class="sxs-lookup"><span data-stu-id="6b725-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![Panneau OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="6b725-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b725-187">Next steps</span></span>

<span data-ttu-id="6b725-188">Dans ce didacticiel, vous avez configuré et examiné des machines virtuelles avec Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="6b725-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="6b725-189">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6b725-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6b725-190">Activer les diagnostics de démarrage sur hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6b725-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="6b725-191">Afficher les diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="6b725-191">View boot diagnostics</span></span>
> * <span data-ttu-id="6b725-192">Afficher les métriques de l’hôte</span><span class="sxs-lookup"><span data-stu-id="6b725-192">View host metrics</span></span>
> * <span data-ttu-id="6b725-193">Activer l’extension diagnostics sur hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6b725-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="6b725-194">Afficher les métriques de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6b725-194">View VM metrics</span></span>
> * <span data-ttu-id="6b725-195">Créer des alertes en fonction des métriques des diagnostics</span><span class="sxs-lookup"><span data-stu-id="6b725-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="6b725-196">Configurer la surveillance avancée</span><span class="sxs-lookup"><span data-stu-id="6b725-196">Set up advanced monitoring</span></span>

<span data-ttu-id="6b725-197">Avance toohello toolearn de didacticiel suivant sur le centre de sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="6b725-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6b725-198">Gérer la sécurité des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="6b725-198">Manage VM security</span></span>](./tutorial-azure-security.md)