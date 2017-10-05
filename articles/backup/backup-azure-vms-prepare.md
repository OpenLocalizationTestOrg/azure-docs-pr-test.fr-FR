---
title: "Préparer votre environnement à la sauvegarde de machines virtuelles Azure | Microsoft Docs"
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
ms.openlocfilehash: 072efdccaa8df5d430314d753a437b524986b53c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="prepare-your-environment-to-back-up-azure-virtual-machines"></a>Préparer votre environnement pour la sauvegarde des machines virtuelles Azure
> [!div class="op_single_selector"]
> * [Modèle Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modèle classique](backup-azure-vms-prepare.md)
>
>

Avant de pouvoir sauvegarder une machine virtuelle (VM) Azure, trois conditions sont requises.

* Vous devez créer un coffre de sauvegarde ou identifier un coffre de sauvegarde existant *dans la même région que votre machine virtuelle*.
* Établissez une connectivité réseau entre les adresses Internet publiques Azure et les points de terminaison de stockage Azure.
* Installez l’agent de machine virtuelle sur celle-ci.

Si vous savez que ces conditions existent déjà dans votre environnement, passez à [l’article traitant de la sauvegarde de vos machines virtuelles](backup-azure-vms.md). Sinon, continuez votre lecture. Cet article vous guidera dans les étapes nécessaires pour préparer votre environnement pour la sauvegarde d’une machine virtuelle Azure.

