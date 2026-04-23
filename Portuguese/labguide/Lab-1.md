# Microsoft Fabric - Fabric Analyst in a Day - Laboratório 1

![](../media/Lab-1/lab1-04-pt.png)

# Sumário

- Estrutura do documento

- Cenário/Declaração do problema

- Visão geral do relatório do Power BI Desktop

    - Tarefa 1: Configurar o Power BI Desktop no ambiente de laboratório

    - Tarefa 2: Analisar relatório do Power BI Desktop

    - Tarefa 3: Revisar Power Queries

- Referências

# Estrutura do documento

O laboratório inclui etapas a serem seguidas pelo usuário juntamente com as capturas de tela associadas que fornecem auxílio visual. Em cada captura de tela, as seções estão destacadas com caixas laranjas para indicar as áreas nas quais o usuário deve se concentrar.

> **Observação:** Algumas capturas de tela podem estar desatualizadas devido às atualizações contínuas do produto.

# Cenário/Declaração do problema

A Fabrikam, Inc. é distribuidora atacadista de produtos inovadores. Como atacadista, os clientes da Fabrikam são principalmente empresas que revendem para pessoas físicas. A Fabrikam vende para clientes de varejo nos Estados Unidos, incluindo lojas especializadas, supermercados, lojas de informática e lojas de atrações turísticas. A Fabrikam também vende para outros atacadistas por meio de uma rede de agentes que promovem os produtos em nome da Fabrikam. Embora todos os clientes da Fabrikam estejam atualmente nos Estados Unidos, a empresa pretende impulsionar a expansão para outros países/regiões.

Você é um Analista de Dados na equipe de Vendas. Você coleta, limpa e interpreta conjuntos de dados para resolver problemas de negócios. Você também reúne visualizações, como tabelas e gráficos, escreve relatórios e os apresenta aos tomadores de decisão na organização.

Para obter insights valiosos dos dados, você extrai dados de vários sistemas, limpa-os e combina-os. Você extrai dados das seguintes fontes:

- **Dados de Vendas:** são obtidos do sistema ERP e armazenados em um banco de dados ADLS Gen2. Eles são atualizados ao meio-dia/12h, todos os dias.

- **Dados do Fornecedor:** são obtidos de diferentes fornecedores e armazenados em um banco de dados Snowflake. São atualizados à meia-noite/24h, todos os dias.

- **Dados do Cliente:** são obtidos do Customer Insights e armazenados no Dataverse. Os dados estão sempre atualizados.

- **Dados do Funcionário:** são obtidos do sistema de RH e armazenados como um arquivo de exportação em uma pasta do SharePoint. São atualizados todas as manhãs, às 9h.

  ![](../media/Lab-1/image6.jpeg)

No momento, você está criando um modelo semântico no Power BI Premium que extrai os dados dos sistemas de origem acima para que você possa gerar relatórios e fornecer aos usuários finais o recurso de autoatendimento. Você usa o Power Query para atualizar seu modelo.

**Você está enfrentando os seguintes desafios:**

- Você precisa atualizar seu conjunto de dados pelo menos três vezes por dia para acomodar os diferentes horários de atualização para as diferentes fontes de dados.

- As atualizações podem demorar, pois é sempre necessário fazer uma atualização completa para capturar tudo o que foi atualizado nos sistemas de origem.

- Os erros detectados em qualquer uma das fontes das quais você está extraindo dados resultarão na interrupção da atualização do conjunto de dados. Muitas vezes o arquivo do funcionário não é carregado no prazo, resultando na interrupção da atualização do conjunto de dados.

- As alterações no modelo de dados demoram muito tempo, pois o Power Query leva tempo para atualizar as versões preliminares devido aos tamanhos de dados grandes e às transformações complexas.

- Você precisa de um computador com Windows para usar o Power BI Desktop mesmo que o padrão corporativo seja Mac.

Você ouviu falar do Microsoft Fabric e decidiu tentar ver se ele resolverá seus desafios.

### **Visão geral do relatório do Power BI Desktop**

Antes de começarmos com o Fabric, vamos dar uma olhada no Relatório atual no Power BI Desktop para entender as transformações e o modelo.

## Tarefa 1: Configurar o Power BI Desktop no ambiente de laboratório

