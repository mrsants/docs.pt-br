---
title: Fluxo de trabalho de desenvolvimento do loop interno para aplicativos do Docker
description: Conheça o fluxo de trabalho de "loop interno" para desenvolvimento de aplicativos do Docker.
ms.date: 02/15/2019
ms.openlocfilehash: ce573546f61b98c2f93e998203497fa949e9efe8
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68673973"
---
# <a name="inner-loop-development-workflow-for-docker-apps"></a><span data-ttu-id="0f23d-103">Fluxo de trabalho de desenvolvimento do loop interno para aplicativos do Docker</span><span class="sxs-lookup"><span data-stu-id="0f23d-103">Inner-loop development workflow for Docker apps</span></span>

<span data-ttu-id="0f23d-104">Antes de disparar o fluxo de trabalho de loop externo que abrange todo o ciclo de DevOps, tudo começa no computador de cada desenvolvedor, codificando o aplicativo em si, usando suas linguagens ou plataformas preferenciais e testando localmente (Figura 4-21).</span><span class="sxs-lookup"><span data-stu-id="0f23d-104">Before triggering the outer-loop workflow spanning the entire DevOps cycle, it all begins on each developer's machine, coding the app itself, using their preferred languages or platforms, and testing it locally (Figure 4-21).</span></span> <span data-ttu-id="0f23d-105">Mas, em todos os casos, você terá um ponto importante em comum, independentemente da linguagem, da estrutura ou das plataformas escolhidas.</span><span class="sxs-lookup"><span data-stu-id="0f23d-105">But in every case, you'll have an important point in common, no matter what language, framework, or platforms you choose.</span></span> <span data-ttu-id="0f23d-106">Neste fluxo de trabalho específico, você sempre está desenvolvendo e testando contêineres do Docker, mas localmente.</span><span class="sxs-lookup"><span data-stu-id="0f23d-106">In this specific workflow, you're always developing and testing Docker containers, but locally.</span></span>

![Etapa 1 – Codificar/executar/depurar](./media/image18.png)

<span data-ttu-id="0f23d-108">**Figura 4-21**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-108">**Figure 4-21**.</span></span> <span data-ttu-id="0f23d-109">Contexto de desenvolvimento do loop interno</span><span class="sxs-lookup"><span data-stu-id="0f23d-109">Inner-loop development context</span></span>

<span data-ttu-id="0f23d-110">O contêiner ou instância de uma imagem de Docker terá estes componentes:</span><span class="sxs-lookup"><span data-stu-id="0f23d-110">The container or instance of a Docker image will contain these components:</span></span>

- <span data-ttu-id="0f23d-111">Uma seleção de sistema operacional (por exemplo, uma distribuição do Linux ou Windows)</span><span class="sxs-lookup"><span data-stu-id="0f23d-111">An operating system selection (for example, a Linux distribution or Windows)</span></span>

- <span data-ttu-id="0f23d-112">Arquivos adicionados pelo desenvolvedor (por exemplo, binários do aplicativo)</span><span class="sxs-lookup"><span data-stu-id="0f23d-112">Files added by the developer (for example, app binaries)</span></span>

- <span data-ttu-id="0f23d-113">Configuração (por exemplo, configurações de ambiente e dependências)</span><span class="sxs-lookup"><span data-stu-id="0f23d-113">Configuration (for example, environment settings and dependencies)</span></span>

- <span data-ttu-id="0f23d-114">Instruções sobre quais processos devem ser executados pelo Docker</span><span class="sxs-lookup"><span data-stu-id="0f23d-114">Instructions for what processes to run by Docker</span></span>

<span data-ttu-id="0f23d-115">Você pode configurar o fluxo de trabalho de desenvolvimento do loop interno que utiliza o Docker como processo (descrito na próxima seção).</span><span class="sxs-lookup"><span data-stu-id="0f23d-115">You can set up the inner-loop development workflow that utilizes Docker as the process (described in the next section).</span></span> <span data-ttu-id="0f23d-116">Observe que as etapas iniciais para configurar o ambiente não estão incluídas, porque você só precisa fazer isso uma vez.</span><span class="sxs-lookup"><span data-stu-id="0f23d-116">Consider that the initial steps to set up the environment are not included, because you only need to do it once.</span></span>

## <a name="building-a-single-app-within-a-docker-container-using-visual-studio-code-and-docker-cli"></a><span data-ttu-id="0f23d-117">Criando um único aplicativo dentro de um contêiner do Docker usando o Visual Studio Code e a CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="0f23d-117">Building a single app within a Docker container using Visual Studio Code and Docker CLI</span></span>

<span data-ttu-id="0f23d-118">Aplicativos são compostos por seus próprios serviços e por bibliotecas adicionais (dependências).</span><span class="sxs-lookup"><span data-stu-id="0f23d-118">Apps are made up from your own services plus additional libraries (dependencies).</span></span>

<span data-ttu-id="0f23d-119">A Figura 4-22 mostra as etapas básicas que normalmente você precisaria executar ao criar um aplicativo do Docker, seguidas por descrições detalhadas de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="0f23d-119">Figure 4-22 shows the basic steps that you usually need to carry out when building a Docker app, followed by detailed descriptions of each step.</span></span>

![Visão geral do fluxo de trabalho: Etapa 1 – Codificar, Etapa 2 – Escrever Dockerfiles, Etapa 3 – Criar imagens definidas com Dockerfiles, Etapa 4 – Definir serviços com o arquivo docker-compose, Etapa 5 – Executar contêineres ou aplicativos compostos, Etapa 6 – Testar aplicativos, Etapa 7 – Efetuar push para iniciar o loop externo (pipelines de CI/CD) ou continuar desenvolvendo.](./media/image19.png)

<span data-ttu-id="0f23d-121">**Figura 4-22**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-121">**Figure 4-22**.</span></span> <span data-ttu-id="0f23d-122">Fluxo de trabalho de alto nível do ciclo de vida de aplicativos em contêineres do Docker usando a CLI do Docker</span><span class="sxs-lookup"><span data-stu-id="0f23d-122">High-level workflow for the life cycle for Docker containerized applications using Docker CLI</span></span>

