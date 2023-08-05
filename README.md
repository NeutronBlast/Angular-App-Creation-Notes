# Angular App Template


## What is this?

Just my way to structure Angular applications, making this document just to remember how to do it next time.

## Folder structure (Nebular)

```
Angular Project/
|-- src/
|   |-- app/
|   |   |-- app-routing/
|   |   |   |-- app-routing.module.ts
|   |   |   |-- routes.ts
|   
|   |   |-- base/
|   |   |   |-- first/
|   |   |   |   |-- first.component.html
|   |   |   |   |-- first.component.ts
|  
|   |   |   |-- base.module.ts
|   |   |   |-- base-routing.module.ts
|   
|   |   |-- core/
|   |   |   |-- services/
|   |   |   |   |-- process-http-message.service.ts
|   |   |   |   |-- process-http-message.service.spec.ts
|   |   |   |-- classes/
|   |   |   |-- constants/
|   |   |   |-- functions/
|   
|   |   |   |-- core.module.ts
|   
|   |   |-- shared/
|   |   |   |-- shared.module.ts
|
|   |   |   |-- nebular/
|   |   |   |   |-- nebular.module.ts
|
|   |   |-- app.component.ts
|   |   |-- app.component.css
|   |   |-- app.component.html
|   |   |-- app.module.ts
|   |-- assets/
|   
|-- .gitattributes
|-- .gitignore
|-- angular.json
|-- package.json
|-- package-lock.json
|-- README.md
|-- tsconfig.app.json
|-- tsconfig.json
|-- tsconfig.spec.json
```

## IDEs
I use IntelliJ to develop in Angular so all the instructions will be based on IntelliJ

## Installation
1. Run `npm install`
2. On `app-routing.module.ts` the code should look like this:
```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { CommonModule } from "@angular/common";

import { routes } from './routes';

@NgModule({
  imports: [CommonModule, RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```
3. On `routes.ts` the code should look like this:
```typescript
import { Routes } from '@angular/router';

export const routes: Routes = [
  {
    path: '',
    loadChildren: () => import('').then(b => b.BaseModule)
  }
];

```
4. On `core.module.ts` the code should look like this:
```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { HttpClientModule } from "@angular/common/http";

@NgModule({
    declarations: [],
    imports: [
        CommonModule,
        HttpClientModule
    ]
})
export class CoreModule { }

```
5. On `base.module.ts` the code should look like this:
```typescript
import { CUSTOM_ELEMENTS_SCHEMA, NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FirstComponent } from "./first/first.component";
import { BaseRoutingModule } from "./base-routing.module";
import { SharedModule } from "../shared/shared.module";

@NgModule({
  declarations: [
    FirstComponent
  ],
  imports: [
    CommonModule,
    SharedModule,
    BaseRoutingModule
  ],
  schemas: [CUSTOM_ELEMENTS_SCHEMA]
})
export class BaseModule { }

```
6. On `base-routing.module.ts` the code should look like this:
```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from "@angular/router";
import { EnhancedFormComponent } from "./first/first.component";

const routes: Routes = [
  {
    path: '',
    component: FirstComponent
  },
]

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class BaseRoutingModule { }

```
7. Install nebular
```shell
ng add @nebular/theme
```
8. Use default theme, enable customizable scss themes and set up browser animations
9. On `shared.module.ts` the code should look like this:
```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule, ReactiveFormsModule } from "@angular/forms";
import { NebularModule } from "./nebular/nebular.module";
import { NbLayoutModule, NbThemeModule } from "@nebular/theme";
import { NbEvaIconsModule } from "@nebular/eva-icons";

@NgModule({
  declarations: [],
  imports: [
    CommonModule,
    FormsModule,
    ReactiveFormsModule,
    NbLayoutModule,
    NbEvaIconsModule,
    NebularModule
  ],
  exports: [
    FormsModule,
    ReactiveFormsModule,
    NbThemeModule,
    NbLayoutModule,
    NbEvaIconsModule,
    NebularModule
  ]
})
export class SharedModule { }

```
10. If you use nebular, then `nebular.module.ts` should look like this:
```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { NbCardModule } from "@nebular/theme";

const NEBULAR_MODULES = [
  CommonModule,
  NbCardModule
]

@NgModule({
  declarations: [],
  imports: [
    ...NEBULAR_MODULES
  ],
  exports: [
    ...NEBULAR_MODULES
  ]
})
export class NebularModule { }

```
11. `app.component.html` should look like this:
```html
<router-outlet></router-outlet>
```
12. `index.html` should look like this:
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>Title</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body class="nb-theme-default">
  <app-root></app-root>
</body>
</html>

```

## Libraries
1. [Nebular](https://akveo.github.io/nebular/)
