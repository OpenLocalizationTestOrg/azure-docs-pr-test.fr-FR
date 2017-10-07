---
title: "aaaHow tooCreate un équilibrage de charge interne ASE à l’aide de Azure Resource Manager les modèles | Documents Microsoft"
description: "Découvrez comment toocreate un interne charger ASE équilibrage à l’aide de modèles Azure Resource Manager."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 091decb6-b0de-42a1-9f2f-c18d9b2e67df
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: stefsch
ms.openlocfilehash: 16db20eccc232ccc73107fcc8291de180fb2a323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-ilb-ase-using-azure-resource-manager-templates"></a>Comment tooCreate un équilibrage de charge interne ASE utilisation Azure Resource Manager de modèles

> [!NOTE] 
> Cet article porte sur hello environnement App Service v1. Il existe une version plus récente de hello environnement App Service toouse plus facile et s’exécute sur une infrastructure plus puissante. toolearn plus d’informations sur la nouvelle version de hello commencent par Bonjour [Introduction toohello environnement App Service](../app-service/app-service-environment/intro.md).
>

## <a name="overview"></a>Vue d'ensemble
Les environnements App Service peuvent être créés avec une adresse interne de réseau virtuel au lieu d’une adresse IP virtuelle publique.  Cette adresse interne est fournie par un composant Azure appelé équilibreur de charge interne hello (équilibrage de charge interne).  Un environnement app service Équilibrage de charge interne peut être créé à l’aide de hello portail Azure.  Il peut également être créé de manière automatisée par le biais des modèles Azure Resource Manager.  Cet article décrit les étapes hello et syntaxe nécessaires toocreate ASE équilibrage de charge avec les modèles Azure Resource Manager.

La création automatisée d’un ILB ASE comporte trois étapes :

