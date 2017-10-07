---
title: "AAA « connexions hybrides de Service d’applications Azure | Documents Microsoft »"
description: "Comment toocreate et l’utilisation des ressources tooaccess connexions hybrides dans des réseaux hétérogènes"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 66774bde-13f5-45d0-9a70-4e9536a4f619
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/22/2017
ms.author: ccompy
ms.openlocfilehash: 61d58068ab0a7c803019e3f0e92bde4273d1a053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-hybrid-connections"></a>Connexions hybrides d’Azure App Service #

## <a name="overview"></a>Vue d'ensemble ##

Connexions hybrides est un service dans Azure ainsi que sur une fonctionnalité Bonjour Azure App Service.  En tant que service, il a utilisation et fonctionnalités au-delà de celles qui sont exploitées dans hello du Service d’applications Azure.  toolearn plus d’informations sur les connexions hybrides et leur utilisation en dehors de hello Azure App Service, vous pouvez démarrer ici, [relais connexions hybrides][HCService]

Hello du Service d’applications Azure, les connexions hybrides peuvent être des ressources d’application tooaccess utilisés dans d’autres réseaux. Il fournit l’accès à partir de votre point de terminaison d’application app tooan.  Elle ne permet pas une autre fonctionnalité tooaccess votre application.  Servent de hello du Service d’applications, chaque connexion hybride met en corrélation tooa TCP hôte et le port une combinaison unique.  Cela signifie que ce point de terminaison de connexion hybride hello peut être n’importe quel système d’exploitation et n’importe quelle application fourni que vous atteignez un port d’écoute TCP. Connexions hybrides ne pas connaître ou en charge le protocole d’application hello est ou que vous accédez à.  Elles fournissent simplement un accès réseau.  


## <a name="how-it-works"></a>Fonctionnement ##
fonctionnalité de connexions hybrides Hello se compose de deux appels sortants tooService Bus Relay.  Il existe une connexion à partir d’une bibliothèque sur l’hôte hello où votre application s’exécute dans le service de l’application hello et puis, il existe une connexion à partir de relais de Bus tooService hello Manager(HCM) de connexion hybride.  Hello HCM est un service de relais que vous déployez au sein de l’hébergement de réseau hello 

Via hello deux connexions jointes votre application a un tooa de tunnel TCP fixe association de port de l’hôte : hello autre côté de hello HCM.  connexion de Hello utilise TLS 1.2 pour la sécurité et des clés SAP pour l’authentification/autorisation.    

![][1]

Lorsque votre application effectue une requête DNS qui correspond à un point de terminaison de connexion hybride de configurer, puis le trafic TCP sortant hello sera redirigé vers le bas de la connexion hybride hello.  

> [!NOTE]
> Cela signifie que vous devez essayer tooalways utilisez un nom DNS pour votre connexion hybride.  Certains logiciels client n’effectue une recherche DNS si le point de terminaison hello utilise une adresse IP à la place.
>
>

Il existe deux types de connexions hybrides, les connexions hybrides nouvelle hello qui sont proposées en tant que service sous Azure relais et hello les anciennes connexions hybrides de BizTalk.  Hello les anciennes connexions hybrides de BizTalk sont visées tooas classique connexions hybrides dans le portail de hello.  Plus d’informations sur celles-ci sont fournies plus loin dans ce document.

### <a name="app-service-hybrid-connection-benefits"></a>Avantages d’une connexion hybride App Service ###

Il existe un nombre d’avantages toohello hybride connexions fonctionnalité, y compris

- les applications peuvent accéder en toute sécurité aux systèmes et services locaux ;
- fonctionnalité de Hello ne nécessite pas d’un point de terminaison accessible internet
- Il est rapide et facile tooset des  
- chaque connexion hybride correspond à la combinaison de port d’hôte unique : tooa qui est un aspect de la sécurité
- normalement n’exige pas trous de pare-feu que les connexions hello sont tout trafic sortantes via les ports web standard
- Étant donné que la fonctionnalité de hello est au niveau du réseau qui signifie également qu’il s’agit de langage toohello agnostique utilisé par votre application et hello la technologie utilisée par le point de terminaison hello
- Il peut être utilisé tooprovide accès dans plusieurs réseaux à partir d’une seule application 

