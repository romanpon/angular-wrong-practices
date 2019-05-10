Code quality recomendations:

+ https://angular.io/guide/styleguide

+ https://en.wikipedia.org/wiki/Code_smell

+ We can use services direct from view 
https://angular.io/tutorial/toh-pt4#bind-to-the-messageservice

+ <a> tag always should have 'href' or href="javascript:void(0)"

+ Read left to right service.someArray.length - 1 !== i

+ Check names in the translator, avoid misspelling

+ Don't put not English charecters into the code

+ Don't put any affensive words even for testing on your local machine. Evering that you write in the project somehow can be deployed to the production by some megical coincidences.

+ Use autoformating in IDE or let's use prittier

+ Never set properies in service from other service, use setPropName()

+ Add types everywhere

+ Don't work with DOM from service (only if there is no other way to solve your issue, but I'm sure in most cases there are other ways)

+ Consider pessimistic scenarios. To avoid crushes use additional chackings
```
this.selected.forEach(i => {
	const obj = this.processedRows.find(o => o.targetid === i);
	if(obj && obj.id) {
		arr.push(obj.id);
	}
});
```

+ Avoid messpeling by destructor and interfaces:
```
let {propname1, propname2, propname3} = item;
arr.push({propname1, propname2, propname3});
```

+ Try to incapsulate css related to component in the component(don't apply classes outside)
```
// DON'T USE:
host: {'class':'class-related-to-component'} 
@HostBinding('class') classList: string = 'breadcrumbs-row';
@HostBinding('class') @Input('class') classList: string = '';	
https://github.com/angular/angular/issues/7289
// 
constructor(public breadcrumbService: BreadcrumbsService,
              private elementRef: ElementRef) {
	this.elementRef.nativeElement.classList.add('breadcrumbs-row');
}
//or
@HostBinding('class.m-grid__item') public bindStyle: boolean = true;
```

+ ngFor https://angular.io/api/common/NgForOf local variables

+ dont put lib that used only in one module into angular.json

+ right prefixes isActive setModel() activeRecord valuesList

+ check spelling in translator culcMetodProperti()

+ Class first properties second methods, functions 

+ Difference Comment vs TODO. TODO - to do it, comment - just for info
//Examples from material, from angular 
//Open real code
https://levelup.gitconnected.com/best-practices-in-angular-a8926fa02ae2

+ TODO, FIXME, BEAWERE
https://en.wikipedia.org/wiki/Comment_%28computer_programming%29#Tags	
https://softwareengineering.stackexchange.com/questions/125320/do-todo-comments-make-sense

Architecture:
https://itnext.io/planning-the-architecture-of-your-angular-app-a4840bfec13b
https://gist.github.com/cyrilletuzi/e6d446c8b1188bd59dd5c6d0f8e31d66#file-architecture-txt
https://itnext.io/choosing-a-highly-scalable-folder-structure-in-angular-d987de65ec7
https://medium.com/@motcowley/angular-folder-structure-d1809be95542
https://angular.io/guide/styleguide





