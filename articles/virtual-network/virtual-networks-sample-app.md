---
title: "Exemple d’application Azure pour une utilisation avec des réseaux de périmètre | Microsoft Docs"
description: "Déployez cette application web simple pour tester des scénarios de flux de trafic suite à la création d’un réseau de périmètre."
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 8506238e41c5d9dac8d76d729d4919b30a0528b9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="3c851-103">Exemple d’application pour une utilisation avec des réseaux de périmètre</span><span class="sxs-lookup"><span data-stu-id="3c851-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="3c851-104">[Revenir à la page Meilleures pratiques relatives aux frontières de sécurité][HOME]</span><span class="sxs-lookup"><span data-stu-id="3c851-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="3c851-105">Ces scripts PowerShell peuvent être exécutés localement sur les serveurs IIS01 et AppVM01. Ils installent et configurent une application web simple qui affiche une page HTML à partir du serveur frontal IIS01 avec du contenu provenant du serveur principal AppVM01.</span><span class="sxs-lookup"><span data-stu-id="3c851-105">These PowerShell scripts can be run locally on the IIS01 and AppVM01 servers to install and set up a simple web application that displays an html page from the front-end IIS01 server with content from the back-end AppVM01 server.</span></span>

<span data-ttu-id="3c851-106">Cette application fournit un environnement de test simple pour la plupart des exemples de réseau de périmètre. Elle permet aussi de voir l’impact des modifications apportées aux points de terminaison, groupes de sécurité réseau, itinéraires définis par l’utilisateur et règles de pare-feu sur les flux de trafic.</span><span class="sxs-lookup"><span data-stu-id="3c851-106">This application provides a simple testing environment for many of the DMZ Examples and how changes on the Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-to-allow-icmp"></a><span data-ttu-id="3c851-107">Règle de pare-feu pour autoriser ICMP</span><span class="sxs-lookup"><span data-stu-id="3c851-107">Firewall rule to allow ICMP</span></span>
<span data-ttu-id="3c851-108">Cette instruction PowerShell simple peut être exécutée sur n’importe quelle machine virtuelle Windows pour autoriser le trafic ICMP (Ping).</span><span class="sxs-lookup"><span data-stu-id="3c851-108">This simple PowerShell statement can be run on any Windows VM to allow ICMP (Ping) traffic.</span></span> <span data-ttu-id="3c851-109">Cette mise à jour de pare-feu permet au protocole ping de franchir le Pare-feu Windows (pour la plupart des distributions Linux, ICMP est activé par défaut), ce qui facilite les tests et la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="3c851-109">This firewall update allows for easier testing and troubleshooting by allowing the ping protocol to pass through the windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="3c851-110">Si vous utilisez les scripts suivants, l’ajout de cette règle de pare-feu est la première instruction.</span><span class="sxs-lookup"><span data-stu-id="3c851-110">If you use the following scripts, this firewall rule addition is the first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="3c851-111">IIS01 - Script d’installation de l’application web</span><span class="sxs-lookup"><span data-stu-id="3c851-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="3c851-112">Ce script :</span><span class="sxs-lookup"><span data-stu-id="3c851-112">This script will:</span></span>

1. <span data-ttu-id="3c851-113">ouvre IMCPv4 (Ping) sur le Pare-feu Windows du serveur local pour faciliter les tests ;</span><span class="sxs-lookup"><span data-stu-id="3c851-113">Open IMCPv4 (Ping) on the local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="3c851-114">installe IIS et le .NET Framework 4.5 ;</span><span class="sxs-lookup"><span data-stu-id="3c851-114">Install IIS and the .Net Framework v4.5</span></span>
3. <span data-ttu-id="3c851-115">crée une page web ASP.NET et un fichier Web.config ;</span><span class="sxs-lookup"><span data-stu-id="3c851-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="3c851-116">modifie le pool d’applications par défaut pour faciliter l’accès aux fichiers ;</span><span class="sxs-lookup"><span data-stu-id="3c851-116">Change the Default application pool to make file access easier</span></span>
5. <span data-ttu-id="3c851-117">affecte votre compte d’administrateur et votre mot de passe à l’utilisateur Anonyme.</span><span class="sxs-lookup"><span data-stu-id="3c851-117">Set the Anonymous user to your admin account and password</span></span>

<span data-ttu-id="3c851-118">Ce script PowerShell doit être exécuté localement, l’accès à IIS01 s’effectuant via RDP.</span><span class="sxs-lookup"><span data-stu-id="3c851-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter the admin account information used to create this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "The Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "The Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from the inside (a web server on a private network),<br />
          and it is making its way to the outside! (If you are viewing this from the internet)<br />
          <br />
          The following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that the web server is reaching AppVM01 on the backend subnet and successfully returning content</li>
            <li> Image from the Internet - Doesnt really show anything, but it made me happy to see this when the app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from the Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool to Clasic Pipeline to remote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure the IIS settings take
    Write-Host "Restarting the W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="3c851-119">AppVM01 - Script d’installation du serveur de fichiers</span><span class="sxs-lookup"><span data-stu-id="3c851-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="3c851-120">Ce script configure le serveur principal pour cette application simple.</span><span class="sxs-lookup"><span data-stu-id="3c851-120">This script sets up the back-end for this simple application.</span></span> <span data-ttu-id="3c851-121">Ce script :</span><span class="sxs-lookup"><span data-stu-id="3c851-121">This script will:</span></span>

