---
title: aaaPublish-WebApplicationWebSite (script Windows PowerShell) | Documents Microsoft
description: "Découvrez comment toopublish un site web de projet tooan site Web Azure. Ce script crée les ressources hello requis dans votre abonnement Azure si elles n’existent pas."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="7e4ea-104">Publish-WebApplicationWebSite (script Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="7e4ea-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="7e4ea-105">Syntax</span></span>
<span data-ttu-id="7e4ea-106">Publie un tooan de projet web site Web Azure.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="7e4ea-107">script de Hello crée les ressources hello requis dans votre abonnement Azure si elles n’existent pas.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="7e4ea-108">Configuration</span><span class="sxs-lookup"><span data-stu-id="7e4ea-108">Configuration</span></span>
<span data-ttu-id="7e4ea-109">Hello chemin d’accès toohello fichier de configuration JSON qui décrit les détails de hello du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="7e4ea-110">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7e4ea-110">Parameter</span></span> | <span data-ttu-id="7e4ea-111">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="7e4ea-112">Alias</span><span class="sxs-lookup"><span data-stu-id="7e4ea-112">Aliases</span></span> |<span data-ttu-id="7e4ea-113">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-113">none</span></span> |
| <span data-ttu-id="7e4ea-114">Requis ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-114">Required?</span></span> |<span data-ttu-id="7e4ea-115">true</span><span class="sxs-lookup"><span data-stu-id="7e4ea-115">true</span></span> |
| <span data-ttu-id="7e4ea-116">Position</span><span class="sxs-lookup"><span data-stu-id="7e4ea-116">Position</span></span> |<span data-ttu-id="7e4ea-117">named</span><span class="sxs-lookup"><span data-stu-id="7e4ea-117">named</span></span> |
| <span data-ttu-id="7e4ea-118">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-118">Default value</span></span> |<span data-ttu-id="7e4ea-119">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-119">none</span></span> |
| <span data-ttu-id="7e4ea-120">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-120">Accept pipeline input?</span></span> |<span data-ttu-id="7e4ea-121">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-121">false</span></span> |
| <span data-ttu-id="7e4ea-122">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-122">Accept wildcard characters?</span></span> |<span data-ttu-id="7e4ea-123">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="7e4ea-124">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="7e4ea-124">SubscriptionName</span></span>
<span data-ttu-id="7e4ea-125">nom Hello Hello abonnement Azure que vous souhaitez le site Web de toocreate hello dans.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="7e4ea-126">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7e4ea-126">Parameter</span></span> | <span data-ttu-id="7e4ea-127">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="7e4ea-128">Alias</span><span class="sxs-lookup"><span data-stu-id="7e4ea-128">Aliases</span></span> |<span data-ttu-id="7e4ea-129">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-129">none</span></span> |
| <span data-ttu-id="7e4ea-130">Requis ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-130">Required?</span></span> |<span data-ttu-id="7e4ea-131">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-131">false</span></span> |
| <span data-ttu-id="7e4ea-132">Position</span><span class="sxs-lookup"><span data-stu-id="7e4ea-132">Position</span></span> |<span data-ttu-id="7e4ea-133">named</span><span class="sxs-lookup"><span data-stu-id="7e4ea-133">named</span></span> |
| <span data-ttu-id="7e4ea-134">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-134">Default value</span></span> |<span data-ttu-id="7e4ea-135">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-135">none</span></span> |
| <span data-ttu-id="7e4ea-136">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-136">Accept pipeline input?</span></span> |<span data-ttu-id="7e4ea-137">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-137">false</span></span> |
| <span data-ttu-id="7e4ea-138">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-138">Accept wildcard characters?</span></span> |<span data-ttu-id="7e4ea-139">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="7e4ea-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="7e4ea-140">WebDeployPackage</span></span>
<span data-ttu-id="7e4ea-141">Hello chemin d’accès toohello web déploiement package toopublish toohello site Web.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="7e4ea-142">Vous pouvez créer ce package à l’aide d’Assistant de publication Web hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="7e4ea-143">Pour plus d’informations, consultez [Prise en main des services cloud Azure et d'ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="7e4ea-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="7e4ea-144">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7e4ea-144">Parameter</span></span> | <span data-ttu-id="7e4ea-145">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="7e4ea-146">Alias</span><span class="sxs-lookup"><span data-stu-id="7e4ea-146">Aliases</span></span> |<span data-ttu-id="7e4ea-147">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-147">none</span></span> |
| <span data-ttu-id="7e4ea-148">Requis ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-148">Required?</span></span> |<span data-ttu-id="7e4ea-149">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-149">false</span></span> |
| <span data-ttu-id="7e4ea-150">Position</span><span class="sxs-lookup"><span data-stu-id="7e4ea-150">Position</span></span> |<span data-ttu-id="7e4ea-151">named</span><span class="sxs-lookup"><span data-stu-id="7e4ea-151">named</span></span> |
| <span data-ttu-id="7e4ea-152">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-152">Default value</span></span> |<span data-ttu-id="7e4ea-153">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-153">none</span></span> |
| <span data-ttu-id="7e4ea-154">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-154">Accept pipeline input?</span></span> |<span data-ttu-id="7e4ea-155">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-155">false</span></span> |
| <span data-ttu-id="7e4ea-156">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-156">Accept wildcard characters?</span></span> |<span data-ttu-id="7e4ea-157">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="7e4ea-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="7e4ea-158">DatabaseServerPassword</span></span>
<span data-ttu-id="7e4ea-159">nom d’utilisateur Hello et le mot de passe pour la base de données SQL hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="7e4ea-160">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7e4ea-160">Parameter</span></span> | <span data-ttu-id="7e4ea-161">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="7e4ea-162">Alias</span><span class="sxs-lookup"><span data-stu-id="7e4ea-162">Aliases</span></span> |<span data-ttu-id="7e4ea-163">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-163">none</span></span> |
| <span data-ttu-id="7e4ea-164">Requis ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-164">Required?</span></span> |<span data-ttu-id="7e4ea-165">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-165">false</span></span> |
| <span data-ttu-id="7e4ea-166">Position</span><span class="sxs-lookup"><span data-stu-id="7e4ea-166">Position</span></span> |<span data-ttu-id="7e4ea-167">named</span><span class="sxs-lookup"><span data-stu-id="7e4ea-167">named</span></span> |
| <span data-ttu-id="7e4ea-168">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-168">Default value</span></span> |<span data-ttu-id="7e4ea-169">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-169">none</span></span> |
| <span data-ttu-id="7e4ea-170">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-170">Accept pipeline input?</span></span> |<span data-ttu-id="7e4ea-171">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-171">false</span></span> |
| <span data-ttu-id="7e4ea-172">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-172">Accept wildcard characters?</span></span> |<span data-ttu-id="7e4ea-173">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="7e4ea-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="7e4ea-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="7e4ea-175">Si la valeur est true, les messages d’impression à partir de hello script toohello flux de sortie.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="7e4ea-176">Paramètre</span><span class="sxs-lookup"><span data-stu-id="7e4ea-176">Parameter</span></span> | <span data-ttu-id="7e4ea-177">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="7e4ea-178">Alias</span><span class="sxs-lookup"><span data-stu-id="7e4ea-178">Aliases</span></span> |<span data-ttu-id="7e4ea-179">(aucun)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-179">none</span></span> |
| <span data-ttu-id="7e4ea-180">Requis ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-180">Required?</span></span> |<span data-ttu-id="7e4ea-181">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-181">false</span></span> |
| <span data-ttu-id="7e4ea-182">Position</span><span class="sxs-lookup"><span data-stu-id="7e4ea-182">Position</span></span> |<span data-ttu-id="7e4ea-183">named</span><span class="sxs-lookup"><span data-stu-id="7e4ea-183">named</span></span> |
| <span data-ttu-id="7e4ea-184">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="7e4ea-184">Default value</span></span> |<span data-ttu-id="7e4ea-185">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-185">false</span></span> |
| <span data-ttu-id="7e4ea-186">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-186">Accept pipeline input?</span></span> |<span data-ttu-id="7e4ea-187">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-187">false</span></span> |
| <span data-ttu-id="7e4ea-188">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="7e4ea-188">Accept wildcard characters?</span></span> |<span data-ttu-id="7e4ea-189">false</span><span class="sxs-lookup"><span data-stu-id="7e4ea-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="7e4ea-190">Remarques</span><span class="sxs-lookup"><span data-stu-id="7e4ea-190">Remarks</span></span>
<span data-ttu-id="7e4ea-191">Pour une explication complète de la façon dont toouse hello script toocreate développement et les environnements de Test, consultez [environnements de Test et à l’aide de Scripts Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="7e4ea-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="7e4ea-192">fichier de configuration JSON Hello spécifie les détails de hello de nouveautés toobe déployé.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="7e4ea-193">Il inclut des informations de hello que vous avez spécifié lorsque vous avez créé le projet hello, telles que le nom de hello et nom d’utilisateur pour le site Web de hello.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="7e4ea-194">Il inclut également hello tooprovision de base de données, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="7e4ea-195">Hello suivant de code montre un exemple de fichier de configuration JSON :</span><span class="sxs-lookup"><span data-stu-id="7e4ea-195">hello following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="7e4ea-196">Vous pouvez modifier hello JSON configuration fichier toochange, ce qui est déployé.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="7e4ea-197">Une section du site Web est requise, mais section base de données de hello est facultatif.</span><span class="sxs-lookup"><span data-stu-id="7e4ea-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e4ea-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e4ea-198">Next steps</span></span>
<span data-ttu-id="7e4ea-199">Pour plus d’informations, consultez [Publish-WebApplicationVM (script Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="7e4ea-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

