# Frontend Style Guide

Welcome to QueroDelivery's Frontend Style Guide. Sit down, have a cup of coffee and read this calmly. ☕

## Introduction

The goal of this guide is to help our team to understand and
follow code style best practices, maintaining a pattern.

As this guide is an extension of the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript),
we **highly recommend** reading it before you continue.

# :pushpin: Table of Contents

* [Folder Structure](#folder-structure)
* [Naming](#naming)
* [Type Importation](#type-importation)

## Folder Structure

```sh
└── src/
    ├── app/                    
    |
    ├── assets/             
    |   ├── brand/ 
    |   |   ├── {some-image}/
    |   ├── images/ 
    |   |   ├── {some-image}/
    |   ├── svg/ 
    |   |   ├── {some-svg}/         
    |   ... 
    |                                 
    ├── components/             
    |   ├── {some-component}/   
    |   ├── layouts/ 
    |   |   ├── {some-component}/   
    |   ...                     
    |                           
    ├── config/                
    |   ├── {some-config}/  
    |   |   ├── lib/         
    |   ...                     
    |                           
    ├── constants/              
    |   ├── {some-constant}/        
    |   ...                     
    |                           
    ├── store/               
    |   ├── {some-context}/        
    |   ...                     
    |                           
    ├── feature/         
    |   ├── {some-feature}/        
    |   |   ├── api/            
    |   |   ├── components/          
    |   |   └── contexts/
    |   |   └── hooks/ 
    |   |   └── constants.ts/     
    |   |   └── index.tsx/  
    |   |   └── tpyes.ts/  
    |   |   └── utils.ts/            
    |   ...                 
    |                       
    ├── hooks/                 
    |   ├── {some-hook}/        
    |   ...                 
    |                       
    ├── pages/                 
    |   ├── {some-page}/                
    |   ...                 
    |                       
    ├── services/              
    |   ├── {some-service}/        
    |   ...                 
    |                       
    ├── styles/                
    |   ├── {some-style}/        
    |   ...                 
    |                       
    ├── types/                 
    |   ├── {some-type}/        
    |   ...                 
    |                       
    ├── utils/                 
    |   ├── {some-util}/        
    |   ...                 
    |                       
    └── index.tsx/          
```

## assets/
- A pasta assets contém todas as imagens, icones, arquivos de fonte, etc. para seu projeto. 
## components/
- Contém componentes reutilizáveis ​​que são usados ​​com mais frequência para compor uma Feature ou Página.
- Esses componentes são quase sempre puros e de apresentação, sem [side-effects](https://medium.com/@remoteupskill/what-is-a-react-side-effect-a5525129d251).
## layouts/
- Contém componentes de layout reutilizáveis. Um Componente de Layout é um componente que compõe o layout de uma página. Muitas vezes, ele importa componentes como sidebar,footer, sidebar.
- Se for provável que seu projeto tenha apenas um único layout, esse diretório pode não ser necessário e o Layout Component pode residir no diretório de componentes.
## config/
- Todas as configurações do aplicativo devem ser mantidas neste caminho. 
- Código de configuração do projeto, variáveis ​​globais, urls etc.
## lib/
- Esta pasta contém [fachadas](https://blog.webdevsimplified.com/2022-07/facade-pattern/) para as várias bibliotecas diferentes que você usa em seu projeto.
- Por exemplo, se você usar o axios library, esta pasta conterá um arquivo para essa biblioteca axios que cria sua própria API sobre a API axios que você usa em seu aplicativo.
- Isso significa que, em vez de importar axios diretamente em seu projeto, você importaria o arquivo desta pasta associado a axios.
## constants/
- Contém strings reutilizáveis ​​e imutáveis, como URLs ou padrões Regex.
## store/
- Redux Store.
## feature/
- Toda a lógica necessária para uma Feature é colocada em um único diretório. Uma Feature geralmente é composto de muitos outros componentes, locais ou compartilhados. 
O mesmo vale para todos os recursos: utils, types, hooks e assim por diante.
- Features geralmente incluem [side-effects](https://medium.com/@remoteupskill/what-is-a-react-side-effect-a5525129d251).
- Se estiver usando Redux e interagir com o Store, a Feature incluirá um arquivo slice que define o “slice” do Redux Store que o recurso representa.
## hooks/
- Contém React Hooks reutilizáveis.
## pages/
- Page componente de página. Cada componente de página está associado a uma rota.
- Page componente compõem o conteúdo de uma página importando Componentes e Features.
- Um Page componente raramente deve incluir [side-effects](https://medium.com/@remoteupskill/what-is-a-react-side-effect-a5525129d251) e, em vez disso, deve delegar [side-effects](https://medium.com/@remoteupskill/what-is-a-react-side-effect-a5525129d251) as Features.
## services/
- Esta pasta contém todo o seu código para interface com qualquer API externa.
## styles/
- Estilos reutilizáveis ​​ou globais. 
- Pode incluir configurações, redefinições ou variáveis.
## types/
- Tipos reutilizáveis ​​para projetos que utilizam TypeScript.
## utils/
- Funções utilitárias reutilizáveis. Essas funções devem ser sempre puras e não produzir [side-effects](https://medium.com/@remoteupskill/what-is-a-react-side-effect-a5525129d251).

## Naming

kebab-case para para nomes de arquivos dos aplicativos React.
```sh
// my-component
// my-component.tsx

return (
    <MyComponent />
)
```

TypeScript.
```ts
ComponentProps = {}
MethodApiResponse = {}
MethodApiParams =  {}
```

Utilizar Interface sempre que possível, Types devem ser utilizados somente quanto obrigado pelo TypeScript,
como na atribuição de valores.
Ex:
```ts
type value = string | number;
```

Objetos com mais de 3 atributos precisam de atenção. Se sua interface está ficando grande considere
quebrar o objeto em outra interface.

Ex:
```ts
/* Interface não precisa ser quebrada */
interface ObjectOne {
    dummyData: {
        _id: string;
        name: string;
        price: number;
    }
}

/* Interface precisa ser quebrada */
🔴 BAD
interface ObjectTwo {
    dummyDataOne: {
        _id: string;
        name: string;
        price: number
    },
    dummyDataTwo: {
        _id: string;
        name: string;
        image: {
            publicId: string;
            src: string;
            version: string;
        }
    }
}

✅ GOOD
interface DummyDataOne {
    _id: string;
    name: string;
    price: number
}

interface DummyDataTwo {
    _id: string;
    name: string;
    price: number;
    image: {
        publicId: string;
        src: string;
        version: string;
    }
}

interface ObjectTwo {
    dummyDataOne: DummyDataOne,
    dummyDataTwo: DummyDatTwo
}
```

## Type Importation 

Motivação: https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-8.html#type-only-imports-and-export

### Como exportar tipos e interfaces ? 

 Tipos podem estar junto de arquivos, comumentemente quando criamos interfaces de Props, por exemplo. 
 Porém, se a tipagem precisar ser exportada, ela deve ser instanciada em um arquivo separado de types, para também ser importada dessa forma. Com isso, nós sempre poderemos utilizar o *import type* para esses arquivos;


🔴 BAD
```ts
// api/get-products.ts

export type GetProductsData {...}

export function useGetProducts(params): GetProductsData {...}

// components/products-list
import { useGetProducts, GetProductsData } from '../api/get-products';

const products: GetProductsData = {...}

```

✅ GOOD
```ts
// api/types

export type GetProductsData {...}

// api/get-products.ts
import type { GetProductsData } from './types';

export function useGetProducts(params): GetProductsData {...}

// components/products-list
import { useGetProducts } from '../api/get-products';
import type { GetProductsData } from './api/types';

const products: GetProductsData = {...}

```

[Back to top ⬆️](#pushpin-table-of-contents)
