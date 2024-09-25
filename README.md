# Case Dadosfera:
Abaixo segue o case com as respostas

[Apresentação do case](https://youtu.be/rQGkaggsq9I)


# Item Troubleshooting

Antes de responder como se estivesse interagindo com o cliente, gostaria de pontuar algumas coisas que observei enquanto fazia uns testes para aprender a mexer na plataforma.

Primeiramente, o pipeline sugerido não está sincronizando. Por conta disso, ele não está mostrando os logs de erro. Durante minha participação no treinamento do Datamesh ministrado pelo Allan, percebi que erros como esse podem ocorrer por conta do excesso de requisições da plataforma, ou algum problema de conexão momentâneo. Além disso utilizando o Charles Proxy, pude ver que ele não apresenta nenhum erro de requisição ou permissão, entretanto ele apresenta os codigos 204 e 304 do HTTP, que indicam respectivamente que a solicitação foi bem-sucedida, mas o servidor não precisa retornar qualquer dado no corpo da resposta e que o recurso solicitado não foi modificado desde a última vez que foi acessado.  

Dando sequência, eu baixei exatamente o mesmo dataset utilizado no dito pipeline para verificar se geraria algum erro em relação ao formato do dataset, mas a sincronização foi um sucesso, consigo visualizar os dados tanto na plataforma da Dadosfera quanto no Metabase, então, a meu ver, não há nenhum problema nos dados colocados no pipeline.

Em vista disso, eu sugeriria ao cliente tentar gerar o pipeline novamente, tomando cuidado para não esquecer de salvar o arquivo como planilha google sheets para evitar o erro 400, referente a erro na operação quando a operação não é suportada pelo documento.

Continuando, eu diria ao cliente para, após observar se nenhum dos passos citados anteriormente foi esquecido, dar continuidade ao procedimento. Além disso, é importante alertar o cliente sobre os dados suportados e não suportados pela plataforma:
> DADOS SUPORTADOS

> * Numéricos: number, decimal numeric, int, integer, bigint, smallint, byteint, float, float4, float8, double, double precision, real
> * String e binários: varchar, char, character, string, text, binary, verbinary
> * Lógicos: boolean
> * Data e hora: date, datetime, time, timestamp, timestamp_ltz, timestamp_ntz, timestamp_tz,
> * Semiestruturados: variant, object, array
> * Geoespaciais: geography

> DADOS NÃO SUPORTADOS
> * LOB (Large Object): blob, clob
> * Outros: enum, user-defined data type


### Como eu responderia isso ao cliente:

Abaixo vou simular uma resposta que eu daria para um cliente. O nome fictício desse cliente será Maria.


> Dona Maria, tente gerar o pipeline novamente, já que ele não está sincronizando, pode ter ocorrido um erro de requisição. Como não estão aparecendo os logs de erro, não podemos precisar com certeza o que aconteceu de fato. Por conta disso, sugiro que você tente enviar a requisição novamente criando outro pipeline para subir os dados, seguindo a recomendação da nossa documentação: suba os dados para o drive, abra-o como planilha Google Sheet e salve como como planilha google sheets após abrir o arquivo no Drive, lembre-se desse detalhe para evitar o erro 400, referente a erro na operação quando a operação não é suportada pelo documento, como mostrado na imagem, abaixo, você pode seguir esses passos com a planilha aberta seguir o seguinte caminho: Arquivo > Salvar como planilhas google.
Uma alternativa para subir os dados na plataforma, é converter esse arquivo para csv. Na nossa plataforma, atualmente não é possível subir diretamente um arquivo no formato excel (xslx). Nesse sentido, você pode converter suas planilhas excel para arquivo csv, indo em: Arquivo > Salvar Como > Selecionar o formato CSV > clicar em salvar > escolher local do arquivo. Logo após, poderá subir os dados para a plataforma da dadosfera, indo no menu lateral e clicando em importar arquivos. Logo após, você pode clicar em Novo Arquivo, selecionar o tipo no menu suspenso, arrastar ou selecionar o arquivo, depois apenas esperar a sincronização ser realizada.
Outros cuidados que a senhora deve tomar é com o formato dos dados enviados para a planilha. Como a plataforma da dadosfera é integrada nativamente com o Data Warehouse Snowflake que permite realizar consultar e criar views dos dados utilizando SQL. Dito isso, atente-se para não enviar planilhas contendo dados binários muito longos (BLOB – Binary Large Object) ou cacteres muito longos (CLOB – Character Large Object), além de dados do tipo ENUM que são colunas em um dataset que só permitem armazenar um conjunto específico de dados.
Caso deseje ajuda com mais alguma coisa, sinta-se à vontade para nos contatar aqui no suporte, tenha um bom dia. Estamos aqui para ajudar e garantir que você tenha uma experiência tranquila com Dadosfera.

# Item Processos Internos

Para a implementação de uma nova plataforma de gerenciamento de diretório em nuvem com SSO e recursos de vida de usuários, considerando que é um processo robusto e os processos iniciais como planejamento e preparação de ambiente e infraestrutua, por exemplo, já tenham sido cumpridos, afinal, na situação hipotética, o processo de mudança já está em curso, eu seguiria os seguintes passos para garantir uma transição tranquila e eficiente:

### Iniciando o processo de migração de dados:

> Essa seria a primeira etapa, onde seriam realizados estudos de como a base de dados anterior era organizada para ter uma noção de como as rotinas de migração de dados serão realizadas de uma base pra outra, analisaria como a plataforma nova iria funcionar para criar essas rotinas, incluindo a limpeza e a transformação de dados, se necessário, e assim garantir melhor eficiência no procedimento.

### Configuração da plataforma:

> O próximo passo após migrar os dados, seria configurar a plataforma de acordo com o sistema de empresa, configurando o SSO para integrá-lo às aplicações existente, verificando se ele está funcionando corretamente e se é possível acessar todas as aplicações através dele.

### Implementação da Plataforma:

> Após realizar as configurações corretamente, realizaremos a implementação do sistema em si para assim iniciarmos os testes.

> Nessa etapa é interessante também a realização do gerenciamento do ciclo de vida de usuário, já que a etapa de provisionamento de usuário no ciclo de vida temos a entrada do usuário no sistema, realizando seu cadastro definindo suas atribuições e seu perfil para garantir a segurança da aplicação de forma assertiva.

> Sobre a questão da segurança, aqui também é realizado o gerenciamento de permissões, onde ocorrerá a manutenção dos níveis de acesso de usuário, definindo quais atividades e funções que poderão ser realizadas por usuários daquele grupo, adotando também políticas de auditoria e monitoramento para registros de atividades e assim garantir um melhor controle do que está sendo feito pelos usuários durante as etapas da transição.


### Testes e Validações:

> Depois da etapa de implementação da plataforma, depois que os dados já foram transferidos e o sistema configurado, são realizados testes funcionais e testes de segurança.

> Testes Funcionais: Testes realizados para testar as novas funcionalidades oriundas da migração de plataforma e verificar se estão funcionando de acordo com o desejado pela empresa.

> Testes de Segurança: Verificar se os logins, as permissões de usuário e se o SSO está funcionando corretamente para garantir que o sistema está seguro o suficiente e se as rotinas de segurança estão funcionando corretamente.

> Testes de Usuário: Por fim, realizamos testes como os usuários, para realizar testes de aceitação, feedback para assim realizar ajustes e correções do novo sistema.


### Treinamentos:

> Depois que a plataforma já está implementada, é interessante realizar treinamentos com todas as equipes da Dadosfera, dependendo das mudanças que forem realizadas com o upgrade da plataforma, caso contrário e não tivermos muitas funcionalidades novas, poderão ser realizados apenas tutoriais para preparar os usuários para essas possíveis novas funcionalidades. Depois, realizaria o mesmo procedimento com os clientes.

### Essas melhorias podem impactar no problema anterior?
> Resposta: Sim, dependendo de como for realizado o upgrade na plataforma, a forma de subir os dados na dadosfera poderiam ser afetadas, pois pode haver mudanças no tipo de dados e arquivos que serão aceitos na plataforma. Pode ser que a nova plataforma permita subir arquivos em excel diretamente como já é feito com CSV, por exemplo, e não tenhamos mais a necessidade de criar pipelines para isso.

### Como daria as interações na base de clientes após as mudanças?
> Resposta: Como um período de suporte mais próximo de acompanhamento ao cliente para a adaptação dessas novas mudanças e para auxiliá-los nos possíveis problemas ocorridos por conta das mudanças pois poderão ter de se adaptar a possíveis novas funcionalidades as quais serão integradas no sistema.


# Implementação de Chatbot com AI na Dadosfera

## Analise de necessidade:
> Realizaria um estudo para verificar quais são as maiores necessidades do cliente verificando os principais pontos para que o chatbot agregue valor e auxilie o cliente da melhor forma possível.


## Escolha da plataforma:
> Escolheria a plataforma de chatbot AI como o GPT-4, por exemplo, com recursos de NLP, machine learning e integração com multiplos canais (web, mobile, ect)

## Integração com a Dadosfera:
> Utilizariamos as APIs da Dadosfera para integrar o chatbot, dando a ele acesso a todos os dados necessários. Também implementaria medidas de segurança adequadas para proteger os dados dos clientes e garantir que o chatbot atenda aos requisitos de conformidade com a privacidade de dados.

## Testes:
> Nessa etapa realizaremos testes para avaliar o desempenho da IA no nosso sistema, identificar bugs e dar feedbacks para avaliação.
> Uma outra ideia é liberar uma versão de teste para um grupo seleto de usuários, para coletar feedbacks sobre o funcionamento do chatbot e procurar mudanças para melhorar a ferramenta.

# Fluxo do Processo de Atendimento

> Início da Interação: O cliente acessa o sistema de atendimento da Dadosfera via website ou aplicativo.

#### Recepção Inicial (IA Chatbot):

> Entrada do Cliente: O cliente faz uma pergunta ou relata um problema.

> Processamento: A IA analisa a consulta e verifica se é uma questão comum ou algo que pode ser resolvido com informações documentadas.

#### Resposta Automática (IA Chatbot):

> Documentação Relevante: A IA consulta a documentação interna (docs.dadosfera.ai) e fornece uma resposta baseada nas informações encontradas.

> Solicitação de Esclarecimento: Caso a consulta seja ambígua, a IA pede mais detalhes ao cliente.

#### Transferência para Suporte Humano:

> Casos Complexos: Se a IA não conseguir resolver a questão, a consulta é encaminhada para um agente humano especializado no suporte da Dadosfera.

> Notificação: O cliente é informado da transferência e do possível tempo de espera.

#### Interação com Suporte Humano:

> Resolução: O agente de suporte analisa o problema e fornece uma solução personalizada.

> Follow-up: A IA pode acompanhar a resolução para garantir que o cliente esteja satisfeito e não tenha dúvidas adicionais.

#### Feedback e Melhoria Contínua:

> Avaliação do Cliente: Após a resolução, o cliente é solicitado a fornecer feedback sobre a experiência.

> Aprimoramento da IA: O feedback é utilizado para treinar e melhorar a performance da IA, aumentando sua eficácia para futuras interações.

## FLuxograma
![URL-da-imagem](https://github.com/LucasMeirellesS/LUCAS_MEIRELLES_DDF_SUPORTE_2024_07/blob/main/fluxograma.png)

# Item Consultas SQL
## Contagem de churn
>SELECT
    CASE
        WHEN CHURN = 1 THEN 'Churn'
        WHEN CHURN = 0 THEN 'Não Churn'
        ELSE NULL
    END AS CHURN_STATUS_IOS,
    COUNT(CHURN) as CHURN_COUNT_IOS
FROM
    TB__MZ7DJ7__USER
WHERE
    IOS_USER = 1
GROUP BY
    CHURN;

![URL-da-imagem](https://github.com/LucasMeirellesS/LUCAS_MEIRELLES_DDF_SUPORTE_2024_07/blob/main/CONTAGEMDECHURN.png)


## Faturamento no Período diário;
>
SELECT
    CASE
        WHEN LENGTH(TRANS.DATE) = 21 THEN LEFT(TRANS.DATE, LENGTH(TRANS.DATE) - 9)
        WHEN LENGTH(TRANS.DATE) = 22 THEN LEFT(TRANS.DATE, LENGTH(TRANS.DATE) - 10)
     END AS DATE_TAX,
    SUM(TAX.TAX) TOTAL
FROM
    TB__UUM1KE__TAX TAX JOIN TB__DBYNA1__TRANSACTIONS TRANS ON TAX.TRANSACTION_ID = TRANS.TRANSACTION_ID
GROUP BY
    DATE_TAX
ORDER BY
    DATE_TAX;

![URL-da-imagem](https://github.com/LucasMeirellesS/LUCAS_MEIRELLES_DDF_SUPORTE_2024_07/blob/main/FATURAMENTO_DIARIO_PERIODO.png)


## Total de Interações;
>
SELECT
    HOUR,
    COUNT(HOUR) HOUR_ACTIVATE,
    SUM(LIKED) TOTAL_LIKES,
    SUM(USED_PREMIUM_FEATURE) USED_PREMIUM_FEATURE_TOTAL
FROM
    TB__WN3XB4__INTERACTION
GROUP BY
    HOUR
ORDER BY
    TO_TIMESTAMP(HOUR, 'HH12:MI AM');

![URL-da-imagem](https://github.com/LucasMeirellesS/LUCAS_MEIRELLES_DDF_SUPORTE_2024_07/blob/main/INTERACTION_GRAFIC.png)

## Media de Churn
> SELECT
    CASE
        WHEN CHURN = 1 THEN 'Churn'
        WHEN CHURN = 0 THEN 'Não Churn'
        ELSE NULL
    END AS CHURN_STATUS,
    AVG(AGE) AS AVG_AGE
FROM
    TB__MZ7DJ7__USER
GROUP BY
    CHURN;

![URL-da-imagem](https://github.com/LucasMeirellesS/LUCAS_MEIRELLES_DDF_SUPORTE_2024_07/blob/main/MediaCHURN.png)

## Quantidade de usuários de Android x IOS;
>SELECT
    USERTYPE,
    Count(*) QUANTITY
FROM(
    SELECT
        CASE
            WHEN ANDROID_USER = 1 THEN 'ANDROID'
            ELSE NULL
        END AS USERTYPE
    FROM
        TB__MZ7DJ7__USER
    WHERE
        ANDROID_USER = 1  
    UNION ALL
    SELECT
        CASE
            WHEN IOS_USER = 1 THEN 'iOS'
            ELSE NULL
        END AS USERTYPE
    FROM
        TB__MZ7DJ7__USER
    WHERE
        IOS_USER = 1
) AS ANDROI_IOS_SUBQUERY
GROUP BY
    USERTYPE;

![URL-da-imagem](https://github.com/LucasMeirellesS/LUCAS_MEIRELLES_DDF_SUPORTE_2024_07/blob/main/USERS_ANDROID.png)


## Faixa Etária com Maior média CREDIT_SCORE;
> SELECT
    AGE,
    AVG(COALESCE(CREDIT_SCORE, 0)) AS CREDIT_SCORE
FROM
    TB__MZ7DJ7__USER
GROUP BY
    AGE
ORDER BY
    CREDIT_SCORE DESC
LIMIT 10;

![URL-da-imagem](https://github.com/LucasMeirellesS/LUCAS_MEIRELLES_DDF_SUPORTE_2024_07/blob/main/MEDIA%20DE%20CREDIT%20SCORE.png)



