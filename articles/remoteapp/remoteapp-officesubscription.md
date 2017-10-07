---
title: aaaHow toouse votre abonnement Office 365 avec Azure RemoteApp | Documents Microsoft
description: "Découvrez comment vous pouvez utiliser votre abonnement Office 365 dans les applications Office tooshare Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: f82b6e23-2b71-47be-846d-fd93f2652f3c
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2648868dd28cbcd93e38461ae6dce25eaa5d5e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-your-office-365-subscription-with-azure-remoteapp"></a>Comment toouse votre abonnement Office 365 avec Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Saviez-vous que vous pouvez utiliser votre abonnement Office 365 existant dans Azure RemoteApp tooshare les applications Office à partir du cloud de hello ? Lisez la suite pour plus d’informations sur votre Office 365 + les options d’Azure RemoteApp, y compris tooarticles de liens sur Office 365 qui vous aident à rendre hello plus de votre abonnement.

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>Comment utiliser des comptes Office 365 pour Azure RemoteApp ?
Consultez l’article de nouveau de Peter pour tous les hello informations : [comment toouse Azure RemoteApp avec des comptes d’utilisateur Office 365](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-toorun-office-applications-in-azure-remoteapp"></a>Puis-je utiliser mes applications de bureau toorun abonnement Office 365 dans Azure RemoteApp ?
Oui. En fait, à l’aide de votre abonnement Office 365 est hello uniquement de façon toobring votre tooAzure d’applications Office RemoteApp.

(Remarque : Si votre déploiement d’Azure RemoteApp n’est fournie par un partenaire d’hébergement, elles peuvent être en mesure de tooprovide des licences Office basés sur un [contrat de licence de fournisseur de services](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx))

Bonjour intéressant de votre abonnement Office 365 est qu’elle vous permet d’utiliser hello même licence d’utilisateur sur les différentes plateformes et environnements, notamment hello cloud Azure. Lorsque vous utilisez des applications Office dans Azure RemoteApp, vous ne devez toopurchase des licences supplémentaires ou configurer vos licences existantes d’une manière particulière. Il vous suffit de disposer d’un abonnement Office 365 qui inclut [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx).

Office 365 ProPlus permet [l’activation d’ordinateurs partagés](https://technet.microsoft.com/library/Dn782860.aspx) : cette fonctionnalité permet l’activation temporaire basée sur les utilisateurs pour Office dans les environnements virtuels et cloud comme Azure RemoteApp (et les Services Bureau à distance).

Quels plans Office 365 incluent Office 365 ProPlus ? Extraire hello [disponibilité au sein de chaque plan de Service](https://technet.microsoft.com/library/office-365-plan-options.aspx) table. Notez que pas tous les plans incluent Office 365 ProPlus (par exemple, un plan Office 365 entreprise hello). Si votre plan n’existe pas, envisagez la mise à niveau de plan tooa qui effectue (par exemple, Office 365 éducation E3).

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>Comment mes licences Office 365 ProPlus sont-elles utilisées avec Azure RemoteApp ?
Chaque licence utilisateur pour Office 365 ProPlus permet un seul utilisateur à activer des applications Office sur des ordinateurs de too5 ainsi que les tablettes et téléphones. Chaque activation est inscrit avec l’utilisateur de hello jusqu'à ce qu’ils désactiver l’appareil de hello Office. (Les utilisateurs peuvent gérer leurs appareils Bonjour [portail Office 365](https://portal.office365.com/).)

Avec Azure RemoteApp un seul utilisateur peut se connecter à plusieurs ordinateurs d’hello même jour sans vous en rendre compte. C’est parce que le service de hello gère automatiquement et met à l’échelle les ressources de cloud de hello, tandis que hello utilisateur voit uniquement les applications de hello et les programmes que vous avez partagé. Pour ce scénario, Office 365 ProPlus offre un mode d’activation ordinateur partagé, cela signifie que l’utilisateur n’a pas besoin toodo tout tooaccess de gestion de licence ces ressources et que les ordinateurs individuels hello ne comptent pas par rapport à la limite de l’activation de l’ordinateur hello 5.

Tant que (admin hello) affecter des licences Office 365 ProPlus tooyour utilisateurs, ils peuvent utiliser Office sur leurs appareils personnels, ainsi que votre collection Azure RemoteApp.

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>Quelles applications Office puis-je utiliser avec Office 365 et Azure RemoteApp ?
Vous pouvez utiliser votre tooactivate d’abonnement Office 365 et partage Office 2013 dans les déploiements Azure RemoteApp. Nous ne gèrent pas utilisez hello d’autres versions d’Office avec Azure RemoteApp. Ceci inclut Office 2003, Office 2007, Office 2010 et Office 2016.

## <a name="what-about-visio-pro-or-project-pro"></a>Qu’en est-il de Visio Pro ou de Project Pro ?
image Office 365 ProPlus de Hello inclus dans votre abonnement RemoteApp inclut Pro de Visio et de Project Professionnel. Mais vous ne pouvez pas utiliser votre tooactivate d’abonnement Office 365 ProPlus ces programmes ; ils ont chacun leur propre licence. Vous pouvez les activer dans hello [portail Office 365](https://portal.office365.com/). 

Vous n’avez toolicense ces programmes si vous ne souhaitez pas toouse les. Activer simplement hello programmes que vous souhaitez toouse - ignorez hello d’autres. Vous devez toujours les voir dans l’image de hello, mais vous ne pouvez pas les utiliser. 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>Comment prendre en main Office 365 et Azure RemoteApp ?
Maintenant que vous connaissez les détails hello du Gestionnaire de licences d’Office 365, nous allons vous aider à démarrer l’utiliser dans Azure RemoteApp, c’est très simple :

Lorsque vous créez votre collection Azure RemoteApp, utilisez hello **Office 365 ProPlus (inscription requise)** image.

![Image Azure RemoteApp avec Office 365 ProPlus](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

Cette image contient la version la plus récente de Windows Server et Office 365 ProPlus hello. Après avoir configuré votre collection (y compris les applications de publication), vos utilisateurs se connectent simplement à Azure RemoteApp (à l’aide de leur client RemoteApp) et fournissent leurs informations d’identification Office 365 pour les applications Office. Les licences sont automatiquement remises et ne nécessitent aucune configuration ou gestion.

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>Puis-je créer une image personnalisée avec Office 365 ProPlus ?
Vous pouvez créer une image personnalisée pour votre collection qui contient Office 365 ProPlus. Il existe 2 choix : utiliser une image de la galerie Azure hello que nous fournir ou vous pouvez créer votre propre image personnalisée et installer Office 365 ProPlus il.

### <a name="use-hello-azure-gallery-image"></a>Utiliser l’image de la galerie Azure hello
toodeploy de façon plus simple Hello Office 365 ProPlus tooa collection est trop[démarrer avec l’une des images de la galerie Azure hello](remoteapp-image-on-azurevm.md) inclus dans votre abonnement Azure RemoteApp. Assurez-vous que vous choisissez hello **Windows Server à distance hôte de Session bureau avec Office 365 ProPlus préinstallé** image. Ensuite, installez toutes les autres applications que vous voulez sur cette image, et vous êtes toogo.

### <a name="use-a-custom-image"></a>Utilisation d’une image personnalisée
Vous pouvez toujours créer une image personnalisée, vous pouvez créer un [Azure VM](remoteapp-image-on-azurevm.md) ou [créer image hello localement](remoteapp-create-custom-image.md) et chargez-le tooAzure. Dans les deux cas, veillez à qu'installer Office 365 ProPlus à l’aide du nœud de l’activation d’ordinateur partagé hello. Hello d’utilisation [outil de déploiement Office](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx) et suivez hello [instructions](https://technet.microsoft.com/library/Dn782858.aspx) pour l’installation.  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>Désactivation des mises à jour automatiques pour Office 365 ProPlus dans votre image personnalisée - IMPORTANT
Votre image personnalisée est utilisé par Azure RemoteApp en tant que modèle pour ajouter des ressources supplémentaires comme la demande de hello à partir de vos utilisateurs augmente. tooprevent les retards et les problèmes de connexion, désactiver les mises à jour automatique pour Office dans l’image de hello. Si vous ne le faites pas, chaque ressource créée avec ce modèle sera automatiquement mise à jour lors de son démarrage. Au lieu de cela, utilisez les processus Azure RemoteApp standard hello pour mettre à jour votre image personnalisée. De cette façon vous mettre à jour les applications Office hello qu’une seule fois sur l’image de modèle hello et puis permettent d’obtenir des mises à jour hello tooyour utilisateurs d’Azure RemoteApp.

toodisable mises à jour automatiques, ajoutez hello le fichier de configuration d’outil de déploiement Office toohello suivant :

        <Updates Enabled="FALSE" />

À présent, votre fichier de configuration doit contenir les lignes suivantes :

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>Comment puis-je mettre à jour une image avec Office 365 ProPlus ?
Il y image de hello de nombreuses raisons tooupdate dans votre collection. En voici quelques-unes :

* Obtenir les mises à jour de Windows plus récentes hello 
* Obtenir hello dernières Office 365 ProPlus application mises à jour
* Mettre à jour votre application personnalisée
* Modifier d’autres paramètres de configuration pour l’image hello elle-même

Pour les étapes de bout en bout hello pour mettre à jour votre image de hello collection toouse vous mis à jour, accédez [ici](remoteapp-update.md). Mais pour plus d’informations sur la façon dont tooupdate hello image et Office 365 ProPlus, hello informations suivantes.

Deux options s’offrent à vous pour la mise à jour de votre image : remplacer votre image par une nouvelle image ou mettre à jour manuellement votre image existante.

### <a name="replace-your-image-with-hello-latest-azure-gallery-image--add-customizations"></a>Remplacez votre image avec la dernière image de la galerie Azure hello + ajouter des personnalisations
Avec cette option, vous autoriser Microsoft à prendre en charge des mises à jour de Windows Server et Office 365 ProPlus hello. Au lieu de la mise à jour de votre image existante, vous allez créer une image entièrement nouvelle, en fonction de la dernière image de la galerie hello. Ensuite, répétez les étapes précédemment toocustomize image de hello - installer des applications personnalisées, modifier la configuration de l’image hello, etc..

images de la galerie Hello sont régulièrement mis à jour, vous pouvez compter, sachant que vos applications Windows Server et Office 365 ProPlus sont des toodate. Bien entendu, les compromis hello sont que vous aurez tooapply vos personnalisations chaque fois que vous obtenez une nouvelle image. Vous pouvez créer tooautomate scripts définissant vos personnalisations.

### <a name="manually-update-your-existing-image"></a>Mise à jour manuelle de votre image existante
Avec cette option, vous utilisez standard outils tooapply mises à jour toohello image système Windows. Pour Office 365 ProPlus, utilisez toodownload d’outil de déploiement Office hello et installer les dernières mises à jour de hello ou les versions d’Office 365 ProPlus.

> [!IMPORTANT]
> N’oubliez pas - désactiver les mises à jour automatiques Office 365 ProPlus hello.
> 
> 

En savoir plus sur l’utilisation de hello outil déploiement d’Office pour les mises à jour ?

* [Déployer en un clic pour les produits Office 365 à l’aide de hello outil déploiement d’Office](https://technet.microsoft.com/library/JJ219423.aspx)
* [Déploiement et mise à jour d’Office 365 ProPlus à l’aide d’outil de déploiement Office hello](https://channel9.msdn.com/Events/Ignite/2015/BRK3168) (vidéo)
* [Définir les paramètres de mise à jour pour Office 365 ProPlus](https://technet.microsoft.com/library/dn761708.aspx)

