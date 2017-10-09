---
title: "modèles d’aaaIssue dans Gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toocustomize hello le contenu des pages de problème hello dans le portail des développeurs dans Gestion des API Azure hello."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 47da4bb2-426e-4e53-8fa7-214ee2e3ab37
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: e12902e52c164f73902a97f15ea550790dfecf1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="6dc20-103">Modèles Problème dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="6dc20-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="6dc20-104">Gestion des API Azure fournit que Hello de contenu de hello toocustomize possibilité de pages du portail développeur à l’aide d’un ensemble de modèles que configurer leur contenu.</span><span class="sxs-lookup"><span data-stu-id="6dc20-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="6dc20-105">À l’aide de [DotLiquid](http://dotliquidmarkup.org/) syntaxe et hello l’éditeur de votre choix, tel que [DotLiquid pour les concepteurs](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), et un ensemble fourni de localisée [ressources de type chaîne](api-management-template-resources.md#strings), [ Ressources de glyphe](api-management-template-resources.md#glyphs), et [Page les contrôles](api-management-page-controls.md), vous avez une grande souplesse tooconfigure hello contenu hello pages comme vous le souhaitez à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="6dc20-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="6dc20-106">modèles de Hello dans cette section vous autoriser le contenu de hello toocustomize de pages de problème hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="6dc20-106">hello templates in this section allow you toocustomize hello content of hello Issue pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="6dc20-107">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="6dc20-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="6dc20-108">Exemples de modèles par défaut sont inclus dans hello suivant la documentation, mais sont toochange sujet en raison des améliorations de toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="6dc20-108">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="6dc20-109">Vous pouvez afficher les modèles par défaut dynamique hello dans le portail des développeurs hello en naviguant toohello souhaitée des modèles individuels.</span><span class="sxs-lookup"><span data-stu-id="6dc20-109">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="6dc20-110">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6dc20-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="6dc20-111"><a name="IssueList"></a> Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="6dc20-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="6dc20-112">Hello **liste des problèmes** modèle vous permet de corps de hello toocustomize de page de liste hello problème dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="6dc20-112">hello **Issue list** template allows you toocustomize hello body of hello issue list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="6dc20-113">![Liste des problèmes dans le portail des développeurs](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "Liste des problèmes APIM dans le portail des développeurs")</span><span class="sxs-lookup"><span data-stu-id="6dc20-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="6dc20-114">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="6dc20-114">Default template</span></span>  
  
```xml  
<div class="row">  
  <div class="col-md-9">  
    <h2>{% localized "IssuesStrings|WebIssuesIndexTitle" %}</h2>  
  </div>  
</div>  
<div class="row">  
  <div class="col-md-12">  
    {% if issues.size > 0 %}  
    <ul class="list-unstyled">  
      {% capture reportedBy %}{% localized "IssuesStrings|WebIssuesStatusReportedBy" %}{% endcapture %}  
      {% assign replaceString0 = '{0}' %}  
      {% assign replaceString1 = '{1}' %}  
      {% for issue in issues %}  
      <li>  
        <h3>  
          <a href="/issues/{{issue.id}}">{{issue.title}}</a>  
        </h3>  
        <p>{{issue.description}}</p>  
        <em>  
          {% capture state %}{{issue.issueState}}{% endcapture %}  
          {% capture devName %}{{issue.subscriptionDeveloperName}}{% endcapture %}  
          {% capture str1 %}{{ reportedBy | replace : replaceString0, state }}{% endcapture %}  
          {{ str1 | replace : replaceString1, devName }}  
          <span class="UtcDateElement">{{ issue.reportedOn | date: "r" }}</span>  
        </em>  
      </li>  
      {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    {% if canReportIssue %}  
    <a class="btn btn-primary" id="createIssue" href="/Issues/Create">{% localized "IssuesStrings|WebIssuesReportIssueButton" %}</a>  
    {% elsif isAuthenticated %}  
    <hr />  
    <p>{% localized "IssuesStrings|WebIssuesNoActiveSubscriptions" %}</p>  
    {% else %}  
    <hr />  
    <p>  
      {% capture signIntext %}{% localized "IssuesStrings|WebIssuesNotSignin" %}{% endcapture %}  
      {% capture link %}<a href="/signin">{% localized "IssuesStrings|WebIssuesSignIn" %}</a>{% endcapture %}  
      {{ signIntext | replace : replaceString0, link }}  
    </p>  
    {% endif %}  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="6dc20-115">Commandes</span><span class="sxs-lookup"><span data-stu-id="6dc20-115">Controls</span></span>  
 <span data-ttu-id="6dc20-116">Hello `Issue list` modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="6dc20-116">hello `Issue list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="6dc20-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="6dc20-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="6dc20-118">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="6dc20-118">Data model</span></span>  
  
|<span data-ttu-id="6dc20-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="6dc20-119">Property</span></span>|<span data-ttu-id="6dc20-120">Type</span><span class="sxs-lookup"><span data-stu-id="6dc20-120">Type</span></span>|<span data-ttu-id="6dc20-121">Description</span><span class="sxs-lookup"><span data-stu-id="6dc20-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="6dc20-122">Problèmes</span><span class="sxs-lookup"><span data-stu-id="6dc20-122">Issues</span></span>|<span data-ttu-id="6dc20-123">Collection d’entités [Problème](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="6dc20-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="6dc20-124">Hello problèmes toohello visible l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="6dc20-124">hello issues visible toohello current user.</span></span>|  
|<span data-ttu-id="6dc20-125">Pagination</span><span class="sxs-lookup"><span data-stu-id="6dc20-125">Paging</span></span>|<span data-ttu-id="6dc20-126">Entité [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="6dc20-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="6dc20-127">informations de pagination Hello pour une collection d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="6dc20-127">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="6dc20-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="6dc20-128">IsAuthenticated</span></span>|<span data-ttu-id="6dc20-129">booléenne</span><span class="sxs-lookup"><span data-stu-id="6dc20-129">boolean</span></span>|<span data-ttu-id="6dc20-130">Indique si l’utilisateur actuel hello est connecté toohello portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="6dc20-130">Whether hello current user is signed-in toohello developer portal.</span></span>|  
|<span data-ttu-id="6dc20-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="6dc20-131">CanReportIssues</span></span>|<span data-ttu-id="6dc20-132">booléenne</span><span class="sxs-lookup"><span data-stu-id="6dc20-132">boolean</span></span>|<span data-ttu-id="6dc20-133">Indique si l’utilisateur actuel hello possède autorisations toofile un problème.</span><span class="sxs-lookup"><span data-stu-id="6dc20-133">Whether hello current user has permissions toofile an issue.</span></span>|  
|<span data-ttu-id="6dc20-134">Search</span><span class="sxs-lookup"><span data-stu-id="6dc20-134">Search</span></span>|<span data-ttu-id="6dc20-135">string</span><span class="sxs-lookup"><span data-stu-id="6dc20-135">string</span></span>|<span data-ttu-id="6dc20-136">Cette propriété est déconseillée et ne doit pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="6dc20-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="6dc20-137">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="6dc20-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how tooconnect my application toohello API",  
            "Description": "I'm having trouble connecting my application toohello backend API.",  
            "SubscriptionDeveloperName": "Clayton",  
            "IssueState": "Proposed",  
            "ReportedOn": "2016-04-04T18:46:35.64",  
            "Comments": null,  
            "Attachments": null,  
            "Services": null  
        }  
    ],  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "IsAuthenticated": true,  
    "CanReportIssue": true,  
    "Search": null  
}  
```

## <a name="next-steps"></a><span data-ttu-id="6dc20-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6dc20-138">Next steps</span></span>
<span data-ttu-id="6dc20-139">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6dc20-139">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
