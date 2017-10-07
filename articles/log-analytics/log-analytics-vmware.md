---
title: aaaVMware solution de surveillance dans le journal Analytique | Documents Microsoft
description: "Découvrez comment hello solution d’analyse de VMware peut aider à gérer les journaux et de surveiller des ordinateurs hôtes ESXi."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 16516639-cc1e-465c-a22f-022f3be297f1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: 959d5c2201fc5c7947f8b8870d055cdf9eea8e01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vmware-monitoring-preview-solution-in-log-analytics"></a>Solution Analyse VMware (version préliminaire) dans Log Analytics

![Symbole VMware](./media/log-analytics-vmware/vmware-symbol.png)

Hello solution d’analyse de VMware dans Analytique de journal est une solution qui vous permet de créer une approche de l’analyse pour des journaux de VMware et de journalisation centralisée. Cet article décrit comment vous pouvez résoudre les problèmes, capturer et gérer les ordinateurs hôtes ESXi hello dans un emplacement unique à l’aide de la solution de hello. Avec la solution de hello, vous pouvez voir les données détaillées pour tous les hôtes ESXi dans un emplacement unique. Vous pouvez voir le nombre d’événements supérieur, l’état et les tendances des hôtes de machine virtuelle et ESXi fournis via les journaux de l’hôte ESXi hello. Vous pouvez résoudre des problèmes en consultant des journaux d’hôte ESXi centralisés et en y effectuant des recherches. Et vous pouvez créer des alertes basées sur des requêtes de recherche de journal.

solution de Hello utilise des fonctionnalités syslog native de hello ESXi hôte toopush tooa cible des données machine virtuelle, qui a l’Agent OMS. Toutefois, les solutions hello n’écrivent les fichiers dans syslog au sein de la cible de hello machine virtuelle. agent d’OMS Hello ouvre le port 1514 et écoute toothis. Une fois qu’il reçoit des données de hello, l’agent OMS de hello pousse les données hello dans OMS.

## <a name="installing-and-configuring-hello-solution"></a>L’installation et la configuration de solution de hello
Utilisez hello suivant tooinstall des informations et configurer une solution de hello.

* Ajouter hello VMware analyse solution tooyour espace de travail OMS à l’aide du processus de hello décrit dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).

#### <a name="supported-vmware-esxi-hosts"></a>Hôtes VMware ESXi pris en charge
vSphere ESXi Host 5.5 et 6.0

#### <a name="prepare-a-linux-server"></a>Préparer un serveur Linux
Créer un tooreceive de machine virtuelle du système d’exploitation Linux toutes les données syslog à partir d’ordinateurs hôtes ESXi hello. Hello [OMS Linux Agent](log-analytics-linux-agents.md) est le point de collecte hello pour toutes les données syslog de hôte ESXi. Vous pouvez utiliser plusieurs ESXi hôtes tooforward journaux tooa Linux serveur unique, comme dans l’exemple suivant de hello.  

   ![Flux Syslog](./media/log-analytics-vmware/diagram.png)

### <a name="configure-syslog-collection"></a>Configurer la collecte Syslog
1. Configurez le transfert de Syslog à VSphere. Pour plus d’informations toohelp de configurer le transfert de syslog, consultez [configuration syslog sur ESXi 5.x et 6.0 (2003322)](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2003322). Accédez trop**Configuration de l’hôte ESXi** > **logiciel** > **paramètres avancés** > **Syslog**.
   ![vsphereconfig](./media/log-analytics-vmware/vsphere1.png)  
2. Bonjour *Syslog.global.logHost* champ, ajoutez votre numéro de port de serveur et hello Linux *1514*. Par exemple, `tcp://hostname:1514` ou `tcp://123.456.789.101:1514`.
3. Ouvrez le pare-feu d’hôte ESXi hello pour syslog. **Configuration de l’hôte ESXi** > **Logiciels** > **Profil de sécurité** > **Pare-feu**, puis ouvrez **Propriétés**.  

    ![vspherefw](./media/log-analytics-vmware/vsphere2.png)  

    ![vspherefwproperties](./media/log-analytics-vmware/vsphere3.png)  
