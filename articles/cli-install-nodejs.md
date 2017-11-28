---
title: "Installer l’interface de ligne de commande Azure CLI 1.0 | Documents Microsoft"
description: "Installation de l’interface de ligne de commande Azure CLI 1.0 pour Mac, Linux et Windows afin d’utiliser les services Azure"
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
ms.openlocfilehash: 63b35ed25b809a16b61b685fd35aa67474b0a369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-cli-10"></a><span data-ttu-id="90aba-103">Installer l’interface de ligne de commande Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="90aba-103">Install the Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90aba-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90aba-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="90aba-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="90aba-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="90aba-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="90aba-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="90aba-107">Cette rubrique explique comment installer l’interface de ligne de commande Azure CLI 1.0, qui est basée sur nodeJs et prend en charge tous les appels d’API de déploiement classique ainsi qu’un grand nombre d’activités de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="90aba-107">This topic describes how to install the Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="90aba-108">Vous devez utiliser l’[interface de ligne de commande Azure CLI 2.0](/cli/azure/overview) pour les déploiements et la gestion, nouveaux et prospectifs, des interfaces de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="90aba-108">You should use the [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="90aba-109">Installez rapidement l’interface de ligne de commande Azure (Azure CLI 1.0) pour bénéficier d’un ensemble de commandes shell open source permettant de créer et de gérer les ressources dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="90aba-109">Quickly install the Azure Command-Line Interface (Azure CLI 1.0) to use a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="90aba-110">Vous avez plusieurs options pour installer ces outils multiplateformes sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="90aba-110">You have several options to install these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="90aba-111">**Package npm** : exécutez npm (le Gestionnaire de package de JavaScript) pour installer le dernier package de l’interface Azure CLI 1.0 sur votre système d’exploitation ou distribution Linux.</span><span class="sxs-lookup"><span data-stu-id="90aba-111">**npm package** - Run npm (the package manager for JavaScript) to install the latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="90aba-112">Requiert l’installation de node.js et npm sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="90aba-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="90aba-113">**Programme d’installation** : téléchargez un programme d’installation pour une installation rapide sur Mac ou Windows.</span><span class="sxs-lookup"><span data-stu-id="90aba-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="90aba-114">**Conteneur Docker** : utilisez la dernière interface CLI dans un conteneur Docker prêt à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="90aba-114">**Docker container** - Start using the latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="90aba-115">Nécessite la présence d’un hôte Docker sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="90aba-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="90aba-116">Pour obtenir davantage d’options générales et de contexte, consultez le référentiel du projet sur [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="90aba-116">For more options and background, see the project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="90aba-117">Une fois l’interface de ligne de commande Azure CLI 1.0 installée, [connectez-vous à l’aide de votre abonnement Azure](xplat-cli-connect.md) et exécutez les commandes **azure** depuis votre interface de ligne de commande (Bash, Terminal, invite de ligne de commande, etc.) pour travailler avec vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="90aba-117">Once the Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run the **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) to work with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="90aba-118">Option 1 : Installer un package npm</span><span class="sxs-lookup"><span data-stu-id="90aba-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="90aba-119">Pour installer l’interface CLI à partir d’un package npm, vérifiez que vous avez téléchargé et installé les [derniers fichiers Node.js et npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="90aba-119">To install the CLI from an npm package, make sure you have downloaded and installed the [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="90aba-120">Ensuite, exécutez **npm install** pour installer le package azure-cli :</span><span class="sxs-lookup"><span data-stu-id="90aba-120">Then, run **npm install** to install the azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="90aba-121">Sur les distributions Linux, vous devrez peut-être utiliser **sudo** pour exécuter la commande **npm**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="90aba-121">On Linux distributions, you might need to use **sudo** to successfully run the **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="90aba-122">Si vous devez installer ou mettre à jour Node.js et npm sur votre distribution Linux ou votre système d’exploitation, nous vous recommandons d’installer la dernière version de Node.js LTS (4.x).</span><span class="sxs-lookup"><span data-stu-id="90aba-122">If you need to install or update Node.js and npm on your Linux distribution or OS, we recommend that you install the most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="90aba-123">Si vous utilisez une version antérieure, vous pouvez obtenir des erreurs d’installation.</span><span class="sxs-lookup"><span data-stu-id="90aba-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="90aba-124">Si vous préférez, téléchargez le dernier [fichier tar][linux-installer] Linux pour le package npm en local.</span><span class="sxs-lookup"><span data-stu-id="90aba-124">If you prefer, download the latest Linux [tar file][linux-installer] for the npm package locally.</span></span> <span data-ttu-id="90aba-125">Ensuite, installez le package npm téléchargé comme suit (sur les distributions Linux vous devrez peut-être utiliser **sudo**) :</span><span class="sxs-lookup"><span data-stu-id="90aba-125">Then, install the downloaded npm package as follows (on Linux distributions you might need to use **sudo**):</span></span>

