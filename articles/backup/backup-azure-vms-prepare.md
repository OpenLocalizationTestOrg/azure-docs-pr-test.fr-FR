---
title: aaaPreparing tooback de votre environnement de machines virtuelles | Documents Microsoft
description: "Assurez-vous que votre environnement est prêt pour la sauvegarde de machines virtuelles dans Azure"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonn
editor: 
keywords: "sauvegardes ; sauvegarde ;"
ms.assetid: 238ab93b-8acc-4262-81b7-ce930f76a662
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/25/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 3b914c507dd6ad703ea799115ae84ac229e27787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-azure-virtual-machines"></a>Préparer votre tooback environnement des machines virtuelles
> [!div class="op_single_selector"]
> * [Modèle Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modèle classique](backup-azure-vms-prepare.md)
>
>

Avant de pouvoir sauvegarder une machine virtuelle (VM) Azure, trois conditions sont requises.

* Vous devez toocreate un coffre de sauvegarde ou identifier un coffre de sauvegarde existant *Bonjour même région que votre machine virtuelle*.
* Établir une connectivité réseau entre hello Internet public Azure adresses et hello des points de terminaison de stockage Azure.
* Installez l’agent de machine virtuelle hello sur hello machine virtuelle.

Si vous connaissez ces conditions existent déjà dans votre environnement puis continuer toohello [sauvegarder votre article de machines virtuelles](backup-azure-vms.md). Dans le cas contraire, lecture, cet article va vous guider hello étapes tooprepare tooback de votre environnement d’une machine virtuelle Azure.

##<a name="supported-operating-system-for-backup"></a>Versions du système d’exploitation prises en charge pour une sauvegarde
 * **Linux**: Azure Backup prend en charge [une liste de distributions approuvées par Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , à l’exception de CoreOS Linux. _Autres Bring-Your-propriétaire-distributions Linux peuvent également fonctionner tant que l’agent de machine virtuelle hello est disponible sur l’ordinateur virtuel de hello et prise en charge de Python existe. Toutefois, nous n’approuvons pas ces distributions pour la sauvegarde._
 * **Windows Server** : les versions antérieures à Windows Server 2008 R2 ne sont pas prises en charge.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limites lors de la sauvegarde et la restauration d’une machine virtuelle
> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). Hello liste suivante présente les limitations de hello lors du déploiement dans le modèle classique de hello.
>
>

