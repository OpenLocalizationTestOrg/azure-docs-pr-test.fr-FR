---
title: aaaUse Docker Compose sur un VM Linux dans Azure | Documents Microsoft
description: "Comment toouse Docker et composition sur les ordinateurs virtuels Linux avec hello CLI d’Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="c1e39-103">Obtenir main toodefine Docker et composer et exécuter une application conteneur multiples dans Azure</span><span class="sxs-lookup"><span data-stu-id="c1e39-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="c1e39-104">Avec [composition](http://github.com/docker/compose), vous utilisez une application composée de plusieurs conteneurs Docker un toodefine de fichier texte simple.</span><span class="sxs-lookup"><span data-stu-id="c1e39-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="c1e39-105">Vous ensuite lancer votre application dans une commande unique qui fait tout toodeploy votre environnement défini.</span><span class="sxs-lookup"><span data-stu-id="c1e39-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="c1e39-106">Par exemple, cet article explique comment tooquickly configurer un blog WordPress avec un service principal de base de données MariaDB SQL sur une VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c1e39-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="c1e39-107">Vous pouvez également utiliser tooset composer des applications plus complexes.</span><span class="sxs-lookup"><span data-stu-id="c1e39-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="c1e39-108">Configurer une machine virtuelle Linux en tant qu’hôte Docker</span><span class="sxs-lookup"><span data-stu-id="c1e39-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="c1e39-109">Vous pouvez utiliser différentes procédures Azure et des images disponibles ou des modèles du Gestionnaire de ressources dans Azure Marketplace de hello toocreate un VM Linux et le configurer comme un hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="c1e39-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="c1e39-110">Par exemple, consultez [votre environnement à l’aide de hello Extension de machine virtuelle Docker toodeploy](dockerextension.md) tooquickly créer une VM Ubuntu avec hello extension de machine virtuelle de Azure Docker à l’aide un [modèle de démarrage rapide](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c1e39-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="c1e39-111">Lorsque vous utilisez des extensions de machine virtuelle de Docker hello, votre machine virtuelle est automatiquement configuré comme un hôte Docker et composition est déjà installée.</span><span class="sxs-lookup"><span data-stu-id="c1e39-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="c1e39-112">Créer un hôte Docker avec Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c1e39-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="c1e39-113">Hello installation dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c1e39-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c1e39-114">Tout d’abord, créez un groupe de ressources pour votre environnement Docker avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c1e39-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c1e39-115">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="c1e39-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="c1e39-116">Ensuite, déployez une machine virtuelle avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create) qui inclut l’extension de machine virtuelle de Azure Docker hello de [ce modèle Azure Resource Manager sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c1e39-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="c1e39-117">Fournissez vos propres valeurs pour *newStorageAccountName*, *adminUsername*, *adminPassword* et *dnsNameForPublicIP* :</span><span class="sxs-lookup"><span data-stu-id="c1e39-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="c1e39-118">Il prend quelques minutes pour hello déploiement toofinish.</span><span class="sxs-lookup"><span data-stu-id="c1e39-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="c1e39-119">Une fois le déploiement de hello est terminé, [déplacer l’étape de toonext](#verify-that-compose-is-installed) tooSSH tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c1e39-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="c1e39-120">Invite de toohello tooinstead redonner le contrôle et de déploiement de hello permettent continuent en arrière-plan de hello, ajoutez éventuellement hello `--no-wait` indicateur toohello précédant la commande.</span><span class="sxs-lookup"><span data-stu-id="c1e39-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="c1e39-121">Ce processus vous permet de tooperform autre travail Bonjour CLI pendant le déploiement hello se poursuit pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c1e39-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="c1e39-122">Vous pouvez ensuite afficher plus d’informations sur l’état de l’hôte Docker hello avec [afficher de machine virtuelle az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="c1e39-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="c1e39-123">Hello exemple suivant vérifie état hello Hello ordinateur virtuel nommé *myDockerVM* (hello nom par défaut à partir du modèle de hello - ne modifiez pas ce nom) dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c1e39-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="c1e39-124">Lorsque cette commande retourne *Succeeded*, hello déploiement est terminé et que vous pouvez SSH toohello VM Bonjour suivant l’étape.</span><span class="sxs-lookup"><span data-stu-id="c1e39-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="c1e39-125">Vérifier que Compose est installé</span><span class="sxs-lookup"><span data-stu-id="c1e39-125">Verify that Compose is installed</span></span>
<span data-ttu-id="c1e39-126">Une fois le déploiement de hello est terminé, SSH tooyour nouvel hôte Docker à l’aide du nom DNS de hello que vous avez fourni pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="c1e39-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="c1e39-127">Vous pouvez utiliser `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview les détails de votre machine virtuelle, y compris le nom DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="c1e39-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="c1e39-128">toocheck composer est installé sur hello machine virtuelle, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c1e39-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="c1e39-129">Vous obtenez une sortie similaire*docker-composer 1.6.2, générez 4D 72027*.</span><span class="sxs-lookup"><span data-stu-id="c1e39-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="c1e39-130">Si vous avez utilisé une autre méthode toocreate un hôte Docker et devez tooinstall composer vous-même, consultez hello [composer documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="c1e39-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="c1e39-131">Créer un fichier de configuration docker-compose.yml</span><span class="sxs-lookup"><span data-stu-id="c1e39-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="c1e39-132">Ensuite, créez un `docker-compose.yml` fichier, qui est simplement un fichier texte de configuration, toorun de conteneurs Docker toodefine hello sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c1e39-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="c1e39-133">fichier de Hello spécifie hello image toorun sur chaque conteneur (ou elle peut être une build à partir d’un fichier Dockerfile), liens hello entre les conteneurs et les dépendances, les ports et les variables d’environnement nécessaires.</span><span class="sxs-lookup"><span data-stu-id="c1e39-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="c1e39-134">Pour plus d’informations sur la syntaxe du fichier yml, consultez [Référence du fichier Compose](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="c1e39-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="c1e39-135">Créer hello *docker-compose.yml* de fichiers comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1e39-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="c1e39-136">Utilisez votre tooadd de l’éditeur de texte favori certains fichiers toohello de données.</span><span class="sxs-lookup"><span data-stu-id="c1e39-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="c1e39-137">exemple Hello utilise hello *vi* éditeur :</span><span class="sxs-lookup"><span data-stu-id="c1e39-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="c1e39-138">Hello coller l’exemple suivant dans votre fichier texte.</span><span class="sxs-lookup"><span data-stu-id="c1e39-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="c1e39-139">Cette configuration utilise des images de hello [docker Hub Registre](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source contenu et création de blogs système de gestion) et un principal lié MariaDB SQL de base de données.</span><span class="sxs-lookup"><span data-stu-id="c1e39-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="c1e39-140">Entrez votre propre *MYSQL_ROOT_PASSWORD* comme suit :</span><span class="sxs-lookup"><span data-stu-id="c1e39-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="c1e39-141">Conteneurs de hello démarrer avec un nouveau message</span><span class="sxs-lookup"><span data-stu-id="c1e39-141">Start hello containers with Compose</span></span>
<span data-ttu-id="c1e39-142">Dans hello même répertoire que votre *docker-compose.yml* fichier, exécutez hello commande suivante (selon votre environnement, vous devrez peut-être toorun `docker-compose` à l’aide de `sudo`) :</span><span class="sxs-lookup"><span data-stu-id="c1e39-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="c1e39-143">Cette commande démarre les conteneurs Docker hello spécifiés dans *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="c1e39-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="c1e39-144">Il prend une ou deux minutes pour toocomplete de cette étape.</span><span class="sxs-lookup"><span data-stu-id="c1e39-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="c1e39-145">Vous consultez toohello similaire de sortie l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c1e39-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="c1e39-146">Être vraiment toouse hello **-d** option de démarrage afin que les conteneurs hello s’exécutent en arrière-plan de hello en continu.</span><span class="sxs-lookup"><span data-stu-id="c1e39-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="c1e39-147">tooverify qui sont des conteneurs de hello, type `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="c1e39-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="c1e39-148">Le résultat suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="c1e39-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="c1e39-149">Vous pouvez désormais connecter tooWordPress directement sur la machine virtuelle sur le port 80 de hello.</span><span class="sxs-lookup"><span data-stu-id="c1e39-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="c1e39-150">Ouvrez un navigateur web et entrez le nom DNS de hello de votre machine virtuelle (tel que `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="c1e39-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="c1e39-151">Vous devez maintenant voir hello que WordPress démarrer écran, où vous effectuez l’installation de hello et prise en main application hello.</span><span class="sxs-lookup"><span data-stu-id="c1e39-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![Écran d’accueil WordPress][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="c1e39-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c1e39-153">Next steps</span></span>
* <span data-ttu-id="c1e39-154">Accédez toohello [guide utilisateur de l’extension Docker VM](https://github.com/Azure/azure-docker-extension/blob/master/README.md) pour plus d’options tooconfigure Docker et composition de votre machine virtuelle Docker.</span><span class="sxs-lookup"><span data-stu-id="c1e39-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="c1e39-155">Par exemple, une option est tooput hello composition yml fichier (converti tooJSON) directement dans la configuration de hello Hello extension de machine virtuelle de Docker.</span><span class="sxs-lookup"><span data-stu-id="c1e39-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="c1e39-156">Extraire hello [composer une référence de ligne de commande](http://docs.docker.com/compose/reference/) et [guide de l’utilisateur](http://docs.docker.com/compose/) pour plus d’exemples de génération et de déploiement d’applications de conteneur multiples.</span><span class="sxs-lookup"><span data-stu-id="c1e39-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="c1e39-157">Utiliser un modèle Azure Resource Manager, soit votre propre ou un obtenue à partir de hello [Communauté](https://azure.microsoft.com/documentation/templates/), toodeploy une machine virtuelle de Azure avec Docker et une application peut être configuré avec la composition.</span><span class="sxs-lookup"><span data-stu-id="c1e39-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="c1e39-158">Par exemple, hello [déployer un blog WordPress avec Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) modèle utilise Docker et composition tooquickly déployer WordPress avec un serveur MySQL principal sur un VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c1e39-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="c1e39-159">Essayez d’intégrer Docker Compose à un cluster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="c1e39-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="c1e39-160">Pour examiner des scénarios, consultez [Utilisation de Compose avec Swarm](https://docs.docker.com/compose/swarm/) .</span><span class="sxs-lookup"><span data-stu-id="c1e39-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
