---
title: aaaHow tooConfigure un v1 environnement App Service
description: Configuration, gestion et la surveillance de hello environnement App Service v1
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>Configuration d’un environnement App Service Environment v1

> [!NOTE]
> Cet article porte sur hello environnement App Service v1.  Il existe une version plus récente de hello environnement App Service toouse plus facile et s’exécute sur une infrastructure plus puissante. toolearn plus d’informations sur la nouvelle version de hello commencent par Bonjour [Introduction toohello environnement App Service](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Vue d'ensemble
Globalement, un environnement Azure App Service se compose de plusieurs composants principaux :

* Ressources de calcul qui sont exécutent dans un environnement App Service de hello le service hébergé.
* Storage
* Une base de données
* Un réseau virtuel Azure (VNet) classique (V1) ou Resource Manager (V2) 
* Un sous-réseau avec service d’environnement App Service hébergé hello en cours d’exécution qu’il contient

### <a name="compute-resources"></a>Ressources de calcul
Vous utilisez les ressources de calcul hello pour vos pools de quatre ressources.  Chaque environnement App Service (ASE) possède un ensemble de serveurs frontaux et trois pools de travail possibles. Vous n’avez pas besoin toouse tous les pools de travail trois--si vous le souhaitez, vous pouvez utiliser uniquement un ou deux.

hôtes Hello dans les pools de ressources hello (frontaux et travailleurs) ne sont pas directement accessibles tootenants. Vous ne peut pas utiliser le protocole RDP (Remote Desktop) tooconnect toothem, modifier leur mise en service ou agir en tant qu’administrateur sur les.

Vous pouvez définir la taille et la quantité des pools de ressources. Dans un environnement App Service, vous disposez de quatre options de taille (P1 à P4). Pour plus de détails sur ces tailles et leur tarification, voir [Tarification de App Service](../app-service/app-service-value-prop-what-is.md).
La modification de la quantité de hello ou la taille est appelée une opération de mise à l’échelle.  Il ne peut y avoir qu’une seule opération de mise à l’échelle en cours à la fois.

**Avant la fin de**: frontaux hello est des points de terminaison HTTP/HTTPS de hello pour vos applications qui sont contenues dans votre ASE. Vous n’exécutez pas les charges de travail Bonjour frontaux.

* Un environnement App Service commence avec deux P2, ce qui est suffisant pour les charges de travail de développement et de test et les charges de travail de production de bas niveau. Nous recommandons vivement P3s tooheavy modérée pour les charges de travail de production.
* Pour les charges de production tooheavy modérée, nous vous recommandons que vous disposez d’au moins quatre P3s tooensure, il existe suffisamment frontaux en cours d’exécution lors de la maintenance planifiée. Les activités de maintenance planifiées interrompront un seul serveur frontal à la fois. Cela réduit la capacité globale disponible des serveurs frontaux pendant les activités de maintenance.
* Frontaux peut prendre jusqu'à tooan heure tooprovision. 
* Plus précisément de l’échelle, vous devez surveiller le pourcentage d’UC hello, pourcentage de mémoire et des métriques de demandes actives pour le pool frontal de hello. Si les pourcentages processeur ou mémoire hello supérieure à 70 % lors de l’exécution P3s, ajoutez plus frontaux. Si la moyenne de hello valeur des demandes actives too15, too20 000, 000 demandes par le serveur frontal, vous devez également ajouter plus frontaux. Hello objectif global est tookeep du processeur et mémoire au-dessous de 70 % et moyenne out toobelow 15 000 demandes par frontal lorsque vous exécutez P3s des demandes actives.  

**Travailleurs**: les workers hello sont où exécutent vos applications. Lorsque vous l’échelle votre application de Service plans qu’utilise des travailleurs dans hello associé pool de travail.

* L’ajout instantané de Workers n’est pas possible. Il peuvent prendre jusqu'à tooan heure tooprovision.
* Mise à l’échelle de taille hello d’une ressource de calcul pour n’importe quel pool prendra < 1 heure par domaine de mise à jour. Un environnement App Service contient 20 domaines de mise à jour. Si l’échelle de taille de calcul hello d’un pool de travail avec des instances de 10 too10 heures toocomplete peut prendre.
* Si vous modifiez la taille de hello hello des ressources de calcul qui sont utilisés dans un pool de travail, vous entraîne le démarrage à froid de hello les applications qui sont exécutent dans ce pool de travail.

Hello plus rapide toochange hello calculer la taille de la ressource d’un pool de travail qui n’exécute pas toutes les applications consiste à :

* Quantité de hello de travailleurs too2 à l’échelle.  échelle minimale de Hello la taille dans le portail de hello est 2. Elle prendra quelques minutes toodeallocate vos instances. 
* Sélectionnez la nouvelle taille de calcul hello et le nombre d’instances. À ce stade, il occupera too2 heures toocomplete.

Si vos applications nécessitent une plus grande taille de ressources de calcul, vous ne peut pas tirer parti des directives antérieures de hello. Au lieu de modifier la taille de hello du pool de travail hello qui héberge ces applications, vous pouvez remplir un autre pool de travail avec les travailleurs de taille de hello souhaité et déplacer vos applications sur toothat pool.

* Créer des instances supplémentaires de hello Hello nécessaire le calcul de taille dans un autre pool de travail. Cette opération prendra des tooan heure toocomplete.
* Réaffecter vos plans de Service d’applications qui hébergent des applications hello nécessitant un plus grand pool de travail toohello qui vient d’être configuré de taille. Il s’agit d’une opération rapide qui devrait prendre moins d’une minute toocomplete.  
* Échelle de pool de travail de première hello si vous n’avez plus besoin des instances inutilisées. Cette opération prend quelques minutes toocomplete.

**Échelle**: un des outils hello qui peuvent vous aider à toomanage votre consommation de ressources de calcul est échelle. Vous pouvez utiliser la mise à l’échelle pour les serveurs frontaux ou les pools de travail. Vous pouvez effectuer des opérations telles que de l’augmentation de vos instances de n’importe quel type de pool matin de hello et réduire les soir hello. Ou, par exemple, vous pouvez ajouter des instances lorsque le nombre de hello de threads de travail qui sont disponibles dans un pool de travail est inférieur à un certain seuil.

Si vous souhaitez que des règles de mise à l’échelle tooset autour des métriques de pool de ressources de calcul, puis conservez dans le temps de hello l’esprit que la mise en service le requiert. Pour plus d’informations sur l’échelle les environnements App Service, consultez [la mise à l’échelle de tooconfigure dans un environnement App Service][ASEAutoscale].

### <a name="storage"></a>Storage
Chaque ASE est configuré avec 500 Go de stockage. Cet espace est utilisé dans toutes les applications hello Bonjour ASE. Cet espace de stockage est une partie de hello ASE et actuellement ne peut pas être commuté toouse votre espace de stockage. Si vous apportez des ajustements tooyour réseau virtuel routage ou sécurité, vous devez toostill autoriser l’accès tooAzure stockage--ou hello ASE ne peut pas fonctionner.

### <a name="database"></a>Base de données
base de données Hello conserve des informations de hello qui définit l’environnement de hello, ainsi que hello plus d’informations sur les applications de hello qui s’exécutent dans celui-ci. Il s’agit trop une partie de hello détenue par Azure l’abonnement. Il n’est pas quelque chose que vous avez un toomanipulate direct de capacité. Si vous apportez des ajustements tooyour réseau virtuel routage ou sécurité, vous devez toostill autoriser l’accès tooSQL Azure--ou hello ASE ne peut pas fonctionner.

### <a name="network"></a>Réseau
Hello réseau virtuel qui est utilisé avec votre ASE peut être une que vous avez effectuées lors de la création de hello ASE ou que vous avez apportées à l’avance. Lorsque vous créez un sous-réseau de hello lors de la création de ASE, il force toobe hello ASE Bonjour même groupe de ressources en tant que réseau virtuel de hello. Si vous avez besoin de groupe de ressources hello utilisé par votre toobe ASE différent de celui de votre réseau virtuel, vous devez toocreate votre ASE à l’aide d’un modèle de gestionnaire de ressources.

Il existe certaines restrictions sur le réseau virtuel hello qui est utilisé pour un environnement app service :

* réseau virtuel de Hello doit être un réseau virtuel régional.
* Il doit y toobe un sous-réseau avec 8 ou plusieurs adresses où hello ASE est déployé.
* Après qu’un sous-réseau est utilisé toohost ASE, hello plage d’adresses hello sous-réseau ne peut pas être modifié. Pour cette raison, nous vous recommandons de que ce sous-réseau hello contient au moins de 64 adresses tooaccommodate toute croissance ASE.
* Il peut y avoir rien d’autre dans le sous-réseau de hello mais hello ASE.

Contrairement au service hello hébergé contenant hello ASE, hello [réseau virtuel] [ virtualnetwork] et le sous-réseau sont sous contrôle de l’utilisateur.  Vous pouvez administrer votre réseau virtuel via hello l’interface utilisateur de réseau virtuel ou de PowerShell.  Un ASE peut être déployé dans un réseau virtuel classique ou Resource Manager.  portail de Hello et l’expérience de l’API diffèrent légèrement entre classique et le Gestionnaire de ressources VNets mais hello expérience de ASE est hello identiques.

Hello réseau virtuel qui est utilisé toohost ASE peut utiliser deux adresses RFC1918 IP privées, ou elle peut utiliser des adresses IP publiques.  Si vous souhaitez toouse une plage IP qui n’est pas couverte par RFC1918 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16), vous devez toocreate votre toobe de réseau virtuel et le sous-réseau utilisé par votre ASE avant la création de ASE.

