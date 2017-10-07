---
title: "aaaMonitor base de données Azure Cosmos demandes et stockage | Documents Microsoft"
description: "Découvrez comment toomonitor votre base de données Azure Cosmos tenir compte des mesures de performance, tels que les demandes et les erreurs de serveur et les métriques d’utilisation, telles que la consommation du stockage."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 4c6a2e6f-6e78-48e3-8dc6-f4498b235a9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: mimig
ms.openlocfilehash: aea029d10717236a573a080dab9d06d87f97f318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-cosmos-db-requests-usage-and-storage"></a>Surveiller le stockage, l’utilisation et les demandes Azure Cosmos DB
Vous pouvez surveiller vos comptes de base de données Azure Cosmos Bonjour [portail Azure](https://portal.azure.com/). Pour chaque compte Azure Cosmos DB, des mesures de performances (notamment les demandes et les erreurs de serveur) et des mesures d’utilisation (par exemple l’espace de stockage utilisé) sont disponibles.

Métriques peuvent être consultés sur le panneau de compte hello, nouveau panneau des métriques hello, ou dans le moniteur de Azure.

## <a name="view-performance-metrics-on-hello-metrics-blade"></a>Afficher les métriques de performances sur le panneau de métriques hello
1. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **plus Services**, faites défiler trop**bases de données**, cliquez sur **base de données Azure Cosmos**, puis cliquez sur nom hello Hello Compte Cosmos DB Azure pour lequel vous souhaitez que les mesures de performances tooview.
2. Dans le menu de ressource hello, sous **analyse**, cliquez sur **métriques**.

Panneau de métriques Hello s’ouvre et vous pouvez sélectionner hello collection tooreview. Vous pouvez consulter des métriques de disponibilité, de requêtes, de débit et de stockage et les comparer toohello Azure Cosmos DB SLA.

## <a name="view-performance-metrics-by-using-azure-monitoring"></a>Affichage des mesures de performances à l’aide de la surveillance Azure
1. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **moniteur** sur hello Jumpbar.
2. Dans le menu de ressource hello, cliquez sur **métriques**.
3. Bonjour **moniteur - métriques** fenêtre hello **groupe de ressources** menu déroulant, groupe de ressources hello sélectionnez associé au compte de base de données Azure Cosmos hello que vous aimeriez toomonitor. 
4. Bonjour **ressource** menu déroulant, sélectionnez hello de base de données compte toomonitor.
5. Dans la liste des hello **métriques disponibles**, sélectionnez toodisplay de métriques hello. Utilisez hello CTRL bouton toomulti-sélectionner. 

    Vos mesures sont affichées sur Bonjour **tracer** fenêtre. 

## <a name="view-performance-metrics-on-hello-account-blade"></a>Afficher les métriques de performances sur le panneau de compte hello
1. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **plus Services**, faites défiler trop**bases de données**, cliquez sur **base de données Azure Cosmos**, puis cliquez sur nom hello Hello Compte Cosmos DB Azure pour lequel vous souhaitez que les mesures de performances tooview.
2. Hello **analyse** thématique affiche hello suivant des vignettes par défaut :
   
   * Nombre total de demandes pour hello jour actuel.
   * Stockage utilisé.
   
   Si votre table affiche **aucune donnée disponible** et que vous pensez qu’il existe des données dans votre base de données, consultez hello [dépannage](#troubleshooting) section.
   
   ![Capture d’écran de l’objectif de surveillance hello qui affiche les demandes hello et l’utilisation du stockage hello](./media/monitor-accounts/documentdb-total-requests-and-usage.png)
3. En cliquant sur hello **demandes** ou **Quota d’utilisation** vignette ouvre un détaillées **métrique** panneau.
4. Hello **métrique** panneau vous donne des détails sur les métriques hello que vous avez sélectionné.  En haut du Panneau de hello hello est un graphique de demandes de toutes les heures et du bien-être ci-dessous, qui est la table qui affiche les valeurs d’agrégation pour les demandes limitées et total.  Hello métriques affiche également hello liste des alertes qui ont été métriques toohello défini, filtrée qui apparaissent dans le panneau de métrique actuel hello (de cette manière, si vous avez un nombre d’alertes, vous seulement verrez hello pertinentes celles présentées ici).   
   
   ![Capture d’écran du Panneau de métrique hello incluant limitée des requêtes](./media/monitor-accounts/documentdb-metric-blade.png)

## <a name="customize-performance-metric-views-in-hello-portal"></a>Personnaliser les affichages de métriques de performances dans le portail de hello
1. les métriques de hello toocustomize qui s’affichent dans un graphique en particulier, cliquez sur hello graphique tooopen dans hello **métrique** panneau, puis cliquez sur **modifier le graphique**.  
   ![Capture d’écran de contrôles hello métriques, modifier le graphique mis en surbrillance](./media/monitor-accounts/madocdb3.png)
2. Sur hello **modifier le graphique** panneau, il existe des métriques de hello toomodify options qui s’affichent dans le graphique de hello, ainsi que leur plage de temps.  
   ![Capture d’écran du Panneau de modifier le graphique de hello](./media/monitor-accounts/madocdb4.png)
3. les métriques de hello toochange affichées dans le cadre de hello, il suffit de sélectionner ou effacer des métriques de performances disponibles hello, puis cliquez sur **OK** bas hello du Panneau de hello.  
4. toochange hello intervalle de temps, choisissez une plage différente (par exemple, **personnalisé**), puis cliquez sur **OK** bas hello du Panneau de hello.  
   
   ![Capture d’écran de partie de plage de temps hello d’affichage de panneau modifier le graphique de hello comment tooenter une plage de temps personnalisé](./media/monitor-accounts/madocdb5.png)

## <a name="create-side-by-side-charts-in-hello-portal"></a>Créer des graphiques de côte à côte dans le portail de hello
Hello portail Azure vous permet de graphiques de métriques toocreate côte-à-côte.  

1. Tout d’abord, avec le bouton droit sur le graphique hello souhaitée toocopy **personnaliser**.
   
   ![Capture d’écran de graphique du nombre Total de demandes hello avec l’option de personnalisation hello mis en surbrillance](./media/monitor-accounts/madocdb6.png)
2. Cliquez sur **Clone** hello partie du menu toocopy hello et puis cliquez sur **fait personnalisation**.
   
   ![Écran de capture du graphique du nombre Total de demandes hello avec hello Clone et effectué la personnalisation des options mis en surbrillance](./media/monitor-accounts/madocdb7.png)  

Vous pouvez désormais traiter cette partie en tant que toute autre partie de métriques, personnalisation hello métriques et la plage horaire affichée dans la partie de hello.  Ce faisant, vous pouvez voir deux mesures différentes graphique-côte à hello même temps.  
    ![Capture d’écran de graphique du nombre Total de demandes hello et hello nouveau nombre Total de demandes au-delà de graphique de l’heure](./media/monitor-accounts/madocdb8.png)  

## <a name="set-up-alerts-in-hello-portal"></a>Configurer des alertes dans le portail de hello
1. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **plus Services**, cliquez sur **base de données Azure Cosmos**, puis cliquez sur nom hello du compte de base de données Azure Cosmos hello pour laquelle vous aimeriez toosetup alertes de métriques de performances.
2. Dans le menu de ressource hello, cliquez sur **les règles d’alerte** Panneau de règles d’alerte tooopen hello.  
   ![Capture d’écran de hello alerte règles partie sélectionnée](./media/monitor-accounts/madocdb10.5.png)
3. Bonjour **règles d’alerte** panneau, cliquez sur **ajouter une alerte**.  
   ![Capture d’écran du Panneau de règles d’alerte hello, avec le bouton Ajouter une alerte de hello en surbrillance](./media/monitor-accounts/madocdb11.png)
4. Bonjour **ajouter une règle d’alerte** panneau, spécifiez :
   
   * nom Hello de règle d’alerte hello que vous configurez.
   * Description de la nouvelle règle d’alerte hello.
   * Bonjour métrique pour la règle d’alerte hello.
   * condition de Hello, seuil et période qui déterminent quand les alerte hello active. Par exemple, une erreur de serveur nombre supérieur à 5 sur hello des 15 dernières minutes.
   * Si coadministrators et administrateur de service hello sont envoyées par courrier électronique lors du déclenche de l’alerte de hello.
   * Des adresses électroniques supplémentaires pour les notifications d'alerte.  
     ![Capture d’écran de hello ajouter un panneau de règle d’alerte](./media/monitor-accounts/madocdb12.png)

## <a name="monitor-azure-cosmos-db-programatically"></a>Surveiller un compte Azure Cosmos DB par programme
Hello métriques de niveau de compte disponibles dans le portail de hello, notamment l’utilisation du stockage compte et le nombre total de demandes, ne sont pas disponibles via hello APIs DocumentDB. Toutefois, vous pouvez récupérer des données d’utilisation au niveau de collection hello à l’aide de hello APIs DocumentDB. données au niveau de collection tooretrieve, hello suivant :

* toouse hello API REST, [effectuer une opération GET sur la collection de hello](https://msdn.microsoft.com/library/mt489073.aspx). Hello les informations de quota et l’utilisation de la collection de hello sont retournées dans les en-têtes x-ms-resource-quota et x-ms-resource-usage de hello en réponse de hello.
* toouse hello .NET SDK, utilisez hello [DocumentClient.ReadDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.readdocumentcollectionasync.aspx) (méthode), qui retourne un [ResourceResponse](https://msdn.microsoft.com/library/dn799209.aspx) qui contient un nombre de propriétés d’utilisation, telle que  **CollectionSizeUsage**, **DatabaseUsage**, **DocumentUsage**et bien plus encore.

tooaccess des métriques supplémentaires, utilisez hello [analyse de Windows Azure SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights). Les définitions de mesures disponibles peuvent être récupérées en appelant :

    https://management.azure.com/subscriptions/{SubscriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metricDefinitions?api-version=2015-04-08

Requêtes tooretrieve mesures individuelles utilisez hello suivant le format :

    https://management.azure.com/subscriptions/{SubecriptionId}/resourceGroups/{ResourceGroup}/providers/Microsoft.DocumentDb/databaseAccounts/{DocumentDBAccountName}/metrics?api-version=2015-04-08&$filter=%28name.value%20eq%20%27Total%20Requests%27%29%20and%20timeGrain%20eq%20duration%27PT5M%27%20and%20startTime%20eq%202016-06-03T03%3A26%3A00.0000000Z%20and%20endTime%20eq%202016-06-10T03%3A26%3A00.0000000Z

Pour plus d’informations, consultez [la récupération des métriques de ressources via hello API REST de Azure analyse](https://blogs.msdn.microsoft.com/cloud_solution_architect/2016/02/23/retrieving-resource-metrics-via-the-azure-insights-api/). Notez que « Azure Inights » a été renommé « Azure Monitor ».  Cette entrée de blog fait référence toohello les nom plus anciens.

## <a name="troubleshooting"></a>Résolution des problèmes
Si votre analyse vignettes affichage hello **aucune donnée disponible** message et vous récemment apportées demandes ou ajouté de base de données toohello de données, vous pouvez modifier hello vignette tooreflect hello l’utilisation récente.

### <a name="edit-a-tile-toorefresh-current-data"></a>Modifier une données actuelles de mosaïque toorefresh
1. les métriques de hello toocustomize qui s’affichent dans un composant particulier, cliquez sur hello de hello graphique tooopen **métrique** panneau, puis cliquez sur **modifier le graphique**.  
   ![Capture d’écran de contrôles hello métriques, modifier le graphique mis en surbrillance](./media/monitor-accounts/madocdb3.png)
2. Sur hello **modifier le graphique** panneau, Bonjour **période** , cliquez sur **après heure**, puis cliquez sur **OK**.  
   ![Capture d’écran du Panneau de modifier le graphique de hello avec la dernière heure sélectionnée](./media/monitor-accounts/documentdb-no-available-data-past-hour.png)
3. Votre mosaïque doit s’actualiser et afficher vos données actuelles et votre utilisation.  
   ![Capture d’écran de mise à jour de hello nombre Total de demandes au-delà de vignette de l’heure](./media/monitor-accounts/documentdb-no-available-data-fixed.png)

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur la base de données Azure Cosmos planification de la capacité, consultez hello [calculatrice de planification de capacité de base de données Azure Cosmos](https://www.documentdb.com/capacityplanner).

