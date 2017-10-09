---
title: "aaaAzure résolution des problèmes de récupération de Site à partir de VMware tooAzure | Documents Microsoft"
description: "Résolution des problèmes rencontrés lors de la réplication de machines virtuelles Azure"
services: site-recovery
documentationcenter: 
author: asgang
manager: srinathv
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/24/2017
ms.author: asgang
ms.openlocfilehash: 912097c8892540dd798ba025e0b10374ca51d664
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-mobility-service-push-install-issues"></a>Résolution des problèmes d’installation Push pour le service Mobilité

Cet article décrit les problèmes courants de hello rencontrés lors de la tentative de tooinstall hello Service mobilité sur le serveur toosource pour activer la protection.

## <a name="error-code-95107-protection-could-not-be-enabled"></a>(Code d’erreur 95107) Impossible d’activer la protection.
**Code d’erreur** | **Causes possibles** | **Recommandations propres à l’erreur**
--- | --- | ---
95107 </br>***Message -*** poussée de l’ordinateur source toohello du service de mobilité hello a échoué avec le code d’erreur ***EP0858***. <br> Compte d’utilisateur hello dispose de privilèges insuffisants ou que les informations d’identification hello fourni service de mobilité tooinstall est incorrect | Informations d’identification de l’utilisateur fourni de service de mobilité tooinstall sur l’ordinateur source est incorrect | Vérifiez que hello utilisateur informations d’identification fournies pour l’ordinateur source de hello sur le serveur de configuration sont correctes. <br> informations d’identification de tooadd/modifier l’utilisateur : accédez tooconfiguration server > Cspsconfigtool icône > Gérer le compte. </br> En outre, vérifiez ci-dessous les conditions préalables sont vérifiés toosuccessfully complet d’installation poussée.

## <a name="error-code-95015-protection-could-not-be-enabled"></a>(Code d’erreur 95015) Impossible d’activer la protection.
**Code d’erreur** | **Causes possibles** | **Recommandations propres à l’erreur**
--- | --- | ---
95105 </br>***Message -*** poussée de l’ordinateur source toohello du service de mobilité hello a échoué avec le code d’erreur ***EP0856***. <br> « Fichier de partage et d’imprimantes » non autorisé sur l’ordinateur source de hello, ou rencontre des problèmes de connectivité réseau entre le serveur de processus hello et ordinateur de source de hello| Le Partage de fichiers et d’imprimantes n’est pas activé | Autoriser « Et partage de fichiers imprimantes » sur l’ordinateur source de hello Bonjour ordinateur source de toohello Go, le pare-feu Windows > paramètres sous le pare-feu Windows > « Autoriser une application ou une fonctionnalité via le pare-feu » > sélectionnez « Partage de fichiers et imprimantes pour tous les profils ». </br> En outre, vérifiez ci-dessous les conditions préalables sont vérifiés toosuccessfully complet d’installation poussée.

## <a name="error-code-95117-protection-could-not-be-enabled"></a>(Code d’erreur 95117) Impossible d’activer la protection.
**Code d’erreur** | **Causes possibles** | **Recommandations propres à l’erreur**
--- | --- | ---
95117 </br>***Message -*** poussée de l’ordinateur source toohello du service de mobilité hello a échoué avec le code d’erreur ***EP0865***. <br> Ordinateur source de hello n’est pas en cours d’exécution, soit il existe des problèmes de connectivité réseau entre le serveur de processus hello et ordinateur de source de hello | Connectivité réseau entre le serveur de processus et le serveur source | Vérifiez la connectivité entre le serveur de processus et le serveur source. </br> En outre, vérifiez ci-dessous les conditions préalables sont vérifiés toosuccessfully complet d’installation poussée.

