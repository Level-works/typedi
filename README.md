# TypeDI

![Build Status](https://github.com/level-works/typedi/workflows/CI/badge.svg)
[![npm version](https://img.shields.io/npm/v/@level-works/typedi)](https://npmjs.com/package/@level-works/typedi)

TypeDI is a [dependency injection](https://en.wikipedia.org/wiki/Dependency_injection) tool for TypeScript and JavaScript. With it you can build well-structured and easily testable applications in Node or in the browser.

Main features includes:

- property based injection
- constructor based injection
- singleton and transient services
- support for multiple DI containers

## Installation

> Note: This installation guide is for usage with TypeScript, if you wish to use
> TypeDI without Typescript please read the documentation about how get started.

To start using TypeDI install the required packages via NPM:

```bash
npm install typedi reflect-metadata
```

Import the `reflect-metadata` package at the **first line** of your application:

```ts
import 'reflect-metadata';

// Your other imports and initialization code
// comes here after you imported the reflect-metadata package!
```

As a last step, you need to enable emitting decorator metadata in your Typescript config. Add these two lines to your `tsconfig.json` file under the `compilerOptions` key:

```json
"emitDecoratorMetadata": true,
"experimentalDecorators": true,
```

Now you are ready to use TypeDI with Typescript!

## Basic Usage

```ts
import { Container, Service } from '@levelworks/typedi';

@Service()
class ExampleInjectedService {
  printMessage() {
    console.log('I am alive!');
  }
}

@Service()
class ExampleService {
  constructor(
    // because we annotated ExampleInjectedService with the @Service()
    // decorator TypeDI will automatically inject an instance of
    // ExampleInjectedService here when the ExampleService class is requested
    // from TypeDI.
    public injectedService: ExampleInjectedService
  ) {}
}

const serviceInstance = Container.get(ExampleService);
// we request an instance of ExampleService from TypeDI

serviceInstance.injectedService.printMessage();
// logs "I am alive!" to the console
```

## Documentation

The detailed usage guide and API documentation for the project can be found:

- at [docs.typestack.community/typedi][docs-stable]
- in the `./docs` folder of the repository

[docs-stable]: https://docs.typestack.community/typedi/
[docs-development]: https://docs.typestack.community/typedi/v/develop/

## Why the fork?

During development using typedi, we ran into the bug described by
[typedi#237](https://github.com/typestack/typedi/issues/237), which prevented us
from implementing decoupled services within our stack. The described bug had
already been fixed, but had yet to be released.

The only activity on [the original typedi](https://github.com/typestack/typedi)
was by bots, not by maintainers. Because of this lack of maintenance, no release
has been made since Jan 15, 2021 even though bugfixes (like one for the above
bug) have been merged into it's develop branch.

The combination of these things led us to fork the original typedi with the
intention of reverting back to the original once it has received a new release.

## Contributing

Please read our [contributing guidelines](./CONTRIBUTING.md) to get started.
