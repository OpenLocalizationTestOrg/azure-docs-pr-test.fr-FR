---
title: "modèles d’aaaApplication dans Gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toocustomize hello contenu hello de pages d’Application dans le portail des développeurs dans Gestion des API Azure hello."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: f3122c4d-e10e-4cdf-977b-36e8f4133fc8
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: f4dc078be7163b047ca2e640a9065ba9e5ba709e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="1a6e9-103">Modèles Application dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="1a6e9-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="1a6e9-104">Gestion des API Azure fournit que Hello de contenu de hello toocustomize possibilité de pages du portail développeur à l’aide d’un ensemble de modèles que configurer leur contenu.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="1a6e9-105">À l’aide de [DotLiquid](http://dotliquidmarkup.org/) syntaxe et hello l’éditeur de votre choix, tel que [DotLiquid pour les concepteurs](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), et un ensemble fourni de localisée [ressources de type chaîne](api-management-template-resources.md#strings), [ Ressources de glyphe](api-management-template-resources.md#glyphs), et [Page les contrôles](api-management-page-controls.md), vous avez une grande souplesse tooconfigure hello contenu hello pages comme vous le souhaitez à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="1a6e9-106">modèles de Hello dans cette section vous autoriser le contenu de hello toocustomize hello de pages d’Application dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-106">hello templates in this section allow you toocustomize hello content of hello Application pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="1a6e9-107">Liste d’applications</span><span class="sxs-lookup"><span data-stu-id="1a6e9-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="1a6e9-108">Application</span><span class="sxs-lookup"><span data-stu-id="1a6e9-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="1a6e9-109">Exemples de modèles par défaut sont inclus dans hello suivant la documentation, mais sont toochange sujet en raison des améliorations de toocontinuous.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="1a6e9-110">Vous pouvez afficher les modèles par défaut dynamique hello dans le portail des développeurs hello en naviguant toohello souhaitée des modèles individuels.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="1a6e9-111">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="1a6e9-112"><a name="ProductList"></a> Liste d’applications</span><span class="sxs-lookup"><span data-stu-id="1a6e9-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="1a6e9-113">Hello **liste Application** modèle vous permet de corps de hello toocustomize de page de liste application hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-113">hello **Application list** template allows you toocustomize hello body of hello application list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1a6e9-114">![Modèles de page Liste d’applications dans le portail des développeurs](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "Modèles de page Liste d’applications dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="1a6e9-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="1a6e9-115">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="1a6e9-115">Default template</span></span>  
  
```xml  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "AppStrings|WebApplicationsHeader" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if applications.size > 0 %}  
        <ul class="list-unstyled">  
        {% for app in applications %}  
            <li>  
            {% if app.application.icon.url != "" %}  
                <aside>  
                    <a href="/applications/details/{{app.application.id}}"><img src="{{app.application.icon.url}}" alt="App Icon" /></a>  
                </aside>  
            {% endif %}  
                <h3><a href="/applications/details/{{app.application.id}}">{{app.application.title}}</a></h3>  
                {{app.application.description}}  
            </li>     
        {% endfor %}  
        </ul>  
        <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="1a6e9-116">Commandes</span><span class="sxs-lookup"><span data-stu-id="1a6e9-116">Controls</span></span>  
 <span data-ttu-id="1a6e9-117">Hello `Product list` modèle peut utiliser des éléments suivants de hello [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="1a6e9-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="1a6e9-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="1a6e9-119">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="1a6e9-119">Data model</span></span>  
  
|<span data-ttu-id="1a6e9-120">Propriété</span><span class="sxs-lookup"><span data-stu-id="1a6e9-120">Property</span></span>|<span data-ttu-id="1a6e9-121">Type</span><span class="sxs-lookup"><span data-stu-id="1a6e9-121">Type</span></span>|<span data-ttu-id="1a6e9-122">Description</span><span class="sxs-lookup"><span data-stu-id="1a6e9-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="1a6e9-123">Pagination</span><span class="sxs-lookup"><span data-stu-id="1a6e9-123">Paging</span></span>|<span data-ttu-id="1a6e9-124">Entité [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="1a6e9-125">informations de pagination Hello pour une collection d’applications hello.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-125">hello paging information for hello applications collection.</span></span>|  
|<span data-ttu-id="1a6e9-126">Applications</span><span class="sxs-lookup"><span data-stu-id="1a6e9-126">Applications</span></span>|<span data-ttu-id="1a6e9-127">Collection d’entités [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="1a6e9-128">Hello applications toohello visible l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-128">hello applications visible toohello current user.</span></span>|  
|<span data-ttu-id="1a6e9-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="1a6e9-129">CategoryName</span></span>|<span data-ttu-id="1a6e9-130">string</span><span class="sxs-lookup"><span data-stu-id="1a6e9-130">string</span></span>|<span data-ttu-id="1a6e9-131">catégorie Hello d’application.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-131">hello category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="1a6e9-132">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="1a6e9-132">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 1,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Applications": [  
        {  
            "Application": {  
                "Id": "5702b96fb16653124c8f9ba8",  
                "Title": "Contoso Calculator",  
                "Description": "A simple online calculator.",  
                "Url": null,  
                "Version": null,  
                "Requirements": "Free application with no requirements.",  
                "State": 2,  
                "RegistrationDate": "2016-04-04T18:59:00",  
                "CategoryId": 5,  
                "DeveloperId": "5702b5b0b16653124c8f9ba4",  
                "Attachments": [  
                    {  
                        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                        "Type": "Icon",  
                        "ContentType": "image/png"  
                    },  
                    {  
                        "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
                        "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
                        "Type": "Screenshot",  
                        "ContentType": "image/png"  
                    }  
                ],  
                "Icon": {  
                    "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
                    "Url": "https://apimgmtst65gdjvjrgdbfhr4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
                    "Type": "Icon",  
                    "ContentType": "image/png"  
                }  
            },  
            "CategoryName": "Finance"  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="1a6e9-133"><a name="Application"></a> Application</span><span class="sxs-lookup"><span data-stu-id="1a6e9-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="1a6e9-134">Hello **Application** modèle vous permet de corps de hello toocustomize de page de l’application hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="1a6e9-134">hello **Application** template allows you toocustomize hello body of hello application page in hello developer portal.</span></span>  
  
 <span data-ttu-id="1a6e9-135">![Modèles de page Application dans le portail des développeurs](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "Modèles de page Application dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="1a6e9-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="1a6e9-136">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="1a6e9-136">Default template</span></span>  
  
```xml  
<h2>{{title}}</h2>  
{% if icon.url != "" %}  
<aside class="applications_aside">  
  <div class="image-placeholder">  
    <img src="{{icon.url}}" alt="Application Icon" />  
  </div>  
