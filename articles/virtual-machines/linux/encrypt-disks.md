---
title: disques aaaEncrypt sur un VM Linux dans Azure | Documents Microsoft
description: "Comment tooencrypt des disques virtuels sur un Linux VM pour à l’aide de la sécurité renforcée hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>Comment tooencrypt des disques virtuels sur un VM Linux
Pour renforcer la sécurité et la conformité de la machine virtuelle, les disques virtuels dans Azure peuvent être chiffrés. Les disques sont chiffrés à l’aide de clés de chiffrement sécurisées dans un coffre de clés Azure. Vous contrôlez ces clés de chiffrement et pouvez effectuer un audit de leur utilisation. Cet article décrit en détail comment tooencrypt des disques virtuels sur un VM Linux à l’aide de hello Azure CLI 2.0. Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Commandes rapides
Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section base commandes tooencrypt disques virtuels présents sur votre machine virtuelle. Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#overview-of-disk-encryption).

Vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login). Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *myKey* et *myVM*.

Tout d’abord, activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure avec [Registre du fournisseur az](/cli/azure/provider#register) et créer un groupe de ressources avec [az groupe créer](/cli/azure/group#create). Hello exemple suivant crée un nom de groupe de ressources *myResourceGroup* Bonjour *eastus* emplacement :

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Créer un coffre de clés Azure avec [az keyvault créer](/cli/azure/keyvault#create) et activer hello coffre de clés pour une utilisation avec le chiffrement de disque. Spécifiez un nom de Key Vault unique pour *keyvault_name* comme suit :

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Créez une clé de chiffrement dans le coffre Key Vault avec [az keyvault key create](/cli/azure/keyvault/key#create). Hello exemple suivant crée une clé nommée *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Créez un principal de service à l’aide d’Azure Active Directory avec [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). handles de principal de service Hello hello authentification et l’échange de clés de chiffrement à partir du coffre de clés. Bonjour à l’exemple suivant lit dans les valeurs hello principal du service hello Id et mot de passe utilisé dans les commandes ultérieures :

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

mot de passe Hello est de sortie uniquement lorsque vous créez hello principal du service. Si vous le souhaitez, afficher et enregistrer hello mot de passe (`echo $sp_password`). Vous pouvez répertorier vos principaux de service avec [az ad sp list](/cli/azure/ad/sp#list) et afficher des informations supplémentaires sur un principal de service spécifique avec [az ad sp show](/cli/azure/ad/sp#show).

Définissez des autorisations sur votre Key Vault avec [az keyvault set-policy](/cli/azure/keyvault#set-policy). Dans l’exemple suivant de hello, hello ID du principal de service est fournie par hello précédant la commande :

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Créez une machine virtuelle avec [az vm create](/cli/azure/vm#create) et attachez un disque de données de 5 Go. Seules certaines images Marketplace prennent en charge le chiffrement de disque. Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide un **CentOS 7.2n** image :

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` indiqué dans la sortie de hello Hello précédant la commande. Créer une partition et le système de fichiers, puis monter le disque de données hello. Pour plus d’informations, consultez [connecter tooa nouveau disque Linux VM toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Fermez votre session SSH.

Chiffrez votre machine virtuelle avec [az vm encryption enable](/cli/azure/vm/encryption#enable). exemple Hello utilise hello `$sp_id` et `$sp_password` variables hello précédent `ad sp create-for-rbac` commande :

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Il prend un certain temps pour toocomplete de processus de chiffrement de disque hello. Surveiller l’état de hello du processus hello avec [afficher de chiffrement de machine virtuelle az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Hello état montre **EncryptionInProgress**. Attendez que l’état de hello pour les rapports de disque du système d’exploitation de hello **VMRestartPending**, puis redémarrez votre machine virtuelle avec [redémarrage de machine virtuelle az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

processus de chiffrement de disque Hello est finalisé pendant le processus de démarrage hello, par conséquent, attendez quelques minutes avant de vérifier l’état de hello du chiffrement à l’aide de **afficher de chiffrement de machine virtuelle az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

rapport d’état de Hello doit maintenant disque de hello du système d’exploitation et de disque de données en tant que **Encrypted**.

## <a name="overview-of-disk-encryption"></a>Présentation du chiffrement de disque
Les disques virtuels sur des machines virtuelles Linux sont chiffrés au repos à l’aide de la commande [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Le chiffrement de disques virtuels dans Azure n’entraîne aucun frais. Clés de chiffrement sont stockées dans le coffre de clés Azure à l’aide du logiciel de protection, ou vous pouvez importer ou générer vos clés dans des Modules de sécurité matériel (HSM) certifié tooFIPS normes de niveau 2 140-2. Vous gardez le contrôle de ces clés de chiffrement et pouvez effectuer un audit de leur utilisation. Ces clés de chiffrement sont utilisé tooencrypt et déchiffrement tooyour de disques virtuels attachés machine virtuelle. Un principal de service Azure Active Directory fournit un mécanisme sécurisé pour l’émission de ces clés de chiffrement lors de la mise sous tension et hors tension des machines virtuelles.

processus de Hello de chiffrement d’une machine virtuelle est la suivante :

1. Créez une clé de chiffrement dans un coffre de clés Azure.
2. Configurer hello chiffrement clé toobe utilisable pour le chiffrement des disques.
3. clé de chiffrement hello tooread de hello Azure Key Vault, créez un service Azure Active Directory principal avec les autorisations appropriées hello.
4. Émettre hello commande tooencrypt vos disques virtuels, en spécifiant le principal du service Azure Active Directory hello et appropriée toobe de clés cryptographique utilisé.
5. demandes principales du service Azure Active Directory Hello hello clé de chiffrement requis à partir d’Azure Key Vault.
6. les disques virtuels Hello sont chiffrées à l’aide de la clé de chiffrement hello fourni.

## <a name="encryption-process"></a>Processus de chiffrement
Chiffrement de disque s’appuie sur hello suivant des composants supplémentaires :

* **Azure Key Vault** -utilisé toosafeguard les clés de chiffrement et les secrets utilisés pour le processus de chiffrement/déchiffrement de disque hello.
  * Le cas échéant, vous pouvez utiliser un coffre de clés Azure existant. Vous n’avez pas de le toodedicate un disques tooencrypting de coffre de clés.
  * les limites administratives tooseparate et la visibilité de clé, vous pouvez créer un coffre de clés dédié.
* **Azure Active Directory** - handles hello échange sécurisé de clés de chiffrement requis et l’authentification pour demandé d’actions.
  * Vous pouvez généralement utiliser une instance Azure Active Directory existante pour héberger votre application.
  * principal du service Hello fournit un mécanisme sécurisé de toorequest et être émis des clés de chiffrement appropriées hello. Vous ne développez pas de réelle application qui s’intègre à Azure Active Directory.

## <a name="requirements-and-limitations"></a>Spécifications et limitations
Configuration requise et scénarios pris en charge pour le chiffrement de disque :

* Hello suivant serveur Linux SKU - Ubuntu, CentOS, SUSE et SUSE Linux Enterprise Server (SLES) et Red Hat Enterprise Linux.
* Toutes les ressources (telles que le coffre de clés, le compte de stockage et machine virtuelle) doivent être Bonjour même région Azure et abonnement.
* Machines virtuelles standard des séries A, D, DS, G et GS.

Chiffrement de disque n’est pas pris en charge dans hello les scénarios suivants :

* Machines virtuelles de niveau de base.
* Machines virtuelles créées à l’aide du modèle de déploiement classique hello.
* Désactivation du chiffrement de disque du système d’exploitation sur les machines virtuelles Linux.
* Mise à jour des clés de chiffrement hello sur une VM Linux déjà chiffré.

## <a name="create-azure-key-vault-and-keys"></a>Créer le coffre de clés Azure et les clés
Vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login). Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Les noms de paramètre sont par exemple *myResourceGroup*, *myKey* et *myVM*.

première étape de Hello est toocreate un toostore Azure Key Vault vos clés de chiffrement. Coffre de clés Azure peuvent stocker des clés, des secrets, ou les mots de passe qui vous permettent de toosecurely leur implémentent dans vos applications et services. Pour le chiffrement de disque virtuel, vous utilisez le coffre de clés toostore une clé de chiffrement qui est utilisé tooencrypt ou déchiffrer vos disques virtuels.

Activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure avec [Registre du fournisseur az](/cli/azure/provider#register) et créer un groupe de ressources avec [az groupe créer](/cli/azure/group#create). Hello exemple suivant crée un nom de groupe de ressources *myResourceGroup* Bonjour `eastus` emplacement :

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Bonjour Azure Key Vault contenant hello clés de chiffrement et calcul associée ressources telles que le stockage et hello machine virtuelle proprement dite doivent résider dans hello même région. Créer un coffre de clés Azure avec [az keyvault créer](/cli/azure/keyvault#create) et activer hello coffre de clés pour une utilisation avec le chiffrement de disque. Spécifiez un nom de Key Vault unique pour *keyvault_name* comme suit :

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Vous pouvez stocker des clés de chiffrement à l’aide d’une protection logicielle ou HSM (modèle de sécurité matériel). L’utilisation d’une protection HSM nécessite un coffre de clés Premium. Il est un toocreating coût supplémentaire un coffre de clés plutôt que le coffre de clés standard qui stocke les clés protégées par logiciel. toocreate un coffre de clés, premium Bonjour précédant l’étape ajouter `--sku Premium` toohello commande. Hello exemple suivant utilise des clés de protection logicielle étant donné que nous avons créé un coffre de clés standard.

Les modèles de protection, hello plateforme Azure doit toobe accordé accès toorequest les clés de chiffrement hello lorsque hello machine virtuelle démarre les disques virtuels toodecrypt hello. Créez une clé de chiffrement dans le coffre Key Vault avec [az keyvault key create](/cli/azure/keyvault/key#create). Hello exemple suivant crée une clé nommée *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Créer hello principal du service Azure Active Directory
Lorsque les disques virtuels sont chiffrées ou déchiffrées, vous spécifiez une authentification hello toohandle des comptes et l’échange de clés de chiffrement à partir du coffre de clés. Ce compte, un principal du service Azure Active Directory, permet de clés de chiffrement approprié hello pour le compte hello VM toorequest de plateforme Windows Azure hello. Une instance Azure Active Directory par défaut est disponible dans votre abonnement, bien que de nombreuses organisations utilisent des répertoires Azure Active Directory dédiés.

Créez un principal de service à l’aide d’Azure Active Directory avec [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac). Bonjour à l’exemple suivant lit dans les valeurs hello principal du service hello Id et mot de passe utilisé dans les commandes ultérieures :

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

mot de passe Hello s’affiche uniquement lorsque vous créez un service de hello principal. Si vous le souhaitez, afficher et enregistrer hello mot de passe (`echo $sp_password`). Vous pouvez répertorier vos principaux de service avec [az ad sp list](/cli/azure/ad/sp#list) et afficher des informations supplémentaires sur un principal de service spécifique avec [az ad sp show](/cli/azure/ad/sp#show).

toosuccessfully chiffrer ou déchiffrer des disques virtuels, les autorisations sur la clé de chiffrement hello stockées dans le coffre de clés doivent être principal tooread hello clés du service Azure Active Directory définies toopermit hello. Définissez des autorisations sur votre Key Vault avec [az keyvault set-policy](/cli/azure/keyvault#set-policy). Dans l’exemple suivant de hello, hello ID du principal de service est fournie par hello précédant la commande :

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Create virtual machine
tooactually chiffrer certains disques virtuels, vous permet de créer une machine virtuelle et ajoutez un disque de données. Créer un tooencrypt de machine virtuelle avec [az vm créer](/cli/azure/vm#create) et attacher un disque de données de 5 Go. Seules certaines images Marketplace prennent en charge le chiffrement de disque. Hello exemple suivant crée un ordinateur virtuel nommé *myVM* à l’aide un **CentOS 7.2n** image :

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH à l’aide de machine virtuelle tooyour hello `publicIpAddress` indiqué dans la sortie de hello Hello précédant la commande. Créer une partition et le système de fichiers, puis monter le disque de données hello. Pour plus d’informations, consultez [connecter tooa nouveau disque Linux VM toomount hello](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Fermez votre session SSH.


## <a name="encrypt-virtual-machine"></a>Chiffrement d’une machine virtuelle
disques virtuels de tooencrypt hello, vous réunissez tous les composants précédents hello :

1. Spécifiez hello principal du service Azure Active Directory et le mot de passe.
2. Spécifier des métadonnées de hello toostore hello coffre de clés pour vos disques chiffrés.
3. Spécifiez toouse de clés de chiffrement hello pour chiffrement hello et le déchiffrement.
4. Spécifier si vous souhaitez disque hello du système d’exploitation de tooencrypt, des disques de données hello ou tous.

Chiffrez votre machine virtuelle avec [az vm encryption enable](/cli/azure/vm/encryption#enable). exemple Hello utilise hello `$sp_id` et `$sp_password` variables hello précédent `ad sp create-for-rbac` commande :

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Il prend un certain temps pour toocomplete de processus de chiffrement de disque hello. Surveiller l’état de hello du processus hello avec [afficher de chiffrement de machine virtuelle az](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Hello de sortie est tronquée exemple après la toohello similaire :

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Attendez que l’état de hello pour les rapports de disque du système d’exploitation de hello **VMRestartPending**, puis redémarrez votre machine virtuelle avec [redémarrage de machine virtuelle az](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

processus de chiffrement de disque Hello est finalisé pendant le processus de démarrage hello, par conséquent, attendez quelques minutes avant de vérifier l’état de hello du chiffrement à l’aide de **afficher de chiffrement de machine virtuelle az**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

rapport d’état de Hello doit maintenant disque de hello du système d’exploitation et de disque de données en tant que **Encrypted**.


## <a name="add-additional-data-disks"></a>Ajouter des disques de données supplémentaires
Une fois que vous avez chiffré vos disques de données, vous pouvez ajouter ultérieurement des disques virtuels tooyour machine virtuelle et également de les chiffrer. Par exemple, vous permet d’ajouter un deuxième tooyour de disque virtuel VM, comme suit :

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Exécuter à nouveau les disques virtuels hello commande tooencrypt hello comme suit :

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la gestion du coffre de clés Azure, y compris la suppression des clés de chiffrement et des coffres, consultez [Gérer le coffre de clés à l’aide de l’interface de ligne de commande](../../key-vault/key-vault-manage-with-cli2.md).
* Pour plus d’informations sur le chiffrement de disque, telles que la préparation d’une tooAzure tooupload machine virtuelle personnalisée chiffré, consultez [chiffrement de disque Azure](../../security/azure-security-disk-encryption.md).
