---
title: "Aide-mémoire XPath de configuration d’un rôle Services cloud | Microsoft Docs"
description: "Les différents paramètres XPath que vous pouvez utiliser dans la configuration d’un rôle de service cloud pour exposer les paramètres sous la forme d'une variable d'environnement."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: fd6efac829d3fd9e2840362b8d2ff423add566d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="287e1-103">Exposer les paramètres de configuration de rôle comme variable d'environnement avec XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="287e1-104">Dans le fichier de définition de service du rôle Web ou du rôle de travail du service cloud, vous pouvez exposer les valeurs de configuration de l'exécution en tant que variables d'environnement.</span><span class="sxs-lookup"><span data-stu-id="287e1-104">In the cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="287e1-105">Les valeurs XPath suivantes sont prises en charge (qui correspondent aux valeurs de l'API).</span><span class="sxs-lookup"><span data-stu-id="287e1-105">The following XPath values are supported (which correspond to API values).</span></span>

<span data-ttu-id="287e1-106">Ces valeurs XPath sont également disponibles via la bibliothèque [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) .</span><span class="sxs-lookup"><span data-stu-id="287e1-106">These XPath values are also available through the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="287e1-107">Application qui s'exécute dans l'émulateur</span><span class="sxs-lookup"><span data-stu-id="287e1-107">App running in emulator</span></span>
<span data-ttu-id="287e1-108">Indique que l'application s'exécute dans l'émulateur.</span><span class="sxs-lookup"><span data-stu-id="287e1-108">Indicates that the app is running in the emulator.</span></span>

| <span data-ttu-id="287e1-109">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-109">Type</span></span> | <span data-ttu-id="287e1-110">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-111">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-111">XPath</span></span> |<span data-ttu-id="287e1-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="287e1-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="287e1-113">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-113">Code</span></span> |<span data-ttu-id="287e1-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="287e1-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="287e1-115">ID de déploiement</span><span class="sxs-lookup"><span data-stu-id="287e1-115">Deployment ID</span></span>
<span data-ttu-id="287e1-116">Récupère l'ID de déploiement de l'instance.</span><span class="sxs-lookup"><span data-stu-id="287e1-116">Retrieves the deployment ID for the instance.</span></span>

| <span data-ttu-id="287e1-117">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-117">Type</span></span> | <span data-ttu-id="287e1-118">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-119">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-119">XPath</span></span> |<span data-ttu-id="287e1-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="287e1-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="287e1-121">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-121">Code</span></span> |<span data-ttu-id="287e1-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="287e1-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="287e1-123">ID de rôle</span><span class="sxs-lookup"><span data-stu-id="287e1-123">Role ID</span></span>
<span data-ttu-id="287e1-124">Récupère l'ID de rôle actuel de l'instance.</span><span class="sxs-lookup"><span data-stu-id="287e1-124">Retrieves the current role ID for the instance.</span></span>

| <span data-ttu-id="287e1-125">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-125">Type</span></span> | <span data-ttu-id="287e1-126">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-127">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-127">XPath</span></span> |<span data-ttu-id="287e1-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="287e1-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="287e1-129">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-129">Code</span></span> |<span data-ttu-id="287e1-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="287e1-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="287e1-131">Mettre à jour le domaine</span><span class="sxs-lookup"><span data-stu-id="287e1-131">Update domain</span></span>
<span data-ttu-id="287e1-132">Récupère le domaine de mise à jour de l'instance.</span><span class="sxs-lookup"><span data-stu-id="287e1-132">Retrieves the update domain of the instance.</span></span>

| <span data-ttu-id="287e1-133">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-133">Type</span></span> | <span data-ttu-id="287e1-134">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-135">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-135">XPath</span></span> |<span data-ttu-id="287e1-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="287e1-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="287e1-137">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-137">Code</span></span> |<span data-ttu-id="287e1-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="287e1-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="287e1-139">Domaine d'erreur</span><span class="sxs-lookup"><span data-stu-id="287e1-139">Fault domain</span></span>
<span data-ttu-id="287e1-140">Récupère le domaine d’erreur de l'instance.</span><span class="sxs-lookup"><span data-stu-id="287e1-140">Retrieves the fault domain of the instance.</span></span>

| <span data-ttu-id="287e1-141">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-141">Type</span></span> | <span data-ttu-id="287e1-142">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-143">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-143">XPath</span></span> |<span data-ttu-id="287e1-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="287e1-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="287e1-145">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-145">Code</span></span> |<span data-ttu-id="287e1-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="287e1-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="287e1-147">Nom de rôle</span><span class="sxs-lookup"><span data-stu-id="287e1-147">Role name</span></span>
<span data-ttu-id="287e1-148">Récupère le nom de rôle des instances.</span><span class="sxs-lookup"><span data-stu-id="287e1-148">Retrieves the role name of the instances.</span></span>

