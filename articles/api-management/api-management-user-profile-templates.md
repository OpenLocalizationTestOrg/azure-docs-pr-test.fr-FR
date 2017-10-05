---
title: "Modèles Profil utilisateur dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment personnaliser le contenu des pages Profil utilisateur dans le portail des développeurs dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2e3b73ef-d223-44fe-9280-c3af3fd4a030
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 9a11bd5800068a5725ab2f099043993bff0b28d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="b8fb6-103">Modèles Profil utilisateur dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="b8fb6-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="b8fb6-104">Gestion des API Azure vous offre la possibilité de personnaliser le contenu des pages du portail des développeurs à l’aide d’un ensemble de modèles qui configurent leur contenu.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="b8fb6-105">En utilisant la syntaxe [DotLiquid](http://dotliquidmarkup.org/) et l’éditeur de votre choix, comme [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ainsi qu’un ensemble de [ressources de chaîne](api-management-template-resources.md#strings), de [ressources de glyphe](api-management-template-resources.md#glyphs) et de [contrôles de page](api-management-page-controls.md) localisés, vous disposez d’un large choix pour configurer le contenu des pages selon vos besoins à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="b8fb6-106">Les modèles de cette section vous permettent de personnaliser le contenu des pages Profil utilisateur dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-106">The templates in this section allow you to customize the content of the User profile pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="b8fb6-107">Profil</span><span class="sxs-lookup"><span data-stu-id="b8fb6-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="b8fb6-108">Abonnements</span><span class="sxs-lookup"><span data-stu-id="b8fb6-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="b8fb6-109">Applications</span><span class="sxs-lookup"><span data-stu-id="b8fb6-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="b8fb6-110">Mettre à jour les informations du compte</span><span class="sxs-lookup"><span data-stu-id="b8fb6-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="b8fb6-111">Les exemples de modèles par défaut inclus dans la documentation suivante sont susceptibles d’être modifiés et améliorés de façon régulière.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-111">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="b8fb6-112">Vous pouvez afficher les modèles dynamiques par défaut dans le portail des développeurs en accédant aux modèles individuels souhaités.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-112">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="b8fb6-113">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-113">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="b8fb6-114"><a name="Profile"></a> Profil</span><span class="sxs-lookup"><span data-stu-id="b8fb6-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="b8fb6-115">Le modèle **Profil** vous permet de personnaliser la section Profil utilisateur de la page Profil utilisateur dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-115">The **profile** template allows you to customize the user profile section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="b8fb6-116">![Page Profil utilisateur](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Page Profil utilisateur APIM")</span><span class="sxs-lookup"><span data-stu-id="b8fb6-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b8fb6-117">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="b8fb6-117">Default template</span></span>  
  
