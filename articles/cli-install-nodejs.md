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
# <a name="install-hello-azure-cli-10"></a><span data-ttu-id="b7df6-103">Installer hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b7df6-103">Install hello Azure CLI 1.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b7df6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7df6-104">PowerShell</span></span>](/powershell/azure/overview)
> * [<span data-ttu-id="b7df6-105">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b7df6-105">Azure CLI 1.0</span></span>](cli-install-nodejs.md)
> * [<span data-ttu-id="b7df6-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b7df6-106">Azure CLI 2.0</span></span>](/cli/azure/install-azure-cli)

> [!IMPORTANT]
> <span data-ttu-id="b7df6-107">Cette rubrique décrit la méthode d’appel de tooinstall hello Azure CLI 1.0, qui repose sur nodeJs et prend en charge toutes les API de déploiement classique, ainsi que d’un grand nombre d’activités de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b7df6-107">This topic describes how tooinstall hello Azure CLI 1.0, which is built on nodeJs and supports all classic deployment API calls as well as a large number of Resource Manager deployment activities.</span></span> <span data-ttu-id="b7df6-108">Vous devez utiliser hello [Azure CLI 2.0](/cli/azure/overview) pour les déploiements CLI nouveau ou prévisionnelles et la gestion.</span><span class="sxs-lookup"><span data-stu-id="b7df6-108">You should use hello [Azure CLI 2.0](/cli/azure/overview) for new or forward-looking CLI deployments and management.</span></span>

<span data-ttu-id="b7df6-109">Installer rapidement hello Interface de ligne de commande de Azure (Azure CLI 1.0) toouse un ensemble de commandes d’environnement open source pour la création et la gestion des ressources dans Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b7df6-109">Quickly install hello Azure Command-Line Interface (Azure CLI 1.0) toouse a set of open-source shell-based commands for creating and managing resources in Microsoft Azure.</span></span> <span data-ttu-id="b7df6-110">Vous avez plusieurs options tooinstall de ces outils inter-plateformes sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="b7df6-110">You have several options tooinstall these cross-platform tools on your computer:</span></span>

* <span data-ttu-id="b7df6-111">**package npm** - exécution (Gestionnaire de package hello pour JavaScript) tooinstall hello dernière Azure CLI 1.0 package npm sur votre système d’exploitation ou la distribution de Linux.</span><span class="sxs-lookup"><span data-stu-id="b7df6-111">**npm package** - Run npm (hello package manager for JavaScript) tooinstall hello latest Azure CLI 1.0 package on your Linux distribution or OS.</span></span> <span data-ttu-id="b7df6-112">Requiert l’installation de node.js et npm sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b7df6-112">Requires node.js and npm on your computer.</span></span>
* <span data-ttu-id="b7df6-113">**Programme d’installation** : téléchargez un programme d’installation pour une installation rapide sur Mac ou Windows.</span><span class="sxs-lookup"><span data-stu-id="b7df6-113">**Installer** - Download an installer for easy installation on Mac or Windows.</span></span>
* <span data-ttu-id="b7df6-114">**Conteneur docker** - démarrer à l’aide de hello dernière CLI dans un conteneur Docker de prêt à s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="b7df6-114">**Docker container** - Start using hello latest CLI in a ready-to-run Docker container.</span></span> <span data-ttu-id="b7df6-115">Nécessite la présence d’un hôte Docker sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b7df6-115">Requires Docker host on your computer.</span></span>

<span data-ttu-id="b7df6-116">Pour plus d’options et d’arrière-plan, consultez le référentiel de projet hello sur [GitHub](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="b7df6-116">For more options and background, see hello project repository on [GitHub](https://github.com/azure/azure-xplat-cli).</span></span>

<span data-ttu-id="b7df6-117">Une fois hello Azure CLI 1.0 est installé, [connectez-le à votre abonnement Azure](xplat-cli-connect.md) et exécution hello **azure** commandes à partir de votre interface de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes et ainsi de suite) toowork avec vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b7df6-117">Once hello Azure CLI 1.0 is installed, [connect it with your Azure subscription](xplat-cli-connect.md) and run hello **azure** commands from your command-line interface (Bash, Terminal, Command prompt, and so on) toowork with your Azure resources.</span></span>

## <a name="option-1-install-an-npm-package"></a><span data-ttu-id="b7df6-118">Option 1 : Installer un package npm</span><span class="sxs-lookup"><span data-stu-id="b7df6-118">Option 1: Install an npm package</span></span>
<span data-ttu-id="b7df6-119">tooinstall hello CLI à partir d’un package npm, assurez-vous que vous avez téléchargé et installé hello [dernières Node.js et npm](https://nodejs.org/en/download/package-manager/).</span><span class="sxs-lookup"><span data-stu-id="b7df6-119">tooinstall hello CLI from an npm package, make sure you have downloaded and installed hello [latest Node.js and npm](https://nodejs.org/en/download/package-manager/).</span></span> <span data-ttu-id="b7df6-120">Ensuite, exécutez **npm installer** package d’azure-cli tooinstall hello :</span><span class="sxs-lookup"><span data-stu-id="b7df6-120">Then, run **npm install** tooinstall hello azure-cli package:</span></span>

```bash
npm install -g azure-cli
```

<span data-ttu-id="b7df6-121">Distributions Linux, vous devrez peut-être toouse **sudo** toosuccessfully exécuter hello **npm** commande, comme suit :</span><span class="sxs-lookup"><span data-stu-id="b7df6-121">On Linux distributions, you might need toouse **sudo** toosuccessfully run hello **npm** command, as follows:</span></span>

```bash
sudo npm install -g azure-cli
```

> [!NOTE]
> <span data-ttu-id="b7df6-122">Si vous devez tooinstall ou mettre à jour Node.js et npm sur votre système d’exploitation ou une distribution Linux, nous vous recommandons d’installer hello dernière Node.js LTS version (4.x).</span><span class="sxs-lookup"><span data-stu-id="b7df6-122">If you need tooinstall or update Node.js and npm on your Linux distribution or OS, we recommend that you install hello most recent Node.js LTS version (4.x).</span></span> <span data-ttu-id="b7df6-123">Si vous utilisez une version antérieure, vous pouvez obtenir des erreurs d’installation.</span><span class="sxs-lookup"><span data-stu-id="b7df6-123">If you use an older version, you might get installation errors.</span></span>

<span data-ttu-id="b7df6-124">Si vous préférez, télécharger hello Linux dernière [fichier tar] [ linux-installer] pour hello npm package localement.</span><span class="sxs-lookup"><span data-stu-id="b7df6-124">If you prefer, download hello latest Linux [tar file][linux-installer] for hello npm package locally.</span></span> <span data-ttu-id="b7df6-125">Ensuite, installez package npm téléchargé de hello comme suit (sur les distributions de Linux, vous devrez peut-être toouse **sudo**) :</span><span class="sxs-lookup"><span data-stu-id="b7df6-125">Then, install hello downloaded npm package as follows (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
npm install -g <path toodownloaded tar file>
```

## <a name="option-2-use-an-installer"></a><span data-ttu-id="b7df6-126">Option 2 : Utiliser un programme d’installation</span><span class="sxs-lookup"><span data-stu-id="b7df6-126">Option 2: Use an installer</span></span>
<span data-ttu-id="b7df6-127">Si vous utilisez un ordinateur Mac ou Windows, hello suit les programmes d’installation CLI est disponible en téléchargement :</span><span class="sxs-lookup"><span data-stu-id="b7df6-127">If you use a Mac or Windows computer, hello following CLI installers are available for download:</span></span>

* <span data-ttu-id="b7df6-128">[Programme d’installation Mac OS X][mac-installer]</span><span class="sxs-lookup"><span data-stu-id="b7df6-128">[Mac OS X installer][mac-installer]</span></span>
* <span data-ttu-id="b7df6-129">[MSI Windows][windows-installer]</span><span class="sxs-lookup"><span data-stu-id="b7df6-129">[Windows MSI][windows-installer]</span></span>

> [!TIP]
> <span data-ttu-id="b7df6-130">Sous Windows, vous pouvez également télécharger hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span><span class="sxs-lookup"><span data-stu-id="b7df6-130">On Windows, you can also download hello [Web Platform Installer](https://go.microsoft.com/?linkid=9828653) tooinstall hello CLI.</span></span> <span data-ttu-id="b7df6-131">Cette offre de programme d’installation vous hello option tooinstall supplémentaires Azure SDK et outils de ligne de commande après l’installation de hello CLI.</span><span class="sxs-lookup"><span data-stu-id="b7df6-131">This installer gives you hello option tooinstall additional Azure SDK and command-line tools after installing hello CLI.</span></span>

## <a name="option-3-use-a-docker-container"></a><span data-ttu-id="b7df6-132">Option 3 : Utiliser un conteneur Docker</span><span class="sxs-lookup"><span data-stu-id="b7df6-132">Option 3: Use a Docker container</span></span>
<span data-ttu-id="b7df6-133">Si vous avez configuré votre ordinateur en tant qu’un [Docker](https://docs.docker.com/engine/understanding-docker/) hôte, vous pouvez exécuter hello dernière Azure CLI 1.0 dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="b7df6-133">If you have set up your computer as a [Docker](https://docs.docker.com/engine/understanding-docker/) host, you can run hello latest Azure CLI 1.0 in a Docker container.</span></span> <span data-ttu-id="b7df6-134">Exécution hello commande suivante (sur les distributions de Linux, vous devrez peut-être toouse **sudo**) :</span><span class="sxs-lookup"><span data-stu-id="b7df6-134">Run hello following command (on Linux distributions you might need toouse **sudo**):</span></span>

```bash
docker run -it microsoft/azure-cli
```

## <a name="run-azure-cli-10-commands"></a><span data-ttu-id="b7df6-135">Exécution des commandes Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b7df6-135">Run Azure CLI 1.0 commands</span></span>
<span data-ttu-id="b7df6-136">Une fois hello Azure CLI 1.0 est installé, exécutez hello **azure** commande à partir de votre interface utilisateur de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes et ainsi de suite).</span><span class="sxs-lookup"><span data-stu-id="b7df6-136">After hello Azure CLI 1.0 is installed, run hello **azure** command from your command-line user interface (Bash, Terminal, Command prompt, and so on).</span></span> <span data-ttu-id="b7df6-137">Par exemple, la commande de help toorun hello, tapez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="b7df6-137">For example, toorun hello help command, type hello following:</span></span>

```azurecli
azure help
```

> [!NOTE]
> <span data-ttu-id="b7df6-138">Sur certaines distributions Linux, vous pouvez recevoir un message d’erreur similaire trop`/usr/bin/env: ‘node’: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="b7df6-138">On some Linux distributions, you may receive an error similar too`/usr/bin/env: ‘node’: No such file or directory`.</span></span> <span data-ttu-id="b7df6-139">Cette erreur est due à l’installation récente de Node.js sous /usr/bin/nodejs.</span><span class="sxs-lookup"><span data-stu-id="b7df6-139">This error comes from recent installations of Node.js being installed at /usr/bin/nodejs.</span></span> <span data-ttu-id="b7df6-140">toofix, créez un lien symbolique trop/usr/bin/nœud en exécutant cette commande :</span><span class="sxs-lookup"><span data-stu-id="b7df6-140">toofix it, create a symbolic link too/usr/bin/node by running this command:</span></span>

```bash
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

<span data-ttu-id="b7df6-141">version de hello toosee Hello Azure 1.0 CLI vous avez installé, hello du type suivant :</span><span class="sxs-lookup"><span data-stu-id="b7df6-141">toosee hello version of hello Azure CLI 1.0 you installed, type hello following:</span></span>

```azurecli
azure --version
```

<span data-ttu-id="b7df6-142">Vous avez terminé l’installation.</span><span class="sxs-lookup"><span data-stu-id="b7df6-142">Now you are ready!</span></span> <span data-ttu-id="b7df6-143">tooaccess tous les hello toowork des commandes CLI avec vos propres ressources et [connecter tooyour abonnement Azure à partir de hello CLI d’Azure](xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="b7df6-143">tooaccess all hello CLI commands toowork with your own resources, [connect tooyour Azure subscription from hello Azure CLI](xplat-cli-connect.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b7df6-144">Lorsque vous utilisez tout d’abord CLI d’Azure, vous voyez un message vous demandant si vous souhaitez que les informations sur l’utilisation de Microsoft toocollect de tooallow.</span><span class="sxs-lookup"><span data-stu-id="b7df6-144">When you first use Azure CLI, you see a message asking if you want tooallow Microsoft toocollect usage information.</span></span> <span data-ttu-id="b7df6-145">La participation se fait sur la base du volontariat.</span><span class="sxs-lookup"><span data-stu-id="b7df6-145">Participation is voluntary.</span></span> <span data-ttu-id="b7df6-146">Si vous choisissez tooparticipate, vous pouvez arrêter à tout moment en exécutant `azure telemetry --disable`.</span><span class="sxs-lookup"><span data-stu-id="b7df6-146">If you choose tooparticipate, you can stop at any time by running `azure telemetry --disable`.</span></span> <span data-ttu-id="b7df6-147">la participation de tooenable à tout moment, exécutez `azure telemetry --enable`.</span><span class="sxs-lookup"><span data-stu-id="b7df6-147">tooenable participation at any time, run `azure telemetry --enable`.</span></span>

## <a name="update-hello-cli"></a><span data-ttu-id="b7df6-148">Mettre à jour hello CLI</span><span class="sxs-lookup"><span data-stu-id="b7df6-148">Update hello CLI</span></span>
<span data-ttu-id="b7df6-149">Microsoft publie fréquemment des versions mises à jour de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b7df6-149">Microsoft frequently releases updated versions of hello Azure CLI.</span></span> <span data-ttu-id="b7df6-150">Réinstallez hello CLI à l’aide du programme d’installation hello pour votre système d’exploitation, ou exécuter le conteneur Docker de la dernière hello.</span><span class="sxs-lookup"><span data-stu-id="b7df6-150">Reinstall hello CLI using hello installer for your operating system, or run hello latest Docker container.</span></span> <span data-ttu-id="b7df6-151">Ou, si vous avez hello dernières Node.js et npm installé, la mise à jour en tapant hello suivante (sur les distributions de Linux, vous devrez peut-être toouse **sudo**).</span><span class="sxs-lookup"><span data-stu-id="b7df6-151">Or, if you have hello latest Node.js and npm installed, update by typing hello following (on Linux distributions you might need toouse **sudo**).</span></span>

```bash
npm update -g azure-cli
```

## <a name="enable-tab-completion"></a><span data-ttu-id="b7df6-152">Activer la saisie semi-automatique via la touche Tab</span><span class="sxs-lookup"><span data-stu-id="b7df6-152">Enable tab completion</span></span>
<span data-ttu-id="b7df6-153">La saisie semi-automatique via la touche Tab des commandes CLI est prise en charge pour Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="b7df6-153">Tab completion of CLI commands is supported for Mac and Linux.</span></span>

<span data-ttu-id="b7df6-154">tooenable dans zsh, exécutez :</span><span class="sxs-lookup"><span data-stu-id="b7df6-154">tooenable it in zsh, run:</span></span>

```bash
echo '. <(azure --completion)' >> .zshrc
```

<span data-ttu-id="b7df6-155">tooenable dans un interpréteur de commandes, exécutez :</span><span class="sxs-lookup"><span data-stu-id="b7df6-155">tooenable it in bash, run:</span></span>

```bash
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.bash_profile
```


## <a name="next-steps"></a><span data-ttu-id="b7df6-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b7df6-156">Next steps</span></span>
* <span data-ttu-id="b7df6-157">[Se connecter à partir de hello CLI tooyour abonnement Azure](xplat-cli-connect.md) toocreate et gérer des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b7df6-157">[Connect from hello CLI tooyour Azure subscription](xplat-cli-connect.md) toocreate and manage Azure resources.</span></span>
* <span data-ttu-id="b7df6-158">toolearn en savoir plus sur hello CLI d’Azure, télécharger le code source, signaler des problèmes, ou contribuent toohello projet, visitez hello [référentiel GitHub pour hello CLI d’Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="b7df6-158">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="b7df6-159">Si vous avez des questions sur l’utilisation de hello CLI d’Azure ou Azure, visitez hello [Forums Windows Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="b7df6-159">If you have questions about using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>


[mac-installer]: http://aka.ms/mac-azure-cli
[windows-installer]: http://aka.ms/webpi-azure-cli
[linux-installer]: http://aka.ms/linux-azure-cli
[cliasm]: /cli/azure/get-started-with-az-cli2
[cliarm]: ./virtual-machines/azure-cli-arm-commands.md
