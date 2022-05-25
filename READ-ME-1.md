**copy and paste below css**

```
h4 {
  font-size: 1.20em;
  color: #7d00ff;
}
.controls {
  background-color: #fff;
  border-top: 4px solid #003b6f;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.1);
  height: 130px;
}
.upload.btn {
  border: 2px solid #008eff;
  font-family: "Graphik Black", Arial, Helvetica, sans-serif;
  padding: 1px 10px;
  color: #008eff;
  text-transform: uppercase;
  float: left;
  border-radius: 50px;
  display: block;
}

.control-wrapper {
  display: grid;
  grid-template-columns: 0.2fr 0.5fr;
  column-gap: 5%;
  align-items: baseline;
}

input#UploadInvoices {
  border: 1px solid #e7e7e7;
  border-radius: 3px;
  color: #565656;
  padding: 8px;
  font-size: 14px;
  -webkit-transition: 0.3s;
  transition: 0.3s;
  outline: none;
}

a.upload-btn {
  border: 2px solid #008eff;
  font-family: "Graphik Black", Arial, Helvetica, sans-serif;
  padding: 1px 10px;
  color: #008eff;
  text-transform: uppercase;
  border-radius: 50px;
  text-decoration: none;
}

.btn {
  display: inline-block;
  margin-bottom: 0;
  font-weight: normal;
  text-align: center;
  vertical-align: middle;
  touch-action: manipulation;
  cursor: pointer;
  background-image: none;
  border: 1px solid transparent;
  white-space: nowrap;
  padding: 10px 12px;
  font-size: 14px;
  line-height: 1.42857;
  border-radius: 0px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.upload-file {
  display: flex;
  flex-direction: row;
}

.controls-title {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}

label {
  font-size: 12px;
}

label > a {
  color: #008eff;
  font-size: 15px;
  font-weight: 500;
}

```



**copy all below html and replace it into your html page**


```<div class="container mt-4">
  <div class="row mb-3 controls">
    <h4>Module Type</h4>
    <div class="controls-title mb-3 mt-2">
      <label>Module Type</label>
      <label><a>Post Receipt Rejection/WIP Template</a></label>
    </div>
    <div class="control-wrapper">
      
      <div class="select-modules">
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

      <div class="upload-file">
        <input
          type="file"
          id="UploadInvoices"
          accept=".csv"
          title="Click here to select csv file"
        />
        <div class="btn">
          <a class="upload-btn">Upload CSV</a>
        </div>
      </div>
    </div>
  </div>

  <div class="row">
    <div class="col-md-12 table-wrapper">
      <span class="font-1-rem">
        **Please click on the table headers to sort the data
      </span>
      <table class="table" style="box-shadow: 8px 8px 5px #88888842;">
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
