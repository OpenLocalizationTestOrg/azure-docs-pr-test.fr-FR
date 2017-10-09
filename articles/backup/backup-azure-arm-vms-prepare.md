---
title: "Sauvegarde Azure : Préparer la tooback les machines virtuelles | Documents Microsoft"
description: "Assurez-vous que votre environnement est prêt pour la sauvegarde de machines virtuelles dans Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "sauvegardes ; sauvegarde ;"
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>Préparer votre tooback environnement déployées par le Gestionnaire de ressources des machines virtuelles
> [!div class="op_single_selector"]
> * [Modèle Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modèle classique](backup-azure-vms-prepare.md)
>
>

Cet article fournit des étapes de hello pour la préparation de votre tooback environnement une machine déployées par le Gestionnaire de ressources de virtuelle (VM). Hello les étapes présentées dans les procédures hello utilisent hello portail Azure.  

Hello service Azure Backup a deux types de coffres (sauvegarder archivages et les coffres des services de récupération) pour protéger vos machines virtuelles. Un coffre de sauvegarde protège les machines virtuelles déployées à l’aide du modèle de déploiement classique hello. Un coffre Recovery Services protège les **machines virtuelles déployées à l’aide du modèle Classic et à l’aide du modèle Resource Manager**. Vous devez utiliser un tooprotect de coffre Recovery Services un ordinateur virtuel déployé de gestionnaire de ressources.

> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Consultez [préparer votre tooback environnement des machines virtuelles](backup-azure-vms-prepare.md) pour plus d’informations sur l’utilisation de déploiement de classique des machines virtuelles de modèle.
>
>

Avant de pouvoir protéger ou sauvegarder une machine virtuelle déployée à l’aide du modèle Resource Manager, vérifiez que ces les conditions préalables suivantes sont remplies :

