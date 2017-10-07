---
title: "données aaaSample dans Azure, SQL Server, les conteneurs d’objets blob et tables de la ruche | Documents Microsoft"
description: "Comment les données de tooexplore stockées dans diverses enviromnents Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 80a9dfae-e3a6-4cfb-aecc-5701cfc7e39d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5a5295b59fa02f91da680fc7495a92ca135e26c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Échantillonner des données dans des conteneurs d'objets blob Azure, SQL Server et des tables Hive
Ce document lie tootopics couvre comment toosample les données stockées dans un des trois emplacements Azure :

* **données de conteneurs d’objets blob Azure** sont échantillonnées par le biais de leur téléchargement par programmation, puis de leur échantillonnage à l’aide d’un exemple de code Python.
* **Les données de SQL Server** sont échantillonnées à l’aide de SQL et hello langage de programmation Python. 
* **tables Hive** sont échantillonnées à l’aide de requêtes Hive.

suivant de Hello **menu** liens toohello rubriques qui décrivent comment toosample des données à partir de chacun de ces environnements de stockage Azure. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

Cette tâche d’échantillonnage est une étape Bonjour [processus de science des données équipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

**Pourquoi échantillonner des données ?**

Si dataset hello vous envisagez de tooanalyze est grand, il est généralement un tooreduce de données recommandé toodown-exemple hello il tooa plus petite mais représentatif et plus facile à gérer la taille. Cette opération facilite la compréhension et l’exploration des données, ainsi que la conception de fonctionnalités. Son rôle dans hello Cortana Analytique processus est tooenable le prototypage rapide des fonctions de traitement des données de hello et modèles d’apprentissage automatique.

