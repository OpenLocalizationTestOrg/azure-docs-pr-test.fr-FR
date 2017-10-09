---
title: "journaux aaaIntegrate d’Azure Key Vault à l’aide de concentrateurs d’événements | Documents Microsoft"
description: "Didacticiel qui fournit les étapes nécessaires de hello toomake le coffre de clés journaux disponible tooa SIEM grâce à l’intégration des journaux Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Didacticiel sur l’intégration des journaux Azure : traiter les événements Azure Key Vault à l’aide d’Event Hubs

Vous pouvez utiliser les événements d’intégration des journaux Azure tooretrieve connecté et les rendre disponibles tooyour événements et des informations système security management (SIEM). Ce didacticiel montre comment intégration des journaux Azure peuvent être des journaux tooprocess utilisés qui sont acquis par Azure Event Hubs.
 
Utilisez ce didacticiel tooget connaissance des comment le travail d’intégration des journaux Azure et les concentrateurs d’événements en suivant hello exemples d’étapes et de comprendre comment chaque étape prend en charge les solutions hello. Ensuite, vous pouvez prendre ce que vous avez appris ici toocreate toosupport de vos propres étapes exigences uniques de votre société.

>[!WARNING]
étapes de Hello et les commandes de ce didacticiel ne sont pas prévu toobe copiées et collées. Elles sont uniquement indiquées à titre d’exemple. N’utilisez pas les commandes de PowerShell hello « tel quel » dans votre environnement dynamique. Vous devez en effet les personnaliser en fonction de votre environnement.


Ce didacticiel vous guide tout au long des processus hello concentrateur d’événements Azure Key Vault activité tooan connecté et rendre disponible en tant que système SIEM JSON fichiers tooyour de. Vous pouvez ensuite configurer vos fichiers JSON de SIEM système tooprocess hello.

>[!NOTE]
>La plupart des étapes hello dans ce didacticiel implique la configuration de coffres de clé, les comptes de stockage et les concentrateurs d’événements. les étapes d’intégration de journal Azure Hello spécifiques sont à fin hello de ce didacticiel. N’effectuez pas ces étapes dans un environnement de production, car elles sont uniquement destinées à un environnement lab. Vous devez personnaliser les étapes hello avant de les utiliser en production.

Les informations fournies le long de permet de façon hello que comprendre les raisons hello derrière chaque étape. Articles tooother de liens pour obtenir plus de détails sur certaines rubriques.

Pour plus d’informations sur les services hello qui mentionne de ce didacticiel, consultez : 