Étant donné que cette fonctionnalité place hello du Service d’applications Azure dans votre réseau virtuel, cela signifie que vos applications qui sont hébergées dans votre ASE peuvent désormais accéder aux ressources qui sont effectuées directement disponibles via ExpressRoute ou des réseaux privés virtuels (VPN) site à site. mise en réseau fonctionnalités tooaccess ressources disponibles toohello réseau virtuelles supplémentaires qui héberge votre environnement App Service ne nécessitent pas Hello les applications qui se trouvent dans votre environnement App Service. Cela signifie que vous n’avez pas besoin toouse intégration de réseau virtuel ou des connexions hybrides tooget tooresources dans ou réseau virtuel de tooyour connecté. Vous pouvez toujours utiliser les deux de ces fonctionnalités se tooaccess des ressources dans les réseaux qui ne sont pas connectés tooyour des réseaux virtuels.

Par exemple, vous pouvez utiliser toointegrate de l’intégration de réseau virtuel avec un réseau virtuel qui se trouve dans votre abonnement, mais n’est pas connecté toohello réseau virtuel figurant dans votre ASE. Vous pouvez toujours également utiliser les ressources de tooaccess connexions hybrides qui se trouvent dans d’autres réseaux, comme vous pouvez normalement.  

Si vous n’avez pas votre réseau virtuel configuré avec un VPN ExpressRoute, vous devez connaître certaines des besoins de routage hello qui dispose d’un environnement app service. Certaines configurations d’itinéraire défini par l’utilisateur ne sont pas compatibles avec un ASE. Pour plus de détails concernant l’exécution d’un ASE dans un réseau virtuel avec ExpressRoute, voir [Exécution d’un environnement App Service dans un réseau virtuel avec ExpressRoute][ExpressRoute].

