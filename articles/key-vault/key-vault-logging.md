---
title: "aaaAzure enregistrement de clé de coffre | Documents Microsoft"
description: "Utilisez ce didacticiel toohelp vous prise en main d’Azure Key Vault journalisation."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Journalisation d’Azure Key Vault
Azure Key Vault est disponible dans la plupart des régions. Pour plus d’informations, consultez hello [page de tarification de coffre de clés](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Introduction
Après avoir créé un ou plusieurs coffres de clé, vous pouvez toomonitor comment et quand les coffres de votre clé sont utilisées et par qui. Pour ce faire, vous pouvez activer la journalisation du coffre de clés, ce qui permet d’enregistrer les informations dans un compte de stockage Azure que vous fournissez. Un nouveau conteneur nommé **insights-logs-auditevent** est automatiquement créé pour le compte de stockage spécifié, et vous pouvez utiliser ce même compte pour recueillir les journaux de plusieurs coffres de clés.

Vous pouvez accéder à vos informations de journalisation au maximum, 10 minutes après la clé de hello coffre l’opération. Dans la plupart des cas, ce sera plus rapide.  Il s’agit des tooyou toomanage vos journaux dans votre compte de stockage :

* Utilisez toosecure de méthodes de contrôle d’accès Azure standard vos journaux en limitant leur accès.
* Supprimer les journaux que vous ne voulez plus tookeep dans votre compte de stockage.

Utilisez ce didacticiel toohelp vous prise en main d’Azure Key Vault journalisation, toocreate votre compte de stockage, activer la journalisation et interpréter les informations de journalisation de hello collectées.  

> [!NOTE]
> Ce didacticiel n’inclut pas les instructions relatives à la toocreate clé archivages, les clés ou les clés secrètes. Pour plus d’informations, consultez [Prise en main d’Azure Key Vault](key-vault-get-started.md). Ou, pour obtenir des instructions de l'interface de ligne de commande interplateforme, consultez [ce didacticiel équivalent](key-vault-manage-with-cli2.md).
>
> Actuellement, vous ne pouvez pas configurer le coffre de clés Azure Bonjour portail Azure. Au lieu de cela, vous devez suivre ces instructions Azure PowerShell.
>
>

Pour plus d’informations générales sur Azure Key Vault, consultez la page [Présentation d’Azure Key Vault](key-vault-whatis.md)

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez avoir hello suivant :

* Un coffre de clés existant que vous utilisez déjà.  
* Azure PowerShell, **version 1.0.1 minimum**. tooinstall Azure PowerShell et associez-le à votre abonnement Azure, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview). Si vous avez déjà installé Azure PowerShell et que vous ne connaissez pas la version de hello, à partir de la console de hello Azure PowerShell, tapez `(Get-Module azure -ListAvailable).Version`.  
* Espace de stockage suffisant sur Azure pour vos journaux de coffre de clés.

## <a id="connect"></a>Se connecter tooyour abonnements
Démarrer une session Azure PowerShell et connectez-vous à tooyour compte Azure avec hello de commande suivante :  

    Login-AzureRmAccount

Dans la fenêtre contextuelle du navigateur de hello, entrez votre nom d’utilisateur de compte Azure et un mot de passe. Azure PowerShell Obtient tous les abonnements hello qui sont associés à ce compte et par défaut, utilise hello premier.

Si vous avez plusieurs abonnements, peut-être toospecify une valeur spécifique qui a été utilisé toocreate votre coffre de clés Azure. Tapez hello suivant toosee les abonnements de hello pour votre compte :

    Get-AzureRmSubscription

Ensuite, toospecify hello abonnement qui est associé à votre coffre de clés que vous se connectent, type :

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> Cette étape est importante et particulièrement utile si plusieurs abonnements sont associés à votre compte. Vous pouvez recevoir une erreur de tooregister Microsoft.Insights si cette étape est ignorée.
>   
>

Pour plus d’informations sur la configuration d’Azure PowerShell, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a id="storage"></a>Création d’un nouveau compte de stockage pour vos journaux
Bien que vous pouvez utiliser un compte de stockage existant pour les journaux, nous allons créer un nouveau compte de stockage qui est des journaux de coffre tooKey dédié. Pour plus de commodité pour nous avons toospecify cela plus tard, nous allons stocker de détails de hello dans une variable nommée **sa**.

Pour une gestion plue facile, nous utilisons également hello le même groupe de ressources comme hello contenant notre coffre de clés. À partir de hello [didacticiel de mise en route](key-vault-get-started.md), ce groupe de ressources nommé **ContosoResourceGroup** et nous continuerons emplacement Asie orientale toouse hello. Remplacez ces valeurs par les vôtres, selon le cas :

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Si vous décidez de toouse un compte de stockage existant, elle doit utiliser hello même abonnement que votre coffre de clés et il doivent utiliser, modèle de déploiement du Gestionnaire de ressources hello, plutôt que de modèle de déploiement classique hello.
>
>

