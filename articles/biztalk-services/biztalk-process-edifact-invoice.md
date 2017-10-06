---
title: "Didacticiel : Traitement des factures EDIFACT à l’aide d’Azure BizTalk Services | Microsoft Docs"
description: "Comment toocreate et configurer l’application Connecteur de zone ou de l’API de hello et l’utiliser dans une application de logique dans Azure App Service"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>Didacticiel : Processus de facturation EDIFACT à l’aide des Services BizTalk Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Vous pouvez utiliser tooconfigure du portail BizTalk Services hello et déployer des accords X12 et EDIFACT. Dans ce didacticiel, nous examinons comment toocreate un accord EDIFACT pour l’échange de factures entre partenaires commerciaux. Ce didacticiel a été rédigé à partir d’une solution de bout en bout faisant intervenir deux partenaires commerciaux, Northwind et Contoso qui échangent des messages EDIFACT.  

## <a name="sample-based-on-this-tutorial"></a>Exemple basé sur ce didacticiel
Ce didacticiel est rédigé autour d’un exemple, **envoi EDIFACT factures à l’aide de BizTalk Services**, qui est toodownload disponible à partir de hello [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=401005). Vous utilisez l’exemple hello et parcourez a ce didacticiel toounderstand comment l’exemple hello a été créée. Vous pouvez également utiliser ce didacticiel toocreate votre propre solution spécialisé. Ce didacticiel est ciblé vers la deuxième approche de hello afin que vous compreniez comment cette solution a été créée. En outre, autant que possible, hello didacticiel est cohérent avec l’exemple hello et utilise hello les mêmes noms pour les artefacts (par exemple, schémas, transformations) que ceux utilisés dans l’exemple hello.  

> [!NOTE]
> Étant donné que cette solution implique l’envoi d’un message à partir d’un pont IAE que pont tooan EDI, il réutilise hello [BizTalk Services Bridge chaining exemple](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) exemple.  
> 
> 

## <a name="what-does-hello-solution-do"></a>Quelle est la solution de hello ?
Dans cette solution, Northwind reçoit des factures EDIFACT de la part de Contoso. Ces factures ne sont pas dans un format EDI standard. Par conséquent, avant d’envoyer hello facture tooNorthwind, il doit être document de facture (également appelé INVOIC) EDIFACT tooan transformé. À la réception, Northwind doit traiter la facture EDIFACT de hello et renvoyer un tooContoso de message (également appelé CONTRL) du contrôle.

![][1]  

tooachieve ce scénario commercial, Contoso utilise des fonctionnalités de hello fournies avec Microsoft Azure BizTalk Services.

* Contoso utilise EAI ponts tootransform hello d’origine facture tooEDIFACT INVOIC.
* pont IAE de Hello envoie ensuite hello tooan de message d’envoi EDI pont est déployé dans le cadre d’un accord configuré dans hello portail BizTalk Services.
* pont d’envoi EDI Hello traite hello EDIFACT INVOIC et l’achemine tooNorthwind.
* Après avoir reçu la facture de hello, Northwind renvoie un toohello de message CONTRL déployé dans le cadre de l’accord de hello de pont de réception EDI.  

> [!NOTE]
> Si vous le souhaitez, cette solution montre également comment toouse le traitement par lot toosend hello factures en lots, au lieu d’envoyer chaque facture séparément.  
> 
> 

scénario de hello toocomplete, nous utilisons des files d’attente Service Bus toosend de facture de Contoso tooNorthwind ou recevoir un accusé de réception de Northwind. Ces files d’attente peuvent être créés à l’aide d’une application cliente, qui est disponible en téléchargement et est incluse dans le package d’exemple hello qui est disponible dans le cadre de ce didacticiel.  

