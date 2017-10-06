---
title: "aide-mémoire aaaCloud rôle des Services Configuration XPath | Documents Microsoft"
description: "Bonjour divers paramètres XPath que vous pouvez utiliser dans les paramètres du rôle config tooexpose pour hello cloud service comme une variable d’environnement."
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
ms.openlocfilehash: 27f98f956a1c790c9bb30f9fefe1ab1736b2b150
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a><span data-ttu-id="c3452-103">Exposer les paramètres de configuration de rôle comme variable d'environnement avec XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-103">Expose role configuration settings as an environment variable with XPath</span></span>
<span data-ttu-id="c3452-104">Dans le traitement du service cloud hello ou fichier de définition de service de rôle web, vous pouvez exposer les valeurs de configuration d’exécution en tant que variables d’environnement.</span><span class="sxs-lookup"><span data-stu-id="c3452-104">In hello cloud service worker or web role service definition file, you can expose runtime configuration values as environment variables.</span></span> <span data-ttu-id="c3452-105">Hello les valeurs XPath suivantes est prises en charge (qui correspondent à des valeurs de tooAPI).</span><span class="sxs-lookup"><span data-stu-id="c3452-105">hello following XPath values are supported (which correspond tooAPI values).</span></span>

<span data-ttu-id="c3452-106">Ces valeurs XPath sont également disponibles via hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="c3452-106">These XPath values are also available through hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) library.</span></span> 

## <a name="app-running-in-emulator"></a><span data-ttu-id="c3452-107">Application qui s'exécute dans l'émulateur</span><span class="sxs-lookup"><span data-stu-id="c3452-107">App running in emulator</span></span>
<span data-ttu-id="c3452-108">Indique que cette application hello est en cours d’exécution dans l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-108">Indicates that hello app is running in hello emulator.</span></span>

| <span data-ttu-id="c3452-109">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-109">Type</span></span> | <span data-ttu-id="c3452-110">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-110">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-111">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-111">XPath</span></span> |<span data-ttu-id="c3452-112">xpath="/RoleEnvironment/Deployment/@emulated"</span><span class="sxs-lookup"><span data-stu-id="c3452-112">xpath="/RoleEnvironment/Deployment/@emulated"</span></span> |
| <span data-ttu-id="c3452-113">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-113">Code</span></span> |<span data-ttu-id="c3452-114">var x = RoleEnvironment.IsEmulated;</span><span class="sxs-lookup"><span data-stu-id="c3452-114">var x = RoleEnvironment.IsEmulated;</span></span> |

## <a name="deployment-id"></a><span data-ttu-id="c3452-115">ID de déploiement</span><span class="sxs-lookup"><span data-stu-id="c3452-115">Deployment ID</span></span>
<span data-ttu-id="c3452-116">Récupère l’ID de déploiement hello pour l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-116">Retrieves hello deployment ID for hello instance.</span></span>

| <span data-ttu-id="c3452-117">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-117">Type</span></span> | <span data-ttu-id="c3452-118">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-118">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-119">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-119">XPath</span></span> |<span data-ttu-id="c3452-120">xpath="/RoleEnvironment/Deployment/@id"</span><span class="sxs-lookup"><span data-stu-id="c3452-120">xpath="/RoleEnvironment/Deployment/@id"</span></span> |
| <span data-ttu-id="c3452-121">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-121">Code</span></span> |<span data-ttu-id="c3452-122">var deploymentId = RoleEnvironment.DeploymentId;</span><span class="sxs-lookup"><span data-stu-id="c3452-122">var deploymentId = RoleEnvironment.DeploymentId;</span></span> |

## <a name="role-id"></a><span data-ttu-id="c3452-123">ID de rôle</span><span class="sxs-lookup"><span data-stu-id="c3452-123">Role ID</span></span>
<span data-ttu-id="c3452-124">Récupère l’ID du rôle actuel hello pour l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-124">Retrieves hello current role ID for hello instance.</span></span>

| <span data-ttu-id="c3452-125">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-125">Type</span></span> | <span data-ttu-id="c3452-126">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-126">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-127">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-127">XPath</span></span> |<span data-ttu-id="c3452-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span><span class="sxs-lookup"><span data-stu-id="c3452-128">xpath="/RoleEnvironment/CurrentInstance/@id"</span></span> |
| <span data-ttu-id="c3452-129">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-129">Code</span></span> |<span data-ttu-id="c3452-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span><span class="sxs-lookup"><span data-stu-id="c3452-130">var id = RoleEnvironment.CurrentRoleInstance.Id;</span></span> |

