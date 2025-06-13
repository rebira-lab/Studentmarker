<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Smart Student Tracker</title>
  <style>
    :root {
      --bg: #f8f9fa;
      --text: #212529;
      --primary: #4361ee;
      --secondary: #3a0ca3;
      --accent: #7209b7;
      --success: #4cc9f0;
      --warning: #f72585;
      --card: #ffffff;
      --border-radius: 10px;
      --transition: 0.3s ease;
      --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      --shadow-hover: 0 6px 12px rgba(0, 0, 0, 0.15);
    }
    
    body.dark-mode {
      --bg: #121212;
      --text: #e0e0e0;
      --card: #1e1e1e;
      --shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
      --shadow-hover: 0 6px 12px rgba(0, 0, 0, 0.4);
    }
    
    body {
      margin: 0;
      padding: 20px;
      background: var(--bg);
      color: var(--text);
      font-family: 'Segoe UI', 'Roboto', sans-serif;
      line-height: 1.6;
      transition: background var(--transition), color var(--transition);
    }
    
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 15px;
    }
    
    .topbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 30px;
      padding-bottom: 15px;
      border-bottom: 2px solid var(--primary);
    }
    
    h1, h2, h3, h4 {
      color: var(--primary);
      margin-top: 0;
    }
    
    h1 {
      font-size: 2.2rem;
      font-weight: 700;
    }
    
    h2 {
      font-size: 1.8rem;
      margin-bottom: 20px;
      padding-bottom: 10px;
      border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    }
    
    h3 {
      font-size: 1.4rem;
      color: var(--accent);
    }
    
    .btn {
      background: var(--primary);
      color: white;
      border: none;
      padding: 12px 20px;
      border-radius: var(--border-radius);
      cursor: pointer;
      transition: all var(--transition);
      font-weight: 600;
      font-size: 1rem;
      box-shadow: var(--shadow);
      display: inline-flex;
      align-items: center;
      gap: 8px;
    }
    
    .btn:hover {
      background: var(--secondary);
      transform: translateY(-2px);
      box-shadow: var(--shadow-hover);
    }
    
    .btn:active {
      transform: translateY(0);
    }
    
    .btn-secondary {
      background: var(--accent);
    }
    
    .btn-export {
      background: var(--success);
    }
    
    .btn-danger {
      background: var(--warning);
    }
    
    .btn-group {
      display: flex;
      gap: 10px;
      margin: 20px 0;
      flex-wrap: wrap;
    }
    
    input,
    select,
    textarea {
      padding: 12px;
      margin: 8px 0 20px;
      border-radius: var(--border-radius);
      border: 1px solid #ddd;
      width: 100%;
      max-width: 400px;
      box-sizing: border-box;
      font-size: 1rem;
      transition: border-color var(--transition), box-shadow var(--transition);
    }
    
    input:focus,
    select:focus,
    textarea:focus {
      border-color: var(--primary);
      outline: none;
      box-shadow: 0 0 0 3px rgba(67, 97, 238, 0.2);
    }
    
    table {
      width: 100%;
      margin: 20px 0;
      border-collapse: collapse;
      background: var(--card);
      box-shadow: var(--shadow);
      transition: background var(--transition), color var(--transition);
    }
    
    th,
    td {
      padding: 12px 15px;
      text-align: left;
      border-bottom: 1px solid #ddd;
    }
    
    th {
      background-color: var(--primary);
      color: white;
      font-weight: 600;
    }
    
    tr:nth-child(even) {
      background-color: rgba(0, 0, 0, 0.02);
    }
    
    tr:hover {
      background-color: rgba(0, 0, 0, 0.05);
    }
    
    .hidden {
      display: none;
    }
    
    .student-img {
      width: 150px;
      height: 150px;
      object-fit: cover;
      border-radius: 50%;
      margin: 0 auto 20px;
      border: 4px solid var(--primary);
      transition: border-color var(--transition);
      display: block;
    }
    
    .student-profile {
      text-align: center;
      margin-bottom: 30px;
    }
    
    .top5-container {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
      gap: 20px;
      margin: 30px 0;
    }
    
    .top5-card {
      background: var(--card);
      padding: 20px;
      border-radius: var(--border-radius);
      box-shadow: var(--shadow);
      transition: all var(--transition);
      text-align: center;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    
    .top5-card:hover {
      transform: translateY(-5px);
      box-shadow: var(--shadow-hover);
    }
    
    .top5-card img {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      object-fit: cover;
      margin-bottom: 15px;
      border: 3px solid var(--accent);
    }
    
    .top5-card h4 {
      margin: 10px 0 5px;
    }
    
    .top5-card p {
      margin: 5px 0;
      font-size: 0.9rem;
    }
    
    .top5-card small {
      color: #666;
      font-size: 0.8rem;
    }
    
    .form-group {
      margin-bottom: 20px;
    }
    
    .form-group label {
      display: block;
      margin-bottom: 8px;
      font-weight: 500;
    }
    
    .subjects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 15px;
      margin: 20px 0;
    }
    
    .subject-input {
      margin-bottom: 0;
    }
    
    .result-card {
      background: var(--card);
      padding: 30px;
      border-radius: var(--border-radius);
      box-shadow: var(--shadow);
      margin: 30px 0;
    }
    
    .performance-summary {
      display: flex;
      justify-content: space-around;
      margin: 20px 0;
      flex-wrap: wrap;
      gap: 20px;
    }
    
    .performance-item {
      text-align: center;
      padding: 15px;
      background: rgba(67, 97, 238, 0.1);
      border-radius: var(--border-radius);
      min-width: 150px;
    }
    
    .performance-item h4 {
      margin-top: 0;
      color: var(--text);
    }
    
    .performance-item p {
      font-size: 1.5rem;
      font-weight: 700;
      margin: 10px 0 0;
      color: var(--primary);
    }
    
    @media (max-width: 768px) {
      .top5-container {
        grid-template-columns: 1fr;
      }
      
      .subjects-grid {
        grid-template-columns: 1fr;
      }
      
      .performance-summary {
        flex-direction: column;
      }
    }
    
    /* Dark mode specific styles */
    body.dark-mode th {
      background-color: var(--secondary);
    }
    
    body.dark-mode tr:nth-child(even) {
      background-color: rgba(255, 255, 255, 0.05);
    }
    
    body.dark-mode tr:hover {
      background-color: rgba(255, 255, 255, 0.1);
    }
    
    body.dark-mode .performance-item {
      background: rgba(67, 97, 238, 0.2);
    }
    
    body.dark-mode input,
    body.dark-mode select,
    body.dark-mode textarea {
      background-color: #2a2a2a;
      border-color: #444;
      color: var(--text);
    }
    
    /* Toggle switch style */
    .toggle-container {
      display: flex;
      align-items: center;
      gap: 10px;
    }
    
    .toggle-switch {
      position: relative;
      display: inline-block;
      width: 60px;
      height: 34px;
    }
    
    .toggle-switch input {
      opacity: 0;
      width: 0;
      height: 0;
    }
    
    .toggle-slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: #ccc;
      transition: .4s;
      border-radius: 34px;
    }
    
    .toggle-slider:before {
      position: absolute;
      content: "";
      height: 26px;
      width: 26px;
      left: 4px;
      bottom: 4px;
      background-color: white;
      transition: .4s;
      border-radius: 50%;
    }
    
    input:checked + .toggle-slider {
      background-color: var(--primary);
    }
    
    input:checked + .toggle-slider:before {
      transform: translateX(26px);
    }
    
    .toggle-label {
      font-weight: 500;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="topbar">
      <h1>📘 Smart Student Tracker</h1>
      <div class="toggle-container">
        <span class="toggle-label">Dark Mode</span>
        <label class="toggle-switch">
          <input type="checkbox" id="darkModeToggle" onclick="toggleDarkMode()">
          <span class="toggle-slider"></span>
        </label>
      </div>
    </div>

    <div class="btn-group">
      <button class="btn" onclick="requestAdminPassword()">
        <span>👨‍💼</span> Admin Panel
      </button>
      <button class="btn" onclick="showSection('studentView')">
        <span>👨‍🎓</span> Student Result
      </button>
    </div>

    <!-- Admin Panel -->
    <div id="adminPanel" class="hidden">
      <h2>Add/Edit Student</h2>
      <form id="studentForm">
        <div class="form-group">
          <label for="name">Full Name</label>
          <input type="text" id="name" placeholder="Enter full name" required />
        </div>
        
        <div class="form-group">
          <label for="grade">Grade</label>
          <input type="number" id="grade" placeholder="1-12" required min="1" max="12" />
        </div>
        
        <div class="form-group">
          <label for="section">Section</label>
          <input type="text" id="section" placeholder="A/B/C" required maxlength="1" />
        </div>
        
        <div class="form-group">
          <label for="roll">Roll Number</label>
          <input type="number" id="roll" placeholder="Roll no" required min="1" />
        </div>
        
        <div class="form-group">
          <label for="gender">Gender</label>
          <select id="gender" required>
            <option value="">Select gender</option>
            <option value="Male">Male</option>
            <option value="Female">Female</option>
            <option value="Other">Other</option>
          </select>
        </div>
        
        <div class="form-group">
          <label for="photo">Student Photo</label>
          <input type="file" id="photo" accept="image/*" />
        </div>
        
        <h3>Subject Marks</h3>
        <div id="subjectsInput" class="subjects-grid"></div>
        
        <div class="form-group">
          <label for="teacherComment">Teacher's Comment</label>
          <textarea id="teacherComment" placeholder="Enter any comments about the student" rows="3"></textarea>
        </div>
        
        <button class="btn" type="submit">
          <span>💾</span> Save Student
        </button>
      </form>

      <div class="btn-group">
        <div class="form-group">
          <label for="editCode">Student Code (Grade+Section+Roll)</label>
          <input type="text" id="editCode" placeholder="e.g. 7A12" />
        </div>
        <button class="btn" onclick="loadStudentForEdit()">
          <span>✏️</span> Edit
        </button>
        <button class="btn btn-danger" onclick="deleteStudent()">
          <span>🗑️</span> Delete
        </button>
      </div>

      <h3>All Students</h3>
      <button class="btn btn-secondary" onclick="showAllStudents()">
        <span>👥</span> Show All Students
      </button>

      <button class="btn btn-export" onclick="exportStudentsData()">
        <span>📤</span> Export Data
      </button>

      <div id="allStudentsTable" class="hidden"></div>
    </div>

    <!-- Student View -->
    <div id="studentView" class="hidden">
      <h2>Student Result Viewer</h2>
      <div class="form-group">
        <label for="searchCode">Enter Your Student Code (Grade+Section+Roll)</label>
        <input type="text" id="searchCode" placeholder="e.g. 7A12" />
      </div>
      <button class="btn" onclick="viewStudent()">
        <span>🔍</span> View Result
      </button>
      
      <div id="resultDisplay"></div>
      
      <h3>🏆 Top 5 Students</h3>
      <div id="top5Container" class="top5-container"></div>
    </div>
  </div>

  <script>
    // [Previous JavaScript code remains exactly the same]
    const adminPassword = "1234";
    const subjectList = [
      "Math",
      "English",
      "Physics",
      "Chemistry",
      "Biology",
      "Geography",
      "History",
      "Economics",
      "Area Study",
      "Afan Oromo",
      "Amharic",
      "ICT",
      "Citizenship",
      "Physical Education",
    ];

    const studentForm = document.getElementById("studentForm");
    const subjectsInput = document.getElementById("subjectsInput");

    subjectList.forEach((sub) => {
      const container = document.createElement("div");
      container.className = "form-group subject-input";
      
      const label = document.createElement("label");
      label.htmlFor = sub;
      label.textContent = sub;
      
      const inp = document.createElement("input");
      inp.type = "number";
      inp.id = sub;
      inp.placeholder = `0-100`;
      inp.min = 0;
      inp.max = 100;
      inp.required = true;
      
      container.appendChild(label);
      container.appendChild(inp);
      subjectsInput.appendChild(container);
    });

    function toggleDarkMode() {
      const toggle = document.getElementById("darkModeToggle");
      document.body.classList.toggle("dark-mode");
      localStorage.setItem("darkMode", document.body.classList.contains("dark-mode"));
    }

    // Check for saved dark mode preference
    if (localStorage.getItem("darkMode") === "true") {
      document.body.classList.add("dark-mode");
      document.getElementById("darkModeToggle").checked = true;
    }

    function requestAdminPassword() {
      const pw = prompt("Enter admin password:");
      if (pw === adminPassword) showSection("adminPanel");
      else alert("Wrong password!");
    }

    function showSection(id) {
      ["adminPanel", "studentView"].forEach((sec) =>
        document.getElementById(sec).classList.add("hidden")
      );
      clearDisplays();
      document.getElementById(id).classList.remove("hidden");
    }

    function clearDisplays() {
      document.getElementById("allStudentsTable").classList.add("hidden");
      document.getElementById("allStudentsTable").innerHTML = "";
      document.getElementById("resultDisplay").innerHTML = "";
      document.getElementById("top5Container").innerHTML = "";
    }

    function saveStudents(list) {
      localStorage.setItem("students", JSON.stringify(list));
    }

    function getStudents() {
      return JSON.parse(localStorage.getItem("students")) || [];
    }

    studentForm.onsubmit = (e) => {
      e.preventDefault();
      let list = getStudents();
      const g = document.getElementById("grade").value.trim();
      const s = document.getElementById("section").value.trim().toUpperCase();
      const r = document.getElementById("roll").value.trim();
      const codeVal = g + s + r;
      const idx = list.findIndex((st) => st.code === codeVal);
      const st = {
        code: codeVal,
        name: document.getElementById("name").value.trim(),
        grade: g,
        section: s,
        roll: r,
        gender: document.getElementById("gender").value.trim(),
        comment: document.getElementById("teacherComment").value.trim(),
        photo: "",
        subjects: {},
        total: 0,
      };
      subjectList.forEach((sub) => {
        const m = +document.getElementById(sub).value;
        st.subjects[sub] = m;
        st.total += m;
      });
      const file = document.getElementById("photo").files[0];
      if (file) {
        const rd = new FileReader();
        rd.onload = () => {
          st.photo = rd.result;
          if (idx > -1) list[idx] = st;
          else list.push(st);
          saveStudents(list);
          alert("Student data saved successfully!");
          studentForm.reset();
        };
        rd.readAsDataURL(file);
      } else {
        st.photo = idx > -1 ? list[idx].photo : "";
        if (idx > -1) list[idx] = st;
        else list.push(st);
        saveStudents(list);
        alert("Student data saved successfully!");
        studentForm.reset();
      }
    };

    function loadStudentForEdit() {
      const code = document.getElementById("editCode").value.trim();
      const st = getStudents().find((x) => x.code === code);
      if (!st) return alert("Student not found");
      document.getElementById("name").value = st.name;
      document.getElementById("grade").value = st.grade;
      document.getElementById("section").value = st.section;
      document.getElementById("roll").value = st.roll;
      document.getElementById("gender").value = st.gender;
      document.getElementById("teacherComment").value = st.comment || "";
      subjectList.forEach((sub) => {
        document.getElementById(sub).value = st.subjects[sub];
      });
      alert("Student data loaded for editing");
    }

    function deleteStudent() {
      const code = document.getElementById("editCode").value.trim();
      if (!code) return alert("Please enter a student code");
      
      if (confirm(`Are you sure you want to delete student ${code}?`)) {
        const list = getStudents().filter((s) => s.code !== code);
        saveStudents(list);
        alert(`Student ${code} has been deleted`);
        document.getElementById("editCode").value = "";
      }
    }

    function showAllStudents() {
      const list = getStudents();
      if (list.length === 0) {
        alert("No students found in the database");
        return;
      }
      
      let html = `
        <table>
          <thead>
            <tr>
              <th>Code</th>
              <th>Name</th>
              <th>Grade</th>
              <th>Section</th>
              <th>Roll</th>
              <th>Total</th>
              <th>Avg</th>
              <th>Comment</th>
            </tr>
          </thead>
          <tbody>
      `;
      
      list.forEach((s) => {
        html += `
          <tr>
            <td>${s.code}</td>
            <td>${s.name}</td>
            <td>${s.grade}</td>
            <td>${s.section}</td>
            <td>${s.roll}</td>
            <td>${s.total}</td>
            <td>${(s.total / subjectList.length).toFixed(2)}</td>
            <td>${s.comment || "-"}</td>
          </tr>
        `;
      });
      
      html += `</tbody></table>`;
      
      const tbl = document.getElementById("allStudentsTable");
      tbl.innerHTML = html;
      tbl.classList.remove("hidden");
    }

    function viewStudent() {
      const code = document.getElementById("searchCode").value.trim();
      if (!code) {
        alert("Please enter your student code");
        return;
      }
      
      const sorted = getStudents().sort((a, b) => b.total - a.total);
      const st = sorted.find((x) => x.code === code);
      const res = document.getElementById("resultDisplay");
      res.innerHTML = "";
      
      if (!st) {
        res.innerHTML = `
          <div class="result-card">
            <h3>Student Not Found</h3>
            <p>No student found with code: ${code}</p>
            <p>Please check your code and try again.</p>
          </div>
        `;
        return;
      }
      
      // Calculate rank
      const rank = sorted.findIndex(s => s.code === code) + 1;
      
      let html = `
        <div class="result-card">
          <div class="student-profile">
            ${st.photo ? `<img src="${st.photo}" class="student-img" alt="${st.name}">` : ""}
            <h2>${st.name}</h2>
            <p>Grade: ${st.grade} | Section: ${st.section} | Roll: ${st.roll}</p>
            <p>Gender: ${st.gender}</p>
          </div>
          
          <div class="performance-summary">
            <div class="performance-item">
              <h4>Total Marks</h4>
              <p>${st.total}</p>
            </div>
            <div class="performance-item">
              <h4>Average</h4>
              <p>${(st.total / subjectList.length).toFixed(2)}</p>
            </div>
            <div class="performance-item">
              <h4>Class Rank</h4>
              <p>${rank}</p>
            </div>
          </div>
          
          <h3>Subject-wise Performance</h3>
          <table>
            <thead>
              <tr>
                <th>Subject</th>
                <th>Mark</th>
                <th>Grade</th>
              </tr>
            </thead>
            <tbody>
      `;
      
      Object.entries(st.subjects).forEach(([sub, mark]) => {
        let grade = "";
        if (mark >= 90) grade = "A+";
        else if (mark >= 80) grade = "A";
        else if (mark >= 70) grade = "B";
        else if (mark >= 60) grade = "C";
        else if (mark >= 50) grade = "D";
        else grade = "F";
        
        html += `
          <tr>
            <td>${sub}</td>
            <td>${mark}</td>
            <td>${grade}</td>
          </tr>
        `;
      });
      
      html += `
            </tbody>
          </table>
          
          ${st.comment ? `
            <div class="teacher-comment" style="margin-top: 30px; padding: 15px; background: rgba(67, 97, 238, 0.1); border-radius: var(--border-radius);">
              <h4>Teacher's Comment</h4>
              <p>${st.comment}</p>
            </div>
          ` : ""}
        </div>
      `;
      
      res.innerHTML = html;
      
      // Show top 5
      const top5 = sorted.slice(0, 5);
      const top5Container = document.getElementById("top5Container");
      top5Container.innerHTML = "";
      
      top5.forEach((student, i) => {
        const card = document.createElement("div");
        card.className = "top5-card";
        card.innerHTML = `
          ${student.photo ? `<img src="${student.photo}" alt="${student.name}">` : "<div style='height:100px; display:flex; align-items:center; justify-content:center; font-size:3rem'>👤</div>"}
          <h4>${i+1}. ${student.name}</h4>
          <p>Total: ${student.total}</p>
          <p>Avg: ${(student.total / subjectList.length).toFixed(2)}</p>
          <small>${student.grade}${student.section}-${student.roll}</small>
        `;
        
        // Highlight the current student if they're in top 5
        if (student.code === code) {
          card.style.border = `2px solid ${document.body.classList.contains("dark-mode") ? "#4cc9f0" : "#f72585"}`;
          card.style.boxShadow = `0 0 0 3px ${document.body.classList.contains("dark-mode") ? "rgba(76, 201, 240, 0.3)" : "rgba(247, 37, 133, 0.3)"}`;
        }
        
        top5Container.appendChild(card);
      });
    }

    function exportStudentsData() {
      const students = getStudents();
      if (students.length === 0) {
        alert("No student data to export");
        return;
      }
      
      // Convert to CSV
      const headers = ["code", "name", "grade", "section", "roll", "gender", "comment", "total", ...subjectList];
      let csv = headers.join(",") + "\n";
      
      students.forEach(student => {
        let row = [
          student.code,
          `"${student.name}"`,
          student.grade,
          student.section,
          student.roll,
          student.gender,
          `"${student.comment || ""}"`,
          student.total
        ];
        
        subjectList.forEach(sub => {
          row.push(student.subjects[sub]);
        });
        
        csv += row.join(",") + "\n";
      });
      
      // Create download link
      const blob = new Blob([csv], { type: "text/csv" });
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href = url;
      a.download = `students_data_${new Date().toISOString().slice(0,10)}.csv`;
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);
    }
  </script>
</body>
</html>