1. Abra o arquivo **FAIAD.pbix** que está na pasta **Reports** na **área de trabalho** do seu ambiente de laboratório. O arquivo será aberto no Power BI Desktop.

    ![](../media/Lab-1/image7.png)

    > ### **Observação:** Se o Power BI Desktop parar de responder na tela **“Digite seu endereço de e-mail”** e você não conseguir digitar, mova o cursor sobre o ícone do Power BI na barra de tarefas **(1)**. Em seguida, feche a janela em branco extra clicando no **X** **(2)**. Isso fará com que a janela principal do Power BI volte a responder.

    ![](../media/Lab-1/lab1-04-pt2.png)

2. Quando o diálogo "Insira seu endereço de email" for exibido, copie o **Nome de usuário**
    e cole-o no campo **Email** do diálogo e selecione **Continuar**.

    - Email/Nome de usuário: <inject key="AzureAdUserEmail"></inject>

      ![](../media/Lab-1/image8.png)

3. Na guia Entrar no Microsoft Azure, você verá a tela de logon. Nessa tela, insira o seguinte Email/Nome de usuário e clique em **Avançar**.

    - Email/Nome de usuário: <inject key="AzureAdUserEmail"></inject>

      ![](../media/Lab-1/image9.png)

4. Agora, insira a seguinte **Senha de Acesso Temporária** e clique em **Entrar**.

    - Senha de Acesso Temporária: <inject key="AzureAdUserPassword"></inject>

      ![](../media/Lab-1/image10.png)

5. A caixa de diálogo **Continuar conectado a todos os aplicativos** é aberta. Selecione **OK**.

    ![](../media/Lab-1/image11.png)

6. **Tudo pronto!** A caixa de diálogo é aberta. Selecione **Concluído**.

    O Power BI Desktop será aberto.

## Tarefa 2: Analisar relatório do Power BI Desktop

O relatório abaixo analisa as Sales da Fabrikam. Os KPIs estão listados no canto superior esquerdo da página. Os visuais restantes destacam as Sales over time, por Territory, Product Group e Reseller Company.

![](../media/Lab-1/image12.jpeg)

> **Observação:** Neste treinamento, estamos nos concentrando na aquisição, transformação e modelagem de dados usando as ferramentas disponíveis no Fabric. Não nos concentraremos no desenvolvimento ou na navegação de relatórios. Vamos reservar alguns minutos para entender o relatório e passar para as próximas etapas.

1. Vamos analisar os dados por Sales Territory. Selecione o visual **New England from the Sales Territory** (gráfico de dispersão). Observe que em Sales over time, Reseller Tailspin Toys tem mais vendas em comparação com Wingtip Toys em New England. Se você olhar o gráfico de colunas Sales YoY%, notará que o crescimento das vendas da Wingtip Toys foi baixo e diminuiu trimestre após trimestre durante o ano passado. Depois de uma pequena recuperação no terceiro trimestre, caiu novamente no quarto.

    ![](../media/Lab-1/image13.jpeg)

2. Vamos comparar isso com a região Rocky Mountain. Selecione o visual **Rocky Mountain from Sales Territory** (gráfico de dispersão). Observe no gráfico de colunas Sales YoY% que as vendas da Wingtip Toys aumentaram drasticamente no quarto trimestre de 2023, depois de terem sido baixas nos dois trimestres anteriores.

    ![](../media/Lab-1/image14.jpeg)

3. Selecione o visual **Rocky Mountain from Sales Territory** para remover o filtro.

4. No visual Gráfico de dispersão, na parte inferior central da tela (Sales Orders por Sales), selecione a exceção no canto superior direito (4º quadrante). Observe que a margem percentual é de 52%, estando acima da média de 50%. Além disso, o Sales YoY% aumentou nos últimos dois trimestres de 2023.

    ![](../media/Lab-1/image15.jpeg)

5. Selecione a exceção Reseller no visual Gráfico de dispersão para **remover o filtro**.

6. Vamos obter os detalhes de Product por Product Group e Reseller. No visual do gráfico de barras Sales por Product Group e Reseller Company, **clique com o botão direito na barra Packaging Materials para Tailspin Toys** e, na caixa de diálogo, selecione **Drill through -> Product Detail**.

    ![](../media/Lab-1/image16.png)

7. Você será direcionado para a página que fornece os Product Details. Observe que também existem algumas ordens futuras em andamento.

