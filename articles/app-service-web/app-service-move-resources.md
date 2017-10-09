---
title: "Ressources d’application Web d’aaaMove tooanother groupe de ressources"
description: "Décrit des scénarios hello où vous pouvez déplacer des applications Web et les Services d’application à partir d’un groupe de ressources tooanother."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a>Configurations de déplacement prises en charge
Vous pouvez déplacer des ressources de l’application Web Azure à l’aide de hello [API ressources déplacer du Gestionnaire de ressources](../azure-resource-manager/resource-group-move-resources.md).

Les applications Web Azure prend actuellement en charge hello déplacer les scénarios suivants :

* Déplacer hello tout le contenu d’un groupe de ressources (les applications web, les plans de service d’application et les certificats) groupe de ressources tooanother. 
   > [!Note]
   > groupe de ressources Hello destination ne peut pas contenir toutes les ressources Microsoft.Web dans ce scénario.

* Déplacer le groupe de ressources différent de tooa des applications web individuelles, tout en hébergeant les dans leur plan app service en cours (hello app service plan reste dans le groupe de ressources ancien hello).


