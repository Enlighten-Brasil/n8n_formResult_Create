# Resposta de Formularios EnSpace [LOTE]

## Automação n8n para responder formulários EnSpace em lote.

### Como usar
1. Copie este repositório e cole na pasta `data` em seu n8n. (Caso não exista, crie uma pasta `data` na raiz do n8n).
2. Na pasta Input, coloque o arquivo `.xlsx` com os dados dos formulários a serem respondidos. 
3. Renomeie o arquivo `config.json.example` para `config.json`.
4. Preencha o arquivo `config.json` com os dados necessários.
5. Abra o n8n e importe o arquivo `workflow.json` para o seu n8n.
6. Execute o workflow.
8. Ao final, na pasta Output será gerado um arquivo `.xlsx` com a relação de formulários respondidos.


### Detalhes do arquivo `config.json`
- `apiUrl`: URL da API EnSpace. (Ex: `https://api.stage.enspace.io`).
  - (Produção) `https://api.enspace.io`
  - (Stage) `https://api.stage.enspace.io`
  - (Local) `http://localhost:1337`
- `inputFilePath`: Nome do arquivo `.xlsx` com os dados dos formulários a serem respondidos.
- `inputUniqueKey`: Nome da coluna que contém o ID único da inserção. (Caso não exista, crie uma coluna com o nome `id` e preencha com um valor único para cada linha).
- `form_id`: ID do formulário a ser respondido
- `request_email`: E-mail do usuário que irá responder os formulários.
- `inputDateFormat`: Formato da data usado no arquivo `.xlsx`. (Ex: `dd/MM/yyyy`, `MM/dd/yyyy`, `yyyy-MM-dd`)

### Tipos de campos suportados e formato de entrada
- Texto, Texto longo
  - Tipo: `string` ou `texto`
  - Exemplo: `Lorem ipsum dolor sit amet`
- Número (Moeda, Porcentagem, decimal)
  - Tipo: `number` ou `número`
  - Exemplo: `123`
  - Formato: `0.00`
- Calendário, Data, Hora* e Data e Hora*
  - Tipo: `string` ou `texto`
  - Exemplo: `01/01/2021`
  - Formato: `dd/MM/yyyy` (configurável no arquivo `config.json`)
  - *Hora e Data e Hora não são suportados no momento (sempre será preenchido como `00:00:00` sem fuso horário)
- Campos de seleção unica (Selação, Radio)
  - Tipo: `string` ou `texto`
  - Exemplo: `Opção 1`
  - Formato: Valor deve ser idêntico ao `valor` (`value`) da opção configurada no formulário
- Campos de seleção multipla - `*Em Progresso` 
  - Tipo: `string` ou `texto`
  - Exemplo: `Opção 1, Opção 2`
  - Formato: Valores devem ser idênticos aos `valores` (`values`) das opções configuradas no formulário, separados por vírgula
  - *Em Progresso: Ainda não é possível selecionar mais de uma opção
- Campos de seleção de arquivos - `*Não suportado`
  - Tipo: `string` ou `texto`
  - Exemplo: `https://www.google.com.br/images/branding/googlelogo/1x/googlelogo_color_272x92dp.png`
  - Formato: URL do arquivo
  - *Não suportado: Ainda não é possível enviar arquivos
- Seleção de usuário
  - Tipo: `number` ou `numero`
  - Exemplo: `01`
  - Formato: ID do usuário
- Campos de Relacionamento (EnRel e EnRelMulti)
  - Tipo: `string` ou `texto`
  - Exemplos: `EXEMPLO-1`, `EXEMPLO-1, EXEMPLO-2, EXEMPLO-3`
  - Formato: Referência do item relacionado, separados por vírgula quando mais de um.
- Mascara de texto
  - Tipo: `string` ou `texto`
  - Exemplo: `123.456.789-00`
  - Formato: Valor deve respeitar a máscara configurada no campo.
- Editor HTML
  - Tipo: `string` ou `texto`
  - Exemplo: `<p>Lorem ipsum dolor sit amet</p>`
  - Formato: HTML
- Documento (OnlyOffice) - `*Não suportado`
  - *Não suportado: Sem previsão de suporte


### Exemplo de arquivo `config.json`
```json
{
  "apiUrl": "https://api.stage.enspace.io",
  "inputFilePath": "input.xlsx",
  "inputUniqueKey": "id",
  "form_id": "5f9b1b3b9c6b4e0001c3b2b0",
  "request_email": "exemplo@exemplo.com",
  "inputDateFormat": "dd/MM/yyyy"
}
```

### Exemplo de formulário
![Formulário](https://i.imgur.com/6ZQZQ8X.png)
### Campos
- nome: Texto
- registro: Calendário
- salario: Número
- Seleção: Seleção única
- Relacionamento: Relacionamento
- Relacionamento Multi: Relacionamento Multi

### Exemplo de arquivo `.xlsx`
| id | nome | registro | salario | Seleção | Relacionamento | Relacionamento Multi
| --- | --- | --- | --- | --- | --- | --- | 
| 1 | João | 01/01/2021 | 123.45 | Opção 1 | EXEMPLO-1 | | 
| 2 | Maria | 02/02/2021 | 456.78 | Opção 2 | EXEMPLO-2 | EXEMPLO-1, EXEMPLO-3 |
| 3 | José | 03/03/2021 | 789.01 | Opção 3 | EXEMPLO-3 | |
| 4 | Joana | 04/04/2021 | 012.34 | Opção 4 | EXEMPLO-4 | |
| 5 | Pedro | 05/05/2021 | 345.67 | Opção 5 | EXEMPLO-5 | |













