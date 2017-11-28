---
title: "Modèles d’API dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment personnaliser le contenu des pages API dans le portail des développeurs dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 3642fd09-ba98-4358-93a6-c48ab0500431
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 3802868470f0f74cd1f895a00195259861ea16f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="api-templates-in-azure-api-management"></a><span data-ttu-id="a7b8d-103">Modèles d’API dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="a7b8d-103">API templates in Azure API Management</span></span>
<span data-ttu-id="a7b8d-104">Gestion des API Azure vous offre la possibilité de personnaliser le contenu des pages du portail des développeurs à l’aide d’un ensemble de modèles qui configurent leur contenu.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="a7b8d-105">En utilisant la syntaxe [DotLiquid](http://dotliquidmarkup.org/) et l’éditeur de votre choix, comme [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ainsi qu’un ensemble de [ressources de chaîne](api-management-template-resources.md#strings), de [ressources de glyphe](api-management-template-resources.md#glyphs) et de [contrôles de page](api-management-page-controls.md) localisés, vous disposez d’un large choix pour configurer le contenu des pages selon vos besoins à l’aide de ces modèles.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="a7b8d-106">Les modèles de cette section vous permettent de personnaliser le contenu des pages API dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-106">The templates in this section allow you to customize the content of the API pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="a7b8d-107">Liste d’API</span><span class="sxs-lookup"><span data-stu-id="a7b8d-107">API list</span></span>](#APIList)  
-   [<span data-ttu-id="a7b8d-108">Opération</span><span class="sxs-lookup"><span data-stu-id="a7b8d-108">Operation</span></span>](#Product)  
-   [<span data-ttu-id="a7b8d-109">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="a7b8d-109">Code samples</span></span>](#CodeSamples)  
    -   [<span data-ttu-id="a7b8d-110">Curl</span><span class="sxs-lookup"><span data-stu-id="a7b8d-110">Curl</span></span>](#Curl)  
    -   [<span data-ttu-id="a7b8d-111">C#</span><span class="sxs-lookup"><span data-stu-id="a7b8d-111">C#</span></span>](#CSharp)  
    -   [<span data-ttu-id="a7b8d-112">Java</span><span class="sxs-lookup"><span data-stu-id="a7b8d-112">Java</span></span>](#Stub)  
    -   [<span data-ttu-id="a7b8d-113">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a7b8d-113">JavaScript</span></span>](#JavaScript)  
    -   [<span data-ttu-id="a7b8d-114">Objective C</span><span class="sxs-lookup"><span data-stu-id="a7b8d-114">Objective C</span></span>](#ObjectiveC)  
    -   [<span data-ttu-id="a7b8d-115">PHP</span><span class="sxs-lookup"><span data-stu-id="a7b8d-115">PHP</span></span>](#PHP)  
    -   [<span data-ttu-id="a7b8d-116">Python</span><span class="sxs-lookup"><span data-stu-id="a7b8d-116">Python</span></span>](#Python)  
    -   [<span data-ttu-id="a7b8d-117">Ruby</span><span class="sxs-lookup"><span data-stu-id="a7b8d-117">Ruby</span></span>](#Ruby)  

> [!NOTE]
>  <span data-ttu-id="a7b8d-118">Les exemples de modèles par défaut inclus dans la documentation suivante sont susceptibles d’être modifiés et améliorés de façon régulière.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-118">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="a7b8d-119">Vous pouvez afficher les modèles dynamiques par défaut dans le portail des développeurs en accédant aux modèles individuels souhaités.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-119">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="a7b8d-120">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-120">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="a7b8d-121"><a name="APIList"></a> Liste d’API</span><span class="sxs-lookup"><span data-stu-id="a7b8d-121"><a name="APIList"></a> API list</span></span>  
 <span data-ttu-id="a7b8d-122">Le modèle **Liste d’API** vous permet de personnaliser le corps de la page Liste d’API dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-122">The **API list** template allows you to customize the body of the API list page in the developer portal.</span></span>  
  
 <span data-ttu-id="a7b8d-123">![Liste d’API dans le portail des développeur](./media/api-management-api-templates/APIM-Developer-Portal-Templates-API-List.png "Modèles Liste d’API dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="a7b8d-123">![Developer Portal API List](./media/api-management-api-templates/APIM-Developer-Portal-Templates-API-List.png "APIM Developer Portal Templates API List")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="a7b8d-124">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-124">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ApisStrings|PageTitleApis" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if apis.size > 0 %}  
    <ol class="list-unstyled">  
    {% for api in apis %}  
        <li>  
        <h3>  
          <a href="/docs/services/{{api.id}}">{{api.name}}</a>  
        </h3>  
       {{api.description}}  
      </li>  
    {% endfor %}  
    </ol>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="a7b8d-125">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-125">Controls</span></span>  
 <span data-ttu-id="a7b8d-126">Le modèle `API list` peut utiliser les [contrôles de page](api-management-page-controls.md) suivants.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-126">The `API list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="a7b8d-127">paging-control</span><span class="sxs-lookup"><span data-stu-id="a7b8d-127">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="a7b8d-128">search-control</span><span class="sxs-lookup"><span data-stu-id="a7b8d-128">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="a7b8d-129">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-129">Data model</span></span>  
  
|<span data-ttu-id="a7b8d-130">Propriété</span><span class="sxs-lookup"><span data-stu-id="a7b8d-130">Property</span></span>|<span data-ttu-id="a7b8d-131">Type</span><span class="sxs-lookup"><span data-stu-id="a7b8d-131">Type</span></span>|<span data-ttu-id="a7b8d-132">Description</span><span class="sxs-lookup"><span data-stu-id="a7b8d-132">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="a7b8d-133">apis</span><span class="sxs-lookup"><span data-stu-id="a7b8d-133">apis</span></span>|<span data-ttu-id="a7b8d-134">Collection d’entités [API summary](api-management-template-data-model-reference.md#APISummary).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-134">Collection of [API summary](api-management-template-data-model-reference.md#APISummary) entities.</span></span>|<span data-ttu-id="a7b8d-135">API visibles par l’utilisateur actuel.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-135">The APIs visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-136">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-136">Sample template data</span></span>  
  
```json  
{  
    "apis": [  
        {  
            "id": "570275f1b16653124c8f9ba3",  
            "name": "Basic Calculator",  
            "description": "Arithmetics is just a call away!"  
        },  
        {  
            "id": "57026e30de15d80041040001",  
            "name": "Echo API",  
            "description": null  
        }  
    ],  
    "pageTitle": "APIs"  
}  
```  
  
##  <span data-ttu-id="a7b8d-137"><a name="Product"></a> Opération</span><span class="sxs-lookup"><span data-stu-id="a7b8d-137"><a name="Product"></a> Operation</span></span>  
 <span data-ttu-id="a7b8d-138">Le modèle **Opération** vous permet de personnaliser le corps de la page Opération dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-138">The **Operation** template allows you to customize the body of the operation page in the developer portal.</span></span>  
  
 <span data-ttu-id="a7b8d-139">![Page Opération dans le portail des développeur](./media/api-management-api-templates/APIM-Developer-Portal-templates-Operation-page.png "Modèles de page Opération dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="a7b8d-139">![Developer Portal Operation page](./media/api-management-api-templates/APIM-Developer-Portal-templates-Operation-page.png "APIM Developer Portal templates Operation page")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="a7b8d-140">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-140">Default template</span></span>  
  
```xml  
<h2>{{api.name}}</h2>  
<p>{{api.description }}</p>  
  
<div class="panel">  
    <h3>{{operation.name}}</h3>  
    <p>{{operation.description }}</p>  
    <a class="btn btn-primary" href="{{consoleUrl}}" id="btnOpenConsole" role="button">  
        Try it  
    </a>  
</div>  
  
<h4>{% localized "Documentation|SectionHeadingRequestUrl" %}</h4>  
<div class="panel">  
    <div class="panel-body">  
        <label>{{ sampleUrl | escape }}</label>  
    </div>  
</div>  
  
{% if operation.request %}  
    {% if operation.request.parameters.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestParameters" %}</h4>  
  
        <div class="panel">  
            {% for parameter in operation.request.parameters %}  
                 <div class="row panel-body">  
                    <div class="col-md-3">  
                        <label>{{parameter.name}}</label>  
                        {% unless parameter.required %}  
                            <span class="text-muted">({% localized "Documentation|FormLabelSubtextOptional" %})</span>  
                        {% endunless %}  
                    </div>  
                    <div class="col-md-1">  
                        {{parameter.typeName}}  
                    </div>  
                    <div class="col-md-8">  
                        {{parameter.description}}  
                    </div>  
                 </div>  
            {% endfor %}  
        </div>  
    {% endif %}  
  
    {% if operation.request.headers.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestHeaders" %}</h4>  
        <div class="panel">  
            {% for header in operation.request.headers %}  
                 <div class="row panel-body">  
                    <div class="col-md-3">  
                        <label>{{header.name}}</label>  
                        {%unless header.required %}  
                            <span class="text-muted">({% localized "Documentation|FormLabelSubtextOptional" %})</span>  
                        {% endunless %}  
                    </div>  
                    <div class="col-md-1">  
                        {{header.typeName}}  
                    </div>  
                    <div class="col-md-8">  
                        {{header.description}}  
                    </div>  
                 </div>  
            {% endfor %}  
        </div>  
    {% endif %}  
  
    {% if operation.request.description or operation.request.representations.size > 0 %}  
        <h4>{% localized "Documentation|SectionHeadingRequestBody" %}</h4>  
        <div class="panel">  
            {% if operation.request.description %}  
                <p>{{operation.request.description }}</p>     
            {% endif %}  
  
            {% if operation.request.representations.size > 0 %}  
                <div role="tabpanel">  
                    <ul class="nav nav-tabs" role="tablist">  
                        {% for representation in operation.request.representations %}  
                            <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                                <a href="#requesttab{{forloop.index}}" role="tab" data-toggle="tab">  
                                    {{representation.contentType}}  
                                </a>  
                            </li>  
                        {% endfor %}  
                    </ul>  
                    <div class="tab-content tab-content-boxed">  
                        {% for representation in operation.request.representations %}  
                            <div id="requesttab{{forloop.index}}" role="tabpanel" class="tab-pane snippet{% if forloop.first %} active{% endif %}">  
  
                                {% if representation.sample or representation.schema %}   
                                <div role="tabpanel">  
                                    {% if representation.sample and representation.schema %}   
                                    <ul class="nav nav-tabs-borderless" role="tablist">  
                                        <li role="presentation" class="active">  
                                            <a href="#requesttab{{forloop.index}}sample" role="tab" data-toggle="tab">Sample</a>  
                                        </li>  
                                        <li role="presentation">  
                                            <a href="#requesttab{{forloop.index}}schema" role="tab" data-toggle="tab">Schema</a>  
                                        </li>  
                                    </ul>  
                                    {% endif %}  
  
                                    <div class="tab-content">  
                                        {% if representation.sample %}  
                                        <div id="requesttab{{forloop.index}}sample" role="tabpanel" class="tab-pane snippet active">  
                                            <pre><code class="{{representation.Brush}}">{{ representation.sample | escape }}</code></pre>  
                                        </div>  
                                        {% endif %}  
  
                                        {% if representation.schema %}  
                                        <div id="requesttab{{forloop.index}}schema" role="tabpanel" class="tab-pane snippet">  
                                            <pre><code class="{{representation.Brush}}">{{ representation.schema | escape }}</code></pre>  
                                        </div>  
                                        {% endif %}  
                                    </div>  
                                </div>  
                                {% endif %}  
                            </div>  
                        {% endfor %}  
                    </div>  
                </div>  
            {% endif %}  
  
            <div class="clearfix"></div>  
        </div>  
    {% endif %}  
{% endif %}  
  
{% if operation.responses.size > 0 %}  
    {% for response in operation.responses %}  
        {% if response.description or response.representations.size > 0 %}  
            <h4>{% localized "Documentation|SectionHeadingResponse" %} {{response.statusCode}}</h4>  
  
            <div class="panel">  
                {% if response.description %}  
                    <p>{{ response.description }}</p>  
                {% endif %}  
  
                {% if response.representations.size > 0 %}  
                    <div role="tabpanel">  
                        <ul class="nav nav-tabs" role="tablist">  
                            {% for representation in response.representations %}  
                                <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                                    <a href="#response{{response.statusCode}}tab{{forloop.index}}" role="tab" data-toggle="tab">  
                                        {{representation.contentType}}  
                                    </a>  
                                </li>  
                            {% endfor %}  
                        </ul>  
                        <div class="tab-content tab-content-boxed">  
                            {% for representation in response.representations %}  
                                <div id="response{{response.statusCode}}tab{{forloop.index}}" role="tabpanel" class="tab-pane snippet{% if forloop.first %} active{% endif %}">  
  
                                    {% if representation.sample or representation.schema %}  
                                    <div role="tabpanel">  
  
                                        {% if representation.sample and representation.schema %}  
                                        <ul class="nav nav-tabs-borderless" role="tablist">  
                                            <li role="presentation" class="active">  
                                                <a href="#response{{response.statusCode}}tab{{forloop.index}}sample" role="tab" data-toggle="tab">  
                                                    Sample  
                                                </a>  
                                            </li>  
                                            <li role="presentation">  
                                                <a href="#response{{response.statusCode}}tab{{forloop.index}}schema" role="tab" data-toggle="tab">  
                                                    Schema  
                                                </a>  
                                            </li>  
                                        </ul>  
                                        {% endif %}  
  
                                        <div class="tab-content">  
                                            {% if representation.sample %}  
                                            <div id="response{{response.statusCode}}tab{{forloop.index}}sample" role="tabpanel" class="tab-pane snippet active">  
                                                <pre><code class="{{representation.Brush}}">{{ representation.sample | escape }}</code></pre>  
                                            </div>  
                                            {% endif %}  
  
                                            {% if representation.schema %}  
                                            <div id="response{{response.statusCode}}tab{{forloop.index}}schema" role="tabpanel" class="tab-pane snippet">  
                                                <pre><code class="{{representation.Brush}}">{{ representation.schema | escape }}</code></pre>  
                                            </div>  
                                            {% endif %}  
                                        </div>  
                                    </div>  
                                    {% endif %}  
                                </div>  
                            {% endfor %}  
                        </div>  
                    </div>  
                {% endif %}  
  
                <div class="clearfix"></div>  
            </div>  
  
        {% endif %}  
    {% endfor %}  
{% endif %}  
  
<h4>{% localized "Documentation|SectionHeadingCodeSamples" %}</h4>  
<div role="tabpanel">  
    <ul class="nav nav-tabs" role="tablist">  
        {% for sample in samples %}  
            <li role="presentation" {% if forloop.first %}class="active"{% endif %}>  
                <a href="#{{sample.brush}}" aria-controls="{{sample.brush}}" role="tab" data-toggle="tab">  
                    {{sample.title}}  
                </a>  
            </li>  
        {% endfor %}  
    </ul>  
    <div class="tab-content tab-content-boxed" title="{% localized "Documentation|TooltipTextDoubleClickToSelectAll=""" %}">  
        {% for sample in samples %}  
            <div role="tabpanel" class="tab-pane tab-content-boxed {% if forloop.first %} active{% endif %} snippet snippet-resizable" id="{{sample.brush}}" >  
                <pre><code class="{{sample.brush}}">{% partial sample.template for sample in samples %}</code></pre>  
            </div>  
        {% endfor %}  
    </div>  
    <div class="clearfix"></div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="a7b8d-141">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-141">Controls</span></span>  
 <span data-ttu-id="a7b8d-142">Le modèle `Operation` ne permet pas d’utiliser de [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-142">The `Operation` template does not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="a7b8d-143">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-143">Data model</span></span>  
  
|<span data-ttu-id="a7b8d-144">Propriété</span><span class="sxs-lookup"><span data-stu-id="a7b8d-144">Property</span></span>|<span data-ttu-id="a7b8d-145">Type</span><span class="sxs-lookup"><span data-stu-id="a7b8d-145">Type</span></span>|<span data-ttu-id="a7b8d-146">Description</span><span class="sxs-lookup"><span data-stu-id="a7b8d-146">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="a7b8d-147">apiId</span><span class="sxs-lookup"><span data-stu-id="a7b8d-147">apiId</span></span>|<span data-ttu-id="a7b8d-148">string</span><span class="sxs-lookup"><span data-stu-id="a7b8d-148">string</span></span>|<span data-ttu-id="a7b8d-149">ID de l’API actuelle.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-149">The id of the current API.</span></span>|  
|<span data-ttu-id="a7b8d-150">apiName</span><span class="sxs-lookup"><span data-stu-id="a7b8d-150">apiName</span></span>|<span data-ttu-id="a7b8d-151">string</span><span class="sxs-lookup"><span data-stu-id="a7b8d-151">string</span></span>|<span data-ttu-id="a7b8d-152">Nom de l’API.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-152">The name of the API.</span></span>|  
|<span data-ttu-id="a7b8d-153">apiDescription</span><span class="sxs-lookup"><span data-stu-id="a7b8d-153">apiDescription</span></span>|<span data-ttu-id="a7b8d-154">string</span><span class="sxs-lookup"><span data-stu-id="a7b8d-154">string</span></span>|<span data-ttu-id="a7b8d-155">Description de l’API.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-155">A description of the API.</span></span>|  
|<span data-ttu-id="a7b8d-156">api</span><span class="sxs-lookup"><span data-stu-id="a7b8d-156">api</span></span>|<span data-ttu-id="a7b8d-157">Entité [API summary](api-management-template-data-model-reference.md#APISummary).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-157">[API summary](api-management-template-data-model-reference.md#APISummary) entity.</span></span>|<span data-ttu-id="a7b8d-158">API actuelle.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-158">The current API.</span></span>|  
|<span data-ttu-id="a7b8d-159">operation</span><span class="sxs-lookup"><span data-stu-id="a7b8d-159">operation</span></span>|[<span data-ttu-id="a7b8d-160">Opération</span><span class="sxs-lookup"><span data-stu-id="a7b8d-160">Operation</span></span>](api-management-template-data-model-reference.md#Operation)|<span data-ttu-id="a7b8d-161">Opération actuellement affichée.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-161">The currently displayed operation.</span></span>|  
|<span data-ttu-id="a7b8d-162">sampleUrl</span><span class="sxs-lookup"><span data-stu-id="a7b8d-162">sampleUrl</span></span>|<span data-ttu-id="a7b8d-163">string</span><span class="sxs-lookup"><span data-stu-id="a7b8d-163">string</span></span>|<span data-ttu-id="a7b8d-164">URL de l’opération actuelle.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-164">The URL for the current operation.</span></span>|  
|<span data-ttu-id="a7b8d-165">operationMenu</span><span class="sxs-lookup"><span data-stu-id="a7b8d-165">operationMenu</span></span>|[<span data-ttu-id="a7b8d-166">Operation menu</span><span class="sxs-lookup"><span data-stu-id="a7b8d-166">Operation menu</span></span>](api-management-template-data-model-reference.md#Menu)|<span data-ttu-id="a7b8d-167">Menu d’opérations pour cette API.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-167">A menu of operations for this API.</span></span>|  
|<span data-ttu-id="a7b8d-168">consoleUrl</span><span class="sxs-lookup"><span data-stu-id="a7b8d-168">consoleUrl</span></span>|<span data-ttu-id="a7b8d-169">URI</span><span class="sxs-lookup"><span data-stu-id="a7b8d-169">URI</span></span>|<span data-ttu-id="a7b8d-170">URI du bouton **Essayer**.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-170">The URI for the **Try it** button.</span></span>|  
|<span data-ttu-id="a7b8d-171">exemples</span><span class="sxs-lookup"><span data-stu-id="a7b8d-171">samples</span></span>|<span data-ttu-id="a7b8d-172">Collection d’entités [Code sample](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-172">Collection of [Code sample](api-management-template-data-model-reference.md#Sample) entities.</span></span>|<span data-ttu-id="a7b8d-173">Exemples de code pour l’opération actuelle.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-173">The code samples for the current operation..</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-174">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-174">Sample template data</span></span>  
  
```json  
{  
    "apiId": "570275f1b16653124c8f9ba3",  
    "apiName": "Basic Calculator",  
    "apiDescription": "Arithmetics is just a call away!",  
    "api": {  
        "id": "570275f1b16653124c8f9ba3",  
        "name": "Basic Calculator",  
        "description": "Arithmetics is just a call away!"  
    },  
    "operation": {  
        "id": "570275f2b1665305c811cf49",  
        "name": "Add two integers",  
        "description": "Produces a sum of two numbers.",  
        "scheme": "https",  
        "uriTemplate": "calc/add?a={a}&b={b}",  
        "host": "sdcontoso5.azure-api.net",  
        "httpMethod": "GET",  
        "request": {  
            "description": null,  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": [  
                {  
                    "name": "a",  
                    "description": "First operand. Default value is <code>51</code>.",  
                    "value": "51",  
                    "options": [  
                        "51"  
                    ],  
                    "required": true,  
                    "kind": 1,  
                    "typeName": null  
                },  
                {  
                    "name": "b",  
                    "description": "Second operand. Default value is <code>49</code>.",  
                    "value": "49",  
                    "options": [  
                        "49"  
                    ],  
                    "required": true,  
                    "kind": 1,  
                    "typeName": null  
                }  
            ],  
            "representations": []  
        },  
        "responses": []  
    },  
    "sampleUrl": "https://sdcontoso5.azure-api.net/calc/add?a={a}&b={b}",  
    "operationMenu": {  
        "ApiId": "570275f1b16653124c8f9ba3",  
        "CurrentOperationId": "570275f2b1665305c811cf49",  
        "Action": "Operation",  
        "MenuItems": [  
            {  
                "Id": "570275f2b1665305c811cf49",  
                "Title": "Add two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4c",  
                "Title": "Divide two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4b",  
                "Title": "Multiply two integers",  
                "HttpMethod": "GET"  
            },  
            {  
                "Id": "570275f2b1665305c811cf4a",  
                "Title": "Subtract two integers",  
                "HttpMethod": "GET"  
            }  
        ]  
    },  
    "consoleUrl": "/docs/services/570275f1b16653124c8f9ba3/operations/570275f2b1665305c811cf49/console",  
    "samples": [  
        {  
            "title": "Curl",  
            "snippet": null,  
            "brush": "plain",  
            "template": "DocumentationSamplesCurl",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "C#",  
            "snippet": null,  
            "brush": "csharp",  
            "template": "DocumentationSamplesCsharp",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Java",  
            "snippet": null,  
            "brush": "java",  
            "template": "DocumentationSamplesJava",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "JavaScript",  
            "snippet": null,  
            "brush": "xml",  
            "template": "DocumentationSamplesJs",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "ObjC",  
            "snippet": null,  
            "brush": "objc",  
            "template": "DocumentationSamplesObjc",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "PHP",  
            "snippet": null,  
            "brush": "php",  
            "template": "DocumentationSamplesPhp",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Python",  
            "snippet": null,  
            "brush": "python",  
            "template": "DocumentationSamplesPython",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        },  
        {  
            "title": "Ruby",  
            "snippet": null,  
            "brush": "ruby",  
            "template": "DocumentationSamplesRuby",  
            "body": "{body}",  
            "method": "GET",  
            "scheme": "https",  
            "path": "/calc/add?a={a}&b={b}",  
            "query": "",  
            "host": "sdcontoso5.azure-api.net",  
            "headers": [  
                {  
                    "name": "Ocp-Apim-Subscription-Key",  
                    "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
                    "value": "{subscription key}",  
                    "typeName": "string",  
                    "options": null,  
                    "required": true,  
                    "readonly": false  
                }  
            ],  
            "parameters": []  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="a7b8d-175"><a name="CodeSamples"></a> Exemples de code</span><span class="sxs-lookup"><span data-stu-id="a7b8d-175"><a name="CodeSamples"></a> Code samples</span></span>  
 <span data-ttu-id="a7b8d-176">Les modèles suivants vous permettent de personnaliser le corps des exemples de code sur la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-176">The following templates allow you to customize the body of the individual code samples on the operation page.</span></span>  
  
 <span data-ttu-id="a7b8d-177">![Modèles Exemples de code dans le portail des développeur](./media/api-management-api-templates/APIM-Developer-Portal-Templates-Code-samples.png "Modèles Exemples de code dans le portail des développeurs APIM")</span><span class="sxs-lookup"><span data-stu-id="a7b8d-177">![Developer Portal Templates Code samples](./media/api-management-api-templates/APIM-Developer-Portal-Templates-Code-samples.png "APIM Developer Portal Templates Code samples")</span></span>  
  
-   [<span data-ttu-id="a7b8d-178">Curl</span><span class="sxs-lookup"><span data-stu-id="a7b8d-178">Curl</span></span>](#Curl)  
  
-   [<span data-ttu-id="a7b8d-179">C#</span><span class="sxs-lookup"><span data-stu-id="a7b8d-179">C#</span></span>](#CSharp)  
  
-   [<span data-ttu-id="a7b8d-180">Java</span><span class="sxs-lookup"><span data-stu-id="a7b8d-180">Java</span></span>](#Stub)  
  
-   [<span data-ttu-id="a7b8d-181">JavaScript</span><span class="sxs-lookup"><span data-stu-id="a7b8d-181">JavaScript</span></span>](#JavaScript)  
  
-   [<span data-ttu-id="a7b8d-182">Objective C</span><span class="sxs-lookup"><span data-stu-id="a7b8d-182">Objective C</span></span>](#ObjectiveC)  
  
-   [<span data-ttu-id="a7b8d-183">PHP</span><span class="sxs-lookup"><span data-stu-id="a7b8d-183">PHP</span></span>](#PHP)  
  
-   [<span data-ttu-id="a7b8d-184">Python</span><span class="sxs-lookup"><span data-stu-id="a7b8d-184">Python</span></span>](#Python)  
  
-   [<span data-ttu-id="a7b8d-185">Ruby</span><span class="sxs-lookup"><span data-stu-id="a7b8d-185">Ruby</span></span>](#Ruby)  
  
###  <span data-ttu-id="a7b8d-186"><a name="Curl"></a> Curl</span><span class="sxs-lookup"><span data-stu-id="a7b8d-186"><a name="Curl"></a> Curl</span></span>  
 <span data-ttu-id="a7b8d-187">Le modèle **DocumentationSamplesCurl** vous permet de personnaliser cet exemple de code dans la section Exemples de code de la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-187">The **DocumentationSamplesCurl** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="a7b8d-188">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-188">Default template</span></span>  
  
```xml  
@ECHO OFF  
  
curl -v -X {{method}} "{{scheme}}://{{host}}{{path}}{{query | escape }}"  
{% for header in headers -%}  
-H "{{ header.name }}: {{ header.value }}"  
{% endfor -%}  
{% if body -%}   
--data-ascii "{{ body | replace:'"','^"' }}"   
{% endif -%}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="a7b8d-189">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-189">Controls</span></span>  
 <span data-ttu-id="a7b8d-190">Les modèles d’exemples de code ne permettent pas d’utiliser des [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-190">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="a7b8d-191">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-191">Data model</span></span>  
 <span data-ttu-id="a7b8d-192">Entité [Exemple de code](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-192">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-193">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-193">Sample template data</span></span>  
  
```json  
{  
    "title": "Curl",  
    "snippet": null,  
    "brush": "plain",  
    "template": "DocumentationSamplesCurl",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="a7b8d-194"><a name="CSharp"></a> C#</span><span class="sxs-lookup"><span data-stu-id="a7b8d-194"><a name="CSharp"></a> C#</span></span>  
 <span data-ttu-id="a7b8d-195">Le modèle **DocumentationSamplesCsharp** vous permet de personnaliser cet exemple de code dans la section Exemples de code de la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-195">The **DocumentationSamplesCsharp** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="a7b8d-196">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-196">Default template</span></span>  
  
```xml  
using System;  
using System.Net.Http.Headers;  
using System.Text;  
using System.Net.Http;  
using System.Web;  
  
namespace CSHttpClientSample  
{  
    static class Program  
    {  
        static void Main()  
        {  
            MakeRequest();  
            Console.WriteLine("Hit ENTER to exit...");  
            Console.ReadLine();  
        }  
  
        static async void MakeRequest()  
        {  
            var client = new HttpClient();  
            var queryString = HttpUtility.ParseQueryString(string.Empty);  
  
{% if headers.size > 0 -%}  
            // Request headers  
{% for header in headers -%}  
{% case header.Name -%}  
{% when "Accept"%}  
            client.DefaultRequestHeaders.Accept.Add(MediaTypeWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Charset" -%}  
            client.DefaultRequestHeaders.AcceptCharset.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Encoding" -%}  
            client.DefaultRequestHeaders.AcceptEncoding.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Accept-Language" -%}  
            client.DefaultRequestHeaders.AcceptLanguage.Add(StringWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Cache-Control" -%}  
            client.DefaultRequestHeaders.CacheControl = CacheControlHeaderValue.Parse("{{header.value}}");  
{% when "Connection" -%}  
            client.DefaultRequestHeaders.Connection.Add("{{header.value}}");  
{% when "Date" -%}  
            client.DefaultRequestHeaders.Date = DateTimeOffset.Parse("{{header.value}}");  
{% when "Expect" -%}  
            client.DefaultRequestHeaders.Expect.Add(NameValueWithParametersHeaderValue.Parse("{{header.value}}"));  
{% when "If-Match" -%}  
            client.DefaultRequestHeaders.IfMatch.Add(EntityTagHeaderValue.Parse("{{header.value}}"));  
{% when "If-Modified-Since" -%}  
            client.DefaultRequestHeaders.IfModifiedSince = DateTimeOffset.Parse("{{header.value}}");  
{% when "If-None-Match" -%}  
            client.DefaultRequestHeaders.IfNoneMatch.Add(EntityTagHeaderValue.Parse("{{header.value}}"));  
{% when "If-Range" -%}  
            client.DefaultRequestHeaders.IfRange = RangeConditionHeaderValue.Parse("{{header.value}}");  
{% when "If-Unmodified-Since" -%}  
            client.DefaultRequestHeaders.IfUnmodifiedSince = DateTimeOffset.Parse("{{header.value}}");  
{% when "Max-Forwards" -%}  
            client.DefaultRequestHeaders.MaxForwards = int.Parse("{{header.value}}");  
{% when "Pragma" -%}  
            client.DefaultRequestHeaders.Pragma.Add(NameValueHeaderValue.Parse("{{header.value}}"));  
{% when "Range" -%}  
            client.DefaultRequestHeaders.Range = RangeHeaderValue.Parse("{{header.value}}");  
{% when "Referer" -%}  
            client.DefaultRequestHeaders.Referrer = new Uri("{{header.value}}");  
{% when "TE" -%}  
            client.DefaultRequestHeaders.TE.Add(TransferCodingWithQualityHeaderValue.Parse("{{header.value}}"));  
{% when "Transfer-Encoding" -%}  
            client.DefaultRequestHeaders.TransferEncoding.Add(TransferCodingHeaderValue.Parse("{{header.value}}"));  
{% when "Upgrade" -%}  
            client.DefaultRequestHeaders.Upgrade.Add(ProductHeaderValue.Parse("{{header.value}}"));  
{% when "User-Agent" -%}  
            client.DefaultRequestHeaders.UserAgent.Add(ProductInfoHeaderValue.Parse("{{header.value}}"));  
{% when "Via" -%}                
            client.DefaultRequestHeaders.Via.Add(ViaHeaderValue.Parse("{{header.value}}"));  
{% when "Warning" -%}  
            client.DefaultRequestHeaders.Warning.Add(WarningHeaderValue.Parse("{{header.value}}"));  
{% when "Content-Type" -%}  
{% else -%}  
            client.DefaultRequestHeaders.Add("{{header.Name}}", "{{header.value}}");  
{% endcase -%}  
{% endfor -%}  
{% endif -%}  
  
{% if parameters.size > 0 -%}  
            // Request parameters  
{% for parameter in parameters -%}  
            queryString["{{parameter.Name}}"] = "{{parameter.Value}}";  
{% endfor -%}  
{% endif -%}  
            var uri = "{{scheme}}://{{host}}{{path}}{% if path contains '?' %}&{% else %}?{% endif %}" + queryString;  
  
{% case method -%}  
  
{% when "POST" -%}  
            HttpResponseMessage response;  
  
            // Request body  
            byte[] byteData = Encoding.UTF8.GetBytes("{{ body | replace:'"','\"'}}");  
  
            using (var content = new ByteArrayContent(byteData))  
            {  
{% if body -%}  
               content.Headers.ContentType = new MediaTypeHeaderValue("< your content type, i.e. application/json >");  
{% endif -%}  
               response = await client.PostAsync(uri, content);  
            }  
  
{% when "GET" -%}  
            var response = await client.GetAsync(uri);  
{% when "DELETE" -%}  
            var response = await client.DeleteAsync(uri);  
{% when "PUT" -%}  
            HttpResponseMessage response;  
  
            // Request body  
            byte[] byteData = Encoding.UTF8.GetBytes("{{ body | replace:'"','\"'}}");  
  
            using (var content = new ByteArrayContent(byteData))  
            {  
{% if body -%}  
                content.Headers.ContentType = new MediaTypeHeaderValue("< your content type, i.e. application/json >");  
{% endif -%}  
                response = await client.PutAsync(uri, content);  
            }  
{% when "HEAD" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Head, uri));  
{% when "OPTIONS" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Options, uri));  
{% when "TRACE" -%}  
            var response = await client.SendAsync(new HttpRequestMessage(HttpMethod.Trace, uri));  
  
            if (response.Content != null)  
            {  
                var responseString = await response.Content.ReadAsStringAsync();  
                Console.WriteLine(responseString);      
            }  
{% endcase -%}  
        }  
    }  
}     
```  
  
#### <a name="controls"></a><span data-ttu-id="a7b8d-197">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-197">Controls</span></span>  
 <span data-ttu-id="a7b8d-198">Les modèles d’exemples de code ne permettent pas d’utiliser des [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-198">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="a7b8d-199">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-199">Data model</span></span>  
 <span data-ttu-id="a7b8d-200">Entité [Exemple de code](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-200">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-201">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-201">Sample template data</span></span>  
  
```json  
{  
    "title": "C#",  
    "snippet": null,  
    "brush": "csharp",  
    "template": "DocumentationSamplesCsharp",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="a7b8d-202"><a name="Stub"></a> Java</span><span class="sxs-lookup"><span data-stu-id="a7b8d-202"><a name="Stub"></a> Java</span></span>  
 <span data-ttu-id="a7b8d-203">Le modèle **DocumentationSamplesJava** vous permet de personnaliser cet exemple de code dans la section Exemples de code de la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-203">The **DocumentationSamplesJava** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="a7b8d-204">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-204">Default template</span></span>  
  
```xml  
// // This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)  
import java.net.URI;  
import org.apache.http.HttpEntity;  
import org.apache.http.HttpResponse;  
import org.apache.http.client.HttpClient;  
import org.apache.http.client.methods.HttpGet;  
import org.apache.http.client.utils.URIBuilder;  
import org.apache.http.impl.client.HttpClients;  
import org.apache.http.util.EntityUtils;  
  
public class JavaSample   
{  
    public static void main(String[] args)   
    {  
        HttpClient httpclient = HttpClients.createDefault();  
  
        try  
        {  
            URIBuilder builder = new URIBuilder("{{scheme}}://{{host}}{{path}}");  
  
{% if parameters.size > 0 -%}  
{% for parameter in parameters -%}  
            builder.setParameter("{{parameter.name}}", "{{parameter.value}}");  
{% endfor -%}  
{% endif -%}  
  
            URI uri = builder.build();  
            Http{{ method | downcase | capitalize }} request = new Http{{ method | downcase | capitalize }}(uri);  
{% for header in headers -%}  
            request.setHeader("{{header.Name}}", "{{header.value}}");  
{% endfor %}  
  
{% if body -%}  
            // Request body  
            StringEntity reqEntity = new StringEntity("{{ body | replace:'"','\"' }}");  
            request.setEntity(reqEntity);  
{% endif -%}  
  
            HttpResponse response = httpclient.execute(request);  
            HttpEntity entity = response.getEntity();  
  
            if (entity != null)   
            {  
                System.out.println(EntityUtils.toString(entity));  
            }  
        }  
        catch (Exception e)  
        {  
            System.out.println(e.getMessage());  
        }  
    }  
}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="a7b8d-205">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-205">Controls</span></span>  
 <span data-ttu-id="a7b8d-206">Les modèles d’exemples de code ne permettent pas d’utiliser des [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-206">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="a7b8d-207">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-207">Data model</span></span>  
 <span data-ttu-id="a7b8d-208">Entité [Exemple de code](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-208">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-209">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-209">Sample template data</span></span>  
  
```json  
{  
    "title": "Java",  
    "snippet": null,  
    "brush": "java",  
    "template": "DocumentationSamplesJava",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="a7b8d-210"><a name="JavaScript"></a> JavaScript</span><span class="sxs-lookup"><span data-stu-id="a7b8d-210"><a name="JavaScript"></a> JavaScript</span></span>  
 <span data-ttu-id="a7b8d-211">Le modèle **DocumentationSamplesJs** vous permet de personnaliser cet exemple de code dans la section Exemples de code de la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-211">The **DocumentationSamplesJs** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="a7b8d-212">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-212">Default template</span></span>  
  
```xml  
<!DOCTYPE html>  
<html>  
<head>  
    <title>JSSample</title>  
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js"></script>  
</head>  
<body>  
  
<script type="text/javascript">  
    $(function() {  
        var params = {  
{% if parameters.size > 0 -%}  
            // Request parameters  
{% for parameter in parameters -%}  
            "{{parameter.name}}": "{{parameter.value}}",  
{% endfor -%}  
{% endif -%}  
        };  
  
        $.ajax({  
            url: "{{scheme}}://{{host}}{{path}}{% if path contains '?' %}&{% else %}?{% endif %}" + $.param(params),  
{% if headers.size > 0 -%}  
            beforeSend: function(xhrObj){  
                // Request headers  
{% for header in headers -%}  
                xhrObj.setRequestHeader("{{header.name}}","{{header.value}}");  
{% endfor -%}  
            },  
{% endif -%}  
            type: "{{method}}",  
{% if body -%}  
            // Request body  
            data: "{{ body | replace:'"','\"' }}",  
{% endif -%}  
        })  
        .done(function(data) {  
            alert("success");  
        })  
        .fail(function() {  
            alert("error");  
        });  
    });  
</script>  
</body>  
</html>  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="a7b8d-213">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-213">Controls</span></span>  
 <span data-ttu-id="a7b8d-214">Les modèles d’exemples de code ne permettent pas d’utiliser des [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-214">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="a7b8d-215">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-215">Data model</span></span>  
 <span data-ttu-id="a7b8d-216">Entité [Exemple de code](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-216">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-217">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-217">Sample template data</span></span>  
  
```json  
{  
    "title": "JavaScript",  
    "snippet": null,  
    "brush": "xml",  
    "template": "DocumentationSamplesJs",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="a7b8d-218"><a name="ObjectiveC"></a> Objective C</span><span class="sxs-lookup"><span data-stu-id="a7b8d-218"><a name="ObjectiveC"></a> Objective C</span></span>  
 <span data-ttu-id="a7b8d-219">Le modèle **DocumentationSamplesObjc** vous permet de personnaliser cet exemple de code dans la section Exemples de code de la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-219">The **DocumentationSamplesObjc** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="a7b8d-220">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-220">Default template</span></span>  
  
```xml  
#import <Foundation/Foundation.h>  
  
int main(int argc, const char * argv[])  
{  
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];  
  
    NSString* path = @"{{scheme}}://{{host}}{{path}}";  
    NSArray* array = @[  
                         // Request parameters  
                         @"entities=true",  
{% if parameters.size > 0 -%}  
{% for parameter in parameters -%}  
                         @"{{parameter.name}}={{parameter.value}}",  
{% endfor -%}  
{% endif -%}  
                      ];  
  
    NSString* string = [array componentsJoinedByString:@"&"];  
    path = [path stringByAppendingFormat:@"?%@", string];  
  
    NSLog(@"%@", path);  
  
    NSMutableURLRequest* _request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:path]];  
    [_request setHTTPMethod:@"{{method}}"];  
{% if headers.size > 0 -%}  
    // Request headers  
{% for header in headers -%}  
    [_request setValue:@"{{header.value}}" forHTTPHeaderField:@"{{header.name}}"];  
{% endfor -%}  
{% endif -%}  
{% if body -%}  
    // Request body  
    [_request setHTTPBody:[@"{{ body | replace:'"','\"' }}" dataUsingEncoding:NSUTF8StringEncoding]];  
{% endif -%}  
  
    NSURLResponse *response = nil;  
    NSError *error = nil;  
    NSData* _connectionData = [NSURLConnection sendSynchronousRequest:_request returningResponse:&response error:&error];  
  
    if (nil != error)  
    {  
        NSLog(@"Error: %@", error);  
    }  
    else  
    {  
        NSError* error = nil;  
        NSMutableDictionary* json = nil;  
        NSString* dataString = [[NSString alloc] initWithData:_connectionData encoding:NSUTF8StringEncoding];  
        NSLog(@"%@", dataString);  
  
        if (nil != _connectionData)  
        {  
            json = [NSJSONSerialization JSONObjectWithData:_connectionData options:NSJSONReadingMutableContainers error:&error];  
        }  
  
        if (error || !json)  
        {  
            NSLog(@"Could not parse loaded json with error:%@", error);  
        }  
  
        NSLog(@"%@", json);  
        _connectionData = nil;  
    }  
  
    [pool drain];  
  
    return 0;  
}  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="a7b8d-221">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-221">Controls</span></span>  
 <span data-ttu-id="a7b8d-222">Les modèles d’exemples de code ne permettent pas d’utiliser des [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-222">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="a7b8d-223">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-223">Data model</span></span>  
 <span data-ttu-id="a7b8d-224">Entité [Exemple de code](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-224">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-225">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-225">Sample template data</span></span>  
  
```json  
{  
    "title": "ObjC",  
    "snippet": null,  
    "brush": "objc",  
    "template": "DocumentationSamplesObjc",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="a7b8d-226"><a name="PHP"></a> PHP</span><span class="sxs-lookup"><span data-stu-id="a7b8d-226"><a name="PHP"></a> PHP</span></span>  
 <span data-ttu-id="a7b8d-227">Le modèle **DocumentationSamplesPhp** vous permet de personnaliser cet exemple de code dans la section Exemples de code de la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-227">The **DocumentationSamplesPhp** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="a7b8d-228">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-228">Default template</span></span>  
  
```xml  
<?php  
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)  
require_once 'HTTP/Request2.php';  
  
$request = new Http_Request2('{{scheme}}://{{host}}{{path}}');  
$url = $request->getUrl();  
  
{% if headers.size > 0 -%}  
$headers = array(  
    // Request headers  
{% for header in headers -%}  
    '{{header.name}}' => '{{header.value}}',  
{% endfor -%}  
);  
  
$request->setHeader($headers);  
{% endif -%}  
  
{% if parameters.size > 0 -%}  
$parameters = array(  
    // Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}' => '{{parameter.value}}',  
{% endfor -%}  
);  
  
$url->setQueryVariables($parameters);  
{% endif -%}  
  
$request->setMethod(HTTP_Request2::METHOD_{{method}});  
  
{% if body -%}  
// Request body  
$request->setBody("{{ body | replace:'"','\"' }}");  
{% endif -%}  
  
try  
{  
    $response = $request->send();  
    echo $response->getBody();  
}  
catch (HttpException $ex)  
{  
    echo $ex;  
}  
  
?>  
```  
  
#### <a name="controls"></a><span data-ttu-id="a7b8d-229">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-229">Controls</span></span>  
 <span data-ttu-id="a7b8d-230">Les modèles d’exemples de code ne permettent pas d’utiliser des [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-230">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="a7b8d-231">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-231">Data model</span></span>  
 <span data-ttu-id="a7b8d-232">Entité [Exemple de code](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-232">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-233">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-233">Sample template data</span></span>  
  
```json  
{  
    "title": "PHP",  
    "snippet": null,  
    "brush": "php",  
    "template": "DocumentationSamplesPhp",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="a7b8d-234"><a name="Python"></a> Python</span><span class="sxs-lookup"><span data-stu-id="a7b8d-234"><a name="Python"></a> Python</span></span>  
 <span data-ttu-id="a7b8d-235">Le modèle **DocumentationSamplesPython** vous permet de personnaliser cet exemple de code dans la section Exemples de code de la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-235">The **DocumentationSamplesPython** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="a7b8d-236">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-236">Default template</span></span>  
  
```xml  
########### Python 2.7 #############  
import httplib, urllib, base64  
  
headers = {  
{% if headers.size > 0 -%}  
    # Request headers  
{% for header in headers -%}  
    '{{header.name}}': '{{header.value}}',  
{% endfor -%}  
{% endif -%}  
}  
  
params = urllib.urlencode({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}': '{{parameter.value}}',  
{% endfor -%}  
{% endif -%}  
})  
  
try:  
{% case scheme -%}  
{% when "http" -%}  
    conn = httplib.HTTPConnection('{{host}}')  
{% when "https" -%}  
    conn = httplib.HTTPSConnection('{{host}}')  
{% endcase -%}  
    conn.request("{{method}}", "{{path}}{% if path contains '?' %}&{% else %}?{% endif %}%s" % params{% if body %}, "{{ body | replace:'"','\"' }}"{% endif %}, headers)  
    response = conn.getresponse()  
    data = response.read()  
    print(data)  
    conn.close()  
except Exception as e:  
    print("[Errno {0}] {1}".format(e.errno, e.strerror))  
  
####################################  
  
########### Python 3.2 #############  
import http.client, urllib.request, urllib.parse, urllib.error, base64  
  
headers = {  
{% if headers.size > 0 -%}  
    # Request headers  
{% for header in headers -%}  
    '{{header.name}}': '{{header.value}}',  
{% endfor -%}  
{% endif -%}  
}  
  
params = urllib.parse.urlencode({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}': '{{parameter.value}}',  
{% endfor -%}  
{% endif -%}  
})  
  
try:  
{% case scheme -%}  
{% when "http" -%}  
    conn = http.client.HTTPConnection('{{host}}')  
{% when "https" -%}  
    conn = http.client.HTTPSConnection('{{host}}')  
{% endcase -%}  
    conn.request("{{method}}", "{{path}}{% if path contains '?' %}&{% else %}?{% endif %}%s" % params{% if body %}, "{{ body | replace:'"','\"' }}"{% endif %}, headers)  
    response = conn.getresponse()  
    data = response.read()  
    print(data)  
    conn.close()  
except Exception as e:  
    print("[Errno {0}] {1}".format(e.errno, e.strerror))  
  
####################################  
```  
  
#### <a name="controls"></a><span data-ttu-id="a7b8d-237">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-237">Controls</span></span>  
 <span data-ttu-id="a7b8d-238">Les modèles d’exemples de code ne permettent pas d’utiliser des [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-238">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="a7b8d-239">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-239">Data model</span></span>  
 <span data-ttu-id="a7b8d-240">Entité [Exemple de code](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-240">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-241">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-241">Sample template data</span></span>  
  
```json  
{  
    "title": "Python",  
    "snippet": null,  
    "brush": "python",  
    "template": "DocumentationSamplesPython",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```  
  
###  <span data-ttu-id="a7b8d-242"><a name="Ruby"></a> Ruby</span><span class="sxs-lookup"><span data-stu-id="a7b8d-242"><a name="Ruby"></a> Ruby</span></span>  
 <span data-ttu-id="a7b8d-243">Le modèle **DocumentationSamplesRuby** vous permet de personnaliser cet exemple de code dans la section Exemples de code de la page Opération.</span><span class="sxs-lookup"><span data-stu-id="a7b8d-243">The **DocumentationSamplesRuby** template allows you to customize that code sample in the code samples section of the operation page.</span></span>  
  
#### <a name="default-template"></a><span data-ttu-id="a7b8d-244">Modèle par défaut</span><span class="sxs-lookup"><span data-stu-id="a7b8d-244">Default template</span></span>  
  
```xml  
require 'net/http'  
  
uri = URI('{{scheme}}://{{host}}{{path}}')  
uri.query = URI.encode_www_form({  
{% if parameters.size > 0 -%}  
    # Request parameters  
{% for parameter in parameters -%}  
    '{{parameter.name}}' => '{{parameter.value}}'{% unless forloop.last %},{% endunless %}  
{% endfor -%}  
{% endif -%}  
})  
  
request = Net::HTTP::{{ method | downcase | capitalize }}.new(uri.request_uri)  
{% for header in headers -%}  
# Request headers  
request['{{header.name}}'] = '{{header.value}}'  
{% endfor -%}  
{% if body -%}  
# Request body  
request.body = "{{ body | replace:'"','\"' }}"  
{% endif -%}  
  
response = Net::HTTP.start(uri.host, uri.port, :use_ssl => uri.scheme == 'https') do |http|  
    http.request(request)  
end  
  
puts response.body  
  
```  
  
#### <a name="controls"></a><span data-ttu-id="a7b8d-245">Commandes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-245">Controls</span></span>  
 <span data-ttu-id="a7b8d-246">Les modèles d’exemples de code ne permettent pas d’utiliser des [contrôles de page](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-246">The code sample templates do not allow the use of any [page controls](api-management-page-controls.md).</span></span>  
  
#### <a name="data-model"></a><span data-ttu-id="a7b8d-247">Modèle de données</span><span class="sxs-lookup"><span data-stu-id="a7b8d-247">Data model</span></span>  
 <span data-ttu-id="a7b8d-248">Entité [Exemple de code](api-management-template-data-model-reference.md#Sample).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-248">[Code sample](api-management-template-data-model-reference.md#Sample) entity.</span></span>  
  
#### <a name="sample-template-data"></a><span data-ttu-id="a7b8d-249">Données d’un exemple de modèle</span><span class="sxs-lookup"><span data-stu-id="a7b8d-249">Sample template data</span></span>  
  
```json  
{  
    "title": "Ruby",  
    "snippet": null,  
    "brush": "ruby",  
    "template": "DocumentationSamplesRuby",  
    "body": "{body}",  
    "method": "GET",  
    "scheme": "https",  
    "path": "/calc/add?a={a}&b={b}",  
    "query": "",  
    "host": "sdcontoso5.azure-api.net",  
    "headers": [  
        {  
            "name": "Ocp-Apim-Subscription-Key",  
            "description": "Subscription key which provides access to this API. Found in your <a href='/developer'>Profile</a>.",  
            "value": "{subscription key}",  
            "typeName": "string",  
            "options": null,  
            "required": true,  
            "readonly": false  
        }  
    ],  
    "parameters": []  
}  
```

## <a name="next-steps"></a><span data-ttu-id="a7b8d-250">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a7b8d-250">Next steps</span></span>
<span data-ttu-id="a7b8d-251">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a7b8d-251">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>