## <a id="identify"></a>Identifier le coffre de clés hello pour les journaux
Dans notre didacticiel de mise en route, le nom de notre coffre de clés a été **ContosoKeyVault**, donc nous allons continuer toouse que nommer et enregistrer des informations sur les hello dans une variable nommée **kv**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Activation de la journalisation
tooenable journalisation pour le coffre de clés, nous utiliserons une applet de commande hello AzureRmDiagnosticSetting de jeu, ainsi que les variables hello créé pour notre coffre de clés et de notre nouveau compte de stockage. Nous mettrons également hello **-activé** indicateur trop**$true** et hello catégorie tooAuditEvent (hello seule catégorie pour la journalisation de coffre de clés), la valeur :

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

sortie Hello pour cela inclut :

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Cela confirme que la journalisation est maintenant activée pour votre coffre de clés, l’enregistrement de compte de stockage tooyour plus d’informations.

Si vous le souhaitez, vous pouvez également définir une stratégie de rétention pour vos journaux, par exemple la suppression automatique des anciens journaux. Par exemple, définissez la stratégie de rétention à l’aide **- RetentionEnabled** indicateur trop**$true** et **- RetentionInDays** paramètre trop**90** donc que les journaux plus de 90 jours seront automatiquement supprimés.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

Éléments consignés :

* toutes les demandes API REST authentifiées sont enregistrées, ce qui inclut des requêtes ayant échoué suite à des demandes, des erreurs système ou des autorisations d’accès incorrectes ;
* Opérations sur la clé de hello coffre lui-même, ce qui inclut la création, de suppression, de stratégies d’accès de coffre de clés de paramètre, et la mise à jour des attributs de coffre de clés telles que des balises.
* Opérations sur les clés et les secrets dans le coffre de clés hello, qui inclut la création, la modification ou la suppression de ces clés ou les clés secrètes ; opérations telles que la connexion, vérifier, chiffrer, déchiffrer, retour à la ligne et désencapsuler les clés, obtenir des clés secrètes, liste des clés et les secrets et leurs versions.
* les requêtes non authentifiées qui génèrent une réponse 401. Par exemple, les requêtes qui ne possèdent pas de jeton de porteur, qui sont incorrectes, qui ont expiré ou qui comportent un jeton non valide.  

## <a id="access"></a>Accéder à vos journaux
Journaux de coffre de clés sont stockés dans hello **insights-journaux-auditevent** conteneur hello compte de stockage fourni. toolist tous les objets BLOB de hello dans ce conteneur, tapez :

Tout d’abord, créez une variable pour le nom du conteneur hello. Il sera utilisé dans l’ensemble de rest hello de procédure pas à pas hello.

    $container = 'insights-logs-auditevent'

toolist tous les objets BLOB de hello dans ce conteneur, tapez :

    Get-AzureStorageBlob -Container $container -Context $sa.Context
sortie de Hello ressemblera toothis quelque chose de similaire :

**URI du conteneur : https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Nom**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Comme vous pouvez le voir à partir de cette sortie, objets BLOB de hello suivre une convention d’affectation de noms : **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**

valeurs de date et d’heure Hello utilisent l’heure UTC.

Hello même compte de stockage pouvant être journaux toocollect utilisé pour plusieurs ressources, hello ID de ressource complet dans le nom d’objet blob hello est très utile tooaccess ou BLOB hello simplement télécharger dont vous avez besoin. Avant cela, nous aborderons tout d’abord comment toodownload tous hello d’objets BLOB.

Commencez par créer un Bonjour de toodownload dossier objets BLOB. Par exemple :

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

Procurez-vous la liste de tous les objets blob :  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Redirigez cette liste via des objets BLOB de 'Get-AzureStorageBlobContent' toodownload hello dans notre dossier de destination :

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

