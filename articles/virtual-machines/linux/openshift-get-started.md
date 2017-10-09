---
title: aaaDeploy OpenShift origine tooAzure | Documents Microsoft
description: "Découvrez les machines virtuelles de toodeploy OpenShift origine tooAzure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>Déployer OpenShift origine tooAzure Machines virtuelles 

[OpenShift Origin](https://www.openshift.org/) est une plateforme de conteneurs open source basée sur [Kubernetes](https://kubernetes.io/). Il simplifie hello déploiement, mise à l’échelle et l’exploitation des applications mutualisées. 

Ce guide décrit comment toodeploy OpenShift origine sur l’utilisation de Machines virtuelles Azure hello CLI d’Azure et les modèles du Gestionnaire de ressources Azure. Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un toomanage KeyVault clés SSH pour le cluster de OpenShift hello.
> * Déployer un cluster OpenShift sur les machines virtuelles Azure. 
> * Installer et configurer hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) cluster hello de toomanage.
> * Personnalisez le déploiement de OpenShift hello.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

Ce démarrage rapide nécessite hello CLI d’Azure version 2.0.8 ou version ultérieure. version de hello toofind, exécutez `az --version`. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure 
Connectez-vous tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran ou cliquez sur **essayez-la** toouse Shell de Cloud.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>Créer un coffre de clés
Créer des clés SSH pour le cluster de hello un Bonjour de toostore KeyVault avec hello [az keyvault créer](/cli/azure/keyvault#create) commande.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>Création d’une clé SSH 
Une clé SSH n’est nécessaire toosecure accès toohello cluster d’origine de OpenShift. Créer une paire de clés SSH à l’aide de hello `ssh-keygen` commande. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> Hello paire de clés SSH vous créez ne doit pas avoir un mot de passe.

Pour plus d’informations sur les clés SSH sur Windows, [comment toocreate SSH clés sur Windows](/azure/virtual-machines/linux/ssh-from-windows).

## <a name="store-ssh-private-key-in-key-vault"></a>Stocker la clé privée SSH dans Key Vault
Hello OpenShift déploiement utilise la clé SSH hello vous avez créé à l’accès toosecure toohello OpenShift master. tooenable hello déploiement toosecurely de récupérer la clé SSH hello, stocker la clé de hello dans le coffre de clés à l’aide de hello commande suivante.

# <a name="enabled-for-template-deployment"></a>Activé pour le déploiement de modèle
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>Créer un principal du service 
OpenShift communique avec Azure à l’aide d’un nom d’utilisateur et d’un mot de passe ou d’un principal de service. Un principal de service Azure est une identité de sécurité que vous pouvez utiliser avec des applications, des services et des outils d’automatisation comme OpenShift. Contrôler et de définir des autorisations de hello comme principal du service hello toowhat opérations réalisables dans Azure. sécurité tooimprove simplement en fournissant un nom d’utilisateur et un mot de passe, cet exemple crée un service de base principale.

Créer un service principal avec [az ad sp créer-de-rbac](/cli/azure/ad/sp#create-for-rbac) et informations d’identification de hello sortie OpenShift doit :

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Prenez note de la propriété d’appId hello retournée à partir de la commande hello.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > Ne créez pas un mot de passe non sécurisé.  Suivez les conseils en matière de [Stratégies et restrictions de mot de passe dans Azure Active Directory](/azure/active-directory/active-directory-passwords-policy).

Pour plus d’informations sur les principaux de service, consultez [Créer un principal du service avec Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli).

## <a name="deploy-hello-openshift-origin-template"></a>Déployer hello modèle d’origine de OpenShift
Vous allez maintenant déployer OpenShift Origin à l’aide d’un modèle Azure Resource Manager. 

> [!NOTE] 
> commande suivante Hello requiert az CLI 2.0.8 ou version ultérieure. Vous pouvez vérifier hello az CLI version avec hello `az --version` commande. tooupdate hello version CLI, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).

Hello d’utilisation `appId` valeur à partir de principal du service hello créé précédemment pour hello `aadClientId` paramètre.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
déploiement de Hello peut prendre jusqu'à too20 minutes toocomplete. Hello URL de console de OpenShift hello et le nom DNS de hello OpenShift maître est imprimé toohello terminal lorsque hello déploiement est terminé.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Se connecter toohello OpenShift cluster
Lorsque hello déploiement terminé, connecter la console de OpenShift toohello à l’aide du navigateur hello à l’aide de hello `OpenShift Console Uri`. Ou bien, vous pouvez vous connecter principale de OpenShift toohello à l’aide de hello commande suivante.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>Supprimer des ressources
Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, OpenShift cluster et toutes les ressources de la commande.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à effectuer les opérations suivantes :
> [!div class="checklist"]
> * Créer un toomanage KeyVault clés SSH pour le cluster de OpenShift hello.
> * Déployer un cluster OpenShift sur les machines virtuelles Azure. 
> * Installer et configurer hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) cluster hello de toomanage.

Maintenant que le cluster OpenShift Origin est déployé, Vous pouvez suivre comment OpenShift didacticiels toolearn toodeploy votre première application et utilisez hello OpenShift outils. Consultez [prise en main d’origine de OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget a démarré. 
