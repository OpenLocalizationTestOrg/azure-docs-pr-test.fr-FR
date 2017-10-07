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
# <a name="download-hello-azure-sdk-for-php"></a>Télécharger hello Azure SDK pour PHP
## <a name="overview"></a>Vue d'ensemble
Hello Azure SDK pour PHP inclut des composants qui vous permettent de toodevelop, déployer et gérer des applications PHP pour Azure. Hello Azure SDK pour PHP comprend des éléments suivants de hello :

* **Hello des bibliothèques clientes PHP pour Azure**. L'interface de ces bibliothèques de classes permet d'accéder aux fonctionnalités Azure, telles que les services de gestion des données et les services cloud.  
* **Hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)**. Cet ensemble de commandes permet de déployer et de gérer des services Azure, tels que Sites Web Azure et Azure Virtual Machines. Hello travail CLI d’Azure sur n’importe quelle plateforme, notamment Windows, Linux et Mac.
* **Azure PowerShell (Windows uniquement)**. Cet ensemble de cmdlets PowerShell permet de déployer et de gérer les services Azure, tels que Cloud Services et Virtual Machines.
* **Hello émulateurs Azure (Windows uniquement)**. émulateurs de calcul et de stockage Hello sont les émulateurs locaux de services de cloud computing et des services de gestion des données qui vous permettent de tootest une application localement. les émulateurs Azure Hello s’exécutant sur Windows uniquement.

les sections de Hello ci-dessous décrivent comment toodownload et installez hello composants décrits ci-dessus.

Hello instructions de cette rubrique supposent que vous avez [PHP] [ install-php] installé.

> [!NOTE]
> Vous devez disposer de PHP 5.5 ou les bibliothèques clientes de supérieur toouse hello PHP pour Azure.
> 
> 

## <a name="php-client-libraries-for-azure"></a>Bibliothèques clientes PHP pour Azure
les bibliothèques clientes Hello PHP pour Azure fournissent une interface pour l’accès aux fonctionnalités Azure, telles que les services de gestion de données et services, à partir de n’importe quel système d’exploitation cloud. Ces bibliothèques peuvent être installés via hello compositeur.

Pour plus d’informations sur la façon dont toouse hello PHP les bibliothèques clientes pour Azure, consultez [comment tooUse hello Service Blob][blob-service], [comment tooUse hello Service de Table] [ table-service] et [comment tooUse hello Service file d’attente][queue-service].

### <a name="install-via-composer"></a>Installation via Composer
1. [Installez Git][install-git].

    > [AZURE.NOTE] Sous Windows, vous devez la variable d’environnement PATH tooadd hello Git tooyour exécutable.

1. Créez un fichier nommé **composer.json** hello racine de votre projet et ajouter hello suivant tooit de code :
   
        {
            "require": {
                "microsoft/windowsazure": "^0.4"
            }
        }
2. Téléchargez **[composer.phar][composer-phar]** à la racine du projet.
3. Ouvrez une invite de commandes et exécutez cette commande à la racine du projet :
   
        php composer.phar install

## <a name="azure-powershell-and-azure-emulators"></a>Azure PowerShell et émulateurs Azure
Azure PowerShell est un ensemble de cmdlets PowerShell permettant de déployer et de gérer les services Azure, tels que Cloud Services et Virtual Machines. les émulateurs Azure Hello sont les émulateurs de services de cloud computing et des services de gestion des données qui vous permettent de tootest une application localement. Ces composants sont pris en charge uniquement par Windows.

Hello recommandée tooinstall Azure PowerShell et hello émulateurs Azure est toouse hello [Microsoft Web Platform Installer][download-wpi]. Notez que vous pouvez également choisir tooinstall autres composants de développement, tels que PHP, SQL Server, hello Microsoft Drivers for SQL Server pour PHP et WebMatrix.

Pour plus d’informations sur la façon toouse Azure PowerShell, consultez [comment tooUse Azure PowerShell][powershell-tools].

## <a name="azure-cli"></a>Interface de ligne de commande Azure
Hello CLI d’Azure est un ensemble de commandes pour déployer et gérer des services Azure, tels que les sites Web Azure et les Machines virtuelles Azure. Pour plus d’informations sur l’installation du CLI d’Azure, consultez [installation Bonjour Azure CLI](cli-install-nodejs.md).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).

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
