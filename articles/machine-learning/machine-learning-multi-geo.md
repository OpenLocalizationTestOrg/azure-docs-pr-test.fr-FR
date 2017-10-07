---
title: "documentation d’aide géo-aaaMulti | Documents Microsoft"
description: "Découvrez comment toocreate un espace de travail et publier un service web dans une région Azure différente de hello South centrale United States (SCUS) région Azure."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Documentation d'aide de zones géographiques multiples
Cet article explique comment vous pouvez créer un espace de travail et publier un service web dans différentes régions Azure.  Hello [produits Azure par page région](https://azure.microsoft.com/en-us/regions/services/) répertorie les zones où Azure Machine Learning n’est disponible.

## <a name="create-a-workspace"></a>Créer un espace de travail
1. Connectez-vous toohello portail classique Azure.
2. Cliquez sur **+NOUVEAU** > **SERVICES DE DONNÉES** > **MACHINE LEARNING** > **CRÉATION RAPIDE**.  Sous **EMPLACEMENT**, sélectionner une autre région, par exemple, l'**Asie du Sud-est**.
   ![Aide zone géographique multiple image 1][1]
3. Sélectionnez l’espace de travail hello, puis cliquez sur **connexion tooML Studio**.
   ![Aide zone géographique multiple image 2][2]
4. Vous disposez désormais d'un espace de travail dans une autre région que vous pouvez utiliser comme tout autre espace de travail. tooswitch entre vos espaces de travail, consultez toohello coin supérieur droit votre écran. Cliquez sur hello déroulante, sélectionnez hello région et espace de travail puis sélectionnez hello. Tout est la région d’espace de travail local toohello.  Par exemple, de tous vos services web créés à partir d’un espace de travail sera Bonjour même espace de travail région hello se trouve dans.
   ![Aide zone géographique multiple image 3][3]

## <a name="open-an-experiment-from-gallery"></a>Ouvrir une expérience à partir de la galerie
Si vous ouvrez une expérience à partir de la galerie, vous pouvez également sélectionner la région que vous souhaitez toocopy hello expérimentation.

![Aide zone géographique multiple image 4][4a]

## <a name="web-service-management"></a>Gestion des services web
tooprogrammatically gérer les services web, tels qu’à instruire de nouveau, utiliser une adresse spécifique à la région hello :

* https://asiasoutheast.management.azureml.net
* https://europewest.management.azureml.net

### <a name="things-toonote"></a>Éléments toonote
1. Vous pouvez copier uniquement les expériences entre les espaces de travail qui appartiennent toohello ainsi la même région. Si vous avez besoin d’expérience de toocopy entre les espaces de travail dans des régions différentes, vous pouvez utiliser hello [PowerShell](http://aka.ms/amlps) applet de commande [ *copie-AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish qui. Une autre solution de contournement est expérience de hello toopublish dans la bibliothèque en mode non listé, ouvrez-le dans l’espace de travail hello de hello autre région.
2. Sélecteur de région de Hello affichera uniquement les espaces de travail pour une région à la fois.  
3. Un accès à espace libre ou invité (anonyme) est créé et hébergé dans la région South Central U.S.  
4. Les services web déployés à partir d'un espace de travail en Asie du Sud-est sont également  hébergés en Asie du Sud-est.  

## <a name="more-information"></a>Plus d’informations
Posez une question sur hello [forum d’Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
