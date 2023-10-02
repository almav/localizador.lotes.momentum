# Localizador de Lotes Momentum

### Descrição
A página é projetada para permitir que os usuários selecionem um empreendimento e realizem uma busca por Quadra e Lote para visualizar a localização no mapa interativo. A posição geográfica poderá ser compartilhada por meio de qrcode, email ou whatsapp.

### Demonstração
https://momentum.localizador.almav.com.br/app.html?empreendimento=SBRR
---
https://momentum.localizador.almav.com.br/app.html?empreendimento=RSCXIII
---
https://momentum.localizador.almav.com.br/app.html?empreendimento=NVIER
---

### Estrutura Básica

```html
<!doctype html>
<html lang="pt-BR" translate="no">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="user-scalable=no, width=device-width, initial-scale=1, minimum-scale=1.0, maximum-scale=1.0, viewport-fit=cover">
    <!-- ... outras metatags ... -->
    <title>Localizador de Lotes | Momentum</title>
</head>
```

### Estilos

O código inclui estilos CSS internos:

```css
/* MAIN */
html, body {
    height: 100%;
    min-height: 100vh;
    margin: 0;
    padding: 0;
}
/* ... outros estilos ... */
```

### Dependências

O código inclui referências a vários scripts externos:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.10.2/dist/umd/popper.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.min.js"></script>
<script src="https://cdn.rawgit.com/davidshimjs/qrcodejs/gh-pages/qrcode.min.js"></script>
```

### Funcionalidade Principal

Quando a página é carregada, ela exibe uma mensagem solicitando ao usuário para selecionar um empreendimento caso o atributo `empreendimento` não seja passado na URL.

```html
<main class="form-search">
    <div id="intro">
        <p class="lead">
            <h5>Localizador de Lotes</h5><span>Selecione o empreendimento para realizar a busca por Quadra e Lote.</span>
        </p>
    </div>
    <!-- ... restante do formulário ... -->
</main>
```

### Como Utilizar

1. Acesse a página.
2. Selecione um empreendimento do dropdown.
3. Insira a Quadra e o Lote desejados.
4. Clique no botão de pesquisa para obter os resultados.

## Uso do Atributo "Empreendimento" na URL

Para pré-selecionar um empreendimento específico ao carregar a página, você pode passar o identificador do empreendimento como um atributo `empreendimento` na URL. Isso permite que os usuários ou sistemas externos direcionem diretamente para um empreendimento específico sem a necessidade de selecioná-lo manualmente no dropdown.

### Exemplo:

Suponha que você queira pré-selecionar o empreendimento "SBRR". Você pode fazer isso adicionando `?empreendimento=SBRR` ao final da URL.

```markdown
[Localizador de Lotes - Santa Bárbara Resort Residence](https://momentum.localizador.almav.com.br/app.html?empreendimento=SBRR)
```

Ao acessar o link acima, a página carregará com o empreendimento "Santa Bárbara Resort Residence" já selecionado, permitindo ao usuário inserir diretamente a Quadra e o Lote desejados.

### Lista de empreendimentos

```javascript
const optionsEmp = {
            "SBRR":{
                "id":"3",
                "name":"Santa Bárbara Resort Residence",
                "gleba":{
                    "alias":"Gleba",
                    "values":["Gleba I","Gleba II","Gleba III"],
                    "Gleba I":"4",
                    "Gleba II":"5",
                    "Gleba III":"6"
                }
            },
            "RSCXIII":{
                "id": "1",
                "name":"Riviera de Santa Cristina XIII",
                "gleba":{
                    "alias":"Setor",
                    "values":["IATE","MARINA"],
                    "IATE":"2",
                    "MARINA":"3"
                }
            },
            "NVIER":{
                "id": "6",
                "setor": "9",
                "name":"Ninho Verde I Eco Residence",
                "gleba":false
            },
            "NVIIER":{
                "id":"2",
                "setor": "3",
                "name":"Ninho Verde II Eco Residence",
                "gleba":false
            },
            "RSCI":{
                "id":"9",
                "setor": "12",
                "name": "Riviera de Santa Cristina I",
                "gleba":false
            },
            "RSCII":{
                "id":"4",
                "setor": "7",
                "name": "Riviera de Santa Cristina II",
                "gleba":false
            },
            "RSCIII":{
                "id":"5",
                "setor": "8",
                "name": "Riviera de Santa Cristina III",
                "gleba":false
            },
            "RSCIV":{
                "id":"8",
                "setor": "11",
                "name": "Riviera de Santa Cristina IV",
                "gleba":false
            },
            "TSCV":{
                "id":"7",
                "setor": "10",
                "name": "Terras de Santa Cristina V",
                "gleba":false
            }
        };
```

## Uso da API

A API do Localizador de Lotes permite que você obtenha informações detalhadas sobre um lote específico, fornecendo o identificador do empreendimento, setor, quadra e lote na URL da API.

### Endpoint:

```
https://api-localizador.momentum.almav.com/v1/<id-empreendimento>/<setor>/<quadra>/<lote>
```

### Parâmetros:

- `<id-empreendimento>`: Identificador único do empreendimento.
- `<setor ou gleba>`: Identificador do setor/gleba dentro do empreendimento.
- `<quadra>`: Identificador da quadra dentro do setor.
- `<lote>`: Identificador do lote dentro da quadra.

### Exemplo:

Suponha que você queira obter informações sobre o lote 7, da quadra AB, do setor IATE, do empreendimento com ID "RSCXIII". A URL da requisição seria:

```
https://api-localizador.momentum.almav.com/v1/1/2/AB/7
```

Ao fazer uma solicitação GET para a URL acima, a API retornará latitude e longitude sobre o lote especificado.