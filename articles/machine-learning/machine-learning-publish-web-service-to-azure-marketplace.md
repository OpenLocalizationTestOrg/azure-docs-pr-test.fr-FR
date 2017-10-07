---
title: web service tooAzure Marketplace apprentissage publication automatique AAA(deprecated) | Documents Microsoft
description: "(déconseillée) Comment toopublish votre toohello de Service Web de Azure Machine Learning Azure Marketplace"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>(déconseillée) Publier le Service Web de Azure Machine Learning toohello Azure Marketplace

> [!NOTE]
> DataMarket et Data Services vont être mis hors service et les abonnements existants seront annulés à compter du 31/03/2017. Par conséquent, cet article deviendra obsolète. 
> 
> En guise d’alternative, vous pouvez publier votre toohello d’expériences d’apprentissage [Cortana Intelligence galerie](https://gallery.cortanaintelligence.com/) pour avantage hello de communauté de science des données hello. Pour plus d’informations, consultez [partager et découvrir des ressources Bonjour Cortana Intelligence galerie](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Bonjour Azure Marketplace permet hello les services web Azure Machine Learning toopublish payée ou libérez de services pour la consommation par les clients externes. Cet article fournit une vue d’ensemble du processus avec des liens tooget de tooguidelines que vous avez démarré. À l’aide de ce processus, vous proposer vos services web pour les autres tooconsume les développeurs dans leurs applications.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>Vue d’ensemble du processus de publication de hello
Hello Voici les étapes de hello pour la publication d’un tooAzure de service web Azure Machine Learning Marketplace :

1. Créez et publiez un service Request-Response (Request-Response Service, service de requête-réponse) Machine Learning
2. Déployez hello service tooproduction et obtenir hello les informations de point de terminaison OData et de la clé d’API.
3. Utilisez les URL de hello Hello publié toopublish de service web trop[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/) 
4. Une fois envoyé, votre offre est examinée et doit toobe approuvée avant son vos clients pouvez commencer à acheter. processus de publication Hello peut prendre de quelques jours ouvrables. 

## <a name="walk-through"></a>Procédure
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>Étape 1 : créez et publiez un RRS (Request-Response Service, service de requête-réponse) Machine Learning
 Si vous ne l’avez pas encore fait, consultez ce [guide](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>Étape 2 : Déployer hello service tooproduction et obtenir hello les informations de point de terminaison OData et de la clé d’API
1. À partir de hello [portail classique Azure](http://manage.windowsazure.com), sélectionnez hello **MACHINE LEARNING** option à partir de la barre de navigation gauche hello et sélectionnez votre espace de travail. 
2. Cliquez sur hello **SERVICES WEB** onglet et sélectionnez hello web vous aimeriez toopublish toohello marketplace.
   
    ![Azure Marketplace][workspace]
3. Sélectionnez le point de terminaison hello vous comme toohave hello marketplace consomme. Si vous n’avez pas créé de points de terminaison supplémentaires, vous pouvez sélectionner hello **par défaut** point de terminaison.
4. Une fois que vous avez cliqué sur le point de terminaison hello, vous serez en mesure de toosee hello **clé API**. Vous aurez besoin de cette information par la suite, lors de l’étape 3. Faites-en une copie.
   
    ![Azure Marketplace][apikey]
5. Cliquez sur hello **demande/réponse** toohello marketplace de services de méthode, à ce stade, nous ne prennent pas en charge la publication de l’exécution par lots. Que vous obtiendrez la page d’aide toohello API hello méthode de demande/réponse.
6. Hello de copie **adresse de point de terminaison OData**, vous devez ces informations ultérieurement à l’étape 3.
   
    ![Azure Marketplace][odata]

déployer un service de hello en production.

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>Étape 3 : Utilisation des URL de hello Hello publié web service toopublish tooAzure Marketplace (DataMarket)
1. Accédez trop[Azure Marketplace (Data Market)](http://datamarket.azure.com/home) 
2. Cliquez sur hello **publier** lien en hello haut hello. Cette opération prendra toohello [portail de publication Microsoft Azure](https://publish.windowsazure.com)
3. Cliquez sur hello **éditeurs** tooregister section comme serveur de publication.
4. Durant la création d’une offre, sélectionnez **Services de données**, puis cliquez sur **Créer un nouveau service de données**. 
   
   ![Azure Marketplace][image1]
   
   <br />
5. Sous **Plans** , indiquez les informations relatives à votre offre, y compris un plan de tarification. Vous pouvez choisir de proposer un service payant ou gratuit. tooget payé, fournissent des informations de paiement telles que vos informations bancaires et les taxes.
6. Sous **Marketing** fournissent des informations sur votre offre, telles que le titre de hello et une description pour votre offre.
7. Sous **tarification** vous pouvez définir les prix hello pour vos plans pour pays spécifiques, ou laissez le système hello « autoprice » dans votre offre.
8. Sur hello **Service de données** , cliquez sur **Service Web** comme hello **Source de données**.
   
    ![Azure Marketplace][image2]
9. Obtenir hello web service URL et la clé API hello portail Azure Classic, comme expliqué à l’étape 2 ci-dessus.
10. Dans la boîte de dialogue de configuration de Service de données Marketplace de hello, collez adresse de point de terminaison OData hello hello **URL du Service** zone de texte.
11. Pour **authentification**, choisissez **en-tête** comme hello **schéma d’authentification**.
    
    * Entrez « Authorization » pour hello **nom d’en-tête**.
    * Pourquoi **valeur d’en-tête**, entrez « Support » (sans les guillemets hello), cliquez sur hello **espace** barre, puis collez la clé d’API de hello.
    * Sélectionnez hello **ce Service est OData** case à cocher.
    * Cliquez sur **tester la connexion** connexion de hello tootest.
12. Sous **Catégories**, assurez-vous que l’option **Apprentissage automatique** est sélectionnée.
13. Lorsque vous avez terminé de saisir toutes hello métadonnées sur votre offre, cliquez sur **publier**, puis **Push tooStaging**. À ce stade, vous soient prévenus de tous les problèmes restants que vous avez besoin de toofix.
14. Une fois que vous avez vérifié que l’achèvement de tous les problèmes en suspens hello, cliquez sur **demander l’approbation toopush tooProduction**. processus de publication Hello peut prendre de quelques jours ouvrables. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

