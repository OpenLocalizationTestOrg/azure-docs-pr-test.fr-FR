---
title: "Notes d’aaaRelease pour Azure BizTalk Services | Documents Microsoft"
description: "Hello répertorie les problèmes connus pour Azure BizTalk Services"
services: biztalk-services
documentationcenter: 
author: msftman
manager: erikre
editor: 
ms.assetid: f4906fdc-4cd9-4a57-a007-a88c2e51a18f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2016
ms.author: deonhe
ms.openlocfilehash: ea53d6c40ed58badf4141453dc77d28dcfc6407f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-biztalk-services"></a>Notes de publication pour Azure BizTalk Services

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

notes de publication Hello pour hello Microsoft Azure BizTalk Services contiennent hello problèmes connus dans cette version.

## <a name="whats-new-in-hello-november-update-of-biztalk-services"></a>Nouveautés de la mise à jour de novembre hello de BizTalk Services
* Chiffrement au repos peut être activé dans hello portail BizTalk Services. Consultez [Activer le chiffrement au repos dans le portail BizTalk Services](https://msdn.microsoft.com/library/azure/dn874052.aspx).

## <a name="update-history"></a>Historique de mise à jour
### <a name="october-update"></a>Mise à jour d’octobre
* Les comptes de société sont pris en charge :  
  * **Scénario** : vous avez inscrit un déploiement de service BizTalk à l’aide d’un compte Microsoft (par exemple, user@live.com). Dans ce scénario, Microsoft seulement les Account les utilisateurs peuvent gérer hello BizTalk Service à l’aide du portail de Services BizTalk hello. Il est impossible d’utiliser un compte professionnel.  
  * **Scénario** : vous avez inscrit un déploiement de service BizTalk à l’aide d’un compte professionnel dans Azure Active Directory (par exemple user@fabrikam.com ou user@contoso.com). Dans ce scénario, seuls les utilisateurs Azure Active Directory au sein de la même organisation peut gérer de hello hello BizTalk Service à l’aide du portail de Services BizTalk hello. Il est impossible d’utiliser un compte Microsoft.  
* Lorsque vous créez un BizTalk Service Bonjour portail Azure classic, vous êtes inscrit automatiquement dans hello portail BizTalk Services.
  * **Scénario**: vous vous connectez à hello portail Azure classic, créez un BizTalk Service, puis **gérer** pourquoi toute première fois. Lorsque le portail BizTalk Services hello s’ouvre, hello BizTalk Service inscrit automatiquement et est prêt pour vos déploiements.  
    Consultez [l’inscription et la mise à jour d’un déploiement de Service BizTalk sur hello portail BizTalk Services](https://msdn.microsoft.com/library/azure/hh689837.aspx).  

### <a name="august-14-update"></a>Mise à jour du 14 août
* Contrat et le découplage des commerciaux des accords de partenariat et les ponts sont maintenant découplés sur hello portail BizTalk Services. Vous créez des accords et des ponts séparément et au runtime ponts accord tooan en fonction des valeurs hello message EDI de type hello. Consultez [Créer des accords dans Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689908.aspx), [Création d’un pont EDI à l’aide du portail BizTalk Services](https://msdn.microsoft.com/library/azure/dn793986.aspx), [Création d’un pont AS2 à l’aide du portail BizTalk Services](https://msdn.microsoft.com/library/azure/dn793993.aspx) et [Comment les ponts résolvent-ils les accords au moment de l’exécution ?](https://msdn.microsoft.com/library/azure/dn794001.aspx)  
* modèles de toocreate option Hello pour les accords n’est plus disponible.  
* Pour l’accord côté envoi de hello, vous pouvez maintenant spécifier différents jeux de délimiteurs pour chaque schéma. Cette configuration est spécifiée dans les paramètres de protocole pour le côté envoi de l’accord. Pour plus d’informations, consultez [Création d’un accord X12 dans Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689847.aspx) et [Création d’un accord EDIFACT dans Azure BizTalk Services](https://msdn.microsoft.com/library/azure/dn606267.aspx). Deux nouvelles entités sont également ajoutées toohello API TPM OM pour hello même but. Consultez [X12DelimiterOverrides](https://msdn.microsoft.com/library/azure/dn798749.aspx) et [EDIFACTDelimiterOverride](https://msdn.microsoft.com/library/azure/dn798748.aspx).  
* Les constructions XSD standard, et notamment les types dérivés, sont désormais prises en charge. Consultez [Utilisation de constructions XSD standard dans vos mappages](https://msdn.microsoft.com/library/azure/dn793987.aspx) et [Scénarios et exemples de mappage de type dérivé](https://msdn.microsoft.com/library/azure/dn793997.aspx).  
* AS2 prend en charge les nouveaux algorithmes MIC pour la signature des messages et de nouveaux algorithmes de chiffrement. Voir [Créer un accord AS2 dans Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689890.aspx).  
  ## <a name="know-issues"></a>Problèmes connus

### <a name="connectivity-issues-after-biztalk-services-portal-update"></a>Problèmes de connectivité après la mise à jour du portail BizTalk Services
  Si vous avez hello ouvrir le portail BizTalk Services pendant la mise à niveau de BizTalk Services tooroll dans modifications toohello service, vous risquez de rencontrer des problèmes de connectivité hello portail BizTalk Services.  
  Comme solution de contournement, vous pouvez redémarrer le navigateur de hello, supprimer le cache du navigateur hello ou démarrer le portail de hello en mode privé.  

### <a name="visual-studio-ide-cannot-locate-hello-artifact-if-you-click-an-error-or-warning-in-a-biztalk-services-project"></a>IDE de Visual Studio ne peut pas localiser l’artefact de hello si vous cliquez sur une erreur ou un avertissement dans un projet BizTalk Services
Installez le problème de hello toofix hello Visual Studio 2012 Update 3 RC 1.  

### <a name="custom-binding-project-reference"></a>Référence de projet de liaison personnalisée
Tenez compte des hello suivant situations avec un projet BizTalk Services dans une solution Visual Studio :  

* Dans hello même solution Visual Studio, il existe un projet BizTalk Services et un projet de liaison personnalisée. Hello projet BizTalk Service dispose d’un fichier de projet de référence toothis liaison personnalisée.
* Hello projet de BizTalk Service a un référence tooa liaison/comportement personnalisé DLL.

Vous 'Build' hello solution dans Visual Studio avec succès. Ensuite, vous « Reconstruisez » ou « Nettoyez » la solution de hello. Après cela, lorsque vous générez ou nettoyez à nouveau, hello suivant a lieu :  
  Impossible de toocopy fichier <Path tooDLL> too"bin\Debug\FileName.dll ». processus de Hello Impossible d’accéder au fichier de hello 'bin\Debug\FileName.dll', car il est utilisé par un autre processus.  

#### <a name="workaround"></a>Solution de contournement
* Si [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) est installé, vous avez hello deux options suivantes :
  
  * Redémarrer Visual Studio ou
  * Redémarrez la solution de hello. Exécutez ensuite une seule Build sur la solution de hello.  
* Si [Visual Studio 2012 Update 3](https://www.microsoft.com/download/details.aspx?id=39305) est ne pas installé, ouvrez le Gestionnaire des tâches et cliquez sur onglet de processus hello, cliquez sur le processus MSBuild.exe hello, puis cliquez sur le bouton Terminer le processus de hello.  

### <a name="routing-toobasichttprelay-endpoints-is-not-supported-from-bridges-and-biztalk-services-portal-if-non-printable-characters-are-promoted-as-http-headers"></a>Routage des points de terminaison tooBasicHttpRelay n'est pas pris en charge à partir des ponts et le portail BizTalk Services si les caractères non imprimables sont promus en tant qu’en-têtes HTTP
Si vous utilisez des caractères non imprimables dans le cadre des propriétés promues des messages, ces messages ne peut pas être routé toorelay destinations qui utilisent une liaison BasicHttpRelay hello. En outre, hello promue propriétés qui sont disponibles dans le cadre du suivi sont codées URL pour les objets BLOB et non codées pour des destinations.  

### <a name="mdn-is-sent-asynchronously-even-if-hello-send-asynchronous-mdn-option-is-unchecked"></a>MDN est envoyé de façon asynchrone même si hello envoyer option MDN asynchrone est désactivée
Envisagez le scénario suivant : Si vous sélectionnez hello **envoyez un MDN asynchrone** case à cocher et spécifier un MDN URL toosend hello asynchrone et désélectionnez hello **envoyez un MDN asynchrone** case à cocher, hello MDN est toujours toohello envoyé spécifié URL bien hello option toosend async MDN n’est pas sélectionnée.  
Pour résoudre ce problème, vous devez effacer hello spécifié l’URL avant de décocher hello **envoyez un MDN asynchrone** case à cocher, puis déployer le contrat de hello AS2.  

### <a name="whitespace-characters-beyond-a-valid-interchange-cause-an-empty-message-toobe-sent-toohello-suspend-endpoint"></a>Les espaces situés au-delà d’une cause d’échange valide un toohello toobe envoyé de message vide suspendre le point de terminaison
S’il existe des espaces au-delà d’un segment IEA, le désassembleur de hello traite cela comme fin de l’échange actuel et examine hello jeu d’espaces suivant comme un nouveau message. Dans la mesure où il ne s’agit pas d’échange valide, vous pouvez observer qu’un message de réussite est envoyé à destination de routage toohello et un message vide est envoyé hello suspendre le point de terminaison.  

### <a name="tracking-in-biztalk-services-portal"></a>Suivi dans le portail Azure BizTalk Services
Événements de suivi sont capturés de traitement des messages EDI toohello et de corrélation. Si un message échoue hors hello étape protocole, le suivi est considéré comme réussi. Dans ce cas, consultez la section du journal toohello sous hello **détails** colonne **suivi** pour les détails de l’erreur.
Hello X12 recevoir et envoyer des paramètres ([créer une X12 accord dans Azure BizTalk Services](https://msdn.microsoft.com/library/azure/hh689847.aspx)) fournissent des informations sur hello étape protocole.  

### <a name="update-agreement"></a>Accord de mise à jour
Hello portail BizTalk Services vous permet de toomodify hello qualificateur d’une identité lorsqu’un accord est configuré. Cela peut entraîner des propriétés incohérentes. Par exemple, il est un accord utilisant ZZ : 1234567 et ZZ : 7654321 hello qualificateur. Dans les paramètres de profil du portail BizTalk Services hello, vous modifiez ZZ : 1234567 toobe 01:ChangedValue. Vous ouvrez l’accord de hello et 01:ChangedValue s’affiche au lieu de ZZ : 1234567.
toomodify hello qualificateur d’une identité, l’accord de hello supprimer, mettre à jour **identités** dans hello du profil de partenaire et recréez le contrat de hello.  

> AZURE.WARNING Ce comportement a un impact sur X12 et AS2.  
> 
> 

### <a name="as2-attachments"></a>Pièces jointes AS2
Les pièces jointes aux messages AS2 ne sont pas prises en charge dans les envois ou la réception. Plus précisément, les pièces jointes sont ignorées silencieusement et le corps du message hello est traité comme un message AS2 classique.  

### <a name="resources-remembering-path"></a>Ressources : mémoriser le chemin d’accès
Lorsque vous ajoutez **ressources**, boîte de dialogue hello plus difficiles à mémoriser hello tooadd de chemin d’accès utilisé précédemment une ressource. tooremember hello précédemment-chemin d’accès utilisé, essayez d’ajouter le site web de portail BizTalk Services hello trop**Sites de confiance** dans Internet Explorer.  

### <a name="if-you-rename-hello-entity-name-of-a-bridge-and-close-hello-project-without-saving-changes-opening-hello-entity-again-results-in-an-error"></a>Si vous renommez le nom de l’entité hello d’un pont et le projet de hello fermer sans enregistrer les modifications, rouvrir l’entité de hello entraîne une erreur
Considérez un scénario Bonjour suivant l’ordre :  

* Ajouter un projet de BizTalk Service de tooa pont (par exemple un pont unidirectionnel XML)  
* Renommez le pont de hello en spécifiant une valeur pour hello propriété de nom de l’entité. Cela renomme hello .bridgeconfig associé avec le nom hello spécifié.  
* Fermez le fichier .bcs de hello (en fermant l’onglet hello dans Visual Studio) sans enregistrer les modifications de hello.  
* Ouvrez le fichier .bcs de hello à nouveau à partir de l’Explorateur de solutions de hello.  
  Vous remarquerez que pendant que le fichier .bridgeconfig associé de hello a le nom du nouveau hello spécifié, nom de l’entité sur l’aire de conception hello hello est toujours l’ancien nom hello. Si vous essayez d’en double-cliquant sur le composant de pont hello tooopen hello Configuration du pont, vous obtenez hello l’erreur suivante :  
  `‘<old name>’ Entity’s associated file ‘<old name>.bridgeconfig’ does not exist`tooavoid en cours d’exécution dans ce scénario, assurez-vous que vous enregistrez les modifications après avoir renommé les entités hello dans un projet de BizTalk Service.  
  
### <a name="biztalk-service-project-builds-successfully-even-if-an-artifact-has-been-excluded-from-a-visual-studio-project"></a>Le projet de BizTalk Service est généré avec succès même si un artefact a été exclu d’un projet Visual Studio
Considérez un scénario où vous ajoutez un projet de BizTalk Service de tooa artefact (par exemple, un fichier XSD), incluez cet artefact Bonjour Configuration du pont (par exemple, en le spécifiant comme un type de message de demande), puis excluez projet de Visual Studio hello. Dans ce cas, la création de projet de hello n’enverrez pas de toute erreur tant qu’artefact de hello supprimé est disponible sur le disque de hello à hello même emplacement que celui où il a été inclus dans le projet de Visual Studio hello.
  
### <a name="hello-biztalk-service-project-does-not-check-for-schema-availability-while-configuring-hello-bridges"></a>Hello projet de BizTalk Service ne vérifie pas pour la disponibilité de schéma lors de la configuration des ponts de hello
Dans un projet de BizTalk Service, si un schéma est ajouté toohello projet importe un autre schéma, hello projet de BizTalk Service ne vérifie pas si les schémas importés hello sont ajouté toohello projet. Si vous essayez toobuild un tel projet, vous n’obtenez pas les erreurs de build.
  
### <a name="hello-response-message-for-a-xml-request-reply-bridge-is-always-of-charset-utf-8"></a>message de réponse Hello pour un pont demande-réponse de XML est toujours du jeu de caractères UTF-8
Pour cette version, jeu de caractères hello hello du message de réponse à partir d’un pont demande-réponse XML est toujours défini tooUTF-8.
  
### <a name="user-defined-datatypes"></a>Types de données définis par l’utilisateur
adaptateurs de BizTalk Adapter Pack Hello dans la fonctionnalité de Service d’adaptateur BizTalk hello, utilisez les types de données définis par l’utilisateur pour les opérations de carte.
Lorsque vous utilisez des types de données définis par l’utilisateur, copiez toodrive:\Program Files\Microsoft de fichiers (.dll) hello BizTalk Adapter Service\BAServiceRuntime\bin\ ou toohello Global Assembly Cache (GAC) sur le serveur hello hello Service d’adaptateur BizTalk service d’hébergement. Dans le cas contraire, hello l’erreur suivante peut se produire sur le client de hello :  
```
<s:Fault xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
<faultcode>s:Client</faultcode>
<faultstring xml:lang="en-US">hello UDT with FullName "File, FileUDT, Version=Value, Culture=Value, PublicKeyToken=Value" could not be loaded. Try placing hello assembly containing hello UDT definition in hello Global Assembly Cache.</faultstring>
<detail>
  <AFConnectRuntimeFault xmlns="http://Microsoft.ApplicationServer.Integration.AFConnect/2011" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <ExceptionCode>ERROR_IN_SENDING_MESSAGE</ExceptionCode>
  </AFConnectRuntimeFault>
</detail>
</s:Fault>
```  
  
> [!IMPORTANT]
> Il est recommandé de toouse GACUtil.exe tooinstall un fichier dans le Global Assembly Cache de hello. GACUtil.exe documents comment toouse cette option de ligne de commande Visual Studio outil et hello.  
> 
> 

### <a name="restarting-hello-biztalk-adapter-service-web-site"></a>Le redémarrage hello Site Web de Service de l’adaptateur BizTalk
Lors de l’installation hello **Runtime du Service de l’adaptateur BizTalk*** crée hello **Service d’adaptateur BizTalk** site web dans IIS qui contient hello **BAService** application. **BAService** application utilise en interne la portée de hello relais liaison tooextend de cloud de toohello de point de terminaison de service local. Pour un service hébergé localement, point de terminaison de relais correspondant hello est inscrit sur hello Service Bus uniquement lors de hello démarrage du service sur site.  

Si vous arrêtez et démarrez une application, la configuration de hello de démarrage automatique d’une application n’est pas reconnue. Par conséquent, lorsque **BAService** est arrêté, vous devez toujours redémarrer hello **Service d’adaptateur BizTalk** site web à la place. Ne pas démarrer ou arrêter hello **BAService** application.

### <a name="special-characters-should-not-be-used-for-address-and-entity-names-of-lob-components"></a>Les caractères spéciaux ne doivent pas être utilisés pour les noms d’adresse et d’entité des composants métier.
Vous ne devez pas utiliser de caractères spéciaux avec les nom et adresse d’entité et des composants métier. Si vous procédez ainsi, vous obtiendrez une erreur lors du déploiement de hello projet de BizTalk Service. Pour certains caractères comme « % », site Web du Service d’adaptateur BizTalk hello peut entrer en état arrêté et vous devez toomanually démarrez-le.

### <a name="test-map-with-get-context-property"></a>Test de mappage avec propriété de contexte Get
Si une transformation contient une opération de mappage **Obtenir une propriété de contexte**, l’opération **Tester le mappage** échoue. En tant que solution de contournement temporaire, remplacez hello **Get Context Property** opération de mappage avec une chaîne de concaténer opération de mappage contenant des données fictives. Cela remplir le schéma cible hello et vous permettre de que tester autres fonctionnalités de transformation.

### <a name="test-map-property-does-not-display"></a>La propriété Tester le mappage ne s’affiche pas
Hello **Test Map** propriétés ne s’affichent pas dans Visual Studio. Cela peut se produire si hello **propriétés** fenêtre et hello **l’Explorateur de solutions** fenêtre ne sont pas ancrées simultanément. tooresolve, hello dock **propriétés** et hello **l’Explorateur de solutions** windows.  

### <a name="datetime-reformat-drop-down-is-grayed-out"></a>La liste déroulante Reformat DateTime est affichée en grisé
Lors de l’ajout d’une opération de mappage de reformater DateTime toohello concevoir hello aire de conception et configurée, Format de liste déroulante peut-être être grisée. Cela peut se produire si la valeur d’affichage de votre ordinateur hello **moyenne – 125 %** ou **grande-150 %**. tooresolve, définissez affichage de hello trop**petite-100 % (par défaut)** à l’aide des étapes hello ci-dessous :  

1. Ouvrez hello **le panneau de configuration** et cliquez sur **apparence et personnalisation**.
2. Cliquez sur **Affichage**.
3. Cliquez sur **Petite - 100 % (par défaut)**, puis sur **Appliquer**.

Hello **Format** liste déroulante devrait désormais fonctionner comme prévu.

### <a name="duplicate-agreements-in-hello-biztalk-services-portal"></a>Accords en double dans hello portail BizTalk Services
Tenez compte des hello scénario :

1. Créer un accord à l’aide de l’API OM hello commercial gestion des partenaires.
2. Ouvrez le contrat de hello dans hello portail BizTalk Services dans les deux onglets différents.
3. Déployer l’accord hello dans les deux onglets hello.
4. Par conséquent, les deux accords hello sont alors déployés, ce qui entraîne des entrées en double dans hello portail BizTalk Services

**Solution de contournement**. Ouvrez l’un des deux accords de hello Bonjour portail BizTalk Services et annuler le déploiement.  

### <a name="bridges-do-not-use-updated-certificate-even-after-a-certificate-has-been-updated-in-hello-artifact-store"></a>Les ponts n’utilisent pas le certificat mis à jour même après qu’un certificat a été mis à jour dans le magasin d’artefacts hello
Tenez compte des hello les scénarios suivants :  

**Scénario 1 : À l’aide de certificats basés sur l’empreinte numérique pour sécuriser le transfert de message à partir d’un point de terminaison pont tooa**  
Envisagez un scénario dans lequel vous utilisez les certificats basés sur l’empreinte numérique dans votre projet de BizTalk Service. Mettre à jour de certificat hello Bonjour portail BizTalk Services avec hello même nom, mais une autre empreinte numérique, mais ne mettez pas à jour hello projet de BizTalk Service en conséquence. Dans ce scénario, hello pont risque de continuer les messages hello tooprocess, car les anciennes données du certificat hello peut-être toujours dans le cache de canaux hello. Après cela, le traitement du message échoue.  

**Solution de contournement**: certificat hello Bonjour projet BizTalk Service de mise à jour et redéployer le projet de hello.  

**Scénario 2 : L’utilisation de certificats de tooidentify comportements basés sur un nom pour sécuriser le transfert de message à partir d’un point de terminaison pont tooa**

Considérez un scénario où vous utilisez des certificats de tooidentify de comportements basés sur le nom de votre projet de BizTalk Service. Mettre à jour le certificat hello Bonjour portail BizTalk Services, mais ne mettez pas à jour hello projet de BizTalk Service en conséquence. Dans ce scénario, hello pont risque de continuer les messages hello tooprocess, car les anciennes données du certificat hello peut-être toujours dans le cache de canaux hello. Après cela, le traitement du message échoue.  

**Solution de contournement**: certificat hello Bonjour projet BizTalk Service de mise à jour et redéployer le projet de hello.  

### <a name="bridges-continue-tooprocess-messages-even-when-hello-sql-database-is-offline"></a>Les ponts continuent tooprocess messages même lorsque la base de données SQL hello est hors connexion
ponts de BizTalk Services Hello continuent tooprocess messages pendant un certain temps, même si hello Microsoft Azure SQL Database (qui stocke hello en cours d’exécution des informations telles que des artefacts déployés et pipelines), est hors connexion. Il s’agit, car les Services BizTalk utilise les artefacts hello mis en cache et la configuration du pont.
Si vous ne souhaitez pas hello ponts tooprocess des messages lorsque hello SQL de base de données est hors connexion, vous pouvez utiliser toostop d’applets de commande PowerShell de Services BizTalk hello ou suspendre hello BizTalk Service. Consultez [exemple de gestion Azure BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=329019) pour les opérations de toomanage applets de commande hello Windows PowerShell.  

### <a name="reading-hello-xml-message-within-a-bridges-custom-code-component-includes-an-extra-bom-character"></a>Message XML de type hello lors de la lecture dans le composant de code personnalisé d’un pont inclut un caractère BOM supplémentaire
Envisagez un scénario où vous souhaitez tooread un message XML dans du code personnalisé d’un pont. Si vous utilisez hello .NET API System.Text.Encoding.UTF8.GetString(bytes) un caractère BOM supplémentaire est inclus dans la sortie hello au début de hello du message de type hello. Par conséquent, si vous ne souhaitez pas hello de hello sortie tooinclude les caractère BOM supplémentaire, vous devez utiliser ```System.IO.StreamReader().ReadToEnd()```.

### <a name="sending-messages-tooa-bridge-using-wcf-does-not-scale"></a>Envoi de messages pont tooa à l’aide de WCF n’évolue pas
Pont tooa à l’aide de WCF n’évolue pas les messages envoyés. Il est préférable d’utiliser HttpWebRequest si vous souhaitez un client évolutif.

### <a name="upgrade-token-provider-error-after-upgrading-from-biztalk-services-preview-toogeneral-availability-ga"></a>Mise à niveau : Erreur du fournisseur de jeton après la mise à niveau à partir de la version d’évaluation de BizTalk Services tooGeneral disponibilité (AG)
Il existe un accord EDI ou AS2 avec des lots actifs. Lorsque hello BizTalk Service est mis à niveau à partir de la version préliminaire tooGA, suivants de hello peut se produire :

* Erreur : le fournisseur de jetons hello a été impossible tooprovide un jeton de sécurité. Fournisseur de jetons a retourné le message : nom de hello distant n’a pas pu être résolu.
* Les tâches de traitement par lots sont annulées.

**Solution de contournement**: après hello BizTalk Service est mis à jour tooGeneral disponibilité (GA), redéployez l’accord de hello.  

### <a name="upgrade-toolbox-shows-hello-old-bridge-icons-after-upgrading-hello-biztalk-services-sdk"></a>Mise à niveau : Boîte à outils affiche hello anciennes icônes des ponts après la mise à niveau hello SDK des Services BizTalk
Une fois que vous mettez à niveau une version antérieure de hello BizTalk Services SDK, qui avait des anciennes icônes représentant des ponts de hello, boîte à outils hello continue tooshow hello anciennes icônes pour les ponts hello. Toutefois, si vous ajoutez une aire de Concepteur de projet de Service de tooBizTalk pont, surface de hello montre icône de nouveau hello.  

**Solution de contournement**. Vous pouvez contourner ce problème en supprimant les fichiers .tbd hello sous <system drive>: \Users\<utilisateur > \AppData\Local\Microsoft\VisualStudio\11.0.  

### <a name="upgrade-biztalk-portal-update-from-preview-tooga-might-show-an-error-indicating-that-hello-edi-capability-is-not-available"></a>Mise à niveau : Mise à jour du portail BizTalk à partir de la version préliminaire tooGA peut afficher une erreur indiquant que cette fonctionnalité EDI hello n’est pas disponible
Si vous êtes connecté en hello portail BizTalk Services pendant hello BizTalk Services est mise à niveau à partir de la version préliminaire tooGA, vous pouvez obtenir hello l’erreur suivante sur le portail hello :  

Cette fonctionnalité n’est pas disponible dans le cadre de cette édition des Services Microsoft Azure BizTalk. toouse ces fonctionnalités basculer l’édition appropriée de tooan.  

**Résolution**: se déconnecter du portail de hello, navigateur de hello close et open, puis connectez-vous hello portail.  

### <a name="upgrade-new-tracking-data-does-not-show-up-after-biztalk-services-is-upgraded-tooga"></a>Mise à niveau : Nouvelles données de suivi ne s’affiche pas une fois que les Services BizTalk est mis à niveau tooGA
Prenons un scénario où vous avez un pont XML déployé sur un abonnement BizTalk Services en version préliminaire. Envoyer des messages toohello pont et données de suivi correspondant hello sont disponibles sur hello portail BizTalk Services. Maintenant, si bits du runtime hello portail BizTalk Services et les Services BizTalk sont mis à niveau tooGA et que vous envoyez un toohello message même point de terminaison de pont déployé précédemment, hello des données de suivi ne s’affiche pas pour les messages envoyés après la mise à niveau.  

### <a name="pipelines-versus-bridges"></a>Pipelines et ponts
Dans ce document, le terme hello « pipeline » et « pont » est utilisés indifféremment. Les deux termes signifient pratiquement hello même chose, c'est-à-dire, une unité de traitement de message déployée sur BizTalk Services.  

### <a name="concepts"></a>Concepts
[BizTalk Services](https://msdn.microsoft.com/library/azure/hh689864.aspx)   

