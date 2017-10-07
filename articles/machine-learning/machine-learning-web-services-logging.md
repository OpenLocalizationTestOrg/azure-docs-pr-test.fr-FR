---
title: aaaLogging pour les services web Machine Learning | Documents Microsoft
description: "Découvrez comment les services web tooenable la journalisation pour l’apprentissage. Journalisation fournit des informations supplémentaires toohelp dépanner hello API."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>Activation de la journalisation pour les services Web de Machine Learning
Ce document fournit des informations sur hello journalisation capacité de services web Machine Learning. Journalisation fournit des informations supplémentaires, au-delà d’un numéro d’erreur et un message, qui peut vous aider à résoudre les problèmes de votre toohello d’appels API de Machine Learning.  

## <a name="how-tooenable-logging-for-a-web-service"></a>Comment tooenable la journalisation pour un service Web

Vous activez la journalisation dans hello [Azure Machine Learning Services Web](https://services.azureml.net) portail. 

1. Connectez-vous au portail de Services Web de Azure Machine Learning toohello à [https://services.azureml.net](https://services.azureml.net). Pour un service web standard, vous pouvez également obtenir toohello portail en cliquant sur **nouvelle expérience de Services Web** sur la page des Services Web de Machine Learning hello dans Machine Learning Studio.

   ![Lien Nouvelle expérience de services web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Dans la barre de menus supérieure hello, cliquez sur **Services Web** pour un nouveau service web, ou cliquez sur **classique des Services Web** pour un classique de service web.

   ![Sélectionner les services web nouveaux ou classiques](media/machine-learning-web-services-logging/select-web-service.png)

3. Pour un service web, cliquez sur le nom du service web hello. Pour un service web standard, cliquez sur le nom du service web hello, puis cliquez sur la page suivante de hello point de terminaison approprié hello.

4. Dans la barre de menus supérieure hello, cliquez sur **configurer**.

5. Ensemble hello **activer la journalisation** option trop*erreur* (toolog les erreurs uniquement) ou *tous les* (pour la journalisation complète).

   ![Sélectionner le niveau de journalisation](media/machine-learning-web-services-logging/enable-logging.png)

6. Cliquez sur **Enregistrer**.

7. Pour les services web standard créer hello **ml-diagnostics** conteneur.

   Tous les journaux de service web sont conservés dans un conteneur d’objets blob nommé **ml-diagnostics** hello compte de stockage associé au service web de hello. Pour les nouveaux services web, ce conteneur est créé hello lors du premier qu'accès de service web de hello. Pour les services web standard, vous avez besoin de conteneur de hello toocreate s’il n’existe pas. 

   1. Bonjour [portail Azure](https://portal.azure.com), accédez toohello compte de stockage associé au service web de hello.

   2. Sous **Service Blob**, cliquez sur **Conteneurs**.

   3. Si le conteneur de hello **ml-diagnostics** n’existe pas, cliquez sur **+ conteneur**, donnez à hello conteneur hello nom « ml-diagnostics » et sélectionnez hello **type d’accès** en tant que « Blob ». Cliquez sur **OK**.

      ![Sélectionner le niveau de journalisation](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> Pour un service web classique, hello Web Services du tableau de bord dans Machine Learning Studio dotée d’un commutateur de tooenable la journalisation. Toutefois, étant donné que la journalisation est gérée via le portail de Services Web hello, vous devez tooenable journalisation via le portail hello comme décrit dans cet article. Si vous déjà activé l’enregistrement dans Studio, puis dans le portail de Services Web de hello, désactiver la journalisation, puis réactivez-la.


## <a name="hello-effects-of-enabling-logging"></a>effets Hello d’activation de la journalisation
Lorsque la journalisation est activée, les erreurs à partir du point de terminaison de service hello web et diagnostics de hello sont enregistrés dans hello **ml-diagnostics** conteneur d’objets blob dans le compte de stockage Azure de hello lié avec l’espace de travail de l’utilisateur hello. Ce conteneur conserve toutes les informations de diagnostics de hello pour tous les postes clients hello web service pour tous les espaces de travail hello associés à ce compte de stockage.

Hello journaux peuvent être affichés à l’aide de hello plusieurs outils tooexplore à disposition un compte de stockage Azure. Hello plus simple peut être le compte de stockage toohello toonavigate hello portail Azure, cliquez sur **conteneurs**, puis cliquez sur le conteneur de hello **ml-diagnostics**.  

## <a name="log-blob-detail-information"></a>Journaliser les informations détaillées sur l’objet blob
Chaque objet blob dans le conteneur de hello conserve des informations de diagnostics hello pour un seul de hello suivant des actions :

* L’exécution de la méthode hello lot en cours d’exécution  
* L’exécution de la méthode hello demande-réponse  
* l’initialisation d'un conteneur de requête-réponse

nom Hello de chaque objet blob a un préfixe de hello suivant du formulaire : 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


Où _type journal_ est une des valeurs suivantes de hello :  

* lot  
* score/requests  
* score/init  

