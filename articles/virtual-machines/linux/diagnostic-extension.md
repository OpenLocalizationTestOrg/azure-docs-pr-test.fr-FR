---
title: "Calcul d’aaaAzure - Extension Diagnostics Linux | Documents Microsoft"
description: "Mode tooconfigure hello métriques de toocollect Azure Linux Diagnostic Extension (SCÉNARISTE) et de consigner les événements dans les machines virtuelles Linux s’exécutant dans Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a>Utilisez l’Extension Diagnostics Linux toomonitor métriques et journaux

Ce document décrit la version 3.0 de hello Extension Diagnostics Linux.

> [!IMPORTANT]
> Pour plus d’informations sur la version 2.3 et les versions antérieures, consultez [ce document](./classic/diagnostic-extension-v2.md).

## <a name="introduction"></a>Introduction

Hello Extension Diagnostics Linux permet à une utilisateur Moniteur hello l’intégrité d’un VM Linux en cours d’exécution sur Microsoft Azure. Il a hello suivant de fonctionnalités :

* Collecte les métriques de performances système hello machine virtuelle et les stocke dans une table spécifique dans un compte de stockage désignées.
* Récupère les journaux d’événements syslog et les stocke dans une table spécifique dans hello désigné du compte de stockage.
* Permet aux utilisateurs toocustomize hello les métriques des données qui sont collectées et téléchargées.
* Permet aux utilisateurs toocustomize hello syslog et des niveaux de gravité des événements qui sont collectées et téléchargées.
* Permet aux utilisateurs tooupload journal spécifié fichiers tooa désigné stockage table.
* Prend en charge l’envoi des métriques de journal des événements tooarbitrary EventHub points de terminaison et et les objets BLOB d’au format JSON Bonjour désigné compte de stockage.

Cette extension fonctionne avec les deux modèles de déploiement d’Azure.

## <a name="installing-hello-extension-in-your-vm"></a>Extension de hello lors de l’installation dans votre machine virtuelle

Vous pouvez activer cette extension à l’aide des applets de commande PowerShell Azure hello, scripts CLI d’Azure ou les modèles de déploiement d’Azure. Pour plus d’informations, consultez [Fonctionnalités des extensions](./extensions-features.md).

Hello portail Azure ne peut pas être utilisé tooenable ou configurer SCÉNARISTE 3.0. Au lieu de cela, il installe et configure la version 2.3. Alertes et des graphiques de portail azure fonctionnent avec des données à partir de deux versions d’extension de hello.

