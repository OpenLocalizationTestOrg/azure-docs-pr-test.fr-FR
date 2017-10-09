---
title: "aaaGeo échelle distribuées avec les environnements de Service d’application"
description: "Découvrez comment toohorizontally l’échelle d’applications à l’aide de la distribution géographique avec Traffic Manager et les environnements de Service d’application."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: c1b05ca8-3703-4d87-a9ae-819d741787fb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: stefsch
ms.openlocfilehash: 9b441f637d8b7f679b3d83240baf99b8ee57e8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="geo-distributed-scale-with-app-service-environments"></a>Mise à l’échelle géolocalisée avec les environnements App Service
## <a name="overview"></a>Vue d'ensemble
Scénarios d’application qui exigent une très grande échelle peuvent dépasser hello calcul capacité disponible tooa seul déploiement de ressources d’une application.  À titre d’exemple, les applications de vote, les événements sportifs et les programmes de divertissement télévisés sont des scénarios qui fonctionnent à très grande échelle. Les besoins à grande échelle peuvent être remplies par l’évolution horizontale des applications, avec plusieurs déploiements d’applications effectués au sein d’une seule région, ainsi qu’entre les régions, les exigences de charge extrême toohandle.

Les environnements App Service sont une plate-forme idéale pour l’évolution horizontale.  Une fois qu’une configuration de l’environnement App Service a été sélectionnée qui peut prendre en charge un taux de demandes connus, les développeurs peuvent déployer des environnements de Service application supplémentaires dans « découpage » de manière tooattain une capacité de charge maximale de votre choix.

Par exemple une application en cours d’exécution sur une configuration de l’environnement App Service a été testée toohandle 20 Ko des demandes par seconde (RPS).  Si la charge de pointe de votre choix hello capacité est 100 Ko RPS, environnements de Service d’application cinq (5) peut être créés et configuré tooensure hello application peut gérer hello maximale prévue de charge.

Étant donné que les clients en général les applications à l’aide d’un domaine personnalisé (ou personnel), les développeurs doivent accéder à une application toodistribute de façon demandes sur toutes les instances d’environnement App Service hello.  Un tooaccomplish excellent moyen il s’agit de tooresolve hello personnalisé de domaine en utilisant un [profil Azure Traffic Manager][AzureTrafficManagerProfile].  Hello Traffic Manager profil peut être configuré toopoint tous les hello environnements de Service d’application individuels.  Traffic Manager gérera automatiquement à la distribution des clients dans l’ensemble de hello Qu'environnements de Service d’application basées sur les paramètres dans le profil Traffic Manager hello d’équilibrage de charge de hello.  Cette approche fonctionne indépendamment de tous les environnements de Service d’application hello sont déployés dans une seule région Azure ou déployés dans le monde dans plusieurs régions Azure.

En outre, étant donné que les clients accéder aux applications via le domaine personnel de hello, les clients ne savent pas nombre hello des environnements de Service d’application une application en cours d’exécution.  Par conséquent les développeurs peuvent rapidement et facilement ajouter et supprimer des environnements App Service en fonction de la charge du trafic observée.

diagramme conceptuel de Hello ci-dessous illustre une application horizontalement répartie sur trois environnements de Service d’application au sein d’une seule région.

![Architecture conceptuelle][ConceptualArchitecture] 

reste Hello de cette rubrique décrit les étapes hello liés à la configuration d’une topologie distribuée pour l’application d’exemple hello à l’aide de plusieurs environnements de Service d’application.

## <a name="planning-hello-topology"></a>Planification de la topologie de hello
Avant la création d’un encombrement de l’application distribuée, il vous aide à toohave quelques informations pièces avance.

