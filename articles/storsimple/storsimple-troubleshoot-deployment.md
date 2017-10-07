---
title: "problèmes de déploiement StorSimple aaaTroubleshoot | Documents Microsoft"
description: "Décrit comment toodiagnose et résoudre les erreurs qui se produisent lorsque vous déployez tout d’abord StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f8352eaa-193c-42d1-8818-0b8e02d8485d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 9a31a3cfb3be577500b226c2bc8172dd8664bad9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>Résolution des problèmes de déploiement d’un appareil StorSimple
## <a name="overview"></a>Vue d'ensemble
Cet article fournit des conseils de dépannage utiles pour votre déploiement de Microsoft Azure StorSimple. Il décrit les problèmes courants, les causes possibles et toohelp les étapes recommandées que résoudre les problèmes que vous pouvez rencontrer lorsque vous configurez StorSimple. Ces informations s’appliquent appareil physique de tooboth hello StorSimple local et un appareil virtuel StorSimple hello.

> [!NOTE]
> Problèmes liés à la configuration de périphérique que vous pouvez rencontrer peuvent se produire lorsque vous déployez des appareils hello pour hello première fois, ou ils peuvent se produire plus tard, lorsque l’appareil de hello est opérationnel. Cet article se concentre sur la résolution des problèmes qui surviennent lors du premier déploiement. tootroubleshoot d’appareil opérationnel, passez trop[résoudre les problèmes opérationnels appareil](storsimple-troubleshoot-operational-device.md).
> 
> 

Cet article décrit les outils hello pour le dépannage des déploiements de StorSimple également et fournit un exemple de dépannage détaillée.

## <a name="first-time-deployment-issues"></a>Problèmes lors du premier déploiement
Si vous rencontrez un problème lors du déploiement de votre appareil pour hello première fois, tenez compte des éléments suivants de hello :

