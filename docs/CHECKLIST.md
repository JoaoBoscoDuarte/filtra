# Checklist do projeto

Acompanhamento de cada processo exigido no enunciado (Avaliação da 3ª unidade, Introdução ao PDI, UFPB). Marque `[x]` quando a etapa estiver concluída e escreva o nome em **Implementado por**. O fluxo de cada coluna está em [CONTRIBUICAO.md](CONTRIBUICAO.md).

- **Estudado**: cada um estudou o processo e sabe explicar o resultado esperado (as perguntas da avaliação são individuais).
- **Revisado por**: revisão cruzada; quem implementou não revisa o próprio código.
- **Revisão final**: revisão mais profunda, feita pelos dois juntos, depois da revisão cruzada.
- **Confirmado com biblioteca**: resultado da implementação manual comparado com o da biblioteca especializada.
- **Desempenho ok**: tempo de processamento e de renderização medidos e aceitáveis.

## Decomposição de cores (só RGB)

| Processo | Parâmetros | Estudado João | Estudada Mari | Implementado por | Revisado por João Bosco | Revisado por Mari | Revisão final | Confirmado com biblioteca | Desempenho ok |
|---|---|---|---|---|---|---|---|---|---|
| Componentes RGB | — | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Componentes HSV | — | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |

## Transformações de intensidade

| Processo | Parâmetros | Estudado João | Estudada Mari | Implementado por | Revisado por João Bosco | Revisado por Mari | Revisão final | Confirmado com biblioteca | Desempenho ok |
|---|---|---|---|---|---|---|---|---|---|
| Limiarização | limiar k | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Transformação logarítmica | ganho c | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Transformação de potência | ganho c, gama γ | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Equalização de histograma (só cinza) | mostrar histogramas antes e depois | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Fatiamento por intensidade | faixa [A, B], preservar fundo ou zerar | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |

## Filtros no espaço

Todos devem permitir alterar o tamanho da janela.

| Processo | Parâmetros | Estudado João | Estudada Mari | Implementado por | Revisado por João Bosco | Revisado por Mari | Revisão final | Confirmado com biblioteca | Desempenho ok |
|---|---|---|---|---|---|---|---|---|---|
| Média gaussiana | desvio padrão σ, janela | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Mediana | janela | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Mínimo | janela | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Máximo | janela | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Mediana adaptativa | tamanho máximo da janela | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Máscara de aguçamento | ganho, janela | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Realce por Laplaciano | mostrar imagem realçada e Laplaciano ajustado, janela | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Gradiente de Sobel | mostrar gradiente, janela | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |

## Filtros na frequência

| Processo | Parâmetros | Estudado João | Estudada Mari | Implementado por | Revisado por João Bosco | Revisado por Mari | Revisão final | Confirmado com biblioteca | Desempenho ok |
|---|---|---|---|---|---|---|---|---|---|
| Passa-baixa gaussiano | frequência de corte | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Passa-alta gaussiano | frequência de corte | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Passa-baixa de Butterworth | frequência de corte, ordem | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Passa-alta de Butterworth | frequência de corte, ordem | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |

## Ruídos

| Processo | Parâmetros | Estudado João | Estudada Mari | Implementado por | Revisado por João Bosco | Revisado por Mari | Revisão final | Confirmado com biblioteca | Desempenho ok |
|---|---|---|---|---|---|---|---|---|---|
| Ruído gaussiano aditivo | intensidade, distribuição | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Ruído sal | — | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Ruído pimenta | — | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |
| Ruído sal e pimenta | distribuição | [ ] | [ ] |  | [ ] | [ ] | [ ] | [ ] | [ ] |

## Requisitos gerais

| Requisito | Implementado por | Revisado por João Bosco | Revisado por Mari | Revisão final |
|---|---|---|---|---|
| Carregar imagem `.png` |  | [ ] | [ ] | [ ] |
| Suporte a cinza 8 bits e RGB 24 bits |  | [ ] | [ ] | [ ] |
| Desabilitar processos que não se aplicam ao tipo da imagem |  | [ ] | [ ] | [ ] |
| Ver original e resultado(s) lado a lado o tempo todo |  | [ ] | [ ] | [ ] |
| Ajustar os parâmetros de cada processo na interface |  | [ ] | [ ] | [ ] |
| Mostrar informações extras (histogramas, Laplaciano etc.) |  | [ ] | [ ] | [ ] |
| Salvar o resultado em novo `.png` |  | [ ] | [ ] | [ ] |
| Execução fácil (instruções e ambiente prontos) |  | [ ] | [ ] | [ ] |
| Revisão geral da interface atrás de erros |  | [ ] | [ ] | [ ] |

## Preparação para a avaliação

- [ ] Ensaio com 4 processos sorteados e parâmetros escolhidos pelo outro membro
- [ ] João explica o resultado esperado de todos os processos sem ajuda
- [ ] Mari explica o resultado esperado de todos os processos sem ajuda
