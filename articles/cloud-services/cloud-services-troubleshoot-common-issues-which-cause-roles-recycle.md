---
title: "Causes courantes de recyclage des rôles de service cloud | Microsoft Docs"
description: "Le recyclage soudain d’un rôle de service cloud peut entraîner d’importants temps d’arrêt. Voici quelques problèmes courants entraînant le recyclage des rôles, qui peuvent vous aider à réduire les temps d’arrêt."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: e55009c72b977ee4a30f6c71043bde483849f78f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="common-issues-that-cause-roles-to-recycle"></a><span data-ttu-id="df9f3-104">Problèmes courants provoquant le recyclage des rôles</span><span class="sxs-lookup"><span data-stu-id="df9f3-104">Common issues that cause roles to recycle</span></span>
<span data-ttu-id="df9f3-105">Cet article examine certaines des causes courantes entraînant des problèmes de déploiement, et indique des conseils de dépannage pour vous aider à résoudre ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="df9f3-105">This article discusses some of the common causes of deployment problems and provides troubleshooting tips to help you resolve these problems.</span></span> <span data-ttu-id="df9f3-106">Une instance de rôle qui ne démarre pas ou qui est recyclée entre les états Initialisation, Occupée et Arrêt indique un problème au niveau de l’application.</span><span class="sxs-lookup"><span data-stu-id="df9f3-106">An indication that a problem exists with an application is when the role instance fails to start, or it cycles between the initializing, busy, and stopping states.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a><span data-ttu-id="df9f3-107">Dépendances d'exécution manquantes</span><span class="sxs-lookup"><span data-stu-id="df9f3-107">Missing runtime dependencies</span></span>
<span data-ttu-id="df9f3-108">Si un rôle dans votre application repose sur un assembly qui ne fait pas partie du .NET Framework ou de la bibliothèque gérée Azure, vous devez inclure explicitement cet assembly dans le package d'application.</span><span class="sxs-lookup"><span data-stu-id="df9f3-108">If a role in your application relies on any assembly that is not part of the .NET Framework or the Azure managed library, you must explicitly include that assembly in the application package.</span></span> <span data-ttu-id="df9f3-109">N'oubliez pas que les autres infrastructures Microsoft ne sont pas disponibles par défaut dans Azure.</span><span class="sxs-lookup"><span data-stu-id="df9f3-109">Keep in mind that other Microsoft frameworks are not available on Azure by default.</span></span> <span data-ttu-id="df9f3-110">Si votre rôle repose sur une telle infrastructure, vous devez ajouter ces assemblys au package d'application.</span><span class="sxs-lookup"><span data-stu-id="df9f3-110">If your role relies on such a framework, you must add those assemblies to the application package.</span></span>

<span data-ttu-id="df9f3-111">Avant de générer et de mettre en package votre application, vérifiez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="df9f3-111">Before you build and package your application, verify the following:</span></span>

* <span data-ttu-id="df9f3-112">Si vous utilisez Visual Studio, assurez-vous que la propriété **Copy Local** est définie sur **True** pour chaque assembly référencé dans votre projet ne faisant pas partie du Kit de développement logiciel (SDK) Azure ni du .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="df9f3-112">If using Visual studio, make sure the **Copy Local** property is set to **True** for each referenced assembly in your project that is not part of the Azure SDK or the .NET Framework.</span></span>
* <span data-ttu-id="df9f3-113">Assurez-vous que le fichier web.config ne fait pas référence à des assemblys inutilisés dans l’élément compilation.</span><span class="sxs-lookup"><span data-stu-id="df9f3-113">Make sure the web.config file does not reference any unused assemblies in the compilation element.</span></span>
* <span data-ttu-id="df9f3-114">La propriété **Build Action** de chaque fichier .cshtml est définie sur **Content**.</span><span class="sxs-lookup"><span data-stu-id="df9f3-114">The **Build Action** of every .cshtml file is set to **Content**.</span></span> <span data-ttu-id="df9f3-115">Cela garantit que les fichiers s’affichent correctement dans le package et permet à d’autres fichiers référencés d’apparaître dans le package.</span><span class="sxs-lookup"><span data-stu-id="df9f3-115">This ensures that the files will appear correctly in the package and enables other referenced files to appear in the package.</span></span>

