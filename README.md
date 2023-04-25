# Desafio-protheus

Para a execução não é necessário a instalação de _Softwares_, a aplicação foi desenvolvida no ambiente _Google Colaboratory_ que é um ambiente de desenvolvimento integrado (_IDE_) baseado em nuvem, que permite aos usuários escrever, executar e compartilhar códigos e documentos colaborativos. Ele é projetado para trabalhar com a linguagem de programação _Python_ e é executado no navegador da _web_, o que significa que não é necessário configurar um ambiente de desenvolvimento em seu próprio computador. Além disso, o _Colab_ oferece recursos gratuitos de alto desempenho, como _CPUs_ e _GPUs_, para executar códigos complexos e pesados de forma rápida e eficiente. Ele também permite importar bibliotecas populares de _Python_, como _NumPy_, _Pandas_ e _TensorFlow_, entre outras.

## Execução

### Passos

* Efetuar o Download do arquivo ```.zip``` ```desafio-protheus```, descompacte o mesmo;

![image](https://user-images.githubusercontent.com/130913679/234148704-d90e12e6-0fa3-4e80-9903-231ab1132dba.png)

* Acesse o ambiente de desenvolvimento _Google Colaboratory_, disponível no link (https://colab.research.google.com/);
* Ir até a aba Arquivo -> Fazer _upload_ de _notebook_ -> Escolher Arquivo e seleciona o arquivo ```desafio_protheus.ipynb```.

![image](https://user-images.githubusercontent.com/130913679/234142958-c74401f0-3b5d-467e-ab7e-44edf00d1f39.png)
![image](https://user-images.githubusercontent.com/130913679/234143056-83db5b77-4938-4412-8e10-99b0ebd7b771.png)

* Após feito _upload_ ir até a aba Ambiente de Execução -> Executar Tudo. Agora só aguardar o processo de execução do Projeto ser concluído.

![image](https://user-images.githubusercontent.com/130913679/234143472-d65d447d-620a-4787-9760-7364d1642ad5.png)

* Depois de concluído é possível verificar os seguintes itens na aba lateral da feramenta:
 * ```desafio_protheus.bd```: Banco de Dados relacional;
 * ```siglas.json```: Arquivo contendo todas as siglas das ações presentes na _API_;  
 * ```dados.pdf```: Arquivo PDF com todas as informações das ações.

Estes arquivos podem ser baixados para posterior verificação dos dados presentes nos mesmos.

## Funcionamento

1. Instala o pacote FPDF no ambiente Python. O FPDF é um pacote para criação de documentos PDF em _Python_. Com ele, é possível criar documentos PDF programaticamente, adicionando textos, imagens e tabelas, por exemplo.

![image](https://user-images.githubusercontent.com/130913679/234136322-daeee4d7-d327-4b85-b10f-8df9bd1ab206.png)

2. Esse trecho de código importa as bibliotecas necessárias para o projeto:

  * __sqlite3_: biblioteca para trabalhar com banco de dados _SQLite_;
  * __requests_: biblioteca para fazer requisições _HTTP_;
  * __json_: biblioteca para trabalhar com _JSON_;
  * __datetime_: biblioteca para trabalhar com datas e horários;
  * _fpdf_: biblioteca para criar arquivos PDF.

![image](https://user-images.githubusercontent.com/130913679/234136232-09d934fa-9275-444e-afa0-b8009c010816.png)

3. Essa parte do código cria uma conexão com o banco de dados ```desafio_protheus.bd``` e cria duas tabelas: **Acao** e **Cotacao**.

  * A tabela **Acao** possui três colunas: _idAcao_, simbolo e nome. A coluna _idAcao_ é uma chave primária que identifica exclusivamente cada ação, enquanto as colunas _simbolo_  e _nome_ armazenam o símbolo e o nome da ação, respectivamente.

  * A tabela **Cotacao** possui sete colunas: _idAcao, idCotacao, Cotacao, ValorMercado, VolumeTransacoes, Moeda e Data_. A coluna _idCotacao_ é uma chave primária que identifica exclusivamente cada registro de cotação, enquanto a coluna _idAcao_ é uma chave estrangeira que relaciona cada cotação com uma ação. As colunas _Cotacao, ValorMercado, VolumeTransacoes, Moeda e Data_ armazenam os valores correspondentes à cotação da ação no momento específico.

![image](https://user-images.githubusercontent.com/130913679/234136351-cd55cb3d-e6cd-4878-abc2-9ec977fab34f.png)

4. Essa parte do código faz o download de uma lista de siglas de ações disponíveis a partir de uma _API_ (https://brapi.dev/api/available) e armazena essas siglas em um arquivo _JSON_ chamado ```siglas.json```. O objetivo é obter as siglas para depois fazer consultas de cotações das ações utilizando _APIs_. O processo consiste em fazer uma solicitação _GET_ para a _API_, verificar se a resposta foi bem-sucedida, converter a resposta para um objeto _Python_, criar um objeto _Python_ com as siglas e escrever o objeto _Python_ em um arquivo _JSON_. Ao final, imprime uma mensagem indicando que as siglas foram armazenadas com sucesso.

![image](https://user-images.githubusercontent.com/130913679/234136397-5bccea6d-07f0-4930-8ddc-c160730b56ff.png)

5. Essa parte do código é responsável por fazer uma solicitação _GET_ para a _API_ da ```brapi.dev``` para cada sigla presente no arquivo ```siglas.json```. Se a resposta da _API_ retornar um ```status_code``` igual a _200_, os dados da cotação são extraídos da resposta _JSON_ e inseridos no banco de dados usando a função ```inserir_cotacao_bd()```. Se o ```status_code``` não for _200_, uma mensagem de erro é exibida informando que houve um problema ao consultar a sigla correspondente.

![image](https://user-images.githubusercontent.com/130913679/234136735-1014c9b9-7471-4119-a11d-d3e4f5309c18.png)
![image](https://user-images.githubusercontent.com/130913679/234136807-c19a0195-37cd-4dc4-8050-091c503d4108.png)

6. Esta etapa cria um arquivo PDF chamado ```dados.pdf``` e adiciona uma página a ele. Em seguida, busca os dados do banco de dados criado anteriormente, percorre os resultados da consulta e adiciona as informações de cada ação em linhas separadas. As informações incluem o símbolo da _ação, o nome, a cotação, o valor de mercado, o volume de transações, a moeda e a data_. Depois de adicionar todas as informações, o PDF é salvo e fechado.

![image](https://user-images.githubusercontent.com/130913679/234136863-0dd924ec-1007-4250-a1e5-23eafd1e071e.png)