#### <a name="securing-inbound-traffic"></a>Sécurisation du trafic entrant
Il existe deux méthodes principales toocontrol entrants ASE tooyour de trafic.  Vous pouvez utiliser Groups(NSGs) de sécurité réseau toocontrol le IP adresses peuvent accéder à votre ASE comme décrit ici [toocontrol comment le trafic dans un environnement App Service entrant](app-service-app-service-environment-control-inbound-traffic.md) et vous pouvez également configurer votre ASE avec une charge interne Balancer(ILB).  Ces fonctionnalités peuvent également être utilisées ensemble si vous souhaitez accéder toorestrict à l’aide de groupes de sécurité réseau tooyour ASE d’équilibrage de charge interne.

Lorsque vous créez un ASE, une adresse IP virtuelle sera créée dans votre réseau virtuel.  Il existe deux types d’adresses IP virtuelles : internes et externes.  Lorsque vous créez un ASE avec une adresse IP virtuelle externe, les applications dans votre ASE sont accessibles via une adresse IP Internet routable. Si vous optez pour une adresse interne, votre ASE sera configuré avec un ILB et ne sera pas directement accessible par Internet.  Un ILB ASE nécessite malgré tout une adresse IP virtuelle externe, mais celle-ci est utilisée uniquement pour l’accès lié à la gestion et à la maintenance Azure.  

