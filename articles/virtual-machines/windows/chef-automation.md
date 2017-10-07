---
title: "déploiement d’ordinateur virtuel aaaAzure avec Chef | Documents Microsoft"
description: "Découvrez comment toouse Chef toodo automatisé déploiement d’ordinateurs virtuels et de configuration sur Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a>Automatisation du déploiement de machine virtuelle Azure avec Chef
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Chef est un excellent outil d’automatisation et de fourniture des configurations d’état souhaitées.

Avec notre dernière version de l’api du cloud, Chef fournit une intégration transparente avec Azure, ce qui vous hello tooprovision de capacité et déployer des États de configuration via une commande unique.

Dans cet article, vous allez apprendre comment tooset de votre tooprovision d’environnement Chef Azure virtual machines et vous guide dans la création d’une stratégie ou un « Livre de recettes » et puis de déployer cette tooan cookbook machine virtuelle Azure.

Commençons !

## <a name="chef-basics"></a>Principes fondamentaux de Chef
Avant de commencer, je vous suggère de que vous passez en revue les concepts de base hello du Chef. Des éléments très intéressants sont disponibles <a href="http://www.chef.io/chef" target="_blank">ici</a> et nous vous recommandons de les passer en revue avant de suivre ce guide. J’ai toutefois récapitulent les principes de base hello avant de commencer.

Hello suivant schéma décrit l’architecture de Chef hello globale.

![][2]

Chef présente trois principaux composants architecturaux : le serveur Chef, le client Chef (nœud) et la station de travail Chef.

Hello serveur Chef est le point de gestion et il existe deux options pour le serveur Chef de hello : une solution hébergée ou une solution sur site. Nous allons utiliser une solution hébergée.

Client Hello Chef (nœud) est l’agent hello qui se trouve sur les serveurs hello que vous gérez.

Hello station de travail Chef est notre station de travail administration, où nous créer notre stratégie et exécuter des commandes de gestion de notre. Nous exécutons hello **knife** de commande à partir de la station de travail Chef toomanage de hello notre infrastructure.

Il est également hello concept de « Cuisine » et « Recettes ». Ceux-ci sont effectivement des stratégies hello nous définir et appliquer des serveurs de tooour.

## <a name="preparing-hello-workstation"></a>Préparation de la station de travail hello
Tout d’abord, vous permet de station de travail de préparation hello. J’utilise une station de travail Windows standard. Nous devons toocreate un toostore directory nos fichiers de configuration et les livres de cuisine.

Commencez par créer un répertoire appelé C:\chef.

Créez ensuite un second répertoire appelé c:\chef\cookbooks.

Nous devons maintenant toodownload notre fichier paramètres Azure pour Chef puisse communiquer avec notre abonnement Azure.

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
Télécharger vos paramètres à l’aide de hello PowerShell Azure de publication [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) commande. 

Enregistrer hello publier le fichier de paramètres dans C:\chef.

