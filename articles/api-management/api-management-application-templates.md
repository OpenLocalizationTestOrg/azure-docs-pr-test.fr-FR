---
title: "Modèles Application dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment personnaliser le contenu des pages Application dans le portail des développeurs dans Gestion des API Azure."
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
ms.openlocfilehash: 6d2d44465800219f16866a621d4822614ac9e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="application-templates-in-azure-api-management"></a><span data-ttu-id="34ed4-103">Modèles Application dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="34ed4-103">Application templates in Azure API Management</span></span>
<span data-ttu-id="34ed4-104">Gestion des API Azure vous offre la possibilité de personnaliser le contenu des pages du portail des développeurs à l’aide d’un ensemble de modèles qui configurent leur contenu.</span><span class="sxs-lookup"><span data-stu-id="34ed4-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="34ed4-105">En utilisant la syntaxe [DotLiquid](http://dotliquidmarkup.org/) et l’éditeur de votre choix, comme [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ainsi qu’un ensemble de [ressources de chaîne](api-management-template-resources.md#strings), de [ressources de glyphe](api-management-template-resources.md#glyphs) et de [contrôles de page](api-management-page-controls.md) localisés, vous disposez d’un large choix pour configurer le contenu des pages selon vos besoins à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="34ed4-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="34ed4-106">Les modèles de cette section vous permettent de personnaliser le contenu des pages Application dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="34ed4-106">The templates in this section allow you to customize the content of the Application pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="34ed4-107">Liste d’applications</span><span class="sxs-lookup"><span data-stu-id="34ed4-107">Application list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="34ed4-108">Application</span><span class="sxs-lookup"><span data-stu-id="34ed4-108">Application</span></span>](#Application)  
  
> [!NOTE]
>  <span data-ttu-id="34ed4-109">Les exemples de modèles par défaut inclus dans la documentation suivante sont susceptibles d’être modifiés et améliorés de façon régulière.</span><span class="sxs-lookup"><span data-stu-id="34ed4-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="34ed4-110">Vous pouvez afficher les modèles dynamiques par défaut dans le portail des développeurs en accédant aux modèles individuels souhaités.</span><span class="sxs-lookup"><span data-stu-id="34ed4-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="34ed4-111">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="34ed4-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="34ed4-112"><a name="ProductList"></a> Liste d’applications</span><span class="sxs-lookup"><span data-stu-id="34ed4-112"><a name="ProductList"></a> Application list</span></span>  
 <span data-ttu-id="34ed4-113">Le modèle **Liste d’applications** vous permet de personnaliser le corps de la page Liste d’applications dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="34ed4-113">The **Application list** template allows you to customize the body of the application list page in the developer portal.</span></span>  
  
 <span data-ttu-id="34ed4-114">![Modèles de page Liste d’applications dans le portail des développeurs](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "Modèles de page Liste d’applications dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="34ed4-114">![Application List Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-List-Page-Developer-Portal-Templates.png "APIM Application List Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="34ed4-115">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="34ed4-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="34ed4-116">Commandes</span><span class="sxs-lookup"><span data-stu-id="34ed4-116">Controls</span></span>  
 <span data-ttu-id="34ed4-117">Le modèle `Product list` peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="34ed4-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="34ed4-118">paging-control</span><span class="sxs-lookup"><span data-stu-id="34ed4-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
### <a name="data-model"></a><span data-ttu-id="34ed4-119">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="34ed4-119">Data model</span></span>  
  
|<span data-ttu-id="34ed4-120">Propriété</span><span class="sxs-lookup"><span data-stu-id="34ed4-120">Property</span></span>|<span data-ttu-id="34ed4-121">Type</span><span class="sxs-lookup"><span data-stu-id="34ed4-121">Type</span></span>|<span data-ttu-id="34ed4-122">Description</span><span class="sxs-lookup"><span data-stu-id="34ed4-122">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="34ed4-123">Pagination</span><span class="sxs-lookup"><span data-stu-id="34ed4-123">Paging</span></span>|<span data-ttu-id="34ed4-124">Entité [Paging](api-management-template-data-model-reference.md#Paging).</span><span class="sxs-lookup"><span data-stu-id="34ed4-124">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="34ed4-125">Informations de pagination de la collection d’applications.</span><span class="sxs-lookup"><span data-stu-id="34ed4-125">The paging information for the applications collection.</span></span>|  
|<span data-ttu-id="34ed4-126">Applications</span><span class="sxs-lookup"><span data-stu-id="34ed4-126">Applications</span></span>|<span data-ttu-id="34ed4-127">Collection d’entités [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="34ed4-127">Collection of [Application](api-management-template-data-model-reference.md#Application) entities.</span></span>|<span data-ttu-id="34ed4-128">Applications visibles par l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="34ed4-128">The applications visible to the current user.</span></span>|  
|<span data-ttu-id="34ed4-129">CategoryName</span><span class="sxs-lookup"><span data-stu-id="34ed4-129">CategoryName</span></span>|<span data-ttu-id="34ed4-130">string</span><span class="sxs-lookup"><span data-stu-id="34ed4-130">string</span></span>|<span data-ttu-id="34ed4-131">Catégorie de l’application.</span><span class="sxs-lookup"><span data-stu-id="34ed4-131">The category of application.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="34ed4-132">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="34ed4-132">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="34ed4-133"><a name="Application"></a> Application</span><span class="sxs-lookup"><span data-stu-id="34ed4-133"><a name="Application"></a> Application</span></span>  
 <span data-ttu-id="34ed4-134">Le modèle **Application** vous permet de personnaliser le corps de la page Application dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="34ed4-134">The **Application** template allows you to customize the body of the application page in the developer portal.</span></span>  
  
 <span data-ttu-id="34ed4-135">![Modèles de page Application dans le portail des développeurs](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "Modèles de page Application dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="34ed4-135">![Application Page Developer Portal Templates](./media/api-management-application-templates/APIM-Application-Page-Developer-Portal-Templates.png "APIM Application Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="34ed4-136">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="34ed4-136">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="34ed4-137">Commandes</span><span class="sxs-lookup"><span data-stu-id="34ed4-137">Controls</span></span>  
 <span data-ttu-id="34ed4-138">Le modèle `Application` ne permet pas d’utiliser de [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="34ed4-138">The `Application` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="34ed4-139">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="34ed4-139">Data model</span></span>  
 <span data-ttu-id="34ed4-140">Entité [Application](api-management-template-data-model-reference.md#Application).</span><span class="sxs-lookup"><span data-stu-id="34ed4-140">[Application](api-management-template-data-model-reference.md#Application) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="34ed4-141">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="34ed4-141">Sample template data</span></span>  
  
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

## <a name="next-steps"></a><span data-ttu-id="34ed4-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34ed4-142">Next steps</span></span>
<span data-ttu-id="34ed4-143">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="34ed4-143">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>