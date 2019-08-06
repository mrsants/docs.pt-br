---
title: Noções básicas de criação de contêiner comum
description: 'Aprenda um princípio fundamental do bom design de contêineres: um contêiner deve hospedar apenas um processo.'
ms.date: 02/15/2019
ms.openlocfilehash: 69f3ff6c9303f0c4082695d861a8c90031295b6a
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68672493"
---
# <a name="common-container-design-principles"></a><span data-ttu-id="27619-103">Noções básicas de criação de contêiner comum</span><span class="sxs-lookup"><span data-stu-id="27619-103">Common container design principles</span></span>

<span data-ttu-id="27619-104">Antes de entrarmos no processo de desenvolvimento, há alguns conceitos básicos que vale a pena mencionar com relação a como você pode usar contêineres.</span><span class="sxs-lookup"><span data-stu-id="27619-104">Ahead of getting into the development process there are a few basic concepts worth mentioning with regard to how you use containers.</span></span>

## <a name="container-equals-a-process"></a><span data-ttu-id="27619-105">Um contêiner é igual a um processo</span><span class="sxs-lookup"><span data-stu-id="27619-105">Container equals a process</span></span>

<span data-ttu-id="27619-106">No modelo de contêiner, um contêiner representa um único processo.</span><span class="sxs-lookup"><span data-stu-id="27619-106">In the container model, a container represents a single process.</span></span> <span data-ttu-id="27619-107">Definindo um contêiner como um limite de processo, você começa a criar os primitivos usados para dimensionar ou agrupar os processos em lotes.</span><span class="sxs-lookup"><span data-stu-id="27619-107">By defining a container as a process boundary, you begin to create the primitives used to scale, or batch-off, processes.</span></span> <span data-ttu-id="27619-108">Quando executar um contêiner do Docker, você verá uma definição [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint).</span><span class="sxs-lookup"><span data-stu-id="27619-108">When you run a Docker container, you'll see an [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#/entrypoint) definition.</span></span> <span data-ttu-id="27619-109">Ela define o processo e o tempo de vida do contêiner.</span><span class="sxs-lookup"><span data-stu-id="27619-109">This defines the process and the lifetime of the container.</span></span> <span data-ttu-id="27619-110">Quando o processo for concluído, o ciclo de vida do contêiner será encerrado.</span><span class="sxs-lookup"><span data-stu-id="27619-110">When the process completes, the container life-cycle ends.</span></span> <span data-ttu-id="27619-111">Há processos de longa execução, como servidores Web, e processos de curta duração, como trabalhos em lotes, que podem ter sido implementados como Microsoft Azure [WebJobs](https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/).</span><span class="sxs-lookup"><span data-stu-id="27619-111">There are long-running processes, such as web servers, and short-lived processes, such as batch jobs, which might have been implemented as Microsoft Azure [WebJobs](https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/).</span></span> <span data-ttu-id="27619-112">Se o processo falhar, o contêiner é encerrado e o orquestrador assume.</span><span class="sxs-lookup"><span data-stu-id="27619-112">If the process fails, the container ends, and the orchestrator takes over.</span></span> <span data-ttu-id="27619-113">Se o orquestrador foi instruído a manter cinco instâncias em execução e uma falhar, ele criará outro contêiner para substituir o processo com falha.</span><span class="sxs-lookup"><span data-stu-id="27619-113">If the orchestrator was instructed to keep five instances running and one fails, the orchestrator will create another container to replace the failed process.</span></span> <span data-ttu-id="27619-114">Em um trabalho em lotes, o processo é iniciado com parâmetros.</span><span class="sxs-lookup"><span data-stu-id="27619-114">In a batch job, the process is started with parameters.</span></span> <span data-ttu-id="27619-115">Quando o processo é concluído, o trabalho é concluído.</span><span class="sxs-lookup"><span data-stu-id="27619-115">When the process completes, the work is complete.</span></span>

<span data-ttu-id="27619-116">Você pode encontrar um cenário em que deseje vários processos em execução em um único contêiner.</span><span class="sxs-lookup"><span data-stu-id="27619-116">You might find a scenario in which you want multiple processes running in a single container.</span></span> <span data-ttu-id="27619-117">Em qualquer documento de arquitetura, nunca há um "nunca" e nem sempre há um "sempre".</span><span class="sxs-lookup"><span data-stu-id="27619-117">In any architecture document, there's never a "never," nor is there always an "always."</span></span> <span data-ttu-id="27619-118">Para cenários que exigem vários processos, um padrão comum é usar o [Supervisor](http://supervisord.org/).</span><span class="sxs-lookup"><span data-stu-id="27619-118">For scenarios requiring multiple processes, a common pattern is to use [Supervisor](http://supervisord.org/).</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="27619-119">[Anterior](design-docker-applications.md)
>[Próximo](monolithic-applications.md)</span><span class="sxs-lookup"><span data-stu-id="27619-119">[Previous](design-docker-applications.md)
[Next](monolithic-applications.md)</span></span>