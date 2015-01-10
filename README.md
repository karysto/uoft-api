A Node.js module for retrieving data from the University of Toronto's course listings.

##### Disclaimer
Please be aware that this module relies on web scrapers to retrieve the data from the University of Toronto course listings. I cannot control how you incorporate this module into your project, and so by using this module you agree that the developer(s) of this module are in no way responsible for any consequences that may (or may not) result because of your use of this module.

#### Getting Started
##### Install:
```sh
$ npm i uoft-api
```
##### Reference:
```js
var uoftAPI = require('uoft-api');
```

### Supported Functions
- `getCourseDepartment`
- `getProgramCourses`

##### `getCourseDepartment`
- Takes a valid three-letter code representing a department at the University (ie/ the first three letters of any  course code). 
- Returns an array of strings, where each string is a department name which offers courses specified by the code.

##### Number of Requests:
- `getCourseDepartment` performs **1** request to retrieve the department name of the specified program.

##### Usage:
```js
uoftAPI.getCourseDepartment(programCode, function(err, department) {
  // do whatever with the course department array
});
```
##### Examples
###### Where all courses from the specified program belong to one department.
```js
uoftAPI.getCourseDepartment('csc', function(err, department) {
  console.log(department);
  /* ['Computer Science'] */
});
```
###### Where courses from the specified program span several departments
```js
uoftAPI.getCourseDepartment('env', function(err, department) {
  console.log(department);
  /*
  [ 'Earth Sciences',
    'Ecology & Evolutionary Biology',
    'Environment, School of',
    'Physics' ]
  */
});
```

##### `getProgramCourses`
- Takes a valid three-letter code representing a department at the University (ie/ the first three letters of any  course code). 
- Returns an array of JSON objects in a callback (as demonstrated below), where each JSON object contains a single course's information and has the following structure:

```js
  {
    courseName: 'Computational Thinking', // Title of the course
    courseCode: 'CSC104H1',               // Course code
    courseTerm: 'F',                      // Course semester
    courseWait: 'Y',                      // If the course contains a wait-list (Y/N)
    courseProf: [ 'D. Heap' ]             // Professor(s) teaching the course
  }
```

##### Number of Requests:
- `getProgramCourses` performs **2** requests to retrieve all course data of the specified program.

##### Usage:
```js
uoftAPI.getProgramCourses(programCode, function(err, courseData) {
  // do whatever with the returned courseData json
});
```
##### Examples
```js
uoftAPI.getProgramCourses('csc', function(err, courseData) {
  console.log(courseData);
  /*
  [
    {
      courseName: 'Computational Thinking',
      courseCode: 'CSC104H1',
      courseTerm: 'F',
      courseWait: 'Y',
      courseProf: [ 'D. Heap' ]
    },
    {
      courseName: 'Computational Thinking',
      courseCode: 'CSC104H1',
      courseTerm: 'S',
      courseWait: 'Y',
      courseProf: [ 'G. Baumgartner' ]
    },
      < ... etc, ordered by course code ... >
    {
      courseName: 'Computabil & Logic',
      courseCode: 'CSC438H1',
      courseTerm: 'F',
      courseWait: 'Y',
      courseProf: [ 'T. Pitassi' ]
    }
  ]
*/
});
```

### Function Addition Roadmap
- Extending `getProgramCourses` to include the lecture and tutorial sections of each respective class in their own arrays.
- Extending `getProgramCourses` to include when each tutorial and lecture section takes place (day of the week and time).
- Extending the module to support course data from the University of Toronto Mississauga and Scarborough campus time-tables.
- Extending the module to support course data from the St. George campus Faculty of Engineering.
