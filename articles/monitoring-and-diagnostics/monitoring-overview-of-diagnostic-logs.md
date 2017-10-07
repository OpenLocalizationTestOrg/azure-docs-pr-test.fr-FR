---
title: aaaOverview de journaux de Diagnostic Azure | Documents Microsoft
description: "Découvrez ce que sont les journaux de diagnostic Azure et comment vous pouvez utiliser les événements de toounderstand qui se produisent au sein d’une ressource Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a>Collecter et utiliser des données de journaux à partir de vos ressources Azure

## <a name="what-are-azure-resource-diagnostic-logs"></a>Présentation des journaux de diagnostic des ressources Azure
**Les journaux de diagnostic au niveau des ressources Azure** journaux émis par une ressource qui fournissent des données riches et fréquentes relatives au fonctionnement de hello de cette ressource. le contenu de ces journaux Hello varie selon le type de ressource. Les compteurs de règles du groupe de sécurité réseau et les audits de coffres de clés sont deux exemples de catégories de journaux de ressource.

Les journaux de diagnostic au niveau des ressources diffèrent hello [le journal d’activité](monitoring-overview-activity-logs.md). Hello journal d’activité fournit des indications sur les opérations de hello qui ont été effectuées sur les ressources dans votre abonnement à l’aide du Gestionnaire de ressources, par exemple, la création d’une machine virtuelle ou la suppression d’une application logique. Hello journal d’activité est un journal au niveau de l’abonnement. Les journaux de diagnostic des ressources, quant à eux, donnent un aperçu des opérations qui ont été effectuées au sein d’une ressource (par exemple, l’obtention d’un secret à partir d’un coffre de clés).

Les journaux de diagnostic des ressources diffèrent également des journaux de diagnostic de système d’exploitation invité. Les journaux de diagnostic de système d’exploitation invité sont collectés par un agent exécuté sur une machine virtuelle ou un autre type de ressource pris en charge. Les journaux de diagnostic au niveau des ressources ne nécessitent aucun agent et capturer des données propres à la ressource à partir de hello plateforme Azure lui-même, les journaux de diagnostic au niveau du système d’exploitation invité de capturer les données de système d’exploitation de hello et applications en cours d’exécution sur un ordinateur virtuel.

Pas toutes les ressources prennent en charge hello nouveau type de ressource des journaux de diagnostic décrites ici. Cet article contient une liste de section quels types de ressources prend en charge les nouveaux journaux de diagnostic au niveau des ressources hello.

