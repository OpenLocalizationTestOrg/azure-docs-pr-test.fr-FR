---
title: "aaaGet a démarré avec des rôles, les autorisations et la sécurité avec l’Analyseur de Azure | Documents Microsoft"
description: "Découvrez comment d’accéder aux ressources de toomonitoring des rôles intégrés et les autorisations toorestrict de l’analyse toouse Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2686e53b-72f0-4312-bcd3-3dc1b4a9b912
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: johnkem
ms.openlocfilehash: 44fdf2a697050309480dfc164ebab51445b19bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-roles-permissions-and-security-with-azure-monitor"></a>Familiarisation avec les rôles, les autorisations et la sécurité dans Azure Monitor
De nombreuses équipes doivent toostrictly réguler l’accès toomonitoring données et des paramètres. Par exemple, si des membres de l’équipe qui travaillent exclusivement sur l’analyse (ingénieurs du support technique, les ingénieurs de devops) ou si vous utilisez un fournisseur de services gérés, vous pouvez toogrant les accès tooonly données d’analyse tout en limitant leur toocreate possibilité, modifier, ou supprimer des ressources. Cet article explique comment tooquickly s’appliquent à un utilisateur de tooa du contrôle RBAC rôle intégré dans Azure ou créer votre propre rôle personnalisé pour un utilisateur ayant besoin de surveillance des autorisations limitées. Il décrit ensuite les considérations de sécurité pour vos ressources de moniteur de Windows Azure et comment vous pouvez limiter l’accès toohello données qu’ils contiennent.

## <a name="built-in-monitoring-roles"></a>Rôles de surveillance intégrés
Les rôles intégrés de l’analyse Azure sont conçues toohelp limite l’accès tooresources dans un abonnement tout en permettant les responsables de l’analyse d’infrastructure tooobtain et configurer les données de hello que dont ils ont besoin. Azure Monitor propose deux rôles prêts à l’emploi : un lecteur d’analyse et un contributeur d’analyse.

### <a name="monitoring-reader"></a>Lecteur d’analyse
Utilisateurs affectés du rôle de lecteur d’analyse de hello pour afficher toutes les données d’analyse dans un abonnement, mais ne peut pas modifier n’importe quelle ressource ou modifier des ressources connexes toomonitoring de paramètres. Ce rôle est approprié pour les utilisateurs dans une organisation, tels que les ingénieurs de prise en charge ou d’opérations, qui ont besoin de toobe en mesure de :

