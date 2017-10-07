---
title: "hello d’aaaDownload Azure SDK pour PHP"
description: "Découvrez comment toodownload et installation Bonjour Azure SDK pour PHP."
documentationcenter: php
services: app-service\web
author: allclark
manager: douge
editor: 
ms.assetid: bac355ac-4c25-42f4-8273-c5112eafa8d4
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 06/01/2016
ms.author: allclark;yaqiyang
ms.openlocfilehash: 94f56fc4f91bb175c08b9f7a43cb221c827694a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="36afc-103">Télécharger hello Azure SDK pour PHP</span><span class="sxs-lookup"><span data-stu-id="36afc-103">Download hello Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="36afc-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="36afc-104">Overview</span></span>
<span data-ttu-id="36afc-105">Hello Azure SDK pour PHP inclut des composants qui vous permettent de toodevelop, déployer et gérer des applications PHP pour Azure.</span><span class="sxs-lookup"><span data-stu-id="36afc-105">hello Azure SDK for PHP includes components that allow you toodevelop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="36afc-106">Hello Azure SDK pour PHP comprend des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="36afc-106">Specifically, hello Azure SDK for PHP includes hello following:</span></span>

* <span data-ttu-id="36afc-107">**Hello des bibliothèques clientes PHP pour Azure**.</span><span class="sxs-lookup"><span data-stu-id="36afc-107">**hello PHP client libraries for Azure**.</span></span> <span data-ttu-id="36afc-108">L'interface de ces bibliothèques de classes permet d'accéder aux fonctionnalités Azure, telles que les services de gestion des données et les services cloud.</span><span class="sxs-lookup"><span data-stu-id="36afc-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="36afc-109">**Hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="36afc-109">**hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="36afc-110">Cet ensemble de commandes permet de déployer et de gérer des services Azure, tels que Sites Web Azure et Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="36afc-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="36afc-111">Hello travail CLI d’Azure sur n’importe quelle plateforme, notamment Windows, Linux et Mac.</span><span class="sxs-lookup"><span data-stu-id="36afc-111">hello Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="36afc-112">**Azure PowerShell (Windows uniquement)**.</span><span class="sxs-lookup"><span data-stu-id="36afc-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="36afc-113">Cet ensemble de cmdlets PowerShell permet de déployer et de gérer les services Azure, tels que Cloud Services et Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="36afc-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="36afc-114">**Hello émulateurs Azure (Windows uniquement)**.</span><span class="sxs-lookup"><span data-stu-id="36afc-114">**hello Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="36afc-115">émulateurs de calcul et de stockage Hello sont les émulateurs locaux de services de cloud computing et des services de gestion des données qui vous permettent de tootest une application localement.</span><span class="sxs-lookup"><span data-stu-id="36afc-115">hello compute and storage emulators are local emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="36afc-116">les émulateurs Azure Hello s’exécutant sur Windows uniquement.</span><span class="sxs-lookup"><span data-stu-id="36afc-116">hello Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="36afc-117">les sections de Hello ci-dessous décrivent comment toodownload et installez hello composants décrits ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="36afc-117">hello sections below describe how toodownload and install hello components described above.</span></span>

<span data-ttu-id="36afc-118">Hello instructions de cette rubrique supposent que vous avez [PHP] [ install-php] installé.</span><span class="sxs-lookup"><span data-stu-id="36afc-118">hello instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="36afc-119">Vous devez disposer de PHP 5.5 ou les bibliothèques clientes de supérieur toouse hello PHP pour Azure.</span><span class="sxs-lookup"><span data-stu-id="36afc-119">You must have PHP 5.5 or higher toouse hello PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="36afc-120">Bibliothèques clientes PHP pour Azure</span><span class="sxs-lookup"><span data-stu-id="36afc-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="36afc-121">les bibliothèques clientes Hello PHP pour Azure fournissent une interface pour l’accès aux fonctionnalités Azure, telles que les services de gestion de données et services, à partir de n’importe quel système d’exploitation cloud.</span><span class="sxs-lookup"><span data-stu-id="36afc-121">hello PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="36afc-122">Ces bibliothèques peuvent être installés via hello compositeur.</span><span class="sxs-lookup"><span data-stu-id="36afc-122">These libraries can be installed via hello Composer.</span></span>