## <a name="prerequisites"></a>Composants requis
* Vous devez disposer d’un espace de noms Azure Service Bus. Pour obtenir des instructions sur la création d’un espace de noms, consultez [Création ou modification d’un espace de noms de service Service Bus](https://msdn.microsoft.com/library/azure/hh674478.aspx). Supposons que vous disposez déjà d’un espace de noms Service Bus configuré appelé **edifactbts**.
* Vous devez posséder un abonnement BizTalk Services. Pour obtenir des instructions, consultez la page [Création d’un service BizTalk à l’aide du portail Azure Classic](http://go.microsoft.com/fwlink/?LinkID=302280). Pour ce didacticiel, supposons que vous disposez d’un abonnement BizTalk Services, appelé **contosowabs**.
* Inscrire votre abonnement BizTalk Services hello portail BizTalk Services. Pour obtenir des instructions, consultez [l’inscription d’un déploiement de Service BizTalk sur hello portail BizTalk Services](https://msdn.microsoft.com/library/hh689837.aspx)
* Visual Studio doit être installé sur votre machine.
* Vous devez disposer du kit de développement logiciel BizTalk Services. Vous pouvez télécharger le SDK à partir de hello [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>Étape 1 : Créer hello files d’attente Service Bus
Cette solution utilise des messages de tooexchange de files d’attente Service Bus entre partenaires commerciaux. Contoso et Northwind envoient des messages toohello les files d’attente d’où les ponts IAE et/ou EDI hello les utiliser. Pour cette solution, vous avez besoin de trois files d’attente Service Bus :

* **northwindreceive** – Northwind reçoit la facture de hello de Contoso sur cette file d’attente.
* **ContosoReceive** : Contoso reçoit l’accusé de réception hello de Northwind sur cette file d’attente.
* **suspendu** – tous les messages interrompus sont routés toothis file. Les messages sont suspendus s’ils échouent en cours du traitement.

Vous pouvez créer ces files d’attente Service Bus à l’aide d’une application cliente incluse dans le package d’exemple hello.  

1. À partir de l’emplacement de hello où vous avez téléchargé l’exemple hello, ouvrez **didacticiel envoi de factures à l’aide de BizTalk Services EDI Bridges.sln**.
2. Appuyez sur **F5** toobuild et démarrer hello **Client de didacticiel** application.
3. Dans l’écran hello, entrez l’espace de noms Service Bus ACS hello, nom de l’émetteur et clé de l’émetteur.
   
   ![][2]  
4. Un message vous informe que trois files d’attente vont être créées dans votre espace de noms Service Bus. Cliquez sur **OK**.
5. Laissez hello Client de didacticiel en cours d’exécution. Ouvrez hello, cliquez sur **Service Bus** > ***votre espace de noms Service Bus*** > **les files d’attente**et vérifiez que les files d’attente hello trois ont été créées.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>Étape 2 : créer et déployer l’accord de partenariat commercial
Créez un accord de partenariat commercial entre Contoso et Northwind. Un accord de partenariat commercial définit un contrat commercial entre partenaires commerciaux hello deux, tels que le toouse de schéma de message, qui toouse de protocole, etc. de messagerie. Un accord de partenariat commercial comprend deux ponts EDI, une toosend des messages des partenaires de tootrading (appelée hello **pont d’envoi EDI**) et les messages un tooreceive des partenaires commerciaux (appelé hello **pont de réception EDI**).

Dans le contexte de hello de cette solution, pont d’envoi EDI hello correspond toohello côté envoi de l’accord de hello et est utilisé toosend hello une facture EDIFACT de Contoso tooNorthwind. De même, hello EDI pont de réception correspond toohello côté réception de l’accord de hello et est utilisé tooreceive les accusés de réception de Northwind.  

### <a name="create-hello-trading-partners"></a>Créer des partenaires commerciaux de hello
toostart, créer des partenaires commerciaux pour Contoso et Northwind.  

1. Bonjour portail BizTalk Services, sur hello **partenaires** , cliquez sur **ajouter**.
2. Dans la page Nouveau partenaire hello, entrez **Contoso** comme un nom de partenaire, puis cliquez sur **enregistrer**.
3. Répétez ces étapes hello étape toocreate hello deuxième partenaire, **Northwind**.  

### <a name="create-hello-agreement"></a>Créer l’accord de hello
Des accords de partenariat commercial sont créés entre les profils d’entreprise de partenaires commerciaux. Cette solution utilise des profils de partenaires hello par défaut sont automatiquement créés lorsque nous avons créé les partenaires hello.  

1. Bonjour portail BizTalk Services, cliquez sur **accords** > **ajouter**.
2. Dans hello du nouvel accord **paramètres généraux** page, spécifiez les valeurs de hello comme indiqué dans l’image hello ci-dessous, puis cliquez sur **continuer**.
   
   ![][3]  
   
   Après avoir cliqué sur **Continuer**, deux onglets, **Paramètres de réception** et **Paramètres d’envoi** deviennent disponibles.
3. Créer un accord d’envoi hello entre Contoso et Northwind. Cet accord détermine comment Contoso envoie tooNorthwind de facture EDIFACT hello.
   
   1. Cliquez sur **Paramètres d’envoi**.
   2. Conserver les valeurs par défaut de hello sur hello **URL entrante**, **transformer**, et **le traitement par lot** onglets.
   3. Sur hello **protocole** onglet, sous hello **schémas** section, télécharger hello **EFACT_D93A_INVOIC.xsd** schéma. Ce schéma est disponible avec le package d’exemple hello.
      
      ![][4]  
   4. Sur hello **Transport** onglet, spécifiez les détails de hello pour les files d’attente Service Bus de hello. Pour l’accord côté envoi de hello, nous utilisons hello **northwindreceive** tooNorthwind de facture EDIFACT toosend hello en file d’attente et hello **suspendu** de file d’attente tooroute tous les messages qui échouent pendant le traitement et sont suspendu. Vous avez créé ces files d’attente de **étape 1 : créer des files d’attente Service Bus hello** (dans cette rubrique).
      
      ![][5]  
      
      Sous **paramètres de Transport > type de Transport** et **paramètres de Suspension de Message > type de Transport**, sélectionnez le Bus des services Azure et de fournir les valeurs hello comme indiqué dans l’image de hello.
4. Créer hello accord entre Contoso et Northwind de réception. Cet accord détermine comment Contoso reçoit l’accusé de réception hello de Northwind.
   
   1. Cliquez sur **Paramètres de réception**.
   2. Conserver les valeurs par défaut de hello sur hello **Transport** et **transformer** onglets.
   3. Sur hello **protocole** onglet, sous hello **schémas** section, télécharger hello **EFACT_4.1_CONTRL.xsd** schéma. Ce schéma est disponible avec le package d’exemple hello.
   4. Sur hello **itinéraire** onglet, créer un filtre tooensure que seuls les accusés de réception de Northwind sont acheminé tooContoso. Sous **paramètres de routage**, cliquez sur **ajouter** toocreate hello filtre de routage.
      
      ![][6]  
      
      1. Fournir des valeurs pour **nom de la règle**, **règle de routage**, et **destination de routage** comme indiqué dans l’image de hello.
      2. Cliquez sur **Enregistrer**.
   5. Sur hello **itinéraire** onglet à nouveau, spécifiez où les accusés de réception suspendus (accusés qui échouent au cours du traitement) sont acheminés vers. La valeur de tooAzure de type hello transport Service Bus, router le type de destination trop**file d’attente**, l’authentification de type trop**Signature d’accès partagé** (SAS), spécifiez la chaîne de connexion de SAP de hello pour hello Service Bus espace de noms, puis entrez le nom de file d’attente hello en tant que **suspendu**.
5. Enfin, cliquez sur **déployer** accord de hello toodeploy. Points de terminaison hello Remarque où hello envoyer et recevoir des accords sont déployés.
   
   * Sur hello **paramètres d’envoi** sous l’onglet sous **URL entrante**, notez le point de terminaison hello. toosend un message à partir de tooNorthwind Contoso à l’aide de hello pont d’envoi EDI, vous devez envoyer un point de terminaison toothis message.
   * Sur hello **paramètres de réception** sous l’onglet sous **Transport**, notez le point de terminaison hello. pont de réception toosend un message à partir de tooContoso de Northwind à l’aide de hello EDI, vous devez envoyer un point de terminaison toothis message.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>Étape 3 : Créer et déployer le projet de Services BizTalk hello
Dans l’étape précédente de hello, vous avez déployé hello EDI envoyer et recevoir des accords tooprocess EDIFACT factures et des accusés de réception. Ces accords peuvent uniquement traiter les messages qui se conforment toohello schéma du message EDIFACT standard. Toutefois, par scénario hello pour cette solution, Contoso envoie une facture tooNorthwind dans un schéma propriétaire en interne. Par conséquent, avant que le message de type hello est envoyé toohello pont d’envoi EDI, il doit être transformé de schéma de facture EDIFACT standard hello schéma en interne toohello. projet de BizTalk Services EAI Hello offre cette possibilité.

projet BizTalk Services Hello **InvoiceProcessingBridge**, que les transformations hello message est également inclus dans le cadre de l’exemple hello que vous avez téléchargé. projet de Hello inclut hello suivant artefacts :

* **INHOUSEINVOICE. XSD** : schéma de facture en interne hello est envoyé à tooNorthwind.
* **EFACT_D93A_INVOIC. XSD** : schéma de facture EDIFACT standard de hello.
* **EFACT_4.1_CONTRL. XSD** – schéma d’accusé de réception EDIFACT hello que Northwind envoie tooContoso.
* **INHOUSEINVOICE_to_D93AINVOIC. TRFM** – hello transformation qui mappe le schéma de facture hello facture en interne schéma toohello standard EDIFACT.  

### <a name="create-hello-biztalk-services-project"></a>Créer le projet BizTalk Services de hello
1. Bonjour solution Visual Studio, développez le projet InvoiceProcessingBridge de hello et ouvrez hello **MessageFlowItinerary.bcs** fichier.
2. Cliquez n’importe où sur la zone de dessin hello et définir hello **URL de Service BizTalk** dans hello toospecify de zone de propriété, le nom de votre abonnement BizTalk Services. Par exemple, `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. À partir de la boîte à outils de hello, faites glisser un **pont unidirectionnel Xml** toohello la zone de dessin. Ensemble hello **nom de l’entité** et **adresse Relative** propriétés Hello pont trop**ProcessInvoiceBridge**. Double-cliquez sur **ProcessInvoiceBridge** surface de configuration de pont tooopen hello.
4. Au sein de hello **Types de messages** , cliquez sur hello signe plu (**+**) schéma de hello toospecify bouton de message entrants hello. Message entrant de hello pour hello pont IAE étant toujours facture en interne de hello, définissez cette trop**INHOUSEINVOICE**.
   
   ![][8]  
5. Cliquez sur hello **transformation Xml** forme et dans la zone de propriété hello, hello **cartes** propriété, cliquez sur les points de suspension hello (**...** ) bouton. Bonjour **sélection des mappages** boîte de dialogue, sélectionnez hello **INHOUSEINVOICE_to_D93AINVOIC** de transformer le fichier, puis cliquez sur **OK**.
   
   ![][9]  
6. Revenir en arrière trop**MessageFlowItinerary.bcs**, à partir de la boîte à outils de hello, faites glisser un **point de terminaison de Service externe bidirectionnel** toohello à droite de hello **ProcessInvoiceBridge**. Définir son **nom de l’entité** propriété trop**EDIBridge**.
7. Bonjour l’Explorateur de solutions, développez hello **MessageFlowItinerary.bcs** et double-cliquez sur hello **EDIBridge.config** fichier. Remplacez le contenu de hello hello **EDIBridge.config** avec les éléments suivants de hello.
   
   > [!NOTE]
   > Pourquoi dois-je le fichier .config de hello tooedit ? point de terminaison de service externe Hello que nous avons ajouté de zone de conception toohello pont représente les ponts EDI hello que nous avons déployés plus tôt. Les ponts EDI sont bidirectionnels et présentent un côté envoi et un côté réception. Toutefois, hello pont IAE que nous avons ajouté le Concepteur de pont toohello est un pont unidirectionnel. Par conséquent, modèles d’échange de messages différents hello toohandle des ponts de deux hello, nous utilisons un comportement de pont personnalisé en incluant sa configuration dans le fichier .config de hello. En outre, un comportement personnalisé hello gère également hello authentification toohello EDI envoi pont point de terminaison. Ce comportement personnalisé est disponible sous forme d’exemple distinct à [BizTalk Services Bridge chaining sample - EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104). Cette solution réutilise l’exemple hello.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Mettre à jour les détails de la configuration du fichier tooinclude de hello EDIBridge.config
   
   * Sous  *<behaviors>* , fournir hello espace de noms ACS et clé associés à hello abonnement BizTalk Services.
   * Sous  *<client>* , indiquez hello de point de terminaison où hello accord d’envoi EDI est déployé.
   
   Enregistrer les modifications et fermez le fichier de configuration hello.
9. À partir de hello boîte à outils, cliquez sur hello **connecteur** et jointure Bonjour **ProcessInvoiceBridge** et **EDIBridge** composants. Sélectionnez le connecteur de hello et dans la zone de propriétés, définissez **Condition de filtre** trop**Match All**. Cela garantit que tous les messages traités par hello pont IAE sont acheminés pont EDI de toohello.
   
   ![][10]  
10. Enregistrer les modifications toohello solution.  

### <a name="deploy-hello-project"></a>Déployer le projet de hello
1. Sur l’ordinateur hello où vous avez créé le projet de Services BizTalk hello, télécharger et installer le certificat SSL de hello pour votre abonnement aux Services de BizTalk. Depuis BizTalk Services, cliquez sur le **Tableau de bord**, puis cliquez sur **Télécharger le certificat SSL**. Double-cliquez sur le certificat de hello et suivez hello toocomplete invite hello installation. Assurez-vous que vous installez le certificat hello sous **autorités de Certification racines de confiance** magasin de certificats.
2. Dans l’Explorateur de solutions Visual Studio, avec le bouton droit hello **InvoiceProcessingBridge** de projet, puis cliquez sur **déployer**.
3. Fournir des valeurs de hello comme indiqué dans l’image de hello, puis cliquez sur **déployer**. Vous pouvez obtenir des informations d’identification hello ACS pour les Services BizTalk en cliquant sur **les informations de connexion** à partir du tableau de bord hello BizTalk Services.
   
   ![][11]  
   
   À partir du volet de sortie hello, copiez le point de terminaison hello où hello pont IAE est déployé, par exemple, `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`. Vous aurez besoin de cette URL de point de terminaison ultérieurement.  

## <a name="step-4-test-hello-solution"></a>Étape 4 : Tester la solution de hello
Dans cette rubrique, nous expliquons comment tootest hello solution à l’aide de hello **Client de didacticiel** application fournie dans le cadre de l’exemple hello.  

1. Dans Visual Studio, appuyez sur F5 toostart hello **Client de didacticiel**.
2. écran Hello doit avoir des valeurs hello préremplis à partir de l’étape de hello où nous avons créé hello files d’attente Service Bus. Cliquez sur **Suivant**.
3. Dans la prochaine fenêtre de hello, fournissez les informations d’identification de l’ACS pour l’abonnement de Services BizTalk et hello des points de terminaison où EAI et EDI (réception) sont déployés les ponts.
   
   Vous avez copié le point de terminaison de pont hello IAE à l’étape précédente de hello. Pour le point de terminaison de pont de réception EDI Bonjour portail BizTalk Services, accédez à toohello accord > Paramètres de réception > Transport > point de terminaison.
   
   ![][12]  
4. Dans la fenêtre suivante de hello, sous Contoso, cliquez sur hello **envoyer la facture en interne** bouton. Bonjour fichier ouvrir la boîte de dialogue, ouvrez le fichier INHOUSEINVOICE.txt de hello. Examinez le contenu du fichier de hello hello, puis cliquez sur **OK** facture de hello toosend.
   
   ![][13]  
5. Dans quelques hello de secondes, celle-ci est reçue par Northwind. Cliquez sur hello **afficher le Message** lien toosee hello perçues par Northwind. Notez comment la facture hello reçue par Northwind est dans un schéma EDIFACT standard lors de hello celle envoyée par Contoso était un schéma en interne.
   
   ![][14]  
6. Sélectionnez la facture de hello, puis cliquez **envoyer un accusé de réception**. Dans la boîte de dialogue hello qui s’affiche, Notez cet échange hello QU'ID est identique sur hello reçu facture hello accusé de réception et envoi. Cliquez sur OK dans hello **envoyer un accusé de réception** boîte de dialogue.
   
   ![][15]  
7. En quelques secondes, accusé de réception hello est reçu par Contoso.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>Étape 5 (facultatif) : envoyer la facture EDIFACT en lots
Les ponts EDI BizTalk Services prennent également en charge le traitement par lots des messages sortants. Cette fonctionnalité est utile pour les partenaires destinataires qui préfèrent tooreceive un lot de messages (respectant certains critères) au lieu de messages individuels.

Hello plus important lorsque vous travaillez avec des lots est version hello du lot hello, également appelé critères de déclenchement hello. critères de déclenchement Hello peuvent reposer sur comment partenaire destinataire de hello veut tooreceive messages. Si le traitement par lots est activé, hello pont EDI n’envoie pas hello toohello de message sortant réception partenaire jusqu'à ce que hello critères de déclenchement est remplie. Par exemple, un critère de traitement par lot basé sur la taille des messages distribue un lot uniquement lorsque « n » messages sont regroupés. Un critère de traitement par lots peut également être basé sur le temps, et faire en sorte qu’un lot soit envoyé à heure fixe chaque jour. Dans cette solution, nous nous efforçons de critère basé sur la taille des messages hello.

1. Bonjour portail BizTalk Services, cliquez sur accord hello que vous avez créé précédemment. Cliquez sur Paramètres d’envoi > Traitement par lot > Ajouter un lot.
2. Comme nom de lot, saisissez **InvoiceBatch**, fournissez une description, puis cliquez sur **Suivant**.
3. Spécifiez des critères de lancement de lots qui définissent les messages devant être regroupés dans lots. Dans cette solution, nous allons regrouper les messages par lot. Par conséquent, sélectionnez hello, utilisez les options définitions avancées, puis entrez **1 = 1**. Il s’agit d’une condition qui conservera toujours la valeur true, et par conséquent, tous les messages seront traités par lot. Cliquez sur **Suivant**.
   
   ![][17]  
4. Spécifiez un critère de lancement par lot. À partir de hello liste déroulante, sélectionnez **MessageCountBased**et pour **nombre**, spécifiez **3**. Cela signifie qu’un lot de trois messages sera envoyé tooNorthwind. Cliquez sur **Suivant**.
   
   ![][18]  
5. Passez en revue le résumé de hello et puis cliquez sur **enregistrer**. Cliquez sur **déployer** accord de hello tooredeploy.
6. Revenir en arrière toohello **Client de didacticiel**, cliquez sur **envoyer la facture en interne**, suivez hello invites toosend hello facture. Vous remarquerez qu’aucune facture n’est reçue par Northwind, car la taille de lot hello n’est pas remplie. Répétez cette étape deux fois de plus, afin que vous avez trois messages de facture envoyés tooNorthwind. Cela satisfait hello critères de déclenchement du lot de 3 messages et vous devez maintenant voir une facture à Northwind.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

