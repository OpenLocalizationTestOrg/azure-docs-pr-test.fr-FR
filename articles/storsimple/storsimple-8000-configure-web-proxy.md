---
title: "aaaSet un proxy web pour appareil de série StorSimple 8000 | Documents Microsoft"
description: "Découvrez comment toouse Windows PowerShell pour StorSimple tooconfigure web paramètres du proxy pour votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: 
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: alkohli
ms.openlocfilehash: ed34ff400df66a5f1950c21d5298b41acc538cca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Configurer le proxy web pour votre appareil StorSimple

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel décrit comment toouse Windows PowerShell pour StorSimple tooconfigure et vue web des paramètres du proxy pour votre appareil StorSimple. paramètres du proxy web Hello sont utilisées par l’appareil StorSimple hello lors de la communication avec le cloud de hello. Un serveur proxy web est tooadd utilisé une autre couche de sécurité, filtre le contenu, mettre en cache les besoins en bande passante tooease ou même aider analytique.

Guide de Hello dans ce didacticiel s’applique uniquement tooStorSimple 8000 series périphériques physiques. Configuration du proxy Web n’est pas pris en charge sur hello StorSimple Appliance de Cloud (8010 et 8020).

Le proxy web est une configuration _facultative_ pour votre appareil StorSimple. Vous pouvez configurer le proxy web uniquement via Windows PowerShell for StorSimple. configuration de Hello est un processus en deux étapes comme suit :

1. Tout d’abord, vous configurez les paramètres de proxy web via l’Assistant d’installation hello ou Windows PowerShell pour les applets de commande StorSimple.
2. Vous ensuite activer des paramètres de proxy web hello configuré via Windows PowerShell pour les applets de commande StorSimple.

Une fois la configuration du proxy web hello est terminée, vous pouvez afficher les paramètres de proxy web hello configuré dans le service du Gestionnaire de périphériques Microsoft Azure StorSimple hello et hello Windows PowerShell pour StorSimple.

Après avoir lu ce didacticiel, vous pourrez :

* Configurer le proxy web à l’aide de l’Assistant d’installation et des cmdlets.
* Activer le proxy web à l’aide des cmdlets.
* Afficher les paramètres de proxy web Bonjour portail Azure.
* Résoudre les erreurs lors de la configuration du proxy web.


## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Configurer le proxy web via Windows PowerShell pour StorSimple

Vous utilisez Hello suivant tooconfigure les paramètres de proxy web :

* Le programme d’installation tooguide de l’Assistant vous guide dans les étapes de configuration hello.
* Les applets de commande Windows PowerShell pour StorSimple

Chacune de ces méthodes est décrite dans les sections suivantes de hello.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Configurer le proxy web via l’Assistant d’installation Bonjour

Utilisez hello le programme d’installation Assistant tooguide que vous guident hello les étapes de configuration du proxy web. Effectuer hello suivant de proxy web de tooconfigure étapes sur votre appareil.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>proxy web tooconfigure via l’Assistant d’installation Bonjour

1. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet** et fournir hello **mot de passe administrateur**. Tapez ce qui suit hello commande toostart une session de l’Assistant d’installation :
   
    `Invoke-HcsSetupWizard`
