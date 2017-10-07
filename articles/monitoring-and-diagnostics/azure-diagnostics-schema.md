---
title: "aaaAzure Diagnostics versions de schéma de configuration de l’extension et l’historique | Documents Microsoft"
description: "Compteurs de performance toocollecting pertinentes dans des Machines virtuelles Azure, jeux de mise à l’échelle de machine virtuelle, l’infrastructure de Service et Services de cloud computing."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Versions et historique des schémas de configuration de l’extension Azure Diagnostics | Microsoft Docs
Cette page d’index versions de schéma d’extension Azure Diagnostics partie intégrante d’hello Microsoft Azure SDK.  

> [!NOTE]
> Hello extension Azure Diagnostics est composant de hello utilisé toocollect les compteurs de performance et d’autres statistiques à partir de :
> - Machines virtuelles Azure 
> - Jeux de mise à l’échelle de machine virtuelle
> - Service Fabric 
> - Services cloud 
> - Groupes de sécurité réseau
> 
> Cette page vous concerne uniquement si vous utilisez l’un de ces services.

Hello extension Azure Diagnostics est utilisé avec d’autres produits de diagnostics de Microsoft, analyse d’Azure, Application Insights et Analytique de journal. Pour plus d’informations, voir [Présentation des outils d’analyse Microsoft](monitoring-overview.md).

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Graphique des versions d’Azure Diagnostics et SDK  

|Version du kit Azure SDK | Version d’extension Azure Diagnostics | Modèle|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |plug-in|  
|2.0 - 2.4         |1.0                            |plug-in|  
|2.5               |1.2                            |extension|  
|2.6               |1.3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1.5                            |"|  
|2,9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 Diagnostics Windows Azure version 1.0 livré dans un modèle de plug-in, c'est-à-dire que, lorsque vous avez installé hello Azure SDK, vous avez obtenu version hello des diagnostics Azure fournis.  

 SDK 2.5 (diagnostics version 1.2), compter des diagnostics Windows Azure est allé tooan modèle d’extension. Hello outils tooutilize nouvelles fonctionnalités ont uniquement disponibles dans les kits de développement Azure plus récente, mais n’importe quel service à l’aide des diagnostics Azure choisit directement à partir d’Azure hello copie plus récente. Par exemple, toute personne qui utilise toujours les SDK 2.5 serait chargement version la plus récente hello indiquée dans le tableau précédent de hello, peu importe s’ils sont de nouvelles fonctionnalités de hello.  

## <a name="schemas-index"></a>Index des schémas  
Les différentes versions d’Azure Diagnostics utilisent des schémas de configuration différents. 

[Schéma de configuration des diagnostics 1.0](azure-diagnostics-schema-1dot0.md)  

[Schéma de configuration des diagnostics 1.2](azure-diagnostics-schema-1dot2.md)  