```bash
npm install -g <path to downloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="90aba-126">Option 2 : Utiliser un programme d’installation</span><span class="sxs-lookup"><span data-stu-id="90aba-126">Option 2: Use an installer</span></span>
<span data-ttu-id="90aba-127">Si vous utilisez un ordinateur Mac ou Windows, les programmes d’installation de l’interface CLI suivants sont disponibles au téléchargement :</span><span class="sxs-lookup"><span data-stu-id="90aba-127">If you use a Mac or Windows computer, the following CLI installers are available for download:</span></span>

* <span data-ttu-id="90aba-128">[Programme d’installation Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="90aba-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="90aba-129">[MSI Windows][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="90aba-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="90aba-130">Sous Windows, vous pouvez également télécharger [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) pour installer l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="90aba-130">On Windows, you can also download the [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) to install the CLI.</span></span> <span data-ttu-id="90aba-131">Ce programme d’installation vous donne la possibilité d’installer des Kits de développement logiciel (SDK) Azure et des outils de ligne de commande supplémentaires après l’installation de l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="90aba-131">This installer gives you the option to install additional Azure SDK and command-line tools after installing the CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="90aba-132">Option 3 : Utiliser un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="90aba-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="90aba-133">Si vous avez configuré votre ordinateur comme hôte [Docker](https://docs.docker.com/engine/understanding-docker/) , vous pouvez exécuter la dernière interface de ligne de commande Azure CLI 1.0 dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="90aba-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run the latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="90aba-134">Exécutez la commande suivante (sur les distributions Linux, vous devrez peut-être utiliser **sudo**.) :</span><span class="sxs-lookup"><span data-stu-id="90aba-134">Run the following command (on Linux distributions you might need to use **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="90aba-135">Exécution des commandes Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="90aba-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="90aba-136">Une fois l’interface de ligne de commande Azure CLI 1.0 installée, exécutez la commande **azure** depuis l’interface de ligne de commande utilisateur (Bash, Terminal, invite de ligne de commande, etc.).</span><span class="sxs-lookup"><span data-stu-id="90aba-136">After the Azure CLI 1.0 is installed, run the **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="90aba-137">Par exemple, pour exécuter la commande d’aide, saisissez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="90aba-137">For example, to run the help command, type the following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="90aba-138">Dans certaines distributions Linux, vous pouvez recevoir une erreur similaire à `/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="90aba-138">On some Linux distributions, you may receive an error similar to `/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="90aba-139">Cette erreur est due à l’installation récente de Node.js sous /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="90aba-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="90aba-140">Pour la corriger, créez un lien symbolique vers /usr/bin/node en exécutant cette commande :</span><span class="sxs-lookup"><span data-stu-id="90aba-140">To fix it, create a symbolic link to /usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="90aba-141">Pour afficher la version de l’interface Azure CLI 1.0 que vous avez installée, saisissez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="90aba-141">To see the version of the Azure CLI 1.0 you installed, type the following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="90aba-142">Vous avez terminé l’installation.</span><span class="sxs-lookup"><span data-stu-id="90aba-142">Now you are ready!</span></span> <span data-ttu-id="90aba-143">Pour accéder à toutes les commandes de l’interface de ligne de commande et travailler avec vos propres ressources, [connectez-vous à votre abonnement Azure à partir de l’interface de ligne de commande Azure](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="90aba-143">To access all the CLI commands to work with your own resources, [connect to your Azure subscription from the Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="90aba-144">Lorsque vous utilisez l’interface de ligne de commande Azure pour la première fois, vous voyez un message vous demandant si vous souhaitez autoriser Microsoft à recueillir des informations d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="90aba-144">When you first use Azure CLI, you see a message asking if you want to allow Microsoft to collect usage information.</span></span> <span data-ttu-id="90aba-145">La participation se fait sur la base du volontariat.</span><span class="sxs-lookup"><span data-stu-id="90aba-145">Participation is voluntary.</span></span> <span data-ttu-id="90aba-146">Si vous choisissez de participer, vous pouvez arrêter à tout moment en exécutant `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="90aba-146">If you choose to participate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="90aba-147">Pour activer la participation, exécutez `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="90aba-147">To enable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-the-cli"></a><span data-ttu-id="90aba-148">Mise à jour de l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="90aba-148">Update the CLI</span></span>
<span data-ttu-id="90aba-149">Microsoft publie fréquemment des versions mises à jour de l’interface CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="90aba-149">Microsoft frequently releases updated versions of the Azure CLI.</span></span> <span data-ttu-id="90aba-150">Réinstallez l’interface CLI à l’aide du programme d’installation pour votre système d’exploitation, ou exécutez le dernier conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="90aba-150">Reinstall the CLI using the installer for your operating system, or run the latest Docker container.</span></span> <span data-ttu-id="90aba-151">Alternativement, si les dernières versions de Node.js et npm sont installées, procédez à la mise à jour en saisissant ce qui suit (dans les distributions Linux, vous devrez peut-être utiliser **sudo**).</span><span class="sxs-lookup"><span data-stu-id="90aba-151">Or, if you have the latest Node.js and npm installed, update by typing the following (on Linux distributions you might need to use **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="90aba-152">Activer la saisie semi-automatique via la touche Tab</span><span class="sxs-lookup"><span data-stu-id="90aba-152">Enable tab completion</span></span>
<span data-ttu-id="90aba-153">La saisie semi-automatique via la touche Tab des commandes CLI est prise en charge pour Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="90aba-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="90aba-154">Pour l’activer dans zsh, exécutez :</span><span class="sxs-lookup"><span data-stu-id="90aba-154">To enable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="90aba-155">Pour l’activer dans bash, exécutez :</span><span class="sxs-lookup"><span data-stu-id="90aba-155">To enable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="90aba-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="90aba-156">Next steps</span></span>
* <span data-ttu-id="90aba-157">[Se connecter à partir de l’interface de ligne de commande à votre abonnement Azure](xplat-cli-connect.md) pour créer et gérer des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="90aba-157">[Connect from the CLI to your Azure subscription](xplat-cli-connect.md) to create and manage Azure resources.</span></span>
* <span data-ttu-id="90aba-158">Pour plus d'informations sur l'interface de ligne de commande Azure, télécharger un code source, signaler des problèmes ou contribuer au projet, voir [Référentiel GitHub pour l'interface de ligne de commande Azure](https://github.com/azure/azure-xplat-cli)(en anglais).</span><span class="sxs-lookup"><span data-stu-id="90aba-158">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="90aba-159">Si vous avez des questions sur l’utilisation de l’interface de ligne de commande Azure ou sur l’utilisation d’Azure, consultez les [forums Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="90aba-159">If you have questions about using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
