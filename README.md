# Análise do código

  1. O provider informa ao Terraform que a Cloud usada será
     a AWS e que a região será us-east-1.
  2. Depois são criadas duas variáveis, projeto e candidato.
  3. Cria uma chave tls usando algoritmo RSA e um par de chave AWS
     usando as variáveis candidato e projeto e a chave tls criada antes.
  4. Cria uma vpc na AWS com cidr 10.0.0.0/16, com suporte a dns,
     hostnames e usando uma tag name baseada nas variáveis anteriores.
  5. Cria uma subnet dentro da VPC criada anteriormente, com cidr 10.0.1.0/24
     zona de disponibilidade us-east-1a e tag name se baseado nas variáveis
     criadas antes.
  6. Cria um internet gateway dentro da VPC, com tag name baseado nas variáveis
     do arquivo.
  7. Cria uma tabela de roteamento para 0.0.0.0/0 usando o internet gateway
     criado antes e associa essa tabela à subnet criada antes, além de novamente
     definir um tag name com bases nas variáveis do passo 2.
  8. Cria um grupo de segurança associado a VPC criada, permitindo conexão SSH(porta 22)
     de qualquer endereço, e permite tráfego de saída. 
  9. Busca uma imagem mais recente debian-12, para usar em virtualização e com owner
     679593333241.
  10. Cria uma instância de ec2 t2.micro usando a imagem de debian do passo anterior, 
      na subnet e security group criados antes e com a aws key pair também criada antes.
      Associa um volume de 20GB gp2 e com argumento para deletar o volume quando a instância
      for terminada. Usa um script para dar o update e upgrade nos pacotes do sistema e 
      associa a instância a um IP público.
  11. Dá output da chave privada PEM para acessar a instância EC2 e do IP público associado
      a instância.

# Modificações e melhorias

  1. Foi adicionada uma variável para representar um IP ou bloco CIDR para ser usada no
     acesso por meio de SSH, onde ao invés de qualquer endereço puder acessar por SSH.
  2. Disabilita o IP público criado automaticamente.
  3. Encriptar o volume da instância EC2.
  4. Habilitar os logs da VPC e salva-los no AWS CloudWatch.
  
  - Alterei a variável nome do candidato para o meu nome.

# Arquivos

  O arquivo main.tf é o arquivo original sem nenhuma alteração e o arquivo main-updated.tf
  é o arquivo depois das alterações da 2a etapa.
