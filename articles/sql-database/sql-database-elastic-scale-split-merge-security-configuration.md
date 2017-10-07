---
title: "configuration de la sécurité fusion aaaSplit | Documents Microsoft"
description: "Définissez les certificats x 409 pour le chiffrement"
metakeywords: Elastic Database certificates security
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: f9e89c57-61a0-484f-b787-82dae2349cb6
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 511c04be0598d8a0889aa3e3fcf02be0bf0e96cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="split-merge-security-configuration"></a>Configuration de la sécurité du fractionnement et de la fusion
service de fractionnement/fusion toouse hello, vous devez correctement configurer la sécurité. service de Hello fait partie de la fonctionnalité de mise à l’échelle élastique hello de base de données SQL Microsoft Azure. Pour plus d’informations, consultez le [didacticiel sur le service de fusion et de fractionnement de l’infrastructure élastique](sql-database-elastic-scale-configure-deploy-split-and-merge.md)

## <a name="configuring-certificates"></a>Configuration des certificats
Les certificats sont configurés de deux manières. 

1. [tooConfigure hello certificat SSL](#to-configure-the-ssl-certificate)
2. [tooConfigure les certificats clients](#to-configure-client-certificates) 

## <a name="tooobtain-certificates"></a>certificats tooobtain
Les certificats peuvent être obtenues à partir d’autorités de certification publique (CA) ou à partir de hello [Service de certificats Windows](http://msdn.microsoft.com/library/windows/desktop/aa376539.aspx). Il s’agit des certificats tooobtain hello préféré méthodes.

Si ces options ne sont pas disponibles, vous pouvez générer des **certificats auto-signés**.

## <a name="tools-toogenerate-certificates"></a>Certificats de toogenerate d’outils
* [makecert.exe](http://msdn.microsoft.com/library/bfsktky3.aspx)
* [pvk2pfx.exe](http://msdn.microsoft.com/library/windows/hardware/ff550672.aspx)

### <a name="toorun-hello-tools"></a>outils de hello toorun
* Depuis une invite de commandes développeur pour Visual Studio, consultez la rubrique [Invite de commandes Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) 
  
    Si installée, accédez à :
  
        %ProgramFiles(x86)%\Windows Kits\x.y\bin\x86 
* Obtenir hello WDK de [Windows 8.1 : télécharger des kits et des outils](http://msdn.microsoft.com/windows/hardware/gg454513#drivers)

## <a name="tooconfigure-hello-ssl-certificate"></a>certificat SSL de hello tooconfigure
Un certificat SSL est requis tooencrypt hello communication et authentifier hello serveur. Choisissez hello plus applicable de trois scénarios hello ci-dessous et exécuter toutes ses étapes :

### <a name="create-a-new-self-signed-certificate"></a>Création d’un certificat auto-signé
1. [Création d’un certificat auto-signé](#create-a-self-signed-certificate)
2. [Création d’un fichier PFX pour un certificat SSL auto-signé](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Télécharger le certificat SSL tooCloud Service](#upload-ssl-certificate-to-cloud-service)
4. [Mise à jour du certificat SSL dans le fichier de configuration de service](#update-ssl-certificate-in-service-configuration-file)
5. [Importation de l’autorité de certification SSL](#import-ssl-certification-authority)

### <a name="toouse-an-existing-certificate-from-hello-certificate-store"></a>stockage d’un certificat existant à partir du certificat de hello toouse
1. [Exportation d’un certificat SSL à partir du magasin de certificats](#export-ssl-certificate-from-certificate-store)
2. [Télécharger le certificat SSL tooCloud Service](#upload-ssl-certificate-to-cloud-service)
3. [Mise à jour du certificat SSL dans le fichier de configuration de service](#update-ssl-certificate-in-service-configuration-file)

### <a name="toouse-an-existing-certificate-in-a-pfx-file"></a>toouse un certificat existant dans un fichier PFX
1. [Télécharger le certificat SSL tooCloud Service](#upload-ssl-certificate-to-cloud-service)
2. [Mise à jour du certificat SSL dans le fichier de configuration de service](#update-ssl-certificate-in-service-configuration-file)

## <a name="tooconfigure-client-certificates"></a>certificats clients tooconfigure
Certificats clients sont requis dans l’ordre tooauthenticate demandes toohello service. Choisissez hello plus applicable de trois scénarios hello ci-dessous et exécuter toutes ses étapes :

### <a name="turn-off-client-certificates"></a>Désactivation des certificats clients
1. [Désactivation de l’authentification par certificat client](#turn-off-client-certificate-based-authentication)

### <a name="issue-new-self-signed-client-certificates"></a>Émission de nouveaux certificats clients auto-signés
1. [Création d’une autorité de certification auto-signée](#create-a-self-signed-certification-authority)
2. [Télécharger le certificat d’autorité de certification tooCloud Service](#upload-ca-certificate-to-cloud-service)
3. [Mise à jour du certificat CA dans le fichier de configuration de service](#update-ca-certificate-in-service-configuration-file)
4. [Émission de certificats clients](#issue-client-certificates)
5. [Création de fichiers PFX pour les certificats clients](#create-pfx-files-for-client-certificates)
6. [Importation d’un certificat client](#Import-Client-Certificate)
7. [Copie des empreintes numériques des certificats clients](#copy-client-certificate-thumbprints)
8. [Configurer les Clients d’autorisé Bonjour fichier de Configuration de Service](#configure-allowed-clients-in-the-service-configuration-file)

### <a name="use-existing-client-certificates"></a>Utilisation de certificats clients existants
1. [Find CA Public Key](#find-ca-public-key)
2. [Télécharger le certificat d’autorité de certification tooCloud Service](#Upload-CA-certificate-to-cloud-service)
3. [Mise à jour du certificat CA dans le fichier de configuration de service](#Update-CA-Certificate-in-Service-Configuration-File)
4. [Copie des empreintes numériques des certificats clients](#Copy-Client-Certificate-Thumbprints)
5. [Configurer les Clients d’autorisé Bonjour fichier de Configuration de Service](#configure-allowed-clients-in-the-service-configuration-file)
6. [Configuration de la vérification de révocation des certificats clients](#Configure-Client-Certificate-Revocation-Check)

## <a name="allowed-ip-addresses"></a>Adresses IP autorisées
Points de terminaison de service accès toohello peuvent être restreint toospecific les plages d’adresses IP.

## <a name="tooconfigure-encryption-for-hello-store"></a>chiffrement tooconfigure pour le magasin de hello
Un certificat est requis tooencrypt informations d’identification hello qui sont stockées dans le magasin de métadonnées hello. Choisissez hello plus applicable de trois scénarios hello ci-dessous et exécuter toutes ses étapes :

### <a name="use-a-new-self-signed-certificate"></a>Utilisation d’un nouveau certificat auto-signé
1. [Création d’un certificat auto-signé](#create-a-self-signed-certificate)
2. [Création d’un fichier PFX pour un certificat de chiffrement auto-signé](#create-pfx-file-for-self-signed-ssl-certificate)
3. [Télécharger le certificat de chiffrement tooCloud Service](#upload-encryption-certificate-to-cloud-service)
4. [Mise à jour du certificat de chiffrement dans le fichier de configuration de service](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-from-hello-certificate-store"></a>Utiliser un certificat existant à partir du magasin de certificats hello
1. [Exportation d’un certificat de chiffrement à partir du magasin de certificats](#export-encryption-certificate-from-certificate-store)
2. [Télécharger le certificat de chiffrement tooCloud Service](#upload-encryption-certificate-to-cloud-service)
3. [Mise à jour du certificat de chiffrement dans le fichier de configuration de service](#update-encryption-certificate-in-service-configuration-file)

### <a name="use-an-existing-certificate-in-a-pfx-file"></a>Utilisation d’un certificat existant dans un fichier PFX
1. [Télécharger le certificat de chiffrement tooCloud Service](#upload-encryption-certificate-to-cloud-service)
2. [Mise à jour du certificat de chiffrement dans le fichier de configuration de service](#update-encryption-certificate-in-service-configuration-file)

## <a name="hello-default-configuration"></a>configuration par défaut de Hello
configuration par défaut de Hello refuse de point de terminaison HTTP tous les accès toohello. Il s’agit de hello recommandée, étant donné que les points de terminaison hello demandes toothese peuvent contenir des informations sensibles telles que des informations d’identification de la base de données.
configuration par défaut de Hello permet de point de terminaison HTTPS tous les accès toohello. Ce paramètre peut être restreint davantage.

### <a name="changing-hello-configuration"></a>La modification de Configuration de hello
groupe de règles de contrôle d’accès qui s’appliquent de point de terminaison tooand Hello sont configurés dans hello  **<EndpointAcls>**  section Bonjour **fichier de configuration de service**.

    <EndpointAcls>
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpIn" accessControl="DenyAll" />
      <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="AllowAll" />
    </EndpointAcls>

règles de Hello dans un groupe de contrôle d’accès sont configurés dans un <AccessControl name=""> section du fichier de configuration de service hello. 

format de Hello est expliquée dans la documentation de listes de contrôle d’accès réseau.
Par exemple, tooallow uniquement des adresses IP dans hello plage 100.100.0.0 too100.100.255.255 tooaccess hello point de terminaison HTTPS, les règles de hello ressemble à ceci :

    <AccessControl name="Retricted">
      <Rule action="permit" description="Some" order="1" remoteSubnet="100.100.0.0/16"/>
      <Rule action="deny" description="None" order="2" remoteSubnet="0.0.0.0/0" />
    </AccessControl>
    <EndpointAcls>
    <EndpointAcl role="SplitMergeWeb" endPoint="HttpsIn" accessControl="Restricted" />

## <a name="denial-of-service-prevention"></a>Prévention du déni de service
Il existe deux mécanismes différents pris en charge toodetect et empêchent les attaques par déni de Service :

* Limiter le nombre de demandes simultanées par hôte distant (désactivé par défaut)
* Limiter le taux d’accès par hôte distant (activé par défaut)

Elles sont basées sur les fonctionnalités de hello en sécurité IP dynamique dans IIS. Lorsque la modification de cette configuration Méfiez-vous de hello suivant facteurs :

* comportement de Hello de proxies et les périphériques de traduction d’adresses réseau sur les informations d’hôte distant hello
* Chaque ressource tooany de demande dans un rôle web de hello est pris en compte (par exemple, le chargement des scripts, des images, etc.)

## <a name="restricting-number-of-concurrent-accesses"></a>Limitation du nombre d'accès simultanés
Hello que configurer ce comportement sont les suivantes :

    <Setting name="DynamicIpRestrictionDenyByConcurrentRequests" value="false" />
    <Setting name="DynamicIpRestrictionMaxConcurrentRequests" value="20" />

Modifier la DynamicIpRestrictionDenyByConcurrentRequests tootrue tooenable cette protection.

## <a name="restricting-rate-of-access"></a>Restriction du taux d’accès
Hello que configurer ce comportement sont les suivantes :

    <Setting name="DynamicIpRestrictionDenyByRequestRate" value="true" />
    <Setting name="DynamicIpRestrictionMaxRequests" value="100" />
    <Setting name="DynamicIpRestrictionRequestIntervalInMilliseconds" value="2000" />

## <a name="configuring-hello-response-tooa-denied-request"></a>Configuration hello réponse tooa a rejeté la demande
Hello paramètre suivant configure tooa de réponse hello a rejeté la demande :

    <Setting name="DynamicIpRestrictionDenyAction" value="AbortRequest" />
Consultez la documentation du toohello pour la sécurité IP dynamique dans IIS pour les autres valeurs prises en charge.

## <a name="operations-for-configuring-service-certificates"></a>Opérations de configuration des certificats de service
Cette rubrique sert de référence uniquement. Suivez les étapes de configuration hello décrites dans :

* Configurer un certificat SSL de hello
* Configuration des certificats clients

## <a name="create-a-self-signed-certificate"></a>Création d’un certificat auto-signé
Exécutez :

    makecert ^
      -n "CN=myservice.cloudapp.net" ^
      -e MM/DD/YYYY ^
      -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1" ^
      -a sha1 -len 2048 ^
      -sv MySSL.pvk MySSL.cer

toocustomize :

* URL du service - n avec hello. Les caractères génériques (CN=*.cloudapp.net) et d’autres noms (CN=myservice1.cloudapp.net, CN=myservice2.cloudapp.net) sont pris en charge.
* -e avec la date d’expiration de certificat hello créer un mot de passe fort et le spécifier lorsque vous y êtes invité.

## <a name="create-pfx-file-for-self-signed-ssl-certificate"></a>Création d’un fichier PFX pour un certificat SSL auto-signé
Exécutez :

        pvk2pfx -pvk MySSL.pvk -spc MySSL.cer

Entrez le mot de passe et exportez le certificat avec les options suivantes :

* Oui, exporter la clé privée de hello
* Exporter toutes les propriétés étendues

## <a name="export-ssl-certificate-from-certificate-store"></a>Exportation d’un certificat SSL à partir du magasin de certificats
* Recherchez le certificat
* Cliquez sur Actions -> Toutes les tâches -> Exporter...
* Exportez le certificat dans un fichier .PFX avec les options suivantes :
  * Oui, exporter la clé privée de hello
  * Inclure tous les certificats dans le chemin d’accès de certification hello si possible * exporter toutes les propriétés étendues

## <a name="upload-ssl-certificate-toocloud-service"></a>Télécharger le service toocloud de certificat SSL
Téléchargez le certificat avec hello existant ou générés. Fichier PFX portant hello paire de clés SSL :

* Entrez hello de mot de passe protège les informations de clé privée hello

## <a name="update-ssl-certificate-in-service-configuration-file"></a>Mise à jour du certificat SSL dans le fichier de configuration de service
Mettre à jour la valeur d’empreinte numérique hello Hello suivant paramètre dans le fichier de configuration de service hello avec l’empreinte numérique hello du service de cloud toohello hello certificat téléchargé :

    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="import-ssl-certification-authority"></a>Importation de l’autorité de certification SSL
Suivez ces étapes dans tous les comptes/machine qui communiqueront avec le service de hello :

* Double-cliquez sur hello. Fichier CER dans l’Explorateur Windows
* Dans la boîte de dialogue certificat hello, cliquez sur Installer le certificat...
* Importer des certificats dans hello que magasin des autorités de Certification racines de confiance

## <a name="turn-off-client-certificate-based-authentication"></a>Désactivation de l’authentification par certificat client
Uniquement basée sur certificat l’authentification du client est prise en charge et sa désactivation autorisera des points de terminaison du service de toohello accès public, à moins que les autres mécanismes sont en place (par exemple, Microsoft Azure Virtual Network).

Modifier toofalse de ces paramètres dans la fonctionnalité hello tooturn du fichier configuration hello service :

    <Setting name="SetupWebAppForClientCertificates" value="false" />
    <Setting name="SetupWebserverForClientCertificates" value="false" />

Ensuite, copiez hello même empreinte numérique que hello SSL de certificat dans le paramètre hello autorité de certification du certificat :

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="create-a-self-signed-certification-authority"></a>Création d’une autorité de certification auto-signée
Exécutez hello suivant les étapes toocreate un tooact un certificat auto-signé comme une autorité de Certification :

    makecert ^
    -n "CN=MyCA" ^
    -e MM/DD/YYYY ^
     -r -cy authority -h 1 ^
     -a sha1 -len 2048 ^
      -sr localmachine -ss my ^
      MyCA.cer

toocustomize il

* -e avec la date d’expiration de certification hello

## <a name="find-ca-public-key"></a>Recherche de la clé publique de l’autorité de certification
Tous les certificats de client doivent avoir été émis par une autorité de Certification approuvée par le service de hello. Trouver toohello de clé publique hello autorité de Certification qui a émis les certificats de client hello qui vont toobe utilisé pour l’authentification dans tooupload d’ordre il toohello le service cloud.

Si le fichier hello avec une clé publique hello n’est pas disponible, l’exporter à partir du magasin de certificats hello :

* Recherchez le certificat
  * Recherche d’un certificat client publié par hello même autorité de Certification
* Double-cliquez sur le certificat de hello.
* Sélectionnez l’onglet de chemin d’accès de Certification hello dans la boîte de dialogue certificat hello.
* Double-cliquez sur entrée d’autorité de certification hello dans le chemin d’accès hello.
* Prenez des notes de propriétés du certificat hello.
* Fermer hello **certificat** boîte de dialogue.
* Recherchez le certificat
  * Recherchez hello autorité de certification indiquée ci-dessus.
* Cliquez sur Actions -> Toutes les tâches -> Exporter...
* Exportez le certificat dans un fichier .CER avec les options suivantes :
  * **Non, ne pas exporter la clé privée de hello**
  * Inclure tous les certificats dans le chemin d’accès de certification hello si possible.
  * Exporter toutes les propriétés étendues.

## <a name="upload-ca-certificate-toocloud-service"></a>Télécharger le service toocloud de certificat autorité de certification
Téléchargez le certificat avec hello existant ou générés. Fichier CER avec une clé publique hello autorité de certification.

## <a name="update-ca-certificate-in-service-configuration-file"></a>Mise à jour du certificat CA dans le fichier de configuration de service
Mettre à jour la valeur d’empreinte numérique hello Hello suivant paramètre dans le fichier de configuration de service hello avec l’empreinte numérique hello du service de cloud toohello hello certificat téléchargé :

    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />

Mettre à jour la valeur hello hello après avoir défini avec hello même empreinte numérique :

    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />

## <a name="issue-client-certificates"></a>Émission de certificats clients
Chaque service de hello individuels tooaccess autorisés doit avoir un certificat client publié pour his/hers exclusif à utiliser et doit choisir que HIS/hers propre mot de passe fort tooprotect sa clé privée. 

Hello suit doit être exécutée dans hello même machine hello auto-signé où certificat d’autorité de certification a été généré et stocké :

    makecert ^
      -n "CN=My ID" ^
      -e MM/DD/YYYY ^
      -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.2" ^
      -a sha1 -len 2048 ^
      -in "MyCA" -ir localmachine -is my ^
      -sv MyID.pvk MyID.cer

Personnalisation :

* -n avec un ID de client toohello qui est authentifié avec ce certificat
* -e avec la date d’expiration de certificat hello
* MyID.pvk et MyID.cer avec des noms de fichier uniques pour ce certificat client

Cette commande demande une toobe de mot de passe créé, puis utilisé une seule fois. Utilisez un mot de passe fort.

## <a name="create-pfx-files-for-client-certificates"></a>Création de fichiers PFX pour les certificats clients
Pour chaque certificat client généré, exécutez :

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personnalisation :

    MyID.pvk and MyID.cer with hello filename for hello client certificate

Entrez le mot de passe et exportez le certificat avec les options suivantes :

* Oui, exporter la clé privée de hello
* Exporter toutes les propriétés étendues
* toowhom individuels de Hello qu'est émis ce certificat doit choisir le mot de passe de hello exportation

## <a name="import-client-certificate"></a>Importation d’un certificat client
Chaque utilisateur pour lequel un certificat client a été émis doit importer la paire de clés hello dans des machines de hello, il utilisera toocommunicate avec le service de hello :

* Double-cliquez sur hello. Fichier PFX dans l’Explorateur Windows
* Importer un certificat dans hello Personal stocker au moins cette option :
  * Inclure toutes les propriétés étendues activées

## <a name="copy-client-certificate-thumbprints"></a>Copie des empreintes numériques des certificats clients
Chaque utilisateur pour lequel un certificat client a été émis devez suivre ces étapes dans l’ordre tooobtain hello empreinte numérique du his/hers certificat qui sera ajouté le fichier de configuration de service toohello :

* Exécutez certmgr.exe
* Sélectionnez l’onglet personnel de hello
* Double-cliquez sur le certificat de client hello toobe utilisé pour l’authentification
* Hello certificat boîte de dialogue qui s’ouvre, sélectionnez onglet Détails de hello
* Veillez à ce que l'option Afficher indique Tous
* Champ Sélectionnez hello nommé l’empreinte numérique dans la liste de hello
* Copier la valeur hello de l’empreinte numérique hello ** supprimer des caractères Unicode non visible devant le premier chiffre de hello ** supprimer tous les espaces

## <a name="configure-allowed-clients-in-hello-service-configuration-file"></a>Configurer les clients autorisés dans le fichier de configuration de service hello
Mettre à jour la valeur hello hello suivant paramètre dans le fichier de configuration de service hello avec une liste séparée par des virgules des empreintes numériques de hello de certificats de client hello autorisées du service d’accès toohello :

    <Setting name="AllowedClientCertificateThumbprints" value="" />

## <a name="configure-client-certificate-revocation-check"></a>Configuration de la vérification de révocation des certificats clients
paramètre par défaut de Hello ne vérifie pas avec hello autorité de Certification pour l’état de révocation du certificat client. tooturn sur hello vérifie si hello autorité de Certification qui a émis les certificats de client hello prend en charge ce type de contrôle, modifiez les hello suivant paramètre avec l’une des valeurs de hello définies dans hello X509RevocationMode énumération :

    <Setting name="ClientCertificateRevocationCheck" value="NoCheck" />

## <a name="create-pfx-file-for-self-signed-encryption-certificates"></a>Création d’un fichier PFX pour un certificat de chiffrement auto-signé
Pour un certificat de chiffrement, exécutez :

    pvk2pfx -pvk MyID.pvk -spc MyID.cer

Personnalisation :

    MyID.pvk and MyID.cer with hello filename for hello encryption certificate

Entrez le mot de passe et exportez le certificat avec les options suivantes :

* Oui, exporter la clé privée de hello
* Exporter toutes les propriétés étendues
* Vous devez mot de passe hello lors du chargement du service de cloud hello certificat toohello.

## <a name="export-encryption-certificate-from-certificate-store"></a>Exportation d’un certificat de chiffrement à partir du magasin de certificats
* Recherchez le certificat
* Cliquez sur Actions -> Toutes les tâches -> Exporter...
* Exportez le certificat dans un fichier .PFX avec les options suivantes : 
  * Oui, exporter la clé privée de hello
  * Inclure tous les certificats dans le chemin d’accès de certification hello si possible 
* Exporter toutes les propriétés étendues

## <a name="upload-encryption-certificate-toocloud-service"></a>Télécharger le service de toocloud de certificat de chiffrement
Téléchargez le certificat avec hello existant ou générés. Fichier PFX avec une paire de clés de chiffrement hello :

* Entrez hello de mot de passe protège les informations de clé privée hello

## <a name="update-encryption-certificate-in-service-configuration-file"></a>Mise à jour du certificat de chiffrement dans le fichier de configuration de service
Mettre à jour la valeur d’empreinte numérique hello Hello suivant les paramètres dans le fichier de configuration de service hello avec l’empreinte numérique hello hello téléchargé toohello cloud du service de certificats :

    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />

## <a name="common-certificate-operations"></a>Opérations courantes de certificat
* Configurer un certificat SSL de hello
* Configuration des certificats clients

## <a name="find-certificate"></a>Recherchez le certificat
Procédez comme suit :

1. Exécutez mmc.exe.
2. Fichier -> Ajouter/supprimer un composant logiciel enfichable...
3. Sélectionnez **Certificats**.
4. Cliquez sur **Add**.
5. Choisissez l’emplacement de magasin de certificats hello.
6. Cliquez sur **Terminer**.
7. Cliquez sur **OK**.
8. Développez les **certificats**.
9. Développez le nœud de magasin de certificat hello.
10. Développez le nœud enfant de certificat hello.
11. Sélectionnez un certificat dans la liste de hello.

## <a name="export-certificate"></a>Exportation du certificat
Bonjour **Assistant Exportation de certificat**:

1. Cliquez sur **Suivant**.
2. Sélectionnez **Oui**, puis **clé privée de hello exportation**.
3. Cliquez sur **Suivant**.
4. Sélectionnez le format de fichier de sortie souhaité hello.
5. Vérifiez les options hello souhaité.
6. Vérifiez le **mot de passe**.
7. Entrez un mot de passe fort et confirmez-le.
8. Cliquez sur **Suivant**.
9. Tapez ou recherchez un nom de fichier où toostore hello certificat (utilisez un. Extension PFX).
10. Cliquez sur **Suivant**.
11. Cliquez sur **Terminer**.
12. Cliquez sur **OK**.

## <a name="import-certificate"></a>Importation d’un certificat
Bonjour Assistant Importation de certificat :

1. Sélectionnez l’emplacement du magasin hello.
   
   * Sélectionnez **utilisateur actuel** si seuls les processus qui s’exécutent sous utilisateur actuel accède au service hello
   * Sélectionnez **Machine locale** si d’autres processus sur cet ordinateur accède au service hello
2. Cliquez sur **Suivant**.
3. Si l’importation à partir d’un fichier, vérifiez le chemin d’accès du fichier hello.
4. Si vous importez depuis un fichier .PFX :
   1. Entrez hello de mot de passe protège la clé privée de hello
   2. Sélectionnez les options d’importation
5. Sélectionnez « Place » certificats hello suivant du magasin
6. Cliquez sur **Parcourir**.
7. Sélectionnez le magasin de votre choix hello.
8. Cliquez sur **Terminer**.
   
   * Si le magasin d’autorité de Certification racine de confiance hello a été choisie, cliquez sur **Oui**.
9. Cliquez sur **OK** dans toutes les fenêtres des boîtes de dialogue.

## <a name="upload-certificate"></a>Téléchargement d’un certificat
Bonjour [portail Azure](https://portal.azure.com/)

1. Sélectionnez **Services Cloud**.
2. Sélectionnez le service de cloud computing hello.
3. Dans le menu supérieur de hello, cliquez sur **certificats**.
4. Dans la barre inférieure de hello, cliquez sur **télécharger**.
5. Sélectionnez le fichier de certificat hello.
6. Si elle est un. PFX fichier, entrez le mot de passe de hello pour la clé privée de hello.
7. Une fois terminé, copiez l’empreinte numérique du certificat hello hello nouvelle entrée dans la liste de hello.

## <a name="other-security-considerations"></a>Autres considérations liées à la sécurité
les paramètres de SSL Hello décrites dans ce document chiffrement la communication entre hello service et ses clients lorsque le point de terminaison hello HTTPS est utilisé. Ceci est important, car les informations d’identification pour l’accès de la base de données et éventuellement d’autres informations sensibles sont contenues dans une communication hello. Toutefois, notez que le service de hello persiste état interne, y compris les informations d’identification, dans ses tables internes de la base de données SQL Microsoft Azure hello que vous avez fournies pour le stockage des métadonnées dans votre abonnement Microsoft Azure. Cette base de données a été défini en tant que partie de hello suivant paramètre dans votre fichier de configuration de service (. Fichier CSCFG) : 

    <Setting name="ElasticScaleMetadata" value="Server=…" />

Les informations d’identification stockées dans cette base de données sont chiffrées. Toutefois, en tant que meilleure pratique, assurez-vous que les rôles web et de travail de vos déploiements de service sont conservés les toodate et sécurisée en tant qu’ils ont tous deux accès toohello métadonnées de base de données et hello certificat utilisé pour le chiffrement et le déchiffrement des informations d’identification stockées. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

