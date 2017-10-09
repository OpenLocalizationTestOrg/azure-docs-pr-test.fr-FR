---
title: "aaaSet d’Azure Key Vault avec rotation de clés de bout en bout et d’audit | Documents Microsoft"
description: "Utilisez cette procédure-tootoohelp que vous être défini sur la rotation des clés et l’analyse des journaux de coffre de clés."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>Configurer Azure Key Vault avec une rotation des clés et un audit de bout en bout
## <a name="introduction"></a>Introduction
Après avoir créé votre coffre de clés, vous serez en mesure de toostart à l’aide de ce coffre toostore vos clés et les clés secrètes. Vos applications n’est plus nécessaire toopersist vos clés ou les clés secrètes, mais au lieu de cela demande les hello coffre de clés en fonction des besoins. Ainsi, vous tooupdate clés et les secrets sans affecter le comportement de hello de votre application, ce qui ouvre un éventail de possibilités autour de votre clé et la gestion des secrets.

Cet article assiste un exemple d’utilisation d’Azure Key Vault toostore un secret, dans ce cas, une clé de compte de stockage Azure qui est accessible par une application. Il vous propose également une démonstration d’implémentation d’une rotation planifiée de cette clé de compte de stockage. Enfin, il décrit une démonstration de comment toomonitor hello les journaux d’audit de coffre de clés et de déclencher des alertes lorsque des demandes inattendus sont effectuées.

> [!NOTE]
> Ce didacticiel n’est pas prévue tooexplain détail hello la configuration initiale de votre coffre de clés. Pour plus d’informations, consultez [Prise en main d’Azure Key Vault](key-vault-get-started.md). Pour connaître la marche à suivre avec l’interface de ligne de commande interplateforme, consultez la rubrique [Gestion de Key Vault à l’aide de l’interface de ligne de commande (CLI)](key-vault-manage-with-cli2.md).
>
>

## <a name="set-up-key-vault"></a>Configuration d’Azure Key Vault
tooenable un tooretrieve application un secret de coffre de clés, vous devez tout d’abord créer la clé secrète de hello et téléchargez-le tooyour coffre. Cela peut être accompli en démarrant une session Azure PowerShell et de signature dans tooyour compte Azure avec hello de commande suivante :

```powershell
Login-AzureRmAccount
```

Dans la fenêtre contextuelle du navigateur de hello, entrez votre nom d’utilisateur de compte Azure et un mot de passe. PowerShell Obtient tous les abonnements hello qui sont associés à ce compte. PowerShell utilise hello premier celui par défaut.

Si vous avez plusieurs abonnements, vous pouvez avoir toospecify qui a été utilisé toocreate hello votre coffre de clés. Entrez hello suivant toosee les abonnements de hello pour votre compte :

```powershell
Get-AzureRmSubscription
```

abonnement hello toospecify associé avec le coffre de clés hello vous se connectent, entrez :

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

Cet article présentant le stockage d’une clé de compte de stockage sous la forme d’un secret, vous devez obtenir cette clé de compte de stockage.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

Après avoir récupéré votre secret (dans ce cas, votre clé de compte de stockage), vous devez convertir cette chaîne sécurisée tooa et ensuite créer une clé secrète avec cette valeur dans votre coffre de clés.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
Ensuite, obtenez hello URI pour secret hello que vous avez créé. Cela est utilisé dans une étape ultérieure lorsque vous appelez hello coffre de clés tooretrieve votre clé secrète. Exécutez hello suivant de commande PowerShell et prenez note de la valeur d’ID hello, qui est un secret hello URI :

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Configurer application hello
Maintenant que vous avez une clé secrète stockée, vous pouvez utiliser le code tooretrieve et l’utiliser. Il existe quelques tooachieve requis d’étapes cela. Bonjour première étape la plus importante est l’inscription de votre application avec Azure Active Directory et puis indiquant le coffre de clés les informations de votre application afin qu’il peut autoriser les demandes à partir de votre application.

> [!NOTE]
> Votre application doit être créée sur hello même locataire Azure Active Directory en tant que votre coffre de clés.
>
>

Ouvrez l’onglet d’applications hello d’Azure Active Directory.

