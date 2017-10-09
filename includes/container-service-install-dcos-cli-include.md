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
> Cela concerne l’utilisation des clusters ACS basés sur DC/OS. Il n’existe aucune toodo besoin cela pour ACS de base essaim clusters.
> 
> 

Tout d’abord, [connecter tooyour basé sur le système d’exploitation contrôleur de domaine de ACS cluster](../articles/container-service/container-service-connect.md). Une fois que vous avez fait, vous pouvez installer hello CLI de contrôleur de domaine/système d’exploitation sur votre ordinateur client avec les commandes hello ci-dessous :

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

Si vous utilisez une ancienne version de Python, vous remarquerez peut-être des messages « InsecurePlatformWarning ». Vous pouvez ignorer ces erreurs.

Dans tooget commande démarré sans avoir à redémarrer votre interpréteur de commandes, exécutez :

```bash
source ~/.bashrc
```

Cette étape n’est pas nécessaire lorsque vous lancez de nouveaux interpréteurs de commandes.

Maintenant, vous pouvez vérifier que hello que CLI est installé :

```bash
dcos --help
```