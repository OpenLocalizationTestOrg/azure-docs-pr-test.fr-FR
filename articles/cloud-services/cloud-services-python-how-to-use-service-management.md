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
# <a name="how-toouse-service-management-from-python"></a>Comment toouse de gestion des services à partir de Python
Ce guide vous explique comment tooprogrammatically effectuer des tâches courantes de gestion de service à partir de Python. Hello **ServiceManagementService** classe Bonjour [Azure SDK pour Python](https://github.com/Azure/azure-sdk-for-python) prend en charge l’accès par programme des toomuch hello liées à la gestion des fonctionnalités des services qui est disponible dans hello [Portail azure classic] [ management-portal] (tel que **création, de mise à jour et de suppression des services de cloud computing, les déploiements, les services de gestion de données et les machines virtuelles**). Cette fonctionnalité peut être utile dans les applications qui nécessitent un accès par programmation tooservice.

## <a name="WhatIs"></a>Présentation de la gestion des services
Hello API de gestion fournit toomuch l’accès par programme hello service de fonctionnalités de gestion disponibles via hello [portail Azure classic][management-portal]. Bonjour Azure SDK pour Python vous permet de toomanage vos services cloud et les comptes de stockage.

toouse hello API de gestion, vous devez trop[créer un compte Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"></a>Concepts
Bonjour Azure SDK pour Python encapsule hello [API de gestion des services Azure][svc-mgmt-rest-api], qui est une API REST. Toutes les opérations de l'API sont effectuées au moyen du protocole SSL et sont mutuellement authentifiées au moyen de certificats X.509 v3. service de gestion Hello être accessibles au sein d’un service en cours d’exécution dans Azure, ou directement via hello Internet à partir de n’importe quelle application qui peut envoyer une demande HTTPS et recevoir une réponse HTTPS.

## <a name="Installation"></a>Installation
Toutes les fonctionnalités de hello décrites dans cet article sont disponibles dans hello `azure-servicemanagement-legacy` package, que vous pouvez installer à l’aide de pip. Pour plus d’informations sur l’installation (par exemple, si vous êtes tooPython nouvelle), consultez l’article : [l’installation de Python et hello Azure SDK](../python-how-to-install.md)

## <a name="Connect"></a>Comment : connecter tooservice management
point de terminaison tooconnect toohello de gestion des services, vous avez besoin votre ID d’abonnement Azure et un certificat de gestion valide. Vous pouvez obtenir votre ID d’abonnement via hello [portail Azure classic][management-portal].

> [!NOTE]
> Il est désormais toouse possible les certificats créés avec OpenSSL lors de l’exécution sur Windows.  Ceci nécessite Python 2.7.4 ou version ultérieure. Nous vous recommandons d’utilisateurs toouse OpenSSL au lieu de .pfx, depuis la prise en charge de .pfx certificats seront probablement supprimés dans les futures hello.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Certificats de gestion sur Windows/Mac/Linux (OpenSSL)
Vous pouvez utiliser [OpenSSL](http://www.openssl.org/) toocreate votre certificat de gestion.  Vous avez besoin toocreate deux certificats, un pour le serveur de hello (un `.cer` fichier) et l’autre pour le client de hello (un `.pem` fichier). toocreate hello `.pem` de fichiers, exécutez :

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

toocreate hello `.cer` de certificat, exécutez :

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Pour plus d’informations sur les certificats Azure, consultez la page [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services-certs-create.md). Pour obtenir une description complète des paramètres de OpenSSL, consultez documentation hello [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

Après avoir créé ces fichiers, vous devez les hello tooupload `.cer` fichier tooAzure via l’action de « Télécharger » hello de l’onglet « Paramètres » de hello Hello [portail Azure classic][management-portal], et que vous devez noter toomake où vous avez enregistré hello `.pem` fichier.

Après avoir obtenu votre ID d’abonnement, créé un certificat et téléchargé hello `.cer` tooAzure de fichier, vous pouvez vous connecter aux toohello point de terminaison de gestion Azure en passant l’id d’abonnement hello et hello chemin d’accès toohello `.pem` trop de fichiers**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

Bonjour précédent exemple, `sms` est un **ServiceManagementService** objet. Hello **ServiceManagementService** classe est hello classe principale utilisée toomanage services Azure.

### <a name="management-certificates-on-windows-makecert"></a>Certificats de gestion sur Windows (MakeCert)
Vous pouvez créer un certificat de gestion auto-signé sur votre machine au moyen de `makecert.exe`.  Ouvrir un **invite de commandes Visual Studio** comme un **administrateur** et utiliser hello commande suivante, en remplaçant *AzureCertificate* avec le nom du certificat que vous souhaitez que hello toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

commande Hello crée hello `.cer` de fichiers et l’installe dans hello **personnel** magasin de certificats. Pour plus d’informations, consultez [Vue d’ensemble des certificats pour Azure Cloud Services](cloud-services-certs-create.md).

Une fois que vous avez créé le certificat de hello, vous devez les hello tooupload `.cer` fichier tooAzure via l’action de « Télécharger » hello de l’onglet « Paramètres » de hello Hello [portail Azure classic][management-portal].

Après avoir obtenu votre ID d’abonnement, créé un certificat et téléchargé hello `.cer` tooAzure de fichier, vous pouvez vous connecter aux toohello point de terminaison de gestion Azure en passant l’id d’abonnement hello et l’emplacement de hello du certificat de hello dans votre **Personnel** trop de magasin de certificats**ServiceManagementService** (là encore, remplacez *AzureCertificate* avec nom hello de votre certificat) :

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

Bonjour précédent exemple, `sms` est un **ServiceManagementService** objet. Hello **ServiceManagementService** classe est hello classe principale utilisée toomanage services Azure.

## <a name="ListAvailableLocations"></a>Affichage de la liste des emplacements disponibles
les emplacements de hello toolist qui sont disponibles pour l’hébergement des services, utilisez hello **liste\_emplacements** méthode :

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

Lorsque vous créez un service cloud ou le service de stockage, vous devez tooprovide un emplacement valide. Hello **liste\_emplacements** méthode retourne toujours une liste actualisée des emplacements de hello actuellement disponibles. À ce jour, les emplacements de hello disponibles sont :

* Europe de l'Ouest
* Europe du Nord
* Asie du Sud-Est
* Est de l'Asie
* Centre des États-Unis
* États-Unis - partie centrale septentrionale
* Centre-Sud des États-Unis
* Ouest des États-Unis
* Est des États-Unis
* Est du Japon
* Ouest du Japon
* Sud du Brésil
* Est de l’Australie
* Sud-est de l’Australie

## <a name="CreateCloudService"></a>Création d’un service cloud
Lorsque vous créez une application et l’exécuter dans Azure, ensemble de la configuration et le code de hello sont appelés Azure [service de cloud computing] [ cloud service] (appelé un *service hébergé* dans précédemment Versions d’Azure). Hello **créer\_hébergé\_service** méthode vous permet de toocreate un nouveau service hébergé en fournissant un nom de service hébergé (qui doit être unique dans Azure), une étiquette (toobase64 codé automatiquement), un Description et un emplacement.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

Vous pouvez répertorier tous les services hébergé de hello pour votre abonnement avec hello **liste\_hébergé\_services** méthode :

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Si vous souhaitez tooget d’informations sur un service hébergé particulier, vous pouvez le faire en passant hello hébergé service nom toohello **obtenir\_hébergé\_service\_propriétés** méthode :

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

Après avoir créé un service cloud, vous pouvez déployer votre service toohello code hello **créer\_déploiement** (méthode).

## <a name="DeleteCloudService"></a>Suppression d’un service cloud
Vous pouvez supprimer un service cloud en passant hello service nom toohello **supprimer\_hébergé\_service** méthode :

    sms.delete_hosted_service('myhostedservice')

Avant de pouvoir supprimer un service, tous les déploiements de service de hello doivent d’abord être supprimées. (consultez la section [Suppression d'un déploiement](#DeleteDeployment) pour plus d'informations).

## <a name="DeleteDeployment"></a>Suppression d’un déploiement
toodelete un déploiement, utilisez hello **supprimer\_déploiement** (méthode). Hello suivant montre comment toodelete un déploiement nommé `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"></a>Création d’un service de stockage
A [service de stockage](../storage/common/storage-create-storage-account.md) vous donne accès tooAzure [BLOB](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), et [les files d’attente](../storage/queues/storage-python-how-to-use-queue-storage.md). toocreate un service de stockage, vous devez un nom pour le service hello (entre 3 et 24 caractères minuscules et unique dans Azure), une description, une étiquette (haut too100 caractères, toobase64 codé automatiquement) et un emplacement. Bonjour à l’exemple suivant montre comment toocreate un stockage en spécifiant un emplacement de service.

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

Notez dans hello précédent exemple état hello du hello **créer\_stockage\_compte** opération peut être récupérée en passant le résultat de hello retourné par **créer\_stockage \_compte** toohello **obtenir\_opération\_état** (méthode).  

Vous pouvez répertorier vos comptes de stockage et leurs propriétés avec hello **liste\_stockage\_comptes** méthode :

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"></a>Suppression d’un service de stockage
Vous pouvez supprimer un service de stockage en passant toohello de nom de service de stockage hello **supprimer\_stockage\_compte** (méthode). Suppression d’un service de stockage supprime toutes les données stockées dans le service hello (objets BLOB, tables et files d’attente).

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"></a>Affichage de la liste des systèmes d’exploitation disponibles
les systèmes d’exploitation toolist hello qui sont disponibles pour l’hébergement des services, utilisez hello **liste\_d’exploitation\_systèmes** méthode :

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

Vous pouvez également utiliser hello **liste\_d’exploitation\_système\_familles** (méthode), qui regroupe des systèmes d’exploitation de hello par famille :

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"></a>Création d’une image du système d’exploitation
tooadd un référentiel d’images toohello image du système d’exploitation, utilisez hello **ajouter\_système d’exploitation\_image** méthode :

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

images de système d’exploitation toolist hello qui sont disponibles, utilisez hello **liste\_système d’exploitation\_images** (méthode). Cela inclut toutes les images de plateforme et les images utilisateur :

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

## <a name="DeleteVMImage"></a>Suppression d’une image du système d’exploitation
toodelete une image de l’utilisateur, utilisez hello **supprimer\_système d’exploitation\_image** méthode :

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"></a>Création d’une machine virtuelle
toocreate une machine virtuelle, vous devez tout d’abord toocreate un [service de cloud computing](#CreateCloudService).  Puis créez le déploiement des ordinateurs virtuels à l’aide de hello hello **créer\_virtuels\_ordinateur\_déploiement** méthode :

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

## <a name="DeleteVM"></a>Suppression d’une machine virtuelle
toodelete une machine virtuelle, vous supprimez tout d’abord déploiement hello à l’aide de hello **supprimer\_déploiement** méthode :

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

service de cloud computing Hello peut alors être supprimé à l’aide de hello **supprimer\_hébergé\_service** méthode :

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Création d’une machine virtuelle à partir d’une image de machine virtuelle capturée
toocapture une image de machine virtuelle, vous appelez d’abord hello **capture\_vm\_image** méthode :

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

Ensuite, toomake assurer que vous avez capturé correctement les images hello, utilisez hello **liste\_vm\_images** api et assurez-vous que votre image est affichée dans les résultats de hello :

    images = sms.list_vm_images()

toofinally créer hello un ordinateur virtuel avec les images capturées hello, utilisez hello **créer\_virtuels\_ordinateur\_déploiement** avant, mais cette fois passer dans hello vm_image_name à la place la méthode

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

toolearn savoir plus sur toocapture une Machine virtuelle Linux, voir [comment tooCapture une Machine virtuelle Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

toolearn savoir plus sur toocapture une Machine virtuelle Windows, voir [comment tooCapture une Machine virtuelle Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"></a>Étapes suivantes
Maintenant que vous avez appris les notions de base de hello de gestion des services, vous pouvez accéder à hello [documentation de référence d’API complète pour hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) et effectuer complexe tâches facilement toomanage votre application python.

Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).

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
