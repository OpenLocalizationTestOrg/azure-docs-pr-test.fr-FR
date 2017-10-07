---
title: "problèmes de connexion aaaTroubleshoot Azure point-to-site | Documents Microsoft"
description: "Découvrez comment les problèmes de connexion de point-to-site tootroubleshoot."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Résolution des problèmes de connexion de point à site Azure

Cet article répertorie les problèmes de connexion de point à site courants que vous pouvez rencontrer. Il décrit également les causes probables de ces problèmes, ainsi que les solutions possibles.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>Erreur du client VPN : le certificat est introuvable

### <a name="symptom"></a>Symptôme

Lorsque vous essayez tooconnect tooan réseau virtuel Azure à l’aide du client VPN de hello, vous recevez hello message d’erreur suivant :

**Impossible de trouver un certificat qui peut être utilisé avec le protocole EAP (Extensible Authentication Protocol). (Erreur 798)**

### <a name="cause"></a>Cause :

Ce problème se produit si le certificat de client hello est absent de **certificats - actuel\Personnel\Certificats**.

### <a name="solution"></a>Solution

Vérifiez que ce certificat de client hello est installé dans hello du magasin de certificats hello (Certmgr.msc) de l’emplacement suivant :
 
**Certificats - Utilisateur actuel\Personnel\Certificats**

