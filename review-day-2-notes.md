# Concepts

### Directives
- A directive is how we give instructions to the DOM to control certain elements in Angular

### Attribute Directives
- An attribute directive is what we use to change the behavior or appearance of elements
- Built-in Attribute Directives include ngClass, ngStyle, ngModel

### Structrual Directives
- A structrual directive is what we use to change the DOM layout by adding, removing or altering elements
- Built-in Structural Directives include ngIf, ngFor, ngSwitch

### Services
- A service in the context of Angular is a centralized store where you can place code so multiple other components can use it.
- Services allow our app to have better "communication".
- This drastically reduces the complexity of the application state because we no longer need to pass a variable through two or more levels of folders using @Input() and @Output().

### Dependency Injection
- Dependency injection is when a class uses code from another class or service instead of writing it locally. You "inject" the code from one part of your app into another

### D.R.Y. Code
- D.R.Y. code stands for "Don't Repeat Yourself". This meta-programming philosophy advises you to abstract away any logic you use in multiple components to a shared place.

### Router Outlet
- The <router-outlet> tag is how we dynamically render the component we want based on the URL path.

### Router Link
- Every link needs to point to a route. The "routerLink" is used instead of an anchore tag to support the SPA methodology. The page will not refresh, even when you change routes!

### Asynchronous
- Asynchronous code is any piece of logic that does not execute right away because it needs to wait for something else to happen first. You can understand asynchronous code better by knowing how Javascript works under the hood.
- Javascript is a "Single-Threaded-Language", meaning that it can only execute one piece of code at a time. So when it runs into, let's say, an HTTP Request... it will be held up for 5-10 seconds! Waiting this long to respond would be a horrible user experience.
- So what happens is, the Javascript Evaluator says: "This might take a bit. I will put a note over here and insert myself when I finish this complex task". Javascript knows to do this when we write Asynchronous code.

### Observable
- An observable is an interface used to handle various everyday asynchronous or event operations. They provide support for passing messages between different sections of your application. Observables are a stream of data that you "subscribe" to receive info when that data changes.

### Observer
- An observer is a way to "subscribe" to observable events. Depending on where the observable is placed, you can write code to handle the data, handle the error and handle the completion

### Subjects
- Subjects are unique observables that act as both the "observer" and the "observable". Subjects allow us to emit new values to the subscription stream using the next() method.

### Template Driven Approach
- The template driven approach to forms is the more intuitive and simpler way to implement form functionality in Angular. This method infers the structure of the "form" object from the DOM.

### Reactive Driven Approach
- The reactive driven approach to forms is more explicit. This way of handling forms is more complicated, but you gain more fine-tuned control and flexibility.

### Pipes
- In angular, pipes are simple functions you can use in HTML template expressions that accept an initial value and return a transformed value.

---

# Classes

### Class 15 - Directives & Services - Angular
01. The difference between attribute & structural directives is that attribute changes the element itself (style and content), while structural changes it's layout (rendering multiple instances or whether it renders at all).
02. Attribute and structural directives are implemented inline in the HTML template. Square brackets [] are typically used for attribute directives while an asterisk * is used for structural.
    - ngStyle is used like [ngStyle]="{'background-color': 'red'}". It can also be used set a collection of styles in an object by using [ngStyle]="styleObj".
    - ngClass is used to add or remove classes from an element It is used like [ngClass]="isSomeBool ? 'className : ''". It can also be used with a javascript object like [ngClass]="someObj".
    - ngModel can be used to display a data property and update the property when changed. It is used like [(ngModel)]="object.name".
    - ngIf can control whether or which elements are shown conditionally. It is used like *ngIf="someBool".
    - ngFor can render multiple instances of elements, for example from arrays. It is used like *ngFor="let item of items". You can also get the index. *ngFor="let item of items; let index = i".
    - ngSwitch works sort of like ngIf instead is uses switch statements. It is used like [ngSwitch]="someObj.someProp" while the elements have *ngSwitchCase="propOne" *ngSwitchCase="propTwo".