8. Quando terminar de revisar esta página, selecione **Ctrl+seta para voltar** na parte superior esquerda da página para voltar ao Sales Report.

    ![](../media/Lab-1/image17.png)

9. Fique à vontade para analisar o relatório posteriormente. Quando estiver pronto, vamos dar uma olhada na exibição do modelo. No painel esquerdo, selecione o **Ícone de exibição do modelo**.

    ![](../media/Lab-1/image18.png)

10. Observe que existem duas tabelas de fatos, Sales e PO.

    a. A granularidade dos dados de Sales é por Date, Reseller, Product e People. Date, Reseller, Product e People conectam-se a Sales.

    b. A granularidade dos dados de PO é por Date, Product e People. Date, Product e People conectam-se a PO.

    c. Temos dados de Supplier por Product. Supplier conecta-se a Product.

    d. Temos os dados de localização de Reseller por Geo. Geo conecta-se a Reseller.

    e. Temos informações de Customer por Reseller. Customer conecta-se a Reseller.

## Tarefa 3: Revisar Power Queries

1. Vamos analisar o Power Query para entender as fontes de dados. Na faixa de opções, selecione **Página Inicial -> Transformar dados**.

    ![](../media/Lab-1/image19.png)

2. A janela do Power Query é aberta. Na faixa de opções, selecione **Página Inicial -> Configurações da fonte de dados**. A caixa de diálogo Configurações da fonte de dados é aberta. Ao percorrer a lista, você notará que existem quatro fontes de dados, conforme mencionado na declaração do problema:

    - Snowflake

    - SharePoint

    - ADLS Gen2

    - Dataverse

3. Selecione **Fechar** para fechar a caixa de diálogo Configurações da fonte de dados.

    ![](../media/Lab-1/image20.png)

4. No painel esquerdo Consultas, observe que as consultas estão agrupadas por fonte de dados.

5. Observe que a pasta **DataverseData** tem os dados de Customer disponíveis em quatro consultas diferentes: BabyBoomer, GenX, GenY e GenZ. Essas quatro consultas são acrescentadas para criar a consulta Customer.

6. Clique na Consulta Customer na janela Consultas. Para selecionar essa consulta, você deverá inserir novamente as credenciais do Dataverse. Clique em **Editar Credenciais**.

    ![](../media/Lab-1/image21.png)

7. Clique em **Entrar** para fazer login na sua conta.

    ![](../media/Lab-1/image22.png)

8. Você pode inserir as credenciais para a fonte de dados do Dataverse inserindo o **Nome de usuário e a Senha**. As credenciais são fornecidas abaixo. Quando concluído, selecione **Conectar**.

    - Email/Nome de usuário: <inject key="AzureAdUserEmail"></inject>

    - Senha: <inject key="AzureAdUserPassword"></inject>

9. Clique na Consulta **ADLS Base Folder** na janela Consultas. Para selecionar essa consulta, forneça as credenciais. Clique em **Editar Credenciais**.

    ![](../media/Lab-1/image23.png)

10. Para a fonte de dados ADLS, escolha a opção **SAS (Assinatura de acesso compartilhado)** e insira o **token SAS** fornecido abaixo. Em seguida, selecione **Conectar**.

    - **Token SAS:** <inject key="Sas token"></inject>

      ![](../media/Lab-1/image24.png)

11. Observe que a pasta **ADLSData** tem múltiplas dimensões: Geo, Product, Reseller e Date.
    Também tem o fato Sales.

    - **Dimensão Geo** é criada mesclando dados da consulta Cities, Countries e States.

    - **Dimensão Product** é criada mesclando dados da consulta Product Groups e Product Item Group.

    - **Dimensão Reseller** é filtrada usando a consulta BuyingGroup.

    - **Fato Sales** é criado mesclando InvoiceLineItems com a consulta Invoice.

12. Para a fonte de dados Snowflake, selecione a consulta **SupplierCategories** na janela Consultas.
    
    A seleção dessa consulta solicitará que você forneça as credenciais. Clique em **Editar Credenciais**.

    ![](../media/Lab-1/image25.png)

