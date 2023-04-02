# Angular 14 HttpClient & Http 服务

> 原文：<https://javascript.plainenglish.io/angular-14-httpclient-http-services-a2ed888b56d?source=collection_archive---------2----------------------->

今天，我们将向您展示如何使用 HttpClient 服务在 Angular 12 中使用 RESTful API。HttpClient 服务是 Angular 中非常有用的 API，用于与远程服务器进行通信。在本帖中，我们将教你如何用 Angular 制作 HTTP 请求。

# 有角度的 HttpClient 功能

*   明显的支持
*   轻松的 API 测试
*   顺畅的请求和响应机制
*   更好的错误处理

HttpClient 是一个可注入的服务，它附带了各种强大的方法来与远程服务器通信。HttpClient API 可以轻松发送 Http POST、GET、PUT 和 DELETE 请求。

# Angular 14 HttpClient 方法

*   `request()`
*   `delete()`
*   `get()`
*   `head()`
*   `jsonp()`
*   `options()`
*   `patch()`
*   `post()`
*   `put()`

我将向您展示标准 HTTP 方法的实际例子，如 GET、PUT、POST 和 DELETE，这些方法允许您与 REST API 服务器进行通信。

本教程结束时，你将能够理解。如何在 Angular app 中设置 HttpClientModule？使用 JSON server NPM 包使用本地服务器发出请求，以及如何使用 HttpClient API 使用 Angular 发出 GET、POST、PUT & DELETE 请求。

# Angular HttpClient 服务示例

*   安装 Angular CLI
*   在 Angular 中配置假的 JSON 服务器
*   在 Angular 中启用路由服务
*   配置角度 HttpClient
*   使用 Angular HttpClient API 创建使用 RESTful API 的 Angular 服务
*   从 Angular 组件访问 HttpClient API
*   在 Angular 中发送 HTTP GET 和 DELETE 请求来管理数据
*   在 Angular 中发出 HTTP PUT 请求以更新数据

# 创建角度项目

为了创建这个演示应用程序，您必须在您的机器上设置 Node JS 开发环境。

Angular 项目是使用 Angular CLI 开发的，这是一个官方工具。点击以下命令安装 Angular CLI，如果已经安装 Angular CLI，则忽略。

我将使用 Angular 创建一个员工记录管理系统，在这个演示应用程序中，我将通过 HttpClient 服务使用 RESTful API。

是时候设置 Angular 项目了，在 Angular CLI 中运行以下命令。

```
ng new angular-httpclient-app
```

它会问你以下问题…

您想要添加角度路由吗？
选择 y 并按回车键。

您想使用哪种样式表格式？(使用箭头键)
选择 CSS 并按回车键

之后你的项目将开始创建，一旦项目被创建，不要忘记进入项目的文件夹。

```
cd angular-httpclient-app
```

我将使用带有 Angular 的 Bootstrap 4 CSS 框架来使用带有 HttpClient 服务的 RESTful API。点击下面的命令在你的 Angular 应用程序中获得引导。

```
npm install bootstrap
```

之后，转到`angular.json`文件，用“样式”替换下面的代码:[ ]数组。

```
"styles": [
            "node_modules/bootstrap/dist/css/bootstrap.min.css",
            "src/styles.css"
          ]
```

现在，我们必须生成以下组件。

```
ng g c employee-create
ng g c employee-edit
ng g c employee-list
```

# 在 Angular 中配置 JSON 服务器

