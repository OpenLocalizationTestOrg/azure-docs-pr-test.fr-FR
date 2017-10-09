---
title: aaaAzure IoT Suite FAQ | Documents Microsoft
description: "Forum Aux Questions (FAQ) relatives à IoT Suite"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a>Forum Aux Questions (FAQ) relatives à IoT Suite

Voir aussi, hello fabrique connecté spécifique [FAQ](iot-suite-faq-cf.md).

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a>Où puis-je trouver code source de hello pour les solutions hello préconfiguré ?

code source de Hello est stocké dans hello suivant des dépôts GitHub :
* [Solution préconfigurée de surveillance à distance][lnk-remote-monitoring-github]
* [Solution préconfigurée de maintenance prédictive][lnk-predictive-maintenance-github]
* [Solution préconfigurée d’usine connectée](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a>Comment mettre à jour toohello version la plus récente de la solution préconfigurée hello surveillance à distance qu’utilise hello des fonctionnalités de gestion des appareils IoT Hub ?

* Si vous déployez une solution préconfigurée à partir du site de https://www.azureiotsuite.com/ hello, il déploie toujours une nouvelle instance de la version la plus récente de la solution de hello hello.
* Si vous déployez une solution préconfigurée, à l’aide de la ligne de commande hello, vous pouvez mettre à jour un déploiement existant par un nouveau code. Consultez [déploiement de cloud computing] [ lnk-cloud-deployment] Bonjour GitHub [référentiel][lnk-remote-monitoring-github].

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a>Comment puis-je ajouter la prise en charge pour une solution préconfigurée de surveillance à distance appareil méthode toohello nouveau ?

Consultez la section de hello [ajouter la prise en charge pour un simulateur de toohello nouvelle méthode] [ lnk-add-method] Bonjour [personnaliser une solution préconfigurée] [ lnk-customize] l’article.

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a>APPAREIL simulé de Hello ignore mes modifications de la propriété souhaitée, pourquoi ?
Bonjour surveillance à distance solution préconfigurée, hello simulée périphérique code utilise uniquement hello **Desired.Config.TemperatureMeanValue** et **Desired.Config.TelemetryInterval** propriétés souhaitée tooupdate hello a signalé des propriétés. Toutes les autres demandes de modification de propriétés souhaitées sont ignorées.

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a>Mon appareil n’apparaît pas dans la liste de hello des périphériques dans le tableau de bord solution hello, pourquoi ?

liste de Hello des périphériques dans le tableau de bord hello solution utilise une liste de hello de tooreturn de requête de périphériques. Pour le moment, une requête ne peut pas retourner plus de 10 000 appareils. Essayez de critères de recherche hello pour votre requête plus restrictive.

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a>Qu’est la différence de hello entre la suppression d’un groupe de ressources Bonjour Azure portail et en cliquant sur Supprimer une solution préconfigurée dans azureiotsuite.com ?

* Si vous supprimez la solution hello préconfiguré dans [azureiotsuite.com][lnk-azureiotsuite], vous supprimez toutes les ressources hello qui ont été configurés lors de la création de solutions de hello préconfiguré. Si vous avez ajouté le groupe de ressources toohello des ressources supplémentaires, ces ressources sont également supprimés. 
* Si vous supprimez le groupe de ressources hello Bonjour [portail Azure][lnk-azure-portal], vous supprimez uniquement les ressources, hello dans ce groupe de ressources. Vous devez également l’application d’Azure Active Directory hello toodelete associée solution hello préconfiguré Bonjour [portail Azure classic][lnk-classic-portal].

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a>Combien d’instances d’IoT Hub puis-je configurer dans un abonnement ?

Par défaut, vous pouvez configurer [10 instances IoT Hub par abonnement][link-azuresublimits]. Vous pouvez créer un [ticket de support Azure] [ link-azuresupportticket] tooraise cette limite. Par conséquent, depuis chaque dispositions solution préconfigurée un IoT Hub, vous ne pouvez configurer des too10 préconfiguré solutions dans un abonnement donné. 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a>Combien d’instances d’Azure Cosmos DB puis-je configurer dans un abonnement ?

Cinquante. Vous pouvez créer un [ticket de support Azure] [ link-azuresupportticket] tooraise cette limite, mais par défaut, vous ne pouvez configurer des instances de base de données Cosmos 50 par abonnement. 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a>Combien d’API Bing Maps gratuites puis-je configurer dans un abonnement ?

Deux. Vous pouvez créer uniquement deux cartes Bing - Transactions internes - Niveau 1 pour les plans d’entreprise dans un abonnement Azure. solution de surveillance à distance Hello est configurée par défaut avec un plan hello interne des Transactions au niveau 1. Par conséquent, vous ne pouvez configurer que des tootwo distant solutions dans un abonnement sans modification de contrôle.

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a>J’ai mis en place le déploiement d’une solution de surveillance à distance avec une carte statique. Comment faire pour ajouter une carte Bing interactive ?

1. Obtenez votre QueryKey Bing Maps API pour Entreprise sur le [portail Azure][lnk-azure-portal] : 
   
   1. Accédez toohello groupe de ressources où votre API Bing Maps pour Enterprise est Bonjour [portail Azure][lnk-azure-portal].
   2. Cliquez sur **Tous les paramètres**, puis sur **Gestion des clés**. 
   3. Vous voyez deux clés : **MasterKey** et **QueryKey**. Copiez la valeur hello pour **QueryKey**.
      
      > [!NOTE]
      > Vous n’avez aucun compte Bing Maps API pour Entreprise ? Créer un dans hello [portail Azure] [ lnk-azure-portal] en cliquant sur + Nouveau, recherche de l’API Bing Maps pour Enterprise et suivre invite toocreate.
      > 
      > 
2. Liste déroulante code dernière hello hello [Azure-IoT-de surveillance à distance][lnk-remote-monitoring-github].
3. Exécuter un local ou cloud de déploiement suivant hello les instructions de déploiement de ligne de commande dans le dossier de /docs/ hello dans le référentiel de hello. 
4. Une fois que vous avez exécuté un local ou cloud de déploiement, recherchez dans votre dossier racine pour hello *. fichier user.config créé au cours du déploiement. Ouvrez ce fichier dans un éditeur de texte. 
5. Valeur de hello tooinclude vous avez copié à partir de la ligne suivante de hello de modifier votre **QueryKey**: 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a>Puis-je créer une solution préconfigurée si je dispose de Microsoft Azure pour DreamSpark ?

Actuellement, il est impossible de créer une solution préconfigurée avec un compte [Microsoft Azure pour DreamSpark][lnk-dreamspark]. Vous pouvez toutefois créer en quelques minutes un [compte d’évaluation Azure gratuit][lnk-30daytrial], que vous pouvez utiliser pour créer une solution préconfigurée.

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a>Puis-je créer une solution préconfigurée si j’ai un abonnement du fournisseur de solutions Cloud (CSP) ?

Actuellement, vous ne pouvez pas créer de solution préconfigurée avec un abonnement de fournisseur de solutions Cloud (CSP). Vous pouvez toutefois créer en quelques minutes un [compte d’évaluation Azure gratuit][lnk-30daytrial], que vous pouvez utiliser pour créer une solution préconfigurée.

### <a name="how-do-i-delete-an-aad-tenant"></a>Comment supprimer un client AAS ?

Consultez le billet de blog d’Eric Golpe, [Procédure pas à pas pour la suppression d’un client Azure AD][lnk-delete-aad-tennant].

### <a name="next-steps"></a>Étapes suivantes

Vous pouvez également découvrir hello autres et les fonctionnalités des solutions de IoT Suite préconfiguré hello :

* [Présentation de la solution préconfigurée de maintenance prédictive][lnk-predictive-overview]
* [Présentation de la solution préconfigurée d’usine connectée](iot-suite-connected-factory-overview.md)
* [IoT hello d’arrière-plan la sécurité][lnk-security-groundup]

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
