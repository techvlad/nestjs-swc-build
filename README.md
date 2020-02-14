# SWC Compiler issue with NestJS

Cannot run application after compiling via swc

## Using `nest` cli build

```bash
npm run build && node dist/main.js
```

```
➜ npm run build && node dist/main.js

> nestjs-swc-build@0.0.1 prebuild /home/hex/Sandbox/nestjs-swc-build
> rimraf dist


> nestjs-swc-build@0.0.1 build /home/hex/Sandbox/nestjs-swc-build
> nest build

[Nest] 21981   - 02/14/2020, 5:22:37 PM   [NestFactory] Starting Nest application...
[Nest] 21981   - 02/14/2020, 5:22:37 PM   [InstanceLoader] AppModule dependencies initialized +10ms
[Nest] 21981   - 02/14/2020, 5:22:37 PM   [RoutesResolver] AppController {/}: +3ms
[Nest] 21981   - 02/14/2020, 5:22:37 PM   [RouterExplorer] Mapped {/, GET} route +2ms
[Nest] 21981   - 02/14/2020, 5:22:37 PM   [NestApplication] Nest application successfully started +1ms
```

```
➜ curl localhost:3000
Hello World!%
```

## Compile using `tsc`

```bash
npx tsc && node dist/src/main.js
```

```
➜ npx tsc && node dist/src/main.js
[Nest] 23007   - 02/14/2020, 5:25:46 PM   [NestFactory] Starting Nest application...
[Nest] 23007   - 02/14/2020, 5:25:46 PM   [InstanceLoader] AppModule dependencies initialized +8ms
[Nest] 23007   - 02/14/2020, 5:25:46 PM   [RoutesResolver] AppController {/}: +3ms
[Nest] 23007   - 02/14/2020, 5:25:46 PM   [RouterExplorer] Mapped {/, GET} route +2ms
[Nest] 23007   - 02/14/2020, 5:25:46 PM   [NestApplication] Nest application successfully started +2ms
```

```
➜ curl localhost:3000
Hello World!%
```

## Compile using `swc`

```bash
npx swc src -s -d ./dist && node dist/main.js
```

```
➜ npx swc src -s -d ./dist && node dist/main.js
Successfully compiled 5 files with swc.
[Nest] 23731   - 02/14/2020, 5:27:26 PM   [NestFactory] Starting Nest application...
[Nest] 23731   - 02/14/2020, 5:27:26 PM   [ExceptionHandler] Nest cannot create the module instance. Often, this is because of a circular dependency between modules. Use forwardRef() to avoid it.

(Read more: https://docs.nestjs.com/fundamentals/circular-dependency)
Scope []
 +5ms
Error: Nest cannot create the module instance. Often, this is because of a circular dependency between modules. Use forwardRef() to avoid it.

(Read more: https://docs.nestjs.com/fundamentals/circular-dependency)
Scope []

    at NestContainer.addModule (/home/hex/Sandbox/nestjs-swc-build/node_modules/@nestjs/core/injector/container.js:42:19)
    at DependenciesScanner.insertModule (/home/hex/Sandbox/nestjs-swc-build/node_modules/@nestjs/core/scanner.js:50:31)
    at DependenciesScanner.scanForModules (/home/hex/Sandbox/nestjs-swc-build/node_modules/@nestjs/core/scanner.js:27:43)
    at DependenciesScanner.scan (/home/hex/Sandbox/nestjs-swc-build/node_modules/@nestjs/core/scanner.js:21:20)
    at processTicksAndRejections (internal/process/task_queues.js:94:5)
    at async /home/hex/Sandbox/nestjs-swc-build/node_modules/@nestjs/core/nest-factory.js:80:17
    at async Function.asyncRun (/home/hex/Sandbox/nestjs-swc-build/node_modules/@nestjs/core/errors/exceptions-zone.js:17:13)
    at async NestFactoryStatic.initialize (/home/hex/Sandbox/nestjs-swc-build/node_modules/@nestjs/core/nest-factory.js:79:13)
    at async NestFactoryStatic.create (/home/hex/Sandbox/nestjs-swc-build/node_modules/@nestjs/core/nest-factory.js:30:9)
    at async bootstrap (/home/hex/Sandbox/nestjs-swc-build/dist/main.js:5:17)`
```

```
➜ curl localhost:3000
curl: (7) Failed to connect to localhost port 3000: Connection refused
```