我们将创建一个假服务器来测试我们的 Angular 应用程序，所以我们将利用 [json-server](https://www.npmjs.com/package/json-server) NPM 包来解决我们的问题。

在我们的项目中安装 JSON 服务器，在 Angular CLI 中运行以下命令。

```
npm i json-server --save
```

然后，创建一个名为 server 的文件夹，并将数据库文件保存在其中，以便在本地管理 API。

```
mkdir server && cd servertouch db.json
```

一旦创建了`db.json`文件，然后在其中添加一些数据。

```
{
  "employees": [{
    "id": 1,
    "name": "Tony Stark",
    "email": "tony@mcu.com",
    "phone": "001-123-4567"
  }, {
    "id": 2,
    "name": "Black Widow",
    "email": "black-widow@mcu.com",
    "phone": "001-123-4568"
  }]
}
```

之后，运行下面的命令来运行 JSON 服务器。

```
json-server --watch db.json
```

现在，如果你用 Angualr 7 Http post 发出任何请求，put，get 或 delete 你的 db.json 文件将在本地得到更新。

您可以在这个 URL `http://localhost:3000/employees`上查看您的本地 db.json 文件。

# 在 Angula 中启用路由服务

为了在 Angular 组件间导航，我们需要激活应用程序中的路由服务，要启用路由，请转到`app-routing.module.ts`文件并添加以下代码。

```
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { EmployeeCreateComponent } from './employee-create/employee-create.component';
import { EmployeeEditComponent } from './employee-edit/employee-edit.component';
import { EmployeeListComponent } from './employee-list/employee-list.component';
const routes: Routes = [
  { path: '', pathMatch: 'full', redirectTo: 'create-employee' },
  { path: 'create-employee', component: EmployeeCreateComponent },
  { path: 'employees-list', component: EmployeeListComponent },
  { path: 'employee-edit/:id', component: EmployeeEditComponent },
];
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

在视图中启用路由，在 app.component.html 文件中添加以下代码。

```
<router-outlet></router-outlet>
```

请确保从“”导入导入批准模块。app.module.ts 文件中的“/app-routing.module”。；

# 导入 HttpClient API

在本教程中，我将向您演示如何使用带有 HttpClient 服务的 Angular 中的 RESTful API 来访问外部服务器以获取数据。为了使用 HttpClient API 与 Http 远程服务器进行通信，您必须在 Angular 应用程序中设置此服务。

转到`app.module.ts`并粘贴以下代码。

```
import { HttpClientModule } from '@angular/common/http';
```

在`@NgModule's`导入数组中包含 HttpClientModule。

```
@NgModule({
  imports: [
    HttpClientModule
   ]
})
```

您已经在应用程序中注入了 HttpClientModule，现在您可以在 Angular app 中轻松使用它。

另外，这里是完整的 app.module.ts 文件，包含路由、表单、app 组件、http 模块。

```
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { AppComponent } from './app.component';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { AppRoutingModule } from './app-routing.module';
import { EmployeeCreateComponent } from './employee-create/employee-create.component';
import { EmployeeEditComponent } from './employee-edit/employee-edit.component';
import { EmployeeListComponent } from './employee-list/employee-list.component';
import { HttpClientModule } from '@angular/common/http';
@NgModule({
  declarations: [
    AppComponent,
    EmployeeCreateComponent,
    EmployeeEditComponent,
    EmployeeListComponent,
  ],
  imports: [
    BrowserModule,
    HttpClientModule,
    FormsModule,
    ReactiveFormsModule,
    AppRoutingModule,
  ],
  providers: [],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

# 创建角度服务

为了使用 Angular HttpClient 服务创建消费 RESTful API，我们需要在应用程序中创建一个服务文件。这个文件将保存我们的演示应用程序的核心逻辑。

## 涵盖的功能:

*   `Create Employee`
*   `Delete Employee`
*   `Update Employee`
*   `Manage Employee List`

为了在 Angular 中使用 RESTful API 创建 CRUD 操作，我们需要生成`employee.ts`类和`rest-api.service.ts`文件。

接下来，生成员工接口类:

```
ng g i shared/Employee
```

转到`shared/employee.ts`并在 Employee 类中定义数据类型。

```
export class Employee {
   id: string;
   name: string;
   email: string;
   phone: number;
}
```

接下来，生成 RestApiService 类:

```
ng g s shared/rest-api
```

我将在这个文件中写下使用 HttpClient API 消费 RESTful API 的核心逻辑。在这个演示应用程序中，我们还将使用 RxJS 来处理异步操作和错误。

让我们转到`shared/rest-api.service.ts`文件并添加以下代码。

```
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Employee } from '../shared/employee';
import { Observable, throwError } from 'rxjs';
import { retry, catchError } from 'rxjs/operators';
@Injectable({
  providedIn: 'root',
})
export class RestApiService {
  // Define API
  apiURL = 'http://localhost:3000';
  constructor(private http: HttpClient) {}
  /*========================================
    CRUD Methods for consuming RESTful API
  =========================================*/
  // Http Options
  httpOptions = {
    headers: new HttpHeaders({
      'Content-Type': 'application/json',
    }),
  };
  // HttpClient API get() method => Fetch employees list
  getEmployees(): Observable<Employee> {
    return this.http
      .get<Employee>(this.apiURL + '/employees')
      .pipe(retry(1), catchError(this.handleError));
  }
  // HttpClient API get() method => Fetch employee
  getEmployee(id: any): Observable<Employee> {
    return this.http
      .get<Employee>(this.apiURL + '/employees/' + id)
      .pipe(retry(1), catchError(this.handleError));
  }
  // HttpClient API post() method => Create employee
  createEmployee(employee: any): Observable<Employee> {
    return this.http
      .post<Employee>(
        this.apiURL + '/employees',
        JSON.stringify(employee),
        this.httpOptions
      )
      .pipe(retry(1), catchError(this.handleError));
  }
  // HttpClient API put() method => Update employee
  updateEmployee(id: any, employee: any): Observable<Employee> {
    return this.http
      .put<Employee>(
        this.apiURL + '/employees/' + id,
        JSON.stringify(employee),
        this.httpOptions
      )
      .pipe(retry(1), catchError(this.handleError));
  }
  // HttpClient API delete() method => Delete employee
  deleteEmployee(id: any) {
    return this.http
      .delete<Employee>(this.apiURL + '/employees/' + id, this.httpOptions)
      .pipe(retry(1), catchError(this.handleError));
  }
  // Error handling
  handleError(error: any) {
    let errorMessage = '';
    if (error.error instanceof ErrorEvent) {
      // Get client-side error
      errorMessage = error.error.message;
    } else {
      // Get server-side error
      errorMessage = `Error Code: ${error.status}\nMessage: ${error.message}`;
    }
    window.alert(errorMessage);
    return throwError(() => {
      return errorMessage;
    });
  }
}
```

# 使用角度 HTTP POST 请求创建数据

转到`employee-create.component.html`添加以下代码。

```
<div class="container custom-container">
  <div class="col-md-12">
    <h3 class="mb-3 text-center">Create Employee</h3>
    <div class="form-group">
      <input type="text" [(ngModel)]="employeeDetails.name" class="form-control" placeholder="Name">
    </div>
    <div class="form-group">
      <input type="text" [(ngModel)]="employeeDetails.email" class="form-control" placeholder="Email">
    </div>
    <div class="form-group">
      <input type="text" [(ngModel)]="employeeDetails.phone" class="form-control" placeholder="Phone">
    </div>
    <div class="form-group">
      <button class="btn btn-success btn-lg btn-block" (click)="addEmployee(employeeDetails)">Create Employee</button>
    </div>
  </div>
