---
title: "Installation et configuration de la gestion des modèles Azure Machine Learning | Microsoft Docs"
description: "Ce document décrit les procédures et les concepts relatifs à l’installation et à la configuration de la gestion des modèles dans Azure Machine Learning."
services: machine-learning
author: raymondlaghaeian
ms.author: raymondl
manager: neerajkh
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 08/29/2017
ms.openlocfilehash: 151e7c2dc808a8fa117a0d7a1950185abe9e3152
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/08/2017
---
# <a name="model-management-setup"></a>Installation de la gestion des modèles

## <a name="overview"></a>Vue d'ensemble
Ce document montre comment utiliser la gestion des modèles Azure ML pour déployer et gérer vos modèles d’apprentissage automatique en tant que services web. 

Avec la Gestion des modèles Azure ML, vous pouvez déployer et gérer efficacement des modèles d’apprentissage automatique générés avec différents frameworks, notamment SparkML, Keras, TensorFlow, Microsoft Cognitive Toolkit ou Python. 

À la fin de ce document, votre environnement de gestion des modèles doit être configuré et prêt pour le déploiement de vos modèles d’apprentissage automatique.

## <a name="what-you-need-to-get-started"></a>Ce dont vous avez besoin pour commencer
Pour tirer le meilleur parti de ce guide, vous devez avoir un accès propriétaire à un abonnement Azure sur lequel vous pouvez déployer vos modèles.
L’interface CLI est préinstallée sur Azure Machine Learning Workbench et sur les [machines virtuelles DSVM Azure](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview).

## <a name="using-the-cli"></a>Utilisation de l’interface CLI
Pour utiliser les interfaces de ligne de commande (CLI) à partir de Workbench, cliquez sur **Fichier** -]**Ouvrir l’interface de ligne de commande**. 

Sur une DSVM, connectez-vous et ouvrez l’invite de commandes. Tapez `az ml -h` pour afficher les options. Pour plus d’informations sur les commandes, utilisez l’indicateur --help.

Sur tous les autres systèmes, vous devez installer les interfaces CLI.

### <a name="installing-or-updating-on-windows"></a>Installation (ou mise à jour) sur Windows

Installez Python à partir de https://www.python.org/. Vérifiez que vous avez choisi d’installer pip.

Ouvrez une invite de commandes avec Exécuter en tant qu’administrateur, puis exécutez les commandes suivantes :

```cmd
pip install azure-cli
pip install azure-cli-ml
```
 
>[!NOTE]
>Si vous avez une version antérieure, désinstallez-la d’abord à l’aide de la commande suivante :
>

```cmd
pip uninstall azure-cli-ml
```

### <a name="installing-or-updating-on-linux"></a>Installation (ou mise à jour) sur Linux
Exécutez la commande suivante à partir de la ligne de commande et suivez les invites :

```bash
sudo -i
pip install azure-cli
pip install azure-cli-ml
```

Une fois l’installation terminée, exécutez la commande suivante :

```bash
sudo /opt/microsoft/azureml/initial_setup.sh
```

>[!NOTE]
>Déconnectez-vous de votre session SSH et reconnectez-vous pour que les modifications prennent effet.
>Vous pouvez utiliser les commandes précédentes pour mettre à jour une version antérieure des interfaces CLI sur la DSVM.
>

## <a name="deploying-your-model"></a>Déploiement de votre modèle
Utilisez les interfaces CLI pour déployer des modèles en tant que services web. Les services web peuvent être déployés localement ou sur un cluster.

Partez d’un déploiement local, vérifiez que votre modèle et votre code fonctionnent, puis déployez-le sur un cluster pour une utilisation en production.

Dans un premier temps, vous devez configurer votre environnement de déploiement. La configuration de l’environnement est une tâche qui ne doit être effectuée qu’une seule fois. Une fois la configuration terminée, vous pouvez réutiliser l’environnement pour les déploiements ultérieurs. Pour plus d’informations, consultez la section suivante.

Pendant la configuration de l’environnement :
- Vous êtes invité à vous connecter à Azure. Pour vous connecter, ouvrez la page https://aka.ms/devicelogin dans un navigateur web et entrez le code fourni pour vous authentifier.
- Pendant le processus d’authentification, vous êtes invité à spécifier le compte avec lequel vous authentifier. Important : choisissez un compte qui est associé à un abonnement Azure valide et qui dispose d’autorisations suffisantes pour créer des ressources dans le compte. Une fois la connexion établie, vos informations d’abonnement sont présentées et vous êtes invité à confirmer si vous souhaitez continuer avec le compte sélectionné.