### <a name="step-1-start-coding-in-visual-studio-code-and-create-your-initial-appservice-baseline"></a><span data-ttu-id="0f23d-123">Etapa 1: Iniciar a codificação no Visual Studio Code e criar a linha de base do aplicativo/serviço inicial</span><span class="sxs-lookup"><span data-stu-id="0f23d-123">Step 1: Start coding in Visual Studio Code and create your initial app/service baseline</span></span>

<span data-ttu-id="0f23d-124">A maneira como você desenvolve seu aplicativo é semelhante à maneira como o faz sem o Docker.</span><span class="sxs-lookup"><span data-stu-id="0f23d-124">The way you develop your application is similar to the way you do it without Docker.</span></span> <span data-ttu-id="0f23d-125">A diferença é que, durante o desenvolvimento, você está implantando e testando o aplicativo ou os serviços em execução dentro de contêineres do Docker colocados no ambiente local (como uma VM Linux ou Windows).</span><span class="sxs-lookup"><span data-stu-id="0f23d-125">The difference is that while developing, you're deploying and testing your application or services running within Docker containers placed in your local environment (like a Linux VM or Windows).</span></span>

<span data-ttu-id="0f23d-126">**Configurando o ambiente local**</span><span class="sxs-lookup"><span data-stu-id="0f23d-126">**Setting up your local environment**</span></span>

<span data-ttu-id="0f23d-127">Com as versões mais recentes do Docker para Mac e Windows, é mais fácil do que nunca desenvolver aplicativos do Docker e a configuração é simples.</span><span class="sxs-lookup"><span data-stu-id="0f23d-127">With the latest versions of Docker for Mac and Windows, it's easier than ever to develop Docker applications, and the setup is straightforward.</span></span>

> [!INFORMAÇÕES]
>
> <span data-ttu-id="0f23d-129">Para obter instruções sobre como configurar o Docker for Windows, acesse <https://docs.docker.com/docker-for-windows/>.</span><span class="sxs-lookup"><span data-stu-id="0f23d-129">For instructions on setting up Docker for Windows, go to <https://docs.docker.com/docker-for-windows/>.</span></span>
>
><span data-ttu-id="0f23d-130">Para obter instruções sobre como configurar o Docker para Mac, acesse <https://docs.docker.com/docker-for-mac/>.</span><span class="sxs-lookup"><span data-stu-id="0f23d-130">For instructions on setting up Docker for Mac, go to <https://docs.docker.com/docker-for-mac/>.</span></span>

<span data-ttu-id="0f23d-131">Além disso, você precisará de um editor de código para que possa desenvolver o aplicativo enquanto estiver usando a CLI do Docker.</span><span class="sxs-lookup"><span data-stu-id="0f23d-131">In addition, you'll need a code editor so that you can actually develop your application while using Docker CLI.</span></span>

