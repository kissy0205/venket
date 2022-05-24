- **step 1**    |   npm install -g json-server in project
- **step 2**    |   create **db.json** in your root folder like below

![image](https://user-images.githubusercontent.com/60337548/170031823-9a1fba9e-dd45-4f24-a29f-caa88d7025c0.png)

- **step 3**    |   create new service using cli **ng g s YOUR-RLEVENT-SERVICE-NAME** and add below code in your service
```
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';
import { IModuleType } from './test.model';

@Injectable({
  providedIn: 'root'
})
export class YOUR-RLEVENT-SERVICE { // change service name

  baseURL = `https://idigi-svc.ciostage.accenture.com/`;
  public testData = `http://localhost:3000/modules`;
  constructor(private _http: HttpClient) { }

  loadModuleTypeData(selectedModuleType: string): Observable<any>{
   // const endPoint = `IDigiWebAPI-Service/IDigiWebAPIPostAR?moduleSelected=${selectedModuleType}`;
   // return this._http.get(this.baseURL + endPoint);
   return this._http.get<IModuleType>(this.testData + `?ModuleNm=${selectedModuleType}`);
  }
  
}
```
- **step 4**    |   create a new component cli **ng g c YOUR-RLEVENT-COMPONENT-NAME** and add below code in your component
```
 selectedModuleType = 'Generic';
  tableData: any;
  collectionSize: any;
  moduleType = [
    { value: 'Generic', name: 'Generic' },
    { value: 'IQN', name: 'IQN' },
    { value: 'RealEstate', name: 'Real Estate' },
    { value: 'Visa', name: 'Visa' },
    { value: 'AP', name: 'AP' },
    { value: 'Forex', name: 'Forex' },
  ];
  page = 1;
  pageSize = 6;
  displayColumns = [
    'Type',
    'File Uploaded',
    'Uploaded By',
    'Uploaded Date',
    'Failed Records',
  ];
  booleanValue: any = false;
  constructor(public test: TestService) {}

  ngOnInit(): void {
    this.loadModuleData(this.selectedModuleType);
  }

  onModuleChange(eventValue: any): void {
    eventValue = eventValue.target.value;
    if (eventValue && eventValue !== '') {
      console.log('Selected Module', eventValue);
      this.loadModuleData(this.selectedModuleType);
    }
  }

  loadModuleData(selectedModule: string): void {
    console.log('loadModuleData mothod :::::>', selectedModule);
    this.test.loadModuleTypeData(selectedModule).subscribe({
      next: (resp: IModuleType[]) => {
        console.log('RESPONSE IN COMPONENT', typeof resp[0]);
        if (resp) {
          this.tableData = resp;
          this.collectionSize = resp.length;
        }
      },
      error: (err: any) => {
        console.log('Errors :::>', err);
      },
      complete: () => {
        console.log('request completed');
      },
    });
  }
```

- **step 5**    |   paste below code in corresponding component's html
```
<div class="container mt-4">
  <div class="row mb-3">
    <div class="col-md-3">
      <select
        class="form-select"
        aria-label="Default select example"
        [(ngModel)]="selectedModuleType"
        (change)="onModuleChange($event)"
      >
        <option
          *ngFor="let m of moduleType"
          value="{{ m.value }}"
          selected="selected"
        >
          {{ m.name }}
        </option>
      </select>
    </div>
  </div>

  <div class="row">
    <div class="col-md-12 table-wrapper">
      <span class="font-1-rem">
        **Please click on the table headers to sort the data
      </span>
      <table class="table">
        <thead class="th-bg-color">
          <tr>
            <th scope="col" *ngFor="let col of displayColumns">{{ col }}</th>
          </tr>
        </thead>
        <tbody style="font-size: 12px; text-align: center">
          <tr *ngFor="let data of tableData">
            <td id="font-12">{{ data.ModuleNm }}</td>
            <td>{{ data.FileNm }}</td>
            <td>{{ data.UploadedBy }}</td>
            <td>{{ data.UploadDttm }}</td>
            <td>{{ data.ErrorFileNm }}</td>
          </tr>
        </tbody>
      </table>

      <ngb-pagination
        [collectionSize]="collectionSize"
        [(page)]="page"
        [maxSize]="5"
        [rotate]="true"
        [ellipses]="false"
        [boundaryLinks]="true"
      ></ngb-pagination>
    </div>
  </div>
</div>

```

- **step 6**    |   open new cmd and run **json-server --watch db.json** to up and run the local server

