---
title: "aaaImplement de récupération d’urgence à l’aide de sauvegarde et de restauration dans la gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toouse sauvegarde et restauration de la récupération d’urgence tooperform dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Comment tooimplement de récupération d’urgence à l’aide du service sauvegarde et la restauration dans la gestion des API Azure
En choisissant toopublish et gérer votre API via la gestion des API Azure vous tirez profit de nombreuses fonctionnalités de l’infrastructure et la tolérance de panne du erreur que vous devriez autrement toodesign, implémenter et gérer. Hello plateforme Azure permet d’atténuer une grande partie de pannes potentielles à moindre coût de hello.

toorecover des problèmes de disponibilité qui affectent la région de hello où votre service de gestion des API est hébergé vous doit être prêt tooreconstitute votre service dans une région différente à tout moment. En fonction de vos objectifs de disponibilité et l’objectif de temps de récupération, vous pouvez souhaitez tooreserve un service de sauvegarde dans une ou plusieurs régions et essayez toomaintain leur contenu synchronisé avec le service actif de hello et configuration. sauvegarde du service Hello et la fonctionnalité de restauration fournit un bloc de construction hello nécessaire pour l’implémentation de votre stratégie de récupération d’urgence.

Ce guide montre comment les demandes tooauthenticate Azure Resource Manager et toobackup et restaurer vos instances de service de gestion des API.

