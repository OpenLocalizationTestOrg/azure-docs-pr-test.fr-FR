---
title: "aaaMonitor opérations, les événements et les compteurs pour l’équilibrage de charge | Documents Microsoft"
description: "Découvrez comment tooenable les événements d’alerte et sonde d’enregistrement de l’état d’intégrité pour l’équilibrage de charge Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac53c2254e06cad780ad6144c5c30f0085d12576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-for-azure-load-balancer"></a>Analyse des journaux de l'équilibreur de charge Azure

Vous pouvez utiliser différents types de journaux dans Azure toomanage et résoudre les problèmes d’équilibreurs de charge. Certaines de ces journaux sont accessibles via le portail de hello. Tous les journaux peuvent être extraits à partir d’un stockage Blob Azure et affichés dans différents outils, comme Excel et PowerBI. Pour plus d’informations sur hello différents types de journaux à partir de la liste de hello ci-dessous.

* **Journaux d’audit :** que vous pouvez utiliser [les journaux d’Audit Azure](../monitoring-and-diagnostics/insights-debugging-with-events.md) (anciennement journaux opérationnels) tooview toutes les opérations en cours tooyour soumis un ou plusieurs abonnements Azure, ainsi que leur état. Journaux d’audit sont activées par défaut et peuvent être consultées dans hello portail Azure.
* **Journaux des événements d’alerte :** vous pouvez utiliser cette rasied d’alertes de tooview journal par l’équilibrage de charge hello. état Hello pour l’équilibrage de charge hello est collecté toutes les cinq minutes. Ce journal est écrit uniquement si un événement d'alerte d’équilibreur de charge est généré.
* **Journaux de sonde d’intégrité :** vous pouvez utiliser cette tooview des journaux des problèmes détectés par votre sonde d’intégrité, telles que nombre hello d’instances dans votre pool principal ne reçoivent pas les demandes d’équilibrage de charge hello en raison d’échecs de sonde d’intégrité. Ce fichier journal est écrit toowhen un changement dans l’état d’intégrité sonde hello.

> [!IMPORTANT]
> L'analyse des journaux s’applique uniquement aux équilibreurs de charge accessibles sur Internet. Les journaux sont uniquement disponibles pour les ressources déployées dans le modèle de déploiement du Gestionnaire de ressources hello. Vous ne pouvez pas utiliser les journaux pour les ressources dans le modèle de déploiement classique hello. Pour plus d’informations sur les modèles de déploiement hello, consultez [déploiement du Gestionnaire de ressources de présentation et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).

## <a name="enable-logging"></a>Activation de la journalisation

La journalisation d’audit est automatiquement activée pour chaque ressource Resource Manager. Vous devez les événements tooenable et toostart de journalisation de sonde d’intégrité collecte des données hello ces journaux. Utilisez hello après la journalisation tooenable étapes.

