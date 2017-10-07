---
title: aaaAzure Traffic Manager - FAQ | Documents Microsoft
description: "Cet article fournit des réponses aux questions à propos de Traffic Manager d’elles sonttrop"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 75d5ff9a-f4b9-4b05-af32-700e7bdfea5a
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: kumud
ms.openlocfilehash: 5530d03b55bbf49a52002841e281e2cf5819c2b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-frequently-asked-questions-faq"></a>Forum Aux Questions (FAQ) relatif à Traffic Manager

## <a name="traffic-manager-basics"></a>Concepts de base de Traffic Manager

### <a name="what-ip-address-does-traffic-manager-use"></a>Quelle est l’adresse IP utilisée par Traffic Manager ?

Comme expliqué dans [fonctionnement de Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager fonctionne en hello au niveau du DNS. Il envoie des réponses DNS service approprié de toodirect clients toohello point de terminaison. Les clients puis connectent point de terminaison de service toohello directement, non par le biais du Gestionnaire de trafic.

Par conséquent, Traffic Manager ne fournit pas de point de terminaison ou l’adresse IP pour tooconnect les clients à. Par conséquent, si vous souhaitez l’adresse IP statique pour votre service, qui doit être configuré au niveau de service hello, pas dans le Gestionnaire de trafic.

### <a name="does-traffic-manager-support-sticky-sessions"></a>Traffic Manager prend-il en charge les sessions « persistantes » ?

Comme expliqué dans [fonctionnement de Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager fonctionne en hello au niveau du DNS. Il utilise des réponses toodirect clients toohello service approprié point de terminaison DNS. Les clients connectent point de terminaison de service toohello directement, non par le biais du Gestionnaire de trafic. Par conséquent, Traffic Manager ne voit pas de trafic hello HTTP entre le client de hello et le serveur de hello.

En outre, adresse hello source de requête DNS hello reçu par le Gestionnaire de trafic appartient toohello le service DNS récursive, pas les clients hello. Par conséquent, Traffic Manager n’a aucun client individuelles de manière tootrack et ne peut pas implémenter 'rémanentes' sessions. Cette limitation est commun tooall DNS du trafic basé sur des systèmes de gestion et n’est pas spécifique tooTraffic Manager.

### <a name="why-am-i-seeing-an-http-error-when-using-traffic-manager"></a>Pourquoi une erreur HTTP s’affiche-t-elle quand j’utilise Traffic Manager ?

Comme expliqué dans [fonctionnement de Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager fonctionne en hello au niveau du DNS. Il utilise des réponses toodirect clients toohello service approprié point de terminaison DNS. Les clients puis connectent point de terminaison de service toohello directement, non par le biais du Gestionnaire de trafic. Traffic Manager ne voit pas le trafic HTTP entre le client et le serveur. C’est pourquoi, toute erreur HTTP que vous voyez doit provenir de votre application. Pour l’application de toohello tooconnect hello client, toutes les étapes de résolution DNS sont terminées. Qui inclut les interactions de Traffic Manager a sur le flux de trafic d’application hello.

Une analyse approfondie doit donc se concentrer sur l’application hello.

en-tête d’hôte Hello HTTP envoyé à partir du navigateur du client hello est hello la plus courante des problèmes. Assurez-vous qu’application hello est configuré tooaccept hello en-tête hello nom de domaine que vous utilisez. Pour les points de terminaison à l’aide de hello du Service d’applications Azure, consultez [configuration d’un nom de domaine personnalisé pour une application web dans Azure App Service à l’aide de Traffic Manager](../app-service-web/web-sites-traffic-manager-custom-domain-name.md).

### <a name="what-is-hello-performance-impact-of-using-traffic-manager"></a>Qu’est hello impact sur les performances à l’aide de Traffic Manager ?

Comme expliqué dans [fonctionnement de Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager fonctionne en hello au niveau du DNS. Étant donné que les clients connectent les points de terminaison service tooyour directement, il n’existe aucun impact sur les performances effectuées lors de l’utilisation de Traffic Manager une fois hello est établie.

Étant donné que Traffic Manager s’intègre avec les applications hello au niveau du DNS, elle nécessite une toobe de recherche DNS supplémentaire insérée dans la chaîne de résolution DNS de hello. impact Hello de Traffic Manager sur le temps de résolution DNS est minime. Traffic Manager utilise un réseau mondial de serveurs de noms et [anycast](https://en.wikipedia.org/wiki/Anycast) réseau tooensure DNS les requêtes sont toujours serveur nom disponible le plus proche de toohello routé. En outre, la mise en cache des réponses DNS signifie que la latence DNS supplémentaire hello générée à l’aide de Traffic Manager s’applique uniquement tooa fraction de sessions.

itinéraires de méthode Hello performances du trafic toohello de point de terminaison disponible le plus proche. résultat net Hello est que hello impact sur les performances globales associées à cette méthode doit être minime. Une augmentation de latence DNS doit être décalée par point de terminaison toohello de latence réseau inférieure.

### <a name="what-application-protocols-can-i-use-with-traffic-manager"></a>Quels protocoles d’application puis-je utiliser avec Traffic Manager ?

Comme expliqué dans [fonctionnement de Traffic Manager](../traffic-manager/traffic-manager-overview.md#how-traffic-manager-works), Traffic Manager fonctionne en hello au niveau du DNS. Une fois que la recherche DNS hello est terminée, les clients connectent le point de terminaison toohello application directement, non par le biais du Gestionnaire de trafic. Par conséquent, connexion de hello peut utiliser tout protocole d’application. Si vous sélectionnez TCP comme hello protocole de surveillance, Traffic Manager Surveillance de l’intégrité de point de terminaison peut être effectuée sans à l’aide de protocoles d’application. Si vous choisissez d’intégrité de hello toohave vérifiée à l’aide d’un protocole d’application, le point de terminaison de hello doit toobe toorespond en mesure de tooeither HTTP ou HTTPS GET des demandes.

### <a name="can-i-use-traffic-manager-with-a-naked-domain-name"></a>Puis-je utiliser Traffic Manager avec un nom de domaine « nu » ?

Non. les normes DNS Hello n’autorisent pas les enregistrements CNAME tooco-existent avec d’autres enregistrements DNS de hello même nom. Hello apex (ou racines) d’une zone DNS contient toujours les deux enregistrements DNS existants ; Hello SOA et hello faisant autoritées enregistrements NS. Cela signifie qu'un enregistrement CNAME ne peut pas être créé au sommet de zone hello sans violer les normes DNS hello.

Traffic Manager nécessite un nom DNS de DNS CNAME toomap enregistrement hello personnel. Par exemple, vous mappez www.contoso.com toohello Traffic Manager profil DNS nom contoso.trafficmanager.net. En outre, hello profil Traffic Manager renvoie un tooindicate DNS CNAME deuxième point de terminaison qui hello client doit se connecter.

toowork résoudre ce problème, nous recommandons d’utiliser un toodirect du trafic de redirection HTTP à partir de hello naked nom tooa différentes URL de domaine, qui permet ensuite de Traffic Manager. Par exemple, hello naked domaine « contoso.com » peut rediriger les utilisateurs toohello CNAME « www.contoso.com » qui pointe toohello nom DNS de Traffic Manager.

La prise en charge complète des domaines nus dans Traffic Manager est suivie dans notre backlog de fonctionnalités. Vous pouvez inscrire votre prise en charge pour cette demande de fonctionnalité en [votant pour celle-ci sur le site de commentaires de notre communauté](https://feedback.azure.com/forums/217313-networking/suggestions/5485350-support-apex-naked-domains-more-seamlessly).

### <a name="does-traffic-manager-consider-hello-client-subnet-address-when-handling-dns-queries"></a>Traffic Manager considère adresse de sous-réseau client hello lors du traitement de requêtes DNS ? 
Non, actuellement Traffic Manager considère uniquement hello adresse IP source de requête DNS hello qu'il reçoit, qui est généralement hello adresseIP du programme de résolution DNS hello lorsque vous effectuez des recherches pour les méthodes de routage géographique et de performances.  
Plus précisément, [7871 RFC – sous-réseau de Client dans les requêtes DNS](https://tools.ietf.org/html/rfc7871) qui fournit un [mécanisme d’Extension pour DNS (EDNS0)](https://tools.ietf.org/html/rfc2671) qui peuvent passer sur l’adresse de sous-réseau hello client à partir de programmes de résolution qui prennent en charge les serveurs tooDNS est actuellement pas pris en charge dans Traffic Manager. Vous pouvez inscrire votre prise en charge pour cette demande de fonctionnalité en [sur le site de commentaires de notre communauté](https://feedback.azure.com/forums/217313-networking).


### <a name="what-is-dns-ttl-and-how-does-it-impact-my-users"></a>Qu’est-ce que le TTL du DNS et comment affecte-t-il mes utilisateurs ?

Lorsqu’une requête DNS arrive sur Traffic Manager, il définit une valeur dans la réponse hello appelée durée de vie (TTL). Cette valeur, dont l’unité est en secondes, indique tooDNS programmes de résolution en aval sur toocache la durée pendant laquelle cette réponse. Alors que les programmes de résolution DNS ne sont pas garanti que toocache ce résultat, la mise en cache leur permet de toorespond tooany les requêtes suivantes hors cache hello au lieu de passer les serveurs du Gestionnaire DNS tooTraffic. Cela a un impact sur les réponses hello comme suit :
- une durée de vie plue réduit le nombre hello des requêtes qui se retrouver sur hello serveurs DNS Traffic Manager, ce qui peuvent de réduire le coût de hello pour un client, car le nombre de requêtes pris en charge est une utilisation facturable.
- une durée de vie plus élevée peut potentiellement réduire hello temps toodo une recherche DNS.
- une durée de vie plus élevée signifie également que vos données ne reflète pas les informations d’intégrité plus récente hello que Traffic Manager a obtenues via ses agents de détection.

### <a name="how-high-or-low-can-i-set-hello-ttl-for-traffic-manager-responses"></a>Comment élevé ou faible puis-je définir hello durée de vie pour les réponses de Traffic Manager ?

Vous pouvez définir, à un par niveau de profil, hello toobe TTL du DNS en tant que 0 secondes et aussi élevée que 2 147 483 647 secondes (hello plage maximale conforme [-la norme RFC 1035](https://www.ietf.org/rfc/rfc1035.txt )). Une durée de vie de 0 signifie que les programmes de résolution DNS en aval ne mettent pas en cache les réponses de requêtes et toutes les requêtes sont attendu des serveurs DNS de gestionnaire de trafic tooreach hello.

## <a name="traffic-manager-geographic-traffic-routing-method"></a>Méthode de routage du trafic « Geographic » (Géographique) de Traffic Manager

### <a name="what-are-some-use-cases-where-geographic-routing-is-useful"></a>Quels sont les cas d’utilisation dans lesquels le routage géographique est utile ? 
Type de routage géographique peut servir dans tout scénario où un client Azure doit toodistinguish leurs utilisateurs basés sur des régions géographiques. Par exemple, à l’aide de la méthode de routage de trafic géographique hello, vous pouvez accorder aux utilisateurs à partir des régions spécifiques une expérience utilisateur autre que ceux d’autres régions. Un autre exemple est le respect des mandats de souveraineté de données locales qui nécessitent que les utilisateurs d’une région spécifique soient servis uniquement par les points de terminaison existant dans cette région.

### <a name="what-are-hello-regions-that-are-supported-by-traffic-manager-for-geographic-routing"></a>Quelles sont les régions hello qui sont pris en charge par le Gestionnaire de trafic pour le routage géographiques ? 
hiérarchie de pays/région de Hello est utilisé par le Gestionnaire de trafic, vous pouvez trouver [ici](traffic-manager-geographic-regions.md). Alors que cette page est mises à jour avec toutes les modifications, vous pouvez également récupérer par programme des hello les mêmes informations à l’aide de hello [REST API de Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/). 

### <a name="how-does-traffic-manager-determine-where-a-user-is-querying-from"></a>Comment Traffic Manager détermine-t-il l’emplacement à partir duquel un utilisateur exécute une requête ? 
Traffic Manager recherche à adresse IP source de hello de requête hello (c’est très probablement un programme de résolution DNS local faisant hello interrogation pour le compte d’utilisateur de hello) et utilise un emplacement de hello toodetermine interne IP tooregion carte. Ce mappage est mis à jour sur un tooaccount régulièrement les modifications apportées à hello internet. 

### <a name="is-it-guaranteed-that-traffic-manager-can-correctly-determine-hello-exact-geographic-location-of-hello-user-in-every-case"></a>Il est garanti que Traffic Manager peut déterminer correctement hello exacte emplacement géographique d’utilisateur hello dans tous les cas ?
Non, Traffic Manager ne peut pas garantir cette région géographique hello nous déduire à partir de l’adresse hello source d’une requête DNS correspond toujours toohello l’emplacement utilisateur en raison de toohello suivant raisons : 

- Tout d’abord, comme décrit dans le précédent Forum aux questions de hello, hello adresse source que nous voyons est celui d’un programme de résolution DNS recherche hello pour le compte d’utilisateur de hello. Zone géographique du programme de résolution DNS hello hello est un bon proxy pour la zone géographique de l’utilisateur de hello hello, il peut également être différents selon l’encombrement hello du service de résolution DNS hello et hello spécifique service de résolution DNS qu'un client a choisi toouse. Par exemple, un client en Malaisie pourrait spécifier en cours d’utilisation des paramètres de leur appareil dont le serveur DNS à Singapour peut obtenir un service de résolution DNS choisi toohandle résolutions de requête hello pour cet utilisateur/appareil. Dans ce cas, Traffic Manager peut voir uniquement IP du programme de résolution hello adresse qui correspond à toohello emplacement de Singapour. Consultez également hello antérieures Forum aux questions relatives aux adresses de sous-réseau client prend en charge sur cette page.

- En second lieu, Traffic Manager utilise un mappage interne toodo hello IP toogeographic région NAT. Alors que ce mappage est validé et mis à jour sur un tooincrease de façon continue, sa précision et un compte pour hello en constante évolution de la nature de hello internet, vous pouvez encore possibilité hello que nos informations ne sont pas une représentation exacte d’un emplacement géographique de hello de tous les adresses IP Hello.


###  <a name="does-an-endpoint-need-toobe-physically-located-in-hello-same-region-as-hello-one-it-is-configured-with-for-geographic-routing"></a>Un toobe besoin de point de terminaison résident physiquement dans hello même région que hello il est configuré avec, pour le routage géographiques ? 
Non, emplacement hello du point de terminaison hello n’impose aucune restriction sur lequel une région peut être mappé tooit. Par exemple, un point de terminaison dans la région du centre des États-Unis Azure peut avoir tous les utilisateurs à partir de l’Inde dirigée tooit.

### <a name="can-i-assign-geographic-regions-tooendpoints-in-a-profile-that-is-not-configured-toodo-geographic-routing"></a>Puis-je attribuer des régions géographiques tooendpoints dans un profil qui n’est pas configuré toodo géographique routage ? 

Oui, si la méthode de routage hello d’un profil n’est pas géographique, vous pouvez utiliser hello [REST API de Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/) tooendpoints de régions géographiques tooassign dans ce profil. Dans les cas de hello des profils de type de routage non géographiques, cette configuration est ignorée. Si vous modifiez un tel profil toogeographic routage type ultérieurement, Traffic Manager peut utiliser ces mappages.


### <a name="why-am-i-getting-an-error-when-i-try-toochange-hello-routing-method-of-an-existing-profile-toogeographic"></a>Pour quelle raison obtenez-vous une erreur lorsque vous essayez de la méthode de routage hello toochange d’un tooGeographic profil existant ?

Tous les points de terminaison de hello sous un profil avec le routage géographique doivent toohave au moins une région mappé tooit. tooconvert un type de routage toogeographic profil existant, vous devez tooassociate régions géographiques tooall ses points de terminaison à l’aide de hello [REST API de Azure Traffic Manager](https://docs.microsoft.com/rest/api/trafficmanager/) avant de modifier hello routage tapez toogeographic. Si à l’aide du portail, supprimez tout d’abord les points de terminaison hello, modifiez la méthode de routage hello de hello profil toogeographic, puis ajoutez les points de terminaison hello, ainsi que leur mappage de région géographique. 


###  <a name="why-is-it-strongly-recommended-that-customers-create-nested-profiles-instead-of-endpoints-under-a-profile-with-geographic-routing-enabled"></a>Pourquoi est-il vivement recommandé que les clients créent des profils imbriqués à la place de points de terminaison sous un profil avec le routage géographique activé ? 

Une région peut être affecté tooonly un point de terminaison dans un profil si sa à l’aide du type de routage géographique. Si ce point de terminaison n’est pas un type imbriqué avec un tooit de profil attaché enfant, si ce point de terminaison va défectueux, Traffic Manager continue toosend trafic tooit depuis alternative hello de ne pas envoyer que tout le trafic n’est pas mieux. Traffic Manager n’est pas basculement tooanother point de terminaison, même lorsque la région de hello affecté est un « parent » de région de hello affecté toohello de point de terminaison qui s’est avéré incorrect (par exemple, si un point de terminaison a région Espagne devient non intègre, que nous n'allons pas basculement tooanother point de terminaison qui a hello région Europe assigné tooit). Cela tooensure le programme d’installation de Traffic Manager respecte hello géographiques disposant d’un client dans son profil. avantages de hello tooget du basculement sur le point de terminaison tooanother lorsqu’un point de terminaison est défectueux, il est recommandé que les régions géographiques appartenir profils toonested avec plusieurs points de terminaison qu’il contient au lieu de points de terminaison individuels. De cette façon, si un point de terminaison échoue de profil enfant hello imbriqué, le trafic peut basculement tooanother point de terminaison à l’intérieur de hello même imbriquées profil enfant.

### <a name="are-there-any-restrictions-on-hello-api-version-that-supports-this-routing-type"></a>Existe-t-il des restrictions sur la version de hello API qui prend en charge ce type de routage ?

Oui, uniquement de la version de l’API 2017-03-01 et prend en charge la plus récente de type de routage géographique hello. Les anciennes versions d’API ne peut pas être toocreated utilisé des profils de type de routage géographique ou affecter des régions géographiques tooendpoints. Si une ancienne version de l’API est profils tooretrieve utilisé à partir d’un abonnement Azure, tout profil d’un type de routage géographique n’est pas retourné. En outre, si vous utilisez des versions anciennes de l’API, les profils retournés qui contiennent des points de terminaison avec une affectation de régions géographiques n’affichent pas les régions géographiques affectées.



## <a name="traffic-manager-endpoints"></a>Points de terminaison Traffic Manager

### <a name="can-i-use-traffic-manager-with-endpoints-from-multiple-subscriptions"></a>Puis-je utiliser Traffic Manager avec des points de terminaison de plusieurs abonnements ?

L’utilisation de points de terminaison à partir de plusieurs abonnements n’est pas possible avec Azure Web Apps. Azure Web Apps requiert que tout nom de domaine personnalisé utilisé avec Web Apps ne soit utilisé que dans un seul abonnement. Il n’est pas toouse possible les applications Web à partir de plusieurs abonnements avec hello même nom de domaine.

Pour d’autres types de point de terminaison, il est possible de toouse Traffic Manager avec les points de terminaison à partir de plusieurs abonnements. Dans le Gestionnaire de ressources, les points de terminaison à partir de n’importe quel abonnement peuvent être ajoutés tooTraffic Manager, tant que personne hello configuration du profil Traffic Manager hello a accès en lecture toohello point de terminaison. Ces autorisations peuvent être accordées à l’aide du [contrôle d’accès en fonction du rôle Azure Resource Manager (RBAC)](../active-directory/role-based-access-control-configure.md).


### <a name="can-i-use-traffic-manager-with-cloud-service-staging-slots"></a>Puis-je utiliser Traffic Manager avec les emplacements intermédiaires de services cloud ?

Oui. Les emplacements intermédiaires de services cloud peuvent être configurés dans Traffic Manager en tant que points de terminaison externes. Contrôles d’intégrité sont toujours facturé au tarif de points de terminaison Azure hello. Étant donné que hello type de point de terminaison externe est en cours d’utilisation, service sous-jacent toohello de modifications ne sont pas appliquées automatiquement. Avec les points de terminaison externes, Traffic Manager ne détecte pas hello Service Cloud est arrêté ou supprimé. Par conséquent, hello Traffic Manager continue de facturation pour les contrôles d’intégrité jusqu'à ce que le point de terminaison hello est désactivé ou supprimé.

### <a name="does-traffic-manager-support-ipv6-endpoints"></a>Traffic Manager prend-il en charge les points de terminaison IPv6 ?

Traffic Manager ne fournit pas actuellement de serveurs de noms adressables en IPv6. Toutefois, Traffic Manager peut encore être utilisée par les clients IPv6 tooIPv6 de points de terminaison de connexion. Ne fait pas d’un client DNS demande directement tooTraffic Manager. En revanche, client de hello utilise un service DNS récursive. Un client IPv6 uniquement envoie des demandes du service DNS récursive toohello via IPv6. Service de récursive hello doit avoir des serveurs de noms en mesure de toocontact hello Traffic Manager à l’aide d’IPv4.

Traffic Manager répond avec le nom DNS de hello du point de terminaison hello. point de terminaison toosupport d’IPv6, AAAA du DNS enregistrer toohello nom pointage hello point de terminaison DNS IPv6 adresse doit exister. Les contrôles d’intégrité Traffic Manager n’acceptent que les adresses IPv4. Hello service a besoin de point de terminaison tooexpose IPv4 sur hello même nom DNS.

### <a name="can-i-use-traffic-manager-with-more-than-one-web-app-in-hello-same-region"></a>Puis-je utiliser Traffic Manager avec plus d’une application Web Bonjour même région ?

En règle générale, Traffic Manager est toodirect utilisé le trafic tooapplications est déployées dans des régions différentes. Toutefois, il peut également servir où une application a plusieurs déploiements Bonjour même région. Hello points de terminaison Traffic Manager Azure ne permettent pas plus d’un point de terminaison de l’application Web à partir de hello même région Azure toobe ajouté toohello même profil Traffic Manager.

##  <a name="traffic-manager-endpoint-monitoring"></a>Surveillance des points de terminaison Traffic Manager

### <a name="is-traffic-manager-resilient-tooazure-region-failures"></a>Échecs de la région n’est tooAzure résilient de Traffic Manager ?

Traffic Manager est un composant clé de la remise des applications hautement disponibles dans Azure hello.
toodeliver haute disponibilité, Traffic Manager doit avoir un niveau d’un nombre exceptionnellement élevé de disponibilité et être résilient tooregional échec.

Par conception, les composants de Traffic Manager sont résilients tooa défaillance complète de n’importe quelle région Azure. Cette tolérance s’applique tooall Traffic Manager composants : serveurs DNS hello, hello API, couche de stockage hello et service de surveillance hello.

Dans l’éventualité improbable hello d’une panne d’un ensemble de la région Azure, Traffic Manager est attendu toocontinue toofunction de normalement. Les applications déployées dans plusieurs régions Azure peuvent reposer sur une instance disponible de Traffic Manager toodirect trafic tooan de leur application.

### <a name="how-does-hello-choice-of-resource-group-location-affect-traffic-manager"></a>Comment le choix hello de l’emplacement du groupe de ressources affecte-t-il Traffic Manager ?

Traffic Manager est un service global unique. Il n’est pas régional. choix de Hello de l’emplacement du groupe de ressources ne fait aucune différence tooTraffic Manager les profils déployés dans ce groupe de ressources.

Le Gestionnaire de ressources Azure nécessite toutes les ressources de groupes toospecify un emplacement, qui détermine l’emplacement par défaut de hello pour les ressources déployées dans ce groupe de ressources. Lorsque vous créez un profil Traffic Manager, il est créé dans un groupe de ressources. Tous les profils Traffic Manager utiliser **global** en tant que leur emplacement, en remplaçant la valeur par défaut de groupe de ressources hello.

### <a name="how-do-i-determine-hello-current-health-of-each-endpoint"></a>Comment déterminer le contrôle d’intégrité actuel de hello de chaque point de terminaison ?

Hello surveillance de l’état de chaque point de terminaison actuel, dans Ajout toohello profil global, s’affiche dans hello portail Azure. Ces informations sont également disponibles via hello moniteur de trafic [API REST](https://msdn.microsoft.com/library/azure/mt163667.aspx), [applets de commande PowerShell](https://msdn.microsoft.com/library/mt125941.aspx), et [CLI d’Azure inter-plateformes](../cli-install-nodejs.md).

Azure ne fournit pas d’informations d’historique sur le point de terminaison passée d’intégrité hello capacité tooraise des alertes ou sur le contrôle d’intégrité de modifications tooendpoint.

### <a name="can-i-monitor-https-endpoints"></a>Puis-je surveiller les points de terminaison HTTPS ?

Oui. Traffic Manager prend en charge la détection sur HTTPS. Configurer **HTTPS** en tant que protocole hello dans la configuration de la surveillance hello.

Traffic manager ne peut pas fournir de validation de certificat :

* Les certificats côté serveur ne sont pas validés.
* Les certificats SNI côté serveur ne sont pas pris en charge.
* Les certificats clients ne sont pas pris en charge.

### <a name="can-i-use-traffic-manager-even-if-my-application-does-not-have-support-for-http-or-https"></a>Puis-je utiliser Traffic Manager même si mon application ne prend pas en charge HTTP ou HTTPS ?

Oui. Vous pouvez spécifier TCP car hello analyse de protocole et Traffic Manager peut établir une connexion TCP et attendre une réponse à partir du point de terminaison hello. Si le point de terminaison hello répond toohello demande de connexion avec une connexion de hello tooestablish réponse, dans le délai d’attente hello point, puis sur ce point de terminaison est marqué comme étant intègre.

### <a name="what-specific-responses-are-required-from-hello-endpoint-when-using-tcp-monitoring"></a>Des réponses spécifiques sont nécessaires à partir du point de terminaison hello lorsque vous utilisez TCP analyse ?

Lors de la surveillance TCP est utilisé, Traffic Manager commence un TCP tridirectionnel en envoyant un SYN demande tooendpoint à hello port spécifié. Ensuite, il attend pendant une période de temps (comme spécifié dans les paramètres de délai d’attente hello) pour une réponse à partir du point de terminaison hello. Si le point de terminaison hello répond toohello SYN de requête avec une réponse SYN ACK dans hello délai imparti spécifié dans les paramètres d’analyse de hello, puis ce point de terminaison est considéré comme sain. Si hello réponse de SYN ACK est reçu, hello Traffic Manager réinitialise la connexion de hello par répond avec un RST.

### <a name="how-fast-does-traffic-manager-move-my-users-away-from-an-unhealthy-endpoint"></a>À quelle vitesse Traffic Manager éloigne-t-il mes utilisateurs d’un point de terminaison défectueux ?

Traffic Manager fournit plusieurs paramètres qui peuvent vous aider à comportement du basculement toocontrol hello de votre profil Traffic Manager comme suit :
- Vous pouvez spécifier que les points de terminaison hello hello pour Traffic Manager sondes plus fréquemment en définissant hello intervalle de détection à 10 secondes. Cela garantit que tout point de terminaison qui devient défectueux peut être détecté le plus tôt possible. 
- Vous pouvez spécifier la durée pendant laquelle expire toowait avant une demande de vérification d’intégrité (valeur de délai minimale est 5 secondes).
- Vous pouvez spécifier le nombre d’erreurs peut se produire avant le point de terminaison hello est marqué comme étant défectueux. Cette valeur peut être faible que 0, dans le point de terminaison hello cas est marqué comme défectueux dès qu’il ne parvient pas hello première vérification. Toutefois, à l’aide de la valeur minimale hello 0 pour nombre hello au terme d’échecs peut entraîner tooendpoints fait d’effectuer la rotation, en raison de problèmes transitoires tooany qui peuvent se produire au moment de hello de détection.
- Vous pouvez spécifier hello time-to-live (TTL) pour hello DNS réponse toobe aussi faible que 0. Cela signifie que les programmes de résolution DNS ne peut pas mettre en cache la réponse de hello et chaque nouvelle requête obtient une réponse qui incorpore les informations de contrôle d’intégrité plus récentes hello que hello Traffic Manager a.

À l’aide de ces paramètres, Traffic Manager peut fournir des basculements moins de 10 secondes après un point de terminaison devient non intègre et une requête DNS est effectuée sur le profil de hello correspondant.

### <a name="how-can-i-specify-different-monitoring-settings-for-different-endpoints-in-a-profile"></a>Comment spécifier différents paramètres de surveillance pour les différents points de terminaison dans un profil ?

Les paramètres de surveillance de Traffic Manager sont définis au niveau du profil. Si vous devez toouse un autre paramètre de surveillance pour qu’un seul point de terminaison, il est possible grâce à ce point de terminaison en tant qu’un [imbriqués profil](traffic-manager-nested-profiles.md) dont les paramètres de surveillance sont différents de profil parent de hello.

### <a name="what-host-header-do-endpoint-health-checks-use"></a>Quel en-tête hôte est utilisé pour les contrôles d’intégrité des points de terminaison ?

Traffic Manager utilise des en-têtes d’hôte pour les contrôles d’intégrité HTTP et HTTPS. en-tête d’hôte Hello utilisée par le Gestionnaire de trafic désigne hello hello cible de point de terminaison configuré dans le profil de hello. valeur de Hello utilisée dans l’en-tête d’hôte hello ne peut pas être spécifiée séparément à partir de la propriété de cible de hello.

### <a name="what-are-hello-ip-addresses-from-which-hello-health-checks-originate"></a>Quelles sont les adresses IP hello à partir de laquelle hello vérifications proviennent ?

Hello liste suivante contient des adresses IP hello à partir de laquelle contrôles peuvent provenir d’intégrité de Traffic Manager. Vous pouvez utiliser cette liste tooensure que les connexions entrantes à partir de ces adresses IP sont autorisées à toocheck des points de terminaison hello son état d’intégrité.

* 40.68.30.66
* 40.68.31.178
* 137.135.80.149
* 137.135.82.249
* 23.96.236.252
* 65.52.217.19
* 40.87.147.10
* 40.87.151.34
* 13.75.124.254
* 13.75.127.63
* 52.172.155.168
* 52.172.158.37
* 104.215.91.84
* 13.75.153.124
* 13.84.222.37
* 23.101.191.199
* 23.96.213.12
* 137.135.46.163
* 137.135.47.215
* 191.232.208.52
* 191.232.214.62
* 13.75.152.253
* 104.41.187.209
* 104.41.190.203

### <a name="how-many-health-checks-toomy-endpoint-can-i-expect-from-traffic-manager"></a>Point de terminaison toomy de vérifications d’intégrité combien puis-je attendre de Traffic Manager ?

nombre de Hello de contrôle d’intégrité de Traffic Manager vérifie atteindre votre point de terminaison varie suivant le hello :
- Hello valeur que vous avez définie pour l’intervalle d’analyse hello (intervalle plus petit signifie que davantage de demandes sur votre point de terminaison de destination dans une période donnée).
- nombre de Hello d’emplacements à partir de l’origine des contrôles d’intégrité de hello (hello adresses IP où vous pouvez vous attendre à ces vérifications est répertorié dans hello précédant le Forum aux questions).

## <a name="traffic-manager-nested-profiles"></a>Profils Traffic Manager imbriqués

### <a name="how-do-i-configure-nested-profiles"></a>Comment configurer des profils imbriqués ?

Profils Traffic Manager imbriqués peuvent être configurés à l’aide de deux hello Azure Resource Manager et hello classic API REST Azure, les applets de commande Azure PowerShell et les commandes de CLI d’Azure inter-plateformes. Elles sont également prises en charge via le nouveau portail de Azure hello. Elles ne sont pas prises en charge dans le portail classique de hello.

### <a name="how-many-layers-of-nesting-does-traffic-manger-support"></a>Combien de couches d’imbrication Traffic Manager prend-il en charge ?

Vous pouvez imbriquer des profils de too10 niveaux. Les « boucles » ne sont pas autorisées.

### <a name="can-i-mix-other-endpoint-types-with-nested-child-profiles-in-hello-same-traffic-manager-profile"></a>Puis-je combiner des autres types de point de terminaison avec des profils enfants imbriqués, en hello même profil Traffic Manager ?

Oui. Il n’existe aucune restriction sur la manière de combiner des points de terminaison de différents types au sein d’un profil.

### <a name="how-does-hello-billing-model-apply-for-nested-profiles"></a>Comment le modèle de facturation hello s’applique pour les profils imbriqués ?

Il n’y a aucun impact négatif sur la tarification en cas d’utilisation de profils imbriqués.

La facturation de Traffic Manager inclut deux composantes : des contrôles d’intégrité des points de terminaison et des millions de requêtes DNS.

* Contrôles d’intégrité des points de terminaison : aucun frais n’est facturé pour un profil enfant configuré en tant que point de terminaison dans un profil parent. Surveillance des points de terminaison hello dans le profil enfant hello est facturée Bonjour normalement.
* Requêtes DNS : chaque requête n’est comptabilisée qu’une seule fois. Une requête sur un profil parent qui retourne un point de terminaison à partir d’un profil enfant est comptée dans le profil parent hello uniquement.

Pour plus d’informations, consultez hello [page de tarification de Traffic Manager](https://azure.microsoft.com/pricing/details/traffic-manager/).

### <a name="is-there-a-performance-impact-for-nested-profiles"></a>Y a-t-il un impact sur les performances en cas de profils imbriqués ?

Non. Non, l’utilisation de profils imbriqués n’a aucune incidence sur les performances.

serveurs de noms de Traffic Manager Hello parcourent hello profil hiérarchie en interne lors du traitement de chaque requête DNS. Un profil de parent de tooa de requête DNS peut recevoir une réponse DNS avec un point de terminaison à partir d’un profil enfant. Un seul enregistrement CNAME est utilisé, que vous utilisiez un profil unique ou des profils imbriqués. Il n’a aucun toocreate besoin un enregistrement CNAME pour chaque profil dans la hiérarchie de hello.

### <a name="how-does-traffic-manager-compute-hello-health-of-a-nested-endpoint-in-a-parent-profile"></a>Comment Traffic Manager ne calcule pas la santé hello d’un point de terminaison imbriquée dans un profil parent ?

profil de parent Hello n’effectue pas les vérifications d’intégrité sur les enfants hello directement. Au lieu de cela, contrôle d’intégrité hello de points de terminaison du profil hello enfants sont utilisés toocalculate hello intégrité globale du profil de hello enfant. Cette information est propagée vers hello imbriqué hiérarchie toodetermine hello intégrité du profil du point de terminaison hello imbriqué. profil de parent Hello utilise cette toodetermine d’intégrité agrégé si le trafic de hello peut être dirigé toohello enfant.

Hello tableau suivant décrit le comportement de hello de Traffic Manager contrôles d’intégrité pour un point de terminaison imbriquée.

| État d’analyse des profils enfants | État d’analyse des points de terminaison parents | Remarques |
| --- | --- | --- |
| Désactivé. le profil enfant Hello a été désactivé. |Arrêté |état de point de terminaison parent Hello est arrêté, ne pas désactivé. Hello désactivé est réservé pour indiquer que vous avez désactivé le point de terminaison hello dans le profil de hello parent. |
| Détérioré. Au moins un point de terminaison du profil enfant a l’état Détérioré. |En ligne : hello nombre de points de terminaison en ligne dans le profil enfant hello est au moins hello la valeur de MinChildEndpoints.<BR>CheckingEndpoint : hello nombre de points de terminaison en ligne plus CheckingEndpoint dans le profil enfant hello est au moins hello la valeur de MinChildEndpoints.<BR>Détérioré : dans le cas contraire. |Le trafic est routé tooan de point de terminaison de l’état CheckingEndpoint. Si MinChildEndpoints est trop élevée, point de terminaison hello est toujours détérioré. |
| En ligne. Au moins un point de terminaison de profil enfant est en état En ligne. Aucun point de terminaison n’est hello état détérioré. |Voir ci-dessus. | |
| CheckingEndpoints. Au moins un point de terminaison de profil enfant est en état « CheckingEndpoint ». Aucun point de terminaison n’est en état « En ligne » ou « Détérioré ». |Identique à ce qui précède. | |
| Inactif. Tous les points de terminaison du profil enfant sont en état Désactivé ou Arrêté, ou ce profil n’a aucun point de terminaison. |Arrêté | |

## <a name="next-steps"></a>Étapes suivantes :
- En savoir plus sur le [basculement automatique et la surveillance des points de terminaison](../traffic-manager/traffic-manager-monitoring.md)de Traffic Manager.
- En savoir plus sur les [méthodes de routage du trafic](../traffic-manager/traffic-manager-routing-methods.md)de Traffic Manager.