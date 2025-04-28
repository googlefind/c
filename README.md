
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Code Examples with Copy Buttons</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
            line-height: 1.6;
        }
        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
        }
        .code-container {
            position: relative;
            margin-bottom: 20px;
            background-color: #f8f8f8;
            border-radius: 6px;
            padding: 15px;
            border-left: 4px solid #4CAF50;
            overflow-x: auto;
        }
        .copy-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            padding: 8px 15px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
        }
        .copy-btn:hover {
            background-color: #45a049;
        }
        .copy-btn.copied {
            background-color: #2196F3;
        }
        pre {
            margin: 0;
            white-space: pre-wrap;
            font-family: 'Courier New', monospace;
            padding: 10px;
            background-color: #f0f0f0;
            border-radius: 4px;
            tab-size: 4;
        }
        .example-title {
            font-weight: bold;
            margin-bottom: 10px;
            color: #444;
        }
    </style>
</head>
<body>
    <h1>Code Examples with Copy Buttons</h1>
    
    <div id="code-examples-container">
        <!-- Example 1 -->
        <div class="code-container">
            <div class="example-title">1. Student Information Class</div>
            <button class="copy-btn" onclick="copyCode(this)">Copy</button>
            <pre><code>#include &lt;iostream&gt;
using namespace std;
class Student_Info
{ int USN;
 char student_name[50], grade[2];
 public:
 void read_data(int count)
 { cout&lt;&lt;"Name of the Student (Max. 50 characters only): ";
 cin&gt;&gt;student_name;
 cout&lt;&lt;"USN: ";
 cin&gt;&gt;USN;
 cout&lt;&lt;"Grade (O, A+, A, B+, B, C, D, F): ";
 cin&gt;&gt;grade; }
 void display_data(int count)
 { cout&lt;&lt;"\nName of the Student: "&lt;&lt;student_name;
 cout&lt;&lt;"\nUSN: "&lt;&lt;USN;
 cout&lt;&lt;"\nGrade Secured: "&lt;&lt;grade; }
};
int main()
{ Student_Info stud[3];
 int i;
 for (i=0; i&lt;3; i++)
 stud[i].read_data(i);
 cout&lt;&lt;"The information of 3 students has been saved.";
 for (i=0; i&lt;3; i++)
 stud[i].display_data(i);
 return 0;
}</code></pre>
        </div>
        
        <!-- Example 2 -->
        <div class="code-container">
            <div class="example-title">2. College Information Structure</div>
            <button class="copy-btn" onclick="copyCode(this)">Copy</button>
            <pre><code>#include &lt;iostream&gt;
using namespace std;
struct college_info{
 char college_name[15];
 char college_code[2];
 char dept[50];
 int intake;
};
int main()
{
 struct college_info college;
 cout&lt;&lt;"\n\n+++++ Enter the College Information +++++\n\n";
 cout&lt;&lt;"Name of the college: ";
cin&gt;&gt;college.college_name;
 cout&lt;&lt;"College Code: ";
 cin&gt;&gt;college.college_code;
 cout&lt;&lt;"Department: ";
 cin&gt;&gt;college.dept;
 cout&lt;&lt;"Department In-take: ";
 cin&gt;&gt;college.intake;
 cout&lt;&lt;"\n\n********* College Information *********\n\n";
 cout&lt;&lt;"Name of the college : "&lt;&lt;college.college_name;
 cout&lt;&lt;"\nCollege University Code: "&lt;&lt;college.college_code;
 cout&lt;&lt;"\nName of the Department: "&lt;&lt;college.dept;
 cout&lt;&lt;"\nThe department of "&lt;&lt;college.dept&lt;&lt;" has in-take : "&lt;&lt;college.intake;
 cout&lt;&lt;"\n\n-----------------------------------------\n\n"; 
 return 0;
}</code></pre>
        </div>
        
        <!-- Example 3 -->
        <div class="code-container">
            <div class="example-title">3. Class with Pointer and Private Member Function</div>
            <button class="copy-btn" onclick="copyCode(this)">Copy</button>
            <pre><code>#include &lt;iostream&gt;
