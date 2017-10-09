---
title: "Sauvegarde Azure : sauvegarde cohérente des applications des machines virtuelles Linux | Microsoft Docs"
description: "Utilisez des scripts tooguarantee sauvegarde cohérente au niveau de l’application tooAzure, pour vos machines virtuelles de Linux. les scripts de Hello s’appliquent tooLinux uniquement des machines virtuelles dans un déploiement du Gestionnaire de ressources ; les scripts Hello ne s’appliquent pas tooWindows machines virtuelles ou aux déploiements de service manager. Cet article vous guide tout au long des étapes de hello pour les scripts de hello, notamment la résolution des problèmes de configuration."
services: backup
documentationcenter: dev-center-name
author: anuragmehrotra
manager: shivamg
keywords: "sauvegarde cohérente des applications ; sauvegarde cohérente des applications de la machine virtuelle Azure ; sauvegarde de la machine virtuelle Linux ; sauvegarde Azure"
ms.assetid: bbb99cf2-d8c7-4b3d-8b29-eadc0fed3bef
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/12/2017
ms.author: anuragm;markgal
ms.openlocfilehash: d557dd973364d79bb4d8ce954f648de835dd345f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-consistent-backup-of-azure-linux-vms-preview"></a>Sauvegarde cohérente des applications des machines virtuelles Linux Azure (version préliminaire)

Cet article traite de hello script avant de Linux et script postérieur à framework, et comment il peut être tootake utilisé des sauvegardes cohérentes avec les applications d’ordinateurs virtuels Linux de Azure.

> [!Note]
> infrastructure de script avant et après script Hello est pris en charge uniquement pour les machines virtuelles déployées par le Gestionnaire de ressources Azure de Linux. Les scripts pour la cohérence d’application ne sont pas pris en charge pour les machines virtuelles déployées par Service Manager ou les machines virtuelles Windows.
>

## <a name="how-hello-framework-works"></a>Fonctionne de l’infrastructure de hello

infrastructure de Hello fournit une option toorun des scripts personnalisés avant et après des scripts pendant que vous prenez des captures instantanées de machine virtuelle. Les scripts sont exécutés juste avant que vous prenez un instantané VM hello et post-scripts sont exécutées immédiatement après avoir appliqué les instantané d’ordinateur virtuel hello. Cela donne hello toocontrol de flexibilité votre environnement et l’application pendant que vous prenez des captures instantanées de machine virtuelle.

Dans ce scénario, il est important tooensure cohérents au niveau de l’application sauvegarde de machine virtuelle. script de Pre Hello peut appeler des natif de l’application API tooquiesce hello IOs et vider toohello de contenu en mémoire disque. Cela garantit qu’un instantané hello est cohérente avec les applications (autrement dit, cette application hello s’affiche quand hello machine virtuelle est démarré après la restauration). Post-script de peut être utilisé toothaw hello IOs. Pour cela, à l’aide des API de l’application en mode natif afin que l’application hello peut reprendre la capture instantanée de post-VM les opérations normales.

## <a name="steps-tooconfigure-pre-script-and-post-script"></a>Étapes tooconfigure script préalable et le script postérieur à

1. Se connecter comme hello racine utilisateur toohello VM Linux que vous souhaitez tooback des.

2. Télécharger **VMSnapshotScriptPluginConfig.json** de [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig), puis copiez toohello **/etc/azure** dossier sur tous les ordinateurs virtuels hello que vous allez tooback des. Créer hello **/etc/azure** active s’il n’existe pas déjà.

3. Copiez hello script avant et après de script pour votre application sur hello toutes les machines virtuelles que vous envisagez de tooback des. Vous pouvez copier l’emplacement tooany des scripts hello sur hello machine virtuelle. Être tooupdate vraiment hello chemin d’accès complet hello des fichiers de script Bonjour **VMSnapshotScriptPluginConfig.json** fichier.

