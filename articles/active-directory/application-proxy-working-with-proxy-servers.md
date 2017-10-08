---
title: aaaWork avec existant local serveurs proxy et Azure AD | Documents Microsoft
description: "Décrit comment toowork avec existant local serveurs proxy."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Travailler avec des serveurs proxy locaux existants

Cet article explique comment toowork de connecteurs de Proxy d’Application Azure Active Directory (Azure AD) tooconfigure avec des serveurs proxy sortant. Il est destiné aux clients avec des environnements réseau qui ont des proxys existants.

Nous allons commencer par examiner les scénarios de déploiement principaux suivants :
* Configurer les connecteurs toobypass les proxys sortants sur site.
* Configurez des connecteurs toouse un tooaccess proxy sortant Proxy d’Application Azure AD.

Pour plus d’informations sur le fonctionnement des connecteurs, consultez [Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md).

## <a name="configure-hello-outbound-proxy"></a>Configurer un proxy sortant de hello

Si vous avez un proxy sortant dans votre environnement, utilisez un compte avec le proxy sortant du hello tooconfigure les autorisations appropriées. Étant donné que le programme d’installation Bonjour s’exécute dans le contexte hello d’utilisateur hello qui effectue l’installation de hello, vous pouvez vérifier la configuration de hello à l’aide de Microsoft Edge ou un autre navigateur Internet.

paramètres du proxy tooconfigure hello dans Microsoft Edge :

