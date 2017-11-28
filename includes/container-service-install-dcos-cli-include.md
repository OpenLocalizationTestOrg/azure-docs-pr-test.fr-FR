---
title: "Installer l’interface de ligne de commande DC/OS | Microsoft Docs"
description: "Installer l’interface de ligne de commande DC/OS."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: a8ea47f158c0d666340815d2e039995c7483257f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
> [!NOTE]
> <span data-ttu-id="51397-104">Cela concerne l’utilisation des clusters ACS basés sur DC/OS.</span><span class="sxs-lookup"><span data-stu-id="51397-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="51397-105">Cette opération est inutile pour les clusters ACS à base de Swarm.</span><span class="sxs-lookup"><span data-stu-id="51397-105">There is no need to do this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="51397-106">Commencez par [vous connecter à votre cluster ACS basé sur DC/OS](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="51397-106">First, [connect to your DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="51397-107">Une fois cette opération terminée, installez l’interface de ligne de commande DC/OS sur votre ordinateur client à l’aide des commandes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="51397-107">Once you have done this, you can install the DC/OS CLI on your client machine with the commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="51397-108">Si vous utilisez une ancienne version de Python, vous remarquerez peut-être des messages « InsecurePlatformWarning ».</span><span class="sxs-lookup"><span data-stu-id="51397-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="51397-109">Vous pouvez ignorer ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="51397-109">You can safely ignore these.</span></span>

<span data-ttu-id="51397-110">Pour démarrer sans avoir à relancer votre interpréteur de commandes, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="51397-110">In order to get started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="51397-111">Cette étape n’est pas nécessaire lorsque vous lancez de nouveaux interpréteurs de commandes.</span><span class="sxs-lookup"><span data-stu-id="51397-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="51397-112">À présent, vous pouvez confirmer l’installation de l’interface de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="51397-112">Now you can confirm that the CLI is installed:</span></span>

```bash
dcos --help
```