[Diagnostics 1.3 et schéma de configuration ultérieur](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Historique des versions


### <a name="diagnostics-extension-19"></a>Extension d’Azure Diagnostics 1.9 
Prise en charge de Docker ajoutée.


### <a name="diagnostics-extension-181"></a>Extension d’Azure Diagnostics 1.8.1 
Pouvez de spécifier un jeton SAP au lieu d’une clé de compte de stockage dans la configuration privée de hello. Si un jeton SAP est fourni, la clé de compte de stockage hello est ignorée.


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>Extension d’Azure Diagnostics 1.8 
TooPublicConfig de Type de stockage ajouté. Le type de stockage (StorageType) peut être *Table*, *Blob* ou *TableAndBlob*. *Table* est la valeur par défaut hello.


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>Extension d’Azure Diagnostics 1.7 
Hello ajouté capacité tooroute tooEventHub.

### <a name="diagnostics-extension-15"></a>Extension de diagnostic 1.5
Ajouté hello récepteurs trop d’élément et hello les données de diagnostic capacité toosend[Application Insights](../application-insights/app-insights-cloudservices.md) rend plus facile toodiagnose problèmes sur votre application, ainsi que les au niveau du système et l’infrastructure hello.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>Extension 1.3 d’Azure Diagnostics et du kit Azure SDK 2.6 
Pour les projets de Service Cloud dans Visual Studio, hello modifications suivantes ont été apportée. (Ces modifications s’appliquent également toolater les versions de Windows Azure SDK.)

* émulateur local de Hello prend désormais en charge les diagnostics. Cela signifie que vous pouvez collecter des données de diagnostic et vérifiez que votre application crée hello traces appropriées lorsque vous développez et testez dans Visual Studio. chaîne de connexion de Hello `UseDevelopmentStorage=true` permet la collecte de données de diagnostic lorsque vous exécutez votre projet de service cloud dans Visual Studio à l’aide d’émulateur de stockage Azure hello. Toutes les données de diagnostic sont collectées dans le compte de stockage hello (stockage de développement).
* chaîne de connexion de compte des stockage Hello diagnostics (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) est stocké à nouveau dans le fichier de configuration (.cscfg) de service hello. Compte de stockage de diagnostics hello Azure SDK 2.5 a été spécifié dans le fichier diagnostics.wadcfgx de hello.

Il existe des différences notables entre la chaîne de connexion hello travaillé dans Azure SDK 2.4 et versions antérieures, et comment il fonctionne dans Azure SDK 2.6 et versions ultérieures.

* Dans Azure SDK 2.4 et versions antérieures, chaîne de connexion hello a été utilisé comme un runtime par hello plug-in tooget hello stockage compte des informations de diagnostic pour le transfert des journaux de diagnostic.
* Dans Azure SDK 2.6 et versions ultérieures, la chaîne de connexion de diagnostics de hello est utilisée par l’extension de Visual Studio tooconfigure hello diagnostics avec les informations de compte de stockage approprié hello lors de la publication. chaîne de connexion Hello permet de définir les comptes de stockage différentes pour différentes configurations de service que Visual Studio utilisera lors de la publication. Toutefois, étant donné que le plug-in des diagnostics hello n’est plus disponible (après Azure SDK 2.5), fichier .cscfg de hello par lui-même ne peut pas activer hello Extension des Diagnostics. Vous disposez d’extension de hello tooenable séparément par le biais d’outils tels que Visual Studio ou PowerShell.
* processus de hello toosimplify de configuration de l’extension de diagnostics hello avec PowerShell, sortie hello du package à partir de Visual Studio contient également hello publique XML de configuration pour l’extension diagnostics hello pour chaque rôle. Visual Studio utilise hello diagnostics connexion chaîne toopopulate hello compte de stockage informations présente dans la configuration publique de hello. les fichiers de configuration publics Hello sont créés dans le dossier d’Extensions hello et suivent hello modèle PaaSDiagnostics. <RoleName>. PubConfig.xml. Tout déploiement basé sur PowerShell peut utiliser toomap de ce modèle chaque tooa configuration rôle.
* Hello chaîne de connexion dans le fichier .cscfg de hello est également utilisé par hello les données de diagnostic hello tooaccess portail Azure afin de pouvoir Bonjour **analyse** chaîne de connexion onglet hello est nécessaire tooconfigure hello service tooshow détaillé données d’analyse dans le portail de hello.

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migration des projets tooAzure SDK 2.6 et versions ultérieur
Lors de la migration à partir d’Azure SDK 2.5 tooAzure SDK 2.6 ou version ultérieure, si vous avez un compte de stockage de diagnostics spécifié dans le fichier .wadcfgx de hello, puis il y restera. avantage tootake de flexibilité hello d’utilisation de stockage différents comptes pour diverses configurations de stockage, vous avez toomanually ajouter un projet de tooyour de chaîne de connexion hello. Si vous migrez un projet à partir d’Azure SDK 2.4 ou antérieure tooAzure 2.6 du Kit de développement logiciel, puis hello diagnostics des chaînes de connexion sont conservés. Toutefois, notez les modifications hello dans la façon dont les chaînes de connexion sont traitées dans Azure SDK 2.6 comme spécifié dans la section précédente de hello.

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Comment Visual Studio détermine le compte de stockage de diagnostics hello
* Si une chaîne de connexion de diagnostic est spécifiée dans le fichier .cscfg de hello, Visual Studio utilise extension de diagnostics tooconfigure hello lors de la publication et lors de la génération des fichiers xml de configuration publique hello lors de l’empaquetage.
* Si aucune chaîne de connexion de diagnostic n’est spécifié dans le fichier .cscfg de hello, puis Visual Studio revient compte de stockage toousing hello spécifié dans hello .wadcfgx tooconfigure hello diagnostics extension de fichier lors de la publication et la génération hello public fichiers de xml de configuration lors de la compression.
* chaîne de connexion des diagnostics Hello dans le fichier .cscfg de hello est prioritaire sur le compte de stockage hello dans le fichier .wadcfgx de hello. Si une chaîne de connexion de diagnostic est spécifiée dans le fichier .cscfg de hello, puis Visual Studio qui utilise et ignore le compte de stockage hello dans .wadcfgx.

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Ce qui hello « Mettre à jour les chaînes de connexion de stockage de développement... »  ?
Hello case à cocher pour **mettre à jour les chaînes de connexion de stockage de développement pour les Diagnostics et la mise en cache avec les informations d’identification de compte de stockage Microsoft Azure lors de la publication tooMicrosoft Azure** vous offre un moyen pratique de tooupdate tout chaînes de connexion de compte de stockage de développement avec le compte de stockage Azure hello spécifié lors de la publication.

Par exemple, supposons que vous sélectionnez cette case à cocher et la chaîne de connexion de diagnostic hello spécifie `UseDevelopmentStorage=true`. Lorsque vous publiez hello projet tooAzure, Visual Studio met automatiquement à jour chaîne de connexion des diagnostics hello avec compte de stockage hello que vous avez spécifié dans l’Assistant de publication hello. Toutefois, si un compte de stockage réel a été spécifié comme chaîne de connexion des diagnostics hello, ce compte est utilisé à la place.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Différences entre les fonctionnalités de diagnostics du Kit de développement logiciel (SDK) Azure 2.4 et les versions antérieures et du Kit de développement logiciel (SDK) Azure 2.5 et les versions ultérieures
Si vous mettez à niveau votre projet à partir d’Azure SDK 2.4 tooAzure SDK 2.5 ou version ultérieure, vous devez garder à hello esprit suivant des différences de fonctionnalités de diagnostics.

* **Les API de configuration sont déconseillées** : la configuration par programmation des diagnostics est disponible dans le Kit de développement logiciel (SDK) Azure 2.4 ou les versions antérieures, mais déconseillée dans le Kit de développement logiciel (SDK) Azure 2.5 et les versions ultérieures. Si votre configuration des diagnostics est actuellement définie dans le code, vous devez tooreconfigure ces paramètres à partir de zéro dans le projet migré de hello dans l’ordre pour l’utilisation de diagnostics tookeep. fichier de configuration des diagnostics Hello pour Azure SDK 2.4 est diagnostics.wadcfg et diagnostics.wadcfgx pour Azure SDK 2.5 et versions ultérieures.
* **Diagnostics pour les applications de service cloud peuvent être configurées uniquement au niveau du rôle hello, pas au niveau de l’instance hello.**
* **Chaque fois que vous déployez votre application, la configuration des diagnostics hello est mise à jour** : cela peut entraîner des problèmes de parité si vous modifiez votre configuration des diagnostics à partir de l’Explorateur de serveurs et redéployez votre application.
* **Dans Azure SDK 2.5 et versions ultérieures, les vidages sur incident sont configurés dans le fichier de configuration de diagnostics hello, pas dans le code** – si vous avez des vidages sur incident configurés dans le code, vous aurez une configuration du transfert de hello toomanually toohello configuration fichier de code, Étant donné que les vidages sur incident de hello ne sont pas transférées au cours de la migration de hello tooAzure 2.6 du Kit de développement logiciel.

