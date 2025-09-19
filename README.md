# ARQUITETURA PARA PROCESSAMENTO DE DADOS NA CLOUD AWS

# Gerenciando Instâncias EC2 na AWS

# *Descrição do Projeto*

A proposta é criar uma *Arquitetura da AWS utilizando os serviços Amazon Elastic Compute Cloud, Elastic Bock Store, Lambda Function e Simple Storage Service* 

O objetivo principal para essa arquitetura é automatizar um pipeline de processamento de dados de forma escalável e resiliente.

Em termos mais simples, a meta é:

# *Automatizar:*  
Iniciar o processamento de forma automática assim que um novo arquivo for enviado para o S3, eliminando a necessidade de intervenção manual.

# *Escalar:*  
Aumentar ou diminuir a capacidade de processamento de forma dinâmica, utilizando o poder do EC2, para lidar com grandes volumes de dados de maneira eficiente e sem interrupções.

# *Aproveitar o "serverless":*  
Utilizando a função Lambda para agir como o "cérebro" do fluxo de trabalho, controlando o início do processamento de forma econômica, sem a necessidade de manter servidores sempre ligados.

# *Manter a Resiliência:*  
Garantir que o armazenamento dos dados brutos e dos resultados seja seguro (S3) e que o processamento tenha um armazenamento de alta performance e persistente (EBS).

Desta maneira, a arquitetura permite que a aplicação possa processar dados de forma rápida, eficiente e confiável, independentemente do volume de informações que chegam.

## **Funcionalidades e Recursos**

O arquivo que entra na arquitetura AWS é a fonte de dados que necessita de algum tipo de processamento. Ele pode ser: 

Arquivo de Agendamentos de Consultas: Como um arquivo CSV ou JSON gerado por exemplo num sistema de clínicas. 

Dados de Dispositivos de Sensores: Um arquivo com leituras de temperatura de um maquinário de fábrica ou dados de um drone, que precisam ser analisados para detectar anomalias.

Dados de Vendas: Um relatório de vendas diário que é enviado para o S3. A arquitetura processaria o arquivo para atualizar um painel de BI (Business Intelligence) em tempo real.

Logs de Aplicações: Arquivos de log de um site ou aplicativo que contêm informações sobre o comportamento do usuário. O processamento pode ser para extrair métricas e insights.

Armazenamento de Dados Brutos (S3): O ponto de partida. Os arquivos são carregados em um S3 Bucket que serve como área de armazenamento para os dados brutos.

Lógica de Acionamento (Lambda): Uma Lambda Function é acionada automaticamente sempre que um novo arquivo é enviado para o bucket S3. A função não processa o arquivo, mas sim a notificação, e sua única tarefa é iniciar a instância EC2.

Computação Pesada (EC2): A instância EC2 é iniciada pela função Lambda. Ela é a "máquina de trabalho" que vai processar os dados. Este é o serviço ideal para tarefas de processamento que podem levar mais tempo ou exigir mais recursos do que o Lambda pode oferecer.

Armazenamento para a Instância (EBS): Um volume EBS é anexado à instância EC2. Ele oferece um disco de alta performance e persistente para a instância, onde ela pode armazenar temporariamente os dados que estão sendo processados, ou até mesmo os resultados finais, antes de salvá-los de volta no S3.

# Diagrama da Arquitetura

Esboço para o Diagrama no Draw.io

 Roteiro da arquitetura AWS, colocando os serviços em destaque:
1.	O arquivo é a fonte de dados que precisa de algum tipo de processamento.
2.	Dentro da VPC iniciamos pelo S3 Bucket. Denominado como "S3 Bucket de Dados Brutos".
3.	O S3 Bucket dispara a Lambda Function. Através de um "Evento: Novo Objeto Criado".
4.	Da Lambda Function em direção a uma Instância EC2. Temos a "Ação: Iniciar Processamento".
5.	A instância EC2, se conecta a um volume EBS. Que será o "Armazenamento Anexado". Como também adicionamos outro S3 Bucket, denominado de "S3 Bucket de Dados Processados", mostrando que os resultados do processamento são salvos lá.


