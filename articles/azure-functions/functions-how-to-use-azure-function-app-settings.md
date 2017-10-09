---
title: "aaaConfigure paramètres d’application Azure fonction | Documents Microsoft"
description: "Découvrez le fonctionnement des tooconfigure Azure sur les paramètres de l’application."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="ed278-103">Comment toomanage une application hello portail Azure (fonction)</span><span class="sxs-lookup"><span data-stu-id="ed278-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="ed278-104">Dans les fonctions d’Azure, une application de la fonction fournit le contexte de l’exécution de hello pour vos fonctions individuelles.</span><span class="sxs-lookup"><span data-stu-id="ed278-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="ed278-105">Comportements d’application de fonction appliquent de fonctions de tooall hébergées par une application de la fonction donnée.</span><span class="sxs-lookup"><span data-stu-id="ed278-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="ed278-106">Cette rubrique décrit comment tooconfigure et gérer vos applications de fonction Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ed278-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="ed278-107">toobegin, accédez toohello [portail Azure](http://portal.azure.com) et connectez-vous à tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ed278-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="ed278-108">Dans la barre de recherche hello haut hello du portail de hello, tapez nom hello de votre application de la fonction et sélectionnez-le dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="ed278-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="ed278-109">Après avoir sélectionné votre application de la fonction, vous voyez hello suivant page :</span><span class="sxs-lookup"><span data-stu-id="ed278-109">After selecting your function app, you see hello following page:</span></span>

