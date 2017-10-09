---
title: aaaConfiguring de Python avec Azure App Service Web Apps
description: "Ce didacticiel décrit les options relatives à la création et à la configuration d’une application Python compatible WSGI (Web Server Gateway Interface) de base dans Azure App Service Web Apps."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="9a5c1-103">Configuration de Python dans Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="9a5c1-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="9a5c1-104">Ce didacticiel décrit les options relatives à la création et à la configuration d’une application Python compatible WSGI (Web Server Gateway Interface) de base dans [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="9a5c1-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="9a5c1-105">Il décrit les fonctions supplémentaires associées au déploiement Git, telles que l’environnement virtuel et l’installation de packages à l’aide de fichier requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="9a5c1-106">Bottle, Django ou Flask ?</span><span class="sxs-lookup"><span data-stu-id="9a5c1-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="9a5c1-107">Bonjour Azure Marketplace contient des modèles pour les infrastructures d’eau, Django et ballon hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-107">hello Azure Marketplace contains templates for hello Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="9a5c1-108">Si vous développez votre première application web dans Azure App Service, ou vous n’êtes pas familiarisé avec Git, nous vous recommandons de suivre une de ces didacticiels, qui incluent des instructions pas à pas pour la création d’une application à partir de la galerie hello à l’aide du déploiement Git à partir de Windows ou Mac :</span><span class="sxs-lookup"><span data-stu-id="9a5c1-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from hello gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="9a5c1-109">Création d’applications web avec Bottle</span><span class="sxs-lookup"><span data-stu-id="9a5c1-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="9a5c1-110">Création d’applications web avec Django</span><span class="sxs-lookup"><span data-stu-id="9a5c1-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="9a5c1-111">Création d’applications web avec Flask</span><span class="sxs-lookup"><span data-stu-id="9a5c1-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="9a5c1-112">Création d’applications web sur le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9a5c1-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="9a5c1-113">Ce didacticiel suppose un existant Azure abonnement et accès toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-113">This tutorial assumes an existing Azure subscription and access toohello Azure Portal.</span></span>