![Ouvrir des applications dans Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

Choisissez **ajouter** tooadd un tooyour application Azure Active Directory.

![Choisir AJOUTER](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Laissez le type d’application hello **WEB APPLICATION et/ou API WEB** et donnez un nom à votre application.

![Application hello nom](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

Attribuez à votre application une **URL DE CONNEXION** et un **URI ID D’APPLICATION**. Pour cette démonstration, il peut s’agir de n’importe quel URL/URI, et vous pouvez les modifier ultérieurement si nécessaire.

![Fournir les URI nécessaires](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Après l’application hello tooAzure Active Directory, vous seront mises en page de l’application hello. Cliquez sur hello **configurer** onglet, puis recherchez et copiez hello **ID Client** valeur. Prenez note de l’ID de client hello pour les étapes ultérieures.

Ensuite, générez une clé pour votre application afin qu’elle puisse interagir avec votre Azure Active Directory. Vous pouvez le créer sous hello **clés** section Bonjour **Configuration** onglet. Prenez note de clé hello qui vient d’être généré à partir de votre application Azure Active Directory pour une utilisation dans une étape ultérieure.

![Clés d’application Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Avant d’établir tous les appels à partir de votre application dans le coffre de clés hello, vous devez indiquer le coffre de clés hello sur votre application et ses autorisations. Hello commande suivante prend hello coffre nom et ID de client hello à partir de votre application d’Azure Active Directory et les allocations **obtenir** tooyour clé forte pour l’application hello.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

À ce stade, vous êtes prêt toostart générer votre application appelle. Dans votre application, vous devez installer hello NuGet packages requis toointeract avec le coffre de clés Azure et Azure Active Directory. À partir de la console du Gestionnaire de Package Visual Studio hello, entrez hello suivant les commandes. À l’écriture de hello de cet article, hello version actuelle du package d’Azure Active Directory hello est 3.10.305231913, vous souhaitez que la version la plus récente tooconfirm hello et mettre à jour en conséquence.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

Dans votre code d’application, créez une méthode de hello toohold classe pour l’authentification Azure Active Directory. Dans cet exemple, la classe est appelée **Utils**. Ajoutez hello qui suit à l’aide d’instruction :

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Ensuite, ajoutez hello suivant un jeton JWT méthode tooretrieve hello d’Azure Active Directory. Pour faciliter la maintenance, vous pouvez choisir les valeurs de chaîne codée en dur toomove hello dans votre configuration de l’application web ou.

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

Ajouter hello code nécessaire toocall le coffre de clés et récupérer la valeur de votre secret principal. Vous devez d’abord ajouter suivant de hello à l’aide d’instruction :

```csharp
using Microsoft.Azure.KeyVault;
```

Ajouter tooinvoke les appels de méthode hello coffre de clés et de récupérer votre clé secrète. Dans cette méthode, vous indiquez hello question secrète URI que vous avez enregistré à l’étape précédente. Notez que hello hello **GetToken** méthode hello **Utils** classe créée précédemment.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

Lorsque vous exécutez votre application, vous devez maintenant authentification tooAzure Active Directory et puis la récupération de la valeur de votre secret principal dans Azure Key Vault.

## <a name="key-rotation-using-azure-automation"></a>Rotation des clés à l’aide d’Azure Automation
Diverses options de mise en œuvre d’une stratégie de rotation sont possibles pour les valeurs que vous stockez sous forme de secrets Azure Key Vault. La rotation des secrets peut être manuelle, elle peut également être effectuée par programmation à l’aide d’appels d’API ou à l’aide d’un script Automation. Pour des raisons de hello de cet article, vous serez à l’aide d’Azure PowerShell combinées avec Azure Automation toochange une clé d’accès de compte de stockage Azure. Ensuite, vous mettrez à jour un secret de coffre de clés avec cette nouvelle clé.

tooallow Azure Automation tooset les valeurs des secrets dans votre coffre de clés, vous devez obtenir les ID de client hello pour connexion hello nommée AzureRunAsConnection, qui a été créée lorsque vous avez établi votre instance Azure Automation. Vous pouvez obtenir cet ID en choisissant **Actifs** dans votre instance Azure Automation. À partir de là, vous choisissez **connexions** , puis sélectionnez hello **AzureRunAsConnection** principe de service. Prenez note de hello **ID de l’Application**.

![ID client Azure Automation](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

Dans **Actifs**, choisissez **Modules**. À partir de **Modules**, sélectionnez **galerie**, puis recherchez et **importation** mis à jour les versions de chacune des hello suivant des modules :

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> À hello l’écriture de cet article, uniquement hello précédemment notées modules nécessaires toobe mis à jour pour hello script suivant. Si vous constatez un échec de votre tâche d’automatisation, vérifiez que tous les modules nécessaires et leurs dépendances ont été importés.
>
>

Une fois que vous avez extrait l’ID de l’application hello pour votre connexion Azure Automation, vous devez indiquer votre coffre de clés que cette application a accès tooupdate secrets dans le coffre. Cela peut être accompli par hello suivant de commande PowerShell :

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

Sélectionnez ensuite **Runbooks** sous votre instance Azure Automation, puis **Ajouter un runbook**. Sélectionnez **Création rapide**. Nom de votre runbook, puis choisissez **PowerShell** en tant que type de runbook hello. Vous avez hello option tooadd une description. Pour finir, cliquez sur **Créer**.

![Créer un runbook](./media/keyvault-keyrotation/Create_Runbook.png)

Collez hello script PowerShell dans le volet de l’éditeur pour votre nouveau runbook hello suivant :

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

Dans le volet de l’éditeur hello, choisissez **volet Test** tootest votre script. Une fois le script de hello s’exécute sans erreur, vous pouvez sélectionner **publier**, et vous pouvez ensuite appliquer une planification pour le runbook hello dans le volet de configuration de runbook hello.

## <a name="key-vault-auditing-pipeline"></a>Pipeline d’audit de Key Vault
Lorsque vous configurez un coffre de clés, vous pouvez activer l’audit des journaux de toocollect sur les demandes d’accès effectuées toohello coffre de clés. Ces journaux sont stockés dans un compte de stockage Azure spécifié et peuvent être récupérés, contrôlés et analysés. Hello scénario suivant utilise des fonctions Azure, les applications de la logique d’Azure et toocreate de journaux d’audit de coffre de clés un toosend pipeline un message électronique quand une application qui ne correspond pas aux ID de l’application hello de hello web application récupère les clés secrètes de coffre de hello.

Vous devez tout d’abord activer la journalisation sur votre coffre de clés. Cela est possible via hello suivant de commandes PowerShell (détails complets peuvent être consultés à [journalisation de coffre de clé](key-vault-logging.md)) :

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

Une fois cette option est activée, les journaux d’audit commencer à collecter dans hello désigné du compte de stockage. Ces journaux contiennent des événements indiquant la méthode et la date/l’heure d’accès à vos coffres de clés, et qui y a accédé.

> [!NOTE]
> Vous pouvez accéder à vos informations de journalisation 10 minutes après l’opération de coffre de clés hello. Elles sont généralement disponibles plus rapidement.
>
>

étape suivante de Hello est trop[créer une file d’attente Azure Service Bus](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md). C’est dans celle-ci que les journaux d’audit de coffre de clés sont envoyés. Lors de la file d’attente de hello des messages du journal d’audit hello, application logique de hello les récupère et agit sur eux. Créer un service bus avec hello comme suit :

1. Créer un espace de noms Service Bus (si vous disposez déjà de celui que vous voulez toouse pour ce faire, ignorer tooStep 2).
2. Parcourir toohello service bus dans hello portail Azure et sélectionnez hello espace de noms que vous souhaitez file d’attente de toocreate hello dans.
3. Sélectionnez **nouveau** et choisissez **Service Bus > file d’attente** et entrez les détails de hello requis.
4. Sélectionnez les informations de connexion de Service Bus hello en choisissant l’espace de noms hello en cliquant sur **les informations de connexion**. Vous devez ces informations pour la section suivante de hello.

Ensuite, [créer une fonction Azure](../azure-functions/functions-create-first-azure-function.md) toopoll les journaux de coffre de clés dans hello compte de stockage et de chercher de nouveaux événements. Il s’agit d’une fonction déclenchée de manière planifiée.

toocreate une fonction d’Azure, choisissez **Nouveau > application de la fonction** Bonjour portail Azure. Lors de la création, vous pouvez utiliser un plan d’hébergement existant ou en créer un nouveau. Vous pouvez également opter pour un hébergement dynamique. Vous trouverez plus d’informations sur les options d’hébergement de fonction à [comment tooscale Azure fonctions](../azure-functions/functions-scale.md).

Lors de la création de hello fonction Azure, accédez tooit et choisir un minuteur de fonction et C\#. Cliquez ensuite sur **Créer cette fonction**.

![Panneau d’accueil d’Azure Functions](./media/keyvault-keyrotation/Azure_Functions_Start.png)

Sur hello **développer** onglet, remplacez le code de run.csx hello par qui suit hello :

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> Rendre les variables de hello tooreplace vraiment Bonjour précédant compte de stockage de code toopoint tooyour où sont écrits les journaux de coffre de clés hello, vous avez créé précédemment, le bus des services hello et hello des journaux de stockage de coffre de clés toohello chemin d’accès spécifique.
>
>

fonction Hello récupère hello du dernier fichier journal à partir du compte de stockage hello où hello coffre de clés sont écrits les journaux, extrait les événements les plus récents hello à partir de ce fichier, et les transmet la file d’attente du Bus des services tooa. Dans la mesure où un seul fichier peut avoir plusieurs événements, vous devez créer un fichier de sync.txt fonction hello examine également horodatage toodetermine hello de hello du dernier événement qui a été récupéré. Cela garantit que vous n’effectuez un push hello même événement plusieurs fois. Ce fichier sync.txt contient un horodatage pour le dernier événement de rencontré hello. les journaux, lors du chargement, Hello ont toobe trié selon tooensure d’horodatage hello qu’ils sont ordonnés correctement.

Pour cette fonction, nous faire référence à quelques bibliothèques supplémentaires qui ne sont pas disponibles en dehors de la zone hello dans les fonctions d’Azure. tooinclude, nous avons besoin de fonctions de Azure toopull les à l’aide de NuGet. Choisissez hello **afficher les fichiers** option.

![Option Afficher les fichiers](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

Et ajoutez un fichier appelé project.json avec le contenu suivant :

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
Fonction **enregistrer**, les fonctions Azure téléchargera les fichiers binaires de hello requis.

Commutateur toohello **intégrer** onglet et donner de paramètre de minuteur hello un toouse nom explicite au sein de la fonction hello. Bonjour précédant le code, il attend toobe de minuteur hello appelé *myTimer*. Spécifiez un [expression CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) comme suit : 0 \* \* \* \* \* de minuterie hello qui provoque hello fonction toorun une fois par minute.

Sur hello même **intégrer** onglet, ajouter une entrée de type de hello **stockage d’objets Blob Azure**. Cela pointe toohello sync.txt fichier qui contient l’horodatage de hello de hello du dernier événement de fonction hello consulté. Ce sera disponible au sein de la fonction hello par nom de paramètre hello. Bonjour précédant le code, entrée de stockage d’objets Blob Azure hello attend toobe de nom de paramètre hello *inputBlob*. Choisissez le compte de stockage hello où se trouve hello sync.txt fichier (il peut être hello même ou à un autre compte de stockage). Dans le champ de chemin d’accès de hello, indiquez le chemin de hello où les fichiers hello résident dans le format hello {container-name}/path/to/sync.txt.

Ajouter une sortie de type de hello *stockage d’objets Blob Azure* sortie. Ce fichier de sync.txt toohello que vous défini dans l’entrée de hello pointe. Ceci est utilisé par hello fonction toowrite hello timestamp de hello du dernier événement étudié. code précédent Hello attend ce toobe paramètre appelé *outputBlob*.

À ce stade, la fonction hello est prête. Rendre toohello de retour que tooswitch **développer** onglet et enregistrer le code de hello. Consultez la fenêtre de sortie hello pour les erreurs de compilation et corrigez-les en conséquence. Si le code hello compilé, puis hello doit maintenant être la vérification du code hello coffre de clés journaux toutes les minutes et en exécutant un push de tous les nouveaux événements sur hello défini de file d’attente Service Bus. Vous devez voir les informations de journalisation écrivent les fenêtre du journal toohello chaque fois que la fonction de hello est déclenchée.

### <a name="azure-logic-app"></a>Application logique Azure
Ensuite, vous devez créer une application Azure logique qui sélectionne les événements hello que fonction hello repousse file d’attente du Service Bus toohello, analyse le contenu de hello et envoie un message électronique selon une condition de correspondance.

[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md) en accédant trop**Nouveau > Application logique**.

Une fois que l’application logique de hello est créée, accédez tooit et choisissez **modifier**. Dans l’éditeur de l’application hello logique, choisissez **file d’attente du Bus de Service** et entrez votre tooconnect d’informations d’identification de Service Bus il file d’attente toohello.

![Service Bus d’application logique Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

Choisissez ensuite **Ajouter une condition**. Dans la condition de hello, basculez toohello éditeur avancé, puis entrez hello suivant de code, en remplaçant APP_ID par hello APP_ID réel de votre application web :

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

Cette expression retourne essentiellement **false** si hello *appid* de hello événement entrant (qui est le corps de hello du message d’appel du Service Bus) n’est pas hello *appid* Hello application.

Créez maintenant une action sous **Si non, ne rien faire**.

![Choisir une action d’application logique Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Pour l’action de hello, choisissez **Office 365 - envoyer un e-mail**. Remplir hello champs toocreate un toosend par courrier électronique lorsque hello définie par la condition retourne **false**. Si vous n’avez pas d’Office 365, vous pouvez examiner alternatives tooachieve hello les mêmes résultats.

À ce stade, vous disposez d’un pipeline tooend fin qui se présente pour les nouveaux journaux d’audit de coffre de clés, une fois par minute. Il exécute un push de nouveaux journaux qu’il trouve la file d’attente de bus de service tooa. application de la logique de Hello est déclenchée lorsqu’un nouveau message arrive dans la file d’attente hello. Si hello *appid* dans hello événement ne correspond pas à ID de l’application hello Hello appel d’application, il envoie un message électronique.
