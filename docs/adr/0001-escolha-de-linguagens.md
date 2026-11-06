# ADR 0001 — Escolha de linguagens por componente

- **Data:** 2026-11-04
- **Status:** Aceito
- **Decisores:** Rodrigo Pereira

## Contexto

O Sentinela é um sistema modular com componentes de naturezas distintas: backend/API, persistência, agente local de coleta, integrações de segurança e interfaces. Cada componente tem requisitos próprios de desempenho, segurança, ecossistema e ergonomia.

## Decisão

Adotar uma linguagem por responsabilidade, evitando sobreposição:

| Componente | Linguagem / Tecnologia |
|---|---|
| Backend, API, autenticação, orquestração | C# / ASP.NET Core |
| Persistência | SQL / PostgreSQL |
| Agente local de monitoramento | Rust |
| Integração com ferramentas de segurança | Python |
| Interfaces (desktop e web) | TypeScript |
| Dashboard desktop | Tauri |
| App mobile | Ionic |

## Consequências

**Positivas**
- Cada linguagem resolve o problema para o qual é mais adequada.
- O aprendizado é distribuído e progressivo (ver cronograma em blocos).
- Ferramentas open source e gratuitas em todo o stack.

**Negativas / Riscos**
- Maior custo de manutenção (várias toolchains).
- Rust exige curva de aprendizado maior (mitigado pelo Bloco 4 dedicado).
- Integração entre componentes exige contratos bem definidos (HTTP/JSON, filas).

## Alternativas consideradas

- **Tudo em C#**: reduziria o número de linguagens, mas o agente local perderia as vantagens de Rust (binário pequeno, sem runtime, segurança de memória).
- **Tudo em Rust**: backend menos produtivo para CRUD/API e ecossistema de segurança menos maduro.
- **Python no backend**: descartado por desempenho e tipagem, dado o foco em aprendizado de C#.

## Referências

- Plano Sentinela v1.0, seção 2 (Visão geral da arquitetura).