1. Première ASE de base hello est créé dans un réseau virtuel à l’aide d’une adresse d’équilibrage de charge interne au lieu d’une adresse VIP publique.  Dans le cadre de cette étape, un nom de domaine racine est affecté toohello ASE d’équilibrage de charge interne.
2. Une fois hello QU'ASE d’équilibrage de charge interne est créée, un certificat SSL est téléchargé.  
3. Hello certificat SSL téléchargé est explicitement affectée toohello ASE d’équilibrage de charge interne en tant que son certificat SSL de « default ».  Ce certificat SSL permettant de tooapps de trafic SSL sur hello ASE d’équilibrage de charge interne lorsque les applications hello sont adressées à l’aide de hello courantes racine domaine affecté toohello ASE (par exemple, https://someapp.mycustomrootcomain.com)

## <a name="creating-hello-base-ilb-ase"></a>Création de hello ASE d’équilibrage de charge interne de Base
Un exemple de modèle Azure Resource Manager et son fichier de paramètres associés sont disponibles sur GitHub, [ici][quickstartilbasecreate].

La plupart des paramètres hello Bonjour *azuredeploy.parameters.json* fichier est des toocreating courantes deux ASEs équilibrage de charge interne, ainsi que ASEs lié tooa les adresses IP virtuelles publiques.  liste de Hello ci-dessous appelle les paramètres out de la Remarque spéciale, ou qui sont uniques, lors de la création d’un environnement app service Équilibrage de charge interne :

* *interalLoadBalancingMode*: dans la plupart des cas, définissez cette too3, ce qui signifie que le trafic HTTP/HTTPS sur les ports 80/443, et les ports de canal de contrôle et de données hello écoutés service hello FTP tooby hello ASE, sera lié tooan équilibrage de charge interne allouée réseau virtuel adresse interne.  Si cette propriété est définie à la place de too2, hello uniquement service FTP liée ports (canaux de contrôle et de données) seront liés tooan équilibrage de charge interne adresse, tandis que le reste sur l’adresse IP virtuelle publique de hello hello le trafic HTTP/HTTPS.
* *un suffixe DNS*: ce paramètre définit le domaine racine par défaut hello toohello ASE sera attribué.  Variante de public de hello du Service d’applications Azure, domaine racine de la valeur par défaut hello pour toutes les applications web est *azurewebsites.net*.  Toutefois, car un environnement app service Équilibrage de charge interne est le réseau virtuel du client de tooa interne, il n’a aucune domaine de racine par défaut du service public sens toouse hello.  Au lieu de cela, un ILB ASE doit avoir un domaine racine par défaut approprié pour une utilisation au sein du réseau virtuel interne d’une société.  Par exemple, un hypothétique Contoso Corporation peut utiliser un domaine de la racine par défaut de *contoso.com interne* pour les applications qui sont prévu tooonly pouvant être résolu et accessible dans le réseau virtuel de Contoso. 
* *ipSslAddressCount*: ce paramètre est automatiquement défini par défaut la valeur tooa 0 Bonjour *azuredeploy.json* fichier, car l’équilibrage de charge interne ASEs ont uniquement une seule adresse d’équilibrage de charge interne.  Aucune adresse IP SSL explicite pour un environnement app service Équilibrage de charge interne et par conséquent hello pool d’adresses IP SSL pour un environnement app service Équilibrage de charge interne doit avoir la valeur toozero, sinon une erreur de configuration se produit. 

Une fois hello *azuredeploy.parameters.json* fichier a été renseigné pour l’équilibrage de charge interne ASE, hello ASE d’équilibrage de charge interne peut ensuite être créé à l’aide de hello suivant extrait de code Powershell.  Modifiez toomatch de chemins d’accès de fichier hello où se trouvent les fichiers de modèle de gestionnaire de ressources Azure hello sur votre ordinateur.  N’oubliez pas également toosupply vos propres valeurs pour le nom du déploiement Azure Resource Manager hello et nom de groupe de ressources.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Après avoir hello Azure Resource Manager modèle est soumise que va prendre quelques heures pour hello ASE d’équilibrage de charge interne toobe est créé.  Une fois la création de hello terminée, hello ASE d’équilibrage de charge interne apparaîtront dans le portail hello UX dans liste hello des environnements de Service d’application pour l’abonnement hello qui a déclenché le déploiement de hello.

## <a name="uploading-and-configuring-hello-default-ssl-certificate"></a>Téléchargement et la configuration de certificat SSL « Par défaut » hello
Une fois hello QU'ASE d’équilibrage de charge interne est créée, un certificat SSL doit être associé hello ASE comme utilisation de certificats SSL hello « par défaut » pour l’établissement de tooapps des connexions SSL.  Poursuivre avec hello hypothétique Contoso Corporation exemple, si DNS par défaut l’hello du ASE suffixe est *contoso.com interne*, puis une connexion trop*https://some-random-app.internal-contoso.com*requiert un certificat SSL valide pour **-contoso.com .internal*. 

Il existe diverses façons tooobtain un certificat SSL valide, y compris les autorités de certification internes et acheter un certificat à partir d’un émetteur externe à l’aide d’un certificat auto-signé.  Quelle que soit la source de hello du certificat SSL de hello, hello des attributs de certificat suivants doivent toobe configuré correctement :

* *Objet*: cet attribut doit être défini trop **.votre-racine-domaine-here.com*
* *Nom de l’autre objet*: cet attribut doit inclure les deux **.votre-racine-domaine-here.com*, et **.scm.your-racine-domaine-here.com*.  raison de la deuxième entrée de hello Hello est que toohello de connexions SSL site SCM/Kudu associé à chaque application est effectué à l’aide d’une adresse sous forme de hello *your-app-name.scm.your-root-domain-here.com*.

Une fois le certificat SSL valide obtenu, deux étapes préparatoires supplémentaires sont nécessaires.  certificat SSL de Hello doit toobe converti/enregistré sous la forme d’un fichier .pfx.  N’oubliez pas de fichier .pfx hello doit tooinclude tous les intermédiaire et les certificats racines et également toobe sécurisé avec un mot de passe.

Fichier .pfx résultant de hello doit ensuite toobe converti en une chaîne encodée base64, car le certificat SSL de hello sera chargé à l’aide d’un modèle Azure Resource Manager.  Étant donné que les modèles Azure Resource Manager sont des fichiers texte, fichier .pfx de hello doit toobe converti en une chaîne encodée base64 afin qu’il peut être inclus en tant que paramètre de modèle de hello.

extrait de code Hello Powershell ci-dessous montre un exemple de la génération d’un certificat auto-signé, exportation hello certificat en tant que fichier .pfx, hello .pfx convertissant en base64 de la chaîne encodée et avant l’enregistrement hello base64 encodée du fichier de chaîne tooa distinct.  Hello code Powershell pour le codage base64 est une adaptation de hello [Blog de Scripts Powershell][examplebase64encoding].

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "*.internal-contoso.com","*.scm.internal-contoso.com"

    $certThumbprint = "cert:\localMachine\my\" + $certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText

    $fileName = "exportedcert.pfx"
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password     

    $fileContentBytes = get-content -encoding byte $fileName
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)
    $fileContentEncoded | set-content ($fileName + ".b64")

Une fois hello certificat a été généré avec succès et chaîne tooa converti en Base64, hello exemple de modèle Azure Resource Manager sur GitHub pour [configuration des certificats SSL hello par défaut] [ configuringDefaultSSLCertificate] peut être utilisé.

Hello paramètres Bonjour *azuredeploy.parameters.json* fichier sont répertoriées ci-dessous :

