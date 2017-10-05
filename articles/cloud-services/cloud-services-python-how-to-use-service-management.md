---
title: "Utilisation de l'API de gestion des services (Python) - Guide des fonctionnalités"
description: "Découvrez comment effectuer des tâches courantes de gestion des services par programme à partir de Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: 13249ba9a4b317a3154776b411ce0bb1f316b3bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="722b3-103">Utilisation de la gestion des services à partir de Python</span><span class="sxs-lookup"><span data-stu-id="722b3-103">How to use Service Management from Python</span></span>
<span data-ttu-id="722b3-104">Ce guide vous explique comment effectuer des tâches courantes de gestion des services par programme à partir de Python.</span><span class="sxs-lookup"><span data-stu-id="722b3-104">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="722b3-105">La classe **ServiceManagementService** du [Kit de développement logiciel (SDK) Azure pour Python](https://github.com/Azure/azure-sdk-for-python) prend en charge l’accès par programme à une grande partie des fonctionnalités liées à la gestion des services disponibles dans le [portail Azure Classic][management-portal] (telles que la **création, la mise à jour et la suppression de services cloud, les déploiements, les services de gestion des données et les machines virtuelles**).</span><span class="sxs-lookup"><span data-stu-id="722b3-105">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="722b3-106">Ces fonctionnalités peuvent être utiles pour la création d'applications nécessitant un accès par programme à la gestion des services.</span><span class="sxs-lookup"><span data-stu-id="722b3-106">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="722b3-107"><a name="WhatIs"> </a>Présentation de la gestion des services</span><span class="sxs-lookup"><span data-stu-id="722b3-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="722b3-108">L’API de gestion des services fournit un accès par programme aux fonctionnalités de gestion des services disponibles par le biais du [portail Azure Classic][management-portal].</span><span class="sxs-lookup"><span data-stu-id="722b3-108">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="722b3-109">Le Kit de développement logiciel (SDK) Azure pour Python vous permet de gérer vos services cloud et vos comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="722b3-109">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="722b3-110">Pour utiliser l'API de gestion des services, vous devez [créer un compte Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="722b3-110">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="722b3-111"><a name="Concepts"> </a>Concepts</span><span class="sxs-lookup"><span data-stu-id="722b3-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="722b3-112">Le Kit de développement logiciel (SDK) Azure pour Python inclut l’[API de gestion des services Azure][svc-mgmt-rest-api], qui est une API REST.</span><span class="sxs-lookup"><span data-stu-id="722b3-112">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="722b3-113">Toutes les opérations de l'API sont effectuées au moyen du protocole SSL et sont mutuellement authentifiées au moyen de certificats X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="722b3-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="722b3-114">La gestion des services est accessible à partir d'un service s'exécutant dans Azure, ou directement sur Internet à partir de toute application pouvant envoyer une demande HTTPS et recevoir une réponse HTTPS.</span><span class="sxs-lookup"><span data-stu-id="722b3-114">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="722b3-115"><a name="Installation"> </a>Installation</span><span class="sxs-lookup"><span data-stu-id="722b3-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="722b3-116">Toutes les fonctionnalités décrites dans cet article sont disponibles dans le package `azure-servicemanagement-legacy` , que vous pouvez installer à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="722b3-116">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="722b3-117">Pour plus d’informations sur l’installation (par exemple si vous ne connaissez pas Python), consultez cet article : [Installation de Python et du SDK Azure](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="722b3-117">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="722b3-118"><a name="Connect"> </a>Connexion à la gestion des services</span><span class="sxs-lookup"><span data-stu-id="722b3-118"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="722b3-119">Pour vous connecter au point de terminaison de la gestion de services, vous avez besoin de votre ID d’abonnement Azure et d’un certificat de gestion valide.</span><span class="sxs-lookup"><span data-stu-id="722b3-119">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="722b3-120">Vous pouvez obtenir votre ID d’abonnement dans le [portail Azure Classic][management-portal].</span><span class="sxs-lookup"><span data-stu-id="722b3-120">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="722b3-121">Il est désormais possible d’utiliser des certificats créés avec OpenSSL sous Windows.</span><span class="sxs-lookup"><span data-stu-id="722b3-121">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="722b3-122">Ceci nécessite Python 2.7.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="722b3-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="722b3-123">Nous recommandons aux utilisateurs d’utiliser OpenSSL au lieu de .pfx, car la prise en charge des certificats .pfx risque de disparaître à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="722b3-123">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="722b3-124">Certificats de gestion sur Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="722b3-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="722b3-125">Vous pouvez utiliser [OpenSSL](http://www.openssl.org/) pour créer votre certificat de gestion.</span><span class="sxs-lookup"><span data-stu-id="722b3-125">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="722b3-126">En fait, vous devez créer deux certificats, un pour le serveur (un fichier `.cer`) et un pour le client (un fichier `.pem`).</span><span class="sxs-lookup"><span data-stu-id="722b3-126">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="722b3-127">Pour créer le fichier `.pem` , exécutez :</span><span class="sxs-lookup"><span data-stu-id="722b3-127">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="722b3-128">Pour créer le certificat `.cer` , exécutez :</span><span class="sxs-lookup"><span data-stu-id="722b3-128">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="722b3-129">Pour plus d’informations sur les certificats Azure, consultez la page [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="722b3-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="722b3-130">Pour une description complète des paramètres OpenSSL, consultez la documentation disponible sur [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="722b3-130">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="722b3-131">Une fois ces fichiers créés, vous devez télécharger le fichier `.cer` sur Azure au moyen de l’action Télécharger de l’onglet Paramètres dans le [portail Azure Classic][management-portal]. Pensez également à noter l’endroit où vous avez enregistré le fichier `.pem`.</span><span class="sxs-lookup"><span data-stu-id="722b3-131">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="722b3-132">Une fois que vous avez obtenu votre ID d’abonnement, créé un certificat et téléchargé le fichier `.cer` sur Azure, vous pouvez vous connecter au point de terminaison de gestion Azure en transmettant l’ID d’abonnement et le chemin du fichier `.pem` vers **ServiceManagementService** :</span><span class="sxs-lookup"><span data-stu-id="722b3-132">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="722b3-133">Dans l’exemple ci-dessus, `sms` est un objet **ServiceManagementService** .</span><span class="sxs-lookup"><span data-stu-id="722b3-133">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="722b3-134">La classe **ServiceManagementService** est la classe principale utilisée pour gérer les services Azure.</span><span class="sxs-lookup"><span data-stu-id="722b3-134">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="722b3-135">Certificats de gestion sur Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="722b3-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="722b3-136">Vous pouvez créer un certificat de gestion auto-signé sur votre machine au moyen de `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="722b3-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="722b3-137">Ouvrez une **invite de commande Visual Studio** en tant **qu’administrateur** et utilisez la commande suivante, en remplaçant *AzureCertificate* par le nom du certificat que vous voulez utiliser.</span><span class="sxs-lookup"><span data-stu-id="722b3-137">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="722b3-138">La commande crée le fichier `.cer` et l’installe dans le magasin de certificats **Personnel** .</span><span class="sxs-lookup"><span data-stu-id="722b3-138">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="722b3-139">Pour plus d’informations, consultez [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="722b3-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="722b3-140">Une fois le certificat créé, vous devez télécharger le fichier `.cer` sur Azure par le biais de l’action Télécharger de l’onglet Paramètres dans le [portail Azure Classic][management-portal].</span><span class="sxs-lookup"><span data-stu-id="722b3-140">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="722b3-141">Une fois que vous avez obtenu votre ID d’abonnement, créé un certificat et téléchargé le fichier `.cer` sur Azure, vous pouvez vous connecter au point de terminaison de gestion Azure en transmettant l’ID d’abonnement et l’emplacement du certificat dans votre magasin de certificats **Personnel** vers **ServiceManagementService** (à nouveau, remplacez *AzureCertificate* par le nom de votre certificat) :</span><span class="sxs-lookup"><span data-stu-id="722b3-141">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="722b3-142">Dans l’exemple ci-dessus, `sms` est un objet **ServiceManagementService** .</span><span class="sxs-lookup"><span data-stu-id="722b3-142">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="722b3-143">La classe **ServiceManagementService** est la classe principale utilisée pour gérer les services Azure.</span><span class="sxs-lookup"><span data-stu-id="722b3-143">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="722b3-144"><a name="ListAvailableLocations"> </a>Affichage de la liste des emplacements disponibles</span><span class="sxs-lookup"><span data-stu-id="722b3-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="722b3-145">Pour afficher la liste des emplacements disponibles pour les services d’hébergement, utilisez la méthode **list\_locations** :</span><span class="sxs-lookup"><span data-stu-id="722b3-145">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="722b3-146">Quand vous créez un service cloud ou un service de stockage, vous devez fournir un emplacement valide.</span><span class="sxs-lookup"><span data-stu-id="722b3-146">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="722b3-147">La méthode **list\_locations** renvoie toujours une liste à jour des emplacements disponibles actuellement.</span><span class="sxs-lookup"><span data-stu-id="722b3-147">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="722b3-148">Lors de la rédaction de cet article, les emplacements disponibles étaient les suivants :</span><span class="sxs-lookup"><span data-stu-id="722b3-148">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="722b3-149">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="722b3-149">West Europe</span></span>
* <span data-ttu-id="722b3-150">Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="722b3-150">North Europe</span></span>
* <span data-ttu-id="722b3-151">Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="722b3-151">Southeast Asia</span></span>
* <span data-ttu-id="722b3-152">Est de l'Asie</span><span class="sxs-lookup"><span data-stu-id="722b3-152">East Asia</span></span>
* <span data-ttu-id="722b3-153">Centre des États-Unis</span><span class="sxs-lookup"><span data-stu-id="722b3-153">Central US</span></span>
* <span data-ttu-id="722b3-154">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="722b3-154">North Central US</span></span>
* <span data-ttu-id="722b3-155">Centre-Sud des États-Unis</span><span class="sxs-lookup"><span data-stu-id="722b3-155">South Central US</span></span>
* <span data-ttu-id="722b3-156">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="722b3-156">West US</span></span>
* <span data-ttu-id="722b3-157">Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="722b3-157">East US</span></span>
* <span data-ttu-id="722b3-158">Est du Japon</span><span class="sxs-lookup"><span data-stu-id="722b3-158">Japan East</span></span>
* <span data-ttu-id="722b3-159">Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="722b3-159">Japan West</span></span>
* <span data-ttu-id="722b3-160">Sud du Brésil</span><span class="sxs-lookup"><span data-stu-id="722b3-160">Brazil South</span></span>
* <span data-ttu-id="722b3-161">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="722b3-161">Australia East</span></span>
* <span data-ttu-id="722b3-162">Sud-est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="722b3-162">Australia Southeast</span></span>

## <span data-ttu-id="722b3-163"><a name="CreateCloudService"> </a>Création d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="722b3-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="722b3-164">Lorsque vous créez une application et que vous l’exécutez dans Azure, l’ensemble constitué du code et de la configuration est appelé [service cloud][cloud service] Azure (également connu sous le nom de *service hébergé* dans les versions antérieures d’Azure).</span><span class="sxs-lookup"><span data-stu-id="722b3-164">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="722b3-165">La méthode **create\_hosted\_service** vous permet de créer un service hébergé en fournissant un nom de service hébergé (qui doit être unique dans Azure), une étiquette (automatiquement codée en base64), une description et un emplacement.</span><span class="sxs-lookup"><span data-stu-id="722b3-165">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="722b3-166">Vous pouvez afficher la liste de tous les services hébergés pour votre abonnement au moyen de la méthode **list\_hosted\_services** :</span><span class="sxs-lookup"><span data-stu-id="722b3-166">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="722b3-167">Si vous souhaitez obtenir des informations sur un service hébergé particulier, transmettez son nom à la méthode **get\_hosted\_service\_properties** :</span><span class="sxs-lookup"><span data-stu-id="722b3-167">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="722b3-168">Une fois que vous avez créé un service cloud, vous pouvez déployer votre code sur le service avec la méthode **create\_deployment**.</span><span class="sxs-lookup"><span data-stu-id="722b3-168">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="722b3-169"><a name="DeleteCloudService"> </a>Suppression d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="722b3-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="722b3-170">Vous pouvez supprimer un service cloud en transmettant son nom à la méthode **delete\_hosted\_service** :</span><span class="sxs-lookup"><span data-stu-id="722b3-170">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="722b3-171">Avant de supprimer un service, vous devez supprimer tous les déploiements associés.</span><span class="sxs-lookup"><span data-stu-id="722b3-171">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="722b3-172">(consultez la section [Suppression d'un déploiement](#DeleteDeployment) pour plus d'informations).</span><span class="sxs-lookup"><span data-stu-id="722b3-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="722b3-173"><a name="DeleteDeployment"> </a>Suppression d’un déploiement</span><span class="sxs-lookup"><span data-stu-id="722b3-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="722b3-174">Pour supprimer un déploiement, utilisez la méthode **delete\_deployment**.</span><span class="sxs-lookup"><span data-stu-id="722b3-174">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="722b3-175">L’exemple suivant indique comment supprimer un déploiement nommé `v1`.</span><span class="sxs-lookup"><span data-stu-id="722b3-175">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="722b3-176"><a name="CreateStorageService"> </a>Création d’un service de stockage</span><span class="sxs-lookup"><span data-stu-id="722b3-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="722b3-177">Un [service de stockage](../storage/common/storage-create-storage-account.md) vous donne accès aux [objets blob](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tables](../cosmos-db/table-storage-how-to-use-python.md) et [files d’attente](../storage/queues/storage-python-how-to-use-queue-storage.md) Azure.</span><span class="sxs-lookup"><span data-stu-id="722b3-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="722b3-178">Pour créer un service de stockage, vous avez besoin d’un nom pour le service (comprenant entre 3 et 24 lettres minuscules et unique au sein d’Azure), une description, une étiquette (jusqu’à 100 caractères, automatiquement codés en base64) et un emplacement.</span><span class="sxs-lookup"><span data-stu-id="722b3-178">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="722b3-179">L'exemple suivant indique comment créer un service de stockage en spécifiant un emplacement.</span><span class="sxs-lookup"><span data-stu-id="722b3-179">The following example shows how to create a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="722b3-180">Dans l’exemple ci-dessus, notez que l’état de l’opération **create\_storage\_account** peut être extrait en transmettant le résultat renvoyé par **create\_storage\_account** à la méthode **get\_operation\_status**.</span><span class="sxs-lookup"><span data-stu-id="722b3-180">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="722b3-181">Vous pouvez afficher la liste de vos comptes de stockage et leurs propriétés avec la méthode **list\_storage\_accounts** :</span><span class="sxs-lookup"><span data-stu-id="722b3-181">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="722b3-182"><a name="DeleteStorageService"> </a>Suppression d’un service de stockage</span><span class="sxs-lookup"><span data-stu-id="722b3-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="722b3-183">Vous pouvez supprimer un service de stockage en transmettant son nom à la méthode **delete\_storage\_account**.</span><span class="sxs-lookup"><span data-stu-id="722b3-183">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="722b3-184">La suppression d’un service de stockage supprime toutes les données qui y sont stockées (objets blob, tables et files d’attente).</span><span class="sxs-lookup"><span data-stu-id="722b3-184">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="722b3-185"><a name="ListOperatingSystems"> </a>Affichage de la liste des systèmes d’exploitation disponibles</span><span class="sxs-lookup"><span data-stu-id="722b3-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="722b3-186">Pour afficher la liste des systèmes d’exploitation disponibles pour les services d’hébergement, utilisez la méthode **list\_operating\_systems** :</span><span class="sxs-lookup"><span data-stu-id="722b3-186">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="722b3-187">Vous pouvez également utiliser la méthode **list\_operating\_system\_families**, qui regroupe les systèmes d’exploitation par famille :</span><span class="sxs-lookup"><span data-stu-id="722b3-187">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="722b3-188"><a name="CreateVMImage"> </a>Création d’une image du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="722b3-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="722b3-189">Pour ajouter une image du système d’exploitation au référentiel d’images, utilisez la méthode **add\_os\_image** :</span><span class="sxs-lookup"><span data-stu-id="722b3-189">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="722b3-190">Pour afficher la liste des images de systèmes d’exploitation qui sont disponibles, utilisez la méthode **list\_os\_images**.</span><span class="sxs-lookup"><span data-stu-id="722b3-190">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="722b3-191">Cela inclut toutes les images de plateforme et les images utilisateur :</span><span class="sxs-lookup"><span data-stu-id="722b3-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="722b3-192"><a name="DeleteVMImage"> </a>Suppression d’une image du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="722b3-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="722b3-193">Pour supprimer une image utilisateur, utilisez la méthode **delete\_os\_image** :</span><span class="sxs-lookup"><span data-stu-id="722b3-193">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="722b3-194"><a name="CreateVM"> </a>Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="722b3-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="722b3-195">Pour créer une machine virtuelle, vous devez d'abord créer un [service cloud](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="722b3-195">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="722b3-196">Ensuite, créez le déploiement de machine virtuelle en utilisant la méthode **create\_virtual\_machine\_deployment** :</span><span class="sxs-lookup"><span data-stu-id="722b3-196">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="722b3-197"><a name="DeleteVM"> </a>Suppression d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="722b3-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="722b3-198">Pour supprimer une machine virtuelle, vous devez d’abord supprimer le déploiement au moyen de la méthode **delete\_deployment** :</span><span class="sxs-lookup"><span data-stu-id="722b3-198">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="722b3-199">Le service cloud peut ensuite être supprimé au moyen de la méthode **delete\_hosted\_service** :</span><span class="sxs-lookup"><span data-stu-id="722b3-199">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="722b3-200">Création d’une machine virtuelle à partir d’une image de machine virtuelle capturée</span><span class="sxs-lookup"><span data-stu-id="722b3-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="722b3-201">Pour capturer une image de machine virtuelle, appelez d’abord la méthode **capture\_vm\_image** :</span><span class="sxs-lookup"><span data-stu-id="722b3-201">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="722b3-202">Ensuite, pour être sûr d’avoir correctement capturé l’image, utilisez l’API **list\_vm\_images** et vérifiez que votre image s’affiche dans les résultats :</span><span class="sxs-lookup"><span data-stu-id="722b3-202">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="722b3-203">Enfin, pour créer la machine virtuelle à l’aide de l’image capturée, utilisez la méthode **create\_virtual\_machine\_deployment** comme avant, mais cette fois en passant la méthode vm_image_name à la place.</span><span class="sxs-lookup"><span data-stu-id="722b3-203">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="722b3-204">Pour en savoir plus sur la capture d’une machine virtuelle Linux, consultez la page [Capture d’une machine virtuelle Linux](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="722b3-204">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="722b3-205">Pour en savoir plus sur la capture d’une machine virtuelle Windows, consultez la page [Capture d’une machine virtuelle Windows](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="722b3-205">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="722b3-206"><a name="What's Next"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="722b3-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="722b3-207">Vous connaissez désormais les principes de base de la gestion des services. Vous pouvez maintenant accéder à la [documentation complète de référence sur l’API du kit SDK Azure pour Python](http://azure-sdk-for-python.readthedocs.org/) et effectuer facilement des tâches complexes pour gérer votre application python.</span><span class="sxs-lookup"><span data-stu-id="722b3-207">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="722b3-208">Pour plus d’informations, consultez le [Centre pour développeurs Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="722b3-208">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
