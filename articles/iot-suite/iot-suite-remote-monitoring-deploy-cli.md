---
title: "Déployer la solution de surveillance à distance Java - Azure | Microsoft Docs"
description: "Ce didacticiel montre comment provisionner les microservices Java de solution préconfigurée de surveillance à distance."
services: 
suite: iot-suite
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-suite
ms.date: 12/12/2017
ms.topic: article
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.workload: NA
ms.openlocfilehash: ea3764299d07f548abbc2857a3adbfb4dc50dec8
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/13/2017
---
# <a name="deploy-the-remote-monitoring-preconfigured-solution-using-the-cli"></a>Déployer la solution préconfigurée de surveillance à distance à l’aide de l’interface CLI

Ce didacticiel montre comment configurer la solution préconfigurée de surveillance à distance. Vous déployez la solution à l’aide de l’interface CLI. Vous pouvez également déployer la solution à l’aide de l’interface utilisateur basée sur le web depuis azureiotsuite.com ; pour en savoir plus sur cette option, consultez [Déployer la solution préconfigurée de surveillance à distance](iot-suite-remote-monitoring-deploy.md).

## <a name="prerequisites"></a>Composants requis

Pour déployer la solution préconfigurée de surveillance à distance, vous avez besoin d’un abonnement Azure actif.

Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](http://azure.microsoft.com/pricing/free-trial/).

Pour pouvoir exécuter l’interface CLI, vous devez installer [Node.js](https://nodejs.org/) sur votre ordinateur local.

## <a name="install-the-cli"></a>Installer l’interface de ligne de commande

Pour installer l’interface CLI, exécutez la commande suivante dans votre environnement de ligne de commande :

```cmd/sh
npm install iot-solutions -g
```

## <a name="sign-in-to-the-cli"></a>Se connecter à l’interface CLI

Avant de déployer la solution préconfigurée, vous devez vous connecter à votre abonnement Azure à l’aide de l’interface CLI comme suit :

```cmd/sh
pcs login
```

Suivez les instructions à l’écran pour effectuer le processus de connexion.

## <a name="deployment-options"></a>Options de déploiement

Quand vous déployez la solution préconfigurée, vous disposez de plusieurs options pour configurer le processus de déploiement :

| Option | Valeurs | Description |
| ------ | ------ | ----------- |
| SKU    | `basic`, `standard` | Utilisez un déploiement _basic_ à des fins de test et de démonstration ; il déploie tous les microservices sur une seule machine virtuelle. Utilisez un déploiement _standard_ à des fins de production ; il déploie les microservices sur plusieurs machines virtuelles. |
| Runtime | `dotnet`, `java` | Sélectionne l’implémentation de langage des microservices. |

## <a name="deploy-the-preconfigured-solution"></a>Déployer la solution préconfigurée

### <a name="example-deploy-net-version"></a>Exemple : déployer la version .NET

L’exemple suivant montre comment déployer la version .NET de base de la solution préconfigurée de surveillance à distance :

```cmd/sh
pcs -t remotemonitoring -s basic -r dotnet
```

### <a name="example-deploy-java-version"></a>Exemple : déployer la version Java

L’exemple suivant montre comment déployer la version Java standard de la solution préconfigurée de surveillance à distance :

```cmd/sh
pcs -t remotemonitoring -s standard -r java
```

### <a name="pcs-command-options"></a>options de la commande pcs

Quand vous exécutez la commande `pcs` pour déployer une solution, vous êtes invité à indiquer les éléments suivants :

- Un nom pour votre solution. Ce nom doit être unique.
- Sélectionnez l’abonnement Azure à utiliser.
- Un emplacement.
- Les informations d’identification des machines virtuelles qui hébergent les microservices. Vous pouvez utiliser ces informations d’identification pour accéder aux machines virtuelles à des fins de dépannage.

Quand la commande `pcs` se termine, elle affiche l’URL du nouveau déploiement de votre solution préconfigurée. La commande `pcs` crée également un fichier `{deployment-name}-output.json` avec des informations supplémentaires telles que le nom du hub IoT qui a été automatiquement provisionné.

Pour plus d’informations sur les paramètres de la ligne de commande, exécutez :

```cmd/sh
pcs -h
```

Pour plus d’informations sur l’interface CLI, consultez [How to use the CLI](https://github.com/Azure/pcs-cli/blob/master/README.md) (Comment utiliser l’interface CLI).

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Configuration de la solution préconfigurée
> * Déploiement de la solution préconfigurée
> * Connexion à la solution préconfigurée

La solution de surveillance à distance étant déployée, l’étape suivante consiste à [explorer les fonctionnalités du tableau de bord des solutions](./iot-suite-remote-monitoring-deploy.md).

<!-- Next tutorials in the sequence -->