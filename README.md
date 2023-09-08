# Docker Python Env

## Por que Docker? (e não ambiente virtual como Poetry)

Diferente de ambientes virtuais como o Poetry, o Docker oferece um nível mais profundo de isolamento. Aqui estão algumas razões pelas quais você pode escolher Docker:

* **Ambiente Isolado**: Todas as dependências do seu projeto, incluindo o sistema operacional, bibliotecas e até mesmo variáveis de ambiente, são encapsuladas em um container. Isso garante que não haja conflitos com outras dependências no host.
    
* **Múltiplos Serviços**: Vários serviços, como bancos de dados, caches e servidores de aplicação, podem ser executados em um mesmo host, cada um em seu próprio container, garantindo que um não interfira no outro.
    
* **Consistência entre Colaboradores**: Como o Docker encapsula tudo, cada membro da equipe trabalha em um ambiente exatamente igual, independente do sistema operacional ou das configurações locais.
    
* **Versões do Python**: Com o Docker, é fácil mudar entre diferentes versões do Python sem ter que reinstalar ou reconfigurar o ambiente de desenvolvimento.
    
* **Redução do Tempo de Onboarding**: Novos colaboradores podem começar a trabalhar mais rapidamente. Basta instalar o Docker e rodar um único comando para configurar todo o ambiente de desenvolvimento.
    

## O que é Docker?

Docker é uma plataforma de software que permite criar, testar e implantar aplicações rapidamente usando containers. Um container é uma unidade padrão de software que empacota o código e todas as suas dependências, de forma que a aplicação rode de maneira rápida e confiável, independentemente do ambiente. Ao usar o Docker, você pode garantir que o software sempre funcionará da mesma forma, independentemente de onde ele é executado: seja em máquinas de desenvolvimento locais, testes ou em produção. Isso elimina o famoso problema "funciona na minha máquina". Em essência, o Docker permite "construir uma vez, rodar em qualquer lugar".

## docker-compose.yml

O `docker-compose.yml` é um arquivo que permite definir e executar múltiplos containers Docker como um único serviço:

* `services:`: Define os serviços (containers) que serão rodados.
    
* `app:`: Este é o serviço principal da sua aplicação Python.
        
* `build: .`: Constrói uma imagem a partir do `Dockerfile` presente no diretório atual.
* `container_name: python-server`: Nomeia o container como "python-server".
* `command: uvicorn src.main:app --host 0.0.0.0 --port 80 --reload`: Sobrescreve o comando padrão especificado no Dockerfile (opcional, já que é o mesmo comando).
* `ports:`: Mapeia portas do host para portas do container.
* `volumes:`: Monta volumes, neste caso, está mapeando o diretório atual do host para `/code` no container, permitindo desenvolvimento em tempo real.
* `depends_on:`: Especifica que o serviço `app` depende do serviço `redis`.
* `redis:`: Este é um serviço de banco de dados Redis.
        
 * `image: redis:alpine`: Usa uma imagem leve do Redis baseada na distribuição Alpine.

## Como rodar o projeto com Docker

1. **Construir e iniciar os containers**:
    
Com o `docker-compose`, é bastante simples rodar este projeto. Execute o seguinte comando para construir e iniciar os containers:
    
```bash
docker-compose up --build
```
    
A opção `--build` garante que a imagem seja construída antes de iniciar os containers.
    
2. **Parar os containers**:
    
Você pode parar os containers a qualquer momento pressionando `Ctrl + C` no terminal. Se desejar pará-los em segundo plano, use:
    
```bash
docker-compose down
```
    
Lembre-se de que, ao usar `docker-compose`, todos os serviços definidos no arquivo serão iniciados juntos, e eles poderão se comunicar entre si como se estivessem na mesma rede local.

Espero que esta explicação ajude a entender a configuração do seu projeto Docker e como rodá-lo!