* Créer un coffre recovery services (ou identifiez un coffre recovery services existants) *Bonjour même emplacement que votre machine virtuelle*.
* Sélectionnez un scénario, définir la stratégie de sauvegarde hello et définir les éléments tooprotect.
* Vérification de l’installation de hello d’Agent de machine virtuelle sur l’ordinateur virtuel.
* Vérifiez la connectivité réseau
* Pour les machines virtuelles Linux, au cas où vous souhaiteriez toocustomize votre environnement de sauvegarde pour des sauvegardes cohérentes application suivez hello [tooconfigure étapes de capture instantanée avant et après les scripts d’instantané](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

Si vous connaissez ces conditions existent déjà dans votre environnement puis continuer toohello [sauvegarder votre article de machines virtuelles](backup-azure-vms.md). Si vous avez besoin tooset ou vérifiez, aucun de ces composants requis, cet article vous guide à travers hello étapes tooprepare cette condition requise.

##<a name="supported-operating-system-for-backup"></a>Versions du système d’exploitation prises en charge pour une sauvegarde
 * **Linux**: Azure Backup prend en charge [une liste de distributions approuvées par Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , à l’exception de CoreOS Linux. _Autres Bring-Your-propriétaire-distributions Linux peuvent également fonctionner tant que l’agent de machine virtuelle hello est disponible sur l’ordinateur virtuel de hello et prise en charge de Python existe. Toutefois, nous n’approuvons pas ces distributions pour la sauvegarde._
 * **Windows Server** : les versions antérieures à Windows Server 2008 R2 ne sont pas prises en charge.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limites lors de la sauvegarde et la restauration d’une machine virtuelle
Avant de préparer votre environnement, notez les limitations hello.

* La sauvegarde de machines virtuelles ayant plus de 16 disques de données n’est pas prise en charge.
* La sauvegarde de machines virtuelles avec des tailles de disque de données supérieures à 1 023 Go n’est pas prise en charge.
* La sauvegarde de machines virtuelles avec une adresse IP réservée et sans point de terminaison n’est pas prise en charge.
* La sauvegarde des machines virtuelles chiffrées BEK seulement n’est pas prise en charge. La sauvegarde des machines virtuelles Linux chiffrées LUKS n’est pas prise en charge.
* La sauvegarde de machines virtuelles sur une configuration Serveur de fichiers avec montée en puissance parallèle n’est pas recommandée.
* Réseau monté lecteurs attachés tooVM n’incluent pas les données de sauvegarde.
* Le remplacement d’une machine virtuelle existante pendant la restauration n’est pas pris en charge. Si vous essayez de toorestore hello VM lorsque hello machine virtuelle existe, l’opération de restauration hello échoue.
* La sauvegarde et la restauration entre différentes régions ne sont pas prises en charge.
* Vous pouvez sauvegarder des machines virtuelles dans toutes les régions publiques d’Azure (consultez hello [liste de vérification](https://azure.microsoft.com/regions/#services) des régions prises en charge). Si la région hello que vous recherchez n’est pas pris en charge aujourd'hui, il s’affiche pas dans la liste déroulante de hello lors de la création du coffre.
* La restauration d’une machine virtuelle de contrôleur de domaine qui fait partie d’une configuration à plusieurs contrôleurs de domaine est prise en charge uniquement par le biais de PowerShell. En savoir plus sur la [restauration d’un contrôleur de domaine dans un environnement à plusieurs contrôleurs de domaine](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Restauration d’ordinateurs virtuels qui ont hello suivant les configurations réseau spéciale est prise en charge uniquement par le biais de PowerShell. Machines virtuelles créées à l’aide de flux de travail de restauration hello Bonjour UI auront pas ces configurations réseau une fois l’opération de restauration hello terminée. toolearn, voir [restauration de machines virtuelles avec des configurations de réseau spéciales](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Machines virtuelles avec configuration d’un équilibreur de charge (internes et externes)
  * Machines virtuelles avec plusieurs adresses IP réservées
  * Machines virtuelles avec plusieurs cartes réseau

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Création d’un coffre Recovery Services pour une machine virtuelle
Un coffre recovery services est une entité qui stocke les sauvegardes hello et les points de récupération qui ont été créées au fil du temps. coffre Hello recovery services contient également des stratégies de sauvegarde hello associés avec des machines virtuelles de hello protégé.

toocreate une récupération des services de coffre :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu du Hub hello, cliquez sur **Parcourir** et, dans la liste hello des ressources, tapez **Recovery Services**. Comme vous commencez à taper, liste de hello filtre en fonction de votre entrée. Cliquez sur **Coffre Recovery Services**.

    ![Cliquez sur le bouton Parcourir de hello et tapez des Services de récupération. Lorsque vous voyez des Services de récupération hello coffre option, cliquez dessus tooopen hello Panneau de coffre de Services de récupération.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    liste de Hello des coffres des Services de récupération s’affiche.
3. Sur hello **les coffres de Services de récupération** menu, cliquez sur **ajouter**.

    ![Créer un coffre Recovery Services - Étape 2](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    Services de récupération Hello coffre s’ouvre le panneau, vous invitant à tooprovide un **nom**, **abonnement**, **groupe de ressources**, et **emplacement**.

    ![Créer un archivage de Recovery Services - Étape 5](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. Pour **nom**, entrez un coffre de hello tooidentify nom convivial. nom de Hello doit toobe unique pour hello abonnement Azure. Tapez un nom contenant entre 2 et 50 caractères. Il doit commencer par une lettre, et ne peut contenir que des lettres, des chiffres et des traits d’union.
5. Cliquez sur **abonnement** toosee hello liste abonnements. Si vous ne savez pas quel toouse d’abonnement, utiliser la valeur par défaut hello (ou suggéré) abonnement. Vous ne disposez de plusieurs choix que si votre compte professionnel est associé à plusieurs abonnements Azure.
6. Cliquez sur **groupe de ressources** toosee hello la liste des groupes de ressources disponibles, ou cliquez sur **nouveau** toocreate un groupe de ressources. Pour plus d’informations sur les groupes de ressources, consultez [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)
7. Cliquez sur **emplacement** tooselect hello région pour le coffre hello. coffre de Hello **doit** être Bonjour même région que hello ordinateurs virtuels que vous souhaitez tooprotect.

   > [!IMPORTANT]
   > Si vous n’êtes pas sûr de hello emplacement dans lequel votre machine virtuelle, fermer la boîte de dialogue Création de coffre hello et atteindre liste toohello des Machines virtuelles dans le portail de hello. Si vous avez des machines virtuelles dans plusieurs régions, vous devez toocreate un coffre Recovery Services dans chaque région. Créer hello coffre dans le premier emplacement de hello avant de passer l’emplacement suivant du toohello. Aucun compte de stockage nécessaire toospecify toostore hello sauvegarde données--le coffre Recovery Services hello et hello Azure Backup service gérer cela automatiquement.
   >
   >

8. Cliquez sur **Créer**. Il peut prendre un certain temps pour hello toobe créé de coffre de Services de récupération. Surveiller les notifications d’état hello dans hello supérieur droit dans le portail de hello. Une fois votre coffre est créé, il apparaît dans la liste hello des coffres des Services de récupération. Si vous ne voyez pas votre coffre, cliquez sur **Actualiser** pour

    ![Liste des archivages de sauvegarde](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Maintenant que vous avez créé votre archivage, découvrez comment tooset hello la réplication du stockage.

## <a name="set-storage-replication"></a>Définir la réplication du stockage
option de réplication de stockage Hello permet toochoose entre le stockage géo-redondant et le stockage localement redondant. Par défaut, votre archivage utilise un stockage géo-redondant. Laissez le stockage redondant toogeo option hello si c’est votre principal de la sauvegarde. Choisissez Stockage localement redondant si vous souhaitez une option plus économique, mais moins durable.

paramètre de réplication de stockage tooedit hello :

1. Sur hello **les coffres de Services de récupération** panneau, sélectionnez votre archivage.
    Lorsque vous cliquez sur le coffre, hello panneau Paramètres (*qui a le nom hello du coffre de hello de haut hello*) et le coffre hello s’ouvre le panneau des détails.

    ![Choisissez votre coffre à partir de la liste de hello des coffres de sauvegarde](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Sur hello **paramètres** panneau, utilisez hello slider vertical tooscroll vers le bas toohello **gérer** section. Cliquez sur **sauvegarde Infrastructure** tooopen son panneau. Bonjour **général** cliquez sur la section **Configuration de la sauvegarde** tooopen son panneau. Sur hello **Configuration de la sauvegarde** panneau, choisissez l’option de réplication de stockage hello pour votre archivage. Par défaut, votre archivage utilise un stockage géo-redondant. Si vous modifiez le type de réplication de stockage hello, cliquez sur **enregistrer**.

    ![Liste des archivages de sauvegarde](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Si vous utilisez Azure comme principal point de terminaison du stockage de sauvegarde, laissez cette option inchangée. Si vous utilisez Azure comme point de terminaison du stockage de sauvegarde non principal, utilisez plutôt le stockage localement redondant. En savoir plus sur [géo-redondant](../storage/common/storage-redundancy.md#geo-redundant-storage) et [localement redondant](../storage/common/storage-redundancy.md#locally-redundant-storage) des options de stockage Bonjour [vue d’ensemble de la réplication de stockage Azure](../storage/common/storage-redundancy.md).
    Après avoir choisi l’option de stockage hello pour votre archivage, vous êtes prêt tooassociate hello machine virtuelle avec le coffre de hello. association de hello toobegin, vous devez découvrir et inscrire hello des machines virtuelles.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Sélectionnez un objectif de sauvegarde, de définir la stratégie et de définir les éléments tooprotect
Avant d’inscrire un ordinateur virtuel dans un coffre, exécutez tooensure de processus de découverte hello que de nouvelles machines virtuelles qui ont été ajoutés toohello abonnement sont identifiés. Hello traiter les requêtes Azure pour la liste des ordinateurs virtuels dans l’abonnement hello, ainsi que les informations hello comme nom du service cloud hello et région de hello. Bonjour portail Azure, scénario fait référence toowhat vous allez tooput dans le coffre hello recovery services. La stratégie est planification hello pour la fréquence et à quel moment les points de récupération sont effectuées. Stratégie inclut également hello de rétention des points de récupération hello.

1. Si vous avez déjà ouvert un coffre Recovery Services, passez toostep 2. Si un coffre Recovery Services n’est pas ouvert, puis ouvrez hello [portail Azure](https://portal.azure.com/) et hello Hub menu, cliquez sur **davantage de services**.

   * Dans la liste de hello des ressources, tapez **Recovery Services**.
   * Comme vous commencez à taper, liste de hello filtre en fonction de votre entrée. Lorsque vous voyez **Coffres Recovery Services**, cliquez dessus.

     ![Créer un archivage de Recovery Services - Étape 1](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     liste Hello des archivages de Recovery Services s’affiche. S’il n’y a aucun coffre dans votre abonnement, cette liste est vide.

    ![Liste les coffres de vue de hello Recovery Services](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * À partir de la liste de hello des archivages de Recovery Services, sélectionnez un coffre tooopen son tableau de bord.

     Panneau de paramètres Hello et hello de coffre de tableau de bord pour l’archivage hello choisi, s’ouvre.

     ![Ouvrir le panneau de l’archivage](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. Menu de tableau de bord coffre hello sur **sauvegarde** Panneau de sauvegarde tooopen hello.

    ![Ouvrir le panneau Sauvegarde](./media/backup-azure-arm-vms-prepare/backup-button.png)

    panneaux de sauvegarde et de sauvegarde objectif Hello ouvre.

    ![Ouvrir le panneau Scénario](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. Sur le panneau d’objectif de sauvegarde hello, définissez **sur lequel s’exécute votre charge de travail** tooAzure et **comment vous souhaitez toobackup** tooVirtual de l’ordinateur, puis cliquez sur **OK**.

    Hello, extension de machine virtuelle est inscrit avec le coffre de hello. Hello objectif sauvegarde panneau se ferme et hello **stratégie de sauvegarde** panneau s’ouvre.

    ![Ouvrir le panneau Scénario](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. Dans Panneau de stratégie de sauvegarde hello, sélectionnez hello sauvegarde stratégie tooapply toohello coffre.

    ![Sélectionner la stratégie de sauvegarde](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Détails de Hello de stratégie par défaut de hello sont répertoriées sous le menu déroulant de hello. Si vous souhaitez toocreate une nouvelle stratégie, sélectionnez **créer un nouveau** à partir du menu déroulant de hello. Pour savoir comment définir une stratégie de sauvegarde, consultez la section [Définition d’une stratégie de sauvegarde](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Cliquez sur **OK** stratégie de sauvegarde hello tooassociate avec le coffre de hello.

    Hello se ferme Panneau de stratégie de sauvegarde et de hello **sélectionner des machines virtuelles** panneau s’ouvre.
5. Bonjour **sélectionner des machines virtuelles** panneau, choisissez tooassociate de machines virtuelles hello avec hello spécifié de stratégie et cliquez sur **OK**.

    ![Sélectionner la charge de travail](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    machine virtuelle de Hello sélectionné est validé. Si vous ne voyez pas hello ordinateurs virtuels que vous vous attendiez toosee, vérifiez qu’ils existent dans le même emplacement que celui de hello coffre de Services de récupération et ne sont pas déjà protégé dans un autre coffre de hello. emplacement de Hello de hello que coffre des Services de récupération est indiqué dans le tableau de bord coffre hello.

6. Maintenant que vous avez défini tous les paramètres pour l’archivage de hello, Bonjour Panneau de sauvegarde cliquez **Enable Backup**. Celui-ci déploie le coffre de toohello stratégie hello et les machines virtuelles de hello. Cela ne crée pas de point de récupération initial hello pour la machine virtuelle de hello.

    ![Activer la sauvegarde](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Après avoir activé avec succès la sauvegarde de hello, votre stratégie de sauvegarde s’exécute sur une planification. Si vous souhaitez maintenant toogenerate un tooback de travail de sauvegarde à la demande des ordinateurs virtuels de hello, consultez [travail de sauvegarde hello Triggering](./backup-azure-arm-vms.md#triggering-the-backup-job).

Si vous avez des problèmes d’inscription de l’ordinateur virtuel de hello, consultez hello suivant des informations sur l’installation d’Agent de machine virtuelle de hello et sur la connectivité réseau. Vous n’avez probablement pas hello informations suivantes si vous protégez des ordinateurs virtuels créés dans Azure. Toutefois si vous avez migré vos machines virtuelles dans Azure, alors que vous avez correctement installé un agent de machine virtuelle hello et que votre machine virtuelle peut communiquer avec un réseau virtuel hello.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Installer hello Agent de machine virtuelle sur l’ordinateur virtuel de hello
Hello Agent de machine virtuelle Azure doit être installé sur la machine virtuelle Azure à hello sauvegarde extension toowork de hello. Si votre machine virtuelle a été créé à partir de la galerie Azure de hello, hello Agent de machine virtuelle est déjà présent sur l’ordinateur virtuel de hello. Ces informations sont fournies pour hello dans certains cas où vous *pas* à l’aide d’un ordinateur virtuel créé à partir de la galerie Azure de hello - par exemple, vous avez migré une machine virtuelle à partir d’un centre de données local. Dans ce cas, hello Agent de machine virtuelle doit toobe installé dans l’ordinateur virtuel de commande tooprotect hello. En savoir plus sur hello [Agent de machine virtuelle](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

Si vous avez des problèmes de sauvegarde hello machine virtuelle Azure, vérifiez que l’Agent de machine virtuelle Azure de hello est correctement installé sur machine virtuelle de hello (voir tableau hello ci-dessous). Hello tableau suivant fournit des informations supplémentaires sur l’Agent de machine virtuelle hello pour Windows et les machines virtuelles Linux.

| **opération** | **Windows** | **Linux** |
| --- | --- | --- |
| Lors de l’installation hello Agent de machine virtuelle |Téléchargez et installez hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vous devrez l’installation de l’administrateur des privilèges toocomplete hello. |<li> Installer hello dernières [agent Linux](../virtual-machines/linux/agent-user-guide.md). Vous devrez l’installation de l’administrateur des privilèges toocomplete hello. Nous vous recommandons d’installer l’agent à partir de votre référentiel de distribution. Nous **déconseillons** d’installer l’agent de machine virtuelle Linux directement à partir de github.  |
| Mise à jour hello Agent de machine virtuelle |Hello mise à jour l’Agent de machine virtuelle est aussi simple que la réinstallation hello [binaires de l’Agent de machine virtuelle](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Assurez-vous qu’aucune opération de sauvegarde n’est en cours d’exécution pendant que l’agent de machine virtuelle hello est en cours de mise à jour. |Suivez les instructions de hello [mise à jour hello Agent de machine virtuelle Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Nous vous recommandons de mettre à jour l’agent à partir de votre référentiel de distribution. Nous **déconseillons** de mettre à jour l’agent de machine virtuelle Linux à partir de github.<br>Assurez-vous qu’aucune opération de sauvegarde n’est en cours d’exécution lors de l’Agent de machine virtuelle est en cours de mise à jour de hello. |
| Validation de l’installation de l’Agent de machine virtuelle hello |<li>Accédez toohello *C:\WindowsAzure\Packages* dossier Bonjour Azure VM. <li>Vous devez rechercher la présence du fichier WaAppAgent.exe hello.<li> Cliquez sur le fichier de hello, accédez trop**propriétés**, puis sélectionnez hello **détails** onglet hello Version du produit doit être 2.6.1198.718 ou une version ultérieure. |N/A |

### <a name="backup-extension"></a>Extension de sauvegarde
Une fois hello que l’Agent VM est installé sur l’ordinateur virtuel de hello, hello service sauvegarde Azure installe hello extension de sauvegarde toohello Agent de machine virtuelle. Hello service sauvegarde Azure met à niveau et correctifs d’extension de sauvegarde hello en toute transparence.

extension de sauvegarde Hello est installée par le service de sauvegarde hello hello machine virtuelle est en cours d’exécution ou non. Une machine virtuelle en cours d’exécution fournit chance de plus grande hello d’obtention d’un point de récupération cohérents avec les applications. Toutefois, hello service Azure Backup continue tooback des hello VM même si elle est désactivée et l’extension de hello n’a pas pu être installée. autrement dit si la machine virtuelle est hors connexion. Dans ce cas, le point de récupération hello sera *cohérent d’incident*.

## <a name="network-connectivity"></a>Connectivité réseau
Dans l’ordre toomanage hello VM des instantanés, extension de sauvegarde hello a besoin de connectivité toohello Azure des adresses IP publiques. Sans connectivité Internet hello, HTTP demandes délai d’attente et hello opération de sauvegarde l’ordinateur virtuel de hello échoue. Si votre déploiement comporte des restrictions d’accès (via un groupe de sécurité réseau (NSG), par exemple), choisissez l’une de ces options pour fournir un chemin clair pour le trafic de sauvegarde :

* [Plages d’adresses IP Whitelist hello centre de données Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -consultez l’article hello pour obtenir des instructions sur la façon dont toowhitelist hello les adresses IP.
* Déployer un serveur de proxy HTTP pour acheminer le trafic.

Lorsque vous décidez quels toouse option, les compromis de hello sont entre facilité de gestion, un contrôle granulaire et le coût.

| Option | Avantages | Inconvénients |
| --- | --- | --- |
| Plages IP de liste blanche |Aucun coût supplémentaire<br><br>Pour l’ouverture d’accès dans un groupe de sécurité réseau, utilisez hello <i>Set-AzureNetworkSecurityRule</i> applet de commande. |Toomanage complexe en tant que la modification des plages IP hello affecté au fil du temps.<br><br>Fournit un ensemble de toohello d’accès d’Azure et pas seulement le stockage. |
| Serveur proxy HTTP |Contrôle granulaire de proxy de hello par rapport au stockage hello URL autorisées.<br>TooVMs d’accès unique point d’Internet.<br>Pas sujet tooAzure changements d’adresses IP. |Frais supplémentaires pour l’exécution d’une machine virtuelle avec le logiciel du serveur proxy hello. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Plages d’adresses IP Whitelist hello centre de données Azure
plages d’IP toowhitelist hello centre de données Azure, consultez hello [site Web Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) pour plus d’informations sur les plages d’adresses IP hello et des instructions.

### <a name="using-an-http-proxy-for-vm-backups"></a>Utilisation d’un proxy HTTP pour les sauvegardes de machine virtuelle
Lorsque vous sauvegardez une machine virtuelle, extension de sauvegarde hello sur hello VM envoie hello instantané gestion des commandes tooAzure stockage à l’aide d’une API de HTTPS. Acheminer le trafic de sauvegarde d’extension de hello via le proxy HTTP de hello, car elle est hello seul composant configuré pour l’accès toohello Internet public.

> [!NOTE]
> Il n’existe aucune recommandation pour les logiciels de proxy hello qui doit être utilisé. Assurez-vous que vous sélectionnez un proxy qui est compatible avec les étapes de configuration hello ci-dessous.
>
>

image d’un exemple Hello ci-dessous montre les étapes de configuration de trois hello nécessaires toouse HTTP proxy :

* Itinéraires d’application virtuelle pour que tout le trafic HTTP lié hello Internet public via Proxy VM.
* Proxy VM autorise le trafic entrant à partir d’ordinateurs virtuels dans le réseau virtuel de hello.
* Hello réseau sécurité groupe (NSG) nommé verrouillage SP a besoin d’un sécurité règle Autoriser trafic Internet sortant à partir de la machine virtuelle de Proxy.

![Groupe de sécurité réseau avec diagramme de déploiement du proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP proxy toocommunicating toohello Internet public, procédez comme suit :

#### <a name="step-1-configure-outgoing-network-connections"></a>Étape 1. Configurer les connexions réseau sortantes
###### <a name="for-windows-machines"></a>Pour les machines Windows
Cela définit la configuration du serveur proxy pour le compte système local.

1. Téléchargez [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Exécutez la commande suivante à partir de l’invite de commandes avec élévation de privilèges.

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Une fenêtre Internet Explorer s’ouvre.
3. Accédez à tooTools -> Options Internet -> connexions -> Paramètres réseau.
4. Vérifiez les paramètres de proxy pour le compte système. Définissez l’adresse IP et le port de proxy.
5. Fermez Internet Explorer.

Cela permet d’installer une configuration de proxy au niveau de l’ordinateur et de l’utiliser pour le trafic HTTP/HTTPS sortant.

Si vous avez le programme d’installation d’un serveur proxy sur un compte d’utilisateur actuel (pas un compte système Local), utilisez hello suivants script tooapply les tooSYSTEMACCOUNT :

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Si vous voyez « (407)Authentification proxy requise » dans le journal du serveur proxy, vérifiez que votre authentification est correctement configurée.
>
>

###### <a name="for-linux-machines"></a>Pour les machines Linux
Ajouter hello suivant ligne toohello ```/etc/environment``` fichier :

```
http_proxy=http://<proxy IP>:<proxy port>
```

Ajouter hello suivant lignes toohello ```/etc/waagent.conf``` fichier :

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Étape 2. Autoriser les connexions entrantes sur le serveur de proxy hello :
1. Sur le serveur de proxy hello, ouvrez le pare-feu Windows. le pare-feu Hello plus simple façon tooaccess hello est toosearch pour le pare-feu Windows avec fonctions avancées de sécurité.

    ![Ouvrez hello pare-feu](./media/backup-azure-vms-prepare/firewall-01.png)
2. Dans la boîte de dialogue Pare-feu Windows hello, cliquez sur **règles de trafic entrant** et cliquez sur **nouvelle règle...** .

    ![Créer une nouvelle règle](./media/backup-azure-vms-prepare/firewall-02.png)
3. Bonjour **Assistant Nouvelle règle de trafic entrant**, choisissez hello **personnalisé** option hello **le Type de règle** et cliquez sur **suivant**.
4. Sur hello de hello page tooselect **programme**, choisissez **tous les programmes** et cliquez sur **suivant**.
5. Sur hello **protocole et Ports** page, entrez hello informations suivantes et cliquez sur **suivant**:

    ![Créer une nouvelle règle](./media/backup-azure-vms-prepare/firewall-03.png)

   * Pour *Type de protocole*, choisissez *TCP*.
   * pour *port Local* choisissez *des Ports spécifiques*, dans le champ hello sous Spécifiez hello ```<Proxy Port>``` qui a été configuré.
   * Pour *Port distant*, sélectionnez *Tous les ports*.

     Pour rest hello d’Assistant de hello, cliquez sur tous les hello moyen toohello fin et donnez un nom à cette règle.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Étape 3. Ajouter un toohello de règle d’exception groupe de sécurité réseau :
Dans une invite de commandes Azure PowerShell, entrez hello de commande suivante :

Hello commande suivante ajoute un groupe de sécurité réseau de toohello exception. Cette exception autorise le trafic TCP à partir de n’importe quel port 10.0.0.5 tooany adresse Internet sur le port 80 (HTTP) ou 443 (HTTPS). Si vous avez besoin d’un port spécifique de hello Internet public, être tooadd que ce port toohello ```-DestinationPortRange``` également.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


*Ces étapes utilisent des noms et des valeurs spécifiques dans cet exemple. Utilisez des noms de hello et les valeurs à votre déploiement lors de la saisie, ou couper et coller les détails de votre code.*

Maintenant que vous savez que vous avez une connexion de réseau, vous êtes prêt tooback de votre machine virtuelle. Voir [Sauvegarde des machines virtuelles déployées sur Azure Resource Manager (ARM)](backup-azure-arm-vms.md).

## <a name="questions"></a>Des questions ?
Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez préparé votre environnement pour la sauvegarde de votre machine virtuelle, la prochaine étape logique est toocreate une sauvegarde. Hello planification article fournit des informations détaillées sur la sauvegarde d’ordinateurs virtuels.

* [Sauvegarde de machines virtuelles](backup-azure-vms.md)
* [Planification de votre infrastructure de sauvegarde de machines virtuelles](backup-azure-vms-introduction.md)
* [Gestion des sauvegardes de machines virtuelles](backup-azure-manage-vms.md)
