---
title: aaaAzure RemoteApp FAQ | Documents Microsoft
description: "Découvrez les réponses toohello plus fréquemment posées sur Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: swadhwa
editor: 
ms.assetid: bad66603-91f9-437f-8a70-236405d2a27f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: da981fea9e38b4e74694aeaba5f97c8ed897ccd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-faq"></a>FAQ Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.
> 
> 

Nous avons hello suivant des questions sur Azure RemoteApp. Vous avez d'autres questions ? Visitez hello [RemoteApp forums](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureRemoteApp) et dites-nous ce que vous devez tooknow, ou un commentaire de liste déroulante ci-dessous.

## <a name="cant-find-what-youre-looking-for-have-a-question-we-didnt-answer"></a>Vous ne trouvez pas ce que vous recherchez ? Vous avez une question à laquelle nous n’avons pas répondu ?
Si vous ne trouvez pas les informations de hello vous avez besoin, ou si vous avez une question supplémentaire qui nous n’allons pas ici couvrant, accédez toohello [forum Azure RemoteApp](http://aka.ms/araforum) et demandez à votre question. Nous pouvons toujours ajouter d’autres réponses à cet emplacement.

## <a name="what-is-azure-remoteapp"></a>Présentation d'Azure RemoteApp
* **Présentation d'Azure RemoteApp** RemoteApp est qu'un service Azure vous permet de fournir des tooapplications un accès sécurisé à distance à partir de nombreux appareils utilisateur. En savoir plus sur [Azure RemoteApp](remoteapp-whatis.md).
* **Quelles sont les options de déploiement hello ?** Il existe deux types de collection RemoteApp : cloud et hybride. Celui dont vous avez besoin dépend de plusieurs facteurs, tels que la nécessité d’une jonction de domaine. Nous parlons de toutes ces décisions [ici](remoteapp-collections.md).

## <a name="quick-tips-on-using-azure-remoteapp"></a>Conseils rapides pour l’utilisation d’Azure RemoteApp
* **Combien de temps peut-il s’écouler avant que je sois déconnecté ? Combien puis-je être inactif avant que pouvez-vous me donner le démarrage de hello ?** 4 heures. Si vous ou l’un de vos utilisateurs êtes inactif pendant 4 heures, vous êtes automatiquement déconnecté d’Azure RemoteApp. Extraction hello autres paramètres par défaut dans [abonnement Azure et limites de Service, Quotas et contraintes](../azure-subscription-service-limits.md).
* **Puis-je essayer ce service gratuitement ?** Oui. Une version d'évaluation gratuite est disponible pendant 30 jours. Après la fin de la version d’évaluation de hello, vous pouvez passer tooa payé compte (que vous pouvez utiliser en production) ou arrêt à l’aide du service de hello. Commencez votre évaluation gratuite en accédant trop[portal.azure.com](http://portal.azure.com) -créer une nouvelle instance de RemoteApp. Avec la version d’évaluation gratuite de hello, vous pouvez générer des 2 instances de RemoteApp avec 10 utilisateurs par instance. N'oubliez pas que cette version d'évaluation n'est utilisable que pendant 30 jours.
  
  ## <a name="azure-remoteapp-subscription-details"></a>Détails de l’abonnement Azure RemoteApp
* **Quelles sont les limites de service hello ?** Vous pouvez en savoir plus sur les paramètres par défaut de hello et d’Azure RemoteApp dans les limites de service [abonnement Azure et limites de Service, Quotas et contraintes](../azure-subscription-service-limits.md). N’hésitez pas à nous contacter si vous avez d'autres questions.
* **Nombre d’utilisateurs faire j’ai toohave ?** Il existe un minimum de 20 utilisateurs. Me permet de répéter que toobe effacer super - hello MINIMUM est de 20. Vous serez facturé pour 20 utilisateurs. 
* **Combien coûte RemoteApp ?** Consultez les [tarifs détaillés d'Azure RemoteApp ](https://azure.microsoft.com/pricing/details/remoteapp/).
* **Un type de collection coûte-t-il plus qu’un autre ?** Oui, il le peut, selon les besoins de votre collection. Une collection hybride nécessite une connexion Azure RemoteApp tooyour sur un réseau local. Si vous utilisez un itinéraire réseau virtuel/Express, il est sans coût supplémentaire. Mais si vous utilisez un réseau virtuel Azure et une passerelle ou Express Route, vous serez facturé pour hello [passerelle VPN](https://azure.microsoft.com/pricing/details/vpn-gateway) ou [Express Route](https://azure.microsoft.com/pricing/details/expressroute/). Ce coût (détaillé dans les liens hello) sur votre Azure RemoteApp mensuelle des coûts lié.

## <a name="collections---whats-supported-which-should-you-use-and-others"></a>Collections : ce qui est pris en charge, laquelle utiliser, etc.
* **Les applications métier personnalisées sont-elles prises en charge ?** Oui. toouse une application personnalisée dans Azure RemoteApp, créez un [image de modèle personnalisé](remoteapp-create-custom-image.md), puis téléchargez toohello RemoteApp collection.
* **Mon application métier personnalisée fonctionne dans Azure RemoteApp ?**  hello meilleures toofigure de façon qu’out est tootest il. Extraire hello [centre de compatibilité de bureau à distance](http://www.rdcompatibility.com/compatibility/default.aspx).
* **Quelle méthode de déploiement (cloud ou hybride) convient le mieux à mon organisation ?** Les collections hybride expérience hello plus complète si vous voulez une intégration complète avec l’authentification unique (SSO) et la connectivité de réseau local sécurisé. Les collections de cloud offrent un moyen simple et agile de tooisolate votre déploiement à l’aide de plusieurs méthodes d’authentification. En savoir plus sur hello [options de déploiement](remoteapp-whatis.md).
* **Nous disposons d'une base de données SQL ou autre localement ou dans Azure. Quel type de déploiement devons-nous utiliser ?** Cela dépend de l'emplacement de votre base de données SQL ou principale. Si la base de données hello est dans un réseau privé, utilisez la collection hybride de hello. Si la base de données hello est exposé toohello Internet et permet aux clients de connexions tooconnect tooit, vous pouvez utiliser la collection de cloud hello.
* **Qu'en est-il du mappage du lecteurs, des ports USB et série, du partage du Presse-papiers et de la redirection d'imprimante ?** Toutes ces fonctionnalités sont prises en charge dans Azure RemoteApp. Le partage du Presse-papiers et la redirection d'imprimante sont activés par défaut. Plus d'informations sur la redirection [ici](remoteapp-redirection.md). 

## <a name="template-images"></a>Images de modèle
* **Puis-je utiliser un cloud ou un ordinateur virtuel existant comme modèle de hello pour ma collection RemoteApp ?** Oui. Vous pouvez créer une image basée sur une machine virtuelle Azure, utilisez une des images hello inclus dans votre abonnement ou créer une image personnalisée. Extraire hello [options d’image RemoteApp](remoteapp-imageoptions.md).

## <a name="network-options"></a>Options réseau
* **collection de Hello hybride nécessite un réseau virtuel. Est-il possible d'utiliser notre réseau virtuel existant ?** Vous pouvez si un réseau virtuel Azure est hello réseau virtuel existant. Consultez « étape 1 : configurer votre réseau virtuel « Bonjour [obtenir des instructions de la collection hybride](remoteapp-create-hybrid-deployment.md) pour plus d’informations.
* **Puis-je utiliser un réseau virtuel avec une collection cloud ?** Vous le pouvez en effet. Pour plus d’informations, consultez [Création d’une collection cloud](remoteapp-create-cloud-deployment.md), en particulier l’étape 1.

## <a name="authentication-options"></a>Options d’authentification
* **Qu'en est-il de l'authentification ? Les méthodes qui sont pris en charge ?**  collection de cloud hello prend en charge les comptes Microsoft et comptes Azure Active Directory, qui sont des comptes Office 365. collection de hybride Hello prend en charge uniquement les comptes Azure Active Directory qui ont été synchronisés (à l’aide d’un outil tel que [synchronisation Azure Active Directory](http://blogs.technet.com/b/ad/archive/2014/09/16/azure-active-directory-sync-is-now-ga.aspx)) à partir d’un déploiement de Windows Server Active Directory ; plus précisément, soit été synchronisés avec hello Option de synchronisation de mot de passe ou synchronisés avec fédération des Services de fédération Active Directory (AD FS) configurée. Vous pouvez également configurer l’[authentification multifacteur](https://azure.microsoft.com/services/multi-factor-authentication/).

> [!NOTE]
> utilisateurs d’Azure Active Directory Hello doivent provenir de locataire hello qui est associé à votre abonnement. (Vous pouvez afficher et modifier votre abonnement sur hello **paramètres** hello portail. Consultez [client Azure Active Directory de modification hello utilisé par RemoteApp](remoteapp-changetenant.md) pour plus d’informations.)
> 
> 

* **Pourquoi ne puis-je pas donner mon compte d’accès Azure Active Directory ?**  utilisateurs d’Azure Active Directory hello doivent provenir de répertoire hello qui est associé à votre abonnement. Vous pouvez afficher ou modifier ce répertoire sur l’onglet Paramètres de hello dans le portail de hello. Consultez [client Azure Active Directory de modification hello utilisé par RemoteApp](remoteapp-changetenant.md) pour plus d’informations.

## <a name="clients---what-device-can-i-use-tooaccess-azure-remoteapp"></a>Les clients - quel appareil peut utiliser tooaccess Azure RemoteApp ?
Vous pouvez trouver des informations client bon, y compris les étapes pour l’installation de clients différents hello [l’accès à vos applications dans Azure RemoteApp](remoteapp-clients.md).

* **Les appareils et les systèmes d’exploitation les applications clientes hello prennent en charge ?**
  Premier, les ordinateurs hello et tablettes : 
  
  * Windows 10 (client en version préliminaire)
  * Windows 8.1 et Windows 8
  * Windows 7 Service Pack 1
  * Mac OS X
  * Windows RT
  * Tablettes Android
  * iPad

    Et les téléphones hello :
  * iPhone
  * Téléphone Android
  * Windows Phone
    
    [Téléchargez](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) un client RemoteApp dès maintenant.
* **Azure RemoteApp prend-il en charge les clients légers ?** Oui, hello clients légers Windows Embedded suivants sont pris en charge :
  
  * Windows Embedded Standard 7
  * Windows Embedded 8 Standard
  * Windows Embedded 8.1 Industry Pro
  * Windows 10 IoT Entreprise
* **La version de Windows Server est prise en charge pour hello hôte de Session de bureau à distance (RDSH) ?** Windows Server 2012 R2.

## <a name="support-and-feedback"></a>Support et commentaires
* **Qu’est le plan de support hello pour RemoteApp ?** La gestion de la facturation et des abonnements est fournie gratuitement. Le support technique est disponible via hello [plans de service Azure](https://azure.microsoft.com/support/plans/). Vous pouvez également bénéficier du support gratuit de la communauté via notre [forum de discussion Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp). 
* **Comment envoyer des commentaires ?** Visitez hello [forum de commentaires](https://feedback.azure.com/forums/247748-azure-remoteapp/).
* **Qui m’adresser toolearn plus d’informations sur Azure RemoteApp ?** Dans Ajout tooour [forum de discussion](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=AzureRemoteApp), qui est une question de toopost idéal, vous pouvez joindre une fois par semaine hello [poser hello Experts webinaire](https://azureinfo.microsoft.com/US-Azure-WBNR-FY15-11Nov-AzureRemoteAppAskTheExperts-Registration-Page.html), où nous parlons de tous les éléments de RemoteApp.
* **Qu'en est-il de la documentation RemoteApp ?** Merci d'avoir posé la question. En outre toohello contenu dans le contenu de l’aide du portail hello d’aide (cliquez simplement sur hello **?** sur une page de portail de hello), hello suivant les articles est disponible tooteach vous tout sur RemoteApp :
  
  * **Mise en route**
    * [Présentation de RemoteApp](remoteapp-whatis.md)
    * [Nouveautés dans les images de modèle RemoteApp hello](remoteapp-images.md)
    * [Comment fonctionne la gestion de licences ?](remoteapp-licensing.md)
    * [Comment RemoteApp et Office fonctionnent ensemble ?](remoteapp-o365.md)
    * [Comment la redirection fonctionne-t-elle dans RemoteApp ?](remoteapp-redirection.md)
  * **Déploiement**
    * [Création d'une image de modèle personnalisée](remoteapp-create-custom-image.md)
    * [Création d'une collection hybride](remoteapp-create-hybrid-deployment.md)
    * [Création d’une collection cloud](remoteapp-create-cloud-deployment.md)
    * [Configuration d'Azure Active Directory pour RemoteApp](remoteapp-ad.md)
    * [Publication d'une application dans RemoteApp](remoteapp-publish.md)
  * **Gestion**
    
    * [Ajout d'utilisateurs](remoteapp-user.md)
    * [Meilleures pratiques pour la configuration et l'utilisation de RemoteApp](remoteapp-bestpractices.md)    
    
    Vidéos Nous vous proposons également un certain nombre de vidéos sur RemoteApp. Certains fournissent introduction ([Introduction tooAzure RemoteApp](https://azure.microsoft.com/documentation/videos/cloud-cover-ep-150-azure-remote-app-with-thomas-willingham-and-nihar-namjoshi/)) tandis que d’autres vous guident tout déploiement ([déploiement de cloud computing](https://www.youtube.com/watch?v=3NAv2iwZtGc&feature=youtu.be) et [déploiement hybride](https://www.youtube.com/watch?v=GCIMxPUvg0c&feature=youtu.be)). Consultez-les !

### <a name="help-us-help-you"></a>Vos commentaires nous aideront à mieux vous servir
Saviez-vous que toorating d’ajout de cet article et de faire des commentaires vers le bas, vous pouvez effectuer modifications toohello article ? Il manque des informations ? Des informations sont erronées ? Certains passages ne sont pas clairs ? Faites défiler et cliquez sur **modifier sur GitHub** toomake modifications - ces proviendront toous pour révision et, une fois que nous se déconnecter sur ces derniers, vous verrez alors vos modifications et des améliorations ici.

