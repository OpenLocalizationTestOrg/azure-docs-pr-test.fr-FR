---
title: aaaDeploy un conteneur Docker de cluster dans Azure | Documents Microsoft
description: "Déployer une solution de Kubernetes, contrôleur de domaine/système d’exploitation ou Docker Swarm dans le conteneur de Service Azure à l’aide de hello portail Azure ou un modèle de gestionnaire de ressources."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a>Déployer un conteneur Docker à l’aide de hello portail Azure de solution d’hébergement



Azure Container Service assure le déploiement rapide des principales solutions de mise en cluster et d’orchestration de containers open source. Ce document vous guide dans le processus de déploiement d’un cluster de Service de conteneur Azure à l’aide de hello portail Azure ou un modèle de démarrage rapide Azure Resource Manager. 

Vous pouvez également déployer un cluster du Service de conteneur Azure à l’aide de hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) ou hello API de Service de conteneur Azure.

Pour obtenir du contexte, consultez [Présentation d’Azure Container Service](../container-service-intro.md).


## <a name="prerequisites"></a>Composants requis

* **Abonnement Azure** : si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935). Pour un cluster de plus grande taille, envisagez de souscrire un abonnement de paiement à l’utilisation ou d’autres options d’achat.

    > [!NOTE]
    > L’utilisation de votre abonnement Azure et [quotas ressources](../../azure-subscription-service-limits.md), telles que les quotas de cœurs, peut limiter la taille de hello du cluster hello vous déployez. toorequest une augmentation du quota, ouvrir une [demande de support technique en ligne](../../azure-supportability/how-to-create-azure-support-request.md) sans frais.
    >

* **Clé publique SSH-RSA**: lors du déploiement via le portail de hello ou l’un des modèles de démarrage rapide Azure hello, vous devez clé publique de tooprovide hello pour l’authentification sur les ordinateurs virtuels du Service de conteneur Azure. les clés RSA de Secure Shell (SSH) toocreate, consultez hello [OS X et Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../../virtual-machines/linux/ssh-from-windows.md) des conseils. 

* **ID client principal et le secret de service** (Kubernetes uniquement) : pour plus d’informations et des recommandations toocreate un principal du service Azure Active Directory, consultez [sur le principal du service pour un cluster Kubernetes hello](../kubernetes/container-service-kubernetes-service-principal.md).



