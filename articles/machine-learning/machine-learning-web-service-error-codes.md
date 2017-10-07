---
title: "codes d’erreur Machine Learning REST API aaaAzure | Documents Microsoft"
description: "Ces codes d’erreur peuvent être renvoyés par une opération effectuée sur un service web Azure Machine Learning."
keywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 0923074b-3728-439d-a1b8-8a7245e39be4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 11/16/2016
ms.author: garye
ms.openlocfilehash: 9495c8ef16e684d3c8978bcd11747cf95227b091
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-rest-api-error-codes"></a>Codes d’erreur de l’API REST Azure Machine Learning
 
Hello codes d’erreur suivants peuvent être retournés par une opération sur un service web Azure Machine Learning.
 
## <a name="badargument-http-status-code-400"></a>BadArgument (code d’état HTTP :  400)
 
Argument non valide fourni.
 
Cette classe d’erreurs indique qu’un des arguments fournis est non valide. Cela peut être un emplacement de toosomething de stockage Azure passé le service web de toohello ou les informations d’identification. Regardez le champ « code d’erreur » hello toodiagnose de section « Détails » hello argument spécifique qui n’est pas valide.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| BadParameterValue | valeur de paramètre Hello ne satisfait pas la règle de paramètre hello sur le paramètre hello |
| BadSubscriptionId | l’abonnement Hello Id tooscore utilisé n’est pas hello existe une dans la ressource de hello |
| BadVersionCall | Paramètre de version non valide a été passé au cours de l’appel d’API de hello : {0}. Vérification hello API page pour passer la version correcte de hello d’aide, puis réessayez. |
| BatchJobInputsNotSpecified | Hello suivant que les entrées requises n’ont pas été spécifié avec la demande de hello : {0}. Vérifiez que l’ensemble des données d’entrées sont spécifiées, puis réessayez. |
| BatchJobInputsTooManySpecified | demande de Hello spécifié plus d’entrées que défini dans le service hello. Liste des entrées acceptées : {0}. Vérifiez que toutes les données d’entrée sont spécifiées correctement, puis réessayez. |
| BlobNameTooLong | Le chemin d’accès au stockage Blob Azure fourni pour les résultats de diagnostics est trop long : {0}. Raccourcissez le chemin d’accès de hello, puis réessayez. |
| BlobNotFound | Impossible de tooaccess hello fourni des objets blob Azure - {0}.  Message d’erreur Azure : {1}. |
| ContainerIsEmpty | Aucun nom de conteneur de stockage Azure n’a été fourni. Fournissez un nom de conteneur valide, puis réessayez. |
| ContainerSegmentInvalid | Nom du conteneur non valide. Fournissez un nom de conteneur valide, puis réessayez. |
| ContainerValidationFailed | La validation du conteneur d’objets blob a été mises en échec avec cette erreur : {0}. |
| DataTypeNotSupported | Le type de données fourni n’est pas pris en charge. Fournissez un type de données valide, puis réessayez. |
| DuplicateInputInBatchCall | requête de lots Hello n’est pas valide. Impossible de spécifier à la fois unique et multiple entrée à hello même temps. Supprimer un de ces éléments à partir de la demande de hello, puis réessayez. |
| ExpiryTimeInThePast | Délai d’expiration fourni est Bonjour passées : {0}. FOurnissez une heure d’expiration postérieure en heure UTC, puis réessayez. toonever expirent, vous définissez tooNULL d’heure d’expiration. |
| IncompleteSettings | Les paramètres de diagnostic sont incomplets. |
| InputBlobRelativeLocationInvalid | Aucun nom d’objet blob de stockage Azure fourni. Fournissez un nom d’objet blob valide, puis réessayez. |
| InvalidBlob | Spécification blob non valide pour l’objet blob : {0}. Assurez-vous du caractère approprié de cette spécification de chaîne de connexion/chemin d’accès relatif ou jeton SAS, puis réessayez. |
| InvalidBlobConnectionString | Hello la chaîne de connexion spécifiée pour un des objets BLOB d’entrée/sortie de hello n’est pas valide : {0}. Corrigez ce problème, puis réessayez. |
| InvalidBlobExtension | référence d’objet blob de Hello : {0} a une extension de fichier non valide ou manquant. Les extensions de fichier prises en charge pour ce type de sortie sont les suivantes : "{1}". |
| InvalidInputNames | Service non valide entrée nom (s) spécifié dans la demande de hello : {0}. Veuillez mapper les entrées de service correcte toohello hello des données d’entrée, puis réessayez. |
| InvalidOutputOverrideName | Nom de remplacement de sortie non valide : {0}. service de Hello n’a pas un nœud de sortie portant ce nom. Passez dans un toooverride de nom de nœud de sortie correcte (respect de la casse s’applique). |
| InvalidQueryParameter | Paramètre de requête non valide '{0}'. {1} |
| MissingInputBlobInformation | Informations manquantes sur l’objet blob de stockage Azure. Fournissez une chaîne de connexion valide et un chemin d’accès relatif ou un URI, puis réessayez. |
| MissingJobId | Aucun ID de travail fourni. Un travail de l’Id est retourné lorsqu’une tâche a été soumise pour hello première fois. Vérifiez que hello Id du travail est correct et réessayez. |
| MissingKeys | Aucune clé fournie, ou les clés primaire ou secondaire ne sont pas fournies. |
| MissingModelPackage | Aucun ID de package de modèle ou package de modèle fourni. Fournissez un ID de package de modèle ou un package de modèle valide, puis réessayez. |
| MissingOutputOverrideSpecification | demande de Hello manque de spécification d’objet blob hello pour la substitution de sortie {0}. Spécifiez un emplacement de l’objet blob valide avec la demande de hello, ou supprimez la spécification de sortie de hello si aucun emplacement de remplacement n’est souhaitée. |
| MissingRequestInput | service web de Hello attend une entrée, mais aucune entrée n’a été fournie. Vérifiez les entrées valides sont fournies en fonction de hello publié d’entrée des ports dans le modèle de hello et recommencez l’opération. |
| MissingRequiredGlobalParameters | Les paramètres requis de service web ne sont pas tous fournis. Vérifiez que hello paramètre (s) attendu pour hello un ou plusieurs modules sont corrects et réessayez. |
| MissingRequiredOutputOverrides | Lors de l’appel d’un point de terminaison de service chiffré dans qu'il est obligatoire toopass sortie remplacements pour les sorties du service du hello. Remplacements manquants à cet horodatage pour ces sorties : {0} |
| MissingWebServiceGroupId | Aucun ID de groupe de service web fourni. Fournissez un ID valide de groupe de service web, puis réessayez. |
| MissingWebServiceId | Aucun ID de service web fourni. Fournissez un ID valide de service web, puis réessayez. |
| MissingWebServicePackage | Aucun package de service web fourni. Fournissez un package valide de service web, puis réessayez. |
| MissingWorkspaceId | Aucun ID d’espace de travail fourni. Fournissez un ID valide d’espace de travail, puis réessayez. |
| ModelConfigurationInvalid | Configuration de modèle non valide dans le package de modèle hello. Vérifiez les configuration de modèle hello contient la définition de points de terminaison de sortie, point de terminaison erreur std, et std point de terminaison et recommencez. |
| ModelPackageIdInvalid | ID non valide de package de modèle. Vérifiez que ce package de modèle hello Id est correct, puis réessayez. |
| RequestBodyInvalid | Aucun corps de la requête fournie ou une erreur lors de la désérialisation du corps de la demande hello. |
| RequestIsEmpty | Aucune requête fournie. Fournissez une requête valide, puis réessayez. |
| UnexpectedParameter | Paramètres inattendus requis. Vérifiez que tous les noms de paramètres sont correctement orthographiés, que seuls les paramètres attendus sont transmis, puis réessayez. |
| UnknownError | Erreur inconnue. |
| UserParameterInvalid | {0} |
| WebServiceConcurrentRequestRequirementInvalid | Impossible de modifier la configuration requise des requêtes simultanées pour le service web {0}. |
| WebServiceIdInvalid | L’ID de service web fourni n’est pas valide. L’ID du service web doit être une valeur GUID valide. |
| WebServiceTooManyConcurrentRequestRequirement | Impossible de définir toomore d’exigence de demandes simultanées à {0}. |
| WebServiceTypeInvalid | Le type du service web fourni n’est pas valide. Vérifiez le type de service web valide hello est correct et réessayez. Types valides de service web : {0}. |
 
