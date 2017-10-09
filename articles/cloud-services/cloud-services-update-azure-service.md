---
title: aaaHow tooupdate un service cloud | Documents Microsoft
description: "Découvrez comment tooupdate cloud services dans Azure. Découvrez comment une mise à jour sur un service cloud poursuit tooensure disponibilité."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c6a8b5e6-5c99-454c-9911-5c7ae8d1af63
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 7e4c8bd46e51a555b4309ea8927d120e8efcf0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-a-cloud-service"></a>Comment tooupdate un service cloud

La mise à jour d’un service cloud, et notamment de ses rôles et du système d’exploitation invité, est un processus qui se déroule en trois étapes. Tout d’abord, fichiers binaires de hello et les fichiers de configuration pour hello nouveau service de cloud computing ou version du système d’exploitation doit être téléchargée. Ensuite, Azure réserve de ressources de calcul et de réseau pour le service cloud hello selon les besoins de la nouvelle version de service cloud hello hello. Enfin, Azure effectue une propagée mise à niveau tooincrementally mise à jour hello client toohello nouvelle version ou invité du système d’exploitation, tout en conservant la disponibilité de votre. Cet article décrit en détail hello de cette dernière étape : hello mise à niveau propagée.

## <a name="update-an-azure-service"></a>Mettre à jour un Service Azure
Azure organise vos instances de rôle en regroupements logiques appelés domaines de mise à niveau (UD). Les domaines de mise à niveau (UD) sont des ensembles logiques d’instances de rôle qui sont mis à jour en tant que groupe.  Azure mises à jour un cloud service un UD à la fois, ce qui permet aux instances dans les autres toocontinue domaines d’erreur desservant le trafic.

