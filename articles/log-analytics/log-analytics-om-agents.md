---
title: aaaConnect Operations Manager tooLog Analytique | Documents Microsoft
description: "étendue de votre investissement existant dans System Center Operations Manager et l’utilisation de toomaintain fonctionnalités avec Analytique de journal, vous pouvez intégrer Operations Manager à votre espace de travail OMS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Se connecter à Operations Manager tooLog Analytique
étendue de votre investissement existant dans System Center Operations Manager et l’utilisation de toomaintain fonctionnalités avec Analytique de journal, vous pouvez intégrer Operations Manager à votre espace de travail OMS.  Cela permet de vous tirer parti des opportunités hello d’OMS, tout en continuant toouse Operations Manager pour :

* Continuer la surveillance de l’intégrité de hello de vos services informatiques avec Operations Manager
* Conserver l’intégration avec vos solutions ITSM pour la gestion des incidents et des problèmes
* Gestion du cycle de vie hello d’agents déployés tooon-site et publics IaaS virtuels que vous surveillez avec Operations Manager

Intégration avec System Center Operations Manager ajoute des stratégie de valeur tooyour service opérations à l’aide de la vitesse de hello et l’efficacité d’OMS, dans la collecte, le stockage et l’analyse des données d’Operations Manager.  Effectuez une corrélation vous aide à OMS et le travail vers l’identification des pannes hello des problèmes et surfaces de récurrences pour prendre en charge votre processus de gestion problème existant.   Hello flexibilité hello recherche moteur tooexamine performances, des événements et des alertes données avec des tableaux de bord riche et tooexpose des fonctionnalités de création de rapports ces données de façon significative, montre force hello OMS apporte élargie Operations Manager.

agents Hello reporting du groupe d’administration Operations Manager toohello collectent des données à partir de vos serveurs basés sur des sources de données Analytique de journal hello et les solutions que vous avez activé dans votre abonnement OMS.  En fonction de la solution hello que vous avez activé, les données à partir de ces solutions sont que soit envoyé directement à partir d’un serveur d’administration Operations Manager toohello OMS de service web, ou en raison de hello le volume de données collectées sur le système de géré par agent hello, sont envoyés directement à partir de hello agent tooOMS de service web. serveur d’administration Hello transfère les données d’OMS hello directement toohello OMS web service ; Il n’est jamais écrite toohello Operations Manager ou OperationsManagerDW de base de données.  Lorsqu’un serveur d’administration perd sa connectivité avec le service web de hello OMS, il met en cache les données hello localement jusqu'à ce que la communication est rétablie avec OMS.  Si le serveur d’administration hello est hors connexion en raison de la maintenance de tooplanned ou d’arrêt non planifié, un autre serveur d’administration dans le groupe d’administration hello reprend la connectivité avec OMS.  

Hello diagramme suivant décrit les connexions hello entre les serveurs d’administration hello et des agents dans un groupe d’administration System Center Operations Manager et l’OMS, y compris les ports et la direction de hello.   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

