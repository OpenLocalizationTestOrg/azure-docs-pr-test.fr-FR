---
title: "aaaAzure Active Directory se connecter d’intégrité FAQ - Azure | Documents Microsoft"
description: "Ce FAQ répond aux questions que vous pouvez vous poser au sujet d’Azure AD Connect. Ce forum aux questions couvre les questions sur l’utilisation du service hello, y compris hello prise en charge, les fonctionnalités, limitations et modèle de facturation."
services: active-directory
documentationcenter: 
author: billmath
manager: samueld
editor: curtand
ms.assetid: f1b851aa-54d7-4cb4-8f5c-60680e2ce866
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 3f15d9e9b557b09ef74ceff85806579dd51f2412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-frequently-asked-questions"></a>Forum Aux Questions (FAQ) Azure AD Connect Health
Cet article inclut elles sonttrop des réponses aux questions (FAQ) sur Azure Active Directory (Azure AD) Connect Health. Ces forums aux questions traitent des questions comment toouse hello service, qui inclut hello prise en charge, les fonctionnalités, limitations et modèle de facturation.

## <a name="general-questions"></a>Questions générales
**Q : Je gère plusieurs annuaires Azure AD. Comment basculer toohello disposant d’Azure Active Directory Premium ?**

tooswitch entre différents locataires Azure AD, sélectionnez hello actuellement connecté de **nom d’utilisateur** sur hello coin supérieur droit, puis choisissez compte approprié de hello. Si le compte de hello n’est pas répertorié ici, sélectionnez **se déconnecter**, puis utiliser les références hello administrateur général du répertoire hello disposant d’Azure Active Directory Premium activé toosign dans.

**Q : Quelles versions des rôles d’identité sont prises en charge par Azure AD Connect Health ?**

Bonjour tableau suivant répertorie les rôles hello et les versions de système d’exploitation prises en charge.

