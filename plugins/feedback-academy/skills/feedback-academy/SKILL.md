---
name: feedback-academy
description: Use quando o aluno da Apple Developer Academy pedir uma revisão ou feedback do código do seu projeto Swift/SwiftUI. Avalia qualidade de código e boas práticas, sem nota, em português, e entrega o feedback em PDF.
---

# Feedback de código para projetos da Apple Developer Academy

Esta skill revisa o código de um projeto Swift/SwiftUI e entrega um feedback detalhado para o próprio aluno ou time que pediu. O critério é sempre a **qualidade do código**: uso de boas práticas em geral, conforme a checklist abaixo.

O objetivo é ensinar. Quem lê o feedback deve entender o que fez bem, o que está errado, **por que** está errado e **como** corrigir. Não há nota.

O feedback é **detalhado e didático**, não um resumo. Cada ponto aponta o arquivo e o tipo exatos, mostra o trecho real do código e, quando for problema, mostra a versão corrigida.

## Fluxo

1. **Peça o contexto do challenge.** Antes de ler qualquer código, peça ao usuário um breve parágrafo com o contexto do challenge: tema, requisitos, restrições (ex.: sem persistência, sem API), plataforma-alvo e se é um projeto inicial ou mais avançado. Se o usuário já tiver dado esse contexto na conversa (em texto ou anexando o enunciado), não peça de novo. Se houver enunciado anexado, leia-o junto com o parágrafo.
2. **Extraia os requisitos** do contexto (por exemplo: responsividade, controle de estado, sem persistência, sem API, animações). Eles alimentam a tabela de requisitos do feedback.
3. **Identifique o nível do projeto.** Se o contexto indicar um projeto inicial, ignore o bloco **Arquitetura e organização** da checklist. Se nada for dito, aplique a checklist inteira.
4. **Leia o código inteiro**, arquivo por arquivo, não só uma amostra. Passe por cada item da checklist e anote, para cada achado, o arquivo, o tipo ou a propriedade e o trecho exato. Conte repetições quando o mesmo problema aparece em vários lugares ("aparece em 12 structs: ...").
5. **App rodando:** se o usuário enviar prints, vídeo ou observações do app em funcionamento, use isso para localizar problemas no código. O app em si não é critério.
6. **Monte o feedback** na estrutura abaixo.
7. **Gere o PDF** (seção **Saída em PDF**).

## Estrutura do feedback

As seções temáticas **não são fixas**: adapte ao que o projeto e o challenge mostrarem. O esqueleto é este:

1. **Título:** "Feedback — <nome do app>", com a plataforma-alvo logo abaixo (ex.: iPhone e iPad).
2. **Resumo dos requisitos:** tabela com as colunas Requisito, Status (✅ Atendido / ⚠️ Parcial / ❌ Não atendido) e Observação, que diz em uma ou duas frases como o código atende, citando tipos e APIs reais. Os requisitos vêm do contexto do challenge.
3. **Destaques positivos:** de 3 a 5 pontos fortes reais. Cada um com título, um parágrafo explicando o que foi feito, por que é uma boa prática e o nome do padrão quando houver, e o trecho de código correspondente.
4. **Seções temáticas (opcional):** quando um problema é transversal ao projeto inteiro, ganha seção própria antes das prioridades, com explicação do conceito, a regra prática e exemplos reais do projeto. Exemplos: comentários excessivos que traduzem o código, mistura de português e inglês nos identificadores, ausência de separação entre view e lógica.
5. **Pontos críticos — prioridade alta:** bugs, comportamento que não funciona como pretendido, duplicação de domínio, código de debug em produção.
6. **Melhorias importantes — prioridade média:** uso incorreto de APIs ou property wrappers, repetição de código, violações de convenção, código morto ou comentado.
7. **Ajustes pontuais — prioridade baixa:** organização de arquivos, acoplamentos frágeis, detalhes de acessibilidade.

Numere as seções a partir de "1. Destaques Positivos". Omita qualquer seção que ficaria vazia.

### Como escrever cada ponto

- **Título** que já diz o problema e onde ele está (ex.: "isPressed em PrimaryButton nunca muda — animação não funciona").
- **Parágrafo** que cita o arquivo e o tipo, descreve o que o código faz, explica **por que** isso é um problema (consequência concreta) e qual é a prática correta.
- **Código:** o trecho real do projeto com o comentário `// Atual` e, em seguida, a versão corrigida com `// Correto`. Mantenha os trechos curtos e focados no ponto.
- Quando o mesmo problema aparece em vários lugares, liste onde e mostre a solução uma vez.
- Tom: português claro, didático e direto, falando com quem pediu a revisão ("você" ou "vocês", se for um time). Sem rodeios e sem elogios vazios.

