---
title: "nœuds de calcul du cluster de HPC Pack aaaManage | Documents Microsoft"
description: "En savoir plus sur PowerShell script outils tooadd, supprimer, démarrer et arrêter les nœuds de calcul de cluster HPC Pack 2012 R2 dans Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Gérer le nombre de hello et de disponibilité de nœuds de calcul dans un cluster HPC Pack dans Azure
Si vous avez créé un cluster HPC Pack 2012 R2 dans des machines virtuelles Azure, vous pourriez façons tooeasily ajouter, supprimer, démarrer (approvisionner) ou arrêter (annuler le déploiement) de certaines machines virtuelles de nœud dans le cluster de calcul. toodo ces tâches, exécuter des scripts PowerShell de Azure qui sont installés sur la machine virtuelle du nœud principal hello. Ces scripts vous permettent de contrôler les nombre hello et la disponibilité de vos ressources de cluster HPC Pack afin de contrôler les coûts.

> [!IMPORTANT] 
> Cet article s’applique uniquement tooHPC Pack 2012 R2 clusters dans Azure créé à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.
> En outre, les scripts PowerShell de hello décrits dans cet article ne sont pas disponibles dans HPC Pack 2016.

## <a name="prerequisites"></a>Composants requis
* **Cluster HPC Pack 2012 R2 dans des machines virtuelles Azure**: créer un cluster HPC Pack 2012 R2 dans le modèle de déploiement classique hello. Par exemple, vous pouvez automatiser le déploiement de hello en utilisant une image de machine virtuelle de HPC Pack 2012 R2 hello Bonjour Azure Marketplace et un script Azure PowerShell. Pour plus d’informations et les conditions préalables requises, consultez [créer un Cluster HPC avec hello script de déploiement IaaS de HPC Pack](hpcpack-cluster-powershell-script.md).
  
    Après le déploiement, recherchez des hello nœud Gestion des scripts dans hello % CCP\_dossier Accueil % bin sur le nœud principal de hello. Exécuter chacun des scripts de hello en tant qu’administrateur.
* **Certificat de gestion ou le fichier de paramètres de publication Azure**: vous devez toodo hello suivantes sur le nœud principal de hello :
  
  * **Fichier de paramètres de publication de hello d’importation Azure**. toodo, hello exécution suivant des applets de commande PowerShell de Azure de nœud principal de hello :
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Configurer le certificat de gestion Azure hello sur le nœud principal de hello**. Si vous disposez de fichier .cer hello, importez-le dans le magasin de certificats CurrentUser\My hello, puis exécutez hello suivant l’applet de commande PowerShell de Azure pour votre environnement Azure (cloud Azure ou AzureChinaCloud) :
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>Ajouter des machines virtuelles à nœud de calcul
Ajouter des nœuds de calcul avec hello **Add-hpciaasnode.ps1** script.

### <a name="syntax"></a>Syntaxe
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>Paramètres
* **ServiceName**: nom du service de cloud hello nouvelles machines virtuelles de nœud de calcul sont ajoutés à.
* **ImageName**: nom d’image de machine virtuelle Azure, qui peut être obtenu via hello portail Azure classic ou l’applet de commande Azure PowerShell **Get-AzureVMImage**. image de Hello doit respecter hello suivant les exigences :
  
  1. Un système d’exploitation Windows doit être installé.
  2. HPC Pack doit être installé dans le rôle de nœud de calcul hello.
  3. image de Hello doit être une image privée dans la catégorie d’utilisateur hello, pas une image de machine virtuelle Azure publique.
* **Quantité**: nombre de toobe de machines virtuelles de nœud de calcul ajouté.
* **InstanceSize**: taille de hello des machines virtuelles de nœud de calcul.
* **DomainUserName**: nom d’utilisateur de domaine, qui est utilisé toojoin hello nouvelles machines virtuelles toohello domaine.
* **DomainUserPassword**: mot de passe d’utilisateur de domaine hello.
* **NodeNameSeries** (facultatif) : modèle de dénomination hello pour les nœuds de calcul. Hello format doit être &lt; *racine\_nom*&gt;&lt;*Démarrer\_nombre*&gt;%. Par exemple, MyCN % 10 % signifie une série de hello calcule les noms des nœuds à partir de MyCN11. Si non spécifié, hello script utilise hello configuré série d’affectation de noms de nœud dans un cluster HPC hello.

