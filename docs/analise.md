# Análise de Requisitos e Domínio — Prato Cheio

## Stakeholders

| Stakeholder | O que quer | Interesse | Influência | Consequência para a iteração 1 |
|---|---|---|---|---|
| **Marta (Patrocinadora / Operação)** | Validar o piloto do projeto e conectar doadores a ONGs de forma rápida | Alto | Alta | Envolver diretamente na validação e aceitar requisitos de operação imediata |
| **ONGs e Cozinhas Comunitárias** | Previsibilidade sobre os alimentos disponíveis e rapidez no aceite/coleta | Alto | Alta | Entrevistar primeiro e aceitar requisitos de aceite simples agora |
| **Vigilância Sanitária (Regulador)** | Garantia de segurança alimentar e rastreabilidade mínima (tipo, quantidade, validade) | Baixo | Alta | Manter satisfeita atendendo a exigência legal de validade e tipo de alimento sem bloquear a operação |
| **Doadores (Restaurantes e Padarias)** | Cadastrar doações com extrema rapidez, sem burocracia no meio da rotina | Alto | Alta | Focar no formulário com tempo de preenchimento reduzido e poucos campos |
| **Voluntários Entregadores** | Rotas claras e bom funcionamento em celulares com conexão instável | Alto | Baixa | Manter informados; requisitos avançados de logística ficam para iterações futuras |
| **Família Atendida (Beneficiário Final)** | Receber refeições seguras, com dignidade e qualidade | Alto | Baixa | Monitorar o impacto e satisfação indiretamente através do feedback das ONGs |

---

## Objetivos de impacto

1. **Reduzir a mediana do tempo de coleta:** Reduzir o tempo decorrido entre o momento da publicação da doação pelo doador e a coleta efetiva pela ONG (linha de base: desconhecida, medir a partir do piloto).
2. **Aumentar o volume de refeições salvas:** Aumentar a quantidade total (em kg/refeições) de alimentos doados e coletados com sucesso antes do vencimento (linha de base: desconhecida, medir no piloto).
3. **Reduzir a taxa de descarte:** Reduzir o percentual de doações cadastradas que chegam ao horário limite sem que nenhuma ONG aceite ou colete (linha de base: desconhecida, medir a partir da iteração 1).

---

## Regras de negócio

### 1. Registro Mínimo de Rastreabilidade (Imposta / Exigência do Regulador)
* **Onde estava:** Exigência da Vigilância Sanitária.
* **Enunciado explícito:** Toda doação cadastrada deve conter obrigatoriamente o tipo do alimento, a quantidade estimada e a data/hora limite de validade.
* **Como verificar:** O sistema deve impedir a submissão de formulários que omitam esses três dados essenciais.

### 2. Exclusividade por Aceite (Praticada / Comportamento Atual)
* **Onde estava:** Comportamento praticado no grupo de WhatsApp ("quem responde primeiro leva").
* **Enunciado explícito:** Uma doação aceita por uma ONG muda imediatamente seu estado para "reservada", ficando indisponível para aceite por qualquer outra ONG.
* **Como verificar:** Ao realizar duas requisições simultâneas de aceite para a mesma doação, apenas a primeira deve obter sucesso e a segunda deve receber erro de indisponibilidade.

### 3. Expiração Automática por Inação (REGRA AUSENTE)
* **Onde estava:** Silêncio do caso ("o que acontece se a ONG aceita e não busca?").
* **Enunciado explícito:** Se uma ONG aceitar uma doação e não realizar a confirmação de coleta em até 2 horas (ou até o limite estipulado no cadastro), o aceite expira automaticamente e a doação volta ao status "disponível" no sistema.
* **Responsável pela decisão:** Decidido pelo time de desenvolvimento junto à operação (Marta).
* **Como verificar:** Simular uma doação aceita sem confirmação de coleta, avançar o tempo do sistema além do limite e verificar se a doação volta a ser exibida na lista de disponíveis.

---

## Conflitos de prioridade

### 1. Falas em conflito
* **Doador:** "Preciso cadastrar a doação em menos de 10 segundos no meio da correria do restaurante, senão jogo a comida no lixo por falta de tempo."
* **Vigilância Sanitária:** "Exijo o registro detalhado e rastreável da validade e do tipo de alimento para liberar a operação sem riscos à saúde pública."

### 2. Anatomia do conflito
* **Eixo do trade-off:** Quantidade de campos obrigatórios e tempo necessário para preencher o formulário de cadastro.
* **O que cada lado perde:** 
  * Se priorizar apenas o Doador: Perde-se a rastreabilidade exigida pelo regulador, arriscando o veto do piloto pela Vigilância Sanitária.
  * Se priorizar apenas a Vigilância Sanitária: Perde-se doadores devido à burocracia do preenchimento demorado.

### 3. Critério de decisão e saída adotada
* **Critério:** Na Iteração 1, o formulário exigirá apenas os 3 campos obrigatórios previstos em lei (Tipo, Quantidade e Validade), utilizando botões de seleção rápida (presets) para dispensar a digitação de texto longo.
* **Saída adotada:** Anular o trade-off (Redesenho de interface com seletores ágeis de validade e quantidade, garantindo conformidade sanitária em um tempo de preenchimento inferior a 15 segundos).