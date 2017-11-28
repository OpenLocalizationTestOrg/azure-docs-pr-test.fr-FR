---
title: "Déploiement d’un cluster Deis à 3 nœuds | Microsoft Docs"
description: "Cet article explique comment créer un cluster Deis à 3 nœuds sur Azure à l’aide d’un modèle Azure Resource Manager."
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
ms.openlocfilehash: 9a0c3dd7562dfb5ce54c2ebfd4665109f59cd8fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="6c7df-103">Déployer et configurer un cluster Deis à 3 nœuds dans Azure</span><span class="sxs-lookup"><span data-stu-id="6c7df-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="6c7df-104">Cet article vous détaille l’approvisionnement d’un cluster [Deis](http://deis.io/) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7df-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="6c7df-105">Il aborde toutes les étapes, de la création des certificats requis au déploiement et à la mise à l’échelle d’un exemple d’application **Go** sur le cluster qui vient d’être approvisionné.</span><span class="sxs-lookup"><span data-stu-id="6c7df-105">It covers all the steps from creating the necessary certificates to deploying and scaling a sample **Go** application on the newly provisioned cluster.</span></span>

<span data-ttu-id="6c7df-106">Le diagramme suivant représente l’architecture du système déployé.</span><span class="sxs-lookup"><span data-stu-id="6c7df-106">The following diagram shows the architecture of the deployed system.</span></span> <span data-ttu-id="6c7df-107">Un administrateur système gère le cluster à l’aide d’outils Deis, comme **deis** et **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="6c7df-107">A system administrator manages the cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="6c7df-108">Les connexions sont établies via un équilibreur de charge Azure, qui transfère les connexions à l’un des nœuds membres du cluster.</span><span class="sxs-lookup"><span data-stu-id="6c7df-108">Connections are established through an Azure load balancer, which forwards the connections to one of the member nodes on the cluster.</span></span> <span data-ttu-id="6c7df-109">Les clients accèdent aux applications déployées via l’équilibreur de charge, également.</span><span class="sxs-lookup"><span data-stu-id="6c7df-109">The clients access deployed applications through the load balancer as well.</span></span> <span data-ttu-id="6c7df-110">Dans ce cas, l’équilibreur de charge envoie le trafic à un maillage de routeur Deis, qui achemine le trafic vers des conteneurs Docker hébergés sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="6c7df-110">In this case, the load balancer forwards the traffic to a Deis router mesh, which further routs traffic to corresponding Docker containers hosted on the cluster.</span></span>

  ![Diagramme d’architecture du cluster Deis déployé](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="6c7df-112">Pour exécuter les étapes suivantes, vous aurez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6c7df-112">In order to run through the following steps, you'll need:</span></span>

* <span data-ttu-id="6c7df-113">Un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6c7df-113">An active Azure subscription.</span></span> <span data-ttu-id="6c7df-114">Si vous n’en avez pas, vous pouvez obtenir une version d’essai sur [azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6c7df-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="6c7df-115">Un ID professionnel ou scolaire afin de pouvoir utiliser des groupes de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7df-115">A work or school id to use Azure resource groups.</span></span> <span data-ttu-id="6c7df-116">Si vous avez un compte personnel et que vous vous connectez avec un ID Microsoft, vous devez [créer un ID de travail à partir de votre ID personnel](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c7df-116">If you have a personal account and log in with a Microsoft id, you need to [create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="6c7df-117">Il vous faut également l’outil [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou la [CLI Azure pour Mac, Linux et Windows](../../cli-install-nodejs.md) de votre système d’exploitation client.</span><span class="sxs-lookup"><span data-stu-id="6c7df-117">Either -- depending on your client operating system -- the [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="6c7df-118">[OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="6c7df-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="6c7df-119">OpenSSL est utilisé pour générer les certificats nécessaires.</span><span class="sxs-lookup"><span data-stu-id="6c7df-119">OpenSSL is used to generate the necessary certificates.</span></span>
* <span data-ttu-id="6c7df-120">Un client Git, comme [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="6c7df-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="6c7df-121">Vous devez également configurer un serveur DNS pour pouvoir tester l’exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="6c7df-121">To test the sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="6c7df-122">Vous pouvez utiliser les serveurs ou services DNS qui prennent en charge les enregistrements DNS de caractères génériques A Record.</span><span class="sxs-lookup"><span data-stu-id="6c7df-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="6c7df-123">Un ordinateur pour exécuter les outils clients Deis.</span><span class="sxs-lookup"><span data-stu-id="6c7df-123">A computer to run Deis client tools.</span></span> <span data-ttu-id="6c7df-124">Vous pouvez utiliser un ordinateur local ou une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c7df-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="6c7df-125">Vous pouvez exécuter ces outils sur n’importe quelle distribution Linux. Toutefois, les instructions suivantes concernent Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6c7df-125">You can run these tools on almost any Linux distribution, but the following instructions use Ubuntu.</span></span>

## <a name="provision-the-cluster"></a><span data-ttu-id="6c7df-126">Approvisionner le cluster</span><span class="sxs-lookup"><span data-stu-id="6c7df-126">Provision the cluster</span></span>
<span data-ttu-id="6c7df-127">Dans cette section, vous allez utiliser un modèle [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) à partir du dépôt open source [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6c7df-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from the open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="6c7df-128">Tout d’abord, copiez le modèle.</span><span class="sxs-lookup"><span data-stu-id="6c7df-128">First, you'll copy down the template.</span></span> <span data-ttu-id="6c7df-129">Ensuite, créez une paire de clés SSH à des fins d’authentification.</span><span class="sxs-lookup"><span data-stu-id="6c7df-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="6c7df-130">Ensuite, configurez le nouvel identifiant de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="6c7df-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="6c7df-131">Enfin, utilisez le script Shell ou le script PowerShell pour approvisionner le cluster.</span><span class="sxs-lookup"><span data-stu-id="6c7df-131">And finally, you'll use either the Shell script or the PowerShell script to provision the cluster.</span></span>

1. <span data-ttu-id="6c7df-132">Clonez le dépôt : [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6c7df-132">Clone the repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="6c7df-133">Accédez au dossier de modèles :</span><span class="sxs-lookup"><span data-stu-id="6c7df-133">Go to the template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="6c7df-134">Créez une paire de clés SSH à l’aide de l’outil ssh-keygen :</span><span class="sxs-lookup"><span data-stu-id="6c7df-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="6c7df-135">Générez un certificat à l’aide de la clé privée ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="6c7df-135">Generate a certificate using the above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. <span data-ttu-id="6c7df-136">Accédez à l’élément [https://discovery.etcd.io/new](https://discovery.etcd.io/new) pour générer un nouveau jeton de cluster, qui ressemblera à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="6c7df-136">Go to [https://discovery.etcd.io/new](https://discovery.etcd.io/new) to generate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="6c7df-137">Chaque cluster CoreOS doit bénéficier d’un jeton unique, fourni par ce service gratuit.</span><span class="sxs-lookup"><span data-stu-id="6c7df-137">Each CoreOS cluster needs to have a unique token from this free service.</span></span> <span data-ttu-id="6c7df-138">Pour plus d’informations, voir la [documentation CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) .</span><span class="sxs-lookup"><span data-stu-id="6c7df-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="6c7df-139">Modifiez le fichier **cloud-config.yaml** afin de remplacer le jeton **discovery** existant par le nouveau jeton :</span><span class="sxs-lookup"><span data-stu-id="6c7df-139">Modify the **cloud-config.yaml** file to replace the existing  **discovery** token with the new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="6c7df-140">Modifiez le fichier **azuredeploy-parameters.json** : ouvrez le certificat que vous avez créé à l’étape 4 dans un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="6c7df-140">Modify the **azuredeploy-parameters.json** file: Open the certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="6c7df-141">Copiez le texte figurant entre les éléments `----BEGIN CERTIFICATE-----` et `-----END CERTIFICATE-----`, et collez-le dans le paramètre **sshKeyData** (vous devrez supprimer tous les caractères de saut de ligne).</span><span class="sxs-lookup"><span data-stu-id="6c7df-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into the **sshKeyData** parameter (you'll need to remove all newline characters).</span></span>
8. <span data-ttu-id="6c7df-142">Modifiez le paramètre **newStorageAccountName** .</span><span class="sxs-lookup"><span data-stu-id="6c7df-142">Modify the **newStorageAccountName** parameter.</span></span> <span data-ttu-id="6c7df-143">Il s’agit du compte de stockage associé aux disques du système d’exploitation de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6c7df-143">This is the storage account for VM OS disks.</span></span> <span data-ttu-id="6c7df-144">Le nom de ce compte doit être unique au niveau global.</span><span class="sxs-lookup"><span data-stu-id="6c7df-144">This account name has to be globally unique.</span></span>
9. <span data-ttu-id="6c7df-145">Modifiez le paramètre **publicDomainName** .</span><span class="sxs-lookup"><span data-stu-id="6c7df-145">Modify the **publicDomainName** parameter.</span></span> <span data-ttu-id="6c7df-146">Il fera partie du nom DNS associé à l’adresse IP publique de l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="6c7df-146">This will become part of the DNS name associated with the load balancer public IP.</span></span> <span data-ttu-id="6c7df-147">Le FQDN présente la valeur suivante : *[valeur de ce paramètre]*.*[région]*.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6c7df-147">The final FQDN will have the format of *[value of this parameter]*.*[region]*.cloudapp.azure.com.</span></span> <span data-ttu-id="6c7df-148">Par exemple, si vous spécifiez le nom « deishbai32 » et que le groupe de ressources est déployé dans la région ouest des États-Unis, le FQDN final de votre équilibreur de charge sera le suivant : deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="6c7df-148">For example, if you specify the name as deishbai32, and the resource group is deployed to the West US region, then the final FQDN to your load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="6c7df-149">Enregistrez le fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="6c7df-149">Save the parameter file.</span></span> <span data-ttu-id="6c7df-150">Ensuite, vous pouvez approvisionner le cluster au moyen de Microsoft Azure PowerShell :</span><span class="sxs-lookup"><span data-stu-id="6c7df-150">And then you can provision the cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="6c7df-151">ou de la CLI Azure :</span><span class="sxs-lookup"><span data-stu-id="6c7df-151">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="6c7df-152">Une fois que le groupe de ressources est approvisionné, vous pouvez voir toutes les ressources dans le groupe sur le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="6c7df-152">Once the resource group is provisioned, you can see all the resources in the group on Azure classic portal.</span></span> <span data-ttu-id="6c7df-153">Comme le montre la capture d’écran suivante, le groupe de ressources contient un réseau virtuel incluant trois machines virtuelles, associées au même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="6c7df-153">As shown in the following screenshot, the resource group contains a virtual network with three VMs, which are joined to the same availability set.</span></span> <span data-ttu-id="6c7df-154">Le groupe contient également un équilibreur de charge, qui est associé à une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="6c7df-154">The group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Groupe de ressources provisionné sur le portail Azure Classic](./media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a><span data-ttu-id="6c7df-156">Installation du client</span><span class="sxs-lookup"><span data-stu-id="6c7df-156">Install the client</span></span>
<span data-ttu-id="6c7df-157">Vous devez utiliser l’outil **deisctl** pour contrôler votre cluster Deis.</span><span class="sxs-lookup"><span data-stu-id="6c7df-157">You need **deisctl** to control your Deis cluster.</span></span> <span data-ttu-id="6c7df-158">Bien que cet outil soit automatiquement installé sur tous les nœuds du cluster, nous vous recommandons de l’utiliser sur un ordinateur d’administration distinct.</span><span class="sxs-lookup"><span data-stu-id="6c7df-158">Although deisctl is automatically installed in all the cluster nodes, it's a good practice to use deisctl on a separate administrative machine.</span></span> <span data-ttu-id="6c7df-159">En outre, comme tous les nœuds sont configurés avec des adresses IP privées uniquement, vous devrez utiliser un tunnel SSL via l’équilibreur de charge, qui présente une adresse IP publique, pour la connexion à tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="6c7df-159">Furthermore, because all nodes are configured with only private IP addresses, you'll need to use SSH tunneling through the load balancer, which has a public IP, to connect to the node machines.</span></span> <span data-ttu-id="6c7df-160">Voici les étapes à suivre pour configurer l’outil deisctl sur une machine virtuelle ou physique distincte dotée d’Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6c7df-160">The following are the steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="6c7df-161">Installez deisctl:mkdir deis.</span><span class="sxs-lookup"><span data-stu-id="6c7df-161">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="6c7df-162">Ajoutez votre clé privée à l’agent ssh :</span><span class="sxs-lookup"><span data-stu-id="6c7df-162">Add your private key to ssh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. <span data-ttu-id="6c7df-163">Configurez deisctl :</span><span class="sxs-lookup"><span data-stu-id="6c7df-163">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

<span data-ttu-id="6c7df-164">Le modèle définit les règles NAT entrantes qui mappent la valeur 2223 à l’instance 1, la valeur 2224, à l’instance 2 et la valeur 2225, à l’instance 3.</span><span class="sxs-lookup"><span data-stu-id="6c7df-164">The template defines inbound NAT rules that map 2223 to instance 1, 2224 to instance 2, and 2225 to instance 3.</span></span> <span data-ttu-id="6c7df-165">Cela assure la redondance liée à l’utilisation de l’outil deisctl.</span><span class="sxs-lookup"><span data-stu-id="6c7df-165">This provides redundancy for using the deisctl tool.</span></span> <span data-ttu-id="6c7df-166">Vous pouvez examiner ces règles sur le portail Azure Classic :</span><span class="sxs-lookup"><span data-stu-id="6c7df-166">You can examine these rules on Azure classic portal:</span></span>

![Règles NAT sur l’équilibreur de charge](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="6c7df-168">Actuellement, le modèle prend uniquement en charge les clusters à 3 nœuds.</span><span class="sxs-lookup"><span data-stu-id="6c7df-168">Currently the template only supports 3-node clusters.</span></span> <span data-ttu-id="6c7df-169">En effet, la définition des règles NAT des modèles Azure Resource Manager présente une limitation : elle ne prend pas en charge la syntaxe de boucle.</span><span class="sxs-lookup"><span data-stu-id="6c7df-169">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-the-deis-platform"></a><span data-ttu-id="6c7df-170">Installer et démarrer la plateforme Deis</span><span class="sxs-lookup"><span data-stu-id="6c7df-170">Install and start the Deis platform</span></span>
<span data-ttu-id="6c7df-171">Vous pouvez désormais utiliser l’outil deisctl pour installer et démarrer la plate-forme Deis :</span><span class="sxs-lookup"><span data-stu-id="6c7df-171">Now you can use deisctl to install and start the Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="6c7df-172">Le démarrage de la plate-forme peut prendre un certain temps (jusqu’à 10 minutes, parfois).</span><span class="sxs-lookup"><span data-stu-id="6c7df-172">Starting the platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="6c7df-173">En particulier, le démarrage du service de générateur peut être long.</span><span class="sxs-lookup"><span data-stu-id="6c7df-173">Especially, starting the builder service can take a long time.</span></span> <span data-ttu-id="6c7df-174">De plus, vous devrez peut-être vous y prendre à plusieurs fois. Si l’opération se fige, appuyez sur `ctrl+c` pour arrêter l’exécution de la commande et recommencer.</span><span class="sxs-lookup"><span data-stu-id="6c7df-174">And sometimes it takes a few tries to succeed: If the operation seems to hang, try typing `ctrl+c` to break execution of the command and retry.</span></span>
> 
> 

<span data-ttu-id="6c7df-175">Vous pouvez utiliser la commande `deisctl list` pour vérifier si tous les services sont exécutés :</span><span class="sxs-lookup"><span data-stu-id="6c7df-175">You can use `deisctl list` to verify if all services are running:</span></span>

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

<span data-ttu-id="6c7df-176">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="6c7df-176">Congratulations!</span></span> <span data-ttu-id="6c7df-177">Votre nouveau cluster Deis est opérationnel sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6c7df-177">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="6c7df-178">À présent, nous allons déployer un exemple d’application Go pour voir le cluster en action.</span><span class="sxs-lookup"><span data-stu-id="6c7df-178">Next, let's deploy a sample Go application to see the cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="6c7df-179">Déployer et mettre à l’échelle une application Hello World</span><span class="sxs-lookup"><span data-stu-id="6c7df-179">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="6c7df-180">Les étapes suivantes indiquent comment déployer une application Go « Hellow World » sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="6c7df-180">The following steps show how to deploy a "Hello World" Go application to the cluster.</span></span> <span data-ttu-id="6c7df-181">Ces étapes sont basées sur la [documentation Deis](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="6c7df-181">The steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="6c7df-182">Pour que le maillage de routage fonctionne correctement, vous devrez disposer d’un enregistrement « A record » pour votre domaine, qui pointe sur l’adresse IP publique de l’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="6c7df-182">For the routing mesh to work properly, you’ll need to have a wildcard A record for your domain pointing to the public IP of the load balancer.</span></span> <span data-ttu-id="6c7df-183">La capture d’écran suivante illustre l’enregistrement « A record » associé à un exemple d’enregistrement de domaine sur GoDaddy :</span><span class="sxs-lookup"><span data-stu-id="6c7df-183">The following screenshot shows the A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Enregistrement « A Record » GoDaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="6c7df-185">Installez l’outil deis :</span><span class="sxs-lookup"><span data-stu-id="6c7df-185">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="6c7df-186">Créez une clé SSH, puis ajoutez la clé publique sur GitHub (bien sûr, vous pouvez également utiliser des clés existantes).</span><span class="sxs-lookup"><span data-stu-id="6c7df-186">Create a new SSH key, and then add the public key to GitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="6c7df-187">Pour créer une paire de clés SSH, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6c7df-187">To create a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. <span data-ttu-id="6c7df-188">Ajoute l’élément id_rsa.pub, ou la clé publique de votre choix, à GitHub.</span><span class="sxs-lookup"><span data-stu-id="6c7df-188">Add id_rsa.pub, or the public key of your choice, to GitHub.</span></span> <span data-ttu-id="6c7df-189">Pour cela, utilisez le bouton permettant d’ajouter une clé SSH sur l’écran de configuration des clés SSH :</span><span class="sxs-lookup"><span data-stu-id="6c7df-189">You can do this by using the Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Clé GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="6c7df-191">Enregistrez un nouvel utilisateur :</span><span class="sxs-lookup"><span data-stu-id="6c7df-191">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="6c7df-192">Ajoutez la clé SSH :</span><span class="sxs-lookup"><span data-stu-id="6c7df-192">Add the SSH key:</span></span>
   
        deis keys:add [path to your SSH public key]
   <p />      
7. <span data-ttu-id="6c7df-193">Créez une application.</span><span class="sxs-lookup"><span data-stu-id="6c7df-193">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="6c7df-194">
8. L’action Git de type push déclenche la création et le déploiement d’images Docker, qui peuvent prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="6c7df-194">
8. The git push will trigger Docker images to be built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="6c7df-195">D’après mon expérience, il arrive parfois que l’étape 10 (insertion d’images dans le dépôt privé) se bloque.</span><span class="sxs-lookup"><span data-stu-id="6c7df-195">From my experience, occasionally, Step 10 (Pushing image to private repository) may hang.</span></span> <span data-ttu-id="6c7df-196">Dans ce cas, vous pouvez arrêter le processus, supprimer l’application à l’aide de `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` pour identifier le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="6c7df-196">When this happens, you can stop the process, remove the application using `deis apps:destroy –a <application name>` to remove the application and try again. You can use `deis apps:list` to find out the name of your application.</span></span> <span data-ttu-id="6c7df-197">Si tout fonctionne, des éléments similaires à ce qui suit doivent figurer à la fin des sorties de commandes :</span><span class="sxs-lookup"><span data-stu-id="6c7df-197">If everything works out, you should see something like the following at the end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="6c7df-198">Vérifiez que l’application fonctionne :</span><span class="sxs-lookup"><span data-stu-id="6c7df-198">Verify if the application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="6c7df-199">Ce qui suit doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="6c7df-199">You should see:</span></span>
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. <span data-ttu-id="6c7df-200">Mettez l’application à l’échelle pour 3 instances :</span><span class="sxs-lookup"><span data-stu-id="6c7df-200">Scale the application to 3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="6c7df-201">Si vous le souhaitez, vous pouvez utiliser la commande « deis info » pour examiner les détails de votre application.</span><span class="sxs-lookup"><span data-stu-id="6c7df-201">Optionally, you can use deis info to examine details of your application.</span></span> <span data-ttu-id="6c7df-202">Les sorties suivantes proviennent du déploiement de mon application :</span><span class="sxs-lookup"><span data-stu-id="6c7df-202">The following outputs are from my application deployment:</span></span>
    
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

## <a name="next-steps"></a><span data-ttu-id="6c7df-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c7df-203">Next Steps</span></span>
<span data-ttu-id="6c7df-204">Cet article vous a présenté toutes les étapes d’approvisionnement d’un nouveau cluster Deis sur Azure, au moyen d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c7df-204">This article walked you through all the steps to provision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="6c7df-205">Le modèle prend en charge la redondance des outils de connexion, ainsi que l’équilibrage de charge des applications déployées.</span><span class="sxs-lookup"><span data-stu-id="6c7df-205">The template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="6c7df-206">Le modèle évite également d’utiliser des adresses IP publiques sur les nœuds membres, ce qui permet de préserver des ressources d’adresses IP publiques précieuses et fournit un environnement plus sécurisé pour les applications hôtes.</span><span class="sxs-lookup"><span data-stu-id="6c7df-206">The template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment to host applications.</span></span> <span data-ttu-id="6c7df-207">Pour en savoir plus, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="6c7df-207">To learn more, see the following articles:</span></span>

<span data-ttu-id="6c7df-208">[Présentation d’Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="6c7df-208">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="6c7df-209">[Utilisation de l’interface de ligne de commande Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="6c7df-209">[How to use the Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="6c7df-210">[Utilisation d’Azure PowerShell avec Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="6c7df-210">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
