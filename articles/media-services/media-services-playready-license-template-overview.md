---
title: "vue d’ensemble du modèle licence PlayReady de Services aaaMedia"
description: "Cette rubrique donne une vue d’ensemble d’un modèle de licence PlayReady utilisé tooconfigure des licences PlayReady."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="f4865-103">Présentation du modèle de licence PlayReady de Media Services</span><span class="sxs-lookup"><span data-stu-id="f4865-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="f4865-104">Azure Media Services fournit à présent un service pour la distribution de licences Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="f4865-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="f4865-105">Lorsque le lecteur hello utilisateur final (par exemple, Silverlight) essaie de tooplay votre PlayReady du contenu protégé, une demande est envoyée toohello licence remise service tooobtain une licence.</span><span class="sxs-lookup"><span data-stu-id="f4865-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="f4865-106">Si le service de licence hello approuve la demande de hello, il émet la licence hello qui est envoyé toohello client et peut être utilisé toodecrypt- and -play hello contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="f4865-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="f4865-107">Media Services propose également des API qui vous permettent de configurer vos licences PlayReady.</span><span class="sxs-lookup"><span data-stu-id="f4865-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="f4865-108">Les licences contiennent les droits hello et restrictions que vous souhaitez pour hello PlayReady DRM runtime tooenforce lorsqu’un utilisateur essaye tooplayback du contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="f4865-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="f4865-109">Voici quelques exemples des restrictions de licences PlayReady que vous pouvez spécifier :</span><span class="sxs-lookup"><span data-stu-id="f4865-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="f4865-110">la date et heure Hello à partir de quels hello licence est valide.</span><span class="sxs-lookup"><span data-stu-id="f4865-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="f4865-111">Hello valeur DateTime où hello licence expire.</span><span class="sxs-lookup"><span data-stu-id="f4865-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="f4865-112">Pour hello licence toobe est enregistré dans un stockage persistant sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="f4865-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="f4865-113">Les licences persistantes sont généralement utilisées tooallow lecture en mode hors connexion de contenu à hello.</span><span class="sxs-lookup"><span data-stu-id="f4865-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="f4865-114">niveau de sécurité minimales Hello qu’un lecteur doit avoir tooplay votre contenu.</span><span class="sxs-lookup"><span data-stu-id="f4865-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="f4865-115">niveau de protection pour les contrôles de sortie hello pour le contenu audio/vidéo de sortie Hello.</span><span class="sxs-lookup"><span data-stu-id="f4865-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="f4865-116">Pour plus d’informations, consultez les contrôles de sortie hello section hello en (3.5) [règles de conformité PlayReady](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="f4865-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="f4865-117">Actuellement, vous pouvez uniquement configurer hello droit de lecture de la licence PlayReady hello (ce droit est requis).</span><span class="sxs-lookup"><span data-stu-id="f4865-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="f4865-118">Hello droit de lecture permet à des clients de hello hello capacité tooplayback hello un contenu.</span><span class="sxs-lookup"><span data-stu-id="f4865-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="f4865-119">Hello droit de lecture permet également de configurer des restrictions des tooplayback spécifique.</span><span class="sxs-lookup"><span data-stu-id="f4865-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="f4865-120">Pour plus d'informations, consultez [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="f4865-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="f4865-121">tooconfigure des licences PlayReady avec Media Services, vous devez configurer le modèle de licence PlayReady de Media Services hello.</span><span class="sxs-lookup"><span data-stu-id="f4865-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="f4865-122">modèle de Hello est défini en XML.</span><span class="sxs-lookup"><span data-stu-id="f4865-122">hello template is defined in XML.</span></span>

