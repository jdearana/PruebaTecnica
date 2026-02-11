Errors:
1. Pipe expects operators.
2. Timer never ends.
3. No unsuscribe so everything is going to be running for ever.
4. When the user writes every key is a new query, so it creates a lot of unnecesary requests

```typescript
@Component({
  selector: 'app-users',
  template: `
    <input 
      type="text" 
      [(ngModel)]="query" 
      (ngModelChange)="querySubject.next($event)"
    >
    <div *ngFor="let user of users$ | async">
      {{ user.email }}
    </div>
  `
})
export class AppUsers implements OnInit, OnDestroy {

  query = '';
  querySubject = new Subject<string>();
  private destroy$ = new Subject<void>();

  users$ = this.querySubject.pipe(
    startWith(this.query),
    debounceTime(300),
    switchMap(query =>
      timer(0, 60000).pipe(
        switchMap(() => this.userService.findUsers(query))
      )
    ),
    takeUntil(this.destroy$)
  );

  constructor(private userService: UserService) {}

  ngOnDestroy(): void {
    this.destroy$.next();
    this.destroy$.complete();
  }
}
```
