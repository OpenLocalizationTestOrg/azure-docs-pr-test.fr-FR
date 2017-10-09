---
title: disques aaaEncrypt sur un VM Linux avec hello Azure CLI 1.0 | Documents Microsoft
description: "Comment un VM Linux à l’aide de disques tooencrypt hello Azure CLI 1.0 et le modèle de déploiement du Gestionnaire de ressources hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Chiffrer les disques sur un VM Linux à l’aide de hello Azure CLI 1.0
Pour renforcer la sécurité et la conformité de la machine virtuelle , les disques virtuels dans Azure peuvent être chiffrés au repos. Les disques sont chiffrés à l’aide de clés de chiffrement sécurisées dans un coffre de clés Azure. Vous contrôlez ces clés de chiffrement et pouvez effectuer un audit de leur utilisation. Cet article décrit en détail comment tooencrypt des disques virtuels sur un VM Linux à l’aide de hello Azure CLI 1.0 et le modèle de déploiement du Gestionnaire de ressources hello.

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

## <a name="quick-commands"></a>Commandes rapides
Si vous avez besoin de tooquickly accomplir la tâche hello, hello suivant hello de détails section base commandes tooencrypt disques virtuels présents sur votre machine virtuelle. Plus d’informations et le contexte de chaque étape se trouve reste hello du document de hello, [Démarrer ici](#overview-of-disk-encryption).

Vous devez hello [dernière Azure CLI 1.0](../../xplat-cli-install.md) installé et connecté à l’aide de mode de gestionnaire de ressources hello comme suit :

```azurecli
azure config mode arm
```

Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs. Exemples de noms de paramètre : `myResourceGroup`, `myKeyVault` et `myVM`.

D’abord activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure et créer un groupe de ressources. Hello exemple suivant crée un nom de groupe de ressources `myResourceGroup` Bonjour `WestUS` emplacement :

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Créez un coffre de clés Azure. Hello exemple suivant crée un coffre de clés nommé `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Créez une clé de chiffrement dans le coffre de clés et activez-la pour le chiffrement du disque. Hello exemple suivant crée une clé nommée `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

Créer un point de terminaison à l’aide d’Azure Active Directory pour la gestion de l’authentification de hello et l’échange de clés de chiffrement à partir du coffre de clés. Hello `--home-page` et `--identifier-uris` n’avez pas besoin d’adresse routable toobe. Hello plus haut niveau de sécurité, les clés secrètes client doivent être utilisés à la place des mots de passe. Hello CLI d’Azure actuellement ne peut pas générer des clés secrètes client. Clés secrètes client ne peuvent pas être générés dans hello portail Azure. Hello exemple suivant crée un point de terminaison Azure Active Directory nommé `myAADApp` et utilise un mot de passe de `myPassword`. Spécifiez votre propre mot de passe comme suit :

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Hello de note `applicationId` indiqué dans la sortie de hello de hello précédant la commande. Cet ID d’application est utilisé dans hello comme suit :

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

Ajouter un tooan de disque de données existante de machine virtuelle. Hello exemple suivant ajoute un tooa de disque de données machine virtuelle nommée `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Passez en revue les détails de hello pour votre clé de coffre de clés et hello que vous avez créé. Vous devez hello ID de clé de coffre, URI et clé de l’URL à l’étape finale de hello. Hello exemple suivant passe en revue les détails de hello pour un coffre de clés nommé `myKeyVault` et la clé nommée `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Chiffrez vos disques comme suit, en entrant vos propres noms de paramètre :

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello CLI d’Azure ne fournit pas des erreurs détaillées au cours du processus de chiffrement hello. Pour obtenir plus d’informations de dépannage, consultez `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`. En tant que hello précédant la commande a plusieurs variables et vous n’obtiendrez pas quantité indication as toowhy hello processus échoue, un exemple de commande complète se présente comme suit :

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Enfin, vérifiez le statut de chiffrement hello à nouveau les tooconfirm que vos disques virtuels ont désormais été chiffrés. exemple Hello vérifie état hello d’un ordinateur virtuel nommé `myVM` Bonjour `myResourceGroup` groupe de ressources :

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>Présentation du chiffrement de disque
Les disques virtuels sur des machines virtuelles Linux sont chiffrés au repos à l’aide de la commande [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Le chiffrement de disques virtuels dans Azure n’entraîne aucun frais. Clés de chiffrement sont stockées dans le coffre de clés Azure à l’aide du logiciel de protection, ou vous pouvez importer ou générer vos clés dans des Modules de sécurité matériel (HSM) certifié tooFIPS normes de niveau 2 140-2. Vous gardez le contrôle de ces clés de chiffrement et pouvez effectuer un audit de leur utilisation. Ces clés de chiffrement sont utilisé tooencrypt et déchiffrement tooyour de disques virtuels attachés machine virtuelle. Un point de terminaison Azure Active Directory fournit un mécanisme sécurisé pour l’émission de ces clés de chiffrement lors de la mise sous tension et hors tension des machines virtuelles.

processus de Hello de chiffrement d’une machine virtuelle est la suivante :

1. Créez une clé de chiffrement dans un coffre de clés Azure.
2. Configurer hello chiffrement clé toobe utilisable pour le chiffrement des disques.
3. clé de chiffrement hello tooread de hello Azure Key Vault, créez un point de terminaison à l’aide d’Azure Active Directory disposant des autorisations appropriées de hello.
4. Émettre hello commande tooencrypt vos disques virtuels, en spécifiant le point de terminaison de hello Azure Active Directory et appropriée toobe de clés cryptographique utilisé.
5. point de terminaison de Azure Active Directory Hello demande la clé de chiffrement requis hello dans Azure Key Vault.
6. les disques virtuels Hello sont chiffrées à l’aide de la clé de chiffrement hello fourni.

## <a name="supporting-services-and-encryption-process"></a>Services pris en charge et processus de chiffrement
Chiffrement de disque s’appuie sur hello suivant des composants supplémentaires :

* **Azure Key Vault** -utilisé toosafeguard les clés de chiffrement et les secrets utilisés pour le processus de chiffrement/déchiffrement de disque hello.
  * Le cas échéant, vous pouvez utiliser un coffre de clés Azure existant. Vous n’avez pas de le toodedicate un disques tooencrypting de coffre de clés.
  * les limites administratives tooseparate et la visibilité de clé, vous pouvez créer un coffre de clés dédié.
* **Azure Active Directory** - handles hello échange sécurisé de clés de chiffrement requis et l’authentification pour demandé d’actions.
  * Vous pouvez généralement utiliser une instance Azure Active Directory existante pour héberger votre application.
  * application Hello est plus d’un point de terminaison pour hello coffre de clés et de Virtual Machine services toorequest et obtenir émis des clés de chiffrement appropriées hello. Vous ne développez pas de réelle application qui s’intègre à Azure Active Directory.

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

## <a name="create-hello-azure-key-vault-and-keys"></a>Créer hello Azure Key Vault et des clés
suite de hello toocomplete de ce guide, vous devez hello [dernière Azure CLI 1.0](../../xplat-cli-install.md) installé et connecté à l’aide de mode de gestionnaire de ressources hello comme suit :

```azurecli
azure config mode arm
```

Dans l’ensemble des exemples de commandes hello, remplacer tous les paramètres de l’exemple avec votre propre nom, l’emplacement et valeurs de clés. Hello exemples suivants utilisent une convention de `myResourceGroup`, `myKeyVault`, `myAADApp`, etc..

première étape de Hello est toocreate un toostore Azure Key Vault vos clés de chiffrement. Coffre de clés Azure peuvent stocker des clés, des secrets, ou les mots de passe qui vous permettent de toosecurely leur implémentent dans vos applications et services. Pour le chiffrement de disque virtuel, vous utilisez le coffre de clés toostore une clé de chiffrement qui est utilisé tooencrypt ou déchiffrer vos disques virtuels.

Activer le fournisseur de coffre de clés Azure hello dans votre abonnement Azure, puis créer un groupe de ressources. Hello exemple suivant crée un groupe de ressources nommé `myResourceGroup` Bonjour `WestUS` emplacement :

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Bonjour Azure Key Vault contenant hello clés de chiffrement et calcul associée ressources telles que le stockage et hello machine virtuelle proprement dite doivent résider dans hello même région. Hello exemple suivant crée un coffre de clés Azure nommé `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Vous pouvez stocker des clés de chiffrement à l’aide d’une protection logicielle ou HSM (modèle de sécurité matériel). L’utilisation d’une protection HSM nécessite un coffre de clés Premium. Il est un toocreating coût supplémentaire un coffre de clés plutôt que le coffre de clés standard qui stocke les clés protégées par logiciel. toocreate un coffre de clés, premium Bonjour précédant l’étape ajouter `--sku Premium` toohello commande. Hello exemple suivant utilise des clés de protection logicielle étant donné que nous avons créé un coffre de clés standard.

Les modèles de protection, hello plateforme Azure doit toobe accordé accès toorequest les clés de chiffrement hello lorsque hello machine virtuelle démarre les disques virtuels toodecrypt hello. Créez une clé de chiffrement dans votre coffre de clés, puis activez-la afin de l’utiliser pour le chiffrement de disque virtuel. Hello exemple suivant crée une clé nommée `myKey` , puis l’active pour le chiffrement de disque :

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Créer l’application Azure Active Directory de hello
Lorsque les disques virtuels sont chiffrées ou déchiffrées, vous utilisez une authentification de hello toohandle point de terminaison et l’échange de clés de chiffrement à partir du coffre de clés. Ce point de terminaison, une application Azure Active Directory, permet de clés de chiffrement approprié hello pour le compte hello VM toorequest de plateforme Windows Azure hello. Une instance Azure Active Directory par défaut est disponible dans votre abonnement, bien que de nombreuses organisations utilisent des répertoires Azure Active Directory dédiés.

Comme vous ne créez pas une application Azure Active Directory complet, hello `--home-page` et `--identifier-uris` paramètres Bonjour exemple suivant n’est pas nécessaire d’adresse routable toobe. Hello exemple suivant spécifie également un mot de passe secret plutôt que des clés génération à partir de hello portail Azure. En tant que cette fois-ci, génération de clés n’est pas possible de hello CLI d’Azure.

Créez votre application Azure Active Directory. Hello exemple suivant crée une application nommée `myAADApp` et utilise un mot de passe de `myPassword`. Spécifiez votre propre mot de passe comme suit :

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Prenez note de hello `applicationId` qui est retourné dans la sortie de hello par hello précédant la commande. Cet ID d’application est utilisé dans certains hello restant comme suit. Ensuite, créez un nom principal de service (SPN) pour que l’application hello est accessible au sein de votre environnement. toosuccessfully chiffrer ou déchiffrer des disques virtuels, les autorisations sur la clé de chiffrement hello stockées dans le coffre de clés doivent être tooread hello clés d’application Azure Active Directory ensemble toopermit hello.

Créer hello SPN et définissez les autorisations appropriées de hello comme suit :

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>Ajouter un disque virtuel et vérifier l’état de chiffrement
tooactually chiffrer certains disques virtuels, permet d’ajouter un tooan de disque existant de machine virtuelle. Ajouter un tooan de disque de données de 5 Go existante de machine virtuelle comme suit :

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

les disques virtuels Hello ne sont pas actuellement chiffrés. Passez en revue hello état actuel du chiffrement de votre machine virtuelle comme suit :

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>Chiffrer des disques virtuels
toonow chiffrer les disques virtuels hello, vous réunissez tous les composants précédents hello :

1. Spécifiez le mot de passe et l’application d’Azure Active Directory hello.
2. Spécifier des métadonnées de hello toostore hello coffre de clés pour vos disques chiffrés.
3. Spécifiez toouse de clés de chiffrement hello pour chiffrement hello et le déchiffrement.
4. Spécifier si vous souhaitez disque hello du système d’exploitation de tooencrypt, des disques de données hello ou tous.

Permet de consulter les détails de hello pour votre clé Azure Key Vault et hello créé, que vous avez besoin hello ID de coffre de clé, un URI, puis l’URL de clés à l’étape finale de hello :

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Chiffrer vos disques virtuels à l’aide de la sortie de hello de hello `azure keyvault show` et `azure keyvault key show` commandes comme suit :

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Comme hello commande précédente a plusieurs variables, hello exemple suivant est commande complète hello pour référence :

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Hello CLI d’Azure ne fournit pas des erreurs détaillées au cours du processus de chiffrement hello. Pour plus d’informations, consultez `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` sur hello vous chiffrez de machine virtuelle.

Enfin, vous permet de consulter l’état du chiffrement hello à nouveau les tooconfirm que vos disques virtuels ont désormais été chiffrés :

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>Ajouter des disques de données supplémentaires
Une fois que vous avez chiffré vos disques de données, vous pouvez ajouter ultérieurement des disques virtuels tooyour machine virtuelle et également de les chiffrer. Lorsque vous exécutez hello `azure vm enable-disk-encryption` commande, la version de la séquence hello incrément à l’aide de hello `--sequence-version` paramètre. Ce paramètre de version de séquence vous permet de tooperform opérations répétées sur hello même machine virtuelle.

Par exemple, vous permet d’ajouter un deuxième tooyour de disque virtuel VM, comme suit :

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Réexécutez hello commande tooencrypt hello disques virtuels, cette fois Ajout hello `--sequence-version` paramètre et valeur hello incrémentation de notre première exécution comme suit :

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>Étapes suivantes
* Pour plus d’informations sur la gestion du coffre de clés Azure, y compris la suppression des clés de chiffrement et des coffres, consultez [Gérer le coffre de clés à l’aide de l’interface de ligne de commande](../../key-vault/key-vault-manage-with-cli2.md).
* Pour plus d’informations sur le chiffrement de disque, telles que la préparation d’une tooAzure tooupload machine virtuelle personnalisée chiffré, consultez [chiffrement de disque Azure](../../security/azure-security-disk-encryption.md).