## <a name="error-code-95103-protection-could-not-be-enabled"></a>(Code d’erreur 95103) Impossible d’activer la protection.
**Code d’erreur** | **Causes possibles** | **Recommandations propres à l’erreur**
--- | --- | ---
95103 </br>***Message -*** poussée de l’ordinateur source toohello du service de mobilité hello a échoué avec le code d’erreur ***EP0854***. <br> « Windows Management Instrumentation (WMI) » n’est pas autorisée sur l’ordinateur source de hello, ou rencontre des problèmes de connectivité réseau entre le serveur de processus hello et ordinateur de source de hello| Windows Management Instrumentation (WMI) est bloquée dans hello pare-feu Windows | Autoriser Windows Management Instrumentation (WMI) Bonjour le pare-feu Windows. Sous Paramètres du Pare-feu Windows > Autoriser une application ou une fonctionnalité via le Pare-feu Windows > sélectionnez WMI pour tous les profils. </br> En outre, vérifiez ci-dessous les conditions préalables sont vérifiés toosuccessfully complet d’installation poussée.

## <a name="check-push-install-logs-for-errors"></a>Vérifier les journaux d’installation Push à la recherche d’erreurs

Sur le serveur de processus de Configuration/hello, accédez à toofile 'PushinstallService' situé à <Microsoft Azure Site Recovery Install Location>\home\svsystems\pushinstallsvc\ toounderstand hello source hello problème et utilisez problème de hello tooresolve étapes de dépannage ci-dessous.</br>
![JournauxInstallationPush](./media/site-recovery-protection-common-errors/pushinstalllogs.png)

## <a name="push-install-pre-requisites-for-windows"></a>Prérequis de l’installation Push pour Windows
### <a name="ensure-file-and-printer-sharing-is-enabled"></a>S’assurer que l’option Partage de fichiers et d’imprimantes est activée
Autoriser les « Fichier de partage et d’imprimantes » et « Windows Management Instrumentation » sur l’ordinateur source hello hello pare-feu Windows </br>
#### <a name="if-source-machine-is-domain-joined-br"></a>Si la machine source est jointe à un domaine : </br>
Configurez les paramètres du Pare-feu à l’aide de la console de gestion des stratégies de groupe (GPMC).
1. Domaine de connexion tooActive active de l’ordinateur en tant qu’administrateur et ouvrez la Console de gestion de stratégie de groupe (GPMC. MSC, exécutez à partir d’un point de départ > Exécuter).</br>
3. Si la console GPMC n’est pas installée, suivez le lien de hello trop[hello d’installer la console GPMC](https://technet.microsoft.com/library/cc725932.aspx) </br>
4. Dans l’arborescence de la console GPMC hello, double-cliquez sur les objets de stratégie de groupe dans la forêt de hello et du domaine et accédez trop « Stratégie de domaine par défaut ». </br>
![gpmc1](./media/site-recovery-protection-common-errors/gpmc1.png) </br>
</br>
5. Cliquez avec le bouton droit sur Stratégie de domaine par défaut > Modifier > une nouvelle fenêtre Éditeur de gestion des stratégies de groupe s’ouvre. </br>
![gpmc2](./media/site-recovery-protection-common-errors/gpmc2.png) </br>
</br>
6. Bonjour, éditeur de gestion de stratégie de groupe, accédez tooComputer Configuration > stratégies > modèles d’administration > réseau > Connexions réseau > pare-feu Windows. </br>
![gpmc3](./media/site-recovery-protection-common-errors/gpmc3.png) </br>
</br>
7. Activer hello suivant les paramètres de profil de domaine et le profil Standard </br>
a) Double-cliquez sur l’exception Pare-feu Windows : autoriser l’exception de partage de fichiers entrants et d’imprimantes. Sélectionnez Activé, puis cliquez sur OK. </br>
b) Double cliquez sur l’exception Pare-feu Windows : autoriser l’exception d’administration à distance entrante. Sélectionnez Activé, puis cliquez sur OK. </br>
![gpmc4](./media/site-recovery-protection-common-errors/gpmc4.png) </br>
</br>

###### <a name="if-source-machine-is-not-domain-joined-and-part-of-workgroup-br"></a>Si la machine source n’est pas jointe à un domaine et qu’elle fait partie d’un groupe de travail </br>
Configurez les paramètres du Pare-feu sur la machine distante (pour le groupe de travail) :
1. Atteindre l’ordinateur source de toohello,</br>
2. Sous Paramètres du Pare-feu Windows > Autoriser une application ou une fonctionnalité via le Pare-feu Windows > sélectionnez Partage de fichiers et d’imprimantes pour tous les profils. </br>
3. Sous Paramètres du Pare-feu Windows > Autoriser une application ou une fonctionnalité via le Pare-feu Windows > sélectionnez WMI pour tous les profils. </br>