<span data-ttu-id="0f23d-132">A Microsoft fornece o Visual Studio Code, que é um editor de código leve com suporte no Mac, no Windows e no Linux, além do IntelliSense com [suporte para várias linguagens](https://code.visualstudio.com/docs/languages/overview) (JavaScript, .NET, Go, Java, Ruby, Python e a maioria das linguagens modernas), [depuração](https://code.visualstudio.com/Docs/editor/debugging), [integração com Git](https://code.visualstudio.com/Docs/editor/versioncontrol) e [suporte para extensões](https://code.visualstudio.com/docs/extensions/overview).</span><span class="sxs-lookup"><span data-stu-id="0f23d-132">Microsoft provides Visual Studio Code, which is a lightweight code editor that's supported on Mac, Windows, and Linux, and provides IntelliSense with [support for many languages](https://code.visualstudio.com/docs/languages/overview) (JavaScript, .NET, Go, Java, Ruby, Python, and most modern languages), [debugging](https://code.visualstudio.com/Docs/editor/debugging), [integration with Git](https://code.visualstudio.com/Docs/editor/versioncontrol) and [extensions support](https://code.visualstudio.com/docs/extensions/overview).</span></span> <span data-ttu-id="0f23d-133">Esse editor é uma excelente opção para desenvolvedores de Mac e Linux.</span><span class="sxs-lookup"><span data-stu-id="0f23d-133">This editor is a great fit for Mac and Linux developers.</span></span> <span data-ttu-id="0f23d-134">No Windows, também é possível usar o aplicativo do Visual Studio completo.</span><span class="sxs-lookup"><span data-stu-id="0f23d-134">In Windows, you also can use the full Visual Studio application.</span></span>

> [!INFORMAÇÕES]
>
> <span data-ttu-id="0f23d-136">Para obter instruções sobre como instalar o Visual Studio Code para Windows, Mac ou Linux, acesse <https://code.visualstudio.com/docs/setup/setup-overview/>.</span><span class="sxs-lookup"><span data-stu-id="0f23d-136">For instructions on installing Visual Studio Code for Windows, Mac, or Linux, go to <https://code.visualstudio.com/docs/setup/setup-overview/>.</span></span>
>
> <span data-ttu-id="0f23d-137">Para obter instruções sobre como configurar o Docker para Mac, acesse <https://docs.docker.com/docker-for-mac/>.</span><span class="sxs-lookup"><span data-stu-id="0f23d-137">For instructions on setting up Docker for Mac, go to <https://docs.docker.com/docker-for-mac/>.</span></span>

<span data-ttu-id="0f23d-138">Você pode trabalhar com a CLI do Docker e escrever seu código usando qualquer editor de código, mas usar o Visual Studio Code com a extensão do Docker torna mais fácil criar arquivos `Dockerfile` e `docker-compose.yml` em seu workspace.</span><span class="sxs-lookup"><span data-stu-id="0f23d-138">You can work with Docker CLI and write your code using any code editor, but using Visual Studio Code with the Docker extension makes it easy to author `Dockerfile` and `docker-compose.yml` files in your workspace.</span></span> <span data-ttu-id="0f23d-139">Você também pode executar tarefas e scripts do IDE do Visual Studio Code para executar comandos do Docker usando a CLI do Docker abaixo.</span><span class="sxs-lookup"><span data-stu-id="0f23d-139">You can also run tasks and scripts from the Visual Studio Code IDE to execute Docker commands using the Docker CLI underneath.</span></span>

<span data-ttu-id="0f23d-140">A extensão do Docker para o VS Code fornece os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="0f23d-140">The Docker extension for VS Code provides the following features:</span></span>

- <span data-ttu-id="0f23d-141">Geração automática de arquivos `Dockerfile` e `docker-compose.yml`</span><span class="sxs-lookup"><span data-stu-id="0f23d-141">Automatic `Dockerfile` and `docker-compose.yml` file generation</span></span>

- <span data-ttu-id="0f23d-142">Destaque de sintaxe e dicas ao passar o mouse para arquivos `docker-compose.yml` e `Dockerfile`</span><span class="sxs-lookup"><span data-stu-id="0f23d-142">Syntax highlighting and hover tips for `docker-compose.yml` and `Dockerfile` files</span></span>

- <span data-ttu-id="0f23d-143">IntelliSense (preenchimentos) para arquivos `Dockerfile` e `docker-compose.yml`</span><span class="sxs-lookup"><span data-stu-id="0f23d-143">IntelliSense (completions) for `Dockerfile` and `docker-compose.yml` files</span></span>

- <span data-ttu-id="0f23d-144">Linting (erros e avisos) para arquivos `Dockerfile`</span><span class="sxs-lookup"><span data-stu-id="0f23d-144">Linting (errors and warnings) for `Dockerfile` files</span></span>

- <span data-ttu-id="0f23d-145">Integração de paleta de comandos (F1) para os comandos do Docker mais comuns</span><span class="sxs-lookup"><span data-stu-id="0f23d-145">Command Palette (F1) integration for the most common Docker commands</span></span>

- <span data-ttu-id="0f23d-146">Integração do Explorer para gerenciar Imagens e Contêineres</span><span class="sxs-lookup"><span data-stu-id="0f23d-146">Explorer integration for managing Images and Containers</span></span>

- <span data-ttu-id="0f23d-147">Implantar imagens do DockerHub e dos Registros de Contêiner do Azure no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="0f23d-147">Deploy images from DockerHub and Azure Container Registries to Azure App Service</span></span>

<span data-ttu-id="0f23d-148">Para instalar a extensão do Docker, pressione Ctrl + Shift + P, digite `ext install` e, em seguida, execute o comando Instalar Extensão para abrir a lista de extensões do Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0f23d-148">To install the Docker extension, press Ctrl+Shift+P, type `ext install`, and then run the Install Extension command to bring up the Marketplace extension list.</span></span> <span data-ttu-id="0f23d-149">Em seguida, digite **docker** para filtrar os resultados e, então, selecione a extensão Docker Support, conforme ilustrado na Figura 4-23.</span><span class="sxs-lookup"><span data-stu-id="0f23d-149">Next, type **docker** to filter the results, and then select the Docker Support extension, as depicted in Figure 4-23.</span></span>

![Modo de exibição da extensão do Docker para VS Code.](./media/image20.png)

<span data-ttu-id="0f23d-151">**Figura 4-23**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-151">**Figure 4-23**.</span></span> <span data-ttu-id="0f23d-152">Instalando a extensão do Docker no Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0f23d-152">Installing the Docker Extension in Visual Studio Code</span></span>

### <a name="step-2-create-a-dockerfile-related-to-an-existing-image-plain-os-or-dev-environments-like-net-core-nodejs-and-ruby"></a><span data-ttu-id="0f23d-153">Etapa 2: Criar um DockerFile relacionado a uma imagem existente (ambientes de desenvolvimento ou SO sem formatação, como Ruby, Node.js e .NET Core)</span><span class="sxs-lookup"><span data-stu-id="0f23d-153">Step 2: Create a DockerFile related to an existing image (plain OS or dev environments like .NET Core, Node.js, and Ruby)</span></span>

<span data-ttu-id="0f23d-154">Você precisará de um `DockerFile` por imagem personalizada a ser criada e por contêiner a ser implantado.</span><span class="sxs-lookup"><span data-stu-id="0f23d-154">You'll need a `DockerFile` per custom image to be built and per container to be deployed.</span></span> <span data-ttu-id="0f23d-155">Se seu aplicativo for composto por um único serviço personalizado, você precisará de um único `DockerFile`.</span><span class="sxs-lookup"><span data-stu-id="0f23d-155">If your app is made up of a single custom service, you'll need a single `DockerFile`.</span></span> <span data-ttu-id="0f23d-156">No entanto, se o aplicativo for composto por vários serviços (por exemplo, em uma arquitetura de microsserviços), você precisará de um `Dockerfile` por serviço.</span><span class="sxs-lookup"><span data-stu-id="0f23d-156">But if your app is composed of multiple services (as in a microservices architecture), you'll need one `Dockerfile` per service.</span></span>

<span data-ttu-id="0f23d-157">Normalmente, o `DockerFile` é colocado na pasta raiz do aplicativo ou serviço e contém os comandos necessários para que o Docker saiba como configurar e executar esse aplicativo ou serviço.</span><span class="sxs-lookup"><span data-stu-id="0f23d-157">The `DockerFile` is commonly placed in the root folder of your app or service and contains the required commands so that Docker knows how to set up and run that app or service.</span></span> <span data-ttu-id="0f23d-158">Você pode criar seu `DockerFile` e adicioná-lo ao projeto junto com o código (Node.js, .NET Core etc.) ou, se você for novo no ambiente, veja a dica a seguir.</span><span class="sxs-lookup"><span data-stu-id="0f23d-158">You can create your `DockerFile` and add it to your project along with your code (node.js, .NET Core, etc.), or, if you're new to the environment, take a look at the following Tip.</span></span>

> [!TIP]
>
> <span data-ttu-id="0f23d-159">Você pode usar a extensão do Docker para orientá-lo ao usar os arquivos `Dockerfile` e `docker-compose.yml` relacionados a seus contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="0f23d-159">You can use the Docker extension to guide you when using the `Dockerfile` and `docker-compose.yml` files related to your Docker containers.</span></span> <span data-ttu-id="0f23d-160">Eventualmente, você provavelmente gravará esses tipos de arquivos sem essa ferramenta, mas usar a extensão do Docker é um bom ponto de partida que acelerará sua curva de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="0f23d-160">Eventually, you'll probably write these kinds of files without this tool, but using the Docker extension is a good starting point that will accelerate your learning curve.</span></span>

<span data-ttu-id="0f23d-161">Na Figura 4-24, você pode ver como um arquivo docker-compose é adicionado usando a extensão do Docker para VS Code.</span><span class="sxs-lookup"><span data-stu-id="0f23d-161">In Figure 4-24, you can see how a docker-compose file is added by using the Docker Extension for VS Code.</span></span>

![Modo de exibição de console da extensão do Docker para VS Code.](./media/image24.png)

<span data-ttu-id="0f23d-163">**Figura 4-24**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-163">**Figure 4-24**.</span></span> <span data-ttu-id="0f23d-164">Arquivos do Docker adicionados usando o **Adicionar arquivos do Docker ao Workspace**</span><span class="sxs-lookup"><span data-stu-id="0f23d-164">Docker files added using the **Add Docker files to Workspace command**</span></span>

<span data-ttu-id="0f23d-165">Quando adiciona um DockerFile, você especificar qual imagem de base do Docker usará (como usar `FROM mcr.microsoft.com/dotnet/core/aspnet`).</span><span class="sxs-lookup"><span data-stu-id="0f23d-165">When you add a DockerFile, you specify what base Docker image you’ll be using (like using `FROM mcr.microsoft.com/dotnet/core/aspnet`).</span></span> <span data-ttu-id="0f23d-166">Normalmente, você criará sua imagem personalizada usando uma imagem de base que obteve de qualquer repositório oficial no [Registro do Docker Hub](https://hub.docker.com/) (como uma [imagem para .NET Core](https://hub.docker.com/_/microsoft-dotnet-core/) o a imagem [para Node.js](https://hub.docker.com/_/node/)).</span><span class="sxs-lookup"><span data-stu-id="0f23d-166">You'll usually build your custom image on top of a base image that you get from any official repository at the [Docker Hub registry](https://hub.docker.com/) (like an [image for .NET Core](https://hub.docker.com/_/microsoft-dotnet-core/) or the one [for Node.js](https://hub.docker.com/_/node/)).</span></span>

<span data-ttu-id="0f23d-167">***Usar uma imagem do Docker oficial existente***</span><span class="sxs-lookup"><span data-stu-id="0f23d-167">***Use an existing official Docker image***</span></span>

<span data-ttu-id="0f23d-168">Usar um repositório oficial de uma pilha de linguagem com um número de versão garante que recursos da mesma linguagem estejam disponíveis em todos os computadores (incluindo desenvolvimento, teste e produção).</span><span class="sxs-lookup"><span data-stu-id="0f23d-168">Using an official repository of a language stack with a version number ensures that the same language features are available on all machines (including development, testing, and production).</span></span>

<span data-ttu-id="0f23d-169">A seguir, há um DockerFile de exemplo para um contêiner do .NET Core:</span><span class="sxs-lookup"><span data-stu-id="0f23d-169">The following is a sample DockerFile for a .NET Core container:</span></span>

```Dockerfile
# Base Docker image to use  
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
  
# Set the Working Directory and files to be copied to the image  
ARG source  
WORKDIR /app  
COPY ${source:-bin/Release/PublishOutput} .  
  
# Configure the listening port to 80 (Internal/Secured port within Docker host)  
EXPOSE 80  
  
# Application entry point  
ENTRYPOINT ["dotnet", "MyCustomMicroservice.dll"]
```

<span data-ttu-id="0f23d-170">Nesse caso, a imagem é baseada na versão 2.2 da imagem oficial do Docker do ASP.NET Core (com várias arquiteturas para Linux e Windows), de acordo com a linha `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`.</span><span class="sxs-lookup"><span data-stu-id="0f23d-170">In this case, the image is based on version 2.2 of the official ASP.NET Core Docker image (multi-arch for Linux and Windows), as per the line `FROM mcr.microsoft.com/dotnet/core/aspnet:2.2`.</span></span> <span data-ttu-id="0f23d-171">(Para obter mais informações sobre esse tópico, confira a página [Imagem do Docker do ASP.NET Core](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) e a página [Imagem do Docker do .NET Core](https://hub.docker.com/_/microsoft-dotnet-core/)).</span><span class="sxs-lookup"><span data-stu-id="0f23d-171">(For more information about this topic, see the [ASP.NET Core Docker Image](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) page and the [.NET Core Docker Image](https://hub.docker.com/_/microsoft-dotnet-core/) page).</span></span>

<span data-ttu-id="0f23d-172">No DockerFile, você também pode instruir o Docker a escutar na porta TCP que usará em tempo de execução (como a porta 80).</span><span class="sxs-lookup"><span data-stu-id="0f23d-172">In the DockerFile, you can also instruct Docker to listen to the TCP port that you'll use at runtime (such as port 80).</span></span>

<span data-ttu-id="0f23d-173">Você pode especificar mais definições de configurações no Dockerfile, dependendo da linguagem e da estrutura usadas.</span><span class="sxs-lookup"><span data-stu-id="0f23d-173">You can specify additional configuration settings in the Dockerfile, depending on the language and framework you're using.</span></span> <span data-ttu-id="0f23d-174">Por exemplo, a linha `ENTRYPOINT` com `["dotnet", "MySingleContainerWebApp.dll"]` instrui o Docker a executar um aplicativo do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0f23d-174">For instance, the `ENTRYPOINT` line with `["dotnet", "MySingleContainerWebApp.dll"]` tells Docker to run a .NET Core application.</span></span> <span data-ttu-id="0f23d-175">Se você estiver usando o SDK e a CLI do .NET Core (`dotnet CLI`) para criar e executar o aplicativo do .NET, essa configuração será diferente.</span><span class="sxs-lookup"><span data-stu-id="0f23d-175">If you're using the SDK and the .NET Core CLI (`dotnet CLI`) to build and run the .NET application, this setting would be different.</span></span> <span data-ttu-id="0f23d-176">O essencial aqui é que a linha ENTRYPOINT e outras configurações dependem da linguagem e da plataforma que você escolher para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0f23d-176">The key point here is that the ENTRYPOINT line and other settings depend on the language and platform you choose for your application.</span></span>

> [!INFORMAÇÕES]
>
> <span data-ttu-id="0f23d-178">Para obter mais informações sobre a criação de imagens do Docker para aplicativos .NET Core, acesse <https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images>.</span><span class="sxs-lookup"><span data-stu-id="0f23d-178">For more information about building Docker images for .NET Core applications, go to <https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images>.</span></span>
>
> <span data-ttu-id="0f23d-179">Para saber mais sobre como criar suas próprias imagens, acesse <https://docs.docker.com/engine/tutorials/dockerimages/>.</span><span class="sxs-lookup"><span data-stu-id="0f23d-179">To learn more about building your own images, go to <https://docs.docker.com/engine/tutorials/dockerimages/>.</span></span>

<span data-ttu-id="0f23d-180">**Usar repositórios de imagens com várias arquiteturas**</span><span class="sxs-lookup"><span data-stu-id="0f23d-180">**Use multi-arch image repositories**</span></span>

<span data-ttu-id="0f23d-181">Um único nome de imagem em um repositório pode conter variantes de plataforma, como uma imagem do Linux e uma imagem do Windows.</span><span class="sxs-lookup"><span data-stu-id="0f23d-181">A single image name in a repo can contain platform variants, such as a Linux image and a Windows image.</span></span> <span data-ttu-id="0f23d-182">Esse recurso permite que fornecedores como a Microsoft (criadores de imagem base) criem um único repositório para abranger várias plataformas (ou seja, Linux e Windows).</span><span class="sxs-lookup"><span data-stu-id="0f23d-182">This feature allows vendors like Microsoft (base image creators) to create a single repo to cover multiple platforms (that is, Linux and Windows).</span></span> <span data-ttu-id="0f23d-183">Por exemplo, o repositório [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/), disponível no registro do Docker Hub, é compatível com Linux e Windows Nano Server usando o mesmo nome de imagem.</span><span class="sxs-lookup"><span data-stu-id="0f23d-183">For example, the [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) repository available in the Docker Hub registry provides support for Linux and Windows Nano Server by using the same image name.</span></span>

<span data-ttu-id="0f23d-184">Efetuar pull da imagem [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) de um host do Windows efetua pull da variante do Windows, enquanto efetuar pull do mesmo nome de imagem de um host Linux efetua pull da variante do Linux.</span><span class="sxs-lookup"><span data-stu-id="0f23d-184">Pulling the [dotnet/core/aspnet](https://hub.docker.com/_/microsoft-dotnet-core-aspnet/) image from a Windows host pulls the Windows variant, whereas pulling the same image name from a Linux host pulls the Linux variant.</span></span>

<span data-ttu-id="0f23d-185">***Criar a imagem base do zero***</span><span class="sxs-lookup"><span data-stu-id="0f23d-185">***Create your base image from scratch***</span></span>

<span data-ttu-id="0f23d-186">Você pode criar sua própria imagem base do Docker do zero, conforme explicado neste [artigo](https://docs.docker.com/engine/userguide/eng-image/baseimages/) do Docker.</span><span class="sxs-lookup"><span data-stu-id="0f23d-186">You can create your own Docker base image from scratch as explained in this [article](https://docs.docker.com/engine/userguide/eng-image/baseimages/) from Docker.</span></span> <span data-ttu-id="0f23d-187">Esse cenário provavelmente não é recomendado para iniciantes no Docker, mas, se você quiser definir os bits específicos de sua própria imagem base, poderá fazer isso.</span><span class="sxs-lookup"><span data-stu-id="0f23d-187">This scenario is probably not the best for you if you're just starting with Docker, but if you want to set the specific bits of your own base image, you can do it.</span></span>

### <a name="step-3-create-your-custom-docker-images-embedding-your-service-in-it"></a><span data-ttu-id="0f23d-188">Etapa 3: Criar suas imagens do Docker personalizadas inserindo seu serviço nelas</span><span class="sxs-lookup"><span data-stu-id="0f23d-188">Step 3: Create your custom Docker images embedding your service in it</span></span>

<span data-ttu-id="0f23d-189">Para cada serviço personalizado que compõe seu aplicativo, você precisará criar uma imagem relacionada.</span><span class="sxs-lookup"><span data-stu-id="0f23d-189">For each custom service that comprises your app, you'll need to create a related image.</span></span> <span data-ttu-id="0f23d-190">Se seu aplicativo for composto por um único serviço ou aplicativo Web, você precisará apenas de uma única imagem.</span><span class="sxs-lookup"><span data-stu-id="0f23d-190">If your app is made up of a single service or web app, you'll need just a single image.</span></span>

> [!NOTE]
>
> <span data-ttu-id="0f23d-191">Ao levar em consideração o "fluxo de trabalho de DevOps de loop externo", as imagens serão criadas por um processo de build automatizado sempre que você efetuar push de seu código-fonte para um repositório Git (integração contínua), portanto, as imagens serão criadas no ambiente global de seu código-fonte.</span><span class="sxs-lookup"><span data-stu-id="0f23d-191">When taking into account the "outer-loop DevOps workflow", the images will be created by an automated build process whenever you push your source code to a Git repository (Continuous Integration), so the images will be created in that global environment from your source code.</span></span>
>
> <span data-ttu-id="0f23d-192">Mas, antes de considerarmos seguir essa rota do loop externo, precisamos garantir que o aplicativo do Docker está funcionando corretamente para que não efetue push de um código que não funciona corretamente para o sistema de controle do código-fonte (Git etc.).</span><span class="sxs-lookup"><span data-stu-id="0f23d-192">But before we consider going to that outer-loop route, we need to ensure that the Docker application is actually working properly so that they don't push code that might not work properly to the source control system (Git, etc.).</span></span>
>
> <span data-ttu-id="0f23d-193">Sendo assim, cada desenvolvedor precisa primeiro realizar todo o processo de loop interno para testar localmente e continuar desenvolvendo até que queiram efetuar push de um recurso ou alteração completa para o sistema de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="0f23d-193">Therefore, each developer first needs to do the entire inner-loop process to test locally and continue developing until they want to push a complete feature or change to the source control system.</span></span>

<span data-ttu-id="0f23d-194">Para criar uma imagem no ambiente local usando o DockerFile, você pode usar o comando docker build, conforme demonstrado na Figura 4-25 (você também pode executar `docker-compose up --build` para aplicativos compostos por vários contêineres/serviços).</span><span class="sxs-lookup"><span data-stu-id="0f23d-194">To create an image in your local environment and using the DockerFile, you can use the docker build command, as demonstrated in Figure 4-25 (you also can run `docker-compose up --build` for applications composed by several containers/services).</span></span>

![Saída do console do build docker-compose, que mostra o progresso do download das imagens.](./media/image25.png)

<span data-ttu-id="0f23d-196">**Figura 4-25**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-196">**Figure 4-25**.</span></span> <span data-ttu-id="0f23d-197">Executando docker build</span><span class="sxs-lookup"><span data-stu-id="0f23d-197">Running docker build</span></span>

<span data-ttu-id="0f23d-198">Opcionalmente, em vez de executar `docker build` diretamente da pasta do projeto, você pode primeiro gerar uma pasta implantável com as bibliotecas .NET necessárias usando o comando run `dotnet publish` e, em seguida, executando `docker build`.</span><span class="sxs-lookup"><span data-stu-id="0f23d-198">Optionally, instead of directly running `docker build` from the project folder, you first can generate a deployable folder with the .NET libraries needed by using the run `dotnet publish` command, and then run `docker build`.</span></span>

<span data-ttu-id="0f23d-199">Este exemplo cria uma imagem do Docker com o nome `cesardl/netcore-webapi-microservice-docker:first` (`:first` é uma marca, como uma versão específica).</span><span class="sxs-lookup"><span data-stu-id="0f23d-199">This example creates a Docker image with the name `cesardl/netcore-webapi-microservice-docker:first` (`:first` is a tag, like a specific version).</span></span> <span data-ttu-id="0f23d-200">Você poderá realizar esta etapa para cada imagem personalizada que precisar criar para o seu aplicativo do Docker composto com vários contêineres.</span><span class="sxs-lookup"><span data-stu-id="0f23d-200">You can take this step for each custom image you need to create for your composed Docker application with several containers.</span></span>

<span data-ttu-id="0f23d-201">Você pode encontrar as imagens existentes no repositório local (seu computador de desenvolvimento) usando o comando docker images, conforme mostrado na Figura 4-26.</span><span class="sxs-lookup"><span data-stu-id="0f23d-201">You can find the existing images in your local repository (your development machine) by using the docker images command, as illustrated in Figure 4-26.</span></span>

![Saída do console do comando docker images, mostrando as imagens existentes.](./media/image26.png)

<span data-ttu-id="0f23d-203">**Figura 4-26**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-203">**Figure 4-26**.</span></span> <span data-ttu-id="0f23d-204">Exibindo imagens existentes usando imagens do Docker</span><span class="sxs-lookup"><span data-stu-id="0f23d-204">Viewing existing images using docker images</span></span>

### <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-composed-docker-app-with-multiple-services"></a><span data-ttu-id="0f23d-205">Etapa 4: Definir os serviços em docker-compose.yml ao criar um aplicativo composto do Docker com vários serviços</span><span class="sxs-lookup"><span data-stu-id="0f23d-205">Step 4: Define your services in docker-compose.yml when building a composed Docker app with multiple services</span></span>

<span data-ttu-id="0f23d-206">Com o arquivo `docker-compose.yml`, você pode definir um conjunto de serviços relacionados para que sejam implantados como um aplicativo composto usando os comandos de implantação explicados na seção sobre a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="0f23d-206">With the `docker-compose.yml` file, you can define a set of related services to be deployed as a composed application with the deployment commands explained in the next step section.</span></span>

<span data-ttu-id="0f23d-207">Crie esse arquivo na pasta principal ou raiz da solução; ele deve ter conteúdo semelhante ao mostrado neste arquivo `docker-compose.yml`:</span><span class="sxs-lookup"><span data-stu-id="0f23d-207">Create that file in your main or root solution folder; it should have content similar to that shown in this `docker-compose.yml` file:</span></span>

```yml
version: '3.4'
services:
  web:
    build: .
    ports:
     - "81:80"
    volumes:
     - .:/code
    depends_on:
     - redis
  redis:
    image: redis
```

<span data-ttu-id="0f23d-208">Nesse caso específico, o arquivo define dois serviços: o serviço Web (seu serviço personalizado) e o serviço Redis (um serviço de cache popular).</span><span class="sxs-lookup"><span data-stu-id="0f23d-208">In this particular case, this file defines two services: the web service (your custom service) and the redis service (a popular cache service).</span></span> <span data-ttu-id="0f23d-209">Cada serviço será implantado como um contêiner, portanto, precisamos usar uma imagem do Docker concreta para cada um.</span><span class="sxs-lookup"><span data-stu-id="0f23d-209">Each service will be deployed as a container, so we need to use a concrete Docker image for each.</span></span> <span data-ttu-id="0f23d-210">Para este serviço Web específico, a imagem precisará fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0f23d-210">For this particular web service, the image will need to do the following:</span></span>

- <span data-ttu-id="0f23d-211">Criar por meio do DockerFile no diretório atual</span><span class="sxs-lookup"><span data-stu-id="0f23d-211">Build from the DockerFile in the current directory</span></span>

- <span data-ttu-id="0f23d-212">Encaminhar a porta 80, exposta no contêiner, para a porta 81, no computador host</span><span class="sxs-lookup"><span data-stu-id="0f23d-212">Forward the exposed port 80 on the container to port 81 on the host machine</span></span>

- <span data-ttu-id="0f23d-213">Montar o diretório do projeto no host em /code dentro do contêiner, possibilitando que você modifique o código sem precisar recompilar a imagem</span><span class="sxs-lookup"><span data-stu-id="0f23d-213">Mount the project directory on the host to /code within the container, making it possible for you to modify the code without having to rebuild the image</span></span>

- <span data-ttu-id="0f23d-214">Vincular o serviço Web ao serviço Redis</span><span class="sxs-lookup"><span data-stu-id="0f23d-214">Link the web service to the redis service</span></span>

<span data-ttu-id="0f23d-215">O serviço Redis usa a [imagem pública do Redis mais recente](https://hub.docker.com/_/redis/) extraída do registro do Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="0f23d-215">The redis service uses the [latest public redis image](https://hub.docker.com/_/redis/) pulled from the Docker Hub registry.</span></span> <span data-ttu-id="0f23d-216">[redis](https://redis.io/) é um sistema de cache popular para aplicativos do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="0f23d-216">[redis](https://redis.io/) is a popular cache system for server-side applications.</span></span>

### <a name="step-5-build-and-run-your-docker-app"></a><span data-ttu-id="0f23d-217">Etapa 5: Criar e executar seu aplicativo do Docker</span><span class="sxs-lookup"><span data-stu-id="0f23d-217">Step 5: Build and run your Docker app</span></span>

<span data-ttu-id="0f23d-218">Se seu aplicativo tiver apenas um contêiner, você precisará apenas executá-lo implantando-o no host do Docker (VM ou servidor físico).</span><span class="sxs-lookup"><span data-stu-id="0f23d-218">If your app has only a single container, you just need to run it by deploying it to your Docker Host (VM or physical server).</span></span> <span data-ttu-id="0f23d-219">No entanto, se o aplicativo for composto por vários serviços, você também precisará *compô-lo*.</span><span class="sxs-lookup"><span data-stu-id="0f23d-219">However, if your app is made up of multiple services, you need to *compose it*, too.</span></span> <span data-ttu-id="0f23d-220">Vejamos as diferentes opções.</span><span class="sxs-lookup"><span data-stu-id="0f23d-220">Let's see the different options.</span></span>

<span data-ttu-id="0f23d-221">***Opção A: Executar um único contêiner ou serviço***</span><span class="sxs-lookup"><span data-stu-id="0f23d-221">***Option A: Run a single container or service***</span></span>

<span data-ttu-id="0f23d-222">Você pode executar a imagem do Docker usando o comando docker run, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="0f23d-222">You can run the Docker image by using the docker run command, as shown here:</span></span>

```console
docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

<span data-ttu-id="0f23d-223">Para essa implantação específica, redirecionaremos as solicitações enviadas à porta 80 para a porta 5000 interna.</span><span class="sxs-lookup"><span data-stu-id="0f23d-223">For this particular deployment, we'll be redirecting requests sent to port 80 to the internal port 5000.</span></span> <span data-ttu-id="0f23d-224">Agora, o aplicativo está escutando na porta 80 externa no nível do host.</span><span class="sxs-lookup"><span data-stu-id="0f23d-224">Now the application is listening on the external port 80 at the host level.</span></span>

<span data-ttu-id="0f23d-225">***Opção B: Compor e executar um aplicativo de vários contêineres***</span><span class="sxs-lookup"><span data-stu-id="0f23d-225">***Option B: Compose and run a multiple-container application***</span></span>

<span data-ttu-id="0f23d-226">Na maioria dos cenários empresariais, um aplicativo do Docker será composto por vários serviços.</span><span class="sxs-lookup"><span data-stu-id="0f23d-226">In most enterprise scenarios, a Docker application will be composed of multiple services.</span></span> <span data-ttu-id="0f23d-227">Nesses casos, você pode executar o comando `docker-compose up` (Figura 4-27), que usará o arquivo docker-compose.yml, que talvez tenha criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0f23d-227">For these cases, you can run the `docker-compose up` command (Figure 4-27), which will use the docker-compose.yml file that you might have created previously.</span></span> <span data-ttu-id="0f23d-228">Executar esse comando implanta um aplicativo composto com todos os contêineres relacionados.</span><span class="sxs-lookup"><span data-stu-id="0f23d-228">Running this command deploys a composed application with all of its related containers.</span></span>

![Saída de console do comando docker-compose up.](./media/image27.png)

<span data-ttu-id="0f23d-230">**Figura 4-27**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-230">**Figure 4-27**.</span></span> <span data-ttu-id="0f23d-231">Resultados da execução do comando "docker-compose up"</span><span class="sxs-lookup"><span data-stu-id="0f23d-231">Results of running the "docker-compose up" command</span></span>

<span data-ttu-id="0f23d-232">Depois de executar `docker-compose up`, implante seu aplicativo e os contêineres relacionados no Host do Docker, conforme ilustrado na Figura 4-28, na representação da VM.</span><span class="sxs-lookup"><span data-stu-id="0f23d-232">After you run `docker-compose up`, you deploy your application and its related container(s) into your Docker Host, as illustrated in Figure 4-28, in the VM representation.</span></span>

![VM executando aplicativos de vários contêineres.](./media/image28.png)

<span data-ttu-id="0f23d-234">**Figura 4-28**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-234">**Figure 4-28**.</span></span> <span data-ttu-id="0f23d-235">VM com contêineres do Docker implantados</span><span class="sxs-lookup"><span data-stu-id="0f23d-235">VM with Docker containers deployed</span></span>

### <a name="step-6-test-your-docker-application-locally-in-your-local-cd-vm"></a><span data-ttu-id="0f23d-236">Etapa 6: Testar seu aplicativo do Docker (localmente, na VM de CD local)</span><span class="sxs-lookup"><span data-stu-id="0f23d-236">Step 6: Test your Docker application (locally, in your local CD VM)</span></span>

<span data-ttu-id="0f23d-237">Esta etapa varia de acordo com o que seu aplicativo está fazendo.</span><span class="sxs-lookup"><span data-stu-id="0f23d-237">This step will vary depending on what your app is doing.</span></span>

<span data-ttu-id="0f23d-238">Em um simples "Olá, Mundo" da API Web do .NET Core implantado como um único contêiner ou serviço, você precisará apenas acessar o serviço fornecendo a porta TCP especificada no DockerFile.</span><span class="sxs-lookup"><span data-stu-id="0f23d-238">In a simple .NET Core Web API "Hello World" deployed as a single container or service, you'd just need to access the service by providing the TCP port specified in the DockerFile.</span></span>

<span data-ttu-id="0f23d-239">Se o localhost não estiver ativado, para navegar até seu serviço, localize o endereço IP do computador usando este comando:</span><span class="sxs-lookup"><span data-stu-id="0f23d-239">If localhost is not turned on, to navigate to your service, find the IP address for the machine by using this command:</span></span>

```console
docker-machine {IP} {YOUR-CONTAINER-NAME}
```

<span data-ttu-id="0f23d-240">No host do Docker, abra um navegador e navegue até esse site. Você deverá ver seu aplicativo/serviço em execução, conforme demonstrado na Figura 4-29.</span><span class="sxs-lookup"><span data-stu-id="0f23d-240">On the Docker host, open a browser and navigate to that site; you should see your app/service running, as demonstrated in Figure 4-29.</span></span>

![Modo de exibição de navegador da resposta de localhost/API/ valores.](./media/image29.png)

<span data-ttu-id="0f23d-242">**Figura 4-29**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-242">**Figure 4-29**.</span></span> <span data-ttu-id="0f23d-243">Testando seu aplicativo do Docker localmente usando localhost</span><span class="sxs-lookup"><span data-stu-id="0f23d-243">Testing your Docker application locally using localhost</span></span>

<span data-ttu-id="0f23d-244">Observe que ele está usando a porta 80, mas internamente está sendo redirecionado para a porta 5000, pois é como ele foi implantado com `docker run`, conforme explicado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0f23d-244">Note that it's using port 80, but internally it's being redirected to port 5000, because that's how it was deployed with `docker run`, as explained earlier.</span></span>

<span data-ttu-id="0f23d-245">Isso pode ser testado usando o CURL no terminal.</span><span class="sxs-lookup"><span data-stu-id="0f23d-245">You can test this by using CURL from the terminal.</span></span> <span data-ttu-id="0f23d-246">Em uma instalação do Docker no Windows, o IP padrão é 10.0.75.1, conforme ilustrado na Figura 4-30.</span><span class="sxs-lookup"><span data-stu-id="0f23d-246">In a Docker installation on Windows, the default IP is 10.0.75.1, as depicted in Figure 4-30.</span></span>

![Saída do console ao obter o http://10.0.75.1/API/values com cURL](./media/image30.png)

<span data-ttu-id="0f23d-248">**Figura 4-30**.</span><span class="sxs-lookup"><span data-stu-id="0f23d-248">**Figure 4-30**.</span></span> <span data-ttu-id="0f23d-249">Testando um aplicativo do Docker localmente usando CURL</span><span class="sxs-lookup"><span data-stu-id="0f23d-249">Testing a Docker application locally by using CURL</span></span>

<span data-ttu-id="0f23d-250">**Depurando um contêiner em execução no Docker**</span><span class="sxs-lookup"><span data-stu-id="0f23d-250">**Debugging a container running on Docker**</span></span>

<span data-ttu-id="0f23d-251">O Visual Studio Code dá suporte à depuração do Docker quando você está usando Node.js e outras plataformas, como contêineres do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0f23d-251">Visual Studio Code supports debugging Docker if you're using Node.js and other platforms like .NET Core containers.</span></span>

<span data-ttu-id="0f23d-252">Você também pode depurar contêineres do .NET Core ou .NET Framework no Docker ao usar o Visual Studio para Windows ou Mac, conforme descrito na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="0f23d-252">You also can debug .NET Core or .NET Framework containers in Docker when using Visual Studio for Windows or Mac, as described in the next section.</span></span>

> [!INFORMAÇÕES]
>
> <span data-ttu-id="0f23d-254">Para saber mais sobre a depuração de contêineres do Docker do Node.js, acesse <https://blog.docker.com/2016/07/live-debugging-docker/> e <https://blogs.msdn.microsoft.com/user_ed/2016/02/27/visual-studio-code-new-features-13-big-debugging-updates-rich-object-hover-conditional-breakpoints-node-js-mono-more/>.</span><span class="sxs-lookup"><span data-stu-id="0f23d-254">To learn more about debugging Node.js Docker containers, go to <https://blog.docker.com/2016/07/live-debugging-docker/> and <https://blogs.msdn.microsoft.com/user_ed/2016/02/27/visual-studio-code-new-features-13-big-debugging-updates-rich-object-hover-conditional-breakpoints-node-js-mono-more/>.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="0f23d-255">[Anterior](docker-apps-development-environment.md)
>[Próximo](visual-studio-tools-for-docker.md)</span><span class="sxs-lookup"><span data-stu-id="0f23d-255">[Previous](docker-apps-development-environment.md)
[Next](visual-studio-tools-for-docker.md)</span></span>