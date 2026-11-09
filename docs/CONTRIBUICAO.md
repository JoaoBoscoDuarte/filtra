# Organização e contribuição

Projeto em dupla: João Bosco e Maria Mariana (Mari). O progresso fica em [CHECKLIST.md](CHECKLIST.md).

## Fluxo de cada processo

1. **Estudar**: os dois estudam o processo, já que as perguntas da avaliação são individuais.
2. **Implementar**: uma pessoa implementa o processo do zero e registra o nome no checklist.
3. **Comparar com a biblioteca**: a mesma pessoa aplica o processo com uma biblioteca especializada (OpenCV, SciPy, scikit-image etc.) e compara os resultados nas mesmas imagens e parâmetros. Diferenças precisam ser explicadas (borda, arredondamento, normalização).
4. **Revisão cruzada**: a outra pessoa revisa código, resultado e comparação. Quem implementou não revisa o próprio trabalho.
5. **Revisão final**: depois da revisão cruzada, os dois fazem juntos uma revisão mais profunda: casos-limite (imagem toda preta ou branca, janela grande, parâmetros extremos), cinza e RGB, e se o resultado é coerente com a teoria.
6. **Desempenho**: medir o tempo de processamento e de exibição. Se ficar lento, otimizar antes de marcar como concluído.

## Implementação manual e de biblioteca

As duas versões ficam no projeto, em pastas separadas e com o mesmo nome de arquivo e de função:

```
core/
  manual/       # implementação própria (é a que a interface usa)
    limiarizacao.py
  biblioteca/   # mesma operação via biblioteca, só para comparação
    limiarizacao.py
```

Pastas em vez de prefixo ou sufixo porque deixam claro qual versão é qual sem poluir os nomes, e o mesmo nome de arquivo facilita comparar as duas.

## Interface

- Sempre revisar o front atrás de erros: console do navegador, estados de carregamento, parâmetros inválidos, imagem cinza x RGB.
- Considerar o tempo de renderização além do de processamento: evitar reprocessar a cada pequena mudança de parâmetro e exibir indicação de carregamento em processos lentos.