Pour plus d’informations sur comment tooinstall hello certificat client, consultez [générer et exporter des certificats pour les connexions de point-to-site](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> Lorsque vous importez le certificat de client hello, ne sélectionnez pas hello **activer la protection renforcée par clé privée** option.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>Erreur du client VPN : message de salutation reçu était inattendu ou incorrectement formatée

### <a name="symptom"></a>Symptôme

Lorsque vous essayez tooconnect tooan réseau virtuel Azure à l’aide du client VPN de hello, vous recevez hello message d’erreur suivant :

**message de salutation reçu était inattendu ou incorrectement formatée. (Erreur 0x80090326)**

### <a name="cause"></a>Cause :

Ce problème se produit si la clé publique du certificat racine hello n’est pas téléchargé dans la passerelle VPN Azure hello. Il peut également se produire si la clé de hello est endommagée ou a expiré.

### <a name="solution"></a>Solution

tooresolve ce problème, vérifiez l’état de la racine de hello hello certificats Bonjour Azure toosee portail si elle a été révoqué. Si elle n’est pas révoqué, essayez de reupload et un certificat racine de hello toodelete. Pour en savoir plus, consultez la section [Créer des certificats](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>Erreur du client VPN : une chaîne de certificats a été traitée mais s’est terminée 

### <a name="symptom"></a>Symptôme 

Lorsque vous essayez tooconnect tooan réseau virtuel Azure à l’aide du client VPN de hello, vous recevez hello message d’erreur suivant :

**Une chaîne de certificats traitée mais s’est terminée par un certificat racine qui n’est pas approuvé par le fournisseur d’approbation hello.**

### <a name="solution"></a>Solution

1. Assurez-vous que hello certificats suivants sont dans l’emplacement correct de hello :

    | Certificat | Emplacement |
    | ------------- | ------------- |
    | AzureClient.pfx  | Utilisateur actuel\Personnel\Certificats |
    | Azuregateway-*GUID*.cloudapp.net  | Utilisateur actuel\Autorités de certification racines de confiance|
    | AzureGateway-*GUID*.cloudapp.net, AzureRoot.cer    | Ordinateur local\Autorités de certification racines de confiance|

2. Si les certificats hello sont déjà dans l’emplacement de hello, essayez les certificats toodelete hello et réinstallez-les. Hello  **azuregateway -*GUID*. cloudapp.net** certificat est dans le package de configuration hello VPN client que vous avez téléchargé à partir de hello portail Azure. Vous pouvez utiliser archivers tooextract hello des fichiers à partir du package de hello.

## <a name="file-download-error-target-uri-is-not-specified"></a>Erreur de téléchargement du fichier : L’URI cible n’est pas spécifié

### <a name="symptom"></a>Symptôme

Hello, message d’erreur suivant s’affiche :

**Erreur de téléchargement du fichier. L’URI cible n’est pas spécifié.**

### <a name="cause"></a>Cause : 

Ce problème se produit lorsque le type de passerelle est incorrecte. 

### <a name="solution"></a>Solution

Hello, type de passerelle VPN doit être **VPN**, et hello type VPN doit être **RouteBased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>Erreur du client VPN : échec du script VPN personnalisé Azure 

### <a name="symptom"></a>Symptôme

Lorsque vous essayez tooconnect tooan réseau virtuel Azure à l’aide du client VPN de hello, vous recevez hello message d’erreur suivant :

**Script personnalisé (tooupdate votre table de routage) a échoué. (Erreur 8007026f)**

### <a name="cause"></a>Cause :

Ce problème peut se produire si la tentative de connexion VPN de tooopen hello-à-point de site à l’aide d’un raccourci.

### <a name="solution"></a>Solution 

Ouvrez le package VPN hello directement au lieu d’ouvrir à partir du raccourci de hello.

## <a name="cannot-install-hello-vpn-client"></a>Impossible d’installer hello VPN client

### <a name="cause"></a>Cause : 

Un certificat supplémentaire est la passerelle VPN hello tootrust requis pour votre réseau virtuel. certificat de Hello est inclus dans le package de configuration hello VPN client qui est généré à partir de hello portail Azure.

### <a name="solution"></a>Solution

Extraire le package de configuration de client VPN hello et recherchez le fichier .cer de hello. tooinstall hello certificat, procédez comme suit :

1. Ouvrez mmc.exe.
2. Ajouter hello **certificats** enfichable.
3. Sélectionnez hello **ordinateur** compte pour l’ordinateur local de hello.
4. Avec le bouton hello **autorités de Certification racines de confiance** nœud. Cliquez sur **All-tâche** > **importation**et le fichier .cer de consultation toohello vous avez extrait à partir du package de configuration de client VPN hello.
5. Redémarrez l’ordinateur de hello. 
6. Essayez de client VPN de hello tooinstall.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Erreur de portail Azure : Échec de la passerelle VPN de hello toosave, et les données de salutation ne sont pas valides

### <a name="symptom"></a>Symptôme

Lorsque vous essayez de modifications de hello toosave pour la passerelle VPN de hello Bonjour portail Azure, vous recevez hello message d’erreur suivant :

**Passerelle de réseau virtuel a échoué toosave &lt;* nom de la passerelle*&gt;. Les données du certificat &lt;*ID de certificat*&gt; ne sont pas valides.**

### <a name="cause"></a>Cause : 

Ce problème peut se produire si hello racine certificat clé publique que vous avez téléchargé contient un caractère non valide, tels qu’un espace.

### <a name="solution"></a>Solution

Assurez-vous que les données hello dans le certificat de hello ne contient pas de caractères non valides, tels que les sauts de ligne (retour chariot). valeur entière de Hello doit être une longue ligne. Hello suivant le texte est un exemple de certificat de hello :

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Erreur de portail Azure : Échec de la passerelle VPN de hello toosave et nom de la ressource hello n’est pas valide

### <a name="symptom"></a>Symptôme

Lorsque vous essayez de modifications de hello toosave pour la passerelle VPN de hello Bonjour portail Azure, vous recevez hello message d’erreur suivant : 

**Passerelle de réseau virtuel a échoué toosave &lt;* nom de la passerelle*&gt;. Nom de la ressource &lt; *nom de certificat que vous essayez de tooupload* &gt; n’est pas valide **.

### <a name="cause"></a>Cause :

Ce problème se produit parce que le nom hello du certificat de hello contient un caractère non valide, tels qu’un espace. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Erreur du portail Azure : téléchargement du fichier de package VPN (Erreur 503)

### <a name="symptom"></a>Symptôme

Lorsque vous essayez de package de configuration client toodownload hello VPN, vous recevez hello message d’erreur suivant :

**Échec de toodownload hello fichier. Détails de l’erreur : erreur 503. Hello serveur est occupé.**
 
### <a name="solution"></a>Solution

Cette erreur peut être due à un problème réseau temporaire. Réessayez dans le package VPN toodownload hello quelques minutes.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>Mise à niveau de passerelle VPN Azure : P2S tous les clients sont tooconnect Impossible

### <a name="cause"></a>Cause :

Si le certificat de hello est plus de 50 % à sa durée de vie, les certificats hello sont restaurée.

### <a name="solution"></a>Solution

tooresolve ce problème, créez et redistribuer les clients VPN de nouveaux certificats toohello. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Trop de clients VPN sont connectés

Pour chaque passerelle VPN, hello de nombre maximal de connexions autorisées est de 128. Vous pouvez voir le nombre total de hello de clients connectés Bonjour portail Azure.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>Point-to-site VPN ajoute incorrectement un itinéraire pour la table d’itinéraires toohello 10.0.0.0/8

### <a name="symptom"></a>Symptôme

Lorsque vous composez hello connexion VPN sur le client de point-to-site hello, client VPN de hello doit ajouter un itinéraire vers le réseau virtuel Azure de hello. service de programme d’assistance IP Hello doit ajouter un itinéraire pour le sous-réseau hello de clients VPN de hello. 

Hello plage de client VPN appartient tooa plus petit sous-réseau 10.0.0.0/8, telles que 10.0.12.0/24. Au lieu d’un itinéraire pour 10.0.12.0/24, un itinéraire pour 10.0.0.0/8 ayant une priorité plus élevée est ajouté. 

Cet itinéraire incorrect rompt la connectivité avec d’autres réseaux locaux qui peuvent appartenir sous-réseau tooanother plage hello 10.0.0.0/8, telles que 10.50.0.0/24, qui n’ont pas un itinéraire spécifique défini. 

### <a name="cause"></a>Cause :

Ce comportement est lié aux clients Windows. Lorsque le client de hello utilise le protocole PPP IPCP de hello, il obtient adresse hello pour l’interface de tunnel hello du serveur de hello (hello passerelle VPN dans ce cas). Toutefois, en raison d’une limitation dans le protocole de hello, client de hello n’a pas de masque de sous-réseau hello. Étant donné qu’aucun autre tooget de façon il, client de hello essaie en fonction de la classe hello d’adresse IP de hello tunnel interface le masque de sous-réseau tooguess hello. 

Par conséquent, ajoutez un itinéraire en fonction de hello suivant mappage statique : 

Si l’adresse appartient tooclass A--> appliquer la valeur/8

Si l’adresse appartient tooclass B--> appliquer /16

Si l’adresse appartient tooclass C--> appliquer /24

## <a name="vpn-client-cannot-access-network-file-shares"></a>Les clients VPN ne peuvent pas accéder aux partages de fichiers réseau

### <a name="symptom"></a>Symptôme

Hello VPN client s’est connecté toohello réseau virtuel Azure. Toutefois, les clients hello ne peut pas accéder aux partages réseau.

### <a name="cause"></a>Cause :

Hello protocole SMB est utilisé pour l’accès de partage de fichier. Lors de la connexion à hello est lancée, client VPN de hello ajoute des informations d’identification de session hello et hello échec se produit. Après hello est établie, un client de hello forcé toouse hello cache informations d’identification pour l’authentification Kerberos. Ce processus lance les requêtes toohello centre de Distribution de clés (un contrôleur de domaine) tooget un jeton. Étant donné que le client de hello se connecte à partir de hello Internet, il peut être contrôleur de domaine en mesure de tooreach hello. Par conséquent, les clients hello ne peuvent pas basculer à partir de tooNTLM de Kerberos. 

Hello uniquement de temps que le client hello est invité à fournir pour une information d’identification est lorsqu’il possède un certificat valide (avec SAN = UPN) émis par toowhich de domaine hello il est joint. Hello client également doit être connectée physiquement toohello un réseau avec domaine. Dans ce cas, les clients hello tente de certificat de hello toouse et contacte le contrôleur de domaine toohello. Hello, Key Distribution Center retourne ensuite une erreur « KDC_ERR_C_PRINCIPAL_UNKNOWN ». client de Hello est forcé toofail sur tooNTLM. 

### <a name="solution"></a>Solution

toowork problème de hello, désactiver hello mise en cache des informations d’identification de domaine à partir de hello suivant la sous-clé de Registre : 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>Ne peut pas trouver la connexion de hello point-to-site VPN dans Windows après la réinstallation du client VPN de hello

### <a name="symptom"></a>Symptôme

Vous supprimez la connexion VPN de point-to-site hello et puis réinstallez le client VPN de hello. Dans ce cas, hello connexion VPN n’est pas configuré correctement. Vous ne voyez pas la connexion VPN de hello Bonjour **des connexions réseau** sous Windows.

### <a name="solution"></a>Solution

problème de hello tooresolve, delete hello ancien VPN client des fichiers de configuration **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, puis exécutez à nouveau le programme d’installation client hello VPN.
