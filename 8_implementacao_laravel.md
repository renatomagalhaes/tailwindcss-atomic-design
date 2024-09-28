# 8. Implementação com Laravel

## 📑 Índice de Implementações

1. [Implementação com Blade Padrão](#1-implementação-com-blade-padrão)
2. [Implementação com InertiaJS e Vue.js](#2-implementação-com-inertiajs-e-vuejs)
3. [Implementação com Livewire](#3-implementação-com-livewire)

## 🛠️ Introdução

Integrar **Atomic Design** com **Laravel** e **Tailwind CSS** permite criar aplicações web bem estruturadas, escaláveis e de fácil manutenção. Nesta seção, exploraremos três abordagens diferentes para implementar **Atomic Design** dentro de um projeto Laravel:

1. **Blade Padrão:** Utilizando **Blade Components** para organizar os componentes seguindo a metodologia Atomic Design.
2. **InertiaJS com Vue.js:** Combinando **InertiaJS** e **Vue.js** para criar aplicações monolíticas com uma experiência de usuário moderna e interativa.
3. **Livewire:** Integrando **Livewire** para construir interfaces dinâmicas sem a necessidade de escrever JavaScript adicional.

Cada abordagem será detalhada com exemplos práticos e explicações claras para facilitar o entendimento e a aplicação.

## 1. Implementação com Blade Padrão

### 🧩 Visão Geral

Utilizaremos **Blade Components** do Laravel para implementar a estrutura do **Atomic Design**. Essa abordagem aproveita os recursos nativos do Laravel para criar componentes reutilizáveis e manter uma organização lógica.

### 📂 Estrutura de Pastas Recomendada

```bash
app/
├── Http/
│   ├── Controllers/
│   │   └── ...
│   └── ...
├── Models/
│   └── ...
resources/
├── views/
│   ├── components/
│   │   ├── atoms/
│   │   │   ├── button.blade.php
│   │   │   ├── input.blade.php
│   │   │   └── ...
│   │   ├── molecules/
│   │   │   ├── search-field.blade.php
│   │   │   └── ...
│   │   ├── organisms/
│   │   │   ├── header.blade.php
│   │   │   └── ...
│   │   ├── templates/
│   │   │   ├── main-layout.blade.php
│   │   │   └── ...
│   │   └── pages/
│   │       ├── home.blade.php
│   │       └── ...
│   ├── layouts/
│   │   └── app.blade.php
│   └── ...
├── css/
│   └── styles.css
├── js/
│   └── app.js
└── ...
```

### 🧱 Criando os Componentes

#### 🟢 **Átomos**

**Exemplo: Botão**

```blade
<!-- resources/views/components/atoms/button.blade.php -->
<button {{ $attributes->merge(['class' => 'bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded']) }}>
    {{ $slot }}
</button>
```

**Uso no Blade:**

```blade
<!-- Exemplo de uso do componente de botão -->
<x-atoms.button>
    Enviar
</x-atoms.button>
```

#### 🟢 **Moléculas**

**Exemplo: Campo de Busca**

```blade
<!-- resources/views/components/molecules/search-field.blade.php -->
<div class="flex">
    <x-atoms.input type="text" placeholder="Buscar..." />
    <x-atoms.button class="bg-green-500 hover:bg-green-700">
        Buscar
    </x-atoms.button>
</div>
```

**Uso no Blade:**

```blade
<!-- Exemplo de uso do componente de campo de busca -->
<x-molecules.search-field />
```

#### 🟢 **Organismos**

**Exemplo: Cabeçalho**

```blade
<!-- resources/views/components/organisms/header.blade.php -->
<header class="flex items-center justify-between p-4 bg-gray-800">
    <div class="text-white text-xl">Meu Site</div>
    <nav class="flex space-x-4">
        <a href="#" class="text-gray-300 hover:text-white">Início</a>
        <a href="#" class="text-gray-300 hover:text-white">Sobre</a>
        <a href="#" class="text-gray-300 hover:text-white">Contato</a>
    </nav>
    <x-molecules.search-field />
</header>
```

**Uso no Blade:**

```blade
<!-- Exemplo de uso do componente de cabeçalho -->
<x-organisms.header />
```

#### 🟢 **Templates**

**Exemplo: Layout Principal**

```blade
<!-- resources/views/components/templates/main-layout.blade.php -->
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="{{ asset('css/output.css') }}" rel="stylesheet">
    <title>{{ $title ?? 'Meu Site' }}</title>
</head>
<body class="flex flex-col min-h-screen">
    <x-organisms.header />

    <main class="flex-grow p-4">
        {{ $slot }}
    </main>

    <footer class="bg-gray-800 text-white p-4">
        <p>&copy; 2024 Meu Site. Todos os direitos reservados.</p>
    </footer>
</body>
</html>
```

**Uso no Blade:**

```blade
<!-- Exemplo de uso do template principal -->
<x-templates.main-layout title="Página Inicial">
    <h1 class="text-2xl font-bold mb-4">Bem-vindo ao Meu Site</h1>
    <p class="text-gray-700">Este é um exemplo de página inicial usando Tailwind CSS com Atomic Design.</p>
</x-templates.main-layout>
```

#### 🟢 **Páginas**

**Exemplo: Página Inicial**

```blade
<!-- resources/views/pages/home.blade.php -->
<x-templates.main-layout title="Página Inicial">
    <h1 class="text-2xl font-bold mb-4">Bem-vindo ao Meu Site</h1>
    <p class="text-gray-700">Este é um exemplo de página inicial usando Tailwind CSS com Atomic Design.</p>
</x-templates.main-layout>
```

**Rota no Laravel:**

```php
// routes/web.php
Route::get('/', function () {
    return view('pages.home');
});
```

### 📈 Vantagens da Implementação com Blade Padrão

- **Reutilização Eficiente:** Maximiza a reutilização de componentes, reduzindo a duplicação de código.
- **Organização Estruturada:** Facilita a navegação e a manutenção do projeto com uma hierarquia clara.
- **Flexibilidade:** Blade Components permitem personalizar e estender componentes facilmente através de slots e props.
- **Integração com Ferramentas Laravel:** Facilita a integração com outras funcionalidades do Laravel, como Livewire e InertiaJS, para criar interfaces dinâmicas e interativas.

## 2. Implementação com InertiaJS e Vue.js

### 🧩 Visão Geral

Integrar **InertiaJS** com **Vue.js** permite criar aplicações monolíticas modernas, aproveitando o poder de frameworks front-end sem a necessidade de uma API separada. Com **Atomic Design**, podemos organizar os componentes de maneira eficiente, garantindo consistência e reutilização.

### 📂 Estrutura de Pastas Recomendada

```bash
app/
├── Http/
│   ├── Controllers/
│   │   └── ...
│   └── ...
├── Models/
│   └── ...
resources/
├── views/
│   ├── components/
│   │   ├── atoms/
│   │   │   ├── Button.vue
│   │   │   ├── Input.vue
│   │   │   └── ...
│   │   ├── molecules/
│   │   │   ├── SearchField.vue
│   │   │   └── ...
│   │   ├── organisms/
│   │   │   ├── Header.vue
│   │   │   └── ...
│   │   ├── templates/
│   │   │   ├── MainLayout.vue
│   │   │   └── ...
│   │   └── pages/
│   │       ├── Home.vue
│   │       └── ...
│   ├── layouts/
│   │   └── app.blade.php
│   └── ...
├── css/
│   └── styles.css
├── js/
│   ├── app.js
│   └── ...
└── ...
```

### 🧱 Passo a Passo da Implementação

#### 1. **Configuração Inicial com InertiaJS e Vue.js**

Siga os passos abaixo para configurar **InertiaJS** e **Vue.js** em seu projeto Laravel.

```bash
# Instale InertiaJS e Vue.js
composer require inertiajs/inertia-laravel
npm install @inertiajs/inertia @inertiajs/inertia-vue3 vue@next
```

#### 2. **Configuração do InertiaJS**

Edite o arquivo `resources/js/app.js` para configurar o **InertiaJS** com **Vue.js**.

```javascript
// resources/js/app.js
import { createApp, h } from 'vue';
import { createInertiaApp } from '@inertiajs/inertia-vue3';
import { InertiaProgress } from '@inertiajs/progress';

createInertiaApp({
    resolve: name => require(`./Pages/${name}.vue`),
    setup({ el, App, props, plugin }) {
        createApp({ render: () => h(App, props) })
            .use(plugin)
            .mount(el);
    },
});

InertiaProgress.init();
```

#### 3. **Criando Componentes com Vue.js seguindo Atomic Design**

##### 🟢 **Átomos**

**Exemplo: Botão Vue**

```vue
<!-- resources/js/components/atoms/Button.vue -->
<template>
    <button :class="buttonClasses" v-bind="$attrs">
        <slot></slot>
    </button>
</template>

<script>
export default {
    props: {
        variant: {
            type: String,
            default: 'primary',
            validator: value => ['primary', 'secondary'].includes(value),
        },
    },
    computed: {
        buttonClasses() {
            return this.variant === 'primary'
                ? 'bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded'
                : 'bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded';
        },
    },
};
</script>
```

##### 🟢 **Moléculas**

**Exemplo: Campo de Busca Vue**

```vue
<!-- resources/js/components/molecules/SearchField.vue -->
<template>
    <div class="flex">
        <Input type="text" class="border border-gray-300 rounded-l py-2 px-4" placeholder="Buscar..." />
        <Button variant="secondary">
            Buscar
        </Button>
    </div>
</template>

<script>
import Button from '../atoms/Button.vue';
import Input from '../atoms/Input.vue';

export default {
    components: {
        Button,
        Input,
    },
};
</script>
```

##### 🟢 **Organismos**

**Exemplo: Cabeçalho Vue**

```vue
<!-- resources/js/components/organisms/Header.vue -->
<template>
    <header class="flex items-center justify-between p-4 bg-gray-800">
        <div class="text-white text-xl">Meu Site</div>
        <nav class="flex space-x-4">
            <a href="#" class="text-gray-300 hover:text-white">Início</a>
            <a href="#" class="text-gray-300 hover:text-white">Sobre</a>
            <a href="#" class="text-gray-300 hover:text-white">Contato</a>
        </nav>
        <SearchField />
    </header>
</template>

<script>
import SearchField from '../molecules/SearchField.vue';

export default {
    components: {
        SearchField,
    },
};
</script>
```

##### 🟢 **Templates**

**Exemplo: Layout Principal Vue**

```vue
<!-- resources/js/layouts/MainLayout.vue -->
<template>
    <div class="flex flex-col min-h-screen">
        <Header />
        <main class="flex-grow p-4">
            <slot></slot>
        </main>
        <footer class="bg-gray-800 text-white p-4">
            <p>&copy; 2024 Meu Site. Todos os direitos reservados.</p>
        </footer>
    </div>
</template>

<script>
import Header from '../components/organisms/Header.vue';

export default {
    components: {
        Header,
    },
};
</script>
```

##### 🟢 **Páginas**

**Exemplo: Página Inicial Vue**

```vue
<!-- resources/js/Pages/Home.vue -->
<template>
    <MainLayout>
        <h1 class="text-2xl font-bold mb-4">Bem-vindo ao Meu Site</h1>
        <p class="text-gray-700">Este é um exemplo de página inicial usando Tailwind CSS com Atomic Design.</p>
    </MainLayout>
</template>

<script>
import MainLayout from '../layouts/MainLayout.vue';

export default {
    components: {
        MainLayout,
    },
};
</script>
```

**Rota no Laravel:**

```php
// routes/web.php
use Inertia\Inertia;

Route::get('/', function () {
    return Inertia::render('Home', [
        'title' => 'Página Inicial',
    ]);
});
```

### 📈 Vantagens da Implementação com InertiaJS e Vue.js

- **Experiência de Usuário Moderna:** Combina a reatividade de frameworks front-end com a simplicidade de aplicações monolíticas.
- **Reutilização Eficiente:** Componentes Vue.js podem ser facilmente reutilizados em diferentes partes da aplicação.
- **Organização Estruturada:** Mantém uma hierarquia clara de componentes seguindo a metodologia Atomic Design.
- **Integração Simplificada:** Facilita a integração com outras ferramentas e bibliotecas Vue.js para funcionalidades avançadas.

## 3. Implementação com Livewire

### 🧩 Visão Geral

**Livewire** é uma biblioteca poderosa para Laravel que permite criar interfaces dinâmicas e interativas utilizando apenas PHP, sem a necessidade de escrever JavaScript. Integrar **Atomic Design** com **Livewire** facilita a criação de componentes reativos e reutilizáveis, mantendo a organização e a consistência do projeto.

### 📂 Estrutura de Pastas Recomendada

```bash
app/
├── Http/
│   ├── Livewire/
│   │   ├── Components/
│   │   │   ├── Atoms/
│   │   │   │   ├── Button.php
│   │   │   │   ├── Input.php
│   │   │   │   └── ...
│   │   │   ├── Molecules/
│   │   │   │   ├── SearchField.php
│   │   │   │   └── ...
│   │   │   ├── Organisms/
│   │   │   │   ├── Header.php
│   │   │   │   └── ...
│   │   │   ├── Templates/
│   │   │   │   ├── MainLayout.php
│   │   │   │   └── ...
│   │   │   └── Pages/
│   │   │       ├── Home.php
│   │   │       └── ...
│   └── ...
resources/
├── views/
│   ├── livewire/
│   │   ├── atoms/
│   │   │   ├── button.blade.php
│   │   │   ├── input.blade.php
│   │   │   └── ...
│   │   ├── molecules/
│   │   │   ├── search-field.blade.php
│   │   │   └── ...
│   │   ├── organisms/
│   │   │   ├── header.blade.php
│   │   │   └── ...
│   │   ├── templates/
│   │   │   ├── main-layout.blade.php
│   │   │   └── ...
│   │   └── pages/
│   │       ├── home.blade.php
│   │       └── ...
│   ├── layouts/
│   │   └── app.blade.php
│   └── ...
├── css/
│   └── styles.css
├── js/
│   └── app.js
└── ...
```

### 🧱 Passo a Passo da Implementação

#### 1. **Instalação do Livewire**

Instale o **Livewire** via Composer e NPM.

```bash
# Instale Livewire via Composer
composer require livewire/livewire

# Instale Livewire via NPM
npm install livewire-vue
```

#### 2. **Publicação dos Assets do Livewire**

Publique os assets do Livewire.

```bash
php artisan livewire:publish --assets
```

#### 3. **Criando os Componentes com Livewire seguindo Atomic Design**

##### 🟢 **Átomos**

**Exemplo: Botão Livewire**

```php
<!-- app/Http/Livewire/Components/Atoms/Button.php -->
<?php

namespace App\Http\Livewire\Components\Atoms;

use Livewire\Component;

class Button extends Component
{
    public $variant = 'primary';

    public function render()
    {
        return view('livewire.components.atoms.button');
    }
}
```

```blade
<!-- resources/views/livewire/components/atoms/button.blade.php -->
<button {{ $attributes->merge(['class' => $variant === 'primary' ? 'bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded' : 'bg-gray-500 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded']) }}>
    {{ $slot }}
</button>
```

**Uso no Blade:**

```blade
<!-- Exemplo de uso do componente de botão Livewire -->
@livewire('components.atoms.button', ['variant' => 'primary'])
    Enviar
@endlivewire
```

##### 🟢 **Moléculas**

**Exemplo: Campo de Busca Livewire**

```php
<!-- app/Http/Livewire/Components/Molecules/SearchField.php -->
<?php

namespace App\Http\Livewire\Components\Molecules;

use Livewire\Component;

class SearchField extends Component
{
    public $query = '';

    public function render()
    {
        return view('livewire.components.molecules.search-field');
    }

    public function search()
    {
        // Lógica de busca
    }
}
```

```blade
<!-- resources/views/livewire/components/molecules/search-field.blade.php -->
<div class="flex">
    @livewire('components.atoms.input', ['type' => 'text', 'placeholder' => 'Buscar...', 'wire:model.debounce.300ms' => 'query'])
    @livewire('components.atoms.button', ['variant' => 'secondary', 'wire:click' => 'search'])
        Buscar
    @endlivewire
</div>
```

**Uso no Blade:**

```blade
<!-- Exemplo de uso do componente de campo de busca Livewire -->
@livewire('components.molecules.search-field')
```

##### 🟢 **Organismos**

**Exemplo: Cabeçalho Livewire**

```php
<!-- app/Http/Livewire/Components/Organisms/Header.php -->
<?php

namespace App\Http\Livewire\Components\Organisms;

use Livewire\Component;

class Header extends Component
{
    public function render()
    {
        return view('livewire.components.organisms.header');
    }
}
```

```blade
<!-- resources/views/livewire/components/organisms/header.blade.php -->
<header class="flex items-center justify-between p-4 bg-gray-800">
    <div class="text-white text-xl">Meu Site</div>
    <nav class="flex space-x-4">
        <a href="#" class="text-gray-300 hover:text-white">Início</a>
        <a href="#" class="text-gray-300 hover:text-white">Sobre</a>
        <a href="#" class="text-gray-300 hover:text-white">Contato</a>
    </nav>
    @livewire('components.molecules.search-field')
</header>
```

**Uso no Blade:**

```blade
<!-- Exemplo de uso do componente de cabeçalho Livewire -->
@livewire('components.organisms.header')
```

##### 🟢 **Templates**

**Exemplo: Layout Principal Livewire**

```php
<!-- app/Http/Livewire/Templates/MainLayout.php -->
<?php

namespace App\Http\Livewire\Templates;

use Livewire\Component;

class MainLayout extends Component
{
    public $title;

    public function render()
    {
        return view('livewire.templates.main-layout');
    }
}
```

```blade
<!-- resources/views/livewire/templates/main-layout.blade.php -->
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="{{ asset('css/output.css') }}" rel="stylesheet">
    <title>{{ $title ?? 'Meu Site' }}</title>
    @livewireStyles
</head>
<body class="flex flex-col min-h-screen">
    @livewire('components.organisms.header')

    <main class="flex-grow p-4">
        {{ $slot }}
    </main>

    <footer class="bg-gray-800 text-white p-4">
        <p>&copy; 2024 Meu Site. Todos os direitos reservados.</p>
    </footer>

    @livewireScripts
</body>
</html>
```

**Uso no Blade:**

```blade
<!-- Exemplo de uso do template principal Livewire -->
@livewire('templates.main-layout', ['title' => 'Página Inicial'])
    <h1 class="text-2xl font-bold mb-4">Bem-vindo ao Meu Site</h1>
    <p class="text-gray-700">Este é um exemplo de página inicial usando Tailwind CSS com Atomic Design.</p>
@endlivewire
```

##### 🟢 **Páginas**

**Exemplo: Página Inicial Livewire**

```php
<!-- app/Http/Livewire/Pages/Home.php -->
<?php

namespace App\Http\Livewire\Pages;

use Livewire\Component;

class Home extends Component
{
    public function render()
    {
        return view('livewire.pages.home');
    }
}
```

```blade
<!-- resources/views/livewire/pages/home.blade.php -->
@livewire('templates.main-layout', ['title' => 'Página Inicial'])
    <h1 class="text-2xl font-bold mb-4">Bem-vindo ao Meu Site</h1>
    <p class="text-gray-700">Este é um exemplo de página inicial usando Tailwind CSS com Atomic Design.</p>
@endlivewire
```

**Rota no Laravel:**

```php
// routes/web.php
use Inertia\Inertia;
use App\Http\Livewire\Pages\Home;

Route::get('/', Home::class);
```

### 📈 Vantagens da Implementação com Livewire

- **Interatividade Dinâmica:** Permite criar interfaces reativas sem a necessidade de escrever JavaScript adicional.
- **Reutilização Eficiente:** Componentes Livewire podem ser facilmente reutilizados em diferentes partes da aplicação.
- **Organização Estruturada:** Mantém uma hierarquia clara de componentes seguindo a metodologia Atomic Design.
- **Integração Simplificada:** Facilita a integração com outras ferramentas e bibliotecas Laravel para funcionalidades avançadas.

### ⚠️ Desvantagens e Considerações

- **Complexidade Inicial:** A configuração de Livewire e a organização segundo Atomic Design podem introduzir complexidade no início do projeto.
- **Sobrecarga de Arquivos:** A criação de muitos componentes pequenos pode levar a uma sobrecarga de arquivos, exigindo uma boa organização e nomenclatura.
- **Curva de Aprendizado:** Desenvolvedores novos em Livewire ou em Atomic Design podem precisar de tempo para se adaptar à metodologia e às ferramentas utilizadas.

## 📝 Considerações Finais

Integrar **Atomic Design** com **Laravel**, **InertiaJS**, **Vue.js** e **Livewire** oferece abordagens flexíveis e poderosas para construir aplicações web bem estruturadas e escaláveis. Cada método possui suas vantagens e considerações, permitindo que você escolha a melhor abordagem conforme as necessidades do seu projeto. Continue explorando as próximas seções para aprofundar ainda mais sua implementação e otimizar seu fluxo de trabalho.
