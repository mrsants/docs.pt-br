---
title: Expressões lambda-referência C#
description: Saiba mais sobre expressões lambda. Há lambdas de expressão que têm uma expressão como seu corpo, ou lambdas de instrução que têm um bloco de instrução como seu corpo.
ms.date: 09/25/2020
helpviewer_keywords:
- lambda expressions [C#]
- outer variables [C#]
- statement lambda [C#]
- expression lambda [C#]
- expressions [C#], lambda
ms.assetid: 57e3ba27-9a82-4067-aca7-5ca446b7bf93
ms.openlocfilehash: a3a753ccea45193c57f31453d7318c14f4898864
ms.sourcegitcommit: c04535ad05e374fb269fcfc6509217755fbc0d54
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91247703"
---
# <a name="lambda-expressions-c-reference"></a>Expressões lambda (referência C#)

Uma *expressão lambda* é uma expressão de uma das duas seguintes formas:

- [Expressão lambda](#expression-lambdas) que tem uma expressão como corpo:

  ```csharp
  (input-parameters) => expression
  ```

- [Instrução lambda](#statement-lambdas) que tem um bloco de instrução como corpo:

  ```csharp  
  (input-parameters) => { <sequence-of-statements> }
  ```

Use o [operador de declaração lambda `=>`](lambda-operator.md) para separar a lista de parâmetros de lambda do corpo. Para criar uma expressão lambda, especifique os parâmetros de entrada (se houver) no lado esquerdo do operador lambda e uma expressão ou um bloco de instrução do outro lado.

Qualquer expressão lambda pode ser convertida para um tipo [delegado](../builtin-types/reference-types.md#the-delegate-type). O tipo delegado no qual uma expressão lambda pode ser convertida é definido pelos tipos de parâmetros e pelo valor retornado. Se uma expressão lambda não retornar um valor, ela poderá ser convertida em um dos tipos delegados `Action`; caso contrário, ela poderá ser convertida em um dos tipos delegados `Func`. Por exemplo, uma expressão lambda que tem dois parâmetros e não retorna nenhum valor pode ser convertida em um delegado <xref:System.Action%602>. Uma expressão lambda que tem um parâmetro e retorna um valor pode ser convertida em um delegado <xref:System.Func%602>. No exemplo a seguir, a expressão lambda `x => x * x` , que especifica um parâmetro denominado `x` e retorna o valor de `x` quadrado, é atribuída a uma variável de um tipo delegado:

[!code-csharp-interactive[lambda is delegate](snippets/lambda-expressions/Introduction.cs#Delegate)]

As lambdas de expressão também podem ser convertidas para os tipos de [árvore de expressão](../../programming-guide/concepts/expression-trees/index.md) , como mostra o exemplo a seguir:

[!code-csharp-interactive[lambda is expression tree](snippets/lambda-expressions/Introduction.cs#ExpressionTree)]

Use expressões lambda em qualquer código que exija instâncias de tipos delegados ou árvores de expressão, por exemplo, como um argumento ao método <xref:System.Threading.Tasks.Task.Run(System.Action)?displayProperty=nameWithType> para passar o código que deve ser executado em segundo plano. Você também pode usar expressões lambda ao escrever [LINQ em C#](../../linq/index.md), como mostra o exemplo a seguir:

[!code-csharp-interactive[lambda is argument in LINQ](snippets/lambda-expressions/Introduction.cs#Argument)]

Quando você usa a sintaxe baseada em método para chamar o método <xref:System.Linq.Enumerable.Select%2A?displayProperty=nameWithType> na classe <xref:System.Linq.Enumerable?displayProperty=nameWithType>, por exemplo, no LINQ to Objects e no LINQ to XML, o parâmetro é um tipo delegado <xref:System.Func%602?displayProperty=nameWithType>. Quando você chama o <xref:System.Linq.Queryable.Select%2A?displayProperty=nameWithType> método na <xref:System.Linq.Queryable?displayProperty=nameWithType> classe, por exemplo, em LINQ to SQL, o tipo de parâmetro é um tipo de árvore de expressão [`Expression<Func<TSource,TResult>>`](<xref:System.Linq.Expressions.Expression%601>) . Em ambos os casos, você pode usar a mesma expressão lambda para especificar o valor do parâmetro. Isso faz com que as duas chamadas `Select` pareçam semelhantes, embora, na verdade, o tipo de objetos criado dos lambdas seja diferente.
  
## <a name="expression-lambdas"></a>Lambdas de expressão

Uma expressão lambda com uma expressão no lado direito do operador `=>` é chamada de *lambda de expressão*. Uma expressão lambda retorna o resultado da expressão e tem o seguinte formato básico:

```csharp
(input-parameters) => expression
```

O corpo de um lambda de expressão pode consistir em uma chamada de método. No entanto, se você estiver criando [árvores de expressão](../../programming-guide/concepts/expression-trees/index.md) que são avaliadas fora do contexto do Common Language Runtime do .net, como no SQL Server, você não deve usar chamadas de método em expressões lambda. Os métodos não terão significado fora do contexto do .NET Common Language Runtime.

## <a name="statement-lambdas"></a>Lambdas de instrução

Uma instrução lambda é semelhante a uma expressão lambda, exceto que suas instruções são colocadas entre chaves:

```csharp  
(input-parameters) => { <sequence-of-statements> }
```

O corpo de uma instrução lambda pode consistir de qualquer número de instruções; no entanto, na prática, normalmente não há mais de duas ou três.

:::code language="csharp" interactive="try-dotnet-method" source="snippets/lambda-expressions/GeneralExamples.cs" id="SnippetStatementLambda":::

Você não pode usar lambdas de instrução para criar árvores de expressão.

## <a name="input-parameters-of-a-lambda-expression"></a>Parâmetros de entrada de uma expressão lambda

Você coloca os parâmetros de entrada de uma expressão lambda entre parênteses. Especifique parâmetros de entrada zero com parênteses vazios:  

:::code language="csharp" source="snippets/lambda-expressions/GeneralExamples.cs" id="SnippetZeroParameters":::

Se uma expressão lambda tiver apenas um parâmetro de entrada, os parênteses serão opcionais:

:::code language="csharp" source="snippets/lambda-expressions/GeneralExamples.cs" id="SnippetOneParameter":::

Dois ou mais parâmetros de entrada são separados por vírgulas:

:::code language="csharp" source="snippets/lambda-expressions/GeneralExamples.cs" id="SnippetTwoParameters":::

Às vezes, o compilador não pode inferir os tipos de parâmetros de entrada. Você pode especificar os tipos de maneira explícita conforme mostrado neste exemplo:

:::code language="csharp" source="snippets/lambda-expressions/GeneralExamples.cs" id="SnippetExplicitlyTypedParameters":::

Os tipos de parâmetro de entrada devem ser todos explícitos ou implícitos; caso contrário, ocorrerá o erro [CS0748](../../misc/cs0748.md) de compilador.

A partir do C# 9,0, você pode usar os [Descartes](../../discards.md) para especificar dois ou mais parâmetros de entrada de uma expressão lambda que não são usados na expressão:

:::code language="csharp" source="snippets/lambda-expressions/GeneralExamples.cs" id="SnippetDiscards":::

Os parâmetros de descarte lambda podem ser úteis quando você usa uma expressão lambda para [fornecer um manipulador de eventos](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).

> [!NOTE]
> Para compatibilidade com versões anteriores, se apenas um único parâmetro de entrada for nomeado `_` , em seguida, dentro de uma expressão lambda, `_` será tratado como o nome desse parâmetro.

## <a name="async-lambdas"></a>Lambdas assíncronos

Você pode facilmente criar expressões e instruções lambda que incorporem processamento assíncrono, ao usar as palavras-chaves [async](../keywords/async.md) e [await](await.md). Por exemplo, o exemplo do Windows Forms a seguir contém um manipulador de eventos que chama e espera um método assíncrono `ExampleMethodAsync`.

```csharp
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
        button1.Click += button1_Click;
    }

    private async void button1_Click(object sender, EventArgs e)
    {
        await ExampleMethodAsync();
        textBox1.Text += "\r\nControl returned to Click event handler.\n";
    }

    private async Task ExampleMethodAsync()
    {
        // The following line simulates a task-returning asynchronous process.
        await Task.Delay(1000);
    }
}
```

Você pode adicionar o mesmo manipulador de eventos ao usar um lambda assíncrono. Para adicionar esse manipulador, adicione um modificador `async` antes da lista de parâmetros lambda, como mostra o exemplo a seguir:

```csharp
public partial class Form1 : Form
{
    public Form1()
    {
        InitializeComponent();
        button1.Click += async (sender, e) =>
        {
            await ExampleMethodAsync();
            textBox1.Text += "\r\nControl returned to Click event handler.\n";
        };
    }

    private async Task ExampleMethodAsync()
    {
        // The following line simulates a task-returning asynchronous process.
        await Task.Delay(1000);
    }
}
```

Para obter mais informações sobre como criar e usar métodos assíncronos, consulte [programação assíncrona com Async e Await](../../programming-guide/concepts/async/index.md).

## <a name="lambda-expressions-and-tuples"></a>Expressões lambda e tuplas

A partir do C# 7.0, a linguagem C# fornece suporte interno para [tuplas](../builtin-types/value-tuples.md). Você pode fornecer uma tupla como um argumento para uma expressão lambda e a expressão lambda também pode retornar uma tupla. Em alguns casos, o compilador do C# usa a inferência de tipos para determinar os tipos dos componentes da tupla.

Você pode definir uma tupla, colocando entre parênteses uma lista delimitada por vírgulas de seus componentes. O exemplo a seguir usa a tupla com três componentes para passar uma sequência de números para uma expressão lambda, que dobra cada valor e retorna uma tupla com três componentes que contém o resultado das multiplicações.

[!code-csharp-interactive[lambda and tuples](snippets/lambda-expressions/LambdasAndTuples.cs#WithoutComponentName)]

Normalmente, os campos de uma tupla são nomeados `Item1` , `Item2` etc. No entanto, você pode definir uma tupla com componentes nomeados, como faz o exemplo a seguir.

[!code-csharp-interactive[lambda and named tuples](snippets/lambda-expressions/LambdasAndTuples.cs#WithComponentName)]

Para obter mais informações sobre tuplas C#, consulte [tipos de tupla](../../language-reference/builtin-types/value-tuples.md).

## <a name="lambdas-with-the-standard-query-operators"></a>Lambdas com os operadores de consulta padrão

O LINQ to Objects, entre outras implementações, tem um parâmetro de entrada cujo tipo faz parte da família de delegados genéricos <xref:System.Func%601>. Esses delegados usam parâmetros de tipo para definir o número e o tipo de parâmetros de entrada e o tipo de retorno do delegado. delegados `Func` são muito úteis para encapsular expressões definidas pelo usuário aplicadas a cada elemento em um conjunto de dados de origem. Por exemplo, considere o seguinte tipo delegado <xref:System.Func%602>:  

```csharp
public delegate TResult Func<in T, out TResult>(T arg)
```

O delegado pode ser instanciado como um `Func<int, bool>`, em que `int` é um parâmetro de entrada e `bool` é o valor de retorno. O valor de retorno é sempre especificado no último parâmetro de tipo. Por exemplo, `Func<int, string, bool>` define um delegado com dois parâmetros de entrada, `int` e `string`, e um tipo de retorno de `bool`. O delegado `Func` a seguir, quando é invocado, retornará um valor booliano que indica se o parâmetro de entrada é ou não igual a cinco:

[!code-csharp-interactive[Func example](snippets/lambda-expressions/LambdasWithQueryMethods.cs#Func)]

Você também pode fornecer uma expressão lambda quando o tipo de argumento é um <xref:System.Linq.Expressions.Expression%601>. Por exemplo, nos operadores de consulta padrão que são definidos no tipo <xref:System.Linq.Queryable>. Quando você especifica um argumento <xref:System.Linq.Expressions.Expression%601>, o lambda é compilado em uma árvore de expressão.
  
O exemplo a seguir usa o operador padrão de consulta <xref:System.Linq.Enumerable.Count%2A>:

[!code-csharp-interactive[Count example](snippets/lambda-expressions/LambdasWithQueryMethods.cs#Count)]

O compilador pode inferir o tipo de parâmetro de entrada ou você também pode especificá-lo explicitamente. Essa expressão lambda em particular conta esses inteiros (`n`) que, quando dividida por dois, tem um resto 1.

O exemplo a seguir gera uma sequência que contém todos os elementos da matriz `numbers` que precedem o 9, porque esse é o primeiro número na sequência que não satisfaz a condição:

[!code-csharp-interactive[TakeWhile example](snippets/lambda-expressions/LambdasWithQueryMethods.cs#TakeWhile)]

O exemplo a seguir especifica vários parâmetros de entrada, colocando-os entre parênteses. O método retorna todos os elementos na matriz `numbers` até encontrar um número cujo valor seja inferior à sua posição ordinal na matriz:

[!code-csharp-interactive[TakeWhile example 2](snippets/lambda-expressions/LambdasWithQueryMethods.cs#TakeWhileWithIndex)]

## <a name="type-inference-in-lambda-expressions"></a>Inferência de tipos em expressões lambda

Ao escrever lambdas, você geralmente não precisa especificar um tipo para os parâmetros de entrada porque o compilador pode inferir o tipo com base no corpo do lambda, nos tipos de parâmetro e em outros fatores, conforme descrito na especificação da linguagem C#. Para a maioria dos operadores de consulta padrão, a primeira entrada é o tipo dos elementos na sequência de origem. Se você estiver consultando um `IEnumerable<Customer>`, a variável de entrada será inferida para ser um objeto `Customer`, o que significa que você terá acesso aos seus métodos e propriedades:  

```csharp
customers.Where(c => c.City == "London");
```

As regras gerais para a inferência de tipos para lambdas são as seguintes:

- O lambda deve conter o mesmo número de parâmetros do tipo delegado.

- Cada parâmetro de entrada no lambda deve ser implicitamente conversível em seu parâmetro delegado correspondente.

- O valor de retorno do lambda (se houver) deve ser implicitamente conversível para o tipo de retorno do delegado.
  
Observe que as expressões lambda em si não têm um tipo porque o sistema de tipo comum não possui nenhum conceito intrínseco de "expressão lambda." No entanto, às vezes é conveniente falar informalmente do "tipo" de uma expressão lambda. Nesses casos, o tipo se refere ao tipo delegado ou tipo <xref:System.Linq.Expressions.Expression> ao qual a expressão lambda é convertida.

## <a name="capture-of-outer-variables-and-variable-scope-in-lambda-expressions"></a>Captura de variáveis externas e escopo variável em expressões lambda

Os lambdas pode fazer referência a *variáveis externas*. Essas são as variáveis que estão no escopo do método que define a expressão lambda ou no escopo do tipo que contém a expressão lambda. As variáveis que são capturadas dessa forma são armazenadas para uso na expressão lambda mesmo que de alguma outra forma elas saíssem do escopo e fossem coletadas como lixo. Uma variável externa deve ser definitivamente atribuída para que possa ser consumida em uma expressão lambda. O exemplo a seguir demonstra estas regras:

[!code-csharp[variable scope](snippets/lambda-expressions/VariableScopeWithLambdas.cs#VariableScope)]

As seguintes regras se aplicam ao escopo variável em expressões lambda:  

- Uma variável capturada não será coletada do lixo até que o delegado que faz referência a ela se qualifique para coleta de lixo.

- As variáveis introduzidas em uma expressão lambda não são visíveis no método delimitador.

- Uma expressão lambda não pode capturar um parâmetro [in](../keywords/in-parameter-modifier.md), [ref](../keywords/ref.md) ou [out](../keywords/out-parameter-modifier.md) diretamente de um método delimitador.

- Uma instrução [return](../keywords/return.md) em uma expressão lambda não faz com que o método delimitador retorne.

- Uma expressão lambda não pode conter uma instrução [goto](../keywords/goto.md), [break](../keywords/break.md) ou [continue](../keywords/continue.md) se o destino daquela instrução de salto estiver fora do bloco da expressão lambda. Também será um erro ter uma instrução de salto fora do bloco da expressão lambda se o destino estiver dentro do bloco.

A partir do C# 9,0, você pode aplicar o `static` modificador a uma expressão lambda para impedir a captura não intencional de variáveis locais ou o estado de instância pelo lambda:

:::code language="csharp" source="snippets/lambda-expressions/GeneralExamples.cs" id="SnippetStatic":::

Um lambda estático não pode capturar variáveis locais ou estado de instância de escopos delimitadores, mas pode referenciar membros estáticos e definições de constante.

## <a name="c-language-specification"></a>Especificação da linguagem C#

Para obter mais informações, confira a seção [Expressões de função anônima](~/_csharplang/spec/expressions.md#anonymous-function-expressions) da [Especificação da linguagem C#](~/_csharplang/spec/introduction.md).

Para obter mais informações sobre os recursos adicionados em C# 9,0, consulte as seguintes notas de proposta de recurso:

- [Parâmetros discard de lambda](~/_csharplang/proposals/csharp-9.0/lambda-discard-parameters.md)
- [Funções anônimas static](~/_csharplang/proposals/csharp-9.0/static-anonymous-functions.md)

## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
- [Operadores e expressões C#](index.md)
- [LINQ (Consulta Integrada à Linguagem)](../../programming-guide/concepts/linq/index.md)
- [Árvores de expressão](../../programming-guide/concepts/expression-trees/index.md)
- [Funções locais vs. expressões lambda](../../programming-guide/classes-and-structs/local-functions.md#local-functions-vs-lambda-expressions)
- [Exemplos de C# do Visual Studio 2008 (veja os arquivos de exemplo de consultas LINQ e programa XQuery)](https://code.msdn.microsoft.com/Visual-Studio-2008-C-d295cdba)
