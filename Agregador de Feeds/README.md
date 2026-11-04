# Agregador de Feeds RSS/Atom (Rust)

**Feito por Guilherme Quintino dos Santos e Ana Clara Dias.**

Projeto desenvolvido em Rust para cadastrar e atualizar feeds RSS/Atom, armazenar artigos em um banco de dados SQLite e permitir a leitura e filtragem de notícias pelo terminal ou por uma interface web local.

## Como executar

Com o arquivo `rss_aggregator.zip` na pasta atual, execute:

```bash
unzip rss_aggregator.zip && cd rss_aggregator
cargo build --release
cargo test
./target/release/rssagg add https://blog.rust-lang.org/feed.xml
./target/release/rssagg update
./target/release/rssagg list --unread
```

## Principais funcionalidades

- Cadastro e remoção de feeds RSS/Atom.
- Atualização dos feeds e armazenamento dos artigos em SQLite.
- Listagem de artigos não lidos e gerenciamento de favoritos.
- Pesquisa e filtros por feed.
- Interface web local para consultar e organizar os artigos.

O banco de dados `rss.db` é criado automaticamente na pasta em que o programa é executado.
