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
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="6d2e7-103">Comment tooimplement de récupération d’urgence à l’aide du service sauvegarde et la restauration dans la gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="6d2e7-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="6d2e7-104">En choisissant toopublish et gérer votre API via la gestion des API Azure vous tirez profit de nombreuses fonctionnalités de l’infrastructure et la tolérance de panne du erreur que vous devriez autrement toodesign, implémenter et gérer.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="6d2e7-105">Hello plateforme Azure permet d’atténuer une grande partie de pannes potentielles à moindre coût de hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="6d2e7-106">toorecover des problèmes de disponibilité qui affectent la région de hello où votre service de gestion des API est hébergé vous doit être prêt tooreconstitute votre service dans une région différente à tout moment.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="6d2e7-107">En fonction de vos objectifs de disponibilité et l’objectif de temps de récupération, vous pouvez souhaitez tooreserve un service de sauvegarde dans une ou plusieurs régions et essayez toomaintain leur contenu synchronisé avec le service actif de hello et configuration.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="6d2e7-108">sauvegarde du service Hello et la fonctionnalité de restauration fournit un bloc de construction hello nécessaire pour l’implémentation de votre stratégie de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="6d2e7-109">Ce guide montre comment les demandes tooauthenticate Azure Resource Manager et toobackup et restaurer vos instances de service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="6d2e7-110">Hello processus de sauvegarde et restauration d’une instance de service de gestion des API pour la récupération d’urgence peut également être utilisé pour la réplication des instances de service de gestion des API dans les scénarios de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="6d2e7-111">À noter que chaque sauvegarde expire au bout de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="6d2e7-112">Si vous essayez de toorestore une sauvegarde après la période d’expiration hello 30 jours a expiré, la restauration de hello échoue avec une `Cannot restore: backup expired` message.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="6d2e7-113">Demandes d'authentification Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6d2e7-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6d2e7-114">Hello API REST pour la sauvegarde et de restauration utilise Azure Resource Manager et présente un mécanisme d’authentification autre que hello API REST pour la gestion de vos entités de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="6d2e7-115">étapes de Hello dans cette section décrivent comment les demandes tooauthenticate Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="6d2e7-116">Pour plus d’informations, consultez [Demandes d'authentification Azure Resource Manager](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d2e7-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="6d2e7-117">Toutes les tâches de hello que vous effectuez sur les ressources à l’aide de hello Azure Resource Manager doivent être authentifiés auprès d’Azure Active Directory à l’aide de hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="6d2e7-118">Ajouter un client Azure Active Directory de toohello application.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="6d2e7-119">Définir des autorisations pour l’application hello que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="6d2e7-120">Obtenir le jeton de hello pour l’authentification des demandes tooAzure Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="6d2e7-121">première étape de Hello est toocreate une application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="6d2e7-122">Connectez-vous à hello [portail classique Azure](http://manage.windowsazure.com/) à l’aide d’abonnement hello qui contient votre service de gestion des API d’instance et accédez toohello **Applications** onglet pour votre Azure Active Directory par défaut.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="6d2e7-123">Si le répertoire de hello Azure Active Directory par défaut n’est pas visible tooyour compte, administrateur de contact hello Hello de toogrant d’abonnement Azure hello requis compte tooyour d’autorisations.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Création d’une application Azure Active Directory][api-management-add-aad-application]

<span data-ttu-id="6d2e7-125">Cliquez sur **Ajouter**, **Ajouter une application développée par mon organisation**, puis choisissez **Application cliente native**.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="6d2e7-126">Entrez un nom descriptif et cliquez sur la flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="6d2e7-127">Entrez une URL de l’espace réservé tel que `http://resources` pour hello **URI de redirection**, comme il s’agit d’un champ obligatoire, mais la valeur de hello n’est pas utilisé plus tard.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="6d2e7-128">Cliquez sur hello case toosave hello application.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="6d2e7-129">Une fois l’application hello est enregistrée, cliquez sur **configurer**, faites défiler vers le bas toohello **autorisations tooother applications** section, puis cliquez sur **ajouter application**.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![Ajout d’autorisations][api-management-aad-permissions-add]

<span data-ttu-id="6d2e7-131">Sélectionnez **Windows** **API de gestion des services Azure** et cliquez sur l’application hello case à cocher tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![Ajout d’autorisations][api-management-aad-permissions]

<span data-ttu-id="6d2e7-133">Cliquez sur **autorisations déléguées** en regard de hello nouvellement ajouté **Windows** **API de gestion des services Azure** application, la case à cocher hello pour **accéder à Azure Gestion des services (version préliminaire)**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Ajout d’autorisations][api-management-aad-delegated-permissions]

