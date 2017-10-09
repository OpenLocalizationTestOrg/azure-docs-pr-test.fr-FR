---
title: "aaaOptions pour la migration en dehors d’Azure RemoteApp | Documents Microsoft"
description: "En savoir plus sur les options de hello pour la migration en dehors d’Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Options de migration hors d’Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp ne sera plus disponible à partir du 31 août 2017. Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.


Si vous avez arrêté à l’aide d’Azure RemoteApp en raison de hello [annonce du retrait](https://go.microsoft.com/fwlink/?linkid=821148) ou parce que vous avez terminé votre version d’évaluation, vous devez toomigrate hors service d’applications Azure RemoteApp tooanother. Il existe deux approches différentes pour la migration : le déploiement autogéré (souvent appelé Infrastructure en tant que Service [IaaS]) ou une offre de plateforme entièrement gérée (souvent appelée Plateforme ou Logiciel en tant que service [PaaS/SaaS]). 

L’IaaS en libre-service est un déploiement personnalisable que vous gérez, exploitez et possédez, directement déployé sur des machines virtuelles (VM) ou des systèmes physiques. À hello autres terminer, une PaaS/SaaS entièrement géré offre est ressemble davantage à Azure RemoteApp - un partenaire fournit une couche de service sur une solution de communication à distance qui gère le fonctionnement et la maintenance, pendant que vous, en tant que client de hello, effectuer une gestion des applications et des images.

[Afficher hello Azure RemoteApp webinaires sur les options de migration](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), ou de lecture pour plus d’informations (y compris des exemples de différente options d’hébergement de hello).

## <a name="self-managed-iaas-solutions"></a>Solutions autogérées (IaaS)
### <a name="rds-on-iaas"></a>**RDS sur IaaS**
Vous pouvez déployer un déploiement de services Bureau à distance natif basé sur les sessions (dans Windows Server) à l’aide de RemoteApp sur des postes de travail locaux ou dans un environnement hébergé (comme sur les machines virtuelles Azure). Les services Bureau à Distance sur les déploiements IaaS sont parfaits pour les clients déjà familiarisés avec cette solution et qui ont une expertise technique existante pour les déploiements de services Bureau à Distance. 

> [!NOTE]
> Vous devez avec Software Assurance (SA) de licence en Volume pour les services Bureau à distance client accès licences toouse cette option de déploiement.

Le déploiement des services Bureau à Distance sur des machines virtuelles Azure est plus facile que jamais lorsque vous utilisez le déploiement et des modèles d’application de correctifs (lisez la [présentation](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) puis [récupérez-les](https://aka.ms/rdautomation)). Vous pouvez obtenir les mêmes fonctionnalités de mise à l’échelle élastiques avec les ressources de modèle de déploiement classique Azure (pas les ressources de modèle de ressource Azure) dans Azure RemoteApp hello à l’aide de hello [mise à l’échelle de script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), bien qu’il existe plus personnalisations et configurations. Lorsque vous déployez des services Bureau à distance sur des machines virtuelles Azure, est prise en charge via [Azure prend en charge](https://azure.microsoft.com/support/plans/), hello même professionnels du support technique vous pris en charge avec Azure RemoteApp. Vous pouvez obtenir des estimations de coût en fonction de votre utilisation existante en contactant [prise en charge Azure](https://azure.microsoft.com/support/plans/), ou vous pouvez effectuer des calculs vous-même à l’aide un bientôt toobe publié calculateur de coût.  En outre, avec des machines virtuelles de série N (actuellement en aperçu privé), vous pouvez ajouter vGPU - plus d’informations sur l’ajout de processeur et sur la façon de réponse trop[maîtriser les améliorations des services Bureau à distance dans Windows Server 2016](https://myignite.microsoft.com/videos/2794) dans notre session Ignite.   

Nous avons des guides de déploiement de l’étape par étape pour [Windows Server 2012 R2](http://aka.ms/rdsonazure) et [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist avec votre déploiement. Extraire hello [blog du Bureau à distance](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) pour les informations les plus récentes hello.

### <a name="citrix-on-iaas"></a>**Citrix sur IaaS**
Un déploiement Citrix natif de XenApp ou de XenDesktop basé sur les sessions peut être déployé localement ou dans un environnement hébergé (par exemple sur des machines virtuelles Azure). 

Guide de déploiement étape par étape hello, consultez [7.6 XA de Citrix sur Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), pour plus d’informations. En savoir plus sur [Citrix sur Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), avec notamment un calculateur de prix. Vous pouvez également rechercher un [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss vos options avec.

## <a name="fully-managed-paassaas-offerings"></a>Offres entièrement gérés (PaaS/SaaS)

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp Essentials (parution : avril 2017)
Disponible pour l’instant sur hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials est le nouveau service de virtualisation d’application hello, associant hello puissance et flexibilité de hello plateforme Cloud de Citrix avec simple hello et normative, et Pour utiliser la vision de Microsoft Azure RemoteApp. 

Les clients Azure RemoteApp existants peuvent [s’inscrire pour profiter d’une version d’évaluation gratuite](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).  Remarque : seul le service utilisateur Citrix est gratuit. Calcul Azure et Stockage Azure sont payants.

En savoir plus :
- [Migrer à partir d’Azure RemoteApp tooCitrix XenApp Essentials](remoteapp-migrate-citrix.md)
- [Citrix et Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Présentation de Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k)  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Services Citrix Cloud XenApp et XenDesktop 

[Le Service Cloud XenApp Citrix et XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) est hello meilleure solution pour la remise de hello des applications et poste de travail, plus avancées de gestion et ses fonctionnalités de surveillance. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (nom de la plateforme : MyCloudIT)
[MyCloudIT](https://mycloudit.com) est une plate-forme d’automatisation pour toosimplify de sociétés informatiques, optimiser et mettre à l’échelle de la migration hello et remise des bureaux à distance, les applications à distance et l’infrastructure dans hello Microsoft Azure Cloud. 

plateforme de MyCloudIT Hello réduit le temps de déploiement en 95 %, Azure coût de 30 % et déplace de l’infrastructure informatique de leurs clients dans cloud hello retirés au bout de quelques séquences de touches. Les partenaires peuvent désormais gérer les clients à partir d’un tableau de bord global, les utilisateurs finaux de service monde hello comme jamais auparavant et augmenter les revenus sans ajouter une charge supplémentaire ou formation Azure complète.  

> Emplacement principal : Dallas, Texas, États-Unis
> 
> Région de l’opération  : monde entier
> 
> Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Fournisseur de services Microsoft : Oui
> 
> Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux
> 
> Solutions de migration Azure RemoteApp : Oui, [en savoir plus](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, vice-président du développement commercial
> 
> Téléphone : 972-218-0741
>   
> E-mail : [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Frame

Les organisations informatiques dans enterprise et gouvernement, fournisseurs de services gérés et principaux fournisseurs de logiciels choisissez toocreate de Frame et gérer leurs espaces de travail sécurisés, défini par logiciel dans le cloud de hello. À partir de toolarge petites organisations, Frame rend très facile toolet utilisateurs accéder aux applications Windows sur n’importe quel navigateur à partir de n’importe quel appareil. Hello plateforme de Frame comprend tout ce dont un administrateur besoins toodeploy applications de cloud hello notamment hello infrastructure Azure et licences des services Bureau à distance (mettre votre propre compte Azure et licences est facultative). 

En savoir plus sur [Frame sur Azure](https://www.fra.me/ara). 

> Emplacement principal : San Mateo, CA, États-Unis
>
> Région de l’opération  : monde entier
>
> Partenaire Microsoft : Oui
> 
> Téléphone : 1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu fournit une solution simple d’espace de travail en ligne qui exécute des applications héritées, SaaS et des documents à partir d’un navigateur html5. Ainsi, les applications sont disponibles en toute sécurité, sur tous les types d’appareils. Pour les services SaaS, un large éventail d’options d’authentification unique (SSO) est disponible. De plus, plusieurs systèmes de fichiers (cloud) peuvent être profondément intégrés dans votre espace de travail. Espace de travail en ligne de Awingu enrichi donne suivant toofull mobilité, une sécurité optimale avec contrôles granulaires (par exemple, du téléchargement/chargement), l’utilisation complète de l’audit, l’authentification multifacteur (par exemple, Azure MFA), l’enregistrement de session et bien plus encore. Solution originale, Awingu permet le partage de session d’application et de document pour une collaboration sûre et optimisée.
Awingu est une solution d’API ouverte, multi-AD et mutualisée. Elle est utilisée par les petites et grandes entreprises, fournisseurs de services Cloud et les [ISV](http://www.isv2saas.com). Ces clients plaira particulièrement hello facile d’utilisation, facilité à installer et à faible coût total de possession.

Awingu tout-en-un est [disponibles dans Azure Marketplace de hello](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) avec 2 utilisateurs simultanés intégrés. Des licences supplémentaires sont disponibles via un [large éventail de distributeurs et revendeurs](http://www.awingu.com/reseller).

En savoir plus sur [Awingu sur comme autre tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).


> Emplacement principal : Belgique
> 
> Régions opérationnelles : EMEA, Amérique du Nord et Brésil
> 
> Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux 
> 
> **Mondial** :
> 
> Arnaud Marlière, CMO
> 
> E-mail : [arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> Téléphone : +1 646 583 3025
> 
> **Siège en Belgique** :
> 
> Ottergemsesteenweg-Zuid 808 B44
> 
> 9000 Gent
> 
> E-mail : [info@awingu.com](mailto:info@awingu.com) 
> 
> Téléphone : +32 9 296 40 11
> 
> **États-Unis** :
> 
> 7 floor, Ave 1177 Hello Amériques,
> 
> New York, NY 10036
> 
> E-mail : [info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Fournisseur de services hébergés Microsoft
Partenaires d’hébergement offrent généralement entièrement géré hébergé bureau Windows et de hello de service d’application, qui peut inclure la gestion des ressources Azure, des systèmes d’exploitation, des applications et de support technique à l’aide du partenaire de hello du Gestionnaire de licences des contrats avec Microsoft et autres fournisseurs de logiciels, ainsi que d’en cours de contrat de licence de fournisseur de services de la licence d’accès abonné (SAL) revente tooallow. Hello ci-après fournit des détails et informations de contact pour certaines des hébergeurs hello spécialisés pour aider les clients avec leur migration d’Azure RemoteApp. Extraire [liste actuelle de hello des fournisseurs de services hébergés](http://aka.ms/rdsonazurecertified) qui terminées hello RDS sur IaaS, chemin d’accès et d’évaluation de la formation.  

### <a name="citrix-service-provider-program"></a>Programme de fournisseur de services de Citrix
Hello Citrix Service fournisseur de programme facilite pour simplifier service fournisseurs toodeliver hello virtuel cloud computing tooSMBs, offre les services hello qu’ils souhaitent dans un modèle simple et de paiement à l’utilisation. Les fournisseurs de services de Citrix développer leur activité Microsoft SPLA et développer leurs investissements de plateforme des services Bureau à distance avec n’importe quel appareil, accès en tout lieu, hello plus large prise en charge des applications une expérience enrichie, renforcer la sécurité et une extensibilité accrue. Ainsi, les fournisseurs de services de Citrix attirent plus d’abonnés, améliorent la satisfaction des clients et réduisent les coûts d’exploitation. [En savoir plus](http://www.citrix.com/products/service-providers.html) ou [trouver un partenaire](https://www.citrix.com/buy/partnerlocator.html).

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) spécialisée de fournir des solutions de bureau hébergées, fourniture de bureau et applications ISV expériences reposant sur la technologie tooa global client Microsoft base à partir d’Azure et de leurs propres centres de données.

> Emplacements principaux : Londres, Royaume-Uni ; Singapour ; Houston, Texas
> 
> Région de l’opération  : monde entier
> 
> Statut du partenaire : Gold
> 
> Fournisseur de services Microsoft : Oui
> 
> Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux
> 
> Solutions de migration Azure RemoteApp : Oui, [en savoir plus](http://www.acuutech.com/ara-migration/)
> 
> **Royaume-Uni** :
>   
> 5/6 York maison, Langston Road,
>   
> Loughton, Essex IG10 3TQ
>   
> Téléphone : +44 (0) 20 8502 2155
> 
> **Singapour** :
>   
> 100 Cecil Street, #09-02, 
>   
> Hello Globe, Singapour 069532
> 
> Téléphone : +65 6709 4933
>   
> **Amérique du Nord** :
>   
> 3601 S. Sandman St.
>   
> Suite 200, Houston, TX 77098
>   
> Téléphone : +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) spécialisé dans les éditeurs de logiciels en cours de transition toohello Cloud et ISV' recherche toooptimize leurs configurations de cloud en cours. ASPEX offre un large éventail de services gérés, d’opérations de développement et de conseil.  

> Emplacement principal : Anvers, Belgique
> 
> Région d’activité : Europe de l’Ouest
> 
> Statut du partenaire : [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Fournisseur de services Microsoft : Oui
> 
> Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux
> 
> Solutions de migration Azure RemoteApp : Oui, [en savoir plus](https://www.aspex.be/en/azure-remote-apps)
> 
> Téléphone  : +3232202198
> 
> Mail : [info@aspex.be](mailto:info@aspex.be)
> 
> Web : [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) aide les entreprises, administrations locales, des organismes non gouvernementaux et les établissements de soins de santé avec leur voyage vers un moyen plus intelligent de travail Bonjour Cloud Microsoft. être productif n’importe où et en toute sécurisé, avec n’importe quel appareil et pour un faible coût informatique. Caase.com est un vrai spécialiste de Microsoft Office 365, Azure, Enterprise Mobility + Security et Windows. Caase.com propose à ses clients du conseil, des services de migration, des programmes d’adoption, des formations, des services de gestion et de support dans l’optique de créer une plateforme optimisée et sécurisée favorisant la collaboration entre leurs employés, leurs partenaires et leurs fournisseurs.
Caase.com est maîtrisée hello de hello espace de travail Azure à distance (espace de travail mobile) et hello espace de travail numérique (Social Intranet). Les deux solutions – accomplies avec adoption – sont foundation hello qui garantit que les utilisateurs de hello de ces solutions ont expérience plus agréable, réussie et efficace de hello dans leur toohello itinéraire Cloud Microsoft.
Vous trouverez un texte de présentation de ces solutions, ainsi qu’une vidéo, à l’adresse suivante (en néerlandais) : http://caase.com/over-ons/

> Région d’exploitation : siège aux Pays-Bas, portée mondiale
> 
> Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Fournisseur de services Microsoft : Oui
> 
> Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux
> 
> Solutions de migration Azure RemoteApp : oui, [en savoir plus](http://caase.com/diensten/microsoft-azure/).
> 
> 
> Pays-bas :
> 
> Rigtersbleek-Zandvoort 10 (De Spinnerij)
> 
> 7521 BE, Enschede
> 
> Téléphone : +31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Nerdio pour Azure](http://getnerdio.com/nfa/) est une plate-forme d’automatisation informatique qui remet ridiculement simple mise en service, la gestion et l’optimisation des environnements informatiques complets Bonjour cloud de Microsoft. Une paire d’heures suffit pour mettre en place des bureaux virtuels, des applications distantes et des serveurs. Administrer l’environnement hello dans trois clics ou moins avec le portail d’administration Nerdio. Utilisez intelligente montée en puissance automatique et enregistrez les 40 % de too60 dans les ressources IaaS Azure.

> Site principal : Chicago, IL. Région d’exploitation : monde. Statut partenaire : [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Fournisseur de services Microsoft Cloud : oui
> 
> Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux
> 
> Solutions de migration Azure RemoteApp : Oui
> 
> 
> 8001 Lincoln Ave
> 
> Suite 212
> 
> Skokie, IL 60077
> 
> États-Unis
> 
> (844) 4NERDIO poste 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/) propose des services cloud privés et publics (Azure) pour toute la gamme Microsoft Dynamics (NAV, AX, GP, SL, CRM).

> Emplacement principal : Pays-Bas
> 
> Région de l’opération : monde entier
> 
> Statut du partenaire : [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Fournisseur de services Microsoft : Oui
> 
> Proposer des solutions RemoteApp et Desktop basées sur les sessions : Oui, les deux
> 
> **Europe / Moyen-Orient / Afrique** :
> 
> Prins Mauritslaan 29-35
> 
> 71 LP Badhoevedorp
> 
> Hello pays-bas
> 
> Téléphone : +31 20 547 8060 
> 
>  **Amérique** :
> 
> 171 Saxony Road, Suite 105
> 
> Encinitas, CA 92024
> 
> San Diego
> 
> États-Unis
> 
> Téléphone : +1 858 385 8900 
> 
> **Asie-Pacifique** :
> 
> 105 Cecil Street
>    
> \#11-08, hello octogone
> 
> Singapour 069534
> 
> Singapour
>   
> Téléphone - Singapour : +65 6222 6591
> 
> Téléphone - Australie : +61 2 8310 5568 
>    
> Téléphone - Nouvelle-Zélande : +64 4 488 0321
> 
## <a name="need-more-help"></a>Besoin de plus d’aide ?
Toujours besoin d’aide pour choisir ou des questions supplémentaires ? Utilisez une des hello suivant les méthodes tooget aide. 

1. Envoyez-nous un e-mail à l’adresse [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
2. Contacter le [support Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Commencez par créer un [ticket d’assistance Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
3. Appelez-nous. [Rechercher le numéro de téléphone d'un service commercial local](https://azure.microsoft.com/overview/sales-number/).