![Présentation de l’application Bonjour portail Azure (fonction)](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="ed278-111"><a name="manage-app-service-settings"></a>Onglet Paramètres de Function App</span><span class="sxs-lookup"><span data-stu-id="ed278-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Présentation de l’application fonction Bonjour portail Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="ed278-113">Hello **paramètres** onglet est où vous pouvez mettre à jour la version du runtime fonctions hello utilisée par votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="ed278-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="ed278-114">Il est également où vous gérer hello hôte clés utilisées toorestrict accès tooall fonctions HTTP hébergées par l’application de fonction hello.</span><span class="sxs-lookup"><span data-stu-id="ed278-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="ed278-115">Functions prend en charge les plans d’hébergement App Service et Consommation.</span><span class="sxs-lookup"><span data-stu-id="ed278-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="ed278-116">Pour plus d’informations, consultez [choisissez plan de service correcte hello pour les fonctions d’Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="ed278-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="ed278-117">Pour une meilleure prévisibilité dans le plan de la consommation de hello, fonctions vous permet de limiter l’utilisation de la plateforme en définissant un quota d’utilisation quotidienne, en secondes de gigaoctets.</span><span class="sxs-lookup"><span data-stu-id="ed278-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="ed278-118">Une fois que le quota d’utilisation quotidienne hello est atteinte, application de fonction hello est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="ed278-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="ed278-119">Une application de la fonction s’est arrêtée suite à atteindre hello dépenses quota peut être réactivée à partir de hello même contexte que l’établissement de hello quotidiennement les dépenses quota.</span><span class="sxs-lookup"><span data-stu-id="ed278-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="ed278-120">Consultez hello [fonctions Azure page de tarification](http://azure.microsoft.com/pricing/details/functions/) pour plus d’informations sur la facturation.</span><span class="sxs-lookup"><span data-stu-id="ed278-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="ed278-121">Onglet Fonctionnalités de la plate-forme</span><span class="sxs-lookup"><span data-stu-id="ed278-121">Platform features tab</span></span>

![Onglet Fonctionnalités de la plate-forme de Function App.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="ed278-123">Les applications de fonction s’exécutent et sont conservées par la plateforme de Service d’applications Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ed278-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="ed278-124">Par conséquent, vos applications de fonction ont toomost d’accès de fonctionnalités hello du site web d’Azure core plateforme d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="ed278-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="ed278-125">Hello **fonctionnalités de plateforme** onglet est où vous avez accès hello nombreuses fonctionnalités de hello plateforme du Service d’applications que vous pouvez utiliser dans vos applications de fonction.</span><span class="sxs-lookup"><span data-stu-id="ed278-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="ed278-126">Pas toutes les fonctionnalités de Service d’applications sont disponibles lorsqu’une application de la fonction s’exécute sur le plan d’hébergement hello consommation.</span><span class="sxs-lookup"><span data-stu-id="ed278-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="ed278-127">reste Hello de cette rubrique concentre sur hello suivant les fonctionnalités du Service de l’application hello portail Azure qui sont utiles pour les fonctions :</span><span class="sxs-lookup"><span data-stu-id="ed278-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="ed278-128">Éditeur App Service</span><span class="sxs-lookup"><span data-stu-id="ed278-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="ed278-129">Paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="ed278-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="ed278-130">Console</span><span class="sxs-lookup"><span data-stu-id="ed278-130">Console</span></span>](#console)
+ [<span data-ttu-id="ed278-131">Outils avancés (Kudu)</span><span class="sxs-lookup"><span data-stu-id="ed278-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="ed278-132">Options de déploiement</span><span class="sxs-lookup"><span data-stu-id="ed278-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="ed278-133">CORS</span><span class="sxs-lookup"><span data-stu-id="ed278-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="ed278-134">Authentification</span><span class="sxs-lookup"><span data-stu-id="ed278-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="ed278-135">Définition de l’API</span><span class="sxs-lookup"><span data-stu-id="ed278-135">API definition</span></span>](#swagger)

<span data-ttu-id="ed278-136">Pour plus d’informations sur la façon toowork avec les paramètres du Service d’applications, consultez [configurer les paramètres de Service Azure App](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="ed278-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="ed278-137"><a name="editor"></a>Éditeur App Service</span><span class="sxs-lookup"><span data-stu-id="ed278-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Éditeur App Service de Function App.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="ed278-139">Hello éditeur de Service de l’application est un éditeur avancé de portail que vous pouvez utiliser les fichiers de configuration JSON toomodify et les fichiers de code similaires.</span><span class="sxs-lookup"><span data-stu-id="ed278-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="ed278-140">L’activation de cette option entraîne l’ouverture d’un onglet distinct du navigateur avec un éditeur de base.</span><span class="sxs-lookup"><span data-stu-id="ed278-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="ed278-141">Cela vous permet de toointegrate avec hello Git référentiel, exécuter et déboguer le code et modifier les paramètres de l’application (fonction).</span><span class="sxs-lookup"><span data-stu-id="ed278-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="ed278-142">Cet éditeur fournit un environnement de développement améliorée pour vos fonctions par rapport à un panneau de l’application hello par défaut (fonction).</span><span class="sxs-lookup"><span data-stu-id="ed278-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![Hello éditeur de Service de l’application](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="ed278-144"><a name="settings"></a>Paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="ed278-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Paramètres de l’application Function App.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="ed278-146">Hello du Service d’applications **paramètres de l’Application** lame est où vous configurer et gérez les versions du framework, le débogage distant, paramètres de l’application et les chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="ed278-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="ed278-147">Lorsque vous intégrez votre Function App avec d’autres services tiers et Azure, vous pouvez modifier ces paramètres ici.</span><span class="sxs-lookup"><span data-stu-id="ed278-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configurer les paramètres de l’application](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="ed278-149"><a name="console"></a>Console</span><span class="sxs-lookup"><span data-stu-id="ed278-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Console d’application de fonction Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="ed278-151">console de portail Hello est un outil de développement idéal lorsque vous préférez toointeract avec votre application de la fonction à partir de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="ed278-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="ed278-152">Les commandes courantes incluent la création de fichiers et de répertoires et la navigation, ainsi que l’exécution de scripts et de fichiers de commandes.</span><span class="sxs-lookup"><span data-stu-id="ed278-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Console Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="ed278-154"><a name="kudu"></a>Outils avancés (Kudu)</span><span class="sxs-lookup"><span data-stu-id="ed278-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Fonction application Kudu Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="ed278-156">Hello outils avancés pour le Service d’application (également appelé Kudu) fournissent l’accès tooadvanced les fonctionnalités d’administration de votre application de la fonction.</span><span class="sxs-lookup"><span data-stu-id="ed278-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="ed278-157">Dans Kudu, vous pouvez gérer les informations système, les paramètres d’application, les variables d’environnement, les extensions de site, les en-têtes HTTP et les variables de serveur.</span><span class="sxs-lookup"><span data-stu-id="ed278-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="ed278-158">Vous pouvez également lancer **Kudu** en parcourant le point de terminaison SCM toohello pour votre application de la fonction, comme`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="ed278-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurer Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="ed278-160"><a name="deployment">Options de déploiement</span><span class="sxs-lookup"><span data-stu-id="ed278-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Options de déploiement d’application fonction Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="ed278-162">Functions vous permet de développer votre code de fonctions sur votre machine locale.</span><span class="sxs-lookup"><span data-stu-id="ed278-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="ed278-163">Vous pouvez ensuite charger votre tooAzure de projet d’application fonction locale.</span><span class="sxs-lookup"><span data-stu-id="ed278-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="ed278-164">En outre de téléchargement FTP tootraditional, fonctions vous permet de déployer votre application de fonction utilisant des solutions d’intégration continue populaires, tels que GitHub, VSTS, Dropbox, Bitbucket et d’autres.</span><span class="sxs-lookup"><span data-stu-id="ed278-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="ed278-165">Pour plus d’informations, consultez [Déploiement continu pour Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ed278-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="ed278-166">tooupload manuellement à l’aide de FTP ou Git local, vous devez également [configurer vos informations d’identification de déploiement](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="ed278-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="ed278-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="ed278-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Fonction application CORS Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="ed278-169">l’exécution du code malveillant tooprevent dans vos services, les blocs de Service de l’application appelle tooyour fonction applications provenant de sources externes.</span><span class="sxs-lookup"><span data-stu-id="ed278-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="ed278-170">Prend en charge les fonctions toolet (CORS) vous définissez une « liste » des autorisé d’origine à partir de laquelle vos fonctions peuvent accepter des demandes à distance du partage des ressources cross-origin.</span><span class="sxs-lookup"><span data-stu-id="ed278-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configurer l’élément CORS de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="ed278-172"><a name="auth"></a>Authentification</span><span class="sxs-lookup"><span data-stu-id="ed278-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Authentification d’application de fonction Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="ed278-174">Lorsque les fonctions utilisent un déclencheur HTTP, vous pouvez exiger que les appels toofirst être authentifié.</span><span class="sxs-lookup"><span data-stu-id="ed278-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="ed278-175">App Service prend en charge l’authentification Azure Active Directory et la connexion avec des fournisseurs sociaux tels que Facebook, Microsoft et Twitter.</span><span class="sxs-lookup"><span data-stu-id="ed278-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="ed278-176">Pour plus d’informations sur la configuration de fournisseurs d’authentification spécifiques, consultez [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md) (Vue d’ensemble de l’authentification Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="ed278-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configurer l’authentification pour une Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="ed278-178"><a name="swagger"></a>Définition de l’API</span><span class="sxs-lookup"><span data-stu-id="ed278-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![API d’application de fonction swagger définition Bonjour portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="ed278-180">Prend en charge les fonctions Swagger tooallow clients toomore consommer facilement vos fonctions déclenchés par HTTP.</span><span class="sxs-lookup"><span data-stu-id="ed278-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="ed278-181">Pour plus d’informations sur la création de définitions d’API avec Swagger, consultez [Prise en main d’API Apps, d’ASP.NET et de Swagger dans Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed278-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="ed278-182">Vous pouvez également utiliser les fonctions proxys toodefine une surface API unique pour plusieurs fonctions.</span><span class="sxs-lookup"><span data-stu-id="ed278-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="ed278-183">Pour plus d’informations, consultez [Utilisation de Azure Functions Proxies (préversion)](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="ed278-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configurer l’API de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="ed278-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ed278-185">Next steps</span></span>

+ [<span data-ttu-id="ed278-186">Configurer des applications web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ed278-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="ed278-187">Déploiement continu pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="ed278-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



