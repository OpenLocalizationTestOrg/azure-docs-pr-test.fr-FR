---
title: "passerelle de données locale aaaInstall - Azure Logic Apps | Documents Microsoft"
description: "Accéder aux sources de données sur site, installer la passerelle de données locale hello pour le transfert de données rapide et le chiffrement entre les sources de données sur site et les applications de la logique"
keywords: "accéder aux données, localement, transfert de données, chiffrement, sources de données"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a>Installer la passerelle de données locale hello pour Azure Logic Apps

Avant que vos applications logiques peuvent accéder à des sources de données sur site, vous devez installer et configurer la passerelle de données locale hello. Hello passerelle fait Office de pont qui fournit le transfert de données rapide et le chiffrement entre systèmes sur site et vos applications logiques. passerelle de Hello transmet des données à partir de sources locales sur des canaux chiffrés via hello Azure Service Bus. Tout le trafic provient sécurisé trafic sortant à partir de l’agent de passerelle hello. En savoir plus sur [le fonctionnement de la passerelle de données hello](#gateway-cloud-service).

passerelle de Hello prend en charge les sources de données de connexions toothese sur site :

*   BizTalk Server 2016
*   DB2  
*   Système de fichiers
*   Informix
*   MQ
*   MySQL
*   Oracle Database
*   PostgreSQL
*   Serveur d’applications SAP 
*   Serveur de messagerie SAP
*   SharePoint
*   SQL Server
*   Teradata

Ces étapes indiquent comment toofirst installation hello local passerelle de données avant de vous [configurer une connexion entre la passerelle de hello et vos applications logiques](./logic-apps-gateway-connection.md). Pour plus d’informations sur les connecteurs pris en charge, voir [Connecteurs pour Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list). 

Pour plus d’informations sur la façon dont toouse hello passerelle avec d’autres services, consultez les articles suivants :

*   [Passerelle de données locale Microsoft Power BI](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Passerelle de données locale Azure Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Passerelle de données locale Microsoft Flow](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Passerelle de données locale Microsoft PowerApps](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a>Configuration requise

**Minimale** :

* .NET Framework 4.5
* Version 64 bits de Windows 7 ou Windows Server 2008 R2 (ou version ultérieure)

**Recommandée** :

* Processeur 8 cœurs
* 8 Go de mémoire
* Version 64 bits de Windows 2012 R2 (ou version ultérieure)

**Points importants à prendre en considération** :

* Installez la passerelle de données locale hello uniquement sur un ordinateur local.
Vous ne pouvez pas installer la passerelle de hello sur un contrôleur de domaine.

   > [!TIP]
   > Vous n’avez pas passerelle de hello tooinstall sur hello même ordinateur que votre source de données. latence de toominimize, vous pouvez installer passerelle hello aussi proche en tant que source de données tooyour possibles, ou sur hello même ordinateur, en supposant que vous disposez des autorisations.

* N’installez pas les passerelle hello sur un ordinateur qui désactive, passe toosleep ou ne connecte pas toohello Internet, car la passerelle de hello ne peut pas s’exécuter dans ces circonstances. De même, les performances de la passerelle peuvent être moindres sur un réseau sans fil.

* Pendant l’installation, vous devez vous connecter avec un [compte professionnel ou scolaire](https://docs.microsoft.com/azure/active-directory/sign-up-organization) géré par Azure Active Directory (Azure AD), et non un compte Microsoft. 

  Vous avez toouse hello même travail ou d’établissement scolaire compte plus tard en hello Azure portal lorsque vous créez et associez une ressource de passerelle à votre installation de la passerelle. Puis, vous sélectionnez cette ressource passerelle lorsque vous créez la connexion de hello entre votre source de données de local application et hello logique. [Pourquoi dois-je utiliser un compte professionnel ou scolaire Azure AD ?](#why-azure-work-school-account)

  > [!TIP]
  > Si vous avez souscrit une offre Office 365 sans fournir votre adresse de messagerie professionnelle réelle, votre adresse de connexion peut ressembler à ceci : jeff@contoso.onmicrosoft.com. 

* Si vous disposez d’une passerelle existante que vous configurez avec un programme d’installation est antérieure à la version 14.16.6317.4, vous ne pouvez pas modifier l’emplacement de votre passerelle par installer de dernière hello en cours d’exécution. Toutefois, vous pouvez utiliser hello dernière tooset de programme d’installation d’une nouvelle passerelle avec emplacement hello souhaitées à la place.
  
  Si vous disposez d’un programme d’installation de passerelle est antérieure à la version 14.16.6317.4, mais vous n’avez pas installé votre passerelle encore, vous pouvez télécharger et utiliser le programme d’installation de la dernière hello.

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a>Installer la passerelle de données hello

1.  [Téléchargez et exécutez le programme d’installation de la passerelle hello sur un ordinateur local](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).

2. Lisez et acceptez les termes du contrat de hello d’utilisation et déclaration de confidentialité.

3. Spécifier le chemin d’accès hello sur votre ordinateur local où vous souhaitez la passerelle de hello tooinstall.

4. Lorsque vous y êtes invité, connectez-vous à votre compte Azure professionnel ou scolaire, pas à un compte Microsoft.

   ![Connexion avec le compte professionnel ou scolaire Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. Maintenant inscrire votre passerelle installée avec hello [service cloud de passerelle](#gateway-cloud-service). Choisissez **Inscrivez une nouvelle passerelle sur cet ordinateur**.

   service de cloud de passerelle Hello chiffre et stocke vos informations d’identification de source de données et les détails de la passerelle. 
   service de Hello achemine les requêtes et leurs résultats entre votre application logique, la passerelle de données locale hello et votre source de données sur site.

6. Entrez un nom pour votre installation de passerelle. Créez une clé de récupération, puis confirmez votre clé de récupération. 

   > [!IMPORTANT] 
   > Votre clé de récupération doit contenir au moins huit caractères. Assurez-vous que vous enregistrez et clé de hello de conserver en lieu sûr. Vous avez besoin de cette clé lorsque vous souhaitez toomigrate, restaurer ou reprendre une passerelle existante.

   1. Cliquez sur la région par défaut pour le service de cloud de passerelle hello et utilisés par votre installation de la passerelle, Azure Service Bus toochange hello **modification région**.

      ![Modification de la région](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      région de Hello par défaut est région hello associée à votre client Azure AD.

   2. Dans le volet suivant de hello, ouvrez hello **sélectionner une région** trop choisir une autre région.

      ![Sélection d’une autre région](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      Par exemple, vous peut sélectionner hello même région que votre application logique, ou sélectionnez hello région le plus proche tooyour des données locales source afin de réduire la latence. Votre ressource de passerelle et votre application logique se trouvent dans des emplacements différents.

      > [!IMPORTANT]
      > Vous ne pouvez pas modifier cette région après l’installation. Cette zone détermine également et restreint l’emplacement hello où vous pouvez créer des ressources Azure de hello pour votre passerelle. Par conséquent, lorsque vous créez votre ressource de passerelle dans Azure, assurez-vous qu’emplacement de la ressource hello correspond à la région de hello que vous avez sélectionné lors de l’installation de la passerelle.
      > 
      > Si vous souhaitez toouse une autre région pour votre passerelle ultérieurement, vous devez configurer une passerelle.

   3. Une fois ces opérations effectuées, sélectionnez **Terminé**.

7. Maintenant, suivez ces étapes dans hello portail Azure afin de pouvoir [créer une ressource Azure pour votre passerelle](../logic-apps/logic-apps-gateway-connection.md). 

En savoir plus sur [le fonctionnement de la passerelle de données hello](#gateway-cloud-service).

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a>Migrer, restaurer ou contrôler une passerelle existante

tooperform ces tâches, vous devez disposer de clé de récupération hello qui a été spécifié lors de la passerelle de hello a été installée.

1. Dans le menu Démarrer de votre ordinateur, choisissez **Passerelle de données locale**.

2. Une fois que hello s’ouvre le programme d’installation et connectez-vous avec hello même Azure fonctionne ou compte scolaire qui était précédemment utilisé la passerelle de hello tooinstall.

3. Choisissez **Migrer, restaurer ou contrôler une passerelle existante**.

4. Fournir la clé de nom et de récupération hello pour la passerelle hello que vous souhaitez toomigrate, restaurez ou remplacez par.

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a>Redémarrez la passerelle de hello

passerelle de Hello s’exécute comme un service Windows. Comme tout autre service Windows, vous pouvez démarrer et arrêter le service hello de plusieurs façons. Par exemple, vous pouvez ouvrir une invite de commandes avec des autorisations élevées sur ordinateur hello où passerelle de hello est en cours d’exécution et exécuter ces deux commandes :

* service de hello toostop, exécutez la commande suivante :
  
    `net stop PBIEgwService`

* service de hello toostart, exécutez la commande suivante :
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a>Compte de service Windows

passerelle de données locale Hello est configurée toouse `NT SERVICE\PBIEgwService` pour hello Windows service informations d’identification d’ouverture de session. Par défaut, passerelle de hello a le droit de « Une session en tant que service » hello pour l’ordinateur de hello sur lequel vous installez la passerelle de hello.

> [!NOTE]
> Hello compte de service Windows diffère compte hello utilisés pour la connexion des sources de données tooon local et de hello travail Azure ou compte scolaire utilisé toosign dans les services toocloud.

## <a name="configure-a-firewall-or-proxy"></a>Configuration d’un pare-feu ou d’un proxy

passerelle de Hello crée une connexion sortante trop [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). tooprovide les informations de proxy pour votre passerelle, consultez [configurer les paramètres de proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).

toocheck si votre pare-feu ou proxy, peut bloquer les connexions, vérifiez si votre ordinateur peut connecter réellement toohello internet et hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/). À partir d’une invite PowerShell, exécutez la commande suivante :

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> Cette commande teste uniquement la connectivité réseau et connectivité toohello Azure Service Bus. Afin de la commande hello ne concerne pas toodo avec la passerelle de hello ou un service de cloud de passerelle hello qui chiffre et stocke vos informations d’identification et les détails de la passerelle. 
>
> Par ailleurs, cette commande est disponible uniquement sur Windows Server 2012 R2 ou version ultérieure, et sur Windows 8.1 ou version ultérieure. Dans les versions antérieures du système d’exploitation, vous pouvez utiliser Telnet trop tester la connectivité. Pour en savoir plus, voir [Solutions Azure Service Bus et hybrides](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

Vos résultats doivent être similaires toothis exemple :

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

Si **TcpTestSucceeded** n’est pas défini trop**True**, vous pouvez être bloqué par un pare-feu. Si vous souhaitez toobe complète, substituer hello **Nom_Ordinateur** et **Port** valeurs avec les valeurs hello répertoriés sous [configurer des ports](#configure-ports) dans cette rubrique.

les pare-feu Hello peuvent également bloquer les connexions que hello Qu'azure Service Bus rend toohello centres de données Azure. Si ce scénario se produit, approuver (débloquer) toutes hello des adresses IP pour les centres de données dans votre région. Pour les adresses IP, [get hello Azure liste d’adresses IP ici](https://www.microsoft.com/download/details.aspx?id=41653).

## <a name="configure-ports"></a>Configuration des ports

passerelle de Hello crée une connexion sortante trop[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) et communique sur des ports sortants : TCP 443 (valeur par défaut), 5671, 5672, 9350 à 9354. passerelle de Hello ne requiert pas les ports entrants. Pour en savoir plus, voir [Solutions Azure Service Bus et hybrides](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).

| NOMS DE DOMAINE | PORTS SORTANTS | DESCRIPTION |
| --- | --- | --- |
| *.analysis.windows.net | 443 | HTTPS | 
| *.login.windows.net | 443 | HTTPS | 
| *.servicebus.windows.net | 5671-5672 | Advanced Message Queuing Protocol (AMQP) | 
| *.servicebus.windows.net | 443, 9350-9354 | Récepteurs du Service Bus Relay sur TCP (nécessite le port 443 pour l’acquisition du jeton Access Control) | 
| *.frontend.clouddatahub.net | 443 | HTTPS | 
| *.core.windows.net | 443 | HTTPS | 
| login.microsoftonline.com | 443 | HTTPS | 
| *.msftncsi.com | 443 | Utilisé une connectivité internet tootest lors de la passerelle de hello est inaccessible par hello service Power BI. | 

Si vous avez des adresses IP tooapprove plutôt que des domaines de hello, vous pouvez télécharger et utiliser hello [liste les plages IP de centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653). Dans certains cas, les connexions Azure Service Bus hello sont effectuées avec l’adresse IP plutôt que des noms de domaine qualifié complet.

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a>Comment fonctionne la passerelle de données hello ?

passerelle de données Hello facilite la communication rapide et sécurisée entre votre application logique, service de cloud de passerelle hello et votre source de données locale. 

![diagramme de flux de passerelle de données locale](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

Par conséquent, lorsque les utilisateur hello dans le cloud de hello interagit avec un élément qui s’est connecté tooyour local source de données :

1. service de cloud de passerelle Hello crée une requête avec informations d’identification hello chiffré de source de données hello et envoie la file d’attente de toohello de requêtes hello pour hello passerelle tooprocess.

2. service de cloud de passerelle Hello analyse hello requête et exécute un push de hello demande toohello Azure Service Bus.

3. passerelle de données locale Hello interroge hello Azure Service Bus pour les demandes en attente.

4. passerelle de Hello obtient hello requête, déchiffre les informations d’identification hello et connecte la source de données toohello avec ces informations d’identification.

5. passerelle de Hello envoie hello toohello récupérer les données pour l’exécution.

6. résultats de Hello sont envoyés à partir de la source de données hello, arrière toohello passerelle, puis toohello service de cloud de passerelle. Hello service cloud de passerelle utilise ensuite les résultats hello.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Forum Aux Questions

### <a name="general"></a>Généralités

**Q**: ai-je besoin d’une passerelle pour les sources de données dans le cloud hello, telles que SQL Azure ? <br/>
**R** : Non. Une passerelle connecte à des sources de données tooon local uniquement.

**Q**: passerelle de hello a-t-elle toobe installé sur hello même ordinateur en tant que source de données hello ? <br/>
**R** : Non. passerelle de Hello connecte toohello source de données à l’aide des informations de connexion hello qui a été fournies. Envisagez de passerelle de hello comme une application cliente en ce sens. passerelle de Hello doit simplement hello capacité tooconnect toohello nom du serveur qui a été fourni.

<a name="why-azure-work-school-account"></a>

**Q**: Pourquoi dois-je utiliser un travail Azure ou établissement scolaire toosign compte dans ? <br/>
**Un**: vous pouvez uniquement utiliser un travail Azure ou scolaire compte lorsque vous installez la passerelle de données locale hello. Votre compte de connexion est stocké dans un client géré par Azure Active Directory (Azure AD). En règle générale, le nom de principal d’utilisateur (UPN) de votre compte Azure AD correspond à adresse de messagerie hello.

**Q** : où mes informations d’identification sont-elles stockées ? <br/>
**A**: informations d’identification hello que vous entrez pour une source de données sont chiffrées et stockées dans le service de cloud de passerelle hello. informations d’identification Hello sont déchiffrées au niveau de la passerelle de données locale hello.

**Q** : Existe-t-il des exigences concernant la bande passante réseau ? <br/>
**R** : Nous vous recommandons d’utiliser une connexion réseau offrant un bon débit. Chaque environnement est différent, et quantité hello des données envoyées affecte les résultats hello. À l’aide d’ExpressRoute peut aider à tooguarantee un niveau de débit entre hello centres de données Azure et locaux.
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
**A**: dans les Services, passerelle de hello est appelé le Service Power BI Enterprise Gateway.

**Q**: pouvez hello service Windows de passerelle s’exécuter avec un compte Azure Active Directory ? <br/>
**R** : Non. Hello service Windows doit avoir un compte Windows valide. Par défaut, le service de hello s’exécute avec hello SID de Service, NT SERVICE\PBIEgwService.

### <a name="high-availability-and-disaster-recovery"></a>Haute disponibilité et récupération d’urgence

**Q** : Quelles sont les options de récupération d’urgence disponibles ? <br/>
**Un**: vous pouvez utiliser toorestore de clé de récupération hello ou déplacer une passerelle. Lorsque vous installez la passerelle de hello, spécifiez la clé de récupération hello.

**Q**: quels sont les avantages de hello de clé de récupération hello ? <br/>
**A**: clé de récupération hello fournit un moyen toomigrate ou récupérer vos paramètres de passerelle après un sinistre.

**Q**: existe-t-il des plans pour activer les scénarios de haute disponibilité avec la passerelle de hello ? <br/>
**A**: ces scénarios sont sur la feuille de route hello, mais nous n’avons pas encore une chronologie.

## <a name="troubleshooting"></a>Résolution des problèmes

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

**Q**: Comment puis-je savoir quelles requêtes sont envoyées source de données locale toohello ? <br/>
**Un**: vous pouvez activer le traçage de requête, qui inclut les requêtes hello qui sont envoyées. N’oubliez pas de requête toochange en remontant la valeur d’origine de toohello faite le problème résolu. Le fait de laisser activé le traçage des requêtes contribue à augmenter la taille des journaux.

Vous pouvez également utiliser les outils de suivi des requêtes proposés par votre source de données. Par exemple, vous pouvez utiliser Extended Events ou SQL Profiler for SQL Server et Analysis Services.

**Q**: où se trouvent les journaux de passerelle hello ? <br/>
**R**: Voir la section Outils plus loin dans cette rubrique.

### <a name="update-toohello-latest-version"></a>Mettre à jour la version la plus récente toohello

Nombreux problèmes peuvent apparaître lors de la version de la passerelle hello devient obsolète. Comme recommandé, assurez-vous d’utiliser la version la plus récente hello. Si vous n’avez pas mis à jour de passerelle de hello pendant un mois ou plus, vous pouvez envisager d’installer la version la plus récente de la passerelle de hello hello et voir si vous pouvez reproduire le problème de hello.

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a>Erreur : Échec de tooadd utilisateur toogroup. (-2147463168 PBIEgwService Performance Log Users)

Vous pouvez obtenir cette erreur si vous essayez de passerelle de hello tooinstall sur un contrôleur de domaine, ce qui n’est pas pris en charge. Assurez-vous que vous déployez la passerelle de hello sur un ordinateur qui n’est pas un contrôleur de domaine.

## <a name="tools"></a>Outils

### <a name="collect-logs-from-hello-gateway-configurer"></a>Collecter les journaux à partir de la configurer de passerelle hello

Vous pouvez collecter plusieurs journaux pour la passerelle de hello. Commencez toujours par les journaux de hello !

#### <a name="installer-logs"></a>Journaux du programme d’installation

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a>Journaux de configuration

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a>Journaux du service de passerelle Enterprise

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a>Journaux d’événements

Vous trouverez hello les journaux de passerelle de gestion des données et PowerBIGateway sous **journaux des applications et Services**.

### <a name="fiddler-trace"></a>Trace Fiddler

[Fiddler](http://www.telerik.com/fiddler) est un outil gratuit développé par Telerik, qui surveille le trafic HTTP. Vous pouvez voir le trafic par le service Power BI à partir de l’ordinateur client de hello de hello. Ce service peut également indiquer les éventuelles erreurs et autres informations connexes.

## <a name="next-steps"></a>Étapes suivantes
    
* [Se connecter tooon locale, les données à partir d’applications de logique](../logic-apps/logic-apps-gateway-connection.md)
* [Fonctionnalités d’intégration d'entreprise](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [Connecteurs pour Azure Logic Apps](../connectors/apis-list.md)