13. Insira o **Nome de usuário do Snowflake** e a **Senha do Snowflake** fornecidos abaixo. Use essas credenciais para conectar todas as tabelas do Snowflake ao Snowflake e selecione **Conectar**.

    - **Nome de usuário do Snowflake:** <inject key="SnowFlake Username" enableCopy="false" />

    - **Senha do Snowflake:** <inject key="SnowFlake Password" enableCopy="false" />

        > **Observação:** se você tiver problemas para se conectar ao Snowflake com as credenciais acima, use as credenciais de backup fornecidas abaixo.

    - **Nome de usuário do Snowflake:** SNOWFLAKE_BACKUP

    - **Senha do Snowflake:** 8UpfRpExVDXv2AC1

14. A pasta SnowflakeData tem a dimensão Supplier e o fato PO (Order/Spend).

    - A **dimensão Supplier** é criada mesclando a consulta Suppliers com a consulta SupplierCategories.

    - O **fato PO** é criado mesclando PO com a consulta PO Line Items.

15. Para a fonte de dados SharePoint, selecione a consulta **People** na janela Consultas. A seleção dessa consulta solicitará que você forneça as credenciais. Clique em **Editar Credenciais**.

    ![](../media/Lab-1/image26.png)

16. Selecione a opção **Conta da Microsoft** e clique em **Entrar**. Insira o Nome de usuário e a Senha fornecidos abaixo e selecione **Conectar**.

    - **Email/Nome de usuário:** <inject key="AzureAdUserEmail"></inject>

    - **Senha:** <inject key="AzureAdUserPassword"></inject>

       ![](../media/Lab-1/image27.png)

17. Observe que a pasta **SharepointData** tem a dimensão People.

    ![](../media/Lab-1/image28.png)

    Agora sabemos com o que estamos lidando. Nos laboratórios a seguir, criaremos um Power Query semelhante usando o Fluxo de Dados Gen2 e uma modelagem usando um Lakehouse.

# Referências

O Fabric Analyst in a Day (FAIAD) apresenta algumas das principais funções disponíveis no Microsoft Fabric. No menu do serviço, a seção Ajuda (?) tem links para ótimos recursos.

![](../media/Lab-1/image29.png)

Veja aqui mais alguns recursos que ajudarão você com as próximas etapas do Microsoft Fabric.