- [Azure Key Vault](../key-vault/key-vault-whatis.md)
- [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Intégration des journaux Azure](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>Configuration initiale

Avant que vous pouvez effectuer les étapes de hello dans cet article, vous devez suivant de hello :

1. Un abonnement Azure et un compte dans cet abonnement avec des droits d’administrateur. Si vous ne disposez d’aucun abonnement, vous pouvez créer [un compte gratuitement](https://azure.microsoft.com/free/).
 
2. Un système avec accès toohello internet qui répond aux exigences de hello pour l’installation d’intégration du journal Azure. système de Hello peut se trouver sur un service cloud ou hébergé localement.

3. Solution d’[intégration des journaux Azure](https://www.microsoft.com/download/details.aspx?id=53324) installée. tooinstall il :

   a. Utilisez Bureau à distance tooconnect toohello système mentionné à l’étape 2.   
   b. Copiez hello Azure journal d’installation toohello système d’intégration. Vous pouvez [télécharger les fichiers d’installation hello](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Démarrer le programme d’installation hello et accepter le contrat de licence logiciel Microsoft hello.   
   d. Si vous fournit des informations de télémétrie, laissez hello case est cochée. Si vous préfère pas envoyer tooMicrosoft des informations d’utilisation, désactivez la case à cocher hello.
   
   Pour plus d’informations sur l’intégration des journaux Azure et comment tooinstall, consultez [intégration du journal Azure avec la journalisation des Diagnostics Windows Azure et le transfert d’événements Windows](security-azure-log-integration-get-started.md).

4. dernière version du PowerShell Hello.
 
   Si vous avez installé Windows Server 2016, vous disposez au moins de PowerShell 5.0. Si vous utilisez une autre version de Windows Server, il est possible que vous possédiez une version antérieure de PowerShell. Vous pouvez vérifier la version de hello en entrant ```get-host``` dans une fenêtre PowerShell. Si vous n’avez pas installé PowerShell 5.0, vous pouvez [le télécharger](https://www.microsoft.com/download/details.aspx?id=50395).

   Une fois que vous avez au moins PowerShell 5.0, vous pouvez passer la version la plus récente tooinstall hello :
   
   a. Dans une fenêtre PowerShell, entrez hello ```Install-Module Azure``` commande. Effectuez les étapes d’installation hello.    
   b. Entrez hello ```Install-Module AzureRM``` commande. Effectuez les étapes d’installation hello.

   Pour plus d’informations, consultez l’article [Installation et configuration d’Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Créer les éléments d’infrastructure sous-jacents

1. Ouvrez une fenêtre PowerShell avec élévation de privilèges et accédez trop**C:\Program Files\Microsoft Azure journal intégration**.
2. Importer les applets de commande hello AzLog en exécutant le script hello LoadAzLogModule.ps1. Entrez hello `.\LoadAzLogModule.ps1` commande. (Hello d’avis ». \ » dans cette commande.) Le résultat suivant devrait s'afficher :</br>

   ![Liste des modules chargés](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Entrez hello `Login-AzureRmAccount` commande. Dans la fenêtre de connexion hello, entrez les informations d’identification de hello pour l’abonnement hello que vous allez utiliser pour ce didacticiel.

   >[!NOTE]
   >S’il s’agit hello première fois que vous êtes connecté dans tooAzure à partir de cet ordinateur, vous verrez un message pour autoriser les données d’utilisation de Microsoft toocollect PowerShell. Nous vous recommandons d’activer cette collecte de données, car elle sera utilisée tooimprove Azure PowerShell.

4. Après une authentification réussie, vous êtes connecté et informations hello hello suivant capture d’écran. Prenez note du nom d’abonnement hello ID et l’abonnement, car vous en aurez besoin toocomplete étapes plus tard.

   ![Fenêtre PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Créer des variables toostore les valeurs qui seront utilisés ultérieurement. Entrez chaque hello PowerShell lignes suivantes. Vous devrez peut-être tooadjust hello valeurs toomatch votre environnement.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Votre nom d’abonnement peut être différent. Vous pouvez voir dans le cadre de la sortie de hello de la commande précédente hello.)
    - ```$location = 'West US'```(Cette variable sera utilisé toopass emplacement de hello où les ressources doivent être créés. Vous pouvez modifier cette variable toobe n’importe quel emplacement de votre choix.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(nom de hello quoi que ce soit possible, mais il doit inclure uniquement des lettres minuscules et chiffres.)
    - ``` $storageName = $name```(Cette variable servira pour le nom de compte de stockage hello.)
    - ```$rgname = $name ```(Cette variable servira pour le nom de groupe de ressources hello.)
    - ``` $eventHubNameSpaceName = $name```(Cela est nom hello d’espace de noms hello événement hub.)
6. Spécifier l’abonnement de hello vous travaillerez avec :
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Créez un groupe de ressources :
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Si vous entrez `$rg` à ce stade, vous devez voir la capture d’écran toothis similaire de sortie :

   ![Sortie après la création d’un groupe de ressources](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Créer un compte de stockage qui sera suivi tookeep utilisé des informations d’état :
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Créer un espace de noms hello événement hub. Il s’agit d’un concentrateur d’événements de toocreate requis.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Obtenir l’ID de règle hello qui est utilisée avec le fournisseur d’insights hello :
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Obtenir tous les emplacements Azure possibles et ajoutez hello noms tooa variable qui peut être utilisé dans une étape ultérieure :
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Si vous entrez `$locations` à ce stade, vous voyez des noms d’emplacement hello sans information supplémentaire de hello retournée par Get-AzureRmLocation.
12. Créez un profil de journal Azure Resource Manager : 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Pour plus d’informations sur hello profil journal Azure, consultez [vue d’ensemble du journal des activités Azure de hello](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> Vous pouvez obtenir un message d’erreur lorsque vous essayez de toocreate un profil de journal. Vous pouvez ensuite vérifier documentation hello pour Get-AzureRmLogProfile et Remove-AzureRmLogProfile. Si vous exécutez Get-AzureRmLogProfile, vous consultez des informations sur le profil du journal hello. Vous pouvez supprimer le profil du journal existant hello en entrant hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` commande.
>
>![Erreur de profil Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Création d’un coffre de clés

1. Créez un coffre de clés hello :

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Configurer la journalisation pour le coffre de clés hello :

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Générer l’activité de journalisation

Demandes doivent toobe envoyé tooKey coffre toogenerate journalisation de l’activité. Des actions telles que la génération de clés, le stockage de secrets ou la lecture de secrets à partir de Key Vault entraînent la création d’entrées de journal.

1. Afficher les clés de stockage actuel hello :
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Générez une nouvelle valeur **key2** :
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Afficher les clés hello et vous constatez que **key2** contient une valeur différente :
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Définir et lire des entrées de journal supplémentaires d’un secret toogenerate :
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Secret renvoyé](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Configurer l’intégration des journaux Azure

Maintenant que vous avez configuré le concentrateur d’événements hello éléments requis toohave journalisation du coffre de clés tooan tous les, vous devez tooconfigure intégration des journaux Azure :

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Exécutez la commande de AzLog hello pour chaque concentrateur d’événements :

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

Après une minute de l’exécution des deux dernières commandes hello, vous devez voir les fichiers au format JSON en cours de génération. Vous pouvez confirmer que par l’analyse du répertoire de hello **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Étapes suivantes

- [Forum aux questions sur l’intégration des journaux Azure](security-azure-log-integration-faq.md)
- [Bien démarrer avec l’intégration des journaux Azure](security-azure-log-integration-get-started.md)
- [Intégrer des journaux à partir de ressources Azure dans vos systèmes SIEM](security-azure-log-integration-overview.md)