| <span data-ttu-id="287e1-149">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-149">Type</span></span> | <span data-ttu-id="287e1-150">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-151">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-151">XPath</span></span> |<span data-ttu-id="287e1-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="287e1-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="287e1-153">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-153">Code</span></span> |<span data-ttu-id="287e1-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="287e1-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="287e1-155">Paramètre de configuration</span><span class="sxs-lookup"><span data-stu-id="287e1-155">Config setting</span></span>
<span data-ttu-id="287e1-156">Récupère la valeur du paramètre de configuration spécifié.</span><span class="sxs-lookup"><span data-stu-id="287e1-156">Retrieves the value of the specified configuration setting.</span></span>

| <span data-ttu-id="287e1-157">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-157">Type</span></span> | <span data-ttu-id="287e1-158">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-159">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-159">XPath</span></span> |<span data-ttu-id="287e1-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="287e1-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="287e1-161">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-161">Code</span></span> |<span data-ttu-id="287e1-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="287e1-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="287e1-163">Chemin de stockage local</span><span class="sxs-lookup"><span data-stu-id="287e1-163">Local storage path</span></span>
<span data-ttu-id="287e1-164">Récupère le chemin de stockage local de l'instance.</span><span class="sxs-lookup"><span data-stu-id="287e1-164">Retrieves the local storage path for the instance.</span></span>

| <span data-ttu-id="287e1-165">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-165">Type</span></span> | <span data-ttu-id="287e1-166">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-167">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-167">XPath</span></span> |<span data-ttu-id="287e1-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="287e1-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="287e1-169">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-169">Code</span></span> |<span data-ttu-id="287e1-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="287e1-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="287e1-171">Taille du stockage local</span><span class="sxs-lookup"><span data-stu-id="287e1-171">Local storage size</span></span>
<span data-ttu-id="287e1-172">Récupère la taille du stockage local de l'instance.</span><span class="sxs-lookup"><span data-stu-id="287e1-172">Retrieves the size of the local storage for the instance.</span></span>

| <span data-ttu-id="287e1-173">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-173">Type</span></span> | <span data-ttu-id="287e1-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-175">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-175">XPath</span></span> |<span data-ttu-id="287e1-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="287e1-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="287e1-177">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-177">Code</span></span> |<span data-ttu-id="287e1-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="287e1-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="287e1-179">Protocole du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="287e1-179">Endpoint protocol</span></span>
<span data-ttu-id="287e1-180">Récupère le protocole du point de terminaison de l'instance.</span><span class="sxs-lookup"><span data-stu-id="287e1-180">Retrieves the endpoint protocol for the instance.</span></span>

| <span data-ttu-id="287e1-181">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-181">Type</span></span> | <span data-ttu-id="287e1-182">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-183">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-183">XPath</span></span> |<span data-ttu-id="287e1-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="287e1-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="287e1-185">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-185">Code</span></span> |<span data-ttu-id="287e1-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="287e1-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="287e1-187">IP du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="287e1-187">Endpoint IP</span></span>
<span data-ttu-id="287e1-188">Récupère l'adresse IP du point de terminaison spécifié.</span><span class="sxs-lookup"><span data-stu-id="287e1-188">Gets the specified endpoint's IP address.</span></span>

| <span data-ttu-id="287e1-189">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-189">Type</span></span> | <span data-ttu-id="287e1-190">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-191">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-191">XPath</span></span> |<span data-ttu-id="287e1-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="287e1-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="287e1-193">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-193">Code</span></span> |<span data-ttu-id="287e1-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="287e1-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="287e1-195">Port du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="287e1-195">Endpoint port</span></span>
<span data-ttu-id="287e1-196">Récupère le port du point de terminaison de l'instance.</span><span class="sxs-lookup"><span data-stu-id="287e1-196">Retrieves the endpoint port for the instance.</span></span>

| <span data-ttu-id="287e1-197">Type</span><span class="sxs-lookup"><span data-stu-id="287e1-197">Type</span></span> | <span data-ttu-id="287e1-198">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="287e1-199">XPath</span><span class="sxs-lookup"><span data-stu-id="287e1-199">XPath</span></span> |<span data-ttu-id="287e1-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="287e1-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="287e1-201">Code</span><span class="sxs-lookup"><span data-stu-id="287e1-201">Code</span></span> |<span data-ttu-id="287e1-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="287e1-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="287e1-203">Exemple</span><span class="sxs-lookup"><span data-stu-id="287e1-203">Example</span></span>
<span data-ttu-id="287e1-204">Voici un exemple de rôle de travail qui crée une tâche de démarrage avec une variable d’environnement nommée `TestIsEmulated`, définie sur la [valeur xpath @emulated](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="287e1-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set to the [@emulated xpath value](#app-running-in-emulator).</span></span> 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a><span data-ttu-id="287e1-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="287e1-205">Next steps</span></span>
<span data-ttu-id="287e1-206">En savoir plus sur le fichier [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) .</span><span class="sxs-lookup"><span data-stu-id="287e1-206">Learn more about the [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="287e1-207">Créer un package [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="287e1-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="287e1-208">Activer le [Bureau à distance](cloud-services-role-enable-remote-desktop.md) pour un rôle.</span><span class="sxs-lookup"><span data-stu-id="287e1-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