1. Accédez trop**paramètres** > **afficher les paramètres avancés** > **ouvrir les paramètres Proxy** > **l’installation manuelle du Proxy** .
2. Définissez **utiliser un serveur proxy** trop**sur**, sélectionnez hello **n’utilisez pas serveur de proxy hello pour les adresses locales (intranet)** case à cocher, puis les tooreflect modification hello adresse et port votre serveur proxy local.
3. Renseignez les paramètres du proxy nécessaire hello.

   ![Boîte de dialogue des paramètres de proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Proxys sortants de contournement

Les connecteurs ont des composants de système d’exploitation sous-jacents qui effectuent des demandes sortantes. Ces composants tente automatiquement de toolocate un serveur proxy sur le réseau de hello. Ils utilisent la détection automatique WPAD (Web Proxy), s’il est activé dans l’environnement de hello.

composants du système d’exploitation Hello tentative toolocate un serveur proxy en effectuant une recherche DNS pour wpad.domainsuffix. Si cela résout dans DNS, une demande HTTP est effectuée puis toohello IP adresse wpad.dat. Cette demande devient un script de configuration du proxy hello dans votre environnement. connecteur de Hello utilise cette tooselect script un serveur proxy sortant. Toutefois, le trafic de connecteur peut toujours pas abouti, en raison des paramètres de configuration supplémentaire nécessaires sur le proxy hello.

Vous pouvez configurer toobypass de connecteur hello votre tooensure proxy local qu’il utilise directe connectivité toohello Azure services. Nous recommandons cette approche (si votre stratégie réseau le permet), car elle signifie que vous disposez d’un moins toomaintain de configuration.

l’utilisation de proxy sortant toodisable pour le connecteur de hello, modifier le fichier de C:\Program Files\Microsoft AAD application Proxy Connector\ApplicationProxyConnectorService.exe.config hello et ajouter hello *system.net* section indiquée dans cet exemple de code :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
tooensure que service de mise à jour du connecteur hello ignore également les proxy hello, apporter un modification toohello ApplicationProxyConnectorUpdaterService.exe.config un fichier similaire situé dans C:\Program Files\Microsoft AAD application Proxy Connector mise à jour.

Être sûr de copies de toomake des fichiers d’origine de hello, au cas où vous avez besoin des fichiers .config de toorevert toohello par défaut.

## <a name="use-hello-outbound-proxy-server"></a>Utiliser un serveur proxy sortant hello

Certains environnements nécessitent tous les toogo le trafic sortant via un proxy sortant, sans exception. Par conséquent, en ignorant les proxy hello n’est pas une option.

Vous pouvez configurer hello connecteur trafic toogo via le proxy sortant hello, comme indiqué dans hello suivant schéma :

 ![Configuration du connecteur les toogo de trafic via un proxy sortant de tooAzure AD Proxy d’Application](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

Par conséquent d’obtenir uniquement le trafic sortant, il est sans tooconfigure besoin accès via votre pare-feu entrant.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>Étape 1 : Configurer le connecteur de hello et liées toogo services via le proxy sortant hello

Comme indiqué précédemment, si WPAD est activée dans l’environnement de hello et correctement configuré, connecteur de hello détecte automatiquement toouse de serveur et de la tentative de proxy sortant hello il. Toutefois, vous pouvez configurer explicitement toogo de connecteur hello via un proxy sortant.

toodo, modifiez le fichier de C:\Program Files\Microsoft AAD application Proxy Connector\ApplicationProxyConnectorService.exe.config hello et ajouter hello *system.net* section indiquée dans cet exemple de code. Modification *proxyserver:8080* tooreflect votre nom de serveur proxy local ou une adresse IP et un hello qu’elle est à l’écoute sur le port.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

Ensuite, configurez le proxy hello toouse du service de mise à jour du connecteur hello en effectuant un fichier de toohello modification similaire situé dans C:\Program Files\Microsoft AAD application Proxy Connector Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>Étape 2 : Configurer hello proxy tooallow le trafic de connecteur de hello et tooflow services connexes via

Il existe quatre aspects tooconsider au proxy sortant de hello :
* Règles sortantes du proxy
* Authentification du proxy
* Ports du proxy
* Inspection SSL

#### <a name="proxy-outbound-rules"></a>Règles sortantes du proxy
Autoriser toohello accès suivant les points de terminaison pour l’accès au service de connecteur :

* *.msappproxy.net
* *.servicebus.windows.net

Autorise l’inscription initiale, toohello d’accès suivant les points de terminaison :

* login.windows.net
* login.microsoftonline.com

Si vous ne pouvez pas autoriser la connexion par le nom de domaine complet et ont besoin de plages d’adresses IP toospecify utiliser à la place, ces options :

* Autoriser l’accès sortant du connecteur hello tooall destinations.
* Autoriser l’accès sortant du connecteur hello trop[plages d’adresses IP de centre de données Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). défi Hello à l’aide de la liste de hello des plages d’adresses IP de centre de données Azure est qu’il est mis à jour chaque semaine. Vous devez tooput un processus dans tooensure lieu que les règles d’accès sont mis à jour en conséquence.

#### <a name="proxy-authentication"></a>Authentification du proxy

L’authentification proxy n'est actuellement pas prise en charge. Notre recommandation actuelle est destinations Internet de la toohello tooallow hello connecteur l’accès anonyme.

#### <a name="proxy-ports"></a>Ports du proxy

connecteur de Hello rend les connexions SSL sortantes en utilisant la méthode de connexion hello. Cette méthode définit essentiellement un tunnel via le proxy sortant hello. Configurer hello proxy server tooallow tunneling tooports 443 et 80.

>[!NOTE]
>Lorsque Service Bus s’exécute via le protocole HTTPS, il utilise le port 443. Toutefois, par défaut, Service Bus tente de connexions TCP directes et revient tooHTTPS uniquement si une connexion directe échoue.

tooensure hello Service Bus, le trafic est également envoyé via le serveur proxy sortant de hello, assurez-vous que le connecteur hello ne peut pas se connecter directement toohello des services Azure pour les ports 9350, 9352 et 5671.

#### <a name="ssl-inspection"></a>Inspection SSL
N’utilisez pas l’inspection SSL pour le trafic de connecteur hello, car il provoque des problèmes pour le trafic de connecteur hello.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Résoudre les problèmes courants de proxy de connecteur et de connectivité du service
Vous devez maintenant voir tout le trafic circulant via le proxy hello. Si vous rencontrez des problèmes, doit favoriser le hello suivant des informations de dépannage.

Hello la meilleure façon tooidentify et résoudre les problèmes de connectivité du connecteur problèmes est tootake un réseau de capture sur le service du connecteur hello lors du démarrage du service Connecteur hello. Cela peut être une tâche ardue, aussi examinons quelques conseils rapides sur la capture et le filtrage des traces réseau.

Vous pouvez utiliser hello analyse de l’outil de votre choix. Pour des raisons de hello de cet article, nous avons utilisé Microsoft Network Monitor 3.4. Vous pouvez [le télécharger à partir de Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).

les exemples Hello et les filtres que nous utilisons dans les sections suivantes de hello sont spécifique tooNetwork moniteur, mais les principes hello peuvent être appliqué tooany l’outil d’analyse.

### <a name="take-a-capture-by-using-network-monitor"></a>Prendre une capture à l’aide de Network Monitor

toostart une capture :

1. Ouvrez Network Monitor, puis cliquez sur **Nouvelle capture**.
2. Cliquez sur hello **Démarrer** bouton.

   ![Fenêtre de Network Monitor](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Après avoir effectué une capture, cliquez sur hello **arrêter** bouton tooend il.

### <a name="take-a-capture-of-connector-traffic"></a>Effectuez une capture du trafic de connecteur

Pour le dépannage initiale, effectuez hello comme suit :

1. À partir de services.msc, arrêtez le service de connecteur Proxy d’Application Azure AD de hello.
2. Démarrer la capture de réseau hello.
3. Démarrer le service de connecteur Proxy d’Application Azure AD hello.
4. Arrêter la capture de réseau hello.

   ![Service de connecteur de proxy d’application Azure AD dans services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Examiner les demandes de hello à partir du serveur de proxy hello connecteur toohello

Maintenant que vous avez une capture réseau, vous êtes prêt toofilter il. toolooking de clé Hello au niveau de la trace de hello est de comprendre comment capturer les toofilter hello.

Un filtre est comme suit (où 8080 est le port du service proxy hello) :

**(http.Request or http.Response) and tcp.port==8080**

Si vous entrez ce filtre Bonjour **filtre d’affichage** et sélectionnez **appliquer**, filtres de trafic hello capturée en fonction de filtre de hello.

Hello filtre précédent montre simplement hello demandes et réponses HTTP à partir de port du proxy hello. Pour un démarrage du connecteur sur lequel le connecteur de hello est toouse configuré un serveur proxy, le filtre de hello indiquerait quelque chose comme ceci :

 ![Exemple de liste de requêtes et réponses HTTP filtrées](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Vous maintenant spécifiquement recherchez hello que Connect demande qui illustrent la communication avec le serveur de proxy hello. En cas de succès, vous obtenez une réponse HTTP OK (200).

Si vous voyez les autres codes de réponse, telles que 407 ou 502, proxy de hello est nécessitant une authentification ou ne pas autoriser le trafic de hello pour une raison quelconque. À ce stade, vous impliquez l’équipe de support technique de votre serveur proxy.

### <a name="identify-failed-tcp-connection-attempts"></a>Identifier les tentatives de connexion TCP ayant échoué

Hello autre scénario courant dans lequel vous pouvez être intéressé est lorsque hello connecteur tente tooconnect directement, mais il échoue.

Un autre filtre de moniteur réseau qui permet d’identifier ce problème vous tooeasily est la suivante :

**property.TCPSynRetransmit**

Un paquet SYN est envoyé de premier paquet de hello tooestablish une connexion TCP. Si ce paquet ne retourne pas une réponse, hello SYN est retentée. Vous pouvez utiliser hello précédant toosee de filtre des requêtes SYN retransmis. Ensuite, vous pouvez vérifier si ces requêtes SYN correspondre tooany liés au connecteur du trafic.

Hello suivant montre une tentative de connexion ayant échoué port de Bus tooService 9352 :

 ![Exemple de réponse à une tentative de connexion ayant échoué](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Si vous voyez quelque chose comme hello précédant la réponse, connecteur de hello tente toocommunicate directement avec hello Service service Bus Azure. Si vous prévoyez de hello connecteur toomake des connexions directes toohello Azure services, cette réponse est une indication que vous avez un problème réseau ou un pare-feu.

>[!NOTE]
>Si vous êtes toouse configuré un serveur proxy, cette réponse peut signifier que Service Bus tente une connexion TCP directe avant de basculer tooattempting une connexion via HTTPS.
>

L’analyse des traces réseau n’est pas faite pour tout le monde. Mais il peut être une outil précieux tooget rapidement des informations sur ce qui se passe votre réseau.

Si vous continuez toostruggle avec des problèmes de connectivité du connecteur, créez un ticket avec notre équipe de support. équipe de Hello peut vous aider à résoudre le problème.

Pour plus d’informations sur la résolution des erreurs avec le connecteur de proxy d’application, consultez [Résoudre les problèmes du proxy d’application](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Étapes suivantes

[Présentation des connecteurs de proxy d’application Azure AD](application-proxy-understand-connectors.md)<br>
[Comment toosilently installer hello connecteur Proxy d’Application Azure AD](active-directory-application-proxy-silent-installation.md)
