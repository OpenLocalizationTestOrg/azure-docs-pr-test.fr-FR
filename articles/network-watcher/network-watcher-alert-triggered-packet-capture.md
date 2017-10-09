---
title: "toodo de capture de paquet aaaUse proactive de la surveillance des alertes et les fonctions d’Azure réseau | Documents Microsoft"
description: "Cet article décrit comment toocreate une alerte déclenchée capture de paquet avec l’Observateur de réseau Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Utiliser une capture de paquets pour effectuer une surveillance proactive du réseau avec des alertes et Azure Functions

Capture des paquets réseau Observateur crée des sessions de capture tootrack un trafic vers et depuis des ordinateurs virtuels. Hello fichier de capture peut avoir un filtre défini tootrack hello uniquement le trafic que vous souhaitez toomonitor. Ces données sont ensuite stockées dans un objet blob de stockage ou localement sur l’ordinateur invité de hello.

Cette fonctionnalité peut être démarrée à distance à partir d’autres scénarios d’automatisation comme Azure Functions. Permet de capture de paquets sur que Hello de captures proactive de la fonctionnalité toorun basés définie anomalies réseau. Elle permet aussi de collecter des statistiques réseau, d’obtenir des informations sur les intrusions, de déboguer des communications client-serveur, etc.

Les ressources qui sont déployées dans Azure s’exécutent 24 heures sur 24, 7 jours sur 7. Vous et votre équipe ne peut pas analyser activement état hello de toutes les ressources 24/7. Par exemple, que se passe-t-il si un problème se produit à 2 h ?

Par l’Observateur réseau, d’alerte et fonctions à partir de hello écosystème Azure, vous pouvez répondre proactive hello données et outils toosolve aux problèmes dans votre réseau.

![Scénario][scenario]

## <a name="prerequisites"></a>Composants requis

