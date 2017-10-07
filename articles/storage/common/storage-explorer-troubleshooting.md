---
title: "guide de dépannage de l’Explorateur de stockage aaaAzure | Documents Microsoft"
description: "Vue d’ensemble de la fonctionnalité de débogage hello deux de Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 5152f70418707d65c0a4bce9a916336829956219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a>Guide de résolution des problèmes de l’Explorateur de stockage Azure

## <a name="introduction"></a>Introduction

Explorateur de stockage Microsoft Azure (aperçu) est une application autonome qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, Mac OS et Linux. application Hello peut se connecter comptes toStorage hébergées sur Azure, les Clouds souverains et pile d’Azure.

Ce guide résume les solutions aux problèmes couramment rencontrés dans l’Explorateur de stockage.

## <a name="sign-in-issues"></a>Problèmes de connexion

Avant de continuer, essayez de redémarrer votre application et voir si des problèmes de hello peuvent être résolus.

### <a name="error-self-signed-certificate-in-certificate-chain"></a>Erreur : certificat auto-signé dans la chaîne d’approbation

Il existe plusieurs raisons pour lesquelles vous pouvez rencontrer cette erreur et hello deux causes principales sont les suivantes :

1. application Hello est connectée via un « proxy transparent », ce qui signifie un serveur (par exemple, le serveur de votre entreprise) est intercepte le trafic HTTPS, déchiffrage et chiffrer à l’aide d’un certificat auto-signé.

2. Vous exécutez une application, telles que les antivirus qui injecte un certificat SSL auto-signé dans les messages hello HTTPS que vous recevez.

Lorsque l’Explorateur de stockage rencontre un des problèmes de hello, il peut ne plus savoir si le message de salutation reçu HTTPS a été modifié. Si vous avez une copie du certificat auto-signé de hello, vous pouvez laisser l’Explorateur de stockage de confiance. Si vous ne savez pas qui injecte les certificats hello, suivez ces étapes toofind il :

