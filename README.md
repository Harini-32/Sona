<form class="modal-content" #form="ngForm" (ngSubmit)="signup()">

  <h1>Sign Up</h1>
  <p>Please fill in this form to create an account.</p>
  <label for="email"><b>Email</b></label>
  <input type="email" placeholder="Enter Email" [(ngModel)]="email" name="email" required>

  <label for="psw"><b>Password</b></label>
  <input type="password" placeholder="Enter Password" [(ngModel)]="password" name="psw" required>

  <label for="psw-repeat"><b>Confirm Password</b></label>
  <input type="password" placeholder="Repeat Password" [(ngModel)]="repeatPassword" name="psw-repeat" required>

  <div class="clearfix">
    <button type="submit" (click)="register()" [disabled]="form.invalid" class="btn btn-success" 
    class="btn btn-primary">Sign Up</button>
    </div>

  <div *ngIf="registerAttempted && registerSuccess" style="color: green"> 
    Registered successfully ! Please 
    <a routerLink='/login'>login here</a>
  </div>

</form>




/* Full-width input fields */
input{
    width: 100%;
    padding: 15px;
    margin: 5px 0 22px 0;
    display: inline-block;
    border: none;
    background: #f1f1f1;
  }

/* Set a style for all buttons */
button {
    padding: 14px 20px;
    margin: 8px 0;
    border: none;
    cursor: pointer;
    width: 100%;
    opacity: 0.8
  }

/* Modal Content/Box */
.modal-content {

  border: 1px solid #888;
  padding: 1em;
  /* Could be more or less, depending on screen size */

}







import {Component, OnInit} from '@angular/core';
import {Router} from '@angular/router';
import {HttpClient} from '@angular/common/http';
const apiUrl = '/api';

@Component({
  selector: 'app-register',
  templateUrl: './register.component.html',
  styleUrls: ['./register.component.css']
})
export class RegisterComponent implements OnInit {

  public email: any;
  public password: string;
  public repeatPassword: any;

  constructor(private router: Router, private http: HttpClient) {
  }

  registerAttempted = false;
  registerSuccess = false;

  ngOnInit() {
  }

  register() {
    this.registerAttempted = true;
    const userInfo = {
      emailId: this.email,
      password: this.password,
    };
    this.addUser(userInfo);
  }

  addUser(userInfo) {
    console.log(userInfo);
    this.http.post('http://localhost:3000/api/register', userInfo).subscribe(data => {
      console.log('register data : ', data);
      this.registerSuccess= true;
    });
  }

}

