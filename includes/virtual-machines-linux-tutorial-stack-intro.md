## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a>Création d'une machine virtuelle

Créer une machine virtuelle avec hello [az vm créer](/cli/azure/vm#create) commande. 

Hello exemple suivant crée un ordinateur virtuel nommé *myVM* et crée des clés SSH s’ils n’existent pas déjà dans un emplacement de la clé par défaut. toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

Lorsque hello machine virtuelle a été créé, hello CLI d’Azure affiche les informations toohello semblable l’exemple suivant. Prenez note de hello `publicIpAddress`. Cette adresse est utilisée tooaccess hello machine virtuelle.

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



## <a name="open-port-80-for-web-traffic"></a>Ouvrez le port 80 pour le trafic web 

Par défaut, seules les connexions SSH sont autorisées dans les machines virtuelles Linux déployées dans Azure. Étant donné que cet ordinateur virtuel va toobe un serveur web, vous devez tooopen port 80 de hello internet. Hello d’utilisation [ouvrir un ordinateur virtuel az-port](/cli/azure/vm#open-port) commande tooopen hello souhaité de port.  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a>Se connecter avec SSH à votre machine virtuelle


Si vous ne connaissez pas déjà hello adresse IP publique de votre machine virtuelle, exécutez hello [liste public-ip de réseau az](/cli/azure/network/public-ip#list) commande :


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

La commande suivante de hello utilisation toocreate une session SSH avec l’ordinateur virtuel de hello. Remplacez hello correct adresse IP publique de votre machine virtuelle. Dans cet exemple, adresse IP de hello est *40.68.254.142*.

```bash
ssh azureuser@40.68.254.142
```

