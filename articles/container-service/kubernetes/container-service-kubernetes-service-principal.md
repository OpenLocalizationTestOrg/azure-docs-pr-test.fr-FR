---
title: principal aaaService pour Azure Kubernetes cluster | Documents Microsoft
description: "Créer et gérer un principal de service Azure Active Directory pour un cluster Kubernetes dans Azure Container Service"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Configurer un principal de service Azure Active Directory pour un cluster Kubernetes dans Container Service


Dans le conteneur de Service Azure, un cluster Kubernetes nécessite un [principal du service Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract avec les API d’Azure. Hello principal du service est nécessaire toodynamically gérer les ressources telles que [itinéraires définis par l’utilisateur](../../virtual-network/virtual-networks-udr-overview.md) et hello [équilibrage de charge de couche 4 Azure](../../load-balancer/load-balancer-overview.md). 


Cet article explique tooset différentes options d’un service principal pour votre cluster Kubernetes. Par exemple, si vous avez installé et configuré hello [Azure CLI 2.0](/cli/azure/install-az-cli2), vous pouvez exécuter hello [ `az acs create` ](/cli/azure/acs#create) commande toocreate hello Kubernetes cluster et hello principal du service à hello même temps.


## <a name="requirements-for-hello-service-principal"></a>Configuration requise pour le principal du service hello

Vous pouvez utiliser un principal de service Azure AD existant que répond aux hello suivant les exigences ou créez-en un.

* **Étendue**: groupe de ressources hello dans l’abonnement de hello utilisés cluster de Kubernetes toodeploy hello ou (moins de manière restrictive) abonnement de hello cluster hello de toodeploy.

* **Rôle** : **Collaborateur**

* **Clé secrète client** : doit être un mot de passe. Actuellement, vous ne pouvez pas utiliser de principal du service configuré pour l’authentification par certificat.

> [!IMPORTANT] 
> toocreate un principal de service, vous devez disposer des autorisations tooregister une application avec votre locataire Azure AD et le rôle de tooa tooassign hello application dans votre abonnement. toosee si vous avez les autorisations requises de hello, [archiver hello Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions). 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>Option 1 : créer un principal de service dans Azure Active Directory

Si vous voulez toocreate un principal du service Azure AD avant de déployer votre cluster Kubernetes, Azure fournit plusieurs méthodes. 

Hello suivant des exemples de commandes vous indiquent comment toodo avec hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). Vous pouvez également créer un service principal à l’aide de [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), ou d’autres méthodes.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

La sortie est similaire toohello suivante (présentée ici rédigé) :

![Créer un principal du service](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Mise en surbrillance sont hello **ID client** (`appId`) et hello **clé secrète client** (`password`) que vous utilisez en tant que paramètres de principal de service pour le déploiement de cluster.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Spécifiez le principal du service lors de la création du cluster de Kubernetes hello

Fournir hello **ID client** (également appelé hello `appId`, pour l’ID de l’Application) et **clé secrète client** (`password`) d’un service existant principal en tant que paramètres lorsque vous créez hello Kubernetes cluster. Assurez-vous que le principal du service hello répond aux exigences de hello en hello à partir de cet article.

Vous pouvez spécifier ces paramètres lors du déploiement de cluster de Kubernetes hello à l’aide de hello [Azure Interface de ligne de commande (CLI) 2.0](container-service-kubernetes-walkthrough.md), [portail Azure](../dcos-swarm/container-service-deployment.md), ou d’autres méthodes.

>[!TIP] 
>Lorsque vous spécifiez hello **ID client**, être vraiment toouse hello `appId`, pas hello `ObjectId`, de principal du service hello.
>

Hello suivant montre une façon toopass paramètres hello avec hello Azure CLI 2.0. Cet exemple utilise hello [Kubernetes quickstart modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Télécharger](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) fichier de paramètres de modèle hello `azuredeploy.parameters.json` à partir de GitHub.

2. service de hello toospecify principal, entrez les valeurs de `servicePrincipalClientId` et `servicePrincipalClientSecret` dans le fichier de hello. (Vous devez également tooprovide vos propres valeurs pour `dnsNamePrefix` et `sshRSAPublicKey`. Hello ce dernier est cluster hello de hello SSH tooaccess de clé publique). Enregistrez le fichier de hello.

    ![Transmettez les paramètres du principal du service](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Exécution hello commande suivante, en utilisant `--parameters` tooset hello chemin d’accès toohello azuredeploy.parameters.json fichier. Cette commande déploie cluster hello dans un groupe de ressources que vous créez appelée `myResourceGroup` dans la région ouest des États-Unis hello.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>Option 2 : Générer un principal de service lors de la création de cluster hello avec`az acs create`

Si vous exécutez hello [ `az acs create` ](/cli/azure/acs#create) toocreate de commande hello Kubernetes cluster, vous avez un principal de service hello option toogenerate automatiquement.

Comme avec d’autres options de création de clusters Kubernetes, vous pouvez spécifier des paramètres pour un principal du service existant lorsque vous exécutez `az acs create`. Toutefois, lorsque vous omettez ces paramètres, hello CLI d’Azure crée un automatiquement pour une utilisation avec le Service de conteneur. Cela s’effectue en toute transparence au cours du déploiement de hello. 

Hello commande suivante crée un cluster Kubernetes et génère des clés SSH et les informations d’identification du principal de service :

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Si votre compte ne dispose pas hello Azure AD et abonnement autorisations toocreate un principal de service, commande hello génère une erreur similaire trop`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>Considérations supplémentaires

* Si vous n’avez toocreate d’autorisations à un principal de service dans votre abonnement, vous devrez peut-être tooask votre annuaire Azure AD ou abonnement administrateur tooassign hello des autorisations nécessaires ou demandez-lui un toouse principal de service avec le Service de conteneur Azure. 

* principal du service Hello pour Kubernetes fait partie de la configuration de cluster hello. Toutefois, n’utilisez pas cluster hello de hello identité toodeploy.

* Chaque principal de service est associé à une application Azure AD. Hello principal du service pour un cluster Kubernetes peut être associé à n’importe quel Azure valide nom de l’application Active Directory (par exemple : `https://www.contoso.org/example`). URL de Hello pour une application hello n’a pas un point de terminaison réel toobe.

* Lorsque vous spécifiez principal du service hello **ID Client**, vous pouvez utiliser la valeur hello hello `appId` (comme indiqué dans cet article) ou principal du service correspondant hello `name` (par exemple,`https://www.contoso.org/example`).

* Sur le maître de hello et de machines virtuelles dans un cluster de Kubernetes hello, hello service principal sont stockées dans hello fichier /etc/kubernetes/azure.json.

* Lorsque vous utilisez hello `az acs create` commande principal du service toogenerate hello automatiquement, les informations d’identification de principal hello service sont écrites toohello fichier ~/.azure/acsServicePrincipal.json sur l’ordinateur de hello utilisé toorun hello. 

* Lorsque vous utilisez hello `az acs create` commande principal du service toogenerate hello automatiquement, le principal du service hello peut également authentifier avec un [Registre de conteneur Azure](../../container-registry/container-registry-intro.md) créées Bonjour même abonnement.




## <a name="next-steps"></a>Étapes suivantes

* [Prise en main de Kubernetes](container-service-kubernetes-walkthrough.md) dans votre cluster de service de conteneur.

* tootroubleshoot hello principal du service pour Kubernetes, consultez hello [documentation du moteur de ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).


