---
title: "aaaGetting a démarré le serveur Azure multi-Factor Authentication | Documents Microsoft"
description: "Il s’agit de page d’authentification multifacteur Azure hello qui décrit comment tooget démarrer avec le serveur Azure MFA."
services: multi-factor-authentication
keywords: "authentification serveur, page d’activation d’application d’authentification Azure Multi Factor Authentication, téléchargement du serveur d’authentification"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Prise en main de hello serveur Azure multi-Factor Authentication

<center>![MFA en local](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Maintenant que nous avons déterminé toouse local Server de l’authentification multifacteur, allons-y. Cette page traite une nouvelle installation du serveur de hello et de la configuration Active Directory local. Si vous avez déjà hello MFA server êtes installé et que vous cherchez tooupgrade, consultez [mise à niveau toohello dernière serveur Azure multi-Factor Authentication](multi-factor-authentication-server-upgrade.md). Si vous recherchez des informations sur l’installation de simplement les service hello web, consultez [hello du déploiement de Service Web d’application Azure multi-Factor Authentication Server Mobile](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Planifier votre déploiement

Avant de télécharger hello serveur Azure multi-Factor Authentication, pensez à votre charge et les exigences de haute disponibilité. Utilisez cette toodecide informations comment et où toodeploy.

Recommandé pour la quantité de hello de mémoire dont vous avez besoin est nombre hello d’utilisateurs souhaitées tooauthenticate régulièrement.

| Utilisateurs | RAM |
| ----- | --- |
| 1-10,000 | 4 Go |
| 10,001-50,000 | 8 Go |
| 50,001-100,000 | 12 Go |
| 100,000-200,001 | 16 Go |
| 200,001+ | 32 Go |

Devez tooset installer plusieurs serveurs pour la haute disponibilité ou l’équilibrage de charge ? Il existe un certain nombre de façons les tooset cette configuration avec le serveur Azure MFA. Lorsque vous installez votre premier serveur de l’authentification Multifacteur Azure, il devient le maître de hello. Tous les serveurs supplémentaires deviennent subordonnés et synchronisent automatiquement des utilisateurs et configuration avec maître de hello. Ensuite, vous pouvez configurer un serveur principal et les autres hello agissent comme sauvegarde, ou vous pouvez configurer équilibrage de charge entre tous les serveurs hello.

Lorsqu’un serveur Azure MFA maître est déconnecté, les serveurs subordonnés hello peuvent toujours traiter les demandes de vérification en deux étapes. Toutefois, vous ne pouvez pas ajouter des utilisateurs et les utilisateurs existants ne peut pas mettre à jour leurs paramètres jusqu'à ce que le maître de hello est remis en ligne ou secondaire est promue.

### <a name="prepare-your-environment"></a>Préparation de votre environnement

Vérifiez que serveur hello que vous utilisez pour l’authentification multifacteur Azure présente hello suivant les exigences :

| Configuration requise du serveur Azure Multi-Factor Authentication | Description |
|:--- |:--- |
| Matériel |<li>200 Mo d’espace disque</li><li>Processeur compatible x32 ou x64</li><li>1 Go de RAM ou plus</li> |
| Logiciel |<li>Windows Server 2008 ou supérieur, si l’hôte hello est un serveur de système d’exploitation</li><li>Windows 7 ou version ultérieure si l’hôte hello est un système d’exploitation client</li><li>Microsoft .NET 4.0 Framework</li><li>IIS version 7.0 ou ultérieure si l’installation hello utilisateur portail ou un service web SDK</li> |

### <a name="azure-mfa-server-components"></a>Composants du serveur Azure MFA

Le serveur Azure MFA est constitué de trois composants Web :

* Le Service SDK - permet la communication avec hello d’autres composants et est installé sur le serveur d’applications Azure MFA hello Web
* Portail de l’utilisateur - un site web IIS qui permet aux utilisateurs tooenroll dans Azure multi-Factor Authentication (MFA) et de gérer leurs comptes.
* Service d’application Web mobile - permet à l’aide d’une application mobile comme application de Microsoft Authenticator hello pour vérification en deux étapes.

Les trois composants peuvent être installés sur hello server même si le serveur de hello est connecté à internet. Si l’arrêt des composants de hello, hello SDK du Service Web est installé sur le serveur d’applications Azure MFA hello et hello portail de l’utilisateur et Service Web d’application Mobile sont installés sur un serveur connecté à internet.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Configuration requise du serveur Azure Multi-Factor Authentication

Chaque serveur de l’authentification Multifacteur doit être en mesure de toocommunicate sur le port 443 sortant toohello est suivant adresses :

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Si le pare-feu sortants sont restreints sur le port 443, ouvrez hello suivant des plages d’adresses IP :

| Sous-réseau IP | Masque réseau | Plage d’adresses IP |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Si vous n’utilisez pas de fonctionnalité de Confirmation d’événement hello et que vos utilisateurs ne sont pas à l’aide de tooverify des applications mobiles à partir de périphériques sur le réseau d’entreprise de hello, vous devez uniquement hello suivant plages :

| Sous-réseau IP | Masque réseau | Plage d’adresses IP |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Télécharger hello serveur Azure multi-Factor Authentication

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.
2. Sur hello gauche, sélectionnez **Active Directory**
3. Cliquez sur **Utilisateurs et groupes**
4. Cliquez sur **Tous les utilisateurs**
5. Cliquez sur **Authentification multifacteur**
6. Dans la section **Authentification multifacteur**, sélectionnez **Paramètres du service**

   ![Page Paramètres du service](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Dans la page Paramètres de services hello, bas hello écran hello, cliquez sur **Go toohello portal**. Une nouvelle page s’ouvre.
7. Cliquez sur **Téléchargements**.
8. Cliquez sur hello **télécharger** lier et enregistrer le programme d’installation hello.

   ![Télécharger le serveur MFA](./media/multi-factor-authentication-get-started-server/download4.png)

9. Laissez cette page ouverte nous appelons tooit après le programme d’installation de hello en cours d’exécution.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>Installer et configurer le serveur Azure multi-Factor Authentication de hello

Maintenant que vous avez téléchargé le serveur hello vous pouvez installer et configurer. Veillez à ce serveur hello sur que vous l’installez répond aux conditions requises répertoriées dans la planification de la section de hello.

1. Double-cliquez sur hello exécutable.
2. Sur l’écran de sélection du dossier Installation Bonjour, assurez-vous que le dossier hello est correct, cliquez sur **suivant**.
3. Une fois l’installation de hello est terminée, cliquez sur **Terminer**.  Assistant de configuration Hello démarre.
4. Sur l’écran Bienvenue hello configuration Assistant, vérifiez **ignorer à l’aide de hello Assistant de Configuration de l’authentification** et cliquez sur **suivant**.  Hello Assistant se ferme et le démarrage du serveur hello.

   ![Cloud](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Retour hello page que nous avons téléchargé serveur hello à partir de, cliquez sur hello **générer les informations d’identification d’Activation** bouton. Copier ces informations dans hello serveur Azure MFA dans des zones de hello fournies et cliquez sur **activer**.

## <a name="send-users-an-email"></a>Envoi d’un e-mail aux utilisateurs

lancement tooease, d’autoriser le serveur MFA toocommunicate avec vos utilisateurs. Serveur MFA peut envoyer un courrier électronique tooinform leur qu’ils ont été inscrits pour la vérification en deux étapes.

messagerie Hello que vous envoyez doit être déterminée par la configuration de vos utilisateurs pour la vérification en deux étapes. Par exemple, si vous êtes en mesure de tooimport les numéros de téléphone à partir de l’annuaire de l’entreprise hello, par courrier électronique hello doit inclure les numéros de téléphone hello par défaut afin que les utilisateurs savent quels tooexpect. Si vous n’importez pas de numéros de téléphone ou vos utilisateurs vont application mobile de toouse hello, leur envoyer un message électronique qui les dirige toocomplete l’inscription de leur compte. Inclure un lien hypertexte de toohello portail d’utilisateur Azure multi-Factor Authentication par courrier électronique hello.

le contenu des messages électroniques de hello Hello varie également selon la méthode hello de vérification qui a été définie pour l’utilisateur hello (appel téléphonique, SMS ou application mobile).  Par exemple, si l’utilisateur de hello est requis toouse un code confidentiel pour s’authentifier, par courrier électronique hello lui indique ce que son code PIN initial a été défini.  Les utilisateurs est requis toochange leur code confidentiel lors de leur première vérification.

### <a name="configure-email-and-email-templates"></a>Configuration du courrier électronique et des modèles de courrier électronique

Sur hello messagerie icône hello de gauche tooset des paramètres de hello pour l’envoi de ces messages électroniques. Cette page est où vous pouvez entrer des informations hello SMTP de votre messagerie serveur et envoyer un courrier électronique en vérifiant hello **envoyer des e-mails toousers** case à cocher.

![Configuration de la messagerie du serveur MFA](./media/multi-factor-authentication-get-started-server/email1.png)

Sur l’onglet contenu des E-mails de hello, vous pouvez voir les modèles de messagerie hello toochoose disponible à partir de. Selon comment vous avez configuré votre vérification en deux étapes de tooperform les utilisateurs, choisissez le modèle hello qui vous convient le mieux.

![Modèles d’e-mail du serveur MFA](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Importation des utilisateurs à partir d'Active Directory

Maintenant que le serveur hello est installé, vous devez tooadd utilisateurs. Vous pouvez choisir toocreate manuellement, importer des utilisateurs d’Active Directory ou configurer la synchronisation automatique avec Active Directory.

### <a name="manual-import-from-active-directory"></a>Importation manuelle à partir d’Active Directory

1. Bonjour, le serveur Azure MFA sur hello gauche, sélectionnez **utilisateurs**.
2. Au bas de hello, sélectionnez **importer à partir d’Active Directory**.
3. Maintenant vous pouvez soit rechercher des utilisateurs individuels ou hello de recherche annuaire AD pour les unités d’organisation avec des utilisateurs dans les.  Dans ce cas, nous spécifions d’unité d’organisation des utilisateurs hello.
4. Mettez en surbrillance tous les utilisateurs de hello sur hello droit et cliquez sur **importation**.  Vous devriez recevoir un message vous indiquant que l’opération a été réalisée avec succès.  Fenêtre d’importation hello fermer.

   ![Importation des utilisateurs du serveur MFA](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Synchronisation automatique avec Active Directory

1. Bonjour, le serveur Azure MFA sur hello gauche, sélectionnez **intégration d’annuaire**.
2. Accédez toohello **synchronisation** onglet.
3. En bas de hello, choisissez **ajouter**
4. Bonjour **ajouter un élément de synchronisation** boîte qui apparaît choisissez hello domaine, unité d’organisation **ou** groupe de sécurité, paramètres, méthode par défaut et langage par défaut pour cette synchronisation de tâches et cliquez sur **Ajouter**.
5. Case à cocher hello appelée **activer la synchronisation avec Active Directory** et choisissez une **l’intervalle de synchronisation** entre une minute et 24 heures.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>Comment hello serveur Azure multi-Factor Authentication traite les données utilisateur

Lorsque vous utilisez hello serveur multi-Factor Authentication (MFA) localement, les données d’un utilisateur sont stockées dans hello sur des serveurs locaux. Aucune donnée utilisateur persistante n’est stockée dans le cloud de hello. Lorsque l’utilisateur de hello qui effectue une vérification en deux étapes, hello serveur MFA envoie des données toohello vérification de l’authentification Multifacteur Azure cloud service tooperform hello. Lorsque ces demandes d’authentification sont envoyés de service de cloud computing toohello, hello champs suivants sont envoyés dans les journaux et de la demande de hello afin qu’ils soient disponibles dans les rapports de l’authentification de l’utilisation du client hello. Certains des champs de hello étant facultatif peut être activés ou désactivés dans hello serveur multi-Factor Authentication. communication Hello hello service de cloud serveur MFA toohello MFA utilise SSL/TLS sur le port 443 sortant. Ces champs sont les suivants :

* ID unique : nom d'utilisateur ou ID du serveur MFA interne
* Prénom et nom (facultatif)
* Adresse de messagerie (facultatif)
* Numéro de téléphone : en cas d'authentification par appel vocal ou SMS
* Jeton du périphérique : en cas d'authentification par application mobile
* mode d'authentification
* Résultat de l'authentification
* Nom du serveur MFA
* Adresse IP du serveur MFA
* Adresse IP du client (si disponible)

En outre, toohello champs ci-dessus, résultat de la vérification hello (réussite/refus) et la raison de tout refus est également stockée avec les données d’authentification hello et disponibles via les rapports d’utilisation de l’authentification/hello.

## <a name="back-up-and-restore-azure-mfa-server"></a>Sauvegarder et restaurer le serveur Azure MFA

S’assurer que vous disposez d’une sauvegarde saine est un tootake étape importante avec n’importe quel système.

tooback Azure MFA Server, assurez-vous que vous disposez d’une copie de hello **C:\Program Files\Multi-Factor Authentication Server\Data** dossier notamment hello **PhoneFactor.pfdata** fichier. 

En l’occurrence, une restauration est nécessaire hello complète comme suit :

1. Réinstallez le serveur Azure MFA sur un nouveau serveur.
2. Activer hello nouveau serveur Azure MFA.
3. Arrêt hello **MultiFactorAuth** service.
4. Remplacer hello **PhoneFactor.pfdata** avec hello sauvegardé.
5. Démarrer hello **MultiFactorAuth** service.

Hello nouveau serveur est maintenant en cours d’exécution avec hello d’origine sauvegardé configuration et les données utilisateur.

## <a name="next-steps"></a>Étapes suivantes

- Installer et configurer hello [portail de l’utilisateur](multi-factor-authentication-get-started-portal.md) pour utilisateur libre-service.
- Installer et configurer hello du serveur Azure MFA avec [Active Directory Federation Services](multi-factor-authentication-get-started-adfs.md), [l’authentification RADIUS](multi-factor-authentication-get-started-server-radius.md), ou [l’authentification LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Installez et configurez la [passerelle des services Bureau à distance et Azure Multi-Factor Authentication Server avec RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- [Déployer hello Service Web d’application Azure multi-Factor Authentication Server Mobile](multi-factor-authentication-get-started-server-webservice.md).
- [Scénarios avancés avec Azure Multi-Factor Authentication et des VPN tiers](multi-factor-authentication-advanced-vpn-configurations.md).
