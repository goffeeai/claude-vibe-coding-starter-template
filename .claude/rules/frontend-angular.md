# Angular

## Overview
Full-featured TypeScript framework by Google

## Create Project

```bash
npm install -g @angular/cli
ng new my-app
cd my-app
ng serve
```

---

## Project Structure

```
src/
├── app/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── guards/
│   ├── app.component.ts
│   ├── app.module.ts
│   └── app-routing.module.ts
├── assets/
├── environments/
└── main.ts
```

---

## Component

```typescript
// button.component.ts
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-button',
  template: `
    <button (click)="onClick()">
      {{ label }}
    </button>
  `,
  styles: [`
    button { padding: 0.5rem 1rem; }
  `]
})
export class ButtonComponent {
  @Input() label = 'Click me';
  @Output() clicked = new EventEmitter<void>();

  onClick() {
    this.clicked.emit();
  }
}
```

---

## Services

```typescript
// user.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  constructor(private http: HttpClient) {}

  getUsers(): Observable<User[]> {
    return this.http.get<User[]>('/api/users');
  }

  getUser(id: number): Observable<User> {
    return this.http.get<User>(`/api/users/${id}`);
  }
}
```

---

## Template Syntax

```html
<!-- Interpolation -->
<p>{{ user.name }}</p>

<!-- Property binding -->
<img [src]="imageUrl" />

<!-- Event binding -->
<button (click)="handleClick()">Click</button>

<!-- Two-way binding -->
<input [(ngModel)]="name" />

<!-- Structural directives -->
<div *ngIf="isVisible">Visible</div>

<ul>
  <li *ngFor="let item of items; let i = index">
    {{ i }}: {{ item.name }}
  </li>
</ul>

<!-- Class binding -->
<div [class.active]="isActive"></div>
```

---

## Routing

```typescript
// app-routing.module.ts
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: 'users/:id', component: UserDetailComponent },
  { path: '**', component: NotFoundComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

---

## CLI Commands

```bash
ng generate component button    # Create component
ng generate service user        # Create service
ng generate module admin        # Create module
ng build                        # Build for production
ng test                         # Run tests
```