* version la plus récente de Hello [Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Une instance existante de Network Watcher. Si vous n’en avez pas, [créez une instance de Network Watcher](network-watcher-create.md).
* Un ordinateur virtuel existant dans hello même région qu’Observateur réseau avec hello [extension Windows](../virtual-machines/windows/extensions-nwa.md) ou [extension de machine virtuelle Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Scénario

Dans cet exemple, votre machine virtuelle envoie des segments TCP plus que d’habitude, et vous souhaitez toobe alerté. Les segments TCP sont utilisés ici à titre d’exemple, mais vous pouvez utiliser n’importe quelle condition d’alerte.

Lorsque vous êtes averti, vous souhaitez toounderstand de données au niveau du paquet tooreceive pourquoi la communication a augmenté. Puis vous pouvez prendre des mesures communication de tooregular tooreturn hello machine virtuelle.

Ce scénario suppose que vous possédez une instance existante de Network Watcher, ainsi qu’un groupe de ressources avec une machine virtuelle valide.

Hello suivant liste est une vue d’ensemble du flux de travail hello qui a lieu :

1. Une alerte est déclenchée sur votre machine virtuelle.
1. alerte de Hello appelle votre fonction Azure via un webhook.
1. Votre fonction Azure traite l’alerte de hello et démarre une session de capture de paquet réseau Observateur.
1. capture des paquets Hello s’exécute sur hello machine virtuelle et le trafic de collecte.
1. Hello fichier de capture de paquet est téléchargé tooa compte de stockage pour la révision et de diagnostic.

tooautomate ce processus, nous créons et connecter une alerte sur notre tootrigger de machine virtuelle lors de l’incident de hello se produit. Nous permet également de créer une fonction toocall dans l’Observateur réseau.

Ce scénario hello suivant :

* crée une fonction Azure qui démarrera une capture de paquets ;
* Crée une règle d’alerte sur un ordinateur virtuel et configure hello toocall de règle d’alerte hello fonction Azure.

## <a name="create-an-azure-function"></a>Création d’une fonction Azure

première étape de Hello est toocreate une alerte de hello tooprocess fonction Azure et créer une capture de paquets.

1. Bonjour [portail Azure](https://portal.azure.com), sélectionnez **nouveau** > **de calcul** > **fonction application**.

    ![Création d’une application de fonction][1-1]

2. Sur hello **fonction application** panneau, entrez des valeurs suivantes de hello, puis sélectionnez **OK** toocreate hello application :

    |**Paramètre** | **Valeur** | **Détails** |
    |---|---|---|
    |**Nom de l’application**|PacketCaptureExample|nom Hello d’application de fonction hello.|
    |**Abonnement**|[Votre abonnement] hello d’abonnement pour l’application de fonction toocreate hello.||
    |**Groupe de ressources**|PacketCaptureRG|ressource groupe toocontain hello fonction application Hello.|
    |**Plan d’hébergement**|Plan de consommation| type Hello du plan par votre application de fonction. Deux options sont disponibles : Consommation ou Plan Azure App Service. |
    |**Emplacement**|Centre des États-Unis| région Hello toocreate hello fonction application.|
    |**Compte de stockage**|{généré automatiquement}| compte de stockage Hello nécessitant des fonctions de Azure pour le stockage à usage général.|

3. Sur hello **PacketCaptureExample fonction applications** panneau, sélectionnez **fonctions** > **fonction personnalisée**  >  **+**.

4. Sélectionnez **HttpTrigger-Powershell**, puis entrez hello restant d’informations. Enfin, toocreate fonction hello, sélectionnez **créer**.

    |**Paramètre** | **Valeur** | **Détails** |
    |---|---|---|
    |**Scénario**|Expérimental|Type de scénario|
    |**Nommer votre fonction**|AlertPacketCapturePowerShell|Nom de la fonction hello|
    |**Niveau d’autorisation**|Fonction|Niveau d’autorisation pour la fonction hello|

![Exemples de fonctions][functions1]

> [!NOTE]
> modèle de PowerShell Hello est expérimentale et n’a pas de prise en charge complète.

Les personnalisations sont requises pour cet exemple, ils sont expliquées dans hello comme suit.

### <a name="add-modules"></a>Ajouter des modules

toouse applets de commande PowerShell de l’Observateur réseau, téléchargez hello dernière PowerShell module toohello fonction application.

1. Sur votre ordinateur local avec des modules Azure PowerShell dernière hello installé, exécutez hello suivant de commande PowerShell :

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    Cela donne exemple hello de chemin d’accès local de vos modules Azure PowerShell. Ces dossiers sont utilisés dans une étape ultérieure. modules de Hello sont utilisées dans ce scénario sont :

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![Dossiers PowerShell][functions5]

1. Sélectionnez **paramètres de l’application de la fonction** > **accédez tooApp éditeur Service**.

    ![Paramètres Function App][functions2]

1. Avec le bouton hello **AlertPacketCapturePowershell** dossier, puis créez un dossier appelé **azuremodules**. 

4. Créez un sous-dossier pour chacun des modules dont vous avez besoin.

    ![Dossier et sous-dossiers][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Avec le bouton hello **AzureRM.Network** sous-dossier, puis sélectionnez **télécharger des fichiers**. 

6. Accédez tooyour Azure modules. Hello local **AzureRM.Network** dossier, sélectionnez tous les fichiers hello dans le dossier de hello. Sélectionnez ensuite **OK**. 

7. Répétez ces étapes pour **AzureRM.Profile** et **AzureRM.Resources**.

    ![Charger des fichiers][functions6]

1. Après avoir terminé, chaque dossier doit avoir des fichiers de module PowerShell hello à partir de votre ordinateur local.

    ![Fichiers PowerShell][functions7]

### <a name="authentication"></a>Authentification

applets de commande PowerShell de hello toouse, vous devez vous authentifier. Vous configurez l’authentification dans l’application de fonction hello. l’authentification tooconfigure, vous devez configurer les variables d’environnement et charger une application de fonction toohello un fichier de clé chiffrée.

> [!NOTE]
> Ce scénario fournit simplement un exemple d’authentification tooimplement avec des fonctions d’Azure. Il existe autres façons toodo cela.

#### <a name="encrypted-credentials"></a>Informations d’identification chiffrées

Hello PowerShell script suivant crée un fichier de clé appelé **PassEncryptKey.key**. Il fournit également une version chiffrée du mot de passe hello qui est fourni. Ce mot de passe est hello même mot de passe est défini pour l’application hello Azure Active Directory qui est utilisée pour l’authentification.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

Dans l’éditeur de Service d’application de l’application de fonction hello de hello, créez un dossier appelé **clés** sous **AlertPacketCapturePowerShell**. Puis téléchargez hello **PassEncryptKey.key** fichier que vous avez créé dans l’exemple PowerShell précédent de hello.

![Clé de fonctions][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Récupérer des valeurs pour les variables d’environnement

spécification finale de Hello est tooset les variables d’environnement hello qui sont des valeurs hello tooaccess nécessaire pour l’authentification. Hello liste suivante montre les variables d’environnement hello qui sont créés :

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

ID de client Hello est hello ID d’Application d’une application dans Azure Active Directory.

1. Si vous n’avez pas encore un toouse de l’application, vous pouvez exécuter hello suivant exemple toocreate une application.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > mot de passe Hello que vous utilisez lors de la création d’application hello doit être hello même mot de passe que vous avez créé précédemment lors de l’enregistrement du fichier de clé hello.

1. Bonjour portail Azure, sélectionnez **abonnements**. Sélectionnez hello abonnement toouse, puis **(IAM) de contrôle d’accès**.

    ![IAM de fonctions][functions9]

1. Choisissez hello compte toouse, puis sélectionnez **propriétés**. Copiez hello ID d’Application.

    ![ID de l’application de fonctions][functions10]

#### <a name="azuretenant"></a>AzureTenant

Obtenir l’ID du locataire hello en exécutant hello suivant l’exemple PowerShell :

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

valeur Hello de variable d’environnement AzureCredPassword hello est la valeur hello que vous obtenez à partir de hello suivant l’exemple PowerShell en cours d’exécution. Cet exemple est hello identique à celui illustré hello précédent **informations d’identification chiffrées** section. Hello valeur suffisant est sortie hello Hello `$Encryptedpassword` variable.  Il s’agit de hello service principal mot de passe que vous avez chiffré à l’aide du script PowerShell de hello.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Enregistrer les variables d’environnement hello

1. Application de fonction toohello accédez. Sélectionnez ensuite **Paramètres Function App** > **Configurer les paramètres de l’application**.

    ![Configuration des paramètres d’application][functions11]

1. Ajouter des variables d’environnement hello et leurs paramètres de l’application toohello valeurs, puis sélectionnez **enregistrer**.

    ![Paramètres de l’application][functions12]

### <a name="add-powershell-toohello-function"></a>Ajouter la fonction toohello de PowerShell

Il est maintenant temps toomake appelle dans l’Observateur réseau à partir de hello fonction Azure. Selon les spécifications de hello, implémentation hello de cette fonction peut varier. Toutefois, le flux général de hello du code de hello est comme suit :

1. Traiter les paramètres d’entrée.
2. Paquet de requête existant tooverify limites de capture et résoudre les conflits de nom.
3. Créer une capture de paquets avec les paramètres appropriés.
4. Sonder régulièrement la capture de paquets jusqu’à la fin.
5. Avertir les utilisateurs hello que la session de capture de paquets hello est terminée.

Hello exemple suivant est le code PowerShell qui peut être utilisé dans la fonction hello. Il existe des valeurs qui doivent toobe remplacé pour **subscriptionId**, **resourceGroupName**, et **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Récupérer l’URL de fonction hello 
1. Une fois que vous avez créé votre fonction, configurez votre URL hello toocall alerte associée à la fonction hello. tooget cette valeur, la fonction hello copier l’URL à partir de votre application de la fonction.

    ![URL de recherche hello (fonction)][functions13]

2. Copier l’URL fonction hello pour votre application de la fonction.

    ![Copie l’URL de hello (fonction)][2]

Si vous avez besoin des propriétés personnalisées dans la charge utile de hello de requête de publication de webhook hello, consultez trop[configurer un webhook sur une alerte de métrique Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Configurer une alerte sur une machine virtuelle

Les alertes peuvent être configurés toonotify personnes lorsqu’une métrique spécifique dépasse un seuil affecté tooit. Dans cet exemple, alerte de hello est sur hello segments TCP envoyés, mais les alerte hello peuvent être déclenchée pour nombreuses autres métriques. Dans cet exemple, une alerte est configuré toocall une fonction de hello toocall webhook.

### <a name="create-hello-alert-rule"></a>Créer une règle d’alerte hello

Atteindre l’ordinateur virtuel existant de tooan, puis ajoutez une règle d’alerte. Pour accéder à une documentation plus détaillée sur la configuration des alertes, consultez l’article [Créer des alertes dans Azure Monitor pour les services Azure - Portail Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). Entrez les valeurs Bonjour suivantes de hello **une règle d’alerte** panneau, puis sélectionnez **OK**.

  |**Paramètre** | **Valeur** | **Détails** |
  |---|---|---|
  |**Nom**|TCP_Segments_Sent_Exceeded|Nom de règle d’alerte hello.|
  |**Description**|Les segments TCP envoyés ont dépassé le seuil|description de Hello pour la règle d’alerte hello.||
  |**Mesure**|Segments TCP envoyés| alerte de hello tootrigger Hello toouse métrique. |
  |**Condition**|Supérieur à| Hello condition toouse lors de l’évaluation de métrique de hello.|
  |**Seuil**|100| valeur Hello de métrique hello qui a déclenché l’alerte de hello. Cette valeur doit être définie tooa de valeur valide pour votre environnement.|
  |**Période**|Sur hello cinq dernières minutes| Détermine la période dans le toolook hello pour le seuil de hello sur métrique de hello.|
  |**Webhook**|[URL du webhook de l’application de fonction]| URL du webhook Hello à partir de l’application hello fonction qui a été créée dans les étapes précédentes hello.|

> [!NOTE]
> métrique de segments TCP Hello n’est pas activé par défaut. En savoir plus sur la façon tooenable des métriques supplémentaires en vous rendant sur [activation de la surveillance et de diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Passez en revue les résultats de hello

Une fois les critères hello pour les déclencheurs d’alerte hello, une capture de paquets est créée. Accédez tooNetwork Observateur, puis sélectionnez **capture des paquets**. Dans cette page, vous pouvez sélectionner la capture des paquets hello fichier lien toodownload hello paquet capture.

![Afficher une capture de paquets][functions14]

Si le fichier de capture hello est stockée localement, vous pouvez le récupérer en vous connectant toohello virtual machine.

Pour obtenir des instructions sur le téléchargement de fichiers à partir de comptes de stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Vous pouvez aussi utiliser [l’Explorateur de stockage](http://storageexplorer.com/).

Une fois la capture téléchargée, vous pouvez l’afficher à l’aide de n’importe quel outil en mesure de lire un fichier **.cap**. Voici les tootwo des liens de ces outils :

- [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment tooview vos captures de paquets en vous rendant sur [analyse des paquets de capture avec Wireshark](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
