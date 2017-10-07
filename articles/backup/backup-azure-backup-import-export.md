---
title: "Sauvegarde - sauvegarde hors connexion ou amorçage initial à l’aide d’aaaAzure hello service Azure Import/Export | Documents Microsoft"
description: "Découvrez comment Azure Backup vous permet de toosend des données réseau hello à l’aide du service d’importation/exportation Azure hello. Cet article explique hello hors connexion amorçage hello initiale des données de sauvegarde à l’aide du service d’importation/exportation Azure hello."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Flux de travail de la sauvegarde hors connexion dans la sauvegarde Azure
Azure Backup a plusieurs efficacité intégrées qui enregistrent les coûts de stockage et de réseau au cours de hello initiales sauvegardes complètes de tooAzure de données. Sauvegardes complètes initiales généralement transfèrent de grandes quantités de données et nécessitent plus de bande passante lors de la comparaison des sauvegardes toosubsequent qui transfèrent uniquement hello deltas/incrémentielles. Sauvegarde Azure compresse les sauvegardes initiales de hello. Processus hello de l’amorçage en mode hors connexion, Azure Backup peut utiliser tooAzure hors connexion des données de sauvegarde initiales hello compressé tooupload disques.  

Hello hors connexion amorçage le processus de sauvegarde Azure est étroitement intégré à hello [service Azure Import/Export](../storage/common/storage-import-export-service.md) qui vous permet de tootransfer données tooAzure à l’aide de disques. Si vous disposez de plusieurs téraoctets (To) de données de sauvegarde initiales qui doit toobe transférée sur un réseau à latence élevée et à faible bande passante, vous pouvez utiliser hello hors connexion amorçage workflow tooship hello copie de sauvegarde initiale sur un ou plusieurs disques durs tooan centre de données Azure. Cet article fournit une vue d’ensemble des étapes hello exécuter ce flux de travail.

## <a name="overview"></a>Vue d'ensemble
Hello l’amorçage en mode hors connexion en fonction de sauvegarde Azure et Azure Import/Export, il est tooAzure hors connexion des données hello tooupload simple à l’aide de disques. Au lieu de transférer la copie initiale complète hello réseau hello, les données de sauvegarde hello sont écrit tooa *emplacement intermédiaire*. Une fois que l’emplacement intermédiaire toohello hello est terminée en utilisant l’outil d’importation/exportation Azure hello, ces données sont écrites tooone ou plusieurs disques SATA, selon la quantité de hello de données. Ces lecteurs sont finalement expédiée toohello le plus proche du centre de données Azure.

