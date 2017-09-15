## <a name="create-a-resource-group"></a><span data-ttu-id="08824-101">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="08824-101">Create a resource group</span></span>

<span data-ttu-id="08824-102">Créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="08824-102">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="08824-103">Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.</span><span class="sxs-lookup"><span data-stu-id="08824-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="08824-104">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *eastus*.</span><span class="sxs-lookup"><span data-stu-id="08824-104">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="08824-105">Création d'une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="08824-105">Create a virtual machine</span></span>

<span data-ttu-id="08824-106">Créez une machine virtuelle avec la commande [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="08824-106">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="08824-107">L’exemple suivant crée une machine virtuelle nommée *myVM* et des clés SSH si elles n’existent pas déjà dans un emplacement de clé par défaut.</span><span class="sxs-lookup"><span data-stu-id="08824-107">The following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="08824-108">Pour utiliser un ensemble spécifique de clés, utilisez l’option `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="08824-108">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="08824-109">Lorsque la machine virtuelle a été créée, l’interface de ligne de commande Azure affiche des informations similaires à l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="08824-109">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="08824-110">Notez la valeur de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="08824-110">Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="08824-111">Cette adresse est utilisée pour accéder à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08824-111">This address is used to access the VM.</span></span>

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



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="08824-112">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="08824-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="08824-113">Par défaut, seules les connexions SSH sont autorisées dans les machines virtuelles Linux déployées dans Azure.</span><span class="sxs-lookup"><span data-stu-id="08824-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="08824-114">Étant donné que cette machine virtuelle sera un serveur web, vous devez ouvrir le port 80 à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="08824-114">Because this VM is going to be a web server, you need to open port 80 from the internet.</span></span> <span data-ttu-id="08824-115">Utilisez la commande [az vm open-port](/cli/azure/vm#open-port) pour ouvrir le port souhaité.</span><span class="sxs-lookup"><span data-stu-id="08824-115">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="08824-116">Se connecter avec SSH à votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="08824-116">SSH into your VM</span></span>


<span data-ttu-id="08824-117">Pour trouver l’adresse IP publique de votre machine virtuelle, exécutez la commande [az network public-ip list](/cli/azure/network/public-ip#list) :</span><span class="sxs-lookup"><span data-stu-id="08824-117">If you don't already know the public IP address of your VM, run the [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="08824-118">Utilisez la commande suivante pour créer une session SSH avec la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08824-118">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="08824-119">Remplacez l’adresse IP publique correcte de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08824-119">Substitute the correct public IP address of your virtual machine.</span></span> <span data-ttu-id="08824-120">Dans cet exemple, l’adresse IP est *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="08824-120">In this example, the IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