4. Vérifiez hello vSphere Console tooverify que ce syslog est correctement configuré. Confirmation sur hello ESXI héberger ce port **1514** est configuré.
5. Téléchargez et installez hello Agent OMS pour Linux sur un serveur Linux de hello. Pour plus d’informations, consultez hello [Documentation de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux).
6. Une fois hello Agent OMS pour Linux est installé, accédez toohello /etc/opt/microsoft/omsagent/sysconf/omsagent.d active et hello vmware_esxi.conf fichier toohello /etc/opt/microsoft/omsagent/conf/omsagent.d répertoire et hello hello propriétaire/groupe de modifications et les autorisations du fichier de hello. Par exemple :

    ```
    sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/vmware_esxi.conf /etc/opt/microsoft/omsagent/conf/omsagent.d
   sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf
    ```
7. Redémarrez hello Agent OMS pour Linux en exécutant `sudo /opt/microsoft/omsagent/bin/service_control restart`.
8. Tester la connectivité des hello entre le serveur de Linux hello et hôte ESXi de hello à l’aide de hello `nc` commande hello hôte ESXi. Par exemple :

    ```
    [root@ESXiHost:~] nc -z 123.456.789.101 1514
    Connection too123.456.789.101 1514 port [tcp/*] succeeded!
    ```

9. Bonjour portail OMS, effectuer une recherche de journal de `Type=VMware_CL`. Lorsque OMS collecte les données syslog hello, il conserve le format de syslog hello. Dans le portail hello, certains des champs spécifiques sont capturées, tel que *nom d’hôte* et *ProcessName*.  

    ![type](./media/log-analytics-vmware/type.png)  

    Si vos résultats de recherche de journal de vue sont similaires image toohello ci-dessus, vous êtes prêt toouse hello VMware d’OMS analyse solution du tableau de bord.  

## <a name="vmware-data-collection-details"></a>Détails sur la collecte de données Linux
Hello solution d’analyse de VMware collecte diverses données de journaux et des métriques de performances à partir d’ordinateurs hôtes ESXi à l’aide de hello les Agents OMS pour Linux que vous avez activé.

Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées.

| plateforme | Agent OMS pour Linux | Agent SCOM | Stockage Azure | SCOM requis ? | Données de l’agent SCOM envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Linux |&#8226; |  |  |  |  |Toutes les 3 minutes. |

Hello tableau présentent des exemples de champs de données collectées par hello solution d’analyse de VMware :

| Nom du champ | Description |
| --- | --- |
| Device_s |appareils de stockage VMware |
| ESXIFailure_s |types d’échec |
| EventTime_t |heure à laquelle l’événement s’est produit |
| HostName_s |nom d’hôte ESXi |
| Operation_s |créer ou supprimer une machine virtuelle |
| ProcessName_s |nom de l’événement |
| ResourceId_s |nom de l’ordinateur hôte VMware hello |
| ResourceLocation_s |VMware |
| ResourceName_s |VMware |
| ResourceType_s |Hyper-V |
| SCSIStatus_s |Statut SCSI de VMware |
| SyslogMessage_s |données Syslog |
| UserName_s |utilisateur qui a créé ou supprimé la machine virtuelle |
| VMName_s |nom de la machine virtuelle |
| Ordinateur |ordinateur hôte |
| TimeGenerated |données hello du temps a été générées. |
| DataCenter_s |centre de données VMware |
| StorageLatency_s |latence de stockage (ms) |

## <a name="vmware-monitoring-solution-overview"></a>Présentation de la solution Analyse VMware
vignette de VMware Hello s’affiche dans hello portail OMS. Elle fournit une vue d’ensemble des erreurs. Lorsque vous cliquez sur la vignette de hello, vous passez dans un affichage tableau de bord.

![vignette](./media/log-analytics-vmware/tile.png)

#### <a name="navigate-hello-dashboard-view"></a>Naviguer dans Affichage de tableau de bord hello
Bonjour **VMware** affichage tableau de bord, les panneaux est organisés par :

* Nombre d’états d’échec
* Hôte principal par nombre d’événements
* Nombres d’événements principaux
* Activités de machine virtuelle
* Événements de disque de l’hôte ESXi

![solution1](./media/log-analytics-vmware/solutionview1-1.png)

![solution2](./media/log-analytics-vmware/solutionview1-2.png)

Cliquez sur n’importe quel tooopen panneau volet de recherche Analytique de journal qui affiche des informations détaillées spécifiques pour les lames hello.

À ce stade, vous pouvez modifier toomodify de requête de recherche hello pour un élément spécifique. Pour un didacticiel sur les principes fondamentaux de hello de recherche d’OMS, consultez hello [didacticiel de recherche de journal OMS.](log-analytics-log-searches.md)

