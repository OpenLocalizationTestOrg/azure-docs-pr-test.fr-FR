---
title: "Implémenter une récupération d’urgence à l’aide d’une sauvegarde et d’une restauration dans Gestion des API Azure | Microsoft Docs"
description: "Apprenez à utiliser la sauvegarde et la restauration pour effectuer une récupération d'urgence dans Gestion des API Azure."
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
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="06f9e-103">Comment implémenter une récupération d'urgence à l'aide d'une sauvegarde de service et la récupérer dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="06f9e-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="06f9e-104">En choisissant de publier et de gérer vos API via la Gestion des API Azure, vous bénéficiez de nombreuses fonctionnalités de tolérance de panne et d'infrastructure que vous auriez à concevoir, implémenter et gérer sans ce service.</span><span class="sxs-lookup"><span data-stu-id="06f9e-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="06f9e-105">La plateforme Azure permet de limiter une grande partie des risques de défaillance à moindres frais.</span><span class="sxs-lookup"><span data-stu-id="06f9e-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="06f9e-106">Pour récupérer à la suite de problèmes de disponibilité affectant la région où votre service Gestion des API est hébergé, vous devez être prêt à reconstituer votre service dans une autre région à tout moment.</span><span class="sxs-lookup"><span data-stu-id="06f9e-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="06f9e-107">En fonction de vos objectifs de disponibilité et de temps de récupération, vous pouvez réserver un service de sauvegarde dans une ou plusieurs régions et tenter de maintenir la synchronisation de leur configuration et de leur contenu avec le service actif.</span><span class="sxs-lookup"><span data-stu-id="06f9e-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="06f9e-108">La fonctionnalité de sauvegarde et de récupération de service fournit le bloc de construction nécessaire pour implémenter votre stratégie de récupération d'urgence.</span><span class="sxs-lookup"><span data-stu-id="06f9e-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="06f9e-109">Ce guide montre comment authentifier des demandes Azure Resource Manager et comment sauvegarder et restaurer vos instances de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="06f9e-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="06f9e-110">Le processus de sauvegarde et de restauration d'une instance de service de gestion des API pour la récupération d'urgence permet également de répliquer les instances de service de gestion des API dans les scénarios intermédiaires.</span><span class="sxs-lookup"><span data-stu-id="06f9e-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="06f9e-111">À noter que chaque sauvegarde expire au bout de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="06f9e-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="06f9e-112">Si vous essayez de restaurer une sauvegarde après l'expiration de la période de 30 jours, la restauration échoue avec un message `Cannot restore: backup expired`.</span><span class="sxs-lookup"><span data-stu-id="06f9e-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="06f9e-113">Demandes d'authentification Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="06f9e-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="06f9e-114">L'API REST pour la sauvegarde et la restauration utilise Azure Resource Manager et dispose d'un autre mécanisme d'authentification que pour les API REST pour la gestion de vos entités de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="06f9e-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="06f9e-115">Les étapes de cette section décrivent comment authentifier les requêtes Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="06f9e-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="06f9e-116">Pour plus d’informations, consultez [Demandes d'authentification Azure Resource Manager](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="06f9e-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="06f9e-117">Toutes les tâches que vous effectuez sur les ressources à l'aide d’Azure Resource Manager doivent être authentifiées avec Azure Active Directory en procédant comme suit.</span><span class="sxs-lookup"><span data-stu-id="06f9e-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="06f9e-118">Ajoutez une application au locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06f9e-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="06f9e-119">Définissez les autorisations pour l'application que vous avez ajoutée.</span><span class="sxs-lookup"><span data-stu-id="06f9e-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="06f9e-120">Obtenez le jeton d'authentification des demandes pour Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="06f9e-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="06f9e-121">La première étape consiste à créer une application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06f9e-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="06f9e-122">Connectez-vous au [portail Azure Classic](http://manage.windowsazure.com/) à l’aide de l’abonnement qui contient votre instance de service Gestion des API et accédez à l’onglet **Applications** pour votre annuaire Azure Active Directory par défaut.</span><span class="sxs-lookup"><span data-stu-id="06f9e-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="06f9e-123">Si le répertoire par défaut de Azure Active Directory n'est pas visible sur votre compte, contactez l'administrateur de l'abonnement Azure pour accorder les autorisations requises de votre compte.</span><span class="sxs-lookup"><span data-stu-id="06f9e-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![Création d’une application Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="06f9e-125">Cliquez sur **Ajouter**, **Ajouter une application développée par mon organisation**, puis choisissez **Application cliente native**.</span><span class="sxs-lookup"><span data-stu-id="06f9e-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="06f9e-126">Saisissez un nom descriptif puis cliquez sur la flèche Suivant.</span><span class="sxs-lookup"><span data-stu-id="06f9e-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="06f9e-127">Entrez une URL d'espace réservé telle que `http://resources` pour l’ **URI de redirection**, étant donné qu’il s’agit d’un champ obligatoire, mais la valeur ne sera pas utilisée par la suite.</span><span class="sxs-lookup"><span data-stu-id="06f9e-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="06f9e-128">Cliquez sur la case à cocher pour enregistrer l'application.</span><span class="sxs-lookup"><span data-stu-id="06f9e-128">Click the check box to save the application.</span></span>

<span data-ttu-id="06f9e-129">Une fois l’application enregistrée, cliquez sur **Configurer**, faites défiler la page vers le bas jusqu’à la section **Autorisations à d’autres applications** et cliquez sur **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="06f9e-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![Ajout d’autorisations][api-management-aad-permissions-add]

<span data-ttu-id="06f9e-131">Sélectionnez **Windows** **API de gestion des services Azure** et cliquez sur la case à cocher pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="06f9e-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![Ajout d’autorisations][api-management-aad-permissions]

<span data-ttu-id="06f9e-133">Cliquez sur **Autorisations déléguées** à côté de la nouvelle application **Windows**, **API de gestion des services Azure**, cochez la case **Accès à la gestion des services Azure (aperçu)**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="06f9e-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Ajout d’autorisations][api-management-aad-delegated-permissions]

<span data-ttu-id="06f9e-135">Avant d'appeler les API qui génèrent la sauvegarde et permettent la restauration, il est nécessaire d’obtenir un jeton.</span><span class="sxs-lookup"><span data-stu-id="06f9e-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="06f9e-136">L'exemple suivant utilise le package nuget [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) pour récupérer le jeton.</span><span class="sxs-lookup"><span data-stu-id="06f9e-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="06f9e-137">Remplacez `{tentand id}`, `{application id}`, et `{redirect uri}` en suivant les instructions suivantes.</span><span class="sxs-lookup"><span data-stu-id="06f9e-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="06f9e-138">Remplacez `{tenant id}` avec l'ID client de l'application Azure Active Directory que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="06f9e-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="06f9e-139">Vous pouvez accéder à l'ID en cliquant sur **Afficher les points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="06f9e-139">You can access the id by clicking **View endpoints**.</span></span>

![Points de terminaison][api-management-aad-default-directory]

![Points de terminaison][api-management-endpoint]

<span data-ttu-id="06f9e-142">Remplacez `{application id}` et `{redirect uri}` à l’aide de l’**ID Client** et l’URL de la section des **URI de redirection** à partir de l’onglet **Configurer** de votre application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="06f9e-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Ressources][api-management-aad-resources]

<span data-ttu-id="06f9e-144">Une fois que les valeurs sont spécifiées, l'exemple de code doit renvoyer un jeton similaire à l'exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="06f9e-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![Jeton][api-management-arm-token]

<span data-ttu-id="06f9e-146">Avant d'appeler les opérations de sauvegarde et de restauration décrites dans les sections suivantes, définissez l'en-tête de demande d'autorisation de votre appel REST.</span><span class="sxs-lookup"><span data-stu-id="06f9e-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="06f9e-147"><a name="step1"> </a>Sauvegarde d’un service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="06f9e-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="06f9e-148">Pour sauvegarder un service Gestion des API, envoyez la demande HTTP suivante :</span><span class="sxs-lookup"><span data-stu-id="06f9e-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="06f9e-149">où :</span><span class="sxs-lookup"><span data-stu-id="06f9e-149">where:</span></span>

* <span data-ttu-id="06f9e-150">`subscriptionId` : ID de l’abonnement qui inclut le service Gestion des API que vous tentez de sauvegarder</span><span class="sxs-lookup"><span data-stu-id="06f9e-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="06f9e-151">`resourceGroupName` : chaîne au format « Api-Default-{service-region} », où `service-region` identifie la région Azure où est hébergé le service Gestion des API que vous tentez de sauvegarder ; par exemple `North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="06f9e-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="06f9e-152">`serviceName` : nom du service Gestion des API que vous tentez de sauvegarder, spécifié au moment de sa création</span><span class="sxs-lookup"><span data-stu-id="06f9e-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="06f9e-153">`api-version` - remplacer par `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="06f9e-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="06f9e-154">Dans le corps de la demande, spécifiez le nom du compte de stockage Azure cible, la clé d’accès, le nom du conteneur d’objets blob et le nom de la sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="06f9e-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="06f9e-155">Définissez la valeur de l’en-tête de la demande `Content-Type` sur `application/json`.</span><span class="sxs-lookup"><span data-stu-id="06f9e-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="06f9e-156">La sauvegarde est une opération de longue durée qui peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="06f9e-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="06f9e-157">Si la demande a réussi et que le processus de sauvegarde a été lancé, vous recevez un code d’état de réponse `202 Accepted` avec un en-tête `Location`.</span><span class="sxs-lookup"><span data-stu-id="06f9e-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="06f9e-158">Envoyez des demandes « GET » à l’URL dans l’en-tête `Location` pour connaître l’état de l’opération.</span><span class="sxs-lookup"><span data-stu-id="06f9e-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="06f9e-159">Lorsque la sauvegarde est en cours, vous continuez à recevoir le code d'état « 202 Accepted ».</span><span class="sxs-lookup"><span data-stu-id="06f9e-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="06f9e-160">Un code de réponse `200 OK` indique que l’opération de sauvegarde a réussi.</span><span class="sxs-lookup"><span data-stu-id="06f9e-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="06f9e-161">Tenez compte des contraintes suivantes lorsque vous faites une demande de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="06f9e-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="06f9e-162">Le **conteneur** spécifié dans le corps de la demande **doit exister**.</span><span class="sxs-lookup"><span data-stu-id="06f9e-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="06f9e-163">Lorsque la sauvegarde est en cours, **vous ne devez tenter aucune opération de gestion des services** telle que la mise à niveau vers une version supérieure/antérieure, la modification d'un nom de domaine, etc.</span><span class="sxs-lookup"><span data-stu-id="06f9e-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="06f9e-164">La restauration d’une **sauvegarde n’est garantie que pendant 30 jours** à partir du moment de sa création.</span><span class="sxs-lookup"><span data-stu-id="06f9e-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="06f9e-165">Les **données d’utilisation** utilisées pour la création des rapports d’analyse **ne sont pas incluses** dans la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="06f9e-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="06f9e-166">Utilisez l’[API REST de Gestion des API Azure][Azure API Management REST API] pour récupérer régulièrement les rapports d’analyse et les conserver en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="06f9e-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="06f9e-167">La fréquence à laquelle vous effectuez les sauvegardes du service affecte votre objectif de point de récupération.</span><span class="sxs-lookup"><span data-stu-id="06f9e-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="06f9e-168">Afin de le réduire au maximum, nous vous conseillons d'implémenter des sauvegardes régulières, ainsi que des sauvegardes à la demande lorsque vous apportez des modifications importantes à votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="06f9e-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="06f9e-169">Les **modifications** de la configuration du service (par ex., API, stratégies, apparence du portail des développeurs) pendant qu’une opération de sauvegarde est en cours **peuvent ne pas être incluses dans la sauvegarde et donc être perdues**.</span><span class="sxs-lookup"><span data-stu-id="06f9e-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="06f9e-170"><a name="step2"> </a>Récupération d’un service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="06f9e-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="06f9e-171">Pour récupérer un service Gestion des API à partir d'une sauvegarde précédemment créée, envoyez la demande HTTP suivante :</span><span class="sxs-lookup"><span data-stu-id="06f9e-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="06f9e-172">où :</span><span class="sxs-lookup"><span data-stu-id="06f9e-172">where:</span></span>

* <span data-ttu-id="06f9e-173">`subscriptionId` : ID de l’abonnement qui inclut le service Gestion des API que vous tentez de récupérer à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="06f9e-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="06f9e-174">`resourceGroupName` : chaîne au format « Api-Default-{service-region} », où `service-region` identifie la région Azure où est hébergé le service Gestion des API que vous tentez de récupérer à partir d’une sauvegarde ; par exemple `North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="06f9e-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="06f9e-175">`serviceName` : nom du service Gestion des API à récupérer, spécifié au moment de sa création</span><span class="sxs-lookup"><span data-stu-id="06f9e-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="06f9e-176">`api-version` - remplacer par `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="06f9e-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="06f9e-177">Dans le corps de la demande, spécifiez l’emplacement du fichier de sauvegarde (c’est-à-dire le nom du compte de stockage Azure), la clé d’accès, le nom du conteneur d’objets blob et le nom de la sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="06f9e-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="06f9e-178">Définissez la valeur de l’en-tête de la demande `Content-Type` sur `application/json`.</span><span class="sxs-lookup"><span data-stu-id="06f9e-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="06f9e-179">La récupération est une opération de longue durée qui peut prendre jusqu'à 30 minutes, voire plus.</span><span class="sxs-lookup"><span data-stu-id="06f9e-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="06f9e-180">Si la demande a réussi et que le processus de récupération a été lancé, vous recevez un code d’état de réponse `202 Accepted` avec un en-tête `Location`.</span><span class="sxs-lookup"><span data-stu-id="06f9e-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="06f9e-181">Envoyez des demandes « GET » à l’URL dans l’en-tête `Location` pour connaître l’état de l’opération.</span><span class="sxs-lookup"><span data-stu-id="06f9e-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="06f9e-182">Lorsque la récupération est en cours, vous continuez à recevoir le code d'état « 202 Accepted ».</span><span class="sxs-lookup"><span data-stu-id="06f9e-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="06f9e-183">Un code de réponse `200 OK` indique que l’opération de récupération a réussi.</span><span class="sxs-lookup"><span data-stu-id="06f9e-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06f9e-184">Le **SKU** du service à restaurer **doit correspondre** à celui du service sauvegardé utilisé pour la restauration.</span><span class="sxs-lookup"><span data-stu-id="06f9e-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="06f9e-185">Les **modifications** de configuration du service (par ex., API, stratégies, apparence du portail des développeurs) pendant qu’une opération de sauvegarde est en cours **peuvent être écrasées**.</span><span class="sxs-lookup"><span data-stu-id="06f9e-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="06f9e-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="06f9e-186">Next steps</span></span>
<span data-ttu-id="06f9e-187">Consultez les blogs Microsoft suivants pour les deux procédures pas à pas différent du processus de sauvegarde et de restauration.</span><span class="sxs-lookup"><span data-stu-id="06f9e-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="06f9e-188">Répliquer des comptes de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="06f9e-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="06f9e-189">Merci à Gisela pour sa contribution à cet article.</span><span class="sxs-lookup"><span data-stu-id="06f9e-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="06f9e-190">Gestion des API Azure : sauvegarde et restauration de la configuration</span><span class="sxs-lookup"><span data-stu-id="06f9e-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="06f9e-191">L'approche détaillée par Stuart ne correspond pas à l'aide officielle mais est très intéressante.</span><span class="sxs-lookup"><span data-stu-id="06f9e-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

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
