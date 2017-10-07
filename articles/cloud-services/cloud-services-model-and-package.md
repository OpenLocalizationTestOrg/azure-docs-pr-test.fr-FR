---
title: "aaaWhat est un modèle de Service Cloud et un package | Documents Microsoft"
description: "Décrit le modèle de service cloud hello (.csdef, .cscfg) et de package (.cspkg) dans Azure"
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
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="bcfae-103">Nouveautés du modèle de Service de cloud computing hello et comment il package ?</span><span class="sxs-lookup"><span data-stu-id="bcfae-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="bcfae-104">Un service cloud est créé à partir de trois composants, définition de service hello *(.csdef)*, la configuration de service de hello *(.cscfg)*et un package de service *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="bcfae-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="bcfae-105">Les deux hello **ServiceDefinition.csdef** et **ServiceConfig.cscfg** fichiers basé sur XML et décrivent structure hello du service de cloud computing hello et la façon dont il est configuré ; collectivement appelé modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="bcfae-106">Hello **ServicePackage.cspkg** est un fichier zip qui est généré à partir de hello **ServiceDefinition.csdef** et entre autres choses, contient toutes les dépendances de fichier binaire hello requis.</span><span class="sxs-lookup"><span data-stu-id="bcfae-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="bcfae-107">Azure crée un service cloud à partir de ces deux hello **ServicePackage.cspkg** et hello **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="bcfae-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="bcfae-108">Une fois que le service de cloud computing hello s’exécute dans Azure, vous pouvez le reconfigurer via hello **ServiceConfig.cscfg** fichier, mais vous ne pouvez pas modifier la définition de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="bcfae-109">Sur quel contenu souhaitez-vous tooknow plus ?</span><span class="sxs-lookup"><span data-stu-id="bcfae-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="bcfae-110">Je veux tooknow plus hello [ServiceDefinition.csdef](#csdef) et [ServiceConfig.cscfg](#cscfg) fichiers.</span><span class="sxs-lookup"><span data-stu-id="bcfae-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="bcfae-111">Je connais déjà cela, mais donnez-moi [quelques exemples](#next-steps) de configuration.</span><span class="sxs-lookup"><span data-stu-id="bcfae-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="bcfae-112">Je veux toocreate hello [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="bcfae-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="bcfae-113">J’utilise Visual Studio et souhaite...</span><span class="sxs-lookup"><span data-stu-id="bcfae-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="bcfae-114">[Création d'un service cloud][vs_create]</span><span class="sxs-lookup"><span data-stu-id="bcfae-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="bcfae-115">[Reconfigurer un service cloud existant][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="bcfae-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="bcfae-116">[Déployer un projet de service cloud][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="bcfae-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="bcfae-117">[Un Bureau à distance sur une instance de service cloud][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="bcfae-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="bcfae-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="bcfae-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="bcfae-119">Hello **ServiceDefinition.csdef** fichier spécifie les paramètres de hello sont utilisées par Azure tooconfigure un service cloud.</span><span class="sxs-lookup"><span data-stu-id="bcfae-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="bcfae-120">Hello [schéma de définition de Service Azure (fichier de .csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) fournit le format autorisé de hello pour un fichier de définition de service.</span><span class="sxs-lookup"><span data-stu-id="bcfae-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="bcfae-121">Hello suivant montre les paramètres hello qui peuvent être définis pour hello Web et rôles de travail :</span><span class="sxs-lookup"><span data-stu-id="bcfae-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

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

<span data-ttu-id="bcfae-122">Vous pouvez faire référence toohello [schéma de définition du Service](https://msdn.microsoft.com/library/azure/ee758711.aspx) pour mieux comprendre le fonctionnement du schéma XML de hello utilisé ici, toutefois, voici une explication rapide de certains des éléments de hello :</span><span class="sxs-lookup"><span data-stu-id="bcfae-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="bcfae-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="bcfae-123">**Sites**</span></span>  
<span data-ttu-id="bcfae-124">Contient les définitions de hello pour les applications web ou des sites Web qui sont hébergées dans IIS 7.</span><span class="sxs-lookup"><span data-stu-id="bcfae-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="bcfae-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="bcfae-125">**InputEndpoints**</span></span>  
<span data-ttu-id="bcfae-126">Contient des définitions de hello pour les points de terminaison utilisé toocontact hello cloud service.</span><span class="sxs-lookup"><span data-stu-id="bcfae-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="bcfae-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="bcfae-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="bcfae-128">Contient les définitions de hello pour les points de terminaison qui sont utilisés par toocommunicate d’instances de rôle entre eux.</span><span class="sxs-lookup"><span data-stu-id="bcfae-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="bcfae-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="bcfae-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="bcfae-130">Contient les définitions de paramètre hello pour les fonctionnalités d’un rôle spécifique.</span><span class="sxs-lookup"><span data-stu-id="bcfae-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="bcfae-131">**Certificats**</span><span class="sxs-lookup"><span data-stu-id="bcfae-131">**Certificates**</span></span>  
<span data-ttu-id="bcfae-132">Contient les définitions de hello pour les certificats qui sont nécessaires pour un rôle.</span><span class="sxs-lookup"><span data-stu-id="bcfae-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="bcfae-133">exemple de code précédent Hello montre un certificat qui est utilisé pour la configuration de hello de Connect de Azure.</span><span class="sxs-lookup"><span data-stu-id="bcfae-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="bcfae-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="bcfae-134">**LocalResources**</span></span>  
<span data-ttu-id="bcfae-135">Contient les définitions de hello pour les ressources de stockage local.</span><span class="sxs-lookup"><span data-stu-id="bcfae-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="bcfae-136">Une ressource de stockage local est un répertoire réservé sur le système de fichiers hello de machine virtuelle de hello dans lequel une instance d’un rôle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bcfae-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="bcfae-137">**Imports**</span><span class="sxs-lookup"><span data-stu-id="bcfae-137">**Imports**</span></span>  
<span data-ttu-id="bcfae-138">Contient les définitions de hello pour les modules importés.</span><span class="sxs-lookup"><span data-stu-id="bcfae-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="bcfae-139">exemple de code précédent Hello présente les modules de hello pour la connexion Bureau à distance et Azure Connect.</span><span class="sxs-lookup"><span data-stu-id="bcfae-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="bcfae-140">**Startup**</span><span class="sxs-lookup"><span data-stu-id="bcfae-140">**Startup**</span></span>  
<span data-ttu-id="bcfae-141">Contient des tâches qui sont exécutées lorsque le rôle de hello démarre.</span><span class="sxs-lookup"><span data-stu-id="bcfae-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="bcfae-142">tâches de Hello sont définies dans un fichier .cmd ou fichier exécutable.</span><span class="sxs-lookup"><span data-stu-id="bcfae-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="bcfae-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="bcfae-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="bcfae-144">configuration de Hello de paramètres hello pour votre service cloud est déterminée par les valeurs hello Bonjour **ServiceConfiguration.cscfg** fichier.</span><span class="sxs-lookup"><span data-stu-id="bcfae-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="bcfae-145">Vous spécifiez le nombre de hello d’instances que vous souhaitez toodeploy pour chaque rôle dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="bcfae-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="bcfae-146">les valeurs Hello hello paramètres de configuration que vous avez définie dans le fichier de définition de service hello sont ajoutés toohello fichier de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="bcfae-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="bcfae-147">empreintes numériques de Hello pour les certificats de gestion qui sont associés au service de cloud computing hello sont également ajoutés toohello fichier.</span><span class="sxs-lookup"><span data-stu-id="bcfae-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="bcfae-148">Hello [schéma de Configuration du Service Azure (.cscfg fichier)](https://msdn.microsoft.com/library/azure/ee758710.aspx) fournit le format autorisé de hello pour un fichier de configuration de service.</span><span class="sxs-lookup"><span data-stu-id="bcfae-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="bcfae-149">Hello fichier de configuration de service n’est pas fourni avec l’application hello, mais est tooAzure téléchargé dans un fichier distinct et est utilisé tooconfigure hello service cloud.</span><span class="sxs-lookup"><span data-stu-id="bcfae-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="bcfae-150">Vous pouvez charger un nouveau fichier de configuration de service sans redéployer votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="bcfae-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="bcfae-151">les valeurs de configuration Hello pour le service cloud hello peuvent être modifiés pendant l’exécution du service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="bcfae-152">Hello suivant montre les paramètres de configuration hello qui peuvent être définis pour hello Web et rôles de travail :</span><span class="sxs-lookup"><span data-stu-id="bcfae-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

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

<span data-ttu-id="bcfae-153">Vous pouvez faire référence toohello [schéma de Configuration de Service](https://msdn.microsoft.com/library/azure/ee758710.aspx) pour une meilleure compréhension hello XSD utilisé ici, toutefois, voici une explication rapide des éléments de hello :</span><span class="sxs-lookup"><span data-stu-id="bcfae-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="bcfae-154">**Instances**</span><span class="sxs-lookup"><span data-stu-id="bcfae-154">**Instances**</span></span>  
<span data-ttu-id="bcfae-155">Configure le nombre hello de l’exécution des instances de rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="bcfae-156">tooprevent votre cloud service devienne indisponible pendant les mises à niveau, il est recommandé de déployer plusieurs instances de vos rôles web.</span><span class="sxs-lookup"><span data-stu-id="bcfae-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="bcfae-157">En déployant plusieurs instances, vous respectez les instructions toohello Bonjour [Azure Compute contrat (SLA)](http://azure.microsoft.com/support/legal/sla/), ce qui garantit une connectivité externe à 99,95 % pour les rôles Internet lorsque deux ou plusieurs rôles instances sont déployées pour un service.</span><span class="sxs-lookup"><span data-stu-id="bcfae-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="bcfae-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="bcfae-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="bcfae-159">Configure les paramètres hello pour hello instances pour un rôle en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bcfae-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="bcfae-160">nom Hello Hello `<Setting>` éléments doivent correspondre à des définitions de paramètre hello dans le fichier de définition de service hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="bcfae-161">**Certificats**</span><span class="sxs-lookup"><span data-stu-id="bcfae-161">**Certificates**</span></span>  
<span data-ttu-id="bcfae-162">Configure les certificats de hello sont utilisées par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="bcfae-163">exemple de code Hello précédent montre comment toodefine hello certificat pour le module RemoteAccess de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="bcfae-164">Hello valeur Hello *l’empreinte numérique* attribut doit être défini à l’empreinte numérique toohello de hello certificat toouse.</span><span class="sxs-lookup"><span data-stu-id="bcfae-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="bcfae-165">fichier de configuration toohello peut être ajouté à l’empreinte numérique Hello pour le certificat de hello, à l’aide d’un éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="bcfae-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="bcfae-166">Ou, à la valeur de hello peut être ajoutée sur hello **certificats** onglet Hello **propriétés** page de rôle hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bcfae-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="bcfae-167">Définition des ports pour les instances de rôle</span><span class="sxs-lookup"><span data-stu-id="bcfae-167">Defining ports for role instances</span></span>
<span data-ttu-id="bcfae-168">Azure ne permet qu’un seul rôle web de tooa de point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="bcfae-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="bcfae-169">En d’autres termes, tout le trafic s’effectue via une adresse IP.</span><span class="sxs-lookup"><span data-stu-id="bcfae-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="bcfae-170">Vous pouvez configurer vos sites Web de tooshare un port en configurant hello hôte en-tête toodirect hello demande toohello emplacement correct.</span><span class="sxs-lookup"><span data-stu-id="bcfae-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="bcfae-171">Vous pouvez également configurer les ports de toowell connue toolisten applications sur l’adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="bcfae-172">Hello exemple suivant illustre les configuration hello pour un rôle web avec un site Web et l’application web.</span><span class="sxs-lookup"><span data-stu-id="bcfae-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="bcfae-173">site Web de Hello est configuré en tant qu’emplacement d’entrée hello par défaut sur le port 80, et les applications web hello sont demandes tooreceive configuré à partir d’un en-tête d’hôte de remplacement est appelé « mail.mysite.cloudapp.net ».</span><span class="sxs-lookup"><span data-stu-id="bcfae-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="bcfae-174">La modification de la configuration d’un rôle hello</span><span class="sxs-lookup"><span data-stu-id="bcfae-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="bcfae-175">Vous pouvez mettre à jour de configuration hello de votre service cloud pendant son exécution dans Azure, sans mise hors service de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="bcfae-176">toochange les informations de configuration, vous pouvez télécharger un fichier de configuration, ou modifier le fichier de configuration hello dans placer et appliquez-le tooyour service en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bcfae-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="bcfae-177">Hello modifications suivantes peuvent être apportées configuration toohello d’un service :</span><span class="sxs-lookup"><span data-stu-id="bcfae-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="bcfae-178">**Modification des valeurs de paramètres de configuration hello**</span><span class="sxs-lookup"><span data-stu-id="bcfae-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="bcfae-179">Lorsqu’une configuration définissant les modifications, une instance de rôle choisissez tooapply hello changer pendant que l’instance de hello est en ligne, ou toorecycle hello l’instance normalement et appliquer hello lors de l’instance de hello est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="bcfae-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="bcfae-180">**La modification de topologie du service hello d’instances de rôle**</span><span class="sxs-lookup"><span data-stu-id="bcfae-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="bcfae-181">Les modifications de la topologie n’affectent pas les instances en cours d’exécution, sauf lorsqu’une instance est supprimée.</span><span class="sxs-lookup"><span data-stu-id="bcfae-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="bcfae-182">Toutes les instances restantes n’est généralement pas nécessaire toobe recyclé ; Toutefois, vous pouvez choisir toorecycle instances de rôle dans la modification de topologie tooa de réponse.</span><span class="sxs-lookup"><span data-stu-id="bcfae-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="bcfae-183">**Modification de l’empreinte numérique du certificat hello**</span><span class="sxs-lookup"><span data-stu-id="bcfae-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="bcfae-184">Vous ne pouvez mettre à jour un certificat que lorsqu’une instance de rôle est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="bcfae-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="bcfae-185">Si un certificat est ajouté, supprimé ou modifié pendant qu’une instance de rôle est en ligne, Azure prend le certificat de hello hello instance tooupdate hors connexion et la remettre en ligne une fois hello modification effectuée normalement.</span><span class="sxs-lookup"><span data-stu-id="bcfae-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="bcfae-186">Gestion des modifications de configuration à l’aide des événements de service Runtime</span><span class="sxs-lookup"><span data-stu-id="bcfae-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="bcfae-187">Hello [bibliothèque du Runtime Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) inclut hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) espace de noms, qui fournit des classes pour interagir avec hello environnement Azure à partir d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="bcfae-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="bcfae-188">Hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) classe définit hello suivant des événements qui sont déclenchés avant et après une modification de configuration :</span><span class="sxs-lookup"><span data-stu-id="bcfae-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="bcfae-189">**[Modification](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) d’un événement**</span><span class="sxs-lookup"><span data-stu-id="bcfae-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="bcfae-190">Cela se produit avant la modification de la configuration hello tooa appliqué les instance spécifiée d’un rôle, ce qui vous donne un tootake chance vers le bas les instances de rôle hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bcfae-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="bcfae-191">**[Événement](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) modifié**</span><span class="sxs-lookup"><span data-stu-id="bcfae-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="bcfae-192">Se produit après la modification de la configuration hello tooa appliqué les instance spécifiée d’un rôle.</span><span class="sxs-lookup"><span data-stu-id="bcfae-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="bcfae-193">Étant donné que les modifications de certificat toujours hors connexion des instances de hello d’un rôle, elles ne déclenchent pas les événements RoleEnvironment.Changing ou RoleEnvironment.Changed hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="bcfae-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="bcfae-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="bcfae-195">toodeploy une application comme un service cloud dans Azure, vous devez première application hello de package au format approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="bcfae-196">Vous pouvez utiliser hello **CSPack** outil de ligne de commande (installé avec hello [Azure SDK](https://azure.microsoft.com/downloads/)) fichier de package toocreate hello en tant qu’une autre tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="bcfae-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="bcfae-197">**CSPack** utilise hello contenu hello service définition du service de fichiers et configuration toodefine hello du contenu du fichier de package de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="bcfae-198">**CSPack** génère un fichier de package d’application (.cspkg) que vous pouvez télécharger tooAzure à l’aide de hello [portail Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="bcfae-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="bcfae-199">Par défaut, le package de hello est nommé `[ServiceDefinitionFileName].cspkg`, mais vous pouvez spécifier un nom différent à l’aide de hello `/out` option de **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="bcfae-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="bcfae-200">**CSPack** se situe dans</span><span class="sxs-lookup"><span data-stu-id="bcfae-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="bcfae-201">CSPack.exe (sous windows) est disponible en exécutant hello **invite de commandes Microsoft Azure** raccourci qui est installé avec le Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="bcfae-202">Réexécutez hello CSPack.exe par lui-même documentation toosee sur tous les commutateurs hello et les commandes.</span><span class="sxs-lookup"><span data-stu-id="bcfae-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="bcfae-203">Exécuter votre service cloud localement Bonjour **émulateur de calcul Azure Microsoft**, utilisez hello **/copyonly** option.</span><span class="sxs-lookup"><span data-stu-id="bcfae-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="bcfae-204">Cette option copie les fichiers binaires hello organisée en répertoires tooa application hello à partir duquel ils peuvent être exécutés dans l’émulateur de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="bcfae-205">Exemple commande toopackage un service cloud</span><span class="sxs-lookup"><span data-stu-id="bcfae-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="bcfae-206">Hello exemple suivant crée un package d’application qui contient des informations de hello pour un rôle web.</span><span class="sxs-lookup"><span data-stu-id="bcfae-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="bcfae-207">commande Hello spécifie toouse de fichier de définition de service hello, répertoire hello où les fichiers binaires peuvent être trouvés et hello nom hello du fichier de package.</span><span class="sxs-lookup"><span data-stu-id="bcfae-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="bcfae-208">Si l’application hello contient un rôle web et un rôle de travail, hello commande suivante est utilisée :</span><span class="sxs-lookup"><span data-stu-id="bcfae-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="bcfae-209">Où les variables de hello sont définies comme suit :</span><span class="sxs-lookup"><span data-stu-id="bcfae-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="bcfae-210">Variable</span><span class="sxs-lookup"><span data-stu-id="bcfae-210">Variable</span></span> | <span data-ttu-id="bcfae-211">Valeur</span><span class="sxs-lookup"><span data-stu-id="bcfae-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="bcfae-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="bcfae-212">\[DirectoryName\]</span></span> |<span data-ttu-id="bcfae-213">Bonjour sous-répertoire hello répertoire racine du projet qui contient le fichier de .csdef hello Hello projet Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="bcfae-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="bcfae-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="bcfae-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="bcfae-215">nom de Hello du fichier de définition de service hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-215">hello name of hello service definition file.</span></span> <span data-ttu-id="bcfae-216">Par défaut, ce fichier se nomme ServiceDefinition.csdef.</span><span class="sxs-lookup"><span data-stu-id="bcfae-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="bcfae-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="bcfae-217">\[OutputFileName\]</span></span> |<span data-ttu-id="bcfae-218">Hello nom hello généré pour le fichier de package.</span><span class="sxs-lookup"><span data-stu-id="bcfae-218">hello name for hello generated package file.</span></span> <span data-ttu-id="bcfae-219">En règle générale, il a la valeur nom toohello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="bcfae-220">Si aucun nom de fichier n’est spécifié, le package d’application hello est créé en tant que \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="bcfae-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="bcfae-221">\[RoleName\]</span><span class="sxs-lookup"><span data-stu-id="bcfae-221">\[RoleName\]</span></span> |<span data-ttu-id="bcfae-222">nom Hello du rôle hello tel que défini dans le fichier de définition de service hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="bcfae-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="bcfae-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="bcfae-224">emplacement Hello des fichiers binaires de hello pour le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="bcfae-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="bcfae-225">\[VirtualPath\]</span></span> |<span data-ttu-id="bcfae-226">répertoires physiques de Hello pour chaque chemin d’accès virtuel défini dans la section de Sites hello de définition du service hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="bcfae-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="bcfae-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="bcfae-228">Bonjour répertoires physiques du contenu hello pour chaque chemin d’accès virtuel défini dans le nœud de site hello de définition du service hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="bcfae-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="bcfae-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="bcfae-230">nom de Hello du fichier binaire de hello pour le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="bcfae-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bcfae-231">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bcfae-231">Next steps</span></span>
<span data-ttu-id="bcfae-232">Je crée un package de service cloud et je souhaite...</span><span class="sxs-lookup"><span data-stu-id="bcfae-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="bcfae-233">[Configurer un Bureau à distance pour une instance de service cloud][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="bcfae-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="bcfae-234">[Déployer un projet de service cloud][deploy]</span><span class="sxs-lookup"><span data-stu-id="bcfae-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="bcfae-235">J’utilise Visual Studio et souhaite...</span><span class="sxs-lookup"><span data-stu-id="bcfae-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="bcfae-236">[Créer un nouveau service de cloud computing][vs_create]</span><span class="sxs-lookup"><span data-stu-id="bcfae-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="bcfae-237">[Reconfigurer un service cloud existant][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="bcfae-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="bcfae-238">[Déployer un projet de service cloud][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="bcfae-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="bcfae-239">[Configurer un Bureau à distance pour une instance de service cloud][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="bcfae-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
