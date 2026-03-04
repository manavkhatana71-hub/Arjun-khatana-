
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ultimate Resume PNG Maker</title>

<script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">

<style>

body{
  margin:0;
  font-family:'Poppins',sans-serif;
  background:linear-gradient(135deg,#ff4da6,#ff0080);
  padding:20px;
}

h1{
  text-align:center;
  color:white;
}

.container{
  max-width:1200px;
  margin:auto;
  display:flex;
  gap:20px;
  margin-top:20px;
}

.form-box{
  width:35%;
  background:white;
  padding:20px;
  border-radius:15px;
  box-shadow:0 10px 30px rgba(0,0,0,0.2);
  height:fit-content;
}

.form-box input,
.form-box textarea{
  width:100%;
  padding:10px;
  margin-bottom:10px;
  border-radius:8px;
  border:1px solid #ddd;
  font-family:'Poppins';
}

.form-box button{
  width:100%;
  padding:12px;
  background:#ff0080;
  border:none;
  color:white;
  font-weight:600;
  border-radius:8px;
  cursor:pointer;
  margin-top:5px;
}

.resume{
  width:65%;
  background:white;
  border-radius:15px;
  overflow:hidden;
  box-shadow:0 20px 50px rgba(0,0,0,0.25);
  display:flex;
}

.left{
  width:35%;
  background:#111;
  color:white;
  padding:30px;
}

.right{
  width:65%;
  padding:30px;
}

.profile{
  text-align:center;
}

.profile-circle{
  width:120px;
  height:120px;
  border-radius:50%;
  overflow:hidden;
  margin:auto;
  margin-bottom:15px;
  border:4px solid #ff0080;
}

.profile-circle img{
  width:100%;
  height:100%;
  object-fit:cover;
}

.section{
  margin-bottom:25px;
}

.section h3{
  margin-bottom:10px;
  border-bottom:2px solid #ff0080;
  padding-bottom:5px;
}

.skill{
  margin-bottom:10px;
}

.skill-bar{
  height:8px;
  background:#ddd;
  border-radius:20px;
  overflow:hidden;
}

.skill-fill{
  height:100%;
  background:#ff0080;
}

</style>
</head>
<body>

<h1>Ultimate Resume PNG Generator</h1>

<div class="container">

<div class="form-box">
  <input type="text" id="name" placeholder="Full Name">
  <input type="text" id="role" placeholder="Job Role">
  <input type="text" id="email" placeholder="Email">
  <input type="text" id="phone" placeholder="Phone">
  <input type="file" id="photo" accept="image/*">
  <textarea id="about" placeholder="Professional Summary"></textarea>
  <textarea id="skills" placeholder="Skills (Example: HTML-90, CSS-80, JS-75)"></textarea>
  <textarea id="experience" placeholder="Work Experience"></textarea>
  <textarea id="education" placeholder="Education"></textarea>

  <button onclick="generateResume()">Generate Resume</button>
  <button onclick="downloadPNG()">Download PNG</button>
</div>

<div class="resume" id="resume">

<div class="left">

  <div class="profile">
    <div class="profile-circle">
      <img id="profilePreview" src="">
    </div>
    <h2 id="r_name">Your Name</h2>
    <p id="r_role">Your Role</p>
  </div>

  <div class="section">
    <h3>Contact</h3>
    <p id="r_contact">email@example.com<br>1234567890</p>
  </div>

  <div class="section">
    <h3>Skills</h3>
    <div id="r_skills"></div>
  </div>

</div>

<div class="right">

  <div class="section">
    <h3>Professional Summary</h3>
    <p id="r_about">Summary here...</p>
  </div>

  <div class="section">
    <h3>Experience</h3>
    <p id="r_experience">Experience here...</p>
  </div>

  <div class="section">
    <h3>Education</h3>
    <p id="r_education">Education here...</p>
  </div>

</div>

</div>

</div>

<script>

document.getElementById("photo").addEventListener("change", function(event){
  const reader = new FileReader();
  reader.onload = function(){
    document.getElementById("profilePreview").src = reader.result;
  }
  reader.readAsDataURL(event.target.files[0]);
});

function generateResume(){

  document.getElementById("r_name").innerText =
    document.getElementById("name").value;

  document.getElementById("r_role").innerText =
    document.getElementById("role").value;

  document.getElementById("r_contact").innerHTML =
    document.getElementById("email").value + "<br>" +
    document.getElementById("phone").value;

  document.getElementById("r_about").innerText =
    document.getElementById("about").value;

  document.getElementById("r_experience").innerText =
    document.getElementById("experience").value;

  document.getElementById("r_education").innerText =
    document.getElementById("education").value;

  // Skills
  const skillsInput = document.getElementById("skills").value.split(",");
  const skillsContainer = document.getElementById("r_skills");
  skillsContainer.innerHTML = "";

  skillsInput.forEach(skill => {
    const parts = skill.split("-");
    const name = parts[0] || "";
    const percent = parts[1] || "80";

    skillsContainer.innerHTML += `
      <div class="skill">
        <p>${name}</p>
        <div class="skill-bar">
          <div class="skill-fill" style="width:${percent}%"></div>
        </div>
      </div>
    `;
  });

}

function downloadPNG(){
  html2canvas(document.getElementById("resume"), {scale:2}).then(canvas => {
    let link = document.createElement("a");
    link.download = "ultimate_resume.png";
    link.href = canvas.toDataURL();
    link.click();
  });
}

</script>

</body>
</html>