</div>
```

转到`employee-create.component.ts`文件并添加以下代码。

```
import { Component, OnInit, Input } from '@angular/core';
import { Router } from '@angular/router';
import { RestApiService } from '../shared/rest-api.service';
@Component({
  selector: 'app-employee-create',
  templateUrl: './employee-create.component.html',
  styleUrls: ['./employee-create.component.scss'],
})
export class EmployeeCreateComponent implements OnInit {
  @Input() employeeDetails = { name: '', email: '', phone: 0 };
  constructor(public restApi: RestApiService, public router: Router) {}
  ngOnInit() {}
  addEmployee(dataEmployee: any) {
    this.restApi.createEmployee(this.employeeDetails).subscribe((data: {}) => {
      this.router.navigate(['/employees-list']);
    });
  }
}
```

通过在 employee create 组件中添加上面给出的代码，我们可以通过 Angular 组件发出 HTTP POST 请求来轻松创建一个雇员。

# 发送 HTTP GET 和 DELETE 请求

在这一部分，我将管理我们在上面创建的员工列表。我将使用我们的 RESTful API 服务，通过我们的自定义 API 发送`get()`和`delete()`请求。

在 employee-list.component.html 文件中添加代码。

```
<div class="container custom-container-2">
  <!-- Show it when there is no employee -->
  <div class="no-data text-center" *ngIf="Employee.length == 0">
    <p>There is no employee added yet!</p>
    <button class="btn btn-outline-primary" routerLink="/create-employee">
      Add Empoyee
    </button>
  </div>
  <!-- Employees list table, it hides when there is no employee -->
  <div *ngIf="Employee.length !== 0">
    <h3 class="mb-3 text-center">Employees List</h3>
    <div class="col-md-12">
      <table class="table table-bordered">
        <thead>
          <tr>
            <th scope="col">User Id</th>
            <th scope="col">Name</th>
            <th scope="col">Email</th>
            <th scope="col">Phone</th>
            <th scope="col">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr *ngFor="let employee of Employee">
            <td>{{ employee.id }}</td>
            <td>{{ employee.name }}</td>
            <td>{{ employee.email }}</td>
            <td>{{ employee.phone }}</td>
            <td>
              <span class="edit" routerLink="/employee-edit/{{ employee.id }}"
                >Edit</span>
              <span class="delete" (click)="deleteEmployee(employee.id)"
                >Delete</span
              >
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
```

在 employee-list.component.ts 文件中添加代码。

```
import { Component, OnInit } from '@angular/core';
import { RestApiService } from '../shared/rest-api.service';
@Component({
  selector: 'app-employee-list',
  templateUrl: './employee-list.component.html',
  styleUrls: ['./employee-list.component.scss'],
})
export class EmployeeListComponent implements OnInit {
  Employee: any = [];
  constructor(public restApi: RestApiService) {}
  ngOnInit() {
    this.loadEmployees();
  }
  // Get employees list
  loadEmployees() {
    return this.restApi.getEmployees().subscribe((data: {}) => {
      this.Employee = data;
    });
  }
  // Delete employee
  deleteEmployee(id: any) {
    if (window.confirm('Are you sure, you want to delete?')) {
      this.restApi.deleteEmployee(id).subscribe((data) => {
        this.loadEmployees();
      });
    }
  }
}
```

# 更新数据

我将在 Angular 中发送 HTTP PUT 请求，以更新我们的小演示应用程序中的当前员工数据，这非常简单，只需遵循以下步骤。

更新 employee-edit.component.html 中的代码:

```
<div class="container custom-container">
  <div class="col-md-12">

    <h3 class="mb-3 text-center">Update Employee</h3>
    <div class="form-group">
      <input type="text" [(ngModel)]="employeeData.name" class="form-control" placeholder="Name">
    </div>
    <div class="form-group">
      <input type="text" [(ngModel)]="employeeData.email" class="form-control" placeholder="Email">
    </div>
    <div class="form-group">
      <input type="text" [(ngModel)]="employeeData.phone" class="form-control" placeholder="Phone">
    </div>
    <div class="form-group">
      <button class="btn btn-success btn-lg btn-block" (click)="updateEmployee()">Update Employee</button>
    </div>

  </div>
