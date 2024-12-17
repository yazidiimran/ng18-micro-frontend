# ng18-micro-frontend

ng new shell
ng new todo

#SHELL

cd shell
npm i -D @angular-architects/native-federation
ng g @angular-architects/native-federation:init --project shell --port 4200 --type dynamic-host
ng g c pages/home  

shell/src/app/app.routes.ts:
export const routes: Routes = [
    { path: '', component: HomeComponent },
    {
        path: 'todo',
        loadComponent: () =>
            loadRemoteModule('todo', './Component').then((m) => m.AppComponent),
    },
    {
        path: '**',
        component: HomeComponent,
    },
];

shell/src/app/app.component.html:
<ul>
  <li><a routerLink="/">Shell</a></li>
  <li><a routerLink="/todo">Todo</a></li>
</ul>
<router-outlet></router-outlet>

ng serve


#TODO
cd todo
npm i -D @angular-architects/native-federation
ng g @angular-architects/native-federation:init --project todo --port 4201 --type remote
ng serve



