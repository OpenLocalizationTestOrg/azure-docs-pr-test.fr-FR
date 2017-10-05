---
title: Configuration de Python dans Azure App Service Web Apps
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
ms.openlocfilehash: 9683a1af13eeff364d3c4714f0b791324fd82659
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="48451-103">Configuration de Python dans Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="48451-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="48451-104">Ce didacticiel décrit les options relatives à la création et à la configuration d’une application Python compatible WSGI (Web Server Gateway Interface) de base dans [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="48451-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="48451-105">Il décrit les fonctions supplémentaires associées au déploiement Git, telles que l’environnement virtuel et l’installation de packages à l’aide de fichier requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="48451-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="48451-106">Bottle, Django ou Flask ?</span><span class="sxs-lookup"><span data-stu-id="48451-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="48451-107">Azure Marketplace comporte des modèles pour les infrastructures Bottle, Django et Flask.</span><span class="sxs-lookup"><span data-stu-id="48451-107">The Azure Marketplace contains templates for the Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="48451-108">Si vous développez votre première application web dans Azure App Service ou que vous n’êtes pas familiarisé avec Git, nous vous invitons à suivre l’un des didacticiels suivants, lesquels présentent des instructions pas à pas pour générer une application à partir de la galerie à l’aide du déploiement Git sur Windows ou Mac :</span><span class="sxs-lookup"><span data-stu-id="48451-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from the gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="48451-109">Création d’applications web avec Bottle</span><span class="sxs-lookup"><span data-stu-id="48451-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="48451-110">Création d’applications web avec Django</span><span class="sxs-lookup"><span data-stu-id="48451-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="48451-111">Création d’applications web avec Flask</span><span class="sxs-lookup"><span data-stu-id="48451-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="48451-112">Création d’applications web sur le portail Azure</span><span class="sxs-lookup"><span data-stu-id="48451-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="48451-113">Ce didacticiel part du principe que vous disposez d'un abonnement Azure et d'un accès au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="48451-113">This tutorial assumes an existing Azure subscription and access to the Azure Portal.</span></span>