Hello [août 2016 mettre à jour de la sauvegarde de Azure (et versions ultérieures)](http://go.microsoft.com/fwlink/?LinkID=229525) inclut hello *outil de préparation du disque Azure*, nommé AzureOfflineBackupDiskPrep, qui :

* Vous permet de préparer vos disques pour l’importation de Azure en utilisant l’outil d’importation/exportation Azure hello.
* Crée automatiquement un travail Azure Import pour hello service Azure Import/Export sur hello [portail Azure classic](https://manage.windowsazure.com) comme toocreating opposé hello même manuellement avec les versions antérieures de Azure Backup.

Une fois le téléchargement hello du tooAzure de données de sauvegarde hello est terminé, Azure Backup copie coffre toohello de données de sauvegarde hello et hello des sauvegardes incrémentielles.

> [!NOTE]
> toouse hello outil de préparation du disque Azure, vérifiez que vous avez installé les mises à jour août 2016 hello de sauvegarde Azure (ou version ultérieure) et effectuerez toutes les étapes de hello du flux de travail hello avec lui. Si vous utilisez une version antérieure de Azure Backup, vous pouvez préparer le disque SATA hello en utilisant l’outil d’importation/exportation Azure hello comme indiqué dans les sections suivantes de cet article.
>
>

## <a name="prerequisites"></a>Composants requis
* [Familiarisez-vous avec les flux de travail Azure Import/Export hello](../storage/common/storage-import-export-service.md).
* Avant le lancement de flux de travail hello, vérifiez hello qui suit :
  * Un coffre de sauvegarde Azure a été créé.
  * Les informations d’identification du coffre ont été téléchargées.
  * Bonjour Azure Backup agent a été installé sur Windows Server et Windows client ou serveur de System Center Data Protection Manager et ordinateur de hello est enregistré avec le coffre de sauvegarde Azure hello.
* [Télécharger les paramètres du fichier de publication Azure hello](https://manage.windowsazure.com/publishsettings) sur ordinateur hello à partir duquel vous prévoyez tooback vos données.
* Préparez un emplacement intermédiaire, qui peut être un partage réseau ou un disque supplémentaire sur l’ordinateur de hello. Hello emplacement intermédiaire est le stockage temporaire, temporairement durant ce flux de travail. Vérifiez que hello emplacement intermédiaire a suffisamment toohold d’espace disque de votre copie initiale. Par exemple, si vous essayez de tooback d’un serveur de fichiers de 500 Go, assurez-vous que la zone de transit hello est au moins de 500 Go. (Une plus petite quantité sert échéance toocompression.)
* Assurez-vous d’utiliser un disque pris en charge. 2,5 pouces uniquement SSD ou 2,5 ou 3,5 pouces SATA II/III des disques durs internes sont prises en charge pour une utilisation avec le service d’importation/exportation de hello. Vous pouvez utiliser des disques durs jusqu'à too10 to. Vérifiez hello [documentation du service Azure Import/Export](../storage/common/storage-import-export-service.md#hard-disk-drives) pour hello dernier jeu de disques qui hello service prend en charge.
* Activer BitLocker sur hello ordinateur toowhich writer de lecteur SATA hello est connecté.
* [Télécharger l’outil d’importation/exportation Azure hello](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) writer de lecteur toohello ordinateur toowhich hello SATA est connecté. Cette étape n’est pas requise si vous avez téléchargé et installé mise à jour août 2016 hello de sauvegarde Azure (ou version ultérieure).

## <a name="workflow"></a>Workflow
les informations de Hello dans cette section vous aident à terminer le flux de travail de sauvegarde hors connexion hello afin que vos données peuvent être remises tooan centre de données Azure et téléchargement tooAzure stockage. Si vous avez des questions sur le service d’importation hello ou à un aspect du processus de hello, consultez hello [vue d’ensemble du service d’importation](../storage/common/storage-import-export-service.md) documentation mentionnée précédemment.

### <a name="initiate-offline-backup"></a>Lancer la sauvegarde hors connexion
1. Lorsque vous planifiez une sauvegarde, vous voyez hello suivant l’écran (dans Windows Server, le client Windows ou System Center Data Protection Manager).

    ![Écran d’importation](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    Voici écran correspondant hello dans System Center Data Protection Manager : <br/>
    ![Écran d’importation DPM](./media/backup-azure-backup-import-export/dpmoffline.png)

    description de Hello d’entrées de hello est comme suit :

    * **Emplacement intermédiaire**: hello stockage temporaire emplacement toowhich hello copie de sauvegarde initiale est écrit. Cela peut être sur un partage réseau ou un ordinateur local. Si l’ordinateur de copie hello et l’ordinateur source sont différentes, nous recommandons que vous spécifiez le chemin d’accès réseau complet de hello Hello emplacement intermédiaire.
    * **Nom de tâche d’importation Azure**: nom unique de hello en importation Azure service et Azure Backup suivre le transfert hello des données envoyées sur disques tooAzure.
    * **Paramètres de publication Azure**: un fichier XML qui contient des informations sur le profil de votre abonnement. Il contient également les informations d’identification sécurisées associées à votre abonnement. Vous pouvez [télécharger le fichier de hello](https://manage.windowsazure.com/publishsettings). Fournir toohello de chemin d’accès local hello publier le fichier de paramètres.
    * **ID d’abonnement Azure**: hello ID d’abonnement Azure pour l’abonnement hello où vous prévoyez de tâche d’importation Azure tooinitiate hello. Si vous avez plusieurs abonnements Azure, utilisez hello des ID d’abonnement hello que vous souhaitez tooassociate avec la tâche d’importation hello.
    * **Compte de stockage Azure**: compte de stockage classique de type hello hello fourni un abonnement Azure qui sera associé au travail d’importation Azure hello.
    * **Conteneur de stockage Azure**: nom hello d’objet blob de stockage de destination hello Bonjour compte de stockage Azure où les données de ce travail sont importées.

    > [!NOTE]
    > Si vous avez enregistré votre tooan serveur Azure Recovery Services coffre à partir de hello [portail Azure](https://portal.azure.com) pour les sauvegardes se trouvent pas dans un abonnement du fournisseur de solutions de Cloud (CSP), vous pouvez toujours créer un compte de stockage de type classique à partir de hello Portail Azure et l’utiliser pour le flux de travail de sauvegarde hors connexion hello.
    >
    >

     Enregistrer toutes ces informations, car vous devez tooenter à nouveau dans comme suit. Hello uniquement *emplacement intermédiaire* est obligatoire si vous avez utilisé des disques hello tooprepare hello préparation du disque Azure outil.    
2. Terminer le flux de travail hello et sélectionnez **sauvegarder maintenant** dans la copie de hello Azure Backup management console tooinitiate hello hors connexion de sauvegarde. sauvegarde initiale de Hello est écrit toohello la zone de transit dans le cadre de cette étape.

    ![Sauvegarder maintenant](./media/backup-azure-backup-import-export/backupnow.png)

    toocomplete hello correspondant flux de travail dans System Center Data Protection Manager, avec le bouton droit hello **groupe de Protection**, puis choisissez hello **créer un point de récupération** option. Vous choisissez ensuite hello **Protection en ligne** option.

    ![Sauvegarder maintenant DPM](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Après l’opération de hello, hello emplacement intermédiaire est prêt toobe utilisé pour la préparation du disque.

    ![Progression de la sauvegarde](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>Préparer un disque SATA et créer une tâche d’importation Azure à l’aide de l’outil de préparation de disque de Azure hello
outil de préparation du disque Azure Hello est disponible dans le répertoire d’installation de l’agent des Services de récupération hello (mise à jour août 2016 et versions ultérieures) Bonjour suivant le chemin d’accès.

   *\Microsoft**Azure**Recovery**Services* *Agent\Utils\*

1. Toohello active, puis hello de copie **AzureOfflineBackupDiskPrep** ordinateur de copie tooa Active le hello toobe lecteurs préparée sont montés. Vérifiez les éléments suivants de hello avec l’ordinateur de copie toohello tenir compte :

    * Hello copie ordinateur peut accéder hello emplacement intermédiaire pour hello hors connexion amorçage du flux de travail à l’aide de hello même réseau de chemin d’accès qui a été fourni dans hello **lancer une sauvegarde hors connexion** flux de travail.
    * BitLocker est activé sur l’ordinateur de hello.
    * ordinateur de Hello accessible hello portail Azure.

    Si nécessaire, ordinateur de copie hello peut hello identique à l’ordinateur source de hello.
2. Ouvrez une invite de commandes avec élévation de privilèges sur l’ordinateur de copie hello avec le répertoire d’outil de préparation du disque Azure hello en tant que répertoire en cours de hello et exécutez hello de commande suivante :

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | Paramètre | Description |
    | --- | --- |
    | s:&lt;*Staging Location Path*&gt; |Entrée obligatoire qui a utilisé tooprovide hello chemin d’accès toohello emplacement que vous avez entré dans hello intermédiaire **lancer une sauvegarde hors connexion** flux de travail. |
    | p:&lt;*tooPublishSettingsFile de chemin d’accès*&gt; |Entrée facultative qui a utilisé tooprovide hello chemin d’accès toohello **paramètres de publication Azure** fichier que vous avez entré dans hello **lancer une sauvegarde hors connexion** flux de travail. |

    > [!NOTE]
    > Hello &lt;tooPublishSettingFile de chemin d’accès&gt; valeur est obligatoire lors de l’ordinateur de copie hello et l’ordinateur source sont différentes.
    >
    >

    Lorsque vous exécutez la commande hello, outil de hello demande la sélection de la tâche d’importation Azure hello correspondant des disques toohello toobe préparée hello. Si seul un travail d’importation est associé aux hello fourni emplacement intermédiaire, vous voyez un écran comme hello qui suit.

    ![Entrée d’outil de préparation des disques Azure](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Entrez la lettre de lecteur hello sans hello à droite du signe deux-points pour hello de disque monté que vous souhaitez tooprepare pour tooAzure de transfert. Fournissez la confirmation de hello mise en forme du lecteur hello lorsque vous y êtes invité.

    outil de Hello commence ensuite le disque de hello tooprepare avec les données de sauvegarde hello. Vous devrez peut-être tooattach des disques supplémentaires lorsque vous y êtes invité par l’outil de hello en cas de hello fournie disque ne dispose pas de suffisamment d’espace pour les données de sauvegarde hello. <br/>

    Extrémité hello de réussite de l’exécution de l’outil de hello, un ou plusieurs disques que vous avez fournies sont préparées pour tooAzure de livraison. En outre, un travail d’importation avec le nom de hello que vous avez fourni pendant hello **lancer une sauvegarde hors connexion** flux de travail est créé sur hello portail Azure classic. Enfin, hello outil affiche hello expédition adresse toohello centre de données Azure où les disques hello doivent toobe livré et hello du travail d’importation lien toolocate hello sur hello portail Azure classic.

    ![Préparation des disques Azure terminée](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. Livraison hello disques toohello cet outil hello fourni d’adresse et conserver hello suivi du numéro de référence future.<br/>

5. Lorsque vous passez toohello lier cet outil hello affiché, vous voyez le compte de stockage Azure hello que vous avez spécifié dans hello **lancer une sauvegarde hors connexion** flux de travail. Ici vous pouvez voir le travail d’importation hello qui vient d’être créé sur hello **IMPORT/EXPORT** onglet hello du compte de stockage.

    ![Travail d’importation créé](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. Cliquez sur **informations d’expédition** bas hello hello page tooupdate vos coordonnées comme indiqué dans hello suivant l’écran. Microsoft utilise cette tooship info votre tooyou arrière disques une fois la tâche d’importation hello est terminée.

    ![Informations de contact](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Entrez hello détails de l’expédition sur l’écran suivant de hello. Fournir hello **transporteur** et **numéro de suivi** détails qui correspondent toohello les disques que vous avez livré toohello centre de données Azure.

    ![INFORMATIONS D’EXPÉDITION](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>Flux de travail hello terminée
Après la tâche d’importation hello, les données de sauvegarde initiales sont disponibles dans votre compte de stockage. Hello agent Recovery Services, puis copie le contenu des données hello à partir de ce coffre de sauvegarde toohello compte ou les Services de récupération hello coffre, selon ce qui est applicable. Hello prochaine planifié du temps de sauvegarde, l’agent de sauvegarde Azure hello effectue la sauvegarde incrémentielle hello sur la copie de sauvegarde initiale hello.

> [!NOTE]
> Hello sections suivantes s’appliquent toousers des versions antérieures de Azure Backup ne disposant pas de l’outil de préparation du disque Azure toohello access.
>
>

### <a name="prepare-a-sata-drive"></a>Préparer un disque SATA
1. Télécharger hello [Microsoft Azure Import/Export Tool](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) ordinateur de copie toohello. Vérifiez que hello emplacement intermédiaire est accessible à partir de l’ordinateur hello dans lesquels vous prévoyez l’ensemble suivant de hello toorun de commandes. Si nécessaire, ordinateur de copie hello peut hello identique à l’ordinateur source de hello.

2. Décompressez le fichier de WAImportExport.zip hello. Exécuter l’outil WAImportExport de hello qui formate le disque SATA hello, écritures disque SATA de hello les données de sauvegarde toohello et il chiffre. Avant d’exécuter hello commande suivante, assurez-vous que BitLocker est activé sur l’ordinateur de hello. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Si vous avez installé la mise à jour août 2016 hello de sauvegarde Azure (ou version ultérieure), vérifiez que hello transit que vous avez entré est hello identique à l’autre sur hello hello **sauvegarder maintenant** écran, qui contient les fichiers AIB et d’objet Blob de Base.
    >
    >

| Paramètre | Description |
| --- | --- |
| /j: <*JournalFile*> |fichier de journal toohello Hello chemin d’accès. Chaque disque doit avoir un seul fichier journal. fichier de journal Hello ne doit pas être sur le lecteur cible hello. extension de fichier journal Hello est .jrn et est créée dans le cadre de l’exécution de cette commande. |
| /id: <*SessionId*> |ID de session Hello identifie une session de copie. Il est utilisé tooensure précise de récupération d’une session de copie interrompue. Les fichiers qui sont copiés dans une session de copie sont stockés dans un répertoire nommé d’après l’ID de session hello sur le lecteur cible hello. |
| /sk: <*StorageAccountKey*> |clé de compte Hello pour les données hello toowhich de compte de stockage hello est importé. hello toobe d’impératifs Hello même tel qu’il a été entré lors de la création de groupe de protection/stratégie de sauvegarde. |
| /BlobType |type Hello d’objet blob. Ce flux de travail réussit uniquement si **PageBlob** est spécifié. Cela n’est pas option par défaut de hello et doit être indiquée dans cette commande. |
| /t: <*TargetDriveLetter*> |lettre de lecteur Hello sans hello à droite du signe deux-points de disque dur cible de hello pour la session actuelle de copie hello. |
| /format |lecteur de hello option tooformat Hello. Spécifiez ce paramètre lorsque le lecteur de hello doit être toobe mise en forme ; Sinon, omettez-le. Avant de l’outil de hello des formats de disque de hello, il demande une confirmation à partir de la console de hello. toosuppress hello confirmation, spécifiez le paramètre /silentmode de hello. |
| /encrypt |lecteur de hello option tooencrypt Hello. Spécifiez ce paramètre lorsque le lecteur de hello n’a pas encore été chiffré avec BitLocker et les besoins toobe chiffré par hello outil. Si hello lecteur a déjà été chiffré avec BitLocker, omettez ce paramètre, spécifiez le paramètre de /bk hello et fournir la clé BitLocker existante de hello. Si vous spécifiez le paramètre de hello/format, vous devez également spécifier hello / chiffrer le paramètre. |
| /srcdir: <*SourceDirectory*> |répertoire source Hello qui contient les fichiers toobe copiés toohello le lecteur cible. Assurez-vous que ce nom de répertoire spécifié hello a un chemin d’accès complet et non relatif. |
| /dstdir: <*DestinationBlobVirtualDirectory*> |Hello chemin d’accès toohello répertoire virtuel de destination dans votre compte de stockage Azure. Lorsque vous spécifiez des répertoires virtuels de destination hello ou des objets BLOB, être toouse que les noms de conteneur valide. N’oubliez pas que les noms de conteneur doivent être en minuscules.  Ce nom de conteneur doit être hello une que vous avez entré lors de la création de groupe de protection/stratégie de sauvegarde. |

> [!NOTE]
> Un fichier journal est créé dans le dossier WAImportExport hello qui capture les informations d’ensemble hello du flux de travail hello. Vous avez besoin de ce fichier lorsque vous créez un travail d’importation dans hello portail Azure.
>
>

  ![Sortie PowerShell](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Créer un travail d’importation Bonjour portail Azure
1. Atteindre le compte de stockage tooyour Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **importation/exportation**, puis **créer tâche d’importation** dans le volet de tâches hello.

    ![Onglet Importer/exporter dans hello portail Azure](./media/backup-azure-backup-import-export/azureportal.png)

2. À l’étape 1 de l’Assistant de hello, indiquent que vous avez préparé votre disque et que vous disposez de fichier journal d’unité hello disponible.

3. À l’étape 2 de l’Assistant de hello, fournissent des informations de contact pour hello personne responsable de cette tâche d’importation.

4. À l’étape 3, téléchargez les fichiers journaux hello lecteur que vous avez obtenu dans la section précédente de hello.

5. À l’étape 4, entrez un nom descriptif pour le travail d’importation hello que vous avez entré lors de la création de groupe de protection/stratégie de sauvegarde. nom Hello que vous entrez peut contenir uniquement des lettres minuscules, des chiffres, des traits d’union et des traits de soulignement, doit commencer par une lettre et ne peut pas contenir d’espaces. nom Hello que vous choisissez est utilisé tootrack vos travaux lorsqu’ils sont en cours d’exécution et lorsqu’elles sont terminées.

6. Ensuite, sélectionnez votre région de centre de données à partir de la liste de hello. région de centre de données Hello indique toowhich centre de données et l’adresse hello, vous devez expédier votre package.

    ![Sélectionner la région de centre de données](./media/backup-azure-backup-import-export/dc.png)

7. À l’étape 5, sélectionnez votre transporteur pour le retour à partir de la liste de hello et entrez votre numéro de compte du transporteur. Microsoft utilise ce compte tooship vos lecteurs sauvegarder tooyou une fois votre travail d’importation est terminée.

8. Expédier les disques hello et entrez hello suivi nombre tootrack hello d’expédition de hello. Une fois le disque de hello arrive dans le centre de données hello, il est copié du compte de stockage toohello et état de hello est mise à jour.

    ![État terminé](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>Flux de travail hello terminée
Une fois que les données de sauvegarde initiales hello seront disponibles dans votre compte de stockage hello agent Microsoft Azure Recovery Services copie le contenu hello de données de salutation à partir de ce coffre de sauvegarde toohello compte ou un coffre Recovery Services, selon ce qui est applicable. Dans la prochaine planification de hello heure de la sauvegarde, hello Azure Backup agent effectue la sauvegarde incrémentielle hello sur la copie de sauvegarde initiale hello.

## <a name="next-steps"></a>Étapes suivantes
* Pour toute question sur le flux de travail Azure Import/Export hello, consultez trop[hello Microsoft Azure Import/Export service tootransfer données tooBlob stockage](../storage/common/storage-import-export-service.md).
* Consultez la section de sauvegarde hors connexion toohello Hello Azure Backup [FAQ](backup-azure-backup-faq.md) pour toute question sur les flux de travail hello.