## <a name="baduserargument-http-status-code-400"></a>BadUserArgument (code d’état HTTP : 400)
 
L’argument utilisateur fourni n’est pas valide.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| InputMismatchError | Les données d’entrée ne correspondent pas au schéma du port d’entrée. |
| InputParseError | L’analyse du vecteur d’entrée a été mise en échec.  Vérifiez le vecteur d’entrée de hello comporte un nombre correct de hello de colonnes et les types de données.  Informations supplémentaires : {0}. |
| MissingRequiredGlobalParameters | Paramètre (s) attendu par le service web hello est manquants. Vérifiez que tous les paramètres requis de hello attendus par le service web hello sont corrects, puis réessayez. |
| UnexpectedParameter | Vérifiez seulement hello requis de paramètres attendus par le service web hello sont passés et réessayez. |
| UserParameterInvalid | {0} |
 
## <a name="invalidoperation-http-status-code-400"></a>InvalidOperation (code d’état HTTP : 400)
 
demande de Hello n’est pas valide dans le contexte actuel de hello.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| CannotStartJob | tâche de Hello ne peut pas être démarrée, car il est en état de {0}. |
| IncompatibleModel | modèle de Hello est incompatible avec la version de la demande hello. version de la demande Hello prend uniquement en charge les modèles de sortie de table de données unique. |
| MultipleInputsNotAllowed | modèle de Hello n’autorise pas plusieurs entrées. |
 