nombre de domaines de mise à niveau par défaut de Hello est 5. Vous pouvez spécifier un nombre différent de domaines de mise à niveau en incluant l’attribut d’upgradeDomainCount hello dans le fichier de définition du service hello (.csdef). Pour plus d’informations sur l’attribut d’upgradeDomainCount hello, consultez [WebRole schéma](https://msdn.microsoft.com/library/azure/gg557553.aspx) ou [WorkerRole schéma](https://msdn.microsoft.com/library/azure/gg557552.aspx).

Lorsque vous effectuez une mise à jour sur place d’un ou plusieurs rôles dans votre service, Azure met à jour les jeux d’instances de rôle en fonction de toohello toowhich de domaine de mise à niveau qu'auquel ils appartiennent. Azure mises à jour toutes les instances de hello dans un domaine de mise à niveau donné – les arrêter, les mettre à jour, les réafficher de sauvegarde en ligne – déplace ensuite sur le domaine suivant de hello. En arrêtant les seules instances hello en hello actuelle mise à niveau de domaine, Azure permet de s’assurer qu’une mise à jour se produit avec hello minimales toohello d’impact sur le service en cours d’exécution. Pour plus d’informations, consultez [l’exécution de mise à jour hello](#howanupgradeproceeds) plus loin dans cet article.

> [!NOTE]
> Alors que les termes du contrat de hello **mettre à jour** et **mise à niveau** ont une signification légèrement différente dans le contexte de hello Azure, ils peuvent être utilisées indifféremment pour les processus hello et les descriptions des fonctionnalités hello dans ce document.
>
>

Votre service doit définir au moins deux instances d’un rôle pour ce rôle toobe mis à jour sur place sans interruption de service. Si le service de hello se compose d’une seule instance d’un rôle, votre service n’est pas disponible tant que hello mise à jour sur place est terminée.

Cette rubrique couvre hello d’informations sur les mises à jour Azure suivantes :

* [Modifications de service autorisées pendant une mise à jour](#AllowedChanges)
* [Déroulement d’une mise à niveau](#howanupgradeproceeds)
* [Restauration d’une mise à jour](#RollbackofanUpdate)
* [Lancement de plusieurs opérations de mutation sur un déploiement en cours](#multiplemutatingoperations)
* [Distribution des rôles entre domaines de mise à niveau](#distributiondfroles)

<a name="AllowedChanges"></a>

## <a name="allowed-service-changes-during-an-update"></a>Modifications de service autorisées pendant une mise à jour
Hello tableau suivant montre hello autorisé modifications tooa service pendant une mise à jour :

| Modifications autorisées toohosting, services et des rôles | Mise à jour sur place | Intermédiaire (échange d’adresses IP virtuelles) | Supprimer et redéployer |
| --- | --- | --- | --- |
| Version de système d’exploitation |Oui |Oui |Oui |
| Niveau de confiance .NET |Oui |Oui |Oui |
| Taille de la machine virtuelle<sup>1</sup> |Oui<sup>2</sup> |Oui |Oui |
| Paramètres de stockage locaux |Augmentation uniquement<sup>2</sup> |Oui |Oui |
| Ajouter et supprimer les rôles dans un service |Oui |Oui |Oui |
| Nombre d’instances d’un rôle particulier |Oui |Oui |Oui |
| Nombre ou type de points de terminaison pour un service |Oui<sup>2</sup> |Non |Oui |
| Noms et valeurs de paramètres de configuration |Oui |Oui |Oui |
| Valeurs (et non noms) des paramètres de configuration |Oui |Oui |Oui |
| Ajouter de nouveau certificats |Oui |Oui |Oui |
| Modifier les certificats existants |Oui |Oui |Oui |
| Déployer un nouveau code |Oui |Oui |Oui |

<sup>1</sup> changement de taille limitée sous-ensemble toohello des tailles disponibles pour le service cloud hello.

<sup>2</sup> Nécessite le kit de développement logiciel (SDK) Azure 1.5 ou versions ultérieures.

> [!WARNING]
> Modification de la taille de machine virtuelle hello détruira les données locales.
>
>

Hello éléments suivants n’est pas pris en charge pendant une mise à jour :

* Changement de nom hello d’un rôle. Supprimez, puis ajoutez rôle hello avec le nouveau nom de hello.
* Modification de hello nombre de domaines de mise à niveau.
* Diminution de la taille de hello des ressources locales de hello.

Si vous apportez des autres mises à jour de définition du service tooyour, tels que la diminution de la taille de hello de ressource locale, vous devez effectuer une mise à jour d’échange de VIP à la place. Pour plus d’informations, consultez [Déploiement d’échange](https://msdn.microsoft.com/library/azure/ee460814.aspx).

<a name="howanupgradeproceeds"></a>

## <a name="how-an-upgrade-proceeds"></a>Déroulement d’une mise à niveau
Vous pouvez décider si vous souhaitez que tooupdate tous les rôles hello dans votre service ou un rôle unique dans le service hello. Dans les deux cas, toutes les instances de chaque rôle qui est en cours de mise à niveau et appartiennent toohello premier domaine de mise à niveau sont arrêtés, mis à niveau et remis en ligne. Une fois qu’ils sont en ligne, hello instances dans le deuxième domaine de mise à niveau hello sont arrêtés, mis à niveau et remis en ligne. Un service cloud peut avoir au plus une mise à niveau active à la fois. mise à niveau Hello est toujours effectuée par rapport à la version la plus récente du service de cloud hello hello.

Hello diagramme suivant illustre comment la mise à niveau hello se poursuit si vous mettez à niveau tous les rôles hello dans le service hello :

![Mettre à niveau le service](media/cloud-services-update-azure-service/IC345879.png "Mettre à niveau le service")

Le diagramme suivant montre comment la mise à jour hello se poursuit si vous mettez à niveau un seul rôle :

![Mettre à niveau le rôle](media/cloud-services-update-azure-service/IC345880.png "Mettre à niveau le rôle")  

Pendant une mise à jour automatique, hello contrôleur de structure Azure évalue périodiquement intégrité hello hello cloud service toodetermine lors de son toowalk safe hello UD suivant. Cette évaluation d’intégrité est effectuée sur une base par rôle et considère que les instances dans la version la plus récente hello (autrement dit, les instances à partir de domaines d’erreur qui ont déjà été parcourues). Il vérifie qu’un nombre minimum d’instances de rôle, pour chaque rôle, a atteint un état terminal satisfaisant.

### <a name="role-instance-start-timeout"></a>Délai de démarrage de l’instance de rôle
Contrôleur de structure de Hello attendra 30 minutes pour chaque tooreach d’instance de rôle un état démarré. Si la durée du délai d’attente hello s’écoule, hello contrôleur de structure continuera de parcours toohello suivant instance de rôle.

### <a name="impact-toodrive-data-during-cloud-service-upgrades"></a>Données d’impact toodrive pendant les mises à niveau de Service Cloud

Lors de la mise à niveau d’un service à partir d’une instance de toomultiple instance unique votre service sera réduit pendant la mise à niveau hello est effectuée en raison de la façon de toohello Qu'azure met à niveau les services. Hello service contrat de niveau garantissant la disponibilité s’applique uniquement à tooservices qui sont déployés avec plusieurs instances. Hello liste suivante décrit comment les données de hello sur chaque disque sont affectées par chaque scénario de mise à niveau de service Azure :

|Scénario|Lecteur C|Lecteur D|Lecteur E|
|--------|-------|-------|-------|
|Redémarrage de la machine virtuelle|Préservé|Préservé|Préservé|
|Redémarrage du portail|Préservé|Préservé|Détruit|
|Réinitialisation du portail|Préservé|Détruit|Détruit|
|Mise à niveau sur place|Préservé|Préservé|Détruit|
|Migration des nœuds|Détruit|Détruit|Détruit|

Notez que, dans hello au-dessus de liste, hello lecteur E: représente le lecteur racine du rôle hello et ne doit pas être codées en dur. Au lieu de cela, utilisez hello **%roleroot%** lecteur de hello toorepresent variable environnement.

temps d’arrêt hello toominimize lors de la mise à niveau d’un service à instance unique, déployez un nouveau serveur à plusieurs instances service toohello intermédiaire et effectuez un échange d’adresses IP virtuelles.

<a name="RollbackofanUpdate"></a>

## <a name="rollback-of-an-update"></a>Restauration d’une mise à jour
Azure fournit une grande souplesse dans la gestion des services pendant une mise à jour en vous permettant de lancer des opérations supplémentaires sur un service, une fois la demande de mise à jour initiale hello est accepté par le contrôleur de structure Azure de hello. Une restauration peut être effectuée uniquement quand une mise à jour (modification de la configuration) ou de mise à niveau est Bonjour **en cours d’exécution** état sur le déploiement de hello. Toobe en cours est considéré comme une mise à jour ou la mise à niveau, tant qu’il existe au moins une instance de service hello qui n’a pas encore été mis à jour toohello nouvelle version. tootest si une restauration est autorisée, vérifiez la valeur hello d’indicateur de RollbackAllowed hello, retourné par [obtenir le déploiement](https://msdn.microsoft.com/library/azure/ee460804.aspx) et [obtenir les propriétés de Service Cloud](https://msdn.microsoft.com/library/azure/ee460806.aspx) opérations, a la valeur tootrue.

> [!NOTE]
> Qu’il est judicieux toocall Rollback sur une **in situ** mettre à jour ou de mise à niveau, car l’adresse IP virtuelle impliquent de remplacer une instance en cours d’exécution complète de votre service avec un autre.
>
>

Restauration d’une mise à jour en cours a hello suivant les effets sur le déploiement de hello :

* Toutes les instances de rôle qui n’avaient pas encore été mis à jour ou mise à niveau toohello nouvelle version ne sont pas mis à jour ou mise à niveau, car ces instances sont déjà équipés hello cible du service de hello.
* Instances de n’importe quel rôle qui a déjà été mise à jour ou toohello mis à niveau une nouvelle version du package de service hello (\*.cspkg) configuration du service de fichier ou hello (\*.cscfg) fichier (ou les deux fichiers) sont toohello restaurée de pré-mise à niveau version de Ces fichiers.

Cette fonction est assurée par hello suivant de fonctionnalités :

* Hello [restauration mettre à jour ou mise à niveau](https://msdn.microsoft.com/library/azure/hh403977.aspx) opération, qui peut être appelée sur une mise à jour de configuration (déclenchée en appelant [modifier la Configuration déploiement](https://msdn.microsoft.com/library/azure/ee460809.aspx)) ou une mise à niveau (déclenchée en appelant [ Mettre à niveau un déploiement](https://msdn.microsoft.com/library/azure/ee460793.aspx)) tant qu’il existe au moins une instance de service de hello qui n’a pas encore été mis à jour toohello nouvelle version.
* Hello verrouillé élément et élément de RollbackAllowed hello, qui sont retournées en tant que partie du corps de réponse hello Hello [obtenir le déploiement](https://msdn.microsoft.com/library/azure/ee460804.aspx) et [obtenir les propriétés de Service Cloud](https://msdn.microsoft.com/library/azure/ee460806.aspx) opérations :

  1. élément verrouillé de Hello vous permet de toodetect lorsqu’une opération de mutation peut être appelée sur un déploiement donné.
  2. Hello RollbackAllowed élément vous permet de toodetect lorsque hello [restauration mise à jour ou mise à niveau](https://msdn.microsoft.com/library/azure/hh403977.aspx) opération peut être appelée sur un déploiement donné.

  Dans l’ordre tooperform une restauration, il est inutile toocheck à la fois hello verrouillé et hello RollbackAllowed éléments. Il suffit de tooconfirm que RollbackAllowed a la valeur tootrue. Ces éléments sont retournés uniquement si ces méthodes sont appelées à l’aide d’en-tête de demande de hello défini trop « x-ms-version : 2011-10-01 » ou une version ultérieure. Pour plus d’informations sur les en-têtes de contrôle de version, consultez [Contrôle de version de gestion de service](https://msdn.microsoft.com/library/azure/gg592580.aspx).

Dans certaines situations, la restauration d’une mise à jour ou d’une mise à niveau n’est pas prise en charge, notamment les suivantes :

* Réduction des ressources locales - si hello mise à jour augmente hello des ressources locales pour un rôle hello plateforme Azure n’autorise pas restaurant.
* Limitations de quota - si une mise à l’échelle vers le bas opération vous pouvez ne plus mise à jour hello n’a opération de restauration suffisante calcul quota toocomplete hello. Chaque abonnement Azure dispose d’un quota associé qui spécifie le nombre maximal de hello de cœurs qui peuvent être consommés par tous les services hébergés qui appartiennent toothat abonnement. Si l’exécution de la restauration d’une mise à jour donnée met votre abonnement au dessus du quota, la restauration ne sera pas activée.
* Condition de concurrence - si la mise à jour initiale de hello terminée, une restauration n’est pas possible.

Est d’un exemple de lorsque la restauration d’une mise à jour hello peut être utile si vous utilisez hello [mettre à niveau un déploiement](https://msdn.microsoft.com/library/azure/ee460793.aspx) opération taux de hello toocontrol mode manuel à laquelle un tooyour mise à niveau majeure sur place Azure le service hébergé est transférée.

Lors du déploiement de mise à niveau hello hello vous appelez [mettre à niveau un déploiement](https://msdn.microsoft.com/library/azure/ee460793.aspx) en mode manuel et commencez les domaines de mise à niveau toowalk. Si à un moment donné, lorsque vous analysez la mise à niveau de hello, vous notez des instances de rôle dans hello premiers domaines de mise à niveau que vous examinez sont devenues ne répond pas, vous pouvez appeler hello [restauration mise à jour ou mise à niveau](https://msdn.microsoft.com/library/azure/hh403977.aspx) opération sur le déploiement de hello, qui Pour laisser instances hello intact qui n’avaient pas encore été mis à niveau et les instances de restauration qui avaient été mis à niveau toohello précédent package de service et de configuration.

<a name="multiplemutatingoperations"></a>

## <a name="initiating-multiple-mutating-operations-on-an-ongoing-deployment"></a>Lancement de plusieurs opérations de mutation sur un déploiement en cours
Dans certains cas vous souhaiterez tooinitiate plusieurs opérations de mutation simultanées sur un déploiement en cours. Par exemple, vous pouvez effectuer une mise à jour de service et, pendant cette mise à jour est déployée sur votre service, vous toomake certaines modifications, par exemple, tooroll hello mise à jour, appliquer une autre mise à jour ou le même supprimer hello. Un cas dans lesquels il peut être nécessaire est si une mise à niveau de service contient un code bogué qui provoque un blocage de toorepeatedly instance rôle mis à niveau. Dans ce cas, hello contrôleur de structure Azure ne sera pas toomake en mesure de sa progression dans l’application de mise à niveau, car un nombre insuffisant d’instances dans le domaine de mise à niveau de hello est intègre. Cet état est tooas auxquels un *déploiement bloqué*. Vous pouvez débloquer le déploiement de hello en annulation de la mise à jour hello ou en appliquant une nouvelle mise à jour par-dessus hello un échec.

Une fois que le service hello hello demande initiale tooupdate ou mise à niveau a été reçu par hello contrôleur de structure Azure, vous pouvez démarrer des opérations de mutation suivantes. Autrement dit, vous n’avez pas les toowait pour hello opération initiale toocomplete avant de commencer une autre opération de mutation.

Initialisation d’une deuxième opération de mise à jour lors de la première mise à jour de hello est en cours effectue une opération rollback toohello similaire. Si la mise à jour de la deuxième hello est en mode automatique, hello premier domaine de mise à niveau est mis à niveau immédiatement, pouvant entraîner tooinstances à partir de plusieurs domaines de mise à niveau soient hors connexion au hello même point dans le temps.

Hello opérations de mutation sont les suivantes : [modifier la Configuration déploiement](https://msdn.microsoft.com/library/azure/ee460809.aspx), [mettre à niveau un déploiement](https://msdn.microsoft.com/library/azure/ee460793.aspx), [état de déploiement de mise à jour](https://msdn.microsoft.com/library/azure/ee460808.aspx), [supprimer Déploiement](https://msdn.microsoft.com/library/azure/ee460815.aspx), et [mise à jour de la restauration ou de mise à niveau](https://msdn.microsoft.com/library/azure/hh403977.aspx).

Deux opérations, [obtenir le déploiement](https://msdn.microsoft.com/library/azure/ee460804.aspx) et [obtenir les propriétés de Service Cloud](https://msdn.microsoft.com/library/azure/ee460806.aspx), retourne un indicateur de verrouillé hello qui peut être examiné toodetermine si une opération de mutation peut être appelée sur un déploiement donné.

Dans la commande toocall hello version de ces méthodes qui retourne hello verrouillé indicateur, vous devez définir des en-tête de demande trop « x-ms-version : 2011-10-01 » ou une version ultérieure. Pour plus d’informations sur les en-têtes de contrôle de version, consultez [Contrôle de version de gestion de service](https://msdn.microsoft.com/library/azure/gg592580.aspx).

<a name="distributiondfroles"></a>

## <a name="distribution-of-roles-across-upgrade-domains"></a>Distribution des rôles entre domaines de mise à niveau
Azure distribue uniformément les instances d’un rôle dans un nombre défini de domaines de mise à niveau, qui peuvent être configurés en tant que partie hello service (.csdef) du fichier de définition. Hello le nombre maximal de domaines de mise à niveau est 20 et par défaut de hello est 5. Pour plus d’informations sur la façon dont toomodify hello le fichier de définition de service, consultez [schéma de définition de Service Azure (fichier de .csdef)](cloud-services-model-and-package.md#csdef).

Par exemple, si votre rôle comporte dix instances, par défaut, chaque domaine de mise à niveau contient deux instances. Si votre rôle a 14 instances, quatre des domaines de mise à niveau hello contiennent trois instances, et un cinquième domaine contient deux.

Domaines de mise à niveau sont identifiés avec un index de base zéro : hello premier domaine de mise à niveau a un ID égal à 0, et deuxième domaine de mise à niveau hello possède un ID de 1 et ainsi de suite.

Hello diagramme suivant illustre comment un service qui contient deux rôles sont distribués lors du service de hello définit deux domaines de mise à niveau. service de Hello exécute huit instances de rôle web de hello et neuf instances de rôle de travail hello.

![Distribution des domaines de mise à niveau](media/cloud-services-update-azure-service/IC345533.png "Distribution des domaines de mise à niveau")

> [!NOTE]
> Notez qu’Azure contrôle la façon dont les instances sont affectées entre d’un domaine de mise à niveau à l’autre. Il n’est pas possible toospecify les instances sont allouées toowhich domaine.
>
>

## <a name="next-steps"></a>Étapes suivantes
[Comment les Services de cloud computing tooManage](cloud-services-how-to-manage.md)  
[Comment les Services de cloud computing tooMonitor](cloud-services-how-to-monitor.md)  
[Comment les Services de cloud computing tooConfigure](cloud-services-how-to-configure.md)  