<span data-ttu-id="48451-114">Si vous ne disposez pas d’une application web existante, vous pouvez en créer une à partir du [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="48451-114">If you do not have an existing web app, you can create one from the [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="48451-115">Cliquez sur le bouton NOUVEAU dans l’angle supérieur gauche, puis cliquez sur **Web + mobile** > **Application web**.</span><span class="sxs-lookup"><span data-stu-id="48451-115">Click the NEW button in the top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="48451-116">Publication Git</span><span class="sxs-lookup"><span data-stu-id="48451-116">Git Publishing</span></span>
<span data-ttu-id="48451-117">Configurez la publication Git de votre nouvelle application web en suivant les instructions de l’article [Déploiement Git local vers Azure App Service](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="48451-117">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="48451-118">Ce didacticiel utilise Git pour créer, gérer et publier notre application web Python dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="48451-118">This tutorial uses Git to create, manage, and publish our Python web app to Azure App Service.</span></span>

<span data-ttu-id="48451-119">Une fois la publication Git configurée, un référentiel Git est créé et associé à votre application web.</span><span class="sxs-lookup"><span data-stu-id="48451-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="48451-120">L’URL du référentiel est affichée et peut désormais être utilisée pour envoyer des données depuis l’environnement de développement local vers le cloud.</span><span class="sxs-lookup"><span data-stu-id="48451-120">The repository's URL will be displayed and can henceforth be used to push data from the local development environment to the cloud.</span></span> <span data-ttu-id="48451-121">Pour publier des applications via Git, vérifiez qu’un client Git est également installé et suivez les instructions fournies pour envoyer le contenu de votre application web vers Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="48451-121">To publish applications via Git, make sure a Git client is also installed and use the instructions provided to push your web app content to Azure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="48451-122">Vue d’ensemble de l’application</span><span class="sxs-lookup"><span data-stu-id="48451-122">Application Overview</span></span>
<span data-ttu-id="48451-123">Dans les sections suivantes, les fichiers qui suivent sont créés.</span><span class="sxs-lookup"><span data-stu-id="48451-123">In the next sections, the following files are created.</span></span> <span data-ttu-id="48451-124">Ils doivent être placés à la racine du référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="48451-124">They should be placed in the root of the Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="48451-125">Gestionnaire WSGI</span><span class="sxs-lookup"><span data-stu-id="48451-125">WSGI Handler</span></span>
<span data-ttu-id="48451-126">WSGI est une norme Python décrite par [PEP 3333](http://www.python.org/dev/peps/pep-3333/) qui définit une interface entre le serveur web et Python.</span><span class="sxs-lookup"><span data-stu-id="48451-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between the web server and Python.</span></span> <span data-ttu-id="48451-127">Elle fournit une interface normalisée pour la rédaction de diverses applications et infrastructures Web à l'aide de Python.</span><span class="sxs-lookup"><span data-stu-id="48451-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="48451-128">Des infrastructures Web Python connues utilisent aujourd’hui WSGI.</span><span class="sxs-lookup"><span data-stu-id="48451-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="48451-129">Azure App Service Web Apps vous offre la prise en charge de ces infrastructures. En outre, les utilisateurs experts peuvent même créer leur propre infrastructure à condition que le gestionnaire personnalisé suive les instructions de la spécification WSGI.</span><span class="sxs-lookup"><span data-stu-id="48451-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as the custom handler follows the WSGI specification guidelines.</span></span>

<span data-ttu-id="48451-130">Voici un exemple de `app.py` définissant un gestionnaire personnalisé :</span><span class="sxs-lookup"><span data-stu-id="48451-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

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

<span data-ttu-id="48451-131">Vous pouvez exécuter cette application localement à l’aide de `python app.py`, puis accéder à `http://localhost:5555` dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="48451-131">You can run this application locally with `python app.py`, then browse to `http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="48451-132">Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="48451-132">Virtual Environment</span></span>
<span data-ttu-id="48451-133">Bien que l’exemple d’application précédent ne requière aucun package externe, il est probable que votre application en requiert un.</span><span class="sxs-lookup"><span data-stu-id="48451-133">Although the example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="48451-134">Pour faciliter la gestion des dépendances des packages externes, le déploiement Azure Git prend en charge la création d’environnements virtuels.</span><span class="sxs-lookup"><span data-stu-id="48451-134">To help manage external package dependencies, Azure Git deployment supports the creation of virtual environments.</span></span>

<span data-ttu-id="48451-135">Lorsqu’Azure détecte un fichier requirements.txt à la racine du référentiel, il crée automatiquement un environnement virtuel nommé `env`.</span><span class="sxs-lookup"><span data-stu-id="48451-135">When Azure detects a requirements.txt in the root of the repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="48451-136">Cette opération intervient uniquement lors du premier déploiement ou lors de tout déploiement faisant suite à la modification du runtime Python sélectionné.</span><span class="sxs-lookup"><span data-stu-id="48451-136">This only occurs on the first deployment, or during any deployment after the selected Python runtime has changed.</span></span>

<span data-ttu-id="48451-137">Vous souhaiterez probablement créer un environnement virtuel local pour le développement, sans pour autant l’inclure à votre référentiel Git.</span><span class="sxs-lookup"><span data-stu-id="48451-137">You will probably want to create a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="48451-138">Gestion des packages</span><span class="sxs-lookup"><span data-stu-id="48451-138">Package Management</span></span>
<span data-ttu-id="48451-139">Les packages répertoriés dans le fichier requirements.txt seront automatiquement installés au sein de l’environnement virtuel à l’aide de pip.</span><span class="sxs-lookup"><span data-stu-id="48451-139">Packages listed in requirements.txt will be installed automatically in the virtual environment using pip.</span></span> <span data-ttu-id="48451-140">Cette opération intervient à chaque déploiement, mais pip ignorera l’installation si un package est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="48451-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="48451-141">Exemple `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="48451-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="48451-142">Version de Python</span><span class="sxs-lookup"><span data-stu-id="48451-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="48451-143">Exemple `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="48451-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="48451-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="48451-144">Web.config</span></span>
<span data-ttu-id="48451-145">Vous devez créer un fichier web.config pour spécifier de quelle manière le serveur doit gérer les demandes.</span><span class="sxs-lookup"><span data-stu-id="48451-145">You'll need to create a web.config file to specify how the server should handle requests.</span></span>

<span data-ttu-id="48451-146">Si vous disposez d’un fichier web.X.Y.config dans votre référentiel, où X.Y correspond au runtime Python sélectionné, Azure copie automatiquement le fichier approprié en tant que fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="48451-146">Note that if you have a web.x.y.config file in your repository, where x.y matches the selected Python runtime, then Azure will automatically copy the appropriate file as web.config.</span></span>

<span data-ttu-id="48451-147">Les exemples de fichier web.config suivants concernent un script proxy d’environnement virtuel, lequel est décrit dans la section suivante.</span><span class="sxs-lookup"><span data-stu-id="48451-147">The following web.config examples rely on a virtual environment proxy script, which is described in the next section.</span></span>  <span data-ttu-id="48451-148">Ces fichiers fonctionnent avec le gestionnaire WSGI utilisé dans l’exemple `app.py` précédent.</span><span class="sxs-lookup"><span data-stu-id="48451-148">They work with the WSGI handler used in the example `app.py` above.</span></span>

<span data-ttu-id="48451-149">Exemple `web.config` pour Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="48451-149">Example `web.config` for Python 2.7:</span></span>

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


<span data-ttu-id="48451-150">Exemple `web.config` pour Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="48451-150">Example `web.config` for Python 3.4:</span></span>

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


<span data-ttu-id="48451-151">Les fichiers statiques sont directement gérés par le serveur web, sans passer par le code Python, afin d’améliorer les performances.</span><span class="sxs-lookup"><span data-stu-id="48451-151">Static files will be handled by the web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="48451-152">Dans les exemples précédents, l’emplacement des fichiers statiques sur le disque doit correspondre à celui présent dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="48451-152">In the above examples, the location of the static files on disk should match the location in the URL.</span></span> <span data-ttu-id="48451-153">Cela signifie qu’une demande pour `http://pythonapp.azurewebsites.net/static/site.css` renverra au fichier présent sur le disque à l’emplacement `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="48451-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve the file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="48451-154">`WSGI_ALT_VIRTUALENV_HANDLER` est l’emplacement où vous spécifiez le gestionnaire WSGI.</span><span class="sxs-lookup"><span data-stu-id="48451-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify the WSGI handler.</span></span> <span data-ttu-id="48451-155">Dans les exemples précédents, il s’agit de `app.wsgi_app`, car le gestionnaire correspond à une fonction nommée `wsgi_app` dans `app.py`, dans le dossier racine.</span><span class="sxs-lookup"><span data-stu-id="48451-155">In the above examples, it's `app.wsgi_app` because the handler is a function named `wsgi_app` in `app.py` in the root folder.</span></span>

<span data-ttu-id="48451-156">`PYTHONPATH` , mais si vous installez toutes vos dépendances dans l’environnement virtuel en les spécifiant dans le fichier requirements.txt, il n’est pas nécessaire de les modifier.</span><span class="sxs-lookup"><span data-stu-id="48451-156">`PYTHONPATH` can be customized, but if you install all your dependencies in the virtual environment by specifying them in requirements.txt, you shouldn't need to change it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="48451-157">Proxy d’environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="48451-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="48451-158">Le script suivant permet de récupérer le gestionnaire WSGI, d’activer l’environnement virtuel et de journaliser les erreurs.</span><span class="sxs-lookup"><span data-stu-id="48451-158">The following script is used to retrieve the WSGI handler, activate the virtual environment and log errors.</span></span> <span data-ttu-id="48451-159">Il est conçu pour être générique et utilisé sans modification.</span><span class="sxs-lookup"><span data-stu-id="48451-159">It is designed to be generic and used without modifications.</span></span>

<span data-ttu-id="48451-160">Contenu de `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="48451-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject to terms and conditions of the Apache License, Version 2.0. A 
     # copy of the license can be found in the License.html file at the root of this distribution. If 
     # you cannot locate the Apache License, Version 2.0, please send an email to 
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing to be bound 
     # by the terms of the Apache License, Version 2.0.
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
        """Logs fatal errors to a log file if WSGI_LOG env var is defined"""
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


## <a name="customize-git-deployment"></a><span data-ttu-id="48451-161">Personnalisation du déploiement Git</span><span class="sxs-lookup"><span data-stu-id="48451-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="48451-162">Résolution des problèmes - Installation des packages</span><span class="sxs-lookup"><span data-stu-id="48451-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="48451-163">Résolution des problèmes - Environnement virtuel</span><span class="sxs-lookup"><span data-stu-id="48451-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="48451-164">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="48451-164">Next steps</span></span>
<span data-ttu-id="48451-165">Pour plus d’informations, consultez le [Centre pour développeurs Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="48451-165">For more information, see the [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="48451-166">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="48451-166">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="48451-167">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="48451-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="48451-168">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="48451-168">What's changed</span></span>
* <span data-ttu-id="48451-169">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="48451-169">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

