# Angular 實戰

### 目錄
* [初識 Angular 與 TypeScript](#初識 Angular 與 TypeScript)
* [環境配置](#環境配置)
* ----- 學習 TypeScript 程式設計 -----
* [型別](#型別)
* [命名空間與模組](#命名空間與模組)
* [模組機制](#模組機制)
* [介面](#介面)
* [函式](#函式)
* [類別](#類別)
* [型別兼容性](#型別兼容性)
* [通用型別](#通用型別)
* [後設資料](#後設資料)
* [泛型](#泛型)
* [型別斷言](#型別斷言)
* [象徵](#象徵)
* [冪運算子](#冪運算子)
* [混入](#混入)
* [合併宣告](#合併宣告)
* [修飾器](#修飾器)
* ----- 學習 Angular 開發 -----
* [元件](#元件)
* [指令](#指令)
* [服務](#服務)
* [管道](#管道)
* ----- 學習 Angular 測試 -----
* [靜態分析](#靜態分析)
* [單元測試](#單元測試)
* [端對端測試](#端對端測試)
* [持續整合](#持續整合)
* ----- 案例開發 -----
* [簡單的應用程式](#簡單的應用程式)
* ----- 附錄 -----
* [參考資料](#參考資料)

***

### 環境配置
* [使用 Angular CLI](https://github.com/angular/angular-cli)
* [使用 Gulp](https://github.com/mgechev/angular2-seed)
* [使用 Webpack](https://github.com/AngularClass/angular2-webpack-starter)

### 型別
```ts
// 布林值
let isDone: boolean = false;
```
```ts
// 數值
let age: number = 18;  // 十進制
```
```ts
// 字串
let myName: string = 'Hale';
// 模板字串
let sentence: string = `My name is ${myName}.`;  // My name is Hale.
```
```ts
// 陣列
let list: number[] = [1, 2, 3];
let list2: string[] = ['a', 'b', 'c'];
// or
let list3: Array<number> = [3, 2, 1];
let list4: Array<string> = ['x', 'y', 'z'];
```
```ts
// 元組
let foo: [number, string];  // 宣告一個元組型別
foo = [123, 'abc'];  // 將 foo 初始化
```
```ts
// 列舉
enum Thing {
  Foo, Bar, Baz
};

let foo: Thing = Thing.Foo;  // 0
let bar: Thing = Thing.Bar;  // 1
let baz: Thing = Thing.Baz;  // 2

enum Thing2 {
  Up = 4,
  Down,
  Left,
  Right
};

let up: Thing2 = Thing2.Up;  // 4
let down: Thing2 = Thing2.Down;  // 5
let left: Thing2 = Thing2.Left;  // 6
let right: Thing2 = Thing2.Right;  // 7

// 使用 const 宣告
const enum Thing3 (
  // ...
)
```
```ts
// 任意值
let notSure: any = 123;
notSure = 'abc';
notSure = 'true';
```
```ts
// 空值
let unusable: void = undefined;
let unusable2: void = null;

function foo(thing: number): void {
  this.thing = thing;
}
```
```ts
// 型別斷言
let foo: any = 'abc';
let bar = <string>foo;  // 語法: <>
let baz: number = bar.length;  // 3
// or
let bar2 = foo as string;  // 語法: as
let baz2: number = bar2.length;  // 3
```
```ts
// 型別併集
let foo: string | number;

foo = 'abc';  // OK
foo = 123;  // OK
```
```ts
// 型別別名
type ThingType = string | number | boolean;
let foo: ThingType;

foo = 'abc';  // OK
foo = 123;  // OK
foo = true;  // OK
```

### 命名空間與模組
```ts
namespace Thing {
  export let prefix: string = 'ng-';
  export interface Foo { }
  export function bar() {  }
  export class Baz { }
}
```

```ts
// thing.d.ts
declare module 'thing-module' {
  export function fn(): void;
}
```
```ts
// module.ts
/// <reference path="thing.d.ts" />
import * as thing from 'thing-module';
```
##### 使用 Typings
```
$ npm i typings -g
```
```bash
$ npm i core-js -S
$ typings i core-js -G -S
```
```bash
# 自訂
$ mkdir manual_typings
```
```ts
// systemjs-builder.d.ts
declare module 'systemjs-builder' {
  class Builder {
    constructor(configObject?: any, baseUrl?: string, configPath?: string);
    bundle(source: string, target: string, options?: any): Promise<any>;
    buildStatic(source: string, target: string, options?: any): Promise<any>;
  }

  module Builder { }
  export = Builder;
}
```
```ts
// module.ts
import * as Builder from 'systemjs-builder';
```

### 模組機制
```ts
// foo.ts
// 導出介面
export interface Foo {
  // ...
}

// 導出變數
export const numberRegexp = /^[0-9]+$/;
```
```ts
// bar.ts
import { Foo } from './foo';

export class Bar {
  // ...
}
```
```ts
// 預設導出
export default thing;
```

### 介面
```ts
interface Foo {
  bar: number;
  baz?: string;  // 可選屬性
}

function thing(foo: Foo) {
  let bar = foo.bar;
  return bar;
}

thing({ bar: 123 });  // OK
thing({ baz: 'abc' });  // Error
thing({ bar: 123, baz: 'abc' });  // OK
```
```ts
interface Thing {
  [index: number]: string;
}

let thing: Thing = ['a', 'b', 'c'];

let foo: string = thing[1];  // 'b'
```

### 函式
```ts
// 設定函式型別
function addition(a: number, b: number): number {
  return a + b;
}

addition(1, 1);  // 2
addition('1', '1');  // Error
```
```ts
// 匿名函式
const addition = function(a: number, b: number): number {
  return a + b;
};

addition(1, 1);  // 2
addition('1', '1');  // Error
```
```ts
// 可選參數
const ng = function(a: string, b: string, c?: string): string {
  return `${a} ${b} ${c}`;
};

ng('Angular', 'Material', 'Firebase');  // Angular Material Firebase
ng('Angular', 'Material');  // Angular Material undefined
ng('Angular');  // Error
```
```ts
// 預設參數
const ng = function(a: string, b: string = 'Angular 2'): string {
  return `${a} and ${b}`;
};

ng('Angular');  // Angular and Angular 2
ng('Angular', 'Material');  // Angular and Material
```

### 類別
```ts
class Foo {
  bar: string;
  constructor() {
    // ...
  }
  baz() {
    // ...
  }
}
```
```ts
// 類別的繼承
class Foo {
  constructor() {
    // ...
  }
}

class Bar extends Foo {
  constructor() {
    super();
    // ...
  }
}
```
```ts
// 修飾字元
class Thing {
  public foo: string;  // 是 foo: string
  private bar: string;
  protected baz: string;
  constructor() {
    // ...
  }
}
```
```ts
class Name {
  private name: string;
  constructor(private theName: 'string') {
    this.name = theName;
  }
}

new Name('Hale').name;  // Error: 'name' is private
```
```ts
class Adder {
  constructor(a: string) { }  // 是 public a: string

  add = (b: string): string => {
    return this.a + b;
  }
}
```
```ts
// 將類別當作介面使用
class Point {
  x: number;
  y: number;
}

interface Point3d extends Point {
  z: number;
}

let point3d: Point3d = {
  x: 60,
  y: 120,
  z: 180
};
```

### 型別兼容性
```ts
interface Foo {
  bar: string;
}

class Thing {
  // ...
}

let thing: Foo;
// 結構性的型別
thing = new Thing();
```

### 通用型別
```ts
const ng: Ng[] = [new Angular(), new Material(), new Firebase()];
```

### 後設資料
```bash
$ npm i reflect-metadata -S
```
```json
{
  "compilerOptions": {
    "target": "es5",
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  }
}
```

### 泛型
```ts
function identity<T>(arg: T): T {
  return arg;
}

identity(123);  // 123
identity('abc');  // 'abc'
identity(true);  // true
```

### 型別斷言
```ts
interface Foo {
  bar: number;
  baz: string;
}

let foo = {} as Foo;
foo.bar = 123;
foo.baz = 'abc';

foo;  // { bar: 123, baz: 'abc' }
```
```ts
interface Foo {
  bar: number;
  baz: string;
}

let foo = <Foo>{};
foo.bar = 123;
foo.baz = 'abc';

foo;  // { bar: 123, baz: 'abc' }
```
```ts
interface Foo {
  bar: number;
  baz: string;
  ts: string;
}

let foo = <Foo>{
  bar: 123,
  baz: 'abc'
};
foo.ts = 'TypeScript';

foo;  // { bar: 123, baz: 'abc', ts: 'TypeScript' }
```
```ts
interface Foo {
  bar: number;
  baz: string;
}

let foo: Foo = {
  bar: 123,
  baz: 'abc'
};

foo;  // { bar: 123, baz: 'abc' }
```

### 象徵
```ts
interface Iterable {
  [Symbol.iterator](): Iterator;
}

interface Iterator {
  next(value?: any): IterationResult;
}

interface IterationResult {
  value: any;
  done: boolean;
}
```

### 冪運算子
```ts
let x = 2 ** 5;  // Math.pow(2, 5)
```

### 混入
```ts
class Disposable {
  isDisposed: boolean;
  dispose() {
    this.isDisposed = true;
  }
}

class Activatable {
  isActive: boolean;
  activate() {
    this.isActive = true;
  }
  deactivate() {
    this.isActive = false;
  }
}

class SmartObject implements Disposable, Activatable { }
```

### 合併宣告
```ts
// 合併介面
interface Box {
  height: number;
  width: number;
}

interface Box {
  scale: number;
}

const box: Box = { height: 5, width: 6, scale: 10 };
```

### 修飾器
##### 修飾屬性
```ts
function thing(value: string) {  // 修飾器工廠
  return function (target) {  // 修飾器
    // 一些 target 和 value 的操作
  }
}
```

##### 修飾類別
```ts
function thing(value: string) {  // 修飾器工廠
  return (target) => {  // 修飾器
    // 一些 target 和 value 的操作
  }
}
```

##### 修飾參數
```ts
function thing(target: any, key: string, index: number) {
  // 一些 target 和參數的操作
}
```

### 元件
```ts
import { Component } from '@angular/core';

/**
 * 建構子
 *
 * selector?: string,
 * inputs?: string[],  // 不建議使用
 * outputs?: string[],  // 不建議使用
 * properties?: string[],
 * events?: string[],
 * host?: {[key: string]: string},  // 不建議使用
 * providers?: any[],
 * exportAs?: string,
 * moduleId?: string,
 * viewProviders?: any[],
 * queries?: {[key: string]: any},
 * changeDetection?: ChangeDetectionStrategy,
 * templateUrl?: string,
 * template?: string,
 * styleUrls?: string[],
 * styles?: string[],
 * directives?: Array<Type | any[]>,
 * pipes?: Array<Type | any[]>,
 * encapsulation?: ViewEncapsulation
 */
@Component({
  // 一些組態在這裡
})
export class AtThingComponent {
  // 一些程式碼在這裡
}
```

```ts
import { Component } from '@angular/core';

/**
 * 常用的組態
 */
@Component({
  moduleId: module.id,
  selector: 'at-thing',
  templateUrl: 'thing.component.html',
  styleUrls: ['thing.component.css']
  // 其它更多的組態
})
export class AtThingComponent {
  // 一些程式碼在這裡
}
```

```ts
// basic-app.ts
import { Component } from '@angular/core';

@Component({
  selector: 'basic-app',
  template: `
    <p>1 + 1 的結果是: {{ 1 + 1 }}</p>
    <a href="{{ link }}">網站連結</a>
  `
})
export class BasicAppComponent {
  public link: string = 'https://angular.io/';
}
```

```ts
// my-name.ts
import { Component } from '@angular/core';

@Component({
  selector: 'my-name',
  template: `
    <p>我的姓名是: {{ myName }}</p>
  `
})
export class MyNameComponent {
  public myName: string = '陳彥澄'; 
}
```

```ts
// hello-world.ts
import { Component } from '@angular/core';

@Component({
  selector: 'hello-world',
  template: `
    <input type="text" [(ngModel)]="name" placeholder="輸入你的名字">
    <p>Hello {{ name }}</p>
  `
})
export class HelloWorldComponent {
  public name: string = '';
}
```

```ts
// click-me.ts
import { Component } from '@angular/core';

@Component({
  selector: 'click-me',
  template: `
    <button (click)="onClick()">點擊我</button>
    <p>{{ message }}</p>
  `
})
export class ClickMeComponent {
  public message: string = '我是點擊「前」的訊息';

  onClick(): string {
    this.message = '我是點擊「後」的訊息';
  }
}
```

```ts
// toggle-me.ts
import { Component } from '@angular/core';

@Component({
  selector: 'toggle-me',
  template: `
    <button (click)="onToggle()">點擊我 (切換內容)</button>
    <p>{{ message }}</p>
  `
})
export class ToggleMeComponent {
  public message: string = '你好';
  public toggle: boolean = true;

  onToggle() {
    this.toggle = !this.toggle;
    this.toggle ? this.message = '你好' : this.message = '再見';
  }
}
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'toggle-class',
  template: `
    <button (click)="isClassVisible = !isClassVisible">Toggle Class</button>
    <p [ngClass]="{ 'my-class': isClassVisible }">Hello Angular 2</p>
  `,
  styles: [`
    .my-class {
      color: #F44336
    }
  `]
})
export class ToggleClassComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'key-up',
  template: `
    <input #new="" (keyup)="onKeyup(new.value)">
    <p>{{ values }}</p>
  `
})
export class KeyUpComponent {
  public valuse: string = '';

  onKeyup(value: string): string {
     this.values += `${ value } | `;
  }
}
```

```ts
// add-item.ts
import { Component } from '@angular/core';

@Component({
  selector: 'add-item',
  template: `
    <input
      #newItem=""
      (keyup.enter)="addItem(newItem.value); newItem.value=''"
      (keyup)="values = newItem.value"
    >
    <p>{{ values }}</p>
    <button (click)="addItem(newItem.value); newItem.value=''; values=''">新增</button>
    <ul>
      <li *ngFor="let item of list">{{ item }}</li>
    </ul>
  `
})
export class AddItemComponent {
  public list: string[] = ['Angular', 'Material', 'Firebase'];

  addItem(newItem: string) {
    if (newItem) {
      this.list.push(newItem);
    }
  }
}
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'at-properties',
  template: `
    <p>Hello Angular {{ atVersion }}</p>
  `,
  properties: ['atVersion']
})
export class AtPropertiesComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'encapsulation-emulated',
  template: `
  `,
  styles: [`
  `],
  encapsulation: ViewEncapsulation.Emulated
})
export class NgClassComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'encapsulation-native',
  template: `
  `,
  styles: [`
  `],
  encapsulation: ViewEncapsulation.Native
})
export class NgClassComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'encapsulation-none',
  template: `
  `,
  styles: [`
  `],
  encapsulation: ViewEncapsulation.None
})
export class NgClassComponent { }
```

##### 表單
```ts
import { Component } from '@angular/core';
import { FORM_DIRECTIVES } from '@angular/common';

@Component({
  selector: 'at-form',
  template: `
    <form [ngFormModel]="group" (ngSubmit)="onSubmit()" novalidate>
      <label for="email">Email:</label>
      <input type="email" id="email" [ngFormControl]="email">

      <label for="password">Password:</label>
      <input type="password" id="password" [ngFormControl]="password">

      <button type="submit">Register</button>
    </form>

    <pre>{{ formValue | json }}</pre>
  `,
  directives: [FORM_DIRECTIVES]
})
export class AtFormComponent {
  public email: Control;
  public password: Control;
  public group: ControlGroup;
  public formValue: any;
  
  constructor(formBuilder: FormBuilder) {
    this.email = new Control();
    this.password = new Control();
    
    this.group = formBuilder.group({
      email: this.email,
      password: this.password
    });
  }
  
  onSubmit() {
    this.formValue = this.group.value;
  }
}
```

##### 元件之間的溝通
```ts
import { Component, Input } from '@angular/core';

@Component({
  selector: 'at-input',
  template: `
    <p>Hello {{ something }}</p>
  `
})
export class AtInputComponent {
  @Input('atSomething') something: string;
}
```

```ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'at-counter',
  template: `
    <button (click)="onClick()">Increment</button>
    <p>Count: {{ count }}</p>
  `
})
export class AtCounterComponent {
  @Input('atCount') count: number = 0;
  @Output('atCountChange') countChange: EventEmitter<number> = new EventEmitter<number>();

  onClick() {
    this.count++;
    this.countChange.emit(this.count);
  }
}
```

```ts
@ContentChild()
@ContentChildren()
@ViewChild()
@ViewChildren()
```

##### 生命週期掛鉤
```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'at-lifecycle'
})
export class AtLifecycleComponent implements OnInit {
  ngOnInit(): void {
    console.log('Hello Angular 2');
  }
}
```

```ts
ngDoCheck() { ... }

ngAfterContentInit() { ... }
ngAfterContentChecked() { ... }
ngAfterViewInit() { ... }
ngAfterViewChecked() { ... }
```

##### 路由
```ts
import { APP_BASE_HREF } from '@angular/common';
import { provide } from '@angular/core';

// ...

bootstrap(App, [
  // ...
  provide(APP_BASE_HREF, { useValue: '/' }),
  // ...
]);
```
```ts
import { Component } from '@angular/core';
import { ROUTER_DIRECTIVES, Routes } from '@angular/router';

import { HomeComponent } from './home';
import { AboutComponent } from './about';

@Component({
  selector: 'app',
  template: `
    <nav>
      <a [routerLink]="['/']">Home</a> /
      <a [routerLink]="['/about']">About</a>
    </nav>
    <router-outlet></router-outlet>
  `,
  directives: [
    ROUTER_DIRECTIVES,
    HomeComponent,
    AboutComponent
  ]
})
@Routes([{
    path: '/',
    component: HomeComponent,
    useAsDefault: true
  }, {
    path: '/about',
    component: AboutComponent
}])
export class App { }
```

### 指令
##### 內建指令
```ts
// see-things.ts
import { Component } from '@angular/core';

@Component({
  selector: 'see-things',
  template: `
    <p *ngIf="true">我看的到它</p>
    <p *ngIf="false">我看不到它</p>
  `
})
export class SeeThingsComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'ng-switch',
  template: `
    <div [ngSwitch]="language">
      <p *ngSwitchWhen="'JavaScript'">Angular 2 in JavaScript</p>
      <p *ngSwitchWhen="'CoffeeScript'">Angular 2 in CoffeeScript</p>
      <p *ngSwitchWhen="'TypeScript'">Angular 2 in TypeScript</p>
      <p *ngSwitchDefault>Something Else</p>
    </div>
  `
})
export class NgSwitchComponent {
  public language: string = 'TypeScript';
}
```

```ts
import { Component } from '@angular/core';

interface List {
  label: string;
}

@Component({
  selector: 'ng-for',
  template: `
    <p>Technologies:</p>
    <ul>
      <li *ngFor="let item of list; let i = index">
        ({{ i + 1 }}) {{ item.label }}
      </li>
    </ul>
  `
})
export class NgForComponent {
  public list: List[] = [
    { label: 'ECMAScript' },
    { label: 'HTML5' },
    { label: 'Node.js' }
  ];
}
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'ng-style',
  template: `
    <!-- 模板表達式 -->
    <p [style.background-color]="'yellow'">
      我的背景是黃色的
    </p>

    <!-- 內建指令 -->
    <p [ngStyle]="{ 'background-color': 'yellow' }"> 
      我的背景也是黃色的
    </p>
  `
})
export class NgStyleComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'ng-class',
  template: `
    <p [ngClass]="{ 'at-color': true }">Angular 2</p>
    <p [ngClass]="{ 'at-color': false }">TypeScript</p>
  `,
  styles: [`
    .at-color {
      color: #F44336
    }
  `]
})
export class NgClassComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'content-projection',
  template: `
    <p>Hi, TypeScript</p>
    <ng-content></ng-content>
  `
})
export class ContentProjectionComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'more-content',
  template: `
    <ng-content select="[js]"></ng-content>
    <p>Angular 1</p>
    <ng-content select="[coffee]"></ng-content>
    <p>Angular 2</p>
    <ng-content select="[ts]"></ng-content>
  `
})
export class MoreContentComponent { }
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'ng-non-bindable',
  template: `
    <p>Hello {{ content }}</p>
    <p ngNonBindable>Hello {{ content }}</p>
  `
})
export class NgNonBindableComponent {
  public content: string = 'Angular 2';
}
```

##### 自訂指令
```ts
import { Directive } from '@angular/core';

@Directive({
  /**
   * at-thing
   * [atThing]
   * .at-thing
   * input[type=text]
   */
  selector: ''
})
export class AtThingDirective { }
```

```ts
import { Directive, ElementRef } from '@angular/core';

@Directive({
  selector: '[atColor]'
})
export class AtColorDirective {
  constructor(private element: ElementRef) {
    element.nativeElement.style.color = '#F44336';
  }
}
```

```ts
import { Directive, HostBinding } from '@angular/core';

@Directive({
  selector: '[at-title]'
})
export class TitleDirective {
  public useTitle: boolean = true;

  @HostBinding('[class.title]')
  get title {
    return this.useTitle;
  }
}
```

```ts
import { Directive, Input, ElementRef, HostListener } from '@angular/core';

@Directive({
  selector: '[atHighlight]'
})
export class HighlightDirective {
  @Input('atHighlight') highlightColor: string;

  private defaultColor: string = 'yellow';

  constructor(private element: ElementRef) { }

  @HostListener('mouseenter', ['$event.target'])
  onMouseEnter() {
    this.highlight(this.highlightColor || this.defaultColor);
  }

  @HostListener('mouseleave', ['$event.target'])
  onMouseLeave() {
    this.highlight(null);
  }

  private highlight(color: string) {
    this.element.nativeElement.style.backgroundColor = color;
  }
}
```
```html
<form>
  <input type="radio" name="colors" (click)="color='#F44336'">紅色
  <input type="radio" name="colors" (click)="color='#4CAF50'">綠色
  <input type="radio" name="colors" (click)="color='#2196F3'">藍色
</form>
<span [atHighlight]="color">滑鼠游標靠過來吧!</span>
```

### 服務
```ts
// languages.ts
import { Injectable } from '@angular/core';

@Injectable()
export class LanguagesService {
  public js: string = 'JavaScript';
  public coffee: string = 'CoffeeScript';
  public ts: string = 'TypeScript';
}
```
```ts
// app.ts
import { Component } from '@angular/core';

import { LanguagesService } from './services/languages';

@Component({
  selector: 'app',
  template: `
    <h3 class="title">Languages Service</h3>
    <div class="content">
      <p>Decided Language: {{ language }}</p>
    </div>
  `,
  viewProviders: [
    LanguagesService
  ]
})
export class App {
  public language: string = '';

  constructor(private languages: LanguagesService) {
    this.language = languages.ts;
  }
}

// or

import { Component, Inject } from '@angular/core';

import { LanguagesService } from './services/languages';

@Component({
  selector: 'app',
  template: `
    <h3 class="title">Languages Service</h3>
    <div class="content">
      <p>Decided Language: {{ language }}</p>
    </div>
  `,
  viewProviders: [
    LanguagesService
  ]
})
export class App {
  public language: string = '';

  constructor(@Inject(LanguagesService) private languages) {  // 不推薦
    this.language = languages.ts;
  }
}
```

```js
// data.json
{
  "title": "Angular2-in-Action",
  "description": "Angular 2 實戰"
}
```
```ts
import { Component, ChangeDetectorRef } from '@angular/core';
import { Http } from '@angular/http';

@Component({
  selector: 'get-data',
  template: `
    <pre>{{ response }}</pre>
  `
})
export class GetDataComponent {
  constructor(private http: Http, private changeDetectorRef: ChangeDetectorRef) {
    http
      .get('./assets/data.json')
      .subscribe((data) => {
        this.response = data._body;
        changeDetectorRef.detectChanges();
      });
  }
}
```

```ts
import { Component } from '@angular/core';
import { Http, Response } from '@angular/http';

@Component({
  selector: 'on-request',
  template: `
    <button type="button" (click)="onRequest()">請求</button>
    <pre>{{ response | json }}</pre>
  `
})
export class OnRequestComponent {
  public response: Object;

  constructor(private http: Http) { }

  onRequest() {
    this.http
      .request('./assets/data.json')  // or .get('./assets/data.json')
      .subscribe((res: Response) => {
        this.response = res.json();
      });
  }
}
```
```ts
import { Injectable } from '@angular/core';
import { Http, Request, RequestMethod } from '@angular/http';

@Injectable()
export class OnRequestService {
  constructor(private http: Http) { }

  onRequest(url: string) {
    return this.http
      .request(new Request({
        method: RequestMethod.Get,
        url: url
      }));
  }
}
```

```ts
// class Http
request(url: string | Request, options?: RequestOptionsArgs) : Observable<Response>
get(url: string, options?: RequestOptionsArgs) : Observable<Response>
post(url: string, body: string, options?: RequestOptionsArgs) : Observable<Response>
put(url: string, body: string, options?: RequestOptionsArgs) : Observable<Response>
delete(url: string, options?: RequestOptionsArgs) : Observable<Response>
patch(url: string, body: string, options?: RequestOptionsArgs) : Observable<Response>
head(url: string, options?: RequestOptionsArgs) : Observable<Response>
```

```ts
import{ Http, Response, RequestOptions, Headers } from'@angular/http';
```

```ts
import { Injectable } from '@angular/core';
import { Http } from '@angular/http';
import 'rxjs/add/operator/map';

@Injectable()
export class PostService {
  constructor(private http: Http) { }

  getPosts() {
    return this.http
      .get('./posts.json')
      .map(res => res.json())
      .map(res => res.posts);
  }
}
```

```ts
import { Injectable } from '@angular/core';
import { Jsonp, URLSearchParams } from '@angular/http';
import 'rxjs/add/operator/map';

@Injectable()
export class WikipediaService {
  constructor(private jsonp: Jsonp) { }

  search(term: string) {
    let wikiUrl = 'http://en.wikipedia.org/w/api.php';

    let params = new URLSearchParams();
    params.set('search', term);
    params.set('action', 'opensearch');
    params.set('format', 'json');
    params.set('callback', 'JSONP_CALLBACK');

    return this.jsonp
      .get(wikiUrl, { search: params })
      .map(request => <string[]>request.json()[1]);
  }
}
```

### 管道
##### 內建管道
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'at-pipes',
  template: `
    <p>{{ thing | uppercase }}</p>
    <p>{{ thing | lowercase }}</p>
    <p>{{ thing | uppercase | lowercase }}</p>  <!-- 先 uppercase 再來 lowercase -->
  `
})
export class AtPipesComponent {
  public thing = 'Angular';
}
```
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'at-date',
  template: `
    <p>{{ atDate | date: "MM/dd" }}</p>
  `
})
export class AtDateComponent {
  public atDate = new Date(2020, 2, 14);
}
```

##### 自訂管道
```ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'length'
})
export class MessageLengthPipe implements PipeTransform {
  transform(value: string, args: string[]): any {
    return `${value.length}`
  }
}
```

### 參考資料
* TypeScript Handbook by TypeScript Team
* TypeScript Deep Dive by Basarat Ali Syed
* Mastering TypeScript by Nathan Rozentals
* Pro TypeScript by Steve Fenton
* Angular 2 Developer Guides by Angular Team
* Introduction to Angular 2 and ngCourse2 by Rangle.io
* ng-book 2 by Ari Lerner, Felipe Coury, Nate Murray and Carlos Taborda
* Switching to Angular 2 by Minko Gechev
