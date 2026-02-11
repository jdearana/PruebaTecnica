```typescript
import { Component, Output, EventEmitter } from '@angular/core';
import { CommonModule } from '@angular/common';  

import { ReactiveFormsModule, FormGroup, FormBuilder, Validators, AbstractControl, ValidationErrors } from '@angular/forms';

@Component({
  selector: 'app-test-component',
  standalone: true,
  imports: [ReactiveFormsModule, CommonModule],
  template: `<form [formGroup]="form" (ngSubmit)="doSubmit()">

      <input
        type="email"
        placeholder="email"
        formControlName="email"
      />

      <input
        type="text"
        placeholder="name"
        formControlName="name"
      />

      <input
        type="date"
        placeholder="birthday"
        formControlName="birthday"
      />
      <div *ngIf="form.get('birthday')?.hasError('pastDate')">
        La fecha debe ser anterior al día de hoy
      </div>

      <div formGroupName="address">
        <input
          type="number"
          placeholder="zip"
          formControlName="zip"
        />

        <input
          type="text"
          placeholder="city"
          formControlName="city"
        />
      </div>

      <button type="submit" [disabled]="form.invalid">
        Submit
      </button>

    </form>`
  
})
export class TestComponentComponent {

  @Output()
  event = new EventEmitter<{
    email: string;
    name: string;
    birthday: Date;
    address: {
      zip: number;
      city: string;
    };
  }>();

  form: FormGroup;

  constructor(private formBuilder: FormBuilder) {
    this.form = this.formBuilder.group({
      email: ['', [Validators.required, Validators.email]],
      name: ['', Validators.required],
      birthday: [null, [Validators.required, this.checkBirthDay]],
      address: this.formBuilder.group({
        zip: [null, Validators.required],
        city: ['', Validators.required]
      })
    });
  }

  private checkBirthDay(
    control: AbstractControl
  ): ValidationErrors | null {

    const value = control.value;
    if (!value) {
      return null;
    }

    const birthday = new Date(value);
    const today = new Date();

    birthday.setHours(0, 0, 0, 0);
    today.setHours(0, 0, 0, 0);

    return birthday < today ? null : { pastDate: true };
  }

  doSubmit(): void {
    
    if (this.form.invalid) {
      return;
    }

    const value = {
      ...this.form.value,
      birthday: new Date(this.form.value.birthday)
    };
    console.log('Emitting event with value:', value);
    this.event.emit(value);
  }
}