# Microsoft Fabric - Fabric Analyst in a Day - Laboratório 4

![](../media/Lab-01/main4.png)

# Sumário
- Introdução
- Fluxo de dados Gen2
    - Tarefa 1: Copiar consultas do SharePoint para o Fluxo de dados
    - Tarefa 2: Criar conexão do SharePoint
    - Tarefa 3: Configurar destino de dados para a consulta People
    - Tarefa 4: Publicar e renomear o Fluxo de Dados do SharePoint
    - Tarefa 5: Copiar consultas do Snowflake para o Fluxo de Dados
    - Tarefa 6: Criar conexão com o Snowflake
    - Tarefa 7: Configurar destino de dados para as consultas Supplier e PO
    - Tarefa 8: Renomear e publicar o fluxo de dados do Snowflake
- Atalho para Lakehouse Interno
    - Tarefa 9: Como criar um atalho para Dataverse
    - Task 10: Create a Shortcut to a Lakehouse
- Referências

# Introdução 

Em nosso cenário, os Dados do Fornecedor estão no Snowflake, os Dados do
Cliente no Dataverse e os Dados do Funcionário no SharePoint. Todas
essas fontes de dados são atualizadas em momentos diferentes. Para
minimizar o número de atualizações de dados para Fluxos de Dados,
criaremos fluxos de dados individuais para as fontes de dados Snowflake
e SharePoint.

>**Observação:** Várias fontes de dados são suportadas em um único Fluxo
de Dados.

A equipe de TI já estabeleceu um link para o Dataverse e aplicou as
transformações de dados necessárias, espelhando-as no arquivo do Power
BI Desktop. Eles ingeriram esses dados no Lakehouse do workspace Admin e
nos deram acesso às tabelas. Vamos criar um atalho para as tabelas que a
equipe de TI do Lakehouse criou.

Ao final deste laboratório, você terá aprendido:

- Como conectar ao SharePoint usando o Fluxo de dados Gen2 e ingerir
  dados no Lakehouse

- Como conectar ao Snowflake usando o Fluxo de dados Gen2 e ingerir
  dados no Lakehouse

- Como ingerir dados de um Lakehouse compartilhado

# Fluxo de dados Gen2

## Tarefa 1: Copiar consultas do SharePoint para o Fluxo de dados

1. Vamos voltar ao workspace do Fabric, **FAIAD_<inject key="Deployment ID" enableCopy="false"/> (1)**, que você criou no Laboratório 2, Tarefa 8.

2. Selecione a opção **+ Novo item (2)** disponível no canto superior esquerdo.

3. Na seção **Obter Dados (3),** selecione **Fluxo de Dados Gen2 (4)**.

    ![](../media/Lab-04/image6.png)

    Deixe o nome padrão e garanta que "Habilitar a integração do Git" esteja marcado. Em seguida, selecione **Criar**. Você navegará até a **página Fluxo de Dados**. A interface do Fluxo de dados Gen2 é igual a do Power Query no Power BI Desktop. Podemos copiar consultas do Power BI Desktop para o Fluxo de dados Gen2. Vamos testar.

4. Se você ainda não tiver aberto, abra o arquivo **FAIAD.pbix** que está na pasta **Reports** na área de trabalho do seu ambiente de laboratório.

5. Na faixa de opções, selecione **Página Inicial -> Transformar dados**. A janela do Power Query é aberta. Como você observou nos laboratórios anteriores, as consultas no painel esquerdo são organizadas por fonte de dados.

6. No painel esquerdo, na pasta SharepointData, **selecione a** consulta **People**.

