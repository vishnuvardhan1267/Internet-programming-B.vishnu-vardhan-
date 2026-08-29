<!DOCTYPE html>
<html>
<head>
<title>MedCare Hospital Appointment System</title>

<style>
*{box-sizing:border-box;font-family:Arial}
body{margin:0;background:#eef7f8;color:#333}
header{background:#087f8c;color:white;text-align:center;padding:20px}
nav{background:#055c66;text-align:center;padding:12px}
nav button{
    padding:10px 15px;margin:4px;border:0;
    border-radius:5px;cursor:pointer
}
.container{width:90%;max-width:1100px;margin:20px auto}
section{
    background:white;padding:25px;margin-bottom:20px;
    border-radius:10px;box-shadow:0 2px 8px #ccc
}
.hidden{display:none}
input,select,textarea{
    width:100%;padding:11px;margin:8px 0 15px;
    border:1px solid #ccc;border-radius:5px
}
.btn{
    background:#087f8c;color:white;padding:10px 18px;
    border:0;border-radius:5px;cursor:pointer
}
.grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
    gap:15px
}
.box{
    border:1px solid #ddd;padding:18px;
    border-radius:8px
}
table{width:100%;border-collapse:collapse}
th,td{border:1px solid #ccc;padding:10px;text-align:center}
th{background:#087f8c;color:white}
footer{
    background:#055c66;color:white;text-align:center;padding:15px
}
.success{color:green}
.error{color:red}

@media(max-width:600px){
    nav button{width:45%}
    table{font-size:12px}
}
</style>
</head>

<body>

<header>
<h1>🏥 MedCare Hospital</h1>
<p>Online Doctor Appointment Booking System</p>
</header>

<nav>
<button onclick="show('home')">Home</button>
<button onclick="show('register')">Register</button>
<button onclick="show('login')">Login</button>
<button onclick="show('search')">Search</button>
<button onclick="show('doctors')">Doctors</button>
<button onclick="show('book')">Book Appointment</button>
<button onclick="show('checkin')">Check-in</button>
<button onclick="show('history')">My Appointments</button>
<button onclick="show('admin')">Admin</button>
</nav>

<div class="container">

<!-- HOME -->
<section id="home">
<h2>Welcome to MedCare</h2>
<p>
MedCare provides an easy way for patients to search hospitals,
find doctors according to specialty and location, and book
appointments at a convenient date and time.
</p>

<button class="btn" onclick="show('search')">
Find a Doctor
</button>
</section>


<!-- REGISTER -->
<section id="register" class="hidden">
<h2>Patient Registration</h2>

<input id="regName" placeholder="Full Name">
<input id="regEmail" placeholder="Email">
<input id="regPhone" placeholder="Phone Number">
<input id="regUser" placeholder="Username">
<input id="regPass" type="password" placeholder="Password">

<button class="btn" onclick="register()">Register</button>

<p id="registerMsg"></p>
</section>


<!-- LOGIN -->
<section id="login" class="hidden">
<h2>Patient Login</h2>

<input id="loginUser" placeholder="Username">
<input id="loginPass" type="password" placeholder="Password">

<button class="btn" onclick="login()">Login</button>

<p id="loginMsg"></p>
</section>


<!-- SEARCH -->
<section id="search" class="hidden">

<h2>Search Hospital / Doctor</h2>

<input id="location"
placeholder="Search by location"
onkeyup="searchDoctors()">

<select id="specialty" onchange="searchDoctors()">
<option value="All">All Specialties</option>
<option>Cardiology</option>
<option>Dermatology</option>
<option>Pediatrics</option>
<option>Orthopedics</option>
</select>

<div id="searchResult" class="grid"></div>

</section>


<!-- DOCTORS -->
<section id="doctors" class="hidden">

<h2>Available Doctors</h2>

<div class="grid">

<div class="box">
<h3>Dr. Arun Kumar</h3>
<p>Specialty: Cardiology</p>
<p>Hospital: MedCare Chennai</p>
<p>Location: Chennai</p>
<p>⭐ ⭐ ⭐ ⭐ ⭐</p>
<button class="btn"
onclick="selectDoctor('Dr. Arun Kumar')">
Book
</button>
</div>

<div class="box">
<h3>Dr. Priya Sharma</h3>
<p>Specialty: Dermatology</p>
<p>Hospital: Apollo Care</p>
<p>Location: Bangalore</p>
<p>⭐ ⭐ ⭐ ⭐</p>
<button class="btn"
onclick="selectDoctor('Dr. Priya Sharma')">
Book
</button>
</div>

<div class="box">
<h3>Dr. Meena Raj</h3>
<p>Specialty: Pediatrics</p>
<p>Hospital: City Children Hospital</p>
<p>Location: Chennai</p>
<p>⭐ ⭐ ⭐ ⭐ ⭐</p>
<button class="btn"
onclick="selectDoctor('Dr. Meena Raj')">
Book
</button>
</div>

<div class="box">
<h3>Dr. Ravi Kumar</h3>
<p>Specialty: Orthopedics</p>
<p>Hospital: Bone & Joint Hospital</p>
<p>Location: Coimbatore</p>
<p>⭐ ⭐ ⭐ ⭐</p>
<button class="btn"
onclick="selectDoctor('Dr. Ravi Kumar')">
Book
</button>
</div>

</div>
</section>


<!-- BOOK APPOINTMENT -->
<section id="book" class="hidden">

<h2>Appointment Booking</h2>

<label>Patient Name</label>
<input id="patientName" placeholder="Enter patient name">

<label>Hospital</label>
<select id="hospital">
<option>MedCare Chennai</option>
<option>Apollo Care</option>
<option>City Children Hospital</option>
<option>Bone & Joint Hospital</option>
</select>

<label>Doctor</label>
<select id="doctor">
<option>Dr. Arun Kumar - Cardiology</option>
<option>Dr. Priya Sharma - Dermatology</option>
<option>Dr. Meena Raj - Pediatrics</option>
<option>Dr. Ravi Kumar - Orthopedics</option>
</select>

<label>Appointment Date</label>
<input id="date" type="date">

<label>Appointment Time</label>
<select id="time">
<option>09:00 AM</option>
<option>10:00 AM</option>
<option>11:00 AM</option>
<option>12:00 PM</option>
<option>02:00 PM</option>
<option>03:00 PM</option>
<option>04:00 PM</option>
<option>05:00 PM</option>
</select>

<button class="btn" onclick="bookAppointment()">
Confirm Appointment
</button>

<p id="bookingMsg"></p>

</section>


<!-- CHECK IN -->
<section id="checkin" class="hidden">

<h2>Patient Check-in Form</h2>

<input id="appointmentId"
placeholder="Appointment ID">

<textarea id="symptoms"
placeholder="Enter symptoms"></textarea>

<input id="temperature"
placeholder="Temperature">

<textarea id="notes"
placeholder="Additional medical information"></textarea>

<button class="btn" onclick="checkIn()">
Submit Check-in
</button>

<p id="checkMsg"></p>

</section>


<!-- HISTORY -->
<section id="history" class="hidden">

<h2>Appointment History</h2>

<div id="historyData"></div>

</section>


<!-- FEEDBACK -->
<section id="feedback">

<h2>Doctor Feedback</h2>

<select id="feedbackDoctor">
<option>Dr. Arun Kumar</option>
<option>Dr. Priya Sharma</option>
<option>Dr. Meena Raj</option>
<option>Dr. Ravi Kumar</option>
</select>

<select id="rating">
<option>5 - Excellent</option>
<option>4 - Very Good</option>
<option>3 - Good</option>
<option>2 - Average</option>
<option>1 - Poor</option>
</select>

<textarea id="review"
placeholder="Write your review"></textarea>

<button class="btn" onclick="submitReview()">
Submit Review
</button>

</section>


<!-- ADMIN -->
<section id="admin" class="hidden">

<h2>Admin Login</h2>

<input id="adminUser" placeholder="Username">
<input id="adminPass" type="password" placeholder="Password">

<button class="btn" onclick="adminLogin()">
Login
</button>

<div id="adminPanel" class="hidden">

<h2>Appointment Management</h2>

<div id="adminAppointments"></div>

<h2>Appointment Statistics</h2>

<div id="statistics"></div>

<h2>Doctor Rating Details</h2>

<div id="ratings"></div>

</div>
</section>

</div>

<footer>
© 2026 MedCare Hospital | Online Appointment System
</footer>


<script>

let users=[];
let appointments=[];
let currentUser="";

/* Navigation */

function show(id){

document.querySelectorAll("section")
.forEach(s=>s.classList.add("hidden"));

document.getElementById(id)
.classList.remove("hidden");

if(id=="search")
searchDoctors();

if(id=="history")
displayHistory();
}


/* Registration */

function register(){

let user={
name:regName.value,
email:regEmail.value,
phone:regPhone.value,
username:regUser.value,
password:regPass.value
};

if(!user.name || !user.email ||
!user.username || !user.password){

registerMsg.innerHTML=
"<span class='error'>Fill all fields</span>";
return;
}

users.push(user);

registerMsg.innerHTML=
"<span class='success'>Registration successful!</span>";

}


/* Login */

function login(){

let user=users.find(u=>
u.username==loginUser.value &&
u.password==loginPass.value
);

if(user){

currentUser=user.username;

loginMsg.innerHTML=
"<span class='success'>Login successful!</span>";

}else{

loginMsg.innerHTML=
"<span class='error'>Invalid username or password</span>";

}
}


/* Search */

function searchDoctors(){

let loc=location.value.toLowerCase();
let spec=specialty.value;

let data=[
["Dr. Arun Kumar","Cardiology","MedCare Chennai","Chennai"],
["Dr. Priya Sharma","Dermatology","Apollo Care","Bangalore"],
["Dr. Meena Raj","Pediatrics","City Children Hospital","Chennai"],
["Dr. Ravi Kumar","Orthopedics","Bone & Joint Hospital","Coimbatore"]
];

let output="";

data.forEach(d=>{

if(d[3].toLowerCase().includes(loc) &&
(spec=="All" || spec==d[1])){

output+=`
<div class="box">
<h3>${d[0]}</h3>
<p>Specialty: ${d[1]}</p>
<p>Hospital: ${d[2]}</p>
<p>Location: ${d[3]}</p>

<button class="btn"
onclick="selectDoctor('${d[0]}')">
Book Appointment
</button>

<button class="btn"
onclick="map('${d[3]}')">
View Map
</button>
</div>`;
}

});

searchResult.innerHTML=
output || "<p>No doctors found.</p>";
}


/* Select Doctor */

function selectDoctor(name){

show("book");

for(let i=0;i<doctor.options.length;i++){

if(doctor.options[i].text.includes(name)){
doctor.selectedIndex=i;
}

}
}


/* Book Appointment */

function bookAppointment(){

if(!currentUser){

alert("Please login first");
show("login");
return;
}

if(!patientName.value || !date.value){

alert("Enter patient name and date");
return;
}

let id="APT"+
Math.floor(10000+Math.random()*90000);

appointments.push({

id:id,
user:currentUser,
patient:patientName.value,
hospital:hospital.value,
doctor:doctor.value,
date:date.value,
time:time.value,
status:"Confirmed"

});

bookingMsg.innerHTML=
"<span class='success'>Appointment booked! ID: "
+id+"</span>";

}


/* Check-in */

function checkIn(){

if(!appointmentId.value){

alert("Enter Appointment ID");
return;
}

checkMsg.innerHTML=
"<span class='success'>Check-in submitted successfully!</span>";

}


/* Appointment History */

function displayHistory(){

let data=appointments.filter(
a=>a.user==currentUser
);

if(data.length==0){

historyData.innerHTML=
"<p>No appointments found.</p>";
return;

}

let html=`
<table>
<tr>
<th>ID</th>
<th>Patient</th>
<th>Doctor</th>
<th>Date</th>
<th>Time</th>
<th>Status</th>
<th>Action</th>
</tr>`;

data.forEach(a=>{

html+=`
<tr>
<td>${a.id}</td>
<td>${a.patient}</td>
<td>${a.doctor}</td>
<td>${a.date}</td>
<td>${a.time}</td>
<td>${a.status}</td>
<td>
<button class="btn"
onclick="cancelAppointment('${a.id}')">
Cancel
</button>
</td>
</tr>`;

});

html+="</table>";

historyData.innerHTML=html;
}


/* Cancel Appointment */

function cancelAppointment(id){

let a=appointments.find(x=>x.id==id);

if(a){

a.status="Cancelled";

displayHistory();

}

}


/* Feedback */

function submitReview(){

if(!review.value){

alert("Write a review");
return;

}

alert("Thank you! Your feedback has been submitted.");

review.value="";

}


/* Google Map */

function map(location){

window.open(
"https://www.google.com/maps/search/?api=1&query="
+encodeURIComponent(location),
"_blank"
);

}


/* Admin Login */

function adminLogin(){

if(adminUser.value=="admin" &&
adminPass.value=="admin123"){

adminPanel.classList.remove("hidden");

showAdmin();

}else{

alert("Invalid Admin Login");

}

}


/* Admin Data */

function showAdmin(){

let html=`
<table>
<tr>
<th>Patient</th>
<th>Hospital</th>
<th>Doctor</th>
<th>Date</th>
<th>Time</th>
<th>Status</th>
</tr>`;

appointments.forEach(a=>{

html+=`
<tr>
<td>${a.patient}</td>
<td>${a.hospital}</td>
<td>${a.doctor}</td>
<td>${a.date}</td>
<td>${a.time}</td>
<td>${a.status}</td>
</tr>`;

});

html+="</table>";

adminAppointments.innerHTML=html;


/* Statistics */

statistics.innerHTML=`
<div class="box">
<h3>Total Appointments</h3>
<p>${appointments.length}</p>
</div>

<div class="box">
<h3>Confirmed</h3>
<p>${appointments.filter(a=>
a.status=="Confirmed").length}</p>
</div>

<div class="box">
<h3>Cancelled</h3>
<p>${appointments.filter(a=>
a.status=="Cancelled").length}</p>
</div>
`;


/* Ratings */

ratings.innerHTML=`
<p>Dr. Arun Kumar - ⭐⭐⭐⭐⭐</p>
<p>Dr. Priya Sharma - ⭐⭐⭐⭐</p>
<p>Dr. Meena Raj - ⭐⭐⭐⭐⭐</p>
<p>Dr. Ravi Kumar - ⭐⭐⭐⭐</p>
`;

}

</script>

</body>
</html>
