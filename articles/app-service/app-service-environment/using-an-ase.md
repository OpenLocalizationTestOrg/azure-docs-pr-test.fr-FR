---
title: aaaUse un environnement Azure App Service
description: "Comment toocreate, publier et mettre à l’échelle d’applications dans un environnement Azure App Service"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a>Utilisation d’un environnement App Service #

## <a name="overview"></a>Vue d'ensemble ##

Azure App Service Environment est un déploiement d’Azure App Service dans un sous-réseau dans le réseau virtuel Azure d’un client. Elle comprend :

- **Avant la fin de**: frontaux hello est où HTTP/HTTPS se termine dans un environnement App Service (ASE).
- **Travailleurs**: traitements de hello sont des ressources hello qui hébergent vos applications.
- **Base de données**: base de données hello conserve des informations qui définissent l’environnement de hello.
- **Stockage**: stockage de hello est utilisé toohost hello publiée par le client applications.

> [!NOTE]
> Il existe deux versions d’App Service Environment : ASEv1 et ASEv2. Dans ASEv1, vous devez gérer les ressources de hello avant de pouvoir les utiliser. toolearn comment tooconfigure et gérer ASEv1, consultez [configurer un v1 d’environnement App Service][ConfigureASEv1]. reste Hello de cet article se concentre sur ASEv2.
>
>

Vous pouvez déployer un environnement ASE (ASEv1 et ASEv2) avec une adresse IP virtuelle externe ou interne pour accéder à l’application. déploiement Hello avec une adresse IP externe est communément appelé ASE externe. version interne de Hello est appelée hello ASE d’équilibrage de charge interne, car elle utilise un équilibreur de charge interne (ILB). toolearn en savoir plus sur hello ASE d’équilibrage de charge interne, consultez [créer et utiliser un environnement app service Équilibrage de charge interne][MakeILBASE].

## <a name="create-a-web-app-in-an-ase"></a>Créer une application web dans un environnement ASE ##

toocreate une application web dans un environnement app service, vous utilisez hello même processus que lors de sa création normalement, mais avec quelques petites différences. Lorsque vous créez un plan App Service :

- Au lieu de choisir un emplacement géographique dans le toodeploy de votre application, vous désignez un environnement app service votre.
- Tous les plans App Service créés dans un environnement ASE doivent être dans un niveau tarifaire Isolé.

Si vous n’avez pas un environnement app service, vous pouvez en créer un en suivant les instructions de hello dans [créer un environnement App Service][MakeExternalASE].

toocreate une application web dans un environnement app service :

1. Sélectionnez **Nouveau** > **Web + Mobile** > **Web App**.

2. Entrez un nom pour l’application web de hello. Si vous avez sélectionné déjà un plan de Service d’applications dans un environnement app service, le nom de domaine hello pour une application hello reflète le nom de domaine hello Hello ASE.

    ![Sélection du nom de l’application web][1]

3. Sélectionnez un abonnement.

4. Entrez un nom pour un groupe de ressources, ou sélectionnez **utiliser l’existante** et sélectionnez une option dans la liste déroulante de hello.

5. Sélectionnez un plan App Service existant dans votre environnement ASE ou créez-en un en procédant comme suit :

    a. Sélectionnez **Créer**.

    b. Entrez le nom hello pour votre plan App Service.

    c. Sélectionnez votre ASE Bonjour **emplacement** liste déroulante.

    d. Sélectionnez un niveau tarifaire **Isolé**. Sélectionnez **Sélectionner**.

    e. Sélectionnez **OK**.
    
    ![Niveaux tarifaires isolés][2]

6. Sélectionnez **Créer**.

## <a name="how-scale-works"></a>Fonctionnement de la mise à l’échelle ##

Chaque application App Service s’exécute dans un plan App Service. modèle de conteneur Hello est environnements contiennent les plans App Service et les plans App Service applications. Lorsque vous faites évoluer une application, vous l’échelle hello plan App Service et par conséquent, l’échelle toutes les applications de hello en hello même plan.

Dans ASEv2, lorsque vous mettez à l’échelle d’un plan App Service, infrastructure de hello nécessité est automatiquement ajouté. A un certain délai tooscale opérations lors de l’infrastructure de hello est ajouté. ASEv1, infrastructure de hello nécessité doit être ajouté avant de créer ou de faire évoluer votre plan App Service. 

Dans mutualisée hello du Service d’applications, mise à l’échelle est généralement immédiate, car un pool de ressources est prête toosupport il. Dans un environnement ASE, il n’existe pas de mémoire tampon et les ressources peuvent être allouées en fonction des besoins.