Connectez-vous toohello [portail Azure](http://portal.azure.com). Si vous ne disposez pas déjà d'un équilibreur de charge, [créez un équilibreur de charge](load-balancer-get-started-internet-arm-ps.md) avant de continuer.

1. Dans le portail de hello, cliquez sur **Parcourir**.
2. Sélectionnez **Équilibreurs de charge**.

    ![portail - équilibreur-charge](./media/load-balancer-monitor-log/load-balancer-browse.png)

3. Sélectionnez un équilibreur de charge existant >> **Tous les paramètres**.
4. Hello droite de la boîte de dialogue hello sous nom hello d’équilibrage de charge hello, faites défiler trop**analyse**, cliquez sur **Diagnostics**.

    ![portail - paramètres-équilibreur-charge](./media/load-balancer-monitor-log/load-balancer-settings.png)

5. Bonjour **Diagnostics** volet, sous **état**, sélectionnez **sur**.
6. Cliquez sur **Compte de stockage**.
7. Sous **LOGS**, sélectionnez un compte de stockage existant ou créez-en un nouveau. Utilisez hello curseur toodetermine le nombre de jours des données d’événement sont stockés dans les journaux des événements hello. 
8. Cliquez sur **Enregistrer**.

    ![Portail - Journaux de diagnostics](./media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> Les journaux d’audit ne nécessitent pas de compte de stockage distinct. Hello d’utilisation du stockage pour les événements et d’intégrité sonde journalisation occasionnent des frais de service.

## <a name="audit-log"></a>Journal d’audit

journal d’audit de Hello est généré par défaut. Hello journaux sont conservées pendant 90 jours dans le magasin de journaux des événements d’Azure. En savoir plus sur ces journaux en lisant hello [afficher les événements et journaux d’audit](../monitoring-and-diagnostics/insights-debugging-with-events.md) l’article.

## <a name="alert-event-log"></a>Journal des événements d'alerte

Ce journal n’est généré que si vous l’avez activé au niveau de chaque équilibreur de charge. événements de Hello sont enregistrés au format JSON et stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello. Hello Voici un exemple d’événement.

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

Hello JSON de sortie montre hello *eventname* propriété qui décrit la raison hello pour l’équilibrage de charge hello créé une alerte. Dans ce cas, alerte hello générée était due tooTCP épuisement du port fait source QU'IP NAT limite (SNAT).

## <a name="health-probe-log"></a>Journal des sondes d’intégrité

Ce journal n’est généré que si vous l’avez activé au niveau de chaque équilibreur de charge, comme détaillé ci-dessous. les données de salutation sont stockées dans le compte de stockage hello que vous avez spécifié lorsque vous avez activé la journalisation hello. Un conteneur nommé « insights-journaux-loadbalancerprobehealthstatus » est créé et hello suivant des données est enregistré :

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

montre la sortie JSON Hello hello propriétés champ hello informations de base pour l’état d’intégrité de sonde hello. Hello *dipDownCount* propriété indique le nombre total de hello d’instances sur hello principaux qui ne reçoivent pas de trafic réseau en raison de réponses de sonde toofailed.

## <a name="view-and-analyze-hello-audit-log"></a>Afficher et analyser le journal d’audit de hello

Vous pouvez afficher et analyser les données du journal d’audit à l’aide d’une des méthodes suivantes de hello :

* **Windows Azure tools :** récupère des informations à partir des journaux d’audit hello Azure PowerShell, hello Azure Interface de ligne de commande (CLI), hello API REST de Azure, ou hello portail Azure preview. Des instructions détaillées pour chaque méthode sont détaillées dans hello [opérations avec le Gestionnaire de ressources de l’Audit](../azure-resource-manager/resource-group-audit.md) l’article.
* **Power BI :** si vous n’avez pas encore de compte [Power BI](https://powerbi.microsoft.com/pricing) , vous pouvez l’essayer gratuitement. À l’aide de hello [les journaux d’Audit Azure pack de contenu pour Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), vous pouvez analyser vos données avec des tableaux de bord préconfigurés, ou vous pouvez personnaliser les vues toosuit vos besoins.

## <a name="view-and-analyze-hello-health-probe-and-event-log"></a>Afficher et analyser le journal des événements et la sonde d’intégrité de hello

Vous devez tooconnect tooyour stockage compte et récupérer les entrées de journal hello JSON pour les journaux de sonde d’intégrité et les événements. Une fois que vous téléchargez des fichiers au format JSON hello, vous pouvez les convertir tooCSV et view dans Excel, Power BI ou tout autre outil de visualisation de données.

> [!TIP]
> Si vous êtes familiarisé avec Visual Studio et les concepts de base de la modification des valeurs de constantes et variables dans c#, vous pouvez utiliser hello [ouvrir une session outils de convertisseur](https://github.com/Azure-Samples/networking-dotnet-log-converter) disponible à partir de GitHub.

## <a name="additional-resources"></a>Ressources supplémentaires

* [Visualiser vos journaux d’audit Azure avec Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) .
* [Afficher et analyser les journaux d’audit Azure dans Power BI et bien plus encore](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) .

## <a name="next-steps"></a>Étapes suivantes

[Comprendre les sondes de l’équilibrage de charge](load-balancer-custom-probe-overview.md)