#### <a name="disable-remote-user-account-control-uac"></a>Désactiver le contrôle de compte d’utilisateur (UAC)
Désactiver le compte d’utilisateur à l’aide du service de mobilité de Registre toopush clé hello.
1. Cliquez sur Démarrer > Exécuter > tapez regedit > Entrée
2. Recherchez et cliquez hello suivant la sous-clé de Registre : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
3. Si l’entrée de Registre LocalAccountTokenFilterPolicy de hello n’existe pas, procédez comme suit :
4. Dans le menu Edition de hello > New > cliquez sur valeur DWORD.
5. Tapez LocalAccountTokenFilterPolicy et appuyez sur Entrée.
6. Cliquez avec le bouton droit sur LocalAccountTokenFilterPolicy, puis cliquez sur Modifier.
7. Dans la zone de données de valeur hello, tapez 1, puis cliquez sur OK.
8. Quittez l’Éditeur du Registre.


## <a name="push-install-pre-requisites-for-linux"></a>Prérequis de l’installation Push pour Linux :

1. Créer un utilisateur racine sur le serveur de Linux hello source. (Utiliser ce compte uniquement pour les mises à jour et de la poussée hello)</br>
2. Vérifiez le fichier/etc/hosts hello sur la source de hello Linux server possède des entrées qui mappent des adresses de tooIP hello nom d’hôte local associés à toutes les cartes réseau. </br>
3. Vérifiez que hello dernière openssh openssh-serveur openssl les packages et sont installés sur le serveur Linux de source. </br>
Vérifiez que le port ssh 22 est activé et fonctionne. </br>
4. Vérifier si les entrées obsolètes des agents sont déjà présentes sur le serveur de source de hello, désinstaller les agents plus anciennes de hello et redémarrer le serveur de hello, réinstallez l’agent. </br>

#### <a name="enable-sftp-subsystem-and-password-authentication-in-hello-sshdconfig-file"></a>Activer l’authentification dans le fichier de sshd_config hello SFTP sous-système et le mot de passe
1. Sur le serveur source, connectez-vous en tant que racine. </br>
2. Dans le fichier /etc/ssh/sshd_config hello,</br> rechercher la ligne hello qui commence par PasswordAuthentication. </br>
3. d.   Supprimez les commentaires de la ligne de hello et modifiez les valeur hello à partir de « non » trop « Oui ». </br>
![Linux1](./media/site-recovery-protection-common-errors/linux1.png)
4. Rechercher la ligne hello qui commence par « Sous-système » et supprimez les commentaires de la ligne de hello. </br>
![Linux2](./media/site-recovery-protection-common-errors/linux2.png)
5. Enregistrez les modifications de hello et redémarrez le service de sshd hello. </br>

## <a name="push-installation-checks-on-configurationprocess-server"></a>Contrôlez l’installation Push sur le serveur de configuration/processus.
#### <a name="validate-credentials-for-discovery-and-installation"></a>Valider les informations d’identification pour la détection et l’installation

1. Depuis le serveur de configuration, lancez Cspsconfigtool.</br>
![VérificationConnexionWMI5](./media/site-recovery-protection-common-errors/wmitestconnect5.png) </br>

2. Assurez-vous que le compte hello utilisé pour la protection dispose des droits d’administrateur sur l’ordinateur source de hello. </br>

#### <a name="check-connectivity-between-process-server-and-source-server"></a>Vérifier la connectivité entre le serveur de processus et le serveur source
1. Vérifiez que le serveur de processus dispose d’une connexion Internet.
2. Vérifiez la connexion WMI à l’aide de wbemtest.exe. </br>
Sur le serveur de processus hello, cliquez sur Démarrer > Exécuter > wbemtest.exe > fenêtre de Windows Management Instrumentation Tester s’ouvre comme indiqué.</br>
   ![VérificationConnexionWMI1](./media/site-recovery-protection-common-errors/wmitestconnect1.png) </br>
   </br>