##<a name="supported-operating-system-for-backup"></a>Versions du système d’exploitation prises en charge pour une sauvegarde
 * **Linux**: Azure Backup prend en charge [une liste de distributions approuvées par Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , à l’exception de CoreOS Linux. _D’autres distributions « Bring-Your-Own-Linux » fonctionnent également tant que l’agent de machine virtuelle est disponible sur la machine virtuelle et que Python est pris en charge. Toutefois, nous n’approuvons pas ces distributions pour la sauvegarde._
 * **Windows Server** : les versions antérieures à Windows Server 2008 R2 ne sont pas prises en charge.


## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limites lors de la sauvegarde et la restauration d’une machine virtuelle
> [!NOTE]
> Azure dispose de deux modèles de déploiement pour créer et utiliser des ressources : [Azure Resource Manager et Azure Classic](../azure-resource-manager/resource-manager-deployment-model.md). La liste suivante indique les limites lors du déploiement dans le modèle classique.
>
>

* La sauvegarde de machines virtuelles ayant plus de 16 disques de données n’est pas prise en charge.
* La sauvegarde de machines virtuelles avec une adresse IP réservée et sans point de terminaison n’est pas prise en charge.
* Les données de sauvegarde n’incluent pas les lecteurs réseau montés attachés à la machine virtuelle.
* Le remplacement d’une machine virtuelle existante pendant la restauration n’est pas pris en charge. Commencez par supprimer la machine virtuelle existante et tous les disques associés, puis restaurez les données de sauvegarde.
* La sauvegarde et la restauration entre différentes régions ne sont pas prises en charge.
* La sauvegarde de machines virtuelles à l’aide du service Azure Backup est prise en charge dans toutes les régions publiques d’Azure (voir la [liste](https://azure.microsoft.com/regions/#services) des régions prises en charge). Si la région que vous recherchez n’est pas prise en charge aujourd’hui, elle n’apparaît pas dans la liste déroulante lors de la création de l’archivage.
* La sauvegarde de machines virtuelles à l’aide du service Azure Backup n’est prise en charge que pour certaines versions de système d’exploitation :
* La restauration d’une machine virtuelle de contrôleur de domaine qui fait partie d’une configuration à plusieurs contrôleurs de domaine est prise en charge uniquement par le biais de PowerShell. En savoir plus sur la [restauration d’un contrôleur de domaine dans un environnement à plusieurs contrôleurs de domaine](backup-azure-restore-vms.md#restoring-domain-controller-vms).
* La restauration de machines virtuelles qui ont des configurations réseau spéciales suivantes est prise en charge uniquement par le biais de PowerShell. Les machines virtuelles créées à l’aide du flux de travail de restauration de l’interface utilisateur n’ont pas ces configurations réseau une fois l’opération de restauration terminée. Pour plus d’informations, consultez [Restauration de machines virtuelles avec des configurations de réseau spéciales](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Machines virtuelles avec configuration d’un équilibreur de charge (internes et externes)
  * Machines virtuelles avec plusieurs adresses IP réservées
  * Machines virtuelles avec plusieurs cartes réseau

## <a name="create-a-backup-vault-for-a-vm"></a>Création d’un coffre de sauvegarde pour une machine virtuelle
Un coffre de sauvegarde est une entité qui stocke les sauvegardes et les points de récupération créés au fil du temps. Le coffre de sauvegarde contient également les stratégies de sauvegarde qui seront appliquées aux machines virtuelles en cours de sauvegarde.

> [!IMPORTANT]
> Depuis mars 2017, vous ne pouvez plus utiliser le portail Classic pour créer des coffres de sauvegarde. Les coffres de sauvegarde existants sont toujours pris en charge, et il est possible [d’utiliser Azure PowerShell pour créer des coffres de sauvegarde](./backup-client-automation-classic.md#create-a-backup-vault). Toutefois, Microsoft vous recommande de créer des coffres Recovery Services pour tous les déploiements, car les améliorations futures s’appliquent uniquement aux coffres Recovery Services.


Cette image illustre les relations entre les différentes entités de sauvegarde Azure : ![Entités et relations de la Sauvegarde Azure](./media/backup-azure-vms-prepare/vault-policy-vm.png)



## <a name="network-connectivity"></a>Connectivité réseau
Afin de gérer les instantanés de la machine virtuelle, l’extension de sauvegarde nécessite une connectivité vers les adresses IP publiques Azure. Sans une bonne connectivité Internet, les requêtes HTTP de la machine virtuelle expirent et l’opération de sauvegarde échoue. Si votre déploiement comporte des restrictions d’accès (via un groupe de sécurité réseau (NSG), par exemple), choisissez l’une de ces options pour fournir un chemin clair pour le trafic de sauvegarde :

* [Mettez sur liste approuvée les plages d’adresses IP des centres de données Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) : consultez l’article pour obtenir des instructions sur la mise sur liste blanche des adresses IP.
* Déployer un serveur de proxy HTTP pour acheminer le trafic.

Lors du choix de l’option à utiliser, le compromis se situe entre la facilité de gestion, le contrôle granulaire et le coût.

| Option | Avantages | Inconvénients |
| --- | --- | --- |
| Plages IP de liste blanche |Aucun coût supplémentaire<br><br>Pour l’ouverture d’accès à un groupe de sécurité réseau, utilisez l’applet de commande <i>Set-AzureNetworkSecurityRule</i>. |Difficile à gérer, car les plages IP concernées changent au fil du temps.<br><br>Fournit un accès à l’ensemble d’Azure et pas seulement au stockage. |
| Serveur proxy HTTP |Contrôle granulaire dans le proxy sur les URL de stockage autorisées. Pour configurer un contrôle granulaire dans le proxy, le modèle d’URL https://\*.blob.core.windows.net/\* doit figurer dans la liste approuvée. Pour ajouter à la liste approuvée uniquement le compte de stockage utilisé par la machine virtuelle, le modèle d’URL https://\<storageAccount\>.blob.core.windows.net/\* doit figurer dans la liste approuvée. <br>Un seul point d’accès Internet aux machines virtuelles.<br>Non soumis aux modifications d’adresse IP Azure. |Frais supplémentaires d’exécution de machine virtuelle avec le logiciel de serveur proxy. |

### <a name="whitelist-the-azure-datacenter-ip-ranges"></a>Mettez sur liste approuvée les plages IP du centre de données Azure
Pour mettre sur liste approuvée les plages d’adresses IP des centres de données Azure, mais aussi obtenir plus d’informations sur les plages d’adresses IP et des instructions, voir le [site web Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) .

### <a name="using-an-http-proxy-for-vm-backups"></a>Utilisation d’un proxy HTTP pour les sauvegardes de machine virtuelle
Lorsque vous sauvegardez une machine virtuelle, l’extension de sauvegarde sur la machine virtuelle envoie les commandes de gestion de capture instantanée vers le stockage Azure à l’aide d’une API HTTPS. Acheminez le trafic de l’extension de sauvegarde via le proxy HTTP, car c’est le seul composant configuré pour l’accès à l’Internet public.

> [!NOTE]
> Il n’existe aucune recommandation pour le logiciel de serveur proxy qui doit être utilisé. Assurez-vous de choisir un proxy qui présente une adhérence sortante et qui est compatible avec les étapes de configuration ci-dessous. Vérifiez que les logiciels tiers ne modifient pas les paramètres de proxy.
>
>

L’image de l’exemple ci-dessous montre les trois étapes de configuration nécessaire pour utiliser un proxy HTTP :

* La machine virtuelle d’application achemine tout le trafic HTTP pour l’Internet public via la machine virtuelle proxy.
* La machine virtuelle proxy autorise le trafic entrant à partir de machines virtuelles sur le réseau virtuel.
* Le groupe de sécurité réseau (NSG) nommé NSF-lockdown a besoin d’une règle de sécurité autorisant le trafic Internet sortant à partir de la machine virtuelle proxy.

![Groupe de sécurité réseau avec diagramme de déploiement du proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

Pour utiliser un proxy HTTP pour communiquer avec le réseau Internet public, procédez comme suit :

#### <a name="step-1-configure-outgoing-network-connections"></a>Étape 1. Configurer les connexions réseau sortantes
###### <a name="for-windows-machines"></a>Pour les machines Windows
Cela définit la configuration du serveur proxy pour le compte système local.

1. Téléchargez [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Exécutez la commande suivante à partir de l’invite de commandes avec élévation de privilèges.

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Une fenêtre Internet Explorer s’ouvre.
3. Accédez à Outils -> Options Internet -> Connexions -> Paramètres réseau.
4. Vérifiez les paramètres de proxy pour le compte système. Définissez l’adresse IP et le port de proxy.
5. Fermez Internet Explorer.

Cela permet d’installer une configuration de proxy au niveau de l’ordinateur et de l’utiliser pour le trafic HTTP/HTTPS sortant.

Si vous avez configuré un serveur proxy sur un compte d’utilisateur actuel (pas un compte système local), utilisez le script suivant pour les appliquer à SYSTEMACCOUNT :

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
Ajoutez la ligne suivante au fichier ```/etc/environment``` :

```
http_proxy=http://<proxy IP>:<proxy port>
```

Ajoutez les lignes suivantes au fichier ```/etc/waagent.conf``` :

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-the-proxy-server"></a>Étape 2. Autoriser les connexions entrantes sur le serveur proxy :
1. Ouvrez le Pare-feu Windows sur le serveur proxy. Pour accéder au pare-feu, le plus simple consiste à rechercher le Pare-feu Windows avec fonctions de sécurité avancées.

    ![Ouvrir le pare-feu](./media/backup-azure-vms-prepare/firewall-01.png)
2. Dans la boîte de dialogue Pare-feu Windows, cliquez avec le bouton droit sur **Règles de trafic entrant**, puis cliquez sur **Nouvelle règle...**.

    ![Créer une nouvelle règle](./media/backup-azure-vms-prepare/firewall-02.png)
3. Dans l’**Assistant Nouvelle règle de trafic entrant**, choisissez l’option **personnalisée** comme **Type de règle**, puis cliquez sur **Suivant**.
4. Dans la page servant à sélectionner le **programme**, choisissez **Tous les programmes**, puis cliquez sur **Suivant**.
5. Dans la page **Protocole et ports**, entrez les informations suivantes, puis cliquez sur **Suivant** :

    ![Créer une nouvelle règle](./media/backup-azure-vms-prepare/firewall-03.png)

   * Pour *Type de protocole*, choisissez *TCP*.
   * Pour *Port local*, choisissez *Ports spécifiques* et dans le champ situé en dessous, spécifiez le ```<Proxy Port>``` qui a été configuré.
   * Pour *Port distant*, sélectionnez *Tous les ports*.

     Pour le reste de l’Assistant, cliquez jusqu’à la fin et donnez un nom à cette règle.

#### <a name="step-3-add-an-exception-rule-to-the-nsg"></a>Étape 3. Ajouter une règle d’exception au groupe de sécurité réseau :
Dans une invite de commandes Azure PowerShell, saisissez la commande suivante :

La commande suivante ajoute une exception pour le groupe de sécurité réseau. Cette exception autorise le trafic TCP à partir d’un port 10.0.0.5 de n’importe quelle adresse Internet sur le port 80 (HTTP) ou 443 (HTTPS). Si vous avez besoin d’un port spécifique de l’Internet public, n’oubliez pas d’ajouter également ce port à ```-DestinationPortRange``` .

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```

*Veillez à remplacer les noms dans l’exemple par les détails correspondant à votre déploiement.*

## <a name="vm-agent"></a>Agent VM
Avant de sauvegarder la machine virtuelle Azure, vérifiez que l’agent de machine virtuelle Azure est correctement installé sur la machine virtuelle. L’agent de machine virtuelle étant un composant facultatif au moment de la création de la machine virtuelle, vérifiez que la case de l’agent de machine virtuelle est cochée avant d’approvisionner la machine virtuelle.

### <a name="manual-installation-and-update"></a>Installation et mise à jour manuelles
L’agent de machine virtuelle est déjà présent dans les machines virtuelles créées à partir de la galerie Azure. Cependant, les machines virtuelles migrées à partir de centres de données locaux n’ont pas d’agent de machine virtuelle. Pour ces machines virtuelles, l’agent de machine virtuelle doit être installé de manière explicite. Pour en savoir plus, consultez la page [Installation de l’agent de machine virtuelle sur une machine virtuelle existante](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

| **Opération** | **Windows** | **Linux** |
| --- | --- | --- |
| Installation de l’agent de machine virtuelle |<li>Téléchargez et installez le fichier [MSI de l’agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Vous aurez besoin de privilèges d’administrateur pour terminer l’installation. <li>[Mettez à jour la propriété de la machine virtuelle](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) pour indiquer que l’agent est installé. |<li> Installez l’ [agent Linux](https://github.com/Azure/WALinuxAgent) le plus récent à partir de GitHub. Vous aurez besoin de privilèges d’administrateur pour terminer l’installation. <li> [Mettez à jour la propriété de la machine virtuelle](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) pour indiquer que l’agent est installé. |
| Mise à jour de l’agent de machine virtuelle |La mise à jour de l’agent de machine virtuelle est aussi simple que la réinstallation des [fichiers binaires de l’agent de machine virtuelle](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br><br>Vérifiez qu’aucune opération de sauvegarde n’est en cours pendant la mise à jour de l’agent de machine virtuelle. |Suivez les instructions fournies dans l’article [Mise à jour d’un agent de machine virtuelle Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br><br>Vérifiez qu’aucune opération de sauvegarde n’est en cours pendant la mise à jour de l’agent de machine virtuelle. |
| Validation de l’installation de l’agent de machine virtuelle |<li>Accédez au dossier *C:\WindowsAzure\Packages* sur la machine virtuelle Azure. <li>Le fichier WaAppAgent.exe doit être présent.<li> Cliquez avec le bouton droit sur le fichier, accédez à **Propriétés**, puis sélectionnez l’onglet **Détails**. Le champ Version du produit doit être défini sur 2.6.1198.718 ou une version ultérieure. |N/A |

En savoir plus sur [l’agent de machine virtuelle](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) et [comment l’installer](https://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/).

### <a name="backup-extension"></a>Extension de sauvegarde
Pour sauvegarder la machine virtuelle, le service Azure Backup installe une extension vers l’agent de machine virtuelle. Le service Azure Backup met à niveau et corrige en toute transparence l'extension de sauvegarde sans intervention supplémentaire de l'utilisateur.

L’extension de sauvegarde est installée si la machine virtuelle est en cours de fonctionnement. Une machine virtuelle en cours d’exécution présente également le plus de chance d’obtenir un point de récupération d’application cohérent. Toutefois, le service Azure Backup poursuit la sauvegarde de la machine virtuelle, même si elle est éteinte et si l’extension n’a pas été installée (c’est-à-dire, si la machine virtuelle est hors connexion). Dans ce cas, le point de récupération est *cohérent suite à l’incident* comme indiqué ci-dessus.

## <a name="questions"></a>Des questions ?
Si vous avez des questions ou si vous souhaitez que certaines fonctionnalités soient incluses, [envoyez-nous vos commentaires](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Étapes suivantes
À présent que votre environnement est prêt pour sauvegarder votre machine virtuelle, l’étape logique suivante consiste à créer une sauvegarde. L’article sur la planification fournit des informations détaillées sur la sauvegarde des machines virtuelles.

* [Sauvegarde de machines virtuelles](backup-azure-vms.md)
* [Planification de votre infrastructure de sauvegarde de machines virtuelles](backup-azure-vms-introduction.md)
* [Gestion des sauvegardes de machines virtuelles](backup-azure-manage-vms.md)
