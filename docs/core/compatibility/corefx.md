---
title: Alterações significativas na biblioteca de classes base
description: Lista as alterações significativas nas principais bibliotecas do .NET.
ms.date: 07/27/2020
ms.openlocfilehash: 3ecf0e81a3adef097aafb760dc44498d7263f0b6
ms.sourcegitcommit: 39b1d5f2978be15409c189a66ab30781d9082cd8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92050553"
---
# <a name="core-net-libraries-breaking-changes"></a>Principais alterações significativas nas bibliotecas do .NET

As principais bibliotecas do .NET fornecem os primitivos e outros tipos gerais usados pelo .NET Core.

As seguintes alterações significativas estão documentadas nesta página:

| Alteração significativa | Versão introduzida |
| - | :-: |
| [O valor de FrameworkDescription é .NET, em vez de .NET Core](#frameworkdescriptions-value-is-net-instead-of-net-core) | 5.0 |
| [Alterações de comportamento da API relacionadas ao assembly para o formato de publicação de arquivo único](#assembly-related-api-behavior-changes-for-single-file-publishing-format) | 5.0 |
| [Ordem das marcas na atividade. as marcas são revertidas](#order-of-tags-in-activitytags-is-reversed) | 5.0 |
| [Nomes de parâmetros alterados no RC1](#parameter-names-changed-in-rc1) | 5.0 |
| [Atributos OSPlatform renomeados ou removidos](#osplatform-attributes-renamed-or-removed) | 5.0 |
| [Thread. Abort é obsoleto](#threadabort-is-obsolete) | 5.0 |
| [Propriedades obsoletas em ConsoleLoggerOptions](#obsolete-properties-on-consoleloggeroptions) | 5.0 |
| [Verificações IsSupported de hardware intrínsecas podem diferir para tipos aninhados](#hardware-intrinsic-issupported-checks-may-differ-for-nested-types) | 5.0 |
| [Nomes de parâmetro alterados em assemblies de referência](#parameter-names-changed-in-reference-assemblies) | 5.0 |
| [Caminhos de URI com caracteres não ASCII são analisados corretamente no UNIX](#uri-paths-with-non-ascii-characters-parse-correctly-on-unix) | 5.0 |
| [Reconhecimento de URI de caminhos UNC no UNIX](#uri-recognition-of-unc-paths-on-unix) | 5.0 |
| [Environment. OSVersion retorna a versão correta do sistema operacional](#environmentosversion-returns-the-correct-operating-system-version) | 5.0 |
| [Complexidade do LINQ OrderBy. primeiro {OrDefault} aumentou](#complexity-of-linq-orderbyfirstordefault-increased) | 5.0 |
| [IntPtr e UIntPtr implementam IFormattable](#intptr-and-uintptr-implement-iformattable) | 5.0 |
| [PrincipalPermissionattribute está obsoleto como erro](#principalpermissionattribute-is-obsolete-as-error) | 5.0 |
| [Os métodos de serialização BinaryFormatter são obsoletos e proibidos em aplicativos ASP.NET](#binaryformatter-serialization-methods-are-obsolete-and-prohibited-in-aspnet-apps) | 5.0 |
| [Os caminhos de código UTF-7 estão obsoletos](#utf-7-code-paths-are-obsolete) | 5.0 |
| [Vetor \<T> sempre gera NotSupportedException para tipos sem suporte](#vectort-always-throws-notsupportedexception-for-unsupported-types) | 5.0 |
| [O ActivityIdFormat padrão é W3C](#default-activityidformat-is-w3c) | 5.0 |
| [Alteração de comportamento para vector2. Lerp e Vector4. Lerp](#behavior-change-for-vector2lerp-and-vector4lerp) | 5.0 |
| [Os métodos SSE e SSE2 CompareGreaterThan manipulam corretamente as entradas NaN](#sse-and-sse2-comparegreaterthan-methods-properly-handle-nan-inputs) | 5.0 |
| [CounterSet. CreateCounterSetInstance agora gera InvalidOperationException se a instância já existir](#countersetcreatecountersetinstance-now-throws-invalidoperationexception-if-instance-already-exists) | 5.0 |
| [Pacote Microsoft. DotNet. PlatformAbstractions removido](#microsoftdotnetplatformabstractions-package-removed) | 5.0 |
| [As APIs que relatam versão agora relatam produto e não versão de arquivo](#apis-that-report-version-now-report-product-and-not-file-version) | 3.0 |
| [Instâncias EncoderFallbackBuffer personalizadas não podem retornar recursivamente](#custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively) | 3.0 |
| [Alterações de comportamento de análise e formatação de ponto flutuante](#floating-point-formatting-and-parsing-behavior-changed) | 3.0 |
| [Operações de análise de ponto flutuante não falham mais ou geram uma estourexception](#floating-point-parsing-operations-no-longer-fail-or-throw-an-overflowexception) | 3.0 |
| [InvalidAsynchronousStateException movido para outro assembly](#invalidasynchronousstateexception-moved-to-another-assembly) | 3.0 |
| [A substituição de sequências de bytes UTF-8 mal formados segue as diretrizes de Unicode](#replacing-ill-formed-utf-8-byte-sequences-follows-unicode-guidelines) | 3.0 |
| [TypeDescriptionProviderAttribute movido para outro assembly](#typedescriptionproviderattribute-moved-to-another-assembly) | 3.0 |
| [O ZipArchiveEntry não lida mais com os arquivos mortos com tamanhos de entrada inconsistentes](#ziparchiveentry-no-longer-handles-archives-with-inconsistent-entry-sizes) | 3.0 |
| [FieldInfo. SetValue gera uma exceção para campos estáticos somente de inicialização](#fieldinfosetvalue-throws-exception-for-static-init-only-fields) | 3.0 |
| [Campos privados adicionados aos tipos de struct internos](#private-fields-added-to-built-in-struct-types) | 2.1 |
| [Alteração no valor padrão de UseShellExecute](#change-in-default-value-of-useshellexecute) | 2.1 |
| [Versões do OpenSSL no macOS](#openssl-versions-on-macos) | 2.1 |
| [UnauthorizedAccessException gerado por FileSystemInfo. Attributes](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes) | 1.0 |
| [Tratamento de exceções de estado de processo corrompido não é suportado](#handling-corrupted-state-exceptions-is-not-supported) | 1.0 |
| [As propriedades UriBuilder não precedem mais os caracteres à esquerda](#uribuilder-properties-no-longer-prepend-leading-characters) | 1.0 |
| [Process. StartInfo gera InvalidOperationException para processos que você não iniciou](#processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start) | 1.0 |

## <a name="net-50"></a>.NET 5,0

[!INCLUDE [frameworkdescription-returns-net-not-net-core](../../../includes/core-changes/corefx/5.0/frameworkdescription-returns-net-not-net-core.md)]

***

[!INCLUDE [assembly-api-behavior-changes-for-single-file-publish](../../../includes/core-changes/corefx/5.0/assembly-api-behavior-changes-for-single-file-publish.md)]

***

[!INCLUDE [reverse-order-of-tags-in-activity-property](../../../includes/core-changes/corefx/5.0/reverse-order-of-tags-in-activity-property.md)]

***

[!INCLUDE [reference-assembly-parameter-names-rc1](../../../includes/core-changes/corefx/5.0/reference-assembly-parameter-names-rc1.md)]

***

[!INCLUDE [os-platform-attributes-renamed](../../../includes/core-changes/corefx/5.0/os-platform-attributes-renamed.md)]

***

[!INCLUDE [thread-abort-obsolete](../../../includes/core-changes/corefx/5.0/thread-abort-obsolete.md)]

***

[!INCLUDE [obsolete-consoleloggeroptions-properties](../../../includes/core-changes/corefx/5.0/obsolete-consoleloggeroptions-properties.md)]

***

[!INCLUDE [hardware-instrinsics-issupported-checks](../../../includes/core-changes/corefx/5.0/hardware-instrinsics-issupported-checks.md)]

***

[!INCLUDE [reference-assembly-parameter-names](../../../includes/core-changes/corefx/5.0/reference-assembly-parameter-names.md)]

***

[!INCLUDE [non-ascii-chars-in-uri-parsed-correctly](../../../includes/core-changes/corefx/5.0/non-ascii-chars-in-uri-parsed-correctly.md)]

***

[!INCLUDE [unc-path-recognition-unix](../../../includes/core-changes/corefx/5.0/unc-path-recognition-unix.md)]

***

[!INCLUDE [environment-osversion-returns-correct-version](../../../includes/core-changes/corefx/5.0/environment-osversion-returns-correct-version.md)]

***

[!INCLUDE [orderby-firstordefault-complexity-increase](../../../includes/core-changes/corefx/5.0/orderby-firstordefault-complexity-increase.md)]

***

[!INCLUDE [intptr-uintptr-implement-iformattable](../../../includes/core-changes/corefx/5.0/intptr-uintptr-implement-iformattable.md)]

***

[!INCLUDE [principalpermissionattribute-obsolete](../../../includes/core-changes/corefx/5.0/principalpermissionattribute-obsolete.md)]

***

[!INCLUDE [binaryformatter-serialization-obsolete](../../../includes/core-changes/corefx/5.0/binaryformatter-serialization-obsolete.md)]

***

[!INCLUDE [utf-7-code-paths-obsolete](../../../includes/core-changes/corefx/5.0/utf-7-code-paths-obsolete.md)]

***

[!INCLUDE [vectort-throws-notsupportedexception](../../../includes/core-changes/corefx/5.0/vectort-throws-notsupportedexception.md)]

***

[!INCLUDE [default-activityidformat-changed](../../../includes/core-changes/corefx/5.0/default-activityidformat-changed.md)]

***

[!INCLUDE [vector-lerp-behavior-change](../../../includes/core-changes/corefx/5.0/vector-lerp-behavior-change.md)]

***

[!INCLUDE [sse-comparegreaterthan-intrinsics](../../../includes/core-changes/corefx/5.0/sse-comparegreaterthan-intrinsics.md)]

***

[!INCLUDE [createcountersetinstance-throws-invalidoperation](../../../includes/core-changes/corefx/5.0/createcountersetinstance-throws-invalidoperation.md)]

***

[!INCLUDE [platformabstractions-package-removed](../../../includes/core-changes/corefx/5.0/platformabstractions-package-removed.md)]

***

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[APIs that report version now report product and not file version](~/includes/core-changes/corefx/3.0/version-information-changes.md)]

***

[!INCLUDE[Custom EncoderFallbackBuffer instances cannot fall back recursively](~/includes/core-changes/corefx/3.0/custom-encoderfallbackbuffer-cannot-be-recursive.md)]

***

[!INCLUDE[Floating point formatting and parsing behavior changes](~/includes/core-changes/corefx/3.0/floating-point-changes.md)]

***

[!INCLUDE[Floating-point parsing operations no longer fail or throw an OverflowException](~/includes/core-changes/corefx/3.0/floating-point-parsing-does-not-overflow.md)]

***

[!INCLUDE[InvalidAsynchronousStateException moved to another assembly](~/includes/core-changes/corefx/3.0/move-invalidasynchronousstateexception.md)]

***

[!INCLUDE[NET Core 3.0 follows Unicode best practices when replacing ill-formed UTF-8 byte sequences](~/includes/core-changes/corefx/3.0/net-core-3-0-follows-unicode-utf8-best-practices.md)]

***

[!INCLUDE[TypeDescriptionProviderAttribute moved to another assembly](~/includes/core-changes/corefx/3.0/move-typedescriptionproviderattribute.md)]

***

[!INCLUDE[ZipArchiveEntry no longer handles archives with inconsistent entry sizes](~/includes/core-changes/corefx/3.0/ziparchiveentry-and-inconsistent-entry-sizes.md)]

***

[!INCLUDE [FieldInfo.SetValue throws exception for static, init-only fields](~/includes/core-changes/corefx/3.0/fieldinfo-setvalue-exception.md)]

***

## <a name="net-core-21"></a>.NET Core 2.1

[!INCLUDE[Private fields added to built-in struct types](~/includes/core-changes/corefx/2.1/instantiate-struct.md)]

***

[!INCLUDE[Change in default value of UseShellExecute](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

***

[!INCLUDE [OpenSSL versions on macOS](../../../includes/core-changes/corefx/openssl-dependencies-macos.md)]

***

## <a name="net-core-10"></a>.NET Core 1.0

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

***

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

***

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

***

[!INCLUDE [startinfo-throws-exception](../../../includes/core-changes/corefx/1.0/startinfo-throws-exception.md)]

***
