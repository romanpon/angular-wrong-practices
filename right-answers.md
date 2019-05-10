#### #6
```html
<!-- Comment @dmkorol:
I noticed that "something-row" is applied for all `some-app-something` components.
Maybe, it would be better to move thouse css rules into component?
-->
<some-app-something class="something-row"></some-app-something>
```
---------------
Possible solution:
In most cases you can apply thouse rules to `:host` directly in compoinent.scss
```scss
:host { ... }
```
BUT if you have to add PREDEFINED class(es) for all components in the whole 
application use this approach 'cause it is a secure way and there are 
no side effects (nobody can accidentally delete your styles)
```html
<some-app-something></some-app-something>
```ts
@Component({
  selector:"class="something-row"
})
constructor(public breadcrumbService: BreadcrumbsService,
              private elementRef: ElementRef) {
	this.elementRef.nativeElement.classList.add('breadcrumbs-row');
}
```
***BEAWERE***: 
There is some tricky parts with usage `:host` and `@HostBinding`	
they can override class='' [ngClass]="..."
See details: https://github.com/angular/angular/issues/7289

