---
title: "Téléchargement du Kit de développement logiciel (SDK) Azure pour PHP"
description: "Découvrez comment télécharger et installer le Kit de développement logiciel (SDK) Azure pour PHP."
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
ms.openlocfilehash: fd3d28b133ef8e646f5c2f1c1127f654daa61b95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="484de-103">Téléchargement du Kit de développement logiciel (SDK) Azure pour PHP</span><span class="sxs-lookup"><span data-stu-id="484de-103">Download the Azure SDK for PHP</span></span>
## <a name="overview"></a><span data-ttu-id="484de-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="484de-104">Overview</span></span>
<span data-ttu-id="484de-105">Le Kit de développement logiciel (SDK) Azure pour PHP inclut des composants qui vous permettent de développer, de déployer et de gérer des applications PHP pour Azure.</span><span class="sxs-lookup"><span data-stu-id="484de-105">The Azure SDK for PHP includes components that allow you to develop, deploy, and manage PHP applications for Azure.</span></span> <span data-ttu-id="484de-106">Il inclut plus précisément les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="484de-106">Specifically, the Azure SDK for PHP includes the following:</span></span>

* <span data-ttu-id="484de-107">**Bibliothèques clientes PHP pour Azure**.</span><span class="sxs-lookup"><span data-stu-id="484de-107">**The PHP client libraries for Azure**.</span></span> <span data-ttu-id="484de-108">L'interface de ces bibliothèques de classes permet d'accéder aux fonctionnalités Azure, telles que les services de gestion des données et les services cloud.</span><span class="sxs-lookup"><span data-stu-id="484de-108">These class libraries provide an interface for accessing Azure features, such as data management services and cloud services.</span></span>  
* <span data-ttu-id="484de-109">**Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)**.</span><span class="sxs-lookup"><span data-stu-id="484de-109">**The Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)**.</span></span> <span data-ttu-id="484de-110">Cet ensemble de commandes permet de déployer et de gérer des services Azure, tels que Sites Web Azure et Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="484de-110">This is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="484de-111">L’interface de ligne de commande Azure fonctionne sur toutes les plateformes, dont Mac, Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="484de-111">The Azure CLI work on any platform, including Mac, Linux, and Windows.</span></span>
* <span data-ttu-id="484de-112">**Azure PowerShell (Windows uniquement)**.</span><span class="sxs-lookup"><span data-stu-id="484de-112">**Azure PowerShell (Windows Only)**.</span></span> <span data-ttu-id="484de-113">Cet ensemble de cmdlets PowerShell permet de déployer et de gérer les services Azure, tels que Cloud Services et Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="484de-113">This is a set of PowerShell cmdlets for deploying and managing Azure Services, such as Cloud Services and Virtual Machines.</span></span>
* <span data-ttu-id="484de-114">**Émulateurs Azure (Windows uniquement)**.</span><span class="sxs-lookup"><span data-stu-id="484de-114">**The Azure Emulators (Windows Only)**.</span></span> <span data-ttu-id="484de-115">Les émulateurs de stockage et de calcul sont des émulateurs locaux des services cloud et de gestion des données qui vous permettent de tester une application localement.</span><span class="sxs-lookup"><span data-stu-id="484de-115">The compute and storage emulators are local emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="484de-116">Les émulateurs Azure fonctionnent uniquement sur Windows.</span><span class="sxs-lookup"><span data-stu-id="484de-116">The Azure Emulators run on Windows only.</span></span>

<span data-ttu-id="484de-117">Les sections ci-dessous présentent les procédures de téléchargement et d'installation des composants décrits plus haut.</span><span class="sxs-lookup"><span data-stu-id="484de-117">The sections below describe how to download and install the components described above.</span></span>

<span data-ttu-id="484de-118">Les instructions de cette rubrique partent du principe que [PHP][install-php] est installé.</span><span class="sxs-lookup"><span data-stu-id="484de-118">The instructions in this topic assume that you have [PHP][install-php] installed.</span></span>

> [!NOTE]
> <span data-ttu-id="484de-119">Vous devez disposer de PHP 5.5 ou d’une version supérieure pour utiliser les bibliothèques clientes PHP pour Azure.</span><span class="sxs-lookup"><span data-stu-id="484de-119">You must have PHP 5.5 or higher to use the PHP client libraries for Azure.</span></span>
> 
> 

## <a name="php-client-libraries-for-azure"></a><span data-ttu-id="484de-120">Bibliothèques clientes PHP pour Azure</span><span class="sxs-lookup"><span data-stu-id="484de-120">PHP client libraries for Azure</span></span>
<span data-ttu-id="484de-121">Les bibliothèques clientes PHP pour Azure fournissent une interface permettant d'accéder aux fonctionnalités Azure, telles que les services cloud et de gestion des données à partir d'un système d'exploitation.</span><span class="sxs-lookup"><span data-stu-id="484de-121">The PHP Client Libraries for Azure provide an interface for accessing Azure features, such as data management services and cloud services, from any operating system.</span></span> <span data-ttu-id="484de-122">Ces bibliothèques peuvent être installées via le compositeur.</span><span class="sxs-lookup"><span data-stu-id="484de-122">These libraries can be installed via the Composer.</span></span>