1. Installez Open SSL.

    - [Windows](https://slproweb.com/products/Win32OpenSSL.html) (une des versions de lumière hello doit être suffisamment)

    - Mac et Linux : doit être inclus dans votre système d’exploitation

2. Exécutez Open SSL.

    - Windows : ouvrez le répertoire d’installation Bonjour, cliquez sur **/bin/**, puis double-cliquez sur **openssl.exe**.
    - Mac et Linux : exécutez **openssl** à partir d’un terminal.

3. Exécutez s_client -showcerts -connect microsoft.com:443.

4. Recherchez les certificats auto-signés. Si vous ne savez pas laquelle sont auto-signés, rechercher n’importe où dans l’objet hello (« %s ») et l’émetteur (« i ») sont hello identiques.

5. Lorsque vous avez trouvé les certificats auto-signés, pour chacune d’elles, copier- coller tous les éléments à **---BEGIN CERTIFICATE---** trop**---END CERTIFICATE---** tooa fichier .cer.

6. Ouvrez l’Explorateur de stockage, cliquez sur **modifier** > **certificats SSL** > **les certificats d’importation**et puis utilisez hello fichier sélecteur toofind, sélectionnez, et ouvrez les fichiers .cer hello que vous avez créé.

Si vous ne trouvez pas les certificats auto-signés à l’aide de hello étapes ci-dessus, nous contacter via l’outil commentaires hello pour plus d’informations.

### <a name="unable-tooretrieve-subscriptions"></a>Impossible de tooretrieve abonnements

Si vous êtes tooretrieve Impossible de vos abonnements après avoir se connecter avec succès, suivez ces étapes tootroubleshoot ce problème :

- Vérifiez que votre compte a accès toohello abonnements en vous connectant à hello portail Azure.

- Assurez-vous que vous êtes connecté à l’aide d’environnement approprié de hello (Azure, Azure Chine, Azure en Allemagne, Azure du gouvernement ou pile d’environnement/Azure personnalisée).

- Si vous êtes derrière un proxy, assurez-vous que vous avez configuré un proxy de l’Explorateur de stockage hello correctement.

- Essayez de supprimer et readding compte de hello.

- Essayez de supprimer les hello fichiers suivants à partir de votre répertoire racine (autrement dit, C:\Users\ContosoUser), puis rajoutez les compte hello :

    - .adalcache

    - .devaccounts

    - .extaccounts

- Console des outils de développement espion hello (en appuyant sur F12) lorsque vous vous connectez des messages d’erreur :

![Outils de développement](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a>Page d’authentification hello toosee Impossible

Si vous êtes page d’authentification impossible toosee hello, procédez comme tootroubleshoot de ces étapes de ce problème :

- Selon la vitesse de votre connexion de hello, elle peut prendre un certain temps pour tooload de page de connexion hello, attendez au moins une minute avant de fermer la boîte de dialogue d’authentification hello.

- Si vous êtes derrière un proxy, assurez-vous que vous avez configuré un proxy de l’Explorateur de stockage hello correctement.

- Afficher la console du développeur hello en appuyant sur la touche F12 de hello. Regardez des réponses hello à partir de la console de développement hello et observez si vous pouvez rechercher un indice pour la raison pour laquelle l’authentification ne fonctionne ne pas.

### <a name="cannot-remove-account"></a>Impossible de supprimer un compte

Si vous n’êtes pas tooremove un compte ou si hello authentifier de nouveau lien ne fait rien, suivez ces étapes tootroubleshoot ce problème :

- Essayez de supprimer les hello fichiers suivants à partir de votre répertoire racine et puis readding compte de hello :

    - .adalcache

    - .devaccounts

    - .extaccounts

- Si vous souhaitez tooremove SAS attaché à des ressources de stockage, supprimez hello fichiers suivants :

    - Dossier %AppData%/StorageExplorer pour Windows

    - /Users/<votre_nom>/Library/Application Support/StorageExplorer pour Mac

    - ~/.config/StorageExplorer pour Linux

> [!NOTE]
>  Vous devez tooreenter vos informations d’identification si vous supprimez ces fichiers.

## <a name="proxy-issues"></a>Problèmes de proxy

Tout d’abord, assurez-vous que vous avez entré des informations suivantes de hello sont tous corrects :

- Hello URL de proxy et le port numéro

- Nom d’utilisateur et mot de passe si nécessaire par proxy de hello

### <a name="common-solutions"></a>Solutions courantes

Si vous rencontrez encore des problèmes, suivez ces étapes tootroubleshoot les :

- Si vous pouvez vous connecter à toohello Internet sans utiliser de votre proxy, vérifiez que l’Explorateur de stockage fonctionne sans paramètres de proxy activées. Si c’est le cas de hello, il peut être un problème avec vos paramètres de proxy. Travailler avec vos problèmes de proxy administrateur tooidentify hello.

- Vérifiez que les autres applications à l’aide du serveur de proxy hello fonctionnent comme prévu.

- Vérifiez que vous pouvez vous connecter à l’aide de votre navigateur web du portail Microsoft Azure toohello

- Vérifiez que vous pouvez recevoir des réponses de vos points de terminaison de service. Entrez une des URL de point de terminaison dans votre navigateur. Si vous pouvez vous connecter, vous devez recevoir une réponse XML InvalidQueryParameterValue ou similaire.

- Si quelqu’un d’autre utilise également l’Explorateur de stockage avec votre serveur proxy, vérifiez que cette personne peut se connecter. Si elles peuvent se connecter, vous avez peut-être toocontact votre administrateur du serveur proxy.

### <a name="tools-for-diagnosing-issues"></a>Outils pour diagnostiquer les problèmes

Si vous disposez des outils de mise en réseau, tel que Fiddler pour Windows, vous pouvez être en mesure de toodiagnose des problèmes hello comme suit :

- Si vous avez toowork via votre proxy, vous avez peut-être tooconfigure votre tooconnect outil réseau via le proxy hello.

- Vérifiez le numéro de port de hello utilisé par votre outil de mise en réseau.

- Entrez l’URL de l’hôte local hello et hello numéro de port de l’outil de mise en réseau en tant que paramètres de proxy dans l’Explorateur de stockage. Si cette quotidiennea lieu, votre outil de mise en réseau lance correctement les demandes réseau apportées par les points de terminaison de l’Explorateur de stockage toomanagement et le service de journalisation. Par exemple, entrez https://cawablobgrs.blob.core.windows.net/ pour votre point de terminaison d’objet blob dans un navigateur, et vous recevez une réponse similaire hello suivant, ce qui suggère hello ressource existe, bien que vous ne pouvez pas y accéder.

![Exemple de code](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a>Contacter l’administrateur du serveur proxy

Si vos paramètres de proxy sont correctes, vous avez peut-être toocontact votre administrateur de serveur proxy, et

- Assurez-vous que votre proxy ne bloque pas le trafic tooAzure gestion ou ressource de points de terminaison.

- Vérifiez que le protocole d’authentification hello utilisé par votre serveur proxy. L’Explorateur de stockage ne prend pas en charge les proxys NTLM.

## <a name="unable-tooretrieve-children-error-message"></a>Message d’erreur « Impossible de tooRetrieve enfants »

Si vous êtes connecté tooAzure via un proxy, vérifiez que vos paramètres de proxy sont corrects. Si vous ont été accordé l’accès tooa ressource propriétaire hello de hello abonnement ou le compte, vérifiez que vous avez lu ou répertorier les autorisations pour cette ressource.

### <a name="issues-with-sas-url"></a>Problèmes liés à l’URL SAP
Si vous vous connectez tooa service à l’aide d’une URL SAS et rencontre cette erreur :

- Vérifiez que les URL hello fournit les autorisations nécessaires hello tooread ou une liste de ressources.

- Vérifiez que hello QU'URL n’a pas expiré.

- Si hello URL SAS est basé sur une stratégie d’accès, vérifiez que la stratégie d’accès hello n’a pas été révoquée.

## <a name="next-steps"></a>Étapes suivantes

Si aucune des solutions de hello vous convient, de soumettre votre problème via l’outil commentaires hello avec votre adresse de messagerie et autant de détails sur le problème hello inclus en tant que vous pouvez, afin que nous pouvons vous contacter pour résoudre le problème de hello.

toodo, cliquez sur **aide** menu, puis sur **envoyer des commentaires**.

![Commentaires](./media/storage-explorer-troubleshooting/4022503_en_1.png)