|Rôle| Système d’exploitation/version|
|--|--|
|Active Directory Federation Services (AD FS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|
|Azure AD Connect | Version 1.0.9125 ou supérieure|
|Active Directory Domain Services (AD DS)| <ul> <li> Windows Server 2008 R2 </li><li> Windows Server 2012  </li> <li>Windows Server 2012 R2 </li> <li> Windows Server 2016  </li> </ul>|

Notez que les fonctionnalités de hello fournies par le service de hello peuvent varier en fonction de rôle de hello et le système d’exploitation de hello. En d’autres termes, toutes les fonctionnalités de hello peut-être pas disponibles pour toutes les versions de système d’exploitation. Consultez les descriptions de fonctionnalités hello pour plus d’informations.

**Q : combien de licences faire ai-je besoin toomonitor mon infrastructure ?**

* Hello première Connect Health Agent nécessite au moins une licence Azure AD Premium.
* Chaque nouvel agent inscrit nécessite 25 licences Azure AD Premium supplémentaires.
* Nombre d’agents est équivalent toohello le nombre total d’agents qui sont inscrits sur tous les rôles analysés (AD FS, Azure AD Connect et/ou les services AD DS).

Informations de licence se trouve également sur hello [page Azure Active Directory tarification](https://aka.ms/aadpricing).

Exemple :

| Agents inscrits | Licences nécessaires | Exemple de configuration de surveillance |
| ------ | --------------- | --- |
| 1 | 1 | 1 serveur Azure AD Connect |
| 2 | 26| 1 serveur Azure AD Connect et 1 contrôleur de domaine |
| 3 | 51 | 1 serveur Active Directory Federation Services (AD FS), 1 proxy AD FS et 1 contrôleur de domaine |
| 4 | 76 | 1 serveur AD FS, 1 proxy AD FS et 2 contrôleurs de domaine |
| 5 | 101 | 1 serveur Azure AD Connect, 1 serveur AD FS, 1 proxy AD FS et 2 contrôleurs de domaine |


## <a name="installation-questions"></a>Questions sur l’installation

**Q : qu’est impact hello d’installation hello Agent Azure AD Connect Health sur des serveurs individuels ?**

impact de Hello de l’installation des serveurs proxy d’applications web Microsoft Azure AD Connect Health Agent, AD FS, hello, des serveurs de Azure AD Connect (synchronisation), des contrôleurs de domaine est minime avec respect toohello processeur, la consommation de mémoire, la bande passante réseau et de stockage.

Hello suit les numéros est approximatifs :

* Consommation du processeur : environ 1-5 % d’augmentation.
* La consommation de mémoire : mémoire totale du système de hello % too10.

> [!NOTE]
> Si l’agent de hello ne peut pas communiquer avec Azure, l’agent de hello stocke les données de hello localement pour une limite maximale définie. l’agent de Hello remplace les données de « mise en cache » hello sur une base « service moins récemment ».
>
>

* Stockage de mémoire tampon locale pour les agents Azure AD Connect Health : environ 20 Mo.
* Pour les serveurs AD FS, nous recommandons que vous configuriez un espace disque de 1 024 Mo (1 Go) pour le canal d’audit hello AD FS Agents Azure AD Connect d’intégrité tooprocess toutes les données d’audit hello avant son remplacement.

**Q : dois-je tooreboot mes serveurs pendant l’installation de hello des Agents d’intégrité de Connect hello Azure AD ?**

Non. installation de Hello d’agents de hello ne nécessite pas de serveur hello tooreboot. Toutefois, l’installation de certaines étapes requises peut nécessiter un redémarrage du serveur de hello.

Par exemple, sur Windows Server 2008 R2, l’installation de .NET 4.5 Framework requiert un redémarrage du serveur.

**Q : Le service Azure AD Connect Health fonctionne-t-il par le biais d’un proxy HTTP intermédiaire ?**

Oui. Les opérations en cours, vous pouvez configurer hello Agent d’intégrité toouse un demandes HTTP sortantes HTTP proxy tooforward.
Pour plus d’informations sur la [configuration du proxy HTTP pour les agents Health, voir ](active-directory-aadconnect-health-agent-install.md#configure-azure-ad-connect-health-agents-to-use-http-proxy).

Si vous devez tooconfigure un serveur proxy lors de l’inscription de l’agent, vous devrez peut-être toomodify vos paramètres de Proxy Internet Explorer au préalable.

1. Allez dans Internet Explorer > **Paramètres** > **Options Internet** > **Connexions** > **Paramètres de réseau local**.
2. Sélectionnez **Utiliser un serveur proxy pour votre réseau local**.
3. Sélectionnez **Avancé** si vous disposez de ports proxy différents pour les protocoles HTTP et HTTPS sécurisé.

**Q : est l’authentification de base Azure AD Connect Health prise en charge lors de la connexion tooHTTP proxys ?**

Non. Un mécanisme toospecify un nom d’utilisateur arbitraire et un mot de passe pour l’authentification de base est actuellement pas en charge.

**Q : que faire les ports de pare-feu ai-je besoin tooopen pour hello Azure AD Connect Health Agent toowork ?**

Consultez hello [section Configuration requise](active-directory-aadconnect-health-agent-install.md#requirements) pour la liste des ports de pare-feu et d’autres besoins en connectivité hello.

**Q : pourquoi deux serveurs avec le même nom dans le portail de hello Azure AD Connect Health de hello ?**

Lorsque vous supprimez un agent à partir d’un serveur, le serveur de hello n’est pas supprimé automatiquement à partir du portail d’Azure AD Connect Health hello. Si vous supprimez un agent à partir d’un serveur ou supprimez le serveur hello lui-même manuellement, vous devez entrée de serveur hello toomanually supprimer à partir du portail de hello Azure AD Connect Health.

Vous pouvez créer une nouvelle image d’un serveur ou créer un nouveau serveur avec hello mêmes détails (par exemple, le nom de l’ordinateur). Si vous n’avez pas supprimé le serveur déjà inscrit de hello à partir du portail de hello Azure AD Connect Health, et que vous avez installé l’agent de hello sur le nouveau serveur de hello, vous pouvez voir deux entrées avec hello même nom.

Dans ce cas, supprimez manuellement entrée hello appartenant toohello ancien serveur. données Hello pour ce serveur doivent être obsolètes.

## <a name="health-agent-registration-and-data-freshness"></a>Inscription de l’agent Health et actualisation des données

**Q : quelles sont les raisons courantes pour les échecs de l’inscription de l’Agent d’intégrité hello et comment résoudre les problèmes ?**

Hello agent d’intégrité peut échouer tooregister échéance toohello suit les raisons possibles :

* l’agent de Hello ne peut pas communiquer avec les points de terminaison hello requis, car un pare-feu bloque le trafic. Cela est particulièrement courant sur les serveurs proxy d’application web. Assurez-vous que vous avez autorisé les ports et les points de terminaison de communication sortante toohello requis. Consultez hello [section Configuration requise](active-directory-aadconnect-health-agent-install.md#requirements) pour plus d’informations.
* Les communications sortantes sont l’inspection SSL tooan soumis par la couche réseau hello. Cela entraîne le certificat hello par l’agent de hello toobe remplacé par entité hello inspection serveur et Échec de l’enregistrement de l’agent hello étapes toocomplete hello.
* utilisateur de Hello n’a pas accès tooperform hello inscription de l’agent de hello. Par défaut, les administrateurs globaux possèdent les droits d’accès. Vous pouvez utiliser [Role Based Access Control](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) toodelegate accès tooother les utilisateurs.

**Q : je suis obtention averti que « données de Service de contrôle d’intégrité ne sont pas de toodate. » Comment résoudre les problème de hello ?**

Azure AD Connect Health génère l’alerte de hello lorsqu’il ne reçoit pas tous les points de données hello du serveur hello Bonjour deux dernières heures. Le déclenchement de cette alerte peut avoir plusieurs origines.

* l’agent de Hello ne peut pas communiquer avec les points de terminaison hello requis, car un pare-feu bloque le trafic. Cela est particulièrement courant sur les serveurs proxy d’application web. Assurez-vous que vous avez autorisé les ports et les points de terminaison de communication sortante toohello requis. Consultez hello [section Configuration requise](active-directory-aadconnect-health-agent-install.md#requirements) pour plus d’informations.
* Les communications sortantes sont l’inspection SSL tooan soumis par la couche réseau hello. Cela entraîne le certificat hello par l’agent de hello toobe remplacé par entité hello inspection serveur et service de Azure AD Connect Health toohello tooupload données hello échoue.
* Vous pouvez utiliser la commande de connectivité hello intégré à l’agent de hello. [En savoir plus](active-directory-aadconnect-health-agent-install.md#test-connectivity-to-azure-ad-connect-health-service).
* les agents Hello prennent également en charge la connectivité sortante via un HTTP Proxy non authentifiés. [En savoir plus](active-directory-aadconnect-health-agent-install.md##configure-azure-ad-connect-health-agents-to-use-http-proxy).

## <a name="operations-questions"></a>Questions sur les opérations
**Q : dois-je tooenable l’audit sur les serveurs proxy de hello web application ?**

Non, audits ne doivent pas toobe activée sur les serveurs proxy de hello web application.

**Q : Comment les alertes Azure AD Connect Health sont-elles résolues ?**

Les alertes Azure AD Connect Health sont résolues en cas de condition de réussite. Agents Azure AD Connect d’intégrité détecter et signaler le service de toohello de conditions de réussite hello régulièrement. Pour certaines alertes, suppression de hello est basé sur le temps. En d’autres termes, si hello même condition d’erreur n’est pas respectée dans les 72 heures à partir de la génération d’alertes, hello est résolue automatiquement.

**Q : je suis obtention averti que « demande d’authentification de Test (Transaction synthétique) Échec tooobtain un jeton ». Comment résoudre les problème de hello ?**

Azure AD Connect Health pour AD FS génère cette alerte en cas de hello installé sur un serveur AD FS de l’Agent d’intégrité tooobtain un jeton dans le cadre d’une transaction synthétique initiée par l’Agent d’intégrité de hello. l’agent d’intégrité Hello utilise le contexte du système local hello et tente de tooget un jeton pour un personnel de confiance. Il s’agit d’un tooensure de tout test AD FS est dans un état d’émission de jetons.

Plus souvent ce test échoue car hello Agent d’intégrité est nom de la batterie impossible tooresolve hello AD FS. Cela peut se produire si les serveurs hello AD FS se trouvent derrière un équilibrage de charge réseau et de demande de hello obtient initiée à partir d’un nœud qui est derrière un équilibreur de charge hello (en tant que client régulière tooa exécutée est devant l’équilibrage de charge hello). Cela peut être fixe en mettant à jour le fichier hello « hosts » situé sous l’adresse d’IP « C:\Windows\System32\drivers\etc » tooinclude hello du serveur de hello AD FS ou d’une adresse IP de bouclage (127.0.0.1) pour le nom de la batterie hello AD FS (par exemple, sts.contoso.com). Ajout du fichier hôte hello sera court-circuit appel de réseau hello, permettant ainsi de jeton de hello tooget hello Agent d’intégrité.

**Q : j’ai reçu un message électronique indiquant que mes machines ne sont pas corrigés pour effectuer des attaques ransomeware récente hello. Pourquoi ai-je reçu cet e-mail ?**

Service de Azure AD Connect Health analysés hello tous les ordinateurs qu’il surveille les correctifs logiciels de tooensure hello requis ont été installés. messagerie de Hello a été envoyé les administrateurs de clients toohello si au moins un ordinateur n’a pas de correctifs critiques de hello. Hello suite logique a été utilisé toomake cette détermination.
1. Rechercher tous les correctifs hello installés sur l’ordinateur de hello.
2. Vérifiez si au moins un des hello correctifs à partir de hello liste définie est présent.
3. Si Oui, l’ordinateur de hello est protégé. Si ce n’est pas le cas, machine de hello est risque d’attaque de hello.

Vous pouvez utiliser hello suivant tooperform de script PowerShell cette vérification manuellement. Il implémente hello ci-dessus logique.

```
Function CheckForMS17-010 ()
{
    $hotfixes = "KB3205409", "KB3210720", "KB3210721", "KB3212646", "KB3213986", "KB4012212", "KB4012213", "KB4012214", "KB4012215", "KB4012216", "KB4012217", "KB4012218", "KB4012220", "KB4012598", "KB4012606", "KB4013198", "KB4013389", "KB4013429", "KB4015217", "KB4015438", "KB4015546", "KB4015547", "KB4015548", "KB4015549", "KB4015550", "KB4015551", "KB4015552", "KB4015553", "KB4015554", "KB4016635", "KB4019213", "KB4019214", "KB4019215", "KB4019216", "KB4019263", "KB4019264", "KB4019472", "KB4015221", "KB4019474", "KB4015219", "KB4019473"

    #checks hello computer it's run on if any of hello listed hotfixes are present
    $hotfix = Get-HotFix -ComputerName $env:computername | Where-Object {$hotfixes -contains $_.HotfixID} | Select-Object -property "HotFixID"

    #confirms whether hotfix is found or not
    if (Get-HotFix | Where-Object {$hotfixes -contains $_.HotfixID})
    {
        "Found HotFix: " + $hotfix.HotFixID
    } else {
        "Didn't Find HotFix"
    }
}

CheckForMS17-010

```



## <a name="related-links"></a>Liens connexes
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Installation de l’agent Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Opérations Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Utilisation d’Azure AD Connect Health avec AD FS](active-directory-aadconnect-health-adfs.md)
* [Utilisation d'Azure AD Connect Health pour la synchronisation (en Anglais)](active-directory-aadconnect-health-sync.md)
* [Utilisation d’Azure AD Connect Health avec AD DS](active-directory-aadconnect-health-adds.md)
* [Historique des versions d’Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