<span data-ttu-id="f4865-123">Hello suivant montre modèle hello plus simple (et le plus courant) qui configure une licence de diffusion en continu de base.</span><span class="sxs-lookup"><span data-stu-id="f4865-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="f4865-124">Avec cette licence, vos clients seraient en mesure de tooplayback votre PlayReady du contenu protégé.</span><span class="sxs-lookup"><span data-stu-id="f4865-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="f4865-125">Hello XML est conforme à toohello modèle schéma XML licence PlayReady défini dans le modèle de licence PlayReady hello section du schéma XML.</span><span class="sxs-lookup"><span data-stu-id="f4865-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="f4865-126">Media Services définit également un ensemble de classes .NET qui peut être utilisé tooserialized et tooand désérialisé à partir de hello XML.</span><span class="sxs-lookup"><span data-stu-id="f4865-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="f4865-127">Pour obtenir une description des classes principales, consultez les [classes .NET de Media Services](media-services-playready-license-template-overview.md#classes)</span><span class="sxs-lookup"><span data-stu-id="f4865-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="f4865-128">qui sont des modèles de licence tooconfigure utilisé.</span><span class="sxs-lookup"><span data-stu-id="f4865-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="f4865-129">Pour obtenir un exemple de bout en bout qui utilise .NET des classes de modèle de licence PlayReady tooconfigure hello, consultez [à l’aide du chiffrement dynamique PlayReady et Service de remise de licence](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="f4865-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="f4865-130"><a id="classes"></a>Classes .NET de Media Services qui sont des modèles de licence utilisé tooconfigure</span><span class="sxs-lookup"><span data-stu-id="f4865-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="f4865-131">Hello Voici les classes .NET principales hello sont des modèles de licence PlayReady de Media Services tooconfigure utilisé.</span><span class="sxs-lookup"><span data-stu-id="f4865-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="f4865-132">Ces classes mappent les types toohello définis dans [schéma XML de modèle de licence PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="f4865-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="f4865-133">Hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) classe est utilisée tooserialize et désérialiser tooand à partir du modèle de licence Media Services hello XML.</span><span class="sxs-lookup"><span data-stu-id="f4865-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="f4865-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="f4865-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="f4865-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) -cette classe représente le modèle de hello pour la réponse de hello envoyées utilisateur toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="f4865-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="f4865-136">Il contient un champ pour une chaîne de données personnalisée entre serveur de licences hello et application hello (peut être utile pour la logique d’application personnalisée), ainsi qu’une liste d’un ou plusieurs modèles de licence.</span><span class="sxs-lookup"><span data-stu-id="f4865-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="f4865-137">Il s’agit de classe de « haut niveau » hello dans la hiérarchie de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="f4865-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="f4865-138">Ce qui signifie que modèle de réponse hello inclut une liste de modèles de licence et les modèles de licence hello incluent (directement ou indirectement) toutes hello d’autres classes qui composent toobe de données de modèle hello sérialisé.</span><span class="sxs-lookup"><span data-stu-id="f4865-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="f4865-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="f4865-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="f4865-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) -classe hello représente un modèle de licence pour la création de toobe de licences PlayReady retournée aux utilisateurs finaux de toohello.</span><span class="sxs-lookup"><span data-stu-id="f4865-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="f4865-141">Elle contient des données sur la clé de contenu hello dans la licence de hello hello et n’importe quel toobe droits ou restrictions appliquée par hello runtime DRM PlayReady lors de l’utilisation de clé de contenu hello.</span><span class="sxs-lookup"><span data-stu-id="f4865-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="f4865-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="f4865-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="f4865-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) -cette classe représente le droit de lecture d’une licence PlayReady de hello.</span><span class="sxs-lookup"><span data-stu-id="f4865-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="f4865-144">Il accorde hello utilisateur hello capacité tooplayback hello toohello de l’objet contenu zéro ou plus de restrictions configuré dans les licences de hello et hello droit de lecture lui-même (pour une stratégie spécifique de la lecture).</span><span class="sxs-lookup"><span data-stu-id="f4865-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="f4865-145">Une grande partie de la stratégie de hello sur hello droit de lecture a toodo avec des restrictions de sortie qui contrôlent les types hello des sorties peut jouer sur le contenu hello et les restrictions qui doivent être mises en place lors de l’utilisation d’une sortie donnée.</span><span class="sxs-lookup"><span data-stu-id="f4865-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="f4865-146">Par exemple, si hello restriction DigitalVideoOnlyContentRestriction est activée, puis hello runtime DRM autoriser uniquement les toobe vidéo hello affiché via des sorties numériques (sorties vidéo analogiques ne sont pas autorisés toopass le contenu hello).</span><span class="sxs-lookup"><span data-stu-id="f4865-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f4865-147">Ces types de restrictions peuvent être très puissants mais peuvent également affecter l’expérience du consommateur hello.</span><span class="sxs-lookup"><span data-stu-id="f4865-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="f4865-148">Si les protections de sortie hello sont configurées trop restrictive, le contenu hello peut être lu sur certains clients.</span><span class="sxs-lookup"><span data-stu-id="f4865-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="f4865-149">Pour plus d’informations, consultez hello [règles de conformité PlayReady](https://www.microsoft.com/playready/licensing/compliance/) document.</span><span class="sxs-lookup"><span data-stu-id="f4865-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="f4865-150">Pour obtenir un exemple des niveaux de protection que Silverlight prend charge, consultez [Protections de sortie prises en charge par Silverlight](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="f4865-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="f4865-151"><a id="schema"></a>Schéma XML de modèle de licence PlayReady</span><span class="sxs-lookup"><span data-stu-id="f4865-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="f4865-152">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="f4865-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="f4865-153">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="f4865-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

