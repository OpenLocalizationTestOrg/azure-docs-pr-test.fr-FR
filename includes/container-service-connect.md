# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="3956e-101">Création d’un cluster de Kubernetes, contrôleur de domaine/système d’exploitation ou Docker Swarm de tooa connexion à distance</span><span class="sxs-lookup"><span data-stu-id="3956e-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="3956e-102">Après avoir créé un cluster du Service de conteneur Azure, vous devez tooconnect toohello cluster toodeploy et gérez des charges de travail.</span><span class="sxs-lookup"><span data-stu-id="3956e-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="3956e-103">Cet article décrit comment tooconnect toohello master VM de hello de cluster à partir d’un ordinateur distant.</span><span class="sxs-lookup"><span data-stu-id="3956e-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="3956e-104">les clusters Kubernetes, contrôleur de domaine/système d’exploitation et Docker Swarm Hello fournissent des points de terminaison HTTP localement.</span><span class="sxs-lookup"><span data-stu-id="3956e-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="3956e-105">Kubernetes, ce point de terminaison est en toute sécurité exposée sur hello internet, et vous pouvez y accéder en exécutant hello `kubectl` outil de ligne de commande à partir de n’importe quel ordinateur connecté à internet.</span><span class="sxs-lookup"><span data-stu-id="3956e-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="3956e-106">Pour le contrôleur de domaine/système d’exploitation et Docker Swarm, nous vous recommandons de créer un tunnel SSH (secure shell) à partir de votre système de gestion de cluster toohello ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="3956e-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="3956e-107">Une fois hello tunnel établi, vous pouvez exécuter des commandes qui utilisent des points de terminaison HTTP hello et interface d’orchestrator vue hello web (si disponible) de votre système local.</span><span class="sxs-lookup"><span data-stu-id="3956e-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3956e-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3956e-108">Prerequisites</span></span>

