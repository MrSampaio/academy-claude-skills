# Academy Claude Skills

Skills do Claude para os alunos da Apple Developer Academy.

| Skill | O que faz |
|---|---|
| `feedback-academy` | Revisa o código do seu projeto Swift/SwiftUI e gera um feedback didático em PDF: requisitos do challenge, destaques positivos e pontos de melhoria por prioridade, com o código atual e a versão corrigida. |

## Como instalar

### Claude Code (recomendado)

Dentro do Claude Code, rode:

```
/plugin marketplace add joaocarloslima/academy-claude-skills
/plugin install feedback-academy@academy-skills
```

Para receber versões novas da skill:

```
/plugin marketplace update academy-skills
```

### Claude Code, sem plugin

Copie a pasta `plugins/feedback-academy/skills/feedback-academy` para:

- `~/.claude/skills/` para usar em todos os seus projetos, ou
- `.claude/skills/` dentro do repositório do seu app, para o time inteiro ter a skill ao clonar.

### claude.ai e app desktop

1. Baixe o arquivo `feedback-academy.zip` na página de **Releases** deste repositório. Não use o botão verde "Code → Download ZIP": ele empacota o repositório inteiro e o upload é recusado.
2. No Claude, abra **Configurações → Capacidades → Skills** e envie o zip.
3. A execução de código precisa estar ativada para a skill gerar o PDF.

## Como usar

Abra o projeto (Claude Code) ou anexe os arquivos do projeto (claude.ai) e peça algo como:

> Revisa o código do meu projeto e me dá um feedback.

A skill vai pedir primeiro um parágrafo curto com o contexto do challenge: tema, requisitos, restrições e plataforma-alvo. Quanto melhor esse contexto, melhor o feedback.

## Importante

O feedback é uma ferramenta de aprendizado. Leia cada ponto, entenda o porquê e faça as correções você mesmo, em vez de pedir para a IA reescrever o código.