* *appServiceEnvironmentName*: nom hello Hello ASE d’équilibrage de charge en cours de configuration.
* *existingAseLocation*: chaîne de texte contenant hello région Azure où hello ASE d’équilibrage de charge interne a été déployé.  Par exemple, « South Central US ».
* *pfxBlobString*: hello based64 encodée du fichier .pfx de hello de représentation sous forme de chaîne.  À l’aide d’extrait de code hello indiqué précédemment, vous serez copier la chaîne hello contenue dans « exportedcert.pfx.b64 » et collez-le dans en tant que valeur hello Hello *pfxBlobString* attribut.
* *mot de passe*: le fichier .pfx hello hello mot de passe utilisé toosecure.
* *certificateThumbprint*: hello empreinte numérique du certificat.  Si vous récupérez cette valeur à partir de Powershell (par exemple, *$certificate. L’empreinte numérique* de hello extrait de code précédent), vous pouvez utiliser la valeur hello-est.  Toutefois si vous copiez la valeur de hello à partir de la boîte de dialogue certificat de Windows hello, n’oubliez pas de toostrip les espaces superflus de hello.  Hello *certificateThumbprint* doit ressembler à : AF3143EB61D43F6727842115BB7F17BBCECAECAE
* *certificateName*: un identificateur de chaîne conviviale de votre choix utilisé certificat de hello tooidentity.  nom de Hello est utilisé en tant que partie de l’identificateur Azure Resource Manager hello pour hello *Microsoft.Web/certificates* entité représentant le certificat SSL de hello.  nom de Hello **doit** se terminer par hello suivant suffixe : \_yourASENameHere_InternalLoadBalancingASE.  Ce suffixe est utilisé par le portail de hello tel qu’un indicateur de hello certificat est utilisé pour sécuriser un environnement app service activé d’équilibrage de charge interne.

Un exemple abrégé de fichier *azuredeploy.parameters.json* est présenté ci-dessous :

    {
         "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json",
         "contentVersion": "1.0.0.0",
         "parameters": {
              "appServiceEnvironmentName": {
                   "value": "yourASENameHere"
              },
              "existingAseLocation": {
                   "value": "East US 2"
              },
              "pfxBlobString": {
                   "value": "MIIKcAIBAz...snip...snip...pkCAgfQ"
              },
              "password": {
                   "value": "PASSWORDGOESHERE"
              },
              "certificateThumbprint": {
                   "value": "AF3143EB61D43F6727842115BB7F17BBCECAECAE"
              },
              "certificateName": {
                   "value": "DefaultCertificateFor_yourASENameHere_InternalLoadBalancingASE"
              }
         }
    }

Une fois hello *azuredeploy.parameters.json* fichier a été renseigné, de certificat SSL de hello par défaut peut être configuré à l’aide de hello suivant extrait de code Powershell.  Modifiez toomatch de chemins d’accès de fichier hello où se trouvent les fichiers de modèle de gestionnaire de ressources Azure hello sur votre ordinateur.  N’oubliez pas également toosupply vos propres valeurs pour le nom du déploiement Azure Resource Manager hello et nom de groupe de ressources.

    $templatePath="PATH\azuredeploy.json"
    $parameterPath="PATH\azuredeploy.parameters.json"

    New-AzureRmResourceGroupDeployment -Name "CHANGEME" -ResourceGroupName "YOUR-RG-NAME-HERE" -TemplateFile $templatePath -TemplateParameterFile $parameterPath

Après avoir hello Azure Resource Manager modèle est soumise que prendra environ 40 minutes minutes par modification de hello ASE tooapply frontal.  Par exemple, avec une valeur par défaut ASE taille à l’aide de deux serveurs frontaux, le modèle de hello prendra autour d’une heure et vingt minutes toocomplete.  Pendant l’exécution de modèle de hello hello ASE ne seront pas en mesure de tooscaled.  

Une fois le modèle de hello terminée, les applications sur hello ASE d’équilibrage de charge interne est accessible via le protocole HTTPS et hello connexions seront sécurisées à l’aide du certificat SSL de hello par défaut.  certificat SSL de Hello par défaut servira lorsque les applications sur hello ASE d’équilibrage de charge interne sont adressées à l’aide d’une combinaison de nom de l’application hello ainsi que le nom d’hôte de hello par défaut.  Par exemple *https://mycustomapp.internal-contoso.com* utiliserait hello par défaut certificat SSL **-contoso.com .internal*.

Toutefois, tout comme les applications qui s’exécutent sur le service de plusieurs locataires hello publique, les développeurs peuvent également configurer les noms d’hôtes personnalisés pour les applications individuelles et puis configurez les liaisons de certificat SSL SNI uniques pour différentes applications.  

## <a name="getting-started"></a>Prise en main
tooget démarré avec les environnements de Service d’application, consultez [Introduction tooApp environnement de Service](app-service-app-service-environment-intro.md)

Tous les articles et comment-de pour les environnements App Service sont disponibles dans hello [fichier Lisezmoi pour les environnements de Service d’Application](../app-service/app-service-app-service-environments-readme.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[quickstartilbasecreate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-create/
[examplebase64encoding]: http://powershellscripts.blogspot.com/2007/02/base64-encode-file.html 
[configuringDefaultSSLCertificate]: https://azure.microsoft.com/documentation/templates/201-web-app-ase-ilb-configure-default-ssl/ 

