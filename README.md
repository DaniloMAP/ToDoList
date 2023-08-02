# Meu Aplicativo TODO List

Este é um aplicativo TODO List desenvolvido em Flutter, que permite ao usuário adicionar, visualizar e remover tarefas pendentes.

## Funcionalidades

- Adicionar uma nova tarefa.
- Visualizar a lista de tarefas pendentes.
- Remover tarefas da lista.

## Tecnologias Utilizadas

- Flutter: Framework de desenvolvimento de aplicativos móveis multiplataforma, permitindo criar apps nativos para Android e iOS a partir de um único código-fonte.
- Dart: Linguagem de programação utilizada pelo Flutter, com foco em simplicidade e agilidade no desenvolvimento de aplicativos.
- shared_preferences: Pacote utilizado para persistência de dados locais, armazenando as tarefas em formato JSON no dispositivo do usuário.

## Persistência de Dados

Neste aplicativo, a persistência de dados é realizada utilizando o pacote `shared_preferences`, que é uma forma simples de armazenar dados chave-valor no dispositivo. Com essa abordagem, as tarefas são armazenadas localmente no dispositivo do usuário mesmo após o aplicativo ser encerrado ou o dispositivo reiniciado.

O código responsável pela persistência de dados está no arquivo `todo_repository.dart`, onde a classe `TodoRepository` gerencia as operações de leitura e gravação dos dados utilizando o `SharedPreferences`.

```dart
import 'dart:convert';
import 'package:shared_preferences/shared_preferences.dart';
import 'package:todo_list/models/todo.dart';

const todoListKey = 'todo_list';

class TodoRepository {
  late SharedPreferences sharedPreferences;

  Future<List<Todo>> getTodoList() async {
    sharedPreferences = await SharedPreferences.getInstance();
    final String jsonString = sharedPreferences.getString(todoListKey) ?? '[]';
    final List jsonDecoded = json.decode(jsonString) as List;
    return jsonDecoded.map((e) => Todo.fromJson(e)).toList();
  }

  void SaveTodoList(List<Todo> todos) {
    final String jsonString = json.encode(todos);
    sharedPreferences.setString(todoListKey, jsonString);
  }
}
```

## Executando o Aplicativo

Para executar o aplicativo, é necessário ter o ambiente de desenvolvimento Flutter configurado. Após clonar este repositório, abra o projeto no Visual Studio Code (ou outra IDE de sua preferência) e execute o comando `flutter run` no terminal para rodar o aplicativo em um emulador ou dispositivo físico.

## Licença

Este projeto está sob a licença MIT. Consulte o arquivo `LICENSE` para obter mais detalhes.