### <a name="things-you-cannot-do-with-hybrid-connections"></a>Ce que vous ne pouvez pas faire avec les connexions hybrides ###

Vous ne pouvez pas faire certaines opérations avec les connexions hybrides, notamment :

- montage d’un lecteur ;
- utilisation d’UDP ;
- accès à des services TCP qui utilisent des ports dynamiques tels que le mode FTP passif ou le mode passif étendu ;
- prise en charge LDAP, qui est parfois requise par UDP ;
- prise en charge d’Active Directory.

## <a name="adding-and-creating-a-hybrid-connection-in-your-app"></a>Ajout et création d’une connexion hybride dans votre application ##

Connexions hybrides peuvent être créées via le portail d’application hello ou à partir du portail de services de connexion hybride hello.  Il est recommandé d’utiliser hello de portail toocreate application hello connexions hybrides vous souhaitez toouse avec votre application.  toocreate une connexion hybride accédez toohello [portail Azure] [ portal] et aller dans hello l’interface utilisateur pour votre application.  Sélectionnez **Mise en réseau > Configurer vos points de terminaison de connexion hybride**.  À ce stade, vous pouvez voir connexions hybrides hello qui sont configurés avec votre application  

![][2]

tooadd une connexion hybride, cliquez sur Ajouter une connexion hybride.  Hello l’interface utilisateur qui s’affiche, et répertorie les connexions hybrides hello que vous avez déjà créé.  tooadd un ou plusieurs d'entre eux tooyour application, cliquez sur hello ceux que vous le souhaitez et atteint **ajouter sélectionné la connexion hybride**.  

![][3]

Si vous souhaitez toocreate une connexion hybride, cliquez sur **créer la connexion hybride**.  Vous spécifiez ici le : 

- Nom du point de terminaison
- Nom d’hôte du point de terminaison
- Port du point de terminaison
- espace de noms ServiceBus que vous souhaitez toouse

![][4]

Chaque connexion hybride est l’espace de noms tooa liée service bus et chaque espace de noms service bus est dans une région Azure.  Il est important de tootry et utilisez un service bus d’espace de noms dans hello même région que votre application, ainsi que la latence du réseau induite par tooavoid.

Si vous souhaitez tooremove votre connexion hybride à partir de votre application, cliquez avec le bouton droit dessus et sélectionnez **déconnexion**.  

Une fois qu’une connexion hybride est ajoutée à l’application web tooyour, vous pouvez voir plus d’informations sur ce dernier en cliquant dessus.  

![][5]

## <a name="hybrid-connections-and-app-service-plans"></a>Connexions hybrides et plans App Service ##

Hello hybride seules connexions maintenant sont les connexions hybrides nouvelle hello.  Elles sont uniquement disponibles dans les références de tarification De base, Standard, Premium et Isolé.  Il n’y a toohello limites liées plan de tarification.  

| Plan de tarification | Nombre de connexions hybrides utilisables dans le plan de hello |
|----|----|
| De base | 5 |
| Standard | 25 |
| Premium | 200 |
| Isolé | 200 |

Dans la mesure où il existe des restrictions du Plan App Service et sont également l’interface utilisateur Bonjour Plan App Service qui vous montre le nombre de connexions hybrides est utilisé par les applications.  

![][6]

Tout comme avec le mode d’application hello, vous pouvez voir plus d’informations sur la connexion hybride en cliquant dessus.  Dans les propriétés de hello illustrées ici, vous pouvez voir toutes les informations de hello vous aviez au mode d’application hello mais que vous pouvez également voir le nombre d’autres applications Bonjour même Plan de Service d’application sont à l’aide de cette connexion hybride.

![][7]

S’il existe une limite du nombre de hello de points de terminaison de connexion hybride qui peut être utilisé dans un Plan de Service d’application, chaque connexion hybride utilisée utilisable sur n’importe quel nombre d’applications dans ce Plan App Service.  Qui est toosay que si j’avais 1 connexion hybride que j’ai utilisé dans des applications distinctes 5 dans Mon Plan de Service d’application, qui est toujours 1 connexion hybride.