1. <span data-ttu-id="3c851-122">ouvre IMCPv4 (Ping) sur le pare-feu pour faciliter les tests ;</span><span class="sxs-lookup"><span data-stu-id="3c851-122">Open IMCPv4 (Ping) on the firewall for easier testing</span></span>
2. <span data-ttu-id="3c851-123">crée un répertoire pour le site web ;</span><span class="sxs-lookup"><span data-stu-id="3c851-123">Create a directory for the web site</span></span>
3. <span data-ttu-id="3c851-124">crée un fichier texte auquel la page web accédera à distance ;</span><span class="sxs-lookup"><span data-stu-id="3c851-124">Create a text file to be remotely access by the web page</span></span>
4. <span data-ttu-id="3c851-125">affecte au répertoire et au fichier des autorisations Anonyme pour autoriser l’accès ;</span><span class="sxs-lookup"><span data-stu-id="3c851-125">Set permissions on the directory and file to Anonymous to allow access</span></span>
5. <span data-ttu-id="3c851-126">désactive la sécurité renforcée d’Internet Explorer pour faciliter la navigation à partir de ce serveur.</span><span class="sxs-lookup"><span data-stu-id="3c851-126">Turn off IE Enhanced Security to allow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3c851-127">**Meilleure pratique**: ne désactivez jamais la sécurité renforcée d’Internet Explorer sur un serveur de production, et sachez qu’il est généralement déconseillé de surfer sur le web à partir d’un serveur de production.</span><span class="sxs-lookup"><span data-stu-id="3c851-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea to surf the web from a production server.</span></span> <span data-ttu-id="3c851-128">Sachez aussi que l’ouverture de partages de fichiers en vue d’un accès anonyme, bien que déconseillée, est effectuée ici par souci de simplicité.</span><span class="sxs-lookup"><span data-stu-id="3c851-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="3c851-129">Ce script PowerShell doit être exécuté localement, l’accès à AppVM01 s’effectuant via RDP.</span><span class="sxs-lookup"><span data-stu-id="3c851-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="3c851-130">PowerShell doit être exécuté avec des autorisations d’administrateur pour garantir la réussite de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="3c851-130">PowerShell is required to be run as Administrator to ensure successful execution.</span></span>

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands to work

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm the contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="3c851-131">DNS01 - Script d’installation du serveur DNS</span><span class="sxs-lookup"><span data-stu-id="3c851-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="3c851-132">Aucun script n’est inclus dans cet exemple d’application pour configurer le serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="3c851-132">There is no script included in this sample application to set up the DNS server.</span></span> <span data-ttu-id="3c851-133">Si les tests que vous conduisez sur les règles de pare-feu, groupes de sécurité réseau ou itinéraires définis par l’utilisateur nécessitent l’inclusion du trafic DNS, le serveur DNS01 doit être configuré manuellement.</span><span class="sxs-lookup"><span data-stu-id="3c851-133">If testing of the firewall rules, NSG, or UDR needs to include DNS traffic, the DNS01 server needs to be set up manually.</span></span> <span data-ttu-id="3c851-134">Dans le fichier XML de configuration réseau et le modèle Resource Manager des deux exemples, DNS01 est le serveur DNS principal, et le serveur DNS public hébergé par le niveau 3 est le serveur DNS secondaire.</span><span class="sxs-lookup"><span data-stu-id="3c851-134">The Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as the primary DNS server and the public DNS server hosted by Level 3 as the backup DNS server.</span></span> <span data-ttu-id="3c851-135">Le serveur DNS de niveau 3 est le serveur DNS utilisé pour le trafic non local, et comme DNS01 n’est pas configuré, aucun réseau DNS local n’a lieu.</span><span class="sxs-lookup"><span data-stu-id="3c851-135">The Level 3 DNS server would be the actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c851-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3c851-136">Next steps</span></span>
* <span data-ttu-id="3c851-137">Exécuter le script IIS01 sur un serveur IIS</span><span class="sxs-lookup"><span data-stu-id="3c851-137">Run the IIS01 script on an IIS server</span></span>
* <span data-ttu-id="3c851-138">Exécuter le script de serveur de fichiers sur AppVM01</span><span class="sxs-lookup"><span data-stu-id="3c851-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="3c851-139">Accéder à l’adresse IP publique sur IIS01 pour valider votre build</span><span class="sxs-lookup"><span data-stu-id="3c851-139">Browse to the Public IP on IIS01 to validate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
