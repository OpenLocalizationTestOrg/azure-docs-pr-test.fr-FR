---
title: modifications aaaTrack avec Analytique de journal Azure | Documents Microsoft
description: "Hello solution de suivi des modifications dans Analytique de journal vous permet d’identifier les logiciels et les modifications de Service Windows qui se produisent dans votre environnement."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>Le suivi des modifications de logiciels dans votre environnement avec hello solution de suivi des modifications

![Symbole Change Tracking](./media/log-analytics-change-tracking/change-tracking-symbol.png)

Cet article vous aide à utiliser hello solution de suivi des modifications dans le journal Analytique tooeasily identifier les modifications dans votre environnement. solution de Hello effectue le suivi des modifications tooWindows logiciels Linux, Windows et clés de Registre, les services Windows et les fichiers les démons Linux. Identifier les modifications de configuration peut vous aider à identifier les problèmes opérationnels.

Installation d’hello solution tooupdate hello type d’agent que vous avez installée. Modifications tooinstalled logiciel, les services Windows et les démons Linux sur les serveurs de hello analysé sont lus. Puis, hello envoyées service Analytique de journal de toohello dans le cloud hello pour le traitement. Logique est appliqué toohello reçu données et service de cloud de hello enregistre les données de salutation. En utilisant les informations de hello sur hello du suivi des modifications du tableau de bord, vous pouvez facilement voir des modifications de hello qui ont été apportées à votre infrastructure de serveur.

## <a name="installing-and-configuring-hello-solution"></a>L’installation et la configuration de solution de hello
Utilisez hello suivant tooinstall des informations et configurer une solution de hello.

* Vous devez avoir un [Windows](log-analytics-windows-agents.md), [Operations Manager](log-analytics-om-agents.md), ou [Linux](log-analytics-linux-agents.md) agent sur chaque ordinateur où vous souhaitez que les modifications de toomonitor.
* Ajouter hello suivi solution tooyour espace de travail OMS à partir de hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview). Ou bien, vous pouvez ajouter la solution hello à l’aide des informations de hello dans [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md). Aucune configuration supplémentaire n'est nécessaire.

### <a name="configure-linux-files-tootrack"></a>Configurer tootrack de fichiers Linux
Utilisez hello suivant les étapes tooconfigure fichiers tootrack sur les ordinateurs Linux.