Dans un environnement app service, vous pouvez monter too100 instances. Ces 100 instances peuvent toutes se trouver dans un seul plan App Service ou être distribuées dans plusieurs plans App Service.

## <a name="ip-addresses"></a>Adresses IP ##

Service d’applications a hello capacité tooallocate une application de tooan d’adresse IP dédiée. Cette fonctionnalité est disponible après avoir configuré une connexion SSL basé sur IP, comme décrit dans [lier un existant SSL certificat tooAzure web applications personnalisées][ConfigureSSL]. Toutefois, dans un environnement ASE, il existe une exception notable. Vous ne pouvez pas ajouter IP supplémentaires adresses toobe utilisé pour une connexion basée sur IP SSL dans un environnement app service Équilibrage de charge interne.

Dans ASEv1, vous devez les adresses IP tooallocate hello en tant que ressources avant de pouvoir les utiliser. Dans ASEv2, vous les utilisez à partir de votre application comme vous le feriez dans mutualisée de hello du Service d’applications. Il y a toujours une adresse de rechange dans ASEv2 des too30 des adresses IP. Chaque fois que vous en utilisez une, une autre est ajoutée afin qu’une adresse soit toujours disponible si besoin. Un délai d’attente de temps requises tooallocate une autre adresse IP, ce qui empêche l’ajout des adresses de suite.

## <a name="front-end-scaling"></a>Mise à l’échelle du serveur frontal ##

Dans ASEv2, lorsque vous faites évoluer vos plans de Service d’applications, travailleurs sont automatiquement ajoutés toosupport les. Chaque environnement ASE est créé avec deux serveurs frontaux. En outre, frontaux hello automatiquement à grande échelle à une fréquence d’un serveur frontal pour chaque instance de 15 dans vos plans de Service d’applications. Par exemple, si vous avez 15 instances, vous avez trois serveurs frontaux. Si vous redimensionnez des occurrences de too30, puis vous avez quatre front se termine et ainsi de suite.

Ce nombre de serveurs frontaux doit être plus que suffisant pour la plupart des scénarios. Toutefois, vous pouvez le faire évoluer à un rythme plus rapide. Vous pouvez modifier le rapport hello tooas faible comme un serveur frontal pour chaque cinq instances. Il existe des frais pour modifier le taux de hello. Pour en savoir plus, consultez [Tarification d’App Service][Pricing].

Ressources frontaux sont point de terminaison HTTP/HTTPS de hello pour hello ASE. Configuration frontale de hello par défaut, l’utilisation de mémoire par le serveur frontal est constamment environ 60 pour cent. Les charges de travail client ne s’exécutent pas sur un serveur frontal. Hello facteur clé pour un serveur frontal avec respect tooscale est à l’UC hello, qui vise principalement le trafic HTTPS.

## <a name="app-access"></a>Accès de l’application ##

Dans un environnement app service externe, domaine hello qui est utilisé lorsque vous créez des applications se mutualisée de hello du Service d’applications. Il inclut le nom hello Hello ASE. Pour plus d’informations sur la façon de toocreate ASE externes, consultez [créer un environnement App Service][MakeExternalASE]. nom de domaine Hello dans un environnement app service externe ressemble à *.&lt; asename&gt;. p.azurewebsites.net*. Par exemple, si votre ASE se nomme _externe-ase_ et vous hébergez une application appelée _contoso_ dans ce ASE, vous contacter à l’hello URL suivantes :

- contoso.external-ase.p.azurewebsites.net
- contoso.scm.external-ase.p.azurewebsites.net

URL de Hello contoso.scm.external-ase.p.azurewebsites.net est console de Kudu hello tooaccess utilisés ou pour la publication déployer votre application à l’aide de web. Pour plus d’informations sur la console de Kudu hello, consultez [console Kudu pour le Service d’applications Azure][Kudu]. Hello Kudu console offre une interface utilisateur web pour le débogage, le téléchargement de fichiers, modification des fichiers et bien plus encore.

Dans un environnement app service Équilibrage de charge interne, vous déterminez le domaine de hello au moment du déploiement. Pour plus d’informations sur comment toocreate un équilibrage de charge interne ASE, consultez [créer et utiliser un environnement app service Équilibrage de charge interne][MakeILBASE]. Si vous spécifiez le nom de domaine hello _ase.info de l’équilibrage de charge interne_, hello applications car ASE Utilisez ce domaine lors de la création de l’application. Pour l’application hello nommée _contoso_, hello URL sont :

- contoso.ilb-ase.info
- contoso.scm.ilb-ase.info

## <a name="publishing"></a>Publication ##

Comme avec mutualisée hello du Service d’applications, dans un environnement app service vous pouvez publier avec :

