# CreatePostgres
Como criar o banco de dados postgres no dcoker


# Explicação Detalhada dos Parâmetros

## `docker run`
- Este é o comando base do Docker para criar e executar containers.  
- Ele combina a criação e a execução do container em uma única etapa.

## `--name my_postgres`
- Define o nome do container como `my_postgres`.  
- Este nome é útil para identificar o container ao gerenciar múltiplos containers no sistema.  
- Você pode usar esse nome em comandos como `docker stop my_postgres` ou `docker logs my_postgres`.

## `-e POSTGRES_PASSWORD=mysecretpassword`
- Define uma variável de ambiente dentro do container.  
- Neste caso, a variável `POSTGRES_PASSWORD` é obrigatória para a imagem do PostgreSQL.  
- Ela configura a senha do usuário padrão do banco de dados, que também é chamado `postgres`.

## `-p 5433:5432`
- Configura o mapeamento de portas entre o host (sua máquina) e o container.  
  - O formato é `host_port:container_port`.  
- No exemplo:
  - `5433`: Porta no host, onde o banco estará acessível externamente.  
  - `5432`: Porta padrão usada pelo PostgreSQL dentro do container.  
- Isso significa que o banco de dados será acessado no host pelo endereço `localhost:5433`, enquanto o PostgreSQL dentro do container continua ouvindo na porta `5432`.

## `-d`
- Executa o container no modo *detached*, ou seja, em segundo plano.  
- Sem esta opção, o terminal permaneceria conectado ao processo do container, exibindo seus logs.

## `--rm`
- Remove automaticamente o container quando ele é parado.  
- Útil para evitar o acúmulo de containers parados, especialmente em ambientes de teste ou desenvolvimento.  
- Se você precisa de persistência do container, não use esta opção.

## `postgres:latest`
- Especifica a imagem do PostgreSQL a ser utilizada para criar o container.  
- `postgres`: Nome da imagem oficial do PostgreSQL hospedada no Docker Hub.  
- `latest`: Tag que indica a versão mais recente disponível da imagem.  
- Você pode substituir `latest` por uma versão específica, como `postgres:15` para garantir previsibilidade.

---

### Notas Importantes

- **Persistência de Dados**:  
  Este comando não configura volumes para persistir os dados do banco. Sem volumes, os dados são armazenados no sistema de arquivos do container, e serão perdidos se o container for removido.  
  Para configurar a persistência de dados, utilize a opção `-v` para montar um volume:

  ```bash
  docker run --name my_postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5433:5432 -d -v my_postgres_data:/var/lib/postgresql/data postgres:latest