4. Vérifiez que hello les autorisations pour ces fichiers suivantes :

   - **VMSnapshotScriptPluginConfig.json** : autorisation « 600 ». Par exemple, seul l’utilisateur « racine » doit avoir les autorisations « lecture » et « écriture » un fichier toothis, et aucun utilisateur ne doit disposer d’autorisations « Exécuter ».

   - **Fichier de pré-script** : autorisation « 700 ».  Par exemple, seul l’utilisateur « racine » doit avoir « lecture », « écriture » et « exécuter » le fichier toothis d’autorisations.
  
   - **Post-script** : autorisation « 700 ». Par exemple, seul l’utilisateur « racine » doit avoir « lecture », « écriture » et « exécuter » le fichier toothis d’autorisations.

   > [!Important]
   > infrastructure de Hello donne aux utilisateurs beaucoup d’énergie. Il est important qu’il est sécurisé et que seul l’utilisateur « racine » a accès toocritical JSON et des fichiers script.
   > Si les exigences précédentes hello ne sont pas remplies, le script de hello ne s’exécute pas. Cela entraîne une sauvegarde du système de fichiers/point cohérent d’incident.
   >

5. Configurez **VMSnapshoScriptPluginConfig.json** comme décrit ici :
    - **pluginName** : laissez ce champ tel quel, sans quoi vos scripts ne fonctionneront pas comme prévu.

    - **preScriptLocation**: fournissent de chemin d’accès complet de hello du script avant de hello sur hello VM de cours toobe sauvegardé.

    - **postScriptLocation**: fournissent de chemin d’accès complet de hello du post-script de hello sur hello VM de cours toobe sauvegardé.

    - **preScriptParams**: fournir des paramètres facultatifs hello nécessitant toobe passé script avant de toohello. Tous les paramètres doivent être entre guillemets et être séparés par des virgules s’il existe plusieurs paramètres.

    - **postScriptParams**: fournir des paramètres facultatifs hello nécessitant toobe passé toohello postérieurs aux scripts. Tous les paramètres doivent être entre guillemets et être séparés par des virgules s’il existe plusieurs paramètres.

    - **preScriptNoOfRetries**: définir nombre hello de script avant de hello doit être retentée si une erreur se produit avant la fin d’exécution. Zéro signifie qu’une seule tentative a lieu et qu’aucune nouvelle tentative n’a lieu en cas d’échec.

    - **postScriptNoOfRetries**: définir nombre hello de post-script de hello doit être retentée si une erreur se produit avant la fin d’exécution. Zéro signifie qu’une seule tentative a lieu et qu’aucune nouvelle tentative n’a lieu en cas d’échec.
    
    - **timeoutInSeconds**: spécifier les délais d’attente individuels pour le script avant de hello et postérieurs aux scripts hello.

    - **continueBackupOnFailure**: définissez cette valeur trop**true** si vous Azure Backup toofall tooa précédent système cohérent d’incident cohérent/sauvegarde de fichiers si le script avant ou après un script échoue. La définition de cette trop**false** échoue hello sauvegarde en cas d’échec de script (sauf lorsque vous avez seul disque VM cette sauvegarde de retour toocrash cohérent de se situe indépendamment de ce paramètre).

    - **fsFreezeEnabled**: spécifiez si Linux fsfreeze doit être appelée lorsque vous prenez la cohérence du système de fichiers hello virtuelle instantané tooensure. Nous vous recommandons de conserver ce paramètre est défini trop**true** , sauf si votre application comporte une dépendance sur la désactivation de fsfreeze.

