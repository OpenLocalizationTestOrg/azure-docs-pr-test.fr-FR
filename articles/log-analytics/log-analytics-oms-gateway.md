---
title: "tooOMS d’ordinateurs aaaConnect à l’aide de hello OMS passerelle | Documents Microsoft"
description: "Se connecter vos appareils gérés par OMS et les ordinateurs analysés par Operations Manager avec le service OMS de hello OMS passerelle toosend données toohello lorsqu’il n’a pas accès à Internet."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Connecter des ordinateurs sans tooOMS d’accès Internet à l’aide de hello OMS passerelle

Ce document décrit comment votre OMS gérés et les ordinateurs analysés de System Center Operations Manager peuvent envoyer service de données toohello OMS lorsqu’il n’a pas accès à Internet. Hello passerelle OMS, qui est un proxy de transfert HTTP qui prend en charge le tunneling HTTP à l’aide de la commande HTTP CONNECT hello peut collecter des données et les envoyer service OMS de toohello de leur part.  

Hello OMS passerelle prend en charge :

* Runbooks Workers hybrides Azure Automation  
* Les ordinateurs Windows avec hello Microsoft Monitoring Agent directement connecté tooan espace de travail OMS
* Les ordinateurs Linux avec hello Agent OMS pour Linux directement connecté tooan espace de travail OMS  
* System Center Operations Manager 2012 SP1 avec UR7, Operations Manager 2012 R2 avec UR3 ou le groupe d’administration Operations Manager 2016 intégré dans OMS.  

Si vos stratégies de sécurité informatique n’autorisent pas les ordinateurs de votre toohello de tooconnect réseau Internet, tels que le point de vente (PDV) appareils ou serveurs prenant en charge des services informatiques, mais vous devez tooconnect tooOMS les toomanage et les surveiller de manière, ils peuvent être configurés toocommunicate directement avec la configuration de tooreceive OMS passerelle hello et transférer des données en leur nom.  Si ces ordinateurs sont configurés avec hello OMS agent toodirectly connecter tooan espace de travail OMS, tous les ordinateurs à la place communiquent avec hello OMS passerelle.  passerelle de Hello transfère les données à partir de hello agents tooOMS directement, il n’analyse pas les données hello en transit.

Quand un groupe d’administration Operations Manager est intégré à OMS, les serveurs d’administration de hello peuvent être configuré tooconnect toohello informations de configuration OMS passerelle tooreceive et envoyer les données collectées en fonction de la solution hello que vous avez activé.  Agents Operations Manager envoient des données telles que des alertes Operations Manager, évaluation de la configuration, espace de l’instance et le serveur d’administration de capacité données toohello. Autres données de volume élevé, tels que les journaux IIS, les performances et les événements de sécurité sont envoyées directement toohello OMS passerelle.  Si vous disposez de davantage de serveurs de passerelle Operations Manager déployés dans un réseau de périmètre ou d’autres toomonitor réseau isolé systèmes non approuvés, il ne peut pas communiquer avec une passerelle d’OMS.  Serveurs d’Operations Manager Gateway peuvent uniquement les serveur d’administration rapports tooa.  Lorsqu’un groupe d’administration Operations Manager est configuré toocommunicate avec hello OMS passerelle, informations de configuration de proxy hello sont distribué automatiquement tooevery gérés par agent ordinateur données toocollect configuré pour l’Analytique des journaux, même si paramètre de Hello est vide.    

tooprovide haute disponibilité pour direct connecté ou les groupes de gestion des opérations qui communiquent avec OMS via la passerelle de hello, vous pouvez utiliser tooredirect d’équilibrage de la charge réseau et répartir le trafic de hello entre plusieurs serveurs de passerelle.  Si un serveur de passerelle tombe en panne, le trafic de hello est redirigé tooanother les nœuds disponibles.  

Il est recommandé d’installer l’agent OMS de hello sur ordinateur hello Bonjour OMS passerelle logiciel toomonitor Bonjour OMS passerelle en cours d’exécution et analyser les données de performances ou des événements. En outre, hello agent permet hello OMS passerelle identifier les points de terminaison de service hello dont il a besoin toocommunicate avec.

Chaque agent doit avoir la passerelle tooits de connectivité réseau afin que les agents peuvent transférer automatiquement tooand de données à partir de la passerelle de hello. L’installation de passerelle hello sur un contrôleur de domaine n’est pas recommandée.

