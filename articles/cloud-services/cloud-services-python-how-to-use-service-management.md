---
title: "gestion des services hello aaaHow toouse API (Python) - guide des fonctionnalités"
description: "Découvrez comment tooprogrammatically effectuer des tâches courantes de gestion de service à partir de Python."
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
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="b8575-103">Comment toouse de gestion des services à partir de Python</span><span class="sxs-lookup"><span data-stu-id="b8575-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="b8575-104">Ce guide vous explique comment tooprogrammatically effectuer des tâches courantes de gestion de service à partir de Python.</span><span class="sxs-lookup"><span data-stu-id="b8575-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="b8575-105">Hello **ServiceManagementService** classe Bonjour [Azure SDK pour Python](https://github.com/Azure/azure-sdk-for-python) prend en charge l’accès par programme des toomuch hello liées à la gestion des fonctionnalités des services qui est disponible dans hello [Portail azure classic] [ management-portal] (tel que **création, de mise à jour et de suppression des services de cloud computing, les déploiements, les services de gestion de données et les machines virtuelles**).</span><span class="sxs-lookup"><span data-stu-id="b8575-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="b8575-106">Cette fonctionnalité peut être utile dans les applications qui nécessitent un accès par programmation tooservice.</span><span class="sxs-lookup"><span data-stu-id="b8575-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="b8575-107"><a name="WhatIs"></a>Présentation de la gestion des services</span><span class="sxs-lookup"><span data-stu-id="b8575-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="b8575-108">Hello API de gestion fournit toomuch l’accès par programme hello service de fonctionnalités de gestion disponibles via hello [portail Azure classic][management-portal].</span><span class="sxs-lookup"><span data-stu-id="b8575-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="b8575-109">Bonjour Azure SDK pour Python vous permet de toomanage vos services cloud et les comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="b8575-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="b8575-110">toouse hello API de gestion, vous devez trop[créer un compte Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8575-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="b8575-111"><a name="Concepts"></a>Concepts</span><span class="sxs-lookup"><span data-stu-id="b8575-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="b8575-112">Bonjour Azure SDK pour Python encapsule hello [API de gestion des services Azure][svc-mgmt-rest-api], qui est une API REST.</span><span class="sxs-lookup"><span data-stu-id="b8575-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="b8575-113">Toutes les opérations de l'API sont effectuées au moyen du protocole SSL et sont mutuellement authentifiées au moyen de certificats X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="b8575-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="b8575-114">service de gestion Hello être accessibles au sein d’un service en cours d’exécution dans Azure, ou directement via hello Internet à partir de n’importe quelle application qui peut envoyer une demande HTTPS et recevoir une réponse HTTPS.</span><span class="sxs-lookup"><span data-stu-id="b8575-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="b8575-115"><a name="Installation"></a>Installation</span><span class="sxs-lookup"><span data-stu-id="b8575-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="b8575-116">Toutes les fonctionnalités de hello décrites dans cet article sont disponibles dans hello `azure-servicemanagement-legacy` package, que vous pouvez installer à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="b8575-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="b8575-117">Pour plus d’informations sur l’installation (par exemple, si vous êtes tooPython nouvelle), consultez l’article : [l’installation de Python et hello Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="b8575-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="b8575-118"><a name="Connect"></a>Comment : connecter tooservice management</span><span class="sxs-lookup"><span data-stu-id="b8575-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="b8575-119">point de terminaison tooconnect toohello de gestion des services, vous avez besoin votre ID d’abonnement Azure et un certificat de gestion valide.</span><span class="sxs-lookup"><span data-stu-id="b8575-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="b8575-120">Vous pouvez obtenir votre ID d’abonnement via hello [portail Azure classic][management-portal].</span><span class="sxs-lookup"><span data-stu-id="b8575-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="b8575-121">Il est désormais toouse possible les certificats créés avec OpenSSL lors de l’exécution sur Windows.</span><span class="sxs-lookup"><span data-stu-id="b8575-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="b8575-122">Ceci nécessite Python 2.7.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b8575-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="b8575-123">Nous vous recommandons d’utilisateurs toouse OpenSSL au lieu de .pfx, depuis la prise en charge de .pfx certificats seront probablement supprimés dans les futures hello.</span><span class="sxs-lookup"><span data-stu-id="b8575-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="b8575-124">Certificats de gestion sur Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="b8575-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="b8575-125">Vous pouvez utiliser [OpenSSL](http://www.openssl.org/) toocreate votre certificat de gestion.</span><span class="sxs-lookup"><span data-stu-id="b8575-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="b8575-126">Vous avez besoin toocreate deux certificats, un pour le serveur de hello (un `.cer` fichier) et l’autre pour le client de hello (un `.pem` fichier).</span><span class="sxs-lookup"><span data-stu-id="b8575-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="b8575-127">toocreate hello `.pem` de fichiers, exécutez :</span><span class="sxs-lookup"><span data-stu-id="b8575-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="b8575-128">toocreate hello `.cer` de certificat, exécutez :</span><span class="sxs-lookup"><span data-stu-id="b8575-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="b8575-129">Pour plus d’informations sur les certificats Azure, consultez la page [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="b8575-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="b8575-130">Pour obtenir une description complète des paramètres de OpenSSL, consultez documentation hello [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="b8575-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="b8575-131">Après avoir créé ces fichiers, vous devez les hello tooupload `.cer` fichier tooAzure via l’action de « Télécharger » hello de l’onglet « Paramètres » de hello Hello [portail Azure classic][management-portal], et que vous devez noter toomake où vous avez enregistré hello `.pem` fichier.</span><span class="sxs-lookup"><span data-stu-id="b8575-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="b8575-132">Après avoir obtenu votre ID d’abonnement, créé un certificat et téléchargé hello `.cer` tooAzure de fichier, vous pouvez vous connecter aux toohello point de terminaison de gestion Azure en passant l’id d’abonnement hello et hello chemin d’accès toohello `.pem` trop de fichiers**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="b8575-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="b8575-133">Bonjour précédent exemple, `sms` est un **ServiceManagementService** objet.</span><span class="sxs-lookup"><span data-stu-id="b8575-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="b8575-134">Hello **ServiceManagementService** classe est hello classe principale utilisée toomanage services Azure.</span><span class="sxs-lookup"><span data-stu-id="b8575-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="b8575-135">Certificats de gestion sur Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="b8575-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="b8575-136">Vous pouvez créer un certificat de gestion auto-signé sur votre machine au moyen de `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="b8575-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="b8575-137">Ouvrir un **invite de commandes Visual Studio** comme un **administrateur** et utiliser hello commande suivante, en remplaçant *AzureCertificate* avec le nom du certificat que vous souhaitez que hello toouse.</span><span class="sxs-lookup"><span data-stu-id="b8575-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="b8575-138">commande Hello crée hello `.cer` de fichiers et l’installe dans hello **personnel** magasin de certificats.</span><span class="sxs-lookup"><span data-stu-id="b8575-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="b8575-139">Pour plus d’informations, consultez [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="b8575-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="b8575-140">Une fois que vous avez créé le certificat de hello, vous devez les hello tooupload `.cer` fichier tooAzure via l’action de « Télécharger » hello de l’onglet « Paramètres » de hello Hello [portail Azure classic][management-portal].</span><span class="sxs-lookup"><span data-stu-id="b8575-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="b8575-141">Après avoir obtenu votre ID d’abonnement, créé un certificat et téléchargé hello `.cer` tooAzure de fichier, vous pouvez vous connecter aux toohello point de terminaison de gestion Azure en passant l’id d’abonnement hello et l’emplacement de hello du certificat de hello dans votre **Personnel** trop de magasin de certificats**ServiceManagementService** (là encore, remplacez *AzureCertificate* avec nom hello de votre certificat) :</span><span class="sxs-lookup"><span data-stu-id="b8575-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="b8575-142">Bonjour précédent exemple, `sms` est un **ServiceManagementService** objet.</span><span class="sxs-lookup"><span data-stu-id="b8575-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="b8575-143">Hello **ServiceManagementService** classe est hello classe principale utilisée toomanage services Azure.</span><span class="sxs-lookup"><span data-stu-id="b8575-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="b8575-144"><a name="ListAvailableLocations"></a>Affichage de la liste des emplacements disponibles</span><span class="sxs-lookup"><span data-stu-id="b8575-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="b8575-145">les emplacements de hello toolist qui sont disponibles pour l’hébergement des services, utilisez hello **liste\_emplacements** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="b8575-146">Lorsque vous créez un service cloud ou le service de stockage, vous devez tooprovide un emplacement valide.</span><span class="sxs-lookup"><span data-stu-id="b8575-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="b8575-147">Hello **liste\_emplacements** méthode retourne toujours une liste actualisée des emplacements de hello actuellement disponibles.</span><span class="sxs-lookup"><span data-stu-id="b8575-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="b8575-148">À ce jour, les emplacements de hello disponibles sont :</span><span class="sxs-lookup"><span data-stu-id="b8575-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="b8575-149">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="b8575-149">West Europe</span></span>
* <span data-ttu-id="b8575-150">Europe du Nord</span><span class="sxs-lookup"><span data-stu-id="b8575-150">North Europe</span></span>
* <span data-ttu-id="b8575-151">Asie du Sud-Est</span><span class="sxs-lookup"><span data-stu-id="b8575-151">Southeast Asia</span></span>
* <span data-ttu-id="b8575-152">Est de l'Asie</span><span class="sxs-lookup"><span data-stu-id="b8575-152">East Asia</span></span>
* <span data-ttu-id="b8575-153">Centre des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b8575-153">Central US</span></span>
* <span data-ttu-id="b8575-154">États-Unis - partie centrale septentrionale</span><span class="sxs-lookup"><span data-stu-id="b8575-154">North Central US</span></span>
* <span data-ttu-id="b8575-155">Centre-Sud des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b8575-155">South Central US</span></span>
* <span data-ttu-id="b8575-156">Ouest des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b8575-156">West US</span></span>
* <span data-ttu-id="b8575-157">Est des États-Unis</span><span class="sxs-lookup"><span data-stu-id="b8575-157">East US</span></span>
* <span data-ttu-id="b8575-158">Est du Japon</span><span class="sxs-lookup"><span data-stu-id="b8575-158">Japan East</span></span>
* <span data-ttu-id="b8575-159">Ouest du Japon</span><span class="sxs-lookup"><span data-stu-id="b8575-159">Japan West</span></span>
* <span data-ttu-id="b8575-160">Sud du Brésil</span><span class="sxs-lookup"><span data-stu-id="b8575-160">Brazil South</span></span>
* <span data-ttu-id="b8575-161">Est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="b8575-161">Australia East</span></span>
* <span data-ttu-id="b8575-162">Sud-est de l’Australie</span><span class="sxs-lookup"><span data-stu-id="b8575-162">Australia Southeast</span></span>

## <span data-ttu-id="b8575-163"><a name="CreateCloudService"></a>Création d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="b8575-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="b8575-164">Lorsque vous créez une application et l’exécuter dans Azure, ensemble de la configuration et le code de hello sont appelés Azure [service de cloud computing] [ cloud service] (appelé un *service hébergé* dans précédemment Versions d’Azure).</span><span class="sxs-lookup"><span data-stu-id="b8575-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="b8575-165">Hello **créer\_hébergé\_service** méthode vous permet de toocreate un nouveau service hébergé en fournissant un nom de service hébergé (qui doit être unique dans Azure), une étiquette (toobase64 codé automatiquement), un Description et un emplacement.</span><span class="sxs-lookup"><span data-stu-id="b8575-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="b8575-166">Vous pouvez répertorier tous les services hébergé de hello pour votre abonnement avec hello **liste\_hébergé\_services** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="b8575-167">Si vous souhaitez tooget d’informations sur un service hébergé particulier, vous pouvez le faire en passant hello hébergé service nom toohello **obtenir\_hébergé\_service\_propriétés** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="b8575-168">Après avoir créé un service cloud, vous pouvez déployer votre service toohello code hello **créer\_déploiement** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b8575-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="b8575-169"><a name="DeleteCloudService"></a>Suppression d’un service cloud</span><span class="sxs-lookup"><span data-stu-id="b8575-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="b8575-170">Vous pouvez supprimer un service cloud en passant hello service nom toohello **supprimer\_hébergé\_service** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="b8575-171">Avant de pouvoir supprimer un service, tous les déploiements de service de hello doivent d’abord être supprimées.</span><span class="sxs-lookup"><span data-stu-id="b8575-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="b8575-172">(consultez la section [Suppression d'un déploiement](#DeleteDeployment) pour plus d'informations).</span><span class="sxs-lookup"><span data-stu-id="b8575-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="b8575-173"><a name="DeleteDeployment"></a>Suppression d’un déploiement</span><span class="sxs-lookup"><span data-stu-id="b8575-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="b8575-174">toodelete un déploiement, utilisez hello **supprimer\_déploiement** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b8575-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="b8575-175">Hello suivant montre comment toodelete un déploiement nommé `v1`.</span><span class="sxs-lookup"><span data-stu-id="b8575-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="b8575-176"><a name="CreateStorageService"></a>Création d’un service de stockage</span><span class="sxs-lookup"><span data-stu-id="b8575-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="b8575-177">A [service de stockage](../storage/common/storage-create-storage-account.md) vous donne accès tooAzure [BLOB](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), et [les files d’attente](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="b8575-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="b8575-178">toocreate un service de stockage, vous devez un nom pour le service hello (entre 3 et 24 caractères minuscules et unique dans Azure), une description, une étiquette (haut too100 caractères, toobase64 codé automatiquement) et un emplacement.</span><span class="sxs-lookup"><span data-stu-id="b8575-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="b8575-179">Bonjour à l’exemple suivant montre comment toocreate un stockage en spécifiant un emplacement de service.</span><span class="sxs-lookup"><span data-stu-id="b8575-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

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

<span data-ttu-id="b8575-180">Notez dans hello précédent exemple état hello du hello **créer\_stockage\_compte** opération peut être récupérée en passant le résultat de hello retourné par **créer\_stockage \_compte** toohello **obtenir\_opération\_état** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b8575-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="b8575-181">Vous pouvez répertorier vos comptes de stockage et leurs propriétés avec hello **liste\_stockage\_comptes** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="b8575-182"><a name="DeleteStorageService"></a>Suppression d’un service de stockage</span><span class="sxs-lookup"><span data-stu-id="b8575-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="b8575-183">Vous pouvez supprimer un service de stockage en passant toohello de nom de service de stockage hello **supprimer\_stockage\_compte** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b8575-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="b8575-184">Suppression d’un service de stockage supprime toutes les données stockées dans le service hello (objets BLOB, tables et files d’attente).</span><span class="sxs-lookup"><span data-stu-id="b8575-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="b8575-185"><a name="ListOperatingSystems"></a>Affichage de la liste des systèmes d’exploitation disponibles</span><span class="sxs-lookup"><span data-stu-id="b8575-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="b8575-186">les systèmes d’exploitation toolist hello qui sont disponibles pour l’hébergement des services, utilisez hello **liste\_d’exploitation\_systèmes** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="b8575-187">Vous pouvez également utiliser hello **liste\_d’exploitation\_système\_familles** (méthode), qui regroupe des systèmes d’exploitation de hello par famille :</span><span class="sxs-lookup"><span data-stu-id="b8575-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="b8575-188"><a name="CreateVMImage"></a>Création d’une image du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="b8575-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="b8575-189">tooadd un référentiel d’images toohello image du système d’exploitation, utilisez hello **ajouter\_système d’exploitation\_image** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

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

<span data-ttu-id="b8575-190">images de système d’exploitation toolist hello qui sont disponibles, utilisez hello **liste\_système d’exploitation\_images** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b8575-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="b8575-191">Cela inclut toutes les images de plateforme et les images utilisateur :</span><span class="sxs-lookup"><span data-stu-id="b8575-191">It includes all platform images and user images:</span></span>

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

## <span data-ttu-id="b8575-192"><a name="DeleteVMImage"></a>Suppression d’une image du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="b8575-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="b8575-193">toodelete une image de l’utilisateur, utilisez hello **supprimer\_système d’exploitation\_image** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="b8575-194"><a name="CreateVM"></a>Création d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b8575-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="b8575-195">toocreate une machine virtuelle, vous devez tout d’abord toocreate un [service de cloud computing](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="b8575-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="b8575-196">Puis créez le déploiement des ordinateurs virtuels à l’aide de hello hello **créer\_virtuels\_ordinateur\_déploiement** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
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

## <span data-ttu-id="b8575-197"><a name="DeleteVM"></a>Suppression d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b8575-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="b8575-198">toodelete une machine virtuelle, vous supprimez tout d’abord déploiement hello à l’aide de hello **supprimer\_déploiement** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="b8575-199">service de cloud computing Hello peut alors être supprimé à l’aide de hello **supprimer\_hébergé\_service** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="b8575-200">Création d’une machine virtuelle à partir d’une image de machine virtuelle capturée</span><span class="sxs-lookup"><span data-stu-id="b8575-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="b8575-201">toocapture une image de machine virtuelle, vous appelez d’abord hello **capture\_vm\_image** méthode :</span><span class="sxs-lookup"><span data-stu-id="b8575-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
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

<span data-ttu-id="b8575-202">Ensuite, toomake assurer que vous avez capturé correctement les images hello, utilisez hello **liste\_vm\_images** api et assurez-vous que votre image est affichée dans les résultats de hello :</span><span class="sxs-lookup"><span data-stu-id="b8575-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="b8575-203">toofinally créer hello un ordinateur virtuel avec les images capturées hello, utilisez hello **créer\_virtuels\_ordinateur\_déploiement** avant, mais cette fois passer dans hello vm_image_name à la place la méthode</span><span class="sxs-lookup"><span data-stu-id="b8575-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
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

<span data-ttu-id="b8575-204">toolearn savoir plus sur toocapture une Machine virtuelle Linux, voir [comment tooCapture une Machine virtuelle Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b8575-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="b8575-205">toolearn savoir plus sur toocapture une Machine virtuelle Windows, voir [comment tooCapture une Machine virtuelle Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b8575-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="b8575-206"><a name="What's Next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8575-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="b8575-207">Maintenant que vous avez appris les notions de base de hello de gestion des services, vous pouvez accéder à hello [documentation de référence d’API complète pour hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) et effectuer complexe tâches facilement toomanage votre application python.</span><span class="sxs-lookup"><span data-stu-id="b8575-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="b8575-208">Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="b8575-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
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