<span data-ttu-id="6d2e7-135">Tooinvoking préalable hello API générer hello sauvegarde et restauration, il s’agit d’un jeton de tooget nécessaire.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="6d2e7-136">exemple Hello utilise hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) jeton de nuget package tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

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

<span data-ttu-id="6d2e7-137">Remplacez `{tentand id}`, `{application id}`, et `{redirect uri}` à l’aide de hello suivant les instructions.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="6d2e7-138">Remplacez `{tenant id}` avec l’id de client hello Hello application Azure Active Directory que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="6d2e7-139">Vous pouvez accéder à des id de hello en cliquant sur **afficher les points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-139">You can access hello id by clicking **View endpoints**.</span></span>

![Points de terminaison][api-management-aad-default-directory]

![Points de terminaison][api-management-endpoint]

<span data-ttu-id="6d2e7-142">Remplacez `{application id}` et `{redirect uri}` à l’aide de hello **Id Client** et hello URL à partir de hello **URI de redirection** section à partir de votre application Azure Active Directory **configurer**  onglet.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Ressources][api-management-aad-resources]

<span data-ttu-id="6d2e7-144">Une fois que les valeurs hello sont spécifiées, exemple de code hello doit renvoyer un jeton toohello semblable l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![Jeton][api-management-arm-token]

<span data-ttu-id="6d2e7-146">Avant d’appeler hello de sauvegarde et de restauration des opérations décrites dans les sections suivantes de hello, définir l’en-tête de demande d’autorisation hello pour votre appel REST.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="6d2e7-147"><a name="step1"></a>Sauvegarde d’un service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="6d2e7-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="6d2e7-148">tooback d’un hello de problème de service de gestion des API suivant demande HTTP :</span><span class="sxs-lookup"><span data-stu-id="6d2e7-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="6d2e7-149">où :</span><span class="sxs-lookup"><span data-stu-id="6d2e7-149">where:</span></span>

* <span data-ttu-id="6d2e7-150">`subscriptionId`-id d’abonnement hello contenant le service de gestion des API hello vous essayez de toobackup</span><span class="sxs-lookup"><span data-stu-id="6d2e7-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="6d2e7-151">`resourceGroupName`-une chaîne sous forme de hello de « Api - par - défaut {région service} » où `service-region` identifie hello région Azure où hello service Gestion des API que vous essayez toobackup est hébergé, par exemple,`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="6d2e7-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="6d2e7-152">`serviceName`-nom hello Hello service de gestion des API vous effectuez une sauvegarde de spécifiée au moment de sa création de hello</span><span class="sxs-lookup"><span data-stu-id="6d2e7-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="6d2e7-153">`api-version` - remplacer par `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="6d2e7-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="6d2e7-154">Dans le corps de demande de hello de hello, spécifiez le nom de compte de stockage Azure hello cible, la clé d’accès, nom de conteneur et nom de la sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="6d2e7-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="6d2e7-155">La valeur hello Hello `Content-Type` en-tête de demande trop`application/json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="6d2e7-156">Sauvegarde est une longue opération qui peut prendre plusieurs minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="6d2e7-157">Si hello demande a abouti et processus de sauvegarde hello a été lancée vous recevrez un `202 Accepted` code d’état de réponse avec un `Location` en-tête.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="6d2e7-158">Vérifiez le 'GET' demande URL toohello Bonjour `Location` toofind en-tête état hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="6d2e7-159">Pendant la sauvegarde de hello vous continuerez tooreceive un code d’état « 202 accepté ».</span><span class="sxs-lookup"><span data-stu-id="6d2e7-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="6d2e7-160">Un code de réponse `200 OK` indique la réussite de l’opération de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="6d2e7-161">Veuillez noter hello suivant contraintes lors d’une demande de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="6d2e7-162">**Conteneur** spécifié dans le corps de la demande hello **doit exister**.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="6d2e7-163">Lorsque la sauvegarde est en cours, **vous ne devez tenter aucune opération de gestion des services** telle que la mise à niveau vers une version supérieure/antérieure, la modification d'un nom de domaine, etc.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="6d2e7-164">Restauration d’un **sauvegarde est garantie uniquement pendant 30 jours** depuis le moment hello de sa création.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="6d2e7-165">**Les données d’utilisation** utilisé pour créer des rapports d’analytique **n’est pas inclus** dans la sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="6d2e7-166">Utilisez [API REST de gestion des API Azure] [ Azure API Management REST API] tooperiodically récupérer des rapports d’analytique en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="6d2e7-167">fréquence de Hello avec lequel vous effectuez des sauvegardes de service affectent votre objectif de point de récupération.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="6d2e7-168">toominimize il nous vous conseillons de mise en œuvre de sauvegardes régulières, ainsi que d’effectuer des sauvegardes de la demande après avoir établi l’important modifie le service de gestion des API tooyour.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="6d2e7-169">**Modifications** configuration du service toohello effectuées (par exemple, API, stratégies, apparence portail des développeurs) lors de l’opération de sauvegarde est en cours **ne sont pas inclus dans la sauvegarde de hello et par conséquent ne sera pas conservé**.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="6d2e7-170"><a name="step2"></a>Récupération d’un service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="6d2e7-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="6d2e7-171">toorestore un service de gestion des API à partir d’une sauvegarde créée précédemment apporter hello suivant demande HTTP :</span><span class="sxs-lookup"><span data-stu-id="6d2e7-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="6d2e7-172">où :</span><span class="sxs-lookup"><span data-stu-id="6d2e7-172">where:</span></span>