#### <a name="find-esxi-host-events"></a>Rechercher des événements de l’hôte ESXi
Un seul hôte ESXi génère plusieurs journaux basés sur leurs processus. Hello solution d’analyse de VMware centralise les et résume le nombre d’événements hello. Cette vue centralisée vous permet de comprendre quel hôte ESXi a un volume élevé d’événements ainsi que les événements qui se produisent le plus fréquemment dans votre environnement.

![événement](./media/log-analytics-vmware/events.png)

Vous pouvez approfondir davantage en cliquant sur un hôte ESXi ou un type d’événement.

Lorsque vous cliquez sur un nom d’hôte ESXi, vous voyez les informations de cet hôte ESXi. Si vous souhaitez que les résultats de toonarrow avec le type d’événement hello, ajoutez `“ProcessName_s=EVENT TYPE”` dans votre requête de recherche. Vous pouvez sélectionner **ProcessName** dans le filtre de recherche hello. Qui restreint les informations hello pour vous.

![explorer](./media/log-analytics-vmware/eventhostdrilldown.png)

#### <a name="find-high-vm-activities"></a>Rechercher les activités de machine virtuelle élevées
Une machine virtuelle peut être créée et supprimée sur tout hôte ESXi. Il est utile pour un administrateur tooidentify le nombre de machines virtuelles un hôte ESXi crée. Qui à leur tour, vous aide à toounderstand performances et planification de capacité. Il est essentiel de suivre les événements d’activité de machine virtuelle lors de la gestion de votre environnement.

![explorer](./media/log-analytics-vmware/vmactivities1.png)

Si vous souhaitez que toosee supplémentaires ESXi hôte de données de création de machine virtuelle, cliquez sur un nom d’hôte ESXi.

![explorer](./media/log-analytics-vmware/createvm.png)

#### <a name="common-search-queries"></a>Requêtes de recherche courantes
solution de Hello inclut des autres requêtes utiles qui peuvent vous aider à gérer vos ordinateurs hôtes ESXi, telles que l’espace de stockage élevé, latence de stockage et d’échec de chemin d’accès.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![queries](./media/log-analytics-vmware/queries.png)


#### <a name="save-queries"></a>Enregistrer des requêtes
L’enregistrement des requêtes de recherche est une fonctionnalité standard dans OMS, qui peut vous aider à conserver toutes les requêtes que vous avez trouvées utiles. Après avoir créé une requête qui vous être utiles, enregistrez-le en cliquant sur hello **favoris**. Une requête enregistrée vous permet de facilement le réutiliser plus tard à partir de hello [mon tableau de bord](log-analytics-dashboards.md) page où vous pouvez créer vos propres tableaux de bord personnalisés.

![DockerDashboardView](./media/log-analytics-vmware/dockerdashboardview.png)