## <a name="libraryexecutionerror-http-status-code-400"></a>LibraryExecutionError (code d’état HTTP : 400)
 
L’exécution du module a rencontré une erreur de bibliothèque interne.
 
 
## <a name="moduleexecutionerror-http-status-code-400"></a>ModuleExecutionError (code d’état HTTP : 400)
 
L’exécution du module a rencontré une erreur.
 
 
## <a name="webservicepackageerror-http-status-code-400"></a>WebServicePackageError (code d’état HTTP : 400)
 
Le package du service web n’est pas valide. Vérifiez le package de service web hello fourni est correct et réessayez.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| FormatError | package de service web Hello est mal formée. Détails : {0} |
| RuntimesError | graphique de package du service web Hello n’est pas valide. Détails : {0} |
| ValidationError | graphique de package du service web Hello n’est pas valide. Détails : {0} |
 
## <a name="unauthorized-http-status-code-401"></a>Unauthorized (code d'état HTTP : 401)
 
Demande est les ressources tooaccess non autorisé.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| AdminRequestUnauthorized | Non autorisé |
| ManagementRequestUnauthorized | Non autorisé |
| ScoreRequestUnauthorized | Informations d’identification non valides fournies. |
 
## <a name="notfound-http-status-code-404"></a>NotFound (code d’état HTTP : 404)
 
La ressource est introuvable.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| ModelPackageNotFound | Le package de modèle est introuvable. Vérifiez le package de modèle hello Id est correct et réessayez. |
| WebServiceIdNotFoundInWorkspace | Le service web de cet espace de travail est introuvable. Il existe une incompatibilité entre hello webServiceId et hello Id_espace_de_travail. Vérifiez que le service web de hello fourni fait partie de l’espace de travail hello, puis réessayez. |
| WebServiceNotFound | Le service web est introuvable. Vérifier le hello web service Id est correct et réessayez. |
| WorkspaceNotFound | L’espace de travail est introuvable. Vérifiez l’espace de travail hello Id est correct et réessayez. |
 
## <a name="requesttimeout-http-status-code-408"></a>RequestTimeout (code d’état HTTP : 408)
 
opération de Hello n’a pas pu se terminer dans hello autorisé de temps.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| RequestCanceled | Demande a été annulée par le client de hello. |
| ScoreRequestTimeout | La requête d’exécution a expiré. |
 
## <a name="conflict-http-status-code-409"></a>Conflit (code d’état HTTP : 409)
 
La ressource existe déjà.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| ModelOutputMetadataMismatch | Le nom du paramètre de sortie n’est pas valide. Essayez d’utiliser des colonnes de toorename module hello métadonnées éditeur, puis réessayez. |
 
## <a name="memoryquotaviolation-http-status-code-413"></a>MemoryQuotaViolation (code d’état HTTP : 413)
 
modèle de Hello avait dépassé le quota de mémoire affecté tooit hello.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| OutOfMemoryLimit | modèle de Hello consommé plus de mémoire a été affectés pour celle-ci. La mémoire maximale autorisée pour le modèle de hello est {0} Mo. Vérifiez que votre modèle ne présente pas de problèmes. |
 
## <a name="internalerror-http-status-code-500"></a>InternalError (code d’état HTTP : 500)
 