Il existe une connexions toohybrid de coût supplémentaire au-delà uniquement ne sont pas utilisables dans la référence (SKU) isolé, Standard, Premium ou Basic.  Pour plus d’informations sur la tarification de la connexion hybride, accédez ici : [Tarification Service Bus][sbpricing].

## <a name="hybrid-connection-manager"></a>Gestionnaire de connexion hybride ##

Toowork des connexions hybrides vous devez un agent de relais dans un réseau de hello qui héberge votre point de terminaison de connexion hybride.  Que l’agent de relais est appelé hello Gestionnaire de connexion hybride (HCM).  Cet outil peut être téléchargé à partir de hello **mise en réseau > configurer vos points de terminaison de connexion hybride** UI disponible à partir de votre application Bonjour [portail Azure][portal].  

Cet outil s’exécute sur Windows Server 2008 R2 et les versions ultérieures de Windows.  Une fois installé hello HCM s’exécute en tant que service.  Ce service connecte à relais de servicebus tooAzure basé sur des points de terminaison hello configuré.  connexions Hello de hello HCM sont tooports sortants 80 et 443.    

Hello HCM possède une interface utilisateur tooconfigure il.  Vous pouvez mettre après hello que HCM est installé hello l’interface utilisateur en exécutant hello HybridConnectionManagerUi.exe qui se trouve dans le répertoire d’installation de gestionnaire de connexions hybrides hello.  Vous pouvez également y accéder facilement sur Windows 10 en saisissant *Interface utilisateur du Gestionnaire de connexion hybride* dans la zone de recherche.  

Lorsque hello HCM UI est démarré, hello première chose que vous consultez est une table qui répertorie toutes les connexions hybrides hello qui sont configurées avec cette instance de hello HCM.  Si vous le souhaitez toomake toutes les modifications que vous devez tooauthenticate avec Azure. 

tooadd une ou plusieurs connexions hybrides tooyour HCM :

1. Démarrer hello HCM UI
1. Cliquez sur Configure another hybrid connection (Configurer une autre connexion hybride) ![][8]

1. Connectez-vous à votre compte Azure
1. Sélectionnez un abonnement
1. Cliquez sur les connexions hybrides hello vous souhaitez que cette toorelay HCM![][9]

1. Cliquez sur Enregistrer.

À ce stade, vous verrez les connexions hybrides hello que vous avez ajouté.  Vous pouvez également cliquer sur la connexion hybride hello configuré et consulter les informations de connexion de hello.

![][10]

Pour vos HCM toobe toosupport en mesure de hello hybride connexions qu’il est configuré avec, il doit :

- TooAzure d’accès TCP sur les ports 80 et 443
- Point de terminaison de connexion TCP accès toohello hybride
- capacité toodo DNS aspect onduleur sur l’hôte de point de terminaison de hello et espace de noms servicebus azure hello

Hello HCM prend en charge les nouvelles connexions hybrides ainsi que des connexions hybrides BizTalk plus anciennes de hello.

### <a name="redundancy"></a>Redondance ###

Chaque GCH peut prendre en charge plusieurs connexions hybrides.  De plus, toute connexion hybride peut être prise en charge par plusieurs GCH.  comportement par défaut de Hello est le trafic de robin tooround sur hello configuré HCMs pour n’importe quel point de terminaison donné.  Si vous souhaitez une haute disponibilité sur vos connexions hybrides à partir de votre réseau, instanciez simplement plusieurs GCH sur des ordinateurs distincts. 

### <a name="manually-adding-a-hybrid-connection"></a>Ajout manuel d’une connexion hybride ###

Si vous souhaitez une personne en dehors de votre abonnement toohost une instance HCM pour une connexion hybride donné, vous pouvez partager avec eux hello la chaîne de connexion de passerelle pour la connexion hybride hello.  Vous pouvez le voir dans les propriétés de hello pour une connexion hybride Bonjour [portail Azure][portal]. toouse de chaîne, cliquez sur hello **configurer manuellement** bouton Bonjour HCM et la coller dans la chaîne de connexion de passerelle hello.


