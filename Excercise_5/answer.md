## 5. Exercise: Improve performance

```typescript
@Component({
  selector: 'app-users',
  template: `
    <div *ngFor="let user of userInitial">
        {{ user }}
    </div>
  `
})
export class AppUsers {

  @Input()
  users: { name: string; }[];
  private userInitial: string[] =[];
  constructor() {}

  ngOnInit() {
    const numUsers= this.users.length;
    for (let i = 0; i < numUsers; i++) {
      const userName = this.users[i].name;
      const nameParts = userName.split(' ');
      const nameLength = nameParts.length;
      let initials = '';
      for (let j = 0; j < nameLength; j++) {
        initials += nameParts[j].charAt(0).toUpperCase();
      }
      this.userInitial.push(initials);
    }
  }
}
```