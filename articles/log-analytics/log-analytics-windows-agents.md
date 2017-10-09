---
title: aaaConnect Windows ordinateurs tooAzure Analytique de journal | Documents Microsoft
description: "Cet article explique les ordinateurs Windows hello hello étapes tooconnect dans votre toohello d’infrastructure sur site service d’Analytique de journal à l’aide d’une version personnalisée de hello Microsoft Monitoring Agent (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Connecter Windows ordinateurs toohello Analytique de journal service dans Azure

Cet article explique les étapes hello tooconnect les ordinateurs Windows dans les espaces de travail local infrastructure tooOMS à l’aide d’une version personnalisée de hello Microsoft Monitoring Agent (MMA). Vous devez tooinstall et connectez les agents pour tous les ordinateurs hello que vous souhaitez tooonboard pour permettre leur service de journal Analytique toosend données toohello et tooview et agir sur ces données. Chaque agent peut signaler des espaces de travail toomultiple.

Vous pouvez installer des agents à l’aide du programme d’installation, de la ligne de commande, ou de la fonction Desired State Configuration (DSC) d’Azure Automation.  

>[!NOTE]
Pour les ordinateurs virtuels s’exécutant dans Azure, vous pouvez simplifier l’installation à l’aide de hello [extension de machine virtuelle](log-analytics-azure-vm-extension.md).

Sur les ordinateurs avec une connexion Internet, l’agent de hello utilise hello connexion toohello Internet toosend données tooOMS. Pour les ordinateurs qui n’ont pas de connectivité Internet, vous pouvez utiliser un proxy ou un hello [OMS passerelle](log-analytics-oms-gateway.md).

La connexion de votre tooOMS d’ordinateurs Windows est simple à l’aide de trois étapes simples :

1. Télécharger le fichier d’installation de l’agent hello à partir du portail OMS hello
2. Installer l’agent hello à l’aide de la méthode hello choisie
3. Configurer l’agent de hello ou ajouter des espaces de travail supplémentaires, si nécessaire

Hello diagramme suivant montre hello relation entre vos ordinateurs Windows et OMS une fois que vous avez installé et configuré des agents.

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