<span data-ttu-id="9a5c1-114">Si vous ne disposez pas d’une application web existante, vous pouvez en créer un à partir de hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9a5c1-114">If you do not have an existing web app, you can create one from hello [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="9a5c1-115">Cliquez sur bouton Nouveau hello hello en haut à gauche, puis cliquez sur **Web + Mobile** > **application Web**.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-115">Click hello NEW button in hello top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="9a5c1-116">Publication Git</span><span class="sxs-lookup"><span data-stu-id="9a5c1-116">Git Publishing</span></span>
<span data-ttu-id="9a5c1-117">Configurer la publication Git de votre application web qui vient d’être créé en suivant les instructions de hello sur [tooAzure de déploiement Git Local du Service d’applications](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="9a5c1-117">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="9a5c1-118">Ce didacticiel utilise Git toocreate, gérer et publier notre tooAzure d’application Python web du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-118">This tutorial uses Git toocreate, manage, and publish our Python web app tooAzure App Service.</span></span>

<span data-ttu-id="9a5c1-119">Une fois la publication Git configurée, un référentiel Git est créé et associé à votre application web.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="9a5c1-120">les URL du référentiel Hello s’affiche et peut être dorénavant utilisés toopush des données du cloud de toohello environnement hello développement local.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-120">hello repository's URL will be displayed and can henceforth be used toopush data from hello local development environment toohello cloud.</span></span> <span data-ttu-id="9a5c1-121">applications toopublish via Git, assurez-vous qu’un client Git est également installé et suivez les instructions hello fourni toopush votre tooAzure de contenu d’application du Service d’applications web.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-121">toopublish applications via Git, make sure a Git client is also installed and use hello instructions provided toopush your web app content tooAzure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="9a5c1-122">Vue d’ensemble de l’application</span><span class="sxs-lookup"><span data-stu-id="9a5c1-122">Application Overview</span></span>
<span data-ttu-id="9a5c1-123">Dans les sections suivantes hello, hello fichiers suivants est créé.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-123">In hello next sections, hello following files are created.</span></span> <span data-ttu-id="9a5c1-124">Ils doivent être placés dans la racine de hello du référentiel Git de hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-124">They should be placed in hello root of hello Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="9a5c1-125">Gestionnaire WSGI</span><span class="sxs-lookup"><span data-stu-id="9a5c1-125">WSGI Handler</span></span>
<span data-ttu-id="9a5c1-126">Wsgi sous est une norme de Python décrite par [PEP 3333](http://www.python.org/dev/peps/pep-3333/) définissant une interface entre le serveur web de hello et Python.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between hello web server and Python.</span></span> <span data-ttu-id="9a5c1-127">Elle fournit une interface normalisée pour la rédaction de diverses applications et infrastructures Web à l'aide de Python.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="9a5c1-128">Des infrastructures Web Python connues utilisent aujourd’hui WSGI.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="9a5c1-129">Azure permet d’application de Service Web Apps que vous prenez en charge pour les versions de .NET Framework ; en outre, les utilisateurs expérimentés peuvent même créer leurs propres tant que gestionnaire personnalisé de hello suit les directives de spécification de wsgi sous hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as hello custom handler follows hello WSGI specification guidelines.</span></span>

<span data-ttu-id="9a5c1-130">Voici un exemple de `app.py` définissant un gestionnaire personnalisé :</span><span class="sxs-lookup"><span data-stu-id="9a5c1-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="9a5c1-131">Vous pouvez exécuter l’application localement avec `python app.py`, puis recherchez trop`http://localhost:5555` dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-131">You can run this application locally with `python app.py`, then browse too`http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="9a5c1-132">Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="9a5c1-132">Virtual Environment</span></span>
<span data-ttu-id="9a5c1-133">Bien que l’application d’exemple hello ci-dessus ne nécessite pas les packages externes, il est probable que votre application nécessite certaines.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-133">Although hello example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="9a5c1-134">toohelp gérer les dépendances du package externe, Azure Git déploiement prend en charge la création d’environnements virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-134">toohelp manage external package dependencies, Azure Git deployment supports hello creation of virtual environments.</span></span>

<span data-ttu-id="9a5c1-135">Quand Azure détecte un requirements.txt racine hello du référentiel de hello, il crée automatiquement un environnement virtuel nommé `env`.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-135">When Azure detects a requirements.txt in hello root of hello repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="9a5c1-136">Cela se produit uniquement sur le premier déploiement de hello, ou pendant un déploiement après hello sélectionné runtime Python a changé.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-136">This only occurs on hello first deployment, or during any deployment after hello selected Python runtime has changed.</span></span>

<span data-ttu-id="9a5c1-137">Vous aurez probablement besoin de toocreate un environnement virtuel localement pour le développement, mais ne pas inclure dans votre référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-137">You will probably want toocreate a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="9a5c1-138">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="9a5c1-138">Package Management</span></span>
<span data-ttu-id="9a5c1-139">Packages répertoriés dans requirements.txt seront automatiquement installés dans un environnement virtuel de hello l’utilisation de pip.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-139">Packages listed in requirements.txt will be installed automatically in hello virtual environment using pip.</span></span> <span data-ttu-id="9a5c1-140">Cette opération intervient à chaque déploiement, mais pip ignorera l’installation si un package est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="9a5c1-141">Exemple `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="9a5c1-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="9a5c1-142">Version de Python</span><span class="sxs-lookup"><span data-stu-id="9a5c1-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="9a5c1-143">Exemple `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="9a5c1-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="9a5c1-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="9a5c1-144">Web.config</span></span>
<span data-ttu-id="9a5c1-145">Vous devez toocreate un toospecify du fichier web.config comment les serveur hello doivent gérer les requêtes.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-145">You'll need toocreate a web.config file toospecify how hello server should handle requests.</span></span>

<span data-ttu-id="9a5c1-146">Notez que si vous disposez d’un fichier web.x.y.config dans votre référentiel où x.y correspond à hello sélectionné runtime Python, puis Azure copie automatiquement le fichier approprié de hello en tant que fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-146">Note that if you have a web.x.y.config file in your repository, where x.y matches hello selected Python runtime, then Azure will automatically copy hello appropriate file as web.config.</span></span>

<span data-ttu-id="9a5c1-147">Hello exemples web.config suivants s’appuient sur un script de proxy environnement virtuel qui est décrit dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-147">hello following web.config examples rely on a virtual environment proxy script, which is described in hello next section.</span></span>  <span data-ttu-id="9a5c1-148">Elles fonctionnent avec le gestionnaire wsgi sous hello utilisé dans l’exemple de hello `app.py` ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-148">They work with hello WSGI handler used in hello example `app.py` above.</span></span>

<span data-ttu-id="9a5c1-149">Exemple `web.config` pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="9a5c1-149">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="9a5c1-150">Exemple `web.config` pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="9a5c1-150">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="9a5c1-151">Fichiers statiques doivent être gérés par le serveur web de hello directement, sans passer par le code Python, pour améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-151">Static files will be handled by hello web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="9a5c1-152">Bonjour exemples ci-dessus, emplacement hello des fichiers statiques de hello sur le disque doit correspondre à emplacement hello dans les URL hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-152">In hello above examples, hello location of hello static files on disk should match hello location in hello URL.</span></span> <span data-ttu-id="9a5c1-153">Cela signifie qu’une demande de `http://pythonapp.azurewebsites.net/static/site.css` servira fichier hello sur le disque à `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve hello file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="9a5c1-154">`WSGI_ALT_VIRTUALENV_HANDLER`est où vous spécifiez le Gestionnaire de wsgi sous hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify hello WSGI handler.</span></span> <span data-ttu-id="9a5c1-155">Bonjour au-dessus des exemples, il a `app.wsgi_app` , car le Gestionnaire de hello est une fonction nommée `wsgi_app` dans `app.py` dans le dossier racine de hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-155">In hello above examples, it's `app.wsgi_app` because hello handler is a function named `wsgi_app` in `app.py` in hello root folder.</span></span>

<span data-ttu-id="9a5c1-156">`PYTHONPATH`peut être personnalisé, mais si vous installez toutes les dépendances dans un environnement virtuel de hello en les spécifiant dans requirements.txt, vous ne devez toochange il.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-156">`PYTHONPATH` can be customized, but if you install all your dependencies in hello virtual environment by specifying them in requirements.txt, you shouldn't need toochange it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="9a5c1-157">Proxy d’environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="9a5c1-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="9a5c1-158">Hello script suivant est associé au gestionnaire utilisé tooretrieve hello wsgi sous, activer les erreurs de journaux et d’environnement virtuels hello.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-158">hello following script is used tooretrieve hello WSGI handler, activate hello virtual environment and log errors.</span></span> <span data-ttu-id="9a5c1-159">Il est conçu toobe générique et utilisé sans modification.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-159">It is designed toobe generic and used without modifications.</span></span>

<span data-ttu-id="9a5c1-160">Contenu de `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="9a5c1-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="9a5c1-161">Personnalisation du déploiement Git</span><span class="sxs-lookup"><span data-stu-id="9a5c1-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="9a5c1-162">Résolution des problèmes - Installation des packages</span><span class="sxs-lookup"><span data-stu-id="9a5c1-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="9a5c1-163">Résolution des problèmes - Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="9a5c1-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="9a5c1-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9a5c1-164">Next steps</span></span>
<span data-ttu-id="9a5c1-165">Pour plus d’informations, consultez hello [centre de développement Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="9a5c1-165">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="9a5c1-166">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-166">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9a5c1-167">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="9a5c1-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="9a5c1-168">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="9a5c1-168">What's changed</span></span>
* <span data-ttu-id="9a5c1-169">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="9a5c1-169">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

