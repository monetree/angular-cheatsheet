# ngIf

## ts

    import { Component } from '@angular/core';

    @Component({
    selector: 'app-root',
    templateUrl: './app.component.html',
    styleUrls: ['./app.component.css']
    })
    export class AppComponent {
    courses = [1,2,3]
    }


## html


    <div *ngIf="courses.length > 0">
        List of courses
    </div>

    <div *ngIf="courses.length == 0">
        No Courses Yet
    </div>

    `--or--`


    <div *ngIf="courses.length > 0; else noCourses">
        List of courses
    </div>

    <ng-template #noCourses>
        No Courses Yet
    </ng-template>


        `--or--`

      <div *ngIf="courses.length > 0;then coursesList else noCourses">
          List of courses
      </div>

      <ng-template #coursesList>
          List of courses
      </ng-template>

      <ng-template #noCourses>
          No Courses Yet
      </ng-template>

        `--or--`

      <div [hidden]="courses.length == 0">
          List of courses
      </div>

      <div [hidden]="courses.length > 0">
          No Courses Yet
      </div>



# ngSwitchCase

## ts


      import { Component } from '@angular/core';

      @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.css']
      })
      export class AppComponent {
        viewMode = 'otherwise';
      }

      ## html


      <ul class="nav nav-pills">
          <li [class.active]="viewMode == 'map'">
              <button (click)="viewMode = 'map'" class="btn btn-info">Map Views</button>
          </li>
          <li [class.active]="viewMode == 'list'">
              <button (click)="viewMode = 'list'" class="btn btn-danger">List View</button>
          </li>
      </ul>

      <div [ngSwitch]="viewMode">
          <div *ngSwitchCase="'map'">Map View Content</div>
          <div *ngSwitchCase="'list'">List view Content</div>
          <div *ngSwitchDefault>OtherWise</div>
      </div>


# ngFor

## ts

      import { Component } from '@angular/core';

      @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.css']
      })
      export class AppComponent {
        courses = [
          { id:1, name:'course1' },
          { id:2, name:'course2' },
          { id:3, name:'course3' }
        ];
      }


## html


    <ul>
        <li *ngFor="let course of courses; index as i">
            {{ i }} - {{ course.name }}
        </li>
    </ul>


    `--even property--`


    <ul>
        <li *ngFor="let course of courses; even as isEven">
            {{ course.name }} <span *ngIf="isEven">Even</span>
        </li>
    </ul>

    `--add remove--`

## ts


    export class AppComponent {
      courses = [
        { id:1, name:'course1' },
        { id:2, name:'course2' },
        { id:3, name:'course3' }
      ];
      onAdd(){
        this.courses.push({ id:4, name:'course4' })
      }
      onRemove(course){
        let index = this.courses.indexOf(course);
        this.courses.splice(index, 1)
      }
    }


## html


      <button class="btn btn-info" (click)="onAdd()">Add</button>

      <ul>
      <li *ngFor="let course of courses; even as isEven">
          {{ course.name }} <span *ngIf="isEven">Even</span>
          <button class="btn btn-danger" (click)="onRemove(course)">Remove</button>
      </li>
      </ul>



      `--trackBy--`


## ts


      trackCourse(index, course){
        return course ? course.id : undefined;
      }


## html

      <button class="btn btn-info" (click)="loadCourses()">loadCourses</button>

      <ul>
          <li *ngFor="let course of courses; trackBy: trackCourse">
              {{ course.name }}
          </li>
      </ul>


# ngStyle

## ts

    canSave = true;

## html


    <button
     [ngStyle]="{
        'backgroundColor': canSave ? 'blue' : 'gray',
        'color': canSave ? 'white' : 'black',
        'fontWeight': canSave ? 'bold' : 'normal'
     }"
     >
     Save
    </button>
