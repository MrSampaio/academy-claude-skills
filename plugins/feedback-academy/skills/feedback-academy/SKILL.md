---
name: feedback-academy
description: Use quando o aluno da Apple Developer Academy pedir uma revisão ou feedback do código do seu projeto Swift/SwiftUI. Avalia qualidade de código e boas práticas, sem nota, em português, e entrega o feedback em PDF.
---

# Feedback de código para projetos da Apple Developer Academy

Esta skill revisa o código de um projeto Swift/SwiftUI e entrega um feedback detalhado para o próprio aluno ou time que pediu. O critério padrão é a **qualidade do código**: uso de boas práticas em geral, conforme a checklist abaixo.

O objetivo é ensinar. Quem lê o feedback deve entender o que fez bem, o que está errado, **por que** está errado e **como** corrigir. Não há nota.

O feedback é **detalhado e didático**, não um resumo. Cada ponto aponta o arquivo e o tipo exatos, mostra o trecho real do código e, quando for problema, mostra a versão corrigida.

**Atenção: a análise aprofundada de segurança da aplicação é opcional e fica desativada por padrão.** Ela só deve ser feita quando o aluno indicar explicitamente, no próprio parágrafo inicial de contexto, que deseja incluir essa análise. A checklist normal de qualidade do código continua valendo independentemente dessa opção.

## Fluxo

1. **Peça o contexto do challenge.** Antes de ler qualquer código, peça ao usuário um breve parágrafo com o contexto do challenge: tema, requisitos, restrições (ex.: sem persistência, sem API), plataforma-alvo e se é um projeto inicial ou mais avançado. Oriente-o a mencionar nesse mesmo parágrafo se também deseja uma análise complementar de segurança, criptografia e rotas de acesso. Essa análise é opcional. Se o usuário já tiver dado esse contexto na conversa (em texto ou anexando o enunciado), não peça de novo. Se houver enunciado anexado, leia-o junto com o parágrafo.
2. **Determine se a análise opcional foi solicitada.** Ative a seção de segurança somente se o usuário pedir isso explicitamente no parágrafo de contexto, por exemplo: “Quero que o feedback também analise segurança, criptografia e rotas de acesso”. Se não houver uma solicitação clara, ou se o usuário disser que não deseja essa análise, mantenha-a desativada. Não deduza consentimento pelo tema do app, pelos dados que ele manipula nem pela presença de autenticação. Não faça perguntas adicionais só para ativar essa opção.
3. **Extraia os requisitos** do contexto (por exemplo: responsividade, controle de estado, sem persistência, sem API, animações). Eles alimentam a tabela de requisitos do feedback.
4. **Identifique o nível do projeto.** Se o contexto indicar um projeto inicial, ignore o bloco **Arquitetura e organização** da checklist. Se nada for dito, aplique a checklist inteira.
5. **Leia o código inteiro**, arquivo por arquivo, não só uma amostra. Passe por cada item da checklist e anote, para cada achado, o arquivo, o tipo ou a propriedade e o trecho exato. Conte repetições quando o mesmo problema aparece em vários lugares ("aparece em 12 structs: ..."). Se a análise opcional de segurança estiver ativada, aplique também a seção **Análise opcional de segurança, criptografia e acesso**.
6. **App rodando:** se o usuário enviar prints, vídeo ou observações do app em funcionamento, use isso para localizar problemas no código. O app em si não é critério.
7. **Monte o feedback** na estrutura abaixo. Inclua a seção de segurança somente se ela tiver sido explicitamente solicitada e houver análise pertinente a apresentar.
8. **Gere o PDF** (seção **Saída em PDF**).

## Estrutura do feedback

As seções temáticas **não são fixas**: adapte ao que o projeto e o challenge mostrarem. O esqueleto é este:

