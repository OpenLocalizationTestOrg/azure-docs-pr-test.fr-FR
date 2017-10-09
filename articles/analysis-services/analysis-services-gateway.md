---
title: "passerelle de données local aaaOn | Documents Microsoft"
description: "Une passerelle locale est nécessaire si votre serveur Analysis Services dans Azure doivent se connecter à des sources de données tooon local."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: cd596155-b608-4a34-935e-e45c95d884a9
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: fc7b9c69e6f81b41deb7a5d6d963225593845d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-tooon-premises-data-sources-with-azure-on-premises-data-gateway"></a>Connexion des sources de données tooon local avec la passerelle de données Azure localement
passerelle de données locale Hello agit comme un pont, assurant le transfert sécurisé des données entre des sources de données sur site et vos serveurs Azure Analysis Services dans le cloud de hello. Dans tooworking Ajout avec plusieurs serveurs Azure Analysis Services Bonjour même région, version la plus récente de la passerelle de hello hello fonctionne également avec Azure Logic Apps, Power BI, les applications Power et Microsoft Flow. Vous pouvez associer plusieurs services Bonjour même région avec une seule passerelle. 

 Azure Analysis Services nécessite une ressource de la passerelle Bonjour même région. Par exemple, si vous avez des serveurs Azure Analysis Services dans la région est des États-Unis 2 hello, vous devez une ressource de passerelle dans la région est des États-Unis 2 hello. Plusieurs serveurs est des États-Unis 2 peuvent utiliser hello même passerelle.

Le programme d’installation avec hello de passerelle hello première est un processus en quatre parties :

- **Télécharger et exécuter le programme d’installation** - Cette étape installe un service de passerelle sur un ordinateur de votre organisation.

- **Inscrivez votre passerelle** : dans cette étape, vous spécifiez un nom et la récupération de clé pour votre passerelle et sélectionnez une région, l’inscription de votre passerelle avec hello Service Cloud de passerelle.

- **Créer une ressource de passerelle dans Azure** - Lors de cette étape, vous créez une ressource de passerelle dans votre abonnement Azure.

- **Se connecter à vos ressources de passerelle serveurs tooyour** -une fois que vous avez une ressource de la passerelle dans votre abonnement, vous pouvez commencer à se connecter à votre tooit de serveurs.

Une fois que vous avez une ressource de la passerelle configurée pour votre abonnement, vous pouvez connecter plusieurs serveurs et autres tooit de services. Uniquement, vous devez tooinstall une autre passerelle et créez des ressources de passerelle supplémentaire si vous avez des serveurs ou autres services dans une autre région.

tooget démarré immédiatement, consultez [installer et configurer la passerelle de données locale](analysis-services-gateway-install.md).

## <a name="how-it-works"></a>Fonctionnement
passerelle Hello vous installez sur un ordinateur de votre organisation s’exécute comme un service Windows, **passerelle de données locale**. Ce service local est inscrit avec hello Service de Cloud de passerelle via Azure Service Bus. Vous créez ensuite la ressource de passerelle correspondante pour votre abonnement Azure. Analysis Services Azure sont ensuite des serveurs connectés tooyour ressource de la passerelle. Lorsque les modèles sur votre tooyour tooconnect du besoin de serveur local pour les requêtes ou le traitement des sources de données, une requête et les données de flux qui traverse hello passerelle ressource, Azure Service Bus, hello service de passerelle de données sur site local et vos sources de données. 

![Fonctionnement](./media/analysis-services-gateway/aas-gateway-how-it-works.png)

Requêtes et flux de données :