</div>
```

# `employee-edit.component.ts`

```
import { Component, OnInit } from '@angular/core';
import { RestApiService } from "../shared/rest-api.service";
import { ActivatedRoute, Router } from '@angular/router';
@Component({
  selector: 'app-employee-details',
  templateUrl: './employee-edit.component.html',
  styleUrls: ['./employee-edit.component.scss']
})
export class EmployeeEditComponent implements OnInit {
  id = this.actRoute.snapshot.params['id'];
  employeeData: any = {};
  constructor(
    public restApi: RestApiService,
    public actRoute: ActivatedRoute,
    public router: Router
  ) { 
  }
  ngOnInit() { 
    this.restApi.getEmployee(this.id).subscribe((data: {}) => {
      this.employeeData = data;
    })
  }
  // Update employee data
  updateEmployee() {
    if(window.confirm('Are you sure, you want to update?')){
      this.restApi.updateEmployee(this.id, this.employeeData).subscribe(data => {
        this.router.navigate(['/employees-list'])
      })
    }
  }
}
```

现在，您可以在浏览器中测试 Angular HttpClient 应用程序，只需在终端中键入`ng serve`。

# 运行角度应用程序

使用下面给出的命令开始您的项目。

```
ng serve --open
```

# 结论

这就是现在…如果这个教程对你有帮助，那么一定要与他人分享。

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，* [***不和***](https://discord.gg/GtDtUAvyhW) ***。*****

***有兴趣规模化你的软件创业*** *？检查* [***电路***](https://circuit.ooo/?utm=publication-post-cta) *。*