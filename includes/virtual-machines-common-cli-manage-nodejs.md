Avant de pouvoir utiliser hello CLI d’Azure avec toodeploy Azure Resource Manager commandes et des modèles de ressources et les charges de travail à l’aide de groupes de ressources, vous aurez besoin un compte Azure. Si vous ne disposez pas d’un compte, vous pouvez obtenir une [version d’essai gratuite d’Azure ici](https://azure.microsoft.com/pricing/free-trial/).

Si vous n’avez pas déjà installé hello CLI d’Azure et abonnement de tooyour connecté, consultez [installation Bonjour Azure CLI](../articles/cli-install-nodejs.md) définir le mode hello trop`arm` avec `azure config mode arm`et rejoignez tooAzure hello `azure login` commande.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- CLI Azure 10 – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](../articles/virtual-machines/linux/cli-manage.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="basic-azure-resource-manager-commands-in-azure-cli"></a>Commandes de base Basic Azure Resource Manager de l’interface de ligne de commande Azure
Cet article traite des commandes de base vous souhaitez toouse avec Azure CLI toomanage et interagir avec vos ressources (principalement de machines virtuelles) dans votre abonnement Azure.  Pour plus d’aide sur les options et les commutateurs de ligne de commande spécifiques, vous pouvez utiliser les fonctions hello en ligne de commande options d’aide et en tapant `azure <command> <subcommand> --help` ou `azure help <command> <subcommand>`.

> [!NOTE]
> Ces exemples n’incluent pas les opérations basées sur des modèles qui sont recommandées pour les déploiements de machines virtuelles dans le Gestionnaire de ressources. Pour plus d’informations, consultez [hello d’utilisation CLI d’Azure avec Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md) et [déployer et gérer des ordinateurs virtuels à l’aide de modèles Azure Resource Manager et hello CLI d’Azure](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

| Task | Gestionnaire de ressources |
| --- | --- | --- |
| Créer hello plus de base pour machine virtuelle |`azure vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password>`<br/><br/>(Obtenir hello `image-urn` de hello `azure vm image list` commande. Consultez [cet article](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour découvrir des exemples.) |
| Créer une machine virtuelle Linux |`azure  vm create [options] <resource-group> <name> <location> -y "Linux"` |
| Créer une machine virtuelle Windows |`azure  vm create [options] <resource-group> <name> <location> -y "Windows"` |
| Énumérer les machines virtuelles |`azure  vm list [options]` |
| Obtenir des informations sur une machine virtuelle |`azure  vm show [options] <resource_group> <name>` |
| Démarrer une machine virtuelle |`azure vm start [options] <resource_group> <name>` |
| Arrêter une machine virtuelle |`azure vm stop [options] <resource_group> <name>` |
| Désallouer une machine virtuelle |`azure vm deallocate [options] <resource-group> <name>` |
| Redémarrer une machine virtuelle |`azure vm restart [options] <resource_group> <name>` |
| Supprimer une machine virtuelle |`azure vm delete [options] <resource_group> <name>` |
| Capturer une machine virtuelle |`azure vm capture [options] <resource_group> <name>` |
| Créer une machine virtuelle à partir d'une image utilisateur |`azure  vm create [options] –q <image-name> <resource-group> <name> <location> <os-type>` |
| Créer une machine virtuelle à partir d'un disque spécialisé |`azue  vm create [options] –d <os-disk-vhd> <resource-group> <name> <location> <os-type>` |
| Ajouter un tooa de disque de données machine virtuelle |`azure  vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]` |
| Supprimer un disque de données à partir d'une machine virtuelle |`azure  vm disk detach [options] <resource-group> <vm-name> <lun>` |
| Ajouter un tooa d’extension générique machine virtuelle |`azure  vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Ajouter l’extension de machine virtuelle accès tooa machine virtuelle |`azure vm reset-access [options] <resource-group> <name>` |
| Ajouter Docker extension tooa machine virtuelle |`azure  vm docker create [options] <resource-group> <name> <location> <os-type>` |
| Supprimer une extension de machine virtuelle |`azure  vm extension set [options] –u <resource-group> <vm-name> <name> <publisher-name> <version>` |
| Obtenir l'utilisation des ressources de la machine virtuelle |`azure vm list-usage [options] <location>` |
| Obtenir toutes les tailles de machines virtuelles disponibles |`azure vm sizes [options]` |

## <a name="next-steps"></a>Étapes suivantes
* Pour obtenir des exemples supplémentaires des commandes CLI de hello augmente au-delà de la gestion de machine virtuelle de base, consultez [Using hello CLI d’Azure avec Azure Resource Manager](../articles/virtual-machines/azure-cli-arm-commands.md).
