## <a name="create-a-resource-group"></a><span data-ttu-id="162c9-101">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="162c9-101">Create a resource group</span></span>

<span data-ttu-id="162c9-102">Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande.</span><span class="sxs-lookup"><span data-stu-id="162c9-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="162c9-103">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="162c9-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="162c9-104">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="162c9-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="162c9-105">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="162c9-105">Create a virtual machine</span></span>

<span data-ttu-id="162c9-106">Créer une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande.</span><span class="sxs-lookup"><span data-stu-id="162c9-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="162c9-107">Hello exemple suivant crée un ordinateur virtuel nommé *myVM* et crée des clés SSH s’ils n’existent pas déjà dans un emplacement de la clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="162c9-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="162c9-108">toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.</span><span class="sxs-lookup"><span data-stu-id="162c9-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="162c9-109">Lorsque hello machine virtuelle a été créé, hello CLI d’Azure affiche les informations toohello semblable l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="162c9-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="162c9-110">Prenez note de hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="162c9-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="162c9-111">Cette adresse est utilisée tooaccess hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="162c9-111">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="162c9-112">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="162c9-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="162c9-113">Par défaut, seules les connexions SSH sont autorisées dans les machines virtuelles Linux déployées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="162c9-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="162c9-114">Étant donné que cet ordinateur virtuel va toobe un serveur web, vous devez tooopen port 80 de hello internet.</span><span class="sxs-lookup"><span data-stu-id="162c9-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="162c9-115">Hello d’utilisation [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port) commande tooopen hello souhaité de port.</span><span class="sxs-lookup"><span data-stu-id="162c9-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="162c9-116">Se connecter avec SSH à votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="162c9-116">SSH into your VM</span></span>


<span data-ttu-id="162c9-117">Si vous ne connaissez pas déjà hello adresse IP publique de votre machine virtuelle, exécutez hello [liste public-ip de réseau az](/cli/azure/network/public-ip#list) commande :</span><span class="sxs-lookup"><span data-stu-id="162c9-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="162c9-118">La commande suivante de hello utilisation toocreate une session SSH avec l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="162c9-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="162c9-119">Remplacez hello correct adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="162c9-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="162c9-120">Dans cet exemple, adresse IP de hello est *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="162c9-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