* **Domaine personnalisé pour une application hello :** ce qui est le nom de domaine personnalisé hello que les clients utilisent tooaccess hello application ?  Pour un domaine personnalisé d’hello application exemple hello nom est *www.scalableasedemo.com*
* **Domaine Traffic Manager :** toobe choisi lors de la création a besoin d’un nom de domaine un [profil Azure Traffic Manager][AzureTrafficManagerProfile].  Ce nom sera combiné avec hello *trafficmanager.net* suffixe tooregister une entrée de domaine qui est gérée par le Gestionnaire de trafic.  Pour l’application d’exemple hello, est choisi de nom hello *évolutive ase-démonstration*.  Par conséquent le nom de domaine complet de hello est géré par le Gestionnaire de trafic est *demo.trafficmanager.net-ase évolutive*.
* **Stratégie de mise à l’échelle l’encombrement application hello :** sera l’impact des applications hello distribué sur plusieurs environnements de Service d’application dans une seule région ?  Plusieurs régions ?  Une combinaison des deux approches ?  décision de Hello doit être basée sur les attentes d’où le trafic de client proviennent, ainsi que la manière d’autres hello bien d’une application prenant en charge l’infrastructure principale peut mettre à l’échelle.  Par exemple, avec une application à 100 % sans état, une application peut être adaptée à très grande échelle à l’aide d’une combinaison de plusieurs environnements App Service, puis multipliée par les environnements App Service déployés dans plusieurs régions Azure.  Avec les régions Azure publique 15 + toochoose disponible à partir de, les clients peuvent générer réellement un encombrement de l’application d’une évolutivité à l’échelle mondiale.  Pour l’application d’exemple hello utilisée pour cet article, trois environnements de Service d’application ont été créés dans une seule région Azure (Amérique du Sud).
* **Convention de dénomination pour hello les environnements App Service :** chaque environnement App Service requiert un nom unique.  Au-delà d’un ou deux environnements de Service d’application, il est utile toohave une convention d’affectation de noms toohelp identifier chaque environnement App Service.  Pour un exemple d’application hello une convention d’affectation de noms simple a été utilisée.  Hello noms des environnements de Service d’application hello trois sont *fe1ase*, *fe2ase*, et *fe3ase*.
* **Convention d’affectation de noms pour les applications de hello :** étant donné que plusieurs instances de l’application hello seront déployés, un nom est requis pour chaque instance de l’application hello déployé.  Une fonctionnalité peu connue, mais très pratique des environnements de Service d’application est que hello même nom d’application peut être utilisé dans différents environnements de Service d’application.  Étant donné que chaque environnement App Service a un suffixe de domaine unique, les développeurs peuvent choisir d’utiliser toore hello exacte même nom de l’application dans chaque environnement.  Par exemple, un développeur peut avoir des applications nommées comme suit : *myapp.foo1.p.azurewebsites.net*, *myapp.foo2.p.azurewebsites.net*, *myapp.foo3.p.azurewebsites.net*, etc.  Pour un exemple d’application hello bien que chaque instance de l’application a également un nom unique.  Hello application les noms d’instance utilisés sont *webfrontend1*, *webfrontend2*, et *webfrontend3*.

## <a name="setting-up-hello-traffic-manager-profile"></a>Configuration de hello profil Traffic Manager
Une fois que plusieurs instances d’une application sont déployés sur plusieurs environnements de Service d’application, les instances d’application individuels hello peuvent être inscrits avec Traffic Manager.  Pour l’application d’exemple hello Gestionnaire de trafic profil est nécessaire pour *demo.trafficmanager.net-ase évolutive* qui peut acheminer les instances d’application clients tooany Hello suivant déployé :

* **webfrontend1.fe1ase.p.azurewebsites.NET :** une instance de l’application d’exemple hello déployée sur hello premier environnement App Service.
* **webfrontend2.fe2ase.p.azurewebsites.NET :** une instance de l’application d’exemple hello déployée sur hello deuxième environnement App Service.
* **webfrontend3.fe3ase.p.azurewebsites.NET :** une instance de l’application d’exemple hello déployée sur hello troisième environnement App Service.

Hello tooregister de façon plus simple de plusieurs services d’application Azure points de terminaison, s’exécutant tous dans hello **même** région Azure, est par hello Powershell [prise en charge Azure Resource Manager Traffic Manager] [ ARMTrafficManager].  

première étape de Hello est toocreate un profil Traffic Manager de Azure.  code Hello ci-dessous montre comment le profil de hello a été créé pour hello, exemple d’application :

    $profile = New-AzureTrafficManagerProfile –Name scalableasedemo -ResourceGroupName yourRGNameHere -TrafficRoutingMethod Weighted -RelativeDnsName scalable-ase-demo -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"

Notez comment hello *RelativeDnsName* paramètre a été défini trop*évolutive ase-démonstration*.  Cela est hello comment de nom de domaine *demo.trafficmanager.net-ase évolutive* est créé et associé à un profil Traffic Manager.

Hello *TrafficRoutingMethod* paramètre définit la stratégie Traffic Manager utilisera toodetermine comment toospread client charger dans l’ensemble de points de terminaison disponibles hello d’équilibrage de charge hello.  Dans cette hello exemple *Weighted* méthode a été choisie.  Ainsi, les demandes des clients sont réparties entre tous points de terminaison d’application hello inscrit en fonction du poids relatif de hello associés à chaque point de terminaison. 

Avec profil hello créé, chaque instance de l’application est ajoutée toohello profil comme un point de terminaison Azure natif.  code Hello ci-dessous extrait d’une application web de référence tooeach front-end, puis ajoute chaque application en tant qu’un point de terminaison Traffic Manager au moyen de hello *TargetResourceId* paramètre.

    $webapp1 = Get-AzureRMWebApp -Name webfrontend1
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend1 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp1.Id –EndpointStatus Enabled –Weight 10

    $webapp2 = Get-AzureRMWebApp -Name webfrontend2
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend2 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp2.Id –EndpointStatus Enabled –Weight 10

    $webapp3 = Get-AzureRMWebApp -Name webfrontend3
    Add-AzureTrafficManagerEndpointConfig –EndpointName webfrontend3 –TrafficManagerProfile $profile –Type AzureEndpoints -TargetResourceId $webapp3.Id –EndpointStatus Enabled –Weight 10

    Set-AzureTrafficManagerProfile –TrafficManagerProfile $profile