## <a name="assembly-targets-wrong-platform"></a><span data-ttu-id="df9f3-116">L’assembly cible la mauvaise plateforme</span><span class="sxs-lookup"><span data-stu-id="df9f3-116">Assembly targets wrong platform</span></span>
<span data-ttu-id="df9f3-117">Azure est un environnement 64 bits.</span><span class="sxs-lookup"><span data-stu-id="df9f3-117">Azure is a 64-bit environment.</span></span> <span data-ttu-id="df9f3-118">Par conséquent, les assemblys .NET compilés pour une cible 32 bits ne fonctionneront pas sur Azure.</span><span class="sxs-lookup"><span data-stu-id="df9f3-118">Therefore, .NET assemblies compiled for a 32-bit target won't work on Azure.</span></span>

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a><span data-ttu-id="df9f3-119">Le rôle génère des exceptions non gérées lors de l'initialisation ou de l'arrêt</span><span class="sxs-lookup"><span data-stu-id="df9f3-119">Role throws unhandled exceptions while initializing or stopping</span></span>
<span data-ttu-id="df9f3-120">Les exceptions levées par les méthodes de la classe [RoleEntryPoint], notamment les méthodes [OnStart], [OnStop] et [Run], sont des exceptions non prises en charge.</span><span class="sxs-lookup"><span data-stu-id="df9f3-120">Any exceptions that are thrown by the methods of the [RoleEntryPoint] class, which includes the [OnStart], [OnStop], and [Run] methods, are unhandled exceptions.</span></span> <span data-ttu-id="df9f3-121">Si une exception non gérée se produit dans une de ces méthodes, le rôle sera recyclé.</span><span class="sxs-lookup"><span data-stu-id="df9f3-121">If an unhandled exception occurs in one of these methods, the role will recycle.</span></span> <span data-ttu-id="df9f3-122">Si le rôle est recyclé à plusieurs reprises, il peut lever une exception non prise en charge chaque fois qu’il tente de démarrer.</span><span class="sxs-lookup"><span data-stu-id="df9f3-122">If the role is recycling repeatedly, it may be throwing an unhandled exception each time it tries to start.</span></span>

## <a name="role-returns-from-run-method"></a><span data-ttu-id="df9f3-123">Le rôle est renvoyé à partir de la méthode Run</span><span class="sxs-lookup"><span data-stu-id="df9f3-123">Role returns from Run method</span></span>
<span data-ttu-id="df9f3-124">La méthode [Run] est destinée à être exécutée indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="df9f3-124">The [Run] method is intended to run indefinitely.</span></span> <span data-ttu-id="df9f3-125">Si votre code remplace la méthode [Run] , il devrait être en veille indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="df9f3-125">If your code overrides the [Run] method, it should sleep indefinitely.</span></span> <span data-ttu-id="df9f3-126">Si la méthode [Run] est renvoyée, le rôle est recyclé.</span><span class="sxs-lookup"><span data-stu-id="df9f3-126">If the [Run] method returns, the role recycles.</span></span>

## <a name="incorrect-diagnosticsconnectionstring-setting"></a><span data-ttu-id="df9f3-127">Chaîne DiagnosticsConnectionString incorrecte</span><span class="sxs-lookup"><span data-stu-id="df9f3-127">Incorrect DiagnosticsConnectionString setting</span></span>
<span data-ttu-id="df9f3-128">Si l’application utilise les diagnostics Azure, votre fichier de configuration de service doit spécifier le paramètre de configuration `DiagnosticsConnectionString` .</span><span class="sxs-lookup"><span data-stu-id="df9f3-128">If application uses Azure Diagnostics, your service configuration file must specify the `DiagnosticsConnectionString` configuration setting.</span></span> <span data-ttu-id="df9f3-129">Ce paramètre doit spécifier une connexion HTTPS à votre compte de stockage dans Azure.</span><span class="sxs-lookup"><span data-stu-id="df9f3-129">This setting should specify an HTTPS connection to your storage account in Azure.</span></span>

