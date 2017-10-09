---
title: aaaHow tooconfigure un service cloud (portail) | Documents Microsoft
description: "Découvrez comment tooconfigure cloud services dans Azure. En savoir plus de la configuration du service cloud tooupdate hello et configurer les instances de toorole d’accès à distance. Ces exemples utilisent hello portail Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Comment les Services de cloud computing tooConfigure
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-how-to-configure-portal.md)
> * [portail Azure Classic](cloud-services-how-to-configure.md)
>
>

Vous pouvez configurer les paramètres de hello couramment utilisé pour un service cloud dans hello portail Azure. Ou, si vous aimez tooupdate vos fichiers de configuration directement, téléchargez un tooupdate de fichier de configuration de service, puis téléchargez hello mise à jour de service de cloud de hello de fichier et de mise à jour avec les modifications de configuration hello. Dans les deux cas, les mises à jour configuration hello sont émis tooall les instances de rôle.

Vous pouvez également gérer des instances de hello de vos rôles de service cloud ou le Bureau à distance dans les.

Azure assurer disponibilité de service 99,95 % au cours de hello mises à jour de la configuration si vous disposez d’au moins deux instances de rôle pour chaque rôle. Qui permet de demandes de client d’ordinateur virtuel tooprocess pendant hello autres est en cours de mise à jour. Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Modification d'un service cloud
Après ouverture hello [portail Azure](https://portal.azure.com/), accédez tooyour le service cloud. Vous pouvez alors gérer plusieurs aspects.

![Page Paramètres](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Hello **paramètres** ou **tous les paramètres** liens ouvriront hello **paramètres** panneau dans laquelle vous pouvez modifier hello **propriétés**, modifier hello **Configuration**, gérer hello **certificats**, le programme d’installation **règles d’alerte**et gérer hello **utilisateurs** qui ont accès service de cloud computing toothis.

![Panneau Paramètres du service cloud Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Gestion de la version de SE invité

Par défaut, Azure met régulièrement à jour votre invité du système d’exploitation toohello dernière image pris en charge dans hello famille de systèmes d’exploitation que vous avez spécifié dans votre configuration de service (.cscfg), par exemple, Windows Server 2016.

Si vous devez tootarget une version du système d’exploitation spécifique, vous pouvez la définir dans hello **Configuration** panneau.

![Définition de la version du système d’exploitation](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> Lorsque vous choisissez une version de système d’exploitation spécifique, les mises à jour de SE automatiques sont désactivées et l’application de correctifs relève alors de votre responsabilité. Vous devez vous assurer que vos instances de rôle sont reçoit des mises à jour, ou vous pouvez exposer les vulnérabilités toosecurity application.

## <a name="monitoring"></a>Surveillance
Vous pouvez ajouter le service de cloud tooyour des alertes. Cliquez sur **Paramètres** > **Règles d’alerte** > **Ajouter une alerte**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

Vous pouvez alors configurer une alerte. Avec hello **métrique** zone déroulante, vous pouvez configurer une alerte pour hello les types de données suivants.

* Lecture du disque
* Écriture sur le disque
* Entrée réseau
* Sortie réseau
* Pourcentage UC

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Configuration de la surveillance à partir d’une vignette de métrique
Au lieu d’utiliser **paramètres** > **les règles d’alerte**, vous pouvez cliquer sur une des vignettes de métrique hello Bonjour **analyse** section Hello **Cloud service** panneau.

![Surveillance du service cloud](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

À ce stade, vous pouvez personnaliser le graphique hello utilisé avec la vignette de hello, ou ajouter une règle d’alerte.

## <a name="reboot-reimage-or-remote-desktop"></a>Redémarrage, réinitialisation ou Bureau à distance
À ce stade, vous ne pouvez pas configurer Bureau à distance à l’aide de hello **portail Azure**. Toutefois, vous pouvez configurer il via hello [portail Azure classic](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), ou via [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

Tout d’abord, cliquez sur l’instance de service cloud hello.

![Instance de service cloud](./media/cloud-services-how-to-configure-portal/cs-instance.png)

Hello panneau qui s’ouvre, vous pouvez établir une connexion Bureau à distance, redémarrer à distance hello instance ou à distance réinitialisation (démarrage avec une image actualisée) hello instance.

![Boutons d’instance de service cloud](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Reconfigurer votre fichier .cscfg
Vous devrez peut-être tooreconfigure votre service cloud via hello [la configuration de service (cscfg)](cloud-services-model-and-package.md#cscfg) fichier. Vous devez toodownload votre .cscfg de fichier, modifiez-le, puis téléchargez-le.

1. Cliquez sur hello **paramètres** icône ou hello **tous les paramètres** lien tooopen des hello **paramètres** panneau.

    ![Page Paramètres](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Cliquez sur hello **Configuration** élément.

    ![Panneau de configuration](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Cliquez sur hello **télécharger** bouton.

    ![Télécharger](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Une fois que vous mettez à jour le fichier de configuration de service hello, télécharger et appliquer les mises à jour de la configuration hello :

    ![Télécharger](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Sélectionnez le fichier .cscfg de hello et cliquez sur **OK**.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).
* Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).
* [Gérez votre service cloud](cloud-services-how-to-manage-portal.md).
* Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).