1. Une requête est créée par le service de cloud hello avec informations d’identification chiffrée de hello pour la source de données locale hello. Il a ensuite envoyées hello passerelle tooprocess tooa file d’attente.
2. service de cloud de passerelle Hello analyse hello requête et exécute un push de hello demande toohello [Azure Service Bus](https://azure.microsoft.com/documentation/services/service-bus/).
3. passerelle de données locale Hello interroge hello Azure Service Bus pour les demandes en attente.
4. passerelle de Hello obtient hello requête, déchiffre les informations d’identification hello et connecte des sources de données toohello avec ces informations d’identification.
5. passerelle de Hello envoie hello toohello récupérer les données pour l’exécution.
6. résultats de Hello sont envoyés de source de données hello toohello arrière passerelle, puis sur le service de cloud computing hello et votre serveur.

## <a name="windows-service-account"></a>Compte de service Windows
Bonjour passerelle de données locale est configurée toouse *NT SERVICE\PBIEgwService* d’identification de connexion du service Windows hello. Par défaut, elle a hello droit d’ouverture de session en tant que service ; dans le contexte hello d’ordinateur hello que vous installez la passerelle de hello sur. Ces informations d’identification n’est pas hello mêmes sources de données de site tooon compte utilisé tooconnect ou votre compte Azure.  

Si vous rencontrez des problèmes avec votre serveur proxy en raison tooauthentication, vous souhaiterez peut-être toochange hello Windows service utilisateur du compte de domaine tooa ou gérés compte de service.

## <a name="ports"></a>Ports
passerelle de Hello crée une connexion sortante de tooAzure Service Bus. Elle communique sur les ports sortants : TCP 443 (par défaut), 5671, 5672 et 9350 à 9354.  passerelle de Hello ne nécessite pas de ports entrants.

Nous vous recommandons des adresses IP whitelist hello pour votre région de données dans votre pare-feu. Vous pouvez télécharger hello [liste IP de centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). Cette liste est actualisée chaque semaine.

> [!NOTE]
> Hello des adresses IP répertoriées dans la liste d’IP de centre de données Azure hello sont en notation CIDR. Par exemple, 10.0.0.0/24 ne signifie pas 10.0.0.0 à 10.0.0.24. En savoir plus sur hello [la notation CIDR](http://whatismyipaddress.com/cidr).
>
>

Hello Voici les noms de domaine hello complet utilisés par la passerelle de hello.

| Noms de domaine | Ports sortants | Description |
| --- | --- | --- |
| *. powerbi.com |80 |Le protocole HTTP utilisé le programme d’installation de toodownload hello. |
| *. powerbi.com |443 |HTTPS |
| *.analysis.windows.net |443 |HTTPS |
| *.login.windows.net |443 |HTTPS |
| *.servicebus.windows.net |5671-5672 |Advanced Message Queuing Protocol (AMQP) |
| *.servicebus.windows.net |443, 9350-9354 |Récepteurs du Service Bus Relay sur TCP (nécessite le port 443 pour l’acquisition du jeton Access Control) |
| *.frontend.clouddatahub.net |443 |HTTPS |
| *.core.windows.net |443 |HTTPS |
| login.microsoftonline.com |443 |HTTPS |
| *.msftncsi.com |443 |Utilisé une connectivité internet tootest si la passerelle de hello est inaccessible par hello service Power BI. |
| *.microsoftonline-p.com |443 |Utilisé pour l’authentification en fonction de la configuration. |

### <a name="force-https"></a>Forcer les communications HTTPS avec Azure Service Bus
Vous pouvez forcer toocommunicate de passerelle hello avec Azure Service Bus à l’aide de HTTPS au lieu de direct TCP ; Toutefois, cette opération donc peut considérablement réduire les performances. Vous pouvez modifier hello *Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config* fichier en modifiant la valeur hello `AutoDetect` trop`Https`. Ce fichier se trouve généralement dans *C:\Program Files\On-premises data gateway*.

```
<setting name="ServiceBusSystemConnectivityModeString" serializeAs="String">
    <value>Https</value>
</setting>
```

## <a name="faq"></a>Forum Aux Questions

### <a name="general"></a>Généralités

**Q**: ai-je besoin d’une passerelle pour les sources de données dans le cloud hello, tels que de la base de données SQL Azure ? <br/>
**R** : Non. Une passerelle connecte à des sources de données tooon local uniquement.

**Q**: passerelle de hello a-t-elle toobe installé sur hello même ordinateur en tant que source de données hello ? <br/>
**R** : Non. passerelle de Hello connecte toohello source de données à l’aide des informations de connexion hello qui a été fournies. Envisagez de passerelle de hello comme une application cliente en ce sens. Hello passerelle doit juste hello capacité tooconnect toohello nom du serveur qui a été fourni, généralement sur hello même réseau.

<a name="why-azure-work-school-account"></a>

**Q**: Pourquoi devez toouse Professionnel ou scolaire toosign compte dans ? <br/>
**Un**: vous pouvez uniquement utiliser un travail Azure ou scolaire compte lorsque vous installez la passerelle de données locale hello. Votre compte de connexion est stocké dans un client géré par Azure Active Directory (Azure AD). En règle générale, le nom de principal d’utilisateur (UPN) de votre compte Azure AD correspond à adresse de messagerie hello.

**Q** : où mes informations d’identification sont-elles stockées ? <br/>
**A**: informations d’identification hello que vous entrez pour une source de données sont chiffrées et stockées dans hello Service Cloud de passerelle. informations d’identification Hello sont déchiffrées au niveau de la passerelle de données locale hello.

**Q** : Existe-t-il des exigences concernant la bande passante réseau ? <br/>
**R** : Il est recommandé d’utiliser une connexion réseau offrant un bon débit. Chaque environnement est différent, et quantité hello des données envoyées affecte les résultats hello. À l’aide d’ExpressRoute peut aider à tooguarantee un niveau de débit entre hello centres de données Azure et locaux.
Vous pouvez utiliser hello un outil tiers Azure Speed Test application toohelp jauge votre débit.

**Q**: quelle est la latence hello pour la source de données en cours d’exécution des requêtes tooa à partir de la passerelle de hello ? Quelle est la meilleure architecture de hello ? <br/>
**A**: tooreduce latence du réseau, passerelle de hello installer en tant que source de données toohello fermer que possible. Si vous pouvez installer la passerelle de hello sur la source de données réelle hello, cette proximité réduit la latence de hello introduite. Envisagez de centres de données hello trop. Par exemple, si votre service utilise hello ouest des États-Unis centre de données, et que SQL Server est hébergé dans une machine virtuelle Azure, votre machine virtuelle Azure doit être trop Bonjour ouest des États-Unis. Cette proximité réduit la latence et évite les frais de sortie sur hello machine virtuelle Azure.

**Q**: comment sont envoyées toohello arrière cloud ? <br/>
**A**: les résultats sont envoyés via hello Azure Service Bus.

**Q**: existe-t-il toute passerelle toohello de connexions entrantes à partir du cloud de hello ? <br/>
**R** : Non. passerelle de Hello utilise des connexions sortantes tooAzure Service Bus.

**Q** : Que se passe-t-il si je bloque les connexions sortantes ? Comment dois-je tooopen ? <br/>
**A**: consultez les ports hello et les hôtes qui hello passerelle utilise.

**Q**: ce que le service de Windows hello réel est appelé ?<br/>
**A**: dans les Services, passerelle de hello est appelé service de passerelle de données locale.

**Q**: pouvez hello service Windows de passerelle s’exécuter avec un compte Azure Active Directory ? <br/>
**R** : Non. Hello service Windows doit avoir un compte Windows valide. Par défaut, le service de hello s’exécute avec hello SID de Service, NT SERVICE\PBIEgwService.

### <a name="high-availability"></a>Haute disponibilité et récupération d’urgence

**Q** : Quelles sont les options de récupération d’urgence disponibles ? <br/>
**Un**: vous pouvez utiliser toorestore de clé de récupération hello ou déplacer une passerelle. Lorsque vous installez la passerelle de hello, spécifiez la clé de récupération hello.

**Q**: quels sont les avantages de hello de clé de récupération hello ? <br/>
**A**: clé de récupération hello fournit un moyen toomigrate ou récupérer vos paramètres de passerelle après un sinistre.

## <a name="troubleshooting"></a>Résolution des problèmes

**Q**: Comment puis-je savoir quelles requêtes sont envoyées source de données locale toohello ? <br/>
**Un**: vous pouvez activer le traçage de requête, qui inclut les requêtes hello qui sont envoyées. N’oubliez pas de requête toochange en remontant la valeur d’origine de toohello faite le problème résolu. Le fait de laisser activé le traçage des requêtes contribue à augmenter la taille des journaux.

Vous pouvez également utiliser les outils de suivi des requêtes proposés par votre source de données. Par exemple, vous pouvez utiliser Extended Events ou SQL Profiler for SQL Server et Analysis Services.

**Q**: où se trouvent les journaux de passerelle hello ? <br/>
**R**: Voir la section Journaux plus loin dans cette rubrique.

### <a name="update"></a>Mettre à jour la version la plus récente toohello

Nombreux problèmes peuvent apparaître lors de la version de la passerelle hello devient obsolète. Comme recommandé, assurez-vous d’utiliser la version la plus récente hello. Si vous n’avez pas mis à jour de passerelle de hello pendant un mois ou plus, vous pouvez envisager d’installer la version la plus récente de la passerelle de hello hello et voir si vous pouvez reproduire le problème de hello.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Erreur : Échec de tooadd utilisateur toogroup. (-2147463168 PBIEgwService Performance Log Users)

Vous pouvez obtenir cette erreur si vous essayez de passerelle de hello tooinstall sur un contrôleur de domaine, ce qui n’est pas pris en charge. Assurez-vous que vous déployez la passerelle de hello sur un ordinateur qui n’est pas un contrôleur de domaine.

## <a name="logs"></a>Journaux

Les fichiers journaux constituent une ressource importante lors du dépannage.

#### <a name="enterprise-gateway-service-logs"></a>Journaux du service de passerelle Enterprise

`C:\Users\PBIEgwService\AppData\Local\Microsoft\On-premises data gateway\<yyyyymmdd>.<Number>.log`

#### <a name="configuration-logs"></a>Journaux de configuration

`C:\Users\<username>\AppData\Local\Microsoft\On-premises data gateway\GatewayConfigurator.log`




#### <a name="event-logs"></a>Journaux d’événements

Vous trouverez hello les journaux de passerelle de gestion des données et PowerBIGateway sous **journaux des applications et Services**.


## <a name="telemetry"></a>Télémétrie
La télémétrie peut être utilisée pour la surveillance et la résolution des problèmes. Par défaut

**tooturn télémétrie**

1.  Vérifiez hello local données passerelle répertoire client sur les ordinateur hello. En règle générale, il s’agit de la **passerelle de données %systemdrive%\Program Files\On-premises**. Ou, vous pouvez ouvrir une console de Services et vérifiez tooexecutable de chemin d’accès hello : une propriété de service de passerelle de données locale hello.
2.  Dans le fichier de Microsoft.PowerBI.DataMovement.Pipeline.GatewayCore.dll.config hello à partir du répertoire du client. Modifier hello SendTelemetry paramètre tootrue.
        
    ```
        <setting name="SendTelemetry" serializeAs="String">
                    <value>true</value>
        </setting>
    ```

3.  Enregistrer vos modifications et redémarrer le service Windows hello : service de passerelle de données locale.




## <a name="next-steps"></a>Étapes suivantes
* [Gérer Analysis Services](analysis-services-manage.md)
* [Obtenir les données d’Azure Analysis Services](analysis-services-connect.md)
