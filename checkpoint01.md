# Kotlin - Checkpoint 01

## Explicação de cada commit e seu código utilizado

### 1 - Implementando a passagem de parâmetros obrigatórios para a tela de Perfil

Nesse primeiro commit, foi feito: 
- A alteração da Rota da tela de Perfil;
- A adição ao escopo do composable da Perfil o parâmetro "nome";
- Alteração do Construtor do arquivo PerfilScreen para receber mais uma variável, sendo essa o nome criado na adição acima;
- Feito o display da variável nome no título da tela de perfil;
- Alterado o botão da tela de menu para seguir a nova Rota.

**Explicação do código**

```kotlin
composable(route = "perfil/{nome}")
```
Altera a rota da tela de perfil para "Perfil/{nome}", sendo que agora ela só estará disponível colocando algum valor após "perfil/"

```kotlin
val nome: String? = it.arguments?.getString("nome", "Usuário anonimo")
```
Adiciona ao escopo do composable a variável nome, podendo ser utilizada na LoginScreen.
No método getString do it.arguments?, os parâmetros são: 
- "nome", que representa a "chave" da variável, ou como ela será referenciada;
- "Usuário anonimo", sendo o valor padrão dessa variável (que no caso não será utilizado, por conta desse parâmetro ser obrigatório na rota)

```kotlin
PerfilScreen(modifier = Modifier.padding(innerPadding), navController, nome!!)
```
Passa o nome para o construtor do Perfil Screen, onde !! diz que essa variável deve ter valor (não nula)

```kotlin
text = "PERFIL de $nome"
```
Mostra o variável no Título de PerfilScreen, onde o $ faz o papel de referencia-la

### 2 - Implementando a passagem de parâmetros opcionais para a tela de Pedidos

No segundo commit, foi feito:
- Alterado a rota de pedidos para aceitar como parâmetro uma variável "cliente"
- Adicionado como argumento no escopo do composable "cliente", com valor padrão "Cliente Anonimo"

**Explicação do código**

```kotlin
composable(
    route = "pedidos?cliente={cliente}",
    arguments = listOf(navArgument("cliente") {
        defaultValue = "Cliente Anonimo"
    })
)
```
- Rota agora aceita o parâmetro "cliente", implementando da mesma forma que uma url na internet (A "?" pode ser entendida como "opcional");
- O parâmetro "arguments" do composable define as varíaveis que podem ser utilizadas pelo mesmo;
- defaultValue define um valor padrão para o parâmetro, caso ele não for passado pela URL.

```kotlin
fun PedidosScreen(modifier: Modifier = Modifier, navController: NavController, cliente: String?) {}
```
É possível verificar que o tipo String tem uma "?" ao lado, que diz que essa variável pode ser nula

### 3 - Adicionando a passagem de mais um parâmetro para a tela de Perfil

No terceiro e último commit, foi feito:
- Alterado a rota de Perfil para perfil/{nome}/{idade}
- Adicionado o parâmetro idade a tela de Perfil, sendo esse também um parâmetro adicional

**Explicação do código**

```kotlin
composable(
    route = "perfil/{nome}/{idade}",
    arguments = listOf(
        navArgument("nome") { type = NavType.StringType },
        navArgument("idade") { type = NavType.IntType }
    )
)
```
- Alterado a rota de perfil
- Define as duas variáveis que serão utilizadas no link

```kotlin
PerfilScreen(
    modifier = Modifier.padding(innerPadding),
    navController,
    nome!!,
    idade!!
)
```

- Altera o construtor de PerfilScreen para aceitar o parâmetro "idade"
- Coloca ambos os parâmetros da rota como não nulos com !!