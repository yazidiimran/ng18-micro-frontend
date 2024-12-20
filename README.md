# ng18 Micro Frontend

## Create Shell and Todo Projects

1. Create the Shell and Todo applications:
    ```bash
    ng new shell
    ng new todo
    ```

## Shell Setup

1. **Navigate to the Shell project**:
    ```bash
    cd shell
    ```

2. **Install `@angular-architects/native-federation`**:
    ```bash
    npm install --save-dev @angular-architects/native-federation
    ```

3. **Initialize the Shell project with Native Federation**:
    ```bash
    ng generate @angular-architects/native-federation:init --project shell --port 4200 --type dynamic-host
    ```

4. **Generate a Home Component**:
    ```bash
    ng generate component pages/home
    ```

5. **Update `federation.manifest.json`** (located in `shell/public/`):
    Ensure the port for the Todo app is correctly set:
    ```json
    {
      "todo": "http://localhost:4201/remoteEntry.json"
    }
    ```

6. **Update `app.routes.ts`** (located in `shell/src/app/`):
    Configure routes and dynamically load the `Todo` component:
    ```typescript
    import { Routes } from '@angular/router';
    import { HomeComponent } from './pages/home.component';
    import { loadRemoteModule } from '@angular-architects/module-federation';

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
    ```

7. **Update `app.component.html`** (located in `shell/src/app/`):
    Set up the navigation and router outlet:
    ```html
    <ul>
      <li><a routerLink="/">Shell</a></li>
      <li><a routerLink="/todo">Todo</a></li>
    </ul>

    <router-outlet></router-outlet>
    ```

8. **Serve the Shell app**:
    ```bash
    ng serve
   
