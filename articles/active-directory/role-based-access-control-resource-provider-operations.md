---
title: "Opérations du fournisseur Gestionnaire de ressources d’aaaAzure | Documents Microsoft"
description: "Détails hello opérations disponibles sur les fournisseurs de ressources de Microsoft Azure Resource Manager hello"
services: active-directory
documentationcenter: 
author: jboeshart
manager: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: jaboes
ms.openlocfilehash: 2d2f912ecbade335667d68fdc42ce03a2930a0eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-resource-provider-operations"></a>Opérations du fournisseur de ressources Azure Resource Manager

Ce document répertorie les opérations de hello disponibles pour chaque fournisseur de ressources Microsoft Azure Resource Manager. Ils peuvent être utilisés dans des rôles personnalisés tooprovide granulaires contrôle d’accès en fonction du rôle (RBAC) autorisations tooresources dans Azure. Notez que cette liste n’est pas exhaustive et que des opérations peuvent être ajoutées ou supprimées à mesure que chaque fournisseur est mis à jour. Chaînes d’opération suivent le format hello `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Pour obtenir la liste complète et en cours utilisez `Get-AzureRmProviderOperation` (dans PowerShell) ou `azure provider operations show` (dans Azure CLI) opérations toolist des fournisseurs de ressources Azure.

## <a name="microsoftadhybridhealthservice"></a>Microsoft.ADHybridHealthService

| Opération | Description |
|---|---|
|/configuration/action|Met à jour la configuration du client.|
|/services/action|Met à jour une instance de service dans le locataire de hello.|
|/configuration/write|Crée une configuration de client.|
|/configuration/read|Lit hello Configuration du client.|
|/services/write|Crée une instance de service dans le locataire de hello.|
|/services/read|Lit les instances de service hello dans le locataire de hello.|
|/services/delete|Supprime une instance de service dans le locataire de hello.|
|/services/servicemembers/action|Crée une instance de membre de service dans le service hello.|
|/services/servicemembers/read|Lit l’instance de membre hello service dans le service hello.|
|/services/servicemembers/delete|Supprime une instance de membre de service dans le service hello.|
|/services/servicemembers/alerts/read|Lit les alertes hello pour un membre du service.|
|/services/alerts/read|Lit les alertes hello pour un service.|
|/services/alerts/read|Lit les alertes hello pour un service.|

## <a name="microsoftadvisor"></a>Microsoft.Advisor

| Opération | Description |
|---|---|
|/generateRecommendations/action|Génère des recommandations|
|/suppressions/action|Crée/met à jour des suppressions|
|/register/action|Enregistre abonnement hello hello Microsoft Advisor|
|/generateRecommendations/read|Obtient l’état de génération de recommandations|
|/recommendations/read|Lit les recommandations|
|/suppressions/read|Obtient les suppressions|
|/suppressions/delete|Supprime la suppression|

## <a name="microsoftanalysisservices"></a>Microsoft.AnalysisServices

| Opération | Description |
|---|---|
|/servers/read|Extrait des informations de hello hello spécifié Analysis Server.|
|/servers/write|Crée ou met à jour hello spécifié le serveur d’analyse.|
|/servers/delete|Suppressions hello Analysis Server.|
|/servers/suspend/action|Suspend hello Analysis Server.|
|/servers/resume/action|Reprend hello Analysis Server.|
|/servers/checkNameAvailability<br>/action|Vérifie que le nom d’Analysis Server donné est valide et non utilisé.|

## <a name="microsoftapimanagement"></a>Microsoft.ApiManagement

| Opération | Description |
|---|---|
|/checkNameAvailability/action|Vérifie si le nom du service indiqué est disponible|
|/register/action|Inscrire l’abonnement pour le fournisseur de ressources Microsoft.ApiManagement|
|/unregister/action|Annuler l’inscription de l’abonnement pour le fournisseur de ressources Microsoft.ApiManagement|
|/service/write|Créer une nouvelle instance du service Gestion des API|
|/service/read|Lire les métadonnées d’une instance du service Gestion des API|
|/service/delete|Supprimer l’instance du service Gestion des API|
|/service/updatehostname/action|Configurer, mettre à jour ou supprimer des noms de domaine personnalisés pour un service Gestion des API|
|/service/uploadcertificate/action|Télécharger le certificat SSL pour un service Gestion des API|
|/service/backup/action|Service Gestion des API toohello spécifié conteneur de sauvegarde dans un utilisateur fourni de compte de stockage|
|/service/restore/action|Restaurer le Service Gestion des API à partir du conteneur spécifié de hello dans un utilisateur de compte de stockage|
|/service/managedeployments/action|Modifier une référence/unité, ajouter/supprimer des déploiements régionaux du service Gestion des API|
|/service/getssotoken/action|Obtient le jeton d’authentification unique qui peut être utilisé toologin portail hérité de Service de gestion des API en tant qu’administrateur|
|/service/applynetworkconfigurationupdates/action|Les mises à jour hello Microsoft.ApiManagement ressources en cours d’exécution dans le réseau virtuel toopick mis à jour les paramètres de réseau.|
|/service/operationresults/read|Obtient l’état actuel d’une opération longue|
|/service/networkStatus/read|Obtient l’état de l’accès réseau hello de ressources.|
|/service/loggers/read|Obtenir la liste des enregistreurs ou obtenir les détails d’un enregistreur|
|/service/loggers/write|Ajouter un nouvel enregistreur ou mettre à jour les détails d’un enregistreur existant|
|/service/loggers/delete|Supprimer l’enregistreur existant|
|/service/users/read|Obtenir la liste des utilisateurs inscrits ou obtenir les informations de compte d’un utilisateur|
|/service/users/write|Inscrire un nouvel utilisateur ou mettre à jour les informations de compte d’un utilisateur existant|
|/service/users/delete|Supprimer le compte d’utilisateur|
|/service/users/generateSsoUrl/action|Générez l’URL d’authentification unique. URL de Hello peut être utilisé tooaccess du portail d’administration|
|/service/users/subscriptions/read|Obtenir la liste des abonnements utilisateur|
|/service/users/keys/read|Obtenir la liste des clés utilisateur|
|/service/users/groups/read|Obtenir la liste des groupes d’utilisateurs|
|/service/tenant/operationResults/read|Obtenir la liste des résultats d’opération ou obtenir le résultat d’une opération spécifique|
|/service/tenant/policy/read|Obtenir la configuration de la stratégie pour le client de hello|
|/service/tenant/policy/write|Définir la configuration de la stratégie pour le client de hello|
|/service/tenant/policy/delete|Supprimer la configuration de la stratégie pour le client de hello|
|/service/tenant/configuration/save/action|Crée la validation avec configuration instantané toohello spécifié branche hello référentiel|
|/service/tenant/configuration/deploy/action|Exécute une tâche de déploiement tooapply modifications de configuration de toohello branche hello git spécifié dans la base de données.|
|/service/tenant/configuration/validate/action|Valide les modifications à partir de la branche git spécifié de hello|
|/service/tenant/configuration/operationResults/read|Obtenir la liste des résultats d’opération ou obtenir le résultat d’une opération spécifique|
|/service/tenant/configuration/syncState/read|Obtenir l’état de la dernière synchronisation git|
|/service/tenant/access/read|Obtenir les informations d’accès client|
|/service/tenant/access/write|Mettre à jour les informations d’accès client|
|/service/tenant/access/regeneratePrimaryKey/action|Régénérer la clé d’accès primaire|
|/service/tenant/access/regenerateSecondaryKey/action|Régénérer la clé d’accès secondaire|
|/service/identityProviders/read|Obtenir la liste des fournisseurs d’identité ou obtenir les détails du fournisseur d’identité|
|/service/identityProviders/write|Créer un nouveau fournisseur d’identité ou mettre à jour les détails d’un fournisseur d’identité existant|
|/service/identityProviders/delete|Supprimer le fournisseur d’identité existant|
|/service/subscriptions/read|Obtenir la liste des abonnements de produit ou obtenir les détails de l’abonnement de produit|
|/service/subscriptions/write|S’abonner à un produit existant du tooan utilisateur existante ou mettre à jour les détails de l’abonnement existant. Cette opération peut être utilisé toorenew abonnement|
|/service/subscriptions/delete|Supprimez l’abonnement. Cette opération peut être utilisé toodelete abonnement|
|/service/subscriptions/regeneratePrimaryKey/action|Régénérer la clé primaire d’abonnement|
|/service/subscriptions/regenerateSecondaryKey/action|Régénérer la clé secondaire d’abonnement|
|/service/backends/read|Obtenir la liste des serveurs principaux ou obtenir les détails du serveur principal|
|/service/backends/write|Ajouter un nouveau serveur principal ou mettre à jour les détails du serveur principal existant|
|/service/backends/delete|Supprimer le serveur principal existant|
|/service/apis/read|Obtenir la liste de toutes les API inscrites ou obtenir les détails de l’API|
|/service/apis/write|Créer une nouvelle API ou mettre à jour les détails de l’API existante|
|/service/apis/delete|Supprimer l’API existante|
|/service/apis/policy/read|Obtenir les détails de configuration de la stratégie pour l’API|
|/service/apis/policy/write|Définir les détails de configuration de la stratégie pour l’API|
|/service/apis/policy/delete|Supprimer la configuration de la stratégie de l’API|
|/service/apis/operations/read|Obtenir la liste des opérations d’API existantes ou obtenir les détails de l’opération d’API|
|/service/apis/operations/write|Créer une nouvelle opération d’API ou mettre à jour une opération d’API existante|
|/service/apis/operations/delete|Supprimer l’opération d’API existante|
|/service/apis/operations/policy/read|Obtenir les détails de configuration de la stratégie pour l’opération|
|/service/apis/operations/policy/write|Définir les détails de configuration de la stratégie pour l’opération|
|/service/apis/operations/policy/delete|Supprimer la configuration de la stratégie de l’opération|
|/service/products/read|Obtenir la liste des produits ou obtenir les détails du produit|
|/service/products/write|Créer un nouveau produit ou mettre à jour des détails du produit existants|
|/service/products/delete|Supprimer un produit existant|
|/service/products/subscriptions/read|Obtenir la liste des abonnements de produit|
|/service/products/apis/read|Obtenez la liste des API ajouté tooexisting produit|
|/service/products/apis/write|Ajouter un produit tooexisting API existant|
|/service/products/apis/delete|Supprimer une API existante d’un produit existant|
|/service/products/policy/read|Obtenir la configuration de stratégie d’un produit existant|
|/service/products/policy/write|Définir la configuration de stratégie pour un produit existant|
|/service/products/policy/delete|Supprimer la configuration de stratégie d’un produit existant|
|/service/products/groups/read|Obtenir la liste des groupes de développeurs associés au produit|
|/service/products/groups/write|Associer un groupe de développeurs existant à un produit existant|
|/service/products/groups/delete|Supprime l’association d’un groupe de développeurs existant à un produit existant|
|/service/openidConnectProviders/read|Obtenir la liste des fournisseurs OpenID Connect ou obtenir les détails du fournisseur OpenID Connect|
|/service/openidConnectProviders/write|Créer un nouveau fournisseur OpenID Connect ou mettre à jour les détails d’un fournisseur OpenID Connect existant|
|/service/openidConnectProviders/delete|Supprimer le fournisseur OpenID Connect existant|
|/service/certificates/read|Obtenir la liste des certificats ou obtenir les détails du certificat|
|/service/certificates/write|Ajouter un nouveau certificat|
|/service/certificates/delete|Supprimer le certificat existant|
|/service/properties/read|Obtient la liste de toutes les propriétés ou obtient les détails de la propriété spécifiée|
|/service/properties/write|Crée une nouvelle propriété ou met à jour la valeur de la propriété spécifiée|
|/service/properties/delete|Supprime la propriété existante|
|/service/groups/read|Obtenir la liste des groupes ou obtient les détails d’un groupe|
|/service/groups/write|Créer un nouveau groupe ou mettre à jour les détails du groupe existant|
|/service/groups/delete|Supprimer le groupe existant|
|/service/groups/users/read|Obtenir la liste des utilisateurs du groupe|
|/service/groups/users/write|Ajouter un groupe de tooexisting utilisateur existant|
|/service/groups/users/delete|Supprimer un utilisateur existant d’un groupe existant|
|/service/authorizationServers/read|Obtenir la liste des serveurs d’autorisation ou obtenir les détails du serveur d’autorisation|
|/service/authorizationServers/write|Créer un nouveau serveur d’autorisation ou mettre à jour les détails d’un serveur d’autorisation existant|
|/service/authorizationServers/delete|Supprimer le serveur d’autorisation existant|
|/service/reports/bySubscription/read|Obtenez le rapport agrégé par abonnement.|
|/service/reports/byRequest/read|Obtenir des données de republication de requêtes|
|/service/reports/byOperation/read|Obtenir le rapport agrégé par opérations|
|/service/reports/byGeo/read|Obtenir le rapport agrégé par région géographique|
|/service/reports/byUser/read|Obtenez le rapport agrégé par développeurs.|
|/service/reports/byTime/read|Obtenir le rapport agrégé par périodes|
|/service/reports/byApi/read|Obtenir le rapport agrégé par API|
|/service/reports/byProduct/read|Obtenez le rapport agrégé par produits.|

## <a name="microsoftappservice"></a>Microsoft.AppService

| Opération | Description |
|---|---|
|/appidentities/Read|Retourne hello inscrit avec hello passerelle de ressource (site web).|
|/appidentities/Write|Crée une nouvelle identité d’application.|
|/appidentities/Delete|Supprime une identité d’application existante.|
|/deploymenttemplates/listMetadata/Action|Répertorie les métadonnées de l’interface utilisateur associée hello package d’application API.|
|/deploymenttemplates/generate/Action|Retourne une tooprovision de modèle de déploiement des instances de l’application API.|
|/gateways/Read|Instance de passerelle retourne hello.|
|/gateways/Write|Crée une nouvelle passerelle ou met à jour une existante.|
|/gateways/Delete|Supprime une instance de passerelle existante.|
|/gateways/listLoginUris/Action|Remplit le magasin de jetons et retourne les URI de connexion OAuth.|
|/gateways/listKeys/Action|Retourne les secrets de passerelle.|
|/gateways/tokens/Write|Crée un nouveau jeton Zumo avec hello prénom.|
|/gateways/registrations/Read|Retourne hello inscrit avec hello passerelle de ressource (site web).|
|/gateways/registrations/Write|Inscrit une ressource (site web) avec hello passerelle.|
|/gateways/registrations/Delete|Annule l’inscription d’une ressource (site web) à partir de la passerelle de hello.|
|/apiapps/Read|Retourne hello l’instance de l’application API.|
|/apiapps/Write|Crée une nouvelle application API ou met à jour une existante.|
|/apiapps/Delete|Supprime une instance d’application API existante.|
|/apiapps/listStatus/Action|Retourne l’état d’application API.|
|/apiapps/listKeys/Action|Retourne des secrets d’application API.|
|/apiapps/apidefinitions/Read|Retourne une définition de l’API d’application API.|

## <a name="microsoftauthorization"></a>Microsoft.Authorization

| Opération | Description |
|---|---|
|/elevateAccess/action|Octroie hello appelant accès d’utilisateur administrateur de l’accès à l’étendue de locataire hello|
|/classicAdministrators/read|Lit les administrateurs hello pour l’abonnement de hello.|
|/classicAdministrators/write|Ajouter ou modifier l’abonnement de tooa administrateur.|
|/classicAdministrators/delete|Supprime l’abonnement de hello d’administrateur de hello.|
|/locks/read|Obtient les verrous à hello spécifié étendue.|
|/locks/write|Ajouter des verrous dans hello spécifié étendue.|
|/locks/delete|Supprimer les verrous à hello spécifié étendue.|
|/policyAssignments/read|Obtenez des informations sur une affectation de stratégie.|
|/policyAssignments/write|Créer une stratégie d’attribution de hello spécifié étendue.|
|/policyAssignments/delete|Supprimer une attribution de stratégie à hello spécifié étendue.|
|/permissions/read|Répertorie tous les hello autorisations hello appelant dans une étendue donnée.|
|/roleDefinitions/read|Obtenez des informations sur une définition de rôle.|
|/roleDefinitions/write|Créez ou mettez à jour une définition de rôle personnalisé avec des autorisations spécifiées et des portées pouvant être affectées.|
|/roleDefinitions/delete|Supprimer hello spécifié la définition de rôle personnalisée.|
|/providerOperations/read|Obtenez des opérations pour tous les fournisseurs de ressources qui peuvent être utilisées dans les définitions de rôles.|
|/policyDefinitions/read|Obtenez des informations sur une définition de stratégie.|
|/policyDefinitions/write|Créez une définition de stratégie personnalisée.|
|/policyDefinitions/delete|Supprimez une définition de stratégie.|
|/roleAssignments/read|Obtenez des informations sur une affectation de rôle.|
|/roleAssignments/write|Créer un rôle d’attribution à hello spécifié étendue.|
|/roleAssignments/delete|Supprimer une attribution de rôle à hello spécifié étendue.|

## <a name="microsoftautomation"></a>Microsoft.Automation

| Opération | Description |
|---|---|
|/automationAccounts/read|Obtient un compte Azure Automation|
|/automationAccounts/write|Crée ou met à jour un compte Azure Automation|
|/automationAccounts/delete|Supprime un compte Azure Automation|
|/automationAccounts/configurations/readContent/action|Obtient un contenu d’Azure Automation DSC|
|/automationAccounts/hybridRunbookWorkerGroups/read|Lit des ressources Runbook Worker hybrides|
|/automationAccounts/hybridRunbookWorkerGroups/delete|Supprime des ressources Runbook Worker hybrides|
|/automationAccounts/jobSchedules/read|Obtient une planification du travail Azure Automation|
|/automationAccounts/jobSchedules/write|Crée une planification du travail Azure Automation|
|/automationAccounts/jobSchedules/delete|Supprime une planification du travail Azure Automation|
|/automationAccounts/connectionTypes/read|Obtient une ressource de type de connexion Azure Automation|
|/automationAccounts/connectionTypes/write|Crée une ressource de type de connexion Azure Automation|
|/automationAccounts/connectionTypes/delete|Supprime une ressource de type de connexion Azure Automation|
|/automationAccounts/modules/read|Obtient un module Azure Automation|
|/automationAccounts/modules/write|Crée ou met à jour un module Azure Automation|
|/automationAccounts/modules/delete|Supprime un module Azure Automation|
|/automationAccounts/credentials/read|Obtient une ressource d’information d’identification Azure Automation|
|/automationAccounts/credentials/write|Crée ou met à jour une ressource d’information d’identification Azure Automation|
|/automationAccounts/credentials/delete|Supprime une ressource d’information d’identification Azure Automation|
|/automationAccounts/certificates/read|Obtient une ressource de certificat Azure Automation|
|/automationAccounts/certificates/write|Crée ou met à jour une ressource de certificat Azure Automation|
|/automationAccounts/certificates/delete|Supprime une ressource de certificat Azure Automation|
|/automationAccounts/schedules/read|Obtient une ressource de planification Azure Automation|
|/automationAccounts/schedules/write|Crée ou met à jour une ressource de planification Azure Automation|
|/automationAccounts/schedules/delete|Supprime une ressource de planification Azure Automation|
|/automationAccounts/jobs/read|Obtient un travail Azure Automation|
|/automationAccounts/jobs/write|Crée un travail Azure Automation|
|/automationAccounts/jobs/stop/action|Arrête un travail Azure Automation|
|/automationAccounts/jobs/suspend/action|Suspend un travail Azure Automation|
|/automationAccounts/jobs/resume/action|Reprend un travail Azure Automation|
|/automationAccounts/jobs/runbookContent/action|Obtient le contenu de runbook Azure Automation de hello hello lors de l’exécution du travail hello hello|
|/automationAccounts/jobs/output/action|Obtient la sortie hello d’un travail|
|/automationAccounts/jobs/read|Obtient un travail Azure Automation|
|/automationAccounts/jobs/write|Crée un travail Azure Automation|
|/automationAccounts/jobs/stop/action|Arrête un travail Azure Automation|
|/automationAccounts/jobs/suspend/action|Suspend un travail Azure Automation|
|/automationAccounts/jobs/resume/action|Reprend un travail Azure Automation|
|/automationAccounts/jobs/streams/read|Obtient un flux de travail Azure Automation|
|/automationAccounts/connections/read|Obtient une ressource de connexion Azure Automation|
|/automationAccounts/connections/write|Crée ou met à jour une ressource de connexion Azure Automation|
|/automationAccounts/connections/delete|Supprime une ressource de connexion Azure Automation|
|/automationAccounts/variables/read|Lit une ressource de variable Azure Automation|
|/automationAccounts/variables/write|Crée ou met à jour une ressource de variable Azure Automation|
|/automationAccounts/variables/delete|Supprime une ressource de variable Azure Automation|
|/automationAccounts/runbooks/readContent/action|Obtient le contenu d’un runbook Azure Automation hello|
|/automationAccounts/runbooks/read|Obtient un runbook Azure Automation|
|/automationAccounts/runbooks/write|Crée ou met à jour un runbook Azure Automation|
|/automationAccounts/runbooks/delete|Supprime un runbook Azure Automation|
|/automationAccounts/runbooks/draft/readContent/action|Obtient le contenu d’un brouillon de runbook Azure Automation hello|
|/automationAccounts/runbooks/draft/writeContent/action|Crée un contenu hello d’un brouillon de runbook Azure Automation|
|/automationAccounts/runbooks/draft/read|Obtient un brouillon de runbook Azure Automation|
|/automationAccounts/runbooks/draft/publish/action|Publie un brouillon de runbook Azure Automation|
|/automationAccounts/runbooks/draft/undoEdit/action|Annuler le brouillon de runbook Azure Automation modifications tooan|
|/automationAccounts/runbooks/draft/testJob/read|Obtient un travail de test de brouillon de runbook Azure Automation|
|/automationAccounts/runbooks/draft/testJob/write|Crée un travail de test de brouillon de runbook Azure Automation|
|/automationAccounts/runbooks/draft/testJob/stop/action|Arrête un travail de test de brouillon de runbook Azure Automation|
|/automationAccounts/runbooks/draft/testJob/suspend/action|Suspend un travail de test de brouillon de runbook Azure Automation|
|/automationAccounts/runbooks/draft/testJob/resume/action|Reprend un travail de test de brouillon de runbook Azure Automation|
|/automationAccounts/webhooks/read|Lit un webhook Azure Automation|
|/automationAccounts/webhooks/write|Crée ou met à jour un webhook Azure Automation|
|/automationAccounts/webhooks/delete|Supprime un webhook Azure Automation |
|/automationAccounts/webhooks/generateUri/action|Génère un URI pour un webhook Azure Automation|

## <a name="microsoftazureactivedirectory"></a>Microsoft.AzureActiveDirectory

Ce fournisseur n’est pas un fournisseur ARM complet et ne fournit aucune opération ARM.

## <a name="microsoftbatch"></a>Microsoft.Batch

| Opération | Description |
|---|---|
|/register/action|Enregistre abonnement hello hello fournisseur de ressources de traitement par lots et permet la création de comptes Batch hello|
|/batchAccounts/write|Crée un nouveau compte Batch ou met à jour un compte Batch existant|
|/batchAccounts/read|Répertorie les comptes de lots ou obtient hello les propriétés d’un compte de traitement par lots|
|/batchAccounts/delete|Supprime un compte Batch|
|/batchAccounts/listkeys/action|Répertorie les clés d’accès pour un compte Batch|
|/batchAccounts/regeneratekeys/action|Régénère les clés d’accès pour un compte Batch|
|/batchAccounts/syncAutoStorageKeys/action|Synchronise les clés d’accès pour le compte de stockage automatique hello configuré pour un compte de traitement par lots|
|/batchAccounts/applications/read|Répertorie les applications ou obtient les propriétés de hello d’une application|
|/batchAccounts/applications/write|Crée une nouvelle application ou met à jour une application existante|
|/batchAccounts/applications/delete|Supprime une application|
|/batchAccounts/applications/versions/read|Obtient les propriétés de hello d’un package d’application|
|/batchAccounts/applications/versions/write|Crée une nouveau package d’application ou met à jour un package d’application existant|
|/batchAccounts/applications/versions/activate/action|Active un package d’application|
|/batchAccounts/applications/versions/delete|Supprime un package d’application|
|/locations/quotas/read|Obtient les quotas de lot de hello l’abonnement à la région Azure hello spécifique|

## <a name="microsoftbilling"></a>Microsoft.Billing

| Opération | Description |
|---|---|
|/invoices/read|Répertorie les factures disponibles|

## <a name="microsoftbingmaps"></a>Microsoft.BingMaps

| Opération | Description |
|---|---|
|/mapApis/Read|Lire une opération|
|/mapApis/Write|Écrire une opération|
|/mapApis/Delete|Supprimer une opération|
|/mapApis/regenerateKey/action|Régénère la clé de hello|
|/mapApis/listSecrets/action|Liste hello Secrets|
|/mapApis/listSingleSignOnToken/action|En lecture seule connexion sur autorisation jeton pour la ressource hello|
|/Operations/read|Description de l’opération de hello.|

## <a name="microsoftcache"></a>Microsoft.Cache

| Opération | Description |
|---|---|
|/checknameavailability/action|Vérifie si un nom peut être utilisé avec un nouveau cache Redis|
|/register/action|Inscrit le fournisseur de ressources hello 'Microsoft.Cache' avec un abonnement|
|/unregister/action|Annule l’inscription du fournisseur de ressources hello 'Microsoft.Cache' avec un abonnement|
|/redis/write|Modifier les paramètres et la configuration dans le portail de gestion hello hello Redis Cache|
|/redis/read|Afficher les paramètres et la configuration du Cache de Redis de hello hello portail de gestion|
|/redis/delete|Delete hello l’intégralité du Cache Redis|
|/redis/listKeys/action|Valeur de hello vue des clés d’accès du Cache Redis dans le portail de gestion hello|
|/redis/regenerateKey/action|Valeur de clés d’accès du Cache Redis dans le portail de gestion hello hello de modification|
|/redis/import/action|Importer des données d’un format spécifié à partir de plusieurs objets blob dans Redis|
|/redis/export/action|Exporter Redis données tooprefixed objets BLOB de stockage dans le format spécifié|
|/redis/forceReboot/action|Forcez le redémarrage d’instance de cache, potentiellement avec une perte de données.|
|/redis/stop/action|Arrêtez une instance de cache.|
|/redis/start/action|Démarrez une instance de cache.|
|/redis/metricDefinitions/read|Obtient les métriques disponibles hello pour un Cache Redis|
|/redis/firewallRules/read|Obtenir des règles de pare-feu hello IP d’un Cache Redis|
|/redis/firewallRules/write|Modifier les règles de pare-feu hello IP d’un Cache Redis|
|/redis/firewallRules/delete|Supprimer des règles de pare-feu IP d’un cache Redis|
|/redis/listUpgradeNotifications/read|Liste hello dernières Notifications de mise à niveau pour le client de cache hello.|
|/redis/linkedservers/read|Obtenez les serveurs liés associés à un cache Redis.|
|/redis/linkedservers/write|Ajouter le serveur lié tooa Cache Redis|
|/redis/linkedservers/delete|Supprimer un serveur lié d’un cache Redis|
|/redis/patchSchedules/read|Hello obtient mise à jour corrective planification d’un Cache Redis|
|/redis/patchSchedules/write|Modifier hello mise à jour corrective de planification d’un Cache Redis|
|/redis/patchSchedules/delete|Supprimer la planification de correctif hello d’un Cache Redis|

## <a name="microsoftcertificateregistration"></a>Microsoft.CertificateRegistration

| Opération | Description |
|---|---|
|/provisionGlobalAppServicePrincipalInUserTenant/Action|Approvisionner le principal de service pour un principal d’application de service|
|/validateCertificateRegistrationInformation/Action|Valider l’objet d’achat de certificat sans le soumettre|
|/register/action|Inscrire le fournisseur de ressources Microsoft Certificates hello pour l’abonnement de hello|
|/certificateOrders/Write|Ajouter un nouveau certificateOrder ou en mettre un existant à jour|
|/certificateOrders/Delete|Supprimer un AppServiceCertificate existant|
|/certificateOrders/Read|Obtenir la liste de hello de CertificateOrders|
|/certificateOrders/reissue/Action|Réémettre un certificateorder existant|
|/certificateOrders/renew/Action|Renouveler un certificateorder existant|
|/certificateOrders/retrieveCertificateActions/Action|Récupérer la liste de hello des actions de certificat|
|/certificateOrders/retrieveEmailHistory/Action|Récupérer l’historique d’e-mails de certificat|
|/certificateOrders/resendEmail/Action|Renvoyer l’e-mail de certificat|
|/certificateOrders/verifyDomainOwnership/Action|Vérifier la propriété du domaine|
|/certificateOrders/resendRequestEmails/Action|Renvoyer l’adresse de messagerie de demande des messages électroniques tooanother|
|/certificateOrders/resendRequestEmails/Action|Récupérer le Seal de site pour un App Service Certificate émis|
|/certificateOrders/certificates/Write|Ajouter un nouveau certificat ou en mettre un existant à jour|
|/certificateOrders/certificates/Delete|Supprimer un certificat existant|
|/certificateOrders/certificates/Read|Obtenir la liste de hello de certificats|

## <a name="microsoftclassiccompute"></a>Microsoft.ClassicCompute

| Opération | Description |
|---|---|
|/register/action|Registre tooClassic calcul|
|/checkDomainNameAvailability/action|Vérifie la disponibilité de hello d’un nom de domaine donné.|
|/moveSubscriptionResources/action|Déplacer un abonnement différent de toutes les ressources classiques tooa.|
|/validateSubscriptionMoveAvailability/action|Valider la disponibilité de l’abonnement hello pour l’opération de déplacement classique.|
|/operatingSystemFamilies/read|Répertorie les familles de système d’exploitation invité hello disponibles dans Microsoft Azure et répertorie les versions de système d’exploitation hello disponibles pour chaque f
|/capabilities/read|Illustre des fonctionnalités de hello|
|/operatingSystems/read|Répertorie les versions de hello du système d’exploitation de hello invité qui sont actuellement disponibles dans Microsoft Azure.|
|/resourceTypes/skus/read|Obtient la liste de référence (SKU) hello pour les types de ressources pris en charge.|
|/domainNames/read|Retourne les noms de domaine hello pour les ressources.|
|/domainNames/write|Ajouter ou modifier les noms de domaine hello pour les ressources.|
|/domainNames/delete|Supprimez les noms de domaine hello pour les ressources.|
|/domainNames/swap/action|Échange hello emplacement de production toohello emplacement de mise en lots.|
|/domainNames/serviceCertificates/read|Retourne hello certificats de service utilisés.|
|/domainNames/serviceCertificates/write|Ajouter ou modifier les certificats de service hello utilisés.|
|/domainNames/serviceCertificates/delete|Supprimer les certificats de service hello utilisés.|
|/domainNames/serviceCertificates/operationStatuses/read|Lit l’état de l’opération hello pour les certificats de service de noms de domaine hello.|
|/domainNames/capabilities/read|Affiche des capacités du nom de domaine de hello|
|/domainNames/extensions/read|Retourne hello des extensions de nom de domaine.|
|/domainNames/extensions/write|Ajouter des extensions de nom de domaine hello.|
|/domainNames/extensions/delete|Supprimer les extensions de nom de domaine hello.|
|/domainNames/extensions/operationStatuses/read|Lit l’état de l’opération hello pour les extensions de noms de domaine hello.|
|/domainNames/active/write|Définit le nom du domaine actif hello.|
|/domainNames/slots/read|Affiche les emplacements de déploiement hello.|
|/domainNames/slots/write|Crée ou mettre à jour le déploiement de hello.|
|/domainNames/slots/delete|Supprime un emplacement de déploiement donné.|
|/domainNames/slots/start/action|Démarre un emplacement de déploiement.|
|/domainNames/slots/stop/action|Suspend l’emplacement de déploiement hello.|
|/domainNames/slots/operationStatuses/read|Lit l’état de l’opération hello pour les emplacements de noms de domaine hello.|
|/domainNames/slots/roles/read|Obtenir le rôle de hello pour l’emplacement de déploiement hello.|
|/domainNames/slots/roles/extensionReferences/read|Retourne hello référence d’extension pour le rôle d’emplacement de déploiement hello.|
|/domainNames/slots/roles/extensionReferences/write|Ajouter ou modifier la référence d’extension hello pour le rôle d’emplacement de déploiement hello.|
|/domainNames/slots/roles/extensionReferences/delete|Supprimez la référence d’extension hello pour le rôle d’emplacement de déploiement hello.|
|/domainNames/slots/roles/extensionReferences/operationStatuses/read|Lit l’état de l’opération hello pour références d’extension rôles emplacements les noms de domaine hello.|
|/domainNames/slots/roles/roleInstances/read|Obtenir l’instance de rôle hello.|
|/domainNames/slots/roles/roleInstances/restart/action|Redémarre des instances de rôle.|
|/domainNames/slots/roles/roleInstances/reimage/action|Instance de rôle reimages hello.|
|/domainNames/slots/roles/roleInstances/operationStatuses/read|Lit l’état de l’opération hello hello domaine noms emplacements rôles instances de rôle.|
|/domainNames/slots/state/start/write|Modifications hello toostopped d’état emplacement de déploiement.|
|/domainNames/slots/state/stop/write|Modifications hello toostarted d’état emplacement de déploiement.|
|/domainNames/slots/upgradeDomain/write|Parcourir le domaine de mise à niveau hello.|
|/domainNames/internalLoadBalancers/read|Obtient les équilibreurs de charge internes hello.|
|/domainNames/internalLoadBalancers/write|Crée un nouvel équilibrage de charge interne.|
|/domainNames/internalLoadBalancers/delete|Supprimez un nouvel équilibrage de charge interne.|
|/domainNames/internalLoadBalancers/operationStatuses/read|Lit l’état de l’opération hello pour équilibreurs de charge internes des noms de domaine de hello.|
|/domainNames/loadBalancedEndpointSets/read|Affiche les jeux de point de terminaison à charge équilibrée hello|
|/domainNames/loadBalancedEndpointSets/operationStatuses/read|Lit l’état de l’opération hello pour les jeux de point de terminaison à charge équilibrée des noms de domaine de hello.|
|/domainNames/availabilitySets/read|Afficher hello groupe à haute disponibilité pour la ressource de hello.|
|/quotas/read|Récupérer le quota de hello pour l’abonnement de hello.|
|/virtualMachines/read|Récupère la liste des machines virtuelles.|
|/virtualMachines/write|Ajoutez ou modifiez des machines virtuelles.|
|/virtualMachines/delete|Supprime des machines virtuelles.|
|/virtualMachines/start/action|Démarrer l’ordinateur virtuel de hello.|
|/virtualMachines/redeploy/action|Redéploie hello virtual machine.|
|/virtualMachines/restart/action|Redémarre des machines virtuelles.|
|/virtualMachines/stop/action|Arrête hello machine virtuelle.|
|/virtualMachines/shutdown/action|Arrêter la machine virtuelle hello.|
|/virtualMachines/attachDisk/action|Joint un ordinateur virtuel de données disque tooa.|
|/virtualMachines/detachDisk/action|Détache un disque de données d’une machine virtuelle.|
|/virtualMachines/downloadRemoteDesktopConnectionFile/action|Télécharge le fichier RDP de hello pour la machine virtuelle.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/read|Obtient le groupe de sécurité réseau hello associée à interface réseau de hello.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/write|Ajoute un groupe de sécurité réseau associé à interface réseau de hello.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/delete|Supprime le groupe de sécurité réseau hello associée à interface réseau de hello.|
|/virtualMachines/networkInterfaces/<br>associatedNetworkSecurityGroups/operationStatuses/read|Lit l’état de l’opération hello pour les ordinateurs virtuels de hello associés des groupes de sécurité réseau.|
|/virtualMachines/providers/Microsoft.Insights/metricDefinitions/read|Obtient les définitions de métriques hello.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/read|Obtenir les paramètres de diagnostic hello.|
|/virtualMachines/providers/Microsoft.Insights/diagnosticSettings/write|Ajoutez ou modifiez des paramètres de diagnostics.|
|/virtualMachines/metrics/read|Obtient les métriques de hello.|
|/virtualMachines/operationStatuses/read|Lit l’état de l’opération hello pour les ordinateurs virtuels de hello.|
|/virtualMachines/extensions/read|Obtient l’extension de machine virtuelle hello.|
|/virtualMachines/extensions/write|Place l’extension de machine virtuelle hello.|
|/virtualMachines/extensions/operationStatuses/read|Lit l’état de l’opération hello pour les extensions de machines virtuelles hello.|
|/virtualMachines/asyncOperations/read|Obtient les hello éventuelles opérations asynchrones|
|/virtualMachines/disks/read|Récupère la liste des disques de données|
|/virtualMachines/associatedNetworkSecurityGroups/read|Obtient le groupe de sécurité réseau hello associé avec l’ordinateur virtuel de hello.|
|/virtualMachines/associatedNetworkSecurityGroups/write|Ajoute un groupe de sécurité réseau associé avec l’ordinateur virtuel de hello.|
|/virtualMachines/associatedNetworkSecurityGroups/delete|Supprime le groupe de sécurité réseau hello associé avec l’ordinateur virtuel de hello.|
|/virtualMachines/associatedNetworkSecurityGroups/operationStatuses/read|Lit l’état de l’opération hello pour les ordinateurs virtuels de hello associés des groupes de sécurité réseau.|

## <a name="microsoftclassicnetwork"></a>Microsoft.ClassicNetwork

| Opération | Description |
|---|---|
|/register/action|Registre tooClassic réseau|
|/gatewaySupportedDevices/read|Récupère la liste hello des appareils pris en charge.|
|/reservedIps/read|Obtient hello des adresses IP réservées|
|/reservedIps/write|Ajouter une nouvelle adresse IP réservée|
|/reservedIps/delete|Supprimez une adresse IP réservée.|
|/reservedIps/link/action|Lier une adresse IP réservée|
|/reservedIps/join/action|Joindre une adresse IP réservée|
|/reservedIps/operationStatuses/read|Lit l’état de l’opération hello pour les adresses IP hello réservé.|
|/virtualNetworks/read|Obtenir le réseau virtuel de hello.|
|/virtualNetworks/write|Ajoutez un nouveau réseau virtuel.|
|/virtualNetworks/delete|Supprime le réseau virtuel de hello.|
|/virtualNetworks/peer/action|Appaire un réseau virtuel avec un autre réseau virtuel.|
|/virtualNetworks/join/action|Joint le réseau virtuel de hello.|
|/virtualNetworks/checkIPAddressAvailability/action|Vérifie la disponibilité de hello d’une adresse IP donnée dans un réseau virtuel.|
|/virtualNetworks/capabilities/read|Illustre des fonctionnalités de hello|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/read|Obtient le groupe de sécurité réseau hello associé au sous-réseau de hello.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/write|Ajoute un groupe de sécurité réseau associé au sous-réseau de hello.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/delete|Supprime le groupe de sécurité réseau hello associé au sous-réseau de hello.|
|/virtualNetworks/subnets/<br>associatedNetworkSecurityGroups/operationStatuses/read|Lit l’état de l’opération hello pour le groupe de sécurité réseau hello réseau virtuel sous-réseau associé.|
|/virtualNetworks/operationStatuses/read|Lit l’état de l’opération hello pour les réseaux virtuels hello.|
|/virtualNetworks/gateways/read|Obtient les passerelles de réseau virtuel hello.|
|/virtualNetworks/gateways/write|Ajoute une passerelle de réseau virtuel.|
|/virtualNetworks/gateways/delete|Supprime la passerelle de réseau virtuel hello.|
|/virtualNetworks/gateways/startDiagnostics/action|Démarre les Diagnostics de passerelle de réseau virtuel hello.|
|/virtualNetworks/gateways/stopDiagnostics/action|Arrête hello Diagnostics pour la passerelle de réseau virtuel hello.|
|/virtualNetworks/gateways/downloadDiagnostics/action|Télécharge les diagnostics de la passerelle hello.|
|/virtualNetworks/gateways/listCircuitServiceKey/action|Récupère la clé de service du circuit hello.|
|/virtualNetworks/gateways/downloadDeviceConfigurationScript/action|Télécharge le script de configuration de périphérique hello.|
|/virtualNetworks/gateways/listPackage/action|Répertorie le package de passerelle de réseau virtuel hello.|
|/virtualNetworks/gateways/operationStatuses/read|Lit l’état de l’opération hello pour les passerelles des réseaux virtuels hello.|
|/virtualNetworks/gateways/packages/read|Obtient le package de passerelle de réseau virtuel hello.|
|/virtualNetworks/gateways/connections/read|Récupère la liste hello des connexions.|
|/virtualNetworks/gateways/connections/connect/action|Connecte une connexion de passerelle site toosite.|
|/virtualNetworks/gateways/connections/disconnect/action|Déconnecte une connexion de passerelle site toosite.|
|/virtualNetworks/gateways/connections/test/action|Teste une connexion de passerelle site toosite.|
|/virtualNetworks/gateways/clientRevokedCertificates/read|Hello de lecture de révoquer les certificats clients.|
|/virtualNetworks/gateways/clientRevokedCertificates/write|Révoque un certificat client.|
|/virtualNetworks/gateways/clientRevokedCertificates/delete|Annule la révocation d’un certificat client.|
|/virtualNetworks/gateways/clientRootCertificates/read|Recherche des certificats racines de client hello.|
|/virtualNetworks/gateways/clientRootCertificates/write|Télécharge un nouveau certificat racine client.|
|/virtualNetworks/gateways/clientRootCertificates/delete|Supprime un certificat de client de passerelle de réseau virtuel hello.|
|/virtualNetworks/gateways/clientRootCertificates/download/action|Télécharge le certificat par empreinte.|
|/virtualNetworks/gateways/clientRootCertificates/listPackage/action|Répertorie le package de certificat de passerelle de réseau virtuel hello.|
|/networkSecurityGroups/read|Obtient le groupe de sécurité réseau hello.|
|/networkSecurityGroups/write|Ajoute un nouveau groupe de sécurité réseau.|
|/networkSecurityGroups/delete|Supprime le groupe de sécurité réseau hello.|
|/networkSecurityGroups/operationStatuses/read|Lit l’état de l’opération hello pour le groupe de sécurité réseau hello.|
|/networkSecurityGroups/securityRules/read|Obtient la règle de sécurité hello.|
|/networkSecurityGroups/securityRules/write|Ajoute ou met à jour une règle de sécurité.|
|/networkSecurityGroups/securityRules/delete|Supprime la règle de sécurité hello.|
|/networkSecurityGroups/securityRules/operationStatuses/read|Lit l’état de l’opération hello pour les règles de sécurité groupe de sécurité hello réseau.|
|/quotas/read|Récupérer le quota de hello pour l’abonnement de hello.|

## <a name="microsoftclassicstorage"></a>Microsoft.ClassicStorage

| Opération | Description |
|---|---|
|/register/action|TooClassic de Registre de stockage|
|/checkStorageAccountAvailability/action|Vérifications de disponibilité hello d’un compte de stockage.|
|/capabilities/read|Illustre des fonctionnalités de hello|
|/publicImages/read|Obtient hello publique machine virtuelle image.|
|/images/read|Image de hello retourne.|
|/storageAccounts/read|Retourne le compte de stockage hello avec hello compte donné.|
|/storageAccounts/write|Ajoute un nouveau compte de stockage.|
|/storageAccounts/delete|Supprimer le compte de stockage hello.|
|/storageAccounts/listKeys/action|Répertorie les touches d’accès hello pour les comptes de stockage hello.|
|/storageAccounts/regenerateKey/action|Régénère les clés d’accès existantes hello hello compte de stockage.|
|/storageAccounts/operationStatuses/read|Lit l’état de l’opération pour la ressource de hello hello.|
|/storageAccounts/images/read|Retourne hello image du compte de stockage.|
|/storageAccounts/images/delete|Supprime une image du compte de stockage spécifique.|
|/storageAccounts/disks/read|Retourne hello disque de compte de stockage.|
|/storageAccounts/disks/write|Ajoute un disque de compte de stockage.|
|/storageAccounts/disks/delete|Supprime un disque de compte de stockage spécifique.|
|/storageAccounts/disks/operationStatuses/read|Lit l’état de l’opération pour la ressource de hello hello.|
|/storageAccounts/osImages/read|Retourne hello image de système d’exploitation de compte de stockage.|
|/storageAccounts/osImages/delete|Supprime une image du système d’exploitation de compte de stockage spécifique.|
|/storageAccounts/services/read|Obtenir les services disponibles hello.|
|/storageAccounts/services/metricDefinitions/read|Obtient les définitions de métriques hello.|
|/storageAccounts/services/metrics/read|Obtient les métriques de hello.|
|/storageAccounts/services/diagnosticSettings/read|Obtenir les paramètres de diagnostic hello.|
|/storageAccounts/services/diagnosticSettings/write|Ajoutez ou modifiez des paramètres de diagnostics.|
|/disks/read|Retourne hello disque de compte de stockage.|
|/osImages/read|Image de système d’exploitation renvoie hello.|
|/quotas/read|Récupérer le quota de hello pour l’abonnement de hello.|

## <a name="microsoftcognitiveservices"></a>Microsoft.CognitiveServices

| Opération | Description |
|---|---|
|/accounts/read|Lit les comptes d’API.|
|/accounts/write|Écrit les comptes d’API.|
|/accounts/delete|Supprime les comptes d’API|
|/accounts/listKeys/action|Afficher la liste des clés|
|/accounts/regenerateKey/action|Régénérer la clé|
|/accounts/skus/read|Lit les références disponibles pour une ressource existante.|
|/accounts/usages/read|Obtenir l’utilisation du quota hello pour une ressource existante.|
|/Operations/read|Description de l’opération de hello.|

## <a name="microsoftcommerce"></a>Microsoft.Commerce

| Opération | Description |
|---|---|
|/RateCard/read|Retourne les données, les métadonnées de la ressource/compteur et les taux pour hello l’abonnement indiqué d’offre.|
|/UsageAggregates/read|Récupère l’utilisation de Microsoft Azure par un abonnement. résultat de Hello contient des agrégats de données d’utilisation, abonnement et ressources informations connexes, sur une période donnée.|

## <a name="microsoftcompute"></a>Microsoft.Compute

| Opération | Description |
|---|---|
|/register/action|Inscrit l’abonnement auprès du fournisseur de ressources Microsoft.Compute|
|/restorePointCollections/read|Obtenir les propriétés de hello d’une collection de points de restauration|
|/restorePointCollections/write|Crée une nouvelle collection de points de restauration ou met à jour une collection existante|
|/restorePointCollections/delete|Collection de points de restauration hello suppressions et les points de restauration de la relation contenant-contenu|
|/restorePointCollections/restorePoints/read|Obtenir les propriétés de hello d’un point de restauration|
|/restorePointCollections/restorePoints/write|Créer un nouveau point de restauration|
|/restorePointCollections/restorePoints/delete|Supprime le point de restauration hello|
|/restorePointCollections/restorePoints/retrieveSasUris/action|Obtenir les propriétés de hello d’un point de restauration, ainsi que l’objet blob SAS URI|
|/virtualMachineScaleSets/read|Obtenir les propriétés de hello d’un ensemble d’échelle de machine virtuelle|
|/virtualMachineScaleSets/write|Créer ou mettre à jour un groupe de machines virtuelles identiques|
|/virtualMachineScaleSets/delete|Supprime l’ensemble d’échelle de machine virtuelle hello|
|/virtualMachineScaleSets/start/action|Démarre hello des instances de l’ensemble d’échelle de machine virtuelle hello|
|/virtualMachineScaleSets/powerOff/action|Met hors tension les instances de hello de hello machines virtuelles identiques|
|/virtualMachineScaleSets/restart/action|Redémarre les instances de hello de hello machines virtuelles identiques|
|/virtualMachineScaleSets/deallocate/action|Met hors tension et libère des ressources de calcul hello pour les instances de hello de hello machines virtuelles identiques |
|/virtualMachineScaleSets/manualUpgrade/action|Modèle de toolatest d’instances de l’ensemble d’échelle de machine virtuelle hello des mises à jour manuellement|
|/virtualMachineScaleSets/scale/action|Augmenter/diminuer le nombre d’instances d’un groupe de machines virtuelles identiques existant|
|/virtualMachineScaleSets/instanceView/read|Obtient la vue d’instance hello de hello machines virtuelles identiques|
|/virtualMachineScaleSets/skus/read|Listes hello des références valides pour un ensemble d’échelle de machine virtuelle existante|
|/virtualMachineScaleSets/virtualMachines/read|Récupère les propriétés hello d’un ordinateur virtuel dans un ensemble d’échelle de machines virtuelles|
|/virtualMachineScaleSets/virtualMachines/delete|Supprimer une machine virtuelle spécifique d’un groupe de machines virtuelles identiques|
|/virtualMachineScaleSets/virtualMachines/start/action|Démarrer une instance de machine virtuelle dans un groupe de machines virtuelles identiques.|
|/virtualMachineScaleSets/virtualMachines/powerOff/action|Mettre hors tension une instance de machine virtuelle dans un groupe de machines virtuelles identiques.|
|/virtualMachineScaleSets/virtualMachines/restart/action|Redémarrer une instance de machine virtuelle dans un groupe de machines virtuelles identiques.|
|/virtualMachineScaleSets/virtualMachines/deallocate/action|Met hors tension et libère des ressources de calcul hello pour un ordinateur virtuel dans un ensemble d’échelle de machine virtuelle.|
|/virtualMachineScaleSets/virtualMachines/instanceView/read|Récupère la vue d’instance hello d’un ordinateur virtuel dans un ensemble d’échelle de machine virtuelle.|
|/images/read|Obtenir les propriétés hello Hello Image|
|/images/write|Créer ou mettre à jour une image|
|/images/delete|Supprime l’image de hello|
|/operations/read|Répertorier les opérations disponibles dans le fournisseur de ressources Microsoft.Compute|
|/disks/read|Obtenir les propriétés d’un disque de hello|
|/disks/write|Créer ou mettre à jour un disque|
|/disks/delete|Suppressions hello disque|
|/disks/beginGetAccess/action|Obtenir hello URI SAS du disque de hello pour l’accès aux objets blob|
|/disks/endGetAccess/action|Révoquer hello URI SAS du disque de hello|
|/snapshots/read|Obtenir les propriétés hello d’un instantané|
|/snapshots/write|Créer ou mettre à jour une capture instantanée|
|/snapshots/delete|Supprimer une capture instantanée|
|/availabilitySets/read|Obtenir les propriétés de hello d’un ensemble de disponibilité|
|/availabilitySets/write|Créer ou mettre à jour un groupe à haute disponibilité|
|/availabilitySets/delete|Supprime le groupe à haute disponibilité hello|
|/availabilitySets/vmSizes/read|Liste des tailles disponibles pour la création ou mise à jour d’une machine virtuelle dans le groupe à haute disponibilité hello|
|/virtualMachines/read|Obtenir les propriétés hello d’un ordinateur virtuel|
|/virtualMachines/write|Créer ou mettre à jour une machine virtuelle|
|/virtualMachines/delete|Supprime l’ordinateur virtuel de hello|
|/virtualMachines/start/action|Démarre l’ordinateur virtuel hello|
|/virtualMachines/powerOff/action|Met hors tension de l’ordinateur virtuel de hello. Notez que l’ordinateur virtuel hello continue toobe facturé.|
|/virtualMachines/redeploy/action|Redéployer la machine virtuelle|
|/virtualMachines/restart/action|Redémarre l’ordinateur virtuel de hello|
|/virtualMachines/deallocate/action|Met hors tension l’ordinateur virtuel de hello et versions hello des ressources de calcul|
|/virtualMachines/generalize/action|Définit hello machine virtuelle état tooGeneralized et prépare la machine virtuelle de hello pour la capture|
|/virtualMachines/capture/action|Capture de machine virtuelle de hello en copiant les disques durs virtuels et génère un modèle qui peut être utilisé toocreate des machines virtuelles similaires|
|/virtualMachines/convertToManagedDisks/action|Convertit les disques hello blob, en fonction des disques de toomanaged hello machine virtuelle|
|/virtualMachines/vmSizes/read|Répertorie les tailles disponibles hello virtuels peuvent être mis à jour pour|
|/virtualMachines/instanceView/read|Obtient hello statut d’exécution détaillé de la machine virtuelle de hello et ses ressources|
|/virtualMachines/extensions/read|Obtenir les propriétés de hello d’une extension de machine virtuelle|
|/virtualMachines/extensions/write|Créer ou mettre à jour une extension de machine virtuelle|
|/virtualMachines/extensions/delete|Supprime l’extension de machine virtuelle hello|
|/locations/vmSizes/read|Répertorier les tailles de machines virtuelles disponibles dans un emplacement|
|/locations/usages/read|Obtient les limites de service et l’utilisation actuelle des ressources de calcul de l’abonnement hello dans un emplacement|
|/locations/operations/read|Obtient l’état de hello d’une opération asynchrone|

## <a name="microsoftcontainerregistry"></a>Microsoft.ContainerRegistry

| Opération | Description |
|---|---|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources de Registre de conteneur hello et permet la création de hello des registres du conteneur.|
|/checknameavailability/read|Vérifie que le nom du registre est valide et qu’il n’est pas déjà utilisé.|
|/registries/read|Retourne hello liste des registres de conteneur ou obtient hello propriétés de Registre de conteneur spécifié hello.|
|/registries/write|Crée un conteneur de Registre avec hello paramètres spécifiés ou mettre à jour les propriétés de hello ou les balises de Registre de conteneur spécifié hello.|
|/registries/delete|Supprime un registre de conteneurs existant.|
|/registries/listCredentials/action|Répertorie les informations d’identification de connexion hello pour le Registre de conteneur spécifié hello.|
|/registries/regenerateCredential/action|Régénère les informations d’identification de connexion hello pour le Registre de conteneur spécifié hello.|

## <a name="microsoftcontainerservice"></a>Microsoft.ContainerService

| Opération | Description |
|---|---|
|/containerServices/subscriptions/read|Get hello Services de conteneur spécifiés en fonction de l’abonnement|
|/containerServices/resourceGroups/read|Get hello Services de conteneur spécifiés selon le groupe de ressources|
|/containerServices/resourceGroups/ContainerServiceName/read|Obtient hello spécifié le Service de conteneur|
|/containerServices/resourceGroups/ContainerServiceName/write|Met ou hello de mises à jour de Service de conteneur spécifié|
|/containerServices/resourceGroups/ContainerServiceName/delete|Suppressions hello spécifié le Service de conteneur|

## <a name="microsoftcontentmoderator"></a>Microsoft.ContentModerator

| Opération | Description |
|---|---|
|/updateCommunicationPreference/action|Mettre à jour les préférences de communication|
|/listCommunicationPreference/action|Répertorier les préférences de communication|
|/applications/read|Opération de lecture|
|/applications/write|Opération d’écriture|
|/applications/write|Opération d’écriture|
|/applications/delete|Opération de suppression|
|/applications/listSecrets/action|Afficher la liste des clés secrètes|
|/applications/listSingleSignOnToken/action|Afficher les jetons d’authentification unique|
|/operations/read|opérations de lecture|

## <a name="microsoftcustomerinsights"></a>Microsoft.CustomerInsights

| Opération | Description |
|---|---|
|/hubs/read|Afficher un concentrateur Azure Customer Insights|
|/hubs/write|Créer ou mettre à jour un concentrateur Azure Customer Insights|
|/hubs/delete|Supprimer un concentrateur Azure Customer Insights|
|/hubs/providers/Microsoft.Insights/metricDefinitions/read|Obtient les métriques disponibles hello pour la ressource|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/read|Obtient le paramètre de diagnostic hello pour la ressource de hello|
|/hubs/providers/Microsoft.Insights/diagnosticSettings/write|Crée ou met à jour le paramètre de diagnostic hello pour la ressource de hello|
|/hubs/providers/Microsoft.Insights/logDefinitions/read|Obtient les journaux disponibles hello pour la ressource|
|/hubs/authorizationPolicies/read|Afficher une stratégie de signature d’accès partagé Azure Customer Insights|
|/hubs/authorizationPolicies/write|Créer ou mettre à jour une stratégie de signature d’accès partagé Azure Customer Insights|
|/hubs/authorizationPolicies/delete|Supprimer une stratégie de signature d’accès partagé Azure Customer Insights|
|/hubs/authorizationPolicies/regeneratePrimaryKey/action|Régénérer la clé primaire d’une stratégie de signature d’accès partagé Azure Customer Insights|
|/hubs/authorizationPolicies/regenerateSecondaryKey/action|Régénérer la clé secondaire d’une stratégie de signature d’accès partagé Azure Customer Insights|
|/hubs/profiles/read|Afficher un profil Azure Customer Insights|
|/hubs/profiles/write|Écrire un profil Azure Customer Insights|
|/hubs/kpi/read|Afficher un indicateur de performance clé Azure Customer Insights|
|/hubs/kpi/write|Créer ou mettre à jour un indicateur de performance clé Azure Customer Insights|
|/hubs/kpi/delete|Supprimer un indicateur de performance clé Azure Customer Insights|
|/hubs/views/read|Afficher une vue d’application Azure Customer Insights|
|/hubs/views/write|Créer ou mettre à jour une vue d’application Azure Customer Insights|
|/hubs/views/delete|Supprimer une vue d’application Azure Customer Insights|
|/hubs/interactions/read|Afficher une interaction Azure Customer Insights|
|/hubs/interactions/write|Créer ou mettre à jour une interaction Azure Customer Insights|
|/hubs/roleAssignments/read|Afficher une affectation RBAC Azure Customer Insights|
|/hubs/roleAssignments/write|Créer ou mettre à jour une affectation RBAC Azure Customer Insights|
|/hubs/roleAssignments/delete|Supprimer une affectation RBAC Azure Customer Insights|
|/hubs/connectors/read|Afficher un connecteur Azure Customer Insights|
|/hubs/connectors/write|Créer ou mettre à jour un connecteur Azure Customer Insights|
|/hubs/connectors/delete|Supprimer un connecteur Azure Customer Insights|
|/hubs/connectors/mappings/read|Afficher un mappage de connecteur Azure Customer Insights|
|/hubs/connectors/mappings/write|Créer ou mettre à jour un mappage de connecteur Azure Customer Insights|
|/hubs/connectors/mappings/delete|Supprimer un mappage de connecteur Azure Customer Insights|

## <a name="microsoftdatacatalog"></a>Microsoft.DataCatalog

| Opération | Description |
|---|---|
|/checkNameAvailability/action|Vérifie la disponibilité du nom de catalogue pour le locataire.|
|/catalogs/read|Affiche les propriétés du ou des catalogues associés à l’abonnement ou au groupe de ressources.|
|/catalogs/write|Crée des balises hello catalogue ou de mises à jour et les propriétés de catalogue de hello.|
|/catalogs/delete|Supprime le catalogue de hello.|

## <a name="microsoftdatafactory"></a>Microsoft.DataFactory

| Opération | Description |
|---|---|
|/datafactories/read|Affiche la fabrique de données.|
|/datafactories/write|Crée ou met à jour la fabrique de données.|
|/datafactories/delete|Supprime la fabrique de données.|
|/datafactories/datapipelines/read|Affiche le pipeline.|
|/datafactories/datapipelines/delete|Supprime le pipeline.|
|/datafactories/datapipelines/pause/action|Suspend le pipeline.|
|/datafactories/datapipelines/resume/action|Rétablit le pipeline.|
|/datafactories/datapipelines/update/action|Met à jour le pipeline.|
|/datafactories/datapipelines/write|Crée ou met à jour un pipeline.|
|/datafactories/linkedServices/read|Affiche le service lié.|
|/datafactories/linkedServices/delete|Supprime le service lié.|
|/datafactories/linkedServices/write|Crée ou met à jour un service lié.|
|/datafactories/tables/read|Affiche la table.|
|/datafactories/tables/delete|Supprime la table.|
|/datafactories/tables/write|Crée ou met à jour la table.|

## <a name="microsoftdatalakeanalytics"></a>Microsoft.DataLakeAnalytics

| Opération | Description |
|---|---|
|/accounts/read|Obtenir des informations sur hello DataLakeAnalytics compte.|
|/accounts/write|Créer ou mettre à jour hello DataLakeAnalytics compte.|
|/accounts/delete|Supprimer un compte DataLakeAnalytics hello.|
|/accounts/firewallRules/read|Obtenir des informations sur une règle de pare-feu.|
|/accounts/firewallRules/write|Créer ou mettre à jour une règle de pare-feu.|
|/accounts/firewallRules/delete|Supprimer une règle de pare-feu.|
|/accounts/storageAccounts/read|Obtenir le compte de stockage lié pour hello DataLakeAnalytics compte.|
|/accounts/storageAccounts/write|Lier un toohello de compte de stockage DataLakeAnalytics compte.|
|/accounts/storageAccounts/delete|Dissocier un compte de stockage à partir de hello DataLakeAnalytics compte.|
|/accounts/storageAccounts/Containers/read|Obtenir les conteneurs sous hello compte de stockage|
|/accounts/storageAccounts/Containers/listSasTokens/action|Liste des jetons SAP hello conteneur de stockage|
|/accounts/dataLakeStoreAccounts/read|Obtenir le compte DataLakeStore lié pour hello DataLakeAnalytics compte.|
|/accounts/dataLakeStoreAccounts/write|Lier un toohello de compte DataLakeStore DataLakeAnalytics compte.|
|/accounts/dataLakeStoreAccounts/delete|Dissocier un compte DataLakeStore hello DataLakeAnalytics compte.|

## <a name="microsoftdatalakestore"></a>Microsoft.DataLakeStore

| Opération | Description |
|---|---|
|/accounts/read|Obtenir des informations sur un compte Data Lake Store existant.|
|/accounts/write|Créer un nouveau compte Data Lake Store ou mettre à jour un compte Data Lake Store existant.|
|/accounts/delete|Supprimer un compte Data Lake Store existant.|
|/accounts/firewallRules/read|Obtenir des informations sur une règle de pare-feu.|
|/accounts/firewallRules/write|Créer ou mettre à jour une règle de pare-feu.|
|/accounts/firewallRules/delete|Supprimer une règle de pare-feu.|
|/accounts/trustedIdProviders/read|Obtenir des informations sur un fournisseur d’identité approuvé.|
|/accounts/trustedIdProviders/write|Créer ou mettre à jour un fournisseur d’identité approuvé.|
|/accounts/trustedIdProviders/delete|Supprimer un fournisseur d’identité approuvé.|

## <a name="microsoftdevices"></a>Microsoft.Devices

| Opération | Description |
|---|---|
|/register/action|Inscription de l’abonnement hello pour hello IotHub ressource fournisseur et vous permet d’hello la création de ressources de IotHub|
|/checkNameAvailability/Action|Vérifier que le nom IotHub est disponible|
|/usages/Read|Obtenir des informations sur l’utilisation de l’abonnement pour ce fournisseur|
|/operations/Read|Afficher toutes les opérations du fournisseur de ressources|
|/iotHubs/Read|Obtient la ressource (s) de hello IotHub|
|/iotHubs/Write|Créer ou mettre à jour une ressource IotHub|
|/iotHubs/Delete|Supprimer une ressource IotHub|
|/iotHubs/listkeys/Action|Obtenir toutes les clés IotHub|
|/iotHubs/exportDevices/Action|Exporter des appareils|
|/iotHubs/importDevices/Action|Importer des appareils|
|/IotHubs/metricDefinitions/read|Obtient les métriques disponibles hello pour hello IotHub service|
|/iotHubs/iotHubKeys/listkeys/Action|Obtenir IotHub Key pour le nom donné de hello|
|/iotHubs/iotHubStats/Read|Afficher les statistiques IotHub|
|/iotHubs/quotaMetrics/Read|Obtenir les mesures de quota|
|/iotHubs/eventHubEndpoints/consumerGroups/Write|Créer un groupe de consommateurs EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Read|Afficher les groupes de consommateurs EventHub|
|/iotHubs/eventHubEndpoints/consumerGroups/Delete|Supprimer le groupe de consommateurs EventHub|
|/iotHubs/routing/routes/$testall/Action|Tester un message sur l’ensemble des itinéraires existants|
|/iotHubs/routing/routes/$testnew/Action|Tester un message sur un itinéraire test fourni|
|/IotHubs/diagnosticSettings/read|Obtient le paramètre de diagnostic hello pour la ressource de hello|
|/IotHubs/diagnosticSettings/write|Crée ou met à jour le paramètre de diagnostic hello pour la ressource de hello|
|/iotHubs/skus/Read|Afficher les références IotHub valides|
|/iotHubs/jobs/Read|Obtenir des informations sur les travaux soumis à un concentrateur IotHub donné|
|/iotHubs/routingEndpointsHealth/Read|Obtient le contrôle d’intégrité hello de tous les points de terminaison de routage pour un IotHub|

## <a name="microsoftdevtestlab"></a>Microsoft.DevTestLab

| Opération | Description |
|---|---|
|/Subscription/register/action|Abonnement hello de registres|
|/labs/delete|Supprimer des laboratoires.|
|/labs/read|Afficher des laboratoires.|
|/labs/write|Ajouter ou modifier des laboratoires.|
|/labs/ListVhds/action|Répertorier les images de disque disponibles pour la création d’images personnalisées.|
|/labs/GenerateUploadUri/action|Générer un URI pour le téléchargement d’images de disque personnalisé tooa Lab.|
|/labs/CreateEnvironment/action|Créer des machines virtuelles dans un laboratoire.|
|/labs/ClaimAnyVm/action|Machine virtuelle qui peuvent être réclamée aléatoire dans le laboratoire de hello de revendication.|
|/labs/ExportResourceUsage/action|Exportations hello l’utilisation des ressources lab dans un compte de stockage|
|/labs/users/delete|Supprimer des profils utilisateur.|
|/labs/users/read|Afficher les profils utilisateur.|
|/labs/users/write|Ajouter ou modifier des profils utilisateur.|
|/labs/users/secrets/delete|Supprimer des clés secrètes.|
|/labs/users/secrets/read|Afficher les clés secrètes.|
|/labs/users/secrets/write|Ajouter ou modifier des clés secrètes.|
|/labs/users/environments/delete|Supprimer des environnements.|
|/labs/users/environments/read|Afficher les environnements.|
|/labs/users/environments/write|Ajouter ou modifier des environnements.|
|/labs/users/disks/delete|Supprimer des disques.|
|/labs/users/disks/delete|Afficher les disques.|
|/labs/users/disks/write|Ajouter ou modifier des disques.|
|/labs/users/disks/Attach/action|Attacher et créer de bail hello de machine virtuelle de hello disque toohello.|
|/labs/users/disks/Detach/action|Détacher et bail hello de saut de disque de hello attaché toohello virtual machine.|
|/labs/customImages/delete|Supprimer des images personnalisées.|
|/labs/customImages/read|Lire des images personnalisées.|
|/labs/customImages/write|Ajouter ou modifier des images personnalisées.|
|/labs/serviceRunners/delete|Supprimer des exécuteurs de service.|
|/labs/serviceRunners/read|Lire des exécuteurs de service.|
|/labs/serviceRunners/write|Ajouter ou modifier des exécuteurs de service.|
|/labs/artifactSources/delete|Supprimer des sources d’artefact.|
|/labs/artifactSources/read|Lire des sources d’artefact.|
|/labs/artifactSources/write|Ajouter ou modifier des sources d’artefact.|
|/labs/artifactSources/artifacts/read|Lire des artefacts.|
|/labs/artifactSources/artifacts/GenerateArmTemplate/action|Génère un modèle ARM pour hello donné d’artefact, télécharge le compte de stockage hello requis fichiers tooa et valide l’artefact de hello généré.|
|/labs/artifactSources/armTemplates/read|Lire les modèles Azure Resource Manager.|
|/labs/costs/read|Lire les coûts.|
|/labs/costs/write|Ajouter ou modifier les coûts.|
|/labs/virtualNetworks/delete|Supprimer des réseaux virtuels.|
|/labs/virtualNetworks/read|Lire les réseaux virtuels.|
|/labs/virtualNetworks/write|Ajouter ou modifier des réseaux virtuels.|
|/labs/formulas/delete|Supprimer des formules.|
|/labs/formulas/read|Lire des formules.|
|/labs/formulas/write|Ajouter ou modifier des formules.|
|/labs/schedules/delete|Supprimer des planifications.|
|/labs/schedules/read|Lire les planifications.|
|/labs/schedules/write|Ajouter ou modifier des planifications.|
|/labs/schedules/Execute/action|Exécuter une planification.|
|/labs/schedules/ListApplicable/action|Répertorier toutes les planifications applicables.|
|/labs/galleryImages/read|Lire des images de la galerie.|
|/labs/policySets/EvaluatePolicies/action|Évaluer la stratégie de laboratoire.|
|/labs/policySets/policies/delete|Supprimer des stratégies.|
|/labs/policySets/policies/read|Lire les stratégies.|
|/labs/policySets/policies/write|Ajouter ou modifier des stratégies.|
|/labs/virtualMachines/delete|Supprimer des machines virtuelles.|
|/labs/virtualMachines/read|Lire les machines virtuelles.|
|/labs/virtualMachines/write|Ajouter ou modifier des machines virtuelles.|
|/labs/virtualMachines/Start/action|Démarrer une machine virtuelle.|
|/labs/virtualMachines/Stop/action|Arrêt d’une machine virtuelle|
|/labs/virtualMachines/ApplyArtifacts/action|Appliquer la machine de toovirtual d’artefacts.|
|/labs/virtualMachines/AddDataDisk/action|Joindre un ordinateur de toovirtual de disque de données nouvelle ou existante.|
|/labs/virtualMachines/DetachDataDisk/action|Détacher un disque spécifié de hello à partir de l’ordinateur virtuel de hello.|
|/labs/virtualMachines/Claim/action|Prendre possession d’une machine virtuelle existante.|
|/labs/virtualMachines/ListApplicableSchedules/action|Répertorier toutes les planifications applicables.|
|/labs/virtualMachines/schedules/delete|Supprimer des planifications.|
|/labs/virtualMachines/schedules/read|Lire les planifications.|
|/labs/virtualMachines/schedules/write|Ajouter ou modifier des planifications.|
|/labs/virtualMachines/schedules/Execute/action|Exécuter une planification.|
|/labs/notificationChannels/delete|Supprimer des canaux de notification.|
|/labs/notificationChannels/read|Lire les canaux de notification.|
|/labs/notificationChannels/write|Ajouter ou modifier des canaux de notification.|
|/labs/notificationChannels/Notify/action|Canal de notification tooprovided d’envoi.|
|/schedules/delete|Supprimer des planifications.|
|/schedules/read|Lire les planifications.|
|/schedules/write|Ajouter ou modifier des planifications.|
|/schedules/Execute/action|Exécuter une planification.|
|/schedules/Retarget/action|Mettre à jour l’ID de ressource cible d’une planification.|
|/locations/operations/read|Opérations de lecture.|

## <a name="microsoftdocumentdb"></a>Microsoft.DocumentDB

| Opération | Description |
|---|---|
|/databaseAccountNames/read|Vérifier la disponibilité du nom.|
|/databaseAccounts/read|Lire un compte de base de données.|
|/databaseAccounts/write|Mettre à jour les comptes de base de données.|
|/databaseAccounts/listKeys/action|Répertorier les clés d’un compte de base de données.|
|/databaseAccounts/regenerateKey/action|Régénérer les clés d’un compte de base de données.|
|/databaseAccounts/listConnectionStrings/action|Obtenir les chaînes de connexion hello d’un compte de base de données|
|/databaseAccounts/changeResourceGroup/action|Modifier le groupe de ressources d’un compte de base de données.|
|/databaseAccounts/failoverPriorityChange/action|Modifier les priorités de basculement des régions pour un compte de base de données. Il s’agit d’opération de basculement manuel tooperform utilisé|
|/databaseAccounts/delete|Supprime les comptes de base de données hello.|
|/databaseAccounts/metricDefinitions/read|Lit le compte de base de données hello définitions de métriques.|
|/databaseAccounts/metrics/read|Lit les métriques de compte de base de données hello.|
|/databaseAccounts/usages/read|Lit les utilisations de compte de base de données hello.|
|/databaseAccounts/databases/collections/metricDefinitions/read|Lit les définitions de métrique collection de hello.|
|/databaseAccounts/databases/collections/metrics/read|Lit les métriques de collection hello.|
|/databaseAccounts/databases/collections/usages/read|Lit les utilisations de collection hello.|
|/databaseAccounts/databases/metricDefinitions/read|Lit les définitions de métrique hello de base de données|
|/databaseAccounts/databases/metrics/read|Lit les métriques de base de données hello.|
|/databaseAccounts/databases/usages/read|Lit les utilisations de base de données hello.|
|/databaseAccounts/readonlykeys/read|Lit le compte de base de données hello les clés en lecture seule.|

## <a name="microsoftdomainregistration"></a>Microsoft.DomainRegistration

| Opération | Description |
|---|---|
|/generateSsoRequest/Action|Générer une demande de connexion au centre de contrôle du domaine.|
|/validateDomainRegistrationInformation/Action|Valider l’objet d’achat de domaine sans le soumettre.|
|/checkDomainAvailability/Action|Vérifier si un domaine est disponible à l’achat.|
|/listDomainRecommendations/Action|Récupérer les recommandations de domaine de liste hello basées sur les mots clés|
|/register/action|Inscrire le fournisseur de ressources Domains Microsoft hello pour l’abonnement de hello|
|/domains/Read|Obtenir la liste de hello de domaines|
|/domains/Write|Ajouter ou mettre à jour un domaine.|
|/domains/Delete|Supprimer un domaine existant.|
|/domains/operationresults/Read|Obtenir une opération de domaine.|

## <a name="microsoftdynamicslcs"></a>Microsoft.DynamicsLcs

| Opération | Description |
|---|---|
|/lcsprojects/read|Afficher les projets de Services de cycle de vie Microsoft Dynamics appartenant tooa utilisateur|
|/lcsprojects/write|Créer et mettre à jour des projets de Services de cycle de vie Microsoft Dynamics appartenant toohello utilisateur. Uniquement hello nom et une description des propriétés peuvent être mis à jour. abonnement de Hello et l’emplacement associé hello projet ne peut pas être mis à jour après la création|
|/lcsprojects/delete|Supprimer des projets de Services de cycle de vie Microsoft Dynamics appartiennent toohello utilisateur|
|/lcsprojects/clouddeployments/read|Afficher les déploiements d’évaluation de Microsoft Dynamics AX 2012 R3 dans un projet de Services de cycle de vie Microsoft Dynamics appartenant tooa utilisateur|
|/lcsprojects/clouddeployments/write|Créer le déploiement de l’évaluation de Microsoft Dynamics AX 2012 R3 dans un projet de Services de cycle de vie Microsoft Dynamics appartenant tooa utilisateur. Les déploiements peuvent être gérés depuis le portail de gestion Azure.|
|/lcsprojects/connectors/read|Lire des connecteurs qui font partie du projet de Services de cycle de vie Microsoft Dynamics tooa|
|/lcsprojects/connectors/write|Créer et mettre à jour des connecteurs qui font partie du projet de Services de cycle de vie Microsoft Dynamics tooa|

## <a name="microsofteventhub"></a>Microsoft.EventHub

| Opération | Description |
|---|---|
|/checkNameAvailability/action|Vérifier la disponibilité d’un espace de noms sous un abonnement donné|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources EventHub hello et permet la création de hello des ressources EventHub|
|/namespaces/write|Créer une ressource Namespace et mettre à jour ses propriétés. Balises et l’état de hello Namespace sont des propriétés de hello qui peuvent être mis à jour.|
|/namespaces/read|Obtenir la liste de hello de Description de la ressource Namespace|
|/namespaces/Delete|Supprimer une ressource Namespace|
|/namespaces/metricDefinitions/read|Obtenir la liste des descriptions de mesures des ressources Namespace|
|/namespaces/authorizationRules/read|Obtenir la liste de hello de description des espaces de noms des règles d’autorisation.|
|/namespaces/authorizationRules/write|Créer des règles d’autorisation au niveau d’une ressource Namespace et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/namespaces/authorizationRules/delete|Supprimer une règle d’autorisation de ressource Namespace. Hello règle d’autorisation de Namespace par défaut ne peut pas être supprimé. |
|/namespaces/authorizationRules/listkeys/action|Obtenir la chaîne de connexion de hello toohello Namespace|
|/namespaces/authorizationRules/regenerateKeys/action|Régénérer hello Primary ou Secondary clé toohello ressource|
|/namespaces/eventhubs/write|Créer ou mettre à jour des propriétés EventHub|
|/namespaces/eventhubs/read|Obtenir la liste des descriptions de ressources EventHub|
|/namespaces/eventhubs/Delete|Opération toodelete ressources EventHub|
|/namespaces/eventHubs/consumergroups/write|Créer ou mettre à jour les propriétés d’un groupe de consommateurs|
|/namespaces/eventHubs/consumergroups/read|Obtenir la liste des descriptions de ressources du groupe de consommateurs|
|/namespaces/eventHubs/consumergroups/Delete|Opération toodelete le groupe de consommateurs ressource|
|/namespaces/eventhubs/authorizationRules/read| Obtenir la liste de hello des règles d’autorisation de EventHub|
|/namespaces/eventhubs/authorizationRules/write|Créer des règles d’autorisation EventHub et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/namespaces/eventhubs/authorizationRules/delete|Opération toodelete EventHub les règles d’autorisation|
|/namespaces/eventhubs/authorizationRules/listkeys/action|Obtenir tooEventHub de chaîne de connexion hello|
|/namespaces/eventhubs/authorizationRules/regenerateKeys/action|Régénérer hello Primary ou Secondary clé toohello ressource|
|/namespaces/diagnosticSettings/read|Obtenir la liste des descriptions des ressources des paramètres de diagnostics Namespace|
|/namespaces/diagnosticSettings/write|Obtenir la liste des descriptions des ressources des paramètres de diagnostics Namespace|
|/namespaces/logDefinitions/read|Obtenir la liste des descriptions des ressources des journaux Namespace|

## <a name="microsoftfeatures"></a>Microsoft.Features

| Opération | Description |
|---|---|
|/providers/features/read|Obtient la fonctionnalité hello d’un abonnement dans un fournisseur de ressources donné.|
|/providers/features/register/action|Enregistre la fonction hello pour un abonnement dans un fournisseur de ressources donné.|
|/features/read|Obtient les fonctionnalités hello d’un abonnement.|

## <a name="microsofthdinsight"></a>Microsoft.HDInsight

| Opération | Description |
|---|---|
|/clusters/write|Créer ou mettre à jour un cluster HDInsight|
|/clusters/read|Obtenir des informations sur un cluster HDInsight|
|/clusters/delete|Supprimer un cluster HDInsight|
|/clusters/changerdpsetting/action|Modifier le paramètre RDP du cluster HDInsight|
|/clusters/configurations/action|Mettre à jour la configuration du cluster HDInsight|
|/clusters/configurations/read|Afficher les configurations du cluster HDInsight|
|/clusters/roles/resize/action|Redimensionner un cluster HDInsight|
|/locations/capabilities/read|Afficher les fonctionnalités de l’abonnement|
|/locations/checkNameAvailability/read|Vérifier la disponibilité du nom|

## <a name="microsoftimportexport"></a>Microsoft.ImportExport

| Opération | Description |
|---|---|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources d’importation/exportation hello et permet la création de hello de travaux d’importation/exportation.|
|/jobs/write|Crée une tâche avec les paramètres spécifiés de hello ou mettre à jour les propriétés de hello ou les balises pour le travail spécifié de hello.|
|/jobs/read|Obtient les propriétés de hello de travail spécifié de hello ou retourne la liste hello des tâches.|
|/jobs/listBitLockerKeys/action|Obtient les clés BitLocker hello pour le travail spécifié de hello.|
|/jobs/delete|Supprime un travail existant.|
|/locations/read|Obtient les propriétés de hello pour hello emplacement ou retourne hello liste spécifiée des emplacements.|

## <a name="microsoftinsights"></a>Microsoft.Insights

| Opération | Description |
|---|---|
|/Register/Action|Inscription du fournisseur d’insights hello microsoft|
|/AlertRules/Write|Configuration de règle d’alerte de l’écriture tooan|
|/AlertRules/Delete|Supprimer une configuration de règle d’alerte|
|/AlertRules/Read|Lire une configuration de règle d’alerte|
|/AlertRules/Activated/Action|Règle d’alerte activée|
|/AlertRules/Resolved/Action|Règle d’alerte résolue|
|/AlertRules/Throttled/Action|Règle d’alerte limitée|
|/AlertRules/Incidents/Read|Lire une configuration d’incident de règle d’alerte|
|/MetricDefinitions/Read|Lire les définitions des mesures|
|/eventtypes/values/Read|Lire les valeurs de types d’événement de gestion|
|/eventtypes/digestevents/Read|Lire le résumé des types d’événement de gestion|
|/Metrics/Read|Lire des mesures|
|/LogProfiles/Write|Écriture de configuration de profil de journal tooa|
|/LogProfiles/Delete|Supprimer la configuration de profil de journal|
|/LogProfiles/Read|Lire les profils de journal|
|/AutoscaleSettings/Write|L’écriture de configuration des paramètres de mise à l’échelle tooan|
|/AutoscaleSettings/Delete|Supprimer une configuration de mise à l’échelle|
|/AutoscaleSettings/Read|Lire une configuration de mise à l’échelle|
|/AutoscaleSettings/Scaleup/Action|Effectuer une opération de montée en puissance|
|/AutoscaleSettings/Scaledown/Action|Effectuer une opération de descente en puissance|
|/AutoscaleSettings/providers/Microsoft.Insights/MetricDefinitions/Read|Lire les définitions des mesures|
|/ActivityLogAlerts/Activated/Action|Hello déclenché l’alerte de journal d’activité|
|/DiagnosticSettings/Write|Configuration des paramètres d’écriture toodiagnostic|
|/DiagnosticSettings/Delete|Supprimer la configuration de diagnostic|
|/DiagnosticSettings/Read|Lire la configuration de diagnostic|
|/LogDefinitions/Read|Lire les définitions de journal|
|/ExtendedDiagnosticSettings/Write|Configuration de paramètres de diagnostic de l’écriture tooextended|
|/ExtendedDiagnosticSettings/Delete|Supprimer la configuration de diagnostic étendue|
|/ExtendedDiagnosticSettings/Read|Lire une configuration de diagnostic étendue|

## <a name="microsoftkeyvault"></a>Microsoft.KeyVault

| Opération | Description |
|---|---|
|/register/action|Enregistrer un abonnement|
|/checkNameAvailability/read|Vérifier que le nom du coffre Key Vault est valide et qu’il n’est pas déjà utilisé|
|/vaults/read|Afficher les propriétés d’un coffre de clés hello|
|/vaults/write|Créer une nouvelle clé hello coffre ou mise à jour des propriétés d’un coffre de clés existant|
|/vaults/delete|Supprimer un coffre Key Vault|
|/vaults/deploy/action|Active des toosecrets dans un coffre de clés d’accès lors du déploiement de ressources Azure|
|/vaults/secrets/read|Afficher les propriétés d’une clé secrète, mais pas sa valeur hello|
|/vaults/secrets/write|Créez une clé secrète ou mise à jour hello valeur d’une clé secrète existante|
|/vaults/accessPolicies/write|Mettre à jour une stratégie d’accès existant par la fusion ou de remplacement, ou ajouter un nouvel archivage tooa de stratégie des accès.|
|/deletedVaults/read|Afficher les propriétés de hello de coffres de clé logicielles supprimées|
|/locations/operationResults/read|Résultat de hello la vérification d’une opération à long terme|
|/locations/deletedVaults/read|Afficher les propriétés d’un coffre de clés supprimée logicielle hello|
|/locations/deletedVaults/purge/action|Vider un coffre Key Vault supprimé de manière réversible|

## <a name="microsoftlogic"></a>Microsoft.Logic

| Opération | Description |
|---|---|
|/workflows/read|Lit un flux de travail hello.|
|/workflows/write|Crée ou met à jour le flux de travail hello.|
|/workflows/delete|Supprime le flux de travail hello.|
|/workflows/run/action|Début d’une exécution du flux de travail hello.|
|/workflows/disable/action|Désactive le flux de travail hello.|
|/workflows/enable/action|Active le flux de travail hello.|
|/workflows/validate/action|Valide le flux de travail hello.|
|/workflows/move/action|Déplace le flux de travail à partir de son id d’abonnement, le groupe de ressources et/ou id d’abonnement différent nom tooa, groupe de ressources existant, et/ou le nom.|
|/workflows/listSwagger/action|Obtient le flux de travail hello swagger définitions.|
|/workflows/regenerateAccessKey/action|Régénère les secrets de clé accès hello.|
|/workflows/listCallbackUrl/action|Obtient l’URL de rappel hello pour les flux de travail.|
|/workflows/versions/read|Lit la version de flux de travail hello.|
|/workflows/versions/triggers/listCallbackUrl/action|Obtient l’URL de rappel hello pour le déclencheur.|
|/workflows/runs/read|Lit un flux de travail hello exécuter.|
|/workflows/runs/cancel/action|Annule l’exécution de hello d’un flux de travail.|
|/workflows/runs/actions/read|Lit le flux de travail hello exécuter l’action.|
|/workflows/runs/operations/read|Lit le flux de travail hello exécuter l’état de l’opération.|
|/workflows/triggers/read|Lit le déclencheur de hello.|
|/workflows/triggers/run/action|Exécute un déclencheur de hello.|
|/workflows/triggers/listCallbackUrl/action|Obtient l’URL de rappel hello pour le déclencheur.|
|/workflows/triggers/histories/read|Lit les historiques de déclencheur hello.|
|/workflows/triggers/histories/resubmit/action|Soumet à nouveau déclencheur du flux de travail hello.|
|/workflows/accessKeys/read|Lit la clé d’accès hello.|
|/workflows/accessKeys/write|Crée ou met à jour la clé d’accès hello.|
|/workflows/accessKeys/delete|Supprime la clé d’accès hello.|
|/workflows/accessKeys/list/action|Répertorie les secrets de clé accès hello.|
|/workflows/accessKeys/regenerate/action|Régénère les secrets de clé accès hello.|
|/locations/workflows/validate/action|Valide le flux de travail hello.|

## <a name="microsoftmachinelearning"></a>Microsoft.MachineLearning

| Opération | Description |
|---|---|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources de service web d’apprentissage hello et permet la création de hello de services web.|
|/webServices/action|Créer des propriétés régionales de service web pour les régions prises en charge|
|/commitmentPlans/read|Lire un plan d’engagement Machine Learning|
|/commitmentPlans/write|Créer ou mettre à jour un plan d’engagement Machine Learning|
|/commitmentPlans/delete|Supprimer un plan d’engagement Machine Learning|
|/commitmentPlans/join/action|Rejoindre un plan d’engagement Machine Learning|
|/commitmentPlans/commitmentAssociations/read|Lire une association de plans d’engagement Machine Learning|
|/commitmentPlans/commitmentAssociations/move/action|Déplacer une association de plans d’engagement Machine Learning|
|/Workspaces/read|Afficher un espace de travail Machine Learning|
|/Workspaces/write|Créer ou mettre à jour un espace de travail Machine Learning|
|/Workspaces/delete|Supprimer un espace de travail Machine Learning|
|/Workspaces/listworkspacekeys/action|Répertorier les clés d’un espace de travail Machine Learning|
|/Workspaces/resyncstoragekeys/action|Resynchroniser les clés d’un compte de stockage configuré pour un espace de travail Machine Learning|
|/webServices/read|Afficher un service web Machine Learning|
|/webServices/write|Créer ou mettre à jour un service web Machine Learning|
|/webServices/delete|Supprimer un service web Machine Learning|

## <a name="microsoftmarketplaceordering"></a>Microsoft.MarketplaceOrdering

| Opération | Description |
|---|---|
|/agreements/offers/plans/read|Renvoyer un contrat pour un élément de place de marché donné|
|/agreements/offers/plans/sign/action|Signer un contrat pour un élément de place de marché donné|
|/agreements/offers/plans/cancel/action|Annuler un contrat pour un élément de place de marché donné|

## <a name="microsoftmedia"></a>Microsoft.Media

| Opération | Description |
|---|---|
|/mediaservices/read||
|/mediaservices/write||
|/mediaservices/delete||
|/mediaservices/regenerateKey/action||
|/mediaservices/listKeys/action||
|/mediaservices/syncStorageKeys/action||

## <a name="microsoftnetwork"></a>Microsoft.Network

| Opération | Description |
|---|---|
|/register/action|Abonnement hello de registres|
|/unregister/action|Annule l’inscription d’abonnement de hello|
|/checkTrafficManagerNameAvailability/action|Vérifie la disponibilité de hello d’un nom DNS relatif de Traffic Manager.|
|/dnszones/read|Obtenir la zone DNS hello, au format JSON. propriétés de la zone Hello incluent les balises, etag, numberOfRecordSets et maxNumberOfRecordSets. Notez que cette commande ne récupère pas les jeux d’enregistrements hello contenus dans la zone de hello.|
|/dnszones/write|Créer ou mettre à jour une zone DNS dans un groupe de ressources.  Balises de hello tooupdate utilisé sur une ressource de zone DNS. Notez que cette commande ne peut pas être utilisé toocreate ou mise à jour de jeux d’enregistrements dans la zone de hello.|
|/dnszones/delete|Supprimer la zone DNS hello, au format JSON. propriétés de la zone Hello incluent les balises, etag, numberOfRecordSets et maxNumberOfRecordSets.|
|/dnszones/MX/read|Obtenir le jeu d’enregistrements de type hello « MX », au format JSON. jeu d’enregistrements Hello contient une liste d’enregistrements, ainsi que des hello durée de vie, les balises et etag.|
|/dnszones/MX/write|Créer ou mettre à jour un jeu d’enregistrements de type « MX » dans une zone DNS. Hello spécifié remplacent les enregistrements en cours hello dans le jeu d’enregistrements hello.|
|/dnszones/MX/delete|Supprimer le jeu d’enregistrements hello d’un nom donné et de type « MX » dans une zone DNS.|
|/dnszones/NS/read|Obtenir le jeu d’enregistrements DNS de type NS|
|/dnszones/NS/write|Créer ou mettre à jour un jeu d’enregistrements DNS de type NS|
|/dnszones/NS/delete|Supprime le jeu d’enregistrements DNS hello de type NS|
|/dnszones/AAAA/read|Obtenir le jeu d’enregistrements de type hello « AAAA », au format JSON. jeu d’enregistrements Hello contient une liste d’enregistrements, ainsi que des hello durée de vie, les balises et etag.|
|/dnszones/AAAA/write|Créer ou mettre à jour un jeu d’enregistrements de type « AAAA » dans une zone DNS. Hello spécifié remplacent les enregistrements en cours hello dans le jeu d’enregistrements hello.|
|/dnszones/AAAA/delete|Supprimer le jeu d’enregistrements hello d’un nom donné et de type « AAAA » dans une zone DNS.|
|/dnszones/CNAME/read|Obtenir le jeu d’enregistrements hello de type « CNAME », au format JSON. jeu d’enregistrements Hello contient hello durée de vie, les balises et etag.|
|/dnszones/CNAME/write|Créer ou mettre à jour un jeu d’enregistrements de type « CNAME » dans une zone DNS. Hello spécifié remplacent les enregistrements en cours hello dans le jeu d’enregistrements hello.|
|/dnszones/CNAME/delete|Supprimer le jeu d’enregistrements hello d’un nom donné et de type « CNAME » dans une zone DNS.|
|/dnszones/SOA/read|Obtenir le jeu d’enregistrements DNS de type SOA|
|/dnszones/SOA/write|Créer ou mettre à jour un jeu d’enregistrements DNS de type SOA|
|/dnszones/SRV/read|Obtenir le jeu d’enregistrements de type hello « SRV », au format JSON. jeu d’enregistrements Hello contient une liste d’enregistrements, ainsi que des hello durée de vie, les balises et etag.|
|/dnszones/SRV/write|Créer ou mettre à jour un jeu d’enregistrements de type SRV|
|/dnszones/SRV/delete|Supprimer le jeu d’enregistrements hello d’un nom donné et de type « SRV » dans une zone DNS.|
|/dnszones/PTR/read|Obtenir le jeu d’enregistrements de type hello « PTR », au format JSON. jeu d’enregistrements Hello contient une liste d’enregistrements, ainsi que des hello durée de vie, les balises et etag.|
|/dnszones/PTR/write|Créer ou mettre à jour un jeu d’enregistrements de type « PTR » dans une zone DNS. Hello spécifié remplacent les enregistrements en cours hello dans le jeu d’enregistrements hello.|
|/dnszones/PTR/delete|Supprimer le jeu d’enregistrements hello d’un nom donné et de type « PTR » dans une zone DNS.|
|/dnszones/A/read|Obtenir le jeu d’enregistrements de type 'A', hello au format JSON. jeu d’enregistrements Hello contient une liste d’enregistrements, ainsi que des hello durée de vie, les balises et etag.|
|/dnszones/A/write|Créer ou mettre à jour un jeu d’enregistrements de type « A » dans une zone DNS. Hello spécifié remplacent les enregistrements en cours hello dans le jeu d’enregistrements hello.|
|/dnszones/A/delete|Supprimer le jeu d’enregistrements hello d’un nom donné et de type « A » à partir d’une zone DNS.|
|/dnszones/TXT/read|Obtenir le jeu d’enregistrements de type hello « TXT », au format JSON. jeu d’enregistrements Hello contient une liste d’enregistrements, ainsi que des hello durée de vie, les balises et etag.|
|/dnszones/TXT/write|Créer ou mettre à jour un jeu d’enregistrements de type « TXT » dans une zone DNS. Hello spécifié remplacent les enregistrements en cours hello dans le jeu d’enregistrements hello.|
|/dnszones/TXT/delete|Supprimer le jeu d’enregistrements hello d’un nom donné et de type « TXT » dans une zone DNS.|
|/dnszones/recordsets/read|Obtient les jeux d’enregistrements DNS parmi les types.|
|/networkInterfaces/read|Obtient une définition d’interface réseau. |
|/networkInterfaces/write|Crée une interface réseau ou met à jour une interface réseau existante. |
|/networkInterfaces/join/action|Joint une interface de réseau de Machine virtuelle tooa|
|/networkInterfaces/delete|Supprime une interface réseau.|
|/networkInterfaces/effectiveRouteTable/action|Obtention de la Table de routage configuré sur l’Interface réseau de machine virtuelle de hello|
|/networkInterfaces/effectiveNetworkSecurityGroups/action|Obtenir hello sur Network Interface de configuré les groupes de sécurité réseau virtuelle|
|/networkInterfaces/loadBalancers/read|Obtient tous les équilibrages de charge hello hello interface réseau fait partie de|
|/networkInterfaces/ipconfigurations/read|Obtient une définition de la configuration de l’adresse IP de l’interface réseau. |
|/publicIPAddresses/read|Obtient une définition de l’adresse IP publique.|
|/publicIPAddresses/write|Crée une adresse IP publique ou met à jour une adresse IP publique existante. |
|/publicIPAddresses/delete|Supprime une adresse IP publique.|
|/publicIPAddresses/join/action|Joint une adresse IP publique.|
|/routeFilters/read|Obtient une définition de filtre de routage.|
|/routeFilters/join/action|Joint un filtre de routage.|
|/routeFilters/delete|Supprime une définition de filtre de routage.|
|/routeFilters/write|Crée un filtre de routage ou met à jour un filtre de routage existant.|
|/routeFilters/rules/read|Obtient une définition de règle de filtre de routage.|
|/routeFilters/rules/write|Crée une règle de filtre de routage ou met à jour une règle de filtre de routage existante.|
|/routeFilters/rules/delete|Supprime une définition de règle de filtre de routage.|
|/networkWatchers/read|Obtenir la définition de l’Observateur réseau hello|
|/networkWatchers/write|Crée un observateur de réseau ou met à jour un observateur de réseau existant.|
|/networkWatchers/delete|Supprime un observateur de réseau.|
|/networkWatchers/configureFlowLog/action|Configure la journalisation des flux pour une ressource cible.|
|/networkWatchers/ipFlowVerify/action|Retourne si les paquets hello sont autorisé ou refusé tooor à partir d’une destination particulière.|
|/networkWatchers/nextHop/action|Pour une cible spécifiée et l’adresse IP de destination, retourner le type de tronçon suivant hello et ensuite espérer que les adresses IP.|
|/networkWatchers/queryFlowLogStatus/action|Obtient l’état hello du flux de journalisation sur une ressource.|
|/networkWatchers/queryTroubleshootResult/action|Obtient les hello résultent hello précédemment exécutée ou en cours d’opération de résolution des problèmes de résolution des problèmes.|
|/networkWatchers/securityGroupView/action|Afficher hello configuré et les règles de groupe de sécurité réseau efficace appliquées sur un ordinateur virtuel.|
|/networkWatchers/topology/action|Obtient une vue au niveau du réseau des ressources et de leurs relations dans un groupe de ressources.|
|/networkWatchers/troubleshoot/action|Démarre la résolution des problèmes sur une ressource réseau dans Azure.|
|/networkWatchers/packetCaptures/queryStatus/action|Obtient des informations sur les propriétés et l’état d’une ressource de capture de paquets.|
|/networkWatchers/packetCaptures/stop/action|Arrêter hello session de capture de paquets en cours d’exécution.|
|/networkWatchers/packetCaptures/read|Obtenir la définition de capture de paquets hello|
|/networkWatchers/packetCaptures/write|Crée une capture de paquets.|
|/networkWatchers/packetCaptures/delete|Supprimer une capture de paquets.|
|/loadBalancers/read|Obtient une définition d’équilibrage de charge.|
|/loadBalancers/write|Crée un équilibrage de charge ou met à jour un équilibrage de charge existant.|
|/loadBalancers/delete|Supprime un équilibrage de charge.|
|/loadBalancers/networkInterfaces/read|Obtient les références d’interfaces de réseau tooall hello sous un équilibreur de charge|
|/loadBalancers/loadBalancingRules/read|Obtient une définition de règle d’équilibrage de charge.|
|/loadBalancers/backendAddressPools/read|Obtient une définition de pool d’adresses principales d’équilibrage de charge.|
|/loadBalancers/backendAddressPools/join/action|Joint un pool d’adresses principales d’équilibrage de charge.|
|/loadBalancers/inboundNatPools/read|Obtient une définition de pool NAT entrant d’équilibrage de charge.|
|/loadBalancers/inboundNatPools/join/action|Joint un pool NAT entrant d’équilibrage de charge.|
|/loadBalancers/inboundNatRules/read|Obtient une définition de règle NAT entrante d’équilibrage de charge.|
|/loadBalancers/inboundNatRules/write|Crée une règle NAT entrante d’équilibrage de charge ou met à jour une règle NAT entrante d’équilibrage de charge existante.|
|/loadBalancers/inboundNatRules/delete|Supprime une règle NAT entrante d’équilibrage de charge.|
|/loadBalancers/inboundNatRules/join/action|Joint une règle NAT entrante d’équilibrage de charge.|
|/loadBalancers/outboundNatRules/read|Obtient une définition de règle NAT sortante d’équilibrage de charge.|
|/loadBalancers/probes/read|Obtient une sonde d’équilibrage de charge.|
|/loadBalancers/virtualMachines/read|Obtient les références virtuels tooall hello sous un équilibreur de charge|
|/loadBalancers/frontendIPConfigurations/read|Obtient une définition de configuration d’adresse IP frontale d’équilibrage de charge.|
|/trafficManagerGeographicHierarchies/read|Obtient hello Traffic Manager géographique hiérarchie contenant des régions qui peuvent être utilisées avec hello méthode de routage du trafic géographiques|
|/bgpServiceCommunities/read|Obtenir les communautés de services BGP.|
|/applicationGatewayAvailableWafRuleSets/read|Obtient les ensembles de règles WAF disponibles pour Application Gateway.|
|/virtualNetworks/read|Obtenir la définition de réseau virtuel hello|
|/virtualNetworks/write|Crée un réseau virtuel ou met à jour un réseau virtuel existant.|
|/virtualNetworks/delete|Supprime un réseau virtuel.|
|/virtualNetworks/peer/action|Appaire un réseau virtuel avec un autre réseau virtuel.|
|/virtualNetworks/virtualNetworkPeerings/read|Obtient une définition d’homologation de réseau virtuel.|
|/virtualNetworks/virtualNetworkPeerings/write|Crée une homologation de réseau virtuel ou met à jour une homologation de réseau virtuel existante.|
|/virtualNetworks/virtualNetworkPeerings/delete|Supprime une homologation de réseau virtuel.|
|/virtualNetworks/subnets/read|Obtient une définition de sous-réseau de réseau virtuel.|
|/virtualNetworks/subnets/write|Crée un sous-réseau de réseau virtuel ou met à jour un sous-réseau de réseau virtuel existant.|
|/virtualNetworks/subnets/delete|Supprime un sous-réseau de réseau virtuel.|
|/virtualNetworks/subnets/join/action|Joint un réseau virtuel.|
|/virtualNetworks/subnets/joinViaServiceTunnel/action|Joint des ressources telles que le compte de stockage ou SQL sous-réseau Service charge le Tunneling de tooa de base de données.|
|/virtualNetworks/subnets/virtualMachines/read|Obtient les références tooall hello ordinateurs virtuels dans un sous-réseau de réseau virtuel|
|/virtualNetworks/checkIpAddressAvailability/read|Vérifiez si l’adresse Ip est disponible sur le réseau virtuel spécifié de hello|
|/virtualNetworks/virtualMachines/read|Obtient les références tooall hello ordinateurs virtuels dans un réseau virtuel|
|/expressRouteServiceProviders/read|Obtient les fournisseurs de services ExpressRoute.|
|/dnsoperationresults/read|Obtient les résultats d’une opération DNS.|
|/localnetworkgateways/read|Obtient une LocalNetworkGateway.|
|/localnetworkgateways/write|Crée une LocalNetworkGateway ou met à jour une LocalNetworkGateway existante.|
|/localnetworkgateways/delete|Supprime une LocalNetworkGateway.|
|/trafficManagerProfiles/read|Obtenir la configuration du profil Traffic Manager hello. Cela inclut les paramètres DNS, les paramètres de routage du trafic, les paramètres de surveillance de point de terminaison et liste hello de points de terminaison routés par ce profil Traffic Manager.|
|/trafficManagerProfiles/write|Créer un profil Traffic Manager, ou modifier la configuration de hello d’un profil Traffic Manager existant Cela inclut l’activation ou la désactivation d’un profil et la modification des paramètres DNS, des paramètres de routage du trafic ou des paramètres de surveillance des points de terminaison. Points de terminaison routés par le profil Traffic Manager hello peuvent être ajoutés, supprimés, activés ou désactivés.|
|/trafficManagerProfiles/delete|Supprimer le profil Traffic Manager hello. Tous les paramètres associés au profil Traffic Manager de hello sont perdues, et profil de hello ne peut plus être utilisé tooroute trafic.|
|/dnsoperationstatuses/read|Obtient l’état d’une opération DNS. |
|/operations/read|Obtenir les opérations disponibles.|
|/expressRouteCircuits/read|Obtenir un ExpressRouteCircuit.|
|/expressRouteCircuits/write|Crée un ExpressRouteCircuit ou met à jour un ExpressRouteCircuit existant.|
|/expressRouteCircuits/delete|Supprime un ExpressRouteCircuit.|
|/expressRouteCircuits/stats/read|Obtient les statistiques d’un ExpressRouteCircuit.|
|/expressRouteCircuits/peerings/read|Obtient une homologation ExpressRouteCircuit.|
|/expressRouteCircuits/peerings/write|Crée une homologation ExpressRouteCircuit ou met à jour une homologation ExpressRouteCircuit existante.|
|/expressRouteCircuits/peerings/delete|Supprime une homologation ExpressRouteCircuit.|
|/expressRouteCircuits/peerings/arpTables/action|Obtient une ArpTable d’homologation ExpressRouteCircuit.|
|/expressRouteCircuits/peerings/routeTables/action|Obtient une RouteTable d’homologation ExpressRouteCircuit.|
|/expressRouteCircuits/peerings/<br>routeTablesSummary/action|Obtient un résumé RouteTable d’homologation ExpressRouteCircuit.|
|/expressRouteCircuits/peerings/stats/read|Obtient les statistiques d’homologation d’un ExpressRouteCircuit.|
|/expressRouteCircuits/authorizations/read|Obtient une autorisation ExpressRouteCircuit.|
|/expressRouteCircuits/authorizations/write|Crée une autorisation ExpressRouteCircuit ou met à jour une autorisation ExpressRouteCircuit existante.|
|/expressRouteCircuits/authorizations/delete|Supprime une autorisation ExpressRouteCircuit.|
|/connections/read|Obtient une VirtualNetworkGatewayConnection.|
|/connections/write|Crée une VirtualNetworkGatewayConnection ou met à jour une VirtualNetworkGatewayConnection existante.|
|/connections/delete|Supprime une VirtualNetworkGatewayConnection.|
|/connections/sharedKey/read|Obtient une SharedKey VirtualNetworkGatewayConnection.|
|/connections/sharedKey/write|Crée une SharedKey VirtualNetworkGatewayConnection ou met à jour une SharedKey VirtualNetworkGatewayConnection existante.|
|/networkSecurityGroups/read|Obtient une définition de groupe de sécurité réseau.|
|/networkSecurityGroups/write|Crée un groupe de sécurité réseau ou met à jour un groupe de sécurité réseau existant.|
|/networkSecurityGroups/delete|Supprime un groupe de sécurité réseau.|
|/networkSecurityGroups/join/action|Joint un groupe de sécurité réseau.|
|/networkSecurityGroups/defaultSecurityRules/read|Obtient une définition de règle de sécurité par défaut.|
|/networkSecurityGroups/securityRules/read|Obtient une définition de règle de sécurité.|
|/networkSecurityGroups/securityRules/write|Crée une règle de sécurité ou met à jour une règle de sécurité existante.|
|/networkSecurityGroups/securityRules/delete|Supprime une règle de sécurité.|
|/applicationGateways/read|Obtient une passerelle d’application.|
|/applicationGateways/write|Crée une passerelle d’application ou met à jour une passerelle d’application.|
|/applicationGateways/delete|Supprime une passerelle d’application.|
|/applicationGateways/backendhealth/action|Obtient l’intégrité du serveur principal d’une passerelle d’application.|
|/applicationGateways/start/action|Démarre une passerelle d’application.|
|/applicationGateways/stop/action|Arrête une passerelle d’application.|
|/applicationGateways/backendAddressPools/join/action|Joint un pool d’adresses principales de passerelle d’application.|
|/routeTables/read|Obtient une définition de table de routage.|
|/routeTables/write|Crée une table de routage ou met à jour une table de routage existante.|
|/routeTables/delete|Supprime une définition de table de routage.|
|/routeTables/join/action|Joint une table de routage.|
|/routeTables/routes/read|Obtient une définition de routage.|
|/routeTables/routes/write|Crée un routage ou met à jour un routage existant.|
|/routeTables/routes/delete|Supprime une définition de routage.|
|/locations/operationResults/read|Obtient le résultat d’une opération DELETE ou POST asynchrone.|
|/locations/checkDnsNameAvailability/read|Vérifie si le nom dns est disponible à l’adresse hello l’emplacement spécifié|
|/locations/usages/read|Obtient des métriques d’utilisation des ressources de hello|
|/locations/operations/read|Obtient la ressource d’opération qui représente l’état d’une opération asynchrone.|

## <a name="microsoftnotificationhubs"></a>Microsoft.NotificationHubs

| Opération | Description |
|---|---|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources NotifciationHubs hello et permet la création de hello de Namespaces et NotificationHubs|
|/CheckNamespaceAvailability/action|Vérifie si un nom de ressource donné Namespace est disponible dans hello service NotificationHub.|
|/Namespaces/write|Créer une ressource Namespace et mettre à jour ses propriétés. Balises et l’état de hello Namespace sont des propriétés de hello qui peuvent être mis à jour.|
|/Namespaces/read|Obtenir la liste de hello de Description de la ressource Namespace|
|/Namespaces/Delete|Supprimer une ressource Namespace.|
|/Namespaces/authorizationRules/action|Obtenir la liste de hello de description des espaces de noms des règles d’autorisation.|
|/Namespaces/CheckNotificationHubAvailability/action|Vérifie si un nom de NotificationHub donné est disponible à l’intérieur d’une ressource Namespace.|
|/Namespaces/authorizationRules/write|Créer des règles d’autorisation au niveau d’une ressource Namespace et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/Namespaces/authorizationRules/read|Obtenir la liste de hello de description des espaces de noms des règles d’autorisation.|
|/Namespaces/authorizationRules/delete|Supprimer une règle d’autorisation de ressource Namespace. Hello règle d’autorisation de Namespace par défaut ne peut pas être supprimé. |
|/Namespaces/authorizationRules/listkeys/action|Obtenir la chaîne de connexion de hello toohello Namespace|
|/Namespaces/authorizationRules/regenerateKeys/action|Namespace d’autorisation règle régénérer principal/SecondaryKey, spécifiez hello clé qui doit toobe régénéré|
|/Namespaces/NotificationHubs/write|Créer un concentrateur de notification et mettre à jour ses propriétés. Ses propriétés incluent principalement des informations d’identification PNS. Durée de vie et règles d’autorisation|
|/Namespaces/NotificationHubs/read|Obtenir la liste des descriptions des ressources de concentrateur de notification.|
|/Namespaces/NotificationHubs/Delete|Supprimer une ressource de concentrateur de notification.|
|/Namespaces/NotificationHubs/authorizationRules/action|Obtenir la liste de hello des règles d’autorisation Notification Hub|
|/Namespaces/NotificationHubs/pnsCredentials/action|Obtenir toutes les informations d’identification PNS du concentrateur de notification. Cela inclut les informations d’identification WNS, MPNS, APNS, GCM et BAIDU.|
|/Namespaces/NotificationHubs/debugSend/action|Envoyer une notification Push de test.|
|/Namespaces/NotificationHubs/metricDefinitions/read|Obtenir la liste des descriptions des mesures de ressource Namespace.|
|/Namespaces/NotificationHubs/<br>authorizationRules/write|Créer des règles d’autorisation de concentrateur de notification et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/Namespaces/NotificationHubs/<br>authorizationRules/read|Obtenir la liste de hello des règles d’autorisation Notification Hub|
|/Namespaces/NotificationHubs/<br>authorizationRules/delete|Supprimer les règles d’autorisation de concentrateur de notification.|
|/Namespaces/NotificationHubs/<br>authorizationRules/listkeys/action|Obtenir la chaîne de connexion de hello toohello Hub de Notification|
|/Namespaces/NotificationHubs/<br>authorizationRules/regenerateKeys/action|Régénération de la notification Hub d’autorisation règle régénérer principal/SecondaryKey, spécifiez hello clé qui doit toobe|

## <a name="microsoftoperationalinsights"></a>Microsoft.OperationalInsights

| Opération | Description |
|---|---|
|/register/action|Inscrire un fournisseur de ressources tooa abonnement.|
|/linkTargets/read|Répertorie les comptes existants qui ne sont pas associés à un abonnement Azure. toolink cet espace de travail tooa abonnement Azure et l’utiliser un id de client retourné par cette opération dans la propriété d’id de client hello Hello opération de créer un espace de travail.|
|/workspaces/write|Crée un nouvel espace de travail ou d’un espace de travail de liens tooan existant en fournissant l’id du client à partir de l’espace de travail existant hello hello.|
|/workspaces/read|Obtient un espace de travail existant.|
|/workspaces/delete|Supprime un espace de travail. Si l’espace de travail hello a été lié tooan l’espace de travail existant au moment de la création puis hello qu’il a été lié toois ne pas supprimer un espace de travail.|
|/workspaces/generateregistrationcertificate/action|Génère le certificat d’inscription pour l’espace de travail hello. Ce certificat est utilisé tooconnect Microsoft System Center Operations Manager toohello espace de travail.|
|/workspaces/sharedKeys/action|Récupère les clés hello partagé pour l’espace de travail hello. Ces clés sont utilisées tooconnect Microsoft Operational Insights agents toohello espace de travail.|
|/workspaces/search/action|Exécute une requête de recherche.|
|/workspaces/datasources/read|Obtenir des sources de données sous un espace de travail.|
|/workspaces/datasources/write|Créer/mettre à jour des sources de données sous un espace de travail.|
|/workspaces/datasources/delete|Supprimer des sources de données sous un espace de travail.|
|/workspaces/managementGroups/read|Obtient les noms de hello et les métadonnées pour System Center Operations Manager management groupes connectés toothis espace de travail.|
|/workspaces/schema/read|Obtient le schéma de recherche hello pour l’espace de travail hello.  Schéma de recherche inclut les champs hello exposée et leurs types.|
|/workspaces/usages/read|Obtient les données d’utilisation pour un espace de travail, y compris la quantité hello des données lues par espace de travail hello.|
|/workspaces/intelligencepacks/read|Répertorie tous les packs d’analyse décisionnelle qui sont visibles pour un espace de travail donné et indique également si le pack de hello est activée ou désactivée pour cet espace de travail.|
|/workspaces/intelligencepacks/enable/action|Active un Intelligence Pack pour un espace de travail donné.|
|/workspaces/intelligencepacks/disable/action|Désactive un Intelligence Pack pour un espace de travail donné.|
|/workspaces/sharedKeys/read|Récupère les clés hello partagé pour l’espace de travail hello. Ces clés sont utilisées tooconnect Microsoft Operational Insights agents toohello espace de travail.|
|/workspaces/savedSearches/read|Obtient une requête de recherche enregistrée.|
|/workspaces/savedSearches/write|Crée une requête de recherche enregistrée.|
|/workspaces/savedSearches/delete|Supprime une requête de recherche enregistrée.|
|/workspaces/storageinsightconfigs/write|Crée une configuration de stockage. Ces configurations sont utilisées toopull des données à partir d’un emplacement dans un compte de stockage existant.|
|/workspaces/storageinsightconfigs/read|Obtient une configuration de stockage.|
|/workspaces/storageinsightconfigs/delete|Supprime une configuration de stockage. Cela arrêtera Microsoft Operational Insights à partir de la lecture des données à partir du compte de stockage hello.|
|/workspaces/configurationScopes/read|Obtenir l’étendue de la configuration.|
|/workspaces/configurationScopes/write|Définir l’étendue de la configuration.|
|/workspaces/configurationScopes/delete|Supprimer l’étendue de la configuration.|

## <a name="microsoftoperationsmanagement"></a>Microsoft.OperationsManagement

| Opération | Description |
|---|---|
|/register/action|Inscrire un fournisseur de ressources tooa abonnement.|
|/solutions/write|Créer une solution OMS.|
|/solutions/read|Obtenir la solution OMS existante.|
|/solutions/delete|Supprimer la solution OMS existante.|

## <a name="microsoftrecoveryservices"></a>Microsoft.RecoveryServices

| Opération | Description |
|---|---|
|/Vaults/backupJobsExport/action|Travaux d’exportation|
|/Vaults/write|L’opération de création de coffre entraîne la création d’une ressource Azure de type « coffre».|
|/Vaults/read|opération d’obtention d’un coffre de Hello Obtient un objet représentant hello ressource Azure de type 'coffre'|
|/Vaults/delete|ressource Azure de type 'coffre' spécifiée pour Hello suppression du coffre opération suppressions hello|
|/Vaults/refreshContainers/read|Actualise la liste de conteneurs hello|
|/Vaults/backupJobsExport/operationResults/read|Retourne hello résultat d’opération du travail exporter.|
|/Vaults/backupOperationResults/read|Renvoie le résultat de l’opération de sauvegarde pour le coffre Recovery Services.|
|/Vaults/monitoringAlerts/read|Obtient les alertes de hello de coffre hello Recovery services.|
|/Vaults/monitoringAlerts/{uniqueAlertId}/read|Obtient les détails de hello d’alerte de hello.|
|/Vaults/backupSecurityPIN/read|Renvoie les informations relatives au code PIN de sécurité pour le coffre Recovery Services.|
|/vaults/replicationEvents/read|Lire des événements.|
|/Vaults/backupProtectableItems/read|Renvoie la liste de tous les éléments pouvant être protégés.|
|/vaults/replicationFabrics/read|Lire des structures.|
|/vaults/replicationFabrics/write|Créer ou mettre à jour des structures.|
|/vaults/replicationFabrics/remove/action|Supprimer une structure.|
|/vaults/replicationFabrics/checkConsistency/action|Vérifications de cohérence hello Fabric|
|/vaults/replicationFabrics/delete|Supprimer des structures.|
|/vaults/replicationFabrics/renewcertificate/action||
|/vaults/replicationFabrics/deployProcessServerImage/action|Déployer une image de serveur de traitement.|
|/vaults/replicationFabrics/reassociateGateway/action|Réassocier une passerelle.|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>read|Lire des fournisseurs Recovery Services.|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>remove/action|Supprimer un fournisseur Recovery Services.|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>delete|Supprimer des fournisseurs Recovery Services.|
|/vaults/replicationFabrics/replicationRecoveryServicesProviders/<br>refreshProvider/action|Actualiser un fournisseur.|
|/vaults/replicationFabrics/replicationStorageClassifications/read|Lire des classifications de stockage.|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/read|Lire des mappages de classifications de stockage.|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/write|Créer ou mettre à jour des mappages de classifications de stockage.|
|/vaults/replicationFabrics/replicationStorageClassifications/<br>replicationStorageClassificationMappings/delete|Supprimer des mappages de classifications de stockage.|
|/vaults/replicationFabrics/replicationvCenters/read|Lire des travaux.|
|/vaults/replicationFabrics/replicationvCenters/write|Créer ou mettre à jour des travaux.|
|/vaults/replicationFabrics/replicationvCenters/delete|Supprimer des travaux.|
|/vaults/replicationFabrics/replicationNetworks/read|Lire des réseaux.|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/read|Lire des mappages de réseau.|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/write|Créer ou mettre à jour des mappages de réseau.|
|/vaults/replicationFabrics/replicationNetworks/<br>replicationNetworkMappings/delete|Supprimer des mappages de réseau.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>read|Lire des conteneurs de protection.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>discoverProtectableItem/action|Découvrir un élément pouvant être protégé.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>write|Créer ou mettre à jour des conteneurs de protection.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>remove/action|Supprimer un conteneur de protection.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>switchprotection/action|Basculer un conteneur de protection.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectableItems/read|Lire des éléments pouvant être protégés.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/read|Lire des mappages de conteneurs de protection.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/write|Créer ou mettre à jour des mappages de conteneurs de protection.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/remove/action|Supprimer un mappage de conteneurs de protection.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectionContainerMappings/delete|Supprimer des mappages de conteneurs de protection.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/read|Lire des éléments protégés.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/write|Créer ou mettre à jour des éléments protégés.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/delete|Supprimer des éléments protégés.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/remove/action|Supprimer un élément protégé.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/plannedFailover/action|Basculement planifié.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/unplannedFailover/action|Basculement|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailover/action|Test Failover|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/testFailoverCleanup/action|Nettoyage de basculement test.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/failoverCommit/action|Validation du basculement.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/reProtect/action|Reprotéger l’élément protégé.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/updateMobilityService/action|Mettre à jour le service Mobilité.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/repairReplication/action|Réparer la réplication.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/applyRecoveryPoint/action|Appliquer un point de récupération.|
|/vaults/replicationFabrics/replicationProtectionContainers/<br>replicationProtectedItems/recoveryPoints/read|Lire des points de récupération de réplication.|
|/vaults/replicationPolicies/read|Lire des stratégies.|
|/vaults/replicationPolicies/write|Créer ou mettre à jour des stratégies.|
|/vaults/replicationPolicies/delete|Supprimer des stratégies.|
|/vaults/replicationRecoveryPlans/read|Lire des plans de récupération.|
|/vaults/replicationRecoveryPlans/write|Créer ou mettre à jour des plans de récupération.|
|/vaults/replicationRecoveryPlans/delete|Supprimer des plans de récupération.|
|/vaults/replicationRecoveryPlans/plannedFailover/action|Plan de récupération de basculement planifié.|
|/vaults/replicationRecoveryPlans/unplannedFailover/action|Plan de récupération de basculement.|
|/vaults/replicationRecoveryPlans/testFailover/action|Plan de récupération de basculement test.|
|/vaults/replicationRecoveryPlans/testFailoverCleanup/action|Plan de récupération de nettoyage de basculement test.|
|/vaults/replicationRecoveryPlans/failoverCommit/action|Plan de récupération de validation de basculement.|
|/vaults/replicationRecoveryPlans/reProtect/action|Reprotéger le plan de récupération.|
|/Vaults/extendedInformation/read|Hello opération d’obtenir les informations étendues Obtient des informations d’étendue d’un objet représentant hello ressource Azure de type ? coffre ?|
|/Vaults/extendedInformation/write|Hello opération d’obtenir les informations étendues Obtient des informations d’étendue d’un objet représentant hello ressource Azure de type ? coffre ?|
|/Vaults/extendedInformation/delete|Hello opération d’obtenir les informations étendues Obtient des informations d’étendue d’un objet représentant hello ressource Azure de type ? coffre ?|
|/Vaults/backupManagementMetaData/read|Renvoie les métadonnées de gestion des sauvegardes pour le coffre Recovery Services.|
|/Vaults/backupProtectionContainers/read|Retourne tous les conteneurs appartenant toohello abonnement|
|/Vaults/backupFabrics/operationResults/read|Retourne l’état de fonctionnement de hello|
|/Vaults/backupFabrics/protectionContainers/read|Renvoie tous les conteneurs inscrits.|
|/Vaults/backupFabrics/protectionContainers/<br>operationResults/read|Obtient les résultats de l’opération effectuée sur le conteneur de protection.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/read|Retourne l’objet détails de l’élément protégé de hello|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/write|Créer un élément protégé de sauvegarde.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/delete|Supprime un élément protégé.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/backup/action|Effectue la sauvegarde d’un élément protégé.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationResults/read|Obtient les résultats de l’opération effectuée sur les éléments protégés.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/operationStatus/read|État de hello retourne d’opération effectuée sur les éléments protégés.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/read|Obtenir les points de récupération des éléments protégés.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>restore/action|Restaurer les points de récupération des éléments protégés.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>provisionInstantItemRecovery/action|Approvisionner la récupération d’éléments instantanée pour l’élément protégé.|
|/Vaults/backupFabrics/protectionContainers/<br>protectedItems/recoveryPoints/<br>revokeInstantItemRecovery/action|Révoquer la récupération d’éléments instantanée pour l’élément protégé.|
|/Vaults/usages/read|Renvoie des détails d’utilisation d’un coffre Recovery Services.|
|/vaults/usages/read|Lire des utilisations de coffre.|
|/Vaults/certificates/write|Hello d’opération de mise à jour du certificat de ressources met à jour le certificat d’informations d’identification hello ressource/coffre.|
|/Vaults/tokenInfo/read|Renvoie des informations de jeton pour le coffre Recovery Services.|
|/vaults/replicationAlertSettings/read|Lire des paramètres d’alertes.|
|/vaults/replicationAlertSettings/write|Créer ou mettre à jour des paramètres d’alertes.|
|/Vaults/backupOperations/read|Renvoie l’état de l’opération de sauvegarde pour le coffre Recovery Services.|
|/Vaults/storageConfig/read|Renvoie la configuration de stockage pour le coffre Recovery Services.|
|/Vaults/storageConfig/write|Met à jour la configuration de stockage pour le coffre Recovery Services.|
|/Vaults/backupUsageSummaries/read|Renvoie des résumés pour les éléments protégés et les serveurs protégés d’un coffre Recovery Services.|
|/Vaults/backupProtectedItems/read|Liste de hello renvoie de tous les éléments protégés.|
|/Vaults/backupconfig/vaultconfig/read|Renvoie la configuration pour le coffre Recovery Services.|
|/Vaults/backupconfig/vaultconfig/write|Met à jour la configuration pour le coffre Recovery Services.|
|/Vaults/registeredIdentities/write|Hello opération d’inscrire un conteneur de Service peut être utilisé tooregister un conteneur avec un Service de récupération.|
|/Vaults/registeredIdentities/read|Hello obtention de conteneurs permet d’obtenir les conteneurs hello inscrits pour une ressource.|
|/Vaults/registeredIdentities/delete|Hello opération d’annuler l’inscription d’un conteneur peut être utilisé toounregister un conteneur.|
|/Vaults/registeredIdentities/operationResults/read|opération de Hello obtenir des résultats de l’opération opération peut être l’état de l’opération hello utilisée pour obtenir et entraîner de façon asynchrone pour hello soumise|
|/vaults/replicationJobs/read|Lire des travaux.|
|/vaults/replicationJobs/cancel/action|Annuler un travail.|
|/vaults/replicationJobs/restart/action|Redémarrer un travail.|
|/vaults/replicationJobs/resume/action|Reprendre un travail.|
|/Vaults/backupPolicies/read|Renvoie toutes les stratégies de protection.|
|/Vaults/backupPolicies/write|Crée une stratégie de protection.|
|/Vaults/backupPolicies/delete|Supprimer une stratégie de protection.|
|/Vaults/backupPolicies/operationResults/read|Obtenir les résultats de l’opération de stratégie.|
|/Vaults/backupPolicies/operationStatus/read|Obtenir l’état de l’opération de stratégie.|
|/Vaults/vaultTokens/read|Hello opération jeton de coffre peut être utilisé tooget de jeton de coffre pour les opérations principales au niveau du coffre.|
|/Vaults/monitoringConfigurations/notificationConfiguration/read|Obtient la configuration de notification de coffre hello Recovery services.|
|/Vaults/backupJobs/read|Renvoie tous les objets de travail.|
|/Vaults/backupJobs/cancel/action|Annuler hello travail|
|/Vaults/backupJobs/operationResults/read|Retourne hello résultat d’opération du travail.|
|/locations/allocateStamp/action|AllocateStamp est une opération interne utilisée par le service.|
|/locations/allocatedStamp/read|GetAllocatedStamp est une opération interne utilisée par le service.|

## <a name="microsoftrelay"></a>Microsoft.Relay

| Opération | Description |
|---|---|
|/checkNamespaceAvailability/action|Vérifie la disponibilité d’un espace de noms sous un abonnement donné.|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources de relais hello et permet la création de hello des ressources de relais|
|/namespaces/write|Créer une ressource Namespace et mettre à jour ses propriétés. Balises et l’état de hello Namespace sont des propriétés de hello qui peuvent être mis à jour.|
|/namespaces/read|Obtenir la liste de hello de Description de la ressource Namespace|
|/namespaces/Delete|Supprimer une ressource Namespace.|
|/namespaces/authorizationRules/write|Créer des règles d’autorisation au niveau d’une ressource Namespace et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/namespaces/authorizationRules/delete|Supprimer une règle d’autorisation de ressource Namespace. Hello règle d’autorisation de Namespace par défaut ne peut pas être supprimé. |
|/namespaces/authorizationRules/listkeys/action|Obtenir la chaîne de connexion de hello toohello Namespace|
|/namespaces/HybridConnections/write|Créer ou mettre à jour des propriétés HybridConnection.|
|/namespaces/HybridConnections/read|Obtenir la liste des descriptions des ressources HybridConnection.|
|/namespaces/HybridConnections/Delete|Opération toodelete HybridConnection ressource|
|/namespaces/HybridConnections/authorizationRules/write|Créer des règles d’autorisation HybridConnection et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/namespaces/HybridConnections/authorizationRules/delete|Opération toodelete HybridConnection les règles d’autorisation|
|/namespaces/HybridConnections/authorizationRules/listkeys/action|Obtenir tooHybridConnection de chaîne de connexion hello|
|/namespaces/WcfRelays/write|Créer ou mettre à jour des propriétés WcfRelay.|
|/namespaces/WcfRelays/read|Obtenir la liste des descriptions des ressources WcfRelay.|
|/namespaces/WcfRelays/Delete|Opération toodelete WcfRelay ressource|
|/namespaces/WcfRelays/authorizationRules/write|Créer des règles d’autorisation WcfRelay et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/namespaces/WcfRelays/authorizationRules/delete|Opération toodelete WcfRelay les règles d’autorisation|
|/namespaces/WcfRelays/authorizationRules/listkeys/action|Obtenir tooWcfRelay de chaîne de connexion hello|

## <a name="microsoftresourcehealth"></a>Microsoft.ResourceHealth

| Opération | Description |
|---|---|
|/AvailabilityStatuses/read|États de disponibilité obtient hello pour toutes les ressources Bonjour spécifié étendue|
|/AvailabilityStatuses/current/read|État de disponibilité obtient hello pour hello de la ressource spécifiée|

## <a name="microsoftresources"></a>Microsoft.Resources

| Opération | Description |
|---|---|
|/checkResourceName/action|Vérifiez la validité du nom de ressource hello.|
|/providers/read|Obtenir la liste de hello des fournisseurs.|
|/subscriptions/read|Obtient la liste hello des abonnements.|
|/subscriptions/operationresults/read|Obtenir des résultats de l’opération abonnement de hello.|
|/subscriptions/providers/read|Obtient ou répertorie les fournisseurs de ressources.|
|/subscriptions/tagNames/read|Obtient ou répertorie les balises d’abonnement.|
|/subscriptions/tagNames/write|Ajoute une balise d’abonnement.|
|/subscriptions/tagNames/delete|Supprime une balise d’abonnement.|
|/subscriptions/tagNames/tagValues/read|Obtient ou répertorie les valeurs des balises d’abonnement.|
|/subscriptions/tagNames/tagValues/write|Ajoute une valeur de balise d’abonnement.|
|/subscriptions/tagNames/tagValues/delete|Supprime une valeur de balise d’abonnement.|
|/subscriptions/resources/read|Obtient les ressources d’un abonnement.|
|/subscriptions/resourceGroups/read|Obtient ou répertorie les groupes de ressources.|
|/subscriptions/resourceGroups/write|Crée ou met à jour un groupe de ressources.|
|/subscriptions/resourceGroups/delete|Supprime un groupe de ressources, ainsi que toutes ses ressources.|
|/subscriptions/resourceGroups/moveResources/action|Déplace les ressources à partir d’une ressource groupe tooanother.|
|/subscriptions/resourceGroups/validateMoveResources/action|Valide le déplacement des ressources à partir d’une ressource groupe tooanother.|
|/subscriptions/resourcegroups/resources/read|Obtient les ressources hello pour le groupe de ressources hello.|
|/subscriptions/resourcegroups/deployments/read|Obtient ou répertorie les déploiements.|
|/subscriptions/resourcegroups/deployments/write|Crée ou met à jour un déploiement.|
|/subscriptions/resourcegroups/deployments/operationstatuses/read|Obtient ou répertorie les états de l’opération de déploiement.|
|/subscriptions/resourcegroups/deployments/operations/read|Obtient ou répertorie les opérations de déploiement.|
|/subscriptions/locations/read|Obtient la liste hello des emplacements pris en charge.|
|/links/read|Obtient ou répertorie les liens des ressources.|
|/links/write|Crée ou met à jour un lien de ressource.|
|/links/delete|Supprime un lien de ressource.|
|/tenants/read|Obtient la liste hello des locataires.|
|/resources/read|Obtenir la liste de hello des ressources en fonction des filtres.|
|/deployments/read|Obtient ou répertorie les déploiements.|
|/deployments/write|Crée ou met à jour un déploiement.|
|/deployments/delete|Supprime un déploiement.|
|/deployments/cancel/action|Annule un déploiement.|
|/deployments/validate/action|Valide un déploiement.|
|/deployments/operations/read|Obtient ou répertorie les opérations de déploiement.|

## <a name="microsoftscheduler"></a>Microsoft.Scheduler

| Opération | Description |
|---|---|
|/jobcollections/read|Obtenir une collection de travaux.|
|/jobcollections/write|Crée ou met à jour une collection de travaux.|
|/jobcollections/delete|Supprime une collection de travaux.|
|/jobcollections/enable/action|Active une collection de travaux.|
|/jobcollections/disable/action|Désactive une collection de travaux.|
|/jobcollections/jobs/read|Obtient un travail.|
|/jobcollections/jobs/write|Crée ou met à jour un travail.|
|/jobcollections/jobs/delete|Supprime un travail.|
|/jobcollections/jobs/run/action|Exécute un travail.|
|/jobcollections/jobs/generateLogicAppDefinition/action|Génère une définition d’application logique basée sur un travail de Scheduler.|
|/jobcollections/jobs/jobhistories/read|Affiche l’historique des travaux.|

## <a name="microsoftsearch"></a>Microsoft.Search

| Opération | Description |
|---|---|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources de recherche hello et permet la création de hello de services de recherche.|
|/checkNameAvailability/action|Vérifie la disponibilité du nom du service hello.|
|/searchServices/write|Crée ou met à jour de service de recherche hello.|
|/searchServices/read|Lit le service de recherche hello.|
|/searchServices/delete|Supprime le service de recherche hello.|
|/searchServices/start/action|Démarre le service de recherche hello.|
|/searchServices/stop/action|Arrête le service de recherche hello.|
|/searchServices/listAdminKeys/action|Lit les clés d’administration hello.|
|/searchServices/regenerateAdminKey/action|Régénère la clé d’administration hello.|
|/searchServices/createQueryKey/action|Crée la clé de requête hello.|
|/searchServices/queryKey/read|Lit les clés de requête hello.|
|/searchServices/queryKey/delete|Supprime la clé de requête hello.|

## <a name="microsoftsecurity"></a>Microsoft.Security

| Opération | Description |
|---|---|
|/jitNetworkAccessPolicies/read|Obtient les stratégies d’accès juste-à-temps réseau hello|
|/jitNetworkAccessPolicies/write|Crée une stratégie d’accès réseau immédiat ou met à jour une stratégie d’accès réseau immédiat existante.|
|/jitNetworkAccessPolicies/initiate/action|Initie une stratégie d’accès réseau immédiat.|
|/securitySolutionsReferenceData/read|Obtient des données de référence de solutions de sécurité hello|
|/securityStatuses/read|Obtient des États d’intégrité de sécurité hello pour les ressources Azure|
|/webApplicationFirewalls/read|Obtient les pare-feux de hello web application|
|/webApplicationFirewalls/write|Crée un pare-feu d’applications web nouvelles ou met à jour un pare-feu d’applications web existant.|
|/webApplicationFirewalls/delete|Supprime un pare-feu d’applications web.|
|/securitySolutions/read|Obtient les solutions de sécurité hello|
|/securitySolutions/write|Crée une solution de sécurité ou met à jour une solution de sécurité existante.|
|/securitySolutions/delete|Supprime une solution de sécurité.|
|/tasks/read|Obtient toutes les recommandations de sécurité disponibles.|
|/tasks/dismiss/action|Ignorer une recommandation de sécurité.|
|/tasks/activate/action|Activer une recommandation de sécurité.|
|/policies/read|Obtient la stratégie de sécurité hello|
|/policies/write|Les mises à jour hello stratégie de sécurité|
|/applicationWhitelistings/read|Obtient les hello application whitelistings|
|/applicationWhitelistings/write|Crée une liste blanche des applications ou met à jour une liste blanche des applications existante.|

## <a name="microsoftservermanagement"></a>Microsoft.ServerManagement

| Opération | Description |
|---|---|
|/subscriptions/write|Crée ou met à jour un abonnement.|
|/gateways/write|Crée ou met à jour une passerelle.|
|/gateways/delete|Supprime une passerelle.|
|/gateways/read|Obtient une passerelle.|
|/gateways/regenerateprofile/action|Régénère le profil de passerelle hello|
|/gateways/upgradetolatest/action|Version plus récente de mises à niveau hello passerelle toohello|
|/nodes/write|Crée ou met à jour un nœud.|
|/nodes/delete|Supprime un nœud.|
|/nodes/read|Obtient un nœud.|
|/sessions/write|Crée ou met à jour une session.|
|/sessions/read|Obtient une session.|
|/sessions/delete|Supprime une session.|

## <a name="microsoftservicebus"></a>Microsoft.ServiceBus

| Opération | Description |
|---|---|
|/checkNameAvailability/action|Vérifier la disponibilité d’un espace de noms sous un abonnement donné|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources ServiceBus hello et permet la création de hello des ressources ServiceBus|
|/namespaces/write|Créer une ressource Namespace et mettre à jour ses propriétés. Balises et l’état de hello Namespace sont des propriétés de hello qui peuvent être mis à jour.|
|/namespaces/read|Obtenir la liste de hello de Description de la ressource Namespace|
|/namespaces/Delete|Supprimer une ressource Namespace|
|/namespaces/metricDefinitions/read|Obtenir la liste des descriptions des mesures de ressource Namespace.|
|/namespaces/authorizationRules/write|Créer des règles d’autorisation au niveau d’une ressource Namespace et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/namespaces/authorizationRules/read|Obtenir la liste de hello de description des espaces de noms des règles d’autorisation.|
|/namespaces/authorizationRules/delete|Supprimer une règle d’autorisation de ressource Namespace. Hello règle d’autorisation de Namespace par défaut ne peut pas être supprimé. |
|/namespaces/authorizationRules/listkeys/action|Obtenir la chaîne de connexion de hello toohello Namespace|
|/namespaces/authorizationRules/regenerateKeys/action|Régénérer hello Primary ou Secondary clé toohello ressource|
|/namespaces/diagnosticSettings/read|Obtenir la liste des descriptions des ressources des paramètres de diagnostics Namespace|
|/namespaces/diagnosticSettings/write|Obtenir la liste des descriptions des ressources des paramètres de diagnostics Namespace.|
|/namespaces/queues/write|Créer ou mettre à jour des propriétés de file d’attente.|
|/namespaces/queues/read|Obtenir la liste des descriptions des ressources de file d’attente.|
|/namespaces/queues/Delete|Opération toodelete ressource de file d’attente|
|/namespaces/queues/authorizationRules/write|Créer des règles d’autorisation de file d’attente et mettre à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/namespaces/queues/authorizationRules/read| Obtenir la liste de hello des règles d’autorisation de file d’attente|
|/namespaces/queues/authorizationRules/delete|Opération toodelete règles d’autorisation de file d’attente|
|/namespaces/queues/authorizationRules/listkeys/action|Obtenir tooQueue de chaîne de connexion hello|
|/namespaces/queues/authorizationRules/regenerateKeys/action|Régénérer hello Primary ou Secondary clé toohello ressource|
|/namespaces/logDefinitions/read|Obtenir la liste des descriptions des ressources des journaux Namespace.|
|/namespaces/topics/write|Créer ou mettre à jour des propriétés de rubrique.|
|/namespaces/topics/read|Obtenir la liste des descriptions des ressources de rubrique.|
|/namespaces/topics/Delete|Opération toodelete ressource de rubrique|
|/namespaces/topics/authorizationRules/write|Crée des règles d’autorisation de rubrique et met à jour leurs propriétés. Droits de l’accès de règles d’autorisation Hello, hello principal et secondaire de clés peuvent être mis à jour.|
|/namespaces/topics/authorizationRules/read| Obtenir la liste de hello des règles d’autorisation de rubrique|
|/namespaces/topics/authorizationRules/delete|Opération toodelete règles d’autorisation de rubrique|
|/namespaces/topics/authorizationRules/listkeys/action|Obtenir tooTopic de chaîne de connexion hello|
|/namespaces/topics/authorizationRules/regenerateKeys/action|Régénérer hello Primary ou Secondary clé toohello ressource|
|/namespaces/topics/subscriptions/write|Crée ou met à jour les propriétés TopicSubscription.|
|/namespaces/topics/subscriptions/read|Récupère la liste des descriptions des ressources TopicSubscription.|
|/namespaces/topics/subscriptions/Delete|Opération toodelete TopicSubscription ressource|
|/namespaces/topics/subscriptions/rules/write|Crée ou met à jour les propriétés de règle.|
|/namespaces/topics/subscriptions/rules/read|Récupère la liste des descriptions des ressources de règle.|
|/namespaces/topics/subscriptions/rules/Delete|Opération toodelete ressource de règle|

## <a name="microsoftsql"></a>Microsoft.Sql

| Opération | Description |
|---|---|
|/servers/read|Retourne une liste de serveurs dans un groupe de ressources sur un abonnement.|
|/servers/write|Crée un serveur ou modifie les propriétés d’un serveur existant dans un groupe de ressources sur un abonnement.|
|/servers/delete|Supprime un serveur et toutes les bases de données et les pools élastiques qu’il contient.|
|/servers/import/action|Créer une base de données sur le serveur de hello et déployer le schéma et les données à partir d’un package DacPac|
|/servers/upgrade/action|Activer la nouvelle fonctionnalité disponible sur la version la plus récente hello du serveur et spécifier le mappage de conversion de bases de données Édition|
|/servers/VulnerabilityAssessmentScans/action|Exécute l’analyse du serveur d’évaluation des vulnérabilités.|
|/servers/operationResults/read|Opération utilisée progression tootrack de mise à niveau du serveur à partir de la plus faible toohigher de version|
|/servers/operationResults/delete|Abandonner la mise à niveau en cours de la version du serveur|
|/servers/securityAlertPolicies/read|Récupérer les détails de la stratégie de détection des menaces hello server configuré sur un serveur donné|
|/servers/securityAlertPolicies/write|Modifier la détection des menaces hello serveur pour un serveur donné|
|/servers/securityAlertPolicies/operationResults/read|Récupérer les résultats de stratégie de détection des menaces opération de définition de serveur de hello|
|/servers/administrators/read|Récupère les détails d’administrateur du serveur.|
|/servers/administrators/write|Crée ou met à jour un administrateur de serveur.|
|/servers/administrators/delete|Supprimer l’administrateur du serveur à partir du serveur de hello|
|/servers/recoverableDatabases/read|Cette opération est utilisée pour la récupération d’urgence de base de données Active toorestore de base de données connue toolast bon point de sauvegarde. Il retourne des informations sur la dernière bonne sauvegarde hello, mais il ne restaure pas réellement de la base de données hello.|
|/servers/serviceObjectives/read|Récupère la liste des objectifs de niveau de service (également appelés niveaux de performance) disponibles sur un serveur donné.|
|/servers/firewallRules/read|Récupère les détails de la règle de pare-feu du serveur.|
|/servers/firewallRules/write|Créer ou mettre à jour de la règle de pare-feu de serveur qui contrôle la plage d’adresses IP autorisée tooconnect toohello server|
|/servers/firewallRules/delete|Supprimer la règle de pare-feu du serveur de hello|
|/servers/administratorOperationResults/read|Récupère les résultats de l’opération de l’administrateur du serveur.|
|/servers/recommendedElasticPools/read|Récupérer la recommandation pour la base de données élastique pools tooreduce coût ou améliorer les performances en fonction de l’utilisation des ressources historica|
|/servers/recommendedElasticPools/metrics/read|Récupère les mesures pour les pools de bases de données élastiques recommandés pour un serveur donné.|
|/servers/recommendedElasticPools/databases/read|Récupère les bases de données qui doivent être ajoutées aux pools de bases de données élastiques recommandés pour un serveur donné.|
|/servers/elasticPools/read|Récupère les détails d’un pool de bases de données élastique sur un serveur donné.|
|/servers/elasticPools/write|Crée ou modifie les propriétés d’un pool de bases de données élastique existant.|
|/servers/elasticPools/delete|Supprime un pool de bases de données élastique existant.|
|/servers/elasticPools/operationResults/read|Récupère les détails d’une opération effectuée dans un pool de bases de données élastique donné.|
|/servers/elasticPools/providers/Microsoft.Insights/<br>metricDefinitions/read|Retourne les types de mesure disponibles pour les pools de bases de données élastiques.|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/read|Obtient le paramètre de diagnostic hello pour la ressource de hello|
|/servers/elasticPools/providers/Microsoft.Insights/<br>diagnosticSettings/write|Crée ou met à jour le paramètre de diagnostic hello pour la ressource de hello|
|/servers/elasticPools/metrics/read|Retourne les mesures d’utilisation des ressources du pool de bases de données élastique.|
|/servers/elasticPools/elasticPoolDatabaseActivity/read|Récupère les activités et les détails d’une base de données spécifique faisant partie d’un pool de bases de données élastique.|
|/servers/elasticPools/advisors/read|Renvoie la liste des conseillers disponibles pour le pool élastique de hello|
|/servers/elasticPools/advisors/write|Met à jour l’état d’exécution automatique d’un conseiller au niveau du pool élastique.|
|/servers/elasticPools/advisors/recommendedActions/read|Renvoie la liste des actions recommandées du conseiller spécifié pour le pool élastique de hello|
|/servers/elasticPools/advisors/recommendedActions/write|Appliquer hello action sur le pool élastique de hello recommandée|
|/Servers/elasticPools/elasticPoolActivity/Read|Récupérer les activités et les détails sur un pool de bases de données élastique donné|
|/servers/elasticPools/databases/read|Récupérer la liste et les détails des bases de données qui font partie du pool de bases de données élastique sur un serveur donné|
|/servers/auditingPolicies/read|Récupérer les détails de la table de serveur hello par défaut configuré sur un serveur donné de stratégie d’audit|
|/servers/auditingPolicies/write|Modifier la table du serveur par défaut hello l’audit pour un serveur donné|
|/servers/disasterRecoveryConfiguration/operationResults/read|Obtenir les résultats des opérations de configuration de la récupération d’urgence|
|/servers/advisors/read|Renvoie la liste des conseillers disponibles pour le serveur de hello|
|/servers/advisors/write|Met à jour l’état d’exécution automatique d’un conseiller au niveau du serveur.|
|/servers/advisors/recommendedActions/read|Renvoie la liste des actions recommandées du conseiller spécifié pour le serveur de hello|
|/servers/advisors/recommendedActions/write|Appliquer hello action sur le serveur de hello recommandée|
|/servers/usages/read|Retourner le quota DTU du serveur et en cours DTU consuption par toutes les bases de données serveur de hello|
|/servers/elasticPoolEstimates/read|Renvoie la liste des estimations du pool élastique déjà créée pour ce serveur|
|/servers/elasticPoolEstimates/write|Crée la nouvelle estimation du pool élastique pour la liste des bases de données fournie|
|/servers/auditingSettings/read|Récupérer les détails de l’objet blob de serveur hello configuré sur un serveur donné de stratégie d’audit|
|/servers/auditingSettings/write|Audit des modifications hello serveur blob pour un serveur donné|
|/servers/auditingSettings/operationResults/read|Récupérer le résultat de l’objet blob de serveur hello une opération de jeu de stratégie d’audit|
|/servers/backupLongTermRetentionVaults/read|Cette opération est tooget utilisé un coffre de rétention de sauvegarde à long terme. Il retourne des informations sur server de hello coffre toothis inscrits.|
|/servers/backupLongTermRetentionVaults/write|Inscrire un coffre de rétention de sauvegarde à long terme|
|/servers/restorableDroppedDatabases/read|Récupérer une liste des bases de données supprimées d’un serveur donné qui se trouvent toujours dans la stratégie de rétention. Cette opération renvoie une liste de bases de données et les métadonnées associées, telle que la date de suppression.|
|/servers/databases/read|Renvoyer une liste de serveurs dans un groupe de ressources sur un abonnement|
|/servers/databases/write|Créer un nouveau serveur ou modifier les propriétés d’un serveur existant dans un groupe de ressources sur un abonnement|
|/servers/databases/delete|Supprimer un serveur et toutes les bases de données et les pools élastiques qu’il contient|
|/servers/databases/export/action|Créer une base de données sur le serveur de hello et déployer le schéma et les données à partir d’un package DacPac|
|/servers/databases/VulnerabilityAssessmentScans/action|Exécuter l’analyse de la base de données d’évaluation de la vulnérabilité.|
|/servers/databases/pause/action|Interrompre une base de données de l’édition DataWarehouse|
|/servers/databases/resume/action|Reprendre une base de données de l’édition DataWarehouse|
|/servers/databases/operationResults/read|Opération utilisée progression tootrack d’une longue opération de base de données, telles que l’échelle.|
|/servers/databases/replicationLinks/read|Renvoie des informations sur les liens de réplication établis pour une base de données spécifique|
|/servers/databases/replicationLinks/delete|Interruption de la relation de réplication hello force et avec perte de données potentielle|
|/servers/databases/replicationLinks/unlink/action|Interruption de la relation de réplication hello force ou après la synchronisation avec les partenaires hello|
|/servers/databases/replicationLinks/failover/action|Basculement après la synchronisation de toutes les modifications à partir de hello principal, ce qui rend de cette base de données dans le principal à distance de la relation de réplication hello hello principal et à effectuer dans une base de données secondaire|
|/servers/databases/replicationLinks/forceFailoverAllowDataLoss/action|Basculement immédiatement avec perte de données potentielle, ce qui rend cette base de données en à distance de la relation de réplication hello hello principal et en principal dans une base de données secondaire|
|/servers/databases/replicationLinks/updateReplicationMode/action|Mettre à jour le mode de réplication pour le lien toosynchronous ou en mode asynchrone|
|/servers/databases/replicationLinks/operationResults/read|Obtenir l’état des opérations à long terme sur les liens de réplication de base de données|
|/servers/databases/dataMaskingPolicies/read|Récupérer les détails de la stratégie configurée sur une base de données de masquage des données hello|
|/servers/databases/dataMaskingPolicies/write|Modifier la stratégie de masquage des données pour une base de données spécifique|
|/servers/databases/dataMaskingPolicies/rules/read|Récupérer les détails des données hello configuré sur une base de données de règle de stratégie de masquage|
|/servers/databases/dataMaskingPolicies/rules/write|Modifier la règle de stratégie de masquage des données pour une base de données spécifique|
|/servers/databases/securityAlertPolicies/read|Récupérer les détails de la stratégie de détection des menaces hello configuré sur une base de données|
|/servers/databases/securityAlertPolicies/write|Modifier la stratégie de détection des menaces hello pour une base de données|
|/servers/databases/providers/Microsoft.Insights/<br>metricDefinitions/read|Renvoie les types de mesures disponibles pour les bases de données|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/read|Obtient le paramètre de diagnostic hello pour la ressource de hello|
|/servers/databases/providers/Microsoft.Insights/<br>diagnosticSettings/write|Crée ou met à jour le paramètre de diagnostic hello pour la ressource de hello|
|/servers/databases/providers/Microsoft.Insights/<br>logDefinitions/read|Obtient les journaux disponibles hello pour les bases de données|
|/servers/databases/topQueries/read|Renvoie les statistiques d’exécution agrégées de la requête sélectionnée dans la période choisie|
|/servers/databases/topQueries/queryText/read|Retourne le texte de Transact-SQL hello pour l’ID de la requête sélectionnée|
|/servers/databases/topQueries/statistics/read|Renvoie les statistiques d’exécution agrégées de la requête sélectionnée dans la période choisie|
|/servers/databases/connectionPolicies/read|Récupérer les détails de la stratégie de connexion hello configuré sur une base de données|
|/servers/databases/connectionPolicies/write|Modifie la stratégie de connexion d’une base de données spécifique.|
|/servers/databases/metrics/read|Retourne les mesures d’utilisation des ressources de base de données.|
|/servers/databases/auditRecords/read|Récupérer les enregistrements d’audit de hello de base de données blob|
|/servers/databases/transparentDataEncryption/read|Récupère l’état et les détails de la fonctionnalité de sécurité Transparent Data Encryption pour une base de données spécifique.|
|/servers/databases/transparentDataEncryption/write|Active ou désactive Transparent Data Encryption pour une base de données spécifique.|
|/servers/databases/transparentDataEncryption/operationResults/read|Récupère l’état et les détails de la fonctionnalité de sécurité Transparent Data Encryption pour une base de données spécifique.|
|/servers/databases/auditingPolicies/read|Récupérer les détails de la stratégie d’audit de table hello configuré sur une base de données|
|/servers/databases/auditingPolicies/write|Modifier la stratégie d’audit de table hello pour une base de données|
|/servers/databases/dataWarehouseQueries/read|Retourne des informations de requête de distribution hello data warehouse pour l’ID de la requête sélectionnée|
|/servers/databases/dataWarehouseQueries/<br>dataWarehouseQuerySteps/read|Hello de retourne distribuée des informations d’étape de requête de requête de l’entrepôt de données pour l’ID de l’étape sélectionnée|
|/servers/databases/serviceTierAdvisors/read|Retourner suggestion à propos de la mise à l’échelle de base de données vers le haut ou vers le bas en fonction des performances de requête d’exécution statistiques tooimprove ou de réduire les coûts|
|/servers/databases/advisors/read|Renvoie la liste des conseillers disponibles pour la base de données hello|
|/servers/databases/advisors/write|Met à jour l’état d’exécution automatique d’un conseiller au niveau de la base de données.|
|/servers/databases/advisors/recommendedActions/read|Renvoie la liste des actions recommandées du conseiller spécifié pour la base de données hello|
|/servers/databases/advisors/recommendedActions/write|Appliquer hello action sur la base de données hello recommandée|
|/servers/databases/usages/read|Retourne la taille maximale de base de données qui peut être atteinte ainsi que la taille actuelle occupée par les données.|
|/servers/databases/queryStore/read|Retourne les valeurs actuelles des paramètres de magasin de requêtes de base de données hello|
|/servers/databases/queryStore/write|Met à jour le paramètre de magasin de requêtes de base de données hello|
|/servers/databases/auditingSettings/read|Récupérer les détails de la stratégie d’audit de blob hello configuré sur une base de données|
|/servers/databases/auditingSettings/write|Modifier la stratégie d’audit de blob hello pour une base de données|
|/servers/databases/schemas/tables/recommendedIndexes/read|Récupère la liste des recommandations d’index d’une base de données.|
|/servers/databases/schemas/tables/recommendedIndexes/write|Applique une recommandation d’index.|
|/servers/databases/schemas/tables/columns/read|Récupère la liste des colonnes d’une table.|
|/servers/databases/missingindexes/read|Suggestions toocreate d’index de base de données de retour, de modifier ou de supprimer des performances de requête de commande tooimprove|
|/servers/databases/missingindexes/write|Utilise une recommandation d’index de base de données dans une base de données particulière.|
|/servers/databases/importExportOperationResults/read|Retourne les détails de l’opération d’importation ou d’exportation de la base de données à partir du fichier DacPac situé dans le compte de stockage.|
|/servers/importExportOperationResults/read|Liste de retour hello avec des détails pour les opérations d’importation de base de données à partir du compte de stockage sur un serveur donné|

## <a name="microsoftstorage"></a>Microsoft.Storage

| Opération | Description |
|---|---|
|/register/action|Enregistre l’abonnement hello pour le fournisseur de ressources de stockage hello et permet la création de hello de comptes de stockage.|
|/checknameavailability/read|Vérifie que le nom du valide est valide et qu’il n’est pas déjà utilisé.|
|/storageAccounts/write|Crée un compte de stockage avec hello spécifié paramètres ou mise à jour hello propriétés ou les balises, ou ajoute personnalisée domaine pour hello spécifié de compte de stockage.|
|/storageAccounts/delete|Supprime un compte de stockage existant.|
|/storageAccounts/listkeys/action|Retourne les clés d’accès hello pour hello spécifié de compte de stockage.|
|/storageAccounts/regeneratekey/action|Régénère les clés d’accès hello pour hello spécifié de compte de stockage.|
|/storageAccounts/read|Retourne hello liste des comptes de stockage ou obtient les propriétés de hello pour hello spécifié de compte de stockage.|
|/storageAccounts/listAccountSas/action|Retourne le jeton du compte SAP hello pour hello spécifié de compte de stockage.|
|/storageAccounts/listServiceSas/action|Jeton SAS du service de stockage|
|/storageAccounts/services/diagnosticSettings/write|Crée/met à jour les paramètres de diagnostic de compte de stockage.|
|/skus/read|Répertorie les hello références (SKU) pris en charge par Microsoft.Storage.|
|/usages/read|Retourne hello limite et hello actuel nombre d’utilisations de ressources Bonjour spécifié d’abonnement|
|/operations/read|Interroge hello état d’une opération asynchrone.|
|/locations/deleteVirtualNetworkOrSubnets/action|Informe Microsoft.Storage que le sous-réseau ou le réseau virtuel est en cours de suppression.|

## <a name="microsoftstorsimple"></a>Microsoft.StorSimple

| Opération | Description |
|---|---|
|/managers/clearAlerts/action|Désactivez toutes les alertes hello associés au Gestionnaire de périphériques hello.|
|/managers/getActivationKey/action|Obtenir la clé d’activation pour le Gestionnaire de périphériques hello.|
|/managers/regenerateActivationKey/action|Régénérer la clé d’activation pour le Gestionnaire de périphériques hello.|
|/managers/regenarateRegistationCertificate/action|Régénérer le certificat d’inscription pour les gestionnaires de périphériques hello.|
|/managers/getEncryptionKey/action|Obtenir la clé de chiffrement pour le Gestionnaire de périphériques hello.|
|/managers/read|Répertorie ou obtient les gestionnaires de périphériques hello|
|/managers/delete|Supprime les gestionnaires de périphériques hello|
|/managers/write|Créer ou mettre à jour de responsables d’appareil hello|
|/managers/configureDevice/action|Configure un appareil.|
|/managers/listActivationKey/action|Obtient la clé d’activation hello Hello StorSimple le Gestionnaire de périphériques.|
|/managers/listPublicEncryptionKey/action|Répertorie les clés de chiffrement publiques d’un gestionnaire StorSimple Device Manager.|
|/managers/listPrivateEncryptionKey/action|Récupère la clé de chiffrement publique d’un gestionnaire StorSimple Device Manager.|
|/managers/provisionCloudAppliance/action|Crée une appliance cloud.|
|/Managers/write|L’opération de création de coffre entraîne la création d’une ressource Azure de type « coffre ».|
|/Managers/read|opération d’obtention d’un coffre de Hello Obtient un objet représentant hello ressource Azure de type 'coffre'|
|/Managers/delete|ressource Azure de type 'coffre' spécifiée pour Hello suppression du coffre opération suppressions hello|
|/managers/storageAccountCredentials/write|Créer ou mettre à jour les informations d’identification de compte de stockage hello|
|/managers/storageAccountCredentials/read|Répertorie ou obtient des informations d’identification de compte de stockage hello|
|/managers/storageAccountCredentials/delete|Supprime les informations d’identification de compte de stockage hello|
|/managers/storageAccountCredentials/listAccessKey/action|Répertorie les clés d’accès des informations d’identification de compte de stockage.|
|/managers/accessControlRecords/read|Répertorie ou obtient les enregistrements de contrôle d’accès hello|
|/managers/accessControlRecords/write|Créer ou mettre à jour des enregistrements de contrôle d’accès hello|
|/managers/accessControlRecords/delete|Supprime les enregistrements de contrôle d’accès hello|
|/managers/metrics/read|Répertorie ou obtient les métriques de hello|
|/managers/bandwidthSettings/read|Liste des paramètres de bande passante hello (série 8000 uniquement)|
|/managers/bandwidthSettings/write|Crée ou met à jour les paramètres de bande passante (série 8000 uniquement).|
|/managers/bandwidthSettings/delete|Supprime des paramètres de bande passante existants (série 8000 uniquement).|
|/Managers/extendedInformation/read|Hello opération d’obtenir les informations étendues Obtient des informations d’étendue d’un objet représentant hello ressource Azure de type ? coffre ?|
|/Managers/extendedInformation/write|Hello opération d’obtenir les informations étendues Obtient des informations d’étendue d’un objet représentant hello ressource Azure de type ? coffre ?|
|/Managers/extendedInformation/delete|Hello opération d’obtenir les informations étendues Obtient des informations d’étendue d’un objet représentant hello ressource Azure de type ? coffre ?|
|/managers/alerts/read|Répertorie ou obtient les alertes hello|
|/managers/storageDomains/read|Répertorie ou obtient les domaines de stockage hello|
|/managers/storageDomains/write|Créer ou mettre à jour des domaines de stockage hello|
|/managers/storageDomains/delete|Supprime les domaines de stockage hello|
|/managers/devices/scanForUpdates/action|Recherche des mises à jour sur un appareil.|
|/managers/devices/download/action|Télécharge les mises à jour d’un appareil.|
|/managers/devices/install/action|Installe des mises à jour sur un appareil.|
|/managers/devices/read|Répertorie ou obtient hello périphériques|
|/managers/devices/write|Créer ou mettre à jour les appareils hello|
|/managers/devices/delete|Permet de supprimer les périphériques hello|
|/managers/devices/deactivate/action|Désactive un appareil.|
|/managers/devices/publishSupportPackage/action|Publie le package de support d’un appareil pour la résolution des problèmes du Support Microsoft.|
|/managers/devices/failover/action|Basculement d’appareil de hello.|
|/managers/devices/sendTestAlertEmail/action|Envoyer des alertes par courrier électronique de test tooconfigured les destinataires de courrier électronique.|
|/managers/devices/installUpdates/action|Installe les mises à jour sur les appareils hello|
|/managers/devices/listFailoverSets/action|Liste hello basculement définit pour un périphérique existant.|
|/managers/devices/listFailoverTargets/action|Liste des cibles de basculement de périphériques de hello|
|/managers/devices/publicEncryptionKey/action|Clé de chiffrement publique liste du Gestionnaire de périphériques hello|
|/managers/devices/hardwareComponentGroups/<br>read|Hello de liste des groupes de composants matériels|
|/managers/devices/hardwareComponentGroups/<br>changeControllerPowerState/action|Modifie l’état d’alimentation du contrôleur des groupes de composants matériels.|
|/managers/devices/metrics/read|Répertorie ou obtient les métriques de hello|
|/managers/devices/chapSettings/write|Créer ou mettre à jour les paramètres Chap hello|
|/managers/devices/chapSettings/read|Répertorie ou obtient les paramètres Chap hello|
|/managers/devices/chapSettings/delete|Supprime les paramètres Chap hello|
|/managers/devices/backupScheduleGroups/read|Répertorie ou obtient les groupes de planification de sauvegarde hello|
|/managers/devices/backupScheduleGroups/write|Créer ou mettre à jour des groupes de planification de sauvegarde hello|
|/managers/devices/backupScheduleGroups/delete|Supprime les groupes de planification de sauvegarde hello|
|/managers/devices/updateSummary/read|Obtient les hello résumé de la mise à jour ou de listes|
|/managers/devices/migrationSourceConfigurations/<br>import/action|Importe les configurations de source pour la migration.|
|/managers/devices/migrationSourceConfigurations/<br>startMigrationEstimate/action|Démarrez une durée de hello tooestimate travail hello du processus de migration.|
|/managers/devices/migrationSourceConfigurations/<br>startMigration/action|Démarre la migration à l’aide des configurations de source.|
|/managers/devices/migrationSourceConfigurations/<br>confirmMigration/action|Vérifie et valide une migration réussie.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationEstimate/action|Extraction de l’état de hello pour la tâche de migration d’estimation hello.|
|/managers/devices/migrationSourceConfigurations/<br>fetchMigrationStatus/action|Extraction de l’état de hello pour la migration de hello.|
|/managers/devices/migrationSourceConfigurations/<br>fetchConfirmMigrationStatus/action|Extraction hello confirmer l’état de la migration.|
|/managers/devices/alertSettings/read|Répertorie ou obtient les paramètres d’alerte hello|
|/managers/devices/alertSettings/write|Créer ou mettre à jour les paramètres d’alerte hello|
|/managers/devices/networkSettings/read|Répertorie ou obtient les paramètres de réseau hello|
|/managers/devices/networkSettings/write|Crée ou met à jour les paramètres réseau.|
|/managers/devices/jobs/read|Répertorie ou obtient les tâches hello|
|/managers/devices/jobs/cancel/action|Annule un travail en cours d’exécution.|
|/managers/devices/metricsDefinitions/read|Répertorie ou obtient les définitions de métriques hello|
|/managers/devices/volumeContainers/write|Crée ou met à jour des conteneurs de volumes (série 8000 uniquement).|
|/managers/devices/volumeContainers/read|Liste des conteneurs de volumes hello (série 8000 uniquement)|
|/managers/devices/volumeContainers/delete|Supprime des conteneurs de volumes existants (série 8000 uniquement).|
|/managers/devices/volumeContainers/listEncryptionKeys/action|Répertorie les clés de chiffrement des conteneurs de volumes.|
|/managers/devices/volumeContainers/rolloverEncryptionKey/action|Clés de chiffrement de substitution des conteneurs de volumes|
|/managers/devices/volumeContainers/metrics/read|Liste des métriques de hello|
|/managers/devices/volumeContainers/volumes/read|Liste des Volumes de hello|
|/managers/devices/volumeContainers/volumes/write|Crée un volume ou met à jour des volumes existants.|
|/managers/devices/volumeContainers/volumes/delete|Supprime un volume existant.|
|/managers/devices/volumeContainers/volumes/metrics/read|Liste des métriques de hello|
|/managers/devices/volumeContainers/volumes/metricsDefinitions/read|Liste des définitions de métriques de hello|
|/managers/devices/volumeContainers/metricsDefinitions/read|Liste des définitions de métriques de hello|
|/managers/devices/iscsiservers/read|Obtient les hello iSCSI serveurs ou de listes|
|/managers/devices/iscsiservers/write|Créer ou mettre à jour hello iSCSI serveurs|
|/managers/devices/iscsiservers/delete|Supprime l’iSCSI hello serveurs|
|/managers/devices/iscsiservers/backup/action|Exécute la sauvegarde d’un serveur iSCSI.|
|/managers/devices/iscsiservers/metrics/read|Répertorie ou obtient les métriques de hello|
|/managers/devices/iscsiservers/disks/read|Répertorie ou obtient les disques hello|
|/managers/devices/iscsiservers/disks/write|Créer ou mettre à jour des disques de hello|
|/managers/devices/iscsiservers/disks/delete|Supprime les disques hello|
|/managers/devices/iscsiservers/disks/metrics/read|Répertorie ou obtient les métriques de hello|
|/managers/devices/iscsiservers/disks/metricsDefinitions/read|Répertorie ou obtient les définitions de métriques hello|
|/managers/devices/iscsiservers/metricsDefinitions/read|Répertorie ou obtient les définitions de métriques hello|
|/managers/devices/backups/read|Obtient les hello du jeu de sauvegarde ou de listes|
|/managers/devices/backups/delete|Suppressions hello du jeu de sauvegarde|
|/managers/devices/backups/restore/action|Restaurer tous les volumes hello à partir d’un jeu de sauvegarde.|
|/managers/devices/backups/elements/clone/action|Clone un partage ou un volume à l’aide d’un élément de sauvegarde.|
|/managers/devices/backupPolicies/write|Crée ou met à jour des stratégies de sauvegarde (série 8000 uniquement).|
|/managers/devices/backupPolicies/read|Hello liste des stratégies de sauvegarde (série 8000 uniquement)|
|/managers/devices/backupPolicies/delete|Supprime des stratégies de sauvegarde existantes (série 8000 uniquement).|
|/managers/devices/backupPolicies/backup/action|Créer une sauvegarde de tous les volumes hello protégés par une stratégie de hello un toocreate sauvegarde manuelle une demande.|
|/managers/devices/backupPolicies/schedules/write|Crée une planification ou met à jour des planifications existantes.|
|/managers/devices/backupPolicies/schedules/read|Liste des planifications hello|
|/managers/devices/backupPolicies/schedules/delete|Supprime une planification existante.|
|/managers/devices/securitySettings/update/action|Mettre à jour les paramètres de sécurité hello.|
|/managers/devices/securitySettings/read|Hello de liste des paramètres de sécurité|
|/managers/devices/securitySettings/<br>syncRemoteManagementCertificate/action|Synchroniser le certificat de gestion à distance hello pour un périphérique.|
|/managers/devices/securitySettings/write|Crée ou met à jour les paramètres de sécurité.|
|/managers/devices/fileservers/read|Répertorie ou obtient les serveurs de fichiers hello|
|/managers/devices/fileservers/write|Créer ou mettre à jour des serveurs de fichiers hello|
|/managers/devices/fileservers/delete|Supprime les serveurs de fichiers hello|
|/managers/devices/fileservers/backup/action|Exécute la sauvegarde d’un serveur de fichiers.|
|/managers/devices/fileservers/metrics/read|Répertorie ou obtient les métriques de hello|
|/managers/devices/fileservers/shares/write|Créer ou mettre à jour des partages de hello|
|/managers/devices/fileservers/shares/read|Répertorie ou obtient des partages de hello|
|/managers/devices/fileservers/shares/delete|Supprime les partages hello|
|/managers/devices/fileservers/shares/metrics/read|Répertorie ou obtient les métriques de hello|
|/managers/devices/fileservers/shares/metricsDefinitions/read|Répertorie ou obtient les définitions de métriques hello|
|/managers/devices/fileservers/metricsDefinitions/read|Répertorie ou obtient les définitions de métriques hello|
|/managers/devices/timeSettings/read|Répertorie ou obtient les paramètres d’heure hello|
|/managers/devices/timeSettings/write|Crée ou met à jour les paramètres horaires.|
|/Managers/certificates/write|Hello d’opération de mise à jour du certificat de ressources met à jour le certificat d’informations d’identification hello ressource/coffre.|
|/managers/cloudApplianceConfigurations/read|Liste hello pris en charge les Configurations Cloud Appliance|
|/managers/metricsDefinitions/read|Répertorie ou obtient les définitions de métriques hello|
|/managers/encryptionSettings/read|Répertorie ou obtient les paramètres de chiffrement hello|

## <a name="microsoftstreamanalytics"></a>Microsoft.StreamAnalytics

| Opération | Description |
|---|---|
|/streamingjobs/Start/action|Démarre une tâche Stream Analytics.|
|/streamingjobs/Stop/action|Arrête une tâche Stream Analytics.|
|/streamingjobs/Read|Lit une tâche Stream Analytics.|
|/streamingjobs/Write|Écrit une tâche Stream Analytics.|
|/streamingjobs/Delete|Supprime une tâche Stream Analytics.|
|/streamingjobs/providers/Microsoft.Insights/metricDefinitions/read|Obtient les métriques disponibles hello pour streamingjobs|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/read|Lit le paramètre de diagnostic.|
|/streamingjobs/providers/Microsoft.Insights/diagnosticSettings/write|Écrit un paramètre de diagnostic.|
|/streamingjobs/providers/Microsoft.Insights/logDefinitions/read|Obtient les journaux disponibles hello streamingjobs|
|/streamingjobs/transformations/Read|Lit une transformation de tâche Stream Analytics.|
|/streamingjobs/transformations/Write|Écrit une transformation de tâche Stream Analytics.|
|/streamingjobs/transformations/Delete|Supprime une transformation de tâche Stream Analytics.|
|/streamingjobs/inputs/Read|Lit une entrée de tâche Stream Analytics.|
|/streamingjobs/inputs/Write|Écrit une entrée de tâche Stream Analytics.|
|/streamingjobs/inputs/Delete|Supprime une entrée de tâche Stream Analytics.|
|/streamingjobs/outputs/Read|Lit une sortie de tâche Stream Analytics.|
|/streamingjobs/outputs/Write|Écrit une sortie de tâche Stream Analytics.|
|/streamingjobs/outputs/Delete|Supprime une sortie de tâche Stream Analytics.|

## <a name="microsoftsupport"></a>Microsoft.Support

| Opération | Description |
|---|---|
|/register/action|Registres tooSupport fournisseur de ressources|
|/supportTickets/read|Obtient les détails du Ticket de Support (y compris l’état, gravité, informations de contact et les communications) ou liste hello des Tickets de Support sur les abonnements.|
|/supportTickets/write|Crée ou met à jour un ticket de support. Vous pouvez créer un ticket de support pour les problèmes techniques ou les problèmes liés à la facturation, aux quotas ou à la gestion des abonnements. Vous pouvez mettre à jour la gravité des problèmes, les détails du contact et les communications pour les tickets de support existants.|

## <a name="microsoftweb"></a>Microsoft.Web

| Opération | Description |
|---|---|
|/unregister/action|Annuler l’inscription du fournisseur de ressources Microsoft.Web pour l’abonnement de hello.|
|/validate/action|Valide.|
|/register/action|Inscrire le fournisseur de ressources Microsoft.Web pour l’abonnement de hello.|
|/hostingEnvironments/Read|Obtenir les propriétés de hello d’un environnement App Service|
|/hostingEnvironments/Write|Crée un environnement App Service ou en met un à jour.|
|/hostingEnvironments/Delete|Supprime un environnement App Service.|
|/hostingEnvironments/reboot/Action|Redémarre tous les ordinateurs dans un environnement App Service.|
|/hostingenvironments/resume/action|Reprend les environnements d’hébergement.|
|/hostingenvironments/suspend/action|Interrompt les environnements d’hébergement.|
|/hostingenvironments/metricdefinitions/read|Récupère les définitions métriques des environnements d’hébergement.|
|/hostingEnvironments/workerPools/Read|Obtenir les propriétés de hello d’un Pool de travail dans un environnement App Service|
|/hostingEnvironments/workerPools/Write|Crée un pool de workers dans un environnement App Service ou en met un à jour.|
|/hostingenvironments/workerpools/metricdefinitions/read|Récupère les définitions métriques des pools de workers des environnements d’hébergement.|
|/hostingenvironments/workerpools/metrics/read|Récupère les mesures des pools de workers des environnements d’hébergement.|
|/hostingenvironments/workerpools/skus/read|Récupère les références des pools de workers des environnements d’hébergement.|
|/hostingenvironments/workerpools/usages/read|Récupère les utilisations des pools de workers des environnements d’hébergement.|
|/hostingenvironments/sites/read|Récupère les applications web des environnements d’hébergement.|
|/hostingenvironments/serverfarms/read|Récupère les plans App Service des environnements d’hébergement.|
|/hostingenvironments/usages/read|Récupère les utilisations des environnements d’hébergement.|
|/hostingenvironments/capacities/read|Récupère les fonctionnalités des environnements d’hébergement.|
|/hostingenvironments/operations/read|Récupère les opérations des environnements d’hébergement.|
|/hostingEnvironments/multiRolePools/Read|Obtenir les propriétés hello d’un Pool de serveur frontal dans un environnement App Service|
|/hostingEnvironments/multiRolePools/Write|Crée un pool frontal dans un environnement App Service ou en met un à jour.|
|/hostingenvironments/multirolepools/metricdefinitions/read|Récupère les définitions métriques des pools multirôles des environnements d’hébergement.|
|/hostingenvironments/multirolepools/metrics/read|Récupère les mesures des pools multirôles des environnements d’hébergement.|
|/hostingenvironments/multirolepools/skus/read|Récupère les références des pools multirôles des environnements d’hébergement.|
|/hostingenvironments/multirolepools/usages/read|Récupère les utilisations des pools multirôles des environnements d’hébergement.|
|/hostingenvironments/diagnostics/read|Récupère les diagnostics des environnements d’hébergement.|
|/publishingusers/read|Récupère la publication des utilisateurs.|
|/publishingusers/write|Met à jour la publication des utilisateurs.|
|/checknameavailability/read|Vérifie si le nom de la ressource est disponible.|
|/geoRegions/Read|Obtenir la liste de hello de région géographique.|
|/sites/Read|Obtenir les propriétés de hello d’une application Web|
|/sites/Write|Crée une application web ou en met une à jour.|
|/sites/Delete|Supprimer une application web existante|
|/sites/backup/Action|Crée une sauvegarde d’application web.|
|/sites/publishxml/Action|Récupère le profil de publication xml pour une application web.|
|/sites/publish/Action|Publie une application web.|
|/sites/restart/Action|Redémarre une application web.|
|/sites/start/Action|Démarre une application web.|
|/sites/stop/Action|Arrête une application web.|
|/sites/slotsswap/Action|Permute des emplacements de déploiement d’application web.|
|/sites/slotsdiffs/Action|Récupère les différences de configuration entre l’application web et les emplacements.|
|/sites/applySlotConfig/Action|Appliquer la configuration de l’emplacement web application à partir de la cible emplacement toohello actuel web app|
|/sites/resetSlotConfig/Action|Réinitialise la configuration d’application web.|
|/sites/functions/action|Fonctions Web Apps.|
|/sites/listsyncfunctiontriggerstatus/action|Répertorie le statut de déclenchement de fonction de synchronisation Web Apps.|
|/sites/networktrace/action|Trace réseau Web Apps.|
|/sites/newpassword/action|Newpassword Web Apps.|
|/sites/sync/action|Synchronise Web Apps.|
|/sites/operationresults/read|Récupère les résultats de l’opération Web Apps.|
|/sites/webjobs/read|Récupère WebJobs de Web Apps.|
|/sites/backup/read|Récupère la sauvegarde Web Apps.|
|/sites/backup/write|Met à jour la sauvegarde Web Apps.|
|/sites/metricdefinitions/read|Récupère les définitions métriques Web Apps.|
|/sites/metrics/read|Récupère les mesures Web Apps.|
|/sites/continuouswebjobs/delete|Supprime des tâches web continues Web Apps.|
|/sites/continuouswebjobs/read|Récupère des tâches web continues Web Apps.|
|/sites/continuouswebjobs/start/action|Démarre des tâches web continues Web Apps.|
|/sites/continuouswebjobs/stop/action|Arrête des tâches web continues Web Apps.|
|/sites/domainownershipidentifiers/read|Récupère l’identificateur de propriété de domaine Web Apps.|
|/sites/domainownershipidentifiers/write|Met à jour l’identificateur de propriété de domaine Web Apps.|
|/sites/premieraddons/delete|Supprime les modules complémentaires Premier Web Apps.|
|/sites/premieraddons/read|Récupère les modules complémentaires Premier Web Apps.|
|/sites/premieraddons/write|Met à jour les modules complémentaires Premier Web Apps.|
|/sites/triggeredwebjobs/delete|Supprime les tâches web déclenchées dans Web Apps.|
|/sites/triggeredwebjobs/read|Récupère les tâches web déclenchées dans Web Apps.|
|/sites/triggeredwebjobs/run/action|Exécute les tâches web déclenchées dans Web Apps.|
|/sites/hostnamebindings/delete|Supprime les liaisons de nom d’hôte Web Apps.|
|/sites/hostnamebindings/read|Récupère les liaisons de nom d’hôte Web Apps.|
|/sites/hostnamebindings/write|Met à jour les liaisons de nom d’hôte Web Apps.|
|/sites/virtualnetworkconnections/delete|Supprime les connexions de réseau virtuel Web Apps.|
|/sites/virtualnetworkconnections/read|Récupère les connexions de réseau virtuel Web Apps.|
|/sites/virtualnetworkconnections/write|Met à jour les connexions de réseau virtuel Web Apps.|
|/sites/virtualnetworkconnections/gateways/read|Récupère les passerelles de connexions de réseau virtuel Web Apps.|
|/sites/virtualnetworkconnections/gateways/write|Met à jour les passerelles de connexions de réseau virtuel Web Apps.|
|/sites/publishxml/read|Récupère publication XML Web Apps.|
|/sites/hybridconnectionrelays/read|Récupère les relais de connexions hybrides Web Apps.|
|/sites/perfcounters/read|Récupère les compteurs de performances Web Apps.|
|/sites/usages/read|Récupère les utilisations Web Apps.|
|/sites/slots/Write|Crée un emplacement d’application web ou en met un à jour.|
|/sites/slots/Delete|Supprime un emplacement d’application web existant.|
|/sites/slots/backup/Action|Crée une sauvegarde d’emplacement d’application web.|
|/sites/slots/publishxml/Action|Récupère le profil de publication xml pour l’emplacement d’application web.|
|/sites/slots/publish/Action|Publie un emplacement d’application web.|
|/sites/slots/restart/Action|Redémarre un emplacement d’application web.|
|/sites/slots/start/Action|Démarre un emplacement d’application web.|
|/sites/slots/stop/Action|Arrête un emplacement d’application web.|
|/sites/slots/slotsswap/Action|Permute des emplacements de déploiement d’application web.|
|/sites/slots/slotsdiffs/Action|Récupère les différences de configuration entre l’application web et les emplacements.|
|/sites/slots/applySlotConfig/Action|Appliquer la configuration de l’emplacement web application à partir de l’emplacement actuel du toohello emplacement cible.|
|/sites/slots/resetSlotConfig/Action|Réinitialise la configuration d’emplacement de l’application web.|
|/sites/slots/Read|Obtenir les propriétés de hello d’un emplacement de déploiement d’application Web|
|/sites/slots/newpassword/action|Emplacements Newpassword Web Apps.|
|/sites/slots/sync/action|Synchronise les emplacements Web Apps.|
|/sites/slots/operationresults/read|Récupère les résultats de l’opération des emplacements Web Apps.|
|/sites/slots/webjobs/read|Récupère WebJobs des emplacements Web Apps.|
|/sites/slots/backup/write|Met à jour la sauvegarde des emplacements Web Apps.|
|/sites/slots/metricdefinitions/read|Récupère les définitions métriques des emplacements Web Apps.|
|/sites/slots/metrics/read|Récupère les mesures des emplacements Web Apps.|
|/sites/slots/continuouswebjobs/delete|Supprime des tâches web continues dans les emplacements Web Apps.|
|/sites/slots/continuouswebjobs/read|Récupère des tâches web continues dans les emplacements Web Apps.|
|/sites/slots/continuouswebjobs/start/action|Démarre des tâches web continues dans les emplacements Web Apps.|
|/sites/slots/continuouswebjobs/stop/action|Arrête des tâches web continues dans les emplacements Web Apps.|
|/sites/slots/premieraddons/delete|Supprime les modules complémentaires Premier dans les emplacements Web Apps.|
|/sites/slots/premieraddons/read|Récupère les modules complémentaires Premier dans les emplacements Web Apps.|
|/sites/slots/premieraddons/write|Met à jour les modules complémentaires Premier dans les emplacements Web Apps.|
|/sites/slots/triggeredwebjobs/delete|Supprime les tâches web déclenchées dans les emplacements Web Apps.|
|/sites/slots/triggeredwebjobs/read|Récupère les tâches web déclenchées dans les emplacements Web Apps.|
|/sites/slots/triggeredwebjobs/run/action|Exécute les tâches web déclenchées dans les emplacements Web Apps.|
|/sites/slots/hostnamebindings/delete|Supprime les liaisons de nom d’hôte dans les emplacements Web Apps.|
|/sites/slots/hostnamebindings/read|Récupère les liaisons de nom d’hôte des emplacements Web Apps.|
|/sites/slots/hostnamebindings/write|Met à jour les liaisons de nom d’hôte des emplacements Web Apps.|
|/sites/slots/phplogging/read|Récupère Phplogging des emplacements Web Apps.|
|/sites/slots/virtualnetworkconnections/delete|Supprime les connexions de réseau virtuel dans les emplacements Web Apps.|
|/sites/slots/virtualnetworkconnections/read|Récupère les connexions de réseau virtuel dans les emplacements Web Apps.|
|/sites/slots/virtualnetworkconnections/write|Met à jour les connexions de réseau virtuel dans les emplacements Web Apps.|
|/sites/slots/virtualnetworkconnections/gateways/write|Met à jour les passerelles de connexions de réseau virtuel dans les emplacements Web Apps.|
|/sites/slots/usages/read|Récupère les utilisations des emplacements Web Apps.|
|/sites/slots/hybridconnection/delete|Supprime une connexion hybride dans les emplacements Web Apps.|
|/sites/slots/hybridconnection/read|Récupère une connexion hybride dans les emplacements Web Apps.|
|/sites/slots/hybridconnection/write|Met à jour une connexion hybride dans les emplacements Web Apps.|
|/sites/slots/config/Read|Récupère les paramètres de configuration de l’emplacement d’application web.|
|/sites/slots/config/list/Action|Répertorie les paramètres sensibles de sécurité de l’emplacement d’application web, tels que les informations d’identification de publication, les paramètres d’application et les chaînes de connexion.|
|/sites/slots/config/Write|Met à jour les paramètres de configuration de l’emplacement d’application web.|
|/sites/slots/config/delete|Supprime la configuration des emplacements Web Apps.|
|/sites/slots/instances/read|Récupère les instances des emplacements Web Apps.|
|/sites/slots/instances/processes/read|Récupère les processus des instances des emplacements Web Apps.|
|/sites/slots/instances/deployments/read|Récupère les déploiements des instances des emplacements Web Apps.|
|/sites/slots/sourcecontrols/Read|Récupère les paramètres de configuration du contrôle de code source de l’emplacement d’application Web.|
|/sites/slots/sourcecontrols/Write|Met à jour les paramètres de configuration du contrôle de code source de l’emplacement d’application web.|
|/sites/slots/sourcecontrols/Delete|Supprime les paramètres de configuration du contrôle de code source de l’emplacement d’application web.|
|/sites/slots/restore/read|Récupère la restauration des emplacements Web Apps.|
|/sites/slots/analyzecustomhostname/read|Récupère le nom d’hôte personnalisé d’analyse des emplacements Web Apps.|
|/sites/slots/backups/Read|Obtenir les propriétés hello de sauvegarde d’un emplacement applications web|
|/sites/slots/backups/list/action|Répertorie les sauvegardes des emplacements Web Apps.|
|/sites/slots/backups/restore/action|Restaure les sauvegardes des emplacements Web Apps.|
|/sites/slots/deployments/delete|Supprime les déploiements des emplacements Web Apps.|
|/sites/slots/deployments/read|Récupère les déploiements des emplacements Web Apps.|
|/sites/slots/deployments/write|Met à jour les déploiements des emplacements Web Apps.|
|/sites/slots/deployments/log/read|Récupère le journal des déploiements des emplacements Web Apps.|
|/sites/hybridconnection/delete|Supprime une connexion hybride Web Apps.|
|/sites/hybridconnection/read|Récupère une connexion hybride Web Apps.|
|/sites/hybridconnection/write|Met à jour une connexion hybride Web Apps.|
|/sites/recommendationhistory/read|Récupère un historique des recommandations Web Apps.|
|/sites/recommendations/Read|Obtenir la liste hello des recommandations pour l’application web.|
|/sites/recommendations/disable/action|Désactive les recommandations des applications web.|
|/sites/config/Read|Récupère les paramètres de configuration des applications web.|
|/sites/config/list/Action|Répertorie les paramètres sensibles de sécurité d’application web, tels que les informations d’identification de publication, les paramètres d’application et les chaînes de connexion.|
|/sites/config/Write|Met à jour les paramètres de configuration d’application web.|
|/sites/config/delete|Supprime la configuration de Web Apps.|
|/sites/instances/read|Récupère des instances Web Apps.|
|/sites/instances/processes/delete|Supprime les processus des instances Web Apps.|
|/sites/instances/processes/read|Récupère les processus des instances Web Apps.|
|/sites/instances/deployments/read|Récupère les déploiements des instances Web Apps.|
|/sites/sourcecontrols/Read|Récupère les paramètres de configuration du contrôle de code source d’application web.|
|/sites/sourcecontrols/Write|Met à jour les paramètres de configuration du contrôle de code source d’application web.|
|/sites/sourcecontrols/Delete|Supprime les paramètres de configuration du contrôle de code source d’application web.|
|/sites/restore/read|Récupère la restauration Web Apps.|
|/sites/analyzecustomhostname/read|Analyse le nom d’hôte personnalisé.|
|/sites/backups/Read|Obtenir les propriétés hello de sauvegarde d’une application web|
|/sites/backups/list/action|Répertorie les sauvegardes Web Apps.|
|/sites/backups/restore/action|Restaure les sauvegardes Web Apps.|
|/sites/snapshots/read|Récupère les captures instantanées de Web Apps.|
|/sites/functions/delete|Supprime les fonctions Web Apps.|
|/sites/functions/listsecrets/action|Répertorie les fonctions Web Apps des clés secrètes.|
|/sites/functions/read|Récupère les fonctions Web Apps.|
|/sites/functions/write|Met à jour les fonctions Web Apps.|
|/sites/deployments/delete|Supprime les déploiements de Web Apps.|
|/sites/deployments/read|Récupère les déploiements de Web Apps.|
|/sites/deployments/write|Met à jour les déploiements de Web Apps.|
|/sites/deployments/log/read|Récupère le journal des déploiements de Web Apps.|
|/sites/diagnostics/read|Récupère les diagnostics de Web Apps.|
|/sites/diagnostics/workerprocessrecycle/read|Récupère le recyclage du processus Worker des diagnostics Web Apps.|
|/sites/diagnostics/workeravailability/read|Récupère la disponibilité Worker des diagnostics Web Apps.|
|/sites/diagnostics/runtimeavailability/read|Récupère la disponibilité d’exécution des diagnostics Web Apps.|
|/sites/diagnostics/cpuanalysis/read|Récupère l’analyse du processeur dans les diagnostics de Web Apps.|
|/sites/diagnostics/servicehealth/read|Récupère l’état du service dans les diagnostics de Web Apps.|
|/sites/diagnostics/frebanalysis/read|Récupère l’analyse FREB dans les diagnostics de Web Apps.|
|/availablestacks/read|Récupère les piles disponibles.|
|/isusernameavailable/read|Vérifie si le nom d’utilisateur est disponible.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Read|Obtenir la liste de hello d’API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Write|Ajoute une nouvelle API ou en met une à jour.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/Delete|Supprime une API existante.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Read|Obtenir la liste de hello de connexions.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Write|Enregistre une nouvelle connexion ou en met une à jour.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/Delete|Supprime une connexion existante.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Read|Lit ConnectionAcls.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Write|Ajout ou met à jour ConnectionAcl.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connections/connectionAcls/Delete|Supprime ConnectionAcl.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/connectionAcls/Read|Lit ConnectionAcls pour l’API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Read|Lit ConnectionAcls.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Write|Crée ou met à jour les listes de contrôle d’accès d’API.|
|/Microsoft.Web/apiManagementAccounts/<br>apis/apiAcls/Delete|Supprime les listes de contrôle d’accès d’API.|
|/serverfarms/Read|Obtenir les propriétés de hello sur un Plan App Service|
|/serverfarms/Write|Crée un plan App Service ou en met un à jour.|
|/serverfarms/Delete|Supprimer un plan App Service existant|
|/serverfarms/restartSites/Action|Redémarre toutes les applications web d’un plan App Service.|
|/serverfarms/operationresults/read|Récupère les résultats de l’opération des plans App Service.|
|/serverfarms/capabilities/read|Récupère les fonctionnalités des plans App Service.|
|/serverfarms/metricdefinitions/read|Récupère les définitions métriques des plans App Service.|
|/serverfarms/metrics/read|Récupère les mesures des plans App Service.|
|/serverfarms/hybridconnectionplanlimits/read|Récupère les limites de plan de connexion hybride des plans App Service.|
|/serverfarms/virtualnetworkconnections/read|Récupère les connexions de réseau virtuel des plans App Service.|
|/serverfarms/virtualnetworkconnections/routes/delete|Supprime les itinéraires des connexions de réseau virtuel des plans App Service.|
|/serverfarms/virtualnetworkconnections/routes/read|Récupère les itinéraires des connexions de réseau virtuel des plans App Service.|
|/serverfarms/virtualnetworkconnections/routes/write|Met à jour les itinéraires des connexions de réseau virtuel des plans App Service.|
|/serverfarms/virtualnetworkconnections/gateways/write|Met à jour les passerelles de connexions de réseau virtuel des plans App Service.|
|/serverfarms/firstpartyapps/settings/delete|Supprime les paramètres des applications principales des plans App Service.|
|/serverfarms/firstpartyapps/settings/read|Récupère les paramètres des applications principales des plans App Service.|
|/serverfarms/firstpartyapps/settings/write|Met à jour les paramètres des applications principales des plans App Service.|
|/serverfarms/sites/read|Récupère les applications web des plans App Service.|
|/serverfarms/workers/reboot/action|Redémarre les Workers des plans App Service.|
|/serverfarms/hybridconnectionrelays/read|Récupère les relais de connexion hybride des plans App Service.|
|/serverfarms/skus/read|Récupère les références des plans App Service.|
|/serverfarms/usages/read|Récupère les usages des plans App Service.|
|/serverfarms/hybridconnectionnamespaces/relays/sites/read|Récupère les applications web des relais d’espace de noms de connexion hybride des plans App Service.|
|/ishostnameavailable/read|Vérifie si le nom d’hôte est disponible.|
|/connectionGateways/Read|Obtenir la liste de hello des passerelles de connexion.|
|/connectionGateways/Write|Crée ou met à jour une passerelle de connexion.|
|/connectionGateways/Delete|Supprime une passerelle de connexion.|
|/connectionGateways/Join/Action|Joint une passerelle de connexion.|
|/classicmobileservices/read|Récupère Classic Mobile Services.|
|/skus/read|Récupère des références.|
|/certificates/Read|Obtenir la liste de hello de certificats.|
|/certificates/Write|Ajoute un nouveau certificat ou en met un à jour.|
|/certificates/Delete|Supprime un certificat existant.|
|/operations/read|Récupère les opérations.|
|/recommendations/Read|Obtenir la liste hello des recommandations pour les abonnements.|
|/ishostingenvironmentnameavailable/read|Récupère des éléments si le nom de l’environnement d’hébergement est disponible.|
|/apiManagementAccounts/Read|Obtenir la liste de hello de ApiManagementAccounts.|
|/apiManagementAccounts/Write|Ajoute un nouveau compte ApiManagementAccount ou en met un à jour.|
|/apiManagementAccounts/Delete|Supprime un compte ApiManagementAccount existant.|
|/apiManagementAccounts/connectionAcls/Read|Obtenir la liste de hello des ACL de connexion.|
|/apiManagementAccounts/apiAcls/Read|Lit ConnectionAcls.|
|/connections/Read|Obtenir la liste de hello de connexions.|
|/connections/Write|Crée ou met à jour une connexion.|
|/connections/Delete|Supprime une connexion.|
|/connections/Join/Action|Joint une connexion.|
|/connections/confirmconsentcode/action|Vérifie le code de consentement des connexions.|
|/connections/listconsentlinks/action|Répertorie les liens de consentement pour les connexions.|
|/deploymentlocations/read|Récupère les emplacements de déploiement.|
|/sourcecontrols/read|Récupère les contrôles de code source.|
|/sourcecontrols/write|Met à jour les contrôles de code source.|
|/managedhostingenvironments/read|Récupère les environnements d’hébergement géré.|
|/managedhostingenvironments/sites/read|Récupère les applications web des environnements d’hébergement géré.|
|/managedhostingenvironments/serverfarms/read|Récupère les plans App Service des environnements d’hébergement géré.|
|/locations/managedapis/read|Récupère les API managées des emplacements.|
|/locations/apioperations/read|Récupère les opérations API d’emplacements.|
|/locations/connectiongatewayinstallations/read|Récupère les installations de la passerelle de connexion des emplacements.|
|/listSitesAssignedToHostName/Read|Obtenir les noms de sites affectés toohostname.|

## <a name="next-steps"></a>Étapes suivantes

- Découvrez comment trop[créer un rôle personnalisé](role-based-access-control-custom-roles.md).

- Hello de révision [générées dans les rôles RBAC](role-based-access-built-in-roles.md).

- Découvrez comment toomanage aux affectations [par l’utilisateur](role-based-access-control-manage-assignments.md) ou [par ressource](role-based-access-control-configure.md) 
