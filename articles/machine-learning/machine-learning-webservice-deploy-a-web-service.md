---
title: aaaDeploying un nouveau service web dans Azure Machine Learning | Documents Microsoft
description: "flux de travail Hello du déploiement d’un ARM en fonction de service web"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>Déployer comme un nouveau service web
Fournit des services web basés sur Microsoft Azure Machine learning maintenant [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permettant de nouvelles options de plan de facturation et déployer vos régions toomultiple du service web.

toodeploy de flux de travail général Hello un service web à l’aide des Services Web de Microsoft Azure Machine Learning est la suivante :

* Créer une expérience prédictive
* la déployer
* choisir son nom
* profil de facturation
* la tester
* l’utiliser.

Hello graphique suivant illustre le flux de travail hello.

![Flux de travail du déploiement d’un service web][1]

## <a name="deploy-web-service-from-studio"></a>Déployer un service web à partir de Studio
toodeploy une expérience en tant qu’un nouveau service web. Connectez-vous à hello Machine Learning Studio et créez un service web prédictif. 

**Remarque**: si vous avez déjà déployé une expérience en tant que service web classique, vous ne pouvez pas le déployer en tant que nouveau service web.

Cliquez sur **exécuter** bas hello hello expérimenter la zone de dessin, puis cliquez sur **déployer le Service Web** et **déployer le Service Web [nouveau]**. page de déploiement de Hello du Gestionnaire de Service Web de Machine Learning hello s’ouvre.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>Page d’expérience de déploiement du Gestionnaire de service web Machine Learning
Sur la page de déployer une expérience de hello, entrez un nom pour le service web de hello.
Sélectionnez un plan de tarification. Si vous avez un plan de tarification existant, que vous pouvez le sélectionner, sinon vous devez créer un nouveau plan de prix pour le service de hello. 

1. Bonjour **Plan tarifaire** liste déroulante, sélectionnez un plan existant ou hello **sélectionnez Nouveau plan** option.
2. Dans **le nom du Plan**, tapez un nom qui identifie le plan hello sur votre facture.
3. Sélectionnez une des hello **niveaux de planification mensuelle**. Notez que les niveaux de plan hello par défaut toohello des plans pour votre région par défaut et votre service web est déployé toothat région.

Cliquez sur **déployer** et de la page de démarrage rapide de hello pour votre service web s’ouvre.

## <a name="quickstart-page"></a>Page Démarrage rapide
page de démarrage rapide du service web Hello vous donne accès et des conseils sur les tâches les plus courantes hello que vous allez effectuer après la création d’un nouveau service web. À ce stade, vous pouvez facilement accéder à la fois hello **Test** page et **consommer** page.

## <a name="testing-your-web-service"></a>Test de votre service web
À partir de la page de démarrage rapide de hello, cliquez sur service web de Test, sous tâches courantes.   

service de tootest hello web comme un Service de requête-réponse (RR) :

* Cliquez sur **Test** sur la barre de menus hello.
* Cliquez sur **Request-Response**(Requête-réponse).
* Entrez les valeurs appropriées pour les colonnes d’entrée hello votre expérience.
* Cliquez sur Tester **requête-réponse**.

Résultat s’affiche sur la droite hello de page de hello.

tootest un service web de Service de l’exécution de lot (BES), vous allez utiliser un fichier CSV :

* Cliquez sur **Test** sur la barre de menus hello.
* Cliquez sur **Lot**.
* Sous votre entrée, cliquez sur Parcourir et naviguez tooyour exemple de fichier de données.
* Cliquez sur **Test**.

état de Hello de votre test s’affiche sous **tester des traitements par lots**.

## <a name="consuming-your-web-service"></a>Utilisation de votre service web
Lors de leur déploiement en tant que services web, les expériences Azure Machine Learning proposent une API REST, qui peut être exploitée par divers périphériques et plateformes. Il s’agit, car des messages au format hello simple API REST accepte et répond avec JSON. Hello portail d’Azure Machine Learning fournit du code qui peut être utilisé toocall hello web service R, c# et Python.

Sur la page de consommation hello, vous pouvez rechercher :

* clé de l’API de Hello et URI pour la consommation de service web dans les applications.
* Tookick de modèles d’application web d’Excel et de démarrer votre consommation.
* Exemple de code dans c#, python et R tooget que vous avez démarré.

Pour plus d’informations sur l’utilisation des services web, consultez [comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des services web, consultez :

[Comment tooconsume un service Web de Azure Machine Learning](machine-learning-consume-web-services.md)

[Services web Azure Machine Learning : déploiement et consommation](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
