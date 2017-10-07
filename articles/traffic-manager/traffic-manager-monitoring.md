---
title: surveillance de point de terminaison de Traffic Manager aaaAzure | Documents Microsoft
description: "Cet article peut vous aider à comprendre comment Traffic Manager utilise toohelp de basculement de point de terminaison automatique Azure et de surveillance de point de terminaison clients déploient des applications de haute disponibilité"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: fff25ac3-d13a-4af9-8916-7c72e3d64bc7
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/22/2017
ms.author: kumud
ms.openlocfilehash: b4862499c88bdb1951833d06199b034a07ac7576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-endpoint-monitoring"></a>Surveillance des points de terminaison Traffic Manager

Azure Traffic Manager inclut la surveillance intégrée des points de terminaison et leur basculement automatique. Cette fonctionnalité vous permet d’offrir des applications de haute disponibilité sont résilientes tooendpoint échec, notamment les échecs de la région Azure.

## <a name="configure-endpoint-monitoring"></a>Configuration de la surveillance des points de terminaison

analyse de point de terminaison tooconfigure, vous devez spécifier hello suivant les paramètres de votre profil Traffic Manager :

* **Protocole**. Choisissez HTTP, HTTPS ou TCP comme protocole de hello Traffic Manager utilise lors de la détection de votre point de terminaison toocheck son intégrité. Surveillance HTTPS ne vérifie pas si votre certificat SSL est valide, elle vérifie seulement que hello certificat est présent.
* **Port**. Choisissez le port hello utilisé pour la demande de hello.
* **Chemin d’accès**. Ce paramètre de configuration est valide uniquement pour les protocoles HTTP et HTTPS hello, pour lequel le paramètre de chemin d’accès spécifiant hello est nécessaire. Fourniture de ce paramètre pour hello TCP analyse protocole entraîne une erreur. Pour le protocole TCP, indiquer chemin d’accès relatif de hello et hello de page Web de hello ou un fichier de hello que hello analyse d’accès. Une barre oblique (/) est une entrée valide pour le chemin d’accès relatif de hello. Cette valeur indique que le fichier hello se trouve dans le répertoire racine de hello (par défaut).
* **Intervalle de détection**. Cette valeur spécifie la fréquence à laquelle l’intégrité d’un point de terminaison est contrôlée par un agent de détection Traffic Manager. Vous pouvez spécifier deux valeurs ici : 30 secondes (détection normale) et 10 secondes (détection rapide). Si aucune valeur n’est fourni, le profil de hello définit tooa par défaut de 30 secondes. Visitez hello [Traffic Manager tarification](https://azure.microsoft.com/pricing/details/traffic-manager) toolearn page plus sur la tarification de détection rapide.
* **Nombre d’échecs tolérés**. Cette valeur spécifie le nombre d’échecs tolérés par un agent de détection de Traffic Manager avant que le point de terminaison soit considéré comme défectueux. La valeur peut être comprise entre 0 et 9. Une valeur de 0 signifie un échec d’analyse unique peut entraîner ce toobe de point de terminaison considéré comme défectueux. Si aucune valeur n’est spécifiée, elle utilise la valeur par défaut 3 hello.
* **Délai d’expiration de la surveillance**. Cette propriété spécifie hello hello de temps Traffic Manager détection de l’agent doit attendre avant de considérer que vérifier un échec lorsqu’un sondage de vérification d’intégrité est envoyé toohello le point de terminaison. Si hello Qu'intervalle de détection est défini too30 secondes, puis vous peut définir la valeur de délai d’attente hello entre 5 et 10 secondes. Si aucune valeur n’est spécifiée, la valeur par défaut est 10 secondes. Si hello Qu'intervalle de détection est défini too10 secondes, puis vous peut définir la valeur de délai d’attente hello comprise entre 5 et 9. Si aucune valeur n’est spécifiée pour le délai d’expiration, la valeur par défaut est 9 secondes.

![Surveillance des points de terminaison Traffic Manager](./media/traffic-manager-monitoring/endpoint-monitoring-settings.png)

**Figure 1 : surveillance des points de terminaison Traffic Manager**

## <a name="how-endpoint-monitoring-works"></a>Fonctionnement de la surveillance des points de terminaison

Si hello analyse protocole est défini en tant que HTTP ou HTTPS, agent de détection de Traffic Manager hello crée un point de terminaison toohello de demande GET à l’aide de hello protocole, port et chemin d’accès relatif donné. S’il obtient une réponse 200-OK, ce point de terminaison est considéré comme sain. Si la réponse de hello est une valeur différente, ou, si aucune réponse n’est reçue dans le délai d’attente hello spécifié, hello Traffic Manager de détection de l’agent essaie selon le paramètre tolérée le nombre d’échecs de toohello (aucune essaie n’est effectuées si ce paramètre est 0) . Si nombre hello d’échecs consécutifs est supérieur au paramètre hello tolérée le nombre d’échecs, ce point de terminaison est considéré comme défectueux. 

Si hello analyse protocole est TCP, agent de détection de Traffic Manager hello lance une demande de connexion TCP à l’aide du port hello spécifié. Si le point de terminaison hello répond demande toohello une réponse tooestablish hello connexion que contrôle d’intégrité est marqué comme une réussite et agent de détection de Traffic Manager hello réinitialise la connexion TCP de hello. Si la réponse de hello est une valeur différente, ou si aucune réponse n’est reçue dans la période du délai d’attente hello spécifiée, hello Traffic Manager de détection de l’agent essaie en fonction du paramètre de tolérée le nombre d’échecs toohello (aucune essaie n’est effectuées si ce paramètre est 0). Si nombre hello d’échecs consécutifs est supérieur au paramètre hello tolérée le nombre d’échecs, ce point de terminaison est marqué comme défectueux.

Dans tous les cas, les tests de Traffic Manager à partir de plusieurs emplacements et détermination de pannes consécutives hello se produit dans chaque région. Cela signifie également que points de terminaison reçoivent sondes d’intégrité à partir de Traffic Manager avec une fréquence plus élevée que le paramètre hello utilisé pour l’intervalle de détection.

>[!NOTE]
>Pour HTTP ou HTTPS, protocole d’analyse, une pratique courante sur le côté du point de terminaison hello est tooimplement une page personnalisée dans votre application - par exemple, /health.aspx. À l’aide de ce chemin d’accès pour la surveillance, vous pouvez effectuer des vérifications spécifiques aux applications, telles que la vérification des compteurs de performance ou de la disponibilité de la base de données. En fonction de ces contrôles personnalisés, la page de hello retourne un code d’état HTTP approprié.

Tous les points de terminaison dans un profil Traffic Manager partagent les mêmes paramètres de surveillance. Si vous avez besoin de toouse différents paramètres de surveillance pour les différents points de terminaison, vous pouvez créer [imbriqués profils Traffic Manager](traffic-manager-nested-profiles.md#example-5-per-endpoint-monitoring-settings).

## <a name="endpoint-and-profile-status"></a>État des points de terminaison et des profils

Vous pouvez activer et désactiver les points de terminaison et les profils Traffic Manager. Toutefois, un changement d’état du point de terminaison peut survenir également comme conséquence des paramètres et des processus automatisés de Traffic Manager.

### <a name="endpoint-status"></a>État du point de terminaison

Vous pouvez activer ou désactiver un point de terminaison spécifique. service sous-jacent Hello, qui pourrait toujours être sain, n’est pas affectée. Contrôles d’état de point de terminaison hello modification hello disponibilité du point de terminaison hello Bonjour profil Traffic Manager. Lorsqu’un état de point de terminaison est désactivé, Traffic Manager ne vérifie pas son intégrité et le point de terminaison hello n’est pas inclus dans une réponse DNS.

### <a name="profile-status"></a>État du profil

À l’aide du paramètre de l’état hello profil, vous pouvez activer ou désactiver un profil spécifique. Alors que l’état du point de terminaison concerne un seul point de terminaison, l’état du profil affecte profil entier hello, y compris tous les points de terminaison. Lorsque vous désactivez un profil, les points de terminaison hello ne sont pas vérifiées pour la santé et aucun point de terminaison n’est inclus dans une réponse DNS. Un [NXDOMAIN](https://tools.ietf.org/html/rfc2308) code de réponse est retourné pour une requête DNS hello.

### <a name="endpoint-monitor-status"></a>État de surveillance des points de terminaison

État de surveillance de point de terminaison est une valeur générée par le Gestionnaire de trafic qui présente l’état de hello de point de terminaison hello. Vous ne pouvez pas modifier ce paramètre manuellement. état de surveillance de point de terminaison Hello est une combinaison de résultats hello de surveillance de point de terminaison et hello état du point de terminaison configuré. les valeurs d’état de surveillance de point de terminaison Hello sont présentées hello tableau suivant :

| État du profil | État du point de terminaison | État de surveillance des points de terminaison | Remarques |
| --- | --- | --- | --- |
| Désactivé |Activé |Inactif |profil de Hello a été désactivé. Bien que l’état du point de terminaison hello est activé, l’état du profil hello (désactivé) est prioritaire. Dans les profils désactivés, les points de terminaison ne sont pas surveillés. Un code de réponse NXDOMAIN est retourné pour la requête DNS de hello. |
| &lt;any&gt; |Désactivé |Désactivé |point de terminaison Hello a été désactivé. Les points de terminaison désactivés ne sont pas surveillés. point de terminaison Hello n’est pas inclus dans les réponses DNS, par conséquent, il ne reçoit pas de trafic. |
| Activé |Activé |En ligne |point de terminaison Hello est analysée et est intègre. Il est inclus dans les réponses DNS et peut recevoir le trafic. |
| Activé |Activé |Détérioré |Les contrôles d’intégrité de surveillance des points de terminaison sont défaillants. point de terminaison Hello n’est pas inclus dans les réponses DNS et ne reçoit pas de trafic. <br>Une exception toothis est si tous les points de terminaison sont défectueux, auquel cas tous les sont considérés comme toobe retournée dans la réponse de requête hello).</br>|
| Activé |Activé |CheckingEndpoint |point de terminaison Hello est surveillé, mais des résultats de la première sonde de hello hello n’ont pas encore été reçus. CheckingEndpoint est un état temporaire qui se produit généralement immédiatement après l’ajout ou l’activation d’un point de terminaison dans le profil de hello. Un point de terminaison avec cet état est inclus dans les réponses DNS et peut recevoir le trafic. |
| Activé |Activé |Arrêté |Hello cloud service ou une application web qui hello toois de points de terminaison ne pas en cours d’exécution. Vérifiez les paramètres application hello cloud service ou web. Cela peut également se produire si le point de terminaison de hello est de type imbriqué de point de terminaison et le profil enfant hello est désactivé ou n’est pas active. <br>Un point de terminaison avec l’état Arrêté n’est pas surveillé. Il n’est pas inclus dans les réponses DNS et ne reçoit pas de trafic. Une exception toothis est si tous les points de terminaison sont défectueux, auquel cas tous les sont considérés comme toobe retournée dans la réponse de requête hello.</br>|

Pour savoir comment l’état de surveillance des points de terminaison est calculé pour les points de terminaison imbriqués, consultez la section relative aux [profils Traffic Manager imbriqués](traffic-manager-nested-profiles.md).

### <a name="profile-monitor-status"></a>État de surveillance du profil

état de surveillance de profil Hello est une combinaison de l’état du profil hello configuré et les valeurs d’état analyse hello point de terminaison pour tous les points de terminaison. les valeurs possibles de Hello sont décrites dans hello tableau suivant :

| État du profil (conformément à la configuration) | État de surveillance des points de terminaison | État de surveillance du profil | Remarques |
| --- | --- | --- | --- |
| Désactivé |&lt;any&gt;  ou profil sans points de terminaison définis. |Désactivé |profil de Hello a été désactivé. |
| Activé |état de Hello d’au moins un point de terminaison est dégradé. |Détérioré |Passez en revue les valeurs d’état point de terminaison individuel d’hello toodetermine quels points de terminaison exigeant une attention accrue. |
| Activé |état Hello d’au moins un point de terminaison est en ligne. Aucun point de terminaison n’a l’état Détérioré. |En ligne |Hello service accepte le trafic. Aucune action supplémentaire n’est requise. |
| Activé |état de Hello d’au moins un point de terminaison est CheckingEndpoint. Aucun point de terminaison n’a l’état En ligne ou Détérioré. |CheckingEndpoints |Cet état de transition se produit lorsqu’un profil est créé ou activé. contrôle d’intégrité du point de terminaison Hello est en cours de vérification pour hello première fois. |
| Activé |États de Hello de tous les points de terminaison dans le profil de hello sont désactivé ou arrêté ou profil de hello n’a aucun point de terminaison défini. |Inactif |Aucun point de terminaison n’est actifs, mais hello profil est toujours activé. |

## <a name="endpoint-failover-and-recovery"></a>Basculement et récupération du point de terminaison

Traffic Manager vérifie périodiquement l’intégrité de hello de chaque point de terminaison, y compris les points de terminaison non intègres. Traffic Manager détecte lorsque l’intégrité d’un point de terminaison est rétablie et ramène celui-ci en rotation.

Un point de terminaison n’est pas sain lorsqu’un des hello suivant des événements se produisent :
- Si hello analyse le protocole est HTTP ou HTTPS :
    - Réception d’une réponse autre que 200 (y compris un code 2xx différent ou une redirection 301/302).
- Si hello analyse protocole est TCP : 
    - Une réponse autre que l’accusé de réception ou SYN-ACK est reçu dans la demande de synchronisation toohello de réponse envoyé par Traffic Manager tooattempt un établissement de la connexion.
- Délai d’expiration. 
- Tout autre problème de connexion aboutissant à un point de terminaison hello n’est ne pas accessible.

Pour plus d’informations sur le dépannage des vérifications en échec, consultez [Résolution des problèmes liés à l’état Détérioré d’Azure Traffic Manager](traffic-manager-troubleshooting-degraded.md). 

Bonjour chronologie suivante dans la Figure 2 est une description détaillée de hello processus du point de terminaison Traffic Manager a hello suivant les paramètres d’analyse : analyse de protocole est HTTP, intervalle de détection est de 30 secondes, nombre d’échecs autorisés est 3, la valeur de délai d’attente est de 10 secondes et le TTL du DNS est de 30 secondes.

![Séquence de basculement et de restauration automatique des points de terminaison Traffic Manager](./media/traffic-manager-monitoring/timeline.png)

**Figure 2 : séquence de basculement et de récupération des points de terminaison Traffic Manager**

1. **GET**. Pour chaque point de terminaison, hello système de surveillance de Traffic Manager effectue une demande GET sur le chemin d’accès de hello spécifié dans les paramètres d’analyse de hello.
2. **200 OK**. système de surveillance de Hello attend un toobe de message HTTP 200 OK retourné dans les 10 secondes. Lorsqu’il reçoit cette réponse, il reconnaît que hello service est disponible.
3. **30 secondes entre les contrôles**. contrôle d’intégrité de point de terminaison Hello est répété toutes les 30 secondes.
4. **Service indisponible**. Hello service devient indisponible. Traffic Manager ne saura pas jusqu'à ce que le contrôle d’intégrité de la prochaine hello.
5. **Hello tooaccess de tentatives analyse le chemin d’accès**. système de surveillance de Hello effectue une demande GET, mais ne reçoit pas une réponse dans un délai de 10 secondes d’attente hello (sinon, une réponse non-200 peut-être être reçue). Il effectue ensuite trois essais supplémentaires par intervalles de 30 secondes. Si une des tentatives de hello est réussie, nombre hello de tentatives est réinitialisé.
6. **État défini tooDegraded**. Panne d’un quatrième consécutifs, hello système de surveillance marque état du point de terminaison non disponible hello comme étant dégradé.
7. **Le trafic est points de terminaison transférés tooother**. Hello serveurs de noms DNS Traffic Manager sont mises à jour et Traffic Manager renvoie le point de terminaison hello n’est plus dans les requêtes tooDNS de réponse. Les nouvelles connexions sont dirigée tooother, points de terminaison disponibles. Toutefois, les réponses DNS précédentes incluant ce point de terminaison peuvent toujours être mises en cache par des serveurs DNS et des clients DNS récursifs. Les clients continuent de point de terminaison toouse hello jusqu'à l’expiration de hello cache DNS. Comme hello cache DNS arrive à expiration, les clients rendre les nouvelles requêtes DNS et sont des points de terminaison toodifferent dirigée. durée du cache de Hello est contrôlée par le paramètre de durée de vie hello Bonjour profil Traffic Manager, par exemple, 30 secondes.
8. **Les contrôles d’intégrité continuent**. Traffic Manager continue d’intégrité de hello toocheck du point de terminaison hello tant qu’il dispose d’un état Degraded (détérioré). Traffic Manager détecte lorsque le point de terminaison hello retourne toohealth.
9. **Le service est remis en ligne**. service de Hello devient disponible. point de terminaison Hello conserve son état dégradé de Traffic Manager jusqu'à ce que le système de surveillance de hello effectue sa prochaine vérification d’intégrité.
10. **Le trafic tooservice reprend**. Traffic Manager envoie une requête GET et reçoit une réponse d’état 200 OK. service de Hello a retourné l’état d’intégrité tooa. serveurs de noms Hello Traffic Manager sont mises à jour, et ils commencent toohand nom du DNS du service hello dans les réponses DNS. Le trafic retourne le point de terminaison de toohello expirent des réponses DNS mises en cache qui retournent d’autres points de terminaison, comme les connexions existantes tooother de points de terminaison sont terminées.

    > [!NOTE]
    > Étant donné que Traffic Manager fonctionne au niveau DNS de hello, il ne peut pas influence le point de terminaison existant connexions tooany. Lorsqu’il dirige le trafic entre les points de terminaison (soit par les paramètres de profil modifié, ou lors du basculement ou la restauration automatique), Traffic Manager dirige les nouveaux points de terminaison connexions tooavailable. Autres points de terminaison peuvent néanmoins tooreceive du trafic via les connexions existantes jusqu'à ce que les sessions sont arrêtées. tooenable toodrain de trafic à partir des connexions existantes, les applications doivent limiter hello durée de session utilisée avec chaque point de terminaison.

## <a name="traffic-routing-methods"></a>Méthodes de routage du trafic

Lorsqu’un point de terminaison a un état Degraded (détérioré), il n’est plus retournée dans les requêtes de tooDNS de réponse. Au lieu de cela, un autre point de terminaison est choisi et renvoyé. méthode de routage du trafic Hello configuré dans le profil de hello détermine comment le point de terminaison autre hello est choisi.

* **Priorité**. Les points de terminaison forment une liste hiérarchisée. Hello premier point de terminaison disponible sur la liste de hello est toujours retournée. Si un état de point de terminaison est endommagée, point de terminaison disponible hello suivant est retourné.
* **Pondération**. N’importe quel point de terminaison disponible est choisi au hasard selon leurs poids attribués et hello poids de hello autres points de terminaison disponibles.
* **Performances**. Hello point de terminaison le plus proche toohello utilisateur est retourné. Si ce point de terminaison n’est pas disponible, un point de terminaison est sélectionnée de manière aléatoire toutes hello autres points de terminaison disponibles. Choix d’un point de terminaison aléatoire permet d’éviter un échec en cascade qui peut se produire lorsque le point de terminaison le plus proche suivant hello est surchargé. Vous pouvez configurer d’autres plans de basculement pour le routage du trafic à l’aide des [profils Traffic Manager imbriqués](traffic-manager-nested-profiles.md#example-4-controlling-performance-traffic-routing-between-multiple-endpoints-in-the-same-region).
* **Géographique**. point de terminaison Hello mappé tooserve hello géographique en fonction de la demande de requête hello que l’adresse IP est retournée. Si ce point de terminaison n’est pas disponible, un autre point de terminaison ne sera pas sélectionné toofailover, depuis un emplacement géographique peut être mappé uniquement tooone point de terminaison dans un profil (plus de détails sont Bonjour [FAQ](traffic-manager-FAQs.md#traffic-manager-geographic-traffic-routing-method)). Comme meilleure pratique, lorsque vous utilisez le routage géographique, nous recommandons aux clients des profils Traffic Manager toouse imbriqué avec plus d’un point de terminaison en tant que points de terminaison hello du profil de hello.

Pour plus d’informations, consultez la rubrique relative aux [méthodes de routage du trafic dans Traffic Manager](traffic-manager-routing-methods.md).

> [!NOTE]
> Le routage du trafic comportement d’une exception toonormal se produit lorsque tous les points de terminaison éligibles ont un état détérioré. Rend Traffic Manager « meilleur effort » tentative et *répond comme si tous les points de terminaison d’état détérioré hello sont réellement en ligne*. Ce comportement est également préférable toohello qu’il serait toonot retourner tout point de terminaison Bonjour réponse DNS. Les points de terminaison désactivés ou arrêtés ne sont pas surveillés et ne sont par conséquent pas éligibles pour le trafic.
>
> Cette condition est généralement dû à une configuration incorrecte du service de hello, telles que :
>
> * Liste contrôle d’accès [ACL] bloque les contrôles d’intégrité de Traffic Manager hello.
> * Une configuration incorrecte de hello analyse de port ou protocole Bonjour du profil Traffic manager.
>
> Hello conséquence de ce comportement est que si les contrôles d’intégrité de Traffic Manager ne sont pas configurés correctement, il peut sembler du trafic hello routage comme si elles étaient Traffic Manager *est* fonctionne correctement. Toutefois, dans ce cas, le basculement de point de terminaison ne peut pas se produire, ce qui affecte la disponibilité globale de l’application. Il est important toocheck que le profil de hello affiche un état en ligne, pas un état Degraded (détérioré). Un état en ligne indique que hello Traffic Manager vérifications fonctionnent comme prévu.

Pour plus d’informations sur le dépannage des contrôles d’intégrité, consultez la section [Résolution des problèmes liés à l’état Détérioré d’Azure Traffic Manager](traffic-manager-troubleshooting-degraded.md).



## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur le [fonctionnement de Traffic Manager](traffic-manager-how-traffic-manager-works.md)

En savoir plus sur hello [des méthodes de routage de trafic](traffic-manager-routing-methods.md) pris en charge par le Gestionnaire de trafic

Découvrez comment trop[créer un profil Traffic Manager](traffic-manager-manage-profiles.md)

[Résolution des problèmes liés à l’état Détérioré](traffic-manager-troubleshooting-degraded.md) sur un point de terminaison Traffic Manager
