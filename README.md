# Coletor setorial — Price Discovery

Coleta métricas de DRE, balanço e DFC das DFPs da CVM (Dados Abertos) para grupos
setoriais definidos em `grupos.yaml`. As empresas de cada grupo vêm da classificação
setorial da B3 (com CNPJ da própria B3) e/ou de inclusões manuais. Janela: últimos 10
exercícios por empresa, ou o maior período disponível, com o motivo do corte na aba `cobertura`.

## Estrutura do repositório
```
coletor_setorial.py
grupos.yaml
requirements.txt
.github/workflows/coletor_setorial.yml
cache_b3/empresas_b3.csv   (gerado e versionado: lista B3 com CNPJ e setor)
saidas/                    (gerado: <grupo>.xlsx e <grupo>_base.csv)
cache_cvm/                 (gerado: ZIPs da CVM; NÃO versionar -> .gitignore)
```

## Uso
```
pip install -r requirements.txt
python coletor_setorial.py setores --atualizar-b3          # 1ª vez: monta a lista B3 (~15-20 min)
python coletor_setorial.py filtrar --setor "petroleo"       # confere quem entra no filtro
python coletor_setorial.py coletar --grupo distribuidoras_combustiveis
python coletor_setorial.py descobrir "nome"                  # busca no cadastro CVM (não listadas)
```
O cache da B3 vale 30 dias (`B3_CACHE_DIAS`); depois disso só as empresas novas têm o
detalhe baixado de novo. `--atualizar-b3` força a atualização completa.

## Abas do Excel
LEIA-ME · painel · mediana_setor · cobertura (com ticker) · reapresentacoes · auditoria · base_longa.