### <a name="example"></a>Exemple
Hello exemple suivant ajoute nœud de calcul de grande taille 20 ordinateurs virtuels dans le service cloud hello *hpccnimage1*, en fonction de l’image de machine virtuelle hello *hpcservice1*.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>Supprimer des machines virtuelles à nœud de calcul
Supprimer des nœuds de calcul avec hello **Remove-hpciaasnode.ps1** script.

### <a name="syntax"></a>Syntaxe
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>Paramètres
* **Nom**: noms des toobe des nœuds de cluster est supprimé. Les caractères génériques sont pris en charge. nom de jeu de paramètre Hello est. Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.
* **Nœud**: objet HpcNode hello pour hello nœuds toobe est supprimé, ce qui peut être obtenu via l’applet de commande PowerShell HPC hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nom du jeu de paramètre Hello est un nœud. Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.
* **DeleteVHD** (facultatif) : paramètre toodelete disques hello associé pour hello machines virtuelles qui sont supprimés.
* **Force** (facultatif) : paramètre tooforce nœuds HPC en mode hors connexion avant de les supprimer.
* **Confirmer** (facultatif) : demander confirmation avant d’exécuter la commande hello.
* **WhatIf**: paramètre toodescribe ce qui se passerait si vous avez exécuté la commande hello sans réellement l’exécuter commande hello.

### <a name="example"></a>Exemple
Hello exemple suivant force les nœuds hors connexion hello dont le nom commence *HPCNode-CN -* et les supprime les nœuds hello et les disques associés.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>Démarrer des machines virtuelles à nœud de calcul
Démarrer les nœuds avec hello **Start-hpciaasnode.ps1** script.

### <a name="syntax"></a>Syntaxe
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>Paramètres
* **Nom**: noms des toobe de nœuds de cluster hello a démarré. Les caractères génériques sont pris en charge. nom de jeu de paramètre Hello est. Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.
* **Nœud**-objet HpcNode hello pour toobe de nœuds hello démarré, qui peut être obtenu via l’applet de commande PowerShell HPC hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nom du jeu de paramètre Hello est un nœud. Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.

### <a name="example"></a>Exemple
Hello exemple suivant démarre les nœuds dont le nom commence *HPCNode-CN -*.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>Arrêter des machines virtuelles à nœud de calcul
Arrêter les nœuds de calcul avec hello **Stop-hpciaasnode.ps1** script.

### <a name="syntax"></a>Syntaxe
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>Paramètres
* **Nom**-noms de toobe de nœuds de cluster hello s’est arrêté. Les caractères génériques sont pris en charge. nom de jeu de paramètre Hello est. Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.
* **Nœud**: objet HpcNode hello pour hello nœuds toobe est arrêté, ce qui peut être obtenu via l’applet de commande PowerShell HPC hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nom du jeu de paramètre Hello est un nœud. Vous ne pouvez pas spécifier les deux hello **nom** et **nœud** paramètres.
* **Force** (facultatif) : paramètre tooforce nœuds HPC en mode hors connexion avant de les arrêter.

### <a name="example"></a>Exemple
Hello exemple suivant force les nœuds hors connexion dont le nom commence *HPCNode-CN -* et puis s’arrête hello nœuds.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>Étapes suivantes
* tooautomatically augmenter ou réduire les nœuds du cluster en fonction de la charge de travail actuelle hello des tâches et des tâches sur le cluster de hello hello, consultez [croître automatiquement et de réduire les ressources de cluster HPC Pack hello dans Azure conséquente toohello la charge du cluster](hpcpack-cluster-node-autogrowshrink.md).