Lors de la création de l’équilibrage de charge interne ASE vous fournissez le sous-domaine hello utilisé par hello ASE d’équilibrage de charge interne et vous devez toomanage votre propre DNS pour le sous-domaine hello que vous spécifiez.  Étant donné que vous définissez le nom de sous-domaine hello, vous devez également les certificats de hello toomanage utilisé pour l’accès HTTPS.  Après ASE création, que vous êtes invité certificat de hello tooprovide.  toolearn en savoir plus sur la création et l’utilisation d’un environnement app service Équilibrage de charge interne lire [à l’aide d’un équilibreur de charge interne avec un environnement App Service][ILBASE]. 

## <a name="portal"></a>Portail
Vous pouvez gérer et surveiller votre environnement App Service à l’aide de hello UI Bonjour portail Azure. Si vous avez un environnement app service, vous êtes probablement toosee hello symbole du Service d’applications sur la barre latérale. Ce symbole est utilisé toorepresent App Service environnements Bonjour portail Azure :

![Symbole d’environnement App Service][1]

tooopen hello d’interface utilisateur qui répertorie tous les environnements de Service de votre application, vous pouvez utiliser des hello icône ou sur les chevrons hello select (« > » symbole) bas hello hello encadré tooselect environnements de Service d’application. En sélectionnant une des ASEs hello répertoriés, vous ouvrez hello l’interface utilisateur qui est utilisé toomonitor et les gérer.

![Interface utilisateur de surveillance et de gestion de votre environnement App Service][2]

Ce premier panneau présente certaines propriétés de votre ASE avec un graphique de mesures par pool de ressources. Certaines des propriétés hello qui figurent dans hello **Essentials** bloc sont également des liens hypertexte qui seront ouvre et le panneau hello qui lui est associé. Par exemple, vous pouvez sélectionner hello **réseau virtuel** tooopen nom de l’interface utilisateur de hello associé avec un réseau virtuel hello votre ASE s’exécutant en. Les **plans App Service** et les **applications** ouvrent des panneaux qui répertorient les éléments figurant dans votre ASE.  

### <a name="monitoring"></a>Surveillance
graphiques de Hello autoriser toosee diverses mesures de performances dans chaque pool de ressources. Pour le pool frontal de hello, vous pouvez surveiller hello moyenne du processeur et la mémoire. Pour les pools de travail, vous pouvez surveiller la quantité hello est utilisée et quantité hello n’est disponible.

Plusieurs plans de faire du Service d’applications utilisent des travailleurs hello dans un pool de travail. charge de travail Hello n’est pas distribuée Bonjour même mode comme avec les serveurs frontaux hello, afin de l’utilisation de l’UC et mémoire hello ne fournissent une grande partie de façon hello d’informations utiles. Il est plus important tootrack le nombre de threads de travail que vous avez utilisés et sont disponible, en particulier si vous gérez ce système pour d’autres toouse.  

Vous pouvez également utiliser toutes les métriques hello qui peuvent être suivis dans tooset de graphiques hello des alertes. Configuration des alertes ici works hello identiques par ailleurs dans le Service d’applications. Vous pouvez définir une alerte à partir de deux hello **alertes** l’interface utilisateur dans le cadre ou à partir de l’exploration des mesures de l’interface utilisateur et en sélectionnant **ajouter une alerte**.

![Interface utilisateur Mesures][3]

métriques Hello simplement décrits sont des mesures d’environnement App Service hello. Il existe également des métriques qui sont disponibles à hello au niveau du plan App Service. C’est là que la surveillance de l’utilisation de l’UC et de la mémoire se révèle intéressante.

