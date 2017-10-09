---
title: "aaaInstall hello CLI de contrôleur de domaine/système d’exploitation | Documents Microsoft"
description: "Installez hello CLI de contrôleur de domaine/système d’exploitation."
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
ms.openlocfilehash: b077c05beff9a5638486ea5efe9df31089e32701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
> [!NOTE]
> <span data-ttu-id="05907-104">Cela concerne l’utilisation des clusters ACS basés sur DC/OS.</span><span class="sxs-lookup"><span data-stu-id="05907-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="05907-105">Il n’existe aucune toodo besoin cela pour ACS de base essaim clusters.</span><span class="sxs-lookup"><span data-stu-id="05907-105">There is no need toodo this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="05907-106">Tout d’abord, [connecter tooyour basé sur le système d’exploitation contrôleur de domaine de ACS cluster](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="05907-106">First, [connect tooyour DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="05907-107">Une fois que vous avez fait, vous pouvez installer hello CLI de contrôleur de domaine/système d’exploitation sur votre ordinateur client avec les commandes hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="05907-107">Once you have done this, you can install hello DC/OS CLI on your client machine with hello commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="05907-108">Si vous utilisez une ancienne version de Python, vous remarquerez peut-être des messages « InsecurePlatformWarning ».</span><span class="sxs-lookup"><span data-stu-id="05907-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="05907-109">Vous pouvez ignorer ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="05907-109">You can safely ignore these.</span></span>

<span data-ttu-id="05907-110">Dans tooget commande démarré sans avoir à redémarrer votre interpréteur de commandes, exécutez :</span><span class="sxs-lookup"><span data-stu-id="05907-110">In order tooget started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="05907-111">Cette étape n’est pas nécessaire lorsque vous lancez de nouveaux interpréteurs de commandes.</span><span class="sxs-lookup"><span data-stu-id="05907-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="05907-112">Maintenant, vous pouvez vérifier que hello que CLI est installé :</span><span class="sxs-lookup"><span data-stu-id="05907-112">Now you can confirm that hello CLI is installed:</span></span>

```bash
dcos --help
```