![Comparaison entre les journaux de diagnostic des ressources et les autres types de journaux ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a>Comment utiliser les journaux de diagnostic au niveau des ressources
Voici quelques-unes des choses hello que vous pouvez faire avec les journaux de diagnostic de ressource :

![Positionnement logique des journaux de diagnostic des ressources](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* Enregistrer les tooa [ **compte de stockage** ](monitoring-archive-diagnostic-logs.md) pour l’inspection de l’audit ou manuelle. Vous pouvez spécifier à l’aide de temps (en jours) de rétention hello **les paramètres de diagnostic ressource**.
* [Les flux trop**concentrateurs d’événements** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) pour l’ingestion par un service tiers ou d’une solution personnalisée analytique telles que Power BI.
* Analysez-les avec [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)

Vous pouvez utiliser un compte de stockage ou d’espace de noms de concentrateurs d’événements qui n’est pas hello même abonnement comme une émission journaux hello. utilisateur de Hello qui configure hello paramètre doit avoir des abonnements tooboth d’accès appropriés RBAC hello.

## <a name="resource-diagnostic-settings"></a>Paramètres de diagnostic des ressources
Les journaux de diagnostic des ressources non liées au calcul sont configurés à l’aide des paramètres de diagnostic des ressources. **Paramètres de diagnostic des ressources** pour un contrôle des ressources :

* Où les journaux de diagnostic des ressources et les mesures sont envoyés (compte de stockage, Concentrateurs d’événements et/ou Analyse des journaux OMS).
* Les catégories de journal envoyées et les données de mesure également envoyées.
* La durée pendant laquelle chaque catégorie de journal doit être conservée dans un compte de stockage
    - Une durée de rétention de zéro jour signifie que les journaux sont conservés indéfiniment. Sinon, valeur de hello peut être n’importe quel nombre de jours compris entre 1 et 2147483647.
    - Si les stratégies de rétention sont définies, mais que le stockage des journaux dans un compte de stockage est désactivé (par exemple, si uniquement les options de concentrateurs d’événements ou OMS sont sélectionnées), les stratégies de rétention hello n’ont aucun effet.
    - Stratégies de rétention sont appliquées par jour, donc à hello fin d’une journée (UTC), consigne un jour hello qui est désormais au-delà de la stratégie de rétention hello sont supprimés. Par exemple, si vous aviez une stratégie de rétention d’un jour, au début de hello du jour hello aujourd'hui hello les journaux à partir de hello avant-hier seraient supprimés.

Ces paramètres sont configurés facilement via les paramètres de diagnostic hello pour une ressource Bonjour portail Azure, via Azure PowerShell et les commandes CLI ou hello [API REST de Azure analyse](https://msdn.microsoft.com/library/azure/dn931943.aspx).

> [!WARNING]
> Journaux de diagnostic et les mesures pour à partir de la couche de système d’exploitation invité hello d’utilisation des ressources (par exemple, les machines virtuelles ou Service Fabric) calcul [un mécanisme distinct pour la configuration et la sélection des sorties](../azure-diagnostics.md).
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a>La collection tooenable des journaux de diagnostic de ressources
Collecte des journaux de diagnostic de ressource peut être activée [dans le cadre de la création d’une ressource dans un modèle de gestionnaire de ressources](./monitoring-enable-diagnostic-logs-using-template.md) ou après avoir créé une ressource à partir de la page de cette ressource dans le portail de hello. Vous pouvez également activer la collection à tout moment à l’aide de commandes Azure PowerShell ou CLI, ou à l’aide de hello API REST du moniteur Azure.

> [!TIP]
> Ces instructions ne peuvent pas appliquer directement tooevery ressource. Consultez les liens de schéma hello bas hello cette page toounderstand spéciaux comme suit qui peuvent s’appliquer à des types de ressources toocertain.
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a>Activer la collecte des journaux de diagnostic de ressource dans le portail de hello
Vous pouvez activer la collecte des journaux de diagnostic de ressource Bonjour Azure portal après la création d’une ressource va de ressource spécifique tooa ou en naviguant tooAzure moniteur. tooenable cela via le moniteur de Windows Azure :

1. Bonjour [portail Azure](http://portal.azure.com), accédez tooAzure analyse et cliquez sur **les paramètres de Diagnostic**

    ![Section Surveillance d’Azure Monitor](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. Vous pouvez également filtrer la liste de hello par type de ressource ou le groupe de ressources, puis cliquez sur ressources hello pour laquelle vous aimeriez tooset un paramètre de diagnostic.

3. Si aucun paramètre n’existe sur la ressource hello que vous avez sélectionné, vous êtes invité à toocreate un paramètre. Cliquez sur « Activer les diagnostics ».

   ![Ajouter le paramètre de diagnostic - aucun paramètre existant](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   S’il existe des paramètres existants sur les ressources hello, vous verrez une liste de paramètres déjà configuré sur cette ressource. Cliquez sur « Ajouter le paramètre de diagnostic ».

   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. Donnez à votre définition d’un nom, hello cases à cocher pour chaque toowhich destination vous toosend données et configurer la ressource qui est utilisée pour chaque destination. Si vous le souhaitez, vous pouvez définir un nombre de jours tooretain ces journaux à l’aide de hello **rétention (jours)** curseurs (uniquement applicable toohello compte destination de stockage). Une durée de rétention de zéro jours stocke les journaux hello indéfiniment.
   
   ![Ajouter le paramètre de diagnostic - paramètres existants](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. Cliquez sur **Enregistrer**.

Après quelques instants, hello nouveau paramètre apparaît dans la liste des paramètres pour cette ressource et les journaux de diagnostic sont envoyées toohello spécifié destinations dès que les nouvelles données d’événement sont générées.

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a>Activer la collecte des journaux de diagnostic des ressources via PowerShell
collection de tooenable de journaux de diagnostic des ressources via Azure PowerShell, hello utilisation suivant les commandes :

stockage tooenable de journaux de diagnostic dans un compte de stockage, utilisez cette commande :

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

stockage Hello ID de compte est hello ID de ressource pour toowhich de compte de stockage hello souhaité toosend hello se connecte.

tooenable de diffusion en continu de concentrateur d’événements des journaux de diagnostic tooan, utilisez cette commande :

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

ID de règle Hello service bus est une chaîne au format suivant : `{Service Bus resource ID}/authorizationrules/{key name}`.

Utilisez la commande tooenable envoi de journaux de diagnostic tooa Analytique de journal espace de travail :

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

Vous pouvez obtenir les ID de ressource hello de votre espace de travail Analytique des journaux à l’aide de hello de commande suivante :

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

Vous pouvez combiner ces paramètres tooenable plusieurs options de sortie.

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a>Activer la collecte des journaux de diagnostic des ressources via l’interface de ligne de commande (CLI)
collection tooenable de journaux de diagnostic des ressources via hello CLI d’Azure, utilisez hello suivant de commandes :

stockage tooenable de journaux de diagnostic dans un compte de stockage, utilisez cette commande :

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

stockage Hello ID de compte est hello ID de ressource pour toowhich de compte de stockage hello souhaité toosend hello se connecte.

tooenable de diffusion en continu de concentrateur d’événements des journaux de diagnostic tooan, utilisez cette commande :

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

ID de règle Hello service bus est une chaîne au format suivant : `{Service Bus resource ID}/authorizationrules/{key name}`.

Utilisez la commande tooenable envoi de journaux de diagnostic tooa Analytique de journal espace de travail :

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

Vous pouvez combiner ces paramètres tooenable plusieurs options de sortie.

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a>Activer la collecte des journaux de diagnostic des ressources via l’API REST
les paramètres de diagnostic toochange à l’aide de hello API REST de moniteur Azure, consultez [ce document](https://msdn.microsoft.com/library/azure/dn931931.aspx).

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a>Gérer les paramètres de diagnostic des ressources dans le portail de hello
Assurez-vous que toutes vos ressources sont configurées avec des paramètres de diagnostic. Accédez trop**moniteur** Bonjour portail et ouvrez **les paramètres de Diagnostic**.

![Diagnostic lame de journaux dans le portail de hello](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

Vous avez peut-être tooclick section d’analyse « Services plus » toofind hello.

Ici, vous pouvez afficher et filtrer toutes les ressources qui prennent en charge les paramètres de diagnostic toosee si elles les diagnostics sont activés. Vous pouvez également Explorer toosee si plusieurs paramètres sont définies sur une ressource et vérifiez quel compte de stockage, espace de noms de concentrateurs d’événements et/ou espace de travail Analytique de journal qui passent des données à.

![Résultats des Journaux de diagnostic dans le portail](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

Ajout de qu'un paramètre de diagnostic affiche hello afficher les paramètres de Diagnostic, où vous pouvez activer, désactiver ou modifier vos paramètres de diagnostic pour hello la ressource sélectionnée.

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a>Services, catégories et schémas pris en charge pour les journaux de diagnostic de ressources
[Consultez l’article](monitoring-diagnostic-logs-schema.md) pour une liste complète des services pris en charge et les catégories du journal hello et les schémas utilisés par ces services.

## <a name="next-steps"></a>Étapes suivantes

* [Flux des journaux de diagnostic de ressource trop**concentrateurs d’événements**](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [Modifier les paramètres de diagnostic de ressources à l’aide de hello API REST du moniteur de Azure](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [Analyser les journaux du stockage Azure avec Log Analytics](../log-analytics/log-analytics-azure-storage.md)