## <a name="creating-a-managed-chef-account"></a>Création d’un compte Chef géré
Inscrivez-vous à un compte Chef hébergé [ici](https://manage.chef.io/signup).

Au cours du processus d’inscription de hello, vous serez invité à toocreate une nouvelle organisation.

![][3]

Une fois que votre organisation est créé, téléchargez hello starter kit.

![][4]

> [!NOTE]
> Si vous recevez un message vous avertissant que vos clés sont réinitialisées, il est OK tooproceed que nous ne disposons d’aucune infrastructure existante comme encore configuré.
> 
> 

Le fichier zip du starter kit comprend vos clés et fichiers de configuration d’organisation.

## <a name="configuring-hello-chef-workstation"></a>Configuration de station de travail Chef hello
Extraire le contenu de hello de hello chef-starter.zip tooC:\chef.

Copiez tous les fichiers sous starter\chef-chef-repo\.chef tooyour c:\chef active.

Votre annuaire doit maintenant ressembler à hello l’exemple suivant.

![][5]

Vous devez maintenant avoir quatre fichiers notamment racine hello c:\chef hello fichier publication Azure.

fichiers PEM de Hello contient votre organisation et l’administration des clés privées pour la communication pendant que le fichier knife.rb de hello contient votre configuration couteau. Nous avons besoin tooedit hello knife.rb fichier.

Ouvrir le fichier de hello dans l’éditeur de votre choix et modifiez hello « cookbook_path » en supprimant les hello /... / à partir du chemin d’accès de hello afin qu’elle apparaisse comme le montre l’illustration suivante.

    cookbook_path  ["#{current_dir}/cookbooks"]

Ajoutez également réfléchissante nom hello de votre Azure de la ligne suivante de hello publier le fichier de paramètres.

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

Votre fichier knife.rb doit maintenant ressembler toohello similaire, l’exemple suivant.

![][6]

Ces lignes garantit que couteau référence active de livres de cuisine hello sous c:\chef\cookbooks et qu’il utilise également le fichier de paramètres de publication Azure lors des opérations de Azure.

## <a name="installing-hello-chef-development-kit"></a>Lors de l’installation hello Chef Development Kit
Suivant [Téléchargez et installez](http://downloads.getchef.com/chef-dk/windows) hello tooset ChefDK (Chef Development Kit) de votre station de travail Chef.

![][7]

Installer dans l’emplacement par défaut hello c:\opscode. Cette opération prendra environ 10 minutes.

Vérifiez que votre variable PATH comprend les entrées de C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;C:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin

S’ils sont absents, assurez-vous de les ajouter !

*Remarque hello ordre de hello chemin d’accès est IMPORTANT !* Si les chemins opscode ne sont pas dans l’ordre correct de hello que vous rencontrez des problèmes.

Redémarrez votre station de travail avant de continuer.

Ensuite, nous allons installer extension d’Azure Knife hello. Cela fournit couteau hello « Plug-in Azure ».

Exécutez hello commande suivante.

    chef gem install knife-azure ––pre

> [!NOTE]
> argument de pre-Hello garantit que vous recevez la dernière version RC hello Hello plug-in Azure Knife qui fournit l’accès toohello dernier jeu d’API.
> 
> 

Il est probable qu’un nombre de dépendances sera également installé à hello même temps.

![][8]

tooensure que tout est configuré correctement, hello exécution commande suivante.

    knife azure image list

Si tout est configuré correctement, vous verrez une liste d’images Azure disponibles défiler.

Félicitations ! station de travail Hello est configurée.

## <a name="creating-a-cookbook"></a>Création d’un livre de recettes
Un livre de recettes est utilisé par le Chef toodefine un ensemble de commandes que vous souhaitez tooexecute sur votre client géré. Création d’un livre de recettes est simple et nous utilisons hello **chef générer cookbook** commande toogenerate notre modèle livre de recettes. Nous appellerons notre livre de recettes webserver, étant donné que je souhaite disposer d’une stratégie qui déploie IIS automatiquement.

Dans le répertoire C:\Chef exécuter hello commande suivante.

    chef generate cookbook webserver

Cette opération génère un ensemble de fichiers sous le répertoire hello C:\Chef\cookbooks\webserver. Nous avons maintenant besoin toodefine hello de commandes que nous souhaitons notre tooexecute de client Chef sur notre machine virtuelle gérée.

commandes Hello sont stockés dans hello fichier default.rb. Dans ce fichier, je vais définissant un ensemble de commandes qui installe les services IIS, démarre IIS et copie un dossier wwwroot toohello modèle.

Modifier le fichier de C:\chef\cookbooks\webserver\recipes\default.rb hello et ajouter les lignes suivantes de hello.

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

Enregistrez le fichier de hello une fois que vous avez terminé.

## <a name="creating-a-template"></a>Création d’un modèle
Comme mentionné précédemment, nous devons toogenerate un fichier de modèle qui sera utilisé en tant que notre page default.html.

Exécutez hello suivant le modèle de commande toogenerate hello.

    chef generate template webserver Default.htm

Maintenant accédez toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb fichier. Modifier le fichier de hello en ajoutant du code HTML « Hello World » simple, puis enregistrez le fichier de hello.

## <a name="upload-hello-cookbook-toohello-chef-server"></a>Télécharger hello Cookbook toohello serveur Chef
Dans cette étape, nous allons prendre une copie de hello Cookbook que nous avons créé sur la machine locale et de les télécharger toohello le serveur Chef hébergé. Une fois téléchargé, hello Cookbook apparaîtra sous hello **stratégie** onglet.

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a>Déployer une machine virtuelle avec Knife Azure
Maintenant nous déployer une machine virtuelle Azure et appliquer hello Cookbook « Serveur Web » qui va installer notre page de web IIS web service et la valeur par défaut.

Dans l’ordre toodo cela, utilisez hello **knife azure serveur créer** commande.

Suis exemple de commande hello s’affiche ensuite.

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

paramètres de Hello sont explicites. Remplacez vos variables particulières et exécutez.

> [!NOTE]
> Via la ligne de commande hello Bonjour, je suis également automatisation mes règles de filtre de point de terminaison réseau à l’aide du paramètre – tcp-points de terminaison de hello. J’ai ouvert les ports 80 et 3389 tooprovide accès toomy web page et session RDP.
> 
> 

Une fois que vous exécutez la commande hello, accédez toohello Azure portal et vous verrez votre ordinateur commencer tooprovision.

![][13]

invite de commandes Hello s’affiche ensuite.

![][10]

Une fois le déploiement de hello est terminé, nous devons être service web de toohello tooconnect en mesure de via le port 80 comme nous avions ouvert le port de hello lorsque nous avons fourni la machine virtuelle hello hello les commandes Knife Azure. Comme cet ordinateur virtuel est hello une machine virtuelle uniquement dans le service cloud, je le connecterai avec l’url du service cloud hello.

![][11]

Comme vous pouvez le voir, le code html est créatif.

N’oubliez pas que nous pouvons également connecter via une session RDP à partir de hello portail Azure via le port 3389.

Nous espérons que cela a été utile ! Démarrez votre voyage vers l’Infrastructure en tant que code avec Azure dès aujourd’hui !

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
