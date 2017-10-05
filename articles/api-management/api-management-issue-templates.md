---
title: "Modèles Problème dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment personnaliser le contenu des pages Problème dans le portail des développeurs dans Gestion des API Azure."
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
ms.openlocfilehash: e13344df198bca4f73c75fa58221436b94e2f258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="issue-templates-in-azure-api-management"></a><span data-ttu-id="b5a4d-103">Modèles Problème dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="b5a4d-103">Issue templates in Azure API Management</span></span>
<span data-ttu-id="b5a4d-104">Gestion des API Azure vous offre la possibilité de personnaliser le contenu des pages du portail des développeurs à l’aide d’un ensemble de modèles qui configurent leur contenu.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="b5a4d-105">En utilisant la syntaxe [DotLiquid](http://dotliquidmarkup.org/) et l’éditeur de votre choix, comme [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ainsi qu’un ensemble de [ressources de chaîne](api-management-template-resources.md#strings), de [ressources de glyphe](api-management-template-resources.md#glyphs) et de [contrôles de page](api-management-page-controls.md) localisés, vous disposez d’un large choix pour configurer le contenu des pages selon vos besoins à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="b5a4d-106">Les modèles de cette section vous permettent de personnaliser le contenu des pages Problème dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-106">The templates in this section allow you to customize the content of the Issue pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="b5a4d-107">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="b5a4d-107">Issue list</span></span>](#IssueList)  
  
> [!NOTE]
>  <span data-ttu-id="b5a4d-108">Les exemples de modèles par défaut inclus dans la documentation suivante sont susceptibles d’être modifiés et améliorés de façon régulière.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-108">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="b5a4d-109">Vous pouvez afficher les modèles dynamiques par défaut dans le portail des développeurs en accédant aux modèles individuels souhaités.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-109">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="b5a4d-110">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b5a4d-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>  
  
##  <span data-ttu-id="b5a4d-111"><a name="IssueList"></a> Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="b5a4d-111"><a name="IssueList"></a> Issue list</span></span>  
 <span data-ttu-id="b5a4d-112">Le modèle **Liste des problèmes** vous permet de personnaliser le corps de la page répertoriant une liste de problèmes dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-112">The **Issue list** template allows you to customize the body of the issue list page in the developer portal.</span></span>  
  
 <span data-ttu-id="b5a4d-113">![Liste des problèmes dans le portail des développeurs](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "Liste des problèmes APIM dans le portail des développeurs")</span><span class="sxs-lookup"><span data-stu-id="b5a4d-113">![Issue List Developer Portal](./media/api-management-issue-templates/APIM-Issue-List-Developer-Portal.png "APIM Issue List Developer Portal")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="b5a4d-114">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="b5a4d-114">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="b5a4d-115">Commandes</span><span class="sxs-lookup"><span data-stu-id="b5a4d-115">Controls</span></span>  
 <span data-ttu-id="b5a4d-116">Le modèle `Issue list` peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-116">The `Issue list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="b5a4d-117">paging-control</span><span class="sxs-lookup"><span data-stu-id="b5a4d-117">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="b5a4d-118">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="b5a4d-118">Data model</span></span>  
  
|<span data-ttu-id="b5a4d-119">Propriété</span><span class="sxs-lookup"><span data-stu-id="b5a4d-119">Property</span></span>|<span data-ttu-id="b5a4d-120">Type</span><span class="sxs-lookup"><span data-stu-id="b5a4d-120">Type</span></span>|<span data-ttu-id="b5a4d-121">Description</span><span class="sxs-lookup"><span data-stu-id="b5a4d-121">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="b5a4d-122">Problèmes</span><span class="sxs-lookup"><span data-stu-id="b5a4d-122">Issues</span></span>|<span data-ttu-id="b5a4d-123">Collection d’entités [Problème](api-management-template-data-model-reference.md#Issue).</span><span class="sxs-lookup"><span data-stu-id="b5a4d-123">Collection of [Issue](api-management-template-data-model-reference.md#Issue) entities.</span></span>|<span data-ttu-id="b5a4d-124">Problèmes visibles par l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-124">The issues visible to the current user.</span></span>|  
|<span data-ttu-id="b5a4d-125">Pagination</span><span class="sxs-lookup"><span data-stu-id="b5a4d-125">Paging</span></span>|<span data-ttu-id="b5a4d-126">Entité [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="b5a4d-126">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="b5a4d-127">Informations de pagination de la collection d’applications.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-127">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="b5a4d-128">IsAuthenticated</span><span class="sxs-lookup"><span data-stu-id="b5a4d-128">IsAuthenticated</span></span>|<span data-ttu-id="b5a4d-129">booléenne</span><span class="sxs-lookup"><span data-stu-id="b5a4d-129">boolean</span></span>|<span data-ttu-id="b5a4d-130">Indique si l’utilisateur actuel est connecté au portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-130">Whether the current user is signed-in to the developer portal.</span></span>|  
|<span data-ttu-id="b5a4d-131">CanReportIssues</span><span class="sxs-lookup"><span data-stu-id="b5a4d-131">CanReportIssues</span></span>|<span data-ttu-id="b5a4d-132">booléenne</span><span class="sxs-lookup"><span data-stu-id="b5a4d-132">boolean</span></span>|<span data-ttu-id="b5a4d-133">Indique si l’utilisateur actuel dispose des autorisations pour poser une question.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-133">Whether the current user has permissions to file an issue.</span></span>|  
|<span data-ttu-id="b5a4d-134">Search</span><span class="sxs-lookup"><span data-stu-id="b5a4d-134">Search</span></span>|<span data-ttu-id="b5a4d-135">string</span><span class="sxs-lookup"><span data-stu-id="b5a4d-135">string</span></span>|<span data-ttu-id="b5a4d-136">Cette propriété est déconseillée et ne doit pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-136">This property is deprecated and should not be used.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="b5a4d-137">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="b5a4d-137">Sample template data</span></span>  
  
```json  
{  
    "Issues": [  
        {  
            "Id": "5702b68bb16653124c8f9ba7",  
            "ApiId": "570275f1b16653124c8f9ba3",  
            "Title": "I couldn't figure out how to connect my application to the API",  
            "Description": "I'm having trouble connecting my application to the backend API.",  
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

## <a name="next-steps"></a><span data-ttu-id="b5a4d-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5a4d-138">Next steps</span></span>
<span data-ttu-id="b5a4d-139">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b5a4d-139">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>