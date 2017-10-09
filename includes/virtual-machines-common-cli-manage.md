Hello Azure CLI 2.0 vous permet de toocreate et gérer vos ressources Azure sur Windows, Linux et macOS. Cet article décrit certains toocreate de commandes courants hello et gérer des machines virtuelles (VM).

Cet article suppose que hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0](/cli/azure/install-azure-cli). Vous pouvez également utiliser [Cloud Shell](/azure/cloud-shell/quickstart) à partir de votre navigateur.

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Commandes de base Basic Azure Resource Manager de l’interface de ligne de commande Azure
Pour plus d’aide sur les options et les commutateurs de ligne de commande spécifiques, vous pouvez utiliser les fonctions hello en ligne de commande options d’aide et en tapant `az <command> <subcommand> --help`.

### <a name="create-vms"></a>Créer des machines virtuelles
| Task | Commandes d’interface de ligne de commande Azure |
| --- | --- |
| Créer un groupe de ressources | `az group create --name myResourceGroup --location eastus` |
| Créer une machine virtuelle Linux | `az vm create --resource-group myResourceGroup --name myVM --image ubuntults` |
| Créer une machine virtuelle Windows | `az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter` |

### <a name="manage-vm-state"></a>Gérer l’état d’une machine virtuelle
| Task | Commandes d’interface de ligne de commande Azure |
| --- | --- |
| Démarrer une machine virtuelle | `az vm start --resource-group myResourceGroup --name myVM` |
| Arrêter une machine virtuelle | `az vm stop --resource-group myResourceGroup --name myVM` |
| Désallouer une machine virtuelle | `az vm deallocate --resource-group myResourceGroup --name myVM` |
| Redémarrer une machine virtuelle | `az vm restart --resource-group myResourceGroup --name myVM` |
| Redéploiement d’une machine virtuelle | `az vm redeploy --resource-group myResourceGroup --name myVM` |
| Supprimer une machine virtuelle | `az vm delete --resource-group myResourceGroup --name myVM` |

### <a name="get-vm-info"></a>Obtenir des informations sur les machines virtuelles
| Task | Commandes d’interface de ligne de commande Azure |
| --- | --- |
| Énumérer les machines virtuelles | `az vm list` |
| Obtenir des informations sur une machine virtuelle | `az vm show --resource-group myResourceGroup --name myVM` |
| Obtenir l'utilisation des ressources de la machine virtuelle | `az vm list-usage --location eastus` |
| Obtenir toutes les tailles de machines virtuelles disponibles | `az vm list-sizes --location eastus` |

## <a name="disks-and-images"></a>Disques et images
| Task | Commandes d’interface de ligne de commande Azure |
| --- | --- |
| Ajouter un tooa de disque de données machine virtuelle | `az vm disk attach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk --size-gb 128 --new ` |
| Supprimer un disque de données à partir d'une machine virtuelle | `az vm disk detach --resource-group myResourceGroup --vm-name myVM --disk myDataDisk` |
| Redimensionner un disque | `az disk update --resource-group myResourceGroup --name myDataDisk --size-gb 256` |
| Effectuer la capture instantanée d’un disque | `az snapshot create --resource-group myResourceGroup --name mySnapshot --source myDataDisk` |
| Créer une image de machine virtuelle | `az image create --resource-group myResourceGroup --source myVM --name myImage` |
| Créer une machine virtuelle à partir d’une image | `az vm create --resource-group myResourceGroup --name myNewVM --image myImage` |


## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des exemples supplémentaires de commandes CLI de hello, consultez hello [créer et gérer des ordinateurs virtuels Linux par hello CLI d’Azure](../articles/virtual-machines/linux/tutorial-manage-vm.md) didacticiel.

