{@a getting-started-with-angular-deployment}
# Начало работы с Angular: Развертывание


Чтобы развернуть ваше приложение, вы должны скомпилировать его, а затем разместить JavaScript, CSS и HTML на веб-сервере. Встроенные приложения Angular очень переносимы и могут работать в любой среде или обслуживаться любыми технологиями, такими как Node, Java,.NET, PHP и многими другими.

<div class="alert is-helpful">


Независимо от того, пришли ли вы прямо из [вашего первого приложения](start "Getting Started: Your First App") или полностью заполнили приложение интернет-магазина с помощью [маршрутизация](start/start-routing "Getting Started: Routing"), [управление данными](start/start-data "Getting Started: Managing Data") и [формы](start/start-forms "Getting Started: Forms") разделы, у вас есть приложение, которое вы можете развернуть, следуя инструкциям в этом разделе.


</div>

{@a share-your-application}
## Поделитесь своей заявкой

Проекты StackBlitz по умолчанию являются общедоступными, что позволяет вам поделиться своим приложением Angular через URL проекта. Имейте в виду, что это отличный способ поделиться идеями и прототипами, но он не предназначен для производственного хостинга.

1. В своем проекте StackBlitz убедитесь, что вы разветвили или сохранили свой проект.
1. На странице предварительного просмотра вы должны увидеть URL, который выглядит как `https://<Project ID>.stackblitz.io`.
1. Поделитесь этим URL с другом или коллегой.
1. Пользователи, которые посещают ваш URL, увидят запуск сервера разработки, а затем загрузится ваше приложение.

{@a building-locally}
## Собираем локально

Чтобы создать приложение локально или для "боевого" сервера, загрузите исходный код из проекта StackBlitz, нажав `Download Project` значок в левом меню напротив `Project` для загрузки ваших файлов.

После того, как исходный код загружен и распакован, используйте [Angular Console](https://angularconsole.com "Angular Console web site") для обслуживания приложения или установите `Node.js` и обслуживайте ваше приложение с помощью Angular CLI.

От терминала, установить Angular CLI глобально с:

```sh
npm install -g @angular/cli
```

Это устанавливает команду `ng` в вашей системе - это команда, которую вы используете для создания новых рабочих пространств, новых проектов, обслуживания вашего приложения во время разработки или создания сборок для совместного использования или распространения.

Создать новую Angular CLI рабочее пространство с помощью [`ng new`](cli/new "CLI ng new command reference") команду:

```sh
ng new my-project-name
```

В вашем новом сгенерированном приложении CLI замените `/src` папка с одним из ваших `StackBlitz`, а затем выполните сборку.

```sh
ng build --prod
```

Это создаст файлы, которые вам нужно развернуть.

<div class="alert is-helpful">

Если выше `ng build` Команда выдает ошибку об отсутствующих пакетах, добавляет отсутствующие зависимости в ваш локальный проект `package.json` Файл файлу в загруженном проекте StackBlitz.

</div>

{@a hosting-the-built-project}
#### Хостинг построенного проекта

Файлы в `dist/my-project-name` является статической. Это означает, что вы можете разместить их на любом веб-сервере, способном обслуживать файлы (например, `Node.js`, Java,.NET) или любой бэкэнд (такой как Firebase, Google Cloud или App Engine).

{@a hosting-an-angular-app-on-firebase}
### Хостинг приложения Angular на Firebase

Один из самых простых способов оживить ваш сайт - разместить его на Firebase.

1. Зарегистрируйте учетную запись в [Firebase Firebase](https://firebase.google.com/ "Firebase web site").
1. Создайте новый проект, присвоив ему любое имя.
1. Добавить `@angular/fire` которые будут обрабатывать ваше развертывание, используя `ng add @angular/fire`.
1. Подключите ваш CLI к вашей учетной записи Firebase и инициализируйте соединение с вашим проектом, используя `firebase login` и `firebase init`.
1. Следуйте инструкциям, чтобы выбрать `Firebase` Проект который вы создаете для хостинга.
    - Выберите `Hosting` Вариант в первой строке.
    - Выберите проект, который вы ранее создали на Firebase.
    - Выбрать `dist/my-project-name` как публичный каталог.
1. Разверните ваше приложение с `ng deploy`.
1. После развертывания посетите https://your-firebase-project-name.firebaseapp.com, чтобы увидеть его вживую!

{@a hosting-an-angular-app-anywhere-else}
### Хостим приложение Angular в другом месте

Чтобы разместить приложение Angular на другом веб-хосте, загрузите или отправьте файлы на хост.
Поскольку вы создаете одностраничное приложение, вам также необходимо убедиться, что вы перенаправили все недействительные URL-адреса на ваш `index.html` файл.
Подробнее о разработке и распространении вашего приложения читайте в руководствах [Сборка и обслуживание](guide/build "Building and Serving Angular Apps") и [Развертывание](guide/deployment "Deployment guide").

{@a join-the-angular-community}
## Присоединяйтесь к сообществу Angular

Теперь вы являетесь разработчиком Angular! [Поделитесь этим моментом](https://twitter.com/intent/tweet?url=https://angular.io/start&text=I%20just%20finished%20the%20Angular%20Getting%20Started%20Tutorial "Angular on Twitter"), расскажите нам, что вы думаете об этом Приступая к работе, или отправьте [предложения для будущих выпусков](https://github.com/angular/angular/issues/new/choose "Angular GitHub repository new issue form").

Angular предлагает гораздо больше возможностей, и теперь у вас есть фундамент, который дает вам возможность создавать приложения и исследовать другие возможности:

* Angular предоставляет расширенные возможности для мобильных приложений, анимации, интернационализации, рендеринга на стороне сервера и многого другого.
* [Angular Material](https://material.angular.io/ "Angular Material web site") предлагает обширную библиотеку компонентов Material Design.
* [Angular Protractor](https://protractor.angular.io/ "Angular Protractor web site") предлагает комплексную среду тестирования для приложений Angular.
* Angular также имеет обширную [сеть сторонних инструментов и библиотек](https://angular.io/resources "Angular resources list").

Будьте в курсе, следуя [Angular блог](https://blog.angular.io/ "Angular blog").




