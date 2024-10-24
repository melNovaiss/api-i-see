# API I See

## Descrição
`api-i-see` é uma API REST criada com Spring Boot para gerenciar séries de usuários no site The Movie Database (TMDB) (https://www.themoviedb.org/). Ela permite que os usuários enviem uma lista de séries para serem favoritadas ou adicionadas em uma watchlist em seu perfil, integrando-se com a API do TMDB (https://developer.themoviedb.org/docs/getting-started). O projeto utiliza SLF4J para logging e ferramentas como Lombok e Spring DevTools para facilitar o desenvolvimento. O objetivo principal é facilitar a migração rápida de listas de séries favoritas para o TMDB.

### Funcionalidades
- Recebe uma lista de séries e adiciona aos favoritos ou a uma watchlist criada do usuário, integrando-se com a API do TMDB.
- Sistema de log centralizado para rastreamento de erros e monitoramento.

## Requisitos
- Java 21+
- Maven 3.8+
- IDE (recomenda-se IntelliJ IDEA)

## Instalação e Execução
Clone o repositório:
```bash
  git clone https://github.com/seu-usuario/api-i-see.git
```
- Para acessar os dados da sua conta, crie um perfil em https://www.themoviedb.org/ , em seguida, vá até 'Configurações' > 'API' > 'Criar' > 'Developer'. Aceite os termos e preencha as informações, indicando que o projeto é pessoal. Após isso, você terá acesso à sua API Key.

- Obetenha seu session_id usando essa url: https://api.themoviedb.org/3/authentication/token/new?api_key=insira_aqui
na respota copie o request_token.
- Envie uma nova requisição para essa url: https://api.themoviedb.org/3/authentication/session/new?api_key=insira_aqui
e no corpo na request mande esse json
```json
{
  "request_token": "insira_aqui"
}
```
na respota copie o session_id.

- Obtenha seu account_id usando essa url: https://api.themoviedb.org/3/account?api_key=insira_aqui&session_id=insira_aqui
 na respota copie o id.

## Endpoint
Buscar IDs das séries
- URL: /api/buscarSeriesIds
- Método: POST
- Descrição: Envia um array com os nomes das séries no corpo da requisição e recebe um array com os respectivos IDs.
Exemplo de Corpo da Requisição:
```json
[
    "Game of Thrones",
    "Looking For Alaska",
    "Love, Death and Robots"
]
```
Exemplo de Resposta:
```json
[
    1399,
    88640,
    86831
]
```

Adicionar séries aos favoritos
- URL: /api/adicionarFavoritos?accountId=insira_aqui&sessionId=insira_aqui
- Método: POST
- Descrição: Envia um array com IDs de séries e adiciona aos favoritos do usuário.
- Exemplo de Corpo da Requisição:
```json
[
    1399,
    88640,
    86831
]
```

Adicionar séries a uma watchlist
Crie uma watchlist copie o id dela e cole em 'idWatchlist' na url.
- URL: https://api.themoviedb.org/4/list/idWatchlist/items?api_key=insira_aqui&session_id=insira_aqui
- Método: POST
- Descrição: Envia um array com IDs de séries e adiciona a watchlist criado pelo usuário.
- Exemplo de Corpo da Requisição:
```json
{
    "items": [
        {
            "media_type": "tv",
            "media_id": 158762
        },
			 {
            "media_type": "tv",
            "media_id": 116135
        }
    ]
}
```

exemplo de resposta:
```json
{
	"success": true,
	"status_code": 1,
	"status_message": "Success.",
	"results": [
		{
			"media_id": 158762,
			"media_type": "tv",
			"error": [
				"Media has already been taken"
			],
			"success": false
		},
		{
			"media_id": 116135,
			"media_type": "tv",
			"error": [
				"Media has already been taken"
			],
			"success": false
		}
	]
}
```