L’exécution a rencontré une erreur interne.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| AdminAuthenticationFailed |  |
| BackendArgumentError |  |
| BackendBadRequest |  |
| ClusterConfigBlobMisconfigured |  |
| ContainerProcessTerminatedWithSystemError | processus de conteneur Hello est arrêté anormalement avec l’erreur système |
| ContainerProcessTerminatedWithUnknownError | processus de conteneur Hello est arrêté anormalement avec une erreur inconnue |
| ContainerValidationFailed | La validation du conteneur d’objets blob a été mises en échec avec cette erreur : {0}. |
| DeleteWebServiceResourceFailed |  |
| ExceptionDeserializationError |  |
| FailedGettingApiDocument |  |
| FailedStoringWebService |  |
| InvalidMemoryConfiguration | InvalidMemoryConfiguration, ConfigValue: {0} |
| InvalidResourceCacheConfiguration |  |
| InvalidResourceDownloadConfiguration |  |
| InvalidWebServiceResources |  |
| MissingTaskInstance | Aucun argument fourni. Vérifiez que les arguments valides sont transmis, puis réessayez. |
| ModelPackageInvalid |  |
| ModuleExecutionFailed |  |
| ModuleLoadFailed |  |
| ModuleObjectCloneFailed |  |
| OutputConversionFailed |  |
| PortDataTypeNotSupported | L’ID de port ={0} présente un type de données non pris en charge : {1}. |
| ResourceDownload |  |
| ResourceLoadFailed |  |
| ServiceUrisNotFound |  |
| SwaggerGeneration | Le génération de l’interface utilisateur Swagger a échoué, Details: {0} |
| UnexpectedScoreStatus |  |
| UnknownBackendErrorResponse |  |
| UnknownError |  |
| UnknownJobStatusCode | Code inconnu d’état du travail {0}. |
| UnknownModuleError |  |
| UpdateWebServiceResourceFailed |  |
| WebServiceGroupNotFound |  |
| WebServicePackageInvalid | InvalidWebServicePackage, Details : {0} |
| WorkerAuthorizationFailed |  |
| WorkerUnreachable |  |
 
## <a name="internalerrorsystemlowonmemory-http-status-code-500"></a>InternalErrorSystemLowOnMemory (code d’état HTTP : 500)
 
L’exécution a rencontré une erreur interne. La capacité de mémoire du système est faible. Réessayez.
 
 
## <a name="modelpackageformaterror-http-status-code-500"></a>ModelPackageFormatError (code d’état HTTP : 500)
 
Le package du modèle n’est pas valide. Vérifiez le package de modèle hello fourni est correct et réessayez.
 
 
## <a name="webservicepackageinternalerror-http-status-code-500"></a>WebServicePackageInternalError (code d’état HTTP : 500)
 
Le package du service web n’est pas valide. Vérifiez que hello web fourni est correct, puis réessayez.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| ModuleError | graphique de package du service web Hello n’est pas valide. Détails : {0} |
 
## <a name="initializingcontainers-http-status-code-503"></a>InitializingContainers (code d’état HTTP : 503)
 
Impossible d’exécuter la demande de Hello comme hello conteneurs sont en cours d’initialisation.
 
 
## <a name="serviceunavailable-http-status-code-503"></a>ServiceUnavailable (code d’état HTTP : 503)
 
Le service est temporairement indisponible.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| NoMoreResources | Aucune ressource n’est disponible pour la requête. |
| RequestThrottled | La requête a été limitée pour le point de terminaison {0}. d’accès concurrentiel maximal de Hello pour le point de terminaison hello est {{1}. |
| TooManyConcurrentRequests | Un nombre trop important de requêtes simultanées ont été envoyées. |
| TooManyHostsBeingInitialized | Hello de trop d’hôtes en cours d’initialisation en même temps. Envisagez de limiter/de réessayer. |
| TooManyHostsBeingInitializedPerModel | Hello de trop d’hôtes en cours d’initialisation en même temps. Envisagez de limiter/de réessayer. |
 
## <a name="gatewaytimeout-http-status-code-504"></a>GatewayTimeout (code d’état HTTP : 504)
 
opération de Hello n’a pas pu se terminer dans hello autorisé de temps.
 
| Code d'erreur | Message utilisateur |
| ---------- |--------------|
| BackendInitializationTimeout | l’initialisation du service web Hello n’a pas pu se terminer dans hello autorisé de temps. |
| BackendScoreTimeout | exécution de la demande Hello web service n’a pas pu être terminer dans hello autorisé de temps. |
 