Dans un environnement app service, tous les hello que plans de Service d’applications sont des plans de Service d’applications dédiés. Que signifie que hello seules les applications qui sont exécutent sur hello hôtes allouées toothat plan App Service sont des applications de hello dans ce plan App Service. toosee les détails de votre plan de Service de l’application, afficher à partir des listes de hello hello ASE UI ou à partir de votre plan App Service **plans de Service d’applications Parcourir** (qui répertorie tous les).   

### <a name="settings"></a>Paramètres
Dans le panneau de hello ASE, il y a un **paramètres** section qui contient plusieurs fonctions importantes :

**Paramètres** > **propriétés**: hello **paramètres** panneau s’ouvre automatiquement lorsque vous faites apparaître votre panneau ASE. Hello est haut **propriétés**. Un certain nombre d’éléments ici toowhat redondant, vous voyez dans **Essentials**, mais ce qui est très utile est **adresse IP virtuelle**, ainsi que **des adresses IP sortant**.

![Panneau Paramètres et Propriétés][4]

**Paramètres** > **Adresses IP** : une adresse IP SSL est nécessaire lorsque vous créez une application IP SSL (Secure Sockets Layer) dans votre ASE. Dans l’ordre tooobtain une, votre ASE doit adresses IP SSL qu’il possède et qui peuvent être alloués. Lorsqu’un ASE est créé, il dispose d’une adresse IP SSL unique à cette fin, mais vous pouvez en ajouter d’autres. Il existe un coût pour SSL IP supplémentaire, les adresses, comme indiqué dans [tarification du Service d’applications] [ AppServicePricing] (dans la section hello sur les connexions SSL). les prix supplémentaires Hello sont hello prix de SSL IP.

**Paramètres** > **de Pool frontal** / **Pools de travail**: chacune de ces panneaux de pool de ressources fournit des informations de toosee de capacité de hello uniquement sur ce pool de ressources , en outre tooproviding contrôle l’échelle de toofully ce pool de ressources.  

Panneau de base Hello pour chaque pool de ressources fournit un graphique avec métriques pour ce pool de ressources. Tout comme avec des graphiques hello dans Panneau de ASE hello, vous pouvez aller dans le graphique de hello et configurer des alertes comme vous le souhaitez. Définition d’une alerte à partir du Panneau de ASE hello pour un pool de ressources spécifique hello même chose que de pool de ressources hello. À partir du pool de travail hello **paramètres** panneau, vous avez hello de tooall d’accès aux applications ou des plans de Service d’applications qui s’exécutent dans ce pool de travail.

![Interface utilisateur Paramètres du pool de travail][5]

### <a name="portal-scale-capabilities"></a>Fonctionnalités de mise à l’échelle du portail
Il existe trois opérations de mise à l’échelle :

* Modification du nombre de hello de Bonjour ASE des adresses IP qui sont disponibles pour l’utilisation de SSL IP.
* Modification de taille hello hello de ressource de calcul qui est utilisée dans un pool de ressources.
* Modification du nombre de hello de ressources de calcul qui sont utilisés dans un pool de ressources manuellement ou à l’échelle automatique.

Dans le portail hello, Voici trois façons toocontrol le nombre de serveurs que vous avez dans votre pools de ressources :

* Une opération de mise à l’échelle du serveur lame ASE principal hello haut hello. Vous pouvez apporter à l’échelle de plusieurs modifications de configuration toohello frontaux et des pools de travail. Toutes les modifications sont appliquées en une seule opération.
* Une opération de mise à l’échelle manuelle à partir du pool de ressources individuels hello **échelle** panneau, ce qui se trouve sous **paramètres**.
* Échelle que vous avez configuré à partir du pool de ressources individuels hello **échelle** panneau.

opération de mise à l’échelle toouse hello dans Panneau de ASE hello, faites glisser la quantité de toohello curseur hello souhaitées, puis enregistrez-les. Cette interface utilisateur prend également en charge la modification de taille de hello.  

![Interface utilisateur Mise à l’échelle][6]