Notez la façon dont un appel est trop*Add-AzureTrafficManagerEndpointConfig* pour chaque instance d’application individuels.  Hello *TargetResourceId* dans chaque commande Powershell fait référence à une des instances d’application déployée trois hello.  Hello profil Traffic Manager est répartir la charge parmi les trois points de terminaison inscrits dans le profil hello.

Tous les hello trois points de terminaison utilisent hello même valeur (10) pour hello *poids* paramètre.  Ainsi, Traffic Manager répartit les demandes clients entre les trois instances d’application de façon relativement uniforme. 

## <a name="pointing-hello-apps-custom-domain-at-hello-traffic-manager-domain"></a>Pointant vers un domaine personnalisé de l’application hello en hello domaine Traffic Manager
dernière étape Hello nécessaire est domaine personnalisé de hello toopoint de l’application hello au domaine Traffic Manager de hello.  Pour un exemple d’application hello, cela signifie pointant *www.scalableasedemo.com* à *demo.trafficmanager.net-ase évolutive*.  Cette étape doit toobe s’est terminée avec des domaines hello qui gère le domaine personnalisé de hello.  

À l’aide des outils de gestion de domaine de votre bureau d’enregistrement, un toobe de besoins d’enregistrements CNAME créé le domaine personnalisé hello points au domaine Traffic Manager de hello.  image Hello ci-dessous montre un exemple de cette configuration de CNAME :

![Enregistrement CNAME pour le domaine personnalisé][CNAMEforCustomDomain] 

Bien que non couvertes dans cette rubrique, souvenez-vous que chaque instance d’application individuels doit enregistré avec lui aussi bien du domaine personnalisé hello toohave.  Dans le cas contraire, si l’instance d’application tooan rend une demande et application hello n’a pas de nom de domaine personnalisé hello enregistré avec l’application hello, demande de hello échoue.  

Dans cette hello exemple domaine personnalisé est *www.scalableasedemo.com*, et chaque instance d’application hello de domaine personnalisé associé.

![Domaine personnalisé][CustomDomain] 

Pour un récapitulatif d’inscription d’un domaine personnalisé avec les applications de Service d’applications Azure, consultez hello l’article suivant [l’enregistrement de domaines personnalisés][RegisterCustomDomain].

## <a name="trying-out-hello-distributed-topology"></a>La tentative de hello distribués topologie
Bonjour résultat final de la configuration de Traffic Manager et DNS hello est que les demandes de *www.scalableasedemo.com* transite hello suivant séquence :

1. Un navigateur ou un périphérique effectue une recherche DNS sur *www.scalableasedemo.com*
2. Hello entrée CNAME auprès de domaines hello provoque hello DNS recherche toobe redirigé tooAzure Traffic Manager.
3. Une recherche DNS est effectuée *demo.trafficmanager.net-ase évolutive* sur l’un des serveurs de Azure DNS Traffic Manager hello.
4. Stratégie d’équilibrage de charge hello (hello *TrafficRoutingMethod* paramètre utilisé précédemment lors de la création du profil Traffic Manager hello), Traffic Manager va sélectionner de hello configuré des points de terminaison et retourne hello de ce nom de domaine complet navigateur de toohello de point de terminaison ou l’appareil.
5. Hello, nom de domaine complet du point de terminaison hello étant hello les Url d’une instance de l’application en cours d’exécution sur un environnement App Service, hello navigateur ou l’appareil vous demande un serveur DNS de Microsoft Azure tooresolve hello adresse tooan de nom de domaine complet. 
6. Hello navigateur ou l’appareil envoie hello HTTP/demande toohello adresse IP.  
7. demande de Hello arriverez à une des instances d’application hello en cours d’exécution sur l’un des hello environnements de Service d’application.

image de la console ci-dessous Hello affiche une recherche DNS pour domaine personnalisé avec succès résolution tooan application instance l’application d’exemple hello en cours d’exécution sur l’un de l’exemple hello trois environnements de Service d’application (dans ce cas hello seconde de hello trois environnements de Service d’application) :

![Recherche DNS][DNSLookup] 

## <a name="additional-links-and-information"></a>Informations et liens supplémentaires
Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

Documentation sur hello Powershell [prise en charge Azure Resource Manager Traffic Manager][ARMTrafficManager].  

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[AzureTrafficManagerProfile]: ../traffic-manager/traffic-manager-manage-profiles.md
[ARMTrafficManager]: ../traffic-manager/traffic-manager-powershell-arm.md
[RegisterCustomDomain]: app-service-web-tutorial-custom-domain.md


<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-geo-distributed-scale/ConceptualArchitecture-1.png
[CNAMEforCustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CNAMECustomDomain-1.png
[DNSLookup]:  ./media/app-service-app-service-environment-geo-distributed-scale/DNSLookup-1.png
[CustomDomain]:  ./media/app-service-app-service-environment-geo-distributed-scale/CustomDomain-1.png 
