# Agregador de Feeds RSS/Atom (Rust)

**Feito por Guilherme Quintino dos Santos e Ana Clara Dias.**

## Sobre o projeto

O Agregador de Feeds RSS/Atom é uma aplicação desenvolvida em Rust para reunir notícias e artigos de diferentes sites em um só lugar. O programa permite cadastrar feeds RSS ou Atom, buscar novas publicações, armazená-las em um banco de dados SQLite e organizar os artigos por meio de filtros, pesquisa, favoritos e status de leitura.

O projeto pode ser utilizado pelo terminal ou por uma interface web local, acessada pelo navegador.

## Tecnologias utilizadas

- **Rust:** linguagem utilizada no desenvolvimento da aplicação.
- **SQLite:** armazenamento dos feeds e dos artigos.
- **HTML, CSS e JavaScript:** construção da interface web.
- **Tokio:** execução de tarefas assíncronas.
- **Reqwest:** comunicação HTTP para buscar os feeds.
- **feed-rs:** interpretação dos formatos RSS e Atom.
- **Serde e Serde JSON:** serialização e comunicação de dados em JSON.
- **Tiny HTTP:** servidor da interface web local.

## Como executar

É necessário ter o Rust instalado. A instalação pode ser feita pelo site: https://rustup.rs.

Com o arquivo `rss_aggregator.zip` na pasta atual, execute os comandos:

```bash
unzip rss_aggregator.zip && cd rss_aggregator
cargo build --release
cargo test
./target/release/rssagg add https://blog.rust-lang.org/feed.xml
./target/release/rssagg update
./target/release/rssagg list --unread
```

O primeiro comando extrai o projeto e acessa sua pasta. Em seguida, o programa é compilado em modo de produção, os testes automatizados são executados, um feed de exemplo é cadastrado, as publicações são atualizadas e os artigos não lidos são exibidos.

### Executar a interface web

Para iniciar a interface pelo terminal:

```bash
./target/release/rssagg serve
```

Depois, acesse no navegador:

```text
http://127.0.0.1:3000
```

## Principais funcionalidades

- **Cadastro de feeds:** adiciona fontes de notícias por meio de uma URL RSS ou Atom.
- **Atualização de publicações:** consulta os feeds cadastrados e busca novos artigos.
- **Armazenamento local:** salva os feeds e artigos em um banco SQLite.
- **Listagem e leitura:** permite visualizar artigos e marcar conteúdos como lidos ou não lidos.
- **Favoritos:** permite favoritar e remover artigos dos favoritos.
- **Pesquisa e filtros:** pesquisa pelo título ou resumo e filtra artigos por feed.
- **Interface web:** oferece uma forma visual de consultar e organizar os artigos pelo navegador.
- **Tratamento de falhas:** registra erros de atualização de um feed sem interromper a atualização dos demais.

## Comandos disponíveis

| Comando | Função |
|---|---|
| `add <url>` | Cadastra um novo feed. |
| `remove <id>` | Remove um feed. |
| `feeds` | Lista os feeds cadastrados. |
| `update` | Atualiza todos os feeds. |
| `serve` | Inicia a interface web local. |
| `list` | Lista os artigos. |
| `list --unread` | Exibe somente artigos não lidos. |
| `list --fav` | Exibe somente os artigos favoritos. |
| `list --feed <id>` | Filtra artigos por feed. |
| `list --search <texto>` | Pesquisa pelo título ou resumo. |
| `read <id>` | Marca um artigo como lido. |
| `unread <id>` | Marca um artigo como não lido. |
| `fav <id>` | Adiciona um artigo aos favoritos. |
| `unfav <id>` | Remove um artigo dos favoritos. |

## Como o projeto funciona

1. O usuário cadastra um feed informando sua URL.
2. A aplicação acessa o endereço e interpreta o conteúdo RSS ou Atom.
3. Os artigos encontrados são armazenados no SQLite.
4. Quando uma atualização é solicitada, o programa consulta os feeds cadastrados e identifica novas publicações.
5. Os artigos podem ser consultados e organizados pelo terminal ou pela interface web.

A atualização dos feeds ocorre de forma concorrente, com limite de até cinco feeds sendo consultados ao mesmo tempo. O programa também utiliza identificadores dos artigos para evitar salvar publicações duplicadas.

## Estrutura do projeto

```text
src/
├── main.rs   # Comandos do terminal e atualização dos feeds
├── feed.rs   # Download e interpretação dos feeds RSS/Atom
├── db.rs     # Operações com o banco de dados SQLite
└── web.rs    # Servidor web local e API JSON

web/
├── index.html  # Estrutura da página
├── style.css   # Estilos e layout
└── app.js      # Comunicação com a API do Rust
```

## Banco de dados

Os dados são armazenados no arquivo `rss.db`, criado automaticamente na pasta em que o programa é executado. Nele ficam registrados os feeds cadastrados e os artigos encontrados, incluindo informações utilizadas para controlar leitura e favoritos.

## Testes

O projeto possui testes automatizados, que podem ser executados com:

```bash
cargo test
```

Os testes ajudam a verificar o funcionamento das partes da aplicação e identificar possíveis problemas durante o desenvolvimento.

## Limitações conhecidas

- A atualização consulta todos os feeds cadastrados; não há atualização individual.
- A pesquisa considera apenas o título e o resumo dos artigos.
- A interface web é destinada ao uso local e não possui sistema de login.
- Cada consulta exibe no máximo 30 artigos.
- O projeto não possui notificações nem atualização automática em segundo plano.
