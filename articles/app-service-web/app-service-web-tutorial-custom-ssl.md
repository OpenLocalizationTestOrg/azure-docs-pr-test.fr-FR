---
title: "aaaBind un SSL personnalisé existant de certificats des applications Web tooAzure | Documents Microsoft"
description: "En savoir plus tootoobind une application de web tooyour de certificat SSL personnalisée, principal de l’application mobile ou API app dans Azure App Service."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>Lier un tooAzure de certificat SSL personnalisé existant Web Apps

Azure Web Apps fournit un service d’hébergement hautement évolutif et appliquant des mises à jour correctives automatiquement. Ce didacticiel vous montre comment toobind une SSL personnalisée de certificats que vous avez acheté auprès d’une autorité de certification approuvée trop[Azure Web Apps](app-service-web-overview.md). Lorsque vous avez terminé, vous serez en mesure de tooaccess votre application web au point de terminaison HTTPS hello de votre domaine DNS personnalisé.

![Application Web avec certificat SSL personnalisé](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Mettre à jour le niveau de tarification de votre application
> * Lier votre tooApp de certificat SSL Service personnalisé
> * Appliquer le protocole HTTPS à votre application
> * Automatiser la liaison de certificat SSL avec des scripts

> [!NOTE]
> Si vous avez besoin de tooget un certificat SSL personnalisé, vous pouvez en obtenir un Bonjour Azure portal directement et liez-le à l’application web tooyour. Suivez hello [didacticiel de certificats de Service d’application](web-sites-purchase-ssl-web-site.md).

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel :

- [Création d’une application App Service](/azure/app-service/)
- [Mapper une application personnalisée DNS nom tooyour web](app-service-web-tutorial-custom-domain.md)
- Acquisition d’un certificat SSL auprès d’une autorité de certification approuvée

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>Conditions requises pour le certificat SSL

toouse un certificat dans le Service d’applications, les certificats hello doivent respecter toutes les hello suivant les exigences :

* Être signé par une autorité de certification approuvée
* Être exporté sous la forme d’un fichier PFX protégé par mot de passe
* Contenir une clé privée d’au moins 2048 bits de long
* Contient tous les certificats intermédiaires dans la chaîne de certificats hello

> [!NOTE]
> Les **certificats de chiffrement à courbe elliptique (ECC)** sont compatibles avec App Service, mais ce sujet sort du cadre de cet article. Travailler avec votre autorité de certification sur les certificats ECC de hello étapes exactes toocreate.

## <a name="prepare-your-web-app"></a>Préparation de votre application web

toobind une SSL personnalisée de certificats tooyour web app, votre [plan App Service](https://azure.microsoft.com/pricing/details/app-service/) doit être Bonjour **base**, **Standard**, ou **Premium** couche. Dans cette étape, vous vous assurer que votre application web est Bonjour pris en charge niveau tarifaire.

### <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez hello [portail Azure](https://portal.azure.com).

### <a name="navigate-tooyour-web-app"></a>Accédez tooyour l’application web

Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web.

![Sélectionner de l’application web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

Vous n’êtes pas pas dans la page de gestion hello de votre application web.  

### <a name="check-hello-pricing-tier"></a>Vérifier le niveau tarifaire de hello

Navigation de gauche hello de page de votre application web, faites défiler toohello **paramètres** section et sélectionnez **montée en puissance (plan App Service)**.

![Menu Monter en puissance](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Vérifiez toomake sûr que votre application web n’est pas hello **libre** ou **Shared** couche. Le niveau actuel de votre application web est encadré d’un rectangle bleu foncé.

![Vérification du niveau de tarification](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

SSL personnalisé n’est pas pris en charge dans hello **libre** ou **Shared** couche. Si vous avez besoin tooscale, suivez les étapes de hello dans la section suivante de hello. Sinon, fermez hello **choisir votre niveau tarifaire** page et ignorer trop[télécharger et de lier votre certificat SSL](#upload).

### <a name="scale-up-your-app-service-plan"></a>Évolution de votre plan App Service

Sélectionnez une des hello **base**, **Standard**, ou **Premium** niveaux.

Cliquez sur **Sélectionner**.

![Sélection du niveau tarifaire](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

Lorsque vous voyez hello suivant la notification, l’opération de mise à l’échelle de hello est terminée.

![Notification de montée en puissance](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>Liaison de votre certificat SSL

Vous est prêt tooupload votre certificat SSL tooyour l’application web.

### <a name="merge-intermediate-certificates"></a>Fusionner les certificats intermédiaires

Si votre autorité de certification vous donne plusieurs certificats dans la chaîne de certificats hello, vous devez les certificats hello toomerge dans l’ordre. 

toodo cela, ouvrez chaque certificat que vous avez reçu dans un éditeur de texte. 

Créer un fichier de certificat fusionné hello, appelé _mergedcertificate.crt_. Dans un éditeur de texte, copiez le contenu de chaque certificat hello dans ce fichier. commande Hello vos certificats doit ressembler à hello suivant le modèle :

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>Exporter le certificat tooPFX

Exporter votre certificat SSL fusionnée avec la clé privée hello votre demande de certificat a été généré avec.

Si vous avez généré votre demande de certificat à l’aide d’OpenSSL, vous avez créé un fichier de clé privée. tooexport tooPFX votre certificat, exécutez hello commande suivante. Remplacez les espaces réservés de hello  _&lt;fichier de clé privée >_ et  _&lt;fusionnée de fichier de certificat >_.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

Lorsque vous y êtes invité, définissez un mot de passe d’exportation. Vous allez utiliser ce mot de passe lors du téléchargement de votre tooApp de certificat SSL Service ultérieurement.

Si vous avez utilisé IIS ou _Certreq.exe_ toogenerate votre demande de certificat, l’installation hello certificat tooyour ordinateur local, puis [exporter hello certificat tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).

### <a name="upload-your-ssl-certificate"></a>Chargement de votre certificat SSL

tooupload votre certificat SSL, cliquez sur **certificats SSL** Bonjour gauche de navigation de votre application web.

Cliquez sur **Charger le certificat**.

Dans **Fichier de certificat PFX**, sélectionnez votre fichier PFX. Dans **mot de passe de certificat**, type hello mot de passe que vous avez créé lorsque vous avez exporté le fichier PFX hello.

Cliquez sur **Télécharger**.

![Téléchargement d’un certificat](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

Lorsque le Service de l’application a terminé de télécharger votre certificat, il apparaît dans hello **certificats SSL** page.

![Certificat chargé](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>Liaison de votre certificat SSL

Bonjour **liaisons SSL** , cliquez sur **ajouter la liaison**.

Bonjour **ajouter la liaison SSL** page, utilisez hello menus déroulants tooselect hello domaine nom toosecure et toouse de certificat hello.

> [!NOTE]
> Si vous avez téléchargé votre certificat, mais ne pas afficher ou les noms de domaine hello Bonjour **nom d’hôte** liste déroulante, essayez d’actualiser la page du navigateur hello.
>
>

Dans **SSL Type**, sélectionnez si toouse  **[Indication de nom de serveur (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ou SSL basé sur IP.

- **SSL basé sur SNI** : plusieurs liaisons SSL basées sur SNI peuvent être ajoutées. Cette option permet à plusieurs toosecure de certificats SSL plusieurs domaines sur hello même adresse IP. La plupart des navigateurs actuels (y compris Internet Explorer, Chrome, Firefox et Opera) prennent en charge SNI (plus d’informations sur la prise en charge des navigateurs dans [Indication du nom du serveur](http://wikipedia.org/wiki/Server_Name_Indication)).
- **SSL basé sur IP** : une seule liaison SSL basée sur IP peut être ajoutée. Cette option ne permet qu’un seul toosecure de certificat SSL à une adresse IP publique dédiée. toosecure plusieurs domaines, vous devez les sécuriser à l’aide de tous les hello même certificat SSL. Il s’agit d’option traditionnelles de hello pour la liaison SSL.

Cliquez sur **Ajouter une liaison**.

![Liaison d’un certificat SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

Lorsque le Service de l’application a terminé de télécharger votre certificat, il apparaît dans hello **liaisons SSL** sections.

![Certificat lié tooweb application](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>Nouveau mappage d’un enregistrement pour SSL IP

Si vous n’utilisez pas SSL basé sur IP dans votre application web, passez trop[HTTPS de Test pour votre domaine personnalisé](#test).

Par défaut, votre application web utilise une adresse IP publique partagée. Dès que vous liez un certificat avec SSL basé sur IP, App Service crée une adresse IP dédiée pour votre application web.

Si vous avez mappé une application web de tooyour enregistrement A, mettre à jour le Registre de votre domaine avec cette nouvelle adresse IP dédiée.

De votre application web **un domaine personnalisé** page est mise à jour avec hello dédié, nouvelle adresse. [Copiez cette adresse IP](app-service-web-tutorial-custom-domain.md#info), puis [remappage hello un enregistrement](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nouvelle adresse.

<a name="test"></a>

## <a name="test-https"></a>Test du protocole HTTPS

Tout ce qui a quitté toodo maintenant est toomake sûr que HTTPS fonctionne pour votre domaine personnalisé. Dans différents navigateurs, recherchez trop`https://<your.custom.domain>` toosee qu’il sert de votre application web.

![Application tooAzure de navigation du portail](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> Si votre application web permet de voir les erreurs de validation de certificat, vous utilisez probablement un certificat auto-signé.
>
> Si tel n’est pas le cas de hello, vous pouvez avoir laissé des certificats intermédiaires lorsque vous exportez votre fichier PFX du certificat toohello.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>Appliquer le protocole HTTPS

App Service n’appliquant *pas* le protocole HTTPS, tout le monde peut accéder à votre application à l’aide de HTTP. tooenforce HTTPS pour votre application web, définissez une règle de réécriture Bonjour _web.config_ fichier de votre application web. Service de l’application utilise ce fichier, quel que soit l’infrastructure de langage hello de votre application web.

> [!NOTE]
> Certaines redirections de requête sont propres au langage. ASP.NET MVC peuvent utiliser hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtre au lieu de la règle de réécriture hello dans _web.config_.

Si vous êtes un développeur .NET, vous connaissez probablement ce fichier. Il est dans la racine de hello de votre solution.

Ou, si vous développez avec PHP, Node.js, Python ou Java, il est possible que ce fichier ait été généré en votre nom dans App Service.

Connecter le point de terminaison de l’application tooyour web FTP en suivant les instructions de hello sur [déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S](app-service-deploy-ftp.md).

Ce fichier doit se trouver dans _/home/site/wwwroot_. Dans le cas contraire, créez un _web.config_ fichier dans ce dossier par hello XML suivant :

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

Pour un existant _web.config_ de fichiers, copiez hello ensemble `<rule>` élément dans votre _web.config_de `configuration/system.webServer/rewrite/rules` élément. S’il existe d’autres `<rule>` éléments dans votre _web.config_, hello place copié `<rule>` élément avant hello autres `<rule>` éléments.

Cette règle retourne un HTTP 301 (redirection permanente) le protocole HTTPS toohello chaque fois que l’utilisateur de hello effectue une demande HTTP tooyour l’application web. Par exemple, il est redirigé à partir de `http://contoso.com` trop`https://contoso.com`.

Pour plus d’informations sur le module de réécriture d’URL IIS hello, consultez hello [réécriture d’URL](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.

## <a name="enforce-https-for-web-apps-on-linux"></a>Mettre en œuvre HTTPS pour Web Apps sous Linux

App Service sous Linux n’appliquant *pas* le protocole HTTPS, tout le monde peut accéder à votre application web à l’aide de HTTP. tooenforce HTTPS pour votre application web, définissez une règle de réécriture Bonjour _.htaccess_ fichier de votre application web. 

Connecter le point de terminaison de l’application tooyour web FTP en suivant les instructions de hello sur [déployer votre tooAzure d’application du Service d’applications à l’aide de FTP/S](app-service-deploy-ftp.md).

Dans _/home/site/wwwroot_, créez un _.htaccess_ fichier avec hello suivant de code :

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

Cette règle retourne un HTTP 301 (redirection permanente) le protocole HTTPS toohello chaque fois que l’utilisateur de hello effectue une demande HTTP tooyour l’application web. Par exemple, il est redirigé à partir de `http://contoso.com` trop`https://contoso.com`.

## <a name="automate-with-scripts"></a>Automatiser des tâches à l’aide de scripts

Vous pouvez automatiser des liaisons SSL pour votre application web avec des scripts, à l’aide de hello [CLI d’Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).

### <a name="azure-cli"></a>Interface de ligne de commande Azure

Hello commande suivante télécharge un fichier PFX exporté et obtient l’empreinte numérique hello.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

Hello commande suivante ajoute une liaison SSL SNI, à l’aide de l’empreinte numérique hello à partir de la commande précédente hello.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

Bonjour commande suivante télécharge un fichier PFX exporté et ajoute une liaison SSL SNI.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Mettre à jour le niveau de tarification de votre application
> * Lier votre tooApp de certificat SSL Service personnalisé
> * Appliquer le protocole HTTPS à votre application
> * Automatiser la liaison de certificat SSL avec des scripts

Avancer toolearn de didacticiel suivant toohello comment toouse Azure Content Delivery Network.

> [!div class="nextstepaction"]
> [Ajouter un tooan de réseau de distribution de contenu (CDN) Azure App Service](app-service-web-tutorial-content-delivery-network.md)
