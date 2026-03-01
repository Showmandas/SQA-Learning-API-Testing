# SQA-Learning-API-Testing
Api Testing with POSTMAN

#Project Title : End-to-End API testing
This project focuses on testing RESTful APIs for a Student Management System where users can create, retrieve, and delete student records. The main objective was to validate API functionality, response structure, status codes, and data integrity using Postman.

The system includes three core API operations:

Create Student (POST):
Verified that new student records can be created successfully with valid request body data. Tested positive and negative scenarios including missing fields, invalid data types, and duplicate entries. Validated response status codes (201 Created) and response payload.

Get Student (GET):
Tested fetching student details by ID and retrieving all students. Validated response status code (200 OK), response time, and correct JSON structure. Checked error handling for invalid or non-existing IDs (404 Not Found).

Delete Student (DELETE):
Verified successful deletion of student records and validated status code (200/204). Also tested deleting non-existing records to confirm proper error response.

Here we used Postman for api testing,excel sheet for tese cases,rest api

Step 1: Create a Collection

1️⃣ Open Postman
2️⃣ Click New → Collection
3️⃣ Name it: create student
4️⃣ Click Create

2. Get Student (GET)
Method → GET
Name -> Get students

3. Delete Student (DELETE)
Method → DELETE
URL → {{base_url}}/api/studentDetails/{{student_id}}

Step 3: Use Environment Variables
Click Environments → Create New Environment
base_url - https://thetestingworldapi.com
student_id 

Add Test Scripts:
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});


Step 5: Run the Collection
🔹 Method 1: Run All APIs Together
1️⃣ Click Students
2️⃣ Click Run Students
3️⃣ Select Environment
4️⃣ Click Run Students
1️⃣ Click Environments → Create New Environment

{{base_url}} = https://thetestingworldapi.com
#API Chainig
Step 1: Create Student (POST)
🔹 Request
POST → {{base_url}/api/studentsDetails
JSON: 
{
    "id": 10859055,
    "first_name": "Elmore",
    "middle_name": "sample string 3",
    "last_name": "Lebsack",
    "date_of_birth": "sample string 5"
}

🪜 Step 2: Extract Student ID from Response
var responseBody = pm.response.json();
pm.environment.set("student_id",responseBody.id);

🪜 Step 3: Get Student (GET)
GET → {{base_url}}/api/studentsDetails/{{student_id}}
Add test:
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

Delete Student (DELETE)
DELETE → {{base_url}}/students/{{student_id}}
Code: 
pm.test("Student deleted successfully", function () {
    pm.response.to.have.status(200);
});

Test Cases check
Create/Get
pm.test("Status code should be 200",function(){
    pm.response.to.have.status(200);
})
pm.test("First Name is sample string 2",function(){
    pm.expect(pm.response.json()[0].first_name).to.eql("sample string 2");
})
pm.test("date of birth is sample string 5",function(){
    pm.expect(pm.response.json()[0].date_of_birth).to.eql("sample string 5");
})

