---
applyTo: "apps/web/**"
---

# Frontend Instructions (Angular)

## Component Guidelines

- Use standalone Angular components (no NgModules).
- Keep components small and reusable.
- Prefer OnPush change detection for performance.
- Use signals for reactive state management where appropriate.
- Move API calls into services in `services/`.
- Avoid business logic inside templates.

## Forms

- Use Angular Reactive Forms for all forms.
- Implement proper validation with error messages.
- Show loading, error, and success states.
- Disable submit button during form submission.

## Accessibility

- Use semantic HTML elements.
- Add proper ARIA labels where needed.
- Ensure keyboard navigation works.
- Provide clear validation error messages.

## Styling

- Use SCSS for component styles.
- Follow BEM naming convention for CSS classes.
- Keep styles scoped to components.
- Use CSS variables for theming.

## Type Safety

- Reuse shared types from `packages/shared/src/types.ts`.
- Define component-specific interfaces in the component file.
- Avoid `any` type.

## Testing

- Add unit tests for services.
- Add component tests for important interaction flows.
- Use Angular Testing Library patterns.
- Mock HTTP calls in tests.

## File Organization

```
apps/web/src/app/
├── components/        # Reusable UI components
│   ├── task-form/
│   ├── task-list/
│   ├── task-item/
│   └── task-filter/
├── pages/             # Route-level components
│   └── home/
├── services/          # API and business logic services
│   └── task.service.ts
├── models/            # Frontend-specific interfaces
└── app.component.ts
```

## Angular-Specific Patterns

```typescript
// Standalone component example
@Component({
  selector: 'app-task-item',
  standalone: true,
  imports: [CommonModule, ReactiveFormsModule],
  templateUrl: './task-item.component.html',
  styleUrls: ['./task-item.component.scss'],
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class TaskItemComponent {
  @Input({ required: true }) task!: Task;
  @Output() toggle = new EventEmitter<string>();
  @Output() delete = new EventEmitter<string>();
}
```

```typescript
// Service with HttpClient example
@Injectable({ providedIn: 'root' })
export class TaskService {
  private readonly apiUrl = 'http://localhost:3000/api/tasks';
  
  constructor(private http: HttpClient) {}
  
  getTasks(): Observable<Task[]> {
    return this.http.get<ApiResponse<Task[]>>(this.apiUrl).pipe(
      map(response => response.success ? response.data : [])
    );
  }
}
```
