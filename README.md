# Interview Questions

В данном репозитории находится контент для приложения [Interview Questions](https://it-incubator.io/simulators/interview-questions/info).
Это дружелюбное приложение для обучения разработчиков и подготовки к собеседованию.

Ты можешь внести свой вклад в развитие проекта: cтать авторов вопроса или теста, исправить ошибки.

### Как внести свой вклад
Ниже приводится инструкция, рассчитанная на новичков в open-source. Ещё более подробную инструкцию можно прочитать [здесь](https://github.com/firstcontributions/first-contributions).

1. Форкни этот репозиторий (в твоём аккаунте появится копия этого репозитория)
2. Склонируй форкнутый репозитория из своего аккаунта к себе на компьютер
3. Создай ветку от ветки develop и внеси в неё необходимые изменения
4. Сделай коммит и запуш свою ветку на GitHub

```git push -u origin your-branch-name```

5. В твоём репозитории на GitHub появится кнопка `Compare & pull request`. С помощью неё отправь пулреквест в ветку develop этого репозитория. В скором времени твои изменения будут приняты :)

### Как добавить новый вопрос в существующий тест
В тестах может быть любое количество вопросов. Сервер всегда выбирает 10 случайных вопросов для отправки. Ты можешь добавлять вопросы в любой из сущестующих тестов.

Для каждого теста существует папка (путь: `src/data/tasks`), в которой лежат файлы вопросов в формате json. Создай новый json-файл и добавь туда вопрос в формате описанном ниже.

В созданном json-файле могут быть следующие ключи:
- `questionText` - текст вопроса. Если в тексте вопросе присутствуют строки кода, оберни их в обратные кавычки(``). Это необходимо для форматирования текста
- `type` - укажи тип вопроса. В данный момент доступны два варианта: `radio` (только один правильный ответ) и `checkbox` (правильных ответов может быть больше одного)
- `code` (опционально) - в вопрос можно добавить блок кода. Значение этого свойства представляет собой объект с двумя ключами:
  - `text` - код в виде строки. Для переноса строк можно использовать символ переноса строки `\n`
  - `lang` - язык на котором написан код. Например, `css`, `js`, `jsx`, `html`
- `answers` - массив, содержащий варианты ответа в виде объектов. Каждый ответ содержит два поля:
  - `text` - текст ответа. Если в тексте ответа есть строки кода, оберни их в ``.
  - `isCorrect` - булевое значение (является ли ответ правильным). В зависимости от типа вопроса правильных ответов может быть один или несколько.
- `author` - (опционально) твой ник на GitHub - будет отображаться в приложении вместе с вопросом.
- `descriptionMarkup` - (опционально) - примечание к вопросу. Сюда можно добавить дополнительную информацию, ссылки на статьи или YouTube-видео, объясняющие вопрос или ответ. Формат - HTML в виде строки. Строки кода выделяются тегами `<code>`. Допустимые теги: `<p>`, `<a>`, `<code>`.

Пример вопроса (ненастоящего):
```json
{
  "questionText": "Как можно сделать глубокую копию этого объекта?",
  "code": {
    "lang": "js",
    "text": "const user = {\n  name: 'Sonya',\n  age: 28,\n  friends: ['Vasilisa', 'Kate', 'Brendan'],\n}\n\nlet userDeepCopy"
  },
  "answers": [
    {
      "text": "Вручную, используя spread-оператор следующим образом: `{...user}`",
      "isCorrect": false
    },
    {
      "text": "Вручную, используя spread-оператор следующим образом: `{...user, friends: [...user.friends]}`",
      "isCorrect": true
    },
    {
      "text": "Использовать метод Object.assign: `Object.assign(userDeepCopy, user)`",
      "isCorrect": false
    },
    {
      "text": "Использовать методы встроенного JSON-объекта: `JSON.parse(JSON.stringify(user))`",
      "isCorrect": true
    },
    {
      "text": "С помощью WebAPI-метода `structuredClone`",
      "isCorrect": true
    }
  ],
  "author": "StarkovSergey",
  "descriptionMarkup": "<p>Следует помнить, что <code>Object.assign</code> и spread-оператор делают неглубокую копию (shallow copy).</code></p><p>Использовать JSON-методы следует с пониманием ограничений JSON-формата. Например, такая копия лишит объект всех методов (JSON не предусматривает функций).</p><p><code>structuredClone</code> - новое браузерное API для глубокого копирования. Почитать о нём можно на <a href='https://developer.mozilla.org/en-US/docs/Web/API/structuredClone' target='_blank' rel=\"noopener noreferrer\">MDN</a>.</p>"
}
```

### Как добавить новый тест
Можно добавлять новые тесты по различным технологиям и на различные темы. 
Для этого нужно: 
1. Создать новую папку (путь: `src/data/tasks`), в которую будут добавляться вопросы
2. Добавить описание теста в массив `exams` (в файле: `src/exams.ts`). 
Описание теста добавляется в следующем формате:
```ts
  {
    id: 'js-basic', // соответствует названию созданной папки, в которой хранятся вопросы
    title: 'JS Basic',
    category: 'JavaScript', // язык или технология
    level: 'basic', //  'basic' | 'middle' | 'advanced'
    labels: ['frontend', 'backend'] // будут использоваться как теги
  }
```
Новый тест будет добавлен в приложение, как только в нём будет хотя бы 5 вопросов.
