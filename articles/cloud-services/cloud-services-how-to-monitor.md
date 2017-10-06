---
title: aaaHow toomonitor un service cloud | Documents Microsoft
description: "Découvrez comment toomonitor services de cloud computing à l’aide de hello portail Azure classic."
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>Comment les Services de cloud computing tooMonitor
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

Vous pouvez surveiller `key` mesures de performance pour vos services cloud Bonjour portail Azure classic. Vous pouvez définir hello au niveau de l’analyse toominimal et détaillés pour chaque rôle de service et que vous pouvez personnaliser les affichages de surveillance de hello. Données de surveillance détaillées sont stockées dans un compte de stockage, vous pouvez accéder à l’extérieur hello portail. 

Affichages de surveillance Bonjour portail Azure classic sont hautement configurables. Vous pouvez choisir les métriques hello souhaité toomonitor dans la liste de mesures hello sur hello **moniteur** page et que vous pouvez choisir le métriques tooplot dans les graphiques de métriques sur hello **moniteur** hello et la page tableau de bord. 

## <a name="concepts"></a>Concepts
Par défaut, la surveillance minimale est fournie pour un nouveau service cloud à l’aide des compteurs de performance collectés hello système d’exploitation hôte pour les instances de rôles hello (machines virtuelles). les métriques minimales Hello sont tooCPU limité pourcentage, de données, données sortantes, débit de lecture du disque et débit d’écriture du disque. En configurant la surveillance détaillée, vous pouvez recevoir des métriques supplémentaires en fonction des données de performances des ordinateurs virtuels de hello (instances de rôle). les métriques détaillées Hello permettent une analyse plus approfondie des problèmes qui se produisent pendant les opérations de l’application.

Par défaut, les données de compteur de performance à partir d’instances de rôle sont échantillonnées et transférées à partir de l’instance de rôle hello à 3 minutes. Lorsque vous activez la surveillance détaillée, données de compteur de performances brutes hello sont agrégées pour chaque instance de rôle et entre les instances de rôle pour chaque rôle à des intervalles de 5 minutes, 1 heure et 12 heures. Hello des données agrégées sont purgées après dix jours.

Après avoir activé la surveillance détaillée, hello agrégée analyse les données est stockée dans des tables dans votre compte de stockage. tooenable pour un rôle de surveillance détaillée, vous devez configurer une chaîne de connexion de diagnostics qui lie le compte de stockage toohello. Vous pouvez utiliser différents comptes de stockage pour différents rôles.

L’activation des augmentations de surveillance détaillées les coûts de stockage liés toodata stockage, le transfert de données et transactions de stockage. La surveillance minimale ne nécessite pas de compte de stockage. données Hello pour les métriques hello qui sont exposés au niveau de surveillance minimale hello ne sont pas stockées dans votre compte de stockage, même si vous définissez hello tooverbose au niveau de surveillance.

## <a name="how-to-configure-monitoring-for-cloud-services"></a>Procédure de configuration de la surveillance des services cloud
Utilisez hello suivant les procédures tooconfigure détaillée ou minimale analyse Bonjour portail Azure classic. 