```xml  
<div class="pull-right">  
  {% if canChangePassword == true %}  
  <a class="btn btn-default" id="ChangePassword" role="button" href="{{changePasswordUrl}}">{% localized "UserProfile|ButtonLabelChangePassword" %}</a>  
  {% endif %}  
  <a id="changeAccountInfo" href="{{changeNameOrEmailUrl}}" class="btn btn-default">  
    <span class="glyphicon glyphicon-user"></span>  
    <span>{% localized "UserProfile|ButtonLabelChangeAccountInfo" %}</span>  
  </a>  
</div>  
<h2>{% localized "SubscriptionStrings|PageTitleDeveloperProfile" %}</h2>  
<div class="container-fluid">  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="Email">{% localized "UserProfile|TextboxLabelEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="Email">{{email}}</div>  
  </div>  
  
  {% if isSystemUser != true %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="FirstName">{% localized "UserProfile|TextboxLabelEmailFirstName" %}</label>  
    </div>  
    <div class="col-sm-9" id="FirstName">{{FirstName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="LastName">{% localized "UserProfile|TextboxLabelEmailLastName" %}</label>  
    </div>  
    <div class="col-sm-9" id="LastName">{{LastName}}</div>  
  </div>  
  {% else %}  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="CompanyName">{% localized "UserProfile|TextboxLabelOrganizationName" %}</label>  
    </div>  
    <div class="col-sm-9" id="CompanyName">{{CompanyName}}</div>  
  </div>  
  <div class="row">  
    <div class="col-sm-3">  
      <label for="AddresserEmail">{% localized "UserProfile|TextboxLabelNotificationsSenderEmail" %}</label>  
    </div>  
    <div class="col-sm-9" id="AddresserEmail">{{AddresserEmail}}</div>  
  </div>  
  {% endif %}  
  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="b8fb6-118">Commandes</span><span class="sxs-lookup"><span data-stu-id="b8fb6-118">Controls</span></span>  
 <span data-ttu-id="b8fb6-119">Ce modèle ne peut pas utiliser de [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="b8fb6-120">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="b8fb6-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b8fb6-121">Les modèles [Profil](#Profile), [Applications](#Applications) et [Abonnements](#Subscriptions) partagent le même modèle de données et reçoivent les mêmes données de modèle.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-121">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="b8fb6-122">Propriété</span><span class="sxs-lookup"><span data-stu-id="b8fb6-122">Property</span></span>|<span data-ttu-id="b8fb6-123">Type</span><span class="sxs-lookup"><span data-stu-id="b8fb6-123">Type</span></span>|<span data-ttu-id="b8fb6-124">Description</span><span class="sxs-lookup"><span data-stu-id="b8fb6-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="b8fb6-125">firstName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-125">firstName</span></span>|<span data-ttu-id="b8fb6-126">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-126">string</span></span>|<span data-ttu-id="b8fb6-127">Prénom de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-127">First name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-128">lastName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-128">lastName</span></span>|<span data-ttu-id="b8fb6-129">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-129">string</span></span>|<span data-ttu-id="b8fb6-130">Nom de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-130">Last name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-131">companyName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-131">companyName</span></span>|<span data-ttu-id="b8fb6-132">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-132">string</span></span>|<span data-ttu-id="b8fb6-133">Nom de l’entreprise de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-133">The company name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="b8fb6-134">addresserEmail</span></span>|<span data-ttu-id="b8fb6-135">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-135">string</span></span>|<span data-ttu-id="b8fb6-136">Adresse e-mail de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-136">Email address of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="b8fb6-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="b8fb6-138">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-138">string</span></span>|<span data-ttu-id="b8fb6-139">URL relative permettant d’afficher les données d’analyse relatives à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-139">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="b8fb6-140">subscriptions</span></span>|<span data-ttu-id="b8fb6-141">Collection d’entités [Abonnement](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="b8fb6-142">Abonnements associés à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-142">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-143">web</span><span class="sxs-lookup"><span data-stu-id="b8fb6-143">applications</span></span>|<span data-ttu-id="b8fb6-144">Collection d’entités [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="b8fb6-145">Applications associées à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-145">The applications of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="b8fb6-146">changePasswordUrl</span></span>|<span data-ttu-id="b8fb6-147">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-147">string</span></span>|<span data-ttu-id="b8fb6-148">URL relative permettant de modifier le mot de passe de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-148">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="b8fb6-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="b8fb6-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="b8fb6-150">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-150">string</span></span>|<span data-ttu-id="b8fb6-151">URL relative permettant de modifier le nom et l’e-mail de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-151">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="b8fb6-152">canChangePassword</span></span>|<span data-ttu-id="b8fb6-153">booléenne</span><span class="sxs-lookup"><span data-stu-id="b8fb6-153">boolean</span></span>|<span data-ttu-id="b8fb6-154">Indique si l’utilisateur actif peut changer son mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-154">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="b8fb6-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="b8fb6-155">isSystemUser</span></span>|<span data-ttu-id="b8fb6-156">booléenne</span><span class="sxs-lookup"><span data-stu-id="b8fb6-156">boolean</span></span>|<span data-ttu-id="b8fb6-157">Indique si l’utilisateur actif est membre de l’un des [groupes](api-management-key-concepts.md#groups) prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-157">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="b8fb6-158">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="b8fb6-158">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="b8fb6-159"><a name="Subscriptions"></a> Abonnements</span><span class="sxs-lookup"><span data-stu-id="b8fb6-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="b8fb6-160">Le modèle **Abonnements** vous permet de personnaliser la section Abonnements de la page Profil utilisateur dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-160">The **Subscriptions** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="b8fb6-161">![Page d’abonnement utilisateur](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Page d’abonnement utilisateur APIM")</span><span class="sxs-lookup"><span data-stu-id="b8fb6-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b8fb6-162">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="b8fb6-162">Default template</span></span>  
  
```xml  
<div class="ap-account-subscriptions">  
  <a href="{{developersUsageStatisticsLink}}" id="UsageStatistics" class="btn btn-default pull-right">  
    <span class="glyphicon glyphicon-stats"></span>  
    <span>{% localized "SubscriptionListStrings|WebDevelopersUsageStatisticsLink" %}</span>  
  </a>  
  
  <h2>{% localized "SubscriptionListStrings|WebDevelopersYourSubscriptions" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th>Subscription details</th>  
        <th>Product</th>  
        <th>{% localized "SubscriptionListStrings|WebDevelopersSubscriptionTableStateHeader" %}</th>  
        <th>Action</th>  
      </tr>  
    </thead>  
    <tbody>  
      {% if subscriptions.size == 0 %}  
      <tr>  
        <td class="text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
      {% else %}  
      {% for subscription in subscriptions %}  
      <tr id="{{subscription.id}}" {% if subscription.hasExpired %} class="expired" {% endif %}>  
        <td>  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelName" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.displayName }}  
            </div>  
            <div class="col-lg-2">  
              <a class="btn-link" href="/Subscriptions/{{subscription.id}}/Rename">Rename</a>  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          {% if subscription.isAwaitingApproval %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelRequestedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.createdDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% else %}  
          {% if subscription.isRejected == false %}  
          {% if subscription.startDate %}  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|SubscriptionPropertyLabelStartedDate" %}</label>  
            <div class="col-lg-6">  
              {{ subscription.startDate | date:"MM/dd/yyyy" }}  
            </div>  
          </div>  
          {% endif %}  
  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.primaryKey}}', '{{subscription.id}}', true) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersPrimaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="primary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <!-- ko if: !requestInProgress() -->  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="togglePrimary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel"></a>  
                |  
                <a href="#" class="btn-link" id="regeneratePrimary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel"></a>  
              </div>  
              <!-- /ko -->  
              <!-- ko if: requestInProgress() -->  
              <div class="progress progress-striped active">  
                <div class="progress-bar" role="progressbar" aria-valuenow="100" aria-valuemin="0" aria-valuemax="100" style="width: 100%">  
                  <span class="sr-only"></span>  
                </div>  
              </div>  
              <!-- /ko -->  
            </div>  
            <div class="clearfix"></div>  
          </div>  
          <!-- /ko -->  
          <!-- ko with: Developers.Account.Root.account.key('{{subscription.secondaryKey}}', '{{subscription.id}}', false) -->  
          <div class="row">  
            <label class="col-lg-3">{% localized "SubscriptionListStrings|WebDevelopersSecondaryKey" %}</label>  
            <div class="col-lg-6">  
              <code data-bind="text: $data.displayKey()" id="secondary_{{subscription.id}}"></code>  
            </div>  
            <div class="col-lg-2">  
              <div class="nowrap">  
                <a href="#" class="btn-link" id="toggleSecondary_{{subscription.id}}" data-bind="click: toggleKeyDisplay, text: toggleKeyLabel">{% localized "SubscriptionListStrings|ButtonLabelShowKey" %}</a>  
                |  
                <a href="#" class="btn-link" id="regenerateSecondary_{{subscription.id}}" data-bind="click: regenerateKey, text: regenerateKeyLabel">{% localized "SubscriptionListStrings|WebDevelopersRegenerateLink" %}</a>  
              </div>  
            </div>  
            <div class="clearfix"> </div>  
          </div>  
          <!-- /ko -->  
          {% endif %}  
          {% endif %}  
        </td>  
        <td>  
          <a href="{{subscription.productDetailsUrl}}">{{subscription.productTitle}}</a>  
        </td>  
        <td>  
          <strong>  
            {{subscription.state}}  
          </strong>  
        </td>  
        <td>  
          <div class="nowrap">  
            {% if subscription.canBeCancelled %}  
            <subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }"></subscription-cancel>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="b8fb6-163">Commandes</span><span class="sxs-lookup"><span data-stu-id="b8fb6-163">Controls</span></span>  
 <span data-ttu-id="b8fb6-164">Ce modèle peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-164">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="b8fb6-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="b8fb6-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="b8fb6-166">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="b8fb6-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b8fb6-167">Les modèles [Profil](#Profile), [Applications](#Applications) et [Abonnements](#Subscriptions) partagent le même modèle de données et reçoivent les mêmes données de modèle.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-167">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="b8fb6-168">Propriété</span><span class="sxs-lookup"><span data-stu-id="b8fb6-168">Property</span></span>|<span data-ttu-id="b8fb6-169">Type</span><span class="sxs-lookup"><span data-stu-id="b8fb6-169">Type</span></span>|<span data-ttu-id="b8fb6-170">Description</span><span class="sxs-lookup"><span data-stu-id="b8fb6-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="b8fb6-171">firstName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-171">firstName</span></span>|<span data-ttu-id="b8fb6-172">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-172">string</span></span>|<span data-ttu-id="b8fb6-173">Prénom de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-173">First name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-174">lastName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-174">lastName</span></span>|<span data-ttu-id="b8fb6-175">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-175">string</span></span>|<span data-ttu-id="b8fb6-176">Nom de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-176">Last name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-177">companyName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-177">companyName</span></span>|<span data-ttu-id="b8fb6-178">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-178">string</span></span>|<span data-ttu-id="b8fb6-179">Nom de l’entreprise de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-179">The company name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="b8fb6-180">addresserEmail</span></span>|<span data-ttu-id="b8fb6-181">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-181">string</span></span>|<span data-ttu-id="b8fb6-182">Adresse e-mail de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-182">Email address of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="b8fb6-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="b8fb6-184">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-184">string</span></span>|<span data-ttu-id="b8fb6-185">URL relative permettant d’afficher les données d’analyse relatives à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-185">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="b8fb6-186">subscriptions</span></span>|<span data-ttu-id="b8fb6-187">Collection d’entités [Abonnement](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="b8fb6-188">Abonnements associés à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-188">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-189">web</span><span class="sxs-lookup"><span data-stu-id="b8fb6-189">applications</span></span>|<span data-ttu-id="b8fb6-190">Collection d’entités [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="b8fb6-191">Applications associées à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-191">The applications of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="b8fb6-192">changePasswordUrl</span></span>|<span data-ttu-id="b8fb6-193">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-193">string</span></span>|<span data-ttu-id="b8fb6-194">URL relative permettant de modifier le mot de passe de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-194">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="b8fb6-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="b8fb6-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="b8fb6-196">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-196">string</span></span>|<span data-ttu-id="b8fb6-197">URL relative permettant de modifier le nom et l’e-mail de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-197">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="b8fb6-198">canChangePassword</span></span>|<span data-ttu-id="b8fb6-199">booléenne</span><span class="sxs-lookup"><span data-stu-id="b8fb6-199">boolean</span></span>|<span data-ttu-id="b8fb6-200">Indique si l’utilisateur actif peut changer son mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-200">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="b8fb6-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="b8fb6-201">isSystemUser</span></span>|<span data-ttu-id="b8fb6-202">booléenne</span><span class="sxs-lookup"><span data-stu-id="b8fb6-202">boolean</span></span>|<span data-ttu-id="b8fb6-203">Indique si l’utilisateur actif est membre de l’un des [groupes](api-management-key-concepts.md#groups) prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-203">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="b8fb6-204">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="b8fb6-204">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="b8fb6-205"><a name="Applications"></a> Applications</span><span class="sxs-lookup"><span data-stu-id="b8fb6-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="b8fb6-206">Le modèle **Applications** vous permet de personnaliser la section Abonnements de la page Profil utilisateur dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-206">The **Applications** template allows you to customize the subscriptions section of the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="b8fb6-207">![Page Applications du compte d’utilisateur](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM Applications du compte d’utilisateur APIM")</span><span class="sxs-lookup"><span data-stu-id="b8fb6-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b8fb6-208">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="b8fb6-208">Default template</span></span>  
  
```xml  
<div class="ap-account-applications">  
  <a id="RegisterApplication" href="/Developer/Applications/Register" class="btn btn-success pull-right">  
    <span class="glyphicon glyphicon-plus"></span>  
    <span>{% localized "ApplicationListStrings|WebDevelopersRegisterAppLink" %}</span>  
  </a>  
  <h2>{% localized "ApplicationListStrings|WebDevelopersYourApplicationsHeader" %}</h2>  
  
  <table class="table">  
    <thead>  
      <tr>  
        <th class="col-md-8">{% localized "ApplicationListStrings|WebDevelopersAppTableNameHeader" %}</th>  
        <th class="col-md-2">{% localized "ApplicationListStrings|WebDevelopersAppTableCategoryHeader" %}</th>  
        <th class="col-md-2" colspan="2">{% localized "ApplicationListStrings|WebDevelopersAppTableStateHeader" %}</th>  
      </tr>  
    </thead>  
    <tbody>  
  
      {% if applications.size == 0 %}  
  
      <tr>  
        <td class="col-md-12 text-center" colspan="4">  
          {% localized "CommonResources|NoItemsToDisplay" %}  
        </td>  
      </tr>  
  
      {% else %}  
  
      {% for app in applications %}  
      <tr>  
        <td class="col-md-8">  
          {{app.title}}  
        </td>  
        <td class="col-md-2">  
          {{app.categoryName}}  
        </td>  
        <td class="col-md-2">  
          <strong>  
            {% case app.state %}  
            {% when ApplicationStateModel.Registered %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotSubminted" %}  
  
            {% when ApplicationStateModel.Unpublished %}  
            {% localized "ApplicationListStrings|WebDevelopersAppNotPublished" %}  
  
            {% else %}  
            {{ app.state }}  
            {% endcase %}  
          </strong>  
        </td>  
        <td class="col-md-1">  
          <div class="nowrap">  
            {% if app.state != ApplicationStateModel.Submitted and app.state != ApplicationStateModel.Published %}  
            <app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
            {% endif %}  
          </div>  
        </td>  
      </tr>  
      {% endfor %}  
  
      {% endif %}  
    </tbody>  
  </table>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="b8fb6-209">Commandes</span><span class="sxs-lookup"><span data-stu-id="b8fb6-209">Controls</span></span>  
 <span data-ttu-id="b8fb6-210">Ce modèle peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-210">This template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="b8fb6-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="b8fb6-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="b8fb6-212">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="b8fb6-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="b8fb6-213">Les modèles [Profil](#Profile), [Applications](#Applications) et [Abonnements](#Subscriptions) partagent le même modèle de données et reçoivent les mêmes données de modèle.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-213">The [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share the same data model and receive the same template data.</span></span>  
  
|<span data-ttu-id="b8fb6-214">Propriété</span><span class="sxs-lookup"><span data-stu-id="b8fb6-214">Property</span></span>|<span data-ttu-id="b8fb6-215">Type</span><span class="sxs-lookup"><span data-stu-id="b8fb6-215">Type</span></span>|<span data-ttu-id="b8fb6-216">Description</span><span class="sxs-lookup"><span data-stu-id="b8fb6-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="b8fb6-217">firstName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-217">firstName</span></span>|<span data-ttu-id="b8fb6-218">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-218">string</span></span>|<span data-ttu-id="b8fb6-219">Prénom de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-219">First name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-220">lastName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-220">lastName</span></span>|<span data-ttu-id="b8fb6-221">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-221">string</span></span>|<span data-ttu-id="b8fb6-222">Nom de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-222">Last name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-223">companyName</span><span class="sxs-lookup"><span data-stu-id="b8fb6-223">companyName</span></span>|<span data-ttu-id="b8fb6-224">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-224">string</span></span>|<span data-ttu-id="b8fb6-225">Nom de l’entreprise de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-225">The company name of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="b8fb6-226">addresserEmail</span></span>|<span data-ttu-id="b8fb6-227">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-227">string</span></span>|<span data-ttu-id="b8fb6-228">Adresse e-mail de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-228">Email address of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="b8fb6-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="b8fb6-230">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-230">string</span></span>|<span data-ttu-id="b8fb6-231">URL relative permettant d’afficher les données d’analyse relatives à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-231">Relative URL to view analytics for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="b8fb6-232">subscriptions</span></span>|<span data-ttu-id="b8fb6-233">Collection d’entités [Abonnement](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="b8fb6-234">Abonnements associés à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-234">The subscriptions for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-235">web</span><span class="sxs-lookup"><span data-stu-id="b8fb6-235">applications</span></span>|<span data-ttu-id="b8fb6-236">Collection d’entités [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="b8fb6-237">Applications associées à l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-237">The applications of the current user.</span></span>|  
|<span data-ttu-id="b8fb6-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="b8fb6-238">changePasswordUrl</span></span>|<span data-ttu-id="b8fb6-239">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-239">string</span></span>|<span data-ttu-id="b8fb6-240">URL relative permettant de modifier le mot de passe de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-240">The relative URL to change the current user's password.</span></span>|  
|<span data-ttu-id="b8fb6-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="b8fb6-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="b8fb6-242">string</span><span class="sxs-lookup"><span data-stu-id="b8fb6-242">string</span></span>|<span data-ttu-id="b8fb6-243">URL relative permettant de modifier le nom et l’e-mail de l’utilisateur actif.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-243">The relative URL to change the name and email for the current user.</span></span>|  
|<span data-ttu-id="b8fb6-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="b8fb6-244">canChangePassword</span></span>|<span data-ttu-id="b8fb6-245">booléenne</span><span class="sxs-lookup"><span data-stu-id="b8fb6-245">boolean</span></span>|<span data-ttu-id="b8fb6-246">Indique si l’utilisateur actif peut changer son mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-246">Whether the current user can change their password.</span></span>|  
|<span data-ttu-id="b8fb6-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="b8fb6-247">isSystemUser</span></span>|<span data-ttu-id="b8fb6-248">booléenne</span><span class="sxs-lookup"><span data-stu-id="b8fb6-248">boolean</span></span>|<span data-ttu-id="b8fb6-249">Indique si l’utilisateur actif est membre de l’un des [groupes](api-management-key-concepts.md#groups) prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-249">Whether the current user is a member of one of the built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="b8fb6-250">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="b8fb6-250">Sample template data</span></span>  
  
```json  
{  
    "firstName": "Administrator",  
    "lastName": "",  
    "companyName": "Contoso",  
    "addresserEmail": "apimgmt-noreply@mail.windowsazure.com",  
    "email": "admin@live.com",  
    "developersUsageStatisticsLink": "/Developer/Analytics",  
    "subscriptions": [  
        {  
            "Id": "57026e30de15d80041070001",  
            "ProductId": "57026e30de15d80041060001",  
            "ProductTitle": "Starter",  
            "ProductDescription": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060001",  
            "State": "Active",  
            "DisplayName": "Starter  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.847",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "b6b2870953d04420a4e02c58f2c08e74",  
            "SecondaryKey": "cfe28d5a1cd04d8abc93f48352076ea5",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070001/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070001/Renew"  
        },  
        {  
            "Id": "57026e30de15d80041070002",  
            "ProductId": "57026e30de15d80041060002",  
            "ProductTitle": "Unlimited",  
            "ProductDescription": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "ProductDetailsUrl": "/Products/57026e30de15d80041060002",  
            "State": "Active",  
            "DisplayName": "Unlimited  (default)",  
            "CreatedDate": "2016-04-04T13:37:52.923",  
            "CanBeCancelled": true,  
            "IsAwaitingApproval": false,  
            "StartDate": null,  
            "ExpirationDate": null,  
            "NotificationDate": null,  
            "PrimaryKey": "8fe7843c36de4cceb4728e6cae297336",  
            "SecondaryKey": "96c850d217e74acf9b514ff8a5b38551",  
            "UserId": 1,  
            "CanBeRenewed": false,  
            "HasExpired": false,  
            "IsRejected": false,  
            "CancelUrl": "/Subscriptions/57026e30de15d80041070002/Cancel",  
            "RenewUrl": "/Subscriptions/57026e30de15d80041070002/Renew"  
        }  
    ],  
    "applications": [],  
    "changePasswordUrl": "/account/password/change",  
    "changeNameOrEmailUrl": "/account/update",  
    "canChangePassword": false,  
    "isSystemUser": true  
}  
```  
  
##  <span data-ttu-id="b8fb6-251"><a name="UpdateAccountInfo"></a> Mettre à jour les informations du compte</span><span class="sxs-lookup"><span data-stu-id="b8fb6-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="b8fb6-252">Le modèle **Mettre à jour les informations du compte** vous permet de personnaliser la page **Mettre à jour les informations du compte** dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="b8fb6-252">The **Uodate account info** template allows you to customize the **Update account information** page in the developer portal.</span></span>  
  
 <span data-ttu-id="b8fb6-253">![Modèles de page Mettre à jour les informations du compte dans le portail des développeurs](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Modèles de page Mettre à jour les informations du compte dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="b8fb6-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b8fb6-254">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="b8fb6-254">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-sm-6 col-md-6">  
    <div class="form-group">  
      <label for="Email">{% localized "SigninResources|TextboxLabelEmail" %}</label>  
      <input autofocus="autofocus" class="form-control" id="Email" name="Email" type="text" value="{{email}}">  
    </div>  
    <div class="form-group">  
      <label for="FirstName">{% localized "SigninResources|TextboxLabelEmailFirstName" %}</label>  
      <input class="form-control" id="FirstName" name="FirstName" type="text" value="{{firstName}}">  
    </div>  
    <div class="form-group">  
      <label for="LastName">{% localized "SigninResources|TextboxLabelEmailLastName" %}</label>  
      <input class="form-control" id="LastName" name="LastName" type="text" value="{{lastName}}">  
    </div>  
    <div class="form-group">  
      <label for="Password">{% localized "SigninResources|WebAuthenticationSigninPasswordLabel" %}</label>  
      <input class="form-control" id="Password" name="Password" type="password">  
    </div>  
  </div>  
</div>  
  
<button type="submit" class="btn btn-primary" id="UpdateProfile">  
  {% localized "UpdateProfileStrings|ButtonLabelUpdateProfile" %}  
</button>  
<a class="btn btn-default" href="/developer" role="button">  
  {% localized "CommonStrings|ButtonLabelCancel" %}  
</a>  
```  
  
### <a name="controls"></a><span data-ttu-id="b8fb6-255">Commandes</span><span class="sxs-lookup"><span data-stu-id="b8fb6-255">Controls</span></span>  
 <span data-ttu-id="b8fb6-256">Ce modèle ne peut pas utiliser de [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="b8fb6-257">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="b8fb6-257">Data model</span></span>  
 <span data-ttu-id="b8fb6-258">Entité [User account info](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="b8fb6-259">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="b8fb6-259">Sample template data</span></span>  
  
```json  
{  
    "FirstName": "Administrator",  
    "LastName": "",  
    "Email": "admin@live.com",  
    "Password": null,  
    "NameIdentifier": null,  
    "ProviderName": null,  
    "IsBasicAccount": false  
}  
```

## <a name="next-steps"></a><span data-ttu-id="b8fb6-260">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8fb6-260">Next steps</span></span>
<span data-ttu-id="b8fb6-261">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b8fb6-261">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>