# Avaliacao-P1
# Projeto Avaliativo P1 - App Flutter com Login e Cadastro (MVVM)

## Membros do Grupo
- Davi Souza Lima
- Eduardo Ferreira Honório
- Gabriel Novais Corsini

## Sobre o Projeto
Este projeto é um aplicativo mobile em Flutter desenvolvido como requisito para a Atividade Avaliativa P1. O objetivo principal do projeto é demonstrar o domínio de conceitos estruturais, navegação entre telas, uso de formulários com validação e a implementação de uma arquitetura limpa com armazenamento de dados mockados em memória.

## Funcionalidades e Fluxo do Aplicativo
O sistema implementa integralmente o fluxo exigido pelas regras da atividade:
1. **Splash Screen**: A primeira tela a ser exibida. Conta com elementos de layout e aguarda o processamento de uma regra de negócio simulada (3 segundos) para navegar automaticamente até o login.
2. **Tela de Login**: Exibe os campos de e-mail e senha. Possui validação de preenchimento, controle de visibilidade de senha e busca o usuário na estrutura mockada na memória. Caso as credenciais não coincidam, exibe uma mensagem de erro (Snackbar), cumprindo um dos diferenciais propostos.
3. **Tela de Cadastro**: Permite registrar um novo usuário com Nome, E-mail e Senha. Ao salvar, os dados são armazenados na memória, uma notificação de sucesso é exibida ao usuário (diferencial), e a navegação retorna à tela de login.
4. **Tela Home**: Acessível apenas com login bem-sucedido. Apresenta o texto de boas-vindas, um ícone centralizado e um botão no cabeçalho para realizar o logout.

## Arquitetura e Organização do Código
A estrutura do projeto foi desenhada seguindo o padrão **MVVM (Model-View-ViewModel)**, garantindo alta separação de responsabilidades. O projeto não faz uso de banco de dados real ou APIs externas, mantendo-se fiel à proposta de dados em memória.

A organização adotada baseou-se nos seguintes pilares:

* **Models (`lib/app/models/`)**: Representam os moldes de dados do sistema. Foi criado a classe `UsuarioModel` contendo os atributos nome, e-mail e senha, reforçando os conceitos de orientação a objetos.
* **Data / Mock Store (`lib/app/data/`)**: Contém a classe `UsuarioMockStore`, desenvolvida utilizando o **Padrão Singleton**. Ela é responsável por manter uma lista de instâncias de `UsuarioModel` viva durante toda a execução do aplicativo. Graças a esse padrão, a tela de cadastro e a tela de login conseguem consultar e adicionar informações na mesma lista compartilhada de forma simples e segura.
* **ViewModels (`lib/app/viewmodels/`)**: Classes que isolam as regras de negócio das telas visuais. 
  * O `LoginViewmodel`, por exemplo, estende `ChangeNotifier` para criar reatividade no layout (como alternar a visualização da senha e mostrar indicador de carregamento).
  * O `RegisterViewModel` se comunica com a camada de `Data` para salvar o modelo em memória.
  * O `SplashViewModel` encapusla a lógica de carregamento inicial.
* **Views (`lib/app/views/`)**: Telas que constroem a interface (`SplashPage`, `LoginPage`, `RegisterPage` e `HomePage`) utilizando formulários (`TextFormField`) e recebendo interações. Elas delegam qualquer decisão ou cálculo complexo para o seu respectivo ViewModel.
* **Routes (`lib/app/routes/`)**: Camada de controle de navegação contendo mapeamento centralizado de rotas (`app_routes.dart` e `app_pages.dart`) implementadas no `AppWidget`, evitando Strings mágicas soltas no código e organizando a troca de telas.
## Estrutura de Pastas Implementada
Seguindo as boas práticas sugeridas na atividade, o repositório está organizado da seguinte maneira:

```text
lib/
├── main.dart
└── app/
    ├── app_widget.dart
    ├── data/
    │   └── usuario_mock_store.dart
    ├── models/
    │   └── usuario_model.dart
    ├── routes/
    │   ├── app_pages.dart
    │   └── app_routes.dart
    ├── viewmodels/
    │   ├── login_viewmodel.dart
    │   ├── register_viewmodel.dart
    │   └── splash_viewmodel.dart
    └── views/
        ├── home_page.dart
        ├── login_page.dart
        ├── register_page.dart
        └── splash_page.dart