* Afficher des tableaux de bord de surveillance dans le portail de hello et créer leurs propres tableaux de bord de surveillance privé.
* Requête pour les mesures à l’aide de hello [API REST de Azure moniteur](https://msdn.microsoft.com/library/azure/dn931930.aspx), [applets de commande PowerShell](insights-powershell-samples.md), ou [inter-plateformes CLI](insights-cli-samples.md).
* Requête hello journal d’activité à l’aide de hello portail, Azure analyse API REST, les applets de commande PowerShell ou inter-plateformes CLI.
* Hello de vue [les paramètres de diagnostic](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) pour une ressource.
* Hello de vue [connecter profil](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) pour un abonnement.
* Affichez les paramètres de mise à l’échelle automatique.
* Afficher les activités et paramètres d’alerte.
* Accéder aux données Application Insights et affichez les données dans AI Analytics.
* Rechercher des données d’espace de travail Analytique des journaux (OMS), y compris les données d’utilisation de l’espace de travail hello.
* Afficher les groupes de gestion de Log Analytics (OMS).
* Récupérer le schéma de recherche hello Analytique des journaux (OMS).
* Répertorier les packs d’analyse décisionnelle de Log Analytics (OMS).
* Récupérer et exécuter les recherches enregistrées de Log Analytics (OMS).
* Récupérer la configuration de stockage hello Analytique des journaux (OMS).

> [!NOTE]
> Ce rôle ne donne pas de données de toolog d’accès en lecture qui a été transmis en continu tooan concentrateur d’événements ou dans un compte de stockage. [Voir ci-dessous](#security-considerations-for-monitoring-data) pour plus d’informations sur la configuration toothese d’accéder aux ressources.
> 
> 

### <a name="monitoring-contributor"></a>Contributeur d’analyse
Utilisateurs affectés hello collaborateur analyse rôle peut afficher toutes les données d’analyse dans un abonnement et créer ou modifier les paramètres d’analyse, mais ne peut pas modifier d’autres ressources. Ce rôle est un sur-ensemble du rôle de lecteur de surveillance hello et est approprié pour les membres de l’équipe de surveillance d’une organisation ou les fournisseurs de services gérés qui, en outre les autorisations toohello ci-dessus, devez toobe en mesure de :

* Publier des tableaux de bord d’analyse en tant que tableau de bord partagé.
* Définissez les [Paramètres de diagnostic](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings) pour une ressource.*
* Ensemble hello [connecter profil](monitoring-overview-activity-logs.md#export-the-activity-log-with-a-log-profile) pour un subscription.*
* Définir les activités et paramètres d’alerte.
* Créer des tests web et composants Application Insights.
* Répertorier les clés partagées d’espace de travail de Log Analytics (OMS).
* Activer ou désactiver les packs d’analyse décisionnelle de Log Analytics (OMS).
* Créer ou supprimer des recherches enregistrées de Log Analytics (OMS).
* Créer et supprimer la configuration du stockage hello Analytique des journaux (OMS).

* utilisateur doit disposer également séparément autorisation ListKeys sur tooset de ressource (stockage compte ou l’événement espace de noms hub) hello cible un profil de journal ou un paramètre de diagnostic.

> [!NOTE]
> Ce rôle ne donne pas de données de toolog d’accès en lecture qui a été transmis en continu tooan concentrateur d’événements ou dans un compte de stockage. [Voir ci-dessous](#security-considerations-for-monitoring-data) pour plus d’informations sur la configuration toothese d’accéder aux ressources.
> 
> 

## <a name="monitoring-permissions-and-custom-rbac-roles"></a>Autorisations d’analyse et rôles RBAC personnalisés
Si hello au-dessus de rôles intégrés ne répondent pas aux besoins de votre équipe hello, vous pouvez [créer un rôle RBAC personnalisé](../active-directory/role-based-access-control-custom-roles.md) avec des autorisations plus précises. Voici les opérations courantes d’Azure RBAC. moniteur avec leurs descriptions hello.

| Opération | Description |
| --- | --- |
| Microsoft.Insights/AlertRules/[Read, Write, Delete] |Règles d’alerte en lecture/écriture/suppression. |
| Microsoft.Insights/AlertRules/Incidents/Read |Liste d’incidents (historique de règle d’alerte hello déclenchée) des règles d’alerte. Cela s’applique uniquement toohello portal. |
| Microsoft.Insights/AutoscaleSettings/[Read, Write, Delete] |Paramètres de mise à l’échelle automatique en lecture/écriture/suppression. |
| Microsoft.Insights/DiagnosticSettings/[Read, Write, Delete] |Paramètres de diagnostic en lecture/écriture/suppression. |
| Microsoft.Insights/eventtypes/digestevents/Read |Cette autorisation est nécessaire pour les utilisateurs qui doivent accéder aux journaux tooActivity via le portail de hello. |
| Microsoft.Insights/eventtypes/values/Read |Événements du journal d’activité, (événements de gestion) dans un abonnement. Cette autorisation est applicable tooboth accès par programmation et portail toohello journal d’activité. |
| Microsoft.Insights/LogDefinitions/Read |Cette autorisation est nécessaire pour les utilisateurs qui doivent accéder aux journaux tooActivity via le portail de hello. |
| Microsoft.Insights/MetricDefinitions/Read |Lire des définitions de mesure (liste de types de mesure disponibles pour une ressource). |
| Microsoft.Insights/Metrics/Read |Lire des mesures pour une ressource. |

> [!NOTE]
> Accès tooalerts, les paramètres de diagnostic et de mesures d’une ressource nécessite que l’utilisateur hello a le type de ressource toohello accès en lecture et l’étendue de la ressource. (« Écriture ») de créer un profil de paramètre ou le journal de diagnostic que les archives tooa stockage compte ou flux tooevent concentrateurs requiert hello utilisateur tooalso autorisé ListKeys sur la ressource cible de hello.
> 
> 

Par exemple, à l’aide de hello au-dessus de table vous pouvez créer un rôle RBAC personnalisé pour un « activité de lecture du journal » comme suit :

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Activity Log Reader"
$role.Description = "Can view activity logs."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Insights/eventtypes/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription")
New-AzureRmRoleDefinition -Role $role 
```

## <a name="security-considerations-for-monitoring-data"></a>Considérations de sécurité pour l’analyse des données
Les données d’analyse (les fichiers journaux en particulier) peuvent contenir des informations sensibles, comme des adresses IP ou des noms d’utilisateur. La surveillance de données dans Azure se présente sous trois formes de base :

1. Hello journal d’activité, qui décrit toutes les actions de plan de contrôle sur votre abonnement Azure.
2. Les journaux de diagnostic, qui sont des journaux émis par une ressource.
3. Les mesures, qui sont émises par les ressources.

Les trois de ces types de données peuvent être stockées dans un compte de stockage ou transmis en continu tooEvent concentrateur, qui sont tous deux des ressources Azure à usage général. Comme ce sont des ressources à usage général, leur création, leur suppression et leur accès sont des opérations privilégiées généralement réservées à un administrateur. Nous vous suggérons d’utiliser hello pratiques pour l’utilisation incorrecte de tooprevent liés à l’analyse des ressources :

* Utilisez un compte de stockage unique, dédié pour l’analyse des données. Si vous devez tooseparate analyse les données en plusieurs comptes de stockage, l’utilisation d’un compte de stockage entre l’analyse ne partagent jamais et non analyse des données, comme cela peuvent donner par inadvertance ceux qui ne doivent accéder qu’aux données toomonitoring (par exemple). serveur SIEM tiers) accéder aux données d’analyse de toonon.
* Utiliser un unique, dédié Service Bus ou concentrateur d’événements espace de noms entre tous les paramètres de diagnostic pour hello de la même raison que ci-dessus.
* Limiter les comptes d’accès au stockage toomonitoring ou concentrateurs d’événements en les conservant dans un groupe de ressources distinct, et [utiliser étendue](../active-directory/role-based-access-control-what-is.md#basics-of-access-management-in-azure) sur vos rôles analyses toolimit accès tooonly ce groupe de ressources.
* Ne jamais autoriser hello ListKeys pour les comptes de stockage ou les concentrateurs d’événements au niveau de l’étendue de l’abonnement lorsqu’un utilisateur a seulement besoin d’accéder à des données toomonitoring. Au lieu de cela, accorder ces autorisations toohello utilisateur à une ressource ou un groupe de ressources (si vous avez un groupe de ressources surveillance dédié) étendue.

### <a name="limiting-access-toomonitoring-related-storage-accounts"></a>Limitation des comptes d’accès de stockage toomonitoring
Lorsqu’un utilisateur ou une application a besoin d’accéder aux données toomonitoring dans un compte de stockage, vous devez [générer une SAP de compte](https://msdn.microsoft.com/library/azure/mt584140.aspx) hello compte de stockage qui contient les données d’analyse avec un stockage tooblob accès en lecture seule de niveau de service. Dans PowerShell, cela pourrait ressembler à :

```powershell
$context = New-AzureStorageContext -ConnectionString "[connection string for your monitoring Storage Account]"
$token = New-AzureStorageAccountSASToken -ResourceType Service -Service Blob -Permission "rl" -Context $context
```

Vous pouvez alors accorder entité toohello jeton hello nécessitant tooread à partir de ce compte de stockage, et peut répertorier et lire à partir de tous les objets BLOB dans ce compte de stockage.

Ou bien, si vous devez toocontrol cette autorisation avec RBAC, vous pouvez accorder ce hello entité Microsoft.Storage/storageAccounts/listkeys/action l’autorisation sur ce compte de stockage particulier. Cela est nécessaire pour les utilisateurs qui ont besoin de tooset en mesure de toobe un diagnostic paramètre ou journal profil tooarchive tooa compte de stockage. Par exemple, vous pouvez créer hello suivant rôle RBAC personnalisé pour un utilisateur ou une application qui ne doit tooread à partir d’un compte de stockage :

```powershell
$role = Get-AzureRmRoleDefinition "Reader"
$role.Id = $null
$role.Name = "Monitoring Storage Account Reader"
$role.Description = "Can get hello storage account keys for a monitoring storage account."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/storageAccounts/listkeys/action")
$role.Actions.Add("Microsoft.Storage/storageAccounts/Read")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/myMonitoringStorageAccount")
New-AzureRmRoleDefinition -Role $role 
```

> [!WARNING]
> Hello ListKeys autorisation permet de clés de compte de stockage principal et secondaire hello utilisateur toolist hello. Ces clés accorder utilisateur de hello toutes signées autorisations (lire, écrire, créer des objets BLOB, supprimer des objets BLOB, etc.) dans l’ensemble signé services (blob, file d’attente, table, fichier) dans ce compte de stockage. Nous vous recommandons d’utiliser un SAP de compte comme décrit ci-dessus, lorsque cela est possible.
> 
> 

### <a name="limiting-access-toomonitoring-related-event-hubs"></a>Limitation des concentrateurs d’événements liés à toomonitoring accès
Un modèle similaire peut être suivi avec les concentrateurs d’événements, mais vous devez toocreate une règle d’autorisation d’écoute dédiée. Si vous souhaitez toogrant accès tooan application nécessitant uniquement des concentrateurs d’événements liés à toomonitoring toolisten, hello suivant :

1. Créer une stratégie d’accès partagé sur hello des hubs d’événements qui ont été créés pour la diffusion en continu des données d’analyse avec uniquement des revendications d’écoute. Pour cela, dans le portail de hello. Par exemple, vous pouvez l’appeler « monitoringReadOnly ». Si possible, vous pouvez toogive clé directement toohello consommateur et ignorer l’étape suivante de hello.
2. Si le consommateur de hello doit toobe tooget en mesure de hello clé ad hoc, accordez hello hello ListKeys intervention pour ce concentrateur d’événements. Il est également nécessaire pour les utilisateurs qui doivent tooset en mesure de toobe un paramètre de diagnostic ou des journaux de concentrateurs de tooevent toostream de profil. Par exemple, vous pouvez créer une règle RBAC :
   
   ```powershell
   $role = Get-AzureRmRoleDefinition "Reader"
   $role.Id = $null
   $role.Name = "Monitoring Event Hub Listener"
   $role.Description = "Can get hello key toolisten tooan event hub streaming monitoring data."
   $role.Actions.Clear()
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/authorizationrules/listkeys/action")
   $role.Actions.Add("Microsoft.ServiceBus/namespaces/Read")
   $role.AssignableScopes.Clear()
   $role.AssignableScopes.Add("/subscriptions/mySubscription/resourceGroups/myResourceGroup/providers/Microsoft.ServiceBus/namespaces/mySBNameSpace")
   New-AzureRmRoleDefinition -Role $role 
   ```

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur RBAC et les autorisations dans Resource Manager](../active-directory/role-based-access-control-what-is.md)
* [Vue d’ensemble de hello en lecture de la surveillance dans Azure](monitoring-overview.md)

