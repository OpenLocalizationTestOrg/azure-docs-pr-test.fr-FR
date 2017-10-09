---
title: "aaaService intégration de carte avec System Center Operations Manager | Documents Microsoft"
description: "Carte de service est une solution de Operations Management Suite qui découvre automatiquement les composants de l’application sur Windows et cartes et les systèmes Linux hello la communication entre les services. Cet article décrit à l’aide de la carte de Service tooautomatically créer des diagrammes d’application distribuée dans Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>Intégration de Service Map avec System Center Operations Manager
  > [!NOTE]
  > Cette fonctionnalité est en version préliminaire publique.
  > 
  
Carte de Service Operations Management Suite détecte les composants de l’application sur les systèmes Windows et Linux et mappe la communication entre services hello automatiquement. Carte de service vous permet de tooview vos serveurs hello d’un moyen, en tant que réseaux interconnectés qui fournissent des services critiques. Carte de service affiche les connexions entre les serveurs, les processus et les ports sur n’importe quelle architecture TCP connectés, sans aucune configuration en dehors de l’installation de hello d’un agent. Pour plus d’informations, consultez hello [documentation de la carte de Service](operations-management-suite-service-map.md).

Cette intégration entre System Center Operations Manager et de carte de Service, vous pouvez créer automatiquement des diagrammes d’application distribuée dans Operations Manager qui sont basées sur des cartes de dépendance dynamique hello dans la carte de Service.

