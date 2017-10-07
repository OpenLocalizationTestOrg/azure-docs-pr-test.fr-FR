---
title: "aaaProvision données scientifiques des Machines virtuelles Azure en tant que serveurs de bloc-notes notebooks | Documents Microsoft"
description: "Configurez une machine virtuelle pour la science des données en tant que serveur de bloc-notes IPython avec des outils de support."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 95e1fa87-794a-4d03-80a4-af4f3f3ac31e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev
ms.openlocfilehash: 7c0abcbcb822918332f76a9f16690a72b90f4b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-azure-data-science-virtual-machines-as-ipython-notebook-servers"></a>Approvisionner des machines virtuelles pour la science des données Azure en tant que serveurs de bloc-notes IPython
Des instructions sont fournies ici qui décrivent comment tooset une machine virtuelle Azure et une machine virtuelle de Azure avec le Service SQL en tant que serveurs de notebooks bloc-notes. l’ordinateur virtuel Windows Hello est configuré avec la prise en charge des outils tels que des notebooks portable, l’Explorateur de stockage Azure et AzCopy, ainsi que d’autres utilitaires qui sont utiles pour les projets scientifiques de données. Explorateur de stockage Azure et AzCopy, par exemple, offrent des moyens pratiques stockage tooupload de tooAzure des données à partir de votre ordinateur local ou un toodownload il tooyour la machine locale à partir du stockage. 

Ce menu lie tootopics qui décrivent comment tooset des hello différents environnements de science des données utilisé par hello [processus de science des données équipe (TDSP)](data-science-process-overview.md).

[!INCLUDE [data-science-environment-setup](../../includes/cap-setup-environments.md)]

Plusieurs types de machines virtuelles peuvent être configurés et configuré toobe utilisé en tant que partie d’un environnement de science des données basées sur le cloud. décision de Hello sur quelle version de la machine virtuelle toouse dépend de type de hello et la quantité de données toobe modelé avec machine learning et hello destination des données dans le cloud de hello. 

* Pour obtenir des conseils sur hello questions tooconsider prendre cette décision, consultez [planifier votre Azure Machine Learning données Science environnement](machine-learning-data-science-plan-your-environment.md). 
* Pour un catalogue de certains scénarios hello vous pouvez rencontrer lors de l’exécution d’analytique avancée, consultez [hello de scénarios pour les processus Analytique avancé et des technologies dans Azure Machine Learning](machine-learning-data-science-plan-sample-scenarios.md)

Deux ensembles d’instructions vous sont fournis :

* [Configurer une machine virtuelle Azure comme serveur notebooks bloc-notes pour analytique avancée](machine-learning-data-science-setup-virtual-machine.md) illustre l’utilisation tooprovision une machine virtuelle Azure avec notebooks bloc-notes et d’autres outils pour la science des données toodo pour les cas dans lesquels une forme de stockage Azure autre que SQL peut être utilisé toostore hello données.
* [Configurer une machine virtuelle Azure SQL Server comme serveur notebooks bloc-notes pour analytique avancée](machine-learning-data-science-setup-sql-server-virtual-machine.md) illustre l’utilisation tooprovision une machine virtuelle de serveur SQL Azure avec notebooks bloc-notes et d’autres outils pour la science des données toodo pour les cas dans lequel une base de données SQL peut être utilisé toostore hello données.

Une fois mis en service et configurés, ces machines virtuelles sont prêt à être utilisé en tant que serveurs notebooks bloc-notes de hello et le traitement des données et pour d’autres tâches que nécessaires avec Azure Machine Learning et hello processus de science des données équipe (TDSP). les étapes suivantes dans le processus de science des données hello Hello sont mappées dans hello [cursus TDSP](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) et peuvent inclure des étapes qui déplacent des données dans SQL Server ou HDInsight, traiter et aperçu en préparation pour l’apprentissage à partir des données hello avec Azure Apprentissage automatique.

> [!NOTE]
> Le service Azure Virtual Machines est facturé au tarif du **paiement à l’utilisation**. tooensure qui vous ne sont pas facturées lorsque vous n’utilisez ne pas votre machine virtuelle, il a toobe Bonjour **arrêté (désalloué)** état à partir de hello [portail classique Azure](http://manage.windowsazure.com/). Pour obtenir des instructions et la manière dont toodeallocate vous virtuels, consultez [arrêt et désallouer une machine virtuelle inutilisés](machine-learning-data-science-setup-virtual-machine.md#shutdown)
> 
> 

