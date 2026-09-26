# Probabilidade por etapa e previsão ponderada do funil

Issue #1535.

- `crm_stages.win_probability` (0–100, nullable): quanto a etapa costuma
  converter, calibrado por quem gere a equipe. `is_won`/`is_lost` valem 100 e 0
  na regra, não gravado.
- `lib/leads/previsao.ts`: regra pura que agrupa os negócios abertos por moeda ×
  mês de `expected_close_date` em `ponderado_cents`/`bruto_cents`/`n`, com balde
  "sem data" e balde "sem probabilidade" reportados à parte (nunca somados como
  zero em silêncio).
- Fonte da probabilidade por funil em `crm_pipelines.settings.previsao.fonte`:
  `"etapa"` (padrão) ou `"ia_quando_houver"` (usa `ai_probability` quando
  existe e cai para a etapa quando não).
- `GET /api/v1/pipelines/[id]/forecast` (papel agent, cliente de sessão para
  respeitar a visibilidade por atendente) e a tool MCP
  `crm_get_pipeline_forecast`.
- Kanban: linha "ponderado" sob o total da coluna. `/app/metrics`: painel
  "Previsão" por mês × moeda.

Aditivo: com a probabilidade nula por padrão, nada muda até alguém configurar.