- Déploiement Web.
- FTP.
- Intégration continue.
- Glisser -déplacer dans la console Kudu hello.
- Un IDE tel que Visual Studio, Eclipse ou Intellij IDEA.

Avec un environnement app service externe, ces options de publication que se comportent hello identiques. Pour plus d’informations, consultez [Déploiement dans Azure App Service][AppDeploy]. 

Hello principale différence avec la publication est avec respect tooan ASE d’équilibrage de charge interne. Avec un environnement app service Équilibrage de charge interne, les points de terminaison de publication hello sont toutes disponibles uniquement par le biais de hello équilibrage de charge interne. Hello équilibrage de charge interne est sur une adresse IP privée dans un sous-réseau de ASE hello dans le réseau virtuel de hello. Si vous n’avez pas toohello d’accès réseau équilibrage de charge interne, vous ne pouvez pas publier toutes les applications de ce ASE. Comme indiqué dans [créer et utiliser un environnement app service Équilibrage de charge interne][MakeILBASE], vous devez tooconfigure DNS pour les applications de hello dans le système de hello. Qui inclut le point de terminaison SCM hello. S’ils ne sont pas définis correctement, vous ne pouvez pas publier. Votre IDE doivent également toohave toohello d’accès réseau équilibrage de charge interne dans l’ordre toopublish tooit directement.

Systèmes de l’élément de configuration basé sur Internet, tels que GitHub et Visual Studio Team Services ne fonctionnent pas avec un environnement app service Équilibrage de charge interne, car le point de terminaison publication hello n’est pas accessible d’Internet. Au lieu de cela, vous devez toouse un système de l’élément de configuration qui utilise un modèle d’extraction, telles que Dropbox.

les points de terminaison de publication Hello pour les applications dans un environnement app service Équilibrage de charge interne utilisent hello de domaine que hello avec QU'ASE d’équilibrage de charge interne a été créé. Vous pouvez le voir dans le profil de publication de l’application hello et dans le panneau de portail de l’application hello (dans **vue d’ensemble** > **Essentials** et également dans **propriétés**). 

## <a name="pricing"></a>Tarification ##

Hello tarification référence (SKU) appelé **isolé** a été créé pour une utilisation uniquement avec ASEv2. Tous les plans de Service d’applications qui sont hébergées dans ASEv2 se trouvent dans hello Isolated tarification référence (SKU). Les tarifs du plan App Service Isolé peuvent varier selon la région. 

En outre les plans de prix toohello pour votre application de Service, un taux plat pour ASE lui-même est. Hello forfaitaire ne changent pas avec une taille de votre ASE hello et paie pour infrastructure hello ASE au taux de 1 supplémentaires de mise à l’échelle par défaut frontal pour chaque 15 instances du plan App Service.  

Si le taux de mise à l’échelle par défaut hello du serveur 1 frontal pour chaque 15 instances du plan App Service n’est pas assez rapide, vous pouvez ajuster le ratio hello à laquelle les serveurs frontaux sont ajoutés ou hello taille de hello les serveurs frontaux.  Lorsque vous ajustez le ratio de hello ou la taille, vous payez pour cœurs frontal hello qui ne seront pas ajoutés par défaut.  

Par exemple, si vous ajustez hello échelle ratio too10, un serveur frontal est ajouté pour toutes les 10 instances dans vos plans de Service d’applications. forfait Hello couvre un taux de mise à l’échelle d’un serveur frontal pour chaque instance de 15. Avec un ratio de la montée en puissance de 10, vous payez un abonnement hello troisième serveur frontal qui a ajouté pour hello 10 instances du plan App Service. Vous n’avez pas besoin toopay pour qu’il lorsque vous atteignez 15 instances, car il a été ajouté automatiquement.

Si vous avez ajusté taille hello de cœurs de too2 hello frontaux mais ne s’ajustent pas ratio de hello puis payer pour hello cœurs supplémentaires.  Un environnement app service est créé avec 2 serveurs frontaux, donc, même sous le seuil mise à l’échelle automatique hello que vous payeriez pour 2 cœurs supplémentaires si vous augmentez hello taille too2 core frontaux.

Pour en savoir plus, consultez [Tarification d’App Service][Pricing].

## <a name="delete-an-ase"></a>Supprimer un environnement ASE ##

toodelete ASE : 

1. Utilisez **supprimer** haut hello hello **environnement App Service** panneau. 

2. Entrez le nom hello de votre tooconfirm ASE que vous souhaitez toodelete il. Lorsque vous supprimez un environnement app service, vous supprimez tout contenu hello qu’il contient également. 

    ![Suppression de ASE][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