</aside>  
{% endif %}  
  
<article>  
  {% if url != "" %}  
    <a target="_blank" href="{{url}}">{{url}}</a>  
  {% endif %}  
  
  <p>{{description}}</p>  
  
  {% if requirements != null %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsRequirementsHeader" %}</h3>  
  <p>{{requirements}}</p>  
  {% endif %}  
  
  {% if attachments.size > 0 %}  
  <h3>{% localized "AppDetailsStrings|WebApplicationsScreenshotsHeader" %}</h3>  
    {% for screenshot in attachments %}  
      {% if screenshot.type != "Icon" %}  
      <a href="{{screenshot.url}}" data-lightbox="example-set">  
          <img src="/Developer/Applications/Thumbnail?url={{screenshot.url}}" alt='{% localized "AppDetailsStrings|WebApplicationsScreenshotAlt" %}' />  
      </a>  
      {% endif %}  
    {% endfor %}  
  {% endif %}  
</article>  
  
```  
  
### <a name="controls"></a><span data-ttu-id="1a6e9-137">Commandes</span><span class="sxs-lookup"><span data-stu-id="1a6e9-137">Controls</span></span>  
 <span data-ttu-id="1a6e9-138">Hello `Application` modèle n’autorise pas l’utilisation de hello de n’importe quel [page les contrôles](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-138">hello `Application` template does not allow hello use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="1a6e9-139">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="1a6e9-139">Data model</span></span>  
 <span data-ttu-id="1a6e9-140">Entité [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="1a6e9-141">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="1a6e9-141">Sample template data</span></span>  
  
```json  
{  
    "Id": "5702b96fb16653124c8f9ba8",  
    "Title": "Contoso Calculator",  
    "Description": "A simple online calculator.",  
    "Url": null,  
    "Version": null,  
    "Requirements": "Free application with no requirements.",  
    "State": 2,  
    "RegistrationDate": "2016-04-04T18:59:00",  
    "CategoryId": 5,  
    "DeveloperId": "5702b5b0b16653124c8f9ba4",  
    "Attachments": [  
        {  
            "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
            "Type": "Icon",  
            "ContentType": "image/png"  
        },  
        {  
            "UniqueId": "2b4fa5dd-00ff-4a8f-b1b7-51e715849ede",  
            "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/2b4fa5dd-00ff-4a8f-b1b7-51e715849ede.png",  
            "Type": "Screenshot",  
            "ContentType": "image/png"  
        }  
    ],  
    "Icon": {  
        "UniqueId": "a58af001-e6c3-45fd-8bc9-c60a1875c3f6",  
        "Url": "https://apimgmtst3aybshdqqcqrle4.blob.core.windows.net/content/applications/a58af001-e6c3-45fd-8bc9-c60a1875c3f6.png",  
        "Type": "Icon",  
        "ContentType": "image/png"  
    }  
}  
```

## <a name="next-steps"></a><span data-ttu-id="1a6e9-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1a6e9-142">Next steps</span></span>
<span data-ttu-id="1a6e9-143">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1a6e9-143">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