Si vos stratégies de sécurité informatique n’autorisent pas les ordinateurs sur votre toohello de tooconnect réseau Internet, les serveurs d’administration peuvent être configuré tooconnect toohello OMS passerelle tooreceive les informations de configuration et envoyer les données collectées en fonction de la solution de hello avoir activé.  Pour plus d’informations sur comment tooconfigure votre toocommunicate de groupe d’administration Operations Manager via un passerelle d’OMS toohello service OMS, pour voir les [connecter tooOMS d’ordinateurs à l’aide de hello OMS passerelle](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Conditions requises pour le système
Avant de commencer, passez en revue hello suivant tooverify détails conditions préalables.

* OMS prend uniquement en charge Operations Manager 2016, Operations Manager 2012 SP1 UR6 et versions supérieures et Operations Manager 2012 R2 UR2 et versions supérieures.  La prise en charge du proxy a été ajoutée dans Operations Manager 2012 SP1 UR7 et Operations Manager 2012 R2 UR3.
* Tous les agents Operations Manager doivent répondre aux exigences en matière de prise en charge. Assurez-vous que les agents sont à la mise à jour de la configuration minimale hello, sinon le trafic de l’agent Windows risque d’échouer et de nombreuses erreurs peuvent saturer le journal des événements Operations Manager hello.
* Un abonnement OMS.  Pour plus d’informations, consultez [Prise en main de Log Analytics](log-analytics-get-started.md).

### <a name="network"></a>Réseau
informations de Hello ci-dessous liste hello proxy et pare-feu informations de configuration requises pour l’agent Operations Manager de hello, les serveurs d’administration et toocommunicate de console d’opérations avec OMS.  Le trafic à partir de chaque composant est sortant à partir de votre service OMS toohello réseau.     

|Ressource | Numéro de port| Ignorer l’inspection HTTP|  
|---------|------|-----------------------|  
|**Agent**|||  
|\*.ods.opinsights.azure.com| 443 |Oui|  
|\*.oms.opinsights.azure.com| 443|Oui|  
|\*.blob.core.windows.net| 443|Oui|  
|\*.azure-automation.net| 443|Oui|  
|**Serveur d’administration**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| Oui|  
|\*.ods.opinsights.azure.com| 443| Oui|  
|*.azure-automation.net | 443| Oui|  
|**Operations Manager console tooOMS**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 et 443||  
|\*.microsoft.com| 80 et 443||  
|\*.microsoftonline.com| 80 et 443||  
|\*.mms.microsoft.com| 80 et 443||  
|login.windows.net| 80 et 443||  


## <a name="connecting-operations-manager-toooms"></a>Connexion tooOMS d’Operations Manager
Effectuer hello série d’étapes tooconfigure votre tooone de tooconnect de groupe d’administration Operations Manager de vos espaces de travail OMS.

1. Dans la console Operations Manager hello, sélectionnez hello **Administration** espace de travail.
2. Développez le nœud de Operations Management Suite hello et cliquez sur **connexion**.
3. Cliquez sur hello **inscrire tooOperations Management Suite** lien.
4. Sur hello **Assistant de l’intégration d’Operations Management Suite : authentification** page, entrez l’adresse de messagerie hello ou numéro de téléphone et un mot de passe du compte d’administrateur hello qui est associé à votre abonnement OMS, cliquez sur  **Connectez-vous**.
5. Une fois que vous êtes authentifié avec succès, sur hello **Assistant de l’intégration d’Operations Management Suite : sélectionnez un espace de travail** page, vous êtes invité à entrer tooselect votre espace de travail OMS.  Si vous avez plus d’un espace de travail, sélectionnez hello espace de travail de votre choix tooregister avec le groupe d’administration Operations Manager hello à partir de la liste déroulante de hello, puis cliquez sur **suivant**.
   
   > [!NOTE]
   > Operations Manager prend uniquement en charge un espace de travail OMS à la fois. connexion de Hello et hello ordinateurs qui ont été inscrits tooOMS avec l’espace de travail précédent hello sont supprimés d’OMS.
   > 
   > 
6. Sur hello **Assistant de l’intégration d’Operations Management Suite : récapitulatif** page, vérifiez vos paramètres et si elles sont correctes, cliquez sur **créer**.
7. Sur hello **Assistant de l’intégration d’Operations Management Suite : fin** , cliquez sur **fermer**.

### <a name="add-agent-managed-computers"></a>Ajout d’ordinateurs gérés par des agents
Après avoir configuré l’intégration avec votre espace de travail OMS, cela seulement connecte avec OMS, aucune donnée n’est collectée à partir des agents hello reporting tooyour groupe d’administration. Les données seront uniquement collectées lorsque vous aurez configuré les ordinateurs gérés par des agents qui seront chargés de collecter les données pour Log Analytics. Vous pouvez sélectionner des objets ordinateur hello individuellement ou vous pouvez sélectionner un groupe qui contient des objets d’ordinateur Windows. Vous ne pouvez pas sélectionner un groupe qui contient des instances d’une autre classe, telles que des disques logiques ou des bases de données SQL.

1. Console d’Operations Manager ouverts hello et sélectionnez hello **Administration** espace de travail.
2. Développez le nœud de Operations Management Suite hello et cliquez sur **connexion**.
3. Cliquez sur hello **ajouter un ordinateur/groupe** lien sous hello Actions en-tête hello côté droit du volet de hello.
4. Bonjour **recherche d’ordinateurs** boîte de dialogue, vous pouvez rechercher des ordinateurs ou des groupes surveillés par Operations Manager. Sélectionnez les ordinateurs ou les groupes tooOMS de tooonboard, cliquez sur **ajouter**, puis cliquez sur **OK**.

Vous pouvez afficher les ordinateurs et de groupes configurés toocollect des données à partir du nœud des ordinateurs gérés hello sous Operations Management Suite Bonjour **Administration** espace de travail de la console d’opérations hello.  De là, vous pouvez ajouter ou supprimer des ordinateurs et des groupes selon les besoins.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Configurer les paramètres de proxy OMS dans la console opérateur de hello
Effectuer hello comme suit si un serveur proxy interne entre le groupe d’administration hello et le service web OMS.  Ces paramètres sont gérées centralement à partir de groupe d’administration hello et systèmes distribués tooagent gérés qui sont inclus dans les données de toocollect étendue hello pour OMS.  Cela s’avère utile pour lorsque certaines solutions de contournement hello management server et enverra des données directement tooOMS de service web.

1. Console d’Operations Manager ouverts hello et sélectionnez hello **Administration** espace de travail.
2. Développez Operations Management Suite, puis cliquez sur **Connexions**.
3. Bonjour vue connexion à OMS, cliquez sur **configurer le serveur Proxy**.
4. Sur **Assistant Operations Management Suite : serveur Proxy** page, sélectionnez **utiliser un ordinateur proxy server tooaccess hello Operations Management Suite**, puis tapez les URL hello avec le numéro de port hello, par exemple, http:// corpproxy:80, puis cliquez sur **Terminer**.

Si votre serveur proxy requiert une authentification, effectuer des étapes suivantes de hello informations d’identification tooconfigure et de paramètres qui doivent toopropagate toomanaged ordinateurs signale tooOMS hello groupe d’administration.

1. Console d’Operations Manager ouverts hello et sélectionnez hello **Administration** espace de travail.
2. Sous **Configuration d’identification**, sélectionnez **Profils**.
3. Ouvrez hello **Proxy System Center Advisor s’exécuter en tant que profil** profil.
4. Bonjour Assistant profil d’identification, cliquez sur toouse d’ajouter un compte d’identification. Vous pouvez créer un [compte d’identification](https://technet.microsoft.com/library/hh321655.aspx) ou utiliser un compte existant. Ce compte doit toohave suffisamment autorisations toopass via un serveur proxy de hello.
5. tooset hello toomanage de compte, choisissez **une classe sélectionnée, un groupe ou un objet**, cliquez sur **sélectionnez...** puis sur **Groupe...** tooopen hello **recherche de groupe** boîte.
6. Recherchez le **groupe Microsoft System Center Advisor Monitoring Server**, puis sélectionnez-le.  Cliquez sur **OK** après avoir sélectionné hello de hello groupe tooclose **recherche de groupe** boîte.
7. Cliquez sur **OK** tooclose hello **ajouter un compte d’identification** boîte.
8. Cliquez sur **enregistrer** toocomplete hello Assistant et enregistrez vos modifications.

Une fois la connexion de hello est créée et vous configurez les agents qui seront collecter et consigner des données tooOMS, hello de configuration suivant est appliquée dans le groupe d’administration hello, pas nécessairement dans l’ordre :

* Hello compte d’identification **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** est créé.  Il est associé au profil d’identification hello **Microsoft System Center Advisor exécuter en tant que profil Blob** et ciblée par deux classes - **serveur collecte** et **groupe d’administration Operations Manager** .
* Deux connecteurs sont créés.  tout d’abord Hello est nommé **Microsoft.SystemCenter.Advisor.DataConnector** et est automatiquement configuré avec un abonnement qui transmet toutes les alertes générées à partir des instances de toutes les classes dans tooOMS de groupe d’administration hello journal Analytique. connecteur de deuxième Hello est **Advisor Connector**, qui est responsable de la communication avec le service web OMS et le partage de données.
* Agents et les groupes que vous avez sélectionné des données de toocollect dans le groupe d’administration hello est ajouté toohello **groupe de serveur d’analyse Microsoft System Center Advisor**.

## <a name="management-pack-updates"></a>Mises à jour du pack d’administration
Une fois la configuration terminée, groupe d’administration Operations Manager hello établit une connexion avec hello service OMS.  serveur d’administration Hello se synchronise avec le service web de hello et recevoir des informations de configuration de mise à jour sous forme de hello de packs d’administration pour les solutions hello que vous avez activé et qui s’intègrent avec Operations Manager.   Operations Manager recherche des mises à jour de ces packs d’administration, puis les télécharge et les importe automatiquement lorsqu’elles sont disponibles.  Deux règles principales contrôlent ce processus :

* **Microsoft.SystemCenter.Advisor.MPUpdate** -met à jour des packs d’administration OMS base hello. S’exécute toutes les 12 heures par défaut.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** : met à jour les packs d’administration de solution activés dans votre espace de travail. Par défaut, elle s’exécute toutes les cinq (5) minutes.

Vous pouvez remplacer ces deux règles tooeither empêcher le téléchargement automatique en désactivant les ou modifier la fréquence de hello pour la fréquence à laquelle hello serveur d’administration se synchronise avec OMS toodetermine si un pack d’administration est disponible et doit être téléchargé.  Suivez les étapes de hello [comment tooOverride une règle ou une analyse](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **fréquence** paramètre avec une valeur en secondes toochange hello calendrier de synchronisation ou modifier hello **activé**  règles de paramètre toodisable hello.  Hello de cible remplace tooall des objets de classe de groupe d’administration Operations Manager.

Si vous souhaitez toocontinue suivant votre processus de contrôle de modifications existant pour le contrôle des versions du Pack d’administration dans votre groupe d’administration de production, vous pouvez désactiver les règles de hello et les activer pendant des heures spécifiques lorsque les mises à jour sont autorisées. Si vous avez un développement ou un groupe d’administration de questions et réponses dans votre environnement et a toohello de connectivité Internet, vous pouvez configurer ce groupe d’administration avec un toosupport d’espace de travail OMS de ce scénario.  Cela vous permet de tooreview et évaluer des versions itératives hello hello OMS des packs d’administration avant de les introduire dans votre groupe d’administration de production.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Basculer un tooa de groupe Operations Manager nouvel espace de travail OMS
1. Connectez-vous à OMS tooyour abonnement et créer un espace de travail dans [Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Console d’Operations Manager hello ouverte avec un compte qui est membre du rôle Administrateurs Operations Manager de hello et sélectionnez hello **Administration** espace de travail.
3. Développez Operations Management Suite, puis sélectionnez **Connexions**.
4. Sélectionnez hello **reconfigurer opération Management Suite** lien hello intermédiaire à côté du volet de hello.
5. Suivez hello **Assistant de l’intégration d’Operations Management Suite** et entrez hello messagerie adresse ou numéro de téléphone et un mot de passe du compte d’administrateur hello qui est associé à votre nouvel espace de travail OMS.
   
   > [!NOTE]
   > Hello **Assistant de l’intégration d’Operations Management Suite : sélectionnez un espace de travail** page présente hello espace de travail existant qui est en cours d’utilisation.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>Valider l’intégration entre Operations Manager et OMS
Il existe plusieurs façons différentes, vous pouvez vérifier que votre tooOperations OMS intégration Manager a réussi.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>intégration de tooconfirm à partir du portail OMS hello
1. Dans le portail OMS hello, cliquez sur hello **paramètres** vignette
2. Sélectionnez **Sources connectées**.
3. Dans la table hello sous hello section de System Center Operations Manager, vous devez voir le nom hello hello du groupe d’administration répertorié avec nombre hello d’état et les agents lors de la dernière réception de données.
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Hello de note **ID de l’espace de travail** valeur sous hello côté gauche de la page de paramètres hello.  Vous la validez par rapport à votre groupe d’administration Operations Manager ci-dessous.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>intégration de tooconfirm à partir de la console opérateur de hello
1. Console d’Operations Manager ouverts hello et sélectionnez hello **Administration** espace de travail.
2. Sélectionnez **packs d’administration** et Bonjour **rechercher :** type zone de texte **Advisor** ou **Intelligence**.
3. Selon que vous avez activé les solutions hello, vous voyez un Pack d’administration correspondant répertoriés dans les résultats de recherche hello.  Par exemple, si vous avez activé hello solution de gestion des alertes, le pack d’administration hello gestion des alertes Microsoft System Center Advisor est dans la liste de hello.
4. À partir de hello **analyse** afficher, accédez toohello **Operations Management Suite\Health état** vue.  Sélectionnez un serveur d’administration sous hello **état serveur d’administration** volet et Bonjour **affichage Détails** volet confirmer hello valeur de la propriété **URI du service d’authentification** correspond aux ID d’espace de travail OMS hello.
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>Supprimer l’intégration à OMS
Lorsque vous n’avez plus besoin intégration entre votre groupe d’administration Operations Manager et l’espace de travail OMS, il existe plusieurs étapes requises tooproperly supprimer la connexion hello et la configuration de groupe d’administration hello. Hello suit a vous mettre à jour votre espace de travail OMS en supprimant la référence hello de votre groupe d’administration, supprimez hello OMS connecteurs, puis supprimez les packs d’administration prenant en charge d’OMS.   

Packs d’administration pour les solutions hello que vous avez activé et qui s’intègrent avec Operations Manager et hello management packs requis toosupport integration avec hello service OMS ne peut pas être supprimée facilement hello groupe d’administration.  Il s’agit, car certains des packs d’administration OMS hello ont des dépendances sur d’autres packs d’administration associées.  packs d’administration toodelete possède une dépendance vis-à-vis d’autres packs d’administration, télécharger le script de hello [supprimer un pack d’administration avec des dépendances](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) à partir du centre de scripts TechNet.  

1. Ouvrez hello interface de commande d’Operations Manager avec un compte qui est membre du rôle Administrateurs Operations Manager de hello.
   
    > [!WARNING]
    > Vérifiez que vous ne disposez pas des packs d’administration personnalisés avec le mot hello Advisor ou IntelligencePack dans nom hello avant de continuer, sinon hello suit les supprime à partir du groupe d’administration hello.
    > 

2. À partir de hello interpréteur de commandes, tapez`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Ensuite, tapez `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. packs de tous les packs d’administration restants qui ont une dépendance sur les autres tâches de gestion de System Center Advisor tooremove, utiliser un script hello *RecursiveRemove.ps1* vous avez téléchargé à partir de hello centre de scripts TechNet.  
 
    > [!NOTE]
    > Ne supprimez pas les packs d’administration Microsoft System Center Advisor ou Microsoft System Center Advisor interne hello.  
    >  

5. Ouvrez la console Opérateur Operations Manager de hello avec un compte qui est membre du rôle Administrateurs Operations Manager de hello.
6. Sous **Administration**, sélectionnez hello **packs d’administration** nœud et Bonjour **rechercher :** , tapez **Advisor** et vérifiez hello Packs d’administration suivants sont toujours importés dans votre groupe d’administration :
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor Internal
7. Dans le portail OMS hello, cliquez sur hello **paramètres** vignette.
8. Sélectionnez **Sources connectées**.
9. Dans la table hello sous hello section de System Center Operations Manager, vous devez voir le nom de hello hello groupe d’administration souhaité tooremove à partir de l’espace de travail hello.  Sous la colonne de hello **dernières données**, cliquez sur **supprimer**.  
   
    > [!NOTE]
    > Hello **supprimer** lien n’est plus disponible jusqu’après 14 jours si aucune activité n’est détectée à partir du groupe d’administration connecté hello.  
    > 

10. Une fenêtre s’affiche vous demandant de tooconfirm que vous souhaitez tooproceed à la suppression de hello.  Cliquez sur **Oui** tooproceed. 

toodelete hello deux connecteurs - Microsoft.SystemCenter.Advisor.DataConnector et le connecteur Advisor, enregistrez le script PowerShell de hello ci-dessous tooyour ordinateur et exécuter à l’aide de hello exemple suivant :

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> ordinateur Hello de que vous exécutez ce script à partir, si ce n’est pas un serveur d’administration, doit avoir interface de commande d’Operations Manager hello installé en fonction de la version de hello de votre groupe d’administration.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

Bonjour ultérieure si vous prévoyez de vous reconnecter à votre espace de travail administration groupe tooan OMS, vous devez toore importation hello `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` fichier de pack d’administration à partir de la dernière mise à jour cumulative de hello appliqué tooyour groupe d’administration.  Vous pouvez trouver ce fichier Bonjour `%ProgramFiles%\Microsoft System Center 2012` ou hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` dossier.

## <a name="next-steps"></a>Étapes suivantes
les fonctionnalités tooadd et collecter des données, consultez [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).


