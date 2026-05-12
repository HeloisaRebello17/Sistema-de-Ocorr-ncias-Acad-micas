# Sistema de Ocorrências Acadêmicas — Análise de Segurança

**Disciplina:** Segurança da Informação  
**Aluna:** Heloísa Rebello Cabral — RA 1327380 | Turma 5B  
**Professor:** Edson Vaz Lopes  
**Data:** Maio/2026

---

## Sobre o projeto

Análise crítica de segurança em um protótipo web de registro de ocorrências acadêmicas, com implementação de melhorias baseadas nos conceitos estudados na disciplina.

## Estrutura

```
sistema-original/
  index.html    ← versão com vulnerabilidades identificadas e comentadas no código

sistema-melhorado/
  index.html    ← versão com 18 melhorias de segurança implementadas

relatorio_final.docx ← relatório técnico completo
README.md       ← este arquivo
```

## Principais vulnerabilidades identificadas (versão original)

1. Credenciais hardcoded em texto puro no JavaScript
2. Campo de senha com `type="text"` (senha visível)
3. Autenticação inteiramente no front-end (contornável via console)
4. Sem controle de sessão (sem token, sem expiração)
5. Ausência de controle de acesso por perfil (RBAC)
6. Alunos visualizam ocorrências de todos os outros alunos
7. CPF exibido em texto puro na listagem
8. Senhas exibidas na aba de usuários
9. Exportação JSON incluía lista de usuários com senhas
10. Logs armazenados no localStorage (apagáveis pelo usuário)
11. Qualquer perfil pode apagar todos os logs
12. CPF desnecessariamente registrado nos logs
13. Sem validação de formato CPF
14. Sem aviso de limitações ao usuário
15. Sem proteção contra XSS

## Melhorias implementadas (versão melhorada)

- `type="password"` no campo de senha
- Aviso de sistema didático no login e no sistema
- Senhas substituídas por hashes simulados (btoa)
- Controle de permissões centralizado por perfil — RBAC
- Menu desabilita botões sem permissão por perfil
- Verificação de permissão ao trocar de aba (com log de tentativa negada)
- Aluno vê apenas suas próprias ocorrências (filtro por matrícula)
- CPF mascarado na exibição (`***.***.***-XX`)
- Aba de usuários não exibe senhas nem hashes
- Exportação JSON sem dados de usuários ou senhas
- CSV exportado sem coluna CPF (minimização de dados)
- Limpeza de logs restrita a admin com confirmação obrigatória
- Timeout de sessão simulado (10 minutos com logout automático)
- Validação completa de campos obrigatórios com feedback visual
- Validação de CPF pelo algoritmo oficial (dois dígitos verificadores)
- Escape de HTML em todas as saídas (proteção XSS)
- Logs sem CPF (apenas matrícula)
- Logs incluem perfil do usuário para melhor rastreabilidade

## Logins para teste (sistema melhorado)

| Usuário   | Senha    | Perfil                              |
| --------- | -------- | ----------------------------------- |
| admin     | admin123 | Administrador                       |
| professor | prof123  | Professor                           |
| aluno     | aluno123 | Aluno (Maria Souza, mat. 2024001)   |
| joao      | joao456  | Aluno (João Ferreira, mat. 2024002) |

> ⚠️ Dados fictícios para fins didáticos. Não inserir dados reais.

## Sistema publicado

https://heloisarebello17.github.io/Sistema-de-Ocorr-ncias-Acad-micas/

## Conclusão técnica

O sistema **não deve ser usado em produção com dados reais** na forma atual. Apesar das melhorias implementadas no protótipo melhorado, ele continua sendo uma aplicação puramente client-side, com persistência em `localStorage`, sem autenticação real, sem controle centralizado de sessão, sem trilha de auditoria em servidor, sem backup institucional e sem garantia efetiva de integridade dos dados.

### Principais impedimentos para produção

- Ausência de back-end e API para autenticação e autorização reais
- Persistência local no navegador, sujeita a perda, limpeza manual e manipulação
- Falta de banco de dados centralizado e backup institucional
- Ausência de mecanismos reais de auditoria, rastreabilidade e recuperação
- Dependência de proteção apenas no front-end, que pode ser contornada

### Mudanças mínimas necessárias

- Implementar back-end com autenticação segura e sessões controladas
- Adotar banco de dados centralizado com criptografia em repouso e backup
- Centralizar RBAC no servidor, com validação de permissões em todas as rotas
- Registrar logs de auditoria em servidor, com retenção e integridade
- Revisar a adequação à LGPD, aplicando minimização, base legal e controle de acesso

### Encerramento

Com as melhorias atuais, o projeto cumpre bem o objetivo didático de análise e comparação de riscos, mas ainda não atende aos requisitos mínimos para uso institucional real.