using namespace std;
// Declare a class
 class MyClass {
 public:
 int value;
 // Member function to display the value
 void display() {
 cout &lt;&lt; "Value: " &lt;&lt; value &lt;&lt; endl;
 display1();
 }
 private: 
 void display1()
 {
 value=10;
 cout &lt;&lt; "Value: " &lt;&lt; value &lt;&lt; endl;
}
 };
 int main() {
 // Declare a pointer to the class
 MyClass *ptr;
 // Dynamically allocate memory for the class object
 ptr = new MyClass;
 // Initialize the class member
 ptr-&gt;value = 42;
 // Display the contents of the class member
 ptr-&gt;display();
 // Free the allocated memory
 delete ptr;
 return 0; 
}</code></pre>
        </div>
        
        <!-- Example 4 -->
        <div class="code-container">
            <div class="example-title">4. Employee Salary Calculation</div>
            <button class="copy-btn" onclick="copyCode(this)">Copy</button>
            <pre><code>#include &lt;windows.h&gt;
 #include &lt;iostream&gt;
 using namespace std;
 class employee
 { int emp_number;
char emp_name[20];
float emp_basic;
float emp_da;
float emp_it;
float emp_net_sal;
public:
void get_emp_details();
float find_net_salary(float basic, float da, float it);
void show_emp_details();
};
void employee :: get_emp_details()
{ cout&lt;&lt;"\nEnter employee number: ";
cin&gt;&gt;emp_number;
cout&lt;&lt;"\nEnter employee name: ";
cin&gt;&gt;emp_name;
cout&lt;&lt;"\nEnter employee basic: ";
cin&gt;&gt;emp_basic;
cout&lt;&lt;"\nEnter employee DA: ";
cin&gt;&gt;emp_da;
cout&lt;&lt;"\nEnter employee IT: ";
cin&gt;&gt;emp_it;
}
float employee :: find_net_salary(float basic, float da, float it)
{ return (basic+da)-it;
}
void employee :: show_emp_details()
{ cout&lt;&lt;"\n\n**** Details of Employee ****";
cout&lt;&lt;"\nEmployee Name : "&lt;&lt;emp_name;
cout&lt;&lt;"\nEmployee number : "&lt;&lt;emp_number;
cout&lt;&lt;"\nBasic salary : "&lt;&lt;emp_basic;
cout&lt;&lt;"\nEmployee DA : "&lt;&lt;emp_da;
cout&lt;&lt;"\nIncome Tax : "&lt;&lt;emp_it;
cout&lt;&lt;"\nNet Salary : "&lt;&lt;find_net_salary(emp_basic, emp_da, emp_it);
cout&lt;&lt;"\n-------------------------------\n\n";
}
int main()
{
 employee emp;
 emp.get_emp_details();
 emp.show_emp_details();
 return 0;
}</code></pre>
        </div>
        
        <!-- Example 5 -->
        <div class="code-container">
            <div class="example-title">5. Multiple Employee Salary Calculation</div>
            <button class="copy-btn" onclick="copyCode(this)">Copy</button>
            <pre><code>#include &lt;iostream&gt;
using namespace std;
int main() {
 int N;
 // Read the number of employees
 cout &lt;&lt; "Enter the number of employees: ";
 cin &gt;&gt; N;
 // Arrays to store employee data
 string names[N];
 double basicSalaries[N];
 // Read data for each employee
 for (int i = 0; i &lt; N; ++i) {
 cout &lt;&lt; "\nEnter details for employee " &lt;&lt; i + 1 &lt;&lt; ":" &lt;&lt; endl;
 cout &lt;&lt; "Name: ";
 cin &gt;&gt; names[i];
 cout &lt;&lt; "Basic Salary: ";
 cin &gt;&gt; basicSalaries[i];
 }
 // Calculate and display net salary for each employee
 cout &lt;&lt; "\nNet Salaries:\n";
 for (int i = 0; i &lt; N; ++i) {
 double DA = 0.52 * basicSalaries[i];
 double grossSalary = basicSalaries[i] + DA;
 double incomeTax = 0.30 * grossSalary;
 double netSalary = grossSalary - incomeTax;
 cout &lt;&lt; "Employee: " &lt;&lt; names[i] &lt;&lt;"\n\nNet Salary: " &lt;&lt; netSalary &lt;&lt;"\n\n**"&lt;&lt;
endl;
 }
 return 0;
}</code></pre>
        </div>
        
        <!-- Example 6 -->
        <div class="code-container">
            <div class="example-title">6. Basic Input/Output Example</div>
            <button class="copy-btn" onclick="copyCode(this)">Copy</button>
            <pre><code>#include &lt;iostream&gt;