Cliquez sur se connecter > entrez l’adresse IP du serveur source hello hello Namespace entrée nom d’utilisateur et mot de passe (si l’ordinateur source est joint au domaine, fournissez un nom de domaine de hello en même temps que le nom d’utilisateur en tant que « Om_utilisateur ». Si l’ordinateur source est dans un groupe de travail, fournit uniquement les nom d’utilisateur hello.) Sélectionnez le niveau de l’authentification de hello comme confidentialité du paquet. </br>
![VérificationConnexionWMI2](./media/site-recovery-protection-common-errors/wmitestconnect2.png) </br>
   </br>
   Cliquez sur Connexion. Maintenant la connexion WMI hello doit réussir avec hello a fourni des données et la fenêtre de Windows Management Instrumentation Tester hello doit être affiché comme indiqué ci-dessous : </br>
   ![VérificationConnexionWMI3](./media/site-recovery-protection-common-errors/wmitestconnect3.png) </br>
</br>
   Si la connexion WMI ne fonctionne pas correctement, un message d’erreur s’affiche dans une fenêtre indépendante. Hello capture d’écran ci-dessous montre une tentative infructueuse si Administration WMI/à distance n’est pas activée dans le pare-feu Windows autorisé d’application. </br>
   ![VérificationConnexionWMIt4](./media/site-recovery-protection-common-errors/wmitestconnect4.png) </br>
</br>

3. Vérifiez l’état hello WMI et la connectivité.</br>
Sur le serveur de processus de configuration/hello, </br>
Cliquez sur Démarrer > Exécuter > wmimgmt.msc > Actions > autres Actions > se connecter à l’ordinateur tooanother (ordinateur source). </br>
Entrez les informations d’identification de hello du compte hello utilisé pour la protection et de vérifier si la connexion est correctement. </br>

#### <a name="verify-network-shared-folders-of-source-machine-is-accessible-from-process-server-ps-remotely-using-specified-credentials"></a>Vérifiez que les dossiers partagés de la machine source sur le réseau sont accessibles depuis le serveur de processus en utilisant à distance les informations d’identification spécifiées.
  1. Ordinateur de serveur (PS) tooProcess d’ouverture de session, ouvrez l’Explorateur de fichiers > dans le type de barre d’adresse hello > «\\\source-machine-ip\C$ » > cliquez sur ENTRÉE. </br>
  ![PartageDeFichiers1](./media/site-recovery-protection-common-errors/fileshare1.png) </br>
  2. Dans l’Explorateur de fichiers, vous êtes invité à indiquer des informations d’identification. Entrez le mot de passe et le nom d’utilisateur hello > cliquez sur OK.</br>
   Si l’ordinateur source est joint au domaine, entrez le nom de domaine de hello en même temps que le nom d’utilisateur en tant que « Om_utilisateur ».</br>
   Si l’ordinateur source est dans un groupe de travail, fournissez uniquement hello « username ». </br>
  ![PartageDeFichiers2](./media/site-recovery-protection-common-errors/fileshare2.png) </br>
  3. Si la connexion est établie, vous pouvez afficher les dossiers de hello de l’ordinateur source à distance à partir de processus serveur (PS) </br>
  ![PartageDeFichiers3](./media/site-recovery-protection-common-errors/fileshare3.png) </br>

> [!NOTE] 
> Si la connexion échoue, vérifiez que tous les prérequis sont bien respectés.
>

Si vous ne souhaitez pas tooopen « Windows Management Instrumentation », vous pouvez également installer manuellement les service mobilité sur l’ordinateur source de hello.</br> [Installer le service Mobilité manuellement par le biais de l’interface utilisateur](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) </br>
[Installation à l’aide du Gestionnaire de configuration](site-recovery-install-mobility-service-using-sccm.md) </br>

## <a name="next-steps"></a>Étapes suivantes
- [Activer la réplication des machines virtuelles VMware](vmware-walkthrough-enable-replication.md)
