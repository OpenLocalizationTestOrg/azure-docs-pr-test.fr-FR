---
title: "Package et modèle Cloud Service dans Azure | Microsoft Docs"
description: "Décrit le modèle de service cloud (.csdef, .cscfg) et le package (.cspkg) dans Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="bc6fc-103">Qu’est-ce que le modèle Cloud Service, et comment en créer un package ?</span><span class="sxs-lookup"><span data-stu-id="bc6fc-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="bc6fc-104">Un service cloud est créé à partir de trois composants : la définition de service *(.csdef)*, la configuration de service*(.cscfg)* et un package de service *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="bc6fc-105">Les deux fichiers XML **ServiceDefinition.csdef** et **ServiceConfig.cscfg** décrivent la structure du service cloud et sa configuration, qui désignent collectivement le modèle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="bc6fc-106">Le fichier ZIP **ServicePackage.cspkg** est généré à partir du fichier **ServiceDefinition.csdef** et il contient, entre autres, toutes les dépendances binaires requises.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="bc6fc-107">Azure crée un service cloud à partir des fichiers **ServicePackage.cspkg** et **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="bc6fc-108">Une fois que le service cloud s’exécute dans Azure, vous pouvez le reconfigurer via le fichier **ServiceConfig.cscfg** , mais vous ne pouvez pas en modifier la définition.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="bc6fc-109">Quels sont les sujets sur lesquels vous souhaitez avoir des informations supplémentaires ?</span><span class="sxs-lookup"><span data-stu-id="bc6fc-109">What would you like to know more about?</span></span>
* <span data-ttu-id="bc6fc-110">Je souhaite en savoir plus sur les fichiers [ServiceDefinition.csdef](#csdef) et [ServiceConfig.cscfg](#cscfg).</span><span class="sxs-lookup"><span data-stu-id="bc6fc-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="bc6fc-111">Je connais déjà cela, mais donnez-moi [quelques exemples](#next-steps) de configuration.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="bc6fc-112">Je souhaite créer le fichier [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="bc6fc-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="bc6fc-113">J’utilise Visual Studio et souhaite...</span><span class="sxs-lookup"><span data-stu-id="bc6fc-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="bc6fc-114">[Création d'un service cloud][vs_create]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="bc6fc-115">[Reconfigurer un service cloud existant][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="bc6fc-116">[Déployer un projet de service cloud][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="bc6fc-117">[Un Bureau à distance sur une instance de service cloud][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="bc6fc-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="bc6fc-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="bc6fc-119">Le fichier **ServiceDefinition.csdef** spécifie les paramètres qui sont utilisés par Azure pour configurer un service cloud.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="bc6fc-120">Le [schéma de définition du service Azure (fichier .csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) indique le format autorisé pour un fichier de définition de service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="bc6fc-121">L’exemple suivant présente les paramètres qui peuvent être définis pour le rôle web et le rôle de travail :</span><span class="sxs-lookup"><span data-stu-id="bc6fc-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="bc6fc-122">Vous pouvez vous reporter au [schéma de définition de service](https://msdn.microsoft.com/library/azure/ee758711.aspx) pour mieux comprendre le schéma XML utilisé ici. Toutefois, voici une brève explication de certains éléments :</span><span class="sxs-lookup"><span data-stu-id="bc6fc-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="bc6fc-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-123">**Sites**</span></span>  
<span data-ttu-id="bc6fc-124">Contient les définitions des sites ou applications web hébergés dans IIS 7.0.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="bc6fc-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-125">**InputEndpoints**</span></span>  
<span data-ttu-id="bc6fc-126">Contient les définitions des points de terminaison qui permettent de contacter le service cloud.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="bc6fc-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="bc6fc-128">Contient les définitions des points de terminaison qui sont utilisés par les instances de rôle pour communiquer entre eux.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="bc6fc-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="bc6fc-130">Contient les définitions de paramètre des fonctionnalités d’un rôle spécifique.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="bc6fc-131">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-131">**Certificates**</span></span>  
<span data-ttu-id="bc6fc-132">Contient les définitions des certificats nécessaires à un rôle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="bc6fc-133">L’exemple de code précédent illustre un certificat qui est utilisé pour la configuration d’Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="bc6fc-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-134">**LocalResources**</span></span>  
<span data-ttu-id="bc6fc-135">Contient les définitions des ressources de stockage local.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="bc6fc-136">Une ressource de stockage local est un répertoire réservé dans le système de fichiers de la machine virtuelle dans lequel s’exécute l’instance d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="bc6fc-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-137">**Imports**</span></span>  
<span data-ttu-id="bc6fc-138">Contient les définitions des modules importés.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="bc6fc-139">L’exemple de code précédent illustre les modules Connexion Bureau à distance et Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="bc6fc-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-140">**Startup**</span></span>  
<span data-ttu-id="bc6fc-141">Contient les tâches qui sont exécutées au démarrage du rôle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="bc6fc-142">Les tâches sont définies dans un fichier .cmd ou exécutable.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="bc6fc-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="bc6fc-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="bc6fc-144">La configuration des paramètres du service cloud est déterminée par les valeurs indiquées dans le fichier **ServiceConfiguration.cscfg** .</span><span class="sxs-lookup"><span data-stu-id="bc6fc-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="bc6fc-145">Vous spécifiez le nombre d’instances que vous souhaitez déployer pour chaque rôle dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="bc6fc-146">Les valeurs des paramètres de configuration que vous avez définis dans le fichier de définition de service sont ajoutées au fichier de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="bc6fc-147">Les empreintes numériques des certificats de gestion qui sont associés au service cloud sont également ajoutées au fichier.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="bc6fc-148">Le [schéma de configuration du service Azure (fichier .cscfg)](https://msdn.microsoft.com/library/azure/ee758710.aspx) indique le format autorisé pour un fichier de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="bc6fc-149">Le fichier de configuration de service n’est pas fourni dans le package de l’application, mais est chargé vers Azure en tant que fichier distinct et permet de configurer le service cloud.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="bc6fc-150">Vous pouvez charger un nouveau fichier de configuration de service sans redéployer votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="bc6fc-151">Les valeurs de configuration du service cloud peuvent être modifiées pendant l’exécution du service cloud.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="bc6fc-152">L’exemple suivant présente les paramètres de configuration qui peuvent être définis pour le rôle web et le rôle de travail :</span><span class="sxs-lookup"><span data-stu-id="bc6fc-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="bc6fc-153">Vous pouvez vous reporter au [schéma de configuration de service](https://msdn.microsoft.com/library/azure/ee758710.aspx) pour mieux comprendre le schéma XML utilisé ici. Toutefois, voici une brève explication des éléments :</span><span class="sxs-lookup"><span data-stu-id="bc6fc-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="bc6fc-154">**rôle web**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-154">**Instances**</span></span>  
<span data-ttu-id="bc6fc-155">Configure le nombre d’instances du rôle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="bc6fc-156">Pour empêcher le service cloud d’être potentiellement indisponible pendant les mises à niveau, il est conseillé de déployer plusieurs instances de vos rôles web.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="bc6fc-157">En déployant plus d’une instance, vous respectez les recommandations du [contrat de niveau de service de Calcul Azure](http://azure.microsoft.com/support/legal/sla/), ce qui garantit une connectivité externe à 99,95 % pour les rôles Internet lorsque deux instances de rôle au moins sont déployées pour un service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="bc6fc-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="bc6fc-159">Configure les paramètres des instances en cours d’exécution d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="bc6fc-160">Le nom des éléments `<Setting>` doit correspondre aux définitions de paramètre dans le fichier de définition de service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="bc6fc-161">**Certificates**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-161">**Certificates**</span></span>  
<span data-ttu-id="bc6fc-162">Configure les certificats utilisés par le service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="bc6fc-163">L’exemple de code précédent montre comment définir le certificat pour le module RemoteAccess.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="bc6fc-164">La valeur de l’attribut *thumbprint* doit être définie sur l’empreinte numérique du certificat à utiliser.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="bc6fc-165">L’empreinte du certificat peut être ajoutée au fichier de configuration à l’aide d’un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="bc6fc-166">La valeur peut également être ajoutée dans l’onglet **Certificats** de la page **Propriétés** du rôle dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="bc6fc-167">Définition des ports pour les instances de rôle</span><span class="sxs-lookup"><span data-stu-id="bc6fc-167">Defining ports for role instances</span></span>
<span data-ttu-id="bc6fc-168">Azure n’autorise qu’un point d’entrée à un rôle web.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="bc6fc-169">En d’autres termes, tout le trafic s’effectue via une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="bc6fc-170">Vous pouvez configurer vos sites web pour partager un port en configurant l’en-tête de l’hôte pour diriger la demande vers l’emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="bc6fc-171">Vous pouvez également configurer les applications pour qu’elles écoutent aux ports connus sur l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="bc6fc-172">L’exemple suivant illustre la configuration d’un rôle web avec un site web et une application web.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="bc6fc-173">Le site web est configuré comme emplacement d’entrée par défaut sur le port 80, et les applications web sont configurées pour recevoir des demandes d’un en-tête d’hôte différent, appelé « mail.mysite.cloudapp.net ».</span><span class="sxs-lookup"><span data-stu-id="bc6fc-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="bc6fc-174">Modification de la configuration d’un rôle</span><span class="sxs-lookup"><span data-stu-id="bc6fc-174">Changing the configuration of a role</span></span>
<span data-ttu-id="bc6fc-175">Vous pouvez mettre à jour la configuration du service cloud pendant son exécution dans Azure, sans le mettre hors connexion.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="bc6fc-176">Pour modifier les informations de configuration, vous pouvez charger un nouveau fichier de configuration ou modifier le fichier de configuration existant et l’appliquer à votre service en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="bc6fc-177">Les modifications suivantes peuvent être apportées à la configuration d’un service :</span><span class="sxs-lookup"><span data-stu-id="bc6fc-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="bc6fc-178">**Modification des valeurs des paramètres de configuration**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="bc6fc-179">Lorsqu’un paramètre de configuration est changé, une instance de rôle peut choisir d’appliquer la modification pendant que l’instance est en ligne ou de recycler l’instance normalement et d’appliquer la modification pendant qu’elle est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="bc6fc-180">**Modification de la topologie de service des instances de rôle**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="bc6fc-181">Les modifications de la topologie n’affectent pas les instances en cours d’exécution, sauf lorsqu’une instance est supprimée.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="bc6fc-182">Généralement, vous n’avez pas besoin de recycler les instances restantes, mais vous pouvez choisir de recycler des instances de rôle en réponse à une modification de la topologie.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="bc6fc-183">**Modification de l’empreinte de certificat**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="bc6fc-184">Vous ne pouvez mettre à jour un certificat que lorsqu’une instance de rôle est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="bc6fc-185">Si un certificat est ajouté, supprimé ou modifié pendant qu’une instance de rôle est en ligne, Azure la met normalement hors connexion pour mettre à jour le certificat avant de la remettre en ligne une fois la modification effectuée.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="bc6fc-186">Gestion des modifications de configuration à l’aide des événements de service Runtime</span><span class="sxs-lookup"><span data-stu-id="bc6fc-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="bc6fc-187">La [bibliothèque Runtime Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) inclut l’espace de noms [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx), qui fournit des classes pour interagir avec l’environnement Azure à partir d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="bc6fc-188">La classe [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) définit les événements suivants qui sont déclenchés avant et après une modification de la configuration :</span><span class="sxs-lookup"><span data-stu-id="bc6fc-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="bc6fc-189">**[Modification](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) d’un événement**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="bc6fc-190">Se produit avant que la modification de la configuration ne soit appliquée à une instance spécifiée d’un rôle, ce qui vous permet de supprimer les instances de rôle si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="bc6fc-191">**[Événement](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) modifié**</span><span class="sxs-lookup"><span data-stu-id="bc6fc-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="bc6fc-192">Se produit après l’application de la modification de la configuration à l’instance spécifiée d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="bc6fc-193">Comme les modifications de certificat placent toujours les instances d’un rôle hors connexion, elles ne déclenchent pas les événements RoleEnvironment.Changing ou RoleEnvironment.Changed.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="bc6fc-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="bc6fc-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="bc6fc-195">Pour déployer une application en tant que service cloud dans Azure, vous devez d’abord créer un package de l’application dans le format approprié.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="bc6fc-196">Vous pouvez utiliser l’outil de ligne de commande **CSPack** (installé avec le [Kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/)) pour créer le fichier de package en tant qu’alternative à Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="bc6fc-197">**CSPack** utilise le contenu du fichier de définition de service et du fichier de configuration de service pour définir le contenu du package.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="bc6fc-198">**CSPack** génère un fichier de package d’application (.cspkg) que vous pouvez charger dans Azure à l’aide du [portail Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="bc6fc-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="bc6fc-199">Par défaut, le package est nommé `[ServiceDefinitionFileName].cspkg`, mais vous pouvez indiquer un autre nom à l’aide de l’option `/out` de **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="bc6fc-200">**CSPack** se situe dans</span><span class="sxs-lookup"><span data-stu-id="bc6fc-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="bc6fc-201">Le fichier CSPack.exe (sur Windows) est disponible en exécutant le raccourci de l’ **invite de commandes Microsoft Azure** , qui est installé avec le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="bc6fc-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="bc6fc-202">Exécutez le programme CSPack.exe pour consulter la documentation relative à l’ensemble des commutateurs et commandes possibles.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="bc6fc-203">Exécutez votre service cloud localement dans **l’émulateur de calcul Microsoft Azure** et utilisez l’option **/copyonly**.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="bc6fc-204">Cette option copie les fichiers binaires de l’application dans une disposition de répertoire d’où ils peuvent être exécutés dans l’émulateur de calcul.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="bc6fc-205">Exemple de commande pour créer un package de service cloud</span><span class="sxs-lookup"><span data-stu-id="bc6fc-205">Example command to package a cloud service</span></span>
<span data-ttu-id="bc6fc-206">L’exemple suivant crée un package d’application qui contient les informations relatives à un rôle web.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="bc6fc-207">La commande spécifie le fichier de définition de service à utiliser, le répertoire dans lequel les fichiers binaires se trouvent, et le nom du fichier de package.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="bc6fc-208">Si l’application contient à la fois un rôle web et un rôle de travail, la commande suivante est utilisée :</span><span class="sxs-lookup"><span data-stu-id="bc6fc-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="bc6fc-209">Où les variables sont définies comme suit :</span><span class="sxs-lookup"><span data-stu-id="bc6fc-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="bc6fc-210">Variable</span><span class="sxs-lookup"><span data-stu-id="bc6fc-210">Variable</span></span> | <span data-ttu-id="bc6fc-211">Valeur</span><span class="sxs-lookup"><span data-stu-id="bc6fc-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bc6fc-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-212">\[DirectoryName\]</span></span> |<span data-ttu-id="bc6fc-213">Sous-répertoire du répertoire racine du projet qui contient le fichier .csdef du projet Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="bc6fc-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="bc6fc-215">Nom du fichier de définition de service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-215">The name of the service definition file.</span></span> <span data-ttu-id="bc6fc-216">Par défaut, ce fichier se nomme ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="bc6fc-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-217">\[OutputFileName\]</span></span> |<span data-ttu-id="bc6fc-218">Nom du fichier de package généré.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-218">The name for the generated package file.</span></span> <span data-ttu-id="bc6fc-219">En règle générale, il correspond au nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="bc6fc-220">Si aucun nom de fichier n’est spécifié, le package d’application est créé sous le nom \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="bc6fc-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-221">\[RoleName\]</span></span> |<span data-ttu-id="bc6fc-222">Nom du rôle défini dans le fichier de définition de service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="bc6fc-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="bc6fc-224">Emplacement des fichiers binaires correspondant au rôle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="bc6fc-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-225">\[VirtualPath\]</span></span> |<span data-ttu-id="bc6fc-226">Répertoires physiques pour chaque chemin d’accès virtuel défini dans la section Sites de la définition de service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="bc6fc-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="bc6fc-228">Répertoires physiques du contenu pour chaque chemin d’accès virtuel défini dans le nœud Site de la définition de service.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="bc6fc-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="bc6fc-230">Nom du fichier binaire correspondant au rôle.</span><span class="sxs-lookup"><span data-stu-id="bc6fc-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bc6fc-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bc6fc-231">Next steps</span></span>
<span data-ttu-id="bc6fc-232">Je crée un package de service cloud et je souhaite...</span><span class="sxs-lookup"><span data-stu-id="bc6fc-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="bc6fc-233">[Configurer un Bureau à distance pour une instance de service cloud][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="bc6fc-234">[Déployer un projet de service cloud][deploy]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="bc6fc-235">J’utilise Visual Studio et souhaite...</span><span class="sxs-lookup"><span data-stu-id="bc6fc-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="bc6fc-236">[Créer un nouveau service de cloud computing][vs_create]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="bc6fc-237">[Reconfigurer un service cloud existant][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="bc6fc-238">[Déployer un projet de service cloud][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="bc6fc-239">[Configurer un Bureau à distance pour une instance de service cloud][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="bc6fc-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
