---
title: "application de Service d’applications Azure tooyour de certificats aaaAdd une connexion SSL | Documents Microsoft"
description: "Découvrez comment tooadd une connexion SSL certificat tooyour application de Service d’applications."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Acheter et configurer un certificat SSL pour votre service Azure App Service

Dans ce didacticiel, vous allez sécuriser votre application web en achetant un certificat SSL pour votre **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, en le stockant dans [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) de manière sécurisée, et en l’associant à un domaine personnalisé.

## <a name="step-1---log-in-tooazure"></a>Étape 1 : ouvrez une session dans tooAzure

Ouvrez une session dans toohello portail Azure à http://portal.azure.com

## <a name="step-2---place-an-ssl-certificate-order"></a>Étape 2 : Passer une commande de certificat SSL

Vous pouvez placer une commande de certificat SSL en créant un [certificat de Service de l’application](https://portal.azure.com/#create/Microsoft.SSL) Bonjour **portail Azure**.

![Création du certificat](./media/app-service-web-purchase-ssl-web-site/createssl.png)

Entrez un nom convivial de **nom** de certificat pour SSL et entrez hello **nom de domaine**

> [!NOTE]
> Il s’agit d’une des parties essentielles de hello du processus d’achat hello. Assurez-vous que tooenter corriger le nom d’hôte (domaine personnalisé) que vous souhaitez tooprotect avec ce certificat. **Ne le faites pas** ajouter le nom d’hôte hello avec WWW. 
>

Sélectionnez votre **abonnement**, **groupe de ressources** et **référence (SKU) de certificat**

> [!WARNING]
> Certificats de Service d’application exclusivement par d’autres Services d’application au sein de hello même abonnement.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>Étape 3 : stocker le certificat hello dans Azure Key Vault

> [!NOTE]
> [Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) est un service Azure qui permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud.
>

Une fois hello achat du certificat SSL est terminée, vous devez tooopen [App Service Certificate](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) panneau des ressources.

![Insérer une image de toostore prêt dans KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

Vous remarquerez que l’état du certificat est **« Émission en attente »** qu’il sont a quelques étapes supplémentaires vous devez toocomplete avant de commencer à l’aide de ce certificat.

Cliquez sur **Configuration de certificat** à l’intérieur du panneau des propriétés du certificat, puis cliquez sur **étape 1 : magasin** toostore ce certificat dans Azure Key Vault.

À partir de **clé de coffre état** panneau, cliquez sur **référentiel de coffre de clé** toochoose un toostore de coffre de clés existant ce certificat **ou créer nouveau coffre de clés** toocreate nouvelle clé de coffre à l’intérieur du même groupe d’abonnement et de ressources.

> [!NOTE]
> Azure Key Vault engendre peu de frais pour le stockage de ce certificat.
> Pour plus d’informations, consultez **[Tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.
>

Après avoir sélectionné hello référentiel de coffre de clé toostore ce certificat dans, hello **magasin** option doit afficher succès.

![insérer une image de réussite du stockage dans KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>Étape 4 - vérifier hello la propriété du domaine

> [!NOTE]
> Il existe 3 types de vérification du domaine pris en charge par les certificats App Service : domaine, e-mail et manuelle. Ceux-ci sont expliquées plus en détails dans hello [avancé section](#advanced).

À partir de hello même **Configuration de certificat** panneau que vous avez utilisé à l’étape 3, cliquez sur **étape 2 : vérifier**.

**Vérification du domaine** ce processus plus pratique de hello est **uniquement si** avoir  **[acheté votre domaine personnalisé à partir du Service d’applications Azure.](custom-dns-web-site-buydomains-web-app.md)**
Cliquez sur **Vérifiez** bouton toocomplete cette étape.

![insérer une image de vérification du domaine](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

Après avoir cliqué sur **Vérifiez**, utilisez hello **Actualiser** bouton jusqu'à ce que hello **Vérifiez** option doit afficher succès.

![insérer une image de réussite de la vérification dans KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>Étape 5 : affecter tooApp du certificat de Service d’applications

> [!NOTE]
> Avant d’effectuer les étapes hello dans cette section, vous devez associé un nom de domaine personnalisé avec votre application. Pour plus d’informations, consultez la page **[Configuration d’un nom de domaine personnalisé pour une application web.](app-service-web-tutorial-custom-domain.md)**
>

Bonjour  **[portail Azure](https://portal.azure.com/)**, cliquez sur hello **du Service d’applications** option à gauche de hello de page de hello.

Cliquez sur le nom de hello de votre application toowhich souhaité tooassign ce certificat.

Bonjour **paramètres**, cliquez sur **certificats SSL**.

Cliquez sur **importer un certificat Service application** et sélectionnez hello certificat que vous venez d’acheter.

![insérer une image d’importation de certificat](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

Bonjour **liaisons ssl** section cliquez sur **ajouter des liaisons**et utilisez hello menus déroulants tooselect hello domaine nom toosecure avec SSL, hello toouse de certificat. Vous pouvez également sélectionner si toouse  **[Indication de nom de serveur (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ou SSL basé sur IP.

![insérer une image de liaisons SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

Cliquez sur **ajouter la liaison de** toosave hello les modifications et activer le protocole SSL.

> [!NOTE]
> Si vous avez sélectionné **SSL basé sur IP** et votre domaine personnalisé est configuré à l’aide d’un enregistrement A, vous devez effectuer des hello supplémentaires comme suit. Ceux-ci sont expliquées plus en détails dans hello [avancé section](#Advanced).

À ce stade, vous doit être en mesure de toovisit à votre application à l’aide de `HTTPS://` au lieu de `HTTP://` tooverify qui hello certificat a été configuré correctement.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>Étape 6 : Tâches de gestion

### <a name="azure-cli"></a>Interface de ligne de commande Azure

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>Avancé

### <a name="verifying-domain-ownership"></a>Vérifier la propriété du domaine

Il existe 2 autres types de vérification du domaine pris en charge par les certificats App Service : e-mail et manuelle.

#### <a name="mail-verification"></a>Vérification par e-mail

Message de vérification a déjà été envoyée à toohello que les adresses de messagerie associé à ce domaine personnalisé.
étape de vérification toocomplete hello par courrier électronique, par courrier électronique hello, cliquez sur le lien de vérification hello.

![insérer une image de vérification par e-mail](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

Si vous avez besoin de message de vérification tooresend hello, cliquez sur hello **renvoyer un E-mail** bouton.

#### <a name="manual-verification"></a>Vérification manuelle

> [!IMPORTANT]
> Vérification de page web HTML (fonctionne uniquement avec la référence du certificat standard)
>

1. Créez un fichier HTML nommé **« starfield.html »**

1. Contenu de ce fichier doit être nom exact de hello Hello jeton de vérification de domaine. (Vous pouvez copier le jeton de hello de hello Panneau de statut de vérification de domaine)

1. Télécharger ce fichier à la racine de hello du serveur web de hello hébergeant votre domaine`/.well-known/pki-validation/starfield.html`

1. Cliquez sur **Actualiser** tooupdate état du certificat hello après la vérification est terminée. Il peut prendre quelques minutes pour toocomplete de vérification.

> [!TIP]
> Vérifiez dans un à l’aide de Terminal Server `curl -G http://<domain>/.well-known/pki-validation/starfield.html` réponse de hello doit contenir hello `<verification-token>`.

#### <a name="dns-txt-record-verification"></a>Vérification d’enregistrement TXT DNS

1. Le Gestionnaire DNS, de créer un enregistrement TXT sur hello `@` sous-domaine avec la valeur de toohello égale jeton de vérification de domaine.
1. Cliquez sur **« Actualiser »** tooupdate hello état du certificat une fois la vérification est terminée.

> [!TIP]
> Vous avez besoin d’un enregistrement TXT de toocreate sur `@.<domain>` avec la valeur `<verification-token>`.

### <a name="assign-certificate-tooapp-service-app"></a>Affecter le certificat tooApp application de Service

Si vous avez sélectionné **SSL basé sur IP** et votre domaine personnalisé est configuré à l’aide d’un enregistrement A, vous devez effectuer des hello supplémentaires comme suit :

Après avoir configuré une adresse IP en fonction de liaison SSL, une adresse IP dédiée est affectée tooyour application. Vous pouvez trouver cette adresse IP sur hello **un domaine personnalisé** page sous les paramètres de votre application, juste au-dessus de hello **noms d’hôtes** section. Elle est répertoriée en tant qu’**Adresse IP externe**

![insérer une image d’IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

Notez que cette adresse IP est différente de celle de l’adresse IP virtuelle hello utilisé précédemment enregistrement tooconfigure hello pour votre domaine. Si vous avez configuré toouse SSL basé sur SNI, ou ne sont pas configurés toouse SSL, aucune adresse n’est répertoriée pour cette entrée.

À l’aide des outils de hello fournis par votre bureau d’enregistrement du nom de domaine, modifiez hello un enregistrement pour votre domaine personnalisé nom toopoint toohello adresse IP à partir de l’étape précédente de hello.

## <a name="rekey-and-sync-hello-certificate"></a>Changement de clé et hello de synchronisation des certificats

Si vous avez besoin tooRekey votre certificat, sélectionnez **recomposition la synchronisation et** option à partir de **propriétés du certificat** panneau.

Cliquez sur **recomposition** bouton processus de hello tooinitiate. Ce processus peut prendre toocomplete de 1 à 10 minutes.

![insérer une image de renouvellement de clé SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

Régénération de votre certificat restaure certificat hello avec un nouveau certificat émis à partir de l’autorité de certification hello.

## <a name="next-steps"></a>Étapes suivantes

* [Ajouter un réseau de distribution de contenu](app-service-web-tutorial-content-delivery-network.md)