2. Si c’est hello première fois que vous avez utilisé l’Assistant Installation de hello pour l’inscription de périphérique, vous devez tooconfigure tous les paramètres de réseau hello nécessaire jusqu'à ce que vous atteigniez la configuration du proxy web hello. Si votre appareil est déjà inscrit, acceptez tous les paramètres de réseau de hello configuré jusqu'à ce que vous atteigniez la configuration du proxy web hello. Dans l’Assistant Installation de hello, tooconfigure demandée web des paramètres de proxy, tapez **Oui**.
3. Pourquoi **URL de Proxy Web**, spécifiez l’adresse IP de hello ou hello du nom de domaine complet (FQDN) de votre web proxy server et hello numéro de port TCP que vous aimeriez toouse de votre appareil pour communiquer avec hello cloud. Utilisez hello suivant le format :
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Par défaut, le numéro de port TCP 8080 est spécifié.
4. Choisissez le type d’authentification hello en tant que **NTLM**, **base**, ou **aucun**. Authentification de base est l’authentification moins sécurisée pour la configuration du serveur proxy hello hello. NT LAN Manager (NTLM) est un protocole d’authentification hautement sécurisé et complexe qui utilise un système de messagerie de trois facteurs (voire quatre si une intégrité supplémentaire est requise) tooauthenticate un utilisateur. Hello par défaut l’authentification est NTLM. Pour plus d’informations, voir la rubrique Authentification [de base](http://hc.apache.org/httpclient-3.x/authentication.html) et [NTLM](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **Bonjour service du Gestionnaire de périphériques StorSimple, les graphiques de surveillance de périphérique hello ne fonctionnent pas lors de la base ou l’authentification NTLM est activée dans la configuration du serveur proxy hello pour appareil de hello. Pourquoi toowork des graphiques d’analyse, vous devez tooensure que l’authentification a la valeur tooNONE.**
  
5. Si vous avez activé l’authentification de hello, fournissez un **nom d’utilisateur du Proxy Web** et un **mot de passe de Proxy Web**. Vous devez également le mot de passe tooconfirm hello.
   
    ![Configuration du proxy web sur l’appareil StorSimple1](./media/storsimple-configure-web-proxy/IC751830.png)

Si vous inscrivez votre appareil pour hello première fois, continuez de l’inscription de hello. Si votre appareil a déjà été enregistré, l’Assistant de hello se ferme. paramètres de Hello configuré sont enregistrés.

Le proxy web est maintenant activé. Vous pouvez ignorer hello [activer le proxy web](#enable-web-proxy) étape et passez directement trop[afficher les paramètres de proxy web Bonjour Azure portal](#view-web-proxy-settings-in-the-azure-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Configuration du proxy web via les applets de commande Windows PowerShell pour StorSimple

Une autre façon tooconfigure les paramètres proxy web est via hello Windows PowerShell pour les applets de commande StorSimple. Effectuer hello suivant le proxy web étapes tooconfigure.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>proxy web tooconfigure via les applets de commande
1. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**. Lorsque vous y êtes invité, fournissez hello **mot de passe administrateur**. mot de passe par défaut Hello est `Password1`.
2. À l’invite de commandes hello, tapez :
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Fournir et confirmer le mot de passe hello lorsque vous y êtes invité.
   
    ![Configuration du proxy web sur l’appareil StorSimple3](./media/storsimple-configure-web-proxy/IC751831.png)

le proxy web Hello est désormais configuré et doit toobe activé.

## <a name="enable-web-proxy"></a>Activation du proxy web

Le proxy web est désactivé par défaut. Après avoir configuré les paramètres de proxy web hello sur votre appareil StorSimple, utilisez hello Windows PowerShell pour les paramètres de proxy web StorSimple tooenable hello.

> [!NOTE]
> **Cette étape n’est pas requise si vous avez utilisé le proxy web tooconfigure hello le programme d’installation Assistant. Le proxy web est automatiquement activé par défaut après une session de l’assistant d’installation.**


Effectuez hello comme suit dans Windows PowerShell pour le proxy web de tooenable StorSimple sur votre appareil :

#### <a name="tooenable-web-proxy"></a>proxy web tooenable
1. Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**. Lorsque vous y êtes invité, fournissez hello **mot de passe administrateur**. mot de passe par défaut Hello est `Password1`.
2. À l’invite de commandes hello, tapez :
   
    `Enable-HcsWebProxy`
   
    Vous avez maintenant activé la configuration du proxy web hello sur votre appareil StorSimple.
   
    ![Configuration du proxy web sur l’appareil StorSimple4](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-portal"></a>Afficher les paramètres de proxy web Bonjour portail Azure

paramètres de proxy web Hello sont configurés via l’interface Windows PowerShell de hello et ne peut pas être modifiées dans le portail de hello. Vous pouvez, toutefois, afficher ces paramètres configurés dans le portail de hello. Effectuer hello suivant le proxy web étapes tooview.

#### <a name="tooview-web-proxy-settings"></a>paramètres de proxy web tooview
1. Accédez trop**service du Gestionnaire de périphériques StorSimple > appareils**. Sélectionner, cliquez sur l’appareil, puis passez trop**paramètres du périphérique > réseau**.

    ![Cliquer sur Réseau](./media/storsimple-8000-configure-web-proxy/view-web-proxy-1.png)

2. Bonjour **paramètres réseau** panneau, cliquez sur hello **proxy Web** vignette.

    ![Cliquer sur Proxy web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-2.png)

3. Bonjour **proxy Web** panneau, les paramètres de proxy web révision hello configuré sur votre appareil StorSimple.
   
    ![Afficher les paramètres de proxy web](./media/storsimple-8000-configure-web-proxy/view-web-proxy-3.png)


## <a name="errors-during-web-proxy-configuration"></a>Erreurs lors de la configuration du proxy web

Si les paramètres de proxy web hello sont incorrectement configurés, les messages d’erreur sont utilisateur toohello affichés dans Windows PowerShell pour StorSimple. Hello tableau suivant décrit certaines de ces messages d’erreur, leurs causes probables et les actions recommandées.

| Numéro de série | Code d’erreur HRESULT | Cause principale possible | Action recommandée |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |Commande est exécutée à partir du contrôleur passif de hello et il n’est pas en mesure de toocommunicate avec le contrôleur actif de hello. |Exécutez la commande hello sur le contrôleur actif de hello. commande hello toorun à partir du contrôleur passif de hello, vous devez corriger connectivité hello de passif tooactive contrôleur. Vous devez contacter le Support Microsoft si cette connectivité est interrompue. |
| 2. |0x800710dd - l’identificateur d’opération hello n’est pas valide |Les paramètres du proxy ne sont pas pris en charge sur StorSimple Cloud Appliance. |Les paramètres du proxy ne sont pas pris en charge sur StorSimple Cloud Appliance. Ils peuvent uniquement être configurés sur un appareil StorSimple physique. |
| 3. |0x80070057 - Paramètre non valide |Un des paramètres de hello fournis pour les paramètres de proxy hello n’est pas valide. |Hello URI n’est pas fourni dans le format correct. Utilisez hello suivant le format :`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - Serveur RPC indisponible |cause première Hello est hello suivantes :</br></br>Le cluster n’est pas disponible. </br></br>Le service Chemin de données n'est pas en cours d'exécution.</br></br>commande Hello est exécutée à partir du contrôleur passif et il n’est pas en mesure de toocommunicate avec le contrôleur actif de hello. |Établir une tooensure de Support technique de Microsoft qui hello cluster est activé et service de chemin de données est en cours d’exécution.</br></br>Exécutez la commande hello à partir du contrôleur actif de hello. Si vous souhaitez que les commandes de hello toorun à partir du contrôleur passif de hello, vous devez vous assurer que hello peut communiquer avec le contrôleur actif de hello. Vous devez contacter le Support Microsoft si cette connectivité est interrompue. |
| 5. |0x800706be - Échec de l’appel RPC |Le cluster est arrêté. |Faites appel au Support technique de Microsoft tooensure qui hello cluster est activé. |
| 6. |0x8007138f - Ressource de cluster introuvable |Impossible de trouver la ressource de cluster du service de plateforme. Cela peut se produire lors de l’installation de hello n’était pas correcte. |Vous devrez peut-être tooperform usine sur votre appareil. Vous devrez peut-être toocreate une ressource de plateforme. Contactez le Support Microsoft pour les étapes suivantes. |
| 7. |0x8007138c - La ressource de cluster n’est pas en ligne |Les ressources de plateforme ou datapath ne sont pas en ligne. |Contact toohelp de Support technique de Microsoft vous assurer que la ressource de service de plateforme et de chemin de données hello sont en ligne. |

> [!NOTE]
> * Hello au-dessus de la liste des messages d’erreur n’est pas exhaustive.
> * Paramètres du proxy erreurs connexes tooweb seront affichera pas Bonjour Azure portal dans votre service de gestionnaire de périphériques StorSimple. S’il existe un problème avec le proxy web après la configuration de hello, état d’appareil de hello devient trop**hors connexion** dans le portail classique de hello. |

## <a name="next-steps"></a>Étapes suivantes
* Si vous rencontrez des problèmes lors du déploiement de votre appareil ou de configuration des paramètres de proxy web, consultez trop[résoudre les problèmes de déploiement de votre périphérique StorSimple](storsimple-troubleshoot-deployment.md).
* toolearn comment toouse hello service du Gestionnaire de périphériques StorSimple, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

