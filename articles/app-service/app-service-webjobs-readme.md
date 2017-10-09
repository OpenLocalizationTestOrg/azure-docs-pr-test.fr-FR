---
title: aaaWebJobs dans Azure App Service
description: "Découvrez comment toobuild WebJobs toorun arrière-plan teste, interagir avec les services de stockage et de Service Bus et créer des tâches planifiées."
services: app-service
documentationcenter: 
author: christopheranderson
manager: erikre
editor: mollybos
ms.assetid: 85975432-04c9-4b83-b937-b30c082d52a1
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/10/2015
ms.author: chrande
ms.openlocfilehash: 25c24bfe71a64036cd48e58f471995b4a06e3b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-webjobs-in-azure-app-service"></a>Utilisation de WebJobs dans Azure App Service
Cet article lie toodocumentation des ressources concernant la manière toouse tâches Web Azure et hello du Kit de développement logiciel Azure WebJobs. Les tâches Web Azure fournissent un script de toorun facilement ou programmes en tant que processus d’arrière-plan sur [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Vous pouvez télécharger et exécuter un fichier exécutable comme cmd, bat, exe (.NET), ps1, sh, php, py, js et jar. Ces programmes s’exécutent en tant que tâches WebJobs selon une planification (cron) ou en continu.

Hello WebJobs SDK rend plus facile toouse le stockage Azure. Hello WebJobs SDK a une liaison et un système de déclencheur qui fonctionne avec Microsoft Azure Storage BLOB, files d’attente et Tables ainsi que les files d’attente de Service Bus.

La création, le déploiement et la gestion des tâches web WebJobs sont parfaitement compatibles avec les outils intégrés dans Visual Studio. Vous pouvez créer les tâches web WebJobs à partir de modèles, les publier et les gérer (exécuter/arrêter/analyser/déboguer).

tableau de bord WebJobs Hello Bonjour portail Azure fournit de puissantes fonctions de gestion qui vous donnent un contrôle total sur l’exécution de hello de tâches Web, y compris hello capacité tooinvoke des fonctions individuelles dans les tâches Web. tableau de bord Hello affiche également les exécutions de la fonction et la sortie de journalisation.

[!INCLUDE [app-service-blueprint-webjobs](../../includes/app-service-blueprint-webjobs.md)]