Lorsque vous exécutez cette commande deuxième, hello  **/**  délimiteur dans les noms d’objets blob hello créer une structure de dossier complet sous le dossier de destination hello, et cette structure sera utilisés toodownload et magasin hello les objets BLOB en tant que fichiers.

tooselectively télécharger des objets BLOB, utilisez des caractères génériques. Par exemple :

* Si vous avez plusieurs coffres de clé et que vous souhaitez que les journaux de toodownload pour qu’un coffre de clés, nommé CONTOSOKEYVAULT3 :

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Si vous avez plusieurs groupes de ressources et que vous souhaitez les journaux toodownload pour le groupe de ressources qu’un seul, utilisez `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Si vous souhaitez toodownload tous les journaux hello pour les mois hello de janvier 2016, utilisez `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Vous êtes maintenant prêt toostart examinant Nouveautés Bonjour se connecte. Mais avant de passer à cela, deux plus de paramètres que vous devrez peut-être tooknow Get-AzureRmDiagnosticSetting :

* état de hello tooquery des paramètres de diagnostic pour votre ressource de coffre de clés :`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* journalisation toodisable pour votre ressource de coffre de clés :`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Interpréter vos journaux Key Vault
Les objets blob individuels sont stockés sous forme de texte en tant qu’objet blob JSON. Voici un exemple d’entrée de journal après l’exécution de `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Hello tableau suivant répertorie les descriptions et les noms de champ hello.

| Nom du champ | Description |
| --- | --- |
| time |Date et heure (UTC) |
| resourceId |ID de ressource Azure Resource Manager Pour les journaux de coffre de clés, il s’agit toujours ID de ressource de coffre de clés hello. |
| operationName |Nom de l’opération de hello, comme indiqué dans le tableau suivant de hello. |
| operationVersion |Il s’agit de version d’API REST de hello demandée par le client de hello. |
| category |Pour les journaux de coffre de clés, AuditEvent est hello disponible valeur unique. |
| resultType |Résultat de la demande d’API REST. |
| resultSignature |État HTTP |
| resultDescription |Description supplémentaire sur le résultat de hello, lorsqu’il est disponible. |
| durationMS |Durée tooservice demande l’API REST hello, en millisecondes. Cela n’inclut pas la latence réseau hello, hello que côté client de hello de mesures peut correspond pas à ce stade. |
| callerIpAddress |Adresse IP du client hello qui a effectué la demande de hello. |
| correlationId |Un GUID facultatif qui hello client peut passer toocorrelate des côté service (le coffre de clés), les journaux côté client. |
| identité |Identité du jeton hello qui a été présenté lors de la demande d’API REST hello. Il s’agit généralement d’un « utilisateur », d’« un principal de service » ou d’une combinaison « utilisateur + appId », comme dans le cas d’une demande résultant d’une applet de commande PowerShell Azure. |
| properties |Ce champ contient des informations différentes en fonction de l’opération hello (NomOpération). Dans la plupart des cas, contient des informations sur le client (hello useragent chaîne passée par le client de hello), hello exacte URI de demande d’API REST et le code d’état HTTP. En outre, lorsqu’un objet est retourné à la suite d’une demande (par exemple, KeyCreate ou VaultGet) il contiendra également hello URI de clé (comme « id »), archivage URI ou un URI de Secret. |

Hello **NomOpération** les valeurs de champ sont au format de ObjectVerb. Par exemple :

* Toutes les opérations de coffre de clés ont hello ' coffre`<action>`' mettre en forme, telles que `VaultGet` et `VaultCreate`.
* Toutes les opérations de clé ont hello ' clé`<action>`' mettre en forme, telles que `KeySign` et `KeyList`.
* Toutes les opérations de secret principal ont hello ' Secret`<action>`' mettre en forme, telles que `SecretGet` et `SecretListVersions`.

Hello tableau suivant répertorie les hello NomOpération et la commande API REST.

| operationName | Commande API REST |
| --- | --- |
| Authentification |Via le point de terminaison Azure Active Directory (Azure AD) |
| VaultGet |[Obtention des informations sur un coffre de clés](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Création ou mise à jour d’un coffre de clés](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Suppression d’un coffre de clés](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Mise à jour d’un coffre de clés](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Liste de l’ensemble des coffres de clés dans un groupe de ressources](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Création d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Obtention des informations sur une clé](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Importation d’une clé dans un coffre](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Sauvegarde d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx). |
| KeyDelete |[Suppression d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Restauration d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Signature avec une clé](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Vérification à l’aide d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Encapsulage d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Désencapsulage d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Chiffrement avec une clé](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Déchiffrement avec une clé](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Mise à jour d’une clé](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Liste des clés hello dans un coffre](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Liste des versions d’une clé hello](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Création d’une clé secrète](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Obtention d’une clé secrète](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Mise à jour d’une clé secrète](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Suppression d’une clé secrète](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Liste des clés secrètes d’un coffre](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Liste des versions d’une clé secrète](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Utilisation de Log Analytics

Vous pouvez utiliser la solution de coffre de clés Azure hello dans tooreview Analytique de journal Qu'azure Key Vault AuditEvent se connecte. Pour plus d’informations, y compris comment tooset cette installation, consultez [solution Azure Key Vault dans le journal Analytique](../log-analytics/log-analytics-azure-key-vault.md). Cet article contient également des instructions si vous avez besoin toomigrate de hello ancien coffre de clés solution qui a été proposé en version préliminaire hello Analytique de journal, où vous routé votre tooan journaux compte de stockage Azure et configuré en premier tooread Analytique de journal à partir de là.

## <a id="next"></a>Étapes suivantes
Pour accéder à un didacticiel utilisant Azure Key Vault dans une application web, consultez l’article [Utilisation d’Azure Key Vault à partir d’une application web](key-vault-use-from-web-application.md).

Pour les références de programmation, consultez [hello guide du développeur Azure Key Vault](key-vault-developers-guide.md).

Pour obtenir la liste des applets de commande Azure PowerShell 1.0 pour Azure Key Vault, consultez l’article [Azure Key Vault Cmdlets (Applets de commande Azure Key Vault)](/powershell/module/azurerm.keyvault/#key_vault).

Pour un didacticiel sur la rotation des clés et le journal d’audit avec Azure Key Vault, consultez [comment toosetup le coffre de clés avec tooend de fin de clé de rotation et de l’audit](key-vault-key-rotation-log-monitoring.md).
