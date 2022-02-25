# Deploy em ambiente AWS Amplify

1. Execute o comando `npm install -g @aws-amplify/cli` para instalar o serverless framework. Utilizaremos a IDE Cloud9 e uma aplicação React.

2. Vamos criar um usuario para executar serviços no amplify. Para iniciar o processo execute o comando `amplify configure`

3. Precione enter para confirmar que esta como administrador. Então selecione `us-east-1` no seletor de região. E no ultima parte desse passo ele pergunta o nome do usuario a ser criado para o amplify. De o nome de `amplify-user`. Ele irá mostrar uma URL, clique nela para ir a outra página do console AWS onde irá criar o usuario. NÃO CLIQUE ENTER.

![img/acharcloud9.png](img/passo12.jpg)

![img/acharcloud9.png](img/passo13.jpg)

4. Avance na página de permissões se estiver como na imagem Clique em `Próximo Tags` e depois em `Próximo: Revisar` em seguida em `Criar usuário`:

![img/acharcloud9.png](img/passo14.jpg)

5. Acabamos de criar um usuário com acesso ao amplify copie os 2 valores em um bloco de notas **ID da chave de acesso** e **Chave de acesso secreta**. Volte ao Cloud9 e pressione **Enter**

6. Cole o **ID da chave de acesso -> accessKeyId** e aperte Enter cole o **Chave de acesso secreta -> secretAccessKey** e aperte Enter em **Profile Name** coloque `amplify-user`

![img/acharcloud9.png](img/passo15.jpg)

7. Agora vamos integrar o amplify ao projeto. no Cloud9 execute o comando `amplify init` digite o nome do seu projeto e depois aperte **Y** e Enter para confirmar

![img/acharcloud9.png](img/passo16.jpg)

8. Selecione `AWS access keys` como meio de acesso e novamente cole as credenciais do passo 21 e selecione a região `us-east-1`.

9. Após esse processo o amplify vai criar a base do projeto na sua conta AWS utilizando cloudformation. É possivel ver o status do projeto com o comando `amplify status`

![img/acharcloud9.png](img/passo17.jpg)

10. Agora faremos a criação do hosting no S3 e integração continua com o amplify. Digite o comando `amplify hosting add`
    1. Selecione `Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)`
    2. Em 'Choose a type' selecione Continuous `deployment (Git-based deployments)`
    3. Vá até o console AWS e busque por **Amplify**
    ![img/acharcloud9.png](img/passo18.jpg)
    4. Entre no seu projeto e selecione a aba `Hosting Environments` Selecione o **GitHub** e clique em **Connect branch** na lateral inferior direita.
    ![img/acharcloud9.png](img/passo19.jpg)
    5. Selecione o projeto postagram e a branch que quiser. Clique em **Next**.
    ![img/acharcloud9.png](img/passo20.jpg)
    6. Selecione o projeto postagram e a branch que quiser. Clique em **Next**.
    7. Selecione **Environment** como `dev` e marque a opção `Enable full-stack continuous deployments (CI/CD)` e depois clique no botão `Create new role` você será direcionado ao console para criar a role.
    8. Em **Casos de uso para outros serviços da AWS:** selecione `Amplify` marque a caixa `Amplify - Backend Deployment` e clique em **Próximo**
    ![img/acharcloud9.png](img/passo21.jpg)
    9. Clique em **Próximo**
    ![img/acharcloud9.png](img/passo22.jpg)
    10. Crie um nome para sua função role e clique em **Criar**
    ![img/acharcloud9.png](img/passo23.jpg)
    11. Volte ao amplify aperte em refresh e selecione a role que acabou de criar e clique em **Next**
    ![img/acharcloud9.png](img/passo24.jpg)
    12. Agora clique em  **Save and deploy**
    ![img/acharcloud9.png](img/passo25.jpg)
    13. Seu primeiro deploy acaba de acontecer.
    ![img/acharcloud9.png](img/passo26.jpg)

11. Vá para o Cloud9 a aperte **Enter**
![img/acharcloud9.png](img/passo27.jpg)

12. Digite os comandos `git add -A` e depois `git status` para visualizar os novos arquivos de configuração
![img/acharcloud9.png](img/passo28.jpg)

13. Digite os comandos abaixo
```
  git add -A
  git status
  git commit -m "adding hosting with amplify"
  git push origin main
  ```
![img/acharcloud9.png](img/passo29.jpg)

14. O Cloud9 irá pedir acesso ao repositório no github, Vá para o github acesse **Settings ->  Developer settings -> Personal access tokens -> Generate new token** crie um nome para seu token dê todas as permissões e clique em `Generate token` copie o token criado em um bloco de notas.
![img/acharcloud9.png](img/passo30.jpg)

15. Volte ao Cloud9 em Username digite o E-mail cadastrado no github e no Password cole o token gerado
![img/acharcloud9.png](img/passo31.jpg)

16. Após conceder a autorização o amplify fará o deploy automaticamente e rodará o pipeline
![img/acharcloud9.png](img/passo32.jpg)

17. Acessando menu **Build settings** Vemos a configuração do pipeline que será executada toda vez que o comando git push for executado na branch main
![img/acharcloud9.png](img/passo33.jpg)

18. Na aba da aplicação temos o campo **Domain** onde a aplicação estará rodando na web
![img/acharcloud9.png](img/passo34.jpg)
  
## Considerações finais

Em poucos passos já temos um ótimo ambiente Cloud seguro e configurado para desenvolvimento de qualquer aplicação.

Notamos que ao utilizar serviços do Amplify e S3 nossa aplicação fica largamente escalável pois varios profissionais podem trabalhar ao mesmo tempo na mesma aplicação fazendo alterações rapidamente.

Os logs no deploy do Amplify servem como uma forma de identificar rapidamente algum problema em algum código tanto no front como no back-end.

Sem dúvidas utilizar o deploy do Amplify e a hospedagem S3 faz com que equipe desenvolvimento e infraestrutura tenham mais produtividade no dia a dia.