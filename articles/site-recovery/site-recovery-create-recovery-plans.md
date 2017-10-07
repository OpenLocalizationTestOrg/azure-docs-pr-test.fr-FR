---
title: "les plans de récupération aaaCreate pour le basculement et récupération dans Azure Site Recovery | Documents Microsoft"
description: "Décrit comment toocreate et personnaliser des plans de récupération d’Azure Site Recovery, toofail sur et récupérer des machines virtuelles et des serveurs physiques"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 72408c62-fcb6-4ee2-8ff5-cab1218773f2
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 09ca7719e92460b283947fdbe752e8654e5b9cab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-recovery-plans"></a>Créer des plans de récupération


Cet article fournit des informations sur la création et la personnalisation des plans de récupération dans [Azure Site Recovery](site-recovery-overview.md).

Valider des commentaires ou des questions au bas de hello de cet article, ou sur hello [Forum sur Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

 Créez hello de toodo de plans de récupération suivant :

* Ils définissent les groupes de machines qui basculent ensemble, puis démarrent ensemble.
* Ils modélisent les dépendances entre les machines, en les rassemblant au sein d’un groupe de plan de récupération. Par exemple, toofail sur et porter une application spécifique, vous regroupez tous les ordinateurs virtuels de hello pour cette application dans hello même groupe de plan de récupération.
* Exécuter un basculement. Vous pouvez exécuter un basculement test, planifié ou non planifié sur un plan de récupération.


## <a name="create-a-recovery-plan"></a>Créer un plan de récupération

1. Cliquez sur l’onglet **Plans de récupération** > **Créer un plan de récupération**.
   Spécifiez un nom pour le plan de récupération hello et d’une source et cible. emplacement de source de Hello doit avoir des machines virtuelles qui sont activés pour le basculement et la récupération.

    - Pour la réplication tooVMM VMM, sélectionnez **Type de Source de** > **VMM**et hello serveurs VMM cible et source. Cliquez sur **Hyper-V** toosee clouds protégés.
    - Pour VMM tooAzure, sélectionnez **Type de Source de** > **VMM**.  Serveur VMM source à hello SELECT, et **Azure** comme cible de hello.
    - Pour tooAzure de réplication Hyper-V (sans VMM), sélectionnez **Type de Source de** > **site Hyper-V**. Site hello sélectionnez en tant que source de hello, et **Azure** comme cible de hello.
    - Pour un VM VMware ou physique locale tooAzure de serveur, sélectionnez un serveur de configuration en tant que source de hello, et **Azure** comme cible de hello.
    - Pour un plan de récupération Azure tooAzure, sélectionnez une région Azure en tant que source de hello et une région Azure secondaire comme cible de hello. les régions Azure secondaire Hello sont qu'uniquement les machines virtuelles de toowhich sont protégés.
2. Dans **sélectionner des machines virtuelles**, sélectionnez les ordinateurs virtuels de hello (ou groupe de réplication) que vous souhaitez groupe par défaut de toohello tooadd (groupe 1) dans le plan de récupération hello.

## <a name="customize-and-extend-recovery-plans"></a>Personnaliser et étendre les plans de récupération

Vous pouvez personnaliser et étendre les plans de récupération :

- **Ajouter de nouveaux groupes**, ajoutez le groupe par défaut toohello récupération supplémentaires plan groupes (haut tooseven) et ajoutez plusieurs ordinateurs ou la réplication des groupes de toothose des groupes de plan de récupération. Les groupes sont numérotées dans l’ordre de hello dans lequel vous les ajoutez. Vous ne pouvez inclure une machine virtuelle ou un groupe de réplication qu’au sein d’un seul plan de récupération.
- **Ajouter une action manuelle**: il est possible d’ajouter des actions manuelles qui s’exécutent avant ou après un groupe de plan de récupération. Lorsque le plan de récupération hello s’exécute, il s’arrête au point hello à laquelle vous avez inséré une action manuelle hello. Une boîte de dialogue vous invite toospecify qu’une action manuelle hello a été exécutée.
- **Ajouter un script** : vous pouvez ajouter des scripts qui s’exécutent avant ou après un groupe de plan de récupération. Lorsque vous ajoutez un script, il ajoute un nouvel ensemble d’actions pour le groupe de hello. Par exemple, un ensemble d’étapes préliminaires pour le groupe 1 sera être créé avec le nom de hello : groupe 1 : étapes préliminaires. L’ensemble des étapes préliminaires seront répertoriées dans cet ensemble. Vous pouvez uniquement ajouter un script sur le site principal de hello si vous avez un serveur VMM déployé.
- **Ajouter des runbooks Azure** : vous pouvez étendre des plans de récupération avec des runbooks Azure. Par exemple, les tâches de tooautomate ou de toocreate seule étape récupération. [En savoir plus](site-recovery-runbook-automation.md).

## <a name="add-scripts"></a>Ajouter des scripts

Vous pouvez utiliser des scripts PowerShell dans vos plans de récupération.

 - Assurez-vous que les scripts utilisent des blocs try-catch afin que les exceptions hello soient gérées normalement.
    - S’il existe une exception dans le script de hello, il arrête l’exécution et tâche hello affiche comme ayant échoué.
    - Si une erreur se produit, toute partie restante du script de hello ne s’exécute pas.
    - Si une erreur se produit lorsque vous exécutez un basculement non planifié, plan de récupération hello continue.
    - Si une erreur se produit lorsque vous exécutez un basculement planifié, le plan de récupération hello s’arrête. Vous devez toofix hello script, vérifiez qu’il s’exécute comme prévu et puis exécutez à nouveau plan de récupération d’hello.
- Hello les commande Write-Host ne fonctionne pas dans un script de plan de récupération et hello script échoue. toocreate de sortie, créez un script de proxy qui exécute ensuite votre script principal. Assurez-vous que toutes les sorties sont obtenues à l’aide de hello >> commande.
  * script de Hello expire si elle ne renvoie pas dans les 600 secondes.
  * Si rien n’est écrit tooSTDERR, le script de hello est classé comme ayant échoué. Ces informations s’affichent dans les détails de l’exécution du script hello.

Si vous utilisez VMM dans votre déploiement :

* Dans un plan de récupération, les scripts exécutés dans le contexte hello Hello compte de Service VMM. Assurez-vous que ce compte dispose des autorisations en lecture sur le partage distant de hello sur quel hello script se trouve. Test toorun de script hello en hello niveau de privilège de compte de service VMM.
* Les applets de commande VMM sont fournies dans un module Windows PowerShell. module de Hello est installé lorsque vous installez la console VMM hello. Il peut être chargé dans votre script, à l’aide de hello commande dans le script de hello suivante :
   - Import-Module -Name virtualmachinemanager. [Plus d’informations](https://technet.microsoft.com/library/hh875013.aspx)
* Vérifiez que vous disposez d’au moins un serveur de bibliothèque au sein de votre déploiement VMM. Par défaut, chemin d’accès du partage de bibliothèque hello pour un serveur VMM se trouve localement sur le serveur VMM, avec le nom du dossier hello MSCVMMLibrary de hello.
    * Si votre chemin d’accès du partage de bibliothèque est distant (ou local, mais pas partagé avec MSCVMMLibrary), configurez le partage de hello comme suit (à l’aide de \\libserver2.contoso.com\share\ par exemple) :
      * Ouvrez hello Éditeur du Registre et accédez trop**HKEY_LOCAL_MACHINE\SOFTWARE\MICROSOFT\Azure Site Recovery\Registration**.
      * Modifier la valeur de hello **ScriptLibraryPath** et le placer en tant que \\libserver2.contoso.com\share\. Spécifiez hello de domaine complet. Fournir des autorisations toohello l’emplacement du partage.
      * Veillez à tester le script hello avec un compte d’utilisateur qui a hello même compte de service les autorisations hello VMM. Cette procédure vérifie qu’autonome s’exécutent dans les scripts testés hello même façon que qu’ils seront dans les plans de récupération. Sur le serveur VMM de hello, définissez toobypass de stratégie d’exécution hello comme suit :
        * Ouvrez la console Windows PowerShell de hello 64 bits avec des privilèges élevés.
        * Entrez : **Set-executionpolicy bypass**. [En savoir plus](https://technet.microsoft.com/library/ee176961.aspx).

## <a name="add-a-script-or-manual-action-tooa-plan"></a>Ajouter un script ou un plan d’action manuelle tooa

Vous pouvez ajouter un groupe de plan de récupération script toohello par défaut une fois que vous avez ajouté des machines virtuelles ou tooit des groupes de réplication et le plan hello créé.

1. Plan de récupération hello ouvert.
2. Cliquez sur un élément Bonjour **étape** liste, puis cliquez sur **Script** ou **Action manuelle**.
3. Spécifiez si le script de toowant tooadd hello ou action avant ou après hello sélectionné élément. Hello d’utilisation **monter** et **Descendre** des boutons, position de hello toomove du script de hello vers le haut ou vers le bas.
4. Si vous ajoutez un script VMM, sélectionnez **basculement tooVMM script**. Dans **chemin d’accès du Script**, partage toohello de type hello chemin d’accès relatif. Dans l’exemple VMM hello ci-dessous, vous spécifiez le chemin d’accès hello : **\RPScripts\RPScript.PS1**.
5. Si vous ajoutez une automatisation Azure exécuter livre, spécifiez compte Azure Automation de hello dans le hello runbook est script de runbook Azure approprié hello trouve, puis sélectionnez.
6. Effectuez un basculement d’un plan de récupération hello, toomake que hello script fonctionne comme prévu.


### <a name="add-a-vmm-script"></a>Ajouter un script VMM

Si vous avez un site source VMM, vous pouvez créer un script sur le serveur VMM de hello et inclure dans votre plan de récupération.

1. Créer un nouveau dossier dans le partage de bibliothèque hello. Par exemple, \<VMMServerName>\MSSCVMMLibrary\RPScripts. Placez-le sur la source de hello et serveurs VMM cible.
2. Créez le script hello (par exemple, RPScript) et vérifier qu’il fonctionne comme prévu.
3. Placez le script de hello dans l’emplacement de hello \<VMMServerName > \MSSCVMMLibrary, sur les serveurs VMM source et cible hello.


## <a name="next-steps"></a>Étapes suivantes

[En savoir plus](site-recovery-failover.md) sur l’exécution des basculements.