1. Dans le portail OMS : hello, cliquez sur **paramètres** (symbole d’engrenage hello).
2. Sur hello **paramètres** , cliquez sur **données**, puis cliquez sur **suivi de fichier Linux**.
3. Sous Linux fichier de suivi des modifications, tapez Bonjour chemin d’accès complet, y compris le nom de fichier hello de hello fichier que vous souhaitez tootrack puis cliquez sur hello **ajouter** symbole. Par exemple : « /etc/*.conf »
4. Cliquez sur **Save**.  

> [!NOTE]
> Le suivi des fichiers Linux est doté de fonctionnalités supplémentaires, y compris le suivi du répertoire, la récursivité dans les répertoires et le suivi des caractères génériques.

### <a name="configure-windows-files-tootrack"></a>Configurer tootrack de fichiers Windows
Utilisez hello suivant les étapes tooconfigure fichiers tootrack sur les ordinateurs Windows.

1. Dans le portail OMS : hello, cliquez sur **paramètres** (symbole d’engrenage hello).
2. Sur hello **paramètres** , cliquez sur **données**, puis cliquez sur **suivi de fichier Windows**.
3. Sous Windows fichier de suivi des modifications, tapez Bonjour chemin d’accès complet, y compris le nom de fichier hello de hello fichier que vous souhaitez tootrack puis cliquez sur hello **ajouter** symbole. Par exemple : C:\Program Files (x86)\Internet Explorer\iexplore.exe ou C:\Windows\System32\drivers\etc\hosts.
4. Cliquez sur **Save**.  
   ![Suivi des modifications des fichiers Windows](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>Configurer tootrack de clés de Registre Windows
Utilisez hello suivant tootrack de clés de Registre de tooconfigure étapes sur les ordinateurs Windows.

1. Dans le portail OMS : hello, cliquez sur **paramètres** (symbole d’engrenage hello).
2. Sur hello **paramètres** , cliquez sur **données**, puis cliquez sur **suivi de Registre Windows**.
3. Sous suivi des modifications du Registre Windows, tapez Bonjour toute clé que vous souhaitez tootrack et puis cliquez sur hello **ajouter** symbole.
4. Cliquez sur **Enregistrer**.  
   ![Suivi des modifications du Registre Windows](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Explication des propriétés de collection de fichiers Linux
1. **Type**
   * **Fichier** (rapport des métadonnées du fichier : taille, date de modification, code de hachage, etc.)
   * **Répertoire** (rapport des métadonnées du fichier : taille, date de modification, etc.)
2. **Liens** (lien symbolique de Linux de la gestion des références tooother fichiers ou répertoires)
   * **Ignorer** (des liens symboliques ignorer pendant recurions toonot incluent hello fichiers/répertoires référencés)
   * **Suivez** (liens symboliques hello de suivre pendant la récursivité tooalso incluent hello fichiers/répertoires référencés)
   * **Gérer** (suivre des liens symboliques hello et alter traitement hello du contenu retourné)

   > [!NOTE]   
   > Hello, option de liens « Gérer » n’est pas recommandée. L’extraction du contenu du fichier n’est pas prise en charge.

3. **Recurse** (parcourt de niveaux de dossiers et effectuer le suivi de tous les fichiers dont l’instruction de chemin d’accès hello)
4. **Sudo** (activer les répertoires ou fichiers d’accès qui nécessitent un privilège sudo)

### <a name="limitations"></a>Limites
Hello solution de suivi des modifications ne prend pas en charge hello éléments suivants :

* Dossiers (répertoires) pour le suivi des fichiers Windows
* Récursivité pour le suivi des fichiers Windows
* Caractères génériques pour le suivi des fichiers Windows
* Variables de chemin d’accès
* Systèmes de fichiers réseau
* Contenu du fichier

Autres limitations :

* Hello **taille maximale du fichier** colonne et les valeurs ne sont pas utilisés dans l’implémentation actuelle de hello.
* Si vous collectez les fichiers de plus de 2 500 dans le cycle de collecte de 30 minutes de hello, dégradation des performances de la solution.
* Lorsque le trafic réseau est élevé, les enregistrements de modifications peuvent prendre tooa toodisplay de six heures au maximum.
* Si vous modifiez la configuration de hello pendant un ordinateur est arrêté, les ordinateur hello peuvent valider les modifications de fichier qui appartenaient toohello les configuration précédente.

## <a name="change-tracking-data-collection-details"></a>Détails de la collecte de données de suivi des modifications
Le suivi des modifications collecte d’inventaire logiciel et métadonnées de Service Windows en utilisant des agents hello que vous avez activés.

Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées pour le suivi des modifications.

| plateforme | Agent direct | Agent Operations Manager | Agent Linux | Azure Storage | Operations Manager requis ? | Données de l’agent Operations Manager envoyées via un groupe d’administration | fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows et Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 minutes minutes too50, selon le type de modification hello. Hello tableau pour plus d’informations, consultez. |


Hello tableau suivant montre fréquence de collecte de données hello pour les types hello de modifications.

| **type de modification** | **frequency** | **L’agent****envoie-t-il****les différences lorsqu’il en détecte ?** |
| --- | --- | --- |
| Registre Windows | 50 minutes | Non |
| Fichier Windows | 30 minutes | Oui. Une capture instantanée est envoyée si aucune modification n’est relevée dans les 24 heures. |
| Fichier Linux | 15 minutes | Oui. Une capture instantanée est envoyée si aucune modification n’est relevée dans les 24 heures. |
| Services Windows | 30 minutes | Oui, toutes les 30 minutes lorsque des modifications sont détectées. Une capture instantanée est envoyée toutes les 24 heures, quelle que soit la modification. Par conséquent, les instantanés hello sont envoyée même lorsqu’il n’y a aucune modification. |
| Démons Linux | 5 minutes | Oui. Une capture instantanée est envoyée si aucune modification n’est relevée dans les 24 heures. |
| Logiciels Windows | 30 minutes | Oui, toutes les 30 minutes lorsque des modifications sont détectées. Une capture instantanée est envoyée toutes les 24 heures, quelle que soit la modification. Par conséquent, les instantanés hello sont envoyée même lorsqu’il n’y a aucune modification. |
| Logiciels Linux | 5 minutes | Oui. Une capture instantanée est envoyée si aucune modification n’est relevée dans les 24 heures. |

### <a name="registry-key-change-tracking"></a>Suivi des modifications des clés de Registre

Analytique de journal effectue le Registre Windows analyse et le suivi avec hello solution de suivi des modifications. Hello analyse modifications tooregistry clés vise toopinpoint les points d’extensibilité où le code tiers et les logiciels malveillants peuvent activer. suivant de Hello répertorie les clés de Registre de valeur par défaut montre hello qui sont suivies par la solution de hello et pourquoi chacune est suivi.

- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - Surveille les scripts qui s’exécutent au démarrage.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - Surveille les scripts qui s’exécutent à l’arrêt.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - Analyse des clés qui sont chargés avant hello utilisateur s’inscrit dans tootheir compte Windows. clé de Hello est utilisée pour les programmes 32 bits s’exécutant sur des ordinateurs 64 bits.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
    - Surveille les modifications apportées tooapplication paramètres.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - Surveille les entrées courantes de démarrage automatique qui se raccordent directement à l’Explorateur Windows et s’exécutent généralement in-process avec Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - Surveille les entrées courantes de démarrage automatique qui se raccordent directement à l’Explorateur Windows et s’exécutent généralement in-process avec Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - Surveille les entrées courantes de démarrage automatique qui se raccordent directement à l’Explorateur Windows et s’exécutent généralement in-process avec Explorer.exe.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Surveille l’enregistrement du gestionnaire des icônes de recouvrement.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - Surveille l’enregistrement du gestionnaire des icônes de recouvrement pour les programmes 32 bits s’exécutant sur des ordinateurs 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Surveille la présence de nouveaux plug-ins d’objet application d’assistance du navigateur pour Internet Explorer. Tooaccess utilisés hello modèle DOM (Document Object) de la navigation de page et toocontrol actuelle hello.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Surveille la présence de nouveaux plug-ins d’objet application d’assistance du navigateur pour Internet Explorer. Tooaccess utilisés hello modèle DOM (Document Object) de hello page et toocontrol volet de navigation de programmes 32 bits s’exécutant sur des ordinateurs 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - Surveille les nouvelles extensions Internet Explorer, notamment les menus d’outils personnalisés et les boutons de barre d’outils personnalisés.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - Surveille les nouvelles extensions Internet Explorer, notamment les menus d’outils personnalisés et les boutons de barre d’outils personnalisés pour les programmes 32 bits s’exécutant sur des ordinateurs 64 bits.
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Analyse les pilotes 32 bits de hello associés wavemapper, wave1 et wave2, msacm.imaadpcm, .msadpcm, .msgsm610 et vidc. Section toohello [drivers] similaire Bonjour système. Fichier INI.
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - Pilotes 32 bits de hello moniteurs associés wavemapper, wave1 et wave2, msacm.imaadpcm, .msadpcm, .msgsm610 et vidc pour les programmes 32 bits s’exécutant sur des ordinateurs 64 bits. Section toohello [drivers] similaire Bonjour système. Fichier INI.
- HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - Moniteurs hello liste des DLL ; sur le système connu ou couramment utilisé Ce système évite que les utilisateurs d’exploiter les autorisations de répertoire d’application faible en déposant dans les versions cheval de Troie des DLL système.
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - Liste des analyses hello packages tooreceive en mesure de notifications d’événements à partir de Winlogon, modèle de prise en charge d’ouverture de session interactive hello hello système d’exploitation Windows.


## <a name="use-change-tracking"></a>Utilisation du suivi des modifications
Une fois la solution de hello est installée, vous pouvez afficher résumé hello des modifications pour vos serveurs surveillés à l’aide de hello **le suivi des modifications** vignette sur hello **vue d’ensemble** page d’OMS.

![image de la vignette de suivi des modifications](./media/log-analytics-change-tracking/change-tracking-tile.png)

Vous pouvez afficher d’infrastructure de tooyour de modifications, puis examiner en détail pourquoi suivant des catégories :

* Modifications selon le type de configuration pour les logiciels et services Windows
* Modifications logicielles tooapplications et les mises à jour pour des serveurs individuels
* Nombre total de modifications logicielles pour chaque application
* Packages Linux
* Modifications de services Windows pour chaque serveur
* Modifications du démon Linux

![image du tableau de bord de suivi des modifications](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![image du tableau de bord de suivi des modifications](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>tooview des modifications pour tout type de modification
1. Sur hello **vue d’ensemble** , cliquez sur hello **le suivi des modifications** vignette.
2. Sur hello **de suivi des modifications** tableau de bord, passez en revue les informations de résumé hello dans un des panneaux de type hello modification et puis cliquez sur une tooview des informations détaillées sur elle Bonjour **recherche de journal** page.
3. Sur les pages de recherche de journal hello, vous pouvez afficher les résultats par heure, les résultats détaillés et votre historique de recherche de journal. Vous pouvez également filtrer selon les résultats de facettes toonarrow hello.

## <a name="next-steps"></a>Étapes suivantes
* Utilisez [connecter recherche Analytique de journal](log-analytics-log-searches.md) tooview détaillées des données de suivi des modifications.
