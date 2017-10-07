---
title: "un modèle d’apprentissage automatique d’aaaRetrain | Documents Microsoft"
description: "Découvrez comment tooretrain un modèle et mise à jour hello Web service toouse hello qui vient d’être formé dans Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a>Reformer un modèle Machine Learning
Dans le cadre du processus de hello d’une Opérationnalisation rapides des modèles d’apprentissage automatique dans Azure Machine Learning, votre modèle est formé et enregistré. Vous utiliser toocreate un service Web predicative. Hello service Web peut ensuite être consommé dans les sites web, des tableaux de bord et des applications mobiles. 

Les modèles que vous créez à l’aide de Machine Learning ne sont généralement pas statiques. Comme de nouvelles données sont disponibles ou lorsque le consommateur hello Hello API a son propre modèle de hello de données doit toobe reformé. 

Il peut être très fréquent d’avoir à effectuer à nouveau l’apprentissage du modèle. Par programme avec la fonctionnalité de programmation API réapprentissage hello, recycler modèle hello utilisation hello API de réapprentissage et de mise à jour hello Web service avec des qui vient d’être formé hello. 

Ce document décrit les hello recyclage de processus et vous montre comment toouse hello réapprentissage des API.

## <a name="why-retrain-defining-hello-problem"></a>Pourquoi recycler : définition hello problème
Dans le cadre de l’apprentissage hello processus d’apprentissage, un modèle est formé à l’aide d’un jeu de données. Les modèles que vous créez à l’aide de Machine Learning ne sont généralement pas statiques. Comme de nouvelles données sont disponibles ou lorsque le consommateur hello Hello API a son propre modèle de hello de données doit toobe reformé.

Dans ces scénarios, une API de programmation fournit un moyen pratique de tooallow vous ou hello consommateur de votre toocreate API un client qui peut, sur une base ponctuelle ou régulière, recycler modèle hello à l’aide de leurs propres données. Ils peuvent évaluer les résultats de hello de recyclage puis hello Web service API toouse hello qui vient d’être formé de mettre à jour.

> [!NOTE]
> Si vous avez une expérience d’apprentissage existants et le service d’un site Web, vous souhaiterez toocheck out recyclage d’un site Web existant prédictive de service au lieu de suivant hello procédure pas à pas mentionnées dans hello suivant la section.
> 
> 

## <a name="end-to-end-workflow"></a>Workflow de bout en bout
processus Hello implique hello suivant composants : expérience d’apprentissage A et une expérience prédictive publiées en tant qu’un service Web. tooenable réapprentissage d’un modèle formé, hello expérience d’apprentissage doit être publiée en tant qu’un service Web avec la sortie de hello d’un modèle formé. Ainsi, le modèle de toohello d’accès API à instruire de nouveau. 

Hello comme suit s’appliquent tooboth nouveau et classique des services Web :

Créer un service Web prédictif initial de hello :

* Créez une expérience d'apprentissage
* Créez une expérience prédictive
* Déployez un service web prédictif

Recycler le service Web de hello :

* Mettre à jour tooallow d’expérience de formation à instruire de nouveau
* Déployer hello recyclage du service web
* Utiliser le modèle hello tooretrain hello Batch Execution Service code

Pour une procédure pas à pas de hello étapes précédentes, consultez [recycler l’apprentissage des modèles par programme](machine-learning-retrain-models-programmatically.md).

> [!NOTE] 
> toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello. Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Si vous avez déployé un service web classique :

* Créer un nouveau point de terminaison de service Web prédictif de hello
* Obtenir l’URL de correctif hello et le code
* Utilisez Bonjour de correctif logiciel des URL toopoint Bonjour nouveau point de terminaison à hello reformés modèle 

Pour une procédure pas à pas de hello étapes précédentes, consultez [recycler un service Web classique](machine-learning-retrain-a-classic-web-service.md).

Si vous rencontrez des difficultés de recyclage d’un service Web classique, consultez [dépannage hello recyclage d’un service Web classique de Azure Machine Learning](machine-learning-troubleshooting-retraining-models.md).

Si vous avez déployé un nouveau service web :

* Connectez-vous à tooyour compte de gestionnaire de ressources Azure
* Obtenir la définition du service Web hello
* Exportation hello définition du Service Web en tant que JSON
* Mettre à jour hello référence toohello `ilearner` blob Bonjour JSON
* Importer des hello JSON dans une définition de Service Web
* Mettre à jour de service Web de hello avec la nouvelle définition de Service Web

Pour une procédure pas à pas de hello étapes précédentes, consultez [recycler un service d’un site Web à l’aide des applets de commande PowerShell de gestion de Machine Learning hello](machine-learning-retrain-new-web-service-using-powershell.md).

processus de Hello pour configurer le recyclage d’un service Web classique comprend hello comme suit :

![Présentation du processus de nouvel apprentissage.][1]

processus Hello pour configurer le recyclage d’un service d’un site Web implique hello comme suit :

![Présentation du processus de nouvel apprentissage.][7]

## <a name="other-resources"></a>Autres ressources
* [Reformation et mise à jour de modèles Microsoft Azure Machine Learning avec Azure Data Factory](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [Créer de nombreux modèles Machine Learning et points de terminaison de service web à partir d’une expérience à l’aide de PowerShell](machine-learning-create-models-and-endpoints-with-powershell.md)
* Hello [agréés réapprentissage des API à l’aide de modèles](https://www.youtube.com/watch?v=wwjglA8xllg) vidéo vous montre comment les modèles de Machine Learning tooretrain créés dans Azure Machine Learning à l’aide de hello PowerShell et API de recyclage.

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