## Checklist de qualidade

### Arquitetura e organização (ignorar em projetos iniciais)
- **Lógica fora da View:** regra de negócio em ViewModel, model ou serviço, não dentro do `body`.
- **Views pequenas:** `body` enxuto, telas quebradas em subviews, `@ViewBuilder` e componentes reutilizáveis.
- **Pastas e arquivos por responsabilidade:** tipos de domínio e navegação em arquivos próprios, não no topo de arquivos de View; projeto organizado em grupos claros.
- **Protocolos e injeção:** dependências injetadas e serviços desacoplados por protocolo.

### SwiftUI e estado
- **Property wrappers certos:** `@State` privado e só para estado local mutável (não para valores recebidos que nunca mudam, que devem ser `let`), `@Binding` para estado do pai, `@Observable` e `@Environment` para estado compartilhado.
- **Fonte única de verdade:** sem estado duplicado, sem dois tipos representando o mesmo conceito de domínio.
- **Navegação moderna:** `NavigationStack`/`NavigationPath`, navegação baseada em valor, sem `NavigationView`.
- **`#Preview` funcionando:** previews com dados mock, idealmente cobrindo os estados relevantes.
- **Sem `AnyView` desnecessário:** prefira `@ViewBuilder`, `Group` ou condicionais.
- **Adaptação de layout:** size classes e `@Environment` em vez de `UIDevice` repetido em cada view.

### Swift idiomático e segurança
- **Sem force unwrap:** evita `!`, `try!` e `as!` sem justificativa.
- **Value types e `let`:** `struct` e `enum` por padrão, `let` em vez de `var` quando possível.
- **Enums robustos:** valores explícitos (raw values, propriedades) em vez de depender da ordem de `allCases`.
- **Tratamento de erros:** `throws`/`do-catch` e estado de erro visível na UI, sem erros engolidos.
- **Concorrência correta:** `async/await`, `Task` e `@MainActor` usados corretamente, sem `DispatchQueue` desnecessário.

### Qualidade geral e plataforma
- **Nomes:** Swift API Design Guidelines, camelCase para propriedades e funções, UpperCamelCase para tipos, sem erros de digitação, um idioma consistente nos identificadores.
- **Sem duplicação e sem código morto:** nada de código comentado, arquivos sem uso (ex.: `ContentView` vazio), magic numbers.
- **Comentários úteis:** comentários explicam o porquê de decisões não óbvias; comentários que só traduzem o código devem sair (são sinal comum de código gerado por IA e não revisado).
- **Sem debug em produção:** nenhum `print()` deixado no código.
- **Acessibilidade:** Dynamic Type, labels e hints de VoiceOver corretos para cada contexto, contraste.
- **Assets e strings:** cores e imagens no Asset Catalog, textos no String Catalog, nada hardcoded espalhado.
- **Git, README e testes:** commits claros, `.gitignore` sem `xcuserdata` e arquivos de build, README explicando o projeto, testes com Swift Testing ou XCTest.

## Saída em PDF

Se a sessão permite gerar arquivos (ferramentas de shell/arquivo disponíveis), a entrega é um **PDF**, com quantas páginas o conteúdo precisar:

- Se houver uma skill de PDF disponível, carregue-a antes de gerar o arquivo e siga as instruções dela. Montar em HTML/CSS e converter com Chromium headless funciona bem para este layout.
- Layout A4, fonte sem serifa para o texto e monoespaçada para o código.
- Título grande; títulos de seção numerados em verde; subtítulos de cada ponto em negrito escuro.
- Tabela de requisitos com cabeçalho verde e texto branco, linhas alternadas.
- Blocos de código com fundo azul-claro, borda verde à esquerda e realce de sintaxe simples; evite que um bloco seja cortado entre páginas quando possível.
- Linha divisória fina entre as seções principais.
- Nome do arquivo: `feedback-<nome-do-app>.pdf`, em minúsculas e sem acentos ou espaços.
- Abra o PDF gerado e confira se o texto, os acentos, as tabelas e os trechos de código estão corretos antes de entregar.
- Entregue o arquivo e, na conversa, diga só uma ou duas linhas com o resumo (ex.: requisitos atendidos e os principais pontos críticos). Não repita o feedback no chat.

Se a sessão não permite gerar arquivos, escreva o feedback direto na conversa, na mesma estrutura.
