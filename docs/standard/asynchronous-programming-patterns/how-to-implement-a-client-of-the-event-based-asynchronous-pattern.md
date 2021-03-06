---
title: 'Como: Implementar um cliente do padrão assíncrono baseado em evento'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- components [.NET Framework], asynchronous
- AsyncOperation class
- threading [Windows Forms], asynchronous features
- AsyncCompletedEventArgs class
ms.assetid: 21a858c1-3c99-4904-86ee-0d17b49804fa
ms.openlocfilehash: d0253745d4d2ee90f355364ed1b1b0d9b74d0fc1
ms.sourcegitcommit: b78018c850590dfc0348301e1748b779c28604cc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "89379181"
---
# <a name="how-to-implement-a-client-of-the-event-based-asynchronous-pattern"></a>Como: Implementar um cliente do padrão assíncrono baseado em evento
O código a seguir descreve como usar um componente que respeita a [Visão geral do Padrão assíncrono baseado em evento](event-based-asynchronous-pattern-overview.md). O formulário desse exemplo usa o componente `PrimeNumberCalculator` descrito em [Como: implementar um componente compatível com o Padrão assíncrono baseado em evento](component-that-supports-the-event-based-asynchronous-pattern.md).  
  
 Quando você executa um projeto que usa este exemplo, você verá um formulário de "Calculadora de números primos" com uma grade e dois botões: **Iniciar Nova Tarefa** e **Cancelar**. Você pode clicar no botão **Iniciar Nova Tarefa** várias vezes consecutivas e, para cada clique, uma operação assíncrona iniciará uma computação para determinar se um número gerado aleatoriamente é primo. O formulário exibirá periodicamente o progresso e os resultados incrementais. Cada operação recebe uma ID de tarefa exclusiva. O resultado da computação é exibido na coluna **Resultado**. Se o número do teste não for primo, ele será rotulado como **Composto** e seu primeiro divisor será exibido.  
  
 Todas as operações pendentes podem ser canceladas com o botão **Cancelar**. Várias seleções podem ser feitas.  
  
> [!NOTE]
> A maioria dos números não será primo. Se não tiver encontrado um número primo após várias operações concluídas, inicie mais tarefas e, eventualmente, você encontrará alguns números primos.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[System.ComponentModel.AsyncOperationManager#10](snippets/component-that-supports-the-event-based-asynchronous-pattern/csharp/primenumbercalculatormain.cs#10)]
 [!code-vb[System.ComponentModel.AsyncOperationManager#10](snippets/component-that-supports-the-event-based-asynchronous-pattern/vb/primenumbercalculatormain.vb#10)]  
  
## <a name="see-also"></a>Confira também

- <xref:System.ComponentModel.AsyncOperation>
- <xref:System.ComponentModel.AsyncOperationManager>
- <xref:System.Windows.Forms.WindowsFormsSynchronizationContext>