1. **Título:** "Feedback — <nome do app>", com a plataforma-alvo logo abaixo (ex.: iPhone e iPad).
2. **Resumo dos requisitos:** tabela com as colunas Requisito, Status (✅ Atendido / ⚠️ Parcial / ❌ Não atendido) e Observação, que diz em uma ou duas frases como o código atende, citando tipos e APIs reais. Os requisitos vêm do contexto do challenge.
3. **Destaques positivos:** de 3 a 5 pontos fortes reais. Cada um com título, um parágrafo explicando o que foi feito, por que é uma boa prática e o nome do padrão quando houver, e o trecho de código correspondente.
4. **Seções temáticas (opcional):** quando um problema é transversal ao projeto inteiro, ganha seção própria antes das prioridades, com explicação do conceito, a regra prática e exemplos reais do projeto. Exemplos: comentários excessivos que traduzem o código, mistura de português e inglês nos identificadores, ausência de separação entre view e lógica. A seção de segurança descrita adiante também pode aparecer nesta área, mas apenas quando solicitada explicitamente.
5. **Pontos críticos — prioridade alta:** bugs, comportamento que não funciona como pretendido, duplicação de domínio, código de debug em produção.
6. **Melhorias importantes — prioridade média:** uso incorreto de APIs ou property wrappers, repetição de código, violações de convenção, código morto ou comentado.
7. **Ajustes pontuais — prioridade baixa:** organização de arquivos, acoplamentos frágeis, detalhes de acessibilidade.

Numere as seções a partir de **"1. Destaques positivos"**. Omita qualquer seção que ficaria vazia. Se a análise opcional de segurança for solicitada, inclua seus achados na seção temática própria e/ou nas prioridades alta, média e baixa, conforme a gravidade. Não duplique o mesmo achado em várias seções.

### Como escrever cada ponto

- **Título** que já diz o problema e onde ele está (ex.: "isPressed em PrimaryButton nunca muda — animação não funciona").
- **Parágrafo** que cita o arquivo e o tipo, descreve o que o código faz, explica **por que** isso é um problema (consequência concreta) e qual é a prática correta.
- **Código:** o trecho real do projeto com o comentário `// Atual` e, em seguida, a versão corrigida com `// Correto`. Mantenha os trechos curtos e focados no ponto.
- Quando o mesmo problema aparece em vários lugares, liste onde e mostre a solução uma vez.
- Tom: português claro, didático e direto, falando com quem pediu a revisão ("você" ou "vocês", se for um time). Sem rodeios e sem elogios vazios.
- Não invente trechos, arquivos, configurações, rotas, APIs nem comportamentos que não aparecem no material enviado. Se não houver código suficiente para confirmar algo, declare a limitação e diga qual arquivo ou configuração seria necessário para investigar.

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

### Swift idiomático e segurança da linguagem

- **Sem force unwrap:** evita `!`, `try!` e `as!` sem justificativa.
- **Value types e `let`:** `struct` e `enum` por padrão, `let` em vez de `var` quando possível.
- **Enums robustos:** valores explícitos (raw values, propriedades) em vez de depender da ordem de `allCases`.
- **Tratamento de erros:** `throws`/`do-catch` e estado de erro visível na UI, sem erros engolidos.
- **Concorrência correta:** `async/await`, `Task` e `@MainActor` usados corretamente, sem `DispatchQueue` desnecessário.

Esta checklist de segurança da linguagem faz parte da revisão normal. Ela **não** ativa a análise opcional de segurança da aplicação descrita a seguir.

### Qualidade geral e plataforma

- **Nomes:** Swift API Design Guidelines, camelCase para propriedades e funções, UpperCamelCase para tipos, sem erros de digitação, um idioma consistente nos identificadores.
- **Sem duplicação e sem código morto:** nada de código comentado, arquivos sem uso (ex.: `ContentView` vazio), magic numbers.
- **Comentários úteis:** comentários explicam o porquê de decisões não óbvias; comentários que só traduzem o código devem sair (são sinal comum de código gerado por IA e não revisado).
- **Sem debug em produção:** nenhum `print()` deixado no código.
- **Acessibilidade:** Dynamic Type, labels e hints de VoiceOver corretos para cada contexto, contraste.
- **Assets e strings:** cores e imagens no Asset Catalog, textos no String Catalog, nada hardcoded espalhado.
- **Git, README e testes:** commits claros, `.gitignore` sem `xcuserdata` e arquivos de build, README explicando o projeto, testes com Swift Testing ou XCTest.

