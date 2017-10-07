---
title: "aaaUse paramètres de Service Web Azure Machine Learning | Documents Microsoft"
description: "Comment toomodify des paramètres de Service Web Azure Machine Learning toouse hello comportement de votre modèle lorsque le service web de hello est accessible."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: 214711eb819a6cea34db905abdf015da11e846d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-web-service-parameters"></a>Utilisation des paramètres de service Web Azure Machine Learning
Un service Web Azure Machine Learning est créé en publiant une expérience qui contient des modules avec des paramètres configurables. Dans certains cas, vous souhaiterez comportement du module hello toochange pendant l’exécution hello web service. *Paramètres de Service Web* permettent de toodo cette tâche. 

Un exemple courant consiste à configurer hello [importer des données] [ reader] module de service web publié de cet utilisateur hello Hello peut spécifier une autre source de données lors de l’accès au service web de hello. Ou la configuration hello [exporter les données] [ writer] module afin qu’une autre destination peut être spécifiée. D’autres exemples incluent la modification du nombre de hello de bits pour hello [Feature Hashing] [ feature-hashing] module ou hello nombre de fonctionnalités pour hello [sélection des fonctionnalités par filtrage] [ filter-based-feature-selection] module. 

Vous pouvez définir des paramètres de service web et les associer à un ou plusieurs paramètres de module dans votre expérience, en spécifiant s’ils sont obligatoires ou facultatifs. utilisateur Hello du service web de hello peut ensuite fournir des valeurs pour ces paramètres lorsqu’il appelle le service web de hello. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-tooset-and-use-web-service-parameters"></a>Comment les paramètres de Service Web tooset et utilisation
Vous définissez un paramètre de Service Web en cliquant sur le paramètre suivant toohello hello icône pour un module et en sélectionnant « Définir en tant que paramètre du service web ». Cela crée un nouveau paramètre de Service Web et le connecte paramètre module de toothat. Ensuite, lorsque le service web de hello est accessible, utilisateur de hello peut spécifier une valeur pour le paramètre du Service Web de hello et il est appliqué toohello module paramètre.

Une fois que vous définissez un paramètre de Service Web, il est disponible tooany autre paramètre de module dans l’expérience de hello. Si vous définissez un paramètre de Service Web associé à un paramètre pour un module, vous pouvez utiliser ce même paramètre de Service Web pour d’autres modules, tant que paramètre hello attend hello même type de valeur. Par exemple, si le paramètre du Service Web de hello est une valeur numérique, puis il peut uniquement être utilisé pour les paramètres du module qui attendent une valeur numérique. Hello définit une valeur pour le paramètre du Service Web de hello, il s’agit des paramètres du module appliqué tooall associé.

Vous pouvez décider si une valeur par défaut de tooprovide valeur pour hello paramètre du Service Web. Si vous, puis hello paramètre est facultatif pour l’utilisateur hello du service web de hello. Si vous ne fournissez une valeur par défaut, utilisateur de hello est tooenter requis une valeur lorsque le service web de hello est accessible.

Hello documentation API pour le service web de hello inclut des informations pour l’utilisateur du service web hello sur comment toospecify hello paramètre du Service Web par programmation lorsque vous accédez hello web service.

> [!NOTE]
> Hello documentation API pour un service web classique est fourni via hello **page d’aide API** lien dans le service web hello **tableau de bord** dans Machine Learning Studio. Hello documentation API pour un service web est fourni via hello [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portail sur hello **consommer** et **Swagger les API** pages pour votre service Web.
> 
> 

## <a name="example"></a>Exemple
Par exemple, supposons que nous disposons d’une expérience avec un [exporter les données] [ writer] module qui envoie le stockage d’objets blob tooAzure plus d’informations. Nous allons définir un paramètre de Service Web nommé « Chemin d’accès d’objets Blob » qui permet de hello web service utilisateur toochange hello chemin d’accès toohello stockage d’objets blob lorsque le service de hello est accessible.

1. Dans Machine Learning Studio, cliquez sur hello [exporter les données] [ writer] module tooselect il. Ses propriétés s’affichent dans hello propriétés volet toohello à droite de la zone de dessin expérience hello.
2. Spécifiez le type de stockage hello :
   
   * Sous le message **Veuillez spécifier la destination des données**, sélectionnez « Stockage d'objets blob Azure ».
   * Sous le message **Veuillez spécifier le type d'authentification**, sélectionnez « Compte ».
   * Entrez les informations de compte hello pour hello stockage d’objets blob Azure. 
     <p />
3.Cliquez sur toohello d’icône hello à droite de hello **chemin tooblob commence avec le paramètre container**. Voici à quoi cela ressemble :
   
   ![Icône de paramètre de service Web][icon]
   
   Sélectionnez « Définir en tant que paramètre du service Web ».
   
   Une entrée est ajoutée sous **paramètres de Service Web** bas hello du volet des propriétés avec hello nom « chemin d’accès tooblob commençant par le conteneur » hello. Il s’agit de hello paramètre du Service Web qui est désormais associé à cet [exporter les données] [ writer] paramètre module.
4. toorename hello paramètre du Service Web, cliquez sur le nom de hello, entrez « Chemin d’accès d’objets Blob » et appuyez sur hello **entrée** clé. 
5. tooprovide une valeur par défaut pour hello paramètre du Service Web, cliquez sur toohello d’icône hello à droite du nom de hello, sélectionnez « Fournir la valeur par défaut », entrez une valeur (par exemple, « container1/output1.csv ») et appuyez sur hello **entrée** clé.
   
   ![Paramètre de service Web][parameter]
6. Cliquez sur **Exécuter**. 
7. Cliquez sur **déployer le Service Web** et sélectionnez **déployer le Service Web [standard]** ou **déployer le Service Web [nouveau]** service web de hello toodeploy.

> [!NOTE] 
> toodeploy un nouveau service web, vous devez disposer des autorisations suffisantes dans hello abonnement toowhich vous déployez le service web de hello. Pour plus d’informations, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md). 

Hello utilisateur du service web de hello peut maintenant spécifier une nouvelle destination pour hello [exporter les données] [ writer] module lors de l’accès au service web de hello.

## <a name="more-information"></a>Plus d’informations
Pour obtenir un exemple plus détaillé, consultez hello [paramètres de Service Web](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entrée Bonjour [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).

Pour plus d’informations sur l’accès au service web Machine Learning, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

<!-- Images -->
[icon]: ./media/machine-learning-web-service-parameters/icon.png
[parameter]: ./media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/