* <span data-ttu-id="3956e-109">Un cluster Kubernetes, DC/OS ou Docker Swarm [déployé dans Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="3956e-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="3956e-110">SSH RSA fichier de clé privée, correspondant toohello toohello ajouté de clé publique cluster pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3956e-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="3956e-111">Ces commandes partent du principe que clé SSH privée de hello est `$HOME/.ssh/id_rsa` sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3956e-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="3956e-112">Pour plus d’informations, consultez ces instructions pour [macOS et Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../articles/virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3956e-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="3956e-113">Si vous ne fonctionne pas hello connexion SSH, vous devrez peut-être trop [réinitialiser vos clés SSH](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3956e-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="3956e-114">Se connecter tooa Kubernetes cluster</span><span class="sxs-lookup"><span data-stu-id="3956e-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="3956e-115">Suivez ces étapes tooinstall et configurer `kubectl` sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="3956e-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="3956e-116">Sur Linux ou macOS, vous devrez peut-être les commandes de hello toorun dans cette section à l’aide de `sudo`.</span><span class="sxs-lookup"><span data-stu-id="3956e-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="3956e-117">Installer kubectl</span><span class="sxs-lookup"><span data-stu-id="3956e-117">Install kubectl</span></span>
<span data-ttu-id="3956e-118">Une façon tooinstall cet outil est toouse hello `az acs kubernetes install-cli` commande Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3956e-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="3956e-119">toorun cette commande, assurez-vous que vous [installé](/cli/azure/install-az-cli2) hello dernière Azure CLI 2.0 et consigné dans tooan compte Azure (`az login`).</span><span class="sxs-lookup"><span data-stu-id="3956e-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="3956e-120">Ou bien, vous pouvez télécharger hello dernières `kubectl` client directement à partir de hello [Kubernetes libère page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span><span class="sxs-lookup"><span data-stu-id="3956e-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="3956e-121">Pour plus d’informations, consultez [Installation et configuration de kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span><span class="sxs-lookup"><span data-stu-id="3956e-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="3956e-122">Télécharger des informations d’identification du cluster</span><span class="sxs-lookup"><span data-stu-id="3956e-122">Download cluster credentials</span></span>
<span data-ttu-id="3956e-123">Une fois que vous avez `kubectl` installé, vous avez besoin d’informations d’identification tooyour ordinateur de toocopy hello cluster.</span><span class="sxs-lookup"><span data-stu-id="3956e-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="3956e-124">Informations d’identification de toodo monodirectionnelle get hello est avec hello `az acs kubernetes get-credentials` commande.</span><span class="sxs-lookup"><span data-stu-id="3956e-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="3956e-125">Passez le nom hello hello du groupe de ressources et le nom hello de ressource de service de conteneur hello :</span><span class="sxs-lookup"><span data-stu-id="3956e-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="3956e-126">Cette commande télécharge les informations d’identification du cluster hello trop`$HOME/.kube/config`, où `kubectl` attend qu’il toobe situé.</span><span class="sxs-lookup"><span data-stu-id="3956e-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="3956e-127">Vous pouvez également utiliser `scp` toosecurely copiez le fichier hello de `$HOME/.kube/config` sur l’ordinateur local hello master virtuelle tooyour.</span><span class="sxs-lookup"><span data-stu-id="3956e-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="3956e-128">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3956e-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="3956e-129">Si vous êtes sous Windows, vous pouvez utiliser l’interpréteur de commandes sur Ubuntu sur Windows, client de copie de fichiers sécurisé PuTTy hello ou un outil similaire.</span><span class="sxs-lookup"><span data-stu-id="3956e-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="3956e-130">Utiliser kubectl</span><span class="sxs-lookup"><span data-stu-id="3956e-130">Use kubectl</span></span>

<span data-ttu-id="3956e-131">Une fois que vous avez `kubectl` configuré, tester la connexion de hello en répertoriant les nœuds hello dans votre cluster :</span><span class="sxs-lookup"><span data-stu-id="3956e-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="3956e-132">Vous pouvez essayer d’autres commandes `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="3956e-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="3956e-133">Par exemple, vous pouvez afficher hello Kubernetes le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="3956e-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="3956e-134">Tout d’abord, exécutez un proxy de serveur de l’API de Kubernetes toohello :</span><span class="sxs-lookup"><span data-stu-id="3956e-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="3956e-135">Hello Kubernetes UI est désormais disponible à l’adresse : `http://localhost:8001/ui`.</span><span class="sxs-lookup"><span data-stu-id="3956e-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="3956e-136">Pour plus d’informations, consultez hello [Kubernetes de démarrage rapide](http://kubernetes.io/docs/user-guide/quick-start/).</span><span class="sxs-lookup"><span data-stu-id="3956e-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="3956e-137">Connecter le cluster de contrôleur de domaine/système d’exploitation ou essaim tooa</span><span class="sxs-lookup"><span data-stu-id="3956e-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="3956e-138">toouse hello contrôleur de domaine/système d’exploitation et les clusters Docker Swarm déployées par le Service de conteneur Azure, suivez ces instructions de toocreate un tunnel SSH à partir de votre système local de Windows, Mac OS ou Linux.</span><span class="sxs-lookup"><span data-stu-id="3956e-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="3956e-139">Ces instructions se concentrent sur le tunnel du trafic TCP via SSH.</span><span class="sxs-lookup"><span data-stu-id="3956e-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="3956e-140">Vous pouvez également démarrer une session SSH interactive avec l’un des systèmes de gestion de cluster interne hello, mais nous ne recommandons pas cela.</span><span class="sxs-lookup"><span data-stu-id="3956e-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="3956e-141">Le fait de travailler directement sur un système interne risque de provoquer des modifications de configuration accidentelles.</span><span class="sxs-lookup"><span data-stu-id="3956e-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="3956e-142">Créer un tunnel SSH sur Linux ou macOS</span><span class="sxs-lookup"><span data-stu-id="3956e-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="3956e-143">Hello première chose que vous effectuez lorsque vous créez un tunnel SSH sur Linux ou macOS est toolocate hello nom DNS public de masques d’équilibrage de la charge hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="3956e-144">Procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3956e-144">Follow these steps:</span></span>


1. <span data-ttu-id="3956e-145">Bonjour [portail Azure](https://portal.azure.com), parcourir le groupe de ressources toohello contenant votre cluster de service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="3956e-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="3956e-146">Développez le groupe de ressources hello afin que chaque ressource est affichée.</span><span class="sxs-lookup"><span data-stu-id="3956e-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="3956e-147">Cliquez sur hello **service de conteneur** ressource, puis cliquez sur **vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="3956e-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="3956e-148">Hello **Master FQDN** Hello cluster apparaît sous **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="3956e-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="3956e-149">Enregistrez ce nom pour pouvoir l’utiliser ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="3956e-149">Save this name for later use.</span></span> 

    ![Nom DNS public](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="3956e-151">Vous pouvez également exécuter hello `az acs show` commande sur votre service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="3956e-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="3956e-152">Recherchez hello **profil : nom de domaine complet principal** propriété dans la sortie de la commande hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="3956e-153">Ouvrez un interpréteur de commandes et exécutez hello `ssh` commande en spécifiant hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="3956e-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="3956e-154">**LOCAL_PORT** est le port TCP hello côté service de hello de tooconnect de tunnel hello pour.</span><span class="sxs-lookup"><span data-stu-id="3956e-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="3956e-155">Pour essaim, définissez cette too2375.</span><span class="sxs-lookup"><span data-stu-id="3956e-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="3956e-156">Pour le contrôleur de domaine/système d’exploitation, définissez cette too80.</span><span class="sxs-lookup"><span data-stu-id="3956e-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="3956e-157">**REMOTE_PORT** port hello du point de terminaison hello que vous souhaitez tooexpose.</span><span class="sxs-lookup"><span data-stu-id="3956e-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="3956e-158">Pour Swarm, utilisez le port 2375.</span><span class="sxs-lookup"><span data-stu-id="3956e-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="3956e-159">Pour DC/OS, utilisez le port 80.</span><span class="sxs-lookup"><span data-stu-id="3956e-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="3956e-160">**Nom d’utilisateur** est le nom d’utilisateur hello qui a été fourni lors du déploiement de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="3956e-161">**DNSPREFIX** est le préfixe du DNS hello que vous avez fourni lors du déploiement de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="3956e-162">**RÉGION** est la région de hello dans lequel se trouve votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="3956e-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="3956e-163">**PATH_TO_PRIVATE_KEY** [facultatif] est hello chemin d’accès toohello clé privée qui correspond la clé publique de toohello vous avez fourni lors de la création de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="3956e-164">Utilisez cette option avec hello `-i` indicateur.</span><span class="sxs-lookup"><span data-stu-id="3956e-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="3956e-165">Hello port de connexion SSH est 2200 et pas hello port standard 22.</span><span class="sxs-lookup"><span data-stu-id="3956e-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="3956e-166">Dans un cluster avec plusieurs machines virtuelles principal, il s’agit de hello connexion port toohello premier masque de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3956e-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="3956e-167">commande Hello retourne sans sortie.</span><span class="sxs-lookup"><span data-stu-id="3956e-167">hello command returns without output.</span></span>

<span data-ttu-id="3956e-168">Consultez les exemples de hello pour le contrôleur de domaine/système d’exploitation et essaim Bonjour les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="3956e-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="3956e-169">Tunnel DC/OS</span><span class="sxs-lookup"><span data-stu-id="3956e-169">DC/OS tunnel</span></span>
<span data-ttu-id="3956e-170">tooopen un tunnel pour les points de terminaison de contrôleur de domaine/système d’exploitation, exécutez une commande hello suivante :</span><span class="sxs-lookup"><span data-stu-id="3956e-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="3956e-171">Vérifiez qu’aucun autre processus local n’est lié au port 80.</span><span class="sxs-lookup"><span data-stu-id="3956e-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="3956e-172">Si nécessaire, vous pouvez spécifier un port local autre que le port 80, tel que le port 8080.</span><span class="sxs-lookup"><span data-stu-id="3956e-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="3956e-173">Toutefois, certains liens de l’interface utilisateur web risquent de ne pas fonctionner si vous utilisez ce port.</span><span class="sxs-lookup"><span data-stu-id="3956e-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="3956e-174">Vous pouvez désormais accéder aux points de terminaison hello contrôleur de domaine/système d’exploitation à partir de votre système local via hello (en supposant que le port local 80) des URL suivantes :</span><span class="sxs-lookup"><span data-stu-id="3956e-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="3956e-175">DC/OS : `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="3956e-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="3956e-176">Marathon : `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="3956e-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="3956e-177">Mesos : `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="3956e-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="3956e-178">De même, vous pouvez atteindre les API rest de hello pour chaque application via ce tunnel.</span><span class="sxs-lookup"><span data-stu-id="3956e-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="3956e-179">Tunnel Swarm</span><span class="sxs-lookup"><span data-stu-id="3956e-179">Swarm tunnel</span></span>
<span data-ttu-id="3956e-180">tooopen un point de terminaison tunnel toohello essaim, exécuter une commande hello suivante :</span><span class="sxs-lookup"><span data-stu-id="3956e-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="3956e-181">Vérifiez qu’aucun autre processus local n’est lié au port 2375.</span><span class="sxs-lookup"><span data-stu-id="3956e-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="3956e-182">Par exemple, si vous exécutez localement démon Docker de hello, elle est définie par le port de toouse par défaut 2375.</span><span class="sxs-lookup"><span data-stu-id="3956e-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="3956e-183">Si nécessaire, vous pouvez spécifier un port local autre que le port 2375.</span><span class="sxs-lookup"><span data-stu-id="3956e-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="3956e-184">Vous pouvez désormais accéder aux cluster de Docker Swarm hello à l’aide d’une interface de ligne hello Docker (CLI Docker) sur votre système local.</span><span class="sxs-lookup"><span data-stu-id="3956e-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="3956e-185">Pour obtenir des instructions d’installation, consultez [Installation de Docker](https://docs.docker.com/engine/installation/).</span><span class="sxs-lookup"><span data-stu-id="3956e-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="3956e-186">Définissez votre toohello de variable environnement DOCKER_HOST port local que vous avez configuré pour un tunnel de hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="3956e-187">Exécutez les commandes Docker ce cluster Docker Swarm de tunnel toohello.</span><span class="sxs-lookup"><span data-stu-id="3956e-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="3956e-188">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="3956e-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="3956e-189">Créer un tunnel SSH sur Windows</span><span class="sxs-lookup"><span data-stu-id="3956e-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="3956e-190">Il existe plusieurs options de création des tunnels SSH sous Windows.</span><span class="sxs-lookup"><span data-stu-id="3956e-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="3956e-191">Si vous exécutez un interpréteur de commandes sur Ubuntu sur Windows ou un outil similaire, vous pouvez suivre les instructions tunneling SSH hello indiquées plus haut dans cet article pour macOS et Linux.</span><span class="sxs-lookup"><span data-stu-id="3956e-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="3956e-192">En guise d’alternative sur Windows, cette section décrit comment tunnel de hello toouse toocreate PuTTY.</span><span class="sxs-lookup"><span data-stu-id="3956e-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="3956e-193">[Télécharger PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour système Windows.</span><span class="sxs-lookup"><span data-stu-id="3956e-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="3956e-194">Exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-194">Run hello application.</span></span>

3. <span data-ttu-id="3956e-195">Entrez un nom d’hôte qui se compose de nom d’utilisateur admin hello cluster et hello nom DNS public du premier masque hello de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="3956e-196">Hello **nom d’hôte** ressemble trop`azureuser@PublicDNSName`.</span><span class="sxs-lookup"><span data-stu-id="3956e-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="3956e-197">Entrez 2200 pour hello **Port**.</span><span class="sxs-lookup"><span data-stu-id="3956e-197">Enter 2200 for hello **Port**.</span></span>

    ![Configuration PuTTY 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="3956e-199">Sélectionnez **SSH > Auth**. Ajoutez un chemin d’accès tooyour fichier de clé privée (format .ppk) pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="3956e-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="3956e-200">Vous pouvez utiliser un outil tel que [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate ce fichier à partir de hello cluster de hello toocreate utilisé clé SSH.</span><span class="sxs-lookup"><span data-stu-id="3956e-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![Configuration PuTTY 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="3956e-202">Sélectionnez **SSH > Tunnels** configurez hello transféré les ports qui suit :</span><span class="sxs-lookup"><span data-stu-id="3956e-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="3956e-203">**Port source :** utilisez 80 pour DC/OS et 2375 pour Swarm.</span><span class="sxs-lookup"><span data-stu-id="3956e-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="3956e-204">**Destination :** utilisez localhost:80 pour DC/OS ou localhost:2375 pour Swarm.</span><span class="sxs-lookup"><span data-stu-id="3956e-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="3956e-205">Hello, l’exemple suivant est configuré pour le contrôleur de domaine/système d’exploitation, mais il ressemblera pour Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="3956e-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3956e-206">Le port 80 ne doit pas être en cours d’utilisation lors de la création de ce tunnel.</span><span class="sxs-lookup"><span data-stu-id="3956e-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![Configuration PuTTY 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="3956e-208">Lorsque vous avez terminé, cliquez sur **Session > Enregistrer** configuration de la connexion toosave hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="3956e-209">tooconnect toohello PuTTY de session, cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="3956e-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="3956e-210">Lorsque vous vous connectez, vous pouvez voir la configuration du port hello dans le journal des événements PuTTY hello.</span><span class="sxs-lookup"><span data-stu-id="3956e-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![Journal des événements PuTTY](./media/container-service-connect/putty4.png)

<span data-ttu-id="3956e-212">Une fois que vous avez configuré le tunnel de hello pour le contrôleur de domaine/système d’exploitation, vous pouvez accéder à hello relatives des points de terminaison à :</span><span class="sxs-lookup"><span data-stu-id="3956e-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="3956e-213">DC/OS : `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="3956e-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="3956e-214">Marathon : `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="3956e-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="3956e-215">Mesos : `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="3956e-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="3956e-216">Une fois que vous avez configuré le tunnel de hello pour Docker Swarm, ouvrez votre tooconfigure de paramètres Windows une variable d’environnement nommée `DOCKER_HOST` avec la valeur `:2375`.</span><span class="sxs-lookup"><span data-stu-id="3956e-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="3956e-217">Ensuite, vous pouvez accéder cluster essaim de hello via hello Docker CLI.</span><span class="sxs-lookup"><span data-stu-id="3956e-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3956e-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3956e-218">Next steps</span></span>
<span data-ttu-id="3956e-219">Déployer et gérer des conteneurs dans votre cluster :</span><span class="sxs-lookup"><span data-stu-id="3956e-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="3956e-220">Gestion des conteneurs avec Kubernetes</span><span class="sxs-lookup"><span data-stu-id="3956e-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="3956e-221">Gestion de conteneur via l’API REST</span><span class="sxs-lookup"><span data-stu-id="3956e-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="3956e-222">Travailler avec hello Service de conteneur Azure et Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="3956e-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