03. Renderer2 is used to intercep rendering of the page or render something without touching the DOM directly. It is used with dependency injection in the constructor of your class.
04. You can use HostListener with the renderer to listen for events in custom directives to change things like element styles.
05. You build custom directives like other classes in angular. They require the @Directive decorator.
06. Services are also built like other classes. The most current way of providing them is to make them @Injectable and add providedIn: 'root'.
07. To use services in another class, they must be injected in the constructor. After that, the methods or variables inside can be accessed with this.serviceName.
08. As above, services must be injected in the class constructor like constructor(private someService: SomeService) {}

### Class 16 - Changing Pages with Routing - Angular
01. Routes are added in the app-routing.module in a Routes array. They are added like { path: 'pathname', component: SomeComponent }
02. Child routes are added by specifying them as an array of children of a path. Like { path: 'pathname', component: SomeComponent, children: [{ path: 'childPath', component: ChildComponent}] }
03. You configure route parameters by injecting ActivatedRoute and subscribing to its params. this.route.params.subscribe((params: Params) => { logic here })
04. You can pass dynamic parameters through links by utilitizing directives like ngFor passing its index to routerLink.
05. You can programmatically edit links by injecting the Router and using the navigate method. You can pass things like index or ids with it. And also append new strings. this.router.naviate(['../', this.id, 'edit'])

### Class 17 - Understanding Observables - Angular
01. Asynchronous code is code that is run non-concurrently with the rest of your app. It might be an HTTP request that needs time to come back.
02. An observable is something your components can subscribe to in order to be notified of things like changes or receiving data from an outside source.
03. You subscribe to observables with their subscribe methods. this.someObservable.subscribe(someData => { logic }). Built-in angular observables clean up after themselves, but any custom observables must be unsubscribed from in ngOnDestroy to prevent memory leaks.
04. RxJs operators are methods you can use on observables to manipulate the data received.
05. Map is an operator used to change the data from transmission. You call it in pipe and manipulate the data there. .pipe(map(data => data.id = this.id))
06. Pipe is used with observables to combine RxJs operators for async operations. You call things like map and filter in pipe to transform the data you receive.
07. A subject is an observable used to send data to other components in your app. They are subscribed to and can send data to subscriptions with the next() function.

### Class 18 - Handling Forms - Angular
01. The two ways of handling forms in angular are template driven and reactive driven.
02. Template driven, like the name implies, keeps all the form logic in the HTML template. Angular infers the component form from the HTML. Reactive driven creates the form in the component class and you assign FormControls in the HTML template to it.
03. You implement a Template approach by importing the FormsModule in your app.module. Your form is created in the template and attributes like ngModel and name let angular know where and what the controls are. You need to add a local reference for the form to be accessed in the component class.
04. An implementation for Reactive approach is started by importing the ReactiveFormsModule in app.module. You create a FormGroup and assign FormControls in it for the data you need. You add variables for formGroup to form in the HTML template and formControlName to the inputs. In both cases you need an ngSubmit method on the form to call a custom method to handle the form.

### Class 19 - Forms Course Project & Pipes - Angular
01. You implement a Template approach by importing the FormsModule in your app.module. Your form is created in the template and attributes like ngModel and name let angular know where and what the controls are. You need to add a local reference for the form to be accessed in the component class.
02. An implementation for Reactive approach is started by importing the ReactiveFormsModule in app.module. You create a FormGroup and assign FormControls in it for the data you need. You add variables for formGroup to form in the HTML template and formControlName to the inputs. In both cases you need an ngSubmit method on the form to call a custom method to handle the form.
03. You create a custom pipe like other classes. They require the @Pipe decorator and must implement PipeTransform. PipeTransform requires a transform method with a return in the class. You can add multiple arguments to the method that can be used as parameters with the pipe.