---
title: "AAA » les modèles de profil utilisateur dans la gestion des API Azure | Documents Microsoft »"
description: "Découvrez le fonctionnement des pages dans le portail des développeurs dans Gestion des API Azure hello toocustomize le contenu hello Hello profil utilisateur."
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
ms.openlocfilehash: c8f153b310221164809acf58e4af236928ceb41d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="user-profile-templates-in-azure-api-management"></a><span data-ttu-id="5e86a-103">Modèles Profil utilisateur dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="5e86a-103">User profile templates in Azure API Management</span></span>
<span data-ttu-id="5e86a-104">Gestion des API Azure fournit que Hello de contenu de hello toocustomize possibilité de pages du portail développeur à l’aide d’un ensemble de modèles que configurer leur contenu.</span><span class="sxs-lookup"><span data-stu-id="5e86a-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="5e86a-105">À l’aide de [DotLiquid](http://dotliquidmarkup.org/) syntaxe et hello l’éditeur de votre choix, tel que [DotLiquid pour les concepteurs](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), et un ensemble fourni de localisée [ressources de type chaîne](api-management-template-resources.md#strings), [ Ressources de glyphe](api-management-template-resources.md#glyphs), et [Page les contrôles](api-management-page-controls.md), vous avez une grande souplesse tooconfigure hello contenu hello pages comme vous le souhaitez à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="5e86a-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="5e86a-106">modèles Hello dans cette section permettent de contenu de hello toocustomize des pages de profil utilisateur hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-106">hello templates in this section allow you toocustomize hello content of hello User profile pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="5e86a-107">Profil</span><span class="sxs-lookup"><span data-stu-id="5e86a-107">Profile</span></span>](#Profile)  
  