- Veja a postagem do blog para ler o [anúncio completo da GA do Microsoft Fabric](https://aka.ms/Fabric-Hero-Blog-Ignite23)

- Explore o Fabric por meio do [Tour Guiado](https://aka.ms/Fabric-GuidedTour)

- Inscreva-se para a [avaliação gratuita do Microsoft Fabric](https://aka.ms/try-fabric)

- Visite o [site do Microsoft Fabric](https://aka.ms/microsoft-fabric)

- Aprenda novas habilidades explorando os [módulos de Aprendizagem do Fabric](https://aka.ms/learn-fabric)

- Explore a [documentação técnica do Fabric](https://aka.ms/fabric-docs)

- Leia o [livro eletrônico gratuito sobre como começar a usar o Fabric](https://aka.ms/fabric-get-started-ebook)

- Participe da [comunidade do Fabric](https://aka.ms/fabric-community) para postar suas perguntas, compartilhar seus comentários e aprender com outras pessoas

Leia os blogs de comunicados de experiências do Fabric em mais detalhes:

- [Experiência do Data Factory no blog do Fabric](https://aka.ms/Fabric-Data-Factory-Blog)

- [Experiência do Synapse Data Engineering no blog do Fabric](https://aka.ms/Fabric-DE-Blog)

- [Experiência do Synapse Data Science no blog do Fabric](https://aka.ms/Fabric-DS-Blog)

- [Experiência do Synapse Data Warehousing no blog do Fabric](https://aka.ms/Fabric-DW-Blog)

- [Experiência do Synapse Real-Time Analytics no blog do Fabric](https://aka.ms/Fabric-RTA-Blog)

- [Blog de comunicado do Power BI](https://aka.ms/Fabric-PBI-Blog)

- [Experiência do Data Activator no blog do Fabric](https://aka.ms/Fabric-DA-Blog)

- [Administração e governança no blog do Fabric](https://aka.ms/Fabric-Admin-Gov-Blog)

- [OneLake no blog do Fabric](https://aka.ms/Fabric-OneLake-Blog)

- [Blog de integração do Dataverse e Microsoft Fabric](https://aka.ms/Dataverse-Fabric-Blog)

© 2026 Microsoft Corporation. Todos os direitos reservados.

Ao usar esta demonstração/este laboratório, você concorda com os seguintes termos:

A tecnologia/funcionalidade descrita nesta demonstração/neste laboratório é fornecida pela Microsoft Corporation para obter seus comentários e oferecer uma experiência de aprendizado. Você pode usar a demonstração/o laboratório somente para avaliar tais funcionalidades e recursos de tecnologia e fornecer comentários à Microsoft. Você não pode usá-los para nenhuma outra finalidade. Você não pode modificar, copiar, distribuir, transmitir, exibir, executar, reproduzir, publicar, licenciar, criar obras derivadas, transferir nem vender esta demonstração/este laboratório ou qualquer parte deles.

A CÓPIA OU A REPRODUÇÃO DA DEMONSTRAÇÃO/DO LABORATÓRIO (OU DE QUALQUER PARTE DELES) EM QUALQUER OUTRO SERVIDOR OU LOCAL PARA REPRODUÇÃO OU REDISTRIBUIÇÃO ADICIONAL É EXPRESSAMENTE PROIBIDA.

ESTA DEMONSTRAÇÃO/ESTE LABORATÓRIO FORNECE DETERMINADOS RECURSOS E FUNCIONALIDADES DE PRODUTO/TECNOLOGIA DE SOFTWARE, INCLUINDO NOVOS RECURSOS E CONCEITOS POTENCIAIS, EM UM AMBIENTE SIMULADO SEM CONFIGURAÇÃO NEM INSTALAÇÃO COMPLEXA PARA A FINALIDADE DESCRITA ACIMA. A TECNOLOGIA/OS CONCEITOS REPRESENTADOS NESTA DEMONSTRAÇÃO/NESTE LABORATÓRIO PODEM NÃO REPRESENTAR A FUNCIONALIDADE COMPLETA DOS RECURSOS E PODEM NÃO FUNCIONAR DA MESMA MANEIRA QUE UMA VERSÃO FINAL. ALÉM DISSO, PODEMOS NÃO LANÇAR UMA VERSÃO FINAL DE TAIS RECURSOS OU CONCEITOS. SUA EXPERIÊNCIA COM O USO DE TAIS RECURSOS E FUNCIONALIDADES EM UM AMBIENTE FÍSICO TAMBÉM PODE SER DIFERENTE. 

**COMENTÁRIOS**. Caso você forneça comentários sobre os recursos de tecnologia, as funcionalidades e/ou os conceitos descritos nesta demonstração/neste laboratório à Microsoft, você concederá à Microsoft, sem encargos, o direito de usar, compartilhar e comercializar seus comentários de qualquer forma e para qualquer finalidade. Você também concede a terceiros, sem encargos, quaisquer direitos de patente necessários para que seus produtos, suas tecnologias e seus serviços usem ou interajam com partes específicas de um software ou um serviço da Microsoft que inclua os comentários. Você não fornecerá comentários que estejam sujeitos a uma licença que exija que a Microsoft licencie seu software ou sua documentação para terceiros em virtude da inclusão de seus comentários neles. Esses direitos continuarão em vigor após o término do contrato.

POR MEIO DESTE, A MICROSOFT CORPORATION SE ISENTA DE TODAS AS GARANTIAS E CONDIÇÕES REFERENTES À DEMONSTRAÇÃO/AO LABORATÓRIO, INCLUINDO TODAS AS GARANTIAS E CONDIÇÕES DE COMERCIALIZAÇÃO, SEJAM ELAS EXPRESSAS, IMPLÍCITAS OU ESTATUTÁRIAS, > E DE ADEQUAÇÃO A UMA FINALIDADE ESPECÍFICA, TÍTULO E NÃO VIOLAÇÃO. A MICROSOFT NÃO DECLARA NEM GARANTE A PRECISÃO DOS RESULTADOS DERIVADOS DO USO DA DEMONSTRAÇÃO/DO LABORATÓRIO NEM A ADEQUAÇÃO DAS INFORMAÇÕES CONTIDAS NA DEMONSTRAÇÃO/NO LABORATÓRIO A QUALQUER FINALIDADE.

**AVISO DE ISENÇÃO DE RESPONSABILIDADE**

Esta demonstração/este laboratório contém apenas uma parte dos novos recursos e aprimoramentos do Microsoft Power BI. Alguns dos recursos podem ser alterados em versões futuras do produto. Nesta demonstração/neste laboratório, você aprenderá sobre alguns dos novos recursos, mas não todos.
