---
title: aaaManage des comptes Azure Media Services avec PowerShell
description: "Découvrez comment les comptes toomanage Azure Media Services avec les applets de commande PowerShell."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>Gérer des comptes Azure Media Services avec PowerShell
> [!div class="op_single_selector"]
> * [Portail](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocreate en mesure de toobe un compte Azure Media Services, vous devez disposer d’un compte Azure. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Version d'évaluation gratuite d'Azure</a>.
> 
> 

## <a name="overview"></a>Vue d'ensemble
Cet article répertorie des applets de commande PowerShell Azure hello pour Azure Media Services (AMS) dans le cadre d’Azure Resource Manager hello. applets de commande Hello existent Bonjour **Microsoft.Azure.Commands.Media** espace de noms.

## <a name="versions"></a>Versions
**ApiVersion** :   "2015-10-01"

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
Créez un service multimédia.

### <a name="syntax"></a>Syntaxe
Jeu de paramètres : StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

Jeu de paramètres : StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>parameters
**-ResourceGroupName &lt;String&gt;**

Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |0 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-AccountName &lt;String&gt;**

Spécifie le nom hello du service de support hello.

| Alias | Nom |
| --- | --- |
| Requis ? |true |
| Position ? |1 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

**-Location &lt;String&gt;**

Spécifie l’emplacement de la ressource du service de support hello hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |2 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-StorageAccountId &lt;String&gt;**

Spécifie un compte de stockage principal associé au service de support hello.

* Nouveau compte de stockage (créée avec hello API Resource Manager) pris en charge uniquement.
* Hello compte de stockage doit exister et a hello même emplacement avec le service de support hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |3 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Nom du jeu de paramètres |StorageAccountIdParamSet |
| Accepter les caractères génériques ? |false |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Spécifie les comptes de stockage associé au service de support hello.

* Nouveau compte de stockage (créée avec hello API Resource Manager) pris en charge uniquement.
* Hello compte de stockage doit exister et a hello même emplacement avec le service de support hello.
* Un seul compte de stockage peut être spécifié comme compte principal.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |3 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Nom du jeu de paramètres |StorageAccountsParamSet |
| Accepter les caractères génériques ? |false |

**-Tags &lt;Hashtable&gt;**

Spécifie une table de hachage de balises hello qui sont associés au service de support hello.

* Exemple : @{« balise1 « = » value1 » ; » balise2 » = : value2 »}

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position ? |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

**&lt;CommandParameters&gt;**

Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.

### <a name="inputs"></a>Entrées
type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.

### <a name="outputs"></a>outputs
type de sortie Hello est de type hello d’objets hello hello applet de commande émet.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Met à jour un service multimédia.

### <a name="syntax"></a>Syntaxe
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>parameters
**-ResourceGroupName &lt;String&gt;**

Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |0 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-AccountName &lt;String&gt;**

Spécifie le nom hello du service de support hello.

| Alias | Nom |
| --- | --- |
| Requis ? |true |
| Position ? |1 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Spécifie les comptes de stockage associé au service de support hello.

* Nouveau compte de stockage (créée avec hello API Resource Manager) pris en charge uniquement.
* Hello compte de stockage doit exister et a hello même emplacement avec le service de support hello.
* Un seul compte de stockage peut être spécifié comme compte principal.

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position ? |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Nom du jeu de paramètres |StorageAccountsParamSet |
| Accepter les caractères génériques ? |false |

**-Tags &lt;Hashtable&gt;**

Spécifie une table de hachage de balises hello qui sont associés à ce service de support.

* balises Hello qui sont associés au service de support hello sont remplacés par la valeur spécifiée par le client de hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |false |
| Position ? |named |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**&lt;CommandParameters&gt;**

Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.

### <a name="inputs"></a>Entrées
type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.

### <a name="outputs"></a>outputs
type de sortie Hello est de type hello d’objets hello hello applet de commande émet.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Supprime un service multimédia.

### <a name="syntax"></a>Syntaxe
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>parameters
**-ResourceGroupName &lt;String&gt;**

Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |0 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-AccountName &lt;String&gt;**

Spécifie le nom hello du service de support hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |2 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |False |

**&lt;CommandParameters&gt;**

Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.

### <a name="inputs"></a>Entrées
type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.

### <a name="outputs"></a>outputs
type de sortie Hello est de type hello d’objets hello hello applet de commande émet.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Obtient tous les services multimédia d'un groupe de ressources ou un service multimédia avec un nom donné.

### <a name="syntax"></a>Syntaxe
Jeu de paramètres : ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

Jeu de paramètres : AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>parameters
**-ResourceGroupName &lt;String&gt;**

Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |0 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Nom du jeu de paramètres |ResourceGroupParameterSet, AccountNameParameterSet |

Accepter les caractères génériques ?   false

**-AccountName &lt;String&gt;**

Spécifie le nom hello du service de support hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |1 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Nom du jeu de paramètres |AccountNameParameterSet |
| Accepter les caractères génériques ? |false |

**&lt;CommandParameters&gt;**

Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.

### <a name="inputs"></a>Entrées
type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.

### <a name="outputs"></a>outputs
type de sortie Hello est de type hello d’objets hello hello applet de commande émet.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Obtient les clés d’un service multimédia.

### <a name="syntax"></a>Syntaxe
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>parameters
**-ResourceGroupName &lt;String&gt;**

Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |0 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-AccountName &lt;String&gt;**

Spécifie le nom hello du service de support hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |1 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**&lt;CommandParameters&gt;**

Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.

### <a name="inputs"></a>Entrées
type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.

### <a name="outputs"></a>outputs
type de sortie Hello est de type hello d’objets hello hello applet de commande émet.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Régénère une clé primaire ou secondaire d’un service multimédia.

### <a name="syntax"></a>Syntaxe
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>parameters
**-ResourceGroupName &lt;String&gt;**

Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |0 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-AccountName &lt;String&gt;**

Spécifie le nom hello du service de support hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |1 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-KeyType &lt;KeyType&gt;**

Spécifie le type de clé hello du service de support hello.

* Principal ou secondaire

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |2 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |false |
| Accepter les caractères génériques ? |false |

**&lt;CommandParameters&gt;**

Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.

### <a name="inputs"></a>Entrées
type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toothe applet de commande.

### <a name="outputs"></a>outputs
type de sortie Hello est de type hello d’objets hello hello applet de commande émet.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Synchronise les clés de compte de stockage pour un compte de stockage associé au service de support hello.

### <a name="syntax"></a>Syntaxe
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>parameters
**-ResourceGroupName &lt;String&gt;**

Spécifie le nom hello de toowhich de groupe de ressources hello qu'auquel appartient ce service de support.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |0 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-AccountName &lt;String&gt;**

Spécifie le nom hello du service de support hello.

| Alias | (aucun) |
| --- | --- |
| Requis ? |true |
| Position ? |1 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**-StorageAccountId &lt;String&gt;**

Spécifie le compte de stockage hello associé au service de support hello.

| Alias | ID |
| --- | --- |
| Requis ? |true |
| Position ? |2 |
| Valeur par défaut |(aucun) |
| Accepter l'entrée de pipeline ? |True(ByPropertyName) |
| Accepter les caractères génériques ? |false |

**&lt;CommandParameters&gt;**

Cette applet de commande prend en charge les paramètres communs de hello :-Debug, - ErrorAction, - ErrorVariable, - InformationAction, - InformationVariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction et - WarningVariable.

### <a name="inputs"></a>Entrées
type d’entrée de Hello est de type hello Hello objets que vous pouvez diriger toohello applet de commande.

### <a name="outputs"></a>outputs
type de sortie Hello est de type hello d’objets hello hello applet de commande émet.

## <a name="next-step"></a>Étape suivante
Consultez les chemins d’apprentissage de Media Services.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