Hello suivant schéma montre le flux de données à partir de tooOMS agents directe à l’aide du serveur de passerelle hello.  Les agents doivent se leur correspondance de la configuration proxy hello même hello du port OMS passerelle est configurée toocommunicate avec tooOMS.  

![diagramme de communication directe entre l’agent et OMS](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

Hello diagramme suivant montre les flux de données à partir d’un tooOMS de groupe d’administration Operations Manager.   

![diagramme de communication entre Operations Manager et OMS](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>Composants requis

Lorsque vous désignez un Bonjour de toorun ordinateur passerelle d’OMS, cet ordinateur doit disposer de hello :

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 et Windows Server 2008
* .NET Framework 4.5
* Au minimum un processeur 4 cœurs et 8 Go de mémoire

### <a name="language-availability"></a>Langues disponibles

Hello OMS passerelle est disponible dans hello suivant langues :

- Chinois (simplifié)
- Chinois (traditionnel)
- Tchèque
- Néerlandais
- Français
- Français
- Allemand
- Hongrois
- Italien
- Japonais
- Coréen
- Polonais
- Portugais (Brésil)
- Portugais (Portugal)
- Russe
- Espagnol (international)

## <a name="download-hello-oms-gateway"></a>Télécharger hello OMS passerelle

Il existe trois façons tooget hello version la plus récente du fichier de configuration de passerelle OMS hello.

1. Télécharger à partir de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54443).

2. Télécharger à partir du portail OMS hello.  Une fois que vous êtes dans l’espace de travail OMS tooyour, accédez trop**paramètres** > **Sources connectées** > **serveurs Windows** sur **Télécharger OMS passerelle**.

3. Télécharger à partir de hello [portail Azure](https://portal.azure.com).  Après votre connexion :  

   1. Parcourir la liste hello des services et sélectionnez **Analytique de journal**.  
   2. Sélectionnez un espace de travail.
   3. Dans le panneau de votre espace de travail, sous **Général**, cliquez sur **Démarrage rapide**.
   4. Sous **choisir un espace de travail de données source tooconnect toohello**, cliquez sur **ordinateurs**.
   5. Bonjour **Agent Direct** panneau, cliquez sur **télécharger la passerelle de OMS**.<br><br> ![télécharger la passerelle OMS](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Installer hello OMS passerelle

tooinstall une passerelle, exécutez hello comme suit.  Si vous avez installé une version antérieure, anciennement *redirecteur Analytique de journal*, il sera mis à niveau de version de toothis.  

1. À partir du dossier de destination hello, double-cliquez sur **OMS Gateway.msi**.
2. Sur hello **Bienvenue** , cliquez sur **suivant**.<br><br> ![Assistant d’installation de la passerelle](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. Sur hello **contrat de licence** page, sélectionnez **J’accepte les termes de hello Bonjour contrat de licence** tooagree toohello CLUF puis cliquez sur **suivant**.
4. Sur hello **Port et l’adresse proxy** page :
   1. Toobe numéro du port TCP hello type utilisé pour la passerelle de hello. Le programme d’installation configure une règle entrante avec ce numéro de port sur le pare-feu Windows.  Hello par défaut est 8080.
      plage valide de Hello hello numéro de port est 1-65535. Si l’entrée de hello n’est pas comprise dans cette plage, un message d’erreur s’affiche.
   2. Si vous le souhaitez, si hello serveur sur lequel la passerelle de hello est installé toocommunicate besoins via un proxy, tapez l’adresse du proxy hello où la passerelle de hello doit tooconnect. Par exemple, `http://myorgname.corp.contoso.com:80`.  Si elle est vide, la passerelle de hello va tenter tooconnect toohello Internet directement.  Si votre serveur proxy requiert une authentification, entrez un nom d'utilisateur et un mot de passe.<br><br> ![Configuration du proxy de l’assistant d’installation de la passerelle](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. Cliquez sur **Suivant**.
5. Si vous n’avez pas activé Microsoft Update, page de Microsoft Update hello s’affiche dans laquelle vous pouvez choisir tooenable il. Effectuez une sélection, puis cliquez sur **Suivant**. Sinon, passez toohello prochaine étape.
6. Sur hello **dossier de Destination** page, laissez hello par défaut C:\Program Files\OMS passerelle ou type hello emplacement du dossier où vous voulez tooinstall passerelle, puis sur **suivant**.
7. Sur hello **tooinstall prêt** , cliquez sur **installer**. Contrôle de compte d’utilisateur peuvent s’afficher demande tooinstall d’autorisation. Dans ce cas, cliquez sur **Oui**.
8. Une fois l’installation terminée, cliquez sur **Terminer**. Vous pouvez vérifier que le service de hello en cours d’exécution en ouvrant le composant logiciel enfichable hello services.msc et vérifiez que **OMS passerelle** s’affiche dans la liste hello de services et de statut est **en cours d’exécution**.<br><br> ![Services – Passerelle OMS](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>Configuration de l’équilibrage de la charge réseau
Vous pouvez configurer la passerelle hello pour la haute disponibilité à l’aide d’équilibrage de charge réseau (NLB) à l’aide de Microsoft charger équilibrage réseau (NLB) ou programmes d’équilibrage de charge matérielle.  Hello équilibrage de charge gère le trafic en redirigeant hello demandés des connexions à partir de hello OMS Agents ou serveurs d’administration Operations Manager via ses nœuds. Si un serveur de passerelle tombe en panne, le trafic de hello Obtient les nœuds de tooother redirigé.

toolearn comment toodesign et le déploiement d’un cluster d’équilibrage de charge réseau Windows Server 2016, consultez [équilibrage de charge réseau](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  Hello étapes suivantes décrivent comment tooconfigure un réseau Microsoft charger le cluster d’équilibrage.  

1.  Se connecter à hello Windows server qui est membre du cluster d’équilibrage de charge réseau hello avec un compte d’administrateur.  
2.  Ouvrez le Gestionnaire d’équilibrage de charge réseau dans le Gestionnaire de serveur, cliquez sur **Outils**, puis sur **Gestionnaire d’équilibrage de charge réseau**.
3. tooconnect un serveur de passerelle d’OMS avec hello Microsoft Monitoring Agent est installé, adresse IP du cluster hello d’avec le bouton droit, puis cliquez sur **tooCluster d’ajouter un ordinateur hôte**.<br><br> ![Gestionnaire d’équilibrage de charge du réseau – ajouter l’hôte tooCluster](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. Entrez l’adresse IP de hello hello du serveur de passerelle que vous souhaitez tooconnect.<br><br> ![Gestionnaire d’équilibrage de charge du réseau – ajouter l’hôte tooCluster : se connecter](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>Configurer l’agent OMS et le groupe d’administration Operations Manager
Hello section suivante inclut des étapes sur tooconfigure directement connexion des agents OMS, un groupe d’administration Operations Manager ou Workers hybrides de Automation Azure avec toocommunicate d’OMS passerelle hello avec OMS.  

spécifications de toounderstand et les étapes sur comment tooinstall hello agent OMS sur les ordinateurs Windows directement la connexion tooOMS, consultez [tooOMS d’ordinateurs Windows de se connecter](log-analytics-windows-agents.md) ou pour voir des ordinateurs Linux [connecter des ordinateurs Linux tooOMS](log-analytics-linux-agents.md).

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>La configuration de l’agent de hello OMS et Operations Manager toouse hello OMS passerelle comme un serveur proxy

### <a name="configure-standalone-oms-agent"></a>Configurer l’agent OMS autonome
Consultez [configurer les paramètres de pare-feu et de proxy avec hello Microsoft Monitoring Agent](log-analytics-proxy-firewall.md) pour plus d’informations sur la configuration d’un agent de toouse un serveur proxy, qui est dans ce cas de passerelle de hello.  Si vous avez déployé plusieurs serveurs de passerelle derrière un équilibreur de charge réseau, la configuration de proxy de l’agent OMS hello est hello adresse IP virtuelle de hello NLB :<br><br> ![Propriétés de Microsoft Monitoring Agent – Paramètres de proxy](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Configuration d’Operations Manager - tous les agents utilisent hello même serveur proxy
Vous configurez le serveur de passerelle Operations Manager tooadd hello.  Hello Operations Manager, configuration du proxy est automatiquement appliquée agents tooall reporting tooOperations Manager, même si le paramètre de hello est vide.

toouse hello passerelle toosupport Operations Manager, vous devez avoir :

* Microsoft Monitoring Agent (version de l’agent – **8.0.10900.0** et versions ultérieures) installé sur le serveur de passerelle hello et configuré pour les espaces de travail OMS hello avec laquelle vous souhaitez toocommunicate.
* passerelle de Hello doit se connecter à Internet ou être le serveur de proxy tooa connectés qui.

> [!NOTE]
> Si vous ne spécifiez pas une valeur pour la passerelle de hello, les valeurs vides sont poussés tooall agents.


1. Console d’Operations Manager ouverts hello et sous **Operations Management Suite**, cliquez sur **connexion** puis cliquez sur **configurer le serveur Proxy**.<br><br> ![Operations Manager – Configurer le serveur proxy](./media/log-analytics-oms-gateway/scom01.png)<br>
2. Sélectionnez **utiliser un ordinateur proxy server tooaccess hello Operations Management Suite** et puis tapez l’adresse IP de hello hello OMS du serveur de passerelle ou une adresse IP virtuelle de hello NLB. Vérifiez que vous démarrez avec hello `http://` préfixe.<br><br> ![Operations Manager – Adresse du serveur proxy](./media/log-analytics-oms-gateway/scom02.png)<br>
3. Cliquez sur **Terminer**. Votre serveur Operations Manager est un espace de travail OMS tooyour connecté.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Configurer Operations Manager : des agents spécifiques utilisent le serveur proxy
Pour les environnements de grandes ou complexes, vous pouvez souhaiter que des serveurs (ou groupes) toouse hello serveur de passerelle d’OMS.  Pour ces serveurs, vous ne pouvez pas mettre à jour hello Operations Manager agent directement en tant que cette valeur est remplacé par valeur globale de hello pour le groupe d’administration hello.  Vous devez à la place toooverride hello règle utilisée toopush ces valeurs.

> [!NOTE]
> Cette même technique de configuration peut être utilisé tooallow hello plusieurs OMS de serveurs de passerelle dans votre environnement.  Par exemple, vous pouvez avoir besoin spécifique toobe de serveurs de passerelle d’OMS spécifié sur une base par région.

1. Console d’Operations Manager ouverts hello et sélectionnez hello **création** espace de travail.  
2. Dans l’espace de travail Création hello, sélectionnez **règles** et cliquez sur hello **étendue** bouton de barre d’outils Operations Manager hello. Si ce bouton n’est pas disponible, vérifiez toomake que vous avez un objet, pas un dossier, sélectionné dans le volet analyse de hello. Hello **étendre les objets de pack d’administration** boîte de dialogue affiche une liste de classes ciblés communes, des groupes ou des objets.
3. Type **Service d’intégrité** Bonjour **recherchez** champ et sélectionnez-le dans la liste de hello.  Cliquez sur **OK**.  
4. Pour rechercher la règle de hello **Advisor Proxy paramètre règle** et dans la barre d’outils de la console hello opérations, cliquez sur **substitue** et pointez trop**remplacement hello Rule\For un objet spécifique de la classe : contrôle d’intégrité Service** et sélectionnez un objet spécifique dans la liste de hello.  Si vous le souhaitez, vous pouvez créer un groupe personnalisé contenant l’objet de service de contrôle d’intégrité hello de serveurs de hello vous souhaitez tooapply cette tooand de remplacement, puis appliquer hello remplacement toothat groupe.
5. Bonjour **propriétés du remplacement** boîte de dialogue, cliquez sur tooplace une case à cocher dans hello **remplacer** toohello suivant de colonne **WebProxyAddress** paramètre.  Bonjour **remplacer par la valeur** , entrez l’URL de hello de vérification du serveur hello OMS passerelle que vous démarrez avec hello `http://` préfixe.
   >[!NOTE]
   > Il est inutile règle de hello tooenable comme il est déjà géré automatiquement avec une substitution contenue dans le pack d’administration Microsoft System Center Advisor remplacement de référence sécurisée hello ciblage hello groupe de serveur d’analyse Microsoft System Center Advisor.
   >
6. Sélectionnez un Pack d’administration à partir de hello **sélectionnez Pack d’administration de destination** liste ou créez un nouveau pack d’administration non scellé en cliquant sur **nouveau**.
7. Lorsque vous effectuez vos modifications, cliquez sur **OK**.

### <a name="configure-for-automation-hybrid-workers"></a>Configuration pour les workers hybrides Automation
Si vous avez des Workers hybrides de Automation dans votre environnement, hello suit fournit des solutions de contournement temporaire, manuel tooconfigure hello passerelle toosupport les.

Bonjour comme suit, vous devez tooknow hello région Azure où hello compte Automation réside. emplacement de hello toolocate :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Sélectionnez le service d’Azure Automation hello.
3. Sélectionnez un compte Azure Automation approprié de hello.
4. Regardez sa région sous **Emplacement**.<br><br> ![Portail Azure – Emplacement du compte Automation](./media/log-analytics-oms-gateway/location.png)  

Hello suivant tables tooidentify hello URL pour chaque emplacement, utilisez :

**URL de service de données d’exécution de la tâche**

| **location** | **URL** |
| --- | --- |
| États-Unis - partie centrale septentrionale |ncus-jobruntimedata-prod-su1.azure-automation.net |
| Europe de l'Ouest |we-jobruntimedata-prod-su1.azure-automation.net |
| Centre-Sud des États-Unis |scus-jobruntimedata-prod-su1.azure-automation.net |
| Est des États-Unis 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Canada central |cc-jobruntimedata-prod-su1.azure-automation.net |
| Europe du Nord |ne-jobruntimedata-prod-su1.azure-automation.net |
| Asie du Sud-Est |sea-jobruntimedata-prod-su1.azure-automation.net |
| Inde centrale |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japon |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australie |ase-jobruntimedata-prod-su1.azure-automation.net |

**URL de service de l’agent**

| **location** | **URL** |
| --- | --- |
| États-Unis - partie centrale septentrionale |ncus-agentservice-prod-1.azure-automation.net |
| Europe de l'Ouest |we-agentservice-prod-1.azure-automation.net |
| Centre-Sud des États-Unis |scus-agentservice-prod-1.azure-automation.net |
| Est des États-Unis 2 |eus2-agentservice-prod-1.azure-automation.net |
| Canada central |cc-agentservice-prod-1.azure-automation.net |
| Europe du Nord |ne-agentservice-prod-1.azure-automation.net |
| Asie du Sud-Est |sea-agentservice-prod-1.azure-automation.net |
| Inde centrale |cid-agentservice-prod-1.azure-automation.net |
| Japon |jpe-agentservice-prod-1.azure-automation.net |
| Australie |ase-agentservice-prod-1.azure-automation.net |

Si votre ordinateur est inscrit en tant qu’un Runbook Worker hybride automatiquement pour la correction à l’aide de la solution de gestion de la mise à jour de hello, procédez comme suit :

1. Ajouter hello données Runtime de la tâche service URL toohello autorisée liste sur hello OMS passerelle. Par exemple : `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Redémarrer le service de passerelle de OMS hello à l’aide de hello suivant l’applet de commande PowerShell :`Restart-Service OMSGatewayService`

Si votre ordinateur est tooAzure embarquée Automation en utilisant l’applet de commande d’inscription de Runbook Worker hybride hello, procédez comme suit :

1. Ajouter hello agent service d’inscription URL toohello autorisée liste sur hello OMS passerelle. Par exemple : `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Ajouter hello données Runtime de la tâche service URL toohello autorisée liste sur hello OMS passerelle. Par exemple : `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Redémarrez le service de passerelle de OMS hello.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>Applets de commande PowerShell utiles
Applets de commande, vous pouvez effectuer les tâches qui sont des paramètres de configuration de la passerelle tooupdate nécessaire hello OMS. Avant de les utiliser, veillez à suivre les instructions suivantes :

1. Installez hello OMS passerelle (MSI).
2. Ouvrez une fenêtre de console PowerShell.
3. module de hello tooimport, tapez la commande suivante :`Import-Module OMSGateway`
4. Si aucune erreur ne s’est produite à l’étape précédente de hello, hello module a été importé avec succès et les applets de commande hello peuvent être utilisés. Saisissez `Get-Module OMSGateway`
5. Une fois que vous apportez des modifications à l’aide des applets de commande hello, assurez-vous que vous redémarrez le service de passerelle hello.

Si vous obtenez une erreur à l’étape 3, le module de hello n’a pas été importé. Erreur de Hello peut se produire quand PowerShell est le module de hello toofind impossible. Vous pouvez le trouver dans le chemin d’installation de la passerelle hello : *C:\Program Files\Microsoft OMS Gateway\PowerShell*.

| **Applet de commande** | **Paramètres** | **Description** | **Exemple** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Clé |Obtient la configuration hello du service de hello |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |Clé (obligatoire) <br> Valeur |Modifications hello configuration du service de hello |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |Obtient l’adresse hello du proxy de relais (en amont) |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |Adresse<br> Nom d’utilisateur<br> Mot de passe |Définit hello adresse (et les informations d’identification) du proxy de relais (en amont) |1. Définir un proxy relais et des informations d’identification :<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. Définir un proxy relais n’exigeant pas d’authentification : `Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. Paramètres du proxy relais hello clair :<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |Obtient hello actuellement autorisée hôte (uniquement hello configuré localement hôte autorisés, ne sont pas des hôtes autorisés téléchargées automatiquement) |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |Hôte (obligatoire) |Ajoute les toohello d’hôte hello liste autorisée |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |Hôte (obligatoire) |Supprime les hôte hello hello liste autorisée |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |Objet (obligatoire) |Ajoute les toohello d’objet du certificat de client hello liste autorisée |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |Objet (obligatoire) |Supprime l’objet du certificat client hello hello liste autorisée |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |Obtient hello actuellement autorisée client sujets de certificat (seule hello localement configurée sujets autorisées, ne sont pas sujets autorisés téléchargées automatiquement) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>Résolution des problèmes
toocollect les événements consignés par la passerelle de hello, vous devez tooalso hello OMS agent est installé.<br><br> ![Observateur d’événements – Journal de la passerelle OMS](./media/log-analytics-oms-gateway/event-viewer.png)

**Identifiants et descriptions des événements de la passerelle OMS**

Hello montre le tableau suivant hello ID d’événement et les descriptions des événements de journal de la passerelle OMS.

| **Identifiant** | **Description** |
| --- | --- |
| 400 |Toute erreur d’application ne disposant pas d’un identifiant spécifique |
| 401 |Configuration incorrecte. Par exemple : listenPort = "texte" au lieu d’un nombre entier |
| 402 |Exception lors de l’analyse des messages de liaison TLS |
| 403 |Erreur de mise en réseau. Par exemple : Impossible de se connecter tootarget server |
| 100 |Informations générales |
| 101 |Le service a démarré |
| 102 |Le service s’est arrêté |
| 103 |Réception d’une commande HTTP CONNECT de la part du client |
| 104 |L’élément n’est pas une commande HTTP CONNECT |
| 105 |Serveur de destination n’est pas dans la liste autorisée ou port de destination hello n’est pas un port sécurisé (443) <br> <br> Assurez-vous que l’agent de MMA hello sur votre serveur de passerelle et agents hello communique avec hello passerelle toohello connecté même espace de travail Analytique de journal. |
| 105 |ERREUR TcpConnection – Certificat client non valide : CN=passerelle <br><br> Assurez-vous que : <br>    <br> &#149; Vous utilisez une passerelle ayant le numéro de version 1.0.395.0 ou supérieur. <br> &#149; Hello MMA agent sur votre serveur de passerelle et agents hello communique avec hello passerelle sont connecté toohello même espace de travail Analytique de journal. |
| 106 |Une raison quelconque, session TLS de hello est suspect et rejetés |
| 107 |session de Hello TLS a été vérifiée. |

**Toocollect des compteurs de performances**

Hello tableau suivant répertorie les compteurs de performances hello disponibles pour hello OMS passerelle. Vous pouvez ajouter des compteurs de hello à l’aide de l’Analyseur de performances.

| **Name** | **Description** |
| --- | --- |
| Passerelle OMS/Connexion du client actif |Nombre de connexions du réseau client actif (TCP) |
| Passerelle OMS/Nombre d’erreurs |Nombre d’erreurs |
| Passerelle OMS/Client connecté |Nombre de clients connectés |
| Passerelle OMS/Nombre de rejets |Nombre de rejets en raison de l’erreur de validation tooany TLS |

![Compteurs de performances de la passerelle OMS](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>Obtenir de l’aide
Lorsque vous êtes connecté toohello portail Azure, vous pouvez créer une demande d’assistance avec hello OMS passerelle ou tout autre service Azure ou la fonctionnalité d’un service.
l’assistance toorequest, cliquez sur le symbole de point d’interrogation hello dans hello coin supérieur droit du portail de hello et puis cliquez sur **nouveau prend en charge la demande**. Ensuite, effectuez de nouveau formulaire de demande de prise en charge hello.

![Nouvelle demande de support](./media/log-analytics-oms-gateway/support.png)

Vous pouvez également laisser des commentaires sur OMS ou Analytique de journal à hello [forum de commentaires de Microsoft Azure](https://feedback.azure.com/forums/267889).

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter des sources de données](log-analytics-data-sources.md) toocollect des données à partir de hello Sources connectées dans votre espace de travail OMS et stockez-le dans le référentiel d’OMS hello.
