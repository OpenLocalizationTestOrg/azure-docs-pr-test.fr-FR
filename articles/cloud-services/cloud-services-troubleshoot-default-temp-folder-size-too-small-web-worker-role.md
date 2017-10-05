---
title: "La taille par défaut du dossier TEMP est trop petite pour un rôle | Microsoft Docs"
description: "Un rôle de service cloud offre un espace limité pour le dossier TEMP. Cet article fournit quelques suggestions pour éviter de manquer d'espace."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 577d090a009eb2331b401273257c7cc7c1eea772
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="8508b-104">La taille par défaut du dossier TEMP est trop petite pour un rôle web/de travail de service cloud</span><span class="sxs-lookup"><span data-stu-id="8508b-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="8508b-105">Le répertoire temporaire par défaut d'un rôle web ou de travail de service cloud a une taille maximale de 100 Mo, et risque d’être saturé à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="8508b-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="8508b-106">Cet article décrit comment éviter de manquer d'espace sur le répertoire temporaire.</span><span class="sxs-lookup"><span data-stu-id="8508b-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="8508b-107">Pourquoi l’espace devient-il insuffisant ?</span><span class="sxs-lookup"><span data-stu-id="8508b-107">Why do I run out of space?</span></span>
<span data-ttu-id="8508b-108">Les variables d’environnement Windows standard TEMP et TMP sont accessibles au code exécuté dans votre application.</span><span class="sxs-lookup"><span data-stu-id="8508b-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="8508b-109">TEMP et TMP pointent toutes les deux vers un répertoire unique d’une taille maximale de 100 Mo.</span><span class="sxs-lookup"><span data-stu-id="8508b-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="8508b-110">Les données stockées dans ce répertoire ne sont pas conservées tout au long du cycle de vie du service cloud ; si les instances de rôle d’un service cloud sont recyclées, le répertoire est nettoyé.</span><span class="sxs-lookup"><span data-stu-id="8508b-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="8508b-111">Suggestion pour corriger le problème</span><span class="sxs-lookup"><span data-stu-id="8508b-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="8508b-112">Implémentez l'une des alternatives suivantes :</span><span class="sxs-lookup"><span data-stu-id="8508b-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="8508b-113">Configurez une ressource de stockage local et accédez-y directement au lieu d’utiliser TEMP ou TMP.</span><span class="sxs-lookup"><span data-stu-id="8508b-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="8508b-114">Pour accéder à une ressource de stockage local à partir du code exécuté dans votre application, appelez la méthode [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8508b-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="8508b-115">Configurez une ressource de stockage local et pointez les répertoires TEMP et TMP vers le chemin d'accès de la ressource de stockage local.</span><span class="sxs-lookup"><span data-stu-id="8508b-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="8508b-116">Cette modification doit être effectuée dans la méthode [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) .</span><span class="sxs-lookup"><span data-stu-id="8508b-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="8508b-117">L'exemple de code suivant montre comment modifier les répertoires cible TEMP et TMP dans la méthode OnStart :</span><span class="sxs-lookup"><span data-stu-id="8508b-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="8508b-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8508b-118">Next steps</span></span>
<span data-ttu-id="8508b-119">Lisez un blog expliquant [comment augmenter la taille du dossier temporaire ASP.NET du rôle web Azure](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="8508b-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="8508b-120">Affichez plus d’ [articles de résolution des problèmes](/?tag=top-support-issue&product=cloud-services) liés aux services cloud.</span><span class="sxs-lookup"><span data-stu-id="8508b-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="8508b-121">Pour découvrir comment résoudre les problèmes liés aux rôles de service cloud à l’aide des données de diagnostic informatiques PaaS Azure, consultez la [série de blogs de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="8508b-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