<span data-ttu-id="36afc-123">Pour plus d’informations sur la façon dont toouse hello PHP les bibliothèques clientes pour Azure, consultez [comment tooUse hello Service Blob][blob-service], [comment tooUse hello Service de Table] [ table-service] et [comment tooUse hello Service file d’attente][queue-service].</span><span class="sxs-lookup"><span data-stu-id="36afc-123">For information about how toouse hello PHP Client Libraries for Azure, see [How tooUse hello Blob Service][blob-service], [How tooUse hello Table Service][table-service] and [How tooUse hello Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="36afc-124">Installation via Composer</span><span class="sxs-lookup"><span data-stu-id="36afc-124">Install via Composer</span></span>
1. <span data-ttu-id="36afc-125">[Installez Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="36afc-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="36afc-126">Sous Windows, vous devez la variable d’environnement PATH tooadd hello Git tooyour exécutable.</span><span class="sxs-lookup"><span data-stu-id="36afc-126">On Windows, you will also need tooadd hello Git executable tooyour PATH environment variable.</span></span>

1. <span data-ttu-id="36afc-127">Créez un fichier nommé **composer.json** hello racine de votre projet et ajouter hello suivant tooit de code :</span><span class="sxs-lookup"><span data-stu-id="36afc-127">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="36afc-128">Téléchargez **[composer.phar][composer-phar]** à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="36afc-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="36afc-129">Ouvrez une invite de commandes et exécutez cette commande à la racine du projet :</span><span class="sxs-lookup"><span data-stu-id="36afc-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="36afc-130">Azure PowerShell et émulateurs Azure</span><span class="sxs-lookup"><span data-stu-id="36afc-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="36afc-131">Azure PowerShell est un ensemble de cmdlets PowerShell permettant de déployer et de gérer les services Azure, tels que Cloud Services et Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="36afc-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="36afc-132">les émulateurs Azure Hello sont les émulateurs de services de cloud computing et des services de gestion des données qui vous permettent de tootest une application localement.</span><span class="sxs-lookup"><span data-stu-id="36afc-132">hello Azure Emulators are emulators of cloud services and data management services that allow you tootest an application locally.</span></span> <span data-ttu-id="36afc-133">Ces composants sont pris en charge uniquement par Windows.</span><span class="sxs-lookup"><span data-stu-id="36afc-133">These components are supported Windows only.</span></span>

<span data-ttu-id="36afc-134">Hello recommandée tooinstall Azure PowerShell et hello émulateurs Azure est toouse hello [Microsoft Web Platform Installer][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="36afc-134">hello recommended way tooinstall Azure PowerShell and hello Azure Emulators is toouse hello [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="36afc-135">Notez que vous pouvez également choisir tooinstall autres composants de développement, tels que PHP, SQL Server, hello Microsoft Drivers for SQL Server pour PHP et WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="36afc-135">Note that you can also choose tooinstall other development components, such as PHP, SQL Server, hello Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="36afc-136">Pour plus d’informations sur la façon toouse Azure PowerShell, consultez [comment tooUse Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="36afc-136">For information about how toouse Azure PowerShell, see [How tooUse Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="36afc-137">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="36afc-137">Azure CLI</span></span>
<span data-ttu-id="36afc-138">Hello CLI d’Azure est un ensemble de commandes pour déployer et gérer des services Azure, tels que les sites Web Azure et les Machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="36afc-138">hello Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="36afc-139">Pour plus d’informations sur l’installation du CLI d’Azure, consultez [installation Bonjour Azure CLI](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="36afc-139">For information about installing Azure CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="36afc-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36afc-140">Next steps</span></span>
<span data-ttu-id="36afc-141">Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="36afc-141">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[install-php]: http://www.php.net/manual/en/install.php
[composer-github]: https://github.com/composer/composer
[composer-phar]: http://getcomposer.org/composer.phar
[nodejs-org]: http://nodejs.org/
[install-node-linux]: https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
[download-wpi]: http://go.microsoft.com/fwlink/?LinkId=253447
[mac-installer]: http://go.microsoft.com/fwlink/?LinkId=252249
[blob-service]: http://go.microsoft.com/fwlink/?LinkId=252714
[table-service]: http://go.microsoft.com/fwlink/?LinkId=252715
[queue-service]: http://go.microsoft.com/fwlink/?LinkId=252716
[azure cli]: http://go.microsoft.com/fwlink/?LinkId=252717
[powershell-tools]: http://go.microsoft.com/fwlink/?LinkId=252718
[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