## <a name="update-domain"></a><span data-ttu-id="c3452-131">Mettre à jour le domaine</span><span class="sxs-lookup"><span data-stu-id="c3452-131">Update domain</span></span>
<span data-ttu-id="c3452-132">Récupère le domaine de mise à jour hello d’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-132">Retrieves hello update domain of hello instance.</span></span>

| <span data-ttu-id="c3452-133">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-133">Type</span></span> | <span data-ttu-id="c3452-134">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-134">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-135">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-135">XPath</span></span> |<span data-ttu-id="c3452-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span><span class="sxs-lookup"><span data-stu-id="c3452-136">xpath="/RoleEnvironment/CurrentInstance/@updateDomain"</span></span> |
| <span data-ttu-id="c3452-137">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-137">Code</span></span> |<span data-ttu-id="c3452-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span><span class="sxs-lookup"><span data-stu-id="c3452-138">var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain;</span></span> |

## <a name="fault-domain"></a><span data-ttu-id="c3452-139">Domaine d'erreur</span><span class="sxs-lookup"><span data-stu-id="c3452-139">Fault domain</span></span>
<span data-ttu-id="c3452-140">Récupère le domaine par défaut de l’instance de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-140">Retrieves hello fault domain of hello instance.</span></span>

| <span data-ttu-id="c3452-141">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-141">Type</span></span> | <span data-ttu-id="c3452-142">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-142">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-143">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-143">XPath</span></span> |<span data-ttu-id="c3452-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span><span class="sxs-lookup"><span data-stu-id="c3452-144">xpath="/RoleEnvironment/CurrentInstance/@faultDomain"</span></span> |
| <span data-ttu-id="c3452-145">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-145">Code</span></span> |<span data-ttu-id="c3452-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span><span class="sxs-lookup"><span data-stu-id="c3452-146">var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain;</span></span> |

## <a name="role-name"></a><span data-ttu-id="c3452-147">Nom de rôle</span><span class="sxs-lookup"><span data-stu-id="c3452-147">Role name</span></span>
<span data-ttu-id="c3452-148">Récupère le nom du rôle d’instances de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-148">Retrieves hello role name of hello instances.</span></span>

| <span data-ttu-id="c3452-149">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-149">Type</span></span> | <span data-ttu-id="c3452-150">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-150">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-151">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-151">XPath</span></span> |<span data-ttu-id="c3452-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span><span class="sxs-lookup"><span data-stu-id="c3452-152">xpath="/RoleEnvironment/CurrentInstance/@roleName"</span></span> |
| <span data-ttu-id="c3452-153">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-153">Code</span></span> |<span data-ttu-id="c3452-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span><span class="sxs-lookup"><span data-stu-id="c3452-154">var rname = RoleEnvironment.CurrentRoleInstance.Role.Name;</span></span> |

## <a name="config-setting"></a><span data-ttu-id="c3452-155">Paramètre de configuration</span><span class="sxs-lookup"><span data-stu-id="c3452-155">Config setting</span></span>
<span data-ttu-id="c3452-156">Valeur hello récupère hello spécifiée de configuration.</span><span class="sxs-lookup"><span data-stu-id="c3452-156">Retrieves hello value of hello specified configuration setting.</span></span>

| <span data-ttu-id="c3452-157">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-157">Type</span></span> | <span data-ttu-id="c3452-158">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-158">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-159">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-159">XPath</span></span> |<span data-ttu-id="c3452-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span><span class="sxs-lookup"><span data-stu-id="c3452-160">xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value"</span></span> |
| <span data-ttu-id="c3452-161">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-161">Code</span></span> |<span data-ttu-id="c3452-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span><span class="sxs-lookup"><span data-stu-id="c3452-162">var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1");</span></span> |

## <a name="local-storage-path"></a><span data-ttu-id="c3452-163">Chemin de stockage local</span><span class="sxs-lookup"><span data-stu-id="c3452-163">Local storage path</span></span>
<span data-ttu-id="c3452-164">Récupère le chemin d’accès de stockage local hello pour l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-164">Retrieves hello local storage path for hello instance.</span></span>

| <span data-ttu-id="c3452-165">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-165">Type</span></span> | <span data-ttu-id="c3452-166">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-166">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-167">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-167">XPath</span></span> |<span data-ttu-id="c3452-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span><span class="sxs-lookup"><span data-stu-id="c3452-168">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path"</span></span> |
| <span data-ttu-id="c3452-169">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-169">Code</span></span> |<span data-ttu-id="c3452-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span><span class="sxs-lookup"><span data-stu-id="c3452-170">var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath;</span></span> |

## <a name="local-storage-size"></a><span data-ttu-id="c3452-171">Taille du stockage local</span><span class="sxs-lookup"><span data-stu-id="c3452-171">Local storage size</span></span>
<span data-ttu-id="c3452-172">Récupère la taille de hello de hello le stockage local pour l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-172">Retrieves hello size of hello local storage for hello instance.</span></span>