fonctionnalités de manuel ou de mise à l’échelle de hello dans un pool de ressources spécifique toouse accédez trop**paramètres** > **de Pool frontal** / **Pools de travail** en tant que approprié. Puis ouvrir le pool de hello que vous souhaitez toochange. Accédez trop**paramètres** > **monter en charge** ou **paramètres** > **mise à l’échelle**. Hello **monter en charge** panneau vous permet de quantité d’instance toocontrol. **Mise à l’échelle** vous permet de taille de la ressource toocontrol.  

![Interface utilisateur Paramètres de mise à l’échelle][7]

## <a name="fault-tolerance-considerations"></a>Éléments à prendre en compte en matière de tolérance de pannes
Vous pouvez configurer un toouse environnement App Service des ressources de calcul total too55. Ces 55 des ressources de calcul, 50 uniquement peut être utilisé toohost les charges de travail. raison Hello est double. Il existe au minimum 2 ressources de calcul frontales,  Cela laisse d’allocation de pool de travail too53 toosupport hello. Commande tooprovide une tolérance de panne, vous devez toohave une ressource de calcul supplémentaire est allouée en fonction de toohello suivant les règles :

* Chaque pool de travail doit au moins 1 ressource de calcul supplémentaires qui n’est pas disponible toobe affecté une charge de travail.
* Lorsque la quantité de hello des ressources de calcul dans un pool de travail dépasse une certaine valeur, une autre ressource de calcul est requise pour la tolérance de panne. Cela ne vaut pas hello dans le pool de frontal hello.

Au sein d’un pool de travail unique, les exigences de tolérance de pannes de hello sont que pour une valeur donnée de X ressources affectées pool de travail tooa :

* Si X est compris entre 2 et 20, quantité hello utilisable des ressources de calcul que vous pouvez utiliser pour les charges de travail est x-1.
* Si X est compris entre 21 et 40, quantité hello utilisable des ressources de calcul que vous pouvez utiliser pour les charges de travail est X-2.
* Si X est entre 41 et 53, quantité hello utilisable des ressources de calcul que vous pouvez utiliser pour les charges de travail est X-3.

encombrement minimal de Hello a 2 serveurs frontaux et 2 workers.  Avec hello ci-dessus ensuite les instructions, voici quelques exemples tooclarify :  

* Si vous avez 30 travailleurs dans un pool unique, 28 d'entre eux peut être utilisé toohost les charges de travail.
* Si vous avez 2 workers dans un pool unique, 1 peut être utilisé toohost les charges de travail.
* Si vous disposez de 20 threads de travail dans un pool unique, 19 peut être utilisé toohost les charges de travail.  
* Si vous avez une 21 workers dans un pool unique, puis toujours de 19 peut être utilisé toohost les charges de travail.  

aspect d’une tolérance de pannes Hello est important, mais vous devez tookeep il à l’esprit lorsque vous mettez à l’échelle au-dessus de certains seuils. Si vous souhaitez tooadd plus la capacité de 20 instances, puis accédez too22 ou une version ultérieure, car il est 21 n’ajoute pas les plus de capacité. Hello que vaut excédant 40, où le nombre suivant hello qui ajoute de la capacité est 42.  

## <a name="deleting-an-app-service-environment"></a>Suppression d'un environnement App Service
Si vous voulez toodelete un environnement App Service, puis utilisez simplement hello **supprimer** action haut hello du panneau d’environnement App Service hello. Lorsque vous faites cela, vous serez nom de hello tooenter demandée de votre tooconfirm environnement App Service que vous voulez réellement toodo cela. Notez que lorsque vous supprimez un environnement App Service, vous supprimez tout contenu hello qu’il contient également.  

![Interface utilisateur Supprimer un environnement App Service][9]  

## <a name="getting-started"></a>Prise en main
tooget démarré avec les environnements de Service d’application, consultez [comment toocreate un environnement App Service](app-service-web-how-to-create-an-app-service-environment.md).

Pour plus d’informations sur la plateforme Azure App Service de hello, consultez [Azure App Service](../app-service/app-service-value-prop-what-is.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
