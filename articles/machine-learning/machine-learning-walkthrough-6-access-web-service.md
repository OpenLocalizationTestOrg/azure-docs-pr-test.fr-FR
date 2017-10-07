---
title: "Étape 6 : Accéder au service de Machine Learning Web hello | Documents Microsoft"
description: "Étape 6 de hello développer la procédure pas à pas une solution prédictive : accéder à un service Web de Azure Machine Learning actif."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a>Étape 6 de la procédure pas à pas : Service web de Azure Machine Learning hello accéder à

C’est hello dernière étape de la procédure pas à pas de hello, [développer une solution prédictive analytique dans Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)

1. [Créer un espace de travail Machine Learning](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [Télécharger des données existantes](machine-learning-walkthrough-2-upload-data.md)
3. [Créer une expérience](machine-learning-walkthrough-3-create-new-experiment.md)
4. [L’apprentissage et évaluer des modèles de hello](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [Déployer le service Web de hello](machine-learning-walkthrough-5-publish-web-service.md)
6. **Accéder au service Web de hello**

- - -
À l’étape précédente de hello dans cette procédure pas à pas, nous avons déployé un service web qui utilise de notre modèle de prévision de risque de crédit. Désormais, les utilisateurs sont en mesure de toosend données tooit et recevoir les résultats. 

Hello service Web est un service web Azure qui peut recevoir et retourner des données à l’aide des API REST de deux manières :  

* **Demande/réponse** - utilisateur de hello envoie un ou plusieurs lignes de toohello de données de crédit de service à l’aide d’un protocole HTTP et hello répond de service avec un ou plusieurs jeux de résultats.
* **L’exécution du lot** - utilisateur de hello stocke une ou plusieurs lignes de données de crédit dans Azure d’objets blob et envoie ensuite le service de toohello emplacement hello blob. les scores de service Hello dans que tous hello des lignes de données Bonjour blob d’entrée, magasins hello aboutit à un autre objet blob et retourne hello URL de ce conteneur.  

Hello tooaccess moyen le plus rapide et plus simple est d’un service web de classique via hello [l’application Web Azure ML avec requête-réponse Service](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) ou [modèle d’application Azure ML lot l’exécution du Service Web](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).

Ces modèles d'applications web peuvent générer une application Web personnalisée qui connaît les données d'entrée et les résultats attendus de votre service Web. Vous toodo suffit de fournir des données et accès tooyour web service et le modèle de hello hello rest.

Pour plus d’informations sur l’utilisation de modèles d’application web hello, consultez [consommer un service Web de Azure Machine Learning avec un modèle d’application web](machine-learning-consume-web-service-with-web-app-template.md).

Vous pouvez également développer tooaccess hello web service d’application personnalisé à l’aide de code de démarrage fourni pour vous dans R, c# et langages de programmation Python.

Vous trouverez plus de détails dans [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

