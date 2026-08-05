# Documento de Análise — Prato Cheio

*Trabalho 1 · máximo 4 páginas · entrega na Aula 5*

## Problema central
Diariamente, estabelecimentos comerciais lidam com o excedente de alimentos em perfeitas condições, que acabam no lixo devido à falta de logística rápida. Simultaneamente, ONGs precisam de doações constantes. O problema central é a ausência de uma conexão ágil entre quem tem alimento sobrando e quem precisa dele, antes que passe do prazo de consumo.

## Incertezas
- Os doadores (restaurantes/mercados) terão tempo para usar o sistema durante o expediente?
- As ONGs terão logística (transporte e pessoal) para retirar as doações a tempo?
- Como garantir a segurança alimentar dos itens doados?

## Stakeholders
| Stakeholder | Interesse | Influência | O que espera |
|---|---|---|---|
| **Doadores (Restaurantes, Mercados)** | Evitar desperdício e contribuir socialmente | Alta | Um processo rápido, sem burocracia e que não atrapalhe a rotina de trabalho. |
| **ONGs / Projetos Sociais** | Captar alimentos para pessoas em vulnerabilidade | Alta | Previsibilidade, clareza sobre o que está disponível e facilidade de reserva. |
| **Equipe de Desenvolvimento** | Construir um software funcional e validado | Média | Cumprir os requisitos da disciplina (CI verde, testes) e entregar valor contínuo. |

## Objetivos de impacto
1. Reduzir o volume de alimentos em boas condições que são descartados diariamente.
2. Aumentar a capacidade de atendimento das ONGs locais.
3. Minimizar o tempo de conexão entre a disponibilidade de uma doação e a sua coleta.

## Regras de negócio
- Uma doação só pode ser aceita por uma única ONG (exclusividade).
- A publicação de uma doação recusa submissões sem os campos obrigatórios (descrição e quantidade).
- Após ser aceita, a doação deve ser imediatamente removida da lista de itens disponíveis.

## Histórias de usuário
| # | História (Como… quero… para…) | INVEST: o que falha |
|---|---|---|
| **1** | **Como** doador, **quero** publicar uma doação com descrição e quantidade **para** que ONGs possam recolher meu excedente. | *Nenhuma falha.* É pequena, independente e testável no walking skeleton. |
| **2** | **Como** ONG, **quero** visualizar as doações disponíveis e aceitar uma delas **para** garantir alimento para minha instituição. | *Nenhuma falha.* Entrega valor imediato ao conectar as duas pontas. |

## Critérios de aceite
**História 2** — **Dado** que existe uma doação de "50 marmitas" na lista de disponíveis, **Quando** a ONG clica para aceitar a doação, **Então** o sistema marca a doação como aceita pela ONG e remove o item da lista de doações disponíveis.

## Riscos
| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Baixa adoção pelos doadores por acharem o sistema complexo | Média | Alto | Focar o *walking skeleton* em uma interface de publicação extremamente minimalista. |
| Duas ONGs tentarem aceitar a mesma doação ao mesmo tempo | Alta | Alto | Implementar bloqueio no banco de dados para garantir que apenas o primeiro clique registre o aceite (regra testada). |
| Alimento estragar antes da coleta | Alta | Alto | (Futuro) Estabelecer janelas de horário rígidas para retirada no momento da doação. |

## Hipótese e experimento
**Hipótese:** Acreditamos que a barreira para a doação é o tempo gasto na comunicação. Se reduzirmos o tempo de publicação para menos de 2 minutos, os estabelecimentos doarão mais.
**Experimento:** O *Walking Skeleton* (U1) vai provar a viabilidade técnica da publicação e reserva em fluxo direto, validando se as regras de concorrência se mantêm intactas com o banco de dados.

## Decisão de análise
- **Problema:** Como lidar com a concorrência se várias ONGs quiserem a mesma doação?
- **Alternativas:** (A) Criar uma fila de espera; (B) Adotar o modelo "primeiro a aceitar, leva".
- **Decisão e justificativa:** Optamos pela alternativa (B). É mais condizente com a necessidade de escoamento rápido de alimentos perecíveis e simplifica a implementação do *walking skeleton*.
- **Riscos e limitações:** ONGs menores ou com menos acesso à internet podem ser prejudicadas por não conseguirem aceitar doações a tempo.

## Uso de IA
**O que geramos com IA:** Estruturação inicial dos tópicos de Stakeholders, Riscos e Histórias de Usuário utilizando o Gemini.
**O que verificamos e o que alteramos:** Verificamos se o escopo se mantinha alinhado às restrições do *Walking Skeleton* da Unidade 1, alteramos os critérios de aceite para refletirem especificamente os testes exigidos no projeto (aceitar doação e removê-la da lista) e adaptamos as regras de negócio à realidade do desenvolvimento local.