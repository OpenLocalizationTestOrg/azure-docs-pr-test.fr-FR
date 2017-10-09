
* [<span data-ttu-id="afe1d-101">Création rapide d’une machine virtuelle dans Azure</span><span class="sxs-lookup"><span data-stu-id="afe1d-101">Quick-create a virtual machine in Azure</span></span>](#quick-create-a-vm-in-azure)
* [<span data-ttu-id="afe1d-102">Déploiement d’une machine virtuelle dans Azure à partir d’un modèle</span><span class="sxs-lookup"><span data-stu-id="afe1d-102">Deploy a virtual machine in Azure from a template</span></span>](#deploy-a-vm-in-azure-from-a-template)
* [<span data-ttu-id="afe1d-103">Création d’une machine virtuelle à partir d’une image personnalisée</span><span class="sxs-lookup"><span data-stu-id="afe1d-103">Create a virtual machine from a custom image</span></span>](#create-a-custom-vm-image)
* [<span data-ttu-id="afe1d-104">Déploiement d’une machine virtuelle qui utilise un réseau virtuel et un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="afe1d-104">Deploy a virtual machine that uses a virtual network and a load balancer</span></span>](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [<span data-ttu-id="afe1d-105">Suppression d’un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="afe1d-105">Remove a resource group</span></span>](#remove-a-resource-group)
* [<span data-ttu-id="afe1d-106">Afficher le journal hello pour un déploiement de groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="afe1d-106">Show hello log for a resource group deployment</span></span>](#show-the-log-for-a-resource-group-deployment)
* [<span data-ttu-id="afe1d-107">Affichage des informations relatives à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="afe1d-107">Display information about a virtual machine</span></span>](#display-information-about-a-virtual-machine)
* [<span data-ttu-id="afe1d-108">Connecter la machine virtuelle tooa Linux</span><span class="sxs-lookup"><span data-stu-id="afe1d-108">Connect tooa Linux-based virtual machine</span></span>](#log-on-to-a-linux-based-virtual-machine)
* [<span data-ttu-id="afe1d-109">Arrêt d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="afe1d-109">Stop a virtual machine</span></span>](#stop-a-virtual-machine)
* [<span data-ttu-id="afe1d-110">Démarrage d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="afe1d-110">Start a virtual machine</span></span>](#start-a-virtual-machine)
* [<span data-ttu-id="afe1d-111">Association d’un disque de données</span><span class="sxs-lookup"><span data-stu-id="afe1d-111">Attach a data disk</span></span>](#attach-a-data-disk)

## <a name="getting-ready"></a><span data-ttu-id="afe1d-112">Préparation</span><span class="sxs-lookup"><span data-stu-id="afe1d-112">Getting ready</span></span>
<span data-ttu-id="afe1d-113">Avant de pouvoir utiliser hello CLI d’Azure avec des groupes de ressources Azure, vous devez version CLI d’Azure toohave hello et un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="afe1d-113">Before you can use hello Azure CLI with Azure resource groups, you need toohave hello right Azure CLI version and an Azure account.</span></span> <span data-ttu-id="afe1d-114">Si vous n’avez pas hello CLI d’Azure, [installer](../articles/cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="afe1d-114">If you don't have hello Azure CLI, [install it](../articles/cli-install-nodejs.md).</span></span>

### <a name="update-your-azure-cli-version-too090-or-later"></a><span data-ttu-id="afe1d-115">Mettre à jour votre too0.9.0 de version CLI d’Azure ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="afe1d-115">Update your Azure CLI version too0.9.0 or later</span></span>
<span data-ttu-id="afe1d-116">Type `azure --version` toosee si vous avez déjà installé la version 0.9.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="afe1d-116">Type `azure --version` toosee whether you have already installed version 0.9.0 or later.</span></span>

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

<span data-ttu-id="afe1d-117">Si votre version n’est pas 0.9.0 ou version ultérieure, vous devez tooupdate en utilisant l’une des hello des programmes d’installation de natives ou via **npm** en tapant `npm update -g azure-cli`.</span><span class="sxs-lookup"><span data-stu-id="afe1d-117">If your version is not 0.9.0 or later, you need tooupdate it by using one of hello native installers or through **npm** by typing `npm update -g azure-cli`.</span></span>

<span data-ttu-id="afe1d-118">Vous pouvez également exécuter CLI d’Azure comme un conteneur Docker en utilisant hello [image Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span><span class="sxs-lookup"><span data-stu-id="afe1d-118">You can also run Azure CLI as a Docker container by using hello following [Docker image](https://registry.hub.docker.com/u/microsoft/azure-cli/).</span></span> <span data-ttu-id="afe1d-119">À partir d’un hôte Docker, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="afe1d-119">From a Docker host, run hello following command:</span></span>

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="afe1d-120">Configurer votre compte et votre abonnement Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="afe1d-120">Set your Azure account and subscription</span></span>
<span data-ttu-id="afe1d-121">Si vous ne possédez pas déjà un abonnement Azure, mais que vous avez un abonnement MSDN, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="afe1d-121">If you don't already have an Azure subscription but you do have an MSDN subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="afe1d-122">Ou vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="afe1d-122">Or you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="afe1d-123">Maintenant [connecter tooyour compte Azure interactivement](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) en tapant `azure login` puis suivez les instructions de hello pour une tooyour d’expérience de connexion interactive compte Azure.</span><span class="sxs-lookup"><span data-stu-id="afe1d-123">Now [log in tooyour Azure account interactively](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) by typing `azure login` and following hello prompts for an interactive login experience tooyour Azure account.</span></span> 

> [!NOTE]
> <span data-ttu-id="afe1d-124">Si vous avez un travail ou d’établissement scolaire ID et que vous savez que vous n’avez pas l’authentification à deux facteurs est activée, vous pouvez **également** utiliser `azure login -u` avec hello Professionnel ou scolaire toolog ID dans *sans* une session interactive.</span><span class="sxs-lookup"><span data-stu-id="afe1d-124">If you have a work or school ID and you know you do not have two-factor authentication enabled, you can **also** use `azure login -u` along with hello work or school ID toolog in *without* an interactive session.</span></span> <span data-ttu-id="afe1d-125">Si vous ne disposez d’un travail ou scolaire ID, vous pouvez [créer un id Professionnel ou scolaire à partir de votre compte Microsoft personnel](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog Bonjour identique.</span><span class="sxs-lookup"><span data-stu-id="afe1d-125">If you don't have a work or school ID, you can [create a work or school id from your personal Microsoft account](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog in hello same way.</span></span>
>
>

<span data-ttu-id="afe1d-126">Votre compte peut avoir plusieurs abonnements.</span><span class="sxs-lookup"><span data-stu-id="afe1d-126">Your account may have more than one subscription.</span></span> <span data-ttu-id="afe1d-127">Vous pouvez répertorier vos abonnements en tapant `azure account list`, ce qui pourrait donner ceci :</span><span class="sxs-lookup"><span data-stu-id="afe1d-127">You can list your subscriptions by typing `azure account list`, which might look something like this:</span></span>

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

<span data-ttu-id="afe1d-128">Vous pouvez définir l’abonnement Azure hello en tapant hello suivante.</span><span class="sxs-lookup"><span data-stu-id="afe1d-128">You can set hello current Azure subscription by typing hello following.</span></span> <span data-ttu-id="afe1d-129">Utilisez hello hello nom ou l’ID d’abonnement qui a des ressources hello toomanage.</span><span class="sxs-lookup"><span data-stu-id="afe1d-129">Use hello subscription name or hello ID that has hello resources you want toomanage.</span></span>

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a><span data-ttu-id="afe1d-130">Basculer le mode de groupe de ressources toohello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="afe1d-130">Switch toohello Azure CLI resource group mode</span></span>
<span data-ttu-id="afe1d-131">Par défaut, hello CLI d’Azure démarre en mode de gestion de service hello (**asm** mode).</span><span class="sxs-lookup"><span data-stu-id="afe1d-131">By default, hello Azure CLI starts in hello service management mode (**asm** mode).</span></span> <span data-ttu-id="afe1d-132">Tapez hello suivant le mode de groupe tooswitch tooresource.</span><span class="sxs-lookup"><span data-stu-id="afe1d-132">Type hello following tooswitch tooresource group mode.</span></span>

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a><span data-ttu-id="afe1d-133">Présentation des groupes et des modèles de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="afe1d-133">Understanding Azure resource templates and resource groups</span></span>
<span data-ttu-id="afe1d-134">La plupart des applications sont basées sur une combinaison de différents types de ressources (au moins une machine virtuelle et un compte de stockage, une base de données SQL, un réseau virtuel ou un réseau de distribution de contenu).</span><span class="sxs-lookup"><span data-stu-id="afe1d-134">Most applications are built from a combination of different resource types (such as one or more VMs and storage accounts, a SQL database, a virtual network, or a content delivery network).</span></span> <span data-ttu-id="afe1d-135">Hello API de gestion des services Azure par défaut et hello portail Azure classic représenté ces éléments à l’aide d’une approche de service par service.</span><span class="sxs-lookup"><span data-stu-id="afe1d-135">hello default Azure service management API and hello Azure classic portal represented these items by using a service-by-service approach.</span></span> <span data-ttu-id="afe1d-136">Cette approche requiert que vous toodeploy et gérer des services individuels hello individuellement (ou rechercher d’autres outils de le faire) et non comme une unité logique de déploiement.</span><span class="sxs-lookup"><span data-stu-id="afe1d-136">This approach requires you toodeploy and manage hello individual services individually (or find other tools that do so), and not as a single logical unit of deployment.</span></span>

<span data-ttu-id="afe1d-137">*Les modèles de gestionnaire de ressources Azure*, toutefois, permettent à vous toodeploy et gérer ces différentes ressources comme une unité logique de déploiement de manière déclarative.</span><span class="sxs-lookup"><span data-stu-id="afe1d-137">*Azure Resource Manager templates*, however, make it possible for you toodeploy and manage these different resources as one logical deployment unit in a declarative fashion.</span></span> <span data-ttu-id="afe1d-138">Au lieu de manière impérative informe Azure toodeploy une commande après l’autre, vous décrivez tout votre déploiement dans un fichier JSON--toutes les ressources de hello et de configuration et les paramètres de déploiement et indiquer à Azure toodeploy ces ressources comme une groupe.</span><span class="sxs-lookup"><span data-stu-id="afe1d-138">Instead of imperatively telling Azure what toodeploy one command after another, you describe your entire deployment in a JSON file -- all of hello resources and associated configuration and deployment parameters -- and tell Azure toodeploy those resources as one group.</span></span>

<span data-ttu-id="afe1d-139">Vous pouvez ensuite gérer hello cycle de vie global des ressources du groupe hello à l’aide des commandes de gestion de ressources CLI d’Azure pour :</span><span class="sxs-lookup"><span data-stu-id="afe1d-139">You can then manage hello overall life cycle of hello group's resources by using Azure CLI resource management commands to:</span></span>

* <span data-ttu-id="afe1d-140">Arrêter, démarrer ou supprimer toutes les ressources hello au sein du groupe de hello à la fois.</span><span class="sxs-lookup"><span data-stu-id="afe1d-140">Stop, start, or delete all of hello resources within hello group at once.</span></span>
* <span data-ttu-id="afe1d-141">Appliquer toolock de règles de contrôle d’accès en fonction du rôle (RBAC) vers le bas des autorisations de sécurité sur ces derniers.</span><span class="sxs-lookup"><span data-stu-id="afe1d-141">Apply Role-Based Access Control (RBAC) rules toolock down security permissions on them.</span></span>
* <span data-ttu-id="afe1d-142">mener des opérations d’audit ;</span><span class="sxs-lookup"><span data-stu-id="afe1d-142">Audit operations.</span></span>
* <span data-ttu-id="afe1d-143">baliser des ressources avec des métadonnées supplémentaires pour améliorer leur suivi.</span><span class="sxs-lookup"><span data-stu-id="afe1d-143">Tag resources with additional metadata for better tracking.</span></span>

<span data-ttu-id="afe1d-144">Vous pouvez apprendre beaucoup plus d’informations sur les groupes de ressources Azure et à quoi ils peuvent vous Bonjour [vue d’ensemble du Gestionnaire de ressources Azure](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="afe1d-144">You can learn lots more about Azure resource groups and what they can do for you in hello [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="afe1d-145">Si vous êtes intéressé par la création de modèles, consultez [Création de modèles Azure Resource Manager](../articles/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="afe1d-145">If you're interested in authoring templates, see [Authoring Azure Resource Manager templates](../articles/resource-group-authoring-templates.md).</span></span>

## <span data-ttu-id="afe1d-146"><a id="quick-create-a-vm-in-azure"></a>Tâche : Créer rapidement une machine virtuelle dans Azure</span><span class="sxs-lookup"><span data-stu-id="afe1d-146"><a id="quick-create-a-vm-in-azure"></a>Task: Quick-create a VM in Azure</span></span>
<span data-ttu-id="afe1d-147">Parfois, vous savez quelle image que vous avez besoin, et vous avez besoin maintenant une machine virtuelle à partir de cette image et vous ne vous souciez trop infrastructure de hello--peut-être tootest quelque chose sur une machine virtuelle propre.</span><span class="sxs-lookup"><span data-stu-id="afe1d-147">Sometimes you know what image you need, and you need a VM from that image right now and you don't care too much about hello infrastructure -- maybe you have tootest something on a clean VM.</span></span> <span data-ttu-id="afe1d-148">C’est lorsque vous souhaitez toouse hello `azure vm quick-create` de commandes et passer toocreate nécessaire des arguments de hello une machine virtuelle et son infrastructure.</span><span class="sxs-lookup"><span data-stu-id="afe1d-148">That's when you want toouse hello `azure vm quick-create` command, and pass hello arguments necessary toocreate a VM and its infrastructure.</span></span>

<span data-ttu-id="afe1d-149">Commencez par créer votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="afe1d-149">First, create your resource group.</span></span>

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="afe1d-150">Ensuite, vous aurez besoin d’une image.</span><span class="sxs-lookup"><span data-stu-id="afe1d-150">Second, you'll need an image.</span></span> <span data-ttu-id="afe1d-151">toofind une image avec hello CLI d’Azure, consultez [Navigating et sélectionner des images de machine virtuelle Azure avec PowerShell et hello CLI d’Azure](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afe1d-151">toofind an image with hello Azure CLI, see [Navigating and selecting Azure virtual machine images with PowerShell and hello Azure CLI](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="afe1d-152">Mais pour cet article, voici une brève liste d’images populaires.</span><span class="sxs-lookup"><span data-stu-id="afe1d-152">But for this article, here's a short list of popular images.</span></span> <span data-ttu-id="afe1d-153">Nous allons utiliser l’image Stable de CoreOS pour cette création rapide.</span><span class="sxs-lookup"><span data-stu-id="afe1d-153">We'll use CoreOS's Stable image for this quick-create.</span></span>

> [!NOTE]
> <span data-ttu-id="afe1d-154">Pour ComputeImageVersion, vous pouvez également simplement fournir « dernier » comme hello paramètre dans les deux langage de modèle hello et Bonjour CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="afe1d-154">For ComputeImageVersion, you can also simply supply 'latest' as hello parameter in both hello template language and in hello Azure CLI.</span></span> <span data-ttu-id="afe1d-155">Ainsi, que vous tooalways utiliser hello dernière modification version et d’image de hello sans avoir toomodify vos scripts ou les modèles.</span><span class="sxs-lookup"><span data-stu-id="afe1d-155">This will allow you tooalways use hello latest and patched version of hello image without having toomodify your scripts or templates.</span></span> <span data-ttu-id="afe1d-156">Consultez l’illustration ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="afe1d-156">This is shown below.</span></span>
>
>

| <span data-ttu-id="afe1d-157">PublisherName</span><span class="sxs-lookup"><span data-stu-id="afe1d-157">PublisherName</span></span> | <span data-ttu-id="afe1d-158">Offer</span><span class="sxs-lookup"><span data-stu-id="afe1d-158">Offer</span></span> | <span data-ttu-id="afe1d-159">Sku</span><span class="sxs-lookup"><span data-stu-id="afe1d-159">Sku</span></span> | <span data-ttu-id="afe1d-160">Version</span><span class="sxs-lookup"><span data-stu-id="afe1d-160">Version</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="afe1d-161">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="afe1d-161">OpenLogic</span></span> |<span data-ttu-id="afe1d-162">CentOS</span><span class="sxs-lookup"><span data-stu-id="afe1d-162">CentOS</span></span> |<span data-ttu-id="afe1d-163">7</span><span class="sxs-lookup"><span data-stu-id="afe1d-163">7</span></span> |<span data-ttu-id="afe1d-164">7.0.201503</span><span class="sxs-lookup"><span data-stu-id="afe1d-164">7.0.201503</span></span> |
| <span data-ttu-id="afe1d-165">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="afe1d-165">OpenLogic</span></span> |<span data-ttu-id="afe1d-166">CentOS</span><span class="sxs-lookup"><span data-stu-id="afe1d-166">CentOS</span></span> |<span data-ttu-id="afe1d-167">7.1</span><span class="sxs-lookup"><span data-stu-id="afe1d-167">7.1</span></span> |<span data-ttu-id="afe1d-168">7.1.201504</span><span class="sxs-lookup"><span data-stu-id="afe1d-168">7.1.201504</span></span> |
| <span data-ttu-id="afe1d-169">CoreOS</span><span class="sxs-lookup"><span data-stu-id="afe1d-169">CoreOS</span></span> |<span data-ttu-id="afe1d-170">CoreOS</span><span class="sxs-lookup"><span data-stu-id="afe1d-170">CoreOS</span></span> |<span data-ttu-id="afe1d-171">Bêta</span><span class="sxs-lookup"><span data-stu-id="afe1d-171">Beta</span></span> |<span data-ttu-id="afe1d-172">647.0.0</span><span class="sxs-lookup"><span data-stu-id="afe1d-172">647.0.0</span></span> |
| <span data-ttu-id="afe1d-173">CoreOS</span><span class="sxs-lookup"><span data-stu-id="afe1d-173">CoreOS</span></span> |<span data-ttu-id="afe1d-174">CoreOS</span><span class="sxs-lookup"><span data-stu-id="afe1d-174">CoreOS</span></span> |<span data-ttu-id="afe1d-175">Stable</span><span class="sxs-lookup"><span data-stu-id="afe1d-175">Stable</span></span> |<span data-ttu-id="afe1d-176">633.1.0</span><span class="sxs-lookup"><span data-stu-id="afe1d-176">633.1.0</span></span> |
| <span data-ttu-id="afe1d-177">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="afe1d-177">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="afe1d-178">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="afe1d-178">DynamicsNAV</span></span> |<span data-ttu-id="afe1d-179">2015</span><span class="sxs-lookup"><span data-stu-id="afe1d-179">2015</span></span> |<span data-ttu-id="afe1d-180">8.0.40459</span><span class="sxs-lookup"><span data-stu-id="afe1d-180">8.0.40459</span></span> |
| <span data-ttu-id="afe1d-181">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="afe1d-181">MicrosoftSharePoint</span></span> |<span data-ttu-id="afe1d-182">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-182">MicrosoftSharePointServer</span></span> |<span data-ttu-id="afe1d-183">2013</span><span class="sxs-lookup"><span data-stu-id="afe1d-183">2013</span></span> |<span data-ttu-id="afe1d-184">1.0.0</span><span class="sxs-lookup"><span data-stu-id="afe1d-184">1.0.0</span></span> |
| <span data-ttu-id="afe1d-185">msopentech</span><span class="sxs-lookup"><span data-stu-id="afe1d-185">msopentech</span></span> |<span data-ttu-id="afe1d-186">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="afe1d-186">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="afe1d-187">Standard</span><span class="sxs-lookup"><span data-stu-id="afe1d-187">Standard</span></span> |<span data-ttu-id="afe1d-188">1.0.0</span><span class="sxs-lookup"><span data-stu-id="afe1d-188">1.0.0</span></span> |
| <span data-ttu-id="afe1d-189">msopentech</span><span class="sxs-lookup"><span data-stu-id="afe1d-189">msopentech</span></span> |<span data-ttu-id="afe1d-190">Oracle-Database-12c-Weblogic-Server-12c</span><span class="sxs-lookup"><span data-stu-id="afe1d-190">Oracle-Database-12c-Weblogic-Server-12c</span></span> |<span data-ttu-id="afe1d-191">Entreprise</span><span class="sxs-lookup"><span data-stu-id="afe1d-191">Enterprise</span></span> |<span data-ttu-id="afe1d-192">1.0.0</span><span class="sxs-lookup"><span data-stu-id="afe1d-192">1.0.0</span></span> |
| <span data-ttu-id="afe1d-193">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-193">MicrosoftSQLServer</span></span> |<span data-ttu-id="afe1d-194">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="afe1d-194">SQL2014-WS2012R2</span></span> |<span data-ttu-id="afe1d-195">Entreprise, optimisé pour l’entrepôt de données</span><span class="sxs-lookup"><span data-stu-id="afe1d-195">Enterprise-Optimized-for-DW</span></span> |<span data-ttu-id="afe1d-196">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="afe1d-196">12.0.2430</span></span> |
| <span data-ttu-id="afe1d-197">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-197">MicrosoftSQLServer</span></span> |<span data-ttu-id="afe1d-198">SQL2014-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="afe1d-198">SQL2014-WS2012R2</span></span> |<span data-ttu-id="afe1d-199">Entreprise, optimisé pour le traitement transactionnel en ligne</span><span class="sxs-lookup"><span data-stu-id="afe1d-199">Enterprise-Optimized-for-OLTP</span></span> |<span data-ttu-id="afe1d-200">12.0.2430</span><span class="sxs-lookup"><span data-stu-id="afe1d-200">12.0.2430</span></span> |
| <span data-ttu-id="afe1d-201">Canonical</span><span class="sxs-lookup"><span data-stu-id="afe1d-201">Canonical</span></span> |<span data-ttu-id="afe1d-202">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-202">UbuntuServer</span></span> |<span data-ttu-id="afe1d-203">12.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="afe1d-203">12.04.5-LTS</span></span> |<span data-ttu-id="afe1d-204">12.04.201504230</span><span class="sxs-lookup"><span data-stu-id="afe1d-204">12.04.201504230</span></span> |
| <span data-ttu-id="afe1d-205">Canonical</span><span class="sxs-lookup"><span data-stu-id="afe1d-205">Canonical</span></span> |<span data-ttu-id="afe1d-206">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-206">UbuntuServer</span></span> |<span data-ttu-id="afe1d-207">14.04.2-LTS</span><span class="sxs-lookup"><span data-stu-id="afe1d-207">14.04.2-LTS</span></span> |<span data-ttu-id="afe1d-208">14.04.201503090</span><span class="sxs-lookup"><span data-stu-id="afe1d-208">14.04.201503090</span></span> |
| <span data-ttu-id="afe1d-209">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-209">MicrosoftWindowsServer</span></span> |<span data-ttu-id="afe1d-210">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-210">WindowsServer</span></span> |<span data-ttu-id="afe1d-211">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="afe1d-211">2012-Datacenter</span></span> |<span data-ttu-id="afe1d-212">3.0.201503</span><span class="sxs-lookup"><span data-stu-id="afe1d-212">3.0.201503</span></span> |
| <span data-ttu-id="afe1d-213">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-213">MicrosoftWindowsServer</span></span> |<span data-ttu-id="afe1d-214">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-214">WindowsServer</span></span> |<span data-ttu-id="afe1d-215">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="afe1d-215">2012-R2-Datacenter</span></span> |<span data-ttu-id="afe1d-216">4.0.201503</span><span class="sxs-lookup"><span data-stu-id="afe1d-216">4.0.201503</span></span> |
| <span data-ttu-id="afe1d-217">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-217">MicrosoftWindowsServer</span></span> |<span data-ttu-id="afe1d-218">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="afe1d-218">WindowsServer</span></span> |<span data-ttu-id="afe1d-219">Windows Server Technical Preview</span><span class="sxs-lookup"><span data-stu-id="afe1d-219">Windows-Server-Technical-Preview</span></span> |<span data-ttu-id="afe1d-220">5.0.201504</span><span class="sxs-lookup"><span data-stu-id="afe1d-220">5.0.201504</span></span> |
| <span data-ttu-id="afe1d-221">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="afe1d-221">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="afe1d-222">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="afe1d-222">WindowsServerEssentials</span></span> |<span data-ttu-id="afe1d-223">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="afe1d-223">WindowsServerEssentials</span></span> |<span data-ttu-id="afe1d-224">1.0.141204</span><span class="sxs-lookup"><span data-stu-id="afe1d-224">1.0.141204</span></span> |
| <span data-ttu-id="afe1d-225">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="afe1d-225">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="afe1d-226">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="afe1d-226">WindowsServerHPCPack</span></span> |<span data-ttu-id="afe1d-227">2012R2</span><span class="sxs-lookup"><span data-stu-id="afe1d-227">2012R2</span></span> |<span data-ttu-id="afe1d-228">4.3.4665</span><span class="sxs-lookup"><span data-stu-id="afe1d-228">4.3.4665</span></span> |

<span data-ttu-id="afe1d-229">Créez simplement votre machine virtuelle en entrant hello `azure vm quick-create` commande et prêt pour hello invites.</span><span class="sxs-lookup"><span data-stu-id="afe1d-229">Just create your VM by entering hello `azure vm quick-create` command and being ready for hello prompts.</span></span> <span data-ttu-id="afe1d-230">Le résultat suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="afe1d-230">It should look something like this:</span></span>

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

<span data-ttu-id="afe1d-231">Et vous voici avec une nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="afe1d-231">And away you go with your new VM.</span></span>

## <span data-ttu-id="afe1d-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Tâche : Déployer une machine virtuelle dans Azure à partir d’un modèle</span><span class="sxs-lookup"><span data-stu-id="afe1d-232"><a id="deploy-a-vm-in-azure-from-a-template"></a>Task: Deploy a VM in Azure from a template</span></span>
<span data-ttu-id="afe1d-233">Utilisez les instructions de hello dans ces sections de toodeploy une machine virtuelle Azure à l’aide d’un modèle avec hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="afe1d-233">Use hello instructions in these sections toodeploy a new Azure VM by using a template with hello Azure CLI.</span></span> <span data-ttu-id="afe1d-234">Ce modèle crée un seul ordinateur virtuel dans un réseau virtuel avec un sous-réseau unique et, contrairement aux `azure vm quick-create`, permet de vous toodescribe précisément ce que vous voulez et répéter sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="afe1d-234">This template creates a single virtual machine in a new virtual network with a single subnet, and unlike `azure vm quick-create`, enables you toodescribe what you want precisely and repeat it without errors.</span></span> <span data-ttu-id="afe1d-235">Voici le résultat du modèle :</span><span class="sxs-lookup"><span data-stu-id="afe1d-235">Here's what this template creates:</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a><span data-ttu-id="afe1d-236">Étape 1 : Examiner le fichier JSON de hello des paramètres du modèle hello</span><span class="sxs-lookup"><span data-stu-id="afe1d-236">Step 1: Examine hello JSON file for hello template parameters</span></span>
<span data-ttu-id="afe1d-237">Voici le contenu de hello du fichier JSON de hello pour le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="afe1d-237">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="afe1d-238">(modèle de hello se trouve également dans [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="afe1d-238">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)</span></span>

<span data-ttu-id="afe1d-239">Les modèles sont flexibles, donc le concepteur hello peut avoir choisi toogive un grand nombre de paramètres ou choisi toooffer uniquement quelques en créant un modèle qui est plus fixe.</span><span class="sxs-lookup"><span data-stu-id="afe1d-239">Templates are flexible, so hello designer may have chosen toogive you lots of parameters or chosen toooffer only a few by creating a template that is more fixed.</span></span> <span data-ttu-id="afe1d-240">Dans l’ordre toocollect hello informations modèle hello de toopass en tant que paramètres, ouvrir le fichier de modèle hello (cette rubrique comprend un modèle inline, ci-dessous) et examiner hello **paramètres** valeurs.</span><span class="sxs-lookup"><span data-stu-id="afe1d-240">In order toocollect hello information you need toopass hello template as parameters, open hello template file (this topic has a template inline, below) and examine hello **parameters** values.</span></span>

<span data-ttu-id="afe1d-241">Dans ce cas, modèle hello ci-dessous vous demandera :</span><span class="sxs-lookup"><span data-stu-id="afe1d-241">In this case, hello template below will ask for:</span></span>

* <span data-ttu-id="afe1d-242">Un nom de compte de stockage unique.</span><span class="sxs-lookup"><span data-stu-id="afe1d-242">A unique storage account name.</span></span>
* <span data-ttu-id="afe1d-243">Un nom d’utilisateur admin hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="afe1d-243">An admin user name for hello VM.</span></span>
* <span data-ttu-id="afe1d-244">Un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="afe1d-244">A password.</span></span>
* <span data-ttu-id="afe1d-245">Un nom de domaine pour hello world toouse à l’extérieur.</span><span class="sxs-lookup"><span data-stu-id="afe1d-245">A domain name for hello outside world toouse.</span></span>
* <span data-ttu-id="afe1d-246">Un numéro de version Ubuntu Server, mais accepte uniquement l’un de ceux répertoriés dans une liste.</span><span class="sxs-lookup"><span data-stu-id="afe1d-246">An Ubuntu Server version number -- but it will accept only one of a list.</span></span>

<span data-ttu-id="afe1d-247">En savoir plus sur les [conditions requises pour les noms d’utilisateur et les mots de passe](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="afe1d-247">See more about [username and password requirements](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span>

<span data-ttu-id="afe1d-248">Une fois que vous décidez de ces valeurs, vous êtes prêt toocreate un groupe pour et déployez ce modèle dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="afe1d-248">Once you decide on these values, you're ready toocreate a group for and deploy this template into your Azure subscription.</span></span>

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="afe1d-249">Étape 2 : Créer un ordinateur virtuel de hello à l’aide du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="afe1d-249">Step 2: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="afe1d-250">Une fois que vous avez vos valeurs de paramètre prêt, vous devez créer un groupe de ressources pour votre déploiement de modèle et ensuite déployer le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="afe1d-250">Once you have your parameter values ready, you must create a resource group for your template deployment and then deploy hello template.</span></span>

<span data-ttu-id="afe1d-251">groupe de ressources toocreate hello, type `azure group create <group name> <location>` par nom de hello du groupe hello et l’emplacement de centre de données hello dans lequel vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="afe1d-251">toocreate hello resource group, type `azure group create <group name> <location>` with hello name of hello group you want and hello datacenter location into which you want toodeploy.</span></span> <span data-ttu-id="afe1d-252">Le processus est rapide :</span><span class="sxs-lookup"><span data-stu-id="afe1d-252">This happens quickly:</span></span>

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="afe1d-253">Déploiement de hello toocreate maintenant, appelez `azure group deployment create` et passer :</span><span class="sxs-lookup"><span data-stu-id="afe1d-253">Now toocreate hello deployment, call `azure group deployment create` and pass:</span></span>

* <span data-ttu-id="afe1d-254">fichier de modèle Hello (si vous avez enregistré hello au-dessus de fichier local tooa de modèle JSON).</span><span class="sxs-lookup"><span data-stu-id="afe1d-254">hello template file (if you saved hello above JSON template tooa local file).</span></span>
* <span data-ttu-id="afe1d-255">Un modèle URI (si vous voulez toopoint au fichier hello dans GitHub ou une autre adresse web).</span><span class="sxs-lookup"><span data-stu-id="afe1d-255">A template URI (if you want toopoint at hello file in GitHub or some other web address).</span></span>
* <span data-ttu-id="afe1d-256">groupe de ressources Hello dans lequel vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="afe1d-256">hello resource group into which you want toodeploy.</span></span>
* <span data-ttu-id="afe1d-257">Un nom pour le déploiement (facultatif).</span><span class="sxs-lookup"><span data-stu-id="afe1d-257">An optional deployment name.</span></span>

<span data-ttu-id="afe1d-258">Vous seront demandées toosupply hello de paramètres dans la section « Paramètres » de hello du fichier JSON de hello.</span><span class="sxs-lookup"><span data-stu-id="afe1d-258">You will be prompted toosupply hello values of parameters in hello "parameters" section of hello JSON file.</span></span> <span data-ttu-id="afe1d-259">Lorsque vous avez spécifié toutes les valeurs de paramètre hello, votre déploiement commence.</span><span class="sxs-lookup"><span data-stu-id="afe1d-259">When you have specified all hello parameter values, your deployment will begin.</span></span>

<span data-ttu-id="afe1d-260">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="afe1d-260">Here is an example:</span></span>

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

<span data-ttu-id="afe1d-261">Vous recevrez hello suivant le type d’informations :</span><span class="sxs-lookup"><span data-stu-id="afe1d-261">You will receive hello following type of information:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <span data-ttu-id="afe1d-262"><a id="create-a-custom-vm-image"></a>Tâche : Créer une image de machine virtuelle personnalisée</span><span class="sxs-lookup"><span data-stu-id="afe1d-262"><a id="create-a-custom-vm-image"></a>Task: Create a custom VM image</span></span>
<span data-ttu-id="afe1d-263">Vous avez déjà vu l’utilisation de base hello de modèles ci-dessus, par conséquent, nous pouvons maintenant utiliser similaire instructions toocreate une machine virtuelle personnalisée à partir d’un fichier .vhd spécifique dans Azure à l’aide d’un modèle via hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="afe1d-263">You've seen hello basic usage of templates above, so now we can use similar instructions toocreate a custom VM from a specific .vhd file in Azure by using a template via hello Azure CLI.</span></span> <span data-ttu-id="afe1d-264">Hello différence est que ce modèle crée un seul ordinateur virtuel à partir d’un disque dur virtuel (VHD) spécifié.</span><span class="sxs-lookup"><span data-stu-id="afe1d-264">hello difference here is that this template creates a single virtual machine from a specified virtual hard disk (VHD).</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="afe1d-265">Étape 1 : Examiner le fichier JSON de hello pour le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="afe1d-265">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="afe1d-266">Voici le contenu hello du fichier JSON hello modèle hello cette section utilise comme exemple.</span><span class="sxs-lookup"><span data-stu-id="afe1d-266">Here are hello contents of hello JSON file for hello template that this section uses as an example.</span></span> <span data-ttu-id="afe1d-267">(modèle de hello se trouve également dans [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span><span class="sxs-lookup"><span data-stu-id="afe1d-267">(hello template is also located in [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)</span></span>

<span data-ttu-id="afe1d-268">Là encore, vous devez toofind hello valeurs tooenter pour les paramètres hello qui n’ont pas de valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="afe1d-268">Again, you will need toofind hello values you want tooenter for hello parameters that do not have default values.</span></span> <span data-ttu-id="afe1d-269">Lorsque vous exécutez hello `azure group deployment create` hello CLI d’Azure vous invite à vous tooenter ces valeurs de la commande.</span><span class="sxs-lookup"><span data-stu-id="afe1d-269">When you run hello `azure group deployment create` command, hello Azure CLI will prompt you tooenter those values.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a><span data-ttu-id="afe1d-270">Étape 2 : Obtenir hello disque dur virtuel</span><span class="sxs-lookup"><span data-stu-id="afe1d-270">Step 2: Obtain hello VHD</span></span>
<span data-ttu-id="afe1d-271">Évidemment, vous aurez besoin d’un fichier .vhd pour cela.</span><span class="sxs-lookup"><span data-stu-id="afe1d-271">Obviously, you'll need a .vhd for this.</span></span> <span data-ttu-id="afe1d-272">Vous pouvez utiliser un fichier dont vous disposez dans Azure ou en télécharger un.</span><span class="sxs-lookup"><span data-stu-id="afe1d-272">You can use one you already have in Azure, or you can upload one.</span></span>

<span data-ttu-id="afe1d-273">Pour un ordinateur virtuel basé sur Windows, consultez [création et téléchargement d’un disque dur virtuel de Windows Server de tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afe1d-273">For a Windows-based virtual machine, see [Create and upload a Windows Server VHD tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="afe1d-274">Pour une machine virtuelle Linux, consultez [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afe1d-274">For a Linux-based virtual machine, see [Creating and uploading a virtual hard disk that contains hello Linux operating system](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a><span data-ttu-id="afe1d-275">Étape 3 : Créer un ordinateur virtuel de hello à l’aide du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="afe1d-275">Step 3: Create hello virtual machine by using hello template</span></span>
<span data-ttu-id="afe1d-276">Vous êtes maintenant prêt toocreate un nouvel ordinateur virtuel basé sur le disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="afe1d-276">Now you're ready toocreate a new virtual machine based on hello .vhd.</span></span> <span data-ttu-id="afe1d-277">Créer un toodeploy de groupe, à l’aide de `azure group create <location>`:</span><span class="sxs-lookup"><span data-stu-id="afe1d-277">Create a group toodeploy into, by using `azure group create <location>`:</span></span>

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="afe1d-278">Puis créez le déploiement de hello à l’aide de hello `--template-uri` toocall option dans le modèle hello directement (ou vous pouvez utiliser hello `--template-file` option toouse un fichier que vous avez enregistré localement).</span><span class="sxs-lookup"><span data-stu-id="afe1d-278">Then create hello deployment by using hello `--template-uri` option toocall in hello template directly (or you can use hello `--template-file` option toouse a file that you have saved locally).</span></span> <span data-ttu-id="afe1d-279">Notez que le modèle de hello ayant des valeurs par défaut spécifiées, vous êtes invité uniquement quelques points.</span><span class="sxs-lookup"><span data-stu-id="afe1d-279">Note that because hello template has defaults specified, you are prompted for only a few things.</span></span> <span data-ttu-id="afe1d-280">Si vous déployez le modèle hello dans des emplacements différents, vous découvrirez peut-être que certains conflits d’affectation de noms se produisent avec les valeurs par défaut hello (en particulier les nom DNS de hello sont crées).</span><span class="sxs-lookup"><span data-stu-id="afe1d-280">If you deploy hello template in different places, you may find that some naming collisions occur with hello default values (particularly hello DNS name you create).</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

<span data-ttu-id="afe1d-281">Sortie se présente comme hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="afe1d-281">Output looks something like hello following:</span></span>

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <span data-ttu-id="afe1d-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Tâche : Déployer une application de plusieurs machines virtuelles utilisant un réseau virtuel et un équilibreur de charge externe</span><span class="sxs-lookup"><span data-stu-id="afe1d-282"><a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Task: Deploy a multi-VM application that uses a virtual network and an external load balancer</span></span>
<span data-ttu-id="afe1d-283">Ce modèle vous permet de toocreate deux machines virtuelles sous un équilibreur de charge et configurer une règle d’équilibrage de charge sur le Port 80.</span><span class="sxs-lookup"><span data-stu-id="afe1d-283">This template allows you toocreate two virtual machines under a load balancer and configure a load-balancing rule on Port 80.</span></span> <span data-ttu-id="afe1d-284">Il déploie également un compte de stockage, un réseau virtuel, une adresse IP publique, un groupe à haute disponibilité et des interfaces réseau.</span><span class="sxs-lookup"><span data-stu-id="afe1d-284">This template also deploys a storage account, virtual network, public IP address, availability set, and network interfaces.</span></span>

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

<span data-ttu-id="afe1d-285">Suivez ces étapes de toodeploy une application multi-VM qui utilise un réseau virtuel et un équilibrage de charge à l’aide d’un modèle de gestionnaire de ressources dans le référentiel de modèle GitHub hello via les commandes Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afe1d-285">Follow these steps toodeploy a multi-VM application that uses a virtual network and a load balancer by using a Resource Manager template in hello GitHub template repository via Azure PowerShell commands.</span></span>

### <a name="step-1-examine-hello-json-file-for-hello-template"></a><span data-ttu-id="afe1d-286">Étape 1 : Examiner le fichier JSON de hello pour le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="afe1d-286">Step 1: Examine hello JSON file for hello template</span></span>
<span data-ttu-id="afe1d-287">Voici le contenu de hello du fichier JSON de hello pour le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="afe1d-287">Here are hello contents of hello JSON file for hello template.</span></span> <span data-ttu-id="afe1d-288">Si vous souhaitez que la version la plus récente hello, elle est située [au référentiel GitHub de hello pour les modèles](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="afe1d-288">If you want hello most recent version, it's located [at hello GitHub repository for templates](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json).</span></span> <span data-ttu-id="afe1d-289">Cette rubrique utilise hello `--template-uri` toocall de commutateur dans le modèle de hello, mais vous pouvez également utiliser hello `--template-file` toopass une version locale de basculer.</span><span class="sxs-lookup"><span data-stu-id="afe1d-289">This topic uses hello `--template-uri` switch toocall in hello template, but you can also use hello `--template-file` switch toopass a local version.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a><span data-ttu-id="afe1d-290">Étape 2 : Créer un déploiement de hello à l’aide du modèle de hello</span><span class="sxs-lookup"><span data-stu-id="afe1d-290">Step 2: Create hello deployment by using hello template</span></span>
<span data-ttu-id="afe1d-291">Créer un groupe de ressources pour le modèle de hello à l’aide de `azure group create <location>`.</span><span class="sxs-lookup"><span data-stu-id="afe1d-291">Create a resource group for hello template by using `azure group create <location>`.</span></span> <span data-ttu-id="afe1d-292">Ensuite, créez un déploiement dans ce groupe de ressources à l’aide de `azure group deployment create` et en passant le groupe de ressources hello, en passant un nom de déploiement et répondre aux invites de hello pour les paramètres dans le modèle hello qui n’avait pas de valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="afe1d-292">Then, create a deployment into that resource group by using `azure group deployment create` and passing hello resource group, passing a deployment name, and answering hello prompts for parameters in hello template that did not have default values.</span></span>

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

<span data-ttu-id="afe1d-293">À présent utiliser hello `azure group deployment create` commande et hello `--template-uri` modèle d’option toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="afe1d-293">Now use hello `azure group deployment create` command and hello `--template-uri` option toodeploy hello template.</span></span> <span data-ttu-id="afe1d-294">Préparez-vous à renseigner les invites relatives aux valeurs de paramètres, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="afe1d-294">Be ready with your parameter values when it prompts you, as shown below.</span></span>

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

<span data-ttu-id="afe1d-295">Notez que ce modèle déploie une image Windows Server ; toutefois, vous pouvez facilement la remplacer par n’importe quelle image Linux.</span><span class="sxs-lookup"><span data-stu-id="afe1d-295">Note that this template deploys a Windows Server image; however, it could easily be replaced by any Linux image.</span></span> <span data-ttu-id="afe1d-296">Vous souhaitez toocreate un cluster de Docker avec plusieurs gestionnaires essaim ?</span><span class="sxs-lookup"><span data-stu-id="afe1d-296">Want toocreate a Docker cluster with multiple swarm managers?</span></span> <span data-ttu-id="afe1d-297">[Vous pouvez le faire](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span><span class="sxs-lookup"><span data-stu-id="afe1d-297">[You can do it](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).</span></span>

## <span data-ttu-id="afe1d-298"><a id="remove-a-resource-group"></a>Tâche : Supprimer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="afe1d-298"><a id="remove-a-resource-group"></a>Task: Remove a resource group</span></span>
<span data-ttu-id="afe1d-299">N’oubliez pas que vous pouvez redéployer le groupe de ressources tooa, mais si vous avez terminé avec l’un, vous pouvez le supprimer à l’aide de `azure group delete <group name>`.</span><span class="sxs-lookup"><span data-stu-id="afe1d-299">Remember that you can redeploy tooa resource group, but if you are done with one, you can delete it by using `azure group delete <group name>`.</span></span>

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <span data-ttu-id="afe1d-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Tâche : Afficher le journal de hello pour un déploiement de groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="afe1d-300"><a id="show-the-log-for-a-resource-group-deployment"></a>Task: Show hello log for a resource group deployment</span></span>
<span data-ttu-id="afe1d-301">Cette tâche est courante lors de la création ou de l’utilisation de modèles.</span><span class="sxs-lookup"><span data-stu-id="afe1d-301">This one is common while you're creating or using templates.</span></span> <span data-ttu-id="afe1d-302">déploiement de hello Hello appel toodisplay journaux pour un groupe est `azure group log show <groupname>`, qui affiche un peu de qui est utiles pour comprendre pourquoi quelque chose s’est produite, ou n’a pas d’informations.</span><span class="sxs-lookup"><span data-stu-id="afe1d-302">hello call toodisplay hello deployment logs for a group is `azure group log show <groupname>`, which displays quite a bit of information that's useful for understanding why something happened -- or didn't.</span></span> <span data-ttu-id="afe1d-303">(Pour plus d’informations sur la résolution des problèmes de vos déploiements, mais aussi pour obtenir des informations supplémentaires sur les problèmes, consultez l’article [Résolution des erreurs courantes dans des déploiements Azure avec Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span><span class="sxs-lookup"><span data-stu-id="afe1d-303">(For more information on troubleshooting your deployments, as well as other information about issues, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)</span></span>

<span data-ttu-id="afe1d-304">échecs de tootarget spécifique, vous pouvez utiliser des outils tels que, par exemple, **jq** choses tooquery un peu plus précisément, tels que les échecs, vous devez toocorrect.</span><span class="sxs-lookup"><span data-stu-id="afe1d-304">tootarget specific failures, for example, you might use tools like **jq** tooquery things a bit more precisely, such as which individual failures you need toocorrect.</span></span> <span data-ttu-id="afe1d-305">Hello exemple suivant utilise **jq** tooparse ouvrir une session pour un déploiement **lbgroup**, qui recherchent des échecs.</span><span class="sxs-lookup"><span data-stu-id="afe1d-305">hello following example uses **jq** tooparse a deployment log for **lbgroup**, looking for failures.</span></span>

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
<span data-ttu-id="afe1d-306">Vous pouvez découvrir très rapidement ce qui pose problème, le corriger et recommencer.</span><span class="sxs-lookup"><span data-stu-id="afe1d-306">You can discover very quickly what went wrong, fix, and retry.</span></span> <span data-ttu-id="afe1d-307">Bonjour suivant le cas, le modèle de hello avait été création deux machines virtuelles au hello même temps, ce qui a créé un verrou sur le disque dur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="afe1d-307">In hello following case, hello template had been creating two VMs at hello same time, which created a lock on hello .vhd.</span></span> <span data-ttu-id="afe1d-308">(Une fois que nous avons modifié le modèle de hello, hello déploiement réussi rapidement.)</span><span class="sxs-lookup"><span data-stu-id="afe1d-308">(After we modified hello template, hello deployment succeeded quickly.)</span></span>

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <span data-ttu-id="afe1d-309"><a id="display-information-about-a-virtual-machine"></a>Tâche : Afficher les informations relatives à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="afe1d-309"><a id="display-information-about-a-virtual-machine"></a>Task: Display information about a virtual machine</span></span>
<span data-ttu-id="afe1d-310">Vous pouvez voir des informations sur les machines virtuelles spécifiques dans votre groupe de ressources à l’aide de hello `azure vm show <groupname> <vmname>` commande.</span><span class="sxs-lookup"><span data-stu-id="afe1d-310">You can see information about specific VMs in your resource group by using hello `azure vm show <groupname> <vmname>` command.</span></span> <span data-ttu-id="afe1d-311">Si vous avez plusieurs machines virtuelles dans votre groupe, vous devrez peut-être tout d’abord hello toolist machines virtuelles dans un groupe à l’aide de `azure vm list <groupname>`.</span><span class="sxs-lookup"><span data-stu-id="afe1d-311">If you have more than one VM in your group, you might first need toolist hello VMs in a group by using `azure vm list <groupname>`.</span></span>

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

<span data-ttu-id="afe1d-312">Ensuite, recherchez myVM1 :</span><span class="sxs-lookup"><span data-stu-id="afe1d-312">And then, looking up myVM1:</span></span>

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> <span data-ttu-id="afe1d-313">Si vous voulez tooprogrammatically magasin manipuler la sortie hello de vos commandes de la console, vous souhaiterez toouse une analyse de JSON outil tel que  **[jq](https://github.com/stedolan/jq)**  ou  **[jsawk](https://github.com/micha/jsawk)** , ou les bibliothèques de langue qui sont bons pour la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="afe1d-313">If you want tooprogrammatically store and manipulate hello output of your console commands, you may want toouse a JSON parsing tool such as **[jq](https://github.com/stedolan/jq)** or **[jsawk](https://github.com/micha/jsawk)**, or language libraries that are good for hello task.</span></span>
>
>

## <span data-ttu-id="afe1d-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Tâche : Ouvrez une session sur l’ordinateur virtuel de basés sur Linux tooa</span><span class="sxs-lookup"><span data-stu-id="afe1d-314"><a id="log-on-to-a-linux-based-virtual-machine"></a>Task: Log on tooa Linux-based virtual machine</span></span>
<span data-ttu-id="afe1d-315">En règle générale, les ordinateurs Linux sont connecté toothrough SSH.</span><span class="sxs-lookup"><span data-stu-id="afe1d-315">Typically Linux machines are connected toothrough SSH.</span></span> <span data-ttu-id="afe1d-316">Pour plus d’informations, consultez [comment toouse SSH avec Linux sur Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afe1d-316">For more information, see [How toouse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <span data-ttu-id="afe1d-317"><a id="stop-a-virtual-machine"></a>Tâche : Arrêter une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="afe1d-317"><a id="stop-a-virtual-machine"></a>Task: Stop a VM</span></span>
<span data-ttu-id="afe1d-318">Exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="afe1d-318">Run this command:</span></span>

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> <span data-ttu-id="afe1d-319">Utilisez ce paramètre tookeep hello adresse IP virtuelle (VIP) du réseau virtuel de hello en cas de hello dernier ordinateur virtuel dans ce réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="afe1d-319">Use this parameter tookeep hello virtual IP (VIP) of hello vnet in case it's hello last VM in that vnet.</span></span> <br><br> <span data-ttu-id="afe1d-320">Si vous utilisez hello `StayProvisioned` paramètre, vous serez toujours facturé pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="afe1d-320">If you use hello `StayProvisioned` parameter, you'll still be billed for hello VM.</span></span>
>
>

## <span data-ttu-id="afe1d-321"><a id="start-a-virtual-machine"></a>Tâche : Démarrer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="afe1d-321"><a id="start-a-virtual-machine"></a>Task: Start a VM</span></span>
<span data-ttu-id="afe1d-322">Exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="afe1d-322">Run this command:</span></span>

```azurecli
azure vm start <group name> <virtual machine name>
```

## <span data-ttu-id="afe1d-323"><a id="attach-a-data-disk"></a>Tâche : Associer un disque de données</span><span class="sxs-lookup"><span data-stu-id="afe1d-323"><a id="attach-a-data-disk"></a>Task: Attach a data disk</span></span>
<span data-ttu-id="afe1d-324">Vous devez également toodecide si tooattach un nouveau disque ou un qui contient des données.</span><span class="sxs-lookup"><span data-stu-id="afe1d-324">You'll also need toodecide whether tooattach a new disk or one that contains data.</span></span> <span data-ttu-id="afe1d-325">Pour un nouveau disque, commande hello crée le fichier .vhd de hello et l’attache Bonjour même commande.</span><span class="sxs-lookup"><span data-stu-id="afe1d-325">For a new disk, hello command creates hello .vhd file and attaches it in hello same command.</span></span>

<span data-ttu-id="afe1d-326">tooattach un nouveau disque, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="afe1d-326">tooattach a new disk, run this command:</span></span>

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

<span data-ttu-id="afe1d-327">tooattach un disque de données existant, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="afe1d-327">tooattach an existing data disk, run this command:</span></span>

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

<span data-ttu-id="afe1d-328">Vous devez le disque toomount hello, comme vous le feriez normalement dans Linux.</span><span class="sxs-lookup"><span data-stu-id="afe1d-328">Then you'll need toomount hello disk, as you normally would in Linux.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afe1d-329">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="afe1d-329">Next steps</span></span>
<span data-ttu-id="afe1d-330">Pour plus d’exemples d’utilisation de CLI d’Azure avec hello **arm** mode, consultez [Using hello CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="afe1d-330">For far more examples of Azure CLI usage with hello **arm** mode, see [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md).</span></span> <span data-ttu-id="afe1d-331">toolearn en savoir plus sur les ressources Azure et les concepts associés, consultez [vue d’ensemble du Gestionnaire de ressources Azure](../articles/azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="afe1d-331">toolearn more about Azure resources and their concepts, see [Azure Resource Manager overview](../articles/azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="afe1d-332">Pour plus d’informations sur les autres modèles utilisables, consultez les articles [Modèles de démarrage rapide Microsoft Azure](https://azure.microsoft.com/documentation/templates/) et [Infrastructures d’application utilisant des modèles](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afe1d-332">For more templates you can use, see [Azure Quickstart templates](https://azure.microsoft.com/documentation/templates/) and [Application frameworks using templates](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
