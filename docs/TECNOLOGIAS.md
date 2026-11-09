# Tecnologias

Tecnologias escolhidas para o **filtra**, aplicação web local desenvolvida para a disciplina de Introdução ao Processamento Digital de Imagens (UFPB).

| Camada | Tecnologia | Papel | Por quê |
|---|---|---|---|
| Core | Python | Implementa os algoritmos de processamento de imagens. | Linguagem padrão em PDI, com ecossistema maduro (NumPy, SciPy, OpenCV) para apoiar a implementação. |
| API | FastAPI | Expõe as funções do core para a interface via HTTP. | Framework Python leve e rápido, com documentação automática dos endpoints. |
| Interface | Next.js | Aplicação web onde o usuário carrega imagens e aplica os processamentos. | Framework React consolidado, com boa estrutura de rotas e componentes. |
| Interface | shadcn/ui | Biblioteca de componentes de interface. | Componentes prontos e acessíveis, copiados para o projeto e fáceis de adaptar. |
| Interface | Tailwind CSS | Estilização da interface. | Estilos utilitários direto nos componentes; é a base do shadcn/ui. |