<span data-ttu-id="484de-123">Pour plus d’informations sur l’utilisation des bibliothèques clientes PHP pour Azure, consultez les pages [Utilisation du service BLOB][blob-service], [Utilisation du service de Table][table-service] et [Utilisation du service de File d’attente][queue-service].</span><span class="sxs-lookup"><span data-stu-id="484de-123">For information about how to use the PHP Client Libraries for Azure, see [How to Use the Blob Service][blob-service], [How to Use the Table Service][table-service] and [How to Use the Queue Service][queue-service].</span></span>

### <a name="install-via-composer"></a><span data-ttu-id="484de-124">Installation via Composer</span><span class="sxs-lookup"><span data-stu-id="484de-124">Install via Composer</span></span>
1. <span data-ttu-id="484de-125">[Installez Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="484de-125">[Install Git][install-git].</span></span>

    > [AZURE.NOTE] <span data-ttu-id="484de-126">Sous Windows, vous devez aussi ajouter l’exécutable Git à votre variable d’environnement PATH.</span><span class="sxs-lookup"><span data-stu-id="484de-126">On Windows, you will also need to add the Git executable to your PATH environment variable.</span></span>

1. <span data-ttu-id="484de-127">Créez un fichier nommé **composer.json** à la racine de votre projet et ajoutez-y le code suivant :</span><span class="sxs-lookup"><span data-stu-id="484de-127">Create a file named **composer.json** in the root of your project and add the following code to it:</span></span>
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. <span data-ttu-id="484de-128">Téléchargez **[composer.phar][composer-phar]** à la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="484de-128">Download **[composer.phar][composer-phar]** in your project root.</span></span>
3. <span data-ttu-id="484de-129">Ouvrez une invite de commandes et exécutez cette commande à la racine du projet :</span><span class="sxs-lookup"><span data-stu-id="484de-129">Open a command prompt and execute this in your project root</span></span>
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a><span data-ttu-id="484de-130">Azure PowerShell et émulateurs Azure</span><span class="sxs-lookup"><span data-stu-id="484de-130">Azure PowerShell and Azure Emulators</span></span>
<span data-ttu-id="484de-131">Azure PowerShell est un ensemble de cmdlets PowerShell permettant de déployer et de gérer les services Azure, tels que Cloud Services et Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="484de-131">Azure PowerShell is a set of PowerShell cmdlets for deploying and managing Azure Services (such as Cloud Services and Virtual Machines).</span></span> <span data-ttu-id="484de-132">Les émulateurs de stockage Azure sont des émulateurs des services cloud et de gestion des données qui vous permettent de tester une application localement.</span><span class="sxs-lookup"><span data-stu-id="484de-132">The Azure Emulators are emulators of cloud services and data management services that allow you to test an application locally.</span></span> <span data-ttu-id="484de-133">Ces composants sont pris en charge uniquement par Windows.</span><span class="sxs-lookup"><span data-stu-id="484de-133">These components are supported Windows only.</span></span>

<span data-ttu-id="484de-134">Pour installer Azure PowerShell et les émulateurs Azure, il est recommandé d’utiliser [Microsoft Web Platform Installer][download-wpi].</span><span class="sxs-lookup"><span data-stu-id="484de-134">The recommended way to install Azure PowerShell and the Azure Emulators is to use the [Microsoft Web Platform Installer][download-wpi].</span></span> <span data-ttu-id="484de-135">Notez que vous pouvez également installer d'autres composants de développement, tels que PHP, SQL Server, les pilotes Microsoft pour SQL Server pour PHP et WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="484de-135">Note that you can also choose to install other development components, such as PHP, SQL Server, the Microsoft Drivers for SQL Server for PHP, and WebMatrix.</span></span>

<span data-ttu-id="484de-136">Pour plus d’informations sur l’utilisation d’Azure PowerShell, consultez la page [Utilisation d’Azure PowerShell][powershell-tools].</span><span class="sxs-lookup"><span data-stu-id="484de-136">For information about how to use Azure PowerShell, see [How to Use Azure PowerShell][powershell-tools].</span></span>

## <a name="azure-cli"></a><span data-ttu-id="484de-137">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="484de-137">Azure CLI</span></span>
<span data-ttu-id="484de-138">L’interface de ligne de commande Azure est un ensemble de commandes permettant de déployer et de gérer des services Azure, tels que Sites Web Azure et Azure Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="484de-138">The Azure CLI is a set of commands for deploying and managing Azure services, such as Azure Websites and Azure Virtual Machines.</span></span> <span data-ttu-id="484de-139">Pour plus d'informations sur l'installation de l’interface de ligne de commande Azure, consultez [Installer l’interface de ligne de commande Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="484de-139">For information about installing Azure CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="484de-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="484de-140">Next steps</span></span>
<span data-ttu-id="484de-141">Pour plus d’informations, consultez le [Centre pour développeurs PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="484de-141">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

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