Si vos stratégies de sécurité informatique n’autorisent pas les ordinateurs sur votre toohello de tooconnect réseau Internet, vous pouvez configurer votre toohello de tooconnect ordinateurs OMS passerelle. Pour plus d’informations sur comment tooconfigure toocommunicate de vos serveurs via un service OMS toohello de passerelle d’OMS, consultez [connecter tooOMS d’ordinateurs à l’aide de hello OMS passerelle](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Configuration requise
Avant d’installer ou de déployer des agents, passez en revue hello suivant tooensure détails hello requise.

- Vous ne pouvez installer hello OMS MMA sur les ordinateurs exécutant Windows Server 2008 SP 1 ou version ultérieure ou Windows 7 SP1 ou version ultérieure.
- Vous avez besoin d’un abonnement Azure.  Pour plus d’informations, consultez l’article [Prise en main de Log Analytics](log-analytics-get-started.md).
- Chaque ordinateur Windows doit être en mesure de tooconnect toohello Internet à l’aide de HTTPS ou toohello OMS passerelle. Cette connexion peut être directe, via un proxy, ou hello OMS passerelle.
- Vous pouvez installer hello OMS MMA sur les ordinateurs autonomes, des serveurs et des ordinateurs virtuels. Si vous souhaitez tooconnect les ordinateurs virtuels hébergés par Azure tooOMS, consultez [tooLog de machines virtuelles Azure de se connecter Analytique](log-analytics-azure-vm-extension.md).
- l’agent Hello doit toouse le port TCP 443 pour les différentes ressources.

### <a name="network"></a>Réseau

Pour Windows agents tooconnect tooand inscrire auprès de service d’OMS hello, ils doivent avoir accès toonetwork ressources, notamment les numéros de port hello et les URL de domaine.

- Pour les serveurs proxy, vous devez tooensure qui hello du serveur proxy approprié ressources sont configurés dans les paramètres de l’agent.
- Pour les pare-feu qui limitent l’accès toohello Internet, vous ou vos ingénieurs réseau doivent tooconfigure votre tooOMS d’accès de toopermit pare-feu. Aucune action n’est nécessaire dans les paramètres de l’agent.

Hello tableau suivant montre les ressources nécessaires pour la communication.

>[!NOTE]
>Certains hello suivant des ressources mentionnent Operational Insights, qui était un ancien nom d’Analytique de journal.

| Ressource de l'agent | Ports | Ignorer l’inspection HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Oui |
| *.oms.opinsights.azure.com | 443 | Oui |
| *.blob.core.windows.net | 443 | Oui |
| *.azure-automation.net | 443 | Oui |



## <a name="download-hello-agent-setup-file-from-oms"></a>Télécharger le fichier d’installation de l’agent hello d’OMS
1. Dans le portail OMS hello, sur hello **vue d’ensemble** , cliquez sur hello **paramètres** vignette.  Cliquez sur hello **Sources connectées** onglet en haut de hello.  
    ![onglet Sources connectées](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Cliquez sur **serveurs Windows** puis cliquez sur **télécharger l’Agent Windows** tooyour applicable ordinateur processeur toodownload hello fichier des paramètres.
3. Sur hello à droite de **ID de l’espace de travail**, cliquez sur icône de copie hello et collez hello ID dans le bloc-notes.
4. Sur hello à droite de **clé primaire**, cliquez sur icône de copie hello et collez la clé de hello dans le bloc-notes.     

## <a name="install-hello-agent-using-setup"></a>Installer l’agent de hello à l’aide du programme d’installation
1. Exécutez l’agent hello de tooinstall le programme d’installation sur un ordinateur que vous souhaitez toomanage.
2. Dans la page d’accueil hello, cliquez sur **suivant**.
3. Dans la page termes du contrat de licence de hello, lisez hello de licence, puis sur **J’accepte**.
4. Sur la page dossier de Destination de hello, modifier ou conservez le dossier d’installation par défaut hello et puis cliquez sur **suivant**.
5. Sur la page d’Options d’installation de l’Agent hello, vous pouvez choisir tooconnect hello agent tooAzure Analytique des journaux (OMS), Operations Manager, ou vous pouvez laisser le choix de hello vide si vous souhaitez que l’agent de tooconfigure hello plus tard. Cliquez sur **Suivant**.   
    - Si vous avez choisi tooconnect tooAzure Analytique des journaux (OMS), collez hello **ID de l’espace de travail** et **clé de l’espace de travail (clé primaire)** que vous avez copié dans le bloc-notes, dans la procédure précédente de hello puis cliquez sur  **Suivant**.  
        ![Coller l’ID et la clé primaire de l’espace de travail](./media/log-analytics-windows-agents/connect-workspace.png)
    - Si vous avez choisi tooconnect tooOperations Manager, tapez Bonjour **nom du groupe d’administration**, **Management Server** nom, et **Port serveur d’administration**, puis cliquez sur **Suivant**. Sur la page compte d’Action de l’Agent de hello, choisissez le compte système Local de hello ou d’un compte de domaine local, puis sur **suivant**.  
        ![Configuration du groupe d’administration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![compte d’action d’agent](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. Dans la page de prêt tooInstall hello, passez en revue vos choix, puis sur **installer**.
7. Page hello Configuration terminée, cliquez sur **Terminer**.
8. Lorsque vous avez terminé, hello **Microsoft Monitoring Agent** s’affiche dans **le panneau de configuration**. Vous pouvez vérifier votre configuration il et vérifiez que l’agent hello est connecté tooOperational Insights (OMS). Lorsque tooOMS connectés, hello agent affiche un message indiquant : **hello Microsoft Monitoring Agent n’est pas connecté service de Microsoft Operations Management Suite toohello.**

## <a name="configure-proxy-settings"></a>Configuration des paramètres de proxy

Vous pouvez utiliser hello suivant les paramètres du proxy tooconfigure procédure pour hello Microsoft Monitoring Agent dans le panneau de configuration. Vous devez toouse de cette procédure pour chaque serveur. Si vous avez plusieurs serveurs que vous avez besoin de tooconfigure, il peut s’avérer plus facile toouse un tooautomate script ce processus. Dans ce cas, consultez la procédure suivante de hello [tooconfigure les paramètres de proxy de Microsoft Monitoring Agent à l’aide d’un script de hello](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>paramètres de proxy tooconfigure pourquoi Microsoft Monitoring Agent dans le panneau de configuration
1. Ouvrez le **Panneau de configuration**.
2. Ouvrez **Microsoft Monitoring Agent**.
3. Cliquez sur hello **paramètres Proxy** onglet.  
    ![Onglet Paramètres de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Sélectionnez **utiliser un serveur proxy** et tapez Bonjour URL et le numéro de port, si une est exemple toohello nécessaire, comme indiqué. Si votre serveur proxy requiert une authentification, tapez Bonjour nom d’utilisateur et mot de passe tooaccess hello serveur proxy.


### <a name="verify-agent-connectivity-toooms"></a>Vérifiez tooOMS de connectivité de l’agent

Vous pouvez facilement vérifier si vos agents communiquent avec OMS à l’aide de la procédure de hello :

1.  Sur l’ordinateur hello avec l’agent Windows hello, ouvrez le panneau de configuration.
2.  Ouvrez Microsoft Monitoring Agent.
3.  Cliquez sur onglet d’Analytique des journaux (OMS) Azure hello.
4.  Dans la colonne d’état hello, vous devez voir que l’agent hello correctement toohello Operations Management Suite service connecté.

![agent connecté](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>paramètres de proxy tooconfigure pourquoi Microsoft Monitoring Agent à l’aide d’un script
Copiez hello suivantes exemple, de mises à jour spécifiques tooyour environnement, enregistrement avec une extension de nom de fichier PS1 et puis exécutez le script de hello sur chaque ordinateur qui se connecte directement service OMS de toohello.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Installer l’agent de hello à l’aide de la ligne de commande hello
- Modifier, puis utilisez hello suivant de l’agent hello exemple tooinstall à l’aide de la ligne de commande hello. exemple de Hello effectue une installation entièrement sans assistance.

    >[!NOTE]
    Si vous voulez tooupgrade un agent, vous devez toouse hello Analytique de journal API de script. Consultez hello suivant section tooupgrade un agent.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

l’agent de Hello utilise IExpress comme son Self-extractor à l’aide de hello `/c` commande. Vous pouvez voir les commutateurs de ligne de commande hello [des commutateurs de ligne de commande pour IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) et puis mise à jour hello exemple toosuit vos besoins.

|Options propres à MMA                   |Remarques         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = espace de travail de l’agent tooreport tooa configurer hello                |
|OPINSIGHTS_WORKSPACE_ID                | Espace de travail Id (guid) pour tooadd d’espace de travail hello                    |
|OPINSIGHTS_WORKSPACE_KEY               | Espace de travail de tooinitially utilisé clé s’authentifier avec un espace de travail hello |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Spécifier l’environnement en nuage hello où se trouve espace de travail hello <br> 0 = cloud commercial Azure (par défaut) <br> 1 = Azure Government |
|OPINSIGHTS_PROXY_URL               | URI pour hello proxy toouse |
|OPINSIGHTS_PROXY_USERNAME               | Nom d’utilisateur tooaccess un proxy authentifié |
|OPINSIGHTS_PROXY_PASSWORD               | Mot de passe tooaccess un proxy authentifié |

>[!NOTE]
limite de longueur de ligne de commande de hello atteinte tooavoid de IExpress, installez l’agent de hello avec aucun espace de travail configuré, puis utilisez une configuration de tooset de script pour l’espace de travail hello.

>[!NOTE]
Si vous obtenez un `Command line option syntax error.` lors de l’utilisation de hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` paramètre, vous pouvez utiliser hello suivant la solution de contournement :
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Ajouter un espace de travail à l’aide d’un script
Ajouter un espace de travail à l’aide des API de script de l’agent hello Analytique de journal avec hello l’exemple suivant :

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd un espace de travail dans Azure pour le gouvernement, hello utilisation suivant l’exemple de script :
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Si vous avez utilisé de ligne de commande hello ou un script précédemment tooinstall ou configurer l’agent hello, `EnableAzureOperationalInsights` a été remplacé par `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Installer l’agent de hello à l’aide de DSC dans Azure Automation

Vous pouvez utiliser hello suivant script exemple tooinstall hello l’agent à l’aide de DSC dans Azure Automation. exemple Hello installe hello agent 64 bits, identifié par hello `URI` valeur. Vous pouvez également utiliser la version 32 bits de hello en remplaçant la valeur de l’URI hello. Hello URI pour les deux versions sont les suivantes :

- Agent Windows 64 bits - https://go.microsoft.com/fwlink/?LinkId=828603
- Agent Windows 32 bits - https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
Cette procédure et cet exemple de script ne mettent pas à niveau un agent existant.

1. Importer hello xPSDesiredStateConfiguration Module DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) dans Azure Automation.  
2.  Créez des ressources variables Azure Automation pour *OPSINSIGHTS_WS_ID* et *OPSINSIGHTS_WS_KEY*. Définissez *OPSINSIGHTS_WS_ID* ID d’espace de travail Analytique des journaux OMS tooyour et *OPSINSIGHTS_WS_KEY* toohello la clé primaire de votre espace de travail.
3.  Utilisez hello suivants de script et l’enregistrement en tant que MMAgent.ps1
4.  Modifier, puis utilisez hello suivant de l’agent hello exemple tooinstall à l’aide de DSC dans Azure Automation. Importer MMAgent.ps1 dans Azure Automation en utilisant l’interface d’Azure Automation hello ou l’applet de commande.
5.  Attribuer une configuration toohello de nœud. Dans les 15 minutes, nœud de hello vérifie sa configuration et hello MMA est transmise toohello nœud.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Obtenir la dernière valeur de ProductId hello

Hello `ProductId value` Bonjour MMAgent.ps1 script est la version de l’agent tooeach unique. Lorsqu’une version mise à jour de chaque agent est publiée, hello ProductId valeur change. Par conséquent, lorsqu’il modifie hello ProductId Bonjour futures, vous trouverez version de l’agent hello à l’aide d’un script simple. Après avoir configuré hello agent version la plus récente installée sur un serveur de test, vous pouvez utiliser hello script tooget hello installé ProductId valeur suivante. À l’aide de la dernière valeur de ProductId hello, vous pouvez mettre à jour hello Bonjour MMAgent.ps1 script.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Configurer un agent manuellement ou ajouter des espaces de travail supplémentaires
Si vous avez installé les agents, mais n’a ne pas configuré les ou si vous souhaitez que les espaces de travail toomultiple hello agent tooreport, vous pouvez utiliser des hello suivant informations tooenable un agent ou le reconfigurer. Une fois que vous avez configuré l’agent de hello, il s’inscrire auprès du service de l’agent de hello et obtenir des informations de configuration nécessaires et les packs d’administration qui contiennent des informations sur la solution.

1. Une fois que vous avez installé hello Microsoft Monitoring Agent, ouvrez **le panneau de configuration**.
2. Ouvrez **Microsoft Monitoring Agent** puis cliquez sur hello **Analytique des journaux (OMS) Azure** onglet.   
3. Cliquez sur **ajouter** tooopen hello **ajouter un espace de travail Analytique de journal** boîte.
4. Hello de coller **ID de l’espace de travail** et **clé de l’espace de travail (clé primaire)** que vous avez copié dans le bloc-notes dans une procédure précédente pour l’espace de travail hello que vous souhaitez tooadd, puis sur **OK**.  
    ![configurer Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)

Une fois que les données sont collectées à partir des ordinateurs analysés par agent de hello, nombre de hello d’ordinateurs analysés par OMS apparaît dans le portail OMS est hello sur hello **Sources connectées** onglet **paramètres** comme  **Serveurs connectés**.


## <a name="toodisable-an-agent"></a>toodisable un agent
1. Après avoir installé l’agent de hello, ouvrez **le panneau de configuration**.
2. Ouvrez Microsoft Monitoring Agent, puis cliquez sur hello **Analytique des journaux (OMS) Azure** onglet.
3. Sélectionnez un espace de travail, puis cliquez sur **Supprimer**. Répétez cette étape pour tous les autres espaces de travail.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>Éventuellement, configurez le groupe d’administration Operations Manager agents tooreport tooan

Si vous utilisez Operations Manager dans votre infrastructure informatique, vous pouvez également utiliser l’agent de hello MMA comme un agent Operations Manager.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>groupe d’administration tooconfigure MMA agents tooreport tooan Operations Manager
1.  Sur ordinateur hello où hello agent est installé, ouvrez **le panneau de configuration**.  
2.  Ouvrez **Microsoft Monitoring Agent** puis cliquez sur hello **Operations Manager** onglet.  
    ![onglet Operations Manager de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/om-mg01.png)
3.  Si vos serveurs Operations Manager sont intégrés à Active Directory, cliquez sur **Met à jour automatiquement les attributions du groupe d’administration à partir d’AD DS**.
4.  Cliquez sur **ajouter** tooopen hello **ajouter un groupe d’administration** boîte de dialogue.  
    ![Microsoft Monitoring Agent Ajouter un groupe d’administration](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  Dans **nom de groupe d’administration** zone, entrez un nom hello de votre groupe d’administration.
6.  Bonjour **serveur d’administration principal** zone, le nom d’ordinateur de type hello hello principal du serveur d’administration.
7.  Bonjour **port serveur d’administration** zone, le numéro de port TCP de type hello.
8.  Sous **compte Action d’Agent**, choisissez le compte système Local de hello ou d’un compte de domaine local.
9.  Cliquez sur **OK** tooclose hello **ajouter un groupe d’administration** boîte de dialogue, puis cliquez sur **OK** tooclose hello **Microsoft des propriétés de l’Agent d’analyse**boîte de dialogue.


## <a name="next-steps"></a>Étapes suivantes

- [Ajouter des solutions d’Analytique de journal à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md) tooadd fonctionnalité et collecter les données.
