---
title: "FEU d’aaaDeploy sur un ordinateur virtuel de Linux dans Azure | Documents Microsoft"
description: "Découvrez comment tooinstall hello feu de pile sur un VM Linux dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a>Déployer une pile LAMP dans Azure
Cet article vous guide tout au long de comment toodeploy un Apache web server, MySQL et PHP (pile de feu hello) sur Azure. Vous avez besoin d’un compte Azure ([obtenir une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/)) et hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2). Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-command-summary"></a>Résumé des commandes rapides

1. Enregistrer et modifier hello [azuredeploy.parameters.json fichier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) préférence tooyour sur votre ordinateur local.
2. Exécutez hello suivant deux commandes toocreate un groupe de ressources et ensuite déployer votre modèle :

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a>Déploiement de LAMP sur une machine virtuelle existante
suivant de Hello packages de mises à jour des commandes, puis installe Apache, MySQL et PHP :

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Procédure pas à pas de déploiement de LAMP sur une nouvelle machine virtuelle

1. Créer un groupe de ressources avec [création de groupe de az](/cli/azure/group#create) toocontain hello nouvelle machine virtuelle :

```azurecli
az group create -l westus -n myResourceGroup
```
toocreate hello machine virtuelle proprement dite, vous pouvez utiliser un modèle Azure Resource Manager déjà écrite [ici sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

2. Enregistrer hello [azuredeploy.parameters.json fichier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour les ordinateur local.
3. Modifier hello **azuredeploy.parameters.json** tooyour de fichier par défaut des entrées.
4. Déployer le modèle hello avec [création du déploiement d’un groupe az] référençant hello téléchargé fichier json :

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

Hello la sortie est similaire toohello l’exemple suivant :

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

Vous avez maintenant créé une machine virtuelle Linux avec LAMP déjà installé. Si vous le souhaitez, vous pouvez vérifier l’installation de hello en sautant trop bas[vérifier feu installé avec succès](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Procédure pas à pas de déploiement de LAMP sur une machine virtuelle existante
Si vous avez besoin d’aide pour créer une VM Linux, vous pouvez head [toolearn ici comment toocreate un VM Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli). Ensuite, vous devez tooSSH dans hello Linux VM. Si vous avez besoin d’aide sur la création d’une clé SSH, vous pouvez head [toolearn ici comment toocreate une clé SSH sur Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Si vous disposez déjà d’une clé SSH, continuez et ouvrez en ligne de commande une connexion SSH à votre machine virtuelle Linux avec `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.

Maintenant que vous utilisez dans votre VM Linux, nous pouvons guider dans l’installation de la pile de feu hello sur les distributions Debian. les commandes exactes Hello peuvent différer pour les autres versions de Linux.

#### <a name="installing-on-debianubuntu"></a>Installation sur Debian/Ubuntu
Vous devez hello suivant des packages installés : `apache2`, `mysql-server`, `php5`, et `php5-mysql`. Vous pouvez les installer directement à partir de ces packages ou à l’aide de Tasksel.
Avant d’installer, vous devez toodownload et mettre à jour les listes de package.

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a>Packages individuels
Utilisation d’apt-get :

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a>Utilisation de Tasksel
Vous pouvez également télécharger Tasksel, un outil Debian/Ubuntu qui installe plusieurs packages connexes en tant que tâche coordonnée sur votre système.

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

Après l’exécution d’une des options précédentes de hello, vous allez être invité à tooinstall ces packages et divers autres dépendances. tooset un mot de passe d’administration pour MySQL, appuyez sur « y », puis sur 'Entrée' toocontinue, suivez toutes les invites. Ce processus installe hello minimale requise PHP les extensions nécessitées toouse PHP avec MySQL. 

![][1]

Exécutez hello suivant commande toosee autres extensions PHP disponibles sous forme de packages :

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a>Création d’un document info.php
Vous devez maintenant être en mesure de toocheck quelle version de PHP, MySQL et Apache vous avez via la ligne de commande hello en tapant `apache2 -v`, `mysql -v`, ou `php -v`.

Si vous devez comme tootest en outre, vous pouvez créer un tooview de page PHP info rapide dans un navigateur. Créez un fichier avec l’éditeur de texte Nano à l’aide de la commande suivante :

```bash
sudo nano /var/www/html/info.php
```

Dans l’éditeur de texte hello GNU Nano, ajoutez hello lignes suivantes :

```php
<?php
phpinfo();
?>
```

Ensuite, enregistrez et quittez l’éditeur de texte hello.

Redémarrez Apache avec cette commande pour que toutes les nouvelles installations prennent effet.

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a>Vérification de l’installation correcte de LAMP
Vous pouvez maintenant vérifier vous avez créé en ouvrant un navigateur et allez toohttp://youruniqueDNS/info.php page des informations hello PHP. Il doit se présenter une image toothis similaire.

![][2]

Vous pouvez vérifier votre installation Apache en consultant hello Apache2 Ubuntu par défaut Page en accédant tooyou http://youruniqueDNS/. Hello la sortie est similaire toohello l’exemple suivant :

![][3]

Félicitations, vous avez configuré une pile LAMP sur votre machine virtuelle Azure !

## <a name="next-steps"></a>Étapes suivantes
Consultez hello documentation Ubuntu sur la pile de feu hello :

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
