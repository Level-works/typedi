# Usage with TypeORM and routing-controllers

To use TypeDI with routing-controllers and/or TypeORM, it's required to configure them to use the top-level
TypeDI container used by your application.

```ts
import { useContainer as rcUseContainer } from 'routing-controllers';
import { useContainer as typeOrmUseContainer } from 'typeorm';
import { Container } from '@levelworks/typedi';

rcUseContainer(Container);
typeOrmUseContainer(Container);
```
