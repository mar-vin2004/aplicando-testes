# Relatório sobre Frameworks de Testes Unitários: xUnit, NUnit e MSTest

## 1. xUnit

### Estrutura e Sintaxe
xUnit é um framework de testes unitários popular em .NET, conhecido por sua simplicidade e por ser uma escolha preferida para novos projetos. A estrutura do código de teste em xUnit é direta e clara, utilizando atributos como `[Theory]` e `[InlineData]` para parametrizar os testes.

### Código de Exemplo
No exemplo fornecido, os testes para o método de conversão de temperatura são definidos usando o atributo `[Theory]`, que permite a execução do mesmo teste com diferentes conjuntos de dados, fornecidos por `[InlineData]`.

```csharp
using System;
using Xunit;

namespace Temperatura.Testes
{
    public class TestesConversorTemperatura
    {
        [Theory]
        [InlineData(32, 0)]
        [InlineData(47, 8.33)]
        [InlineData(86, 30)]
        [InlineData(90.5, 32.5)]
        [InlineData(120.18, 48.99)]
        [InlineData(212, 100)]
        public void TestarConversaoTemperatura(
            double fahrenheit, double celsius)
        {
            double valorCalculado =
                ConversorTemperatura.FahrenheitParaCelsius(fahrenheit);
            Assert.Equal(celsius, valorCalculado);
        }
    }
}
```

### Vantagens e Desvantagens
#### Vantagens:
Suporte robusto para teorias e dados de entrada parametrizados.
Integração fácil com várias ferramentas de CI/CD.
Boa documentação e comunidade ativa.

#### Desvantagens:
Pode ser um pouco diferente para aqueles acostumados a outros frameworks de teste como NUnit ou MSTest, exigindo alguma curva de aprendizado.


## 2. NUnit
### Estrutura e Sintaxe
NUnit é um framework de testes unitários amplamente utilizado na comunidade .NET, com uma longa história e uma ampla base de usuários. Ele é conhecido por sua flexibilidade e vasta gama de atributos de teste, permitindo uma configuração rica de testes.

### Código de Exemplo
O exemplo utiliza [TestCase] para fornecer diferentes conjuntos de dados para o método de teste TesteConversaoTemperatura.

```csharp
using NUnit.Framework;

namespace Temperatura.Testes
{
    public class TestesConversorTemperatura
    {
        [TestCase(32, 0)]
        [TestCase(47, 8.33)]
        [TestCase(86, 30)]
        [TestCase(90.5, 32.5)]
        [TestCase(120.18, 48.99)]
        [TestCase(212, 100)]
        public void TesteConversaoTemperatura(
            double tempFahrenheit, double tempCelsius)
        {
            double valorCalculado =
                ConversorTemperatura.FahrenheitParaCelsius(tempFahrenheit);
            Assert.AreEqual(tempCelsius, valorCalculado);
        }
    }
}
```

### Vantagens e Desvantagens
#### Vantagens:
Suporte extensivo a diferentes atributos e tipos de testes.
Ampla adoção e compatibilidade com muitas ferramentas.
Alta flexibilidade e configurabilidade dos testes.

#### Desvantagens:
Pode ser verboso e complexo para configurações mais simples.
Inicialmente pode ser mais complicado para novos usuários devido à vasta gama de funcionalidades.

## 3. MSTest
### Estrutura e Sintaxe
MSTest é o framework de testes unitários oficial da Microsoft para .NET. É bem integrado ao Visual Studio e outras ferramentas Microsoft, tornando-o uma escolha natural para muitos desenvolvedores.

### Código de Exemplo
O exemplo utiliza [DataRow] dentro de um [DataTestMethod] para fornecer diferentes conjuntos de dados para o teste de conversão de temperatura.

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace Temperatura.Testes
{
    [TestClass]
    public class TestesConversorTemperatura
    {
        [DataRow(32, 0)]
        [DataRow(47, 8.33)]
        [DataRow(86, 30)]
        [DataRow(90.5, 32.5)]
        [DataRow(120.18, 48.99)]
        [DataRow(212, 100)]
        [DataTestMethod]
        public void TesteConversaoTemperatura(
            double tempFahrenheit, double tempCelsius)
        {
            double valorCalculado =
                ConversorTemperatura.FahrenheitParaCelsius(tempFahrenheit);
            Assert.AreEqual(tempCelsius, valorCalculado);
        }
    }
}
```

### Vantagens e Desvantagens

#### Vantagens:

Integração nativa com Visual Studio, oferecendo uma excelente experiência de desenvolvimento.
Simplicidade e familiaridade para desenvolvedores acostumados ao ecossistema Microsoft.

#### Desvantagens:
Pode ser menos flexível comparado a xUnit e NUnit.
Menos adotado fora do ecossistema Microsoft.

## Conclusão

Cada um dos frameworks de teste unitário xUnit, NUnit e MSTest possui suas próprias vantagens e desvantagens. A escolha do framework mais adequado depende das necessidades específicas do projeto e das preferências da equipe de desenvolvimento. xUnit oferece simplicidade e boa integração com ferramentas modernas, NUnit é extremamente flexível e poderoso, e MSTest é bem integrado ao ambiente de desenvolvimento Microsoft, oferecendo uma experiência de uso suave dentro do Visual Studio.
