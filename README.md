### NOS Automation Testing

**1. Escolher uma ferramenta para automatizar testes à seguinte Api REST, explica o porquê dessa escolha. https://gorest.co.in/**

*Resposta:* A ferramenta escolhida foi o **Postman**. Ele se tornou popular entre desenvolvedores e testers de API por ter uma interface amigável. É uma ferramenta com uma ótima usabilidade, permitindo organizar bem as requisições e testes de forma simples e clara. Além disso, ele também tem suporte multiplataforma. De acordo com algumas pesquisas, podemos ver que o Postman está entre as 10 melhores ferramentas para testes de API e é utilizado por muitas empresas.

**2. Explica os use case de teste;**

*Resposta:* O objetivo dos casos de testes é conseguir visualizar que a API está retornando os dados esperados nos formatos esperados na requisição que foi feita. Além disso, ajudam a identificar problemas em lugares específicos quando alguma coisa não estiver retornando da maneira correta, ajudando assim a encontrar e solucionar o problema com mais eficácia.

Nos testes realizados nessa API, mais especificamente com a resposta da requisição gorest.co.in/public/v2/todos, estou validando que os campos estejam sendo preenchidos com os tipos certos de dados e no formato correto.

Campos como ```"id"``` e ```"user_id"``` são campos numéricos então devem sempre conter respostas com números inteiros. Os outros campos como ```"title", "due_on"``` e ```"status"``` devem conter textos, no caso, strings.

No caso do campo ```"due_on"```, valido também que esteja no formato date-time que é a data e a hora.
Além disso, valido também se o campo "status" está com a informação "completed" em todas as respostas. No caso dessa resposta da API, existem alguns como "pending", portanto o teste não vai passar por não serem todos "completed".
Se algum desses campos receber alguma informação diferente dos formatos validados no schema, então os testes vão falhar e vamos conseguir identificar onde estava a resposta incorreta.

**3. Em automação, com resposta desta API gorest.co.in/public/v2/todos**
  * **3.1. Aplica uma validação de schema ao resultado;**
    
*Resposta:* A utilização de schema valida se os campos da resposta estão preenchidos no formato correto. Considerando isso e verificando a resposta da API, vemos que temos os campos ```"id", "user_id", "title", "due_on"``` e ```"status"``` sendo ```"id"``` e ```"user_id"``` do tipo integer e ```"title", "due_on"``` e ```"status"``` do tipo string, portanto, fiz a validação conforme o código também disponível aqui no repositório. 
De acordo com o teste, se alterarmos o tipo de uma das propriedades para um diferente do que realmente é, o teste não vai passar. Por exemplo, se colocarmos o ```“id”``` com o type string, o teste não vai passar já que o formato que deve aparecer nas respostas é o tipo integer. Isso consegue validar se as respostas estão sempre vindo no tipo esperado.

  * **3.2. Valida se todos os resultados têm status completed;**
    
*Resposta:* Para este teste, armazenei a resposta JSON em uma variável para usá-la para verificar a propriedade ```“status”```. Também criei uma variável do tipo booleana para armazenar o status. Dito isso, iterei a resposta verificando o status de cada item dentro da resposta JSON e, caso o status não fosse “completed” a variável seria marcada como false. No caso desse teste, verificamos no final se todos os itens são “completed” (true), caso tenha algum diferente (false), o teste vai falhar já que esperamos que todos sejam true.

  * **3.3. Interpreta e valida o valor “due_on”**
    
*Resposta:* Considerando que precisamos validar também o campo ```“due_on”```, conseguimos fazer isso na mesma schema do item 3.1.
Analisando a resposta conseguimos ver que o tipo nesse campo é o de data e hora, dessa forma, conseguimos fazer a validação de que o tipo do campo ```“due_on”``` é um string com o formato de data e hora. 

**4. DevOps, CI/CD.**
  * **4.1. Explica e justifica uma implementação de testes de carga a esta API;**
    
*Resposta:* Os testes de carga da API exige que exitam muitas requisições simultâneas com o objetivo de avaliar o desempenho da API, identificar limites de capacidade, gargalos e assegurar que ela vai conseguir lidar com o número de requisições sem que isso prejudique o funcionamento. Para a implementação então seria necessário escolher uma ferramenta, como o JMeter, por exemplo, preparar o ambiente e os dados de teste e configurar relatórios. Também é importante se certificar que o ambiente em que os testes serão executados seja o mais próximo possível do ambiente de produção. Logo depois da execução é preciso analisar os resultados para ver como a API reagiu a elevação de carga e assim tomar as medidas necessárias.

  * **4.2. Como implementarias uma solução de Continuous Testing, justifica;**
  * 
*Resposta:* Para implementar o Continuous Testing, eu, juntamente com a equipe, definiria e configuraria um ambiente de Integração Contínua (CI), como o Azure DevOps que tem ferramentas tanto para integração contínua (CI) quanto para entrega contínua (CD), ou outro como Jenkins, GitLab e etc. Após essa definição e configuração, reuniríamos e/ou criaríamos testes automatizados tanto unitários como de integração, funcionais e regressão e faríamos a integração desses testes na Pipeline, de forma que eles serão executados automaticamente sempre que forem feitas alterações no código, possibilitando assim a visibilidade melhor nos builds, onde eles só serão feitos se todos os testes passarem.
Outro ponto importante é configurar relatórios e até mesmo notificações no e-mail, por exemplo, assim é possível acompanhar se algo acontecer. Com essa implementação, também é possível criar métricas para o melhor monitoramente e cobertura do sistema
