---
title: aaaHow toomonitor un compte Azure Storage | Documents Microsoft
description: "Découvrez comment toomonitor un compte de stockage dans Azure à l’aide de hello portail Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 782873648fdbccc0191a074cd4044f97af8b7c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>Surveillance d’un compte de stockage Bonjour portail Azure

[Azure Storage Analytics](storage-analytics.md) fournit des métriques pour tous les services de stockage et des journaux pour les objets Blob, les files d’attente et les tables. Vous pouvez utiliser hello [portail Azure](https://portal.azure.com) tooconfigure les mesures et les journaux est enregistré pour votre compte et configurer des graphiques qui fournissent des représentations visuelles de vos données de métriques.

> [!NOTE]
> Il existe des coûts liés à l’examen des données d’analyse Bonjour portail Azure. Pour plus d'informations, consultez la page [Storage Analytics et facturation](/rest/api/storageservices/Storage-Analytics-and-Billing).
>
> Le stockage de fichiers Azure prend actuellement en charge les métriques de Storage Analytics, mais pas encore la journalisation.
>
> Les comptes de stockage avec un type de réplication de stockage redondance de Zone (ZRS) actuellement n’ont pas de métriques de hello ou la fonctionnalité de journalisation activée.
> 
> Pour des instructions détaillées sur l’utilisation de stockage Analytique et les autres outils tooidentify, diagnostiquer et résoudre les problèmes liés au stockage Azure, consultez [moniteur, diagnostiquer et résoudre les problèmes de Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).
>

## <a name="configure-monitoring-for-a-storage-account"></a>Configuration de la surveillance d'un compte de stockage

1. Bonjour [portail Azure](https://portal.azure.com), sélectionnez **comptes de stockage**, puis hello stockage compte nom tooopen hello compte du tableau de bord.
1. Sélectionnez **Diagnostics** Bonjour **analyse** section du Panneau de menu hello.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. Sélectionnez hello **type** de données de métriques pour chaque **service** vous le souhaitez toomonitor et hello **stratégie de rétention** pour les données de salutation. Vous pouvez également désactiver la surveillance en définissant **état** trop**hors**.

    ![MonitoringOptions](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   Il existe deux types de métriques que vous pouvez activer pour chaque service. Les deux sont activés par défaut pour les nouveaux comptes de stockage :

   * **Agréger** : collecte des métriques telles que l'entrée/la sortie, la disponibilité, la latence et les pourcentages de réussite. Ces mesures sont agrégées pour les objets blob de hello, de file d’attente, de table et de services de fichiers.
   * **Par API**: dans Ajout toohello d’agrégation des mesures, collecte hello même ensemble de mesures pour chaque opération de stockage Bonjour API de service de stockage Azure.

   stratégie de rétention données tooset hello, déplacement hello **rétention (jours)** curseur ou entrez le nombre de hello de jours de tooretain de données, à partir de 1 too365. valeur par défaut de Hello pour les nouveaux comptes de stockage est de sept jours. Si vous ne souhaitez pas tooset une stratégie de rétention, entrez zéro. S’il n’existe aucune stratégie de rétention, c’est tooyou toodelete hello est données d’analyse.

   > [!WARNING]
   > Vous êtes facturé lorsque vous supprimez manuellement les données de métrique. Données d’analytique obsolètes (antérieure à votre stratégie de rétention de données) sont supprimées par système hello sans frais. Nous vous recommandons de définir une stratégie de rétention en fonction de la durée pendant laquelle vous voulez données analytique de stockage tooretain pour votre compte. Consultez [Quels sont les frais encourus quand vous activez les métriques de stockage ?](storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) pour plus d’informations.
   >

1. Lorsque vous avez terminé la configuration de la surveillance hello, sélectionnez **enregistrer**.

Un ensemble par défaut de mesures s’affiche dans les graphiques sur le panneau de compte de stockage hello, ainsi que les panneaux de service individuels hello (blob, file d’attente, table et fichier). Une fois que vous avez activé les métriques pour un service, peut prendre jusqu'à une heure tooan tooappear de données dans les graphiques. Vous pouvez sélectionner **modifier** sur n’importe quel métrique du graphique trop[configurer les métriques](#how-to-customize-metrics-charts) sont affichés dans le graphique de hello.

Vous pouvez désactiver la collecte de métriques et la journalisation en définissant **état** trop**hors**.

> [!NOTE]
> Le stockage Azure utilise [stockage de table](storage-introduction.md#table-storage) toostore les métriques de hello pour votre compte de stockage et les métriques de hello de magasins dans les tables de votre compte. Pour plus d’informations, consultez. [Stockage des métriques](storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>Personnaliser les graphiques de métrique

Utilisez hello suivant la procédure toochoose le tooview de métriques de stockage dans un graphique des métriques. 

1. Démarrez en affichant un graphique de métriques de stockage Bonjour portail Azure. Vous pouvez trouver des graphiques sur hello **Panneau de compte de stockage** et Bonjour **métriques** panneau pour un service (blob, file d’attente, table, fichier).

   Dans cet exemple, nous travaillons avec hello suivant graphique qui s’affiche sur hello **Panneau de compte de stockage**:

   ![Sélection de graphique dans le portail Azure](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. Ensuite, cliquez n’importe où dans hello de hello graphique tooopen **métrique** panneau. Sélectionnez **modifier le graphique** tooopen hello **modifier le graphique** panneau.

   ![Bouton Modifier le graphique sur le panneau du graphique](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. Sur hello **modifier le graphique** panneau, sélectionnez hello **période** de toodisplay de métriques hello dans le graphique de hello et hello **service** (blob, file d’attente, de table, de fichiers) dont vous souhaitez de métriques toodisplay. Ici, nous avons sélectionné hello toodisplay au-delà de métriques de la semaine pour le service d’objets blob hello :

   ![Sélection de plage et le service de temps dans le panneau de modifier le graphique de hello](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. Sélectionnez hello individuels **métriques** vous aviez comme affiché dans le graphique de hello, puis cliquez sur **OK**. Par exemple, ici nous avons choisi toodisplay hello *ContainerCount* et *ObjectCount* métriques :

   ![Sélection de métrique individuelle dans le panneau Modifier le graphique](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

Vos paramètres du graphique ne pas affecter la collection de hello, l’agrégation ou stockage de données d’analyse dans le compte de stockage hello, hello uniquement de consultation des données de métriques.

### <a name="metrics-availability-in-charts"></a>Disponibilité des métriques dans les graphiques

liste de Hello des modifications de métriques disponibles basé sur lequel le service que vous avez choisie dans la liste déroulante de hello et type d’unité hello du graphique de hello que vous modifiez. Par exemple, vous pouvez sélectionner les métriques de pourcentage comme *PercentNetworkError* et *PercentThrottlingError* uniquement si vous modifiez un graphique qui affiche les unités en pourcentage :

![Graphique de pourcentage demande erreur Bonjour portail Azure](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>Résolution des métriques

métriques Hello que vous avez sélectionné dans les Diagnostics détermine la résolution hello de métriques hello qui sont disponibles pour votre compte :

* La surveillance **Agréger** fournit des métriques telles que l’entrée/la sortie, la disponibilité, la latence et les pourcentages de réussite. Ces mesures sont agrégées à partir de hello blob, table, fichier et les services de file d’attente.
* **Par API** assure la résolution plus précie, avec des mesures disponibles pour les opérations de stockage individuelles, en plus toohello les agrégats de niveau de service.

## <a name="configure-metrics-alerts"></a>Configurer des alertes de métriques

Vous pouvez créer des alertes toonotify vous lorsque les seuils ont été atteints pour les métriques de ressources de stockage.

1. tooopen hello **Panneau de règles d’alerte**, défiler toohello **analyse** section Hello **Panneau de Menu** et sélectionnez **règles d’alerte**.
1. Sélectionnez **ajouter une alerte** tooopen hello **ajouter une règle d’alerte** panneau
1. Sélectionnez un **ressource** (blob, de fichiers, de file d’attente, de table) à partir de hello de liste déroulante, puis entrez un **nom** et **Description** pour votre nouvelle règle d’alerte.
1. Sélectionnez hello **métrique** pour laquelle vous aimeriez tooadd une alerte, une alerte **Condition**et un **seuil**. modifications de type Hello seuil unité en fonction de la métrique de hello que vous avez choisie. Par exemple, « count » est le type d’unité hello pour *ContainerCount*, lors de l’unité de hello pour hello *PercentNetworkError* métrique est un pourcentage.
1. Sélectionnez hello **période**. Les métriques qui atteignent ou dépassent hello seuil dans un déclencheur de période hello une alerte.
1. (Facultatif) Configurez des notifications **E-mail** et **Webhook**. Pour plus d’informations sur webhooks, consultez [Configurer un webhook sur une alerte de métrique Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md). Si vous ne configurez pas de notifications par courrier électronique ou webhook, les alertes s’affichent uniquement dans hello portail Azure.

!['Ajouter une règle d’alerte' lame hello portail Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>Ajouter des métriques graphiques toohello portail du tableau de bord

Vous pouvez ajouter des graphiques de métriques de stockage Azure pour une de votre tableau de bord de stockage comptes tooyour portail.

1. Cliquez sur Sélectionnez **modifier le tableau de bord** lors de l’affichage de votre tableau de bord Bonjour [portail Azure](https://portal.azure.com).
1. Bonjour **vignette galerie**, sélectionnez **recherche les vignettes par** > **Type**.
1. Sélectionnez **Type** > **Comptes de stockage**.
1. Dans **ressources**, sélectionnez le compte de stockage hello dont vous souhaitez tooadd toohello du tableau de bord de métriques.
1. Sélectionnez **Catégories** > **Surveillance**.
1. Graphique de glisser-déposer hello vignette sur votre tableau de bord pour mesure hello vous aimeriez est affichée. Répétez pour toutes les métriques que vous aimeriez affichés sur le tableau de bord hello. Bonjour suivant image, graphique de « Objets BLOB - nombre Total de demandes » hello est mis en surbrillance par exemple, mais tous les graphiques de hello sont disponibles pour la sélection élective sur votre tableau de bord.

   ![Galerie de vignettes dans le portail Azure](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. Sélectionnez **fait personnalisation** haut hello du tableau de bord hello lorsque vous avez terminé l’ajout de graphiques.

Une fois que vous avez ajouté le tableau de bord tooyour de graphiques, vous pouvez les personnaliser davantage comme décrit dans [personnaliser des graphiques de métriques](#how-to-customize-metrics-charts).

## <a name="configure-logging"></a>Configuration de la journalisation

Vous pouvez indiquer des journaux de diagnostics toosave de stockage Azure pour lire, écrivent et supprimer les demandes de hello blob, table et les services de file d’attente. stratégie de rétention de données Hello que vous définissez s’applique également à toothese journaux.

> [!NOTE]
> Le stockage de fichiers Azure prend actuellement en charge les métriques de Storage Analytics, mais pas encore la journalisation.
>

1. Bonjour [portail Azure](https://portal.azure.com), sélectionnez **comptes de stockage**, puis nom hello du panneau des stockage compte hello hello stockage compte tooopen.
1. Sélectionnez **Diagnostics** Bonjour **analyse** section du Panneau de menu hello.

    ![Élément de menu Diagnostics sous surveillance Bonjour portail Azure.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. Vérifiez **état** est défini trop**sur**et sélectionnez hello **services** pour lequel vous souhaitez que la journalisation tooenable.

    ![Configurer la journalisation dans hello portail Azure.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. Cliquez sur **Enregistrer**.

Hello les journaux de diagnostic sont enregistrés dans un conteneur d’objets blob nommé $logs dans votre compte de stockage. Vous pouvez afficher les données du journal à l’aide d’un Explorateur de stockage comme hello hello [Explorateur de stockage Microsoft](http://storageexplorer.com), ou par programme à l’aide de PowerShell ou la bibliothèque cliente de stockage hello.

Pour plus d’informations sur l’accès au conteneur de hello $logs, consultez [l’activation de la journalisation du stockage et l’accès aux données du journal](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).

## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur [les métriques, la journalisation et la facturation](storage-analytics.md) pour Storage Analytics.
* [Activer les métriques Stockage Azure et afficher les données des métriques](storage-enable-and-view-metrics.md) à l’aide de PowerShell et par programme avec C#.
