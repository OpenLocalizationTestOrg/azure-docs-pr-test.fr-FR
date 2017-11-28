---
title: "Configurer les paramètres Azure Function App | Microsoft Docs"
description: "Apprenez à configurer les paramètres d’application Azure Functions."
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
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="437f8-103">Comment gérer une Function App dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="437f8-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="437f8-104">Dans Azure Functions, une Function App fournit le contexte d’exécution de vos fonctions individuelles.</span><span class="sxs-lookup"><span data-stu-id="437f8-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="437f8-105">Les comportements de la Function App s’appliquent à toutes les fonctions hébergées par une Function App donnée.</span><span class="sxs-lookup"><span data-stu-id="437f8-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="437f8-106">Cette rubrique décrit comment configurer et gérer vos Function Apps dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="437f8-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="437f8-107">Commencez par accéder au [portail Azure](http://portal.azure.com) et connectez-vous à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="437f8-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="437f8-108">Dans la barre de recherche en haut du portail, tapez le nom de votre Function App et sélectionnez-la dans la liste.</span><span class="sxs-lookup"><span data-stu-id="437f8-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="437f8-109">Après avoir sélectionné votre Function App, la page suivante s’affiche :</span><span class="sxs-lookup"><span data-stu-id="437f8-109">After selecting your function app, you see the following page:</span></span>

![Vue d’ensemble de Function App dans le portail Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="437f8-111"><a name="manage-app-service-settings"></a>Onglet Paramètres de Function App</span><span class="sxs-lookup"><span data-stu-id="437f8-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Vue d’ensemble de Function App dans le portail Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="437f8-113">Dans l’onglet **Paramètres**, vous pouvez mettre à jour la version du runtime Functions utilisée par votre Function App.</span><span class="sxs-lookup"><span data-stu-id="437f8-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="437f8-114">C’est également ici que vous gérez les clés de l’hôte utilisées pour restreindre l’accès HTTP à toutes les fonctions hébergées par la Function App.</span><span class="sxs-lookup"><span data-stu-id="437f8-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="437f8-115">Functions prend en charge les plans d’hébergement App Service et Consommation.</span><span class="sxs-lookup"><span data-stu-id="437f8-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="437f8-116">Pour plus d’informations, consultez [Choisir le plan de service approprié pour Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="437f8-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="437f8-117">Pour une meilleure prévisibilité dans le plan Consommation, Functions vous permet de limiter l’utilisation de la plate-forme en définissant un quota d’utilisation quotidienne, en gigaoctets-secondes.</span><span class="sxs-lookup"><span data-stu-id="437f8-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="437f8-118">Une fois ce quota d’utilisation quotidienne atteint, la Function App s’arrête.</span><span class="sxs-lookup"><span data-stu-id="437f8-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="437f8-119">Une Function App arrêtée parce qu’elle a atteint le quota d’utilisation peut être réactivée dans le même contexte en établissant un nouveau quota d’utilisation quotidienne.</span><span class="sxs-lookup"><span data-stu-id="437f8-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="437f8-120">Consultez la [page Tarification de Functions](http://azure.microsoft.com/pricing/details/functions/) pour plus d’informations sur la tarification.</span><span class="sxs-lookup"><span data-stu-id="437f8-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="437f8-121">Onglet Fonctionnalités de la plate-forme</span><span class="sxs-lookup"><span data-stu-id="437f8-121">Platform features tab</span></span>

![Onglet Fonctionnalités de la plate-forme de Function App.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="437f8-123">Les Function Apps s’exécutent dans la plateforme Azure App Service et y sont entretenues.</span><span class="sxs-lookup"><span data-stu-id="437f8-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="437f8-124">Par conséquent, vos Function Apps ont accès à la plupart des fonctionnalités de la plateforme d’hébergement web principale d’Azure.</span><span class="sxs-lookup"><span data-stu-id="437f8-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="437f8-125">Dans l’onglet **Fonctionnalités de la plate-forme**, vous pouvez vous accéder aux nombreuses fonctionnalités de la plateforme App Service que vous pouvez utiliser dans vos Function Apps.</span><span class="sxs-lookup"><span data-stu-id="437f8-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="437f8-126">Toutes les fonctionnalités App Service ne sont pas disponibles quand une Function App s’exécute dans le cadre du plan d’hébergement Consommation.</span><span class="sxs-lookup"><span data-stu-id="437f8-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="437f8-127">Le reste de cette rubrique se concentre sur les fonctionnalités App Service du portail Azure qui sont utiles pour Functions :</span><span class="sxs-lookup"><span data-stu-id="437f8-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="437f8-128">Éditeur App Service</span><span class="sxs-lookup"><span data-stu-id="437f8-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="437f8-129">Paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="437f8-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="437f8-130">Console</span><span class="sxs-lookup"><span data-stu-id="437f8-130">Console</span></span>](#console)
+ [<span data-ttu-id="437f8-131">Outils avancés (Kudu)</span><span class="sxs-lookup"><span data-stu-id="437f8-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="437f8-132">Options de déploiement</span><span class="sxs-lookup"><span data-stu-id="437f8-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="437f8-133">CORS</span><span class="sxs-lookup"><span data-stu-id="437f8-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="437f8-134">Authentification</span><span class="sxs-lookup"><span data-stu-id="437f8-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="437f8-135">Définition de l’API</span><span class="sxs-lookup"><span data-stu-id="437f8-135">API definition</span></span>](#swagger)

<span data-ttu-id="437f8-136">Pour plus d’informations sur l’utilisation des paramètres App Service, consultez [Configurer des applications web dans Azure App Service](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="437f8-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="437f8-137"><a name="editor"></a>Éditeur App Service</span><span class="sxs-lookup"><span data-stu-id="437f8-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Éditeur App Service de Function App.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="437f8-139">L’éditeur App Service est un éditeur avancé intégré au portail. Vous pouvez l’utiliser pour modifier les fichiers de configuration JSON et les fichiers de code.</span><span class="sxs-lookup"><span data-stu-id="437f8-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="437f8-140">L’activation de cette option entraîne l’ouverture d’un onglet distinct du navigateur avec un éditeur de base.</span><span class="sxs-lookup"><span data-stu-id="437f8-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="437f8-141">Vous pouvez ainsi l’intégrer au référentiel GitHub, exécuter et déboguer du code et modifier les paramètres de Function App.</span><span class="sxs-lookup"><span data-stu-id="437f8-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="437f8-142">Cet éditeur fournit un environnement de développement amélioré pour vos fonctions en comparaison avec le panneau Function App par défaut.</span><span class="sxs-lookup"><span data-stu-id="437f8-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![L’éditeur App Service](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="437f8-144"><a name="settings"></a>Paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="437f8-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Paramètres de l’application Function App.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="437f8-146">Dans le panneau **Paramètres de l’application**, vous configurez et gérez les versions de framework, le débogage distant, les paramètres de l’application et les chaînes de connexion.</span><span class="sxs-lookup"><span data-stu-id="437f8-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="437f8-147">Lorsque vous intégrez votre Function App avec d’autres services tiers et Azure, vous pouvez modifier ces paramètres ici.</span><span class="sxs-lookup"><span data-stu-id="437f8-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Configurer les paramètres de l’application](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="437f8-149"><a name="console"></a>Console</span><span class="sxs-lookup"><span data-stu-id="437f8-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Console Function App dans le portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="437f8-151">La console intégrée au portail est un outil de développement idéal lorsque vous souhaitez interagir avec Function App à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="437f8-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="437f8-152">Les commandes courantes incluent la création de fichiers et de répertoires et la navigation, ainsi que l’exécution de scripts et de fichiers de commandes.</span><span class="sxs-lookup"><span data-stu-id="437f8-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Console Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="437f8-154"><a name="kudu"></a>Outils avancés (Kudu)</span><span class="sxs-lookup"><span data-stu-id="437f8-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Kudu Function App dans le portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="437f8-156">Les outils avancés pour App Service (également appelé Kudu) donnent accès aux fonctionnalités d’administration avancées de votre Function App.</span><span class="sxs-lookup"><span data-stu-id="437f8-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="437f8-157">Dans Kudu, vous pouvez gérer les informations système, les paramètres d’application, les variables d’environnement, les extensions de site, les en-têtes HTTP et les variables de serveur.</span><span class="sxs-lookup"><span data-stu-id="437f8-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="437f8-158">Vous pouvez également lancer **Kudu** en naviguant vers le point de terminaison SCM pour votre Function App, comme `https://<myfunctionapp>.scm.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="437f8-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurer Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="437f8-160"><a name="deployment">Options de déploiement</span><span class="sxs-lookup"><span data-stu-id="437f8-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Options de déploiement Function App dans le portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="437f8-162">Functions vous permet de développer votre code de fonctions sur votre machine locale.</span><span class="sxs-lookup"><span data-stu-id="437f8-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="437f8-163">Vous pouvez ensuite charger votre projet Function App local vers Azure.</span><span class="sxs-lookup"><span data-stu-id="437f8-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="437f8-164">En plus du chargement FTP traditionnel, Functions vous permet de déployer votre Function App à l’aide de solutions d’intégration continue populaires, telles que GitHub, VSTS, Dropbox, Bitbucket, etc.</span><span class="sxs-lookup"><span data-stu-id="437f8-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="437f8-165">Pour plus d’informations, consultez [Déploiement continu pour Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="437f8-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="437f8-166">Pour charger manuellement à l’aide de FTP ou Git local, vous devez également [configurer vos informations d’identification de déploiement](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="437f8-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="437f8-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="437f8-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![CORS Function App dans le portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="437f8-169">Pour empêcher l’exécution de code malveillant dans vos services, App Service bloque les appels vers vos Function Apps provenant de sources externes.</span><span class="sxs-lookup"><span data-stu-id="437f8-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="437f8-170">Functions prend en charge des ressources cross-origin (CORS) pour vous permettre de définir une « liste approuvée » d’origines autorisées à partir desquelles vos fonctions peuvent accepter les demandes distantes.</span><span class="sxs-lookup"><span data-stu-id="437f8-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configurer l’élément CORS de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="437f8-172"><a name="auth"></a>Authentification</span><span class="sxs-lookup"><span data-stu-id="437f8-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Authentification Function App dans le portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="437f8-174">Lorsque les fonctions utilisent un déclencheur HTTP, vous pouvez exiger l’authentification préalable des appels.</span><span class="sxs-lookup"><span data-stu-id="437f8-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="437f8-175">App Service prend en charge l’authentification Azure Active Directory et la connexion avec des fournisseurs sociaux tels que Facebook, Microsoft et Twitter.</span><span class="sxs-lookup"><span data-stu-id="437f8-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="437f8-176">Pour plus d’informations sur la configuration de fournisseurs d’authentification spécifiques, consultez [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md) (Vue d’ensemble de l’authentification Azure App Service).</span><span class="sxs-lookup"><span data-stu-id="437f8-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configurer l’authentification pour une Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="437f8-178"><a name="swagger"></a>Définition de l’API</span><span class="sxs-lookup"><span data-stu-id="437f8-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Définition Swagger de l’API Function App dans le portail Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="437f8-180">Functions prend en charge Swagger pour permettre aux clients de consommer plus facilement vos fonctions déclenchées via HTTP.</span><span class="sxs-lookup"><span data-stu-id="437f8-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="437f8-181">Pour plus d’informations sur la création de définitions d’API avec Swagger, consultez [Prise en main d’API Apps, d’ASP.NET et de Swagger dans Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="437f8-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="437f8-182">Vous pouvez également utiliser les Functions Proxies pour définir une surface d’API unique pour plusieurs fonctions.</span><span class="sxs-lookup"><span data-stu-id="437f8-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="437f8-183">Pour plus d’informations, consultez [Utilisation de Azure Functions Proxies (préversion)](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="437f8-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configurer l’API de Function App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="437f8-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="437f8-185">Next steps</span></span>

+ [<span data-ttu-id="437f8-186">Configurer des applications web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="437f8-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="437f8-187">Déploiement continu pour Azure Functions</span><span class="sxs-lookup"><span data-stu-id="437f8-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



