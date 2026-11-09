# Arquitetura

Como o código do filtra é organizado. A regra central: **cada processo é uma classe que declara seus metadados e parâmetros; um registro único reúne todas; a API e a interface só consomem esse registro.** Adicionar um processo novo não exige mexer na API nem criar tela nova.

## Camadas

| Camada | Pasta | Responsabilidade | Não pode |
|---|---|---|---|
| Core | `backend/core/` | Algoritmos sobre `numpy.ndarray`. | Importar FastAPI ou saber de HTTP. |
| API | `backend/api/` | Receber PNG e parâmetros, chamar o core, devolver o resultado. | Conter lógica de processamento. |
| Interface | `frontend/` | Carregar imagem, montar controles, exibir resultados. | Processar imagem. |

Core puro pode ser testado e usado num notebook sem subir servidor; isso também ajuda a estudar para as perguntas.

## Estrutura de pastas

```
backend/
  core/
    base.py              # Processo (classe abstrata), TipoImagem, Resultado
    registro.py          # dicionário id -> processo
    imagem.py            # ler/salvar PNG, detectar cinza ou RGB
    processos/           # uma classe por processo: metadados + parâmetros
      limiarizacao.py
      ...
    manual/              # implementação própria (função pura)
      limiarizacao.py
    biblioteca/          # mesma função via OpenCV/SciPy/scikit-image
      limiarizacao.py
  api/
    main.py              # app FastAPI
    rotas.py
  tests/
    imagens/             # PNGs de teste (cinza e RGB, pequenas)
    test_manual_vs_biblioteca.py
frontend/
  app/                   # páginas (App Router)
  components/
    ui/                  # componentes do shadcn/ui
    processos/           # seletor, formulário de parâmetros, visualizador
  lib/api.ts             # chamadas à API
```

## Contrato de um processo: classe abstrata

```python
class TipoImagem(Enum):
    CINZA = "cinza"
    RGB = "rgb"

@dataclass
class Resultado:
    imagens: dict[str, np.ndarray]   # ex.: {"resultado": ..., "laplaciano": ...}
    extras: dict[str, Any]           # ex.: histogramas
    tempo_ms: float = 0.0

class Processo(ABC):
    id: ClassVar[str]
    nome: ClassVar[str]
    grupo: ClassVar[str]                  # "Filtros no espaço", "Ruídos"...
    tipos: ClassVar[set[TipoImagem]]      # quais imagens aceita
    Parametros: ClassVar[type[BaseModel]]

    def executar(self, img: np.ndarray, params: BaseModel) -> Resultado:
        # valida o tipo da imagem, mede o tempo e chama aplicar()
        ...

    @abstractmethod
    def aplicar(self, img: np.ndarray, params: BaseModel) -> Resultado: ...
```

Exemplo de processo concreto:

```python
class Parametros(BaseModel):
    k: int = Field(128, ge=0, le=255, description="Limiar")

@registrar
class Limiarizacao(Processo):
    id = "limiarizacao"
    nome = "Limiarização"
    grupo = "Transformações de intensidade"
    tipos = {TipoImagem.CINZA, TipoImagem.RGB}
    Parametros = Parametros

    def aplicar(self, img, params):
        return Resultado({"resultado": manual.limiarizar(img, params.k)}, {})
```

**Por que classe abstrata (ABC) e não `Protocol`:** temos comportamento comum (validar tipo de imagem, medir tempo) que fica uma vez só em `executar`, e o ABC impede instanciar um processo que esqueceu `aplicar`. `Protocol` serve para classes que não controlamos, o que não é o caso.

**Por que o algoritmo fica numa função à parte (`manual/`, `biblioteca/`):** a classe só descreve o processo; o algoritmo é uma função pura `(img, ...) -> ndarray`, fácil de testar e com a mesma assinatura nas duas pastas, o que torna a comparação direta.

## Parâmetros com Pydantic

Cada processo tem um modelo Pydantic com tipo, padrão, limites e descrição. A API valida a entrada de graça, e `Parametros.model_json_schema()` gera o JSON que a interface usa para montar os controles (slider para números com `ge`/`le`, seletor para `Literal`, checkbox para `bool`). Um único lugar define cada parâmetro.

## Registro central

`@registrar` adiciona a classe a um dicionário `id -> processo`. A API expõe:

- `GET /processos`: lista com id, nome, grupo, tipos aceitos e schema dos parâmetros.
- `POST /processos/{id}`: recebe o PNG e os parâmetros, devolve as imagens (PNG em base64), extras e `tempo_ms`.

A interface pede a lista uma vez, agrupa por `grupo`, desabilita os processos cujo `tipos` não inclui o tipo da imagem carregada e gera o formulário a partir do schema. Assim, um processo novo aparece na tela sem mudar o front.

## Convenções

- **Nomes**: domínio em português (`limiarizacao`, `fatiamento_intensidade`), como no enunciado. Python em `snake_case`, classes em `PascalCase`; no front, componentes em `PascalCase.tsx`.
- **Tipagem**: type hints em todo o core, verificados com `mypy`; TypeScript em modo `strict` no front.
- **Imagens**: dentro do core sempre `np.ndarray` `uint8` (cinza `H×W`, RGB `H×W×3`). Conversões para `float` ficam dentro da função e voltam para `uint8` no final, com recorte em 0–255.
- **Formatação**: `ruff` no Python, `eslint` e `prettier` no front.

## Testes

`pytest` com um teste parametrizado pelo registro: para cada processo, roda a versão manual e a de biblioteca nas imagens de `tests/imagens/` e compara com tolerância (`np.allclose` ou PSNR mínimo). Diferenças esperadas (tratamento de borda, arredondamento) ficam documentadas no próprio teste. Ruídos, por serem aleatórios, são testados por estatística (média e desvio do ruído) com semente fixa.

## Tempo de execução

- **Processamento**: medido em `Processo.executar` com `time.perf_counter()` e devolvido como `tempo_ms`; a interface mostra esse valor.
- **Rede e renderização**: medido no front com `performance.now()` entre o envio e a imagem exibida.
- Com os dois números dá para saber se a lentidão está no algoritmo ou na interface. Filtros na frequência devem usar FFT (`numpy.fft`), e filtros no espaço devem ser vetorizados com NumPy em vez de laços em Python puro.
