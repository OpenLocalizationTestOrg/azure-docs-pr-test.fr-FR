---
title: "aaaDeploy 3 nœuds Deis cluster | Documents Microsoft"
description: "Cet article décrit comment toocreate Deis 3 nœuds clusters sur Azure à l’aide d’un modèle Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="6849b-103">Déployer et configurer un cluster Deis à 3 nœuds dans Azure</span><span class="sxs-lookup"><span data-stu-id="6849b-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="6849b-104">Cet article vous détaille l’approvisionnement d’un cluster [Deis](http://deis.io/) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6849b-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="6849b-105">Elle couvre toutes les étapes de hello de création toodeploying des certificats nécessaires hello et un exemple de mise à l’échelle **accédez** application sur le cluster qui vient d’être mis en service de hello.</span><span class="sxs-lookup"><span data-stu-id="6849b-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="6849b-106">Hello diagramme suivant illustre architecture hello du système de hello déployé.</span><span class="sxs-lookup"><span data-stu-id="6849b-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="6849b-107">Un administrateur système gère à l’aide du cluster hello Deis des outils tels que **deis** et **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="6849b-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="6849b-108">Les connexions sont établies via un équilibrage de charge Azure, qui transfère les nœuds de cluster de hello tooone de connexions hello du membre de hello.</span><span class="sxs-lookup"><span data-stu-id="6849b-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="6849b-109">accès des clients Hello des applications via l’équilibrage de charge hello également déployées.</span><span class="sxs-lookup"><span data-stu-id="6849b-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="6849b-110">Dans ce cas, équilibrage de charge hello transfère hello trafic tooa Deis maillage du routeur, qui achemine davantage de conteneurs Docker de trafic toocorresponding hébergés sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="6849b-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![Diagramme d’architecture du cluster Deis déployé](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="6849b-112">Dans toorun ordre via hello comme suit, vous devez :</span><span class="sxs-lookup"><span data-stu-id="6849b-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="6849b-113">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6849b-113">An active Azure subscription.</span></span> <span data-ttu-id="6849b-114">Si vous n’en avez pas, vous pouvez obtenir une version d’essai sur [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6849b-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="6849b-115">Un travail ou des groupes de ressources Azure scolaire id toouse.</span><span class="sxs-lookup"><span data-stu-id="6849b-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="6849b-116">Si vous avez un compte personnel et un journal avec un id Microsoft, vous devez trop[créer un id de travail de votre personnel une](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6849b-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="6849b-117">Soit--selon votre système d’exploitation du client--hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello [CLI d’Azure pour Mac, Linux et Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6849b-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="6849b-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="6849b-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="6849b-119">OpenSSL est utilisé toogenerate hello les certificats nécessaires.</span><span class="sxs-lookup"><span data-stu-id="6849b-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="6849b-120">Un client Git, comme [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="6849b-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="6849b-121">tootest hello exemple d’application, vous devez également un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="6849b-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="6849b-122">Vous pouvez utiliser les serveurs ou services DNS qui prennent en charge les enregistrements DNS de caractères génériques A Record.</span><span class="sxs-lookup"><span data-stu-id="6849b-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="6849b-123">Un ordinateur toorun Deis des outils clients.</span><span class="sxs-lookup"><span data-stu-id="6849b-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="6849b-124">Vous pouvez utiliser un ordinateur local ou une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6849b-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="6849b-125">Vous pouvez exécuter ces outils sur presque n’importe quel distribution Linux, mais Ubuntu utilisent hello instructions suivantes.</span><span class="sxs-lookup"><span data-stu-id="6849b-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="6849b-126">Cluster hello de disposition</span><span class="sxs-lookup"><span data-stu-id="6849b-126">Provision hello cluster</span></span>
<span data-ttu-id="6849b-127">Dans cette section, vous allez utiliser un [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) modèle à partir du référentiel open source de hello [modèles de démarrage rapide azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6849b-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="6849b-128">Tout d’abord, vous allez copier vers le bas du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="6849b-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="6849b-129">Ensuite, créez une paire de clés SSH à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="6849b-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="6849b-130">Ensuite, configurez le nouvel identifiant de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6849b-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="6849b-131">Et enfin, vous allez utiliser le script de Shell hello ou le cluster hello tooprovision hello PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="6849b-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="6849b-132">Référentiel de hello clone : [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6849b-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="6849b-133">Atteindre le dossier de modèles toohello :</span><span class="sxs-lookup"><span data-stu-id="6849b-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="6849b-134">Créez une paire de clés SSH à l’aide de l’outil ssh-keygen :</span><span class="sxs-lookup"><span data-stu-id="6849b-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="6849b-135">Générer un certificat à l’aide de hello au-dessus de clé privée :</span><span class="sxs-lookup"><span data-stu-id="6849b-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="6849b-136">Accédez trop[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate un nouveau jeton de cluster, qui ressemble à quelque chose comme :</span><span class="sxs-lookup"><span data-stu-id="6849b-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="6849b-137">Chaque cluster CoreOS doit toohave un jeton unique à partir de ce service gratuit.</span><span class="sxs-lookup"><span data-stu-id="6849b-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="6849b-138">Pour plus d’informations, voir la [documentation CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) .</span><span class="sxs-lookup"><span data-stu-id="6849b-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="6849b-139">Modifier hello **cloud-config.yaml** fichier existant de hello tooreplace **découverte** jeton avec le nouveau jeton d’hello :</span><span class="sxs-lookup"><span data-stu-id="6849b-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="6849b-140">Modifier hello **azuredeploy-parameters.json** fichier : certificat hello ouvrir créé à l’étape 4 dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="6849b-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="6849b-141">Copiez tout le texte entre `----BEGIN CERTIFICATE-----` et `-----END CERTIFICATE-----` dans hello **sshKeyData** paramètre (vous devez tooremove tous les caractères de saut de ligne).</span><span class="sxs-lookup"><span data-stu-id="6849b-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="6849b-142">Modifier hello **newStorageAccountName** paramètre.</span><span class="sxs-lookup"><span data-stu-id="6849b-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="6849b-143">Il s’agit de compte de stockage hello pour les disques de machine virtuelle du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="6849b-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="6849b-144">Nom de ce compte a toobe global unique.</span><span class="sxs-lookup"><span data-stu-id="6849b-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="6849b-145">Modifier hello **publicDomainName** paramètre.</span><span class="sxs-lookup"><span data-stu-id="6849b-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="6849b-146">Cela va faire partie du nom DNS de hello associé hello charge équilibrage adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="6849b-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="6849b-147">Hello FQDN final auront hello format de *[valeur de ce paramètre]*. *[Région]* . cloudapp.azure.com. Par exemple, si vous spécifiez le nom de hello en tant que deishbai32, et groupe de ressources hello est la région ouest des États-Unis toohello déployé, puis hello final équilibrage de charge de nom de domaine complet tooyour sera deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6849b-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="6849b-148">Enregistrez le fichier de paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="6849b-148">Save hello parameter file.</span></span> <span data-ttu-id="6849b-149">Et ensuite, vous pouvez configurer cluster hello à l’aide d’Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="6849b-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="6849b-150">ou de la CLI Azure :</span><span class="sxs-lookup"><span data-stu-id="6849b-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="6849b-151">Une fois le groupe de ressources hello est configuré, vous pouvez voir toutes les ressources hello dans le groupe de hello sur le portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="6849b-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="6849b-152">Comme indiqué dans hello suivant hello capture d’écran, groupe de ressources contient un réseau virtuel avec trois machines virtuelles, qui sont jointes toohello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6849b-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="6849b-153">groupe de Hello contient également un équilibreur de charge, ce qui a une adresse IP publique associée.</span><span class="sxs-lookup"><span data-stu-id="6849b-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Hello configuré le groupe de ressources sur le portail Azure classic](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="6849b-155">Installer le client de hello</span><span class="sxs-lookup"><span data-stu-id="6849b-155">Install hello client</span></span>
<span data-ttu-id="6849b-156">Vous devez **deisctl** toocontrol votre Deis de cluster.</span><span class="sxs-lookup"><span data-stu-id="6849b-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="6849b-157">Deisctl est installé automatiquement dans tous les nœuds de cluster hello, mais il est un deisctl toouse de bonnes pratiques sur un ordinateur d’administration distinct.</span><span class="sxs-lookup"><span data-stu-id="6849b-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="6849b-158">En outre, étant donné que tous les nœuds sont configurés avec uniquement des adresses IP privées, vous devez toouse SSH tunneling via l’équilibrage de charge hello, qui a une adresse IP publique, ordinateurs de nœud tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="6849b-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="6849b-159">Hello Voici étapes hello paramétrant deisctl sur un ordinateur virtuel ou Ubuntu physique distinct.</span><span class="sxs-lookup"><span data-stu-id="6849b-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="6849b-160">Installez deisctl:mkdir deis.</span><span class="sxs-lookup"><span data-stu-id="6849b-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="6849b-161">Ajoutez votre agent toossh de clé privée :</span><span class="sxs-lookup"><span data-stu-id="6849b-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="6849b-162">Configurez deisctl :</span><span class="sxs-lookup"><span data-stu-id="6849b-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="6849b-163">Hello modèle définit les règles NAT entrantes qui mappent 2223 tooinstance 1, 2224 tooinstance 2 et 2225 tooinstance 3.</span><span class="sxs-lookup"><span data-stu-id="6849b-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="6849b-164">Cela procure une redondance pour l’outil de deisctl hello.</span><span class="sxs-lookup"><span data-stu-id="6849b-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="6849b-165">Vous pouvez examiner ces règles sur le portail Azure Classic :</span><span class="sxs-lookup"><span data-stu-id="6849b-165">You can examine these rules on Azure classic portal:</span></span>

![Règles NAT sur l’équilibrage de charge hello](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="6849b-167">Actuellement le modèle de hello prend uniquement en charge les clusters à 3 nœuds.</span><span class="sxs-lookup"><span data-stu-id="6849b-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="6849b-168">En effet, la définition des règles NAT des modèles Azure Resource Manager présente une limitation : elle ne prend pas en charge la syntaxe de boucle.</span><span class="sxs-lookup"><span data-stu-id="6849b-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="6849b-169">Installez et démarrez hello Deis de plate-forme</span><span class="sxs-lookup"><span data-stu-id="6849b-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="6849b-170">Vous pouvez désormais utiliser deisctl tooinstall et démarrer hello Deis plateforme :</span><span class="sxs-lookup"><span data-stu-id="6849b-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="6849b-171">Plateforme de hello départ prend un certain temps (jusqu'à 10 minutes).</span><span class="sxs-lookup"><span data-stu-id="6849b-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="6849b-172">En particulier, le démarrage du service de générateur hello peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="6849b-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="6849b-173">Et parfois, il prend quelques tentatives toosucceed : si l’opération de hello semble toohang, essayez de taper `ctrl+c` exécution toobreak de commande hello, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="6849b-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="6849b-174">Vous pouvez utiliser `deisctl list` tooverify si tous les services sont en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="6849b-174">You can use `deisctl list` tooverify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="6849b-175">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="6849b-175">Congratulations!</span></span> <span data-ttu-id="6849b-176">Votre nouveau cluster Deis est opérationnel sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6849b-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="6849b-177">Ensuite, nous allons déployer un cluster de hello Go application toosee dans l’action de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="6849b-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="6849b-178">Déployer et mettre à l’échelle une application Hello World</span><span class="sxs-lookup"><span data-stu-id="6849b-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="6849b-179">Hello étapes suivantes montrent comment toodeploy « Hello World » accédez cluster toohello d’application.</span><span class="sxs-lookup"><span data-stu-id="6849b-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="6849b-180">étapes de Hello sont basées sur [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="6849b-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="6849b-181">Pour hello routage maillage toowork correctement, vous devez toohave un enregistrement générique A pour votre domaine pointe toohello adresse IP publique de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="6849b-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="6849b-182">Hello capture d’écran suivante affiche hello un enregistrement d’un enregistrement de domaine exemple sur GoDaddy :</span><span class="sxs-lookup"><span data-stu-id="6849b-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Enregistrement « A Record » GoDaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="6849b-184">Installez l’outil deis :</span><span class="sxs-lookup"><span data-stu-id="6849b-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="6849b-185">Créer une clé SSH, puis ajoutez hello tooGitHub de clé publique (bien entendu, vous pouvez également réutiliser vos clés existantes).</span><span class="sxs-lookup"><span data-stu-id="6849b-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="6849b-186">toocreate une nouvelle paire de clés SSH, utilisez :</span><span class="sxs-lookup"><span data-stu-id="6849b-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="6849b-187">Ajoutez id_rsa.pub ou hello de clé publique de votre choix, tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="6849b-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="6849b-188">Pour cela, à l’aide de hello ajouter SSH bouton clé dans l’écran de configuration de clés SSH :</span><span class="sxs-lookup"><span data-stu-id="6849b-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Clé GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="6849b-190">Enregistrez un nouvel utilisateur :</span><span class="sxs-lookup"><span data-stu-id="6849b-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="6849b-191">Ajoutez la clé SSH hello :</span><span class="sxs-lookup"><span data-stu-id="6849b-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="6849b-192">Créez une application.</span><span class="sxs-lookup"><span data-stu-id="6849b-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="6849b-193">
8.push de git Hello déclenchera Docker images toobe généré et déployé, qui prendra quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="6849b-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="6849b-194">À partir de mon expérience, occasionnellement, étape 10 (référentiel de push image tooprivate) peut se bloquer.</span><span class="sxs-lookup"><span data-stu-id="6849b-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="6849b-195">Dans ce cas, vous pouvez arrêter le processus de hello, à l’aide de remove hello application ' deis applications : détruire : un <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind nom hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="6849b-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="6849b-196">Si tout fonctionne, vous devez voir quelque chose comme suit hello à fin hello de sorties de commandes :</span><span class="sxs-lookup"><span data-stu-id="6849b-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="6849b-197">Vérifiez si l’application hello fonctionne :</span><span class="sxs-lookup"><span data-stu-id="6849b-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="6849b-198">Ce qui suit doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="6849b-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="6849b-199">Mettre à l’échelle too3 instances de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="6849b-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="6849b-200">Si vous le souhaitez, vous pouvez utiliser deis Infos tooexamine détails de votre application.</span><span class="sxs-lookup"><span data-stu-id="6849b-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="6849b-201">Hello sorties suivantes sont mon déploiement d’application :</span><span class="sxs-lookup"><span data-stu-id="6849b-201">hello following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="6849b-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6849b-202">Next Steps</span></span>
<span data-ttu-id="6849b-203">Cet article vous parcouru toutes les tooprovision d’étapes hello Deis un nouveau cluster sur Azure à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6849b-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="6849b-204">modèle de Hello prend en charge la redondance dans les connexions, ainsi que pour les applications déployées d’équilibrage de charge des outils.</span><span class="sxs-lookup"><span data-stu-id="6849b-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="6849b-205">modèle de Hello évite également à l’aide d’adresses IP publiques sur les nœuds membres, qui enregistre des précieuses ressources IP publics et fournit un environnement plus sécurisé d’applications toohost.</span><span class="sxs-lookup"><span data-stu-id="6849b-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="6849b-206">toolearn, voir hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="6849b-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="6849b-207">[Présentation d’Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="6849b-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="6849b-208">[Comment toouse hello CLI d’Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="6849b-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="6849b-209">[Utilisation d’Azure PowerShell avec Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="6849b-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