#include &lt;string&gt;
using namespace std;
int main() {
 // Variable to store input
 int age;
 string name;
 // Output message to the console
 cout &lt;&lt; "Enter your name: ";
 // Input from the console
 getline(cin, name);
 // Output message to the console
 cout &lt;&lt; "Enter your age: ";
 // Input from the console
 cin &gt;&gt; age;
 // Output message to the console
 cout &lt;&lt; "Hello, " &lt;&lt; name &lt;&lt; "! You are " &lt;&lt; age &lt;&lt; " years old." &lt;&lt; endl;
 return 0;
}</code></pre>
        </div>
        
        <!-- Example 7 -->
        <div class="code-container">
            <div class="example-title">7. Variable Scope Demonstration</div>
            <button class="copy-btn" onclick="copyCode(this)">Copy</button>
            <pre><code>#include &lt;iostream&gt;
using namespace std;
// Global variable
int value = 10;
class MyClass {
public:
 // Static member
 static int value;
 // Member function
 void displayValue() {
 int value = 30; // Local variable
 cout &lt;&lt; "Local variable value: " &lt;&lt; value &lt;&lt; endl;
 cout &lt;&lt; "Static class member value: " &lt;&lt; MyClass::value &lt;&lt; endl;
 cout &lt;&lt; "Global variable value: " &lt;&lt; ::value &lt;&lt; endl;
 }
};
// Definition of the static member
int MyClass::value = 20;
int main() {
 MyClass obj;
 obj.displayValue();
 return 0;
}</code></pre>
        </div>
    </div>
  <div class="code-container">
            <div class="example-title">7. Variable Scope Demonstration</div>
            <button class="copy-btn" onclick="copyCode(this)">Copy</button>
            <pre><code>
#include <iostream>
using namespace std;
#define max 100
class Student
{ string stud_name;
 int marks;
 public:
 void getStudentInfo(int i)
 { cout<< endl << "Enter the student " << i << " details" << endl;
 cout<< "Name of the Student: ";
 cin>> stud_name;
cout<< "Marks secured: ";
 cin>> marks; }
 void displayStudentInfo()
 { cout << "Name of the Student : " << stud_name << endl;
 cout << "Marks secured : " << marks << endl; }
};
int main()
{ Student stud[max],*ptr;
 int class_size;
 ptr=stud;
 cout<< "Enter the number of students in the class ( < " << max << "): ";
 cin>> class_size;
 for( int i=1; i<=class_size; i++ )
 { (ptr+i)->getStudentInfo(i);
 }
 cout<< endl << "***** Entered student data *****" << endl;
 for( int i=1; i<=class_size; i++ )
 { cout << "Student " << i << endl;
 (ptr+i)->displayStudentInfo();
 }
 return 0;
}
</code></pre>
        </div>
    </div>

    <script>
        function copyCode(button) {
            const codeContainer = button.parentElement;
            const codeElement = codeContainer.querySelector('code');
            const textToCopy = codeElement.textContent;
            
            navigator.clipboard.writeText(textToCopy).then(() => {
                // Visual feedback
                button.textContent = 'Copied!';
                button.classList.add('copied');
                
                // Reset button after 2 seconds
                setTimeout(() => {
                    button.textContent = 'Copy';
                    button.classList.remove('copied');
                }, 2000);
            }).catch(err => {
                console.error('Failed to copy: ', err);
                alert('Failed to copy code. Please try again.');
            });
        }
    </script>
</body>
</html>