* <span data-ttu-id="6d2e7-173">`subscriptionId`-id d’abonnement hello contenant le service de gestion des API hello vous restaurez une sauvegarde dans</span><span class="sxs-lookup"><span data-stu-id="6d2e7-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="6d2e7-174">`resourceGroupName`-une chaîne sous forme de hello de « Api - par - défaut {région service} » où `service-region` identifie hello région Azure où hello service de gestion des API vous restaurez une sauvegarde dans est hébergé, par exemple,`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="6d2e7-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="6d2e7-175">`serviceName`-nom hello Hello gestion des API du service en cours de restauration dans spécifié lors de sa création hello</span><span class="sxs-lookup"><span data-stu-id="6d2e7-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="6d2e7-176">`api-version` - remplacer par `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="6d2e7-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="6d2e7-177">Dans le corps de demande de hello de hello, spécifiez l’emplacement du fichier de sauvegarde de hello, par exemple, nom de compte de stockage Azure, la clé d’accès, nom de conteneur et nom de la sauvegarde :</span><span class="sxs-lookup"><span data-stu-id="6d2e7-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="6d2e7-178">La valeur hello Hello `Content-Type` en-tête de demande trop`application/json`.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="6d2e7-179">La restauration est une longue opération qui peut prendre jusqu'à too30 ou de plusieurs minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="6d2e7-180">Si la demande de hello a abouti et processus de restauration hello a été lancée vous recevrez un `202 Accepted` code d’état de réponse avec un `Location` en-tête.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="6d2e7-181">Vérifiez le 'GET' demande URL toohello Bonjour `Location` toofind en-tête état hello d’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="6d2e7-182">Pendant la restauration de hello vous continuerez code d’état tooreceive « 202 accepté ».</span><span class="sxs-lookup"><span data-stu-id="6d2e7-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="6d2e7-183">Un code de réponse `200 OK` indique la réussite de l’opération de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6d2e7-184">**Hello SKU** du service hello restaurée dans **doit correspondre à** hello référence (SKU) de hello sauvegardé de service en cours de restauration.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="6d2e7-185">**Modifications** configuration du service toohello effectuées (par exemple, API, stratégies, apparence portail des développeurs) lors de l’opération de restauration est en cours d’exécution **pourrait être remplacé**.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="6d2e7-186">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6d2e7-186">Next steps</span></span>
<span data-ttu-id="6d2e7-187">Consultez hello suivant blogs Microsoft pour les deux procédures pas à pas différent du processus de sauvegarde/restauration hello.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="6d2e7-188">Répliquer des comptes de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="6d2e7-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="6d2e7-189">Merci d’avoir tooGisela pour son article toothis de contribution.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="6d2e7-190">Gestion des API Azure : sauvegarde et restauration de la configuration</span><span class="sxs-lookup"><span data-stu-id="6d2e7-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="6d2e7-191">approche Hello détaillée par Stuart ne correspond pas aux directives officielles hello, mais il est très intéressant.</span><span class="sxs-lookup"><span data-stu-id="6d2e7-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

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
