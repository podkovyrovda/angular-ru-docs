{@a providers}
# Провайдеры

Поставщик - это инструкция для системы [внедрение зависимостей](/guide/dependency-injection)о том, как получить значение для зависимости. В большинстве случаев эти зависимости являются услугами, которые вы создаете и предоставляете.

Для окончательного примера приложения с использованием провайдера, описанного на этой странице
увидеть <live-example></live-example>.

{@a providing-a-service}
## Предоставление услуги

Если у вас уже есть приложение, которое было создано с помощью [Angular CLI](cli), вы можете создать службу, используя [` ` ng generate` ](cli/generate)Команда CLI в корневом каталоге проекта. Замените _User_ на название вашего сервиса.

```sh
ng generate service User
```

Эта команда создает следующее `UserService` скелет:

<code-example path="providers/src/app/user.service.0.ts" header="src/app/user.service.ts"></code-example>

Теперь вы можете ввести `UserService` любом месте вашего приложения.

Сам сервис - это класс, сгенерированный CLI и `@Injectable()` . По умолчанию этот декоратор имеет `providedIn` свойство, которое создает провайдера для сервиса. В этом случае, `providedIn: 'root'` указывает, что Angular должен предоставлять сервис в корневом инжекторе.


{@a provider-scope}
## Объем провайдера

Когда вы добавляете поставщика услуг в инжектор корневого приложения, он становится доступным во всем приложении. Кроме того, эти поставщики также доступны для всех классов в приложении, если у них есть токен поиска.

Вы должны всегда предоставлять свою услугу в корневом инжекторе, если только вы не хотите, чтобы эта служба была доступна, только если потребитель импортирует определенный `@NgModule`.

{@a providedin-and-ngmodules}
## `providedIn` и NgModules

Также можно указать, что услуга должна предоставляться в определенном `@NgModule` . Например, если вы не хотите `UserService` будет доступен для приложений, если они не импортируют `UserModule` вы создали, вы можете указать, что служба должна быть предусмотрена в модуле:

<code-example path="providers/src/app/user.service.1.ts" header="src/app/user.service.ts"></code-example>

В приведенном выше примере показан предпочтительный способ предоставления услуги в модуле. Этот метод предпочтителен, потому что он позволяет трясти службу в дереве, если ее не внедряют. Если это не представляется возможным указать в службе, модуль должен обеспечить его, вы можете также объявить поставщик для службы в модуле:

<code-example path="providers/src/app/user.module.ts" header="src/app/user.module.ts"></code-example>

{@a limiting-provider-scope-by-lazy-loading-modules}
## Ограничение возможностей провайдера ленивой загрузкой модулей

В базовом приложении, сгенерированном CLI, модули загружаются с нетерпением, что означает, что все они загружаются при запуске приложения. Angular использует систему инжекторов, чтобы сделать вещи доступными между модулями. В загружаемом приложении с добавлением корневых приложений все поставщики во всех модулях доступны во всем приложении.

Это поведение обязательно меняется, когда вы используете ленивую загрузку. Ленивая загрузка - это когда вы загружаете модули только тогда, когда они вам нужны; например, при маршрутизации. Они загружаются не сразу, как в случае загруженных модулей. Это означает, что любые сервисы, перечисленные в их массивах провайдеров, недоступны, поскольку корневой инжектор не знает об этих модулях.

<!-- KW--Make diagram here -->
<!-- KW--per Misko: not clear if the lazy modules are siblings or grand-children. They are both depending on router structure. -->
Когда Angular маршрутизатор лениво загружает модуль, он создает новый инжектор. Этот инжектор является дочерним для инжектора корневого приложения. Представьте себе дерево инжекторов; Существует один корневой инжектор, а затем дочерний инжектор для каждого лениво загруженного модуля. Маршрутизатор добавляет всех поставщиков от корневого инжектора к дочернему инжектору. Когда маршрутизатор создает компонент в лениво загруженном контексте, Angular предпочитает экземпляры службы, созданные из этих поставщиков, экземплярам службы корневого инжектора приложения.

Любой компонент, созданный в контексте лениво загруженного модуля, например, с помощью навигации по маршрутизатору, получает локальный экземпляр службы, а не экземпляр в инжекторе корневого приложения. Компоненты во внешних модулях продолжают получать экземпляр, созданный для корня приложения.

Хотя вы можете предоставлять услуги с помощью отложенной загрузки модулей, не все службы могут загружаться с отложенной загрузкой. Например, некоторые модули работают только в корневом модуле, например, в маршрутизаторе. Маршрутизатор работает с глобальным объектом местоположения в браузере.


{@a limiting-provider-scope-with-components}
## Ограничение объема провайдера с компонентами

Другой способ ограничить область действия поставщика - добавить службу, которую вы хотите ограничить, к компоненту
 `providers` массив . Поставщики компонентов и поставщики NgModule не зависят друг от друга. Это
Метод полезен, когда вы хотите загружать модуль, которому нужен только сервис.
Предоставление услуги в компоненте ограничивает службу только к тому, что компонент (другие компоненты
Тот же модуль не может получить доступ к нему).

<code-example path="providers/src/app/app.component.ts" region="component-providers" header="src/app/app.component.ts"></code-example>


{@a providing-services-in-modules-vs.-components}
## Предоставление услуг в модулях против компонентов

Как правило, предоставьте сервисы, необходимые для всего приложения в корневом модуле, и предоставьте сервисы в виде лениво загруженных модулей.

Маршрутизатор работает на корневом уровне, поэтому, если вы поместите провайдеров в компонент, даже `AppComponent`, лениво загруженные модули, которые зависят от маршрутизатора, не могут их видеть.

<!-- KW--Make a diagram here -->
Зарегистрируйте поставщика с компонентом, если необходимо ограничить экземпляр службы компонентом и его деревом компонентов, то есть его дочерними компонентами. Например, пользовательский компонент редактирования, `UserEditorComponent`, который нуждается в закрытой копии кэширования `UserService` должен зарегистрировать `UserService` с `UserEditorComponent` . Затем каждый новый экземпляр `UserEditorComponent` получает свой собственный кэшированный экземпляр службы.


<hr>

{@a more-on-ngmodules}
## Больше на NgModules

Вы также можете быть заинтересованы в:
* [Singleton Services](guide/singleton-services), которая развивает концепции, описанные на этой странице.
* [Ленивые загрузочные модули](guide/lazy-loading-ngmodules).
* [Поставщики деревьев](guide/dependency-injection-providers#tree-shakable-providers).
* [NgModule FAQ](guide/ngmodule-faq).