## Análise opcional de segurança, criptografia e acesso

**Esta seção só pode ser executada quando o aluno solicitar explicitamente a análise complementar no parágrafo inicial de contexto. Ela não é obrigatória para nenhum projeto.** Se não houver solicitação explícita, não faça essa revisão aprofundada, não adicione esta seção ao PDF e não trate a ausência dela como uma falha do projeto. Não é necessário pedir justificativas ao aluno.

Quando ativada, a análise deve ser didática, adequada ao nível de experiência indicado e limitada ao código, configurações e demais materiais realmente fornecidos. Verifique os pontos aplicáveis abaixo; não exija recursos de segurança que não façam sentido para o escopo, o modelo de dados ou as restrições do challenge.

### O que verificar

- **Rotas e pontos de entrada:** percorra os fluxos de navegação e os pontos pelos quais o usuário pode chegar a funcionalidades ou dados, quando existirem: `NavigationStack`/`NavigationPath`, deep links, Universal Links, URL schemes, notificações, widgets, extensões, App Intents e outras entradas aplicáveis. Identifique telas ou ações sensíveis acessíveis por caminhos alternativos, rotas sem validação suficiente e estados de navegação que possam ser manipulados indevidamente. Não presuma que um app usa todos esses mecanismos.
- **Autenticação e autorização:** verifique como a identidade do usuário é estabelecida e como o acesso a telas, ações e recursos é controlado. Diferencie ocultar um botão ou uma tela de realmente autorizar uma operação. Quando houver backend/API, avalie nos materiais disponíveis se a autorização é validada também no servidor; controles apenas no cliente não protegem, por si só, os dados no servidor.
- **Possíveis brechas:** procure indícios concretos, no material fornecido, de exposição indevida de dados, acesso horizontal ou vertical não autorizado, validação insuficiente de entrada, informações sensíveis em logs, segredos ou chaves embutidos no código, configurações permissivas, tratamento inseguro de sessão e outros riscos pertinentes à arquitetura encontrada. Relacione cada risco a um trecho, arquivo ou configuração específica sempre que possível.
- **Criptografia e dados sensíveis:** verifique se existe uma necessidade real de criptografia, quais dados são sensíveis e onde transitam ou ficam armazenados. Se o app usa criptografia, observe se utiliza APIs consolidadas do sistema, como CryptoKit ou serviços de segurança apropriados, e se evita algoritmos ou implementações criptográficas próprias sem justificativa. Não recomende criar criptografia customizada nem adicionar criptografia sem necessidade identificada.
- **Armazenamento local e segredos:** examine o uso de `UserDefaults`, arquivos, caches, banco de dados local e Keychain conforme o tipo de dado. Sinalize senhas, tokens, chaves privadas ou outros segredos armazenados em locais inadequados. Considere as opções de proteção de dados da plataforma quando forem pertinentes. Não afirme que o Keychain é necessário para qualquer dado, nem que seu uso sozinho garante segurança.
- **Comunicação de rede:** quando houver chamadas de rede, verifique o uso de HTTPS/TLS, a configuração do App Transport Security (ATS), o tratamento de erros e a exposição de credenciais ou dados sensíveis em URLs, logs e respostas. Sinalize exceções de transporte inseguras observáveis no projeto. Não recomende certificate pinning automaticamente; só discuta essa medida quando houver justificativa concreta e explique seus custos e limitações.
- **Permissões e privacidade:** confira solicitações de permissões, chaves de uso no `Info.plist`, princípio do menor privilégio e se o acesso a localização, câmera, microfone, fotos, contatos ou outros recursos é solicitado em contexto adequado. Quando aplicável, observe transparência no uso de dados, coleta mínima e configurações relacionadas à privacidade. Não presuma que uma permissão é necessária apenas porque uma API está disponível.
- **Frameworks e APIs da Apple:** avalie se os frameworks utilizados são apropriados ao problema e se as APIs foram usadas conforme a documentação oficial, incluindo requisitos de permissões, entitlements, ciclo de vida, concorrência e tratamento de erros quando relevantes. Aponte APIs obsoletas, usos incorretos ou atalhos frágeis observáveis. Não classifique uma API como proibida ou incompatível sem base documental.
- **Diretrizes da Apple:** quando o destino ou a distribuição do app tornarem isso pertinente, faça uma verificação preliminar das diretrizes oficiais atuais aplicáveis, como App Review Guidelines, requisitos de privacidade, uso de APIs e permissões. Diferencie claramente requisitos documentados de recomendações de engenharia. Não garanta que o app será aprovado pela App Review.

