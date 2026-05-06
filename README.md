# Sistema de Ocorrências Acadêmicas — Análise de Segurança

**Disciplina:** Segurança da Informação  
**Aluna:** Heloísa Rebello Cabral | Turma 5B  
**Professor:** Edson Vaz Lopes  

## Sobre o projeto

Análise crítica de segurança em um protótipo web de registro de ocorrências acadêmicas, desenvolvida como atividade prática da disciplina.

## Estrutura

- `original/` — versão original com vulnerabilidades identificadas e comentadas
- `melhorado/` — versão com 18 melhorias de segurança implementadas
- `relatorio.pdf` — relatório técnico completo

## Principais vulnerabilidades identificadas

- Credenciais hardcoded no JavaScript
- Autenticação inteiramente no front-end (contornável)
- Ausência de controle de acesso por perfil
- CPF e senhas expostos na interface
- Logs armazenados apenas no localStorage

## Melhorias implementadas

- RBAC com controle centralizado de permissões
- Mascaramento de CPF na exibição
- Proteção contra XSS
- Timeout de sessão simulado
- Validação completa de formulários com validação de CPF

## Sistema publicado

https://heloisarebello17.github.io/Sistema-de-Ocorr-ncias-Acad-micas/