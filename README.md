<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Emergency Helpline App</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
    body{
        font-family: Arial, sans-serif;
        background:#f2f2f2;
        margin:0;
        padding:0;
        text-align:center;
    }
    h1{
        background:red;
        color:white;
        padding:15px;
        margin:0;
    }
    .container{
        padding:15px;
    }
    .card{
        background:white;
        margin:10px 0;
        padding:12px;
        border-radius:10px;
        box-shadow:0 0 5px rgba(0,0,0,0.2);
        display:flex;
        justify-content:space-between;
        align-items:center;
    }
    .btn{
        background:green;
        color:white;
        border:none;
        padding:8px 12px;
        border-radius:6px;
        cursor:pointer;
        font-size:14px;
    }
    .add-box{
        margin-top:20px;
        background:white;
        padding:15px;
        border-radius:10px;
    }
    input{
        padding:8px;
        margin:5px;
        width:40%;
    }
</style>
</head>

<body>

<h1>🚨 Emergency Helpline App</h1>

<div class="container" id="list">

<!-- Default Emergency Numbers -->
</div>

<div class="add-box">
    <h3>Add New Emergency Number</h3>
    <input type="text" id="name" placeholder="Name (e.g. Mom)">
    <input type="text" id="number" placeholder="Number (e.g. 9876543210)">
    <br>
    <button class="btn" onclick="addNumber()">Add</button>
</div>

<script>
let defaultNumbers = [
    {name:"Police", number:"112"},
    {name:"Ambulance", number:"108"},
    {name:"Fire Brigade", number:"101"},
    {name:"Women Helpline", number:"181"},
    {name:"Child Helpline", number:"1098"}
];

let saved = JSON.parse(localStorage.getItem("emergencyNumbers")) || [];
let numbers = defaultNumbers.concat(saved);

function render(){
    document.getElementById("list").innerHTML = "";
    numbers.forEach((item,index)=>{
        document.getElementById("list").innerHTML += `
        <div class="card">
            <div>
                <b>${item.name}</b><br>
                ${item.number}
            </div>
            <a href="tel:${item.number}">
                <button class="btn">📞 Call</button>
            </a>
        </div>`;
    });
}

function addNumber(){
    let name = document.getElementById("name").value;
    let number = document.getElementById("number").value;

    if(name=="" || number==""){
        alert("Please fill both fields");
        return;
    }

    let obj = {name:name, number:number};
    numbers.push(obj);
    saved.push(obj);

    localStorage.setItem("emergencyNumbers", JSON.stringify(saved));

    document.getElementById("name").value="";
    document.getElementById("number").value="";

    render();
}

render();
</script>

</body>
</html>