6. environnement de script Hello est maintenant configurée. Si la sauvegarde d’ordinateurs virtuels hello est déjà configurée, sauvegarde suivante de hello appelle les scripts de hello et déclenche une sauvegarde cohérente de l’application. Si la sauvegarde d’ordinateurs virtuels hello n’est pas configuré, le configurer à l’aide de [sauvegarder les coffres des Services de machines virtuelles tooRecovery.](https://docs.microsoft.com/azure/backup/backup-azure-vms-first-look-arm)

## <a name="troubleshooting"></a>Résolution des problèmes

Assurez-vous que vous ajoutez un enregistrement approprié lors de l’écriture de votre script avant et un script postérieur à et examinez votre toofix de journaux script tous les problèmes de script. Si vous rencontrez des problèmes d’exécution de scripts, consultez toohello tableau pour plus d’informations.

| Error | Message d’erreur | Action recommandée |
| ------------------------ | -------------- | ------------------ |
| Pre-ScriptExecutionFailed |script de Pre Hello a renvoyé une erreur, de sauvegarde peut donc pas être cohérentes avec les applications. | Examinez les journaux des échecs hello pour votre problème de hello toofix script.|  
|   Post-ScriptExecutionFailed |    post-script de Hello a retourné une erreur qui peut affecter l’état de l’application. |  Examinez les journaux des échecs hello pour votre problème de hello toofix script et vérifier l’état de l’application hello. |
| Pre-ScriptNotFound |  Hello script préalable est introuvable à l’emplacement de hello est spécifié dans hello **VMSnapshotScriptPluginConfig.json** le fichier de configuration. | Assurez-vous que ce préalable script est présent dans le chemin de hello est spécifié dans la sauvegarde de tooensure de fichiers config hello cohérents avec les applications.|
| Post-ScriptNotFound | script postérieur à Hello n’a pas été trouvé à l’emplacement de hello qui est spécifié dans hello **VMSnapshotScriptPluginConfig.json** le fichier de configuration. | Assurez-vous que ce postérieur au script est présent dans le chemin de hello est spécifié dans la sauvegarde de tooensure de fichiers config hello cohérents avec les applications.|
| IncorrectPluginhostFile | Hello **Pluginhost** , qui est livré avec hello VmSnapshotLinux extension, il est endommagé, donc script avant et après script ne peut pas exécuter et de sauvegarde de hello ne pourra plus être cohérentes avec les applications.   | Désinstaller hello **VmSnapshotLinux** extension et il seront automatiquement réinstallé avec le problème de hello suivant toofix sauvegarde hello. |
| IncorrectJSONConfigFile | Hello **VMSnapshotScriptPluginConfig.json** fichier est incorrecte, par conséquent, le script avant et après script ne peut pas exécuter et sauvegarde de hello ne pourra plus être cohérentes avec les applications. | Télécharger à partir de hello [GitHub](https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig) et le configurer à nouveau. |
| InsufficientPermissionforPre-Script | Pour exécuter des scripts, utilisateur de « root » doit être propriétaire de hello du fichier de hello et fichier de hello doit avoir des autorisations « 700 » (autrement dit, seuls « propriétaire » doit avoir « lecture », « écriture » et « exécuter les autorisations »). | Assurez-vous que l’utilisateur « racine » est hello « propriétaire » du fichier de script hello et que seul « propriétaire » a « autorisations de lecture », « écriture » et « exécuter ». |
| InsufficientPermissionforPost-Script | Pour exécuter des scripts, utilisateur racine doit être propriétaire de hello du fichier de hello et fichier de hello doit avoir des autorisations « 700 » (autrement dit, seuls « propriétaire » doit avoir « lecture », « écriture » et « exécuter les autorisations »). | Assurez-vous que l’utilisateur « racine » est hello « propriétaire » du fichier de script hello et que seul « propriétaire » a « autorisations de lecture », « écriture » et « exécuter ». |
| Pre-ScriptTimeout | Hello l’exécution du script avant sauvegarde cohérents au niveau de l’application hello expiré. | Vérifier le script de hello et augmenter le délai d’expiration de hello en hello **VMSnapshotScriptPluginConfig.json** fichier qui se trouve dans **azure/etc/**. |
| Post-ScriptTimeout | l’exécution de Hello hello cohérents avec les applications après du script de sauvegarde a expiré. | Vérifier le script de hello et augmenter le délai d’expiration de hello en hello **VMSnapshotScriptPluginConfig.json** fichier qui se trouve dans **azure/etc/**. |

## <a name="next-steps"></a>Étapes suivantes
[Configurer le coffre Recovery Services de sauvegarde tooa machine virtuelle](https://docs.microsoft.com/azure/backup/backup-azure-arm-vms)
