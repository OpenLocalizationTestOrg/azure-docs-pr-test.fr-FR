


Cette rubrique montre comment :

* injecter des données dans une machine virtuelle Azure lors de son approvisionnement ;
* les récupérer avec Windows et Linux ;
* Utiliser des outils spéciaux disponibles sur certains systèmes toodetect et gérer automatiquement les données personnalisées.

> [!NOTE]
> Cet article décrit les données personnalisées peuvent être ajoutées à l’aide d’une machine virtuelle créée avec hello API de gestion des services Azure. toosee toouse hello API de gestion des ressources Azure, voir [exemple de modèle de hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a>Injection de données personnalisées dans votre machine virtuelle Azure
Cette fonctionnalité est actuellement pris en charge uniquement dans hello [Interface de ligne de commande Azure](https://github.com/Azure/azure-xplat-cli). Ici, nous créons un `custom-data.txt` fichier qui contient nos données, puis injecter qui dans toohello machine virtuelle lors de la configuration. Bien que vous pouvez utiliser une des options de hello pour hello `azure vm create` suivant de hello illustre une approche très élémentaire de la commande :

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a>À l’aide des données personnalisées dans la machine virtuelle de hello
* Si votre machine virtuelle Azure est un ordinateur virtuel basé sur Windows, hello données personnalisé est enregistré trop`%SYSTEMDRIVE%\AzureData\CustomData.bin`. Bien qu’il était codée en base64 de tootransfer de toohello d’ordinateur local hello nouvel ordinateur virtuel, il est automatiquement décodé et peut être ouvert ou utilisées immédiatement.
  
  > [!NOTE]
  > Si le fichier de hello existe, il est remplacé. sécurité Hello sur le répertoire de hello est définie trop**système : contrôle total** et **administrateurs : contrôle total**.
  > 
  > 
* Si votre machine virtuelle Azure est une machine virtuelle basés sur Linux, puis le fichier de données personnalisées hello se trouve dans un des éléments suivants de hello place en fonction de votre distribution. les données de salutation peuvent être codée en base64, donc vous devez tout d’abord les données de salutation toodecode :
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a>Cloud-init sur Azure
Si votre machine virtuelle Azure est à partir d’une image Ubuntu ou CoreOS, vous pouvez utiliser CustomData toosend un toocloud cloud-config-init. Sinon, si votre fichier de données personnalisées est un script, Cloud-init peut l’exécuter.

### <a name="ubuntu-cloud-images"></a>Images cloud Ubuntu
Dans la plupart des images Azure Linux, vous devez modifier « / etc/waagent.conf » tooconfigure hello temporaire de ressources disque et échange le fichier. Pour plus d’information, consultez le [Guide d’utilisation de l’agent Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) .

Toutefois, sur les Images de hello Ubuntu Cloud, vous devez utiliser disque de ressources cloud-init tooconfigure hello (autrement dit, un disque « éphémère » hello) et échange partition. Consultez hello suivant page Wiki d’Ubuntu hello pour plus d’informations : [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a>Étapes suivantes : Utilisation de Cloud-init
Pour plus d’informations, consultez hello [documentation cloud-init pour Ubuntu](https://help.ubuntu.com/community/CloudInit).

<!--Link references-->
[Référence sur l’opération Ajouter un rôle de l’API REST de gestion des services](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[Interface de ligne de commande Azure](https://github.com/Azure/azure-xplat-cli)