| <span data-ttu-id="c3452-173">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-173">Type</span></span> | <span data-ttu-id="c3452-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-174">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-175">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-175">XPath</span></span> |<span data-ttu-id="c3452-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span><span class="sxs-lookup"><span data-stu-id="c3452-176">xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB"</span></span> |
| <span data-ttu-id="c3452-177">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-177">Code</span></span> |<span data-ttu-id="c3452-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span><span class="sxs-lookup"><span data-stu-id="c3452-178">var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes;</span></span> |

## <a name="endpoint-protocol"></a><span data-ttu-id="c3452-179">Protocole du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="c3452-179">Endpoint protocol</span></span>
<span data-ttu-id="c3452-180">Récupère le protocole de point de terminaison hello pour l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-180">Retrieves hello endpoint protocol for hello instance.</span></span>

| <span data-ttu-id="c3452-181">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-181">Type</span></span> | <span data-ttu-id="c3452-182">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-182">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-183">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-183">XPath</span></span> |<span data-ttu-id="c3452-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span><span class="sxs-lookup"><span data-stu-id="c3452-184">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol"</span></span> |
| <span data-ttu-id="c3452-185">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-185">Code</span></span> |<span data-ttu-id="c3452-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span><span class="sxs-lookup"><span data-stu-id="c3452-186">var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol;</span></span> |

## <a name="endpoint-ip"></a><span data-ttu-id="c3452-187">IP du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="c3452-187">Endpoint IP</span></span>
<span data-ttu-id="c3452-188">Obtient hello spécifié l’adresse du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="c3452-188">Gets hello specified endpoint's IP address.</span></span>

| <span data-ttu-id="c3452-189">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-189">Type</span></span> | <span data-ttu-id="c3452-190">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-190">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-191">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-191">XPath</span></span> |<span data-ttu-id="c3452-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span><span class="sxs-lookup"><span data-stu-id="c3452-192">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address"</span></span> |
| <span data-ttu-id="c3452-193">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-193">Code</span></span> |<span data-ttu-id="c3452-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span><span class="sxs-lookup"><span data-stu-id="c3452-194">var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address</span></span> |

## <a name="endpoint-port"></a><span data-ttu-id="c3452-195">Port du point de terminaison</span><span class="sxs-lookup"><span data-stu-id="c3452-195">Endpoint port</span></span>
<span data-ttu-id="c3452-196">Récupère le port du point de terminaison hello pour l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="c3452-196">Retrieves hello endpoint port for hello instance.</span></span>

| <span data-ttu-id="c3452-197">Type</span><span class="sxs-lookup"><span data-stu-id="c3452-197">Type</span></span> | <span data-ttu-id="c3452-198">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-198">Example</span></span> |
| --- | --- |
| <span data-ttu-id="c3452-199">XPath</span><span class="sxs-lookup"><span data-stu-id="c3452-199">XPath</span></span> |<span data-ttu-id="c3452-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span><span class="sxs-lookup"><span data-stu-id="c3452-200">xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port"</span></span> |
| <span data-ttu-id="c3452-201">Code</span><span class="sxs-lookup"><span data-stu-id="c3452-201">Code</span></span> |<span data-ttu-id="c3452-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span><span class="sxs-lookup"><span data-stu-id="c3452-202">var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port;</span></span> |

## <a name="example"></a><span data-ttu-id="c3452-203">Exemple</span><span class="sxs-lookup"><span data-stu-id="c3452-203">Example</span></span>
<span data-ttu-id="c3452-204">Voici un exemple d’un rôle de travail qui crée une tâche de démarrage avec une variable d’environnement nommée `TestIsEmulated` définir toohello [ @emulated valeur xpath](#app-running-in-emulator).</span><span class="sxs-lookup"><span data-stu-id="c3452-204">Here is an example of a worker role that creates a startup task with an environment variable named `TestIsEmulated` set toohello [@emulated xpath value](#app-running-in-emulator).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="c3452-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3452-205">Next steps</span></span>
<span data-ttu-id="c3452-206">En savoir plus sur hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) fichier.</span><span class="sxs-lookup"><span data-stu-id="c3452-206">Learn more about hello [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) file.</span></span>

<span data-ttu-id="c3452-207">Créer un package [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .</span><span class="sxs-lookup"><span data-stu-id="c3452-207">Create a [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) package.</span></span>

<span data-ttu-id="c3452-208">Activer le [Bureau à distance](cloud-services-role-enable-remote-desktop.md) pour un rôle.</span><span class="sxs-lookup"><span data-stu-id="c3452-208">Enable [remote desktop](cloud-services-role-enable-remote-desktop.md) for a role.</span></span>

