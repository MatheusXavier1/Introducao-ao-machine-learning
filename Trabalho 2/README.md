# Previsão de Preço de Imóveis Residenciais

Trabalho 2 da disciplina Introdução a Machine Learning (eletiva), Engenharia de Controle e Automação, Escola Politécnica da UFRJ, 6º período.

**Autor:** Matheus Xavier Martins

## Problema

Estimar o preço de venda de imóveis residenciais de uma cidade brasileira a partir de ofertas publicadas em site especializado. É um problema de regressão supervisionada.

- **Treino:** 4683 imóveis, com 20 características e o preço de venda.
- **Teste:** 2000 imóveis, só com as características. O preço é o valor a estimar.
- **Total:** 6683 imóveis.

## Arquivos

|Arquivo|Conteúdo|
|---|---|
|`conjunto_de_treinamento.csv`|Características e preço dos 4683 imóveis de treino|
|`conjunto_de_teste.csv`|Características dos 2000 imóveis de teste|
|`exemplo_arquivo_respostas.csv`|Formato esperado da submissão (preços estimados para o teste)|
|`onehot.py`|Script do one-hot encoding|
|`conjunto_de_treinamento_onehot.csv`|Treino codificado, com as 10 binárias originais (107 colunas)|
|`conjunto_de_treinamento_onehot_sem_originais.csv`|Treino codificado, sem as 10 binárias originais (97 colunas)|

## Dados

|Campo|Descrição|
|---|---|
|`Id`|Identificação única do imóvel|
|`tipo`|Apartamento, casa, loft ou quitinete|
|`bairro`|Bairro do imóvel|
|`tipo_vendedor`|Imobiliária ou pessoa física|
|`quartos`|Número de quartos|
|`suites`|Número de suítes|
|`vagas`|Vagas de garagem|
|`area_util`|Área útil (m²)|
|`area_extra`|Área extra (m²)|
|`diferenciais`|Texto com as duas principais características que diferenciam o imóvel|
|`churrasqueira`, `estacionamento`, `piscina`, `playground`, `quadra`, `s_festas`, `s_jogos`, `s_ginastica`, `sauna`, `vista_mar`|1 se o anúncio menciona o item, 0 caso contrário|
|`preco`|Preço de venda (alvo, só no treino)|

Detalhes:

- `estacionamento` se refere a estacionamento para visitantes.
- `quadra` cobre quadra poliesportiva, quadra de squash e campo de futebol.
- As 10 colunas binárias vêm da coluna `diferenciais`.

Composição do treino:

- `tipo`: 4501 apartamentos, 177 casas, 3 lofts, 2 quitinetes.
- `tipo_vendedor`: 4556 imobiliárias, 127 pessoas físicas.
- `bairro`: 66 bairros, com Boa Viagem concentrando 1599 imóveis.
- Não há valores nulos.

## Pré-processamento

One-hot encoding completo (sem `drop_first`), feito em `onehot.py`:

- `tipo` gera 4 colunas, `bairro` gera 66 e `tipo_vendedor` gera 2.
- `diferenciais` é multi-label, separado por " e ", e gera 18 colunas `diferenciais_*`.
- As colunas de texto originais saem do dataset.

As 10 binárias originais não cobrem todos os diferenciais. Faltam copa (321 imóveis), esquina (101), children care (6), vestiário (4) e hidromassagem (3), o que afeta 427 imóveis. Em 103 deles, as 10 binárias aparecem todas zeradas, igual a um anúncio sem diferencial nenhum. As colunas `diferenciais_*` resolvem isso, e por isso existe a versão sem as originais.

Para aplicar o mesmo tratamento no teste, as colunas precisam ser alinhadas às do treino (categorias ausentes no teste entram zeradas, categorias novas são descartadas).

## Modelagem

A preencher: modelos testados, validação e métricas.

## Resultados

A preencher.

## Como reproduzir

```bash
python3 onehot.py
```

Requer Python 3 com `pandas`. O script lê `conjunto_de_treinamento.csv` e gera o CSV codificado.