### <a name="environment-setup"></a>Configuration de l’environnement
Pour lancer le processus de configuration, vous devez inscrire le fournisseur d’environnement en entrant la commande suivante :

```azurecli
az provider register -n Microsoft.MachineLearningCompute
```

#### <a name="local-deployment"></a>Déploiement local
Pour déployer et tester votre service web sur l’ordinateur local, configurez un environnement local à l’aide de la commande suivante :

```azurecli
az ml env setup -l [location of Azure Region, e.g. eastus2] -n [your environment name] [-g [existing resource group]]
```
>[!NOTE] 
>Le déploiement local d’un service web exige que vous installiez Docker sur l’ordinateur local. 
>

La commande de configuration d’environnement local crée les ressources suivantes dans votre abonnement :
- Un groupe de ressources (s’il n’est pas fourni)
- Un compte de stockage
- Un ACR (Azure Container Registry)
- Application Insights

Une fois la configuration terminée, définissez l’environnement à utiliser à l’aide de la commande suivante :

```azurecli
az ml env set -n [environment name] -g [resource group]
```

#### <a name="cluster-deployment"></a>Déploiement de cluster
Utilisez le déploiement de cluster pour des scénarios de production à grande échelle. Un cluster ACS est alors défini avec Kubernetes en tant qu’orchestrateur. Vous pouvez effectuer une montée en puissance du cluster ACS afin de gérer un débit supérieur pour vos appels de service web.

Pour déployer votre service web dans un environnement de production, commencez par configurer l’environnement à l’aide de la commande suivante :

```azurecli
az ml env setup -c --name [your environment name] --location [Azure region e.g. eastus2] [-g [resource group]]
```

La commande de configuration d’environnement de cluster crée les ressources suivantes dans votre abonnement :
- Un groupe de ressources (s’il n’est pas fourni)
- Un compte de stockage
- Un ACR (Azure Container Registry)
- Un déploiement Kubernetes sur un cluster ACS
- Application Insights

Le groupe de ressources, le compte de stockage et l’ACR sont créés rapidement. Le déploiement ACS peut prendre jusqu’à 20 minutes. 

Une fois la configuration terminée, vous devez définir l’environnement à utiliser pour ce déploiement. Utilisez la commande suivante :

```azurecli
az ml env set -n [environment name] -g [resource group]
```

>[!NOTE] 
> Une fois l’environnement créé, pour les déploiements suivants, il suffit d’exécuter la commande set ci-dessus pour le réutiliser.
>

>[!NOTE] 
>Pour créer un point de terminaison HTTPS, spécifiez un certificat SSL lors de la création d’un cluster à l’aide des options --cert-name et --cert-pem dans az ml env setup. Cela configure le cluster pour qu’il traite les demandes HTTPS, sécurisées à l’aide du certificat fourni. Une fois l’installation terminée, créez un enregistrement DNS CNAME qui pointe vers le nom de domaine complet du cluster.

### <a name="create-an-account"></a>Créer un compte
Un compte est nécessaire pour déployer des modèles. Vous devez effectuer cette opération une fois par compte, et vous pouvez réutiliser le même compte dans plusieurs déploiements.

Pour créer un compte, utilisez la commande suivante :

```azurecli
az ml account modelmanagement create -l [Azure region, e.g. eastus2] -n [your account name] -g [resource group name] --sku-instances [number of instances, e.g. 1] --sku-name [Pricing tier for example S1]
```

Pour utiliser un compte existant, utilisez la commande suivante :
```azurecli
az ml account modelmanagement set -n [your account name] -g [resource group it was created in]
```

### <a name="deploy-your-model"></a>Déployer votre modèle
Vous êtes maintenant prêt à déployer votre modèle enregistré en tant que service web. 

```azurecli
az ml service create realtime --model-file [model file/folder path] -f [scoring file e.g. score.py] -n [your service name] -s [schema file e.g. service_schema.json] -r [runtime for the Docker container e.g. spark-py or python] -c [conda dependencies file for additional python packages]
```

### <a name="next-steps"></a>Étapes suivantes
Essayez l’un des nombreux exemples de la galerie.
