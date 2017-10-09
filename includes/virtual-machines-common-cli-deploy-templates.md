
* [Création rapide d’une machine virtuelle dans Azure](#quick-create-a-vm-in-azure)
* [Déploiement d’une machine virtuelle dans Azure à partir d’un modèle](#deploy-a-vm-in-azure-from-a-template)
* [Création d’une machine virtuelle à partir d’une image personnalisée](#create-a-custom-vm-image)
* [Déploiement d’une machine virtuelle qui utilise un réseau virtuel et un équilibreur de charge](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [Suppression d’un groupe de ressources](#remove-a-resource-group)
* [Afficher le journal hello pour un déploiement de groupe de ressources](#show-the-log-for-a-resource-group-deployment)
* [Affichage des informations relatives à une machine virtuelle](#display-information-about-a-virtual-machine)
* [Connecter la machine virtuelle tooa Linux](#log-on-to-a-linux-based-virtual-machine)
* [Arrêt d’une machine virtuelle](#stop-a-virtual-machine)
* [Démarrage d’une machine virtuelle](#start-a-virtual-machine)
* [Association d’un disque de données](#attach-a-data-disk)

## <a name="getting-ready"></a>Préparation
Avant de pouvoir utiliser hello CLI d’Azure avec des groupes de ressources Azure, vous devez version CLI d’Azure toohave hello et un compte Azure. Si vous n’avez pas hello CLI d’Azure, [installer](../articles/cli-install-nodejs.md).

### <a name="update-your-azure-cli-version-too090-or-later"></a>Mettre à jour votre too0.9.0 de version CLI d’Azure ou version ultérieure
Type `azure --version` toosee si vous avez déjà installé la version 0.9.0 ou version ultérieure.

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

Si votre version n’est pas 0.9.0 ou version ultérieure, vous devez tooupdate en utilisant l’une des hello des programmes d’installation de natives ou via **npm** en tapant `npm update -g azure-cli`.

Vous pouvez également exécuter CLI d’Azure comme un conteneur Docker en utilisant hello [image Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/). À partir d’un hôte Docker, exécutez hello de commande suivante :

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a>Configurer votre compte et votre abonnement Microsoft Azure
Si vous ne possédez pas déjà un abonnement Azure, mais que vous avez un abonnement MSDN, vous pouvez activer vos [avantages abonnés MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Ou vous pouvez vous inscrire à un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).

Maintenant [connecter tooyour compte Azure interactivement](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) en tapant `azure login` puis suivez les instructions de hello pour une tooyour d’expérience de connexion interactive compte Azure. 

> [!NOTE]
> Si vous avez un travail ou d’établissement scolaire ID et que vous savez que vous n’avez pas l’authentification à deux facteurs est activée, vous pouvez **également** utiliser `azure login -u` avec hello Professionnel ou scolaire toolog ID dans *sans* une session interactive. Si vous ne disposez d’un travail ou scolaire ID, vous pouvez [créer un id Professionnel ou scolaire à partir de votre compte Microsoft personnel](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog Bonjour identique.
>
>

Votre compte peut avoir plusieurs abonnements. Vous pouvez répertorier vos abonnements en tapant `azure account list`, ce qui pourrait donner ceci :

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

Vous pouvez définir l’abonnement Azure hello en tapant hello suivante. Utilisez hello hello nom ou l’ID d’abonnement qui a des ressources hello toomanage.

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a>Basculer le mode de groupe de ressources toohello CLI d’Azure
Par défaut, hello CLI d’Azure démarre en mode de gestion de service hello (**asm** mode). Tapez hello suivant le mode de groupe tooswitch tooresource.

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a>Présentation des groupes et des modèles de ressources Azure
La plupart des applications sont basées sur une combinaison de différents types de ressources (au moins une machine virtuelle et un compte de stockage, une base de données SQL, un réseau virtuel ou un réseau de distribution de contenu). Hello API de gestion des services Azure par défaut et hello portail Azure classic représenté ces éléments à l’aide d’une approche de service par service. Cette approche requiert que vous toodeploy et gérer des services individuels hello individuellement (ou rechercher d’autres outils de le faire) et non comme une unité logique de déploiement.

*Les modèles de gestionnaire de ressources Azure*, toutefois, permettent à vous toodeploy et gérer ces différentes ressources comme une unité logique de déploiement de manière déclarative. Au lieu de manière impérative informe Azure toodeploy une commande après l’autre, vous décrivez tout votre déploiement dans un fichier JSON--toutes les ressources de hello et de configuration et les paramètres de déploiement et indiquer à Azure toodeploy ces ressources comme une groupe.

Vous pouvez ensuite gérer hello cycle de vie global des ressources du groupe hello à l’aide des commandes de gestion de ressources CLI d’Azure pour :

* Arrêter, démarrer ou supprimer toutes les ressources hello au sein du groupe de hello à la fois.
* Appliquer toolock de règles de contrôle d’accès en fonction du rôle (RBAC) vers le bas des autorisations de sécurité sur ces derniers.
* mener des opérations d’audit ;
* baliser des ressources avec des métadonnées supplémentaires pour améliorer leur suivi.

Vous pouvez apprendre beaucoup plus d’informations sur les groupes de ressources Azure et à quoi ils peuvent vous Bonjour [vue d’ensemble du Gestionnaire de ressources Azure](../articles/azure-resource-manager/resource-group-overview.md). Si vous êtes intéressé par la création de modèles, consultez [Création de modèles Azure Resource Manager](../articles/resource-group-authoring-templates.md).

## <a id="quick-create-a-vm-in-azure"></a>Tâche : Créer rapidement une machine virtuelle dans Azure
Parfois, vous savez quelle image que vous avez besoin, et vous avez besoin maintenant une machine virtuelle à partir de cette image et vous ne vous souciez trop infrastructure de hello--peut-être tootest quelque chose sur une machine virtuelle propre. C’est lorsque vous souhaitez toouse hello `azure vm quick-create` de commandes et passer toocreate nécessaire des arguments de hello une machine virtuelle et son infrastructure.

Commencez par créer votre groupe de ressources.

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

Ensuite, vous aurez besoin d’une image. toofind une image avec hello CLI d’Azure, consultez [Navigating et sélectionner des images de machine virtuelle Azure avec PowerShell et hello CLI d’Azure](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Mais pour cet article, voici une brève liste d’images populaires. Nous allons utiliser l’image Stable de CoreOS pour cette création rapide.

> [!NOTE]
> Pour ComputeImageVersion, vous pouvez également simplement fournir « dernier » comme hello paramètre dans les deux langage de modèle hello et Bonjour CLI d’Azure. Ainsi, que vous tooalways utiliser hello dernière modification version et d’image de hello sans avoir toomodify vos scripts ou les modèles. Consultez l’illustration ci-dessous.
>
>

| PublisherName | Offer | Sku | Version |
|:--- |:--- |:--- |:--- |
| OpenLogic |CentOS |7 |7.0.201503 |
| OpenLogic |CentOS |7.1 |7.1.201504 |
| CoreOS |CoreOS |Bêta |647.0.0 |
| CoreOS |CoreOS |Stable |633.1.0 |
| MicrosoftDynamicsNAV |DynamicsNAV |2015 |8.0.40459 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2013 |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Standard |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Entreprise |1.0.0 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Entreprise, optimisé pour l’entrepôt de données |12.0.2430 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Entreprise, optimisé pour le traitement transactionnel en ligne |12.0.2430 |
| Canonical |UbuntuServer |12.04.5-LTS |12.04.201504230 |
| Canonical |UbuntuServer |14.04.2-LTS |14.04.201503090 |
| MicrosoftWindowsServer |WindowsServer |2012-Datacenter |3.0.201503 |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |4.0.201503 |
| MicrosoftWindowsServer |WindowsServer |Windows Server Technical Preview |5.0.201504 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |1.0.141204 |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |4.3.4665 |

Créez simplement votre machine virtuelle en entrant hello `azure vm quick-create` commande et prêt pour hello invites. Le résultat suivant doit s’afficher :

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

Et vous voici avec une nouvelle machine virtuelle.

## <a id="deploy-a-vm-in-azure-from-a-template"></a>Tâche : Déployer une machine virtuelle dans Azure à partir d’un modèle
Utilisez les instructions de hello dans ces sections de toodeploy une machine virtuelle Azure à l’aide d’un modèle avec hello CLI d’Azure. Ce modèle crée un seul ordinateur virtuel dans un réseau virtuel avec un sous-réseau unique et, contrairement aux `azure vm quick-create`, permet de vous toodescribe précisément ce que vous voulez et répéter sans erreurs. Voici le résultat du modèle :

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a>Étape 1 : Examiner le fichier JSON de hello des paramètres du modèle hello
Voici le contenu de hello du fichier JSON de hello pour le modèle de hello. (modèle de hello se trouve également dans [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)

Les modèles sont flexibles, donc le concepteur hello peut avoir choisi toogive un grand nombre de paramètres ou choisi toooffer uniquement quelques en créant un modèle qui est plus fixe. Dans l’ordre toocollect hello informations modèle hello de toopass en tant que paramètres, ouvrir le fichier de modèle hello (cette rubrique comprend un modèle inline, ci-dessous) et examiner hello **paramètres** valeurs.

Dans ce cas, modèle hello ci-dessous vous demandera :

* Un nom de compte de stockage unique.
* Un nom d’utilisateur admin hello machine virtuelle.
* Un mot de passe.
* Un nom de domaine pour hello world toouse à l’extérieur.
* Un numéro de version Ubuntu Server, mais accepte uniquement l’un de ceux répertoriés dans une liste.

En savoir plus sur les [conditions requises pour les noms d’utilisateur et les mots de passe](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).

Une fois que vous décidez de ces valeurs, vous êtes prêt toocreate un groupe pour et déployez ce modèle dans votre abonnement Azure.

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

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a>Étape 2 : Créer un ordinateur virtuel de hello à l’aide du modèle de hello
Une fois que vous avez vos valeurs de paramètre prêt, vous devez créer un groupe de ressources pour votre déploiement de modèle et ensuite déployer le modèle de hello.

groupe de ressources toocreate hello, type `azure group create <group name> <location>` par nom de hello du groupe hello et l’emplacement de centre de données hello dans lequel vous souhaitez toodeploy. Le processus est rapide :

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

Déploiement de hello toocreate maintenant, appelez `azure group deployment create` et passer :

* fichier de modèle Hello (si vous avez enregistré hello au-dessus de fichier local tooa de modèle JSON).
* Un modèle URI (si vous voulez toopoint au fichier hello dans GitHub ou une autre adresse web).
* groupe de ressources Hello dans lequel vous souhaitez toodeploy.
* Un nom pour le déploiement (facultatif).

Vous seront demandées toosupply hello de paramètres dans la section « Paramètres » de hello du fichier JSON de hello. Lorsque vous avez spécifié toutes les valeurs de paramètre hello, votre déploiement commence.

Voici un exemple :

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

Vous recevrez hello suivant le type d’informations :

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


## <a id="create-a-custom-vm-image"></a>Tâche : Créer une image de machine virtuelle personnalisée
Vous avez déjà vu l’utilisation de base hello de modèles ci-dessus, par conséquent, nous pouvons maintenant utiliser similaire instructions toocreate une machine virtuelle personnalisée à partir d’un fichier .vhd spécifique dans Azure à l’aide d’un modèle via hello CLI d’Azure. Hello différence est que ce modèle crée un seul ordinateur virtuel à partir d’un disque dur virtuel (VHD) spécifié.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Étape 1 : Examiner le fichier JSON de hello pour le modèle de hello
Voici le contenu hello du fichier JSON hello modèle hello cette section utilise comme exemple. (modèle de hello se trouve également dans [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)

Là encore, vous devez toofind hello valeurs tooenter pour les paramètres hello qui n’ont pas de valeurs par défaut. Lorsque vous exécutez hello `azure group deployment create` hello CLI d’Azure vous invite à vous tooenter ces valeurs de la commande.

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

### <a name="step-2-obtain-hello-vhd"></a>Étape 2 : Obtenir hello disque dur virtuel
Évidemment, vous aurez besoin d’un fichier .vhd pour cela. Vous pouvez utiliser un fichier dont vous disposez dans Azure ou en télécharger un.

Pour un ordinateur virtuel basé sur Windows, consultez [création et téléchargement d’un disque dur virtuel de Windows Server de tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Pour une machine virtuelle Linux, consultez [création et chargement d’un disque dur virtuel qui contient le système d’exploitation de Linux hello](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a>Étape 3 : Créer un ordinateur virtuel de hello à l’aide du modèle de hello
Vous êtes maintenant prêt toocreate un nouvel ordinateur virtuel basé sur le disque dur virtuel hello. Créer un toodeploy de groupe, à l’aide de `azure group create <location>`:

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

Puis créez le déploiement de hello à l’aide de hello `--template-uri` toocall option dans le modèle hello directement (ou vous pouvez utiliser hello `--template-file` option toouse un fichier que vous avez enregistré localement). Notez que le modèle de hello ayant des valeurs par défaut spécifiées, vous êtes invité uniquement quelques points. Si vous déployez le modèle hello dans des emplacements différents, vous découvrirez peut-être que certains conflits d’affectation de noms se produisent avec les valeurs par défaut hello (en particulier les nom DNS de hello sont crées).

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

Sortie se présente comme hello suivantes :

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

## <a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Tâche : Déployer une application de plusieurs machines virtuelles utilisant un réseau virtuel et un équilibreur de charge externe
Ce modèle vous permet de toocreate deux machines virtuelles sous un équilibreur de charge et configurer une règle d’équilibrage de charge sur le Port 80. Il déploie également un compte de stockage, un réseau virtuel, une adresse IP publique, un groupe à haute disponibilité et des interfaces réseau.

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

Suivez ces étapes de toodeploy une application multi-VM qui utilise un réseau virtuel et un équilibrage de charge à l’aide d’un modèle de gestionnaire de ressources dans le référentiel de modèle GitHub hello via les commandes Azure PowerShell.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Étape 1 : Examiner le fichier JSON de hello pour le modèle de hello
Voici le contenu de hello du fichier JSON de hello pour le modèle de hello. Si vous souhaitez que la version la plus récente hello, elle est située [au référentiel GitHub de hello pour les modèles](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json). Cette rubrique utilise hello `--template-uri` toocall de commutateur dans le modèle de hello, mais vous pouvez également utiliser hello `--template-file` toopass une version locale de basculer.

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

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a>Étape 2 : Créer un déploiement de hello à l’aide du modèle de hello
Créer un groupe de ressources pour le modèle de hello à l’aide de `azure group create <location>`. Ensuite, créez un déploiement dans ce groupe de ressources à l’aide de `azure group deployment create` et en passant le groupe de ressources hello, en passant un nom de déploiement et répondre aux invites de hello pour les paramètres dans le modèle hello qui n’avait pas de valeurs par défaut.

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

À présent utiliser hello `azure group deployment create` commande et hello `--template-uri` modèle d’option toodeploy hello. Préparez-vous à renseigner les invites relatives aux valeurs de paramètres, comme indiqué ci-dessous.

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

Notez que ce modèle déploie une image Windows Server ; toutefois, vous pouvez facilement la remplacer par n’importe quelle image Linux. Vous souhaitez toocreate un cluster de Docker avec plusieurs gestionnaires essaim ? [Vous pouvez le faire](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).

## <a id="remove-a-resource-group"></a>Tâche : Supprimer un groupe de ressources
N’oubliez pas que vous pouvez redéployer le groupe de ressources tooa, mais si vous avez terminé avec l’un, vous pouvez le supprimer à l’aide de `azure group delete <group name>`.

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <a id="show-the-log-for-a-resource-group-deployment"></a>Tâche : Afficher le journal de hello pour un déploiement de groupe de ressources
Cette tâche est courante lors de la création ou de l’utilisation de modèles. déploiement de hello Hello appel toodisplay journaux pour un groupe est `azure group log show <groupname>`, qui affiche un peu de qui est utiles pour comprendre pourquoi quelque chose s’est produite, ou n’a pas d’informations. (Pour plus d’informations sur la résolution des problèmes de vos déploiements, mais aussi pour obtenir des informations supplémentaires sur les problèmes, consultez l’article [Résolution des erreurs courantes dans des déploiements Azure avec Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md).)

échecs de tootarget spécifique, vous pouvez utiliser des outils tels que, par exemple, **jq** choses tooquery un peu plus précisément, tels que les échecs, vous devez toocorrect. Hello exemple suivant utilise **jq** tooparse ouvrir une session pour un déploiement **lbgroup**, qui recherchent des échecs.

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
Vous pouvez découvrir très rapidement ce qui pose problème, le corriger et recommencer. Bonjour suivant le cas, le modèle de hello avait été création deux machines virtuelles au hello même temps, ce qui a créé un verrou sur le disque dur virtuel hello. (Une fois que nous avons modifié le modèle de hello, hello déploiement réussi rapidement.)

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <a id="display-information-about-a-virtual-machine"></a>Tâche : Afficher les informations relatives à une machine virtuelle
Vous pouvez voir des informations sur les machines virtuelles spécifiques dans votre groupe de ressources à l’aide de hello `azure vm show <groupname> <vmname>` commande. Si vous avez plusieurs machines virtuelles dans votre groupe, vous devrez peut-être tout d’abord hello toolist machines virtuelles dans un groupe à l’aide de `azure vm list <groupname>`.

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

Ensuite, recherchez myVM1 :

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
> Si vous voulez tooprogrammatically magasin manipuler la sortie hello de vos commandes de la console, vous souhaiterez toouse une analyse de JSON outil tel que  **[jq](https://github.com/stedolan/jq)**  ou  **[jsawk](https://github.com/micha/jsawk)** , ou les bibliothèques de langue qui sont bons pour la tâche hello.
>
>

## <a id="log-on-to-a-linux-based-virtual-machine"></a>Tâche : Ouvrez une session sur l’ordinateur virtuel de basés sur Linux tooa
En règle générale, les ordinateurs Linux sont connecté toothrough SSH. Pour plus d’informations, consultez [comment toouse SSH avec Linux sur Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a id="stop-a-virtual-machine"></a>Tâche : Arrêter une machine virtuelle
Exécutez cette commande :

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> Utilisez ce paramètre tookeep hello adresse IP virtuelle (VIP) du réseau virtuel de hello en cas de hello dernier ordinateur virtuel dans ce réseau virtuel. <br><br> Si vous utilisez hello `StayProvisioned` paramètre, vous serez toujours facturé pour hello machine virtuelle.
>
>

## <a id="start-a-virtual-machine"></a>Tâche : Démarrer une machine virtuelle
Exécutez cette commande :

```azurecli
azure vm start <group name> <virtual machine name>
```

## <a id="attach-a-data-disk"></a>Tâche : Associer un disque de données
Vous devez également toodecide si tooattach un nouveau disque ou un qui contient des données. Pour un nouveau disque, commande hello crée le fichier .vhd de hello et l’attache Bonjour même commande.

tooattach un nouveau disque, exécutez la commande suivante :

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

tooattach un disque de données existant, exécutez la commande suivante :

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

Vous devez le disque toomount hello, comme vous le feriez normalement dans Linux.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’exemples d’utilisation de CLI d’Azure avec hello **arm** mode, consultez [Using hello CLI d’Azure pour Mac, Linux et Windows avec Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md). toolearn en savoir plus sur les ressources Azure et les concepts associés, consultez [vue d’ensemble du Gestionnaire de ressources Azure](../articles/azure-resource-manager/resource-group-overview.md).

Pour plus d’informations sur les autres modèles utilisables, consultez les articles [Modèles de démarrage rapide Microsoft Azure](https://azure.microsoft.com/documentation/templates/) et [Infrastructures d’application utilisant des modèles](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