## <a name="troubleshooting"></a>Résolution des problèmes ##

Lorsque votre connexion hybride est configurée avec une application en cours d’exécution et il existe au moins un HCM qui possède cette connexion hybride configurée, puis hello état indique **connecté** dans le portail de hello.  Si elle n’affiche pas **connecté** cela signifie que votre application est arrêté ou que votre HCM ne peut pas se connecter à tooAzure sur les ports 80 ou 443.  

Hello principale raison que les clients ne peuvent pas se connecter à tootheir le point de terminaison est, car le point de terminaison hello a été spécifié à l’aide d’une adresse IP au lieu d’un nom DNS.  Si votre application ne peut pas atteindre le point de terminaison hello souhaitée et que vous avez utilisé une adresse IP, basculez toousing un nom DNS valide sur l’ordinateur hôte de hello où hello HCM est en cours d’exécution.  Autres toocheck choses sont que hello nom DNS résout correctement sur l’ordinateur hôte de hello où hello HCM est en cours d’exécution et que vous disposez de connectivité à partir de l’hôte hello hello HCM exécutant point de terminaison de connexion toohello hybride.  

Il existe un outil Bonjour Service d’application qui peut être appelée à partir de la console hello appelé tcpping.  Cet outil peut vous indiquer si vous avez accès tooa point de terminaison TCP, mais ne vous indiquez pas si vous avez accès de point de terminaison tooa hybride connexion.  Lorsqu’il est utilisé dans la console hello par rapport à un point de terminaison de connexion hybride, un test ping réussi uniquement vous indiquera que vous disposez d’une connexion hybride configurée pour votre application qui utilise cette combinaison d’hôte : port.  

## <a name="biztalk-hybrid-connections"></a>Connexions hybrides BizTalk ##

capacité de connexions hybrides BizTalk Hello antérieure a été fermée hors tension de créations de connexion hybride BizTalk toofurther.  Vous pouvez continuer à l’aide de vos connexions hybrides de BizTalk préexistant avec vos applications mais que vous migrez toohello nouveau service.  Hello avantages dans le nouveau service de hello sur la version de BizTalk hello sont notamment :

- aucun compte BizTalk supplémentaire n’est requis ;
- TLS 1.2 au lieu de 1.0 comme dans les connexions hybrides BizTalk ;
- La communication est via les ports 80 et 443 à l’aide d’un tooreach de nom DNS Azure au lieu d’adresses IP et une plage d’autres ports.  

tooadd une application BizTalk hybride connexion tooyour, application tooyour accédez Bonjour [portail Azure] [ portal] et cliquez sur **mise en réseau > configurer vos points de terminaison de connexion hybride**.  Dans la table de connexions hybrides hello classique, cliquez sur **ajouter une connexion hybride classique**.  La liste de vos connexions hybrides BizTalk s’affiche alors.  


<!--Image references-->
[1]: ./media/app-service-hybrid-connections/hybridconn-connectiondiagram.png
[2]: ./media/app-service-hybrid-connections/hybridconn-portal.png
[3]: ./media/app-service-hybrid-connections/hybridconn-addhc.png
[4]: ./media/app-service-hybrid-connections/hybridconn-createhc.png
[5]: ./media/app-service-hybrid-connections/hybridconn-properties.png
[6]: ./media/app-service-hybrid-connections/hybridconn-aspproperties.png
[7]: ./media/app-service-hybrid-connections/hybridconn-hcm.png
[8]: ./media/app-service-hybrid-connections/hybridconn-hcmadd.png
[9]: ./media/app-service-hybrid-connections/hybridconn-hcmadded.png
[10]: ./media/app-service-hybrid-connections/hybridconn-hcmdetails.png

<!--Links-->
[HCService]: http://docs.microsoft.com/azure/service-bus-relay/relay-hybrid-connections-protocol/
[portal]: http://portal.azure.com/
[oldhc]: http://docs.microsoft.com/azure/biztalk-services/integration-hybrid-connection-overview/
[sbpricing]: http://azure.microsoft.com/pricing/details/service-bus/