## <a name="create-a-cluster-by-using-hello-azure-portal"></a>Créer un cluster à l’aide de hello portail Azure
1. Connexion toohello portail Azure, sélectionnez **nouveau**, puis recherchez hello Azure Marketplace pour **Service de conteneur Azure**.

    ![Azure Container Service dans Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. Cliquez sur **Azure Container Service**, puis cliquez sur **Créer**.

3. Sur hello **notions de base** panneau, entrez hello informations suivantes :

    * **Orchestrator**: sélectionnez une des hello conteneur orchestrators toodeploy sur le cluster de hello.
        * **DC/OS**: déploie un cluster DC/OS.
        * **Swarm**: déploie un cluster Docker Swarm.
        * **Kubernetes** : déploie un cluster Kubernetes.
    * **Abonnement**: sélectionnez un abonnement Azure.
    * **Groupe de ressources**: entrez le nom hello d’un nouveau groupe de ressources pour le déploiement de hello.
    * **Emplacement**: sélectionnez une région Azure pour le déploiement du Service de conteneur Azure hello. Pour connaître la disponibilité, consultez [Disponibilité des produits par région](https://azure.microsoft.com/regions/services/).
    
    ![Paramètres de base](./media/container-service-deployment/acs-portal3.png)  <br />
    
    Cliquez sur **OK** lorsque vous êtes prêt tooproceed.

4. Sur hello **maître configuration** panneau, entrez hello suivant les paramètres pour hello Linux maître ou les nœuds de cluster hello (certains paramètres sont spécifiques tooeach orchestrator) :

    * **Nom DNS du contrôleur**: hello toocreate de préfixe utilisé un seul nom de domaine complet (FQDN) pour maître de hello. Hello, le nom de domaine complet principal se présente sous forme de hello *préfixe*gestion*emplacement*. cloudapp.azure.com.
    * **Nom d’utilisateur**: nom d’utilisateur hello pour un compte sur chaque hello Linux machines virtuelles hello cluster.
    * **Clé publique SSH-RSA**: ajouter hello toobe clé publique utilisée pour l’authentification sur les ordinateurs virtuels Linux hello. Il est important que cette clé ne contient aucun saut de ligne, et il inclut hello `ssh-rsa` préfixe. Hello `username@domain` suffixe est facultatif. Hello clé doit ressembler à hello suivantes : **AAAAB3Nz ssh-rsa... <> …... UcyupgH azureuser@linuxvm** . 
    * **Principal du service**: Si vous avez sélectionné orchestrator Kubernetes de hello, entrez un répertoire Azure Active Directory **ID de client principal de Service** (également appelé hello appId) et **clé secrète client principal du Service** (mot de passe). Pour plus d’informations, consultez [sur le principal du service pour un cluster Kubernetes hello](../kubernetes/container-service-kubernetes-service-principal.md).
    * **Maître nombre**: hello nombre de masques dans le cluster de hello.
    * **Diagnostics de machine virtuelle**: pour certains orchestrators, vous pouvez activer les diagnostics de machine virtuelle sur les maîtres hello.

    ![Configuration maître](./media/container-service-deployment/acs-portal4.png)  <br />

    Cliquez sur **OK** lorsque vous êtes prêt tooproceed.

5. Sur hello **configuration de l’Agent** panneau, entrez hello informations suivantes :

    * **Nombre d’agents**: pour Docker essaim et Kubernetes, cette valeur est le nombre initial de hello d’agents dans l’ensemble d’échelle de l’agent hello. Pour le contrôleur de domaine/système d’exploitation, il est nombre initial de hello d’agents dans un ensemble d’échelle privé. En outre, un groupe identique public est créé pour DC/OS et contient un nombre prédéterminé d’agents. nombre d’agents dans cet ensemble d’échelle publique Hello est déterminé par nombre de hello de masques dans le cluster de hello : un agent public pour un maître et deux agents publics pour trois ou cinq formes de base.
    * **Taille de machine virtuelle de l’agent**: hello taille des ordinateurs virtuels de l’agent hello.
    * **Système d’exploitation**: ce paramètre est actuellement disponible uniquement si vous avez sélectionné orchestrator Kubernetes de hello. Choisissez une distribution Linux ou un toorun de système d’exploitation Windows Server sur les agents de hello. Ce paramètre détermine si votre cluster peut exécuter des applications de conteneur Windows ou Linux. 

        > [!NOTE]
        > La prise en charge de conteneur Windows est en version préliminaire pour les clusters Kubernetes. Pour les clusters DC/OS et Swarm, seuls les agents Linux sont actuellement pris en charge dans Azure Container Service.

    * **Informations d’identification de l’agent**: Si vous avez sélectionné le système d’exploitation de Windows hello, entrez un administrateur **nom d’utilisateur** et **mot de passe** pour l’agent hello machines virtuelles. 

    ![Configuration de l’agent](./media/container-service-deployment/acs-portal5.png)  <br />

    Cliquez sur **OK** lorsque vous êtes prêt tooproceed.

6. Cliquez sur **OK** une fois la validation du service terminée.

    ![Validation](./media/container-service-deployment/acs-portal6.png)  <br />

7. Passez en revue les termes du contrat de hello. processus de déploiement toostart hello, cliquez sur **créer**.

    Si vous avez choisi toopin hello déploiement toohello portail Azure, vous pouvez voir l’état du déploiement hello.

    ![état du déploiement](./media/container-service-deployment/acs-portal8.png)  <br />

déploiement de Hello prend plusieurs minutes toocomplete. Ensuite, le cluster du Service de conteneur Azure hello est prêt à être utilisé.


## <a name="create-a-cluster-by-using-a-quickstart-template"></a>Créer un cluster à l’aide d’un modèle de démarrage rapide
Les modèles de démarrage rapide Azure sont disponible toodeploy un cluster dans le conteneur de Service Azure. Hello fourni des modèles de démarrage rapide peuvent être modifiée tooinclude configuration Azure supplémentaires ou avancés. toocreate un cluster du Service de conteneur Azure à l’aide d’un modèle de démarrage rapide Azure, vous devez un abonnement Azure. Si ce n’est pas le cas, inscrivez-vous dès aujourd’hui pour un [essai gratuit](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935). 

Suivez ces étapes toodeploy un cluster à l’aide d’un modèle et hello Azure CLI 2.0 (voir [instructions d’installation et](/cli/azure/install-az-cli2)).

> [!NOTE] 
> Si vous êtes sur un système Windows, vous pouvez utiliser un modèle à l’aide d’Azure PowerShell similaire toodeploy d’étapes. Consultez les étapes plus loin dans cette section. Vous pouvez également déployer un modèle de par Bonjour [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) ou d’autres méthodes.

1. toodeploy un contrôleur de domaine/système d’exploitation, Docker Swarm ou Kubernetes du cluster, sélectionnez un des modèles de démarrage rapide disponible hello à partir de GitHub. Une liste partielle s’affiche. Hello contrôleur de domaine/système d’exploitation et les modèles essaim sont hello même, à l’exception de sélection d’orchestrator hello par défaut.

    * [Modèle DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Modèle Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Modèle Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Connectez-vous à tooyour compte Azure (`az login`) et assurez-vous que hello CLI d’Azure est connecté tooyour abonnement Azure. Vous pouvez voir l’abonnement de hello par défaut à l’aide de hello de commande suivante :

    ```azurecli
    az account show
    ```
    
    Si vous avez plusieurs tooset d’abonnement et d’avoir un abonnement par défaut différent, exécutez `az account set --subscription` et spécifiez le nom ou ID d’abonnement hello.

3. Comme meilleure pratique, utilisez un groupe de ressources pour le déploiement de hello. toocreate un groupe de ressources, utilisez hello `az group create` commande spécifie un nom de groupe de ressources et l’emplacement : 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. Créer un modèle requis hello de conteneur fichier JSON de paramètres. Fichier de paramètres hello téléchargement nommé `azuredeploy.parameters.json` qui accompagne le modèle de Service de conteneur Azure hello `azuredeploy.json` dans GitHub. Entrez les valeurs de paramètre requises pour votre cluster. 

    Par exemple, toouse hello [modèle de contrôleur de domaine/système d’exploitation](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), fournir des valeurs de paramètre pour `dnsNamePrefix` et `sshRSAPublicKey`. Consultez les descriptions de hello dans `azuredeploy.json` et options pour les autres paramètres.  
 

5. Créer un cluster du Service de conteneur en transmettant le fichier de paramètres de déploiement hello avec hello suivant de commande, où :

    * **RESOURCE_GROUP** est le nom hello hello du groupe de ressources que vous avez créé à l’étape précédente de hello.
    * **DEPLOYMENT_NAME** (facultatif) est un nom que vous donnez toohello déploiement.
    * **TEMPLATE_URI** est l’emplacement de hello du fichier de déploiement hello `azuredeploy.json`. Cet URI doit être le fichier brut hello, pas un toohello pointeur GitHub UI. toofind cet URI, sélectionnez hello `azuredeploy.json` fichier dans GitHub, puis cliquez sur hello **Raw** bouton.  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    Vous pouvez également fournir des paramètres sous forme de chaîne au format JSON sur la ligne de commande hello. Utilisez un commande similaire toohello qui suit :

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > déploiement de Hello prend plusieurs minutes toocomplete.
    > 

### <a name="equivalent-powershell-commands"></a>Commandes PowerShell équivalentes
Vous pouvez également déployer un modèle de cluster Azure Container Service avec PowerShell. Ce document est basé sur la version 1.0 du hello [module Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).

1. toodeploy un contrôleur de domaine/système d’exploitation, Docker Swarm ou Kubernetes du cluster, sélectionnez un des modèles de démarrage rapide disponible hello à partir de GitHub. Une liste partielle s’affiche. Notez que le hello contrôleur de domaine/système d’exploitation et les modèles essaim sont hello à identiques, à l’exception de hello de sélection d’orchestrator hello par défaut.

    * [Modèle DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [Modèle Swarm](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [Modèle Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. Avant de créer un cluster dans votre abonnement Azure, vérifiez que votre session PowerShell a été signée dans tooAzure. Cela avec hello `Get-AzureRMSubscription` commande :

    ```powershell
    Get-AzureRmSubscription
    ```

3. Si vous devez toosign dans tooAzure, utilisez hello `Login-AzureRMAccount` commande :

    ```powershell
    Login-AzureRmAccount
    ```

4. Comme meilleure pratique, utilisez un groupe de ressources pour le déploiement de hello. toocreate un groupe de ressources, utilisez hello `New-AzureRmResourceGroup` de commandes et spécifier une région de nom et la destination groupe de ressources :

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. Après avoir créé un groupe de ressources, vous pouvez créer votre cluster avec hello commande suivante. Hello URI Hello souhaité template est spécifié avec hello `-TemplateUri` paramètre. Lorsque vous exécutez cette commande, PowerShell vous invite à saisir les valeurs des paramètres de déploiement.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a>Indication des paramètres du modèle
Si vous êtes familiarisé avec PowerShell, vous savez que vous pouvez passer en revue les paramètres disponibles de hello pour une applet de commande en tapant un signe moins (-) et en appuyant sur la touche TAB. hello. Cette fonctionnalité fonctionne également avec les paramètres que vous définissez dans votre modèle. Dès que vous tapez le nom du modèle hello, applet de commande hello extrait le modèle de hello, analyse hello paramètres et ajoute hello modèle paramètres toohello commande dynamiquement. Cela permet de valeurs de paramètre de modèle simple toospecify hello. Et, si vous oubliez d’une valeur de paramètre obligatoire, PowerShell vous invite à valeur de hello.

Voici la commande hello complète, avec des paramètres inclus. Fournissez vos propres valeurs pour les noms des ressources de hello hello.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a>Étapes suivantes
À présent que vous disposez d’un cluster opérationnel, consultez les documents suivants pour obtenir des informations supplémentaires concernant la connexion et la gestion du cluster :

* [Connecter le cluster du Service de conteneur Azure tooan](../container-service-connect.md)
* [Gestion de conteneur via l’API REST](container-service-mesos-marathon-rest.md)
* [Gestion des conteneurs avec Docker Swarm](container-service-docker-swarm.md)
* [Gestion des conteneurs avec Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)
