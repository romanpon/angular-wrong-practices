#What is wrong?
--------------
All formating and structures are oiriginal. 

All variables were renamed to avoid sharing projects data.

Look at the code and ask what could be changed to improve quality of code.

Additionaly you can count how many [code smells](https://en.wikipedia.org/wiki/Code_smell) you can find.

#### #1
```ts
// some-page.component.ts
@Component({
  selector: 'appprefix-some-page',
})
export class SomePageComponent implements OnInit {

  today: number = Date.now();
  wrongDataText;
  isWrongData = false;
  isErrorShow;
  isErrorShowUserName;
  isErrorShowPassword;
  arrControls;
  isLoading = false;
  dataFormGroup: FormGroup;
  validators: ValidatorFn[];
  constructor(private some: SomeService,
              private someOther: SomeOtherService,
              private translate: TranslateService,
              private router: Router
  ) {
```

#### #2
```html
// something.component.html
  <li class="something-list-item"
      *ngFor="let something of somethingService.stepSomething;
              let i = index">
    <a
      *ngIf="i !== somethingbService.stepSomething.length - 1"
      class="something-link"
      (click)="somethingService.clickSmth(i)"
    >{{ something.title }}</a>
    <span
      *ngIf="i === somethingService.stepSomethings.length - 1"
      class="something-link"
    >{{ something.title }}</span>
  </li>
```

#### #3
```ts
// something.service.ts
@Injectable({
  providedIn: 'root'
})
export class SomethingService {
...
  nextSomething() {
    const somethingListHtmlElement: any = document.getElementsByClassName('something-list');
    const somethingRowHtmlElement: any = document.getElementsByClassName('something-row');

    if (somethingRowHtmlElement[0] &&
      somethingRowHtmlElement[0] &&
      somethingRowHtmlElement[0].offsetWidth >=
      somethingRowHtmlElement[0].offsetWidth) {
      this.stepSomething.splice(1, 1);
      setTimeout(() => {
        this.nextSomething();
      }, 300);
    }
...
}
```

#### #4
```ts
const arr = [];
this.selected.forEach(i => {
    const obj = this.processedRows.find(o => o.targetid === i);
    arr.push(obj.id);
});
let structure = {};
```

#### #5
```html
<!-- table.component.html -->
<h1>`{{listName}} {{this.getTableName(tableName)}}</h1>
```
```ts
// table.component.ts
...
getTableName(tableName): string {
    const findTable = this.tablesData ? this.tablesData.find(table => table.tableName === tableName) : this.tablesData;
    
    if (findTable) {
      switch (this.settings.language) {
        case 'en':
          return findTable.somethingEnglish;
        case 'de':
          return findTable.somethingGerman;
      }
    } else {
      return undefined;
    }
}
...
```

#### #6
```html
<!-- 
In all files this component is always with the same class.
What can we do with than? 
-->
<some-app-something class="something-row"></some-app-something>
```

#### #7
```js
//angular.json
"architect": {
"build": {
  "builder": "@angular-devkit/build-angular:browser",
  "options": {
    "outputPath": "dist/somename",
    "index": "src/index.html",
    "main": "src/main.ts",
    "polyfills": "src/polyfills.ts",
    "tsConfig": "src/tsconfig.app.json",
    "assets": [
      "src/favicon.ico",
      "src/assets"
    ],
    "styles": [
      "src/styles.scss",
      "./src/assets/lib/external-lib-name/some.css"
    ],
    "scripts": [
      "node_modules/external-lib-name/dist/external-lib-name.min.js",
      "node_modules/external-lib-name/dist/external-lib-name-html.js",
      "./src/assets/lib/external-lib-name/external-feature1-min.js",
      "./src/assets/lib/external-lib-name/external-feature2-min.js",
      "./src/assets/lib/external-lib-name/external-feature3-min.js",
      "./src/assets/lib/external-lib-name/external-feature4-min.js",
      "./src/assets/lib/external-lib-name/license.js"
    ]
  },
```
 Additional info from file (bundle analyzer)[https://alligator.io/angular/angular-webpack-bundle-analyzer/]:
```js
    "external-lib-name.min.js", // 100kb
    "external-lib-name-html.js", // 50kb
    "external-feature1-min.js", // 4.5mb
    "external-feature2-min.js", // 400kb
    "external-feature3-min.js", // 100kb
    "external-feature4-min.js", // 500kb
```

#### #8
```html
<div (click)='allUnitsMetricActive(true)'>Show all</div>
<div *ngIf="unitsMetricActive">
    <someapp-all-units-metric></someapp-all-units-metric>
</div>
```
```ts
...
    unitsMetricActive = false;

    allUnitsMetricActive(event: boolean) {
        this.unitsMetricActive = event;
    }
...
```

#### #9
```ts
// metrics-details.component.ts
@Component({
    selector: 'details-table'
})
export DetailMetricesComponent {
...
    culcMetric(someMetricsArr): Config.SmthObj {
        if (!someMetricsArr.length) {
            return;
        }
    
        // Copy initial object for no mutation
        const currObj: Config.SmthObj = JSON.parse(JSON.stringify(someMetricsArr[0]));
        const nextObj: Config.SmthObj = someMetricsArr[1];
    
        // Culculate Metric on "Current - Metric" formula
        for (const currentKey in currObj) {
            if (currObj.hasOwnProperty(currentKey)) {
                for (const nextKey in nextObj) {
                    if (currentKey === nextKey) {
                        currObj[currentKey] = currObj[currentKey] - nextObj[nextKey];
                    }
                }
            }
        }
    
        console.log(currObj);
        return currObj;
    }
...
}
```

#### #10
```ts
// config/dictionaries.ts
export const SomesDictionary: MetricDictionary[] = [
    {name: 'Two wrongs don't make a right.', value: 0},
    {name: 'The pen is mightier than the sword.', value: 0},
    {name: 'No man is an island.', value: 0},
    {name: 'Fortune favors the bold.', value: 0},
    {name: 'When the going gets tough, the tough get going.', value: 0},
    {name: 'Hope for the best, but prepare for the worst.', value: 0},
    {name: 'Birds of a feather flock together.', value: 0},
    {name: 'A picture is worth a thousand words', value: 0},
];
```
```ts
// some.component.ts
export class SomeComponent {
 setSomeUnits(specialMetricsObj) {
        this.isDashboardLoaded = true;

        this.specialMetricsUnits.forEach((specialMetricsUnit: Config.MetricDictionary) => {
            switch (specialMetricsUnit.name) {
                case 'Two wrongs don't make a right.':
                    specialMetricsUnit.value = this.valueFormattingPipe.transform(
                        specialMetricsObj.blablabla, 'TransformArea'
                    );
                    break;
                case 'The pen is mightier than the sword.':
                    specialMetricsUnit.value = this.valueFormattingPipe.transform(
                        specialMetricsObj.somethingOtherField, 'TransformEuro'
                    );
                    break;
                case 'Birds of a feather flock together.':
                    specialMetricsUnit.value = this.percentPipe.transform(
                        specialMetricsObj.someCodeName
                    );
                    break;
            }
        });
    }
}
```

#### #11
```ts
@Component({
  selector: 'someapp-name-custom-header.externallib-header-label',
  templateUrl: './omeapp-name-custom-header.component.html',
  styleUrls: ['./omeapp-name-custom-header.component.scss']
})
export class CustomHeaderComponent {

  constructor() { }
  params: any;

  ascSort: string;
  descSort: string;
  noSort: string;
  multiRow: boolean;
  mainColumnsSort;
  secondMainColumnSort;
  externallibInit(params): void {

    this.params = params;
    if (params.column.someFieldName.multiRow) {
      this.multiRow = true;
      this.mainColumnsSort = {
        first: {
          colId: this.params.column.someotherFieldName.columnsField[0],
          sort: params.column.colUniqName.sorting === 'date' ? 'desc' : 'asc'
        },
        second: {
          colId: this.params.column.someSpecialFieldName.columnsField[1],
          sort: 'asc'
        }
      };
  ....
```

#### #12
```ts
//todo changing filter
const arr = rowData.value.map( i => i.id );
```

#### #13
```ts
// super-master.module.ts
...
import {SomeMenuComponent} from '../core/modules/general-table/components/some-side/some-side.component';
import { SortablejsModule } from 'angular-sortablejs';

@NgModule({
  imports: [SortablejsModule],
  declarations: [
    SomeMenuComponent,
  ],
  exports: []
})
export class SuperMasterModule {}
...
```

#### #14
```ts
// somemenu.interface.ts
  export interface ISomethingItems {
    title?: string;
    somethingIcon?: string;
    somethingTitle: string;
    somethingLinks: ILink[];
    somethingTableName: string;
  }
  
// somemenu.component.ts
  ...
  @Input() someMenu: ISomethingItems[];
  selectedItem: string;
  ...
  constructor(
    private router: Router,
    private someSetting: SomeSettingsService,
    private somethingElseService: SomthingElseService
  ) {
    this.router.events.pipe(take(21)).subscribe((res) => {
      if (res instanceof NavigationEnd && this.someMenu) {
        if (this.router.url === '/someurl') {
          this.selectedItem = this.someMenu[0].title;
        } else if (this.router.url === '/someelseurl') {
          this.selectedItem = this.someMenu[2].somethingTitle;
        } else if (this.router.url === '/somethirdurl') {
          this.selectedItem = 'settings';
        } else {
          const someMenu = this.someMenu.find(item => item.somthingTableName === this.router.url.split(/[/?]+/)[1]);

          if (someMenu) {
            this.selectedItem = someMenu.somethingTitle;
          }
        }
      }
    });
    ...
```

#### #15
```ts
@Component({
  selector: 'someapp-table',
  templateUrl: './someapp-table.component.html',
  styleUrls: ['./someapp-table.component.scss']
})
export class SomeTableComponent implements OnInit, OnDestroy {
...
 ngOnInit() {
    this.selectedRowLid = [];
    this.httpService.getData(this.linkFilter)
      .subscribe((value: any) => {
        this.topList = value.lists;
        this.topFilter.emit(this.topList);
      });
    document.addEventListener(
      'special-header',
      (e: any) => {
        setTimeout(() => {
          this.selectedRowLid = e.detail;
          this.isChangedRows = this.selectedRowLid.length > 0;
        }, 0);
      },
      false
    );
    document.addEventListener(
      'some-more',
      (e: any) => {
        setTimeout(() => {
          this.isDataLoading = true;
          this.isShowingInnerColumns = true;
          this.clickSomeMore(e.detail);
        }, 0);
      },
      false
    );
    document.addEventListener(
      'some-click-back',
      () => {
        this.isDataLoading = true;
        setTimeout(() => {
          this.isShowingInnerColumns = false;
          this.clickSomeAction();
        }, 0);
      },
      false
    );
    ...
```

#### #16
```ts
 .pipe(
    map((someSetting: any) => {
      return someSetting.blocks.reduce((resultSettings, block) => {
        block.columns.forEach(column => {
          resultSettings.push(column);
        });
        return resultSettings;
      }, []);
    })
  )
```