## <a name="prerequisites"></a>Composants requis
* Un groupe d’administration d’Operations Manager qui gère un ensemble de serveurs.
* Un espace de travail Operations Management Suite avec hello solutions de carte de Service activée.
* Un ensemble de serveurs (au moins un), et qui sont gérés par Operations Manager et d’envoi données tooService carte. Les serveurs Windows et Linux sont pris en charge.
* Un principal de service avec accès toohello abonnement Azure qui est associé avec un espace de travail Operations Management Suite hello. Pour plus d’informations, consultez trop[créer un principal de service](#creating-a-service-principal).

## <a name="install-hello-service-map-management-pack"></a>Installer le Pack d’administration de carte de Service hello
Vous activez l’intégration de hello entre Operations Manager et de la carte de Service par l’importation du groupement de packs d’administration hello Microsoft.SystemCenter.ServiceMap (Microsoft.SystemCenter.ServiceMap.mpb). regroupement de Hello contient hello suivant des packs d’administration :
* Microsoft Service Map - Vues de l’application
* Microsoft System Center Service Map - Interne
* Microsoft System Center Service Map - Valeurs de remplacement
* Microsoft System Center Service Map

## <a name="configure-hello-service-map-integration"></a>Configurer l’intégration de carte de Service hello
Après avoir installé le pack d’administration de carte de Service hello, un nouveau nœud, **carte de Service**, est affiché sous **Operations Management Suite** Bonjour **Administration** volet. 

tooconfigure intégration de la carte de Service, procédez comme hello suivant :

1. Assistant de configuration hello tooopen, Bonjour **vue d’ensemble du plan de Service** volet, cliquez sur **ajouter l’espace de travail**.  

    ![Vue d’ensemble de Service Map](media/oms-service-map/scom-configuration.png)

2. Bonjour **Configuration de la connexion** fenêtre, entrez le nom de client hello ou ID, ID de l’application (également appelé nom d’utilisateur hello ou clientID) et un mot de passe de principal du service hello, puis cliquez sur **suivant**. Pour plus d’informations, consultez trop[créer un principal de service](#creating-a-service-principal).

    ![fenêtre de Configuration de la connexion Hello](media/oms-service-map/scom-config-spn.png)

3. Bonjour **abonnement sélection** fenêtre, sélectionnez hello abonnement Azure, le groupe de ressources Azure (hello qui contient l’espace de travail Operations Management Suite hello) et espace de travail Operations Management Suite, puis cliquez sur **Suivant**.

    ![Hello, espace de travail de Configuration Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. Bonjour **sélection de groupe ordinateur** fenêtre, que vous choisissez les groupes d’ordinateurs Service carte vous souhaitez toosync tooOperations Manager. Cliquez sur **ajouter/supprimer des groupes d’ordinateurs**, choisissez des groupes à partir de la liste des hello **des groupes d’ordinateurs disponibles**, puis cliquez sur **ajouter**.  Lorsque vous avez fini de sélectionner des groupes, cliquez sur **Ok** toofinish.
    
    ![Hello groupes d’ordinateur de Configuration Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. Bonjour **sélection du serveur** fenêtre, vous configurez hello groupe de serveurs de carte de Service avec les serveurs de hello que vous souhaitez toosync entre Operations Manager et de la carte de Service. Cliquez sur **Ajouter/Supprimer des serveurs**.   
    
    Pour toobuild d’intégration hello un diagramme d’application distribuée pour un serveur, le serveur de hello doit être :

    * Géré par Operations Manager
    * Géré par Service Map
    * Répertoriées dans hello groupe de serveurs de carte de Service

    ![Hello groupe de Configuration Operations Manager](media/oms-service-map/scom-config-group.png)

6. Facultatif : Activez toocommunicate de pool de ressources de serveur d’administration hello avec Operations Management Suite, puis cliquez sur **ajouter un espace de travail**.

    ![Hello Pool de ressources de Configuration Operations Manager](media/oms-service-map/scom-config-pool.png)

    Peut prendre une minute tooconfigure et enregistrer l’espace de travail Operations Management Suite hello. Une fois qu’il est configuré, Operations Manager lance la première synchronisation de carte de Service hello à partir d’Operations Management Suite.

    ![Hello Pool de ressources de Configuration Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>Surveillance de Service Map
Une fois l’espace de travail Operations Management Suite hello connecté, un nouveau dossier, carte de Service s’affiche dans hello **analyse** volet de console d’Operations Manager hello.

![volet d’analyse d’Operations Manager Hello](media/oms-service-map/scom-monitoring.png)

dossier de carte de Service Hello a quatre nœuds :
* **Alertes actives**: répertorie toutes les alertes actives hello sur la communication hello entre Operations Manager et de la carte de Service.  Notez que ces alertes ne sont pas des alertes Operations Management Suite en cours synchronisées tooOperations Manager. 

* **Serveurs**: serveurs de hello analysé de listes qui sont configurés toosync à partir de la carte de Service.

    ![volet des serveurs d’analyse Operations Manager Hello](media/oms-service-map/scom-monitoring-servers.png)

* **Vues de dépendance de groupe d’ordinateurs** : répertorie tous les groupes d’ordinateurs synchronisés depuis Service Map. Vous pouvez cliquer sur n’importe quel groupe tooview le diagramme d’application distribuée.

    ![diagramme d’application distribuée Hello Operations Manager](media/oms-service-map/scom-group-dad.png)

* **Vues de dépendance au serveur** : répertorie tous les serveurs synchronisés à partir de Service Map. Vous pouvez cliquer sur n’importe quel serveur tooview le diagramme d’application distribuée.

    ![diagramme d’application distribuée Hello Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>Modifier ou supprimer l’espace de travail hello
Vous pouvez modifier ou supprimer l’espace de travail hello configuré via hello **vue d’ensemble du plan de Service** volet (**Administration** volet > **Operations Management Suite**  >  **Carte de service**). Vous ne pouvez configurer qu’un seul espace de travail Operations Management Suite pour l’instant.

![volet d’espace de travail Operations Manager modifier Hello](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Configuration des règles et des valeurs de remplacement
Une règle, _Microsoft.SystemCenter.ServiceMapImport.Rule_, créé les informations d’extraction tooperiodically à partir de la carte de Service. minutage de synchronisation toochange, vous pouvez configurer des remplacements de règle de hello (**création** volet > **règles** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![fenêtre Propriétés de remplacements de Operations Manager Hello](media/oms-service-map/scom-overrides.png)

* **Enabled** : activer ou désactiver les mises à jour automatiques. 
* **IntervalMinutes**: réinitialiser l’heure hello entre les mises à jour. intervalle de salutation par défaut est d’une heure. Si vous souhaitez toosync server maps plus fréquemment, vous pouvez modifier la valeur de hello.
* **TimeoutSeconds**: réinitialiser la longueur de la durée avant expiration de la demande de hello hello. 
* **TimeWindowMinutes**: fenêtre de temps réinitialisation hello pour interroger des données. Valeur par défaut : fenêtre de 60 minutes. valeur maximale de Hello autorisé par carte de Service est de 60 minutes.

## <a name="known-issues-and-limitations"></a>Problèmes connus et limitations

conception actuelle Hello présente suivant de hello problèmes et limitations :
* Vous ne pouvez connecter tooa seul Operations Management Suite espace de travail.
* Bien que vous pouvez ajouter des serveurs toohello groupe de serveurs de carte de Service manuellement à l’aide de hello **création** volet, maps hello pour ces serveurs ne sont pas synchronisés immédiatement.  Ils seront synchronisées à partir de la carte de Service pendant hello prochain cycle de synchronisation.
* Si vous apportez des modifications de diagrammes d’Application distribuée toohello créé par le Pack d’administration de hello, ces modifications sont probablement écrasées dans la prochaine synchronisation de hello avec la carte de Service.

## <a name="create-a-service-principal"></a>Créer un principal du service
Pour obtenir une documentation Azure officielle sur la création d’un principal de service, consultez :
* [Création d’un principal de service à l’aide de PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Création d’un principal de service à l’aide d’Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Créez un principal de service à l’aide de hello portail Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Commentaires
Avez-vous des commentaires à nous transmettre à propos de Service Map ou de sa documentation ? Consultez notre [page Voix utilisateur](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map) qui vous permet de suggérer des fonctionnalités ou de voter pour les suggestions en cours.
