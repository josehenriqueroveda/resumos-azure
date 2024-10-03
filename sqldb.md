# Criar um banco de dados individual (sem servidor)

Para criar um banco de dados individual no portal do Azure, este início rápido começa na página SQL do Azure.

1. Navegue até a página Selecionar uma opção de Implantação do SQL.

2. Em Bancos de dados SQL, deixe Tipo de recurso definido como Banco de dados individual e selecione Criar.

![](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/single-database-create-quickstart/select-deployment.png?view=azuresql)

3. Na guia Noções básicas do formulário Criar Banco de Dados SQL, em Detalhes do projeto, selecione a Assinatura do Azure desejada.

4. Para Grupo de recursos, selecione Criar, insira myResourceGroup e selecione OK.

5. Para Nome do banco de dados, insira mySampleDatabase.

6. Para Servidor, selecione Criar e preencha o formulário Novo servidor com os seguintes valores:

  - Nome do servidor: Insira mysqlserver e adicione caracteres para que o nome seja exclusivo. Não podemos fornecer um nome do servidor exato a ser usado porque os nomes dos servidores devem ser globalmente exclusivos para todos os servidores no Azure, não apenas para uma assinatura. Portanto, insira algo como mysqlserver12345 e o portal informará se esse nome está disponível ou não.
  
  - Localização: Selecione uma localização na lista suspensa.
  
  - Método de autenticação: selecione Usar autenticação do SQL.
  
  - Logon de administrador do servidor: insira azureuser.
  
  - Senha: insira uma senha que atenda aos requisitos e insira-a novamente no campo Confirmar senha.
  
Selecione OK.

7. Deixe Deseja usar o pool elástico do SQL definido como Não.
8. Para o Ambiente de carga de trabalho, especifique Desenvolvimento para este exercício.

O portal do Azure fornece uma opção de Ambiente de carga de trabalho que ajuda a predefinir algumas definições de configuração. Essas configurações podem ser substituídas. Essa opção se aplica somente à página do portal Criar Banco de Dados SQL. Caso contrário, a opção de Ambiente de carga de trabalho não terá impacto no licenciamento ou em outras definições de configuração de bancos de dados.

A escolha do ambiente de carga de trabalho de desenvolvimento define algumas opções, entre elas:

- A opção de Redundância do armazenamento de backup é o armazenamento com redundância local. O armazenamento com redundância local gera menos custos e é apropriado para ambientes de pré-produção que não exigem redundância do armazenamento com replicação de zona ou área geográfica.
- Computação + armazenamento é de Uso geral, Sem servidor com um único vCore. Por padrão, há um atraso de pausa automática de uma hora.
Escolhendo os conjuntos de ambientes de carga de trabalho de Produção:
- A Redundância de armazenamento de backup é o armazenamento com redundância geográfica, a opção padrão.
- Computação + armazenamento é Uso geral, Provisionado com 2 vCores e 32 GB de armazenamento. Isso pode ser modificado na próxima etapa.

9. Em Computação + armazenamento, selecione Configurar banco de dados.
10. Este guia de início rápido usa um banco de dados sem servidor. Portanto, mantenha Camada de serviço definida como Uso Geral (computação sem servidor mais econômica) e defina Camada de computação como Sem servidor. Escolha Aplicar.
11. Em Redundância de armazenamento de backup, escolha uma opção de redundância para a conta de armazenamento em que os seus backups serão salvos.
12. Selecione Avançar: Rede na parte inferior da página.

![](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/single-database-create-quickstart/new-sql-database-basics.png?view=azuresql)

13. Na guia Rede, para Método de conectividade, selecione Ponto de extremidade público.
14. Para Regras de firewall, defina Adicionar endereço IP do cliente atual como Sim. Deixe Permitir que serviços e recursos do Azure acessem este servidor definido como Não.
![](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/single-database-create-quickstart/networking.png?view=azuresql)

15. Em Política de conexão, escolha a política de conexão Padrão e mantenha Versão mínima do TLS no padrão de TLS 1.2.
16. Selecione Próximo: Segurança na parte inferior da página.

![](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/single-database-create-quickstart/networking-connections.png?view=azuresql)

17. Na página Segurança, você pode optar por iniciar uma avaliação gratuita do Microsoft Defender para SQL, bem como configurar o Razão, as Identidades gerenciadas e a TDE (Transparent Data Encryption), se desejar. Selecione Avançar: Configurações adicionais na parte inferior da página.
18. Na guia Configurações adicionais, na seção Fonte de dados, para Usar dados existentes, selecione Exemplo. Isso cria um banco de dados de amostra AdventureWorksLT, de modo que haja algumas tabelas e dados a consultar e com os quais experimentar, em vez de um banco de dados em branco vazio. Você também pode configurar o agrupamento de banco de dados e uma janela de manutenção.
19. Selecione Examinar + criar na parte inferior da página:

![](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/single-database-create-quickstart/additional-settings.png?view=azuresql)

20. Na página Examinar + criar, após examinar, selecione Criar.

# Consultar o banco de dados

Depois que o banco de dados for criado, você poderá usar o Editor de consultas (versão prévia) no portal do Azure para conectar-se ao banco de dados e consultar dados. 

1. No portal, pesquise e selecione bancos de dados SQL e selecione seu banco de dados na lista.
2. Na página para o seu banco de dados, selecione Editor de consultas (versão prévia) no menu à esquerda.
3. Insira suas informações de logon do administrador do servidor da autenticação do SQL ou use a autenticação do Microsoft Entra.

![](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/single-database-create-quickstart/query-editor-login.png?view=azuresql)

4. Insira a consulta a seguir no painel Editor de consultas.
```sql
SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
FROM SalesLT.ProductCategory pc
JOIN SalesLT.Product p
ON pc.productcategoryid = p.productcategoryid;
```

5. Selecione Executar e, em seguida, examine os resultados da consulta no painel Resultados.

![](https://learn.microsoft.com/pt-br/azure/azure-sql/database/media/single-database-create-quickstart/query-editor-results.png?view=azuresql)

6. Feche a página Editor de consultas e selecione OK quando solicitado para descartar as edições não salvas.

# Limpar os recursos

Mantenha o grupo de recursos, o servidor e o banco de dados individual para as próximas etapas e saiba como conectar e consultar seu banco de dados com métodos diferentes.

Quando você terminar de usar esses recursos, você poderá excluir o grupo de recursos criado, que também excluirá o servidor e o banco de dados individual dentro dele.

Para excluir myResourceGroup e todos os recursos dele usando o portal do Azure:

1. No portal, pesquise e selecione Grupos de recursos e, em seguidas, myResourceGroup na lista.
2. Na página Grupo de recursos, selecione Excluir grupo de recursos.
3. Em Digite o nome do grupo de recursos, insira myResourceGroup e selecione Excluir.
