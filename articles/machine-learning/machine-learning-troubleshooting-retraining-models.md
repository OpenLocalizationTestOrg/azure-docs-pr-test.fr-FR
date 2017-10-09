---
title: "service web d’aaaTroubleshoot réapprentissage un Azure Machine Learning Classic | Documents Microsoft"
description: "Identifiez et corrigez rencontré de problèmes courants lorsque vous sont former le modèle de hello pour un Service Web de Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a>Résolution des problèmes de hello recyclage d’un service Web classique de Azure Machine Learning
## <a name="retraining-overview"></a>Vue d’ensemble de la reformation
Lorsque vous déployez une expérience prédictive en tant que service web d’évaluation, il s’agit d’un modèle statique. Comme les nouvelles données sont disponibles ou lorsque le consommateur hello Hello API a ses propres données, modèle de hello doit toobe reformé. 

Pour obtenir une description complète de hello recyclage de processus d’un service Web classique, consultez [recycler Machine Learning modèles par programme](machine-learning-retrain-models-programmatically.md).

## <a name="retraining-process"></a>Processus de reformation
Lorsque vous devez tooretrain hello service Web, vous devez ajouter certains éléments supplémentaires :

* Un service Web est déployé à partir de hello expérience d’apprentissage. expérience de Hello doit avoir un **sortie du Service Web** module attaché sortie toohello Hello **Train Model** module.  
  
    ![Attacher le modèle de hello web service sortie toohello train.][image1]
* Un nouveau point de terminaison ajouté tooyour calcul du score du service Web.  Vous pouvez ajouter des point de terminaison hello par programmation à l’aide des exemples de code hello référencés Bonjour recycler l’apprentissage des modèles par programme rubrique ou via hello portail Azure classic.

Vous pouvez ensuite utiliser hello exemple c# code à partir API aide page tooretrain modèle du Service Web hello formation. Une fois que vous avez évalué les résultats hello et soyez satisfaisants, vous mettez à jour formé hello calcul du score du service web à l’aide de hello nouveau point de terminaison que vous avez ajouté.

Avec tous les éléments de hello en place, les étapes majeures hello vous devez prendre le modèle de hello tooretrain sont les suivantes :

1. Appelez hello Service Web de formation : appel de hello est toohello Service de l’exécution de lot (BES), ne Hello pas les demandes de Service de réponse (RR). Vous pouvez utiliser le code c# exemple hello astreinte hello API aide page toomake hello. 
2. Rechercher les valeurs hello hello *BaseLocation*, *RelativeLocation*, et *SasBlobToken*: ces valeurs sont retournées dans la sortie de hello à partir de votre toohello appel Web de formation Service. 
   ![affichage de sortie hello Hello réapprentissage exemple et hello BaseLocation, RelativeLocation et SasBlobToken des valeurs.][image6]
3. Mise à jour hello ajouté modèle entraîné de point de terminaison de hello score de nouveau service web avec hello : à l’aide des exemples de code hello fournies hello recycler l’apprentissage des modèles par programmation, mettre à jour nouveau point de terminaison hello, vous avez ajouté toohello score du modèle avec hello récemment modèle formé à partir de hello formation Web Service.

## <a name="common-obstacles"></a>Obstacles courants
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a>Vérifiez toosee si vous avez hello Corrigez-la de correctif logiciel
Hello URL de correctif logiciel que vous utilisez doit être hello associé hello nouveau calcul du score du point de terminaison que vous avez ajouté toohello calcul du score du service Web. Il existe un certain nombre de façons tooobtain hello de correctif logiciel des URL :

**Option 1 : par programme**

tooget hello Corrigez-la de correctif logiciel :

1. Exécutez hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) exemple de code.
2. À partir de la sortie de hello de AddEndpoint, recherche hello *HelpLocation* valeur et copier l’URL de hello.
   
   ![HelpLocation sortie hello addEndpoint exemple hello.][image2]
3. Collez hello URL dans une page du navigateur toonavigate tooa qui fournit des liens d’aide pour le service Web de hello.
4. Cliquez sur hello **mise à jour de ressource** page d’aide lien tooopen hello correctif.

**Option 2 : Utiliser hello portail Azure classic**

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Onglet d’apprentissage hello ouvert. ![Onglet Machine Learning.][image4]
3. Cliquez sur le nom de votre espace de travail, puis sur **Services web**.
4. Cliquez sur hello calcul du score du service Web que vous utilisez. (Si vous n’avez pas modifié le nom par défaut de hello du service web de hello, il va se terminer dans [score Exp.].)
5. Cliquez sur **Ajouter un point de terminaison**.
6. Une fois le point de terminaison hello est ajouté, cliquez sur nom de point de terminaison hello. Puis cliquez sur **mise à jour de ressource** tooopen hello correction page d’aide.

> [!NOTE]
> Si vous avez ajouté toohello de point de terminaison hello Service Web de formation au lieu de hello prédictive Service Web, vous recevrez l’erreur suivante lorsque vous cliquez sur hello de hello **mise à jour de ressource** lien : nous sommes désolés, mais cette fonctionnalité n’est pas prise en charge ou disponible dans ce contexte. Ce service web n’a aucune ressource actualisable. Nous excuser pour tout désagrément de hello et que vous travaillez sur l’amélioration de ce flux de travail.
> 
> 

![Nouveau tableau de bord de point de terminaison.][image3]

page d’aide du correctif Hello contient hello correctif URL, vous devez utiliser et fournit des exemples de code que vous pouvez utiliser toocall il.

![URL d’application de correctifs.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a>Vérifiez que vous mettez à jour point de terminaison hello correct score de toosee
* Pas de correctif logiciel hello Service Web de formation : opération de hello patch doit être effectuée sur hello calcul du score du service Web.
* Correctif pas de point de terminaison hello par défaut sur le service Web : opération de hello patch doit être effectuée sur hello nouveau calcul du score du point de terminaison Web service que vous avez ajouté.

Vous pouvez vérifier quel point de terminaison Web service hello est sous tension en visite hello portail Azure classic. 

> [!NOTE]
> Assurez-vous que vous ajoutez toohello de point de terminaison hello prédictive Web Service, pas hello formation Web Service. Si vous avez correctement déployé à la fois un service web prédictif et un service web de formation, vous devez voir deux services web distincts répertoriés. Hello prédictive Service Web doit se terminer par « [exp prédictive.] ».
> 
> 

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Onglet d’apprentissage hello ouvert. ![Interface utilisateur de l’espace de travail Machine Learning.][image4]
3. Sélectionnez votre espace de travail.
4. Cliquez sur **Services web**.
5. Sélectionnez votre service web prédictif.
6. Vérifiez que votre nouveau point de terminaison a été ajouté de service Web de toohello.

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a>Vérifiez l’espace de travail hello que votre service web est en tooensure, qu'il se trouve dans la région correcte de hello
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Sélectionnez la Machine Learning à partir du menu de hello.
   ![Interface utilisateur de la région Machine Learning.][image4]
3. Vérifiez l’emplacement hello de votre espace de travail.

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