#### <a name="create-alerts-from-queries"></a>Créer des alertes à partir de requêtes
Une fois que vous avez créé vos requêtes, vous souhaiterez peut-être toouse hello requêtes tooalert lorsque des événements spécifiques se produisent. Consultez [alertes dans le journal Analytique](log-analytics-alerts.md) pour plus d’informations sur la façon toocreate alertes. Pour obtenir des exemples de requêtes et autres exemples de requête des alertes, consultez hello [VMware d’analyse à l’aide d’Analytique des journaux OMS](https://blogs.technet.microsoft.com/msoms/2016/06/15/monitor-vmware-using-oms-log-analytics) billet de blog.

## <a name="frequently-asked-questions"></a>Forum Aux Questions
### <a name="what-do-i-need-toodo-on-hello-esxi-host-setting-what-impact-will-it-have-on-my-current-environment"></a>De quoi ai-je besoin toodo sur le paramètre de l’hôte ESXi hello ? Quel sera l’impact sur mon environnement actuel ?
solution de Hello utilise mécanisme de transfert hello natif ESXi hôte Syslog. Vous n’avez pas besoin des logiciels Microsoft supplémentaires sur les journaux de hello hôte ESXi toocapture hello. Il doit avoir un environnement existant de faible impact tooyour. Toutefois, vous avez besoin de transfert tooset syslog, ce qui est une fonctionnalité ESXI.

### <a name="do-i-need-toorestart-my-esxi-host"></a>Dois-je toorestart mon hôte ESXi ?
Non. Ce processus ne nécessite pas de redémarrage. Parfois, vSphere n’est pas correctement actualisée hello syslog. Dans ce cas, ouvrez une session sur l’ordinateur hôte de toohello ESXi et recharger hello syslog. Là encore, vous n’avez toorestart hôte de hello, donc ce processus n’est pas tooyour perturbateur environnement.

### <a name="can-i-increase-or-decrease-hello-volume-of-log-data-sent-toooms"></a>Puis-je augmenter ou baisser le volume de données de journaux envoyés tooOMS hello ?
Oui, vous pouvez. Vous pouvez utiliser les paramètres de niveau de journal hôte ESXi hello dans vSphere. Collecte des journaux est basée sur hello *info* niveau. Par conséquent, si vous souhaitez tooaudit création d’ordinateurs virtuels ou de suppression, vous devez tookeep hello *info* niveau sur Hôted. Pour plus d’informations, consultez hello [Base de connaissances VMware](https://kb.vmware.com/selfservice/microsites/search.do?&cmd=displayKC&externalId=1017658).

### <a name="why-is-hostd-not-providing-data-toooms-my-log-setting-is-set-tooinfo"></a>Pourquoi Hôted fournit pas les données tooOMS ? Paramètre du journal a la valeur tooinfo.
Un bogue d’hôte ESXi pour hello syslog timestamp s’est produite. Pour plus d’informations, consultez hello [Base de connaissances VMware](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2111202). Après avoir appliqué la solution de contournement hello, Hôted doit fonctionner normalement.

### <a name="can-i-have-multiple-esxi-hosts-forwarding-syslog-data-tooa-single-vm-with-omsagent"></a>Puis-je avoir plusieurs ESXi hôtes transfert syslog données tooa unique machine virtuelle avec omsagent ?
Oui. Vous pouvez avoir plusieurs ESXi hôtes transfert tooa unique machine virtuelle avec omsagent.

### <a name="why-dont-i-see-data-flowing-into-oms"></a>Pourquoi ne puis-je pas voir les données échangées avec OMS ?
Il peut y avoir plusieurs raisons :

* hôte ESXi de Hello n’est pas correctement envoyant données toohello machine virtuelle en cours d’exécution omsagent. tootest, effectuer hello comme suit :

  1. tooconfirm, ouvrez une session sur l’ordinateur hôte ESXi de toohello à l’aide de ssh et exécutez hello de commande suivante :`nc -z ipaddressofVM 1514`

      Si cela n’a pas réussi, les paramètres vSphere Bonjour Configuration avancée sont probablement pas corrigé. Consultez [configurer la collecte de syslog](#configure-syslog-collection) pour plus d’informations sur comment tooset des hello ESXi hôte pour le transfert de syslog.
  2. Si la connectivité des ports syslog a réussi, mais vous ne voyez toujours pas toutes les données, puis rechargez syslog hello sur l’ordinateur hôte de hello ESXi à l’aide de ssh hello toorun commande suivante :` esxcli system syslog reload`
* Hello machine virtuelle avec l’Agent OMS n’est pas défini correctement. tootest, effectuer hello comme suit :

  1. OMS écoute le port toohello 1514 et transmet des données à OMS. tooverify qu’il est ouvert, exécutez hello de commande suivante :`netstat -a | grep 1514`
  2. Vous devez voir le port `1514/tcp` ouvert. Si vous ne le faites pas, vérifiez qu’omsagent hello est correctement installé. Si vous ne voyez pas les informations de port hello, port syslog de hello n’est pas ouvert sur hello machine virtuelle.

     1. Vérifiez que hello OMS Agent est en cours d’exécution à l’aide de `ps -ef | grep oms`. Si elle n’est pas en cours d’exécution, lancer hello en exécutant la commande hello` sudo /opt/microsoft/omsagent/bin/service_control start`
     2. Ouvrez hello `/etc/opt/microsoft/omsagent/conf/omsagent.d/vmware_esxi.conf` fichier.

         Vérifiez que l’utilisateur hello et paramètre de groupe est valide, comme dans :`-rw-r--r-- 1 omsagent omiusers 677 Sep 20 16:46 vmware_esxi.conf`

         Si le fichier de hello ou n’existe pas hello utilisateur et le paramètre de groupe est incorrect, prendre une action corrective par [préparation d’un serveur Linux](#prepare-a-linux-server).

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [recherches de journal](log-analytics-log-searches.md) dans le journal Analytique tooview détaillées des données de l’hôte VMware.
* [Créer vos propres tableaux de bord](log-analytics-dashboards.md) affichant des données de l’hôte VMware.
* [Créer des alertes](log-analytics-alerts.md) lorsque des événements d’hôte VMware spécifiques se produisent.