7. **Clique com o botão direito do mouse** e selecione **Copiar**.

    ![P56#yIS1](../media/Lab-04/image7.png)

8. Volte para a tela **Fluxo de Dados** no navegador.

9. No **painel Fluxo de dados**, pressione **Ctrl+V** (no momento, não é possível clicar com o botão direito do mouse em Colar). Se você estiver usando o dispositivo MAC, use Cmd+V para colar.

    ![](../media/Lab-04/image8.png)

    >**Observação:** se você estiver trabalhando no ambiente de laboratório, selecione as reticências no canto superior direito da tela. Use o controle deslizante para **habilitar** **VM Native Clipboard**. Selecione OK na caixa de diálogo. Depois que terminar de colar as consultas, você poderá desabilitar essa opção.

    ![P60#yIS1](../media/Lab-04/image9.png)

    Observe se a consulta foi colada e se está disponível no painel esquerdo. Como não temos uma conexão criada para o SharePoint, você verá uma mensagem de aviso solicitando que configure a conexão.

    ![](../media/Lab-04/image10.png)

## Tarefa 2: Criar conexão do SharePoint

1. Selecione **Configurar conexão**.

    ![](../media/Lab-04/image11.png)

2. A caixa de diálogo Conectar-se à fonte de dados é aberta. Na lista suspensa **Conexão**, verifique se **Criar nova conexão** está selecionada.

3. O **Tipo de autenticação** deve ser **Conta organizacional**.

4. Selecione **Conectar**.

    >**Observação:** você vai se conectar usando suas credenciais. Elas serão diferentes da captura de tela abaixo.

    ![P69#yIS1](../media/Lab-04/image12.png)

## Tarefa 3: Configurar destino de dados para a consulta People

A conexão é estabelecida, e você pode exibir os dados no painel de visualização. Fique à vontade para navegar pelas Etapas aplicadas das consultas. Agora precisamos ingerir os dados de People no Lakehouse.

1. Selecione a consulta **People (1)**.

2. Na faixa de opções, selecione **Página Inicial -> Consulta (2) -> Adicionar destino de dados (3) ->** **Lakehouse (4)**.

    ![](../media/Lab-04/image13.png)

3. A caixa de diálogo Conectar ao destino de dados é aberta. Precisamos criar uma nova Conexão com o Lakehouse. Com a opção **Criar nova conexão** selecionada na lista suspensa Conexão e **Tipo de autenticação** definido como **Conta organizacional**, selecione **Próximo**.

    ![](../media/Lab-04/image14.png)

4. A caixa de diálogo Escolher alvo de destino é aberta. Verifique se o botão de opção **Nova tabela** está selecionado, pois estamos criando uma nova tabela.

5. Queremos criar a tabela no Lakehouse que criamos anteriormente. No painel esquerdo, navegue para **Lakehouse -> FAIAD_<inject key="Deployment ID" enableCopy="false"/>**

6. Selecione **lh_FAIAD**.

7. Deixe o nome da tabela como **People**.

8. Selecione **Próximo**.

    ![](../media/Lab-04/image15.png)

9. A caixa de diálogo Escolher configurações de destino é aberta. **Habilite** "**Usar configurações automáticas**".

    >**Observação:** você pode desativar as configurações automáticas e notar que tem opções para definir o método Update e as opções de esquema. Depois de explorar, **habilite** "**Usar configurações automáticas**".

10. Selecione **Salvar configurações**.

    ![](../media/Lab-04/image16.png)

## Tarefa 4: Publicar e renomear o Fluxo de Dados do SharePoint

1. Você será direcionado de volta à **janela Power Query**. No **canto inferior direito**, Destino de dados está definido como **Lakehouse (2)**.

2. No canto superior esquerdo, selecione **Salvar e Executar (1)**. Depois de ver a notificação de que uma atualização foi iniciada, você poderá fechar o fluxo de dados **(3)**

    ![](../media/Lab-04/image17.png)

    > **Observação:** você será direcionado de volta para o **workspace FAIAD_<inject key="Deployment ID" enableCopy="false"/>**. Pode levar alguns instantes para que a execução do Fluxo de Dados seja encerrada.

3. **Dataflow 1** é o fluxo de dados no qual estávamos trabalhando. Vamos renomeá-lo antes de continuarmos. Clique nas **reticências (...)** ao lado de Dataflow 1. Selecione **Configurações** (enquanto o Dataflow está em execução, não é possível acessar as configurações).

    ![](../media/Lab-04/image18.png)

4. A janela Configurações do fluxo de dados é aberta. Altere o **nome** para **df_People_SharePoint (1)**.

5. Na caixa de texto **Descrição**, adicione **Dataflow to ingest People data from SharePoint to Lakehouse (2)**.

6. Quando terminar, feche a janela de configurações **(3)**.

    ![](../media/Lab-04/image19.png)

    Você será direcionado de volta para o **workspace FAIAD_<inject key="Deployment ID" enableCopy="false"/>**.

7. Selecione **lh_FAIAD** para acessar o lakehouse.

8. Verifique se você está na exibição Lakehouse (não no ponto de extremidade da análise SQL).

9. Veja que a tabela **People** está disponível no Lakehouse.

    ![](../media/Lab-04/image20.png)

> **Observação:** se você não vir as tabelas recém-criadas, selecione as reticências ao lado de Tabelas e selecione Atualizar para atualizar as tabelas.

## Tarefa 5: Copiar consultas do Snowflake para o Fluxo de Dados

1. Vamos voltar ao workspace do Fabric, **FAIAD_<inject key="Deployment ID" enableCopy="false"/> (1)**.

2. Selecione a opção **+ Novo item (2)** disponível no canto superior esquerdo.

3. Em Itens recomendados, selecione **Fluxo de dados Gen2 (3)**.

    ![](../media/Lab-04/image21.png)

    Deixe o nome padrão e garanta que "Habilitar a integração do Git" esteja marcado. Em seguida, selecione **criar**. Se você receber uma mensagem informando "Já existe um fluxo de dados com este nome", em seguida, altere o nome para **Fluxo de Dados 2**. Você navegará até a **página Fluxo de Dados**. Agora que estamos familiarizados com o Fluxo de Dados, vamos continuar e copiar as consultas do Power BI Desktop no Fluxo de Dados.

4. Se você ainda não tiver aberto, abra o arquivo **FAIAD.pbix** que está na pasta **Reports** na área de trabalho do seu ambiente de laboratório.

5. Na faixa de opções, selecione **Página Inicial -> Transformar dados**. A janela do Power Query é aberta. Como você observou no laboratório anterior, as consultas no painel esquerdo são organizadas por fonte de dados.

6. No painel esquerdo, na pasta **SnowflakeData**, pressione
    **Ctrl+Select** ou Shift+Select para selecionar as seguintes consultas:

    a. SupplierCategories

    b. Suppliers

    c. Supplier

    d. PO

    e. POLineItems

7. **Clique com o botão direito do mouse** e selecione **Copiar**.

    ![](../media/Lab-04/image22.png)

8. Volte para o **navegador**.

9. No **painel Dataflow**, selecione o **painel central** e pressione **Ctrl+V** (no momento, não é possível clicar com o botão direito do mouse em Colar). Se você estiver usando o dispositivo MAC, use Cmd+V para colar.

    > **Observação:** se você estiver trabalhando no ambiente de
    > laboratório, selecione as **reticências(...)** no canto superior
    > direito da tela. Use o controle deslizante para **habilitar** **VM
    > Native Clipboard**. Selecione OK na caixa de diálogo. Depois que
    > terminar de colar as consultas, você poderá desabilitar essa opção.

    ![P123#yIS1](../media/Lab-04/image23.png)

## Tarefa 6: Criar conexão com o Snowflake

Observe que as cinco consultas foram coladas e agora você tem o painel Consultas à esquerda. Como não temos uma conexão criada para o Snowflake, você verá uma mensagem de aviso solicitando que configure a conexão.

1. Selecione **Configurar conexão**.

    ![](../media/Lab-04/image24.png)

2. A caixa de diálogo Conectar-se à fonte de dados é aberta. Na lista suspensa **Conexão**, verifique se **Criar nova conexão** está selecionada.

3. O **Tipo de autenticação** deve ser **Snowflake**.

4. Insira o **Nome de usuário do Snowflake** e a **Senha do Snowflake** fornecidos abaixo. Use essas credenciais para conectar todas as tabelas do **Snowflake** ao Snowflake e selecione **Conectar**.

    - **Nome de usuário do Snowflake:** <inject key="SnowFlake Username" enableCopy="false" />

    - **Senha do Snowflake:** <inject key="SnowFlake Password" enableCopy="false" />

    >**Observação:** Se você encontrar problemas para se conectar ao Snowflake usando as credenciais dos detalhes do ambiente, use as credenciais fornecidas abaixo.

    - **Nome de usuário do Snowflake:** SNOWFLAKE_BACKUP

    - **Senha do Snowflake:** 8UpfRpExVDXv2AC1

5. Selecione **Conectar**.

    ![](../media/Lab-04/image25.png)

    A conexão é estabelecida e você pode exibir os dados no painel de visualização. Fique à vontade para navegar pelas Etapas aplicadas das consultas. Basicamente, a consulta Suppliers tem os detalhes dos fornecedores e a tabela SupplierCategories, como o nome indica, tem todas as categorias de fornecedores. Essas duas tabelas são unidas para criar a dimensão Supplier, com as colunas necessárias. Da mesma forma, temos a consulta PO Line Items mesclada com PO para criar o fato PO. Agora precisamos ingerir os dados de Supplier e PO no Lakehouse.

## Tarefa 7: Configurar destino de dados para as consultas Supplier e PO

1. Selecione a consulta **Supplier (1)**.

2. Na faixa de opções, selecione **Página Inicial (2) -> Adicionar destino de dados (3) -> Lakehouse (4)**.

    ![](../media/Lab-04/image26.png)

3. A caixa de diálogo Conectar ao destino de dados é aberta. Na **lista suspensa Conexão**, selecione **Lakehouse odl_user_<inject key="Deployment ID" enableCopy="false"/> (nenhum)**.

4. Selecione **Próximo**.

    ![](../media/Lab-04/image27.png)

5. A caixa de diálogo Escolher alvo de destino é aberta. Verifique se o botão de opção **Nova tabela** está selecionado, pois estamos criando uma nova tabela.

6. Queremos criar a tabela no Lakehouse que criamos anteriormente. No painel esquerdo, navegue para **Lakehouse -> FAIAD_<inject key="Deployment ID" enableCopy="false"/>**

7. Selecione **lh_FAIAD**.

8. Deixe o nome da tabela como **Supplier**.

9. Selecione **Próximo**.

    ![](../media/Lab-04/image28.png)

10. A caixa de diálogo Escolher configurações de destino é aberta. Usaremos as configurações automáticas, pois assim será feita uma atualização completa dos dados. Além disso, as colunas serão renomeadas conforme necessário. Selecione **Salvar configurações**.

    ![](../media/Lab-04/image29.png)

11. Você será direcionado de volta à **janela Power Query**. No **canto inferior direito, Destino de dados** está definido como **Lakehouse**. Da mesma forma, **configure o Destino de dados para a consulta PO**. Uma vez feito isso, sua consulta **PO** deverá ter **Destino de dados** definido como **Lakehouse** conforme mostrado na captura de tela abaixo.

    ![](../media/Lab-04/image30.png)

## Tarefa 8: Renomear e publicar o fluxo de dados do Snowflake

1. Na parte superior da tela, selecione a **seta ao lado do Dataflow 2 (o nome pode ser diferente)** para renomear.

2. Na caixa de diálogo, altere o nome para **df_Supplier_Snowflake**.

3. Clique em **Enter** para salvar a alteração do nome.

    ![](../media/Lab-04/image31.png)

4. No canto superior esquerdo, selecione **Salvar e Executar (1)**. Depois de ver a notificação de que uma atualização foi iniciada, você poderá fechar o fluxo de dados **(2)**

    ![](../media/Lab-04/image32.png)

    Você será direcionado de volta para o **workspace FAIAD_<inject key="Deployment ID" enableCopy="false"/>**. Pode levar alguns instantes para que Fluxo de Dados seja publicado.

5. Selecione **lh_FAIAD** para acessar o lakehouse.

6. Verifique se você está na exibição Lakehouse (não no ponto de extremidade da análise SQL).

7. Veja que as tabelas **PO** e **Supplier** agora estão disponíveis no Lakehouse.

    ![](../media/Lab-04/image33.png)

    >**Observação:** se você não vir as tabelas recém-criadas, selecione as reticências ao lado de Tabelas e selecione Atualizar para atualizar as tabelas.

    Agora vamos criar um atalho para mostrar dados do Dataverse.

# Atalho para Lakehouse Interno

## Tarefa 9: Como criar um atalho para Dataverse

Você deve estar no Lakehouse **lh_FAIAD**. Verifique se você está na exibição Lakehouse (não no ponto de extremidade da análise SQL).

![](../media/Lab-04/image34.png)

1. No painel **Explorer**, selecione as **reticências** ao lado de **Tabelas**.

2. Selecione **Novo atalho**.

    ![](../media/Lab-04/image35.png)

3. A caixa de diálogo Novo atalho é aberta. Em **Fontes externas**, selecione **Dataverse**.

    > **Observação:** no laboratório anterior, seguimos etapas semelhantes para criar um atalho para Azure Data Lake Storage Gen2.

    ![](../media/Lab-04/image36.png)

4. **Selecione Nova conexão (1).** O diálogo Configurações de conexão é aberto. Insira **org6c18814a.crm.dynamics.com (2)** como **Domínio de ambiente.**

5. Deixe **Tipo de autenticação** como **Conta organizacional (3)**.

6. Selecione **Entrar** se você ainda não estiver conectado.

    ![](../media/Lab-04/image37.png)

7. Na caixa de diálogo Entrar, select a **conta de usuário** que você tem usado para esses laboratórios. A caixa de diálogo Entrar na sua conta é aberta. Escolha sua conta para entrar. **Observação:** sua conta será diferente da captura de tela abaixo.

    ![P184#yIS1](../media/Lab-04/image38.png)

8. Selecione **Próximo** na caixa de diálogo Configurações de conexão. Você será direcionado para um diálogo para escolher o bucket/diretório diferente do Dataverse. Observe que há muitas opções de buckets disponíveis. Podemos escolher os buckets que precisamos e seguir o processo como o Laboratório 3 (usar consulta visual para transformar dados e criar exibições). Também podemos usar o Fluxo de dados Gen2 como usamos anteriormente neste laboratório para nos conectarmos ao
SharePoint. Em nosso cenário, a equipe de TI já estabeleceu um link para o Dataverse e aplicou as transformações de dados necessárias, espelhando-as no arquivo do Power BI Desktop. Eles ingeriram esses dados no Lakehouse do workspace Admin e nos deram acesso às tabelas. Como nossa equipe de TI fez todo o trabalho árduo, podemos criar um atalho para esse Lakehouse
no workspace Admin.

9. Selecione **Cancelar** na caixa de diálogo Novo atalho para voltar ao Lakehouse.

    ![](../media/Lab-04/image39.png)

### Task 10: Create a Shortcut to a Lakehouse

1. No painel **Explorer**, selecione as **reticências** ao lado de **Tabelas**.

2. Selecione **Novo atalho**.

    ![](../media/Lab-04/image35.png)

3. A caixa de diálogo Novo atalho é aberta. Selecione a opção
    **Microsoft OneLake** em Fontes internas.

    ![](../media/Lab-04/image40.png)

4. Selecione **lh_dataverse**.

5. Selecione **Avançar**.

    ![](../media/Lab-04/image41.png)

6. No painel esquerdo, expanda **lh_dataverse -> Tables**. Observe que o administrador de TI forneceu acesso à tabela Customer.

7. Selecione **Customer**.

8. Selecione **Avançar**.

    ![](../media/Lab-04/image42.png)

9. Na próxima caixa de diálogo, selecione **Criar**. Você será
    direcionado de volta ao lakehouse lh_FAIAD.

    ![](../media/Lab-04/image43.png)

10. No painel **Explorer** à esquerda, observe que a nova tabela **Customer** foi criada.

11. Selecione a tabela **Customer** para exibir os dados no painel de visualização.

    ![](../media/Lab-04/image44.png)

    Criamos com sucesso um atalho para outro lakehouse.

    Agora ingerimos todos os dados necessários em nosso Lakehouse. No próximo laboratório, agendaremos uma atualização para o nosso Fluxo de Dados do SharePoint.

# Referências

O Fabric Analyst in a Day (FAIAD) apresenta algumas das principais
funções disponíveis no Microsoft Fabric. No menu do serviço, a seção
Ajuda (?) tem links para ótimos recursos.

![](../media/Lab-01/image28.png)

Veja aqui mais alguns recursos que ajudarão você com as próximas etapas
do Microsoft Fabric.

- Veja a postagem do blog para ler o [anúncio completo da GA do
  Microsoft Fabric](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Explore o Fabric por meio do [Tour
  Guiado](https://aka.ms/Fabric-GuidedTour)

- Inscreva-se para a [avaliação gratuita do Microsoft
  Fabric](https://aka.ms/try-fabric)

- Visite o [site do Microsoft Fabric](https://aka.ms/microsoft-fabric)

- Aprenda novas habilidades explorando os [módulos de Aprendizagem do
  Fabric](https://aka.ms/learn-fabric)

- Explore a [documentação técnica do Fabric](https://aka.ms/fabric-docs)

- Leia o [livro eletrônico gratuito sobre como começar a usar o
  Fabric](https://aka.ms/fabric-get-started-ebook)

- Participe da [comunidade do Fabric](https://aka.ms/fabric-community)
  para postar suas perguntas, compartilhar seus comentários e aprender
  com outras pessoas

Leia os blogs de comunicados de experiências do Fabric em mais detalhes:

- [Experiência do Data Factory no blog do
  Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Experiência do Synapse Data Engineering no blog do
  Fabric](https://aka.ms/Fabric-DE-Blog)

- [Experiência do Synapse Data Science no blog do
  Fabric](https://aka.ms/Fabric-DS-Blog)

- [Experiência do Synapse Data Warehousing no blog do
  Fabric](https://aka.ms/Fabric-DW-Blog)

- [Experiência do Synapse Real-Time Analytics no blog do
  Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Blog de comunicado do Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Experiência do Data Activator no blog do
  Fabric](https://aka.ms/Fabric-DA-Blog)

- [Administração e governança no blog do
  Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [OneLake no blog do Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog de integração do Dataverse e Microsoft
  Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Todos os direitos reservados.

Ao usar esta demonstração/este laboratório, você concorda com os
seguintes termos:

A tecnologia/funcionalidade descrita nesta demonstração/neste
laboratório é fornecida pela Microsoft Corporation para obter seus
comentários e oferecer uma experiência de aprendizado. Você pode usar
a demonstração/o laboratório somente para avaliar tais funcionalidades
e recursos de tecnologia e fornecer comentários à Microsoft. Você não
pode usá-los para nenhuma outra finalidade. Você não pode modificar,
copiar, distribuir, transmitir, exibir, executar, reproduzir,
publicar, licenciar, criar obras derivadas, transferir nem vender esta
demonstração/este laboratório ou qualquer parte deles.

A CÓPIA OU A REPRODUÇÃO DA DEMONSTRAÇÃO/DO LABORATÓRIO (OU DE QUALQUER
PARTE DELES) EM QUALQUER OUTRO SERVIDOR OU LOCAL PARA REPRODUÇÃO OU
REDISTRIBUIÇÃO ADICIONAL É EXPRESSAMENTE PROIBIDA.

ESTA DEMONSTRAÇÃO/ESTE LABORATÓRIO FORNECE DETERMINADOS RECURSOS
E FUNCIONALIDADES DE PRODUTO/TECNOLOGIA DE SOFTWARE, INCLUINDO NOVOS
RECURSOS E CONCEITOS POTENCIAIS, EM UM AMBIENTE SIMULADO SEM
CONFIGURAÇÃO NEM INSTALAÇÃO COMPLEXA PARA A FINALIDADE DESCRITA ACIMA.
A TECNOLOGIA/OS CONCEITOS REPRESENTADOS NESTA DEMONSTRAÇÃO/NESTE
LABORATÓRIO PODEM NÃO REPRESENTAR A FUNCIONALIDADE COMPLETA DOS
RECURSOS E PODEM NÃO FUNCIONAR DA MESMA MANEIRA QUE UMA VERSÃO FINAL.
ALÉM DISSO, PODEMOS NÃO LANÇAR UMA VERSÃO FINAL DE TAIS RECURSOS OU
CONCEITOS. SUA EXPERIÊNCIA COM O USO DE TAIS RECURSOS E
FUNCIONALIDADES EM UM AMBIENTE FÍSICO TAMBÉM PODE SER DIFERENTE.

**COMENTÁRIOS**. Caso você forneça comentários sobre os recursos de
tecnologia, as funcionalidades e/ou os conceitos descritos nesta
demonstração/neste laboratório à Microsoft, você concederá
à Microsoft, sem encargos, o direito de usar, compartilhar e
comercializar seus comentários de qualquer forma e para qualquer
finalidade. Você também concede a terceiros, sem encargos, quaisquer
direitos de patente necessários para que seus produtos, suas
tecnologias e seus serviços usem ou interajam com partes específicas
de um software ou um serviço da Microsoft que inclua os comentários.
Você não fornecerá comentários que estejam sujeitos a uma licença que
exija que a Microsoft licencie seu software ou sua documentação para
terceiros em virtude da inclusão de seus comentários neles.
Esses direitos continuarão em vigor após o término do contrato.

POR MEIO DESTE, A MICROSOFT CORPORATION SE ISENTA DE TODAS AS
GARANTIAS E CONDIÇÕES REFERENTES À DEMONSTRAÇÃO/AO LABORATÓRIO,
INCLUINDO TODAS AS GARANTIAS E CONDIÇÕES DE COMERCIALIZAÇÃO, SEJAM
ELAS EXPRESSAS, IMPLÍCITAS OU ESTATUTÁRIAS,
E DE ADEQUAÇÃO A UMA FINALIDADE ESPECÍFICA, TÍTULO E NÃO VIOLAÇÃO. A
MICROSOFT NÃO DECLARA NEM GARANTE A PRECISÃO DOS RESULTADOS DERIVADOS
DO USO DA DEMONSTRAÇÃO/DO LABORATÓRIO NEM A ADEQUAÇÃO DAS INFORMAÇÕES
CONTIDAS NA DEMONSTRAÇÃO/NO LABORATÓRIO A QUALQUER FINALIDADE.

**AVISO DE ISENÇÃO DE RESPONSABILIDADE**

Esta demonstração/este laboratório contém apenas uma parte dos novos
recursos e aprimoramentos do Microsoft Power BI. Alguns dos recursos
podem ser alterados em versões futuras do produto. Nesta
demonstração/neste laboratório, você aprenderá sobre alguns dos novos
recursos, mas não todos.