* Si vous dépannez un périphérique physique, assurez-vous que le matériel de hello a été installé et configuré comme décrit dans [installer votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md) ou [installer votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md).
* Vérifiez les conditions préalables pour le déploiement. Assurez-vous que toutes les informations de hello décrites dans hello [liste de vérification de configuration déploiement](storsimple-deployment-walkthrough.md#deployment-configuration-checklist).
* Passez en revue hello Notes de publication de StorSimple toosee si le problème de hello est décrit. notes de publication Hello incluent des solutions de contournement concernant les problèmes d’installation connus. 

Pendant le déploiement de l’appareil, hello courants émet que les utilisateurs sont confrontés se produisent lorsqu’ils exécutent l’Assistant Installation de hello et quand ils Inscrivez appareil hello via Windows PowerShell pour StorSimple. (Vous utilisez Windows PowerShell pour StorSimple tooregister et configurez votre appareil StorSimple. Pour plus d'informations sur l’inscription des appareils, consultez l’ [Étape 3 : configuration et inscription de votre appareil via Windows PowerShell pour StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).)

Hello les sections suivantes peut vous aider à résoudre les problèmes que vous rencontrez lorsque vous configurez l’appareil StorSimple hello pour hello la première fois.

## <a name="first-time-setup-wizard-process"></a>Processus de l’Assistant Première installation
processus de l’Assistant Installation hello résument les Hello comme suit. Pour obtenir des informations de configuration détaillées, consultez [Déploiement de votre appareil StorSimple local](storsimple-deployment-walkthrough.md).

1. Exécutez hello [Invoke-HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) applet de commande toostart hello Assistant qui vous guidera tout au long hello restant comme suit. 
2. Configurer le réseau de hello : Assistant hello vous permet de configurer les paramètres réseau pour hello interface réseau DATA 0 sur votre appareil StorSimple. Ces paramètres hello suivants :
   * Virtual IP (VIP), masque de sous-réseau et passerelle : hello [Set-HcsNetInterface](https://technet.microsoft.com/library/dn688161.aspx) applet de commande est exécutée en arrière-plan de hello. Il configure hello adresse IP, masque de sous-réseau et passerelle pour hello interface réseau DATA 0 sur votre appareil StorSimple.
   * Serveur DNS principal : hello [Set-HcsDnsClientServerAddress](https://technet.microsoft.com/library/dn688172.aspx) applet de commande est exécutée en arrière-plan de hello. Il configure les paramètres de DNS hello pour votre solution StorSimple.
   * Serveur NTP : hello [Set-HcsNtpClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) applet de commande est exécutée en arrière-plan de hello. Il configure les paramètres du serveur NTP hello pour votre solution StorSimple.
   * Facultatif web proxy : hello [Set-HcsWebProxy](https://technet.microsoft.com/library/dn688154.aspx) applet de commande est exécutée en arrière-plan de hello. Il définit et permet la configuration du proxy web hello pour votre solution StorSimple.
3. Définir des mots de passe hello : hello prochaine étape consiste tooset administrateur de l’appareil et les mots de passe du Gestionnaire d’instantanés StorSimple. Si vous exécutez une mise à jour 1, alors vous sera pas requis tooset mot de passe de gestionnaire d’instantanés StorSimple hello.
   
   * mot de passe administrateur de périphérique Hello est toolog utilisé sur l’appareil de tooyour. mot de passe par défaut Hello est **Password1**.
   * mot de passe de gestionnaire d’instantanés StorSimple Hello est requis lorsque vous configurez un toouse périphérique StorSimple Snapshot Manager. Vous devez toofirst hello mot de passe dans l’Assistant Installation de hello, et puis vous pouvez définir et modifier à partir de hello service StorSimple Manager. Ce mot de passe authentifie l’appareil hello avec Gestionnaire d’instantanés StorSimple.
     
     > [!IMPORTANT]
     > Les mots de passe sont collectés avant l’enregistrement, mais appliqués uniquement après l’inscription des appareils de hello. S’il existe un tooapply échec un mot de passe, vous sera demandée toosupply hello mot de passe à nouveau jusqu'à ce que hello requis des mots de passe (qui répondent aux exigences de complexité hello) sont collectés.
     > 
     > 
4. Inscrire l’appareil de hello : hello dernière étape consiste appareil de hello tooregister avec le service StorSimple Manager hello en cours d’exécution dans Microsoft Azure. Hello inscription exige que vous trop[obtenir la clé d’inscription hello](storsimple-manage-service.md#get-the-service-registration-key) de hello portail Azure classic et indiquez-le dans l’Assistant Installation de hello. Une fois hello appareil est correctement inscrit, une clé de chiffrement est fournie tooyou. Veillez à tookeep ce chiffrement de clé dans un emplacement sûr, car il sera requis tooregister tous les appareils suivants avec le service de hello.

## <a name="common-errors-during-device-deployment"></a>Erreurs courantes lors du déploiement de l’appareil
Hello suivants tables liste hello les erreurs courantes que vous pouvez rencontrer lorsque vous :

* Configurer les paramètres de réseau hello requis.
* Configurer les paramètres de proxy web hello.
* Configurer l’administrateur de l’appareil hello et mots de passe de gestionnaire d’instantanés StorSimple. 
* Inscription de l’appareil hello. 

## <a name="errors-during-hello-required-network-settings"></a>Erreurs pendant les paramètres réseau hello requis
| Non. | Message d’erreur | Causes possibles | Action recommandée |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard : Cette commande peut uniquement être exécutée sur le contrôleur actif de hello. |Configuration a été effectuée sur le contrôleur passif de hello. |Exécutez cette commande à partir du contrôleur actif de hello. Pour plus d’informations, consultez la page [Identification d’un contrôleur actif sur votre appareil](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invoke-HcsSetupWizard : l’appareil n’est pas prêt. |Il existe des problèmes de connectivité de réseau hello sur DATA 0. |Vérifiez la connectivité de réseau physique hello sur DATA 0. |
| 3 |Invoke-HcsSetupWizard : Il existe un conflit d’adresse IP avec un autre système sur le réseau de hello (Exception de HRESULT : 0x80070263). |adresse IP de Hello fournie pour DATA 0 était déjà en cours d’utilisation par un autre système. |Fournissez une nouvelle adresse IP qui n’est pas en cours d’utilisation. |
| 4 |Invoke-HcsSetupWizard : échec de la ressource de cluster (Exception de HRESULT : 0x800713AE). |Adresse IP virtuelle en double. Hello fourni IP est déjà en cours d’utilisation. |Fournissez une nouvelle adresse IP qui n’est pas en cours d’utilisation. |
| 5. |Invoke-HcsSetupWizard : adresse IPv4 non valide. |adresse IP de Hello est fourni dans un format incorrect. |Format de hello et fournissez à nouveau votre adresse IP. Pour plus d’informations, consultez la page [Adressage IPv4][1]. |
| 6 |Invoke-HcsSetupWizard : adresse IPv6 non valide. |adresse IP de Hello est fourni dans un format incorrect. |Format de hello et fournissez à nouveau votre adresse IP. Pour plus d’informations, consultez la page [Adressage IPv6][2]. |
| 7 |Invoke-HcsSetupWizard : Aucun point de terminaison plus ne sont disponibles à partir de mappeur de point de terminaison hello. (Exception de HRESULT : 0x800706D9) |la fonctionnalité de cluster Hello ne fonctionne pas. |[contactez le support technique Microsoft](storsimple-contact-microsoft-support.md) . |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Erreurs au cours des paramètres de proxy web hello
| Non. | Message d’erreur | Causes possibles | Action recommandée |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard : paramètre non valide (exception de HRESULT: 0 x 80070057). |Un des paramètres de hello fournis pour les paramètres de proxy hello n’est pas valide. |Hello URI n’est pas fourni dans le format correct de hello. Hello utilisation suivant le format : http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard : serveur RPC non disponible (exception de HRESULT : 0x800706ba). |cause première Hello est hello suivantes :<ol><li>cluster de Hello n’est pas disponible.</li><li>contrôleur passif de Hello ne peut pas communiquer avec le contrôleur actif de hello et commande hello est exécuté à partir de contrôleur passif.</li></ol> |Selon la cause première hello :<ol><li>[Contactez le Support Microsoft](storsimple-contact-microsoft-support.md) toomake que ce cluster hello est activé.</li><li>Exécutez la commande hello à partir du contrôleur actif de hello. Si vous souhaitez que les commandes de hello toorun à partir du contrôleur passif de hello, vous devez tooensure ce contrôleur passif hello peut communiquer avec le contrôleur actif de hello. Vous devez trop[contactez le Support Microsoft](storsimple-contact-microsoft-support.md) si cette connectivité est défaillante.</li></ol> |
| 3 |Invoke-HcsSetupWizard : l’appel RPC a échoué (exception de HRESULT : 0x800706be). |Le cluster est arrêté. |[Contactez le Support Microsoft](storsimple-contact-microsoft-support.md) toomake que ce cluster hello est activé. |
| 4 |Invoke-HcsSetupWizard : ressource de cluster introuvable (exception de HRESULT : 0x8007138f). |ressource de cluster Hello est introuvable. Cela peut se produire lors de l’installation de hello n’était pas correcte. |Vous devrez peut-être tooreset hello appareil toohello paramètres par défaut. [Contactez le Support Microsoft](storsimple-contact-microsoft-support.md) toocreate une ressource de cluster. |
| 5 |Invoke-HcsSetupWizard : ressource de cluster pas en ligne (exception de HRESULT : 0x8007138c). |Les ressources de cluster ne sont pas en ligne. |[contactez le support technique Microsoft](storsimple-contact-microsoft-support.md) . |

## <a name="errors-related-toodevice-administrator-and-storsimple-snapshot-manager-passwords"></a>Erreurs liées toodevice administrateur et les mots de passe de gestionnaire d’instantanés StorSimple
mot de passe de l’administrateur d’appareil Hello par défaut est **Password1**. Ce mot de passe expire après hello première ouverture de session ; Par conséquent, vous devez toouse hello le programme d’installation Assistant toochange il. Vous devez fournir un nouveau mot de passe administrateur périphérique lorsque vous inscrivez des appareils hello pour hello première fois. 

Si vous utilisez un logiciel de gestionnaire d’instantanés StorSimple hello en cours d’exécution sur le périphérique hello toomanage hello Windows serveur hôte, vous devez également fournir un mot de passe du Gestionnaire d’instantanés StorSimple pendant la première inscription. 

Assurez-vous que vos mots de passe respectent hello suivant les exigences :

* Le mot de passe Administrateur de votre appareil doit comprendre entre 8 et 15 caractères.
* Le mot de passe du Gestionnaire d’instantanés StorSimple doit comporter 14 ou 15 caractères.
* Les mots de passe doivent contenir 3 des hello les 4 types de caractères suivants : minuscules, majuscules, numériques et spéciaux. 
* Votre mot de passe ne peut pas être hello identique hello derniers 24 mots de passe.

En outre, n’oubliez pas que les mots de passe expirent chaque année et peut être modifié uniquement après l’inscription des appareils de hello. Si l’inscription de hello échoue pour une raison quelconque, il se peut que les mots de passe hello ne seront pas modifiés. Pour plus d’informations sur l’administrateur de l’appareil et les mots de passe de gestionnaire d’instantanés StorSimple, consultez trop[utilisez hello toochange du service StorSimple Manager vos mots de passe StorSimple](storsimple-change-passwords.md).

Vous pouvez rencontrer un ou plusieurs des erreurs suivantes lorsque vous configurez l’administrateur de l’appareil hello et mots de passe de gestionnaire d’instantanés StorSimple de hello.

| Non. | Message d’erreur | Action recommandée |
| --- | --- | --- |
| 1 |mot de passe Hello dépasse la longueur maximale de hello. |Utilisez un mot de passe qui répond à ces exigences :<ul><li>Votre mot de passe administrateur d’appareil doit comprendre entre 8 et 15 caractères.</li><li>Votre mot de passe du Gestionnaire d’instantanés StorSimple doit comporter 14 ou 15 caractères.</li></ul> |
| 2 |mot de passe Hello ne respecte pas la longueur de hello requis. |Utilisez un mot de passe qui répond à ces exigences :<ul><li>Votre mot de passe administrateur d’appareil doit comprendre entre 8 et 15 caractères.</li><li>Votre mot de passe du Gestionnaire d’instantanés StorSimple doit comporter 14 ou 15 caractères.</lu></ul> |
| 3 |mot de passe Hello doit contenir des caractères en minuscules. |Les mots de passe doivent contenir 3 des hello les 4 types de caractères suivants : minuscules, majuscules, numériques et spéciaux. Assurez-vous que votre mot de passe répond à ces exigences. |
| 4 |mot de passe Hello doit contenir des caractères numériques. |Les mots de passe doivent contenir 3 des hello les 4 types de caractères suivants : minuscules, majuscules, numériques et spéciaux. Assurez-vous que votre mot de passe répond à ces exigences. |
| 5 |Hello le mot de passe doit contenir des caractères spéciaux. |Les mots de passe doivent contenir 3 des hello les 4 types de caractères suivants : minuscules, majuscules, numériques et spéciaux. Assurez-vous que votre mot de passe répond à ces exigences. |
| 6 |Hello mot de passe doit contenir 3 des hello les 4 types de caractères suivants : majuscules, minuscules, numériques et spéciaux. |Votre mot de passe ne contient pas de types hello requis de caractères. Assurez-vous que votre mot de passe répond à ces exigences. |
| 7 |Le paramètre ne correspond pas à la confirmation. |Assurez-vous que votre mot de passe répond à toutes les exigences et que vous l’avez entré correctement. |
| 8 |Votre mot de passe ne peut pas correspondre à par défaut de hello. |mot de passe Hello *Password1*. Vous devez toochange ce mot de passe après que vous être connecté pour hello première fois. |
| 9 |vous avez entré un mot de passe Hello ne correspond pas de mot de passe de périphérique hello. Retapez le mot de passe hello. |Mot de passe hello et tapez-le à nouveau. |

Les mots de passe sont collectés avant de l’appareil de hello est enregistrée, mais sont appliqués uniquement après l’inscription. workflow de récupération de mot de passe Hello requiert hello toobe de périphérique enregistré. 

> [!IMPORTANT]
> En règle générale, si une tentative tooapply un mot de passe échoue, les logiciels hello tente à plusieurs reprises un mot de passe toocollect hello jusqu'à ce qu’il réussisse. Dans de rares cas, un mot de passe hello ne peut pas être appliqué. Dans ce cas, vous pouvez inscrire l’appareil de hello et continuer, cependant les mots de passe hello ne seront pas modifiés. Vous ne recevrez aucune information comme mot de passe toowhich n’a pas été modifié : mot de passe administrateur de périphérique hello ou hello Gestionnaire d’instantanés StorSimple. Si cette situation se produit, nous vous recommandons de modifier les deux mots de passe.
> 
> 

Vous pouvez réinitialiser les mots de passe hello Bonjour portail classique Azure via hello service StorSimple Manager. Pour plus d'informations, accédez à : 

* [Mot de passe de l’administrateur d’appareil modification hello](storsimple-change-passwords.md#change-the-device-administrator-password).
* [Mot de passe du Gestionnaire d’instantanés StorSimple modification hello](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

## <a name="errors-during-device-registration"></a>Erreurs pendant l'inscription d’un appareil
Vous utilisez le service StorSimple Manager hello en cours d’exécution dans l’appareil de hello tooregister Microsoft Azure. Vous pouvez rencontrer un ou plusieurs des hello suivants lors de l’inscription de périphérique.

| Non. | Message d’erreur | Causes possibles | Action recommandée |
| --- | --- | --- | --- |
| 1 |Erreur 350027 : Impossible de dispositif hello tooregister hello StorSimple Manager. | |Attendez quelques minutes et recommencez l’opération hello. Si le problème de hello persiste, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md). |
| 2 |Erreur 350013 : Une erreur s’est produite lors de l’inscription de périphérique de hello. Cela peut être dû tooincorrect clé d’inscription. | |Inscrivez de hello appareil à nouveau avec la clé d’inscription de service correcte hello. Pour plus d’informations, consultez [clé d’inscription Get hello.](storsimple-manage-service.md#get-the-service-registration-key) |
| 3 |Erreur 350063 : Authentification tooStorSimple service Manager transmis, mais échec de l’inscription. Recommencez l’opération hello plus tard. |Cette erreur indique que l’authentification avec ACS a passé, mais hello register appel effectué toohello service a échoué. Cela peut résulter d’un problème réseau sporadique. |Si le problème de hello persiste, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md). |
| 4 |Erreur 350049 : Impossible d’accéder au service de hello lors de l’inscription. |Lorsque les hello est appelé toohello service, une exception web est reçue. Dans certains cas, ceci peut être résolu en renouvelant l’opération hello plus tard. |Veuillez vérifier votre adresse IP et le nom DNS, puis recommencez les opération hello. Si le problème de hello persiste, [contactez le Support Microsoft.](storsimple-contact-microsoft-support.md) |
| 5 |Erreur 350031 : hello appareil a déjà été inscrit. | |Aucune action requise. |
| 6. |Erreur 350016 : Échec de l’inscription de l’appareil. | |Vérifiez que la clé d’inscription de hello est correcte. |
| 7 |Invoke-HcsSetupWizard : Une erreur s’est produite lors de l’inscription de votre appareil ; Cela peut être dû tooincorrect adresse ou le nom DNS. Vérifiez vos paramètres réseau et réessayez. Si le problème de hello persiste, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md). (Erreur 350050) |Assurez-vous que votre appareil peut ping hello en dehors du réseau. Si vous n’avez pas de réseau toooutside de connectivité, l’inscription de hello peut échouer avec l’erreur. Cette erreur peut être une combinaison d’une ou plusieurs des éléments suivants de hello :<ul><li>IP incorrecte</li><li>Sous-réseau incorrect</li><li>Passerelle incorrecte</li><li>Paramètres DNS incorrects</li></ul> |Consultez les étapes hello Bonjour [exemple de dépannage pas à pas](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invoke-HcsSetupWizard : hello opération en cours a échoué en raison de l’erreur de service interne tooan [0x1FBE2]. Recommencez l’opération hello plus tard. Si hello problème persiste, contactez le Support technique de Microsoft. |Il s’agit d’une erreur générique levée pour toutes les erreurs du service ou de l’agent invisibles pour l’utilisateur. raison la plus courante Hello peut être que l’authentification hello ACS a échoué. Des causes possibles de l’échec de hello sont qu’il existe des problèmes avec la configuration du serveur NTP hello et sur hello périphérique n’est pas défini correctement. |Corrigez les temps de hello (s’il existe des problèmes), puis recommencez opération d’inscription de hello. Si vous utilisez le fuseau horaire de hello fuseau horaire - Set-HcsSystem commande tooadjust hello, majuscule chaque fuseau horaire de hello (par exemple « Pacific Standard Time »).  Si le problème persiste, contactez le [support technique Microsoft](storsimple-contact-microsoft-support.md) pour les étapes suivantes. |
| 9 |Avertissement : Impossible d’activer les périphériques hello. Les mots de passe de l’administrateur de l’appareil et du Gestionnaire d’instantanés StorSimple n’ont pas été modifiés. |Si l’inscription de hello échoue, administrateur de l’appareil hello et mots de passe de gestionnaire d’instantanés StorSimple ne sont pas modifiés. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>Outils de résolution des problèmes de déploiement de StorSimple
StorSimple comprend plusieurs outils que vous pouvez utiliser tootroubleshoot votre solution StorSimple. Vous avez notamment vu les points suivants :

* Packages de prise en charge et journaux d’appareil 
* Applets de commande conçues spécialement pour la résolution des problèmes 

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Packages de prise en charge et journaux d’appareil disponibles pour la résolution des problèmes
Un package de support contient tous les journaux appropriés hello qui peuvent aider l’équipe de Support technique de Microsoft hello avec la résolution des problèmes de l’appareil. Vous pouvez utiliser Windows PowerShell pour StorSimple toogenerate un package de support chiffré que vous pouvez ensuite partager avec le service de support technique.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>journaux de hello tooview ou contenu hello hello du package de support
1. Utiliser Windows PowerShell pour StorSimple toogenerate un package de prise en charge, comme décrit dans [créer et gérer un package de prise en charge](storsimple-create-manage-support-package.md).
2. Télécharger hello [script de déchiffrement](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) localement sur votre ordinateur client.
3. Utilisez cette [procédure pas à pas](storsimple-create-manage-support-package.md#edit-a-support-package) tooopen et decrypt package de prise en charge de hello.
4. Hello déchiffrer un package de prise en charge les journaux sont dans un format etw/etvx. Vous pouvez effectuer hello suivant les étapes tooview ces fichiers dans l’Observateur d’événements Windows :
   
   1. Exécutez hello **eventvwr** commande sur votre client Windows. Ceci démarrera hello Observateur d’événements.
   2. Bonjour **Actions** volet, cliquez sur **ouvrir le journal enregistré** et point toohello les fichiers journaux dans le format etvx/etw (package de prise en charge hello). Vous pouvez désormais afficher les fichiers hello. Après avoir ouvert le fichier de hello, vous pouvez avec le bouton droit et enregistrer le fichier de hello sous forme de texte.
      
      > [!IMPORTANT]
      > Vous pouvez également utiliser hello **Get-WinEvent** tooopen de l’applet de commande ces fichiers dans Windows PowerShell. Pour plus d’informations, consultez [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) Bonjour documentation de référence d’applet de commande Windows PowerShell.
      > 
      > 
5. Lorsque les journaux de hello ouverts dans l’Observateur d’événements, recherchez hello suivant des fichiers journaux qui contiennent la configuration de l’appareil problèmes connexes toohello :
   
   * hcs_pfconfig/Operational Log
   * hcs_pfconfig/Config
6. Dans les fichiers journaux de hello, rechercher des chaînes associées toohello les applets de commande appelée par l’Assistant Installation de hello. Pour obtenir la liste de ces applets de commande, consultez la section [Processus de l’Assistant Première installation](#first-time-setup-wizard-process) . 
7. Si vous n’êtes pas en mesure de toofigure cause hello de problème de hello, vous pouvez [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) pour les étapes suivantes. Hello d’utiliser les étapes [créer une demande de support](storsimple-contact-microsoft-support.md#create-a-support-request) lorsque vous contactez le Support Microsoft pour obtenir une assistance.

## <a name="cmdlets-available-for-troubleshooting"></a>Applets de commande disponibles pour la résolution des problèmes
Utilisez hello les erreurs de connectivité de toodetect applets de commande Windows PowerShell suivantes.

* `Get-NetAdapter`: Utilisez cette applet de commande toodetect la santé hello des interfaces réseau. 
* `Test-Connection`: Utilisez cette applet de commande toocheck hello connectivité à l’intérieur et en dehors du réseau de hello.
* `Test-HcsmConnection`: Utilisez cette applet de commande toocheck hello la connectivité d’un appareil inscrit correctement.

Si 1 de mise à jour sont en cours d’exécution sur votre appareil StorSimple, hello suivant d’applets de commande de diagnostic est également disponible.

* `Sync-HcsTime`: Utilisez cette heure de l’appareil toodisplay applet de commande et forcer une synchronisation avec le serveur NTP hello.
* `Enable-HcsPing`et `Disable-HcsPing`: utilisez ces interfaces réseau d’applets de commande tooallow hello hôtes tooping hello sur votre appareil StorSimple. Par défaut, les interfaces réseau de StorSimple hello ne répondent pas tooping demandes.
* `Trace-HcsRoute`: utilisez cette applet de commande comme un outil de suivi d’itinéraire. Il envoie le routeur tooeach de paquets sur la destination finale du tooa hello moyen sur une période de temps et calcule ensuite les résultats basés sur les paquets hello renvoyés par chaque tronçon. Étant donné que `Trace-HcsRoute` affiche degré hello de perte de paquets sur un routeur ou un lien, vous pouvez identifier les routeurs ou les liens peuvent être à l’origine des problèmes de réseau. 
* `Get-HcsRoutingTable`: Utilisez cette applet de commande toodisplay hello locale table de routage IP.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Résoudre les problèmes avec l’applet de commande Get-NetAdapter hello
Lorsque vous configurez des interfaces réseau pour un déploiement de la première fois, état du matériel hello n’est pas disponible dans hello interface utilisateur du service StorSimple Manager, car l’appareil de hello n’est pas encore inscrit avec le service de hello. En outre, page d’état du matériel hello toujours correctement ne reflètent pas état hello du périphérique de hello, en particulier si des problèmes qui affectent la synchronisation du service. Dans ces situations, vous pouvez utiliser hello `Get-NetAdapter` toodetermine de l’applet de commande hello intégrité et l’état des interfaces réseau.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>toosee une liste de toutes les cartes réseau de hello sur votre appareil
1. Démarrez Windows PowerShell pour StorSimple, puis tapez `Get-NetAdapter`. 
2. Utiliser la sortie hello Hello `Get-NetAdapter` applet de commande et hello suivant les instructions toounderstand hello l’état de votre interface réseau.
   
   * Si l’interface de hello est intègre et activée, hello **ifIndex** l’état est affiché en tant que **des**.
   * Si l’interface de hello est intègre, mais n’est pas physiquement connectée (par un câble réseau), hello **ifIndex** est affiché comme **désactivé**.
   * Si l’interface de hello est intègre mais pas activée, hello **ifIndex** l’état est affiché en tant que **absent**.
   * Si l’interface de hello n’existe pas, il n’apparaît pas dans cette liste. Hello d’interface utilisateur du service StorSimple Manager continue d’afficher cette interface dans un état d’échec.

Pour plus d’informations sur la façon de toouse cette applet de commande, accédez trop[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) Bonjour référence d’applet de commande Windows PowerShell. 

Hello sections suivantes présentent des exemples de sortie de hello `Get-NetAdapter` applet de commande. 

 Dans ces exemples, le contrôleur 0 était le contrôleur passif de hello et a été configuré comme suit :

* DATA 0, DATA 1, DATA 2 et données 3 réseau interfaces existaient sur le périphérique de hello.
* DATA 4 et les cartes d’interface réseau DATA 5 n’étaient pas présentes ; Par conséquent, ils ne sont pas répertoriées dans la sortie de hello.
* DATA 0 était activée.

Contrôleur 1 était le contrôleur actif de hello et a été configuré comme suit :

* DATA 0, DATA 1, données 2, données 3, DATA 4 et réseau DATA 5 interfaces existaient sur le périphérique de hello.
* DATA 0 était activée.

**Exemple de sortie – contrôleur 0**

Hello Voici la sortie de hello du contrôleur 0 (contrôleur passif de hello). DATA 1, DATA 2 et DATA 3 ne sont pas connectées. DATA 4 et DATA 5 ne sont pas répertoriées, car ils ne sont pas présents sur l’appareil de hello. 

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Exemple de sortie – contrôleur 1**

Hello Voici la sortie de hello du contrôleur 1 (contrôleur actif de hello). Uniquement hello DATA 0 interface réseau sur l’appareil de hello est configuré et fonctionne.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Résoudre les problèmes avec l’applet de commande Test-Connection hello
Vous pouvez utiliser hello `Test-Connection` toodetermine de l’applet de commande si votre appareil StorSimple peut se connecter à toohello en dehors du réseau. Si tous les paramètres de mise en réseau hello, y compris hello DNS, sont correctement configurés dans l’Assistant Installation de hello, vous pouvez utiliser hello `Test-Connection` tooping de l’applet de commande une adresse connue en dehors du réseau de hello, comme outlook.com. 

Vous devez activer les problèmes de connectivité tootroubleshoot ping cette applet de commande si ping est désactivée.

Consultez hello suivant des exemples de sortie à partir de hello `Test-Connection` applet de commande. 

> [!NOTE]
> Dans le premier exemple de hello, appareil de hello est configuré avec un DNS incorrect. Dans le deuxième exemple de hello, hello DNS est correct.
> 
> 

**Exemple de sortie – DNS incorrect**

Bonjour suivant l’exemple, aucune sortie n’est pour les adresses IPV4 et IPV6 de hello, ce qui indique que hello que DNS n’est pas résolu. Cela signifie qu’il n’existe aucun toohello de connectivité en dehors du réseau et un DNS correct doit toobe fourni. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Exemple de sortie : DNS correct**

Bonjour suivant l’exemple, hello DNS renvoie hello l’adresse IPV4, indiquant que hello que DNS est correctement configuré. Cela confirme qu’il y a toohello de connectivité en dehors du réseau. 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Résoudre les problèmes avec l’applet de commande Test-HcsmConnection hello
Hello d’utilisation `Test-HcsmConnection` applet de commande pour un périphérique qui est déjà connecté tooand inscrit auprès du service StorSimple Manager. Cette applet de commande vous permet de vérifier la connectivité hello entre un appareil inscrit et le hello correspondant du service StorSimple Manager. Vous pouvez exécuter cette commande sur Windows PowerShell pour StorSimple. 

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>applet de commande Test-HcsmConnection de hello toorun
1. Assurez-vous que cet appareil hello est inscrit.
2. Vérifiez l’état du périphérique hello. Si l’appareil de hello est désactivé, en mode maintenance ou hors connexion, vous pouvez voir hello les erreurs suivantes : 
   
   * ErrorCode.CiSDeviceDecommissioned – indique cet appareil hello est désactivé.
   * ErrorCode.DeviceNotReady – indique cet appareil hello est en mode maintenance.
   * ErrorCode.DeviceNotReady – indique cet appareil hello n’est pas en ligne.
3. Vérifiez que le service StorSimple Manager hello est en cours d’exécution (utilisez hello [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) applet de commande). Si le service de hello ne fonctionne pas, vous pouvez voir hello les erreurs suivantes :
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError : indique qu’une exception est survenue lors de l’exécution de Get-ClusterResource.
4. Vérifiez le jeton du Service de contrôle d’accès (ACS) hello. Si ce dernier lève une exception web, il peut être hello résultat d’un problème de passerelle, une authentification de proxy manquant, un DNS incorrect ou un échec d’authentification. Vous pouvez voir hello les erreurs suivantes :
   
   * ErrorCode.CiSApplianceGateway – indique une exception HttpStatusCode.BadGateway : service de résolution de nom hello n’a pas pu résoudre le nom d’hôte de hello. 
   * ErrorCode.CiSApplianceProxy – indique une exception HttpStatusCode.ProxyAuthenticationRequired (code d’état HTTP 407) : client de hello Impossible d’authentifier avec le serveur de proxy hello. 
   * ErrorCode.CiSApplianceDNSError – indique une exception WebExceptionStatus.NameResolutionFailure : service de résolution de nom hello n’a pas pu résoudre le nom d’hôte de hello.
   * ErrorCode.CiSApplianceACSError – indique que le service de hello a renvoyé une erreur d’authentification, mais il existe une connectivité.
     
     Si l’erreur ne lève pas d’exception web, recherchez ErrorCode.CiSApplianceFailure. Cela indique que hello a échoué.
5. Vérifiez la connectivité de service cloud hello. Si le service de hello lève une exception web, vous pouvez voir hello les erreurs suivantes :
   
   * ErrorCode.CiSApplianceGateway – indique une exception HttpStatusCode.BadGateway : un serveur proxy intermédiaire a reçu une demande incorrecte d’un autre proxy ou du serveur d’origine de hello.
   * ErrorCode.CiSApplianceProxy – indique une exception HttpStatusCode.ProxyAuthenticationRequired (code d’état HTTP 407) : client de hello Impossible d’authentifier avec le serveur de proxy hello. 
   * ErrorCode.CiSApplianceDNSError – indique une exception WebExceptionStatus.NameResolutionFailure : service de résolution de nom hello n’a pas pu résoudre le nom d’hôte de hello.
   * ErrorCode.CiSApplianceACSError – indique que le service de hello a renvoyé une erreur d’authentification, mais il existe une connectivité.
     
     Si l’erreur ne lève pas d’exception web, recherchez ErrorCode.CiSApplianceSaasServiceError. Cela indique un problème avec hello service StorSimple Manager.
6. Vérifiez la connectivité d’Azure Service Bus. ErrorCode.CiSApplianceServiceBusError indique que cet appareil hello ne peut pas se connecter toohello Service Bus.

Hello des fichiers journaux CiSCommandletLog0Curr.errlog et cisagentsvc0curr.errlog plus d’informations, telles que les détails de l’exception. 

Pour plus d’informations sur la façon dont toouse hello applet de commande, accédez trop[Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) dans Windows PowerShell de hello documentation de référence.

> [!IMPORTANT]
> Vous pouvez exécuter cette applet de commande pour hello active et contrôleur passif de hello. 
> 
> 

Consultez hello suivant des exemples de sortie à partir de hello `Test-HcsmConnection` applet de commande. 

**Exemple de sortie : appareil inscrit exécutant StorSimple Release (juillet 2014)**

Hello premier exemple porte sur un périphérique qui a été enregistré avec hello service StorSimple Manager et ne présente aucun problème de connectivité. 

     Controller1>Test-HcsmConnection -verbose
     Checking device state  ... Success.
     Device registered successfully
     Checking device authentication.  ... This operation will take few minutes toocomplete....
     Checking device authentication.  ... Success.
     Checking connectivity from device tooStorSimple Manager service.  ... This operation will take few minutes toocomplete....
     Checking connectivity from device tooStorSimple Manager service.  ... Success.
     Checking connectivity from StorSimple Manager service tooStorSimple device. .... Success.
     Controller1>

**Exemple de sortie : appareil inscrit exécutant StorSimple Update 1**

Si la mise à jour 1 sont en cours d’exécution sur votre appareil StorSimple, vous ne devez pas toorun avec le commutateur de commentaires hello.

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Exemple de sortie : appareil hors connexion exécutant StorSimple Release (juillet 2014)**

Cet exemple est d’un appareil qui a le statut **hors connexion** Bonjour portail Azure classic.

     Checking device state: Success 
     Device is registered successfully 
     Checking connectivity from device tooSaaS.. Failure

Appareil de Hello pas pu se connecter à l’aide de la configuration du proxy web actuelle hello. Cela peut être un problème avec la configuration du proxy web hello ou un problème de connectivité réseau. Dans ce cas, vous devez vous assurer que vos paramètres de proxy web sont corrects et que vos serveurs de proxy web sont en ligne et accessibles. 

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Résoudre les problèmes avec l’applet de commande hello HcsTime de synchronisation
Utilisez cette applet de commande toodisplay hello heure de l’appareil. Si l’heure de l’appareil hello comporte un décalage avec le serveur NTP hello, vous pouvez ensuite utiliser cette applet de commande tooforce-hello être synchronisée avec votre serveur NTP. Si le décalage hello entre l’appareil de hello et le serveur NTP est supérieure à 5 minutes, vous verrez un avertissement. Si le décalage de hello dépasse 15 minutes, les appareils hello mis hors connexion. Vous pouvez toujours utiliser cette applet de commande de tooforce une synchronisation. Toutefois, si le décalage de hello dépasse 15 heures, puis vous ne serez pas en mesure de tooforce-synchroniser l’heure hello et un message d’erreur s’affichera.

**Exemple de sortie : synchronisation forcée à l’aide de l’applet de commande Sync-HcsTime**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Résoudre les problèmes avec les applets de commande Enable-HcsPing et Disable-HcsPing hello
Utilisez ces tooensure applets de commande que les interfaces réseau de hello sur votre appareil répondent tooICMP les requêtes de ping. Par défaut les interfaces réseau de StorSimple hello ne répondent pas tooping demandes. Cette applet de commande est tooknow de façon plus simple de hello si votre appareil est en ligne et accessibles.  

**Exemple de sortie : Enable-HcsPing et Disable-HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Résoudre les problèmes avec l’applet de commande Trace-HcsRoute hello
Utilisez cette applet de commande comme un outil de suivi d’itinéraire. Il envoie le routeur tooeach de paquets sur la destination finale du tooa hello moyen sur une période de temps et calcule ensuite les résultats basés sur les paquets hello renvoyés par chaque tronçon. Étant donné que l’applet de commande hello indique le degré de hello de perte de paquets sur n’importe quel routeur ou lien, vous pouvez identifier les routeurs ou des liens peuvent être à l’origine des problèmes de réseau.

**Résultat de l’exemple montrant comment tootrace hello itinéraire d’un paquet avec HcsRoute de Trace**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Résoudre les problèmes avec l’applet de commande Get-HcsRoutingTable hello
Utilisez cette table de routage d’hello tooview applet de commande pour votre appareil StorSimple. Une table de routage est un ensemble de règles qui peuvent aider à déterminer où les paquets de données circulant sur un réseau IP (Internet Protocol) sont dirigés. 

table de routage Hello montre les interfaces hello et réseaux spécifié hello passerelle que les itinéraires hello toohello de données. Elle donne également la métrique de routage hello est décideur hello pour tooreach de chemin d’accès emprunté hello une destination particulière. Hello inférieur hello routage métrique, hello hello une préférence plus élevée. 

Par exemple, si vous avez 2 interfaces réseau DATA 2 et 3, toohello connecté Internet. Si les métriques de routage hello pour DATA 2 et 3 sont respectivement de 15 et 261, DATA 2 avec une métrique de routage inférieure hello est interface par défaut du hello utilisé tooreach hello Internet.

Si 1 de mise à jour sont en cours d’exécution sur votre appareil StorSimple, votre interface réseau DATA 0 possède une préférence plus élevée de hello pour le trafic cloud hello. Cela implique que, même s’il existe des autres interfaces activé pour le cloud, le trafic de nuage hello serait routé via DATA 0. 

Si vous exécutez hello `Get-HcsRoutingTable` applet de commande sans spécifier tous les paramètres (comme hello suivant montre l’exemple), hello applet de commande affiche les tables de routage IPv4 et IPv6. Vous pouvez également spécifier `Get-HcsRoutingTable -IPv4` ou `Get-HcsRoutingTable -IPv6` tooget une table de routage appropriée.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Exemple de résolution pas à pas des problèmes de StorSimple
Hello suivant montre un dépannage pas à pas d’un déploiement de StorSimple. Dans le scénario d’exemple hello, DRS échoue avec un message d’erreur indiquant que les paramètres de réseau hello ou un nom DNS de hello est incorrecte.

message d’erreur Hello retourné est :

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

Hello erreur pourrait résulter hello suivants :

* Installation matérielle incorrecte
* Interface(s) réseau défectueuse(s)
* Adresse IP, masque de sous-réseau, passerelle, serveur DNS principal ou proxy web incorrect
* Clé d’inscription incorrecte
* Paramètres de pare-feu incorrects

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>problème de l’inscription de périphérique hello toolocate et de correctif
1. Vérifiez votre configuration de périphérique : sur le contrôleur actif de hello, exécutez `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > Assistant Hello doit s’exécuter sur le contrôleur actif de hello. tooverify que vous êtes le contrôleur actif toohello connectés, examinez la bannière hello présentée dans la console série hello. bannière de Hello indique que vous êtes connecté toocontroller 0 ou contrôleur 1, et si le contrôleur de hello est actif ou passif. Pour plus d’informations, consultez trop[identifier un contrôleur actif sur votre appareil](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
   > 
   > 
2. Assurez-vous que cet appareil hello est branché correctement : Vérifiez réseau hello câblage sur périphérique hello fond de panier. câblage de Hello est modèle toohello spécifique de l’appareil. Pour plus d’informations, consultez trop[installer votre appareil StorSimple 8100](storsimple-8100-hardware-installation.md) ou [installer votre appareil StorSimple 8600](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > Si vous utilisez des ports réseau 10 GbE, vous devez hello toouse fourni adaptateurs QSFP-SFP et les câbles SFP. Pour plus d’informations, consultez hello [liste des câbles, commutateurs et transmetteurs recommandés pour les ports hello 10 GbE](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
   > 
   > 
3. Vérifier le fonctionnement de hello d’interface de réseau hello :
   
   * Utilisez hello Get-NetAdapter applet de commande toodetect hello intégrité des hello interfaces réseau Data 0. 
   * Si le lien de hello ne fonctionne pas, hello **ifindex** état indiquera cette interface hello est arrêté. Vous devez ensuite la connexion de réseau toocheck hello de dispositif de toohello port hello et toohello commutateur. Vous devez également toorule câbles incorrect. 
   * Si vous pensez que hello DATA 0 port sur le contrôleur actif de hello a échoué, vous pouvez le vérifier en vous connectant toohello le port DATA 0 sur le contrôleur 1. tooconfirm, débranchez câble hello hello arrière appareil hello du contrôleur 0, connecter hello câble toocontroller 1, puis exécutez de nouveau l’applet de commande Get-NetAdapter de hello. 
     Si hello DATA 0 port sur un contrôleur est défaillant, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) pour les étapes suivantes. Vous devrez peut-être le contrôleur de hello tooreplace sur votre système.
4. Vérifiez que le commutateur de toohello hello connectivité :
   
   * Assurez-vous que les interfaces réseau DATA 0 sur les contrôleurs 0 et 1 dans le boîtier principal sont sur hello même sous-réseau. 
   * Vérification hello concentrateur ou routeur. En règle générale, vous devez vous connecter à la fois toohello contrôleurs même concentrateur ou routeur. 
   * Assurez-vous que hello commutateurs que vous utilisez pour la connexion de hello ont DATA 0 pour les deux contrôleurs Bonjour même réseau local virtuel.
5. Éliminez les erreurs utilisateur :
   
   * Réexécutez l’Assistant Installation de hello (exécuter **Invoke-HcsSetupWizard**), puis entrez hello valeurs nouveau toomake assurer qu’il n’y a aucune erreur. 
   * Vérification de l’inscription de hello clé utilisée. Hello la même clé d’inscription peut être utilisé tooconnect plusieurs périphériques tooa service StorSimple Manager. Utilisez la procédure hello dans [clé d’inscription Get hello](storsimple-manage-service.md#get-the-service-registration-key) tooensure que vous utilisez hello clé d’inscription correcte.
     
     > [!IMPORTANT]
     > Si vous avez plusieurs services en cours d’exécution, vous devez tooensure cette clé d’inscription de hello pour service approprié de hello est appareil de hello tooregister utilisé. Si vous avez enregistré un appareil avec le service StorSimple Manager incorrect hello, vous devez trop[contactez le Support Microsoft](storsimple-contact-microsoft-support.md) pour les étapes suivantes. Vous avez peut-être tooperform une réinitialisation des paramètres de périphérique hello (ce qui peut entraîner une perte de données) toothen connecter toohello destinée service.
     > 
     > 
6. Utilisez tooverify d’applet de commande hello tester la connexion que vous avez toohello de connectivité en dehors du réseau. Pour plus d’informations, consultez trop[dépannage avec l’applet de commande Test-Connection de hello](#troubleshoot-with-the-test-connection-cmdlet).
7. Vérifiez les interférences avec le pare-feu. Si vous avez vérifié que hello virtuel paramètres IP (VIP), de sous-réseau, passerelle et DNS sont corrects et vous rencontrez encore des problèmes de connectivité, puis il est possible que votre pare-feu bloque les communications entre votre appareil et un hello en dehors du réseau. Vous devez tooensure que les ports 80 et 443 sont disponibles sur votre appareil StorSimple pour les communications sortantes. Pour plus d’informations, consultez la page [Configuration réseau requise pour votre appareil StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Consultez les journaux hello. Accédez trop[prennent en charge des packages et des journaux de périphérique disponibles pour le dépannage](#support-packages-and-device-logs-available-for-troubleshooting).
9. Si hello étapes précédentes ne résolvent pas le problème de hello, [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) pour obtenir une assistance.

## <a name="next-steps"></a>Étapes suivantes
[Découvrez comment tootroubleshoot d’appareil opérationnel](storsimple-troubleshoot-operational-device.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
