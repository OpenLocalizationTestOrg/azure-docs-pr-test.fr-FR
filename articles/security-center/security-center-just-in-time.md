---
title: "aaaJust dans la machine virtuelle de temps d’accès dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous guide comment juste-à-temps tooyour Azure d’accéder aux accès de machine virtuelle dans Azure Security Center vous permet de contrôler les ordinateurs virtuels."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Gérer l’accès Juste à temps à la machine virtuelle

Juste-à-temps virtual machine (VM) accès peut être utilisé toolock vers le bas le trafic entrant tooyour les machines virtuelles Azure, réduire l’exposition tooattacks tout en offrant un accès facile tooconnect tooVMs si nécessaire.

> [!NOTE]
> Hello juste-à-temps est en version préliminaire et disponible sur hello niveau Standard de centre de sécurité.  Consultez [tarification](security-center-pricing.md) niveaux de tarification du toolearn en savoir plus sur le centre de sécurité.
>
>

## <a name="attack-scenario"></a>Scénario d’attaque

Force brute des attaques généralement les ports de gestion cible comme un tooa d’accès signifie toogain machine virtuelle. En cas de réussite, un intrus peut prendre le contrôle hello VM et établir une brèche dans votre environnement.

Attaque en force brute de tooreduce monodirectionnelle exposition tooa est durée hello toolimit pendant laquelle un port est ouvert. Les ports de gestion ne pas les ouvrir toobe besoin à tout moment. Il leur suffit de toobe ouverte lorsque vous est connecté toohello machine virtuelle, par exemple tooperform tâches de maintenance ou de gestion. Lorsque juste-à-temps est activé, le centre de sécurité utilise [groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md) règles (NSG), qui restreignent l’accès toomanagement ports afin qu’ils ne peuvent pas être ciblés par les attaquants.

![Scénario Juste à temps][1]

## <a name="how-does-just-in-time-access-work"></a>Comment l’accès Juste à temps fonctionne-t-il ?

Lorsque juste-à-temps est activé, le centre de sécurité bloque le trafic entrant tooyour machines virtuelles Azure en créant une règle de groupe de sécurité réseau. Vous sélectionnez les ports hello sur hello VM toowhich le trafic entrant sera verrouillé. Ces ports sont contrôlées par hello juste-à-solution de temps.

Lorsqu’un utilisateur demande l’accès tooa machine virtuelle, le centre de sécurité vérifie que l’utilisateur hello a [contrôle d’accès en fonction du rôle (RBAC)](../active-directory/role-based-access-control-configure.md) autorisations qui fournissent un accès en écriture pour hello ressource Azure. Si elles ont des autorisations en écriture, hello demande est approuvée et centre de sécurité configure automatiquement les groupes de sécurité réseau (NSG) hello tooallow entrant ports de gestion du trafic toohello pour durée hello spécifié. Une fois hello délai expiré, centre de sécurité restaure États précédents de hello NSG tootheir.