<span data-ttu-id="df9f3-130">Pour vous assurer que votre paramètre `DiagnosticsConnectionString` est correct avant de déployer votre package d'application dans Azure, vérifiez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="df9f3-130">To ensure that your `DiagnosticsConnectionString` setting is correct before you deploy your application package to Azure, verify the following:</span></span>  

* <span data-ttu-id="df9f3-131">Le paramètre `DiagnosticsConnectionString` pointe vers un compte de stockage valide dans Azure.</span><span class="sxs-lookup"><span data-stu-id="df9f3-131">The `DiagnosticsConnectionString` setting points to a valid storage account in Azure.</span></span>  
  <span data-ttu-id="df9f3-132">Par défaut, ce paramètre pointe vers le compte de stockage émulé, et vous devez donc modifier explicitement ce paramètre avant de déployer votre package d'application.</span><span class="sxs-lookup"><span data-stu-id="df9f3-132">By default, this setting points to the emulated storage account, so you must explicitly change this setting before you deploy your application package.</span></span> <span data-ttu-id="df9f3-133">Si vous ne modifiez pas ce paramètre, une exception est générée lorsque l'instance de rôle tente de démarrer le moniteur de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="df9f3-133">If you do not change this setting, an exception is thrown when the role instance attempts to start the diagnostic monitor.</span></span> <span data-ttu-id="df9f3-134">L'instance de rôle risque alors d’être recyclée indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="df9f3-134">This may cause the role instance to recycle indefinitely.</span></span>
* <span data-ttu-id="df9f3-135">La chaîne de connexion est spécifiée au [format](../storage/common/storage-configure-connection-string.md) suivant.</span><span class="sxs-lookup"><span data-stu-id="df9f3-135">The connection string is specified in the following [format](../storage/common/storage-configure-connection-string.md).</span></span> <span data-ttu-id="df9f3-136">(Le protocole HTTPS doit être spécifié.) Remplacez *MyAccountName* par le nom de votre compte de stockage et *MyAccountKey* par votre clé d’accès :</span><span class="sxs-lookup"><span data-stu-id="df9f3-136">(The protocol must be specified as HTTPS.) Replace *MyAccountName* with the name of your storage account, and *MyAccountKey* with your access key:</span></span>    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  <span data-ttu-id="df9f3-137">Si vous développez votre application à l’aide d’outils Azure pour Microsoft Visual Studio, vous pouvez utiliser les pages de propriétés pour définir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="df9f3-137">If you are developing your application by using Azure Tools for Microsoft Visual Studio, you can use the property pages to set this value.</span></span>

## <a name="exported-certificate-does-not-include-private-key"></a><span data-ttu-id="df9f3-138">Le certificat exporté ne contient aucune clé privée</span><span class="sxs-lookup"><span data-stu-id="df9f3-138">Exported certificate does not include private key</span></span>
<span data-ttu-id="df9f3-139">Pour exécuter un rôle web sous SSL, vous devez vous assurer que votre certificat de gestion exporté inclut la clé privée.</span><span class="sxs-lookup"><span data-stu-id="df9f3-139">To run a web role under SSL, you must ensure that your exported management certificate includes the private key.</span></span> <span data-ttu-id="df9f3-140">Si vous utilisez le *gestionnaire de certificats Windows* pour exporter le certificat, veillez à sélectionner **Oui** pour l’option **Exporter la clé privée**.</span><span class="sxs-lookup"><span data-stu-id="df9f3-140">If you use the *Windows Certificate Manager* to export the certificate, be sure to select **Yes** for the **Export the private key** option.</span></span> <span data-ttu-id="df9f3-141">Le certificat doit être exporté au format PFX, l’unique format actuellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="df9f3-141">The certificate must be exported in the PFX format, which is the only format currently supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df9f3-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df9f3-142">Next steps</span></span>
<span data-ttu-id="df9f3-143">Affichez plus d’ [articles de résolution des problèmes](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) liés aux services cloud.</span><span class="sxs-lookup"><span data-stu-id="df9f3-143">View more [troubleshooting articles](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="df9f3-144">Affichez d’autres scénarios de recyclage des rôles dans la [série du blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="df9f3-144">View more role recycling scenarios at [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[Run]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx