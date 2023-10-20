# Components

## Table of Contents

- [About](#about)
- [Directory Structure](#directory_structure)
- [Component Names](#names)
- [Dynamic Imports](#imports)
- [Npm Packages](#npm)
- [ClientOnly Component](#clientonly)

##
<h3><a href="https://nuxt.com/docs/guide/directory-structure/components">Документация</a></h3>

##

## About <a name = "about"></a>

Nuxt автоматически импортирует любые компоненты в этот каталог (вместе с компонентами, зарегистрированными любыми модулями, которые вы можете использовать).

## Directory Structure <a name = "directory_structure"></a>

Nuxt автоматически импортирует любые компоненты в этот каталог (вместе с компонентами, зарегистрированными любыми модулями, которые вы можете использовать).

```
| components/
--| AppHeader.vue
--| AppFooter.vue
```

```html
<!-- app.vue -->
<template>
  <div>
    <AppHeader />
    <NuxtPage />
    <AppFooter />
  </div>
</template>
```

## Component Names <a name = "names"></a>
Если у вас есть компонент во вложенных каталогах, например:
```
| components/
--| base/
----| foo/
------| Button.vue
```
... тогда имя компонента будет основано на его собственном каталоге пути и имени файла, при этом повторяющиеся сегменты будут удалены. Таким образом, имя компонента будет:

```html
<BaseFooButton />
```

> Для ясности мы рекомендуем, чтобы имя файла компонента совпадало с его именем. Итак, в приведенном выше примере вы можете переименовать Button.vue в BaseFooButton.vue.

## Dynamic Imports <a name = "imports"></a>
Чтобы динамически импортировать компонент (также известный как отложенная загрузка компонента), все, что вам нужно сделать, это добавить префикс Lazy к имени компонента. Это особенно полезно, если компонент не всегда нужен.

Используя префикс Lazy, вы можете отложить загрузку кода компонента до нужного момента, что может быть полезно для оптимизации размера вашего пакета JavaScript.

```html
<!-- pages/index.vue -->
<script setup>
  const show = ref(false)
</script>

<template>
  <div>
    <h1>Mountains</h1>
    <LazyMountainsList v-if="show" />
    <button v-if="!show" @click="show = true">Show List</button>
  </div>
</template>
```

## npm Packages <a name = "npm"></a>
Если вы хотите автоматически импортировать компоненты из пакета npm, вы можете использовать addComponent в локальном модуле для их регистрации.

```js
// ~/modules/register-component.ts
import { addComponent, defineNuxtModule } from '@nuxt/kit'

export default defineNuxtModule({
  setup() {
    // import { MyComponent as MyAutoImportedComponent } from 'my-npm-package'
    addComponent({
      name: 'MyAutoImportedComponent',
      export: 'MyComponent',
      filePath: 'my-npm-package',
    })
  },
})
```
>Любые вложенные каталоги необходимо добавлять в первую очередь, поскольку они сканируются по порядку.

## ClientOnly Component <a name = "clientonly"></a>
Nuxt предоставляет компонент ClientOnly для целенаправленной визуализации компонента только на стороне клиента.

```html
<!-- pages/example.vue -->
<template>
  <div>
    <Sidebar />
    <ClientOnly>
      <!-- this component will only be rendered on client-side -->
      <Comments />
    </ClientOnly>
  </div>
</template>
```
Используйте слот в качестве запасного варианта, пока ClientOnly не будет установлен на стороне клиента.

```html
<!-- pages/example.vue -->
<template>
  <div>
    <Sidebar />
    <!-- This renders the "span" element on the server side -->
    <ClientOnly fallbackTag="span">
      <!-- this component will only be rendered on client side -->
      <Comments />
      <template #fallback>
        <!-- this will be rendered on server side -->
        <p>Loading comments...</p>
      </template>
    </ClientOnly>
  </div>
</template>
```
