---
title: "taille du dossier TEMP aaaDefault est trop petite pour un rôle | Documents Microsoft"
description: "Un rôle de service cloud a une quantité limitée d’espace pour le dossier temporaire hello. Cet article fournit des suggestions sur la façon de tooavoid manque d’espace."
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
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="0d53b-104">La taille par défaut du dossier TEMP est trop petite pour un rôle web/de travail de service cloud</span><span class="sxs-lookup"><span data-stu-id="0d53b-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="0d53b-105">la valeur par défaut Hello répertoire temporaire d’un rôle web ou de travail du service cloud a une taille maximale de 100 Mo, ce qui peut devenir complète à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="0d53b-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="0d53b-106">Cet article décrit comment tooavoid manque d’espace pour le répertoire temporaire de hello.</span><span class="sxs-lookup"><span data-stu-id="0d53b-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="0d53b-107">Pourquoi l’espace devient-il insuffisant ?</span><span class="sxs-lookup"><span data-stu-id="0d53b-107">Why do I run out of space?</span></span>
<span data-ttu-id="0d53b-108">Hello standard Windows variables d’environnement TEMP et TMP sont toocode disponible qui est en cours d’exécution dans votre application.</span><span class="sxs-lookup"><span data-stu-id="0d53b-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="0d53b-109">TEMP et TMP point tooa répertoire unique qui a une taille maximale de 100 Mo.</span><span class="sxs-lookup"><span data-stu-id="0d53b-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="0d53b-110">Toutes les données stockées dans ce répertoire ne sont pas conservées lors du cycle de vie hello du service de cloud hello ; Si les instances de rôle hello dans un service cloud sont recyclées, répertoire de hello est nettoyé.</span><span class="sxs-lookup"><span data-stu-id="0d53b-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="0d53b-111">Problème de suggestion toofix hello</span><span class="sxs-lookup"><span data-stu-id="0d53b-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="0d53b-112">Implémentez l’une des hello suivant alternatives :</span><span class="sxs-lookup"><span data-stu-id="0d53b-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="0d53b-113">Configurez une ressource de stockage local et accédez-y directement au lieu d’utiliser TEMP ou TMP.</span><span class="sxs-lookup"><span data-stu-id="0d53b-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="0d53b-114">tooaccess une ressource de stockage local à partir de code qui s’exécute au sein de votre application, l’appel hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="0d53b-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="0d53b-115">Configurez une ressource de stockage local et pointez hello TEMP et TMP répertoires toopoint toohello chemin d’accès de ressource de stockage local hello.</span><span class="sxs-lookup"><span data-stu-id="0d53b-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="0d53b-116">Cette modification doit être effectuée dans hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) (méthode).</span><span class="sxs-lookup"><span data-stu-id="0d53b-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="0d53b-117">Hello exemple de code suivant montre comment toomodify hello répertoires cibles pour TEMP et TMP à partir de la méthode OnStart de hello :</span><span class="sxs-lookup"><span data-stu-id="0d53b-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
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

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="0d53b-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d53b-118">Next steps</span></span>
<span data-ttu-id="0d53b-119">Lire un blog décrivant [comment tooincrease hello taille du dossier temporaire de ASP.NET rôle Web Azure de hello](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53b-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="0d53b-120">Affichez plus d’ [articles de résolution des problèmes](/?tag=top-support-issue&product=cloud-services) liés aux services cloud.</span><span class="sxs-lookup"><span data-stu-id="0d53b-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="0d53b-121">toolearn comment les problèmes de rôle du service cloud tootroubleshoot à l’aide de données de diagnostic d’ordinateur PaaS Azure, afficher [série du blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d53b-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>