* La sauvegarde de machines virtuelles ayant plus de 16 disques de données n’est pas prise en charge.
* La sauvegarde de machines virtuelles avec une adresse IP réservée et sans point de terminaison n’est pas prise en charge.
* Réseau monté lecteurs attachés tooVM n’incluent pas les données de sauvegarde.
* Le remplacement d’une machine virtuelle existante pendant la restauration n’est pas pris en charge. Tout d’abord supprimer les ordinateur virtuel existant hello et tous les disques associés et restaurer les données de salutation à partir de la sauvegarde.
* La sauvegarde et la restauration entre différentes régions ne sont pas prises en charge.
* Sauvegarde des ordinateurs virtuels à l’aide du service de sauvegarde Azure hello est pris en charge dans toutes les régions publiques d’Azure (consultez hello [liste de vérification](https://azure.microsoft.com/regions/#services) des régions prises en charge). Si la région hello que vous recherchez n’est pas pris en charge aujourd'hui, il s’affiche pas dans la liste déroulante de hello lors de la création du coffre.
* Sauvegarde des ordinateurs virtuels à l’aide du service de sauvegarde Azure hello est pris en charge uniquement pour les systèmes d’exploitation select :
* La restauration d’une machine virtuelle de contrôleur de domaine qui fait partie d’une configuration à plusieurs contrôleurs de domaine est prise en charge uniquement par le biais de PowerShell. En savoir plus sur la [restauration d’un contrôleur de domaine dans un environnement à plusieurs contrôleurs de domaine](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* Restauration d’ordinateurs virtuels qui ont hello suivant les configurations réseau spéciale est prise en charge uniquement par le biais de PowerShell. Machines virtuelles que vous créez à l’aide de flux de travail de restauration hello Bonjour UI auront pas ces configurations réseau une fois l’opération de restauration hello terminée. toolearn, voir [restauration de machines virtuelles avec des configurations de réseau spéciales](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Machines virtuelles avec configuration d’un équilibreur de charge (internes et externes)
  * Machines virtuelles avec plusieurs adresses IP réservées
  * Machines virtuelles avec plusieurs cartes réseau

## <a name="create-a-backup-vault-for-a-vm"></a>Création d’un coffre de sauvegarde pour une machine virtuelle
Un coffre de sauvegarde est une entité qui stocke toutes les sauvegardes de hello et les points de récupération qui ont été créées au fil du temps. coffre de sauvegarde Hello contient également des stratégies de sauvegarde hello qui seront appliqués toohello ordinateurs virtuels en cours de sauvegarde.

> [!IMPORTANT]
> À partir de mars 2017, vous pouvez utiliser n’est plus les coffres de sauvegarde hello toocreate portail classique. Les archivages de sauvegarde existants sont toujours gérés, et il est possible de[utilisent les coffres de sauvegarde Azure PowerShell toocreate](./backup-client-automation-classic.md#create-a-backup-vault). Toutefois, Microsoft recommande de que créer des coffres de Services de récupération pour tous les déploiements, car les améliorations ultérieures s’appliquent tooRecovery les coffres des Services, uniquement.


Cette image montre les relations de hello entre hello différentes entités de sauvegarde Azure : ![des entités de sauvegarde Azure et de relations](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Connectivité réseau
Dans l’ordre toomanage hello VM des instantanés, extension de sauvegarde hello a besoin de connectivité toohello Azure des adresses IP publiques. Sans connectivité Internet hello, HTTP demandes délai d’attente et hello opération de sauvegarde l’ordinateur virtuel de hello échoue. Si votre déploiement comporte des restrictions d’accès (via un groupe de sécurité réseau (NSG), par exemple), choisissez l’une de ces options pour fournir un chemin clair pour le trafic de sauvegarde :

* [Plages d’adresses IP Whitelist hello centre de données Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) -consultez l’article hello pour obtenir des instructions sur la façon dont toowhitelist hello les adresses IP.
* Déployer un serveur de proxy HTTP pour acheminer le trafic.

Lorsque vous décidez quels toouse option, les compromis de hello sont entre facilité de gestion, un contrôle granulaire et le coût.

| Option | Avantages | Inconvénients |
| --- | --- | --- |
| Plages IP de liste blanche |Aucun coût supplémentaire<br><br>Pour l’ouverture d’accès dans un groupe de sécurité réseau, utilisez hello <i>Set-AzureNetworkSecurityRule</i> applet de commande. |Toomanage complexe en tant que la modification des plages IP hello affecté au fil du temps.<br><br>Fournit un ensemble de toohello d’accès d’Azure et pas seulement le stockage. |
| Serveur proxy HTTP |Contrôle granulaire de proxy de hello par rapport au stockage hello URL autorisées. contrôle granulaire de toosetup dans le proxy de hello, https://\*.blob.core.windows.net/\* toobe dans la liste approuvée a besoin de modèle d’URL. toowhitelist hello uniquement le compte de stockage utilisé par hello machine virtuelle, https://\<storageAccount\>.blob.core.windows.net/\* toobe dans la liste approuvée a besoin de modèle d’URL. <br>TooVMs d’accès unique point d’Internet.<br>Pas sujet tooAzure changements d’adresses IP. |Frais supplémentaires pour l’exécution d’une machine virtuelle avec le logiciel du serveur proxy hello. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Plages d’adresses IP Whitelist hello centre de données Azure
plages d’IP toowhitelist hello centre de données Azure, consultez hello [site Web Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) pour plus d’informations sur les plages d’adresses IP hello et des instructions.

### <a name="using-an-http-proxy-for-vm-backups"></a>Utilisation d’un proxy HTTP pour les sauvegardes de machine virtuelle
Lorsque vous sauvegardez une machine virtuelle, extension de sauvegarde hello sur hello VM envoie hello instantané gestion des commandes tooAzure stockage à l’aide d’une API de HTTPS. Acheminer le trafic de sauvegarde d’extension de hello via le proxy HTTP de hello, car elle est hello seul composant configuré pour l’accès toohello Internet public.

> [!NOTE]
> Il n’existe aucune recommandation pour les logiciels de proxy hello qui doit être utilisé. Assurez-vous que vous sélectionnez un proxy possédant le caractère collant sortante et qui est compatible avec les étapes de configuration hello ci-dessous. Assurez-vous que les logiciels tiers ne modifiez pas les paramètres du proxy hello
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

*Veillez à remplacer les noms de hello dans hello exemple avec le déploiement de hello détails tooyour appropriée.*

## <a name="vm-agent"></a>Agent VM
Avant que vous puissiez sauvegarder hello machine virtuelle Azure, vous devez vous assurer que l’agent de machine virtuelle Azure hello est correctement installé sur l’ordinateur virtuel de hello. Étant donné que l’agent de machine virtuelle hello est un composant facultatif au moment de hello hello d’ordinateur virtuel est créé, assurez-vous que hello case à cocher à l’agent de machine virtuelle hello est sélectionnée avant de la machine virtuelle de hello est configurée.

### <a name="manual-installation-and-update"></a>Installation et mise à jour manuelles
agent de machine virtuelle Hello est déjà présent dans les ordinateurs virtuels qui sont créés à partir de la galerie Azure de hello. Toutefois, les ordinateurs virtuels qui sont migrés à partir de centres de données locale n’ont pas installé l’agent de machine virtuelle hello. Pour ces ordinateurs virtuels, agent de machine virtuelle hello doit toobe installé de manière explicite. En savoir plus sur [agent de machine virtuelle hello lors de l’installation sur un ordinateur virtuel existant](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **opération** | **Windows** | **Linux** |
| --- | --- | --- |
| L’installation d’agent de machine virtuelle hello |<li>Téléchargez et installez hello [agent MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vous devrez l’installation de l’administrateur des privilèges toocomplete hello. <li>[Mettre à jour la propriété de machine virtuelle hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate qui hello agent est installé. |<li> Installer hello dernières [agent Linux](https://github.com/Azure/WALinuxAgent) à partir de GitHub. Vous devrez l’installation de l’administrateur des privilèges toocomplete hello. <li> [Mettre à jour la propriété de machine virtuelle hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate qui hello agent est installé. |
| Mise à jour d’agent de machine virtuelle hello |Mise à jour l’agent de machine virtuelle hello est aussi simple que la réinstallation hello [binaires de l’agent de machine virtuelle](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Assurez-vous qu’aucune opération de sauvegarde n’est en cours d’exécution pendant que l’agent de machine virtuelle hello est en cours de mise à jour. |Suivez les instructions de hello [mise à jour de l’agent Linux VM de hello ](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Assurez-vous qu’aucune opération de sauvegarde n’est en cours d’exécution pendant que l’agent de machine virtuelle hello est en cours de mise à jour. |
| Valider l’installation de l’agent de machine virtuelle hello |<li>Accédez toohello *C:\WindowsAzure\Packages* dossier Bonjour Azure VM. <li>Vous devez rechercher la présence du fichier WaAppAgent.exe hello.<li> Cliquez sur le fichier de hello, accédez trop**propriétés**, puis sélectionnez hello **détails** onglet hello Version du produit doit être 2.6.1198.718 ou une version ultérieure. |N/A |

En savoir plus sur hello [agent de machine virtuelle](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) et [comment tooinstall il](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Extension de sauvegarde
tooback machine virtuelle de hello, hello service Azure Backup installe un agent de machine virtuelle toohello extension. Hello service sauvegarde Azure met à niveau et correctifs d’extension de sauvegarde hello sans intervention de l’utilisateur supplémentaires en toute transparence.

extension de sauvegarde Hello est installée si hello machine virtuelle est en cours d’exécution. Une machine virtuelle en cours d’exécution fournit également un risque de plus grande hello d’obtention d’un point de récupération cohérents avec les applications. Toutefois, hello Azure Backup service continuera tooback des hello machine virtuelle, même si elle est désactivée et l’extension de hello n’a pas pu être installé (aka hors connexion VM). Dans ce cas, le point de récupération hello sera *cohérent d’incident* comme indiqué ci-dessus.

## <a name="questions"></a>Des questions ?
Si vous avez des questions, ou s’il en existe toute fonctionnalité qui vous aimeriez toosee inclus, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous avez préparé votre environnement pour la sauvegarde de votre machine virtuelle, la prochaine étape logique est toocreate une sauvegarde. Hello planification article fournit des informations détaillées sur la sauvegarde d’ordinateurs virtuels.

* [Sauvegarde de machines virtuelles](backup-azure-vms.md)
* [Planification de votre infrastructure de sauvegarde de machines virtuelles](backup-azure-vms-introduction.md)
* [Gestion des sauvegardes de machines virtuelles](backup-azure-manage-vms.md)