Ces instructions d’installation et un [exemple de configuration téléchargeable](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configurent l’extension de diagnostic Linux 3.0 pour :

* capture et magasin hello mêmes métriques comme ont été fournies par SCÉNARISTE 2.3 ;
* capturer un ensemble utile de métriques de système de fichier, nouveau tooLAD 3.0 ;
* capturer la collection de syslog par défaut hello activée par SCÉNARISTE 2.3 ;
* Activer hello expérience du portail Azure pour les graphiques et la génération d’alertes sur des métriques de machine virtuelle.

configuration de téléchargeable Hello est juste un exemple ; Modifiez-le toosuit vos propres besoins.

### <a name="prerequisites"></a>Composants requis

* **Agent Azure Linux version 2.2.0 ou ultérieure**. La plupart des images de la galerie Linux de machines virtuelles Azure incluent la version 2.2.7 ou ultérieure. Exécutez `/usr/sbin/waagent -version` tooconfirm hello version est installée sur la machine virtuelle de hello. Si hello machine virtuelle exécute une ancienne version de l’agent invité de hello, procédez comme [ces instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate il.
* **Interface de ligne de commande Azure**. [Configurer hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environnement sur votre ordinateur.
* Hello wget commande, si vous ne l’avez déjà : exécuter `sudo apt-get install wget`.
* Un abonnement Azure et un stockage existant compte qu’il contient les données de salutation toostore.

### <a name="sample-installation"></a>Exemple d’installation

Renseignez les paramètres corrects de hello sur hello trois premières lignes, puis exécuter ce script en tant que racine :

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

URL de Hello pour la configuration d’exemple hello et son contenu, est toochange de l’objet. Téléchargez une copie du fichier JSON de paramètres de portail hello et personnaliser en fonction de vos besoins. Les modèles ou l’automation que vous construisez doit utiliser votre propre copie au lieu de télécharger cette URL à chaque fois.

### <a name="updating-hello-extension-settings"></a>Mise à jour des paramètres d’extension hello

Une fois que vous avez modifié les paramètres de votre protégé ou Public, déployez-les toohello machine virtuelle en exécutant hello même commande. Si rien modifié dans les paramètres de hello, paramètres de hello mis à jour sont envoyées toohello extension. SCÉNARISTE recharge la configuration de hello et redémarre automatiquement.

### <a name="migration-from-previous-versions-of-hello-extension"></a>Migration à partir de versions précédentes de l’extension de hello

version la plus récente de l’extension de hello Hello est **3.0**. **Les anciennes versions (2.x) sont dépréciées, et leur publication peut cesser le 31 juillet 2018 ou après**.

> [!IMPORTANT]
> Cette extension présente la configuration de toohello de modifications avec rupture d’extension de hello. Une telle modification sécurité de hello tooimprove d’extension de hello ; Par conséquent, descendante compatibilité avec 2.x Échec de la maintenance. En outre, hello Extension de serveur de publication pour cette extension est différent à publisher hello pour les versions 2.x hello.
>
> toomigrate de 2.x toothis nouvelle version de l’extension de hello, vous devez désinstaller ancienne extension de hello (sous l’ancien nom du serveur de publication hello), puis installez la version 3 d’extension de hello.

Recommandations :

* Installez l’extension de hello avec mise à niveau de version mineure automatique activée.
  * Sur le modèle de déploiement classique de machines virtuelles, spécifiez « 3.* » en tant que version de hello si vous installez extension hello via Azure-XPLAT-CLI ou Powershell.
  * Modèle de machines virtuelles sur le déploiement d’Azure Resource Manager, incluez ' « autoUpgradeMinorVersion » : true' dans le modèle de déploiement d’ordinateur virtuel hello.
* Utilisez un compte de stockage nouveau ou différent pour l’extension de diagnostic Linux 3.0. Il existe plusieurs petites incompatibilités entre l’extension de diagnostic Linux 2.3 et l’extension de diagnostic Linux 3.0, qui rendent problématique le partage d’un compte :
  * L’extension de diagnostic Linux 3.0 stocke les événements Syslog dans une table avec un nom différent.
  * chaînes de counterSpecifier de Hello pour `builtin` métriques diffèrent dans SCÉNARISTE 3.0.

## <a name="protected-settings"></a>Paramètres protégés

Cet ensemble d’informations de configuration contient des informations sensibles qui doivent être protégées d’une exposition publique, par exemple les informations d’identification de stockage. Ces paramètres sont transmis tooand stockée par extension hello sous forme chiffrée.

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

Nom | Valeur
---- | -----
storageAccountName | nom Hello hello du compte de stockage dans lequel les données sont écrites par l’extension de hello.
storageAccountEndPoint | point de terminaison (facultatif) hello identification cloud hello dans le hello compte de stockage existe. Si ce paramètre est absent, SCÉNARISTE par défaut toohello cloud public Azure, `https://core.windows.net`. toouse un compte de stockage dans Azure situés en Allemagne, Azure Government ou Azure Chine, définissez cette valeur en conséquence.
storageAccountSasToken | Un [jeton compte SAP](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) pour les services Blob et de Table (`ss='bt'`), toocontainers applicable et les objets (`srt='co'`), qui accorde ajouter, créer, répertorier, mettre à jour et d’autorisations en écriture (`sp='acluw'`). Faire *pas* inclure hello début-point d’interrogation ( ?).
mdsdHttpProxy | (facultatif) HTTP proxy informations nécessaires tooenable hello extension tooconnect toohello spécifié le compte de stockage et de point de terminaison.
sinksConfig | (facultatif) Détails des autres destinations toowhich mesures et les événements peuvent être remis. Hello des détails spécifiques chaque récepteur de données pris en charge par l’extension de hello sont décrites dans les sections hello qui suivent.

Vous pouvez aisément construire le jeton SAS de hello requis via hello portail Azure.

1. Sélectionnez toowhich de compte de stockage à usage général hello souhaité hello extension toowrite
1. Sélectionnez « Signature d’accès partagé » à partir de la partie des paramètres hello du menu de gauche hello
1. Vérifiez les sections appropriées hello comme décrites précédemment
1. Cliquez sur le bouton de « Générer SAS » hello.

![image](./media/diagnostic-extension/make_sas.png)

Hello de copie généré SAS dans le champ de storageAccountSasToken hello ; supprimer hello-interrogation de début (« ? »).

### <a name="sinksconfig"></a>sinksConfig

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

Cette section facultative définit autres destinations extension de hello toowhich envoie des informations de hello qu'il collecte. tableau de « sink » Hello contient un objet pour chaque récepteur de données supplémentaires. Hello attribut « type » détermine hello autres attributs dans l’objet de hello.

Élément | Valeur
------- | -----
name | Chaîne utilisée récepteur de toothis toorefer ailleurs dans la configuration de l’extension hello.
type | type Hello du récepteur en cours de définition. Détermine les hello autres valeurs (le cas échéant) dans les instances de ce type.

La version 3.0 de hello Extension Diagnostics Linux prend en charge deux types de récepteur : EventHub et JsonBlob.

#### <a name="hello-eventhub-sink"></a>récepteur d’EventHub Hello

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

« sasURL » Hello contient hello URL complète, y compris le jeton SAS, pourquoi données toowhich de concentrateur d’événements doit être publiée. SCÉNARISTE requiert une SAP une stratégie qui active la revendication d’envoi hello d’affectation de noms. Exemple :

* Créer un espace de noms Event Hub appelé `contosohub`
* Créer un concentrateur d’événements dans l’espace de noms hello appelé`syslogmsgs`
* Créer une stratégie d’accès partagé sur hello concentrateur d’événements nommé `writer` qu’Active hello revendication d’envoi

Si vous avez créé une SAP de bonne jusqu'à minuit UTC sur 1 janvier 2018, la valeur de sasURL hello peut être :

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

Pour plus d’informations sur la génération de jetons SAS pour les Event Hubs, consultez [cette page web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).

#### <a name="hello-jsonblob-sink"></a>récepteur de JsonBlob Hello

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

Données dirigées tooa JsonBlob récepteur est stocké dans des objets BLOB dans le stockage Azure. Chaque instance de l’extension de diagnostic Linux crée un objet blob toutes les heures pour chaque nom de récepteur. Chaque objet blob contient toujours un tableau JSON syntaxiquement valide de l’objet. Nouvelles entrées sont ajoutées atomiquement toohello tableau. Objets BLOB sont stockés dans un conteneur avec hello même nom comme récepteur de hello. Hello des règles de stockage Azure pour les noms de conteneur d’objets blob s’appliquent à des noms de toohello des récepteurs de JsonBlob : entre 3 et 63 caractères ASCII alphanumériques de minuscules ou des tirets.

## <a name="public-settings"></a>Paramètres publics

Cette structure contient différents blocs de paramètres qui contrôlent les informations hello collectées par l’extension de hello. Chaque paramètre est facultatif. Si vous spécifiez `ladCfg`, vous devez aussi spécifier `StorageAccount`.

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

Élément | Valeur
------- | -----
StorageAccount | nom Hello hello du compte de stockage dans lequel les données sont écrites par l’extension de hello. Doit être hello même nom que celui qu’est spécifiée dans hello [paramètres protégés par](#protected-settings).
mdsdHttpProxy | (facultatif) Identique à celui inclus hello [paramètres protégés par](#protected-settings). valeur de publique Hello est remplacée par valeur privé de hello, si définie. Placer les paramètres de proxy qui contiennent une clé secrète, par exemple un mot de passe, Bonjour [paramètres protégés par](#protected-settings).

les éléments restants Hello sont décrites en détail dans les sections suivantes de hello.

### <a name="ladcfg"></a>ladCfg

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

Cette collecte de données facultatif structure contrôles hello de mesures et les journaux toohello de remise des données de service et tooother Azure métriques récepteurs. Vous devez spécifier `performanceCounters` ou `syslogEvents`, ou les deux. Vous devez spécifier hello `metrics` structure.

Élément | Valeur
------- | -----
eventVolume | (facultatif) Contrôles hello nombre de partitions créées au sein de la table de stockage hello. Doit être `"Large"`, `"Medium"` ou `"Small"`. Si non spécifié, la valeur par défaut de hello est `"Medium"`.
sampleRateInSeconds | intervalle par défaut de hello (facultatif) entre la collection de brute (non agrégée). taux d’échantillonnage Hello plus petit pris en charge est de 15 secondes. Si non spécifié, la valeur par défaut de hello est `15`.

#### <a name="metrics"></a>Mesures

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

Élément | Valeur
------- | -----
resourceId | ID de ressource Azure Resource Manager Hello de hello machine virtuelle ou d’échelle de machines virtuelles hello définie hello toowhich que machine virtuelle appartient. Ce paramètre doit être également spécifiée si n’importe quel récepteur JsonBlob est utilisé dans la configuration de hello.
scheduledTransferPeriod | Hello fréquence à laquelle les métriques d’agrégation toobe calculées et transférées tooAzure métriques, exprimée sous la forme d’un intervalle de temps est un 8601. période de transfert plus petit Hello est de 60 secondes, autrement dit, PT1M. Vous devez spécifier au moins une scheduledTransferPeriod.

Exemples de hello métriques spécifiés dans la section des compteurs de performance hello sont collectées toutes les 15 secondes ou à des taux d’échantillonnage hello explicitement définie pour le compteur de hello. Si plusieurs fréquences scheduledTransferPeriod apparaissent (comme dans l’exemple de hello), chaque agrégation est calculée indépendamment.

#### <a name="performancecounters"></a>performanceCounters

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

Collection de hello des métriques de contrôles de cette section facultative. Exemples brutes sont agrégées pour chaque [scheduledTransferPeriod](#metrics) tooproduce ces valeurs :

* mean
* minimum
* maximum
* dernière valeur collectée
* nombre d’échantillons bruts utilisé agrégat de hello toocompute

Élément | Valeur
------- | -----
sinks | (facultatif) Une liste séparée par des virgules des noms des récepteurs toowhich que SCÉNARISTE envoie les résultats de mesure agrégées. Toutes les mesures agrégées sont publiées tooeach répertorié récepteur. Consultez [sinksConfig](#sinksconfig). Exemple : `"EHsink1, myjsonsink"`.
type | Identifie hello réelle du fournisseur de métrique de hello.
class | Avec « counter », identifie le métrique spécifique de hello au sein de l’espace de noms du fournisseur hello.
counter | Avec « classe », identifie le métrique spécifique de hello au sein de l’espace de noms du fournisseur hello.
counterSpecifier | Identifie les mesures spécifiques de hello au sein de l’espace de noms de métriques de Azure hello.
condition | (facultatif) Applique de sélectionne une instance spécifique de la métrique de hello hello objet toowhich ou sélectionne hello d’agrégation sur toutes les instances de cet objet. Pour plus d’informations, consultez hello [ `builtin` définitions de métrique](#metrics-supported-by-builtin).
sampleRate | EST l’intervalle 8601 qui définit les taux de hello collecte des échantillons brutes pour cette métrique. Si non définie, intervalle de collecte hello a la valeur par valeur hello de [sampleRateInSeconds](#ladcfg). taux d’échantillonnage pris en charge le plus court de Hello est de 15 secondes (PT15S).
unité | Doit être une des chaînes suivantes : « Count », « Bytes », « Seconds », « Percent », « CountPerSecond », « BytesPerSecond », « Millisecond ». Définit l’unité hello pour métrique de hello. Consommateurs de données de hello collectée s’attendre hello collectées toomatch de valeurs de données de cette unité. L’extension de diagnostic Linux ignore ce champ.
displayName | Hello étiquette (dans le langage de hello spécifié par les paramètres régionaux associé de hello) toobe attaché toothis des données dans Azure métriques. L’extension de diagnostic Linux ignore ce champ.

counterSpecifier de Hello est un identificateur arbitraire. Les consommateurs de métriques, telles que hello graphiques portail Azure et alerte de fonctionnalité, utilisent counterSpecifier comme hello « clé » qui identifie une mesure ou une instance d’une métrique. Pour les métriques `builtin`, nous vous recommandons d’utiliser des valeurs pour counterSpecifier qui commencent par `/builtin/`. Si vous collectez une instance spécifique d’une mesure, nous vous recommandons de que vous joignez identificateur hello de valeur de counterSpecifier toohello hello instance. Voici quelques exemples :

* `/builtin/Processor/PercentIdleTime` : Temps d’inactivité moyen pour tous les cœurs
* `/builtin/Disk/FreeSpace(/mnt)`-Espace pour le système de fichiers/mnt hello
* `/builtin/Disk/FreeSpace` : Espace libre moyen pour tous les systèmes de fichiers montés

SCÉNARISTE, ni hello portail Azure attend hello counterSpecifier valeur toomatch n’importe quel modèle. Soyez cohérent dans la façon dont vous construisez les valeurs de counterSpecifier.

Lorsque vous spécifiez `performanceCounters`, SCÉNARISTE écrit toujours table tooa de données dans le stockage Azure. Vous pouvez avoir hello même les données écrites tooJSON BLOB et/ou les concentrateurs d’événements, mais vous ne pouvez pas désactiver le stockage table tooa de données. Toutes les instances de hello extension diagnostic configurée toouse hello compte de stockage de même nom et le point de terminaison ajoutent leur toohello métriques et les journaux même table. Si vous écrivent trop grand nombre de machines virtuelles toohello même partition de table, Azure peut accélérer écrit toothat partition. eventVolume Hello définissant les causes entrées toobe réparties sur 1 (petit), 10 (moyen) ou 100 (grand) différentes partitions. En règle générale, « Moyenne » est suffisante tooensure trafic n’est pas limité. fonctionnalité de métriques de Azure Hello Hello portail Azure utilise des données de hello dans cette graphiques tooproduce de table ou les alertes de tootrigger. nom de la table Hello est la concaténation de hello de ces chaînes :

* `WADMetrics`
* Hello « scheduledTransferPeriod » pour hello agrégées des valeurs stockées dans la table de hello
* `P10DV2S`
* Une date, dans l’écran hello « AAAAMMJJ », ce qui modifie tous les 10 jours

Exemples : `WADMetricsPT1HP10DV2S20170410` et `WADMetricsPT1MP10DV2S20170609`.

#### <a name="syslogevents"></a>syslogEvents

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

Cette section facultative contrôle collection hello de journaux d’événements à partir de syslog. Si la section de hello est omise, les événements syslog ne sont pas capturés du tout.

Hello syslogEventConfiguration comporte une entrée pour chaque fonction syslog dignes d’intérêt. Si minSeverity est « NONE » pour une installation donnée, ou si cette fonctionnalité n’apparaît pas du tout dans l’élément de hello, aucun événement à partir de cette fonctionnalité n’est capturées.

Élément | Valeur
------- | -----
sinks | Une liste séparée par des virgules des noms des récepteurs toowhich de journal des événements sont publiés. Tous les événements de journal correspondant à des restrictions de hello dans syslogEventConfiguration sont publiées tooeach répertorié récepteur. Exemple : « EHforsyslog »
facilityName | Nom de fonction Syslog (comme « LOG\_USER » ou « LOG\_LOCAL0 »). Voir « installation » hello section hello [page de manuel syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) pour la liste complète hello.
minSeverity | Niveau de gravité Syslog (comme « LOG\_ERR » ou « LOG\_INFO »). Consultez la section « niveau » de hello Hello [page de manuel syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) pour la liste complète hello. extension de Hello capture la fonctionnalité de toohello événements envoyés à ou ci-dessus hello spécifié au niveau.

Lorsque vous spécifiez `syslogEvents`, SCÉNARISTE écrit toujours table tooa de données dans le stockage Azure. Vous pouvez avoir hello même les données écrites tooJSON BLOB et/ou les concentrateurs d’événements, mais vous ne pouvez pas désactiver le stockage table tooa de données. Hello partitionnement le comportement de cette table est hello identique à celle décrite pour `performanceCounters`. nom de la table Hello est la concaténation de hello de ces chaînes :

* `LinuxSyslog`
* Une date, dans l’écran hello « AAAAMMJJ », ce qui modifie tous les 10 jours

Exemples : `LinuxSyslog20170410` et `LinuxSyslog20170609`.

### <a name="perfcfg"></a>perfCfg

Cette section facultative contrôle l’exécution des requêtes [OMI](https://github.com/Microsoft/omi) arbitraires.

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

Élément | Valeur
------- | -----
namespace | espace de noms OMI de hello (facultatif) dans le hello requête doit être exécutée. Si non spécifié, valeur par défaut de hello est « racine/scx », implémentée par hello [System Center inter-plateformes fournisseurs](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).
query | Hello OMI requête toobe doit être exécutée.
table | table de stockage Azure hello (facultatif), Bonjour désigné du compte de stockage (voir [paramètres protégés par](#protected-settings)).
frequency | nombre de hello (facultatif) de secondes entre chaque exécution de requête de hello. La valeur par défaut est 300 (5 minutes). La valeur minimale est de 15 secondes.
sinks | (facultatif) Une liste séparée par des virgules des noms des résultats des mesures supplémentaires récepteurs toowhich exemple brut doit être publiée. Aucune agrégation de ces exemples brutes n’est calculée par extension de hello ou par les métriques de Azure.

Vous devez spécifier « table » ou « sinks », ou les deux.

### <a name="filelogs"></a>fileLogs

Hello de contrôles capturer des fichiers journaux. SCÉNARISTE capture les nouvelles lignes de texte qu’ils sont écrits toohello fichier et écrit les lignes tootable et/ou les récepteurs spécifiés (JsonBlob ou EventHub).

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

Élément | Valeur
------- | -----
file | chemin d’accès complet Hello de toobe de fichier journal hello observé et capturées. chemin d’accès Hello doit désigner un fichier unique ; Il ne peut pas nommer un répertoire ou contenir des caractères génériques.
table | table de stockage Azure hello (facultatif), dans le stockage hello désigné (comme spécifié dans la configuration de hello protégé), dans les nouvelles lignes du compte hello « fin » du fichier de hello est écrits.
sinks | (facultatif) Une liste séparée par des virgules de noms de lignes de journal supplémentaires récepteurs toowhich envoyé.

Vous devez spécifier « table » ou « sinks », ou les deux.

## <a name="metrics-supported-by-hello-builtin-provider"></a>Mesures prises en charge par le fournisseur de builtin hello

fournisseur de métrique builtin Hello est une source de métriques plus intéressantes tooa large ensemble d’utilisateurs. Ces métriques se répartissent en cinq classes principales :

* Processeur
* Mémoire
* Réseau
* Filesystem
* Disque

### <a name="builtin-metrics-for-hello-processor-class"></a>métriques de Builtin pour hello classe du processeur

Hello classe du processeur de métriques fournit des informations sur l’utilisation du processeur Bonjour machine virtuelle. Lors de l’agrégation des pourcentages, hello résulte moyenne de hello toutes les unités centrales. Dans une machine virtuelle avec deux cœurs, si un seul cœur était occupé à 100 % et hello autres 100 % inactif, hello signalé que percentidletime serait 50. Si chaque noyau a 50 % de disponibilité pour hello même période, hello signalé le résultat est également 50. Quatre principaux de machine virtuelle, avec un seul cœur 100 % occupé et hello autres inactif, hello signalé que percentidletime serait 75.

counter | Signification
------- | -------
PercentIdleTime | Pourcentage de temps au cours de la fenêtre d’agrégation hello que processeurs sont exécutaient boucle inactive du noyau hello
percentProcessorTime | Pourcentage de temps passé à exécuter un thread actif
PercentIOWaitTime | Pourcentage de temps d’attente des toocomplete des opérations d’e/s
PercentInterruptTime | Pourcentage de temps passé à exécuter des interruptions matérielles/logicielles et des appels DPC (appels de procédure différés)
PercentUserTime | De temps au cours de la fenêtre d’agrégation hello, pourcentage de hello de temps passé dans utilisateur plus au niveau de priorité normale
PercentNiceTime | De temps, hello le pourcentage de temps passé à basse priorité (nice)
PercentPrivilegedTime | De temps, hello le pourcentage de temps passé en mode privilégié (noyau)

Hello tout d’abord quatre compteurs doivent additionner too100 %. Hello dernière trois compteurs également somme too100 % ; ils subdivisent somme hello PercentProcessorTime PercentIOWaitTime et PercentInterruptTime.

tooobtain une seule mesure agrégée sur tous les processeurs, définissez `"condition": "IsAggregate=TRUE"`. tooobtain une métrique pour un processeur spécifique, telles que le deuxième processeur logique hello de quatre principaux de machine virtuelle, définissez `"condition": "Name=\\"1\\""`. Numéros des processeurs logiques sont dans la plage de hello `[0..n-1]`.

### <a name="builtin-metrics-for-hello-memory-class"></a>métriques de Builtin pour hello classe de mémoire

Hello classe de mémoire de métriques fournit des informations sur l’utilisation de mémoire, la pagination et le remplacement.

counter | Signification
------- | -------
AvailableMemory | Mémoire physique disponible en Mio
PercentAvailableMemory | Mémoire physique disponible sous forme de pourcentage de la mémoire totale
UsedMemory | Mémoire physique utilisée (Mio)
PercentUsedMemory | Mémoire physique utilisée sous forme de pourcentage de la mémoire totale
PagesPerSec | Pagination totale (lecture/écriture)
PagesReadPerSec | Pages lues dans le magasin de stockage (fichier d’échange, fichier programme, fichier mappé, etc.)
PagesWrittenPerSec | Stocker les pages écrites toobacking (fichier d’échange, fichier mappé, etc.).
AvailableSwap | Espace d’échange non utilisé (Mio)
PercentAvailableSwap | Espace d’échange non utilisé sous forme de pourcentage de l’espace d’échange total
UsedSwap | Espace d’échange utilisé (Mio)
PercentUsedSwap | Espace d’échange utilisé sous forme de pourcentage de l’espace d’échange total

Cette classe de métriques n’a qu’une seule instance. attribut de « condition » Hello possède pas de paramètres utiles et doit être omis.

### <a name="builtin-metrics-for-hello-network-class"></a>métriques de Builtin pour hello classe du réseau

Hello classe réseau de métriques fournit des informations sur l’activité du réseau sur une interface réseau depuis le démarrage. L’extension de diagnostic Linux n’expose pas de métriques de la bande passante, qui peuvent être récupérées à partir des métriques de l’hôte.

compteur | Signification
------- | -------
BytesTransmitted | Nombre total d’octets envoyés depuis le démarrage
Octets reçus | Nombre total d’octets reçus depuis le démarrage
BytesTotal | Nombre total d’octets envoyés ou reçus depuis le démarrage
PacketsTransmitted | Nombre total de paquets envoyés depuis le démarrage
PacketsReceived | Nombre total de paquets reçus depuis le démarrage
TotalRxErrors | Nombre d’erreurs de réception depuis le démarrage
TotalTxErrors | Nombre d’erreurs de transmission depuis le démarrage
TotalCollisions | Nombre de collisions signalées par des ports réseau hello depuis le démarrage

 Bien que cette classe soit instanciée, l’extension de diagnostic Linux ne prend pas en charge la capture de métriques réseau agrégées pour tous les périphériques réseau. définir des métriques de hello tooobtain pour une interface spécifique, tel qu’eth0, `"condition": "InstanceID=\\"eth0\\""`.

### <a name="builtin-metrics-for-hello-filesystem-class"></a>métriques de Builtin pour hello classe du système de fichiers

Hello classe de système de fichiers de métriques fournit des informations sur l’utilisation du système de fichiers. Valeurs absolues et le pourcentage sont signalés comme utilisateur ordinaire de tooan affichées (pas de racine).

counter | Signification
------- | -------
FreeSpace | Espace disque disponible en octets
UsedSpace | Espace disque utilisé en octets
PercentFreeSpace | Pourcentage d’espace libre
PercentUsedSpace | Pourcentage d’espace utilisé
PercentFreeInodes | Pourcentage d’inodes non utilisés
PercentUsedInodes | Pourcentage total d’inodes alloués (utilisés) pour tous les systèmes de fichiers
BytesReadPerSecond | Octets lus par seconde
BytesWrittenPerSecond | Octets écrits par seconde
BytesPerSecond | Octets lus ou écrits par seconde
ReadsPerSecond | Opérations de lecture par seconde
WritesPerSecond | Opérations d’écriture par seconde
TransfersPerSecond | Opérations de lecture ou d’écriture par seconde

Les valeurs agrégées pour tous les systèmes de fichiers peuvent être obtenues en définissant `"condition": "IsAggregate=True"`. Les valeurs pour un système de fichiers monté spécifique, comme « / mnt », peuvent être obtenues en définissant `"condition": 'Name="/mnt"'`.

### <a name="builtin-metrics-for-hello-disk-class"></a>métriques de Builtin pour hello classe disque

Hello classe disque de métriques fournit des informations sur l’utilisation du disque. Ces statistiques s’appliquent toohello intégralité du lecteur. S’il existe plusieurs systèmes de fichiers sur un appareil, compteurs hello pour cet appareil sont en réalité, agrégés sur tous les.

counter | Signification
------- | -------
ReadsPerSecond | Opérations de lecture par seconde
WritesPerSecond | Opérations d’écriture par seconde
TransfersPerSecond | Nombre total d’opérations par seconde
AverageReadTime | Nombre moyen de secondes par opération de lecture
AverageWriteTime | Nombre moyen de secondes par opération d’écriture
AverageTransferTime | Nombre moyen de secondes par opération
AverageDiskQueueLength | Nombre moyen d’opérations disque en file d’attente
ReadBytesPerSecond | Nombre d’octets lus par seconde
WriteBytesPerSecond | Nombre d’octets écrits par seconde
Octets par seconde | Nombre d’octets lus ou écrits par seconde

Les valeurs agrégées pour tous les disques peuvent être obtenues en définissant `"condition": "IsAggregate=True"`. jeu d’informations tooget pour un périphérique spécifique (par exemple, / dev/sdf1), `"condition": "Name=\\"/dev/sdf1\\""`.

## <a name="installing-and-configuring-lad-30-via-cli"></a>Installation et configuration de l’extension de diagnostic Linux 3.0 via CLI

En supposant que vos paramètres protégés sont dans le fichier de hello PrivateConfig.json et vos informations de configuration publique est PublicConfig.json, exécutez la commande suivante :

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

commande Hello suppose que vous utilisez le mode de gestion des ressources Azure hello (arm) de hello CLI d’Azure. tooconfigure SCÉNARISTE pour le déploiement classique (ASM) VMs du modèle, trop de basculer le mode « asm » (`azure config mode asm`) et omettre le nom de groupe de ressources hello dans la commande hello. Pour plus d’informations, consultez hello [documentation relative à CLI inter-plateformes](https://docs.microsoft.com/azure/xplat-cli-connect).

## <a name="an-example-lad-30-configuration"></a>Exemple de configuration de l’extension de diagnostic Linux 3.0

En fonction de hello précédant définitions, ici un exemple de configuration d’extension SCÉNARISTE 3.0 avec une explication. tooapply cet exemple tooyour de cas, vous devez utiliser votre propre nom de compte de stockage, le compte jeton SAS et des jetons EventHubs SAS.

### <a name="privateconfigjson"></a>PrivateConfig.json

Ces paramètres privés configurent :

* un compte de stockage
* un jeton SAS de compte correspondant
* plusieurs récepteurs (JsonBlob ou EventHubs avec des jetons SAS)

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a>PublicConfig.json

Ces paramètres publics font que l’extension de diagnostic Linux :

* Télécharger les métriques pourcentage de temps de processeur et l’espace disque utilisé toohello `WADMetrics*` table
* Télécharger les messages syslog fonctionnalité « utilisateur » et la gravité « info » toohello `LinuxSyslog*` table
* Télécharger brutes OMI requête résultats (PercentProcessorTime et PercentIdleTime) toohello nommé `LinuxCPU` table
* Télécharger les lignes ajoutées dans le fichier `/var/log/myladtestlog` toohello `MyLadTestLog` table

Dans chaque cas, les données sont également chargées dans :

* Stockage d’objets Blob Azure (nom du conteneur est tel que défini dans le récepteur de JsonBlob hello)
* Point de terminaison EventHubs (comme spécifié dans le récepteur de EventHubs hello)

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

Hello `resourceId` hello configuration doit correspondre aux que de l’échelle de machines virtuelles de machine virtuelle ou hello hello définie.

* Métriques de plateforme Azure graphiques et d’alerte sait resourceId hello Hello ordinateur virtuel sur lequel vous travaillez. Il attend des données de hello toofind pour votre machine virtuelle à l’aide de la clé de recherche hello resourceId hello.
* Si vous utilisez Azure mise à l’échelle, resourceId hello dans la configuration de mise à l’échelle hello doit correspondre à resourceId hello utilisé par SCÉNARISTE.
* Hello resourceId est intégrée à des noms de hello de JsonBlobs écrits par SCÉNARISTE.

## <a name="view-your-data"></a>Affichage de vos données

Utiliser des données de performances hello tooview portail Azure, ou définir des alertes :

![image](./media/diagnostic-extension/graph_metrics.png)

Hello `performanceCounters` données sont toujours stockées dans une table de stockage Azure. Les API Stockage Azure sont disponibles pour de nombreux langages et de nombreuses plateformes.

Données envoyées tooJsonBlob récepteurs sont stockées dans des objets BLOB dans le compte de stockage hello nommé Bonjour [paramètres protégés par](#protected-settings). Vous pouvez utiliser les données d’objet blob hello à l’aide des API de stockage Blob Azure.

En outre, vous pouvez utiliser ces données de l’interface utilisateur outils tooaccess hello dans le stockage Azure :

* Explorateur de serveurs Visual Studio.
* [Explorateur de stockage Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Explorateur de stockage Azure").

Cet instantané d’une session de Microsoft Azure Storage Explorer affiche hello généré des tables de stockage Azure et les conteneurs à partir d’une extension SCÉNARISTE 3.0 correctement configurée sur une machine virtuelle de test. image de Hello ne correspond pas exactement à hello [exemple de configuration SCÉNARISTE 3.0](#an-example-lad-30-configuration).

![image](./media/diagnostic-extension/stg_explorer.png)

Consultez hello pertinentes [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn comment tooconsume messages publiés tooan EventHubs point de terminaison.

## <a name="next-steps"></a>Étapes suivantes

* Créer des alertes de métriques dans [moniteur Azure](../../monitoring-and-diagnostics/insights-alerts-portal.md) pour vous collectez les mesures de hello.
* Créez [des graphiques de surveillance](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) pour vos métriques.
* Découvrez comment trop[créer un ensemble d’échelle de machine virtuelle](/azure/virtual-machines/linux/tutorial-create-vmss) à l’aide de votre échelle toocontrol de métriques.
