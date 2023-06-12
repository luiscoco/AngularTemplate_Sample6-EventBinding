# Angular_Event-Binding

In Angular, event binding is a way to capture and handle events triggered by user interactions or other sources, such as button clicks, form submissions, mouse movements, and keyboard inputs. It allows you to associate a specific event with a method or function in your component's class, so that when the event occurs, the corresponding method is executed.

Event binding is typically done using parentheses () around an event name followed by an equal sign (=) and the method or function you want to call. The event name is enclosed in quotes and represents the event you want to bind to. Here's an example of event binding in Angular:

```html
<!-- HTML template -->
<button (click)="handleClick()">Click me</button>
```

In the example above, the (click) event binding is used to bind the handleClick() method to the button's click event. When the button is clicked, the handleClick() method in the component's class will be executed.

Here's the corresponding TypeScript code in the component class:

```typescript
// Component class
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  templateUrl: './example.component.html',
  styleUrls: ['./example.component.css']
})
export class ExampleComponent {
  handleClick() {
    console.log('Button clicked!');
    // Perform additional actions or logic here
  }
}
```

In the component class, the handleClick() method is defined to handle the button click event. In this example, it simply logs a message to the console, but you can perform any additional actions or logic you need within the method.

You can bind to various other events in Angular using event binding, such as (mouseover), (keyup), (submit), etc. The syntax remains the same, where you enclose the event name in parentheses and assign a method or function to it.

Event binding in Angular allows you to create interactive and dynamic web applications by responding to user actions and updating the application state accordingly.


## Determining an event target

To determine an event target, Angular checks if the name of the target event matches an event property of a known directive.

Create the following example: (Angular checks to see if myClick is an event on the custom ClickDirective)

src/app/app.component.html
```html
<h4>myClick is an event on the custom ClickDirective:</h4>
<button type="button" (myClick)="clickMessage=$event" clickable>click with myClick</button>
{{clickMessage}}
```

If the target event name, myClick fails to match an output property of ClickDirective, Angular will instead bind to the myClick event on the underlying DOM element.

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  clickMessage: string;
}
```

```typescript
// click.directive.ts
import { Directive, EventEmitter, HostListener, Output } from '@angular/core';

@Directive({
  selector: '[clickable]'
})
export class ClickDirective {
  @Output() myClick: EventEmitter<string> = new EventEmitter();

  @HostListener('click', ['$event'])
  onClick(event: MouseEvent): void {
    this.myClick.emit('Button clicked!');
  }
}
```

Make sure to create these files in your Angular project, and the ClickDirective is correctly imported and added to the declarations array of your module.

## Binding to keyboard events

In Angular, binding to keyboard events refers to the process of capturing and handling keyboard-related events within your application. This allows you to respond to user keyboard input, such as key presses, key releases, or other keyboard actions. Angular provides a convenient way to bind these events and execute custom code based on the user's keyboard interactions.

To bind to keyboard events in Angular, you can use the (keydown), (keyup), or (keypress) event binding syntax. Here's an explanation of each event:

(keydown): This event is triggered when a key is pressed down.
(keyup): This event is triggered when a key is released.
(keypress): This event is triggered when a key is pressed and released.
To demonstrate how to bind to keyboard events in Angular, here's an example:

```html
<!-- keyboard-event.component.html -->
<input type="text" (keyup)="onKeyUp($event)" placeholder="Type something...">
```

In the above code snippet, we have an input field that captures the keyup event and calls the onKeyUp method defined in the component.

```typescript
// keyboard-event.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-keyboard-event',
  templateUrl: './keyboard-event.component.html',
  styleUrls: ['./keyboard-event.component.css']
})
export class KeyboardEventComponent {
  onKeyUp(event: any): void {
    console.log('Key pressed:', event.key);
    // Perform custom logic based on the key pressed
  }
}
```

In the component code, we define the onKeyUp method, which is triggered when a key is released. Inside the method, you can access the event object to get information about the key that was pressed. In this example, we simply log the pressed key to the console, but you can perform any custom logic based on the key pressed.

To use this component, you would need to include it in your parent component or module and use the appropriate selector to display it on the page.

This is a basic example to demonstrate how to bind to keyboard events in Angular. You can extend this concept to handle more complex keyboard interactions, such as listening for specific key combinations or tracking keyboard focus on different elements.