### Como apresentar os resultados

Para cada achado, informe:

1. **Gravidade sugerida:** crítica, alta, média ou baixa, explicando brevemente o impacto e considerando o contexto. Não use gravidade alta só por precaução; justifique-a pelo risco concreto.
2. **Evidência:** arquivo, tipo, função, rota, configuração ou trecho real que sustenta a observação.
3. **Cenário e consequência:** explique em linguagem acessível como o problema poderia ocorrer e o que poderia ser exposto ou alterado.
4. **Correção recomendada:** mostre uma alteração concreta e adequada ao nível do projeto, com trecho `// Atual` e `// Correto` sempre que for possível propor uma correção de código.
5. **Limitações:** se algo depender do backend, das configurações de assinatura, de entitlements, de políticas do servidor ou de arquivos que não foram enviados, marque como **não verificável com o material disponível** e indique o que faltaria analisar. Não declare uma vulnerabilidade confirmada sem evidências suficientes.

Separe os resultados entre **problema confirmado no código**, **risco potencial que precisa ser validado** e **item não verificável com os materiais enviados**. Se nenhum problema for identificado, informe que não foram encontrados problemas evidentes no escopo analisado — nunca que o app é totalmente seguro.

Esta revisão é uma análise estática e educacional do material fornecido. Ela não substitui uma auditoria profissional, testes dinâmicos, análise de dependências, revisão de infraestrutura/backend nem testes de penetração autorizados. Não alegue ter executado o app, verificado um servidor ou testado uma brecha se isso não aconteceu.

### Referências oficiais para consultar quando a análise estiver ativada

Use a documentação oficial atual da Apple pertinente ao caso, em vez de depender apenas da memória. Consulte apenas as referências relevantes ao projeto:

- [App Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)
- [Security — Apple Developer Documentation](https://developer.apple.com/documentation/security)
- [Keychain Services](https://developer.apple.com/documentation/security/keychain-services)
- [CryptoKit](https://developer.apple.com/documentation/cryptokit)
- [Preventing Insecure Network Connections](https://developer.apple.com/documentation/security/preventing_insecure_network_connections)
- [Information Property List](https://developer.apple.com/documentation/bundleresources/information_property_list)
- [Privacy manifest files](https://developer.apple.com/documentation/bundleresources/privacy_manifest_files)

Se não houver acesso à documentação atual, deixe isso claro e evite afirmar conformidade definitiva com diretrizes que não pôde verificar.

## Saída em PDF

Se a sessão permite gerar arquivos (ferramentas de shell/arquivo disponíveis), a entrega é um **PDF**, com quantas páginas o conteúdo precisar:

- Se houver uma skill de PDF disponível, carregue-a antes de gerar o arquivo e siga as instruções dela. Montar em HTML/CSS e converter com Chromium headless funciona bem para este layout.
- Layout A4, fonte sem serifa para o texto e monoespaçada para o código.
- Título grande; títulos de seção numerados em verde; subtítulos de cada ponto em negrito escuro.
- Tabela de requisitos com cabeçalho verde e texto branco, linhas alternadas.
- Blocos de código com fundo azul-claro, borda verde à esquerda e realce de sintaxe simples; evite que um bloco seja cortado entre páginas quando possível.
- Nome do arquivo: `feedback-<nome-do-app>.pdf`, em minúsculas e sem acentos ou espaços.
- Abra o PDF gerado e confira se o texto, os acentos, as tabelas e os trechos de código estão corretos antes de entregar.
- Entregue o arquivo e, na conversa, diga só uma ou duas linhas com o resumo (ex.: requisitos atendidos e os principais pontos críticos). Não repita o feedback no chat.

Se a sessão não permite gerar arquivos, escreva o feedback direto na conversa, na mesma estrutura.
