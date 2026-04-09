# Estudo de Navegação com Jetpack Compose

Este projeto é um guia prático para aprender os conceitos fundamentais de navegação no Android utilizando **Jetpack Compose**.

## 🚀 Conceitos Chave

### 1. NavController
O `navController` é o componente central. Ele mantém o estado da pilha de ecrãs e permite a navegação entre eles.
```kotlin
val navController = rememberNavController()
```

### 2. NavHost
O `NavHost` define o grafo de navegação, associando rotas (strings) a funções Composable.
```kotlin
NavHost(navController = navController, startDestination = "first") {
    composable("first") { FirstScreen(navController) }
    composable("second/{userName}") { ... }
}
```

### 3. Passagem de Argumentos
Existem duas formas principais de passar dados entre ecrãs:

*   **Argumentos Obrigatórios:** Definidos no path da rota: `second/{userName}`.
*   **Argumentos Opcionais (Query Params):** Definidos com `?`: `second/{userName}?age={age}`.

#### Exemplo de configuração:
```kotlin
composable(
    route = "second/{userName}?age={age}",
    arguments = listOf(
        navArgument("userName") { type = NavType.StringType },
        navArgument("age") { 
            type = NavType.StringType
            defaultValue = "0"
        }
    )
) { backStackEntry ->
    val name = backStackEntry.arguments?.getString("userName") ?: ""
    val age = backStackEntry.arguments?.getString("age") ?: "0"
    SecondScreen(navController, name, age)
}
```

### 4. Navegação e Voltar
*   **Ir para um ecrã:** `navController.navigate("rota")`
*   **Voltar atrás:** `navController.navigateUp()` ou `navController.popBackStack()`

---

## 🛠️ Interface e Layout

*   **Arrangement.Center & Alignment.CenterHorizontally:** Usados na `Column` para centrar os elementos vertical e horizontalmente.
*   **Modifier.background(Color):** Define a cor de fundo de um componente.
*   **remember { mutableStateOf("") }:** Utilizado para gerir o estado dos campos de texto (`TextField`).

## 📝 Notas de Estudo

1.  **Sintaxe `by`:** Requer os imports `androidx.compose.runtime.getValue` e `setValue`.
2.  **Segurança de Tipos:** Sempre usar o operador Elvis (`?:`) ao extrair argumentos do `backStackEntry` para evitar crashes por valores nulos.
3.  **Rotas:** A string da rota na navegação deve coincidir exatamente com a definida no `NavHost`. Cuidado com barras `/` extras antes de parâmetros opcionais.

---