### <a name="before-you-begin"></a>Avant de commencer
* Créer un *classique* hello de toostore de compte de stockage données d’analyse. Vous pouvez utiliser différents comptes de stockage pour différents rôles. Pour plus d’informations, consultez [comment toocreate un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Activez le diagnostic Azure pour vos rôles de service cloud. Consultez [Configuration des diagnostics pour les services cloud](cloud-services-dotnet-diagnostics.md).

Assurez-vous que la chaîne de connexion des diagnostics hello est présent dans la configuration du rôle hello. Vous ne pouvez pas activer la surveillance détaillée jusqu'à ce que vous activez les Diagnostics de Azure et incluez une chaîne de connexion de diagnostic dans la configuration du rôle hello.   

> [!NOTE]
> Projets ciblant Azure SDK 2.5 n’incluent pas automatiquement de chaîne de connexion des diagnostics hello dans le modèle de projet hello. Pour que ces projets, vous devez toomanually ajouter la configuration du rôle connexion chaîne toohello hello diagnostics.
> 
> 

**toomanually ajouter une configuration de tooRole de chaîne de connexion de diagnostic**

1. Projet de Service Cloud hello ouvert dans Visual Studio
2. Double-cliquez sur hello **rôle** tooopen hello Concepteur de rôle et sélectionnez hello **paramètres** onglet
3. Recherchez un paramètre appelé **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**. 
4. Si ce paramètre n’est pas présent, cliquez sur hello **ajouter un paramètre** bouton tooadd il toohello configuration et des modifications de type pour hello nouveau paramètre trop hello**ConnectionString**
5. La valeur hello pour hello de chaîne de connexion en cliquant sur hello **...**  bouton. S’ouvre une boîte de dialogue qui vous tooselect un compte de stockage.
   
    ![Paramètres Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>hello toochange tooverbose au niveau de surveillance ou minimale
1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), ouvrez hello **configurer** page déployer le service cloud hello.
2. Dans **Niveau**, cliquez sur **Détaillé** ou **Minimal**. 
3. Cliquez sur **Enregistrer**.

Une fois que vous activez la surveillance détaillée, vous devez commencer à voir les hello analyser les données Bonjour portail Azure classic heure de hello.

données de compteur de performances brutes Hello et analyse des données agrégées sont stockées dans le compte de stockage hello dans les tables qualifiés par ID de déploiement hello pour les rôles de hello. 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>Procédure de réception d’alertes pour les mesures des services cloud
Vous pouvez recevoir des alertes en fonction des mesures de surveillance de votre service cloud. Sur hello **des Services de gestion** page de hello portail Azure classic, vous pouvez créer une règle tootrigger une alerte lorsque la métrique hello vous choisissez atteint une valeur que vous spécifiez. Vous pouvez également choisir toohave par e-mail quand hello alerte est déclenchée. Pour plus d’informations, consultez la page [Réception de notifications d’alerte et gestion des règles d’alerte dans Azure](http://go.microsoft.com/fwlink/?LinkId=309356).

## <a name="how-to-add-metrics-toohello-metrics-table"></a>Comment : ajouter la table des mesures métriques toohello
1. Bonjour [portail Azure classic](http://manage.windowsazure.com/), ouvrez hello **moniteur** page hello cloud service.
   
    Par défaut, la table des métriques hello affiche un sous-ensemble des métriques disponibles de hello. l’illustration Hello hello par défaut les métriques détaillées pour un service cloud, qui est un compteur de performance Memory\Available MBytes toohello limité, avec les données agrégées au niveau du rôle hello. Utilisez **ajouter des métriques** agrégat supplémentaires de tooselect et toomonitor de métriques au niveau du rôle dans hello portail Azure classic.
   
    ![Affichage détaillé](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. table des mesures métriques toohello tooadd :
   
   1. Cliquez sur **ajouter des métriques** tooopen **choisir des métriques**, comme illustré ci-dessous.
      
       métrique de disponible premier de Hello est développé tooshow les options qui sont disponibles. Pour chaque mesure, option top de hello affiche des données d’analyse agrégées pour tous les rôles. En outre, vous pouvez choisir les rôles individuels toodisplay les données de.
      
       ![Ajouter des métriques](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect métriques toodisplay
      
      * Cliquez sur hello flèche vers le bas par Bonjour tooexpand métrique Bonjour options de surveillance.
      * Hello Select case à cocher pour chaque option que vous souhaitez toodisplay d’analyse.
        
        Vous pouvez afficher les métriques de too50 dans la table des métriques hello.
        
        > [!TIP]
        > La surveillance détaillée, liste de mesures hello peut contenir des dizaines de métriques. toodisplay une barre de défilement, placez votre curseur sur le côté droit de hello de boîte de dialogue hello. liste de hello toofilter, cliquez sur icône de recherche hello et entrez le texte dans la zone de recherche de hello, comme indiqué ci-dessous.
        > 
        > 
        
        ![Add metrics search](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. Une fois que vous avez terminé de sélectionner les mesures, cliquez sur OK (coche).
   
    Hello les métriques sélectionnées sont ajoutées toohello table des métriques, comme indiqué ci-dessous.
   
    ![mesures de surveillance](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. toodelete une mesure à partir de la table des métriques hello, tooselect de métrique hello il, puis cliquez sur **supprimer une métrique**. ( **Delete Metric** ne s'affiche que si une mesure est sélectionnée.)

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>table des métriques toohello tooadd des mesures personnalisées
Hello **Verbose** analyse niveau fournit une liste des mesures par défaut que vous pouvez surveiller sur le portail hello. En outre vous toothese vous pouvez surveiller les compteurs de performance définis par votre application via le portail de hello ni des mesures personnalisées.

Hello étapes suivantes supposent que vous avez activé **Verbose** niveau de surveillance et avez configuré vos compteurs de performances personnalisés application toocollect et de transfert. 

compteurs de performances personnalisés toodisplay hello dans hello portail que vous avez besoin de configuration hello tooupdate wad-control-container :

1. Ouvrez l’objet blob wad-control-container de hello dans votre compte de stockage de diagnostics. Vous pouvez utiliser Visual Studio ou toute autre toodo de l’Explorateur de stockage cela.
   
    ![Explorateur de serveurs Visual Studio.](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. Parcourir le chemin d’accès de l’objet blob hello à l’aide du modèle de hello **DeploymentId/RoleName/RoleInstance** configuration de hello toofind pour votre instance de rôle. 
   
    ![Explorateur de stockage Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. Télécharger le fichier de configuration hello pour votre instance de rôle et le mettre à jour tooinclude des compteurs de performance personnalisés. Par exemple toomonitor *octets/s d’écriture sur disque* pour hello *lecteur C* ajouter suivantes hello sous **PerformanceCounters\Subscriptions** nœud
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. Enregistrez les modifications hello et toohello précédent du fichier configuration hello téléchargement remplacement du même emplacement hello un fichier existant dans l’objet blob de hello.
5. Basculer vers le mode tooVerbose Bonjour configuration du portail Azure classique. Si vous étiez en mode documenté déjà avoir tootoggle les tooverbose toominimal et inversement.
6. compteur de performances personnalisé Hello seront désormais disponible dans hello **ajouter des métriques** boîte de dialogue. 

## <a name="how-to-customize-hello-metrics-chart"></a>Comment : personnaliser le graphique des métriques hello
1. Dans la table des métriques hello, sélectionnez tooplot de métriques too6 sur le graphique des métriques hello. tooselect une mesure, cliquez sur hello case à cocher sur son côté gauche. tooremove une mesure à partir du graphique des métriques hello, désactivez sa case à cocher dans la table des métriques hello.
   
    Lorsque vous sélectionnez des mesures dans la table des métriques hello, les métriques de hello sont ajoutés toohello graphique des métriques. Sur un affichage étroit, une **plus de n** liste déroulante contienne les en-têtes de métriques qui ne tient pas afficher de hello.
2. tooswitch entre l’affichage des valeurs relatives (valeur finale uniquement pour chaque mesure) et les valeurs absolues (affiché de l’axe Y), sélectionnez Relative ou absolue haut hello du graphique de hello.
   
    ![Relative ou Absolute](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. graphique des mesures toochange hello temps plage hello affiche, sélectionnez les 1 heure, 24 heures ou 7 jours haut hello du graphique de hello.
   
    ![Période d'affichage de la surveillance](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    Sur le graphique des métriques hello du tableau de bord, la méthode hello pour les mesures de traçage est différent. Un ensemble standard de métriques est disponible, et les métriques sont ajoutés ou supprimés en sélectionnant l’en-tête de métrique hello.

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>graphique des métriques toocustomize hello sur le tableau de bord hello
1. Ouvrez le tableau de bord de hello pour le service cloud hello.
2. Ajouter ou supprimer des métriques dans le graphique de hello :
   
   * tooplot une case à cocher hello métrique, sélectionnez nouvelle mesure hello dans les en-têtes du graphique hello. Sur un étroit affichage, cliquez sur hello bas par  ***n* ?? métriques** tooplot une zone d’en-tête hello métrique graphique ne peut pas afficher.
   * toodelete une métrique est tracée sur le graphique de hello, hello désactivez case à cocher par son en-tête.
   
3. Basculez entre les affichages **Relative** et **Absolute**.
4. Choisissez une heure, 24 heures ou 7 jours de données toodisplay.

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>Comment : accéder aux données de surveillance détaillées à l’extérieur de hello portail Azure classic
Données de surveillance détaillées sont stockées dans des tables dans les comptes de stockage hello que vous spécifiez pour chaque rôle. Pour chaque déploiement de service cloud, les six tables sont créées pour le rôle de hello. Deux tables sont créées toutes les (5 minutes, 1 heure et 12 heures). Une de ces tables stocke les agrégations au niveau du rôle. Bonjour autres agrégations de magasins de table pour les instances de rôle. 

les noms de table Hello ont hello suivant le format :

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

où :

* *ID de déploiement* est hello GUID affecté le déploiement du service cloud toohello
* *aggregation_interval* = 5 m, 1 h ou 12 h
* consolidations au niveau du rôle = R
* consolidations pour les instances de rôle = RI

Par exemple, hello tableaux suivants stocke des données de surveillance détaillées agrégées à des intervalles de 1 heure :

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
