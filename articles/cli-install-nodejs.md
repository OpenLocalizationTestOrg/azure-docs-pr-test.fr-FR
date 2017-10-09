---
title: aaaInstall hello Azure CLI 1.0 | Documents Microsoft
description: "Installer hello Azure CLI 1.0 pour Windows, Linux et Mac toostart à l’aide des services Azure"
editor: 
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: bdb776c8-7a76-4f3a-887c-236b4fffee10
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: rasquill
ms.openlocfilehash: a8cd4e38fde6e4b17a768a7caecd280cd91a70f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-cli-10"></a>Installer hello Azure CLI 1.0
> [!div class="op_single_selector"]
> * [PowerShell](/powershell/azure/overview)
> * [Azure CLI 1.0](cli-install-nodejs.md)
> * [Azure CLI 2.0](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> Cette rubrique décrit la méthode d’appel de tooinstall hello Azure CLI 1.0, qui repose sur nodeJs et prend en charge toutes les API de déploiement classique, ainsi que d’un grand nombre d’activités de déploiement Resource Manager. Vous devez utiliser hello [Azure CLI 2.0](/cli/azure/overview) pour les déploiements CLI nouveau ou prévisionnelles et la gestion.

Installer rapidement hello Interface de ligne de commande de Azure (Azure CLI 1.0) toouse un ensemble de commandes d’environnement open source pour la création et la gestion des ressources dans Microsoft Azure. Vous avez plusieurs options tooinstall de ces outils inter-plateformes sur votre ordinateur :

* **package npm** - exécution (Gestionnaire de package hello pour JavaScript) tooinstall hello dernière Azure CLI 1.0 package npm sur votre système d’exploitation ou la distribution de Linux. Requiert l’installation de node.js et npm sur votre ordinateur.
* **Programme d’installation** : téléchargez un programme d’installation pour une installation rapide sur Mac ou Windows.
* **Conteneur docker** - démarrer à l’aide de hello dernière CLI dans un conteneur Docker de prêt à s’exécuter. Nécessite la présence d’un hôte Docker sur votre ordinateur.

Pour plus d’options et d’arrière-plan, consultez le référentiel de projet hello sur [GitHub](https://github.com/azure/azure-xplat-cli).

Une fois hello Azure CLI 1.0 est installé, [connectez-le à votre abonnement Azure](xplat-cli-connect.md) et exécution hello **azure** commandes à partir de votre interface de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes et ainsi de suite) toowork avec vos ressources Azure.

## <a name="option-1-install-an-npm-package"></a>Option 1 : Installer un package npm
tooinstall hello CLI à partir d’un package npm, assurez-vous que vous avez téléchargé et installé hello [dernières Node.js et npm](https://nodejs.org/en/download/package-manager/). Ensuite, exécutez **npm installer** package d’azure-cli tooinstall hello :

```bash
npm install -g azure-cli
```

Distributions Linux, vous devrez peut-être toouse **sudo** toosuccessfully exécuter hello **npm** commande, comme suit :

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> Si vous devez tooinstall ou mettre à jour Node.js et npm sur votre système d’exploitation ou une distribution Linux, nous vous recommandons d’installer hello dernière Node.js LTS version (4.x). Si vous utilisez une version antérieure, vous pouvez obtenir des erreurs d’installation.

Si vous préférez, télécharger hello Linux dernière [fichier tar] [ linux-installer] pour hello npm package localement. Ensuite, installez package npm téléchargé de hello comme suit (sur les distributions de Linux, vous devrez peut-être toouse **sudo**) :

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a>Option 2 : Utiliser un programme d’installation
Si vous utilisez un ordinateur Mac ou Windows, hello suit les programmes d’installation CLI est disponible en téléchargement :

* [Programme d’installation Mac OS X][mac-installer]
* [MSI Windows][windows-installer]

> [!TIP]
> Sous Windows, vous pouvez également télécharger hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI. Cette offre de programme d’installation vous hello option tooinstall supplémentaires Azure SDK et outils de ligne de commande après l’installation de hello CLI.

## <a name="option-3-use-a-docker-container"></a>Option 3 : Utiliser un conteneur Docker
Si vous avez configuré votre ordinateur en tant qu’un [Docker](https://docs.docker.com/engine/understanding-docker/) hôte, vous pouvez exécuter hello dernière Azure CLI 1.0 dans un conteneur Docker. Exécution hello commande suivante (sur les distributions de Linux, vous devrez peut-être toouse **sudo**) :

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a>Exécution des commandes Azure CLI 1.0
Une fois hello Azure CLI 1.0 est installé, exécutez hello **azure** commande à partir de votre interface utilisateur de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes et ainsi de suite). Par exemple, la commande de help toorun hello, tapez hello qui suit :

```azurecli
azure help
```

> [!NOTE]
> Sur certaines distributions Linux, vous pouvez recevoir un message d’erreur similaire trop`/usr/bin/env: ‘node’: No such file or directory`. Cette erreur est due à l’installation récente de Node.js sous /usr/bin/nodejs. toofix, créez un lien symbolique trop/usr/bin/nœud en exécutant cette commande :

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

version de hello toosee Hello Azure 1.0 CLI vous avez installé, hello du type suivant :

```azurecli
azure --version
```

Vous avez terminé l’installation. tooaccess tous les hello toowork des commandes CLI avec vos propres ressources et [connecter tooyour abonnement Azure à partir de hello CLI d’Azure](xplat-cli-connect.md).

> [!NOTE]
> Lorsque vous utilisez tout d’abord CLI d’Azure, vous voyez un message vous demandant si vous souhaitez que les informations sur l’utilisation de Microsoft toocollect de tooallow. La participation se fait sur la base du volontariat. Si vous choisissez tooparticipate, vous pouvez arrêter à tout moment en exécutant `azure telemetry --disable`. la participation de tooenable à tout moment, exécutez `azure telemetry --enable`.

## <a name="update-hello-cli"></a>Mettre à jour hello CLI
Microsoft publie fréquemment des versions mises à jour de hello CLI d’Azure. Réinstallez hello CLI à l’aide du programme d’installation hello pour votre système d’exploitation, ou exécuter le conteneur Docker de la dernière hello. Ou, si vous avez hello dernières Node.js et npm installé, la mise à jour en tapant hello suivante (sur les distributions de Linux, vous devrez peut-être toouse **sudo**).

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a>Activer la saisie semi-automatique via la touche Tab
La saisie semi-automatique via la touche Tab des commandes CLI est prise en charge pour Mac et Linux.

tooenable dans zsh, exécutez :

```bash
echo '. <(azure --completion)' >> .zshrc
```

tooenable dans un interpréteur de commandes, exécutez :

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a>Étapes suivantes
* [Se connecter à partir de hello CLI tooyour abonnement Azure](xplat-cli-connect.md) toocreate et gérer des ressources Azure.
* toolearn en savoir plus sur hello CLI d’Azure, télécharger le code source, signaler des problèmes, ou contribuent toohello projet, visitez hello [référentiel GitHub pour hello CLI d’Azure](https://github.com/azure/azure-xplat-cli).
* Si vous avez des questions sur l’utilisation de hello CLI d’Azure ou Azure, visitez hello [Forums Windows Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
