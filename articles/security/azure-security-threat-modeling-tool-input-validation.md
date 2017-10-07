---
title: "aaaInput Validation - outil de modélisation des menaces Microsoft - Azure | Documents Microsoft"
description: "mesures d’atténuation des menaces exposé Bonjour outil de modélisation des menaces"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 823503881f4bae292ef021834d5e64acf2a0f54a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-input-validation--mitigations"></a>Infrastructure de sécurité : validation des entrées | Mesures de correction 
| Produit/Service | Article |
| --------------- | ------- |
| **Application web** | <ul><li>[Désactiver les scripts XSLT pour toutes les transformations à l’aide de feuilles de style non approuvées](#disable-xslt)</li><li>[S’assurer que chaque page susceptible de comporter du contenu contrôlable par l’utilisateur refuse la détection MIME automatique](#out-sniffing)</li><li>[Renforcer ou désactiver la résolution d’entité XML](#xml-resolution)</li><li>[Les applications utilisant http.sys doivent procéder à la vérification de la canonisation des URL](#app-verification)</li><li>[S’assurer que les contrôles appropriés sont en place lors de l’acceptation de fichiers provenant d’utilisateurs](#controls-users)</li><li>[S’assurer que des paramètres de type sécurisé sont utilisés dans une application web pour l’accès aux données](#typesafe)</li><li>[Utilisez les classes de liaison de modèle distinct ou une vulnérabilité de tooprevent MVC attribution en masse de listes de filtres de liaison](#binding-mvc)</li><li>[Encoder toorendering préalable de sortie web non fiable](#rendering)</li><li>[Procéder à la validation et au filtrage des entrées sur les propriétés de modèle de tous types de chaînes](#typemodel)</li><li>[Les champs de formulaire acceptant tous les caractères, par exemple dans un éditeur de texte enrichi, doivent être nettoyés](#richtext)</li><li>[N’affectez pas toosinks d’éléments DOM qui n’ont pas de codage intégrés](#inbuilt-encode)</li><li>[Valider toutes les redirections au sein de l’application hello sont fermées ou terminées en toute sécurité](#redirect-safe)</li><li>[Implémenter la validation des entrées sur tous les paramètres de type de chaîne acceptés par les méthodes de contrôleur](#string-method)</li><li>[Définir le délai d’expiration de la limite supérieure pour le traitement DoS tooprevent en raison des expressions régulières toobad d’expressions régulières](#dos-expression)</li><li>[Éviter l’utilisation de Html.Raw dans les vues Razor](#html-razor)</li></ul> | 
| **Base de données** | <ul><li>[Ne pas utiliser les requêtes dynamiques dans les procédures stockées](#stored-proc)</li></ul> |
| **API Web** | <ul><li>[S’assurer que la validation du modèle est effectuée sur les méthodes d’API Web](#validation-api)</li><li>[Implémenter la validation des entrées sur tous les paramètres de type de chaîne acceptés par les méthodes d’API Web](#string-api)</li><li>[S’assurer que les paramètres de type sécurisé sont utilisés dans une API Web pour l’accès aux données](#typesafe-api)</li></ul> | 
| **Azure Document DB** | <ul><li>[Utiliser des requêtes SQL paramétrables pour DocumentDB](#sql-docdb)</li></ul> | 
| **WCF** | <ul><li>[Validation des entrées WCF par le biais de la liaison de schéma](#schema-binding)</li><li>[WCF - Validation des entrées par le biais des inspecteurs de paramètres](#parameters)</li></ul> |

## <a id="disable-xslt"></a>Désactiver les scripts XSLT pour toutes les transformations à l’aide de feuilles de style non approuvées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Sécurité XSLT](https://msdn.microsoft.com/library/ms763800(v=vs.85).aspx), [Propriété XsltSettings.EnableScript](http://msdn.microsoft.com/library/system.xml.xsl.xsltsettings.enablescript.aspx) |
| **Étapes** | XSLT prend en charge l’écriture de scripts à l’intérieur des feuilles de style à l’aide de hello `<msxml:script>` élément. Cela permet de toobe des fonctions personnalisées utilisée dans une transformation XSLT. Hello est exécuté sous le contexte de hello du processus de hello hello transformation. Script XSLT doit être désactivé dans une exécution de tooprevent d’environnement non fiable de code non fiable. *Si vous utilisez .NET :* script XSLT est désactivé par défaut ; Toutefois, vous devez vous assurer qu’elle n'a pas été explicitement activée via hello `XsltSettings.EnableScript` propriété.|

### <a name="example"></a>Exemple 

```C#
XsltSettings settings = new XsltSettings();
settings.EnableScript = true; // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Exemple
Si vous n’utilisez pas l’utilisation de MSXML 6.0, le script XSLT est désactivé par défaut. Toutefois, vous devez vous assurer qu’elle n'a pas été explicitement activée via la propriété de l’objet DOM XML hello AllowXsltScript. 

```C#
doc.setProperty("AllowXsltScript", true); // WRONG: THIS SHOULD BE SET toofalse
```

### <a name="example"></a>Exemple
Si vous utilisez MSXML 5 ou une version antérieure, les scripts XSLT sont activés par défaut et vous devez les désactiver explicitement. Définissez hello DOM XML objet propriété AllowXsltScript toofalse. 

```C#
doc.setProperty("AllowXsltScript", false); // CORRECT. Setting toofalse disables XSLT scripting.
```

## <a id="out-sniffing"></a>S’assurer que chaque page susceptible de comporter du contenu contrôlable par l’utilisateur refuse la détection MIME automatique

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [IE8 Security Part V - Comprehensive Protection (Sécurité IE8 Partie V - Protection complète)](http://blogs.msdn.com/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx)  |
| **Étapes** | <p>Pour chaque page peut contenir du contenu contrôlable par l’utilisateur, vous devez utiliser hello en-tête HTTP `X-Content-Type-Options:nosniff`. toocomply à cette exigence, vous pouvez soit hello requis en-tête de page par page pour que les pages qui peuvent contenir des informations contrôlable à l’utilisateur, ou définies globalement pour toutes les pages de l’application hello.</p><p>Chaque type de fichier provenant d’un serveur web est associé à un [type MIME](http://en.wikipedia.org/wiki/Mime_type) (également appelé un *type de contenu*) qui décrit la nature hello du contenu hello (autrement dit, image, texte, application, etc.)</p><p>en-tête de Hello X-contenu-Type-Options est un en-tête HTTP qui permet aux développeurs toospecify que leur contenu ne doit pas être détectées de MIME. Cet en-tête est conçue toomitigate détection MIME sur les attaques. La prise en charge de cet en-tête a été ajoutée dans Internet Explorer 8 (IE8).</p><p>Seuls les utilisateurs d’Internet Explorer 8 (IE8) bénéficient de l’en-tête X-Content-Type-Options. Les versions antérieures d’Internet Explorer ne respectent pas actuellement l’en-tête X-contenu-Type-Options de hello</p><p>Internet Explorer 8 (et versions ultérieur) sont hello uniquement les fonctionnalités d’annulations principaux navigateurs tooimplement une détection MIME. Si et quand les autres principaux navigateurs (Firefox, Safari, Chrome) implémentent des fonctionnalités similaires, cette recommandation sera syntaxe tooinclude mis à jour pour ces navigateurs aussi</p>|

### <a name="example"></a>Exemple
en-tête requis du hello tooenable globalement pour toutes les pages de l’application hello, vous pouvez effectuer hello suivantes : 

* Ajouter l’en-tête de hello dans le fichier web.config de hello si l’application hello est hébergée par Internet Information Services (IIS) 7 

```
<system.webServer> 
  <httpProtocol> 
    <customHeaders> 
      <add name=""X-Content-Type-Options"" value=""nosniff""/>
    </customHeaders>
  </httpProtocol>
</system.webServer> 
```

* Ajouter un en-tête hello via hello Application globale\_BeginRequest 

``` 
void Application_BeginRequest(object sender, EventArgs e)
{
  this.Response.Headers[""X-Content-Type-Options""] = ""nosniff"";
} 
```

* Implémentez le module HTTP personnalisé 

``` 
public class XContentTypeOptionsModule : IHttpModule 
  {
    #region IHttpModule Members 
    public void Dispose() 
    { 

    } 
    public void Init(HttpApplication context)
    { 
      context.PreSendRequestHeaders += newEventHandler(context_PreSendRequestHeaders); 
    } 
    #endregion 
    void context_PreSendRequestHeaders(object sender, EventArgs e) 
      { 
        HttpApplication application = sender as HttpApplication; 
        if (application == null) 
          return; 
        if (application.Response.Headers[""X-Content-Type-Options ""] != null) 
          return; 
        application.Response.Headers.Add(""X-Content-Type-Options "", ""nosniff""); 
      } 
  } 

``` 

* Vous pouvez activer l’en-tête requis de hello uniquement pour les pages spécifiques en ajoutant des réponses de tooindividual : 

```
this.Response.Headers[""X-Content-Type-Options""] = ""nosniff""; 
``` 

## <a id="xml-resolution"></a>Renforcer ou désactiver la résolution d’entité XML

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [XML Entity Expansion (Extension d’entité XML)](http://capec.mitre.org/data/definitions/197.html), [Attaques par déni de service XML et moyens de défense](http://msdn.microsoft.com/magazine/ee335713.aspx), [Vue d’ensemble de la sécurité MSXML](http://msdn.microsoft.com/library/ms754611(v=VS.85).aspx), [Meilleures pratiques pour la sécurisation du Code MSXML](http://msdn.microsoft.com/library/ms759188(VS.85).aspx), [Référence de protocole NSXMLParserDelegate](http://developer.apple.com/library/ios/#documentation/cocoa/reference/NSXMLParserDelegate_Protocol/Reference/Reference.html), [Résolution des ressources externes](https://msdn.microsoft.com/library/5fcwybb2.aspx) |
| **Étapes**| <p>Bien qu’il n’est pas largement utilisé, il existe une fonctionnalité de XML qui permet des entités de macro hello XML parser tooexpand avec les valeurs définies dans le document hello lui-même ou à partir de sources externes. Par exemple, les documents hello peuvent définir une entité « companyname » avec la valeur de hello « Microsoft », afin que chaque fois hello texte «&companyname;» s’affiche dans le document de hello, il est automatiquement remplacé par le texte hello Microsoft. Ou bien, le document de hello peut définir une entité « MSFTStock » qui fait référence à une web externe service toofetch hello valeur actuelle du stock de Microsoft.</p><p>Puis à tout moment «&MSFTStock;» s’affiche dans le document de hello, il est automatiquement remplacé par hello cours. Toutefois, cette fonctionnalité peut être outrepassés toocreate des attaques de déni de service (DoS). Une personne malveillante peut imbriquer plusieurs entités toocreate une limite d’expansion exponentielle XML qui consomme toute la mémoire disponible sur le système de hello. </p><p>Ou bien, il peut créer une référence externe qui diffuse en continu différée une quantité infinie de données ou qui se simplement bloque le thread de hello. Par conséquent, toutes les équipes doivent désactiver la résolution d’entité XML interne ou externe entièrement si leur application ne pas utiliser, ou manuellement limiter hello de mémoire et l’heure auxquelles l’application hello peut consommer pour la résolution d’entité, si cette fonctionnalité est C’est absolument nécessaire. Si la résolution d’entité n’est pas requise par votre application, désactivez-la. </p>|

### <a name="example"></a>Exemple
Pour le code .NET Framework, vous pouvez utiliser hello méthodes suivantes :

```C#
XmlTextReader reader = new XmlTextReader(stream);
reader.ProhibitDtd = true;

XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);

// for .NET 4
XmlReaderSettings settings = new XmlReaderSettings();
settings.DtdProcessing = DtdProcessing.Prohibit;
XmlReader reader = XmlReader.Create(stream, settings);
```
Notez cette valeur par défaut hello `ProhibitDtd` dans `XmlReaderSettings` est true, mais dans `XmlTextReader` a la valeur false. Si vous utilisez XmlReaderSettings, vous n’avez pas besoin tooset ProhibitDtd tootrue explicitement, mais il est recommandé pour des raisons de sécurité que vous effectuez. Notez que hello classe XmlDocument permet également la résolution d’entité par défaut. 

### <a name="example"></a>Exemple
résolution d’entité toodisable pour XmlDocument, utilisez hello `XmlDocument.Load(XmlReader)` surcharge de hello Load (méthode) et définissez hello propriétés appropriées dans la résolution de toodisable XmlReader argument hello, comme illustré dans hello suivant de code : 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = true;
XmlReader reader = XmlReader.Create(stream, settings);
XmlDocument doc = new XmlDocument();
doc.Load(reader);
```

### <a name="example"></a>Exemple
Si la désactivation de la résolution d’entité n’est pas possible pour votre application, valeur hello XmlReaderSettings.MaxCharactersFromEntities propriété tooa raisonnable en fonction des besoins de l’application tooyour. Cela limite impact hello d’attaques de déni de service potentielles exponentielle d’extension. Hello suivant code fournit un exemple de cette approche : 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
XmlReader reader = XmlReader.Create(stream, settings);
```

### <a name="example"></a>Exemple
Si vous devez tooresolve inline entités mais que vous n’avez pas besoin de tooresolve des entités externes, définissez hello XmlReaderSettings.XmlResolver propriété toonull. Par exemple : 

```C#
XmlReaderSettings settings = new XmlReaderSettings();
settings.ProhibitDtd = false;
settings.MaxCharactersFromEntities = 1000;
settings.XmlResolver = null;
XmlReader reader = XmlReader.Create(stream, settings);
```
Notez que dans MSXML6, ProhibitDTD a la valeur tootrue (désactiver le traitement des DTD) par défaut. Pour le code Apple OSX/iOS, vous pouvez utiliser deux analyseurs XML : NSXMLParser et libXML2. 

## <a id="app-verification"></a>Les applications utilisant http.sys doivent procéder à la vérification de la canonisation des URL

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Toutes les applications utilisant http.sys doivent suivre ces instructions :</p><ul><li>Limitez hello URL longueur toono plus de 16 384 caractères (Unicode ou ASCII). Il s’agit de hello absolue longueur maximale des URL basée sur la configuration d’Internet Information Services (IIS) 6 hello par défaut. Les sites web doivent, dans la mesure du possible, proposer une longueur inférieure</li><li>Utiliser des classes de fichier d’e/s de .NET Framework standards hello (par exemple, FileStream) comme ces tirera parti d’hello règles de canonisation Bonjour .NET FX</li><li>Créez explicitement une liste verte des noms de fichiers connus</li><li>Refusez explicitement les types de fichiers connus qui ne vous serviront pas et qu’UrlScan refuse : exe, bat, cmd, com, htw, ida, idq, htr, idc, shtm[l], stm, printer, ini, pol et dat</li><li>Intercepter hello suivant des exceptions :<ul><li>System.ArgumentException (pour les noms d’appareils)</li><li>System.NotSupportedException (pour les flux de données)</li><li>System.IO.FileNotFoundException (pour les noms de fichiers avec séquence d’échappement non valide)</li><li>System.IO.FileNotFoundException (pour les noms de répertoires avec séquence d’échappement non valide)</li></ul></li><li>*Ne le faites pas* appeler tooWin32 fichier I/O APIs. Sur une URL non valide normalement retourner une 400 erreur toohello et journaux d’erreur réelle de hello.</li></ul>|

## <a id="controls-users"></a>S’assurer que les contrôles appropriés sont en place lors de l’acceptation de fichiers provenant d’utilisateurs

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Unrestricted File Upload (Chargement de fichiers sans restriction)](https://www.owasp.org/index.php/Unrestricted_File_Upload), [File Signature Table (Table de signatures de fichier)](http://www.garykessler.net/library/file_sigs.html) |
| **Étapes** | <p>Les fichiers téléchargés représentent une risque tooapplications.</p><p>Hello première étape de nombreuses attaques est tooget certaines toobe de système de code toohello une attaque. Attaque de hello doit ensuite uniquement toofind un façon, le code hello tooget exécuté. Chargement d’un fichier aide les intrus hello accomplir la première étape de hello. conséquences Hello de téléchargement du fichier illimitée peuvent varier, notamment la prise en charge complète du système, un système de fichiers surchargée ou de la base de données, systèmes tooback attaques et dégradation simple de transfert.</p><p>Il varie selon quelle application hello fait avec les fichiers hello téléchargé et en particulier où il est stocké. Il manque la validation des téléchargements de fichiers côté serveur. Le suivi des contrôles de sécurité doit être implémenté pour la fonctionnalité de téléchargement de fichiers :</p><ul><li>Vérification de l’extension du fichier (seul un ensemble valide de types de fichiers autorisés doit être accepté)</li><li>Taille maximale du fichier</li><li>Fichier ne doit pas être téléchargée toowebroot ; emplacement de Hello doit être un répertoire sur un lecteur non système</li><li>Convention d’affectation de noms doit être suivie, telles que hello nom du fichier téléchargé avoir certains aléatoire, donc en tant que tooprevent remplace les fichiers</li><li>Fichiers doivent être analysés pour la protection antivirus avant d’écrire toohello disque</li><li>Vous assurer que le nom de fichier hello et d’autres métadonnées (par exemple, chemin d’accès de fichier) sont validées pour des caractères nuisibles</li><li>Signature de format de fichier doit être vérifiée, tooprevent un utilisateur de télécharger un fichier masquée (par exemple, en téléchargeant un fichier exe en modifiant l’extension tootxt)</li></ul>| 

### <a name="example"></a>Exemple
Pour hello dernier point concernant la validation de signature de format de fichier, consultez la classe toohello ci-dessous pour plus d’informations : 

```C#
        private static Dictionary<string, List<byte[]>> fileSignature = new Dictionary<string, List<byte[]>>
                    {
                    { ".DOC", new List<byte[]> { new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 } } },
                    { ".DOCX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".PDF", new List<byte[]> { new byte[] { 0x25, 0x50, 0x44, 0x46 } } },
                    { ".ZIP", new List<byte[]> 
                                            {
                                              new byte[] { 0x50, 0x4B, 0x03, 0x04 },
                                              new byte[] { 0x50, 0x4B, 0x4C, 0x49, 0x54, 0x55 },
                                              new byte[] { 0x50, 0x4B, 0x53, 0x70, 0x58 },
                                              new byte[] { 0x50, 0x4B, 0x05, 0x06 },
                                              new byte[] { 0x50, 0x4B, 0x07, 0x08 },
                                              new byte[] { 0x57, 0x69, 0x6E, 0x5A, 0x69, 0x70 }
                                                }
                                            },
                    { ".PNG", new List<byte[]> { new byte[] { 0x89, 0x50, 0x4E, 0x47, 0x0D, 0x0A, 0x1A, 0x0A } } },
                    { ".JPG", new List<byte[]>
                                    {
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE1 },
                                              new byte[] { 0xFF, 0xD8, 0xFF, 0xE8 }
                                    }
                                    },
                    { ".JPEG", new List<byte[]>
                                        { 
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE0 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE2 },
                                            new byte[] { 0xFF, 0xD8, 0xFF, 0xE3 }
                                        }
                                        },
                    { ".XLS", new List<byte[]>
                                            {
                                              new byte[] { 0xD0, 0xCF, 0x11, 0xE0, 0xA1, 0xB1, 0x1A, 0xE1 },
                                              new byte[] { 0x09, 0x08, 0x10, 0x00, 0x00, 0x06, 0x05, 0x00 },
                                              new byte[] { 0xFD, 0xFF, 0xFF, 0xFF }
                                            }
                                            },
                    { ".XLSX", new List<byte[]> { new byte[] { 0x50, 0x4B, 0x03, 0x04 } } },
                    { ".GIF", new List<byte[]> { new byte[] { 0x47, 0x49, 0x46, 0x38 } } }
                };

        public static bool IsValidFileExtension(string fileName, byte[] fileData, byte[] allowedChars)
        {
            if (string.IsNullOrEmpty(fileName) || fileData == null || fileData.Length == 0)
            {
                return false;
            }

            bool flag = false;
            string ext = Path.GetExtension(fileName);
            if (string.IsNullOrEmpty(ext))
            {
                return false;
            }

            ext = ext.ToUpperInvariant();

            if (ext.Equals(".TXT") || ext.Equals(".CSV") || ext.Equals(".PRN"))
            {
                foreach (byte b in fileData)
                {
                    if (b > 0x7F)
                    {
                        if (allowedChars != null)
                        {
                            if (!allowedChars.Contains(b))
                            {
                                return false;
                            }
                        }
                        else
                        {
                            return false;
                        }
                    }
                }

                return true;
            }

            if (!fileSignature.ContainsKey(ext))
            {
                return true;
            }

            List<byte[]> sig = fileSignature[ext];
            foreach (byte[] b in sig)
            {
                var curFileSig = new byte[b.Length];
                Array.Copy(fileData, curFileSig, b.Length);
                if (curFileSig.SequenceEqual(b))
                {
                    flag = true;
                    break;
                }
            }

            return flag;
        }
```

## <a id="typesafe"></a>S’assurer que des paramètres de type sécurisé sont utilisés dans une application web pour l’accès aux données

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Si vous utilisez la collection de paramètres hello, SQL traite hello entrée est comme une valeur littérale et non en tant que code exécutable. collection de paramètres de Hello peut être tooenforce utilisé les contraintes de type et la longueur des données d’entrée. Les valeurs en dehors de la plage de hello déclenchent une exception. Si les paramètres SQL de type sécurisé ne sont pas utilisés, des personnes malveillantes peuvent être en mesure de tooexecute les attaques par injection sont incorporés dans l’entrée de hello non filtré.</p><p>Utiliser les paramètres de type sécurisé lors de la construction SQL interroge tooavoid possibles attaques par injection SQL qui peuvent se produire avec des entrées non filtrées. Vous pouvez utiliser des paramètres de type sécurisé avec des procédures stockées et des instructions SQL dynamiques. Les paramètres sont traités comme des valeurs littérales par base de données hello et non en tant que code exécutable. Le type et la longueur sont également vérifiés pour les paramètres.</p>|

### <a name="example"></a>Exemple 
Hello de code suivant montre comment toouse paramètres de type sécurisés avec hello SqlParameterCollection lors de l’appel d’une procédure stockée. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Bonjour précédant l’exemple de code, la valeur d’entrée de hello ne peut pas être supérieure à 11 caractères. Si les données de salutation n’est pas conforme toohello type ou la longueur définie par le paramètre hello, hello SqlParameter, classe lève une exception. 

## <a id="binding-mvc"></a>Utilisez les classes de liaison de modèle distinct ou une vulnérabilité de tooprevent MVC attribution en masse de listes de filtres de liaison

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Les attributs de métadonnées](http://msdn.microsoft.com/library/system.componentmodel.dataannotations.metadatatypeattribute), [Public clé sécurité vulnérabilité et atténuation](https://github.com/blog/1068-public-key-security-vulnerability-and-mitigation), [Guide complet tooMass affectation dans ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2012/03/11/complete-guide-to-mass-assignment-in-asp-net-mvc.aspx), [prise en main d’EF à l’aide de MVC](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application#overpost) |
| **Étapes** | <ul><li>**Quand dois-je rechercher les vulnérabilités de survalidation ? -** Les vulnérabilités de survalidation peuvent se produire partout où vous liez des classes de modèle à partir d’entrées utilisateur. Les infrastructures telles que MVC peuvent représenter des données utilisateur dans des classes .NET personnalisées, y compris les objets CLR traditionnels (OCT). MVC remplit automatiquement ces classes de modèle avec des données à partir de la demande de hello, fournissant une représentation pratique pour traiter les entrées d’utilisateur. Lorsque ces classes incluent des propriétés qui ne doivent pas être définies par l’utilisateur de hello, application hello peut être vulnérable attaques tooover-validation, qui permettent le contrôle utilisateur de données application hello jamais prévue. Comme la liaison du modèle MVC, les technologies d’accès de base de données tels que les mappeurs objet/relationnel comme Entity Framework souvent également prend en charge POCO objets toorepresent base de données. Ces classes de modèle de données fournissent hello même simplifier la gestion des données de base de données comme MVC dans le traitement des entrées d’utilisateur. Étant donné que MVC et hello de base de données prend en charge des modèles similaires, telles que les objets POCO, il semble hello tooreuse facile même des classes pour les deux fonctions. Cette échoue pratique toopreserve la séparation des problèmes et il est fréquemment où des propriétés sont exposées toomodel liaison, l’activation des attaques de validation excessive.</li><li>**Pourquoi ne dois-je pas utiliser mes classes de modèle de base de données non filtrées en tant qu’actions de MVC toomy paramètres ? -** Liaison de modèle MVC car rien liera dans cette classe. Même si hello données n’apparaissent pas dans votre affichage, qu'un utilisateur malveillant peut envoyer une demande HTTP avec ces données incluses et MVC prêts liera il car votre action indique que la classe de base de données est de forme hello des données, il doit accepter pour l’entrée d’utilisateur.</li><li>**Pourquoi devez-vous vous soucier forme hello utilisé pour la liaison de modèle ? -** Liaison de modèle à l’aide de ASP.NET MVC avec des modèles trop larges expose un attaques de validation tooover d’application. Validation excessive pourrait permettre des données d’application des personnes malveillantes toochange au-delà de ce que développeur hello destiné, telles que la substitution de prix hello pour un élément ou hello des privilèges de sécurité d’un compte. Applications doivent utiliser tooprovide de modèles (ou les listes de filtres de propriétés autorisés spécifique) de liaison spécifiques à certaines actions un contrat explicite pour le tooallow d’entrée non approuvé via la liaison de modèle.</li><li>**Le fait de disposer de modèles de liaison distincts équivaut-il simplement à une duplication de code ? -** Non, c’est une question de séparation des intérêts. Si vous réutilisez les modèles de base de données dans les méthodes d’action, vous dites toute propriété (ou la sous-propriété) qu’une classe peut être définie par l’utilisateur hello dans une requête HTTP. Si ce n’est pas ce que vous voulez toodo MVC, vous devez une liste de filtres ou un tooshow de forme classe distincte MVC, les données peuvent provenir d’utilisateur d’entrée à la place.</li><li>**Si j’utilise des modèles de liaison distincte pour l’entrée d’utilisateur, dois-je tooduplicate tous les attributs d’annotations mes données ? -** N’est pas nécessairement. Vous pouvez utiliser MetadataTypeAttribute sur hello de base de données classe toolink toohello métadonnées du modèle sur une classe de liaison de modèle. Simplement hello type référencé par hello MetadataTypeAttribute doivent être un sous-ensemble de hello référençant le type de (il peut avoir moins de propriétés, mais pas plus).</li><li>**Le déplacement des données entre les modèles d’entrée utilisateur et les modèles de base de données s’avère fastidieux. Puis-je simplement copier toutes les propriétés par réflexion ? -** Oui. Hello uniquement les propriétés qui apparaissent dans les modèles de liaison hello sont hello ceux que vous avez déterminé toobe sécurisé pour l’entrée d’utilisateur. Il n’existe aucune raison de sécurité qui empêche l’utilisation de la réflexion toocopy sur toutes les propriétés qui existent en commun entre ces deux modèles.</li><li>**Qu’en est-il de [Bind(Exclude ="â€¦")] ? Puis-je l’utiliser à la place de modèles de liaison distincts ? -** Cette approche n’est pas recommandée. L’utilisation de [Bind(Exclude ="â€¦")] indique que toute nouvelle propriété peut être liée par défaut. Lorsque vous ajoutez une nouvelle propriété, un choses de tookeep tooremember étape supplémentaire est sécurisée, plutôt que conception de hello être sécurisé par défaut. En fonction de développeur de hello il est risquée de la vérification de cette liste chaque fois qu’une propriété est ajoutée.</li><li>**[Bind(Include ="â€¦")] est-il utile pour les opérations de modification ? -** Non. [Bind(Include ="â€¦")] convient uniquement aux opérations de style INSERT (ajout de nouvelles données). Pour les opérations de mise à jour-style (revoir les données existantes), utilisez une autre approche, comme ayant des modèles de liaison distincts ou en passant une liste explicite des propriétés autorisées tooUpdateModel ou TryUpdateModel. Ajout d’un [lier (Include = "¦ d’â€ »)] l’attribut sur une opération de modification signifie que MVC crée une instance d’objet et définir uniquement hello répertoriés propriétés, en laissant toutes les autres valeurs par défaut. Lorsque les données de salutation sont rendu persistant, il remplace entièrement entité existante hello, réinitialisation des valeurs hello pour toutes les valeurs par défaut de propriétés omises tootheir. Par exemple, si IsAdmin a été omis d’un [lier (Include = « ¦ d’â€ »)] l’attribut sur une opération de modification, tout utilisateur dont le nom a été modifié par cette action serait réinitialisation tooIsAdmin = false (n’importe quel utilisateur modifié perdrait le statut d’administrateur). Tooprevent met à jour les propriétés de toocertain, utilisez une des hello autres approches ci-dessus. Certaines versions des outils MVC génèrent des classes de contrôleur avec [Bind(Include ="â€¦")] sur les actions de modification et impliquent que la suppression d’une propriété de cette liste empêche les attaques par survalidation. Toutefois, comme décrit ci-dessus, cette approche ne fonctionne pas comme prévu et réinitialise à la place des données dans les propriétés tootheir hello omis par défaut.</li><li>**Pour les opérations de création, des mises en garde utilisent-elles [Bind(Include ="â€¦")] au lieu de modèles de liaison distincts ? -** Oui. Tout d’abord, cette approche ne fonctionne pas pour les scénarios de modification, qui nécessitent le maintien de deux approches distinctes afin de limiter toutes les vulnérabilités de survalidation. Séparation des responsabilités entre la forme hello utilisé pour la forme d’entrée et hello utilisateur utilisée pour la persistance, appliquent des modèles de la deuxième liaison quelque chose [lier (Include = "¦ de €â »)] ne fait pas. Enfin, notez que [lier (Include = « ¦ de €â »)] peut uniquement gérer les propriétés de niveau supérieur ; Vous ne peut pas autoriser uniquement les parties des sous-propriétés (par exemple, « Details.Name ») dans l’attribut de hello. Enfin et, éventuellement, plus important encore, à l’aide de [lier (Include = "¦ de €â »)] ajoute une étape supplémentaire qui doit être mémorisée n’importe quelle classe hello de temps utilisée pour la liaison de modèle. Si une méthode d’action lie directement des classes de données toohello et oublie tooinclude un [lier (Include = « ¦ d’â€ »)] attribut, il peut être vulnérable tooover-validation attaques, par conséquent, hello [lier (Include = « ¦ d’â€ »)] approche est un peu moins sécurisée par défaut. Si vous utilisez [lier (Include = "¦ de €â »)], veillez à toujours tooremember toospecify il chaque fois que vos classes de données s’affichent en tant que paramètres de méthode d’action.</li><li>**Des opérations de création, ce que sur l’intégration de hello [lier (Include = « ¦ de €â »)] l’attribut sur la classe de modèle hello elle-même ? Ne pas cette approche éviter hello besoin tooremember mise hello attribut sur chaque méthode d’action ? -** Cette approche fonctionne dans certains cas. À l’aide de [lier (Include = « ¦ de €â »)] sur le type de modèle hello lui-même (et non sur les paramètres d’action à l’aide de cette classe), éviter Bonjour besoin tooremember tooinclude Bonjour [lier (Include = « ¦ de €â »)] l’attribut sur chaque méthode d’action. Utilisation efficace des attributs de hello directement sur la classe hello crée une surface d’exposition distincte de cette classe pour à des fins de liaison de modèle. Toutefois, cette approche ne permet qu’une seule forme de liaison de modèle par classe de modèle. Si une méthode d’action doit tooallow liaison de modèle d’un champ (par exemple, un administrateur uniquement action qui met à jour des rôles d’utilisateur) et autres actions doivent tooprevent liaison de modèle de ce champ, cette approche ne fonctionnera pas. Chaque classe peut avoir qu’une seule forme de liaison de modèle ; Si des actions différentes doivent les formes de liaison de modèle différent, ils doivent toorepresent ces formes à l’aide de deux classes de liaison de modèle distinct de séparer ou séparent [lier (Include = "¦ de €â »)] attributs sur les méthodes d’action hello.</li><li>**Ce que sont les modèles de liaison ? Sont qu'elles hello identique à afficher les modèles ? -** Ce sont deux concepts connexes. terme de Hello tooa classe de modèle utilisé dans une action fait référence au modèle de liaison est la liste de paramètres (forme hello passé à partir de la méthode d’action MVC modèle liaison toohello). modèle d’affichage Hello terme fait référence tooa classe de modèle passée à partir d’une vue de tooa méthode action. À l’aide d’un modèle spécifique à la vue est une approche commune pour passer des données à partir d’une vue de tooa méthode action. Souvent, cette forme peut également être utilisée pour la liaison de modèle et le modèle de vue hello terme peut être hello toorefer utilisés même modèle utilisé dans les deux emplacements. toobe précise, cette procédure traite spécifiquement sur la liaison de modèles, en mettant l’accent sur la forme hello passé toohello action, ce qui est important pour des raisons d’attribution en masse.</li></ul>| 

## <a id="rendering"></a>Encoder toorendering préalable de sortie web non fiable

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, Web Forms, MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Comment tooprevent Cross-site scripting dans ASP.NET](http://msdn.microsoft.com/library/ms998274.aspx), [Cross-site Scripting](http://cwe.mitre.org/data/definitions/79.html), [XSS (XSS) prévention Cheat Sheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet) |
| **Étapes** | Les scripts entre sites (XSS généralement abrégé) sont un vecteur d’attaque pour les services en ligne ou n’importe quel/composant d’application qui consomme l’entrée à partir du web de hello. Vulnérabilités XSS peuvent permettre à un attaquant tooexecute script sur l’ordinateur d’un autre utilisateur via une application web vulnérable. Les scripts malveillants vous pouvez les cookies utilisés toosteal et sinon falsifier un ordinateur cible via JavaScript. Pour empêcher les scripts intersites, il faut procéder à la validation des entrées utilisateur, en s’assurant que la forme et l’encodage sont corrects avant le rendu sur une page web. La validation des entrées et l’encodage des sorties peuvent se faire au moyen de Web Protection Library. Pour du code managé (C\#, VB.net, etc.), utilisez une ou plus approprié de méthodes d’encodage à partir de hello bibliothèque Web Protection (Anti-XSS), selon le contexte hello où obtient explicitée hello l’entrée d’utilisateur :| 

### <a name="example"></a>Exemple

```C#
* Encoder.HtmlEncode 
* Encoder.HtmlAttributeEncode 
* Encoder.JavaScriptEncode 
* Encoder.UrlEncode
* Encoder.VisualBasicScriptEncode 
* Encoder.XmlEncode 
* Encoder.XmlAttributeEncode 
* Encoder.CssEncode 
* Encoder.LdapEncode 
```

## <a id="typemodel"></a>Procéder à la validation et au filtrage des entrées sur les propriétés de modèle de tous types de chaînes

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Adding Validation (Ajout d’une validation)](http://www.asp.net/mvc/overview/getting-started/introduction/adding-validation), [Validating Model Data in an MVC Application (Validation des données de modèle dans une application MVC)](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Principes directeurs pour vos applications ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Étapes** | <p>Tous les paramètres d’entrée hello doivent être validées avant d’être utilisées dans hello application tooensure que l’application hello est sauvegardée sur les entrées utilisateur malveillant. Valider les valeurs d’entrée hello côté serveur avec une stratégie de contrôle d’autorisation à l’aide de validations d’expression régulière. Unsanitized des entrées d’utilisateur / paramètres passés toohello méthodes peuvent entraîner les vulnérabilités d’injection du code.</p><p>Pour les applications web, les points d’entrée peuvent également inclure des champs de formulaire, des chaînes de requête, des cookies, des en-têtes HTTP et des paramètres de service web.</p><p>Hello les contrôles de validation d’entrée suivant doivent être effectuées sur la liaison de modèle :</p><ul><li>Propriétés du modèle Hello doivent être annotées avec l’annotation RegularExpression, permettant d’accepter les caractères autorisés et la longueur maximale autorisée</li><li>les méthodes de contrôleur Hello doivent effectuer ModelState validité</li></ul>|

## <a id="richtext"></a>Les champs de formulaire acceptant tous les caractères, par exemple dans un éditeur de texte enrichi, doivent être nettoyés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Encode Unsafe Input (Encodage d’entrées à risque)](https://msdn.microsoft.com/library/ff647397.aspx#paght000003_step3), [HTML Sanitizer](https://github.com/mganss/HtmlSanitizer) |
| **Étapes** | <p>Identifier toutes les balises que vous souhaitez toouse statique. Une pratique courante est mise en forme des éléments de toosafe HTML, tels que des toorestrict `<b>` (gras) et `<i>` (en italique).</p><p>Avant d’écrire des données hello, encoder en HTML il. Cela rend n’importe quel script malveillant sécurisé en lui faisant toobe géré comme du texte, pas comme du code exécutable.</p><ol><li>Désactiver la demande ASP.NET validation en ajoutant des hello hello ValidateRequest = toohello d’attribut « false » directive @ Page</li><li>Encoder l’entrée de chaîne hello avec la méthode de HtmlEncode hello</li><li>Utiliser un StringBuilder et l’appel de ses tooselectively de la méthode Replace supprimer hello encodage sur les éléments de hello HTML que vous souhaitez toopermit</li></ol><p>Hello hello dans page références désactive la validation de la demande ASP.NET en définissant `ValidateRequest="false"`. Il encode au format HTML de hello d’entrée et permet de manière sélective hello `<b>` et `<i>` également une bibliothèque .NET pour le nettoyage du HTML peut également être utilisée.</p><p>HtmlSanitizer est une bibliothèque .NET pour le nettoyage des fragments HTML et les constructions qui peuvent entraîner des attaques de tooXSS des documents. Il utilise AngleSharp tooparse, manipuler et effectuer le rendu HTML et CSS. HtmlSanitizer peut être installé comme un package NuGet et hello l’entrée d’utilisateur peut être passée aux méthodes le nettoyage du code HTML ou CSS, le cas échéant, sur le côté du serveur hello. Dans le cadre du contrôle de sécurité, le nettoyage doit être envisagé uniquement en dernier recours.</p><p>La validation des entrées et l’encodage des sorties sont considérés comme de meilleurs contrôles de sécurité.</p> |

## <a id="inbuilt-encode"></a>N’affectez pas toosinks d’éléments DOM qui n’ont pas de codage intégrés

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | De nombreuses fonctions JavaScript ne procèdent pas à l’encodage par défaut. Lorsque vous affectez des éléments tooDOM d’entrée non fiable par le biais de ces fonctions, peut entraîner entre les exécutions de script (XSS) de site.| 

### <a name="example"></a>Exemple
Voici quelques exemples non sécurisés : 

```
document.getElementByID("div1").innerHtml = value;
$("#userName").html(res.Name);
return $('<div/>').html(value)
$('body').append(resHTML);   
```
N’utilisez pas `innerHtml`. Utilisez plutôt `innerText`. De même, au lieu de `$("#elm").html()`, utilisez`$("#elm").text()` 

## <a id="redirect-safe"></a>Valider toutes les redirections au sein de l’application hello sont fermées ou terminées en toute sécurité

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Hello OAuth 2.0 Authorization Framework - redirecteurs ouvert](http://tools.ietf.org/html/rfc6749#section-10.15) |
| **Étapes** | <p>Conception d’applications nécessitant l’emplacement de fourni par l’utilisateur tooa redirection doit limiter hello redirection possibles cibles tooa « sécurisée » liste prédéfinie de sites ou domaines. Toutes les redirections dans une application hello doivent être fermé/safe.</p><p>toodo cela :</p><ul><li>Identifiez toutes les redirections</li><li>Implémentez une mesure de correction appropriée pour chaque redirection. Les mesures de correction appropriées incluent la confirmation utilisateur ou les listes blanches de redirection. Si un site web ou un service avec vulnérabilité par redirection ouverte utilise les fournisseurs d’identité Facebook/OAuth/OpenID, une personne malveillante peut voler le jeton d’ouverture de session d’un utilisateur et emprunter l’identité de cet utilisateur. Il s’agit d’un risque à prendre lors de l’utilisation de OAuth, qui est décrit dans la RFC 6749 « hello OAuth 2.0 Authorization Framework », Section 10.15 « ouvrir redirige » de la même façon, informations d’identification des utilisateurs peuvent être compromises par des attaques d’hameçonnage spear à l’aide de redirections ouvertes</li></ul>|

## <a id="string-method"></a>Implémenter la validation des entrées sur tous les paramètres de type de chaîne acceptés par les méthodes de contrôleur

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Validating Model Data in an MVC Application (Validation des données de modèle dans une application MVC)](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Principes directeurs pour vos applications ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Étapes** | Pour les méthodes qui acceptent uniquement un type de données primitif, et non les modèles en tant qu’argument, la validation des entrées doit être effectuée à l’aide d’expressions régulières. Dans le cas présent, Regex.IsMatch doit être utilisé avec un modèle d’expression régulière valide. Si hello entrée ne correspond pas à hello d’Expression régulière spécifiée, contrôle ne doit pas poursuivre et un avertissement adéquat concernant l’échec de la validation doit être affiché.| 

## <a id="dos-expression"></a>Définir le délai d’expiration de la limite supérieure pour le traitement DoS tooprevent en raison des expressions régulières toobad d’expressions régulières

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, Web Forms, MVC5, MVC6  |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Propriété DefaultRegexMatchTimeout](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.defaultregexmatchtimeout.aspx) |
| **Étapes** | tooensure attaques par déni de service contre mal créé des expressions régulières qui entraînent un grand nombre de la rétroaction, définir le délai d’attente de hello global par défaut. Si le temps de traitement hello prend plus de temps que hello défini par la limite supérieure, elle lève une exception de délai d’attente. Si rien n’est configuré, délai d’attente hello serait infinie.| 

### <a name="example"></a>Exemple
Par exemple, hello de configuration suivant lève une RegexMatchTimeoutException, si le traitement de hello prend plus de 5 secondes : 

```C#
<httpRuntime targetFramework="4.5" defaultRegexMatchTimeout="00:00:05" />
```

## <a id="html-razor"></a>Éviter l’utilisation de Html.Raw dans les vues Razor

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Application web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| Étape | ASP.Net WebPages (Razor) procède à un encodage HTML automatique. Toutes les chaînes imprimées par des pépites, ou nuggets, de code (blocs @) sont automatiquement encodées au format HTML. Toutefois, lorsque la méthode `HtmlHelper.Raw` est appelée, elle renvoie un balisage qui n’est pas encodé au format HTML. Si `Html.Raw()` méthode d’assistance est utilisé, il ignore hello encodage protection automatique qui fournit de Razor.|

### <a name="example"></a>Exemple
Voici un exemple non sécurisé : 

```C#
<div class="form-group">
            @Html.Raw(Model.AccountConfirmText)
        </div>
        <div class="form-group">
            @Html.Raw(Model.PaymentConfirmText)
        </div>
</div>
```
N’utilisez pas `Html.Raw()` sauf si vous avez besoin toodisplay balisage. Cette méthode n’effectue pas de codage implicite en sortie. Utilisez d’autres aides ASP.NET, comme `@Html.DisplayFor()` 

## <a id="stored-proc"></a>Ne pas utiliser les requêtes dynamiques dans les procédures stockées

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Base de données | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Une attaque d’injection SQL exploite les vulnérabilités de validation d’entrée toorun des commandes arbitraires dans la base de données hello. Il peut se produire lorsque votre application utilise tooconstruct d’entrée dynamique tooaccess d’instructions SQL hello de base de données. Cela peut également se produire si votre code utilise des procédures stockées contenant des chaînes transmises qui comportent des entrées utilisateur brutes. À l’aide de hello attaque par injection SQL, les intrus hello peuvent exécuter des commandes arbitraires dans la base de données hello. Toutes les instructions SQL (y compris les instructions SQL hello dans les procédures stockées) doivent être paramétrables. Instructions SQL paramétrées accepte les caractères ayant tooSQL une signification particulière (par exemple, le guillemet simple) sans problème, car ils sont fortement typées. |

### <a name="example"></a>Exemple
Voici un exemple de procédure stockée dynamique non sécurisée : 

```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteria]
(
  @productName nvarchar(200) = NULL,
  @startPrice float = NULL,
  @endPrice float = NULL
)
AS
 BEGIN
  DECLARE @sql nvarchar(max)
  SELECT @sql = ' SELECT ProductID, ProductName, Description, UnitPrice, ImagePath' +
       ' FROM dbo.Products WHERE 1 = 1 '
       PRINT @sql
  IF @productName IS NOT NULL
     SELECT @sql = @sql + ' AND ProductName LIKE ''%' + @productName + '%'''
  IF @startPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice > ''' + CONVERT(VARCHAR(10),@startPrice) + ''''
  IF @endPrice IS NOT NULL
     SELECT @sql = @sql + ' AND UnitPrice < ''' + CONVERT(VARCHAR(10),@endPrice) + ''''

  PRINT @sql
  EXEC(@sql)
 END
```

### <a name="example"></a>Exemple
Voici hello même procédure stockée a été implémentée en toute sécurité : 
```C#
CREATE PROCEDURE [dbo].[uspGetProductsByCriteriaSecure]
(
             @productName nvarchar(200) = NULL,
             @startPrice float = NULL,
             @endPrice float = NULL
)
AS
       BEGIN
             SELECT ProductID, ProductName, Description, UnitPrice, ImagePath
             FROM dbo.Products where
             (@productName IS NULL or ProductName like '%'+ @productName +'%')
             AND
             (@startPrice IS NULL or UnitPrice > @startPrice)
             AND
             (@endPrice IS NULL or UnitPrice < @endPrice)         
       END
```

## <a id="validation-api"></a>S’assurer que la validation du modèle est effectuée sur les méthodes d’API Web

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | MVC5, MVC6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Model Validation in ASP.NET Web API (Validation du modèle dans l’API Web ASP.NET)](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api) |
| **Étapes** | Lorsqu’un client envoie des API web de tooa données, ce sont des données de hello toovalidate obligatoire avant de procéder à un traitement. Pour les API Web ASP.NET qui acceptent des modèles en tant qu’entrée, utiliser des annotations de données sur les règles de validation de modèles tooset sur les propriétés hello du modèle de hello.|

### <a name="example"></a>Exemple
Hello suivant de code montre hello même : 

```C#
using System.ComponentModel.DataAnnotations;

namespace MyApi.Models
{
    public class Product
    {
        public int Id { get; set; }
        [Required]
        [RegularExpression(@"^[a-zA-Z0-9]*$", ErrorMessage="Only alphanumeric characters are allowed.")]
        public string Name { get; set; }
        public decimal Price { get; set; }
        [Range(0, 999)]
        public double Weight { get; set; }
    }
}
```

### <a name="example"></a>Exemple
Dans la méthode d’action hello de contrôleurs d’API hello, la validité du modèle de hello a toobe vérifié de façon explicite comme indiqué ci-dessous : 

```C#
namespace MyApi.Controllers
{
    public class ProductsController : ApiController
    {
        public HttpResponseMessage Post(Product product)
        {
            if (ModelState.IsValid)
            {
                // Do something with hello product (not shown).

                return new HttpResponseMessage(HttpStatusCode.OK);
            }
            else
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
            }
        }
    }
}
```

## <a id="string-api"></a>Implémenter la validation des entrées sur tous les paramètres de type de chaîne acceptés par les méthodes d’API Web

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, MVC 5, MVC 6 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Validating Model Data in an MVC Application (Validation des données de modèle dans une application MVC)](http://msdn.microsoft.com/library/dd410404(v=vs.90).aspx), [Principes directeurs pour vos applications ASP.NET MVC](http://msdn.microsoft.com/magazine/dd942822.aspx) |
| **Étapes** | Pour les méthodes qui acceptent uniquement un type de données primitif, et non les modèles en tant qu’argument, la validation des entrées doit être effectuée à l’aide d’expressions régulières. Dans le cas présent, Regex.IsMatch doit être utilisé avec un modèle d’expression régulière valide. Si hello entrée ne correspond pas à hello d’Expression régulière spécifiée, contrôle ne doit pas poursuivre et un avertissement adéquat concernant l’échec de la validation doit être affiché.|

## <a id="typesafe-api"></a>S’assurer que les paramètres de type sécurisé sont utilisés dans une API Web pour l’accès aux données

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | API Web | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | N/A  |
| **Étapes** | <p>Si vous utilisez la collection de paramètres hello, SQL traite hello entrée est comme une valeur littérale et non en tant que code exécutable. collection de paramètres de Hello peut être tooenforce utilisé les contraintes de type et la longueur des données d’entrée. Les valeurs en dehors de la plage de hello déclenchent une exception. Si les paramètres SQL de type sécurisé ne sont pas utilisés, des personnes malveillantes peuvent être en mesure de tooexecute les attaques par injection sont incorporés dans l’entrée de hello non filtré.</p><p>Utiliser les paramètres de type sécurisé lors de la construction SQL interroge tooavoid possibles attaques par injection SQL qui peuvent se produire avec des entrées non filtrées. Vous pouvez utiliser des paramètres de type sécurisé avec des procédures stockées et des instructions SQL dynamiques. Les paramètres sont traités comme des valeurs littérales par base de données hello et non en tant que code exécutable. Le type et la longueur sont également vérifiés pour les paramètres.</p>|

### <a name="example"></a>Exemple
Hello de code suivant montre comment toouse paramètres de type sécurisés avec hello SqlParameterCollection lors de l’appel d’une procédure stockée. 

```C#
using System.Data;
using System.Data.SqlClient;

using (SqlConnection connection = new SqlConnection(connectionString))
{ 
DataSet userDataset = new DataSet(); 
SqlDataAdapter myCommand = new SqlDataAdapter(LoginStoredProcedure", connection); 
myCommand.SelectCommand.CommandType = CommandType.StoredProcedure; 
myCommand.SelectCommand.Parameters.Add("@au_id", SqlDbType.VarChar, 11); 
myCommand.SelectCommand.Parameters["@au_id"].Value = SSN.Text; 
myCommand.Fill(userDataset);
}  
```
Bonjour précédant l’exemple de code, la valeur d’entrée de hello ne peut pas être supérieure à 11 caractères. Si les données de salutation n’est pas conforme toohello type ou la longueur définie par le paramètre hello, hello SqlParameter, classe lève une exception. 

## <a id="sql-docdb"></a>Utiliser des requêtes SQL paramétrables pour Azure Cosmos DB

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | Azure Document DB | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique |
| **Attributs**              | N/A  |
| **Informations de référence**              | [Announcing SQL Parameterization in DocumentDB (Annonce de paramétrage SQL dans DocumentDB)](https://azure.microsoft.com/blog/announcing-sql-parameterization-in-documentdb/) |
| **Étapes** | Bien que DocumentDB prenne uniquement en charge les requêtes en lecture seule, l’injection de code SQL reste possible si les requêtes sont construites par concaténation avec les entrées utilisateur. Il est possible pour un toodata de l’accès utilisateur toogain qu’ils ne doivent pas être y accéder à hello même collection, en créant des requêtes SQL malveillantes. Utilisez des requêtes SQL paramétrables si les requêtes sont créées à partir d’entrées utilisateur. |

## <a id="schema-binding"></a>Validation des entrées WCF par le biais de la liaison de schéma

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff647820.aspx) |
| **Étapes** | <p>Un manque de validation entraîne toodifferent type d’attaques par injection de code.</p><p>Validation de message représente une ligne de défense dans la protection de votre application WCF hello. Avec cette approche, vous validez des messages à l’aide des opérations de service WCF schémas tooprotect contre une attaque par un client malveillant. Valider tous les messages reçus par le client de hello tooprotect hello client contre les attaques par un service malveillant. Validation de message rend possible toovalidate messages quand opérations consomment des contrats de message ou des contrats de données, ce qui ne peut pas être effectuées à l’aide de la validation de paramètre. Validation des messages vous permet de toocreate la logique de validation à l’intérieur des schémas, pour une plus grande flexibilité et réduire les temps de développement. Les schémas peuvent être réutilisées entre différentes applications au sein de l’organisation hello, la création de normes pour la représentation sous forme de données. En outre, validation des messages vous permet des opérations tooprotect quand ils consomment des types de données plus complexes impliquant des contrats de logique métier.</p><p>validation de message tooperform vous tout d’abord créez un schéma qui représente les opérations de hello votre service hello types de données et consommées par ces opérations. Vous créez ensuite une classe .NET qui implémente un inspecteur de message client personnalisé et personnalisée de répartiteur de messages inspecteur toovalidate hello messages envoyés/reçus à partir de service de hello. Ensuite, vous implémentez une validation de message de point de terminaison personnalisé comportement tooenable sur hello client et le service de hello. Enfin, vous implémentez un élément de configuration personnalisée sur une classe hello qui permet de vous hello de tooexpose étendu de comportement de point de terminaison personnalisé dans le fichier de configuration hello du service de hello ou du client de hello »</p>|

## <a id="parameters"></a>WCF - Validation des entrées par le biais des inspecteurs de paramètres

| Intitulé                   | Détails      |
| ----------------------- | ------------ |
| **Composant**               | WCF | 
| **Phase SDL**               | Créer |  
| **Technologies applicables** | Générique, NET Framework 3 |
| **Attributs**              | N/A  |
| **Informations de référence**              | [MSDN](https://msdn.microsoft.com/library/ff647875.aspx) |
| **Étapes** | <p>Entrée et validation de données représente une ligne importante de défense dans la protection de votre application WCF hello. Vous devez valider tous les paramètres sont exposés dans le service WCF service operations tooprotect hello contre une attaque par un client malveillant. À l’inverse, vous devez également valider toutes les valeurs de retour reçues par le client de hello tooprotect hello client contre les attaques par un service malveillant</p><p>WCF fournit des points d’extensibilité différents qui vous permettent de comportement d’exécution WCF toocustomize hello en créant des extensions personnalisées. Les inspecteurs de paramètre et les inspecteurs sont deux mécanismes d’extensibilité utilisée toogain plus grand contrôle sur les données de salutation passage entre un client et un service. Vous devez utiliser des inspecteurs de paramètre pour la validation d’entrée et utiliser des inspecteurs de message uniquement lorsque vous devez tooinspect hello intégralité du message entrants et sortants d’un service.</p><p>validation des entrées tooperform, vous allez créer une classe .NET et implémenter un inspecteur de paramètre personnalisé dans les paramètres de toovalidate de commande sur les opérations dans votre service. Vous allez ensuite implémenter une validation de tooenable de comportement de point de terminaison personnalisé sur hello client et le service de hello. Enfin, vous allez implémenter un élément de configuration personnalisé sur une classe hello qui permet de vous hello de tooexpose étendu de comportement de point de terminaison personnalisé dans le fichier de configuration hello du service de hello ou du client de hello</p>|