> [!NOTE]
> L’accès Juste à temps à la machine virtuelle Security Center prend en charge uniquement les machines virtuelles déployées par le biais d’Azure Resource Manager. toolearn d’informations sur hello classique et les modèles de déploiement Resource Manager, consultez [Azure Resource Manager et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Utilisation de l’accès Juste à temps

Hello **juste à l’accès des ordinateurs virtuels de temps** vignette sur hello **centre de sécurité** panneau montre le nombre hello de machines virtuelles configurées pour juste-à-temps accès et hello le numéro approuvées de demandes d’accès effectuées Bonjour la semaine dernière.

Sélectionnez hello **juste à l’accès des ordinateurs virtuels de temps** vignette et hello **juste à l’accès des ordinateurs virtuels de temps** panneau s’ouvre.

![Vignette Accès Juste à temps à la machine virtuelle][2]

Hello **juste à l’accès des ordinateurs virtuels de temps** panneau fournit des informations sur l’état de vos machines virtuelles hello :

- **Configuré** -les ordinateurs virtuels qui ont été configuré toosupport juste-à-accès des ordinateurs virtuels de temps. données Hello présentées sont pourquoi la semaine dernière et inclut pour chaque numéro de hello de machine virtuelle de demandes approuvées, date du dernier accès et l’heure et dernier utilisateur.
- **Recommandé** : machines virtuelles qui peuvent prendre en charge l’accès Juste à temps à la machine virtuelle, mais n’ont pas été configurées dans cette optique. Nous vous recommandons d’activer le contrôle d’accès Juste à temps à la machine virtuelle pour ces machines virtuelles. Consultez [Activer l’accès Juste à temps à la machine virtuelle](#enable-just-in-time-vm-access).
- **Aucune recommandation** -raisons qui peuvent provoquer une machine virtuelle pas les toobe recommandé sont :
  - Manquant NSG - hello juste-à-solution de temps nécessite une toobe de groupe de sécurité réseau en place.
  - Machine virtuelle classique : l’accès Juste à temps à la machine virtuelle Security Center prend en charge uniquement les machines virtuelles déployées par le biais d’Azure Resource Manager. Un déploiement classique n’est pas pris en charge par hello juste-à-solution de temps.
  - Autre - une machine virtuelle est dans cette catégorie si hello juste-à-temps solution est désactivée dans la stratégie de sécurité hello d’abonnement de hello ou un groupe de ressources hello ou cette machine virtuelle hello est manquant pour une adresse IP publique et n’a pas un groupe de sécurité réseau en place.

## <a name="configuring-a-just-in-time-access-policy"></a>Configuration d’une stratégie d’accès Juste à temps

hello tooselect machines virtuelles que vous souhaitez tooenable :

1. Sur hello **juste à l’accès des ordinateurs virtuels de temps** panneau, sélectionnez hello **recommandé** onglet.

  ![Activer l’accès Juste à temps à la machine virtuelle][3]

2. Sous **machines virtuelles**, sélectionnez les machines virtuelles de hello que vous souhaitez tooenable. Cela permet de placer un ordinateur virtuel de tooa suivant coche.
3. Sélectionnez **Enable JIT on VMs** (Activer JIT sur les machines virtuelles).
4. Sélectionnez **Enregistrer**.

### <a name="default-ports"></a>Ports par défaut

Vous pouvez voir des ports par défaut hello centre de sécurité recommande l’activation juste-à-temps.

1. Sur hello **juste à l’accès des ordinateurs virtuels de temps** panneau, sélectionnez hello **recommandé** onglet.

  ![Afficher les ports par défaut][6]

2. Sous **Machines virtuelles**, sélectionnez une machine virtuelle. Cela permet de placer une coche suivant toohello VM et ouvre hello **configuration de l’accès JIT VM** panneau. Ce panneau affiche les ports par défaut de hello.

### <a name="add-ports"></a>Ajouter des ports

À partir de hello **configuration de l’accès JIT VM** panneau, vous pouvez également ajouter et configurer un nouveau port sur lequel vous souhaitez hello tooenable juste-à-solution de temps.

1. Sur hello **configuration de l’accès JIT VM** panneau, sélectionnez **ajouter**. Cette opération ouvre hello **configuration du port ajouter** panneau.

  ![Configuration du port][7]

2. Sur **configuration du port ajouter** panneau, vous identifiez port hello, type de protocole, autorisé des adresses IP source et au maximum le temps de demande.

  Autorisé des adresses IP source est hello IP plages tooget autorisées sur une demande approuvée.

  Durée maximale de la demande est la fenêtre de temps maximal hello ouverture d’un port spécifique.

3. Sélectionnez **OK**.

## <a name="requesting-access-tooa-vm"></a>Demande d’accès tooa machine virtuelle

toorequest tooa d’accès aux ordinateurs virtuels :

1. Sur hello **juste à l’accès des ordinateurs virtuels de temps** panneau, sélectionnez hello **configuré** onglet.
2. Sous **machines virtuelles**, sélectionnez les machines virtuelles de hello que vous souhaitez tooenable accès. Cela permet de placer un ordinateur virtuel de tooa suivant coche.
3. Sélectionnez **Demander l’accès**. Cette opération ouvre hello **demander l’accès** panneau.

  ![Demande l’accès tooa machine virtuelle][4]

4. Sur hello **demander l’accès** panneau, que vous configurez pour chaque tooopen de ports hello machine virtuelle, ainsi que l’adresse IP source hello hello port est ouvert la fenêtre de temps tooand hello pour le hello port est ouvert. Vous pouvez demander des ports toohello uniquement d’accès qui sont configurés dans hello simplement dans la stratégie. Chaque port a une durée maximale autorisée dérivée hello simplement dans la stratégie.
5. Sélectionnez **Ports ouverts**.

## <a name="editing-a-just-in-time-access-policy"></a>Modification d’une stratégie d’accès Juste à temps

Vous pouvez modifier l’ordinateur virtuel existant juste-à-stratégie par ajout et configuration d’un nouveau tooopen de port pour cette machine virtuelle, ou en modifiant un autre paramètre tooan connexe déjà protégé port.

Dans commande tooedit existant juste-à-stratégie d’une machine virtuelle, hello **configuré** onglet est utilisé :

1. Sous **machines virtuelles**, sélectionnez une machine virtuelle tooadd un tooby de port sur les points de hello trois au sein de la ligne de hello pour cette machine virtuelle. Un menu s’ouvre.
2. Sélectionnez **modifier** dans le menu de hello. Cette opération ouvre hello **configuration de l’accès JIT VM** panneau.

  ![Modifier la stratégie][8]

3. Sur hello **configuration de l’accès JIT VM** panneau, vous pouvez modifier les paramètres existants hello d’un port déjà protégé en cliquant sur son port ou vous pouvez sélectionner **ajouter**. Cette opération ouvre hello **configuration du port ajouter** panneau.

  ![Ajouter un port][7]

4. Sur **configuration du port ajouter** panneau identifier le port de hello, type de protocole, des adresses IP sources autorisées et durée maximale de la demande.
5. Sélectionnez **OK**.
6. Sélectionnez **Enregistrer**.

## <a name="auditing-just-in-time-access-activity"></a>Audit de l’activité d’accès Juste à temps

Vous pouvez obtenir des informations sur les activités des machines virtuelles à l’aide de la recherche dans les journaux. journaux de tooview :

1. Sur hello **juste à l’accès des ordinateurs virtuels de temps** panneau, sélectionnez hello **configuré** onglet.
2. Sous **machines virtuelles**, sélectionnez une informations tooview de machine virtuelle sur en cliquant sur les points de hello trois au sein de la ligne de hello pour cette machine virtuelle. Un menu s’ouvre.
3. Sélectionnez **le journal d’activité** dans le menu de hello. Cette opération ouvre hello **le journal d’activité** panneau.

![Sélectionner un journal d’activité][9]

Hello **le journal d’activité** panneau fournit une vue filtrée des opérations précédentes pour cette machine virtuelle, ainsi que l’abonnement, date et l’heure.

![Afficher le journal d’activité][5]

Vous pouvez télécharger les informations du journal hello en sélectionnant **cliquez ici tous les éléments hello de type toodownload en tant que volume partagé de cluster**.

Modifier les filtres de hello et sélectionnez **appliquer** toocreate une recherche et un journal.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Utilisation de l’accès Juste à temps à la machine virtuelle par le biais de PowerShell

Bonjour toouse de commande juste-à-solution de temps via PowerShell, assurez-vous que vous avez hello [dernière](/powershell/azure/install-azurerm-ps) Azure PowerShell version.
Une fois que vous le faites, vous devez tooinstall hello [dernière](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) Azure Security Center à partir de la galerie de PowerShell hello.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>Configuration d’une stratégie Juste à temps pour une machine virtuelle

tooconfigure seulement dans la stratégie sur un ordinateur virtuel spécifique, vous devez toorun cette commande dans votre session PowerShell : Set-ASCJITAccessPolicy.
Suivez hello applet de commande documentation toolearn plus.

### <a name="requesting-access-tooa-vm"></a>Demande d’accès tooa machine virtuelle

tooaccess un ordinateur virtuel spécifique qui est protégé par Bonjour juste-à-solution de temps, vous devez toorun cette commande dans votre session PowerShell : ASCJITAccess appeler.
Suivez hello applet de commande documentation toolearn plus.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment juste à temps accès machine virtuelle dans le centre de sécurité permet de contrôler l’accès tooyour Azure virtual machines.

toolearn en savoir plus sur le centre de sécurité, voir hello :

- [Définition de stratégies de sécurité](security-center-policies.md) — Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.
- [Gestion des recommandations de sécurité](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.
- [Contrôle d’intégrité de la sécurité](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure.
- [La gestion et de répondre toosecurity alertes](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre.
- [Surveillance des solutions de partenaire](security-center-partner-solutions.md) — Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
- [Forum aux questions du centre de sécurité](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
- [Blog sur la sécurité Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
