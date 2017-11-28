---
title: aaaPublish-WebApplicationVM | Documents Microsoft
description: "Découvrez comment toodeploy un ordinateur virtuel de web application tooa. Ce script crée les ressources hello requis dans votre abonnement Azure si elles n’existent pas."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="42f30-104">Publish-WebApplicationVM (script Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="42f30-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="42f30-105">Déploie un ordinateur virtuel de web application tooa.</span><span class="sxs-lookup"><span data-stu-id="42f30-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="42f30-106">script de Hello crée les ressources hello requis dans votre abonnement Azure si elles n’existent pas.</span><span class="sxs-lookup"><span data-stu-id="42f30-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="42f30-107">Configuration</span><span class="sxs-lookup"><span data-stu-id="42f30-107">Configuration</span></span>
<span data-ttu-id="42f30-108">Hello chemin d’accès toohello fichier de configuration JSON qui décrit les détails de hello du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="42f30-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="42f30-109">Alias</span><span class="sxs-lookup"><span data-stu-id="42f30-109">Aliases</span></span> | <span data-ttu-id="42f30-110">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="42f30-111">Requis ?</span><span class="sxs-lookup"><span data-stu-id="42f30-111">Required?</span></span> |<span data-ttu-id="42f30-112">true</span><span class="sxs-lookup"><span data-stu-id="42f30-112">true</span></span> |
| <span data-ttu-id="42f30-113">Position</span><span class="sxs-lookup"><span data-stu-id="42f30-113">Position</span></span> |<span data-ttu-id="42f30-114">named</span><span class="sxs-lookup"><span data-stu-id="42f30-114">named</span></span> |
| <span data-ttu-id="42f30-115">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="42f30-115">Default value</span></span> |<span data-ttu-id="42f30-116">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-116">none</span></span> |
| <span data-ttu-id="42f30-117">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="42f30-117">Accept pipeline input?</span></span> |<span data-ttu-id="42f30-118">false</span><span class="sxs-lookup"><span data-stu-id="42f30-118">false</span></span> |
| <span data-ttu-id="42f30-119">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="42f30-119">Accept wildcard characters?</span></span> |<span data-ttu-id="42f30-120">false</span><span class="sxs-lookup"><span data-stu-id="42f30-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="42f30-121">SubscriptionName</span><span class="sxs-lookup"><span data-stu-id="42f30-121">SubscriptionName</span></span>
<span data-ttu-id="42f30-122">nom Hello de hello abonnement Azure dans lequel vous souhaitez toocreate hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="42f30-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="42f30-123">Alias</span><span class="sxs-lookup"><span data-stu-id="42f30-123">Aliases</span></span> | <span data-ttu-id="42f30-124">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="42f30-125">Requis ?</span><span class="sxs-lookup"><span data-stu-id="42f30-125">Required?</span></span> |<span data-ttu-id="42f30-126">false</span><span class="sxs-lookup"><span data-stu-id="42f30-126">false</span></span> |
| <span data-ttu-id="42f30-127">Position</span><span class="sxs-lookup"><span data-stu-id="42f30-127">Position</span></span> |<span data-ttu-id="42f30-128">named</span><span class="sxs-lookup"><span data-stu-id="42f30-128">named</span></span> |
| <span data-ttu-id="42f30-129">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="42f30-129">Default value</span></span> |<span data-ttu-id="42f30-130">Utilise le premier abonnement de hello dans le fichier d’abonnement hello</span><span class="sxs-lookup"><span data-stu-id="42f30-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="42f30-131">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="42f30-131">Accept pipeline input?</span></span> |<span data-ttu-id="42f30-132">false</span><span class="sxs-lookup"><span data-stu-id="42f30-132">false</span></span> |
| <span data-ttu-id="42f30-133">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="42f30-133">Accept wildcard characters?</span></span> |<span data-ttu-id="42f30-134">false</span><span class="sxs-lookup"><span data-stu-id="42f30-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="42f30-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="42f30-135">WebDeployPackage</span></span>
<span data-ttu-id="42f30-136">Hello chemin d’accès toohello web déploiement package toopublish toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="42f30-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="42f30-137">Vous pouvez créer ce package à l’aide d’Assistant de publication Web hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="42f30-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="42f30-138">Consultez [Création d’un package de déploiement web dans Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="42f30-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="42f30-139">Alias</span><span class="sxs-lookup"><span data-stu-id="42f30-139">Aliases</span></span> | <span data-ttu-id="42f30-140">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="42f30-141">Requis ?</span><span class="sxs-lookup"><span data-stu-id="42f30-141">Required?</span></span> |<span data-ttu-id="42f30-142">false</span><span class="sxs-lookup"><span data-stu-id="42f30-142">false</span></span> |
| <span data-ttu-id="42f30-143">Position</span><span class="sxs-lookup"><span data-stu-id="42f30-143">Position</span></span> |<span data-ttu-id="42f30-144">named</span><span class="sxs-lookup"><span data-stu-id="42f30-144">named</span></span> |
| <span data-ttu-id="42f30-145">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="42f30-145">Default value</span></span> |<span data-ttu-id="42f30-146">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-146">none</span></span> |
| <span data-ttu-id="42f30-147">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="42f30-147">Accept pipeline input?</span></span> |<span data-ttu-id="42f30-148">false</span><span class="sxs-lookup"><span data-stu-id="42f30-148">false</span></span> |
| <span data-ttu-id="42f30-149">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="42f30-149">Accept wildcard characters?</span></span> |<span data-ttu-id="42f30-150">false</span><span class="sxs-lookup"><span data-stu-id="42f30-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="42f30-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="42f30-151">AllowUntrusted</span></span>
<span data-ttu-id="42f30-152">Si la valeur est true, autoriser l’utilisation de hello de certificats qui ne sont pas signés par une autorité racine approuvée.</span><span class="sxs-lookup"><span data-stu-id="42f30-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="42f30-153">Alias</span><span class="sxs-lookup"><span data-stu-id="42f30-153">Aliases</span></span> | <span data-ttu-id="42f30-154">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="42f30-155">Requis ?</span><span class="sxs-lookup"><span data-stu-id="42f30-155">Required?</span></span> |<span data-ttu-id="42f30-156">false</span><span class="sxs-lookup"><span data-stu-id="42f30-156">false</span></span> |
| <span data-ttu-id="42f30-157">Position</span><span class="sxs-lookup"><span data-stu-id="42f30-157">Position</span></span> |<span data-ttu-id="42f30-158">named</span><span class="sxs-lookup"><span data-stu-id="42f30-158">named</span></span> |
| <span data-ttu-id="42f30-159">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="42f30-159">Default value</span></span> |<span data-ttu-id="42f30-160">false</span><span class="sxs-lookup"><span data-stu-id="42f30-160">false</span></span> |
| <span data-ttu-id="42f30-161">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="42f30-161">Accept pipeline input?</span></span> |<span data-ttu-id="42f30-162">false</span><span class="sxs-lookup"><span data-stu-id="42f30-162">false</span></span> |
| <span data-ttu-id="42f30-163">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="42f30-163">Accept wildcard characters?</span></span> |<span data-ttu-id="42f30-164">false</span><span class="sxs-lookup"><span data-stu-id="42f30-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="42f30-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="42f30-165">VMPassword</span></span>
<span data-ttu-id="42f30-166">informations d’identification de Hello pour le compte d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="42f30-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="42f30-167">Exemple : - VMPassword @{nom = « admin » ; Mot de passe = « password »}</span><span class="sxs-lookup"><span data-stu-id="42f30-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="42f30-168">Alias</span><span class="sxs-lookup"><span data-stu-id="42f30-168">Aliases</span></span> | <span data-ttu-id="42f30-169">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="42f30-170">Requis ?</span><span class="sxs-lookup"><span data-stu-id="42f30-170">Required?</span></span> |<span data-ttu-id="42f30-171">false</span><span class="sxs-lookup"><span data-stu-id="42f30-171">false</span></span> |
| <span data-ttu-id="42f30-172">Position</span><span class="sxs-lookup"><span data-stu-id="42f30-172">Position</span></span> |<span data-ttu-id="42f30-173">named</span><span class="sxs-lookup"><span data-stu-id="42f30-173">named</span></span> |
| <span data-ttu-id="42f30-174">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="42f30-174">Default value</span></span> |<span data-ttu-id="42f30-175">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-175">none</span></span> |
| <span data-ttu-id="42f30-176">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="42f30-176">Accept pipeline input?</span></span> |<span data-ttu-id="42f30-177">false</span><span class="sxs-lookup"><span data-stu-id="42f30-177">false</span></span> |
| <span data-ttu-id="42f30-178">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="42f30-178">Accept wildcard characters?</span></span> |<span data-ttu-id="42f30-179">false</span><span class="sxs-lookup"><span data-stu-id="42f30-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="42f30-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="42f30-180">DatabaseServerPassword</span></span>
<span data-ttu-id="42f30-181">informations d’identification de Hello pour la base de données SQL hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="42f30-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="42f30-182">Exemple : - DatabaseServerPassword @{nom = « admin » ; Mot de passe = « password »}</span><span class="sxs-lookup"><span data-stu-id="42f30-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="42f30-183">Alias</span><span class="sxs-lookup"><span data-stu-id="42f30-183">Aliases</span></span> | <span data-ttu-id="42f30-184">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="42f30-185">Requis ?</span><span class="sxs-lookup"><span data-stu-id="42f30-185">Required?</span></span> |<span data-ttu-id="42f30-186">false</span><span class="sxs-lookup"><span data-stu-id="42f30-186">false</span></span> |
| <span data-ttu-id="42f30-187">Position</span><span class="sxs-lookup"><span data-stu-id="42f30-187">Position</span></span> |<span data-ttu-id="42f30-188">named</span><span class="sxs-lookup"><span data-stu-id="42f30-188">named</span></span> |
| <span data-ttu-id="42f30-189">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="42f30-189">Default value</span></span> |<span data-ttu-id="42f30-190">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-190">none</span></span> |
| <span data-ttu-id="42f30-191">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="42f30-191">Accept pipeline input?</span></span> |<span data-ttu-id="42f30-192">false</span><span class="sxs-lookup"><span data-stu-id="42f30-192">false</span></span> |
| <span data-ttu-id="42f30-193">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="42f30-193">Accept wildcard characters?</span></span> |<span data-ttu-id="42f30-194">false</span><span class="sxs-lookup"><span data-stu-id="42f30-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="42f30-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="42f30-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="42f30-196">Si la valeur est true, les messages d’impression à partir de hello script toohello flux de sortie.</span><span class="sxs-lookup"><span data-stu-id="42f30-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="42f30-197">Alias</span><span class="sxs-lookup"><span data-stu-id="42f30-197">Aliases</span></span> | <span data-ttu-id="42f30-198">(aucun)</span><span class="sxs-lookup"><span data-stu-id="42f30-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="42f30-199">Requis ?</span><span class="sxs-lookup"><span data-stu-id="42f30-199">Required?</span></span> |<span data-ttu-id="42f30-200">false</span><span class="sxs-lookup"><span data-stu-id="42f30-200">false</span></span> |
| <span data-ttu-id="42f30-201">Position</span><span class="sxs-lookup"><span data-stu-id="42f30-201">Position</span></span> |<span data-ttu-id="42f30-202">named</span><span class="sxs-lookup"><span data-stu-id="42f30-202">named</span></span> |
| <span data-ttu-id="42f30-203">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="42f30-203">Default value</span></span> |<span data-ttu-id="42f30-204">false</span><span class="sxs-lookup"><span data-stu-id="42f30-204">false</span></span> |
| <span data-ttu-id="42f30-205">Accepter l'entrée de pipeline ?</span><span class="sxs-lookup"><span data-stu-id="42f30-205">Accept pipeline input?</span></span> |<span data-ttu-id="42f30-206">false</span><span class="sxs-lookup"><span data-stu-id="42f30-206">false</span></span> |
| <span data-ttu-id="42f30-207">Accepter les caractères génériques ?</span><span class="sxs-lookup"><span data-stu-id="42f30-207">Accept wildcard characters?</span></span> |<span data-ttu-id="42f30-208">false</span><span class="sxs-lookup"><span data-stu-id="42f30-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="42f30-209">Remarques</span><span class="sxs-lookup"><span data-stu-id="42f30-209">Remarks</span></span>
<span data-ttu-id="42f30-210">Pour une explication complète de la façon dont toouse hello script toocreate développement et les environnements de Test, consultez [environnements de Test et à l’aide de Scripts Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="42f30-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="42f30-211">fichier de configuration JSON Hello spécifie les détails de hello de nouveautés toobe déployé.</span><span class="sxs-lookup"><span data-stu-id="42f30-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="42f30-212">Il inclut des informations de hello que vous avez spécifié lorsque vous avez créé le projet hello, telles que le nom de hello, groupe d’affinités, image de disque dur virtuel et taille de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="42f30-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="42f30-213">Il inclut des points de terminaison hello sur l’ordinateur virtuel de hello, hello tooprovision de bases de données, le cas échéant et vous les paramètres de déploiement.</span><span class="sxs-lookup"><span data-stu-id="42f30-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="42f30-214">Hello suivant de code montre un exemple de fichier de configuration JSON :</span><span class="sxs-lookup"><span data-stu-id="42f30-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="42f30-215">Vous pouvez modifier hello JSON configuration fichier toochange, ce qui est configuré.</span><span class="sxs-lookup"><span data-stu-id="42f30-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="42f30-216">Un ordinateur virtuel et un service cloud sont requis, mais hello de base de données section est facultative.</span><span class="sxs-lookup"><span data-stu-id="42f30-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