> [!NOTE]
> Hello processus de sauvegarde et restauration d’une instance de service de gestion des API pour la récupération d’urgence peut également être utilisé pour la réplication des instances de service de gestion des API dans les scénarios de mise en lots.
>
> À noter que chaque sauvegarde expire au bout de 30 jours. Si vous essayez de toorestore une sauvegarde après la période d’expiration hello 30 jours a expiré, la restauration de hello échoue avec une `Cannot restore: backup expired` message.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Demandes d'authentification Azure Resource Manager
> [!IMPORTANT]
> Hello API REST pour la sauvegarde et de restauration utilise Azure Resource Manager et présente un mécanisme d’authentification autre que hello API REST pour la gestion de vos entités de gestion des API. étapes de Hello dans cette section décrivent comment les demandes tooauthenticate Azure Resource Manager. Pour plus d’informations, consultez [Demandes d'authentification Azure Resource Manager](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Toutes les tâches de hello que vous effectuez sur les ressources à l’aide de hello Azure Resource Manager doivent être authentifiés auprès d’Azure Active Directory à l’aide de hello comme suit.

* Ajouter un client Azure Active Directory de toohello application.
* Définir des autorisations pour l’application hello que vous avez ajouté.
* Obtenir le jeton de hello pour l’authentification des demandes tooAzure Gestionnaire de ressources.

première étape de Hello est toocreate une application Azure Active Directory. Connectez-vous à hello [portail classique Azure](http://manage.windowsazure.com/) à l’aide d’abonnement hello qui contient votre service de gestion des API d’instance et accédez toohello **Applications** onglet pour votre Azure Active Directory par défaut.

> [!NOTE]
> Si le répertoire de hello Azure Active Directory par défaut n’est pas visible tooyour compte, administrateur de contact hello Hello de toogrant d’abonnement Azure hello requis compte tooyour d’autorisations.

![Création d’une application Azure Active Directory][api-management-add-aad-application]

Cliquez sur **Ajouter**, **Ajouter une application développée par mon organisation**, puis choisissez **Application cliente native**. Entrez un nom descriptif et cliquez sur la flèche suivant de hello. Entrez une URL de l’espace réservé tel que `http://resources` pour hello **URI de redirection**, comme il s’agit d’un champ obligatoire, mais la valeur de hello n’est pas utilisé plus tard. Cliquez sur hello case toosave hello application.

Une fois l’application hello est enregistrée, cliquez sur **configurer**, faites défiler vers le bas toohello **autorisations tooother applications** section, puis cliquez sur **ajouter application**.

![Ajout d’autorisations][api-management-aad-permissions-add]

Sélectionnez **Windows** **API de gestion des services Azure** et cliquez sur l’application hello case à cocher tooadd hello.

![Ajout d’autorisations][api-management-aad-permissions]

Cliquez sur **autorisations déléguées** en regard de hello nouvellement ajouté **Windows** **API de gestion des services Azure** application, la case à cocher hello pour **accéder à Azure Gestion des services (version préliminaire)**, puis cliquez sur **enregistrer**.

![Ajout d’autorisations][api-management-aad-delegated-permissions]

Tooinvoking préalable hello API générer hello sauvegarde et restauration, il s’agit d’un jeton de tooget nécessaire. exemple Hello utilise hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) jeton de nuget package tooretrieve hello.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Remplacez `{tentand id}`, `{application id}`, et `{redirect uri}` à l’aide de hello suivant les instructions.

Remplacez `{tenant id}` avec l’id de client hello Hello application Azure Active Directory que vous venez de créer. Vous pouvez accéder à des id de hello en cliquant sur **afficher les points de terminaison**.

![Points de terminaison][api-management-aad-default-directory]

![Points de terminaison][api-management-endpoint]

Remplacez `{application id}` et `{redirect uri}` à l’aide de hello **Id Client** et hello URL à partir de hello **URI de redirection** section à partir de votre application Azure Active Directory **configurer**  onglet.

![Ressources][api-management-aad-resources]

Une fois que les valeurs hello sont spécifiées, exemple de code hello doit renvoyer un jeton toohello semblable l’exemple suivant.

![Jeton][api-management-arm-token]

Avant d’appeler hello de sauvegarde et de restauration des opérations décrites dans les sections suivantes de hello, définir l’en-tête de demande d’autorisation hello pour votre appel REST.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"></a>Sauvegarde d’un service Gestion des API
tooback d’un hello de problème de service de gestion des API suivant demande HTTP :

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

où :

* `subscriptionId`-id d’abonnement hello contenant le service de gestion des API hello vous essayez de toobackup
* `resourceGroupName`-une chaîne sous forme de hello de « Api - par - défaut {région service} » où `service-region` identifie hello région Azure où hello service Gestion des API que vous essayez toobackup est hébergé, par exemple,`North-Central-US`
* `serviceName`-nom hello Hello service de gestion des API vous effectuez une sauvegarde de spécifiée au moment de sa création de hello
* `api-version` - remplacer par `2014-02-14`

Dans le corps de demande de hello de hello, spécifiez le nom de compte de stockage Azure hello cible, la clé d’accès, nom de conteneur et nom de la sauvegarde :

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

La valeur hello Hello `Content-Type` en-tête de demande trop`application/json`.

Sauvegarde est une longue opération qui peut prendre plusieurs minutes toocomplete.  Si hello demande a abouti et processus de sauvegarde hello a été lancée vous recevrez un `202 Accepted` code d’état de réponse avec un `Location` en-tête.  Vérifiez le 'GET' demande URL toohello Bonjour `Location` toofind en-tête état hello d’opération de hello. Pendant la sauvegarde de hello vous continuerez tooreceive un code d’état « 202 accepté ». Un code de réponse `200 OK` indique la réussite de l’opération de sauvegarde hello.

Veuillez noter hello suivant contraintes lors d’une demande de sauvegarde.

* **Conteneur** spécifié dans le corps de la demande hello **doit exister**.
* Lorsque la sauvegarde est en cours, **vous ne devez tenter aucune opération de gestion des services** telle que la mise à niveau vers une version supérieure/antérieure, la modification d'un nom de domaine, etc.
* Restauration d’un **sauvegarde est garantie uniquement pendant 30 jours** depuis le moment hello de sa création.
* **Les données d’utilisation** utilisé pour créer des rapports d’analytique **n’est pas inclus** dans la sauvegarde de hello. Utilisez [API REST de gestion des API Azure] [ Azure API Management REST API] tooperiodically récupérer des rapports d’analytique en lieu sûr.
* fréquence de Hello avec lequel vous effectuez des sauvegardes de service affectent votre objectif de point de récupération. toominimize il nous vous conseillons de mise en œuvre de sauvegardes régulières, ainsi que d’effectuer des sauvegardes de la demande après avoir établi l’important modifie le service de gestion des API tooyour.
* **Modifications** configuration du service toohello effectuées (par exemple, API, stratégies, apparence portail des développeurs) lors de l’opération de sauvegarde est en cours **ne sont pas inclus dans la sauvegarde de hello et par conséquent ne sera pas conservé**.

## <a name="step2"></a>Récupération d’un service Gestion des API
toorestore un service de gestion des API à partir d’une sauvegarde créée précédemment apporter hello suivant demande HTTP :

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

où :

* `subscriptionId`-id d’abonnement hello contenant le service de gestion des API hello vous restaurez une sauvegarde dans
* `resourceGroupName`-une chaîne sous forme de hello de « Api - par - défaut {région service} » où `service-region` identifie hello région Azure où hello service de gestion des API vous restaurez une sauvegarde dans est hébergé, par exemple,`North-Central-US`
* `serviceName`-nom hello Hello gestion des API du service en cours de restauration dans spécifié lors de sa création hello
* `api-version` - remplacer par `2014-02-14`

Dans le corps de demande de hello de hello, spécifiez l’emplacement du fichier de sauvegarde de hello, par exemple, nom de compte de stockage Azure, la clé d’accès, nom de conteneur et nom de la sauvegarde :

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

La valeur hello Hello `Content-Type` en-tête de demande trop`application/json`.

La restauration est une longue opération qui peut prendre jusqu'à too30 ou de plusieurs minutes toocomplete.  Si la demande de hello a abouti et processus de restauration hello a été lancée vous recevrez un `202 Accepted` code d’état de réponse avec un `Location` en-tête.  Vérifiez le 'GET' demande URL toohello Bonjour `Location` toofind en-tête état hello d’opération de hello. Pendant la restauration de hello vous continuerez code d’état tooreceive « 202 accepté ». Un code de réponse `200 OK` indique la réussite de l’opération de restauration hello.

> [!IMPORTANT]
> **Hello SKU** du service hello restaurée dans **doit correspondre à** hello référence (SKU) de hello sauvegardé de service en cours de restauration.
>
> **Modifications** configuration du service toohello effectuées (par exemple, API, stratégies, apparence portail des développeurs) lors de l’opération de restauration est en cours d’exécution **pourrait être remplacé**.
>
>

## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant blogs Microsoft pour les deux procédures pas à pas différent du processus de sauvegarde/restauration hello.

* [Répliquer des comptes de gestion des API Azure](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * Merci d’avoir tooGisela pour son article toothis de contribution.
* [Gestion des API Azure : sauvegarde et restauration de la configuration](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * approche Hello détaillée par Stuart ne correspond pas aux directives officielles hello, mais il est très intéressant.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