-   [<span data-ttu-id="5e86a-108">Abonnements</span><span class="sxs-lookup"><span data-stu-id="5e86a-108">Subscriptions</span></span>](#Subscriptions)  
  
-   [<span data-ttu-id="5e86a-109">Applications</span><span class="sxs-lookup"><span data-stu-id="5e86a-109">Applications</span></span>](#Applications)  
  
-   [<span data-ttu-id="5e86a-110">Mettre à jour les informations du compte</span><span class="sxs-lookup"><span data-stu-id="5e86a-110">Update account info</span></span>](#UpdateAccountInfo)  
  
> [!NOTE]
>  <span data-ttu-id="5e86a-111">Exemples de modèles par défaut sont inclus dans hello suivant la documentation, mais sont toochange sujet en raison des améliorations de toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="5e86a-111">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="5e86a-112">Vous pouvez afficher les modèles par défaut dynamique hello dans le portail des développeurs hello en naviguant toohello souhaitée des modèles individuels.</span><span class="sxs-lookup"><span data-stu-id="5e86a-112">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="5e86a-113">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="5e86a-113">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="5e86a-114"><a name="Profile"></a> Profil</span><span class="sxs-lookup"><span data-stu-id="5e86a-114"><a name="Profile"></a> Profile</span></span>  
 <span data-ttu-id="5e86a-115">Hello **profil** modèle vous permet de section de profil utilisateur toocustomize hello de page de profil utilisateur hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-115">hello **profile** template allows you toocustomize hello user profile section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e86a-116">![Page Profil utilisateur](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "Page Profil utilisateur APIM")</span><span class="sxs-lookup"><span data-stu-id="5e86a-116">![User Profile Page](./media/api-management-user-profile-templates/APIM-User-Profile-Page.png "APIM User Profile Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5e86a-117">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="5e86a-117">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="5e86a-118">Commandes</span><span class="sxs-lookup"><span data-stu-id="5e86a-118">Controls</span></span>  
 <span data-ttu-id="5e86a-119">Ce modèle ne peut pas utiliser de [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5e86a-119">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="5e86a-120">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="5e86a-120">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e86a-121">Hello [profil](#Profile), [Applications](#Applications), et [abonnements](#Subscriptions) hello des mêmes données de modèle et de réception hello partagent des modèles de données du même modèle.</span><span class="sxs-lookup"><span data-stu-id="5e86a-121">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="5e86a-122">Propriété</span><span class="sxs-lookup"><span data-stu-id="5e86a-122">Property</span></span>|<span data-ttu-id="5e86a-123">Type</span><span class="sxs-lookup"><span data-stu-id="5e86a-123">Type</span></span>|<span data-ttu-id="5e86a-124">Description</span><span class="sxs-lookup"><span data-stu-id="5e86a-124">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5e86a-125">firstName</span><span class="sxs-lookup"><span data-stu-id="5e86a-125">firstName</span></span>|<span data-ttu-id="5e86a-126">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-126">string</span></span>|<span data-ttu-id="5e86a-127">Prénom de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-127">First name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-128">lastName</span><span class="sxs-lookup"><span data-stu-id="5e86a-128">lastName</span></span>|<span data-ttu-id="5e86a-129">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-129">string</span></span>|<span data-ttu-id="5e86a-130">Nom de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-130">Last name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-131">companyName</span><span class="sxs-lookup"><span data-stu-id="5e86a-131">companyName</span></span>|<span data-ttu-id="5e86a-132">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-132">string</span></span>|<span data-ttu-id="5e86a-133">nom de l’utilisateur actuel hello Hello société.</span><span class="sxs-lookup"><span data-stu-id="5e86a-133">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-134">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="5e86a-134">addresserEmail</span></span>|<span data-ttu-id="5e86a-135">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-135">string</span></span>|<span data-ttu-id="5e86a-136">Adresse de messagerie de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-136">Email address of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-137">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="5e86a-137">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="5e86a-138">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-138">string</span></span>|<span data-ttu-id="5e86a-139">Analytique de tooview URL relative pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-139">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-140">subscriptions</span><span class="sxs-lookup"><span data-stu-id="5e86a-140">subscriptions</span></span>|<span data-ttu-id="5e86a-141">Collection d’entités [Abonnement](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="5e86a-141">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="5e86a-142">abonnements Hello pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-142">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-143">web</span><span class="sxs-lookup"><span data-stu-id="5e86a-143">applications</span></span>|<span data-ttu-id="5e86a-144">Collection d’entités [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="5e86a-144">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="5e86a-145">applications Hello de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-145">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-146">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="5e86a-146">changePasswordUrl</span></span>|<span data-ttu-id="5e86a-147">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-147">string</span></span>|<span data-ttu-id="5e86a-148">mot de passe Hello relatif URL toochange hello l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="5e86a-148">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="5e86a-149">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="5e86a-149">changeNameOrEmailUrl</span></span>|<span data-ttu-id="5e86a-150">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-150">string</span></span>|<span data-ttu-id="5e86a-151">Bonjour nom URL toochange hello et par courrier électronique pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-151">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-152">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="5e86a-152">canChangePassword</span></span>|<span data-ttu-id="5e86a-153">booléenne</span><span class="sxs-lookup"><span data-stu-id="5e86a-153">boolean</span></span>|<span data-ttu-id="5e86a-154">Si l’utilisateur actuel hello peut changer leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5e86a-154">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="5e86a-155">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="5e86a-155">isSystemUser</span></span>|<span data-ttu-id="5e86a-156">booléenne</span><span class="sxs-lookup"><span data-stu-id="5e86a-156">boolean</span></span>|<span data-ttu-id="5e86a-157">Si l’utilisateur actuel hello est un membre de l’un des intégrées de hello [groupes](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="5e86a-157">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5e86a-158">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="5e86a-158">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="5e86a-159"><a name="Subscriptions"></a> Abonnements</span><span class="sxs-lookup"><span data-stu-id="5e86a-159"><a name="Subscriptions"></a> Subscriptions</span></span>  
 <span data-ttu-id="5e86a-160">Hello **abonnements** modèle vous permet de section d’abonnements hello toocustomize de page de profil utilisateur hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-160">hello **Subscriptions** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e86a-161">![Page d’abonnement utilisateur](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "Page d’abonnement utilisateur APIM")</span><span class="sxs-lookup"><span data-stu-id="5e86a-161">![User Subscription Page](./media/api-management-user-profile-templates/APIM-User-Subscription-Page.png "APIM User Subscription Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5e86a-162">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="5e86a-162">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="5e86a-163">Commandes</span><span class="sxs-lookup"><span data-stu-id="5e86a-163">Controls</span></span>  
 <span data-ttu-id="5e86a-164">Ce modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5e86a-164">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5e86a-165">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="5e86a-165">subscription-cancel</span></span>](api-management-page-controls.md#subscription-cancel)  
  
### <a name="data-model"></a><span data-ttu-id="5e86a-166">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="5e86a-166">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e86a-167">Hello [profil](#Profile), [Applications](#Applications), et [abonnements](#Subscriptions) hello des mêmes données de modèle et de réception hello partagent des modèles de données du même modèle.</span><span class="sxs-lookup"><span data-stu-id="5e86a-167">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="5e86a-168">Propriété</span><span class="sxs-lookup"><span data-stu-id="5e86a-168">Property</span></span>|<span data-ttu-id="5e86a-169">Type</span><span class="sxs-lookup"><span data-stu-id="5e86a-169">Type</span></span>|<span data-ttu-id="5e86a-170">Description</span><span class="sxs-lookup"><span data-stu-id="5e86a-170">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5e86a-171">firstName</span><span class="sxs-lookup"><span data-stu-id="5e86a-171">firstName</span></span>|<span data-ttu-id="5e86a-172">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-172">string</span></span>|<span data-ttu-id="5e86a-173">Prénom de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-173">First name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-174">lastName</span><span class="sxs-lookup"><span data-stu-id="5e86a-174">lastName</span></span>|<span data-ttu-id="5e86a-175">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-175">string</span></span>|<span data-ttu-id="5e86a-176">Nom de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-176">Last name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-177">companyName</span><span class="sxs-lookup"><span data-stu-id="5e86a-177">companyName</span></span>|<span data-ttu-id="5e86a-178">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-178">string</span></span>|<span data-ttu-id="5e86a-179">nom de l’utilisateur actuel hello Hello société.</span><span class="sxs-lookup"><span data-stu-id="5e86a-179">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-180">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="5e86a-180">addresserEmail</span></span>|<span data-ttu-id="5e86a-181">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-181">string</span></span>|<span data-ttu-id="5e86a-182">Adresse de messagerie de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-182">Email address of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-183">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="5e86a-183">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="5e86a-184">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-184">string</span></span>|<span data-ttu-id="5e86a-185">Analytique de tooview URL relative pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-185">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-186">subscriptions</span><span class="sxs-lookup"><span data-stu-id="5e86a-186">subscriptions</span></span>|<span data-ttu-id="5e86a-187">Collection d’entités [Abonnement](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="5e86a-187">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="5e86a-188">abonnements Hello pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-188">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-189">web</span><span class="sxs-lookup"><span data-stu-id="5e86a-189">applications</span></span>|<span data-ttu-id="5e86a-190">Collection d’entités [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="5e86a-190">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="5e86a-191">applications Hello de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-191">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-192">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="5e86a-192">changePasswordUrl</span></span>|<span data-ttu-id="5e86a-193">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-193">string</span></span>|<span data-ttu-id="5e86a-194">mot de passe Hello relatif URL toochange hello l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="5e86a-194">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="5e86a-195">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="5e86a-195">changeNameOrEmailUrl</span></span>|<span data-ttu-id="5e86a-196">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-196">string</span></span>|<span data-ttu-id="5e86a-197">Bonjour nom URL toochange hello et par courrier électronique pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-197">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-198">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="5e86a-198">canChangePassword</span></span>|<span data-ttu-id="5e86a-199">booléenne</span><span class="sxs-lookup"><span data-stu-id="5e86a-199">boolean</span></span>|<span data-ttu-id="5e86a-200">Si l’utilisateur actuel hello peut changer leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5e86a-200">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="5e86a-201">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="5e86a-201">isSystemUser</span></span>|<span data-ttu-id="5e86a-202">booléenne</span><span class="sxs-lookup"><span data-stu-id="5e86a-202">boolean</span></span>|<span data-ttu-id="5e86a-203">Si l’utilisateur actuel hello est un membre de l’un des intégrées de hello [groupes](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="5e86a-203">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5e86a-204">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="5e86a-204">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="5e86a-205"><a name="Applications"></a> Applications</span><span class="sxs-lookup"><span data-stu-id="5e86a-205"><a name="Applications"></a> Applications</span></span>  
 <span data-ttu-id="5e86a-206">Hello **Applications** modèle vous permet de section d’abonnements hello toocustomize de page de profil utilisateur hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-206">hello **Applications** template allows you toocustomize hello subscriptions section of hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e86a-207">![Page Applications du compte d’utilisateur](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM Applications du compte d’utilisateur APIM")</span><span class="sxs-lookup"><span data-stu-id="5e86a-207">![User Account Applications Page](./media/api-management-user-profile-templates/APIM-User-Account-Applications-Page.png "APIM User Account Applications Page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5e86a-208">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="5e86a-208">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="5e86a-209">Commandes</span><span class="sxs-lookup"><span data-stu-id="5e86a-209">Controls</span></span>  
 <span data-ttu-id="5e86a-210">Ce modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5e86a-210">This template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="5e86a-211">app-actions</span><span class="sxs-lookup"><span data-stu-id="5e86a-211">app-actions</span></span>](api-management-page-controls.md#app-actions)  
  
### <a name="data-model"></a><span data-ttu-id="5e86a-212">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="5e86a-212">Data model</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e86a-213">Hello [profil](#Profile), [Applications](#Applications), et [abonnements](#Subscriptions) hello des mêmes données de modèle et de réception hello partagent des modèles de données du même modèle.</span><span class="sxs-lookup"><span data-stu-id="5e86a-213">hello [Profile](#Profile), [Applications](#Applications), and [Subscriptions](#Subscriptions) templates share hello same data model and receive hello same template data.</span></span>  
  
|<span data-ttu-id="5e86a-214">Propriété</span><span class="sxs-lookup"><span data-stu-id="5e86a-214">Property</span></span>|<span data-ttu-id="5e86a-215">Type</span><span class="sxs-lookup"><span data-stu-id="5e86a-215">Type</span></span>|<span data-ttu-id="5e86a-216">Description</span><span class="sxs-lookup"><span data-stu-id="5e86a-216">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="5e86a-217">firstName</span><span class="sxs-lookup"><span data-stu-id="5e86a-217">firstName</span></span>|<span data-ttu-id="5e86a-218">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-218">string</span></span>|<span data-ttu-id="5e86a-219">Prénom de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-219">First name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-220">lastName</span><span class="sxs-lookup"><span data-stu-id="5e86a-220">lastName</span></span>|<span data-ttu-id="5e86a-221">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-221">string</span></span>|<span data-ttu-id="5e86a-222">Nom de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-222">Last name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-223">companyName</span><span class="sxs-lookup"><span data-stu-id="5e86a-223">companyName</span></span>|<span data-ttu-id="5e86a-224">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-224">string</span></span>|<span data-ttu-id="5e86a-225">nom de l’utilisateur actuel hello Hello société.</span><span class="sxs-lookup"><span data-stu-id="5e86a-225">hello company name of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-226">addresserEmail</span><span class="sxs-lookup"><span data-stu-id="5e86a-226">addresserEmail</span></span>|<span data-ttu-id="5e86a-227">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-227">string</span></span>|<span data-ttu-id="5e86a-228">Adresse de messagerie de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-228">Email address of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-229">developersUsageStatisticsLinkk</span><span class="sxs-lookup"><span data-stu-id="5e86a-229">developersUsageStatisticsLinkk</span></span>|<span data-ttu-id="5e86a-230">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-230">string</span></span>|<span data-ttu-id="5e86a-231">Analytique de tooview URL relative pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-231">Relative URL tooview analytics for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-232">subscriptions</span><span class="sxs-lookup"><span data-stu-id="5e86a-232">subscriptions</span></span>|<span data-ttu-id="5e86a-233">Collection d’entités [Abonnement](api-management-template-data-model-reference.md#Subscription).</span><span class="sxs-lookup"><span data-stu-id="5e86a-233">Collection of [Subscription](api-management-template-data-model-reference.md#Subscription) entities.</span></span>|<span data-ttu-id="5e86a-234">abonnements Hello pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-234">hello subscriptions for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-235">web</span><span class="sxs-lookup"><span data-stu-id="5e86a-235">applications</span></span>|<span data-ttu-id="5e86a-236">Collection d’entités [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="5e86a-236">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="5e86a-237">applications Hello de l’utilisateur actuel hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-237">hello applications of hello current user.</span></span>|  
|<span data-ttu-id="5e86a-238">changePasswordUrl</span><span class="sxs-lookup"><span data-stu-id="5e86a-238">changePasswordUrl</span></span>|<span data-ttu-id="5e86a-239">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-239">string</span></span>|<span data-ttu-id="5e86a-240">mot de passe Hello relatif URL toochange hello l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="5e86a-240">hello relative URL toochange hello current user's password.</span></span>|  
|<span data-ttu-id="5e86a-241">changeNameOrEmailUrl</span><span class="sxs-lookup"><span data-stu-id="5e86a-241">changeNameOrEmailUrl</span></span>|<span data-ttu-id="5e86a-242">string</span><span class="sxs-lookup"><span data-stu-id="5e86a-242">string</span></span>|<span data-ttu-id="5e86a-243">Bonjour nom URL toochange hello et par courrier électronique pour l’utilisateur actuel de hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-243">hello relative URL toochange hello name and email for hello current user.</span></span>|  
|<span data-ttu-id="5e86a-244">canChangePassword</span><span class="sxs-lookup"><span data-stu-id="5e86a-244">canChangePassword</span></span>|<span data-ttu-id="5e86a-245">booléenne</span><span class="sxs-lookup"><span data-stu-id="5e86a-245">boolean</span></span>|<span data-ttu-id="5e86a-246">Si l’utilisateur actuel hello peut changer leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="5e86a-246">Whether hello current user can change their password.</span></span>|  
|<span data-ttu-id="5e86a-247">isSystemUser</span><span class="sxs-lookup"><span data-stu-id="5e86a-247">isSystemUser</span></span>|<span data-ttu-id="5e86a-248">booléenne</span><span class="sxs-lookup"><span data-stu-id="5e86a-248">boolean</span></span>|<span data-ttu-id="5e86a-249">Si l’utilisateur actuel hello est un membre de l’un des intégrées de hello [groupes](api-management-key-concepts.md#groups).</span><span class="sxs-lookup"><span data-stu-id="5e86a-249">Whether hello current user is a member of one of hello built-in [groups](api-management-key-concepts.md#groups).</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="5e86a-250">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="5e86a-250">Sample template data</span></span>  
  
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
            "ProductDescription": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
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
            "ProductDescription": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
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
  
##  <span data-ttu-id="5e86a-251"><a name="UpdateAccountInfo"></a> Mettre à jour les informations du compte</span><span class="sxs-lookup"><span data-stu-id="5e86a-251"><a name="UpdateAccountInfo"></a> Update account info</span></span>  
 <span data-ttu-id="5e86a-252">Hello **les informations de compte Uodate** modèle vous permet de toocustomize hello **mettre à jour les informations de compte** page dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="5e86a-252">hello **Uodate account info** template allows you toocustomize hello **Update account information** page in hello developer portal.</span></span>  
  
 <span data-ttu-id="5e86a-253">![Modèles de page Mettre à jour les informations du compte dans le portail des développeurs](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "Modèles de page Mettre à jour les informations du compte dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="5e86a-253">![User Account Info Page Developer Portal Templates](./media/api-management-user-profile-templates/APIM-User-Account-Info-Page-Developer-Portal-Templates.png "APIM User Account Info Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="5e86a-254">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="5e86a-254">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="5e86a-255">Commandes</span><span class="sxs-lookup"><span data-stu-id="5e86a-255">Controls</span></span>  
 <span data-ttu-id="5e86a-256">Ce modèle ne peut pas utiliser de [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="5e86a-256">This template may not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="5e86a-257">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="5e86a-257">Data model</span></span>  
 <span data-ttu-id="5e86a-258">Entité [User account info](api-management-template-data-model-reference.md#UserAccountInfo).</span><span class="sxs-lookup"><span data-stu-id="5e86a-258">[User account info](api-management-template-data-model-reference.md#UserAccountInfo) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="5e86a-259">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="5e86a-259">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="5e86a-260">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e86a-260">Next steps</span></span>
<span data-ttu-id="5e86a-261">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="5e